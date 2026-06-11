# 练习

本课程每讲都配有一组练习。有些给出明确任务，有些是开放题，比如「试试使用 X 和 Y 工具」。我们非常鼓励你亲自上手。

这些练习暂无标准答案。如果被某个问题卡住了，欢迎在 [Discord](https://ossu.dev/#community) 的 `#missing-semester-forum` 发帖，或邮件告诉我们你已经尝试了什么，我们会尽力帮忙。 这些练习也很适合作为与 LLM 交流的起点，让你以交互方式深入探索。练习的真正价值在于「探索答案的过程」，而不只是答案本身。我们鼓励你在做题时顺着分支问题继续深挖，多问「为什么」，而不是只追求最短路径。

1. 本课程要求你使用类 Unix 的 Shell，如 Bash 或 ZSH 。若你在 Linux 或 macOS 上，无需额外设置。若你在 Windows 上，请确认你用的不是 `cmd.exe` 或 `PowerShell`；你可以使用 [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/) 或 Linux 虚拟机来获得 Unix 风格的命令行工具。要确认当前 Shell 是否合适，可运行 `echo $SHELL`；若输出类似 `/bin/bash` 或 `/usr/bin/zsh`，就说明没问题。
2. `ls` 的 `-l` 选项（flag）作用是什么？运行 `ls -l /` 并观察输出。每一行最前面的 10 个字符分别代表什么？（提示：`man ls`）
3. 在命令 `find ~/Downloads -type f -name "*.zip" -mtime +30` 中，`*.zip` 是一个 「glob」。什么是 glob？新建一个测试目录并创建一些文件，试试 `ls *.txt`、`ls file?.txt`、`ls {a,b,c}.txt` 等模式。参见 Bash 手册中的 [Pattern Matching](https://www.gnu.org/software/bash/manual/html_node/Pattern-Matching.html)。
4. `'单引号'`、`"双引号"` 和 `$'ANSI 引号'` 有什么区别？写一条命令，输出一个同时包含字面量 `$` 、 `!` 和换行符的字符串。参见 [Quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)。
5. Shell 有三条标准流：stdin（0）、stdout（1）、stderr（2）。运行 `ls /nonexistent /tmp`，把 stdout 和 stderr 分别重定向到两个文件。你将如何把两者都重定向到同一个文件？参见 [Redirections](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)。
6. `$?` 保存上一条命令的退出状态（0 表示成功）。`&&` 仅在前一条成功时执行后一条；`||` 仅在前一条失败时执行后一条。写一个一行命令：仅当 `/tmp/mydir` 不存在时才创建它。参见 [Exit Status](https://www.gnu.org/software/bash/manual/html_node/Exit-Status.html)。
7. 为什么 `cd` 必须是 Shell 内建命令，而不能是独立程序？（提示：想想子进程能影响和不能影响父进程的哪些状态。）
8. 写一个脚本，接收文件名参数（`$1`），用 `test -f` 或 `[ -f ... ]` 检查该文件是否存在，并根据结果输出不同提示。参见 [Bash Conditional Expressions](https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html)。
9. 把上一题完成的脚本保存为文件（如 `check.sh`）。先运行 `./check.sh somefile`，会发生什么？然后执行 `chmod +x check.sh` 再试一次。为什么这一步是必须的？（提示：比较 `chmod` 前后的 `ls -l check.sh` 输出）
10. 在脚本的 `set` 选项（flag）里加入 `-x` 会发生什么？写个简单脚本试试并观察输出。参见 [The Set Builtin](https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html)。
11. 写一条命令，把文件复制为带当天日期的备份文件名（例如 `notes.txt` → `notes_2026-01-12.txt`）。（提示：`$(date +%Y-%m-%d)`）参见 [Command Substitution](https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.html)。
12. 修改讲义中的「复现偶尔才会失败的测试」脚本（flaky test），使它能够从命令行参数接收测试命令，而不是在脚本中写死 `cargo test my_test`。（提示：`$1` 或 `$@`）参见 [Special Parameters](https://www.gnu.org/software/bash/manual/html_node/Special-Parameters.html）。
13. 使用管道找出你「home 目录」中最常见的 5 种文件扩展名。（提示：组合 `find`、`grep` / `sed` / `awk`、`sort`、`uniq -c` 以及 `head`）
14. `xargs` 会把 stdin 的每一行转换为命令参数。结合 `find` 和 `xargs`（不要用 `find -exec`），找出目录中所有 `.sh` 文件，并用 `wc -l` 统计每个文件行数。加分项：正确处理文件名中的空格。（提示：`-print0` 和 `-0`）参见 `man xargs`。
15. 使用 `curl` 获取 [课程网站](https://missing.csail.mit.edu/) 的 HTML，并通过 `grep` 统计列出了多少讲。（提示：找出每讲课程名称在那份 HTML 中的共性；用 `curl -s` 关闭进度输出。）
16. [`jq`](https://jqlang.github.io/jq/) 是处理 JSON 的强大工具。用 curl 获取示例数据 https://microsoftedge.github.io/Demos/json-dummy-data/64KB.json，再用 jq 提取 version 大于 6 的人员姓名。（提示：先 `jq .` 看结构；再试 `jq '.[] | select(...) | .name'`）
17. `awk` 可以按列值过滤行并改写输出。例如，`awk '$3 ~ /pattern/ {$4=""; print}'` 会只输出第三列匹配 `pattern` 的行，并省略第四列。请写一个 `awk` 命令：只输出第二列大于 100 的行，并交换第一列和第三列。可用这条命令测试：`printf 'a 50 x\nb 150 y\nc 200 z\n'`
18. 拆解讲义中的 [SSH 日志处理管道](https://missing-semester-cn.github.io/2026/course-shell/#shell-%E8%AF%AD%E8%A8%80bash)：每一步分别做了什么？然后仿照它构建一个管道，从 `~/.bash_history`（或 `~/.zsh_history`）中找出你最常使用的 Shell 命令。

# 练习答案

## 1. 选择类 Unix Shell

类 Unix Shell 是指像 Bash、Zsh 这样的命令行解释器，它们在 Linux、macOS 或 WSL 中运行。Windows 自带的 `cmd.exe` 和 `PowerShell` 不是类 Unix Shell，它们的语法和行为与 Bash/Zsh 不完全相同。

如果你在 Windows 上，推荐使用：

- WSL（Windows Subsystem for Linux）
- Linux 虚拟机
- Git Bash 或 MSYS2（作为简易替代）

要检查当前 Shell 是否是类 Unix Shell，运行：

```bash
echo $SHELL
```

如果输出类似 `/bin/bash`、`/usr/bin/zsh`、`/usr/bin/fish`，说明你已经在合适的 Shell 里。

## 2. `ls -l` 的作用和前 10 个字符含义

`ls -l` 是 `ls` 的“长格式”选项，它会显示更多信息：文件类型、权限、硬链接数、所有者、所属组、大小、修改时间、文件名等。

每一行最前面的 10 个字符表示：

- 第 1 个字符：文件类型
- 接下来的 9 个字符：权限，分成 3 组，每组 3 个字符
  - 第 2-4：所有者权限
  - 第 5-7：所属组权限
  - 第 8-10：其他用户权限

常见字符含义：

- 第 1 个字符：
  - `-`：普通文件
  - `d`：目录
  - `l`：符号链接
  - `c`：字符设备
  - `b`：块设备

- 权限字符：
  - `r`：可读
  - `w`：可写
  - `x`：可执行
  - `-`：没有该权限

例如：

```text
-rw-r--r--
```

表示：普通文件，所有者可读可写，组用户可读，其他用户可读。

## 3. 什么是 glob

Glob 是 shell 用来匹配文件名的通配符模式。Shell 会在命令执行前把 glob 模式展开成匹配的文件名。

常见 glob 语法：

- `*`：匹配任意数量的任意字符
- `?`：匹配单个任意字符
- `[abc]`：匹配方括号中的任意一个字符
- `[!abc]`：匹配不在方括号中的字符
- `{a,b,c}`：匹配大括号中的任意一个模式

例如：

```bash
mkdir -p ~/glob-test
cd ~/glob-test
printf '%s\n' a.txt b.txt c.log file1.txt fileA.txt > /dev/null
ls *.txt       # 匹配所有以 .txt 结尾的文件
ls file?.txt   # 匹配 file1.txt、fileA.txt，但不匹配 file10.txt
ls {a,b,c}.txt # 匹配 a.txt、b.txt、c.txt
```

注意：大括号 `{a,b,c}` 不是 glob 模式本身，而是 Bash 的 brace expansion，它在文件名展开阶段生成多个候选词。

## 4. 三种引号的区别和示例

Shell 中常用的 3 种引号：

- 单引号 `'...'`：完全原义，不进行变量替换、命令替换、转义处理。
- 双引号 `"..."`：保持大部分字符原义，但允许变量替换、命令替换和一些转义序列。
- ANSI-C 引号 `$'...'`：在双引号的基础上还支持 `\n`、`\t`、`\xHH` 等 ANSI C 风格的转义序列。

举例：

```bash
var=hello
echo '$var'   # 输出 $var
echo "$var"  # 输出 hello
```

要输出一个同时包含字面量 `$`、`!` 和换行符的字符串，推荐用 ANSI-C 引号：

```bash
echo $'$
!
'
```

这条命令会输出：

- `$`
- 换行
- `!`
- 换行

如果你想用 `printf`，也可以这样写：

```bash
printf '%s\n' '$' '!'
```

## 5. stdout 和 stderr 的重定向

Shell 中：

- stdin：文件描述符 0
- stdout：文件描述符 1
- stderr：文件描述符 2

运行：

```bash
ls /nonexistent /tmp >stdout.txt 2>stderr.txt
```

会把正常输出写入 `stdout.txt`，把错误输出写入 `stderr.txt`。

要把两者都写到同一个文件：

```bash
ls /nonexistent /tmp >all.txt 2>&1
```

解释：

- `>all.txt`：把 stdout（1）写入 `all.txt`
- `2>&1`：把 stderr（2）重定向到 stdout 当前的目标，也就是 `all.txt`

顺序很重要：先重定向 stdout，然后再把 stderr 重定向到 stdout。

在 Bash 中，你也可以用简写：

```bash
ls /nonexistent /tmp &>all.txt
```

这两种写法最终效果相同。

## 6. `&&`、`||` 与条件执行

在 Shell 中：

- `command1 && command2`：只有 `command1` 成功（退出状态 0）时才执行 `command2`
- `command1 || command2`：只有 `command1` 失败（非 0）时才执行 `command2`

例如，要在 `/tmp/mydir` 不存在时才创建它：

```bash
[ ! -d /tmp/mydir ] && mkdir /tmp/mydir
```

或者：

```bash
test -d /tmp/mydir || mkdir /tmp/mydir
```

说明：

- `[ ! -d /tmp/mydir ]` 检查目录是否不存在。
- 如果条件为真，`mkdir /tmp/mydir` 就会执行。

## 7. 为什么 `cd` 必须是 Shell 内建命令

`cd` 必须是 Shell 内建命令，因为它改变的是当前进程的工作目录。

如果 `cd` 是独立程序：

- Shell 会启动一个子进程来运行它
- 子进程改变自己的工作目录后退出
- 父 Shell 的工作目录不会改变

所以你仍然会留在原来的目录里，`cd` 的效果就不起作用了。

这也是为什么 `cd`、`export`、`alias` 这些命令通常都是 shell 内建命令。

## 8. 检查文件是否存在的脚本

下面是一个从零开始的脚本示例：

```bash
#!/usr/bin/env bash

if [ $# -eq 0 ]; then
  echo "用法：$0 <文件名>"
  exit 1
fi

if [ -f "$1" ]; then
  echo "文件 '$1' 存在，且是普通文件。"
else
  echo "文件 '$1' 不存在，或不是普通文件。"
fi
```

说明：

- `#!/usr/bin/env bash`：告诉系统用 Bash 来运行这个脚本。
- `if [ -f "$1" ]`：判断第一个参数是否是普通文件。
- `$1`是脚本执行时传入的第一个位置参数。
- `"$1"` 用双引号包起来，避免文件名中有空格出错。

## 9. `chmod +x` 为什么必须

假设你保存脚本为 `check.sh`，如果文件权限没有可执行位，直接运行：

```bash
./check.sh somefile
```

可能会得到“Permission denied”。

执行：

```bash
chmod +x check.sh
```

之后，再运行：

```bash
./check.sh somefile
```

就能正常执行。

`chmod +x` 的作用是为文件添加“可执行权限”。

用 `ls -l check.sh` 可以看到差别：

- 没加可执行权限前：`-rw-r--r--`
- 加了可执行权限后：`-rwxr-xr-x`

如果你不想加可执行权限，也可以用：

```bash
bash check.sh somefile
```

这条命令是让 Bash 这个程序去读取脚本并执行。

## 10. `set -x` 的作用

`set -x` 会打开 shell 的跟踪模式，它会在执行每条命令前把命令打印出来。这个功能非常适合调试脚本。

例如：

```bash
#!/usr/bin/env bash
set -x

echo "开始"
ls /tmp
```

运行结果会类似：

```text
+ echo 开始
开始
+ ls /tmp
...
```

这能让你看到脚本执行时实际展开后的命令，帮助定位错误。

## 11. 用日期给文件做备份

最简单的命令是：

```bash
cp notes.txt "notes_$(date +%Y-%m-%d).txt"
```

解释：

- `$(date +%Y-%m-%d)` 会被替换成当天日期，例如 `2026-06-11`
- `"notes_$(...) .txt"` 会生成 `notes_2026-06-11.txt`

如果你想让命令更通用，可以这样写：

```bash
orig=notes.txt
cp "$orig" "${orig%.txt}_$(date +%Y-%m-%d).txt"
```

这里的 `${orig%.txt}` 会把字符串末尾的 `.txt` 删除。

## 12. 修改 flaky test 脚本

要让脚本从命令行接收要执行的测试命令，可以使用 `$@` 来表示所有参数。

一个示例脚本：

```bash
#!/usr/bin/env bash

if [ $# -eq 0 ]; then
  echo "用法：$0 <测试命令> [参数...]"
  exit 1
fi

retry=3
for i in $(seq 1 $retry); do
  echo "第 $i 次运行： $@"
  "$@"
  status=$?
  if [ $status -eq 0 ]; then
    echo "测试通过"
    exit 0
  fi
  echo "测试失败，退出状态 $status"
  sleep 1
done

exit 1
```

说明：

- `$@` 表示传入脚本的所有参数，保留原始分隔。
- `"$@"` 可以正确处理参数中的空格。
- `status=$?` 保存上一个命令的退出状态。

## 13. 找出 home 目录最常见的 5 种扩展名

一种常见写法：

```bash
find ~ -type f -name '*.*' -print0 \
  | awk -v RS='\0' -F. '{print $NF}' \
  | sort \
  | uniq -c \
  | sort -rn \
  | head -5
```

说明：

- `find ~ -type f -name '*.*' -print0`：查找带点的文件名，并用 NUL 分隔，避免空格问题。
- `awk -v RS='\0' -F. '{print $NF}'`：按点分割，并打印最后一列，也就是扩展名。
- `sort | uniq -c | sort -rn | head -5`：统计并按次数降序取前 5 个。

如果不需要处理空格：

```bash
find ~ -type f -name '*.*' | sed 's|.*/||; s/.*\.//' | sort | uniq -c | sort -rn | head -5
```

## 14. `find` 和 `xargs` 结合统计 `.sh` 文件行数

要正确处理文件名中的空格，推荐这样写：

```bash
find . -name '*.sh' -print0 | xargs -0 wc -l
```

如果你想让每个文件单独统计一行：

```bash
find . -name '*.sh' -print0 | xargs -0 -n1 wc -l
```

说明：

- `find . -name '*.sh' -print0`：找到所有 `.sh` 文件，并用 NUL 字符分隔文件名。
- `xargs -0`：从 NUL 分隔的输入中读取参数，避免空格问题。
- `wc -l`：统计行数。

## 15. 用 `curl` 和 `grep` 统计课程网站讲数

这个问题的关键是先观察网页 HTML，找出每一讲标题的共同模式。一个常见做法是：

```bash
curl -s https://missing.csail.mit.edu/ | grep -o 'Lecture [0-9]\+' | sort -u | wc -l
```

如果网页是用 `<h3>` 或其他标签包裹讲名，也可以改成：

```bash
curl -s https://missing.csail.mit.edu/ | grep -o '<h3>[^<]*</h3>' | wc -l
```

重点是：先用 `curl -s` 获取 HTML，再用 `grep` 或 `sed` 提取对应的行或标记，最后统计数量。

## 16. 用 `jq` 处理 JSON

先查看 JSON 结构：

```bash
curl -s https://microsoftedge.github.io/Demos/json-dummy-data/64KB.json | jq .
```

如果结构是一个数组，每个元素有 `version` 和 `name`，那么可以这样筛选：

```bash
curl -s https://microsoftedge.github.io/Demos/json-dummy-data/64KB.json \
  | jq -r '.[] | select(.version > 6) | .name'
```

说明：

- `.[]`：遍历数组中的每个对象。
- `select(.version > 6)`：只保留 `version` 大于 6 的对象。
- `.name`：输出名称。
- `-r`：去掉 jq 默认的双引号，直接打印纯文本。

## 17. `awk` 输出第二列大于 100，并交换第一列和第三列

你可以这样写：

```bash
printf 'a 50 x\nb 150 y\nc 200 z\n' | awk '$2 > 100 {print $3, $1}'
```

解释：

- `awk` 按空白字符拆分列。
- `$2 > 100`：只处理第二列大于 100 的行。
- `print $3, $1`：输出第三列和第一列，顺序对调。

这条命令会打印：

```text
y b
z c
```

## 18. 拆解 SSH 日志处理管道，并统计常用命令

一个典型的 SSH 日志处理管道会做这些事：

1. 读取日志文件，比如 `/var/log/auth.log` 或 `/var/log/secure`。
2. 用 `grep sshd` 筛选出与 SSH 相关的行。
3. 用 `awk`、`cut`、`sed` 等工具提取感兴趣的字段，例如远程 IP、用户名、登录结果。
4. 用 `sort | uniq -c | sort -rn` 统计每种结果的出现次数。

例如：

```bash
grep sshd /var/log/auth.log | awk '{print $1,$2,$3,$11}' | sort | uniq -c | sort -rn | head
```

要从历史文件统计最常使用的命令，可以这样做：

- 对 Bash：

```bash
cat ~/.bash_history | awk '{print $1}' | sort | uniq -c | sort -rn | head -20
```

- 对 Zsh：

```bash
cat ~/.zsh_history | sed 's/^:[0-9]*:[0-9];//' | awk '{print $1}' | sort | uniq -c | sort -rn | head -20
```

说明：

- Bash 历史文件通常每行就是一个命令。
- Zsh 历史文件可能包含时间戳前缀，需要先用 `sed` 删除。
- `awk '{print $1}'` 取每行的第一个单词，也就是命令名称。
- `sort | uniq -c | sort -rn` 统计出现次数并按多到少排序。
- `head -20` 只取最常用的前 20 个命令。
