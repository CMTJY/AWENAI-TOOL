# 技术部 (Tech Department)

通用技术开发部门,负责所有软件类项目的实现。

## Agent 清单

| Agent ID | 文件 | 职能 | 使用场景 |
|----------|------|------|----------|
| tech-architect | [architect.md](architect.md) | 技术选型、系统架构、模块拆分 | 项目启动、技术决策、架构评审 |
| tech-backend-dev | [backend-dev.md](backend-dev.md) | 后端 API、数据库、服务端逻辑 | 接口开发、业务逻辑实现 |
| tech-frontend-dev | [frontend-dev.md](frontend-dev.md) | Web 前端、UI 实现、交互 | 页面开发、组件实现 |
| tech-mobile-dev | [mobile-dev.md](mobile-dev.md) | iOS / Android / 小程序 | 移动端应用开发 |
| tech-devops | [devops.md](devops.md) | CI/CD、部署、监控 | 部署上线、运维自动化 |
| tech-qa | [qa.md](qa.md) | 功能测试、自动化测试 | 质量保障、缺陷管理 |

## 典型协作模式

### 软件开发项目
```
需求分析(由 product-pm 主导)
    ↓
技术架构(tech-architect)
    ↓
并行实现:
├── tech-backend-dev
├── tech-frontend-dev
└── tech-mobile-dev
    ↓
测试(tech-qa)
    ↓
部署(tech-devops)
```

### 快速 MVP
```
tech-architect(轻量方案)
    ↓
tech-frontend-dev + tech-backend-dev(并行)
    ↓
tech-qa(冒烟测试)
    ↓
tech-devops(快速部署)
```