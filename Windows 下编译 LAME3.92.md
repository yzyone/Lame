
### Windows 下编译 LAME3.92 ###

---

文章目录

Mingw-w32 编译环境

Mingw-w64 编译环境

Win-builds 编译环境

MSYS2 运行环境

Cygwin 运行环境

编译 LAME

使用 LAME

发表评论

一、Mingw-w32 编译环境

Mingw-w32：MinGW 是 “Minimalist GNU for Windows” 的缩写，是 Microsoft Windows 应用程序的极简主义开发环境。包含 Mingw-w32（编译环境）和 MSYS（运行环境）。

    Mingw-w32 下载：mingw-get-setup.exe

    Mingw-w32 的使用：C:\MinGW\msys\1.0\msys.bat

二、Mingw-w64 编译环境

Mingw-w64：是 mingw.org 项目的一个改进，创建这个项目是为了在 Windows 系统上支持 GCC 编译器。为了支持 64 位和新的 api ，它在2007年将其分岔。从那以后，它得到了广泛的使用和分发。

    Mingw-w64 Sourceforge.net Projects

Mingw-w64 版本：x86_64 是 64 位系统用的版本，i686 是 32 位系统用的版本。posix 通常用于跨平台，比win32兼容性好一些。seh 结尾是纯 64 位编译，sjlj 结尾是 32/64 两种编译，需加 -m32 或 -m64 参数。

Mingw-w64 的使用：一般结合运行环境使用，MSYS2 及 Cygwin 运行环境都可以安装 Mingw-w64 相关的软件包。

三、Win-builds 编译环境

Win-builds：是 Windows 下二进制包的大型发行版，由源代码构建。Win-builds 提供了一个包管理器，可以在 Windows，MSYS，Cygwin 和 Linux 上运行。它完全是免费软件。

    Win-builds 下载：win-builds-1.5.0.exe
    
    i686：source /opt/windows_32/bin/win-builds-switch
    
    x86_64：source /opt/windows_64/bin/win-builds-switch

四、MSYS2 运行环境

MSYS2：是 Windows 的软件发行版和构建平台其核心是基于现代 Cygwin（POSIX兼容层）和 MinGW-w64 的 MSYS 的独立重写，旨在与本机 Windows 软件实现更好的互操作性。 它提供了一个 bash shell，Autotools，版本控制系统等，用于使用 MinGW-w64 工具链构建本机 Windows 应用程序。

    MSYS2 Sourceforge.net Projects
    
    MSYS2 下载：msys2-x86_64-20180531.exe | msys2-i686-20180531.exe

MSYS2 镜像使用帮助

① 编辑 /etc/pacman.d/mirrorlist.mingw32 ，在文件开头添加：

	Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/i686
	Server = https://mirrors.huaweicloud.com/msys2/mingw/i686

② 编辑 /etc/pacman.d/mirrorlist.mingw64 ，在文件开头添加：

	Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/x86_64
	Server = https://mirrors.huaweicloud.com/msys2/mingw/x86_64

③ 编辑 /etc/pacman.d/mirrorlist.msys ，在文件开头添加：

	Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/msys/$arch
	Server = https://mirrors.huaweicloud.com/msys2/msys/$arch

常用命令：

    刷新软件包数据：pacman -Sy
    在线更新软件包： pacman -Syu
    安装编译程序：pacman -S gcc base-devel
    清理本地缓存：pacman -Sc
    列出软件包：pacman -Sl

五、Cygwin 运行环境

Cygwin：提供大量 GNU 和开放源码工具的合集，它们提供的功能类似于 Windows 上的 Linux 发行版。提供了大量 POSIX API 功能的 DLL (cygwin1.dll)。

    Cygwin 下载：64-bit installation | 32-bit installation
    
    创建 passwd 文件：mkpasswd -l > /etc/passwd

Cygwin 镜像使用帮助

    网易镜像站：http://mirrors.163.com/cygwin/
    阿里镜像站：https://mirrors.aliyun.com/cygwin/
    华为镜像站：https://mirrors.huaweicloud.com/cygwin/
    清华镜像站：https://mirrors.tuna.tsinghua.edu.cn/cygwin/

安装 apt-cyg 程序：lynx -source https://raw.githubusercontent.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg && install apt-cyg /bin

设定 apt-cyg 镜像源：apt-cyg mirror https://mirrors.huaweicloud.com/cygwin/

列出软件包：apt-cyg list gcc

安装软件包：apt-cyg install gcc

编译 LAME

说明：由于 LAME 3.92 版本较旧，建议使用 Mingw-w32 编译环境进行编译，其他编译环境 make 时可能会出错。

	./configure 参数说明：
    --build: the machine you are building on
    --host: the machine you are building for
    --target: the machine that GCC will produce binary for

64 bit 编译参数：

    ./configure --prefix=/home/Desen/lame392/ --build=x86_64-pc-mingw32 --host=x86_64-pc-mingw32 --target=x86_64-pc-mingw32
    ./configure --prefix=/home/Desen/lame392/ --build=x86_64-w64-mingw32 --host=x86_64-w64-mingw32 --target=x86_64-w64-mingw32

32 bit 编译参数：

    ./configure --prefix=/home/Desen/lame392/ --build=i686-pc-mingw32 --host=i686-pc-mingw32 --target=i686-pc-mingw32
    ./configure --prefix=/home/Desen/lame392/ --build=i686-w64-mingw32 --host=i686-w64-mingw32 --target=i686-w64-mingw32
    make && make install

六、使用 LAME

LAME 3.92 版本 MP3 转码音质比其他版本高。

LAME 命令参数说明：

	-k : 告诉编码器使用全带宽并禁用所有过滤器。
	-q : 算法质量设置 0...9，默认为 5，值为 2 时等同于 -h 参数，1 为最佳算法质量。
	-m : 立体声模式，s（stereo），j（joint stereo），f（forced joint stereo）。
	-b : 当与可变比特率编码 VBR 一起使用时，-b 指定要使用的最小比特率。
	-B : 指定使用 VBR/ABR 时允许的最大比特率。
	-V : VBR 质量设置 0...9，默认为 4，0 表示最高音质。
	-X : 降噪设置 0...7，默认为 0。
	--cbr : 强制使用恒定比特率。
	--abr : 打开具有 n kbits 的目标平均比特率的编码，允许使用不同大小的帧。
	--vbr-new : 算法比 --vbr-old 快两倍。

LAME 转 MP3 CBR/ABR/VBR 命令示例：

	lame -k -q 1 -m j --cbr -b 192 Alba.wav CBR.mp3
	lame -k -q 1 -m j --abr 192 -b 32 -B 320 Alba.wav ABR.mp3
	lame -k -q 1 -m j -V 3 --vbr-new -b 32 -B 320 Alba.wav VBR.mp3