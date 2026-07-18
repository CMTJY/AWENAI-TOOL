# StartupPlanner Pro v2 智能体协作规范

## 1. 目标

本规范定义团队如何拆解任务、选择角色、装载技能、隔离文件范围、审核产物、处理冲突和完成交付。它与根目录 `AGENTS.md`、能力注册表和工作流模板共同构成通用协议，不依赖某个 AI 工具的专有 Agent 格式。

## 2. 组织与职责

### 2.1 控制面

| 角色 | 负责 | 不负责 |
|---|---|---|
| Orchestrator | 状态、依赖调度、技能路由、委派、重试和失败控制 | 领域产物 |
| Task Planner | DAG、产物、文件边界、验收和失败策略 | 选择或执行角色 |
| Router | 能力匹配、约束过滤和备选角色 | 拆任务和执行 |
| Quality Reviewer | 非代码产物与最终交付的独立验收 | 补写原产物 |
| Aggregator | 整合已通过审核的产物 | 放行不合格产物 |

### 2.2 技术专业面

| 角色 | 责任边界 |
|---|---|
| `tech-architect` | 架构、契约、实现 DAG、文件与集成边界 |
| `tech-backend-dev` | 后端、API、数据、服务端测试和证据 |
| `tech-frontend-dev` | Web 界面、状态、可访问性、响应式和测试 |
| `tech-mobile-dev` | 移动平台实现、权限、生命周期和真机验证 |
| `tech-code-reviewer` | 规格符合性、正确性、安全、性能、兼容、可维护性与测试质量审查 |
| `tech-qa` | 测试策略、集成、E2E、性能、兼容与验收 |
| `tech-devops` | 可重复构建、CI/CD、可观测性、回滚与发布就绪 |

专业角色默认平级，不能自行调度其他角色。新增任务、返工和跨部门对齐均由 Orchestrator 记录和调度。

## 3. 角色本地技能

有本地技能的角色按以下顺序工作：

1. 读取自身角色文件；
2. 读取同目录 `skills/SKILL_INDEX.md`；
3. 只加载 Task Packet 的 `required_skills` 或触发条件明确匹配的技能；
4. 按 `SOURCE_MANIFEST.yaml` 记录的冻结副本工作，不读取 StartupPlanner Pro 外部源目录。

角色本地技能是 StartupPlanner Pro 的独立物理副本。仓库级 `Skills/superpowers` 仅是维护来源；同步必须人工审核、复制、更新清单并重新验证，禁止运行时动态继承。

### 3.1 开放式任务的方向门

新创业、BP、从 0 到 1 产品或重大工作流在建立 Project Brief 前必须执行重大歧义扫描。问题 / 品类、目标用户、产品形态或首要市场缺失时，由 Orchestrator 加载私有 `brainstorming` 技能，一次只询问一个关键问题，并在用户确认或明确授权团队代选后生成 `direction-brief`。

方向门没有通过时，领域任务不能进入 `ready`。完整明确的请求、机械修改和已经冻结范围的局部工作不重复提问。详细状态与防回归场景见 [方向发现与用户确认门](direction-discovery.md)。

## 4. Project Brief 与 Task Packet

并行角色使用同一份只读 Project Brief 快照。每个任务必须是可独立执行和验收的工作单元：

```yaml
task_packet:
  task_id: frontend-checkout
  objective: 实现结账页面的加载、成功和失败状态
  selected_agent_id: tech-frontend-dev
  selected_agent_file: tech/frontend-dev/frontend-dev.md
  depends_on: [architecture, test-strategy]
  required_artifacts: [product-requirements, technical-design, test-strategy]
  expected_artifact: {id: frontend-checkout-package, type: frontend-code}
  file_scope:
    allowed: [src/checkout/**, tests/checkout/**]
    prohibited: [server/**, migrations/**]
    shared: [package-lock.json]
  required_skills: [test-driven-development, verification-before-completion]
  acceptance_criteria:
    - 三种状态均有可重复验证
    - API 调用符合冻结契约
  verification_required: [targeted-tests, build]
  reviewer: tech-code-reviewer
  attempt: 1
```

禁止使用“全部材料”“所有文件”等无法追踪的输入或范围。共享可写文件不能被并行任务同时修改，应归入后续串行集成任务。

## 5. 依赖、并行与文件所有权

