# 自定义工作流

当预设工作流不满足需求时,你可以**自己定义**协作流程。

## 使用方式

### 方式 1:告诉 orchestrator 你的工作流
```
用户:"帮我做一个 X 任务,流程是:先 A,再同时 B 和 C,最后 D"

Orchestrator:
1. 解析工作流
2. 识别每步对应的 agent
3. 按依赖关系并行/串行执行
```

### 方式 2:写一个 YAML 工作流文件
参考 templates/ 下其他 yaml 的格式,新建一个:
```yaml
workflow:
  id: my-custom-flow
  name: 我的自定义流程
  stages:
    - stage: 步骤1
      tasks:
        - agent: {agent_id}
          outputs: [...]
    - stage: 步骤2
      depends_on: [步骤1 的 task_id]
      parallel: true
      tasks: [...]
```

保存为 `templates/my-flow.yaml`,下次直接告诉 orchestrator "按 my-flow 跑"。

### 方式 3:动态生成
告诉 orchestrator "现在帮我设计一个适合 XX 场景的工作流",它会调用 `core-task-planner` 临时生成。

## 简单规则

- `parallel: true` 表示该 stage 内所有 task 并行执行
- `depends_on` 列出前置 task_id
- `optional: true` 表示该 task 失败不影响整体
- `estimated_effort` 用于排期参考(trivial/small/medium/large)

## 工作流模板库

| 工作流 ID | 文件 | 适用场景 |
|----------|------|----------|
| software-dev | [software-dev.yaml](software-dev.yaml) | 软件开发 |
| marketing-campaign | [marketing-campaign.yaml](marketing-campaign.yaml) | 营销活动 |
| research-project | [research-project.yaml](research-project.yaml) | 综合调研 |
| bp-planning | [bp-planning.yaml](bp-planning.yaml) | 商业计划书 |