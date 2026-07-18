# 自定义工作流 v2

自定义流程必须遵循根目录 `AGENTS.md` 和现有 v2 工作流格式。

## 最小模板

```yaml
schema_version: "2.0"
workflow:
  id: my-workflow
  name: 我的工作流
  version: "2.0"
  goal: 可验证的最终目标
  system_inputs: [project-brief]
  final_artifacts: [final-artifact]
  tasks:
    - id: first-task
      objective: 生成第一个可验收产物
      agent: registered-agent-id
      depends_on: []
      requires: [project-brief]
      produces: {id: first-artifact, type: report}
      acceptance_criteria: [至少一条可客观检查的标准]
      reviewer: core-quality-reviewer
      retry: {max_attempts: 2}
      failure_policy: block_dependents
```

不要手工声明一个阶段“并行”。运行时会根据 `depends_on` 自动找出所有 ready 任务并并行执行。

保存后检查依赖无环、产物唯一、审核独立，并用任一支持原生 Subagent 的宿主工具执行一次任务走查。
