# agent-skill 格式规范参考文档

## 目录结构

一个有效技能以独立目录形式存在，最小结构仅需包含必填文件 SKILL.md，可根据功能需求补充3个可选目录，完整结构如下：

```
skill-name/      # 目录名必须与 SKILL.md 中 "name" 字段完全一致
├── SKILL.md     # 必填：存储元数据与技能操作指令
├── scripts/     # 可选：存放可执行代码脚本，该文件夹下不可再新建文件夹
├── references/  # 可选：存放补充说明文档，该文件夹下不可再新建文件夹
└── assets/      # 可选：存放静态资源文件，该文件夹下不可再新建文件夹
```

## SKILL.md 核心格式

### 前置元数据（YAML格式）

```yaml
---
name: skill-name  # 必填，1-64字符；仅含小写字母(a-z)、数字、连字符(-)；不首尾含连字符、无连续连字符(--)；需与目录名一致

description: 必填，1-1024字符；需说明「技能功能+使用场景」，包含关键词(方便智能体识别)。

license: 选填，简短标注授权类型或授权文件引用，例：license:Apache-2.0/license: 详见LICENSE.txt

compatibility: 选填，1-500字符；仅当技能有特殊环境要求时填写(如依赖软件、网络权限、适配产品)，否则无需填写。

metadata: 选填，自定义键值对，键名建议唯一(避免冲突)，可存储作者、版本、依赖等信息。
---
```

### Markdown正文（技能指令）

正文无强制格式限制，核心作用是为智能体提供清晰的操作指引，建议结构化呈现以下内容：

- 分步执行说明（按操作逻辑排序）
- 输入/输出示例（明确预期格式）
- 常见边界情况与异常处理方案

**约束要求：** 建议正文容量≤5000 tokens（约500行），超长内容需拆分至references/目录。

## 字段说明

### name（必填）

- **格式**：1-64字符
- **字符限制**：仅含小写字母(a-z)、数字、连字符(-)
- **命名规则**：
  - 不首尾含连字符
  - 无连续连字符(--)
  - 需与目录名完全一致

**示例：**
```
name: skill-ad
name: pdf
name: xlsx
```

### description（必填）

- **格式**：1-1024字符
- **内容要求**：需说明「技能功能+使用场景」
- **关键词**：包含关键词(方便智能体识别)

**示例：**
```
description: 搜索、修改和安装技能的工具。支持从本地skill原始库或GitHub查找匹配的skill，进行标准化修改，并安装到全局skill目录。
```

### license（选填）

- **格式**：简短标注授权类型或授权文件引用
- **示例**：
  - `license: Apache-2.0`
  - `license: 详见LICENSE.txt`

### compatibility（选填）

- **格式**：1-500字符
- **填写条件**：仅当技能有特殊环境要求时填写
- **示例**：
  - `compatibility: 需要GitHub MCP支持，需要访问本地文件系统的权限`
  - `compatibility: 需要Python 3.8+环境`

### metadata（选填）

- **格式**：自定义键值对
- **键名要求**：建议唯一(避免冲突)
- **常见内容**：作者、版本、依赖等信息

**示例：**
```yaml
metadata:
  version: 1.0.0
  author: skill-ad
  local_storage: E:\AI applic\agent test\skills-in-storage
  global_skills: C:\Users\JOKerDen\.trae-cn\skills
```

## 目录说明

### SKILL.md（必填）

存储元数据与技能操作指令，是skill的核心文件。

### scripts/（可选）

存放可执行代码脚本，该文件夹下不可再新建文件夹。

**常见脚本类型：**
- Python脚本（.py）
- JavaScript脚本（.js）
- Shell脚本（.sh）
- PowerShell脚本（.ps1）

### references/（可选）

存放补充说明文档，该文件夹下不可再新建文件夹。

**常见文档类型：**
- 参考文档（.md）
- API文档（.md）
- 使用指南（.md）

### assets/（可选）

存放静态资源文件，该文件夹下不可再新建文件夹。

**常见资源类型：**
- 图片（.png, .jpg, .svg）
- 配置文件（.json, .yaml, .xml）
- 模板文件（.template）

## 命名规范

### 目录命名

- 必须与SKILL.md中的name字段完全一致
- 仅含小写字母、数字、连字符
- 不首尾含连字符
- 无连续连字符

**示例：**
```
skill-ad/
pdf/
xlsx/
```

### 文件命名

- 使用小写字母、数字、连字符、下划线
- 避免使用空格和特殊字符
- 使用有意义的文件名

**示例：**
```
search_skill.py
download_github.py
reference.md
```

## 最佳实践

1. **简洁明了**：description应该简洁明了，包含关键词
2. **结构化内容**：正文内容应该结构化，便于智能体理解
3. **合理拆分**：超长内容应该拆分至references/目录
4. **版本管理**：使用metadata字段管理版本信息
5. **兼容性说明**：有特殊环境要求时，填写compatibility字段

## 常见错误

1. **目录名与name不一致**：目录名必须与SKILL.md中的name字段完全一致
2. **缺少必填字段**：name和description是必填字段
3. **命名不规范**：使用大写字母、空格或特殊字符
4. **内容过长**：正文内容超过5000 tokens，应该拆分
5. **缺少关键词**：description中缺少关键词，不利于智能体识别

## 示例

### 完整示例

```yaml
---
name: skill-ad
description: 搜索、修改和安装技能的工具。支持从本地skill原始库或GitHub查找匹配的skill，进行标准化修改，并安装到全局skill目录。
license: Apache-2.0
compatibility: 需要GitHub MCP支持，需要访问本地文件系统的权限
metadata:
  version: 1.0.0
  author: skill-ad
  local_storage: E:\AI applic\agent test\skills-in-storage
  global_skills: C:\Users\JOKerDen\.trae-cn\skills
---

# skill-ad：技能搜索、修改和安装工具

## 功能概述

skill-ad 是一个用于搜索、修改和安装技能的工具...

## 工作流程

### 第一步：搜索本地skill原始库

...

## 使用示例

...

## 注意事项

...
```

## 相关资源

- [agent-skill官方文档](https://example.com)
- [skill-creator使用指南](https://example.com)
