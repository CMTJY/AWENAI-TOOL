---
name: lark-doc-local-publish
version: 1.0.0
description: "将本地 Markdown 文章优化排版后发布到飞书云文档（个人文档库或指定 docx）：支持 append/overwrite、飞书原生标题自动编号（seq/seq-level）。当用户要把本地 .md 同步/覆盖/追加到飞书文档、优化标题层级编号、或发布到「我的文档库」时使用。"
metadata:
  requires:
    bins: ["lark-cli"]
  cliHelp: "lark-cli docs +update --api-version v2 --help; lark-cli wiki +node-list --help"
---

# 本地 Markdown 发布到飞书文档

> **前置条件（MUST READ）：**
> 1. [`../lark-shared/SKILL.md`](../lark-shared/SKILL.md) — 认证、`--as user`
> 2. [`../lark-doc/SKILL.md`](../lark-doc/SKILL.md) — `docs +fetch` / `+update` / v2 API
> 3. [`../lark-wiki/SKILL.md`](../lark-wiki/SKILL.md) — 个人文档库 = `my_library`
> 4. 写入前读 [`../lark-doc/references/lark-doc-xml.md`](../lark-doc/references/lark-doc-xml.md)

## 典型场景（本 skill 来源）

用户有一篇本地 `.md` 长文，希望：

1. **优化标题层级与编号**（先本地改，用户确认后再同步）
2. **写入飞书个人文档库**中已有同名文档（如《具身智能》）
3. **使用飞书原生自动编号**（1. / 1.1. / 1.1.1.），而非标题文字里手写数字

## 快速决策

| 用户意图 | 操作 | 格式 |
|---------|------|------|
| 仅改本地，不同步飞书 | 只编辑 `.md` | Markdown |
| 追加到文档末尾 | `docs +update --command append` | 用户指定 Markdown 或 XML |
| **全文替换**（覆盖旧内容） | `docs +update --command overwrite` | **需飞书原生编号时用 XML** |
| 飞书原生标题编号 | 标题加 `seq="auto" seq-level="auto"`，**标题文字不含** `1.` / `1.1.` | DocxXML |
| 定位「我的文档库」文档 | `wiki +node-list --space-id my_library` | — |

**默认身份：** 个人文档库与 docx 写入一律 `--as user`。

## 工作流

### 1. 认证

```bash
lark-cli auth status
# user 不可用时：
lark-cli auth login --domain docs,drive --no-wait --json
# 展示 verification_url + QR（lark-cli auth qrcode "<url>" -o ./auth-qr.png）
# 用户授权后：
lark-cli auth login --device-code "<device_code>"
```

### 2. 定位目标文档

**个人文档库（my_library）：**

```bash
lark-cli wiki +node-list --as user --space-id my_library --page-all --format pretty
```

按 `title` 匹配；记录 `obj_token`（docx 时即 `--doc` token）与 `url`。

已知 token 时可直接：

```bash
lark-cli docs +fetch --api-version v2 --as user --doc "<obj_token>" --scope outline --max-depth 2
```

### 3. 本地 Markdown 优化（可选）

在同步前于本地完成结构与措辞调整。编号策略三选一，**与用户确认**：

| 策略 | 本地 Markdown 写法 | 同步到飞书 |
|------|-------------------|-----------|
| A. 中文层级 | `## 一、…` / `### （一）…` | 需转 XML + `seq="auto"` 或保留纯文字 |
| B. 手写数字 | `## 1. …` / `### 1.1. …` | 同步前**去掉**标题内数字，改用语义标题 + XML 自动编号 |
| C. 飞书原生（推荐） | 本地可无编号，仅 `## 基础认知` | 转 XML，`seq="auto" seq-level="auto"` |

用户明确「不要同步飞书」时，**只改本地文件，停止于此**。

### 4. 转为 DocxXML（飞书原生编号）

**规则：**

- 文档名：`<title>具身智能</title>`（与文档库显示名一致）
- 各级标题：**不写** `1.`、`1.1.` 等前缀
- 启用自动编号：

