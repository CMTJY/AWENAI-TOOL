# StartupPlanner Pro v2 通用多智能体团队

StartupPlanner Pro 是一套纯 Markdown/YAML、可被不同 Agent 工具共同读取的团队协议。Codex、Cursor、TRAE、CodeBuddy 或其他工具使用同一套主控协议、40 个已注册角色、能力注册表和工作流；项目本身不运行模型、不要求额外模型 API，也不提供平台专用 Agent 封装。

## 怎么使用

把本目录放在当前 AI 工具可读取的项目范围，在新对话中输入：

```text
请先读取 ./AGENTS.md，然后使用 StartupPlanner Pro 执行：
为一个面向跨境电商卖家的 AI 视频产品完成需求、技术方案和 MVP 开发计划。
```

如果宿主自动加载 `AGENTS.md`，可直接描述任务。宿主有原生子 Agent 时执行真实委派；没有时会明确降级为单 Agent 串行角色模拟，不会伪装成真实并行协作。

### 开放式请求会先确认方向

如果只输入：

```text
请使用 StartupPlanner Pro 写一份完整的跨境电商商业计划书。
```

团队不会自行选择美国、家居或某个具体品类。主控会先运行方向发现门，一次询问一个会改变方案的关键问题；用户没有既定方向时，主控提供 2–3 个方向及权衡，等待确认后才启动市场、竞品、产品、财务和 BP 工作流。

方向已经完整时不会重复提问，例如：

```text
为中国供应链出海、面向美国租房者的轻量收纳品牌，
使用 Amazon US + Shopify，编写投资人版商业计划书。
```

若希望团队直接代选，需明确授权范围并说明是否无需二次确认；“帮我推荐”“你看着办”默认只允许提出选项，不允许直接替用户定案。

## 目录结构

```text
StartupPlanner Pro/
├── README.md                         面向使用者的项目总览
├── AGENTS.md                         通用主控与协作协议
├── docs/
│   ├── README.md                     文档统一导航
│   ├── departments.md                部门与角色索引
│   ├── methodology/                  方法论
│   └── templates/                    交付物模板
└── agents/
    ├── config/
    │   ├── capabilities.yaml         角色、状态、能力和文件注册表
    │   └── routing-rules.yaml        意图与能力路由
    ├── templates/                    参考任务 DAG
    ├── core/
    │   └── orchestrator/
    │       ├── orchestrator.md
    │       └── skills/               主控独立技能副本
    ├── tech/
    │   ├── architect/ backend-dev/ frontend-dev/ mobile-dev/
    │   └── code-reviewer/ qa/ devops/
    ├── research/ strategy/ product/ marketing/
    ├── finance/ organization/ risk/
    └── _director/
```

没有 `.codex`、`.cursor`、`.trae` 或 `.codebuddy` 平台目录。

## 两种“独立”不要混淆

1. **角色定义通用**：每个 Agent 角色只在 `agents/` 中维护一次，所有宿主读取同一文件。
2. **角色技能自包含**：主控和技术角色将适用 Superpowers 技能物理复制到自己的 `skills/` 内，运行时不依赖仓库根目录的技能源。

因此，角色技能副本不是“为不同平台各复制一套”，而是 StartupPlanner Pro 内部的能力封装。每个技能目录都有索引、来源清单和许可证；源集合更新不会自动覆盖这些副本。

## 技术团队重构

技术部由七个职责互斥的角色组成：

- `tech-architect`：架构、稳定契约、技术任务图与文件边界；
- `tech-backend-dev`：服务端、API、数据与后端测试；
- `tech-frontend-dev`：Web 体验、可访问性、状态与前端测试；
- `tech-mobile-dev`：移动平台行为、权限、生命周期与真机验证；
- `tech-code-reviewer`：规格符合性和代码质量双门审；
- `tech-qa`：测试策略、集成、E2E、性能和验收；
- `tech-devops`：构建、CI/CD、可观测性、回滚与发布就绪。

标准软件链路：

```text
需求 → 架构/契约 → 测试策略
→ 无冲突文件范围内并行实现
→ 规格审查 → 代码质量审查
→ 集成与验收测试 → 发布就绪 → 最终质检
```

详见 [部门与角色索引](docs/departments.md)、[文档导航](docs/README.md) 和 [软件交付工作流](agents/templates/software-dev.yaml)。

## 协作不变量

- 先生成 Project Brief 和带依赖的 Task Packet，再委派。
- 代码任务必须声明 `file_scope`、验收标准、所需技能和验证要求。
- 只有无依赖且无共享可写状态的任务可并行。
- 执行者不得审核自己；QA 与代码审查员职责分离。
- 缺陷定向退回责任角色，不重跑无关任务。
- 只整合已通过审核且证据可追溯的产物。
- 未经用户授权，不部署、合并、推送、创建 PR 或丢弃工作。

## 维护入口

- 文档导航与放置规则：`docs/README.md`。
- 部门和角色总览：`docs/departments.md`，部门目录不再分散维护 README。
- 新增角色：创建角色 Markdown，再注册到 `agents/config/capabilities.yaml`。
- 新增路由：更新 `agents/config/routing-rules.yaml`。
- 新增固定协作顺序：更新 `agents/templates/`。
- 更新角色技能：从审核过的源基线复制，更新角色 `SKILL_INDEX.md` 和 `SOURCE_MANIFEST.yaml`，再运行完整验证。
- 不新增平台专用角色副本或外部模型运行时。
