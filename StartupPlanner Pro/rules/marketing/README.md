# Marketing 营销部

本目录用于存放 StartupPlanner 营销相关的智能体规则和配置。

## 目录结构

```
marketing/
├── README.md           # 本文件 - 营销部结构说明
├── Product-EVENT/      # 产品增长与活动策划
├── media-content/      # 媒体内容运营
├── fans-domain/        # 私域流量运营
└── product-sales/      # 产品销售与电商运营
```

## 各分类说明

### 1. Product-EVENT/
**产品增长与活动策划**

用于存放以下智能体：
- 增长黑客 (Growth Hacker)
- 活动策划师 (Event Planner)
- 产品推广策略师
- 用户增长专家

### 2. media-content/
**媒体内容运营**

用于存放以下智能体：
- 内容创作者 (Content Creator)
- 抖音策略师 (Douyin Strategist)
- 小红书运营 (Xiaohongshu Operator)
- 社交媒体运营师
- 短视频策划师

### 3. fans-domain/
**私域流量运营**

用于存放以下智能体：
- 私域运营师 (Private Domain Operator)
- 社群运营专家
- 用户留存策略师
- 会员运营师

### 4. product-sales/
**产品销售与电商运营**

用于存放以下智能体：
- 电商运营师 (E-commerce Operator)
- 跨境电商师 (Cross-border E-commerce)
- 直播教练 (Live Streaming Coach)
- 带货主播助手
- 电商数据分析师

## 迁移计划

### 阶段一：目录初始化（已完成）
- [x] 创建营销部主目录
- [x] 创建四大分类子目录
- [x] 编写 README.md 说明文档

### 阶段二：MarketMaster 智能体迁移（待进行）
- [ ] 从 MarketMaster 导出增长黑客智能体配置
- [ ] 从 MarketMaster 导出活动策划师智能体配置
- [ ] 从 MarketMaster 导出内容创作者智能体配置
- [ ] 从 MarketMaster 导出抖音策略师智能体配置
- [ ] 从 MarketMaster 导出小红书运营智能体配置
- [ ] 从 MarketMaster 导出私域运营师智能体配置
- [ ] 从 MarketMaster 导出电商运营师智能体配置
- [ ] 从 MarketMaster 导出跨境电商师智能体配置
- [ ] 从 MarketMaster 导出直播教练智能体配置

### 阶段三：配置规范化（待进行）
- [ ] 统一智能体配置文件格式
- [ ] 建立智能体命名规范
- [ ] 编写智能体使用指南
- [ ] 建立智能体能力矩阵文档

## 使用说明

1. 每个智能体应在对应分类目录下创建独立子目录
2. 智能体目录命名建议采用 `kebab-case` 格式
3. 每个智能体目录内应包含：
   - `agent.yaml` - 智能体配置文件
   - `system-prompt.md` - 系统提示词
   - `README.md` - 智能体说明文档（可选）

## 注意事项

- 当前目录结构为 MarketMaster 迁移准备阶段
- 请勿直接在此目录下创建非分类相关的文件
- 新增智能体分类需经过团队评审

---

**最后更新**: 2026-05-12
**维护者**: StartupPlanner Team
