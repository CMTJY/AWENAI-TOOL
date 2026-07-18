# 工作流模板库 v2

这里存放供不同宿主 Agent 读取的通用参考任务 DAG。主控将模板转换为根目录 `AGENTS.md` 定义的 Task Packet，并使用当前宿主已有的原生委派能力执行。

## 预设流程

- [bp-planning.yaml](bp-planning.yaml)：创业验证与商业计划协作流
- [software-dev.yaml](software-dev.yaml)：软件交付协作流，包含代码双门审、QA 验收和发布就绪
- [marketing-campaign.yaml](marketing-campaign.yaml)：营销活动协作流
- [research-project.yaml](research-project.yaml)：多源调研协作流
- [custom.md](custom.md)：自定义工作流指南

## 关键约束

- 并行性只由 `depends_on` DAG、文件范围和共享状态共同决定。
- `depends_on` 引用任务 ID，`requires` 引用产物 ID或系统输入。
- 每个产物有且只有一个权威生产者。
- 每个关键任务有非执行者 reviewer 和可执行验收标准。
- 代码任务必须声明 `file_scope`、`required_skills` 和验证证据要求。
- 实现任务由 `tech-code-reviewer` 依次执行规格符合性与代码质量审核；`tech-qa` 负责测试验收，二者不得互换。
- 工作流必须无环，最终产物必须从系统输入可达。

修改模板后必须验证：角色与路由引用存在、DAG 无环、产物生产者唯一、执行者与审核者不同、所需技能存在于对应角色本地索引。
