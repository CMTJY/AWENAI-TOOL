# 通用 AI Agent 团队规则库

<p align="center">
  <strong>通用多智能体协作平台</strong><br>
  <em>不绑定任何业务领域,可灵活扩展的软件/调研/营销/创业等多场景 AI Agent 团队</em>
</p>

---

## 目录简介

本目录是一个**通用的多智能体协作规则库**。它不再局限于创业规划场景,而是面向**任何类型的任务**(软件开发、市场调研、内容创作、商业规划等),通过统一的编排机制自动调度合适的 subagent 协作完成。

## 核心理念

把过去的"创业规划专属"团队,改造成:

| 维度 | 过去 | 现在 |
|------|------|------|
| 适用范围 | 仅创业规划 | **通用,任何领域** |
| 部门划分 | 写死的 6 个部门 | **可扩展的 N 个部门** |
| Agent 加入 | 改硬编码 | **加文件即可** |
| 工作流 | 写死的 3 阶段 | **可复用的工作流模板** |
| 任务路由 | 人工判断 | **基于能力的自动路由** |
| 调用方式 | 模拟 subagent | **可接入真实多 agent 框架** |

## 新架构总览

```
agents/
├── core/                          # 通用调度层(新增)
│   ├── orchestrator.md            # 通用主控:接收任务 → 调度 → 汇总
│   ├── router.md                  # 意图识别 + 能力路由
│   ├── task-planner.md            # 任务拆解
│   └── aggregator.md              # 多 subagent 结果汇总
│
├── config/                        # 配置中心(新增)
│   ├── capabilities.yaml          # 所有 agent 能力注册表
│   └── routing-rules.yaml         # 任务关键词 → agent 映射规则
│
├── templates/                     # 工作流模板(新增)
│   ├── software-dev.yaml          # 软件开发
│   ├── marketing-campaign.yaml    # 营销活动
│   ├── research-project.yaml      # 综合调研
│   ├── bp-planning.yaml           # 商业计划书
│   └── custom.md                  # 自定义工作流
│
├── tech/                          # 技术部(新增)
│   ├── architect.md               # 技术架构师
│   ├── backend-dev.md             # 后端开发
│   ├── frontend-dev.md            # 前端开发
│   ├── mobile-dev.md              # 移动端开发
│   ├── devops.md                  # DevOps
│   └── qa.md                      # 测试工程师
│
├── research/                      # 调研分析部(新增)
│   ├── analyst.md                 # 通用调研分析师
│   ├── market.md                  # 市场研究员
│   └── competitor.md              # 竞品分析师
│
├── strategy/                      # 战略部(原有,通用化)
├── product/                       # 产品部(原有,通用化)
├── marketing/                     # 营销部(原有)
├── finance/                       # 财务部(原有)
├── organization/                  # 组织部(原有)
├── risk/                          # 风险部(原有)
│
└── _director/                     # 兼容层
```

## 工作原理

### 用户视角(超简单)
```
用户:"帮我开发一个 XX 工具"

Orchestrator:
1. router 识别 → 这是软件类任务
2. 加载 software-dev 工作流
3. 并行调用 product-pm + tech-architect
4. 串行调 backend/frontend
5. aggregator 汇总输出完整方案
```

### 主控视角(自动编排)
```
收到任务 → router 路由 → task-planner 拆解 → 并行/串行调用 subagent → aggregator 汇总
```

## 如何使用

### 方式 1:直接与通用主控对话(推荐)
把 `core/orchestrator.md` 作为入口 agent。它会自动调用其他 agent 协作。

### 方式 2:选预设工作流
告诉主控:"按 software-dev 工作流跑"或"用 marketing-campaign 流程"

### 方式 3:自定义工作流
参见 `templates/custom.md`

### 方式 4:直接调单个 agent

## 各部门能力

| 部门 | Agent 数 | 核心能力 | 典型场景 |
|------|----------|----------|----------|
| **core** | 4 | 编排、路由、拆解、汇总 | 任何任务的入口 |
| **tech** | 6 | 架构、开发、部署、测试 | 软件开发、技术决策 |
| **research** | 3 | 调研、市场、竞品 | 信息收集、市场分析 |
| **strategy** | 3+ | 战略、商业模式、行业 | 战略规划、商业分析 |
| **product** | 3 | PRD、路线图、需求 | 产品规划、需求管理 |
| **marketing** | 9+ | 增长、内容、电商、私域 | 营销活动、获客、品牌 |
| **finance** | 2 | 财务建模、融资 | 财务规划、融资路演 |
| **organization** | 2 | 架构、招聘 | 组织设计、人才规划 |
| **risk** | 1 | 风险识别、合规 | 风险评估、合规审查 |

## 添加新 Agent(极简流程)

1. 在对应部门下创建 `xxx.md`,写好 frontmatter(加 `agent_id` 和 `capabilities`)
2. 在 `config/capabilities.yaml` 中注册
3. 在 `config/routing-rules.yaml` 中加路由规则(可选)

**就这么简单**,无需改其他任何文件。

## 接入真实多 Agent 框架

本规则库可以**零成本**接入以下框架:

| 框架 | 适配方式 |
|------|----------|
| **CrewAI** | 每份 `.md` 是一个 CrewAI Agent 配置 |
| **LangGraph** | 用 `templates/*.yaml` 定义 LangGraph 工作流 |
| **AutoGen** | `core/orchestrator.md` 作为 GroupChat Manager |
| **Claude Code Subagent** | 复制到 `.claude/agents/` 直接生效 |

## 与原 StartupPlanner 的关系

- 完全兼容:原 12 个核心 agent、所有 skill、所有模板都保留
- 渐进升级:旧的工作流(director-startup)继续可用
- 新能力:通用调度层 + 自动路由 + 可扩展工作流
- 建议:新项目用 `core/orchestrator`,老 BP 项目仍可用 `director-startup`

## 更新日志

| 日期 | 版本 | 更新内容 |
|------|------|----------|
| 2026-05-12 | v1.0.0 | 初始版本,创业规划专属 12 个核心 agent |
| 2026-06-23 | v1.1.0 | 产品经理升级:封装 54 个 PM skill |
| 2026-06-23 | v1.2.0 | 战略部升级:新增 OPC 战略师 |
| 2026-07-16 | **v2.0.0** | **通用化重塑**:新增 core/ 调度层、config/ 配置中心、tech/ + research/ 通用部门、templates/ 工作流库;支持自动任务路由 |

## 维护者

- **StartupPlanner Team**

---

**最后更新**: 2026-07-16 · v2.0.0 — 从"创业规划专属"升级为"通用 AI Agent 协作平台"