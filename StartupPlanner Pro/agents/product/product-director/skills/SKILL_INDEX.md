# Skill Index — 产品开发全流程统筹专家

## 1. Skill 清单

| # | Skill 名称 | 文件夹 | 类型 | 核心用途 | 对应阶段 | 适用类型 |
|---|-----------|--------|------|---------|---------|---------|
| 1 | mvp-development-playbook | `mvp-development-playbook/` | Workflow | 软件MVP全流程开发（7步） | MVP | 纯软件 |
| 2 | launch-readiness-playbook | `launch-readiness-playbook/` | Workflow | 软件发布阶段 readiness（6步） | 发布 | 纯软件 |
| 3 | scale-moat-playbook | `scale-moat-playbook/` | Workflow | 软件规模化+护城河构建（6步） | 规模化 | 纯软件 |
| 4 | hardware-mvp-scope-lock | `hardware-mvp-scope-lock/` | Component | 硬件MVP范围锁定 | MVP | 硬件/IoT |
| 5 | hardware-evidence-metrics | `hardware-evidence-metrics/` | Component | 硬件度量框架+PMF验证 | MVP | 硬件/IoT |
| 6 | hardware-compliance-workflow | `hardware-compliance-workflow/` | Component | 硬件合规持续工作流 | 发布 | 硬件/IoT |

## 2. Skill 详细描述

### mvp-development-playbook（纯软件）
- **描述**: Guide software MVP development through 7 steps: architecture lock, scope freeze, metrics framework, build execution, security review, feedback loop, and evidence-based iteration.
- **触发条件**: Invoke when building a software MVP to validate PMF with minimal waste and avoid false positives.
- **输出**: CLAUDE.md + Scope Contract + Metrics Framework + Build Plan
- **预计时间**: 2-3 weeks (full MVP stage)
- **来源**: 第四章 MVP阶段方法论

### launch-readiness-playbook（纯软件）
- **描述**: Guide software product launch through 6 steps: repay tech debt, build repeatable growth, embed security compliance, audit founder workload, establish PM processes, and resist premature scaling.
- **触发条件**: Invoke when transitioning from MVP to launch stage to ensure the business is ready for sustainable growth.
- **输出**: Tech Debt Plan + Growth Channels + Compliance Workflow + PM OS
- **预计时间**: 6-10 weeks
- **来源**: 第五章 发布阶段方法论

### scale-moat-playbook（纯软件）
- **描述**: Guide software product scaling through 6 steps: delegate operations, upgrade to enterprise infrastructure, build GTM function, encode domain knowledge into AI, compound user data into flywheel, and create workflow lock-in.
- **触发条件**: Invoke when entering scale stage to build durable competitive advantages.
- **输出**: Delegation Matrix + Enterprise Infra + GTM Engine + Moat Roadmap
- **预计时间**: 3-6 months
- **来源**: 第六章 规模化阶段方法论

### hardware-mvp-scope-lock（硬件/IoT）
- **描述**: Lock MVP scope for hardware/IoT products by defining must-build, must-not-build, and evidence thresholds for scope expansion.
- **触发条件**: Invoke when planning a hardware MVP to prevent BOM creep, certification bloat, and feature sprawl before production.
- **输出**: MVP Scope Contract（范围合同）
- **预计时间**: 60-90 min
- **来源**: 第四章 Step 2 方法论迁移

### hardware-evidence-metrics（硬件/IoT）
- **描述**: Build pre-launch measurement framework and PMF validation metrics for hardware/IoT products.
- **触发条件**: Invoke before any hardware goes to production to define activation, retention, and false-positive detectors.
- **输出**: Metrics Framework + False-Positive Detector
- **预计时间**: 75-90 min
- **来源**: 第四章 Step 3,7 方法论迁移

### hardware-compliance-workflow（硬件/IoT）
- **描述**: Build continuous compliance workflow for hardware certifications (3C, FCC, CE, RoHS, etc.).
- **触发条件**: Invoke when preparing for market entry or when adding new markets/regions to ensure certification is embedded in development cycles, not treated as a one-time project.
- **输出**: Compliance Baseline + DFC Checklist + Change-Control Workflow
- **预计时间**: 85-105 min
- **来源**: 第五章 Step 3 方法论迁移