- 任务 B 消费 A 的产物时，B 必须在 `depends_on` 中声明 A。
- 所有依赖为 `passed` 或条件性 `skipped` 后，任务才能进入 `ready`。
- 并行要求同时满足：无数据依赖、无共享可写文件、无共享外部状态、可独立验收。
- 条件任务未触发时记为 `skipped`，不得伪造空产物。
- 每个产物只有一个权威生产者；多方意见通过 reconciliation 任务对齐。
- 架构师负责规划文件边界，Orchestrator 在派发前做冲突检查。

## 6. Artifact Envelope

角色之间不广播完整对话历史，只传 Project Brief、Task Packet 和必需上游产物：

```yaml
artifact:
  schema_version: "2.0"
  artifact_id: frontend-checkout-package
  artifact_type: frontend-code
  producer_agent_id: tech-frontend-dev
  task_id: frontend-checkout
  status: complete
  changed_files: []
  evidence: []
  assumptions: []
  verification:
    commands: []
    results: []
  risks: []
  review: {status: pending}
```

置信度和实现者自评不能代替审核与可复现验证。

## 7. 状态机与证据

通用任务：

```text
pending → ready → running → verifying → reviewing
                                      ├─ revision → running
                                      ├─ passed → completed
                                      └─ failed
```

代码任务：

```text
running → verifying
→ specification-compliance-review
→ code-quality-review
→ qa-validation
→ release-readiness
```

`verification` 必须记录实际命令或检查、结果、退出状态和无法执行项。状态事件至少包含时间、任务 ID、attempt、产物和原因。

## 8. 审核分层

### 8.1 通用产物审核

非代码关键产物由 `core-quality-reviewer` 逐条检查输入、验收标准、证据时效、假设分离、计算一致性和上游冲突。

### 8.2 代码 Gate 1：规格符合性

`tech-code-reviewer` 先确认：

- 需求和验收标准是否全部覆盖；
- API、数据、权限、错误和兼容契约是否一致；
- 是否超出 Task Packet 的文件和功能范围；
- 实现证据能否定位到具体变更。

Gate 1 不通过时停止，不进入代码质量审查。

### 8.3 代码 Gate 2：代码质量

审查正确性、安全、并发与事务、性能、资源释放、可观测性、迁移兼容、可维护性和测试有效性。缺陷必须给出位置、证据、影响、必改内容和复核方法。

### 8.4 QA 验收

`tech-qa` 消费已通过代码双门审的实现，执行集成、端到端、性能、兼容和业务验收。QA 不做代码风格放行，也不直接修复开发代码。

审核输出：

```yaml
review:
  reviewer:
  gate:
  status: passed | revision | failed
  criterion_results: []
  defects:
    - id:
      severity: critical | major | minor
      evidence:
      impact:
      required_change:
      recheck:
  residual_risks: []
```

任一必选标准失败或存在 critical 缺陷时不得通过。

## 9. 定向返工与失败

- `revision` 只退回责任执行者，并保留缺陷 ID 与 attempt。
- 修复后只重跑受影响的验证和审核，不重跑无关上游任务。
- `block_dependents` 保持下游阻塞；`fail_workflow` 表示关键交付失败。
- `continue` 只用于明确标记 optional 的非关键任务。
- 默认最多返工 2 次；达到上限必须公开缺口并请求决策，不能无限循环或降低标准。

## 10. 冲突处理

Aggregator 不直接裁决领域冲突。Orchestrator 创建 reconciliation 任务，产物至少包含：冲突、各方证据、影响、可逆性、采用决策、依据、责任人和未决项。

典型冲突包括产品范围与工期、API 契约与实现、增长 CAC 与财务模型、团队成本与现金流、风险控制与营销或产品方案。

## 11. 上下文、安全与授权

- 只向角色传递完成任务所需内容，避免广播隐私与无关历史。
- API key 只从宿主安全环境读取，不写入 Brief、产物或日志。
- 法律、监管、医疗等高风险结论必须标记需专业人员复核。
- merge、push、PR、部署、删除或丢弃工作必须处于用户授权范围内。
- 无原生委派能力时明确标记单 Agent 角色模拟，不虚报独立上下文或并行。

## 12. 可观测性与配置门禁

每次运行应记录 `run_id`、`workflow_id`、任务状态、attempt、角色文件、加载技能、开始与完成时间、验证证据、审核与返工原因、最终产物引用和失败原因。

角色、路由、技能或工作流变更后必须检查：

- 注册 ID、角色文件和 frontmatter 一致；
- 路由只引用 active 且存在的角色；
- DAG 无环，最终产物可达，产物生产者唯一；
- 执行者、代码审查员与 QA 边界独立；
- 本地技能索引、目录、来源清单、许可证和链接一致；
- 没有平台专用角色副本或运行时外部技能依赖。
