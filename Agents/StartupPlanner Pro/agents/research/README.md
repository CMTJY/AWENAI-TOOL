# 调研分析部 (Research Department)

通用调研与分析部门,负责所有领域的信息收集、市场研究、竞品分析。

## Agent 清单

| Agent ID | 文件 | 职能 | 使用场景 |
|----------|------|------|----------|
| research-analyst | [analyst.md](analyst.md) | 通用调研、信息收集、报告撰写 | 任何领域的资料整理 |
| research-market | [market.md](market.md) | 市场调研、用户洞察、TAM/SAM/SOM | 市场规模评估、用户画像 |
| research-competitor | [competitor.md](competitor.md) | 竞品分析、对比矩阵、SWOT | 竞品对比、差异化定位 |

## 典型协作模式

### 完整调研任务
```
research-analyst(信息收集)
    ↓
并行:
├── research-market(市场维度)
└── research-competitor(竞品维度)
    ↓
research-analyst(综合报告)
```

### 进入新市场
```
research-market(市场扫描)
    ↓
research-competitor(主要玩家分析)
    ↓
research-analyst(综合机会评估)
```