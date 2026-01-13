---
description: 执行 wsl2win：/wsl2win <WSL_PATH> <WIN_PATH>（自动把 \ 转成 /；可只传 WIN_PATH）
---

用户会以如下形式调用：
- /wsl2win <WSL_PATH> <WIN_PATH>
- /wsl2win <WIN_PATH>

用户输入参数为：$ARGUMENTS

## 要求
1) 参数解析（分支处理）
   - 如果 $ARGUMENTS 里包含 **两个参数**：
     - WSL_PATH = 第一个参数（例如：~/projects/work/xxx/src）
     - WIN_PATH_RAW = 第二个参数（例如：D:\workspace-...\src）
   - 如果 $ARGUMENTS 里只有 **一个参数**：
     - WIN_PATH_RAW = 该参数
     - WSL_PATH = 当前工作目录（pwd）
       - 若当前目录不以 /src 结尾，则优先尝试取 git 仓库根目录并拼接 /src：
         - repo_root = `git rev-parse --show-toplevel`（失败则用 pwd）
         - WSL_PATH = "${repo_root}/src"

2) 规范化 Windows 路径：
   - WIN_PATH = 将 WIN_PATH_RAW 中所有反斜杠 "\" 替换为正斜杠 "/"
     例：D:\a\b\c  ->  D:/a/b/c

3) 生成并执行命令：
```bash
wsl2win <WSL_PATH> <WIN_PATH>
````