```xml
<h1 seq="auto" seq-level="auto">具身智能知识概览</h1>
<h2 seq="auto" seq-level="auto">基础认知</h2>
<h3 seq="auto" seq-level="auto">什么是具身智能</h3>
```

- 有序列表：`<ol><li seq="auto">第一项</li><li seq="auto">第二项</li></ol>`
- 引用 → `<blockquote><p>…</p></blockquote>`；表格/列表/加粗按 [`lark-doc-xml.md`](../lark-doc/references/lark-doc-xml.md)
- 文本中的 `&` `<` 按 XML 规则转义

将 XML 写入临时文件，用 `@path` 传参，避免 shell 转义问题。

### 5. 写入飞书

**覆盖全文（常用）：**

```bash
cd /path/to/article/dir
lark-cli docs +update --api-version v2 --as user \
  --doc "<obj_token>" \
  --command overwrite \
  --content @article-feishu.xml
```

**追加到末尾：**

```bash
lark-cli docs +update --api-version v2 --as user \
  --doc "<obj_token>" \
  --command append \
  --doc-format markdown \
  --content @article-append.md
```

> `overwrite` 会清空原文再写入，可能丢失旧评论/嵌入资源；执行前确认用户意图。

### 6. 验证

```bash
# 目录结构
lark-cli docs +fetch --api-version v2 --as user --doc "<token>" \
  --scope outline --max-depth 3 --format pretty

# 确认 seq 属性已保留（编号由飞书前端渲染，outline/Markdown 导出可能不显示数字）
lark-cli docs +fetch --api-version v2 --as user --doc "<token>" --detail full \
  | rg 'seq="auto"'
```

期望输出含：`h1/h2/h3 … seq="auto" seq-level="auto"`。

## 编号层级对照（飞书原生）

启用 `seq="auto" seq-level="auto"` 后，前端典型渲染：

```
1. 具身智能知识概览          ← h1
   1.1 基础认知              ← h2
       1.1.1 什么是具身智能  ← h3
   1.2 技术架构
       1.2.1 感知层
```

h1 计入编号树；若只需从「第一章」起编号，可与用户确认是否省略顶层 h1，改用语义段落 + 从 h2 开始。

## 命令速查

```bash
# 列出个人文档库
lark-cli wiki +node-list --as user --space-id my_library --page-all --format pretty

# 读取现有文档
lark-cli docs +fetch --api-version v2 --as user --doc "<token>" --doc-format markdown

# 覆盖 + 原生编号
lark-cli docs +update --api-version v2 --as user --doc "<token>" \
  --command overwrite --content @article-feishu.xml

# 追加 Markdown 片段
lark-cli docs +update --api-version v2 --as user --doc "<token>" \
  --command append --doc-format markdown --content @fragment.md
```

## 注意事项

- **个人文档库 ≠ 云盘根目录**：用 `wiki +node-list --space-id my_library`，不要用 `drive +search` 代替（除非用户明确要求搜 owned 文档且已具备 `search:docs:read` scope）。
- **Markdown 写入无法设置标题自动编号**；需要飞书自带编号时必须用 **DocxXML + `seq="auto"`**。
- **本地与飞书可 intentionally 分叉**：用户说「只改本地」或「不要同步飞书」时，禁止调用 `docs +update`。
- 交叉引用改用语义名称（如「数据采集 + 仿真服务」），避免引用会随自动编号变化的 `6.1` 字面量。
- 临时 XML/QR 文件可在任务完成后删除，勿提交含 token 的文件。

## 延伸阅读

- 标题编号 API 背景：[GitHub larksuite/cli#316](https://github.com/larksuite/cli/issues/316)、[#671](https://github.com/larksuite/cli/issues/671)
- XML 语法：[`../lark-doc/references/lark-doc-xml.md`](../lark-doc/references/lark-doc-xml.md)
- 更新指令：[`../lark-doc/references/lark-doc-update.md`](../lark-doc/references/lark-doc-update.md)
