# 工作流模板库

存放可复用的多 agent 协作流程模板,主控可按用户任务自动匹配。

## 目录

- [software-dev.yaml](software-dev.yaml) — 软件开发工作流
- [marketing-campaign.yaml](marketing-campaign.yaml) — 营销活动工作流
- [research-project.yaml](research-project.yaml) — 综合调研工作流
- [bp-planning.yaml](bp-planning.yaml) — 商业计划书工作流
- [custom.md](custom.md) — 自定义工作流指南

## 格式规范

```yaml
workflow:
  id: {唯一标识}
  name: {可读名}
  description: {简介}

  stages:
    - stage: {阶段名}
      parallel: {true/false}
      depends_on: [前置 task_id 列表]
      tasks:
        - id: {task_id}
          agent: {agent_id}
          inputs: [...]
          outputs: [...]
          optional: {true/false}
          estimated_effort: {trivial/small/medium/large}
```

## 添加新工作流

1. 在本目录创建新 yaml 文件
2. 遵循上述格式
3. 在 README.md 中添加链接
4. 在 `config/routing-rules.yaml` 中引用(可选)