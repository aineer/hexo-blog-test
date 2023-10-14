---
layout: post
title: Arch Linux 安装教程
author: Two
catrgories: jekyll
tags: ArchLinux GNU/Linux 自由软件 操作系统
---

# Arch Linux 安装教程

## 更新于2023年10月11日

### 版本：1.1

### 维护者：two

## 01：开始前

### 本文讲述如何在你的 x86-64 计算机上安装Arch Linux 操作系统和一系列配置

#### 注：本文目标用户是新手，建议有能力的用户去看 Arch Linux Wiki 的 [Installation_guide](https://wiki.archlinux.org/title/Installation_guide "Installation_guide") 以获得最好的指导

## 02：安装条件

### · 准备条件

1. 一台x86-64的计算机，支持UEFI启动和GPT分区表
2. 一个可移动U盘设备
3. 一个可以正常使用的操作系统
4. 超过30G的空闲硬盘空间
5. 一颗折腾的心

## 03：准备

### 注：这里先下载 Arch Linux ISO 然后使用软件烧录到U盘

使用原有的 Windows 或者 GNU/Linux 操作系统打开 [Arch Linux ISO下载页](https://archlinux.org/download/ "Arch Linux ISO")，国内用户可以选择一个合适的镜像源下载 Arch Linux ISO 文件。
下面是国内常用的提供 Arch Linux 安装镜像的开源镜像站（选一个即可）

1. **[中国科学技术大学开源镜像站](https://mirrors.ustc.edu.cn/)**
2. **[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/)**
3. **[华为开源镜像站](https://repo.huaweicloud.com/archlinux/)**
4. **[兰州大学开源镜像站](https://mirror.lzu.edu.cn/archlinux/)**

比如我这里用 tuna 的 [Arch Linux ISO](https://mirrors.tuna.tsinghua.edu.cn/archlinux/iso/2023.09.01/) 镜像站：

![tuna](/_data/images/2023-10-11-arch-linux-insatll_img/tuna-arch-iso.png)

下载 archlinux-2023.09.01-x86-64.iso 文件（在写文章时时间是9月11日，arch iso 是每月月初发布的，发布时会将文件名替换为发布的日期，和文章记载时间有出入所以读者下载时最好下载本月月初发布的最新的iso文件以获得最新的补丁）。

下载好后准备烧录iso文件到U盘。插入U盘设备到你的计算机。这里用的U盘启动工具是Ventoy。Windows用户下载安装包然后解压开。双击执行Ventoy2Disk.exe 选择磁盘设备，然后点击安装按钮即可。

如图：

![ventoy img](/_data/images/2023-10-11-arch-linux-insatll_img/ventoy_install.png)

点安装

![安装完成](/_data/images/2023-10-11-arch-linux-insatll_img/ventoy_install_done.png)

完成
然后把下载的 Arch Linux ISO 文件移动/复制到新格式化的U盘里。

自此U盘烧录就完成了。

### 注：下面要划分空硬盘分区用来储存Arch Linux操作系统和文件。划分硬盘时要小心不要搞错了，丢失数据就麻烦了。划分时如果有充足的硬盘空间建议给多点如果要长期使用建议128G以上（这里是Arch Linux和Windows双系统方案）如果想单硬盘安装Arch Linux可以等进入到live cd 环境里全盘格式化，也就是说可以跳过下面这一步。但是双系统还是单硬盘安装取决于你的需求

Windows 10里右键点击 「开始菜单」 > 点击 「磁盘管理」

右键点击 「需要压缩的分区」 > 点击 「压缩卷」

![disk_manager](/_data/images/2023-10-11-arch-linux-insatll_img/disk_manager.avif)

在输入「压缩空间量\(MB\)」里输入你想要为 Arch Linux 分配的空间，我这里是128G。

![compression](/_data/images/2023-10-11-arch-linux-insatll_img/compression.webp)

点压缩，然后关闭 Windows 磁盘管理程序。

### 注：不要在这里做多余的操作，也不要划分多个或以上的分区

自此空硬盘划分就完成了

### 注：下面要在BIOS（Basic Input/Output System）里关闭安全启动（Secure Boot），然后把准备安装Arch Linux的U盘调整到第一启动顺序

### 注：接下来的操作需要关闭你的计算机，请事先保存好待保存的数据

重启后进入BIOS。以华硕主板为例开机显示logo时摁F2进入BIOS，其他的主板可以在互联网上搜索「**xx主板如何进入BIOS**」，一般会有你想要的答案。

进入BIOS后找到「Secure Boot」然后选择「disabled」将其禁用。 然后找到「boot」选项拦里将安装U盘调整为第一启动项然后保存退出（一般是F10，看具体的主板）。 自此准备工作就完成了，下面就重启进入到安装U盘里面，准备安装Arch Linux！

### 注：为了方便撰写文章和演示（截图），我这里用的是Oracle VM VirtualBox 虚拟机安装Arch Linux（放心和你在物理机安装步骤是一样的。）

### 注：Arch Linux安装盘应该一直插在电脑上

重启计算机到 Ventor 的引导界面，然后点击 Arch Linux ISO 进入到 grub 里面点击第一个条目也就是「Arch Linux install medium（x86-64，UEFI）」回车。

![archlinux_grub_setup](/_data/images/2023-10-11-arch-linux-insatll_img/uefi_grub_setup.png)

![start](/_data/images/2023-10-11-arch-linux-insatll_img/start.png)

进入到安装界面。

## 04：安装

### 注：下面进入到正式的 Arch Linux 安装教程

### 教程分几步

1. [禁用 reflector](#1)
2. [验证引导模式](#2)
3. [联网](#3)
4. [测试网络连通性](#4)
5. [同步时间](#5)
6. [更换镜像源](#6)
7. [磁盘分区](#7)
8. [格式化](#8)
9. [挂载](#9)
10. [安装基本系统和软件](#10)
11. [生成 fstab 文件](#11)
12. [Chroot root](#12)
13. [设置主机名和时区](#13)
14. [硬件时间设置](#14)
15. [设置 Locale](#15)
16. [设置 root 密码](#16)
17. [安装微码](#17)
18. [安装和设置引导程序](#18)
19. [重启到新系统](#19)

下面根据这些步骤进行安装。

## > 禁用 reflector 服务 {#1}

Reflector 根据 Arch Linux Wiki 的描述是：

*Reflector is a Python script which can retrieve the latest mirror list from the Arch Linux Mirror Status page, filter the most up-to-date mirrors, sort them by speed and overwrite the file /etc/pacman.d/mirrorlist.*

中译：
Reflector 是一个 Python 脚本；它从 Arch Linux Mirror Status 页面获取最新的镜像列表，然后筛选出最新的镜像并按速度排序，最后将结果写入到 /etc/pacman.d/mirrorlist 文件。

### 注：reflector 是一个好工具，他会帮你筛选出最新的镜像然后写入到 mirrorlist 里。但是在中国这种封闭的网络环境可能并不适用，所以将其禁用

```bash
systemctl stop reflector
```

![stop](/_data/images/2023-10-11-arch-linux-insatll_img/stop.png)

## > 验证引导模式 {#2}

再次验证身份是 UEFI 模式启动：

```bash
ls /sys/firmware/efi/efivars/
```

![efivars](/_data/images/2023-10-11-arch-linux-insatll_img/efi_var.png)

可以看到输入了一堆EFI变量，代表当前是UEFI启动。（如果是传统BIOS 启动可能根本不会有这个目录）。

## > 联网 {#3}

Arch Linux 的安装需要联网。

如果你是虚拟机安装同时虚拟网卡配置正常宿主机也连上网络，那么正常情况已经有网络了，也就是可以跳过这一步。

如果是有线连接只要插上一个联网的路由器的网线（DHCP），直接就能联网。也可以跳过这一步。

这里主要指无线连接：

```bash
    iwctl
    # 进入iwctl命令行
    device list
    # 扫描无线网卡名称
    station wlan0 scan
    # 扫描网络，这里的「wlan0」看具体的设备名，也就是看device list的输出
    station wlan0 get-networks
    # 列出wifi
    station wlan0 connect $WIFI-NAME
    #连接Wi-Fi，这里的 $WIFI-NAME 看具体连接的 Wi-Fi 名，不要跟着敲
    exit
    # 退出  
```

### 注：「#」开头的是注释是为了方便读者理解加的，不用敲上

## > 测试网络连通性 {#4}

```bash
ping -c 4 www.baidu.com
```

![ping baidu.com](/_data/images/2023-10-11-arch-linux-insatll_img/ping_net.png)

如果显示超时的话请回到联网一节重新连接。

## > 同步时间 {#5}

同步系统时间是**非常重要**的。系统时间不正确时有些应用程序甚至无法正常执行。这里用 timedatectl 同步时间。

```bash
timedatectl set-ntp true
```

![sync_time](/_data/images/2023-10-11-arch-linux-insatll_img/sync_time.png)

## > 更换镜像源 {#6}

在安装过程中，推荐使用一个国内的镜像站来加快下载速度。

用 vim 或者你喜欢的编辑器编辑该文件

在 vim 编辑器里摁「i」进入插入模式，开始编辑文件。通过h、j、k、l进行左、下、上、右移动，编辑完成后摁「ESC」回到命令模式，输入「:wq」保存退出。

```bash
vim /etc/pacman.d/mirrorlist
```

推荐的源如下：

```bash
Server = https://mirroes.ustc.edu.cn/archlinux/\$repo/os/\$arch
# 中科大源
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/\$repo/os/\$arch
# 清华源
```

如图：
![mirror](/_data/images/2023-10-11-arch-linux-insatll_img/mirror_list.png)

## > 磁盘分区 {#7}

这里我用的分区分案是：
・/boot分区分400M。
・swap单独一个分区，大小一般建议是物理内存的两倍。
・/ 和 /home 同一个分区，用 btrfs 子券来管理/ 和 /home，分其他剩余的全部硬盘空间。

```bash
lsblk # 查看你的分区配置和信息
```

![lsblk](/_data/images/2023-10-11-arch-linux-insatll_img/lsblk_message.png)

准备分区

```bash
cfdisk /dev/nvmeXn1 
# 不要完全照着我输入命令，NVMe的硬盘最后的X只是代表如a、b、c、d的符号请根据 lsblk 的输出自行判断）
```

cfdisk 是一个磁盘分区工具，用来方便的进行磁盘分区。

![partiton lable typw](/_data/images/2023-10-11-arch-linux-insatll_img/select_label_table.png)

分区表类型视情况选择（近年的新硬盘一般是GPT）。用你键盘的方向键选中，选中好摁Enter。这里选择GPT。

![paretion](/_data/images/2023-10-11-arch-linux-insatll_img/cfdisk_parttion.png)

通过方向键 ↑ 和 ↓ 可以在要操作磁盘分区移动；通过方向键 ← 和 → 在对当前高亮的磁盘分区或空余空间将要执行的操作中移动。

如上图的「Free space」是指未分配的磁盘空间（也就是你在Windows用磁盘分区工具分配的空间），我们要为它分区。

首先是 /boot 分区，用来储存启动信息，这里分400M，BIOS 引导可以不分 /boot分区，但是 uefi 必须有一个分区作为efi分区。双系统（Arch Linux + Windows）可以不分 /boot分区，双系统启动时 kernel 直接将Windows的efi分区挂载到 /boot。但是 **Windows的efi分区大小只有100M-200M左右，在Windows 10、Windows 11 很可能出现分区大小不足的情况。** 所以这里还是分了单独的 /boot分区。

选中「Free Space」> 再选中操作「New」> 然后按下回车「Enter」以新建分区。摁下Enter后左下角的「Partition size」是叫你输入分区大小（单位可以是MB或者是GB等等）这里输入400MB后摁Enter，成功新建分区。默认新建的分区类型是linux filesystem，我们需要将类型更改为EFI System。用方向键←、→选中操作[Type] > 然后按下Enter > 通过方向键 ↑ 和 ↓ 选中 EFI System > 最后按下 Enter。

![efi](/_data/images/2023-10-11-arch-linux-insatll_img/select_table_efi.png)

然后分交换分区。再次选中「Free Space」 > 再选中操作「New」 > 然后按下回车「Enter」以新建swap分区（内存快满时，会将一部分空闲内存转移到 swap 分区）

这里输入2G（一般我建议小于或等于16G分内存的二分之一倍或者是内存两倍，如果你内存够大甚至可以不用分）后摁Enter，成功新建分区。默认新建的分区类型是linux filesystem，我们需要将类型更改为Linux swap。用方向键←、→选中操作[Type] > 然后按下Enter > 通过方向键 ↑ 和 ↓ 选中 Linux swap > 最后按下 Enter。

![swap](/_data/images/2023-10-11-arch-linux-insatll_img/select_table_swap.png)

接下来要在分一个分区当根目录，因为这里文件系统使用btrfs所以**不需要分单独的/home分区**，只需要用子卷来划分 / 和 /home 就好。

这里我分配了剩下的全部空间当根目录（根据实际情况）。然后分区类型就是「linux filesystem」不需要更换。

![mnt](/_data/images/2023-10-11-arch-linux-insatll_img/select_table_mnt.png)

分区完毕，用方向键选中[Write]，然后左下角提示你是否确定写入，检查分区无误（**一定要耐心检查，不要搞错了不然很可能会丢失数据**）后输入“yes”然后摁 Enter 写入。 写入后完毕用方向键选中[Quit]退出 cfdisk 分区工具。

分区结束。

退出后再次用 lsblk 检查磁盘分区有无错误。（这里sda下面的sda1、sda2、sda3都是我刚才的分区，以实际情况为准）

![lsblk](/_data/images/2023-10-11-arch-linux-insatll_img/lsblk_parttion_message.png)

## > 格式化 {#8}

分好区然后把它们格式化成对应文件系统的格式

### 注：格式化是危险的操作会清除你当前分区的数据，进行操作前要一定细心检查操作是否无误，不然丢失数据就麻烦了，切记切记

首先是对应的 efi 分区：

```bash
mkfs.fat -F32 /dev/sdxn # 看你自己的分区，这里是sda1
```

![efi](/_data/images/2023-10-11-arch-linux-insatll_img/mkfs_efi.png)

然后是对应的 swap 分区：

```bash
mkswap /dev/sdxn
```

![swap](/_data/images/2023-10-11-arch-linux-insatll_img/mkfs.swap.png)

最后格式化btrfs分区

```bash
mkfs.btrfs -L ArchLinuxFileSystem /dev/sdxn
```

### 注：-L后指定该分区的表（可以理解为名字），这里是ArchLinuxFileSystem。可以自定义，但不能使用特殊字符以及空格

![btrfs](/_data/images/2023-10-11-arch-linux-insatll_img/mkfs_btrfs.png)

为了创建字卷要先挂载到/mnt

```bash
mount -t btrfs -o compress=zstd /dev/sdxn /mnt
### 注意/dev/sdxn要看你的情况
```

```bash
df -h
```

![df -h](/_data/images/2023-10-11-arch-linux-insatll_img/df-message.png "可以看到（这里是/dev/sda3）已经挂载上/mnt了")

创建 @/ 和 @home 两个子卷，字卷名字可以任意。这里叫 @/ 和 @home，是因为「timeshift」快照工具只认这种字卷名，如果你不打算用 timeshift 来创建和管理 btrfs 快照）也可以取其他的快照名。

```bash
btrfs subvolume create /mnt/@
# 创建 / 子卷
btrfs subvolume create /mnt/@home
# 创建 /home 子卷
```

![subvolume](/_data/images/2023-10-11-arch-linux-insatll_img/create_subvolume.png "创建字卷")

检查一下

```bash
btrfs subvolume list -p /mnt
```

![list subvolume](/_data/images/2023-10-11-arch-linux-insatll_img/list_subvolume.png "检查字卷情况")

完毕后卸载 /mnt，以便接下来挂载

```bash
umount /mnt
```

## > 挂载 {#9}

挂载格式好的分区到 /mnt，/mnt里面的就是你安装的系统。

**按下面的顺序来 —— 要先挂/mnt。注意不要打错了，要挂载的分区名字也要看你的情况写。**

```bash
mount -t btrfs -o subvol=/@,compress=zstd /dev/sdxn /mnt # 挂载 /
mkdir /mnt/home # 创建 /home 目录 
mount -t btrfs -o subvol=/@home,compress=zstd /dev/sdxn /mnt/home # 挂载 /home 
mkdir -p /mnt/boot/efi # 创建 /boot/efi 目录 
mount /dev/sdxn /mnt/boot/efi # 挂载 /boot/efi 目录
swapon /dev/sdxn # 启动交换分区
```

![mount_to_mnt](/_data/images/2023-10-11-arch-linux-insatll_img/mount_parttion_to_mnt.png "不要挂载错了哦😮")

挂载完毕后检查下：

```bash
lsblk 
```

![cleck /mnt](/_data/images/2023-10-11-arch-linux-insatll_img/lsblk_cleck_mnt.png "要确认好才继续")

查看下 swap 分区的情况：

```bash
free -h
```

![cleck swap](/_data/images/2023-10-11-arch-linux-insatll_img/free_cleck_swap.png "要确认好才继续")

## > 安装基本系统和软件 {#10}

使用 pacstrap 脚本安装基础包、内核、固件包和其他常用工具：

```bash
pacstrap /mnt base base-devel linux linux-firmware btrfs-progs networkmanager vim sudo 
```

### 用 btrfs 额外装 btrfs-progs 包，可以把 vim 切换成你喜欢的编辑器比如 Emacs或者 Nano

![insatll base system](/_data/images/2023-10-11-arch-linux-insatll_img/pacstrap_insatll_base_system.png)

## > 生成fstab文件 {#11}

fstab 文件可用于定义磁盘分区，各种其他块设备或远程文件系统应如何装入文件系统。 关于更多fstab的信息可以看[这里](https://wiki.archlinux.org/title/Fstab)

```bash
genfstab -U /mnt > /mnt/etc/fstab # 用 arch-install-script 脚本提供的 genfstab 脚本方便的生成 fstab 文件
```

检查下生成的fstab文件是否有误：

```bash
cat /etc/fstab
```

![fstab](/_data/images/2023-10-11-arch-linux-insatll_img/fstab_message.png)

输出结果应该类似。

## > Chroot root {#12}

切换到新安装好的 Arch Linux系统

```bash
arch-chroot /mnt # 可以看到原来的/mnt 变成了 /
```

![arch-chroot](/_data/images/2023-10-11-arch-linux-insatll_img/arch-chroot.png)

## > 设置主机名和时区 {#13}

```bash
vim /etc/hostname
```

文件写上你的主机名（最好有意义），这里我的主机的名字是 live-arch

![hostname](/_data/images/2023-10-11-arch-linux-insatll_img/hostname.png)

然后在/etc/hosts文件这样写：

```bash
vim /etc/hosts 
```

```bash
127.0.0.1 localhost
::1 localhost
127.0.0.1 live-arch.localdomain live-arch
```

![hosts](/_data/images/2023-10-11-arch-linux-insatll_img/hosts_file.png)

**注意这里的 live-arch 要替换成自己的主机名**
创建时区的符号链接，这里是上海（没有北京）

```bash
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

## > 硬件时间设置 {#14}

```bash
hwclock --systohc # 同步硬件时间
```

## > 设置 Locale {#15}

Locale 决定了软件使用的语言、书写习惯和字符集。

```bash
vim /etc/locale.gen
```

用 / 搜索然后去掉「en_US.UTF-8 UTF-8」以及「zh_CN.UTF-8 UTF-8」行前的注释（#）

输入以下命令生成Locale：

```bash
locale-gen
```

![locale-gen](/_data/images/2023-10-11-arch-linux-insatll_img/locale-gen.png)

向 /etc/locale.conf 输入内容：

```bash
echo 'LANG=en_US.UTF-8' > /etc/locale.conf
```

## > 设置root密码 {#16}

```bash
passwd root
```

第一次是输入新密码 第二次是重新输入新密码

### 注：密码输入时是看不到的，不要以为是键盘或者系统坏了

## > 安装微码 {#17}

来自 archcn wiki：

*处理器制造商会发布对处理器微码的稳定性和安全性更新。这些更新提供了对系统稳定性至关重要的错误修复。如果没有这些更新，则可能会遇到不明原因的崩溃或难以跟踪的意外停机。
使用 AMD 或 Intel CPU 的用户都应该安装微码更新以确保系统稳定性。在虚拟机或容器中时,微码更新应在主机上实施,而不是客户机。*

可以看到 wiki 建议安装和更新微码保持系统稳定性。

如果是 Intel CPU 执行以下命令：

```bash
pacman -S intel-ucode # intel
```

如果是 AMD CPU 执行以下命令：

```bash
pacman -S amd-ucode # amd 
```

## > 安装和设置引导程序 {#18}

这里用 grub（GRand Unified Bootloader）引导程序来引导新安装的Arch Linux。
也可以参考 [wiki](https://wiki.archlinux.org/title/GRUB)

先安装grub和其他常用程序：

```bash
pacman -S grub efibootmgr os-prober
# grub用来引导、efibootmgr将启动项写入NVRAM、os-prober用来引导多系统
```

安装grub

```bash
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=live-arch
```

### --efi-directory=/boot/efi 是将grubx64.efi安装到指定的目录（这里是 /boot/efi）

### --bootloader-id=live-arch 是取名为 live-arch（你也可以叫其他的）

![grub-insatll-done](/_data/images/2023-10-11-arch-linux-insatll_img/grub-insatll-done.png)

然后做一些**可选**的小配置

```bash
vim /etc/default/grub
```

打开 /etc/default/grub文件去掉「GRUB_CMDLINE_LINUX_DEFAULT」行中的「quiet」参数。

在「GRUB_CMDLINE_LINUX_DEFAULT」行加入「nowatchdog」[内核参数](https://wiki.archlinux.org/title/Kernel_parameters)禁用[内核看门狗](https://wiki.archlinux.org/title/Improving_performance#Watchdogs)。

取消最后一行「#GRUB_DISABLE_OS_PROBER=false」行的注释，因为现在的 os-prober 默认不开启引导其他操作系统，需要取消这行的注释。

编辑完成后如下：

![grub-cfg](/_data/images/2023-10-11-arch-linux-insatll_img/grub_edit.png)

![enable_prober](/_data/images/2023-10-11-arch-linux-insatll_img/enable_os_prober.png)

执行 grub-mkconfig -o /boot/grub/grub.cfg 生成grub的配置文件：

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

结果大概如下：

![grub-mkconfig](/_data/images/2023-10-11-arch-linux-insatll_img/grub-mkconfig_done.png)

### 注：这里没有引导到 Windows 和其他操作系统是正常现象，是 os-prober 的bug。只需要等下重启后在新安装的系统里再一次执行「grub-mkconfig -o /boot/grub/grub.cfg 」命令即可

## > 重启到新系统 {#19}

### 到激动人心的时刻了

```bash
exit           # 退出 chroot 环境 
umount -R /mnt #卸载/mnt
reboot         # 重启 
```

这个时候可以拔掉U盘了。

![setup-to-grub](/_data/images/2023-10-11-arch-linux-insatll_img/new-arch-setup-to-grub.png)

选择「Arch Linux」项。

Enter

![login](/_data/images/2023-10-11-arch-linux-insatll_img/login_to_system.png)

进入系统后在「archlinux login」里输入你的用户名（这里是root），然后 Enter 输入密码（密码是不可见的）。输入完毕摁 Enter 然后登入系统。

```bash
systemctl enable --now NetworkManager # 启动NetworkManager
```

如果是有线连接已经连接上了

```bash
ping -c 4 baidu.com # 测试连接 
```

如果是无线连接：

```bash
nmcli dev wifi list # 显示附近的 Wi-Fi 网络 
nmcli dev wifi connect "Wi-Fi名" password "密码" # 类似这样
ping -c 4 baidu.com # 测试连接 
```

```bash
pacman -S neofetch # 最后可以安装neofetch
```

```bash
neofetch
```

![neofetch](/_data/images/2023-10-11-arch-linux-insatll_img/neofetch_to_system_message.png "帅气的Arch Logo")

恭喜你，你成功在你的计算机上安装了Arch Linux 操作系统

这篇 Arch Linux 安装教程就结束了。

## > 05：后记

这就是在 x86-64 CPU 架构 Arch Linux操作系统基本安装的内容。

如果有空我会在出一篇安装图形桌面环境和针对日常使用配置的文章。

这篇文章只是本人无聊一时兴起写的，内容不像 Arch Wiki 那样系统全面。最后还是推荐看 Arch Linux Wiki 获得最详细的安装和配置指导。

**最后希望大家在使用 GNU/Linux 和 Arch Linux 发行版以及自由及开放源代码软件的过程中感受到快乐。**

**谢谢观看。**
