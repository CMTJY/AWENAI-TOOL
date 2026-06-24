# 会话案例：具身智能.md → 飞书《具身智能》

本文档记录一次完整操作，供 skill 使用者参考。

## 背景

- 本地文件：`具身智能.md`（具身智能科普 + 产业 + 低成本入局指南）
- 目标：飞书个人文档库已有文档 **《具身智能》**（此前几乎为空）
- 用户诉求演变：
  1. 优化标题等级与编号 → 追加到飞书
  2. 本地改为 `1.` / `1.1.` / `1.1.1.` 手写编号，**不同步飞书**
  3. **覆盖**飞书全文，编号改用 **飞书文档自带自动编号**

## 阶段一：排版优化 + 追加

1. 将混用的 `一、` + `1.1` + `方向一` 统一为中文公文编号 `一、（一）（二）`
2. 定位文档：

```bash
lark-cli wiki +node-list --as user --space-id my_library --page-all --format pretty
# 命中：title=具身智能, obj_token=JbNOdPALvo6WAnxvEawcnn62nfh
```

3. 以 Markdown `append` 写入（当时尚未使用原生编号）

## 阶段二：仅本地数字编号

用户要求本地 Markdown 使用：

```markdown
## 1. 基础认知
### 1.1. 什么是具身智能
```

**未**调用 `docs +update`。

## 阶段三：覆盖 + 飞书原生编号

1. 将 Markdown 转为 DocxXML，标题去掉手写数字，添加：

```xml
<h2 seq="auto" seq-level="auto">基础认知</h2>
<h3 seq="auto" seq-level="auto">什么是具身智能</h3>
```

2. 覆盖写入：

```bash
lark-cli docs +update --api-version v2 --as user \
  --doc JbNOdPALvo6WAnxvEawcnn62nfh \
  --command overwrite \
  --content @具身智能-feishu.xml
```

3. 验证：`docs +fetch --detail full` 中所有 h1/h2/h3 均含 `seq="auto" seq-level="auto"`。

## 最终文档结构（语义标题，编号由飞书渲染）

| 层级 | 示例标题 |
|------|---------|
| title | 具身智能 |
| h1 | 具身智能知识概览 |
| h2 | 基础认知、技术架构、…、低成本入局指南（5 万以内） |
| h3 | 什么是具身智能、感知层、…、推荐组合 |

## 产出链接

https://ideamake.feishu.cn/docx/JbNOdPALvo6WAnxvEawcnn62nfh
