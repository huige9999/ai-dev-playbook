---
description: 根据当前 git staged changes 生成一条中文 commit message
---

用户会以如下形式调用：
/commit-msg

## 任务
1) 在 Claude Code 环境中通过终端获取 staged changes：
   - 必须运行：`git diff --cached`
   - 可选辅助：`git diff --cached --stat`
2) 基于 staged changes，生成 **一条**面向 git 的 commit message（中文）：
   - 格式：Conventional Commits：`type(scope): 摘要`
   - scope：能从改动路径推断就写，推断不出就省略 `(scope)`
   - 摘要：中文、简洁、以动词开头、<= 72 字符、不要句号
   - type 从 `feat|fix|refactor|perf|test|docs|build|ci|chore` 中选择最贴切的一个
3) **输出要求：只输出 commit message 一行，不能包含其它任何文字、标点装饰或代码块。**

现在开始：先读取 staged changes，再输出最终的那一行 commit message。