## 3. 任务 → Skill 路由速查

### 纯软件场景
| 用户说的话 | 匹配 Skill | 理由 |
|-----------|-----------|------|
| "MVP 怎么开发" / "CLAUDE.md" / "锁范围" / "埋度量" | mvp-development-playbook | 软件MVP全流程 |
| "发布阶段" / "技术债" / "增长渠道" / " founder 负载" / "防扩张" | launch-readiness-playbook | 软件发布阶段 |
| "规模化" / "护城河" / "GTM" / "数据飞轮" / "工作流锁定" | scale-moat-playbook | 软件规模化 |

### 硬件/IoT 场景
| 用户说的话 | 匹配 Skill | 理由 |
|-----------|-----------|------|
| "硬件 MVP" / "BOM" / "功能砍掉" / "模具" | hardware-mvp-scope-lock | 硬件范围控制 |
| "硬件 PMF" / "留存" / "抽屉测试" / "激活" | hardware-evidence-metrics | 硬件度量框架 |
| "3C 认证" / "FCC" / "CE" / "硬件合规" | hardware-compliance-workflow | 硬件合规认证 |

### 通用场景
| 用户说的话 | 匹配 Skill | 理由 |
|-----------|-----------|------|
| "统筹产品开发" / "全流程" / "从 0 到 1" | 多个组合 | 按阶段组合 |

## 4. Skill 组合建议

### 纯软件产品路径
| 场景 | 主 Skill | 辅助 Skill | 执行顺序 |
|------|---------|-----------|---------|
| 从零启动软件 MVP | mvp-development-playbook | — | 按7步执行 |
| MVP 后准备发布 | launch-readiness-playbook | mvp-development-playbook (回顾) | 先回顾 → 后发布准备 |
| 发布后进规模化 | scale-moat-playbook | launch-readiness-playbook (回顾) | 先回顾 → 后规模化 |
| 软件全流程健康检查 | 全部3个纯软件skill | — | 按阶段顺序 |

### 硬件/IoT 产品路径
| 场景 | 主 Skill | 辅助 Skill | 执行顺序 |
|------|---------|-----------|---------|
| 硬件 MVP 范围定义 | hardware-mvp-scope-lock | hardware-evidence-metrics | 先范围 → 后度量 |
| 硬件准备量产 | hardware-compliance-workflow | hardware-evidence-metrics | 并行执行 |
| 硬件全流程检查 | 全部3个硬件skill | — | 按阶段顺序 |

### 混合场景（软件+硬件）
| 场景 | 主 Skill | 辅助 Skill | 执行顺序 |
|------|---------|-----------|---------|
| 物联网产品 MVP | mvp-development-playbook (软件) | hardware-mvp-scope-lock (硬件) | 并行 |
| 物联网产品发布 | launch-readiness-playbook (软件) | hardware-compliance-workflow (硬件) | 并行 |

## 5. 文件结构

```
product-director/
├── product-director.md              ← 智能体角色定义
└── skills/
    ├── SKILL_INDEX.md               ← 本文件
    ├── mvp-development-playbook/    ← Skill 1: 纯软件MVP
    │   └── SKILL.md
    ├── launch-readiness-playbook/   ← Skill 2: 纯软件发布
    │   └── SKILL.md
    ├── scale-moat-playbook/         ← Skill 3: 纯软件规模化
    │   └── SKILL.md
    ├── hardware-mvp-scope-lock/     ← Skill 4: 硬件MVP范围
    │   └── SKILL.md
    ├── hardware-evidence-metrics/   ← Skill 5: 硬件度量
    │   └── SKILL.md
    └── hardware-compliance-workflow/← Skill 6: 硬件合规
        └── SKILL.md
```

## 6. 使用规则

1. **匹配时只读取 SKILL.md 的 frontmatter（name + description）**，不扫描全文
2. **执行时必须用 Read 工具读取完整 SKILL.md**，按 Application 章节执行
3. **每个 skill 的 description 已包含触发条件**，用于自动匹配决策
4. **复杂任务可组合多个 skill**，按组合建议的顺序执行
5. **纯软件 vs 硬件/IoT 区分**：根据用户提到的产品类型（软件/硬件/物联网）优先匹配对应类别的 skill
