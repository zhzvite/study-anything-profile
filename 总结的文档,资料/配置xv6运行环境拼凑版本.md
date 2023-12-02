# **前言:这是师傅经过彻夜的摸索总结的一条坎坷道路**

## 配置xv6的运行环境

### 安装 GCC/binutils

如果没有提前搭建好运行环境，执行 `make qemu` 就会报错。

> Error: Couldn't find a riscv64 version of GCC/binutils.

根据报错信息，可以知道我们需要 riscv64 版本的 binutils。使用 `apt search` 命令搜索相关 packages。

```text
apt search binutils  |grep binutils-riscv64
```

找到 3 个相关的 packages.

- binutils-riscv64-linux-gnu
- binutils-riscv64-linux-gnu-dbg
- binutils-riscv64-unknown-elf

使用 `apt install` 命令安装上面三个 packages。

```text
sudo apt install binutils-riscv64-linux-gnu
sudo apt install binutils-riscv64-linux-gnu-dbg
sudo apt install binutils-riscv64-unknown-elf
```

安装成功后，执行 `make qemu` 命令，提示如下报错。

> make: riscv64-unknown-elf-gcc: Command not found

`riscv64-unknown-elf-gcc` 可以当作是 gcc，但是是 riscv64 版本的。

```text
sudo apt install gcc-10-riscv64-linux-gnu
```

安装之后得到 `riscv64-linux-gnu-gcc-10` 文件，进入 /usr/bin 目录，建立软连接。

```text
sudo ln -s riscv64-linux-gnu-gcc-10 riscv64-unknown-elf-gcc
```

链接[[xv6\] xv6 的运行环境搭建 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/509296983)

### **qemu**

按官网所说，下载qemu 5.1.0并解压缩

```text
wget https://download.qemu.org/qemu-5.1.0.tar.xz 
tar xf qemu-5.1.0.tar.xz
```

执行一系列指令

```text
cd qemu-5.1.0 
./configure --disable-kvm --disable-werror --prefix=/usr/local --target-list="riscv64-softmmu" 
make 
sudo make install 
cd ..
```

其中最长的那行命令可能出问题，如果报这个错误:

```text
ERROR: glib-2.48 gthread-2.0 is required to compile QEMU
```

解决方法为`sudo apt install libglib2.0-dev`

还可能报这个错误：

```text
ERROR: pixman >= 0.21.8 not present.
       Please install the pixman devel package.
```

解决方法为`sudo apt install libpixman-1-dev`

一切正常的话, 输出的最后是

```text
default devices   yes
plugin support    no
fuzzing support   no
gdb               /usr/bin/gdb
rng-none          no
Linux keyring     yes
cross containers  no
```

------

## **xv6操作系统源码**

直接clone吧，虽然速度慢，好在文件不大

```text
git clone git://g.csail.mit.edu/xv6-labs-2020
```

你可能会发现clone下来的这个文件夹是空的，别担心，git就是这样的，运行这两条指令

```text
cd xv6-labs-2020
git checkout util
```

文件夹里就有东西了，很神奇吧

链接[[6.S081\] 刷后总结与环境配置 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/544013654)

# **测试**

```bash
# 按官方指南手册 安装必须的工具链
$ sudo apt-get install git build-essential gdb-multiarch qemu-system-misc gcc-riscv64-linux-gnu binutils-riscv64-linux-gnu 
# 单独移除掉qemu的新版本, 因为不知道为什么build时候会卡壳
$ sudo apt-get remove qemu-system-misc
# 额外安装一个旧版本的qemu
$ wget https://download.qemu.org/qemu-5.1.0.tar.xz
$ tar xf qemu-5.1.0.tar.xz
$ cd qemu-5.1.0
$ ./configure --disable-kvm --disable-werror --prefix=/usr/local --target-list="riscv64-softmmu"
$ make
$ sudo make install

# 克隆xv6实验仓库
$ git clone git://g.csail.mit.edu/xv6-labs-2020
$ cd xv6-labs-2020
$ git checkout util

# 进行编译
$ make qemu
# 编译成功并进入xv6操作系统的shell
$ xv6 kernel is booting

$ hart 2 starting
$ hart 1 starting
$ init: starting sh
$ (shell 等待用户输入...)
 
# 尝试一下ls指令
$ ls
.              1 1 1024
..             1 1 1024
README         2 2 2226
xargstest.sh   2 3 93
cat            2 4 23680
echo           2 5 22536
forktest       2 6 13256
grep           2 7 26904
init           2 8 23320
kill           2 9 22440
ln             2 10 22312
ls             2 11 25848
mkdir          2 12 22552
rm             2 13 22544
sh             2 14 40728
stressfs       2 15 23536
usertests      2 16 150160
grind          2 17 36976
wc             2 18 24616
zombie         2 19 21816
console        3 20 0
```

至此, 实验环境设立完成, 我们成功boot了**xv6**这个简易操作系统.

本实验中, 因为实现的都是用户侧的函数, 所以比较懒惰的我忽略了不少系统调用的错误返回值检查. 希望大家不要学我.

链接[MIT 6.S081 Operating System  - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/624091268)