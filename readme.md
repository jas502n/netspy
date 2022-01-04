## ✨ 项目简介

🦄 **netspy是一款快速探测内网可达网段工具**

![image](https://user-images.githubusercontent.com/24275308/147852768-08c706e4-5574-4b75-9b24-ba5b277b063a.png)


#### 编译：

```bash
$ export GO111MODULE=on
```

```bash

$ ./build.sh
Build netspy_linux_amd64 ...
linux GOARCH=amd64 go build -tags all --ldflags= -o output/netspy_linux_amd64
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
   6675724 ->   3571712   53.50%   linux/amd64   netspy_linux_amd64

Packed 1 file.
Build netspy_linux_386 ...
linux GOARCH=386 go build -tags all --ldflags= -o output/netspy_linux_386
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
   5881272 ->   3427464   58.28%   linux/i386    netspy_linux_386

Packed 1 file.
Build netspy_windows_amd64.exe ...
windows GOARCH=amd64 go build -tags all --ldflags= -o output/netspy_windows_amd64.exe
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
   6839296 ->   3587072   52.45%    win64/pe     netspy_windows_amd64.exe

Packed 1 file.
Build netspy_windows_386.exe ...
# github.com/mdlayher/raw
../../../pkg/mod/github.com/mdlayher/raw@v0.0.0-20190313224157-43dbcdd7739d/timeval32.go:14:42: undefined: unix.Timeval
../../../pkg/mod/github.com/mdlayher/raw@v0.0.0-20190313224157-43dbcdd7739d/timeval32.go:16:16: undefined: timeoutError
../../../pkg/mod/github.com/mdlayher/raw@v0.0.0-20190313224157-43dbcdd7739d/timeval32.go:18:10: undefined: unix.Timeval
windows GOARCH=386 go build -tags all --ldflags= -o output/netspy_windows_386.exe
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
upx: netspy_windows_386.exe: FileNotFoundException: netspy_windows_386.exe: No such file or directory

Packed 0 files.
Build netspy_darwin_amd64 ...
darwin GOARCH=amd64 go build -tags all --ldflags= -o output/netspy_darwin_amd64
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
   6497968 ->   3293200   50.68%   macho/amd64   netspy_darwin_amd64

Packed 1 file.


$ ls output
netspy_darwin_amd64      netspy_linux_386         netspy_linux_amd64       netspy_windows_amd64.exe
```

当我们进入内网后想要扩大战果，那我们可能首先想知道当前主机能通哪些内网段。

netspy正是一款应用而生的小工具，体积较小，速度极快，支持跨平台，支持多种协议探测，希望能帮到你！

## 🚀 快速使用
1. 查看帮助信息
    ```bash
    netspy -h
    ```

2. 使用icmpspy模块进行探测

    ```bash
    netspy icmpspy
    ```
   注：当没有权限发送icmp包时可以尝试使用arpspy模块。

3. 使用arpspy模块进行探测
    指定使用eth0网络接口进行arp协议探测。
    ```bash
    netspy arpspy -i eth0
    ```

4. 使用tcpspy模块进行探测

    ```bash
    netspy tcpspy -p 22 -p 3389
    ```
   注：如果不指定-p参数，netspy默认探测21, 22, 23, 80, 135, 139, 443, 445, 3389, 8080端口。

5. 使用udpspy模块进行探测

    ```bash
    netspy udpspy -p 53 -p 137
    ```
   注：如果不指定-p参数，netspy默认探测53, 123, 137, 161, 520, 523, 1645, 1701, 1900, 5353端口。

## 😸 帮助信息

```text

               __
  ____   _____/  |_  ____________ ___.__.
 /    \_/ __ \   __\/  ___/\____ <   |  |
|   |  \  ___/|  |  \___ \ |  |_> >___  |
|___|  /\___  >__| /____  >|   __// ____|
     \/     \/          \/ |__|   \/
version: 0.0.1

NAME:
   netspy - powerful intranet segment spy tool

USAGE:
   netspy.exe  [global options] command [command options] [arguments...]

COMMANDS:
   icmpspy, is   使用icmp协议探测
   pingspy, ps   使用ping命令探测
   arpspy,  as   使用arp协议探测
   tcpspy,  ts   使用tcp协议探测
   udpspy,  us   使用udp协议探测
   version, v    显示版本信息
   help, h       实现帮助信息

GLOBAL OPTIONS:
   --net value, -n value      指定探测网段(172,192,10,all) (默认: "all")
   --number value, -g value   指定IP末尾数字(默认: 1, 2, 254, 255)
   --thread value, -t value   并发数量(默认: 200)
   --timeout value, -m value  发包超时(默认: 3秒)
   --output value, -o value   结果保存路径(默认: "result.txt")
   --silent, -s               只显示存活网段(默认: false)
   --debug, -d                显示调试信息(默认: false)
   --help, -h                 显示帮助信息(默认: false)
```

## 🏂 计划功能

* 支持自定义网段探测

欢迎反馈贴近实战的建议！

## 😽 鸣谢

感谢网上开源的相关项目！

## 📜 免责声明

本工具仅能在取得足够合法授权的企业安全建设中使用，在使用本工具过程中，您应确保自己所有行为符合当地的法律法规。
如您在使用本工具的过程中存在任何非法行为，您将自行承担所有后果，本工具所有开发者和所有贡献者不承担任何法律及连带责任。
除非您已充分阅读、完全理解并接受本协议所有条款，否则，请您不要安装并使用本工具。
您的使用行为或者您以其他任何明示或者默示方式表示接受本协议的，即视为您已阅读并同意本协议的约束。

## 💖Star趋势

[![Stargazers over time](https://starchart.cc/shmilylty/netspy.svg)](https://starchart.cc/shmilylty/netspy)
   
