---
name: lark-doc-precision
version: 1.0.0
description: "精准修改飞书文档指定 block，定位目标后只改目标块，文档中其他内容一律不动。当用户需要对飞书文档做精准修改、替换代码块/段落/表格等特定内容时使用。"
metadata:
  requires:
    bins: ["lark-cli"]
---


# 精准修改飞书文档

> **前置条件：** 先阅读 [`../lark-shared/SKILL.md`](../lark-shared/SKILL.md)。

## 核心原则：精准手术

**只改用户指定的 block，文档中其他任何内容一律不动。** 这是铁律，不是建议。每次修改文档前必须遵守。

---

## 工作流程

### 步骤一：获取 block ID

必须先拿到目标 block 的 ID，才能精准修改：

```bash
# 场景 A：已知目标关键词（如代码块 caption 标题）
lark-cli docs +fetch --api-version v2 --doc "<文档URL或token>" \
  --scope keyword --keyword "<关键词>" \
  --detail with-ids --max-depth 0 \
  --context-before 1 --context-after 3 --format pretty
```

```bash
# 场景 B：已知章节标题
lark-cli docs +fetch --api-version v2 --doc "<文档URL或token>" \
  --scope section --start-block-id "<章节标题block_id>" \
  --detail with-ids
```

```bash
# 场景 C：已知文档 URL 但不知关键词，先拿大纲定位
lark-cli docs +fetch --api-version v2 --doc "<文档URL或token>" \
  --scope outline --max-depth 5 \
  --detail with-ids --format pretty
```

> **技巧：** 如果输出是 pretty 格式不方便解析，写入临时文件后用 Python `re` 搜索：
> ```bash
> lark-cli docs +fetch ... --format pretty > _tmp_doc.txt
> # 然后用 Python 正则搜索目标 block id
> ```

### 步骤二：执行精准修改

根据修改内容选择命令：

#### 方式 A：替换整个 block（推荐）

```bash
# 将 XML 内容写入临时文件
# 然后用 @文件 语法传入
lark-cli docs +update --api-version v2 \
  --doc "<文档URL或token>" \
  --command block_replace \
  --block-id "<目标block_id>" \
  --content "@<相对路径文件>"
```

#### 方式 B：全文字符串替换

```bash
lark-cli docs +update --api-version v2 \
  --doc "<文档URL或token>" \
  --command str_replace \
  --pattern "<要替换的旧文本>" \
  --content "<新文本>"
```

> **注意：** `str_replace` 在 XML 模式下只支持行内匹配，无法跨 block 修改。块级改动必须用 `block_replace`。

### 步骤三：验证修改

```bash
# 验证修改结果
lark-cli docs +fetch --api-version v2 \
  --doc "<文档URL或token>" \
  --scope keyword --keyword "<关键词>" \
  --max-depth 0 \
  --format pretty
```

---

## XML 格式规范（block_replace 专用）

所有 block 级替换内容必须使用 XML 格式：

```xml
<!-- 代码块 -->
<pre caption="可选说明" lang="Plain Text"><code>代码内容<br/>每行用 &lt;br/&gt; 分隔</code></pre>

<!-- 普通段落 -->
<p>段落内容，<b>加粗</b> <a href="https://...">链接</a></p>

<!-- 表格 -->
<table>
  <colgroup><col width="100"/><col width="200"/></colgroup>
  <thead><tr><th>表头1</th><th>表头2</th></tr></thead>
  <tbody><tr><td>单元格1</td><td>单元格2</td></tr></tbody>
</table>

<!-- 标题 -->
<h2>标题</h2>
```

### 转义规则（铁律）

- 标签本身 **禁止转义**，只有标签内部的文本内容才需要转义
- 错误：`&lt;p&gt;内容&lt;/p&gt;`（把标签也转义了）
- 正确：`<p>A &amp; B 的对比</p>`（标签保持原样，`&` 转义为 `&amp;`）
- 换行符 → `<br/>`
- `<` → `&lt;`，`>` → `&gt;`，`&` → `&amp;`

---

## 典型工作流示例：替换代码块

假设要修改文档中 caption="工程结构框架" 的代码块：

```bash
# Step 1: 获取 block ID
lark-cli docs +fetch --api-version v2 \
  --doc "https://xxx.feishu.cn/wiki/xxx" \
  --scope keyword --keyword "工程结构框架" \
  --detail with-ids --format pretty > _tmp.txt

# Step 2: 用 Python 从临时文件中提取 block_id
python -c "import re; data=open('_tmp.txt').read(); m=re.search(r'<pre\s+id=\"([^\"]+)\"[^>]*caption=\"工程结构框架\"', data); print(m.group(1))"

# Step 3: 准备新内容（写入临时 XML 文件）
python -c "
content = '新代码内容'.replace('&', '&amp;').replace('<', '&lt;').replace('>', '&gt;').replace('\n', '<br/>')
print(f'<pre caption=\"工程结构框架\" lang=\"Plain Text\"><code>{content}</code></pre>')
" > _new_pre.xml

# Step 4: 执行 block_replace（必须在同一目录下）
lark-cli docs +update --api-version v2 \
  --doc "https://xxx.feishu.cn/wiki/xxx" \
  --command block_replace \
  --block-id "<上一步拿到的ID>" \
  --content "@_new_pre.xml"

# Step 5: 验证
lark-cli docs +fetch --api-version v2 \
  --doc "https://xxx.feishu.cn/wiki/xxx" \
  --scope keyword --keyword "工程结构框架" \
  --format pretty
```

---

## 安全规则

- **写入操作前确认用户意图**，建议先用 `--dry-run` 预览
- **禁止输出密钥**（appSecret、accessToken）
- **文件路径只接受相对路径**：`@file` 只接受当前目录下的相对路径，传绝对路径会报 `unsafe file path`。数据输入优先用 stdin 传入
- **同一 block 只能被 replace 一次**：多次修改同一 block 请合并为一次 block_replace
- **block_replace 后旧 ID 可能失效**：如需继续操作相邻块，先重新 fetch 获取最新 ID

## 权限

| 操作 | 所需 scope |
|------|-----------|
| 读取文档 | `docs:document:readonly` |
| 修改文档 | `docs:document` |
