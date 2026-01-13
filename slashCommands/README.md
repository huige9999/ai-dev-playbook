# AI Dev Playbook

一套「可复制粘贴」的 Markdown 工作流库，用于在 Claude Code / Cursor / Codex 等 AI 辅助编码工具中复用：slash commands、采访式需求澄清、代码收集打包、模块文档、提交信息生成、经验沉淀等。

> 本仓库以 **只读使用** 为目标：打开 → 复制对应 md → 粘贴到你的工具里用。

---

## 快速开始

### 1) 放到 Claude Code（推荐）
将这些 md 作为 slash commands 使用：

- **用户级（全局）**：`~/.claude/commands/`
- **项目级（当前仓库）**：`.claude/commands/`

把本仓库的 md 文件复制到上述目录即可（或手动复制内容新建同名文件）。

### 2) 日常使用节奏（建议）
**采访澄清 → 收集范围 → 生成模块文档 → 编码执行 → 生成提交信息 → 经验沉淀**

对应命令：
`/interview-code` → `/collect` → `/module-doc` → `/code` → `/commit-msg` → `/save-memory`

---

## 工作流导航

### 0) 常用命令速览
- `/wsl2win`：WSL 路径与 Windows 路径映射（Windows 路径自动把 `\` 转 `/`）
- `/commit-msg`：根据 staged changes 生成 **一条中文** commit message
- `/collect`：根据线索定位相关模块，多轮 include/ignore 后执行 `repomix`
- `/module-doc`：为模块生成「可分享上下文包」：模块文档 + 关键代码片段 + 技术栈信息
- `/interview-code`：不熟模块时，用“读代码 + 采访”循环把模糊需求澄清到可执行规格
- `/code`：严格遵循某个方案 md 执行编码任务（你写方案，agent照做）
- `/save-memory`：将本轮任务沉淀为可复用记忆块（你自己建文件粘贴保存）

---

## 文件导航

### `wsl2win.md`
**用途**：把 WSL 的模块路径映射到 Windows 路径，方便跨环境同步/调用。  
**典型用法**：
- 两参：`/wsl2win <wsl_path> <win_path>`
- 一参：`/wsl2win <win_path>`（WSL 侧自动取当前工作目录或 repo_root/src）
- Win 路径会自动把 `\` 规范化为 `/`

---

### `commit-msg.md`
**用途**：总结本次 staged changes，并输出 **一条中文** commit message（只输出一行，便于复制）。  
**典型用法**：
- `/commit-msg`
> 提交前先 `git add ...`，确保暂存区就是你要提交的改动。

---

### `interview-code.md`
**用途**：当你对目标模块不熟、需求又模糊时，agent 会边读代码边采访你，逐轮收敛成清晰规格。  
**典型用法**：
- `/interview-code <模糊需求/命令>`
- 你补充回答几轮后：输入 `OK / 定稿` 输出《最终规格》+《建议改动范围》

推荐搭配：定稿后接 `/collect` 或 `/module-doc`。

---

### `collect.md`
**用途**：根据线索/需求定位相关模块，给 high/middle/low 候选清单；你多轮审查后 `OK`，自动执行：
`repomix --include "..." --ignore "..."`  
**典型用法**：
- `/collect <线索/需求...>`
- 你反馈：保留/排除/补充线索
- 你输入：`OK` → 执行 repomix 打包

---

### `module-doc.md`
**用途**：把指定模块打包成「可丢给网页端 LLM 的上下文包」：模块背景、边界、关键流程、技术栈、关键代码片段。  
**理想用法**（推荐用 `--` 分隔需求）：
- `/module-doc <path1> <path2> -- <需求/目的>`
例：
- `/module-doc src/views/homeViews/cityPartner -- 修复月结页金额计算错误`

---

### `code.md`
**用途**：严格按你写的方案 md 执行编码任务。  
**典型用法**：
- `/code <方案md路径>`
> 适合你先写一份“完美方案”，再让 agent 只执行，不扩展范围。

---

### `save-memory.md`
**用途**：把本轮成功完成的任务压缩成一段 Markdown 记忆块（只输出可粘贴内容）。  
**典型用法**：
- `/save-memory`
> 你自己在仓库里新建文件，把输出粘贴保存即可。

---

## 推荐组合（按场景）

### 场景 A：不熟模块 + 模糊需求
1. `/interview-code ...`（澄清到可执行规格）
2. `/collect ...`（确定相关模块范围）
3. `/module-doc ... -- ...`（导出上下文包给网页端 LLM）
4. 编码实现（手动或 `/code plan.md`）
5. `/commit-msg`（生成提交信息）
6. `/save-memory`（沉淀经验）

### 场景 B：需求清晰，只要快速打包相关代码让外部 LLM 建议
1. `/collect ...` → `OK` → repomix
2. `/module-doc ... -- ...`（补一份背景文档）
3. 把“文档 + 代码片段/打包结果”丢给网页端 LLM

---

## 约定
- 本仓库内容以 Markdown 为主，强调 **可复制粘贴** 与 **可复用**。
- 每个命令的行为以对应 md 文件为准；README 仅作导航。

