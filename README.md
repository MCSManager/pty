# MCSManager pty application

[![--](https://img.shields.io/badge/Go_Version-1.18.3-green.svg)](https://github.com/MCSManager)
[![--](https://img.shields.io/badge/Support-Windows/Linux-yellow.svg)](https://github.com/MCSManager)
[![--](https://img.shields.io/badge/License-MIT-red.svg)](https://github.com/MCSManager)

中文 | [English](README_EN.md)

<br />

## 什么是 PTY/TTY？

tty = "teletype"，pty = "pseudo-teletype"

众所周知，程序拥有输入与输出流，但是数据流与显示器之间有一个区别，那便是缺少行和高的排列维度。简而言之，PTY 的中文意义就是伪装设备终端，让我们的程序伪装成一个拥有固定高宽的显示器，接受来自程序的输出内容。

<br />

## 使用

使用方法一：开一个 PTY 并执行命令，设置固定窗口大小，IO 流直接转发。

- 注意：-cmd 接收的是一个数组, 命令的参数以数组的形式传递，如：`["java","-jar","ser.jar","nogui"]`

```bash
go build main.go
./main -dir "." -cmd '["bash"]' -size 50,50
```

接下来您会得到一个设置好大小宽度的窗口，并且您可以像 SSH 终端一样，进行任何交互。

```
ping google.com
top
htop
```

<br />

使用方法二：开启一个 PTY 并执行命令，并接受动态指令调整。

```bash
go build main.go
./main.exe -dir "." -cmd '["cmd.exe"]'
```

Ping google.com

这段数据需要向程序的输入流发送，末尾跟上 `\n` 符

```bash
{"type":1,"data":"ping google.com\r\n"}\n
```

重设 PTY 窗口大小

```
{"type":2,"data":"20,20"}\n
```

<br />

## MCSManager

MCSManager 是一款开源，分布式，开箱即用，支持 Minecraft 和其他控制台应用的程序管理面板。

这个程序是专门为了 MCSManager 而设计，您也可以尝试嵌入到您自己的程序中。

More info: [https://github.com/mcsmanager](https://github.com/mcsmanager)

<br />

## 贡献

此程序属于 MCSManager 的最重要的核心功能之一，非必要不新增功能。

-   如果您想为这个项目提供新功能，那您必须开一个 `issue` 说明此功能，并提供编程思路，我们一起经过讨论后再决定是否开发

-   如果您是修复 BUG，可以直接提交 PR 并说明情况

<br />

## MIT license

遵循 [MIT License](https://opensource.org/licenses/MIT) 开源协议。

版权所有 [zijiren233](https://github.com/zijiren233) 和贡献者们。
