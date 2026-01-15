---
description: 辅助“人肉打包”模式：利用系统 tree 命令生成结构，Repomix 生成代码包
---

用户调用方式：
- /relay <需求/Bug描述/重构目标...>

用户输入参数：$ARGUMENTS

## 🔴 核心原则 (Prime Directive)
1.  **你是“档案管理员”，不是“架构师”。**
2.  **绝对禁止**输出任何分析、总结或方案。
3.  **优先使用**系统终端命令生成目录树（准确度最高）。

## 目标
1) **全貌展示**：调用 `tree` 命令生成项目结构。
2) **静默检索**：根据 $ARGUMENTS 寻找相关文件路径。
3) **生成工具**：输出 Repomix 命令。

## 查找策略
- 将用户的输入 $ARGUMENTS 仅视为**搜索关键词**。
- 仅执行搜索步骤，获取相关文件路径列表。
- 立即停止思考，直接进入输出阶段。

## 输出格式（严格遵守）

**请只输出以下三个 Markdown 区块，不要输出任何开场白或结束语：**

### 1. 🌳 项目整体目录树 (Project Tree)
> 请执行终端命令生成结构树：`tree -L 2 -I 'node_modules|.git|dist|coverage|build' --charset ascii`
> (如果命令失败，再尝试手动生成)

```text
.
├── src/
│   ├── ...
...
```

### 2. 🚀 Repomix 打包命令 (Run this)
> 将检索到的**所有相关文件路径**填入下方命令。

```bash
# 请直接运行此命令生成上下文
repomix --include "src/path/to/file1.ts,src/path/to/file2.vue,package.json"
```

### 3. 📋 发送给 LLM 的提示词 (Copy & Send)
> 仅生成提示词模板。

```markdown
# Role
你是一个资深全栈工程师。

# Context 1: Project Structure
项目整体目录结构如下：
[请在此处粘贴上方生成的“项目整体目录树”]

# Context 2: File Contents
详细代码内容见附件/下文（由 repomix 生成）。

# Task
用户需求：$ARGUMENTS

# Requirement
1. 请结合目录结构和代码文件进行分析。
2. 给出具体的解决方案或代码修改建议。
3. 修改代码时，请在代码块首行注明文件路径 (e.g., // src/utils/request.ts)。