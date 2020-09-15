# Ubuntu安装配置

主要在Ubuntu18.04上配置

## 设置root密码

sudo passwd root

输入设置的root密码

## 更改源

清华源

https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

/etc/apt/sources.list

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-proposed main restricted universe multiverse
```

更新

sudo apt update

sudp apt upgrade

## 安装搜狗输入法

### 安装fcitx

sudo apt-get install fcitx-bin

相关的依赖库和框架都会自动安装上

sudo apt-get install fcitx-table

配置fcitx

Language中修改ibus为fcitx

重启

### 安装搜狗输入法

下载 https://pinyin.sogou.com/linux/

安装

### 输入法配置

![在这里插入图片描述](https://tva1.sinaimg.cn/large/006tNbRwly1g9o22chxl1j30850e6aaj.jpg)

选择: Configure

![在这里插入图片描述](https://tva1.sinaimg.cn/large/006tNbRwly1g9o22p14lkj30nl0d03zl.jpg)

点击 +
找到 Sogou Pinyin, 添加
如果找不到，等几分钟或者重启试试

完成

## 安装chrome

下载

http://www.ubuntuchrome.com/

安装

## 挂载exfatU盘

sudo apt install exfat-utils

## 安装驱动

### 禁用nouveau

在/etc/modprobe.d/blacklist.conf里添加，如下内容，并执行 `sudo update-initramfs -u`

```
blacklist nouveau
options nouveau modeset=0
```

重启后用`lsmod | grep nouveau`,如果没有任何输出说明禁用成功。

### 直接输入如下命令：

```
$ sudo ubuntu-drivers autoinstall
```

验证是否安装成功：
 `$ nvidia-smi`

如果显示显卡相关信息则表示安装成功

如果需要安装新版本的驱动可以先添加源：

```ruby
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
```

然后执行：

```cpp
$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:02.0/0000:05:00.0 ==
modalias : pci:v000010DEd00001C82sv000019DAsd00002456bc03sc00i00
vendor   : NVIDIA Corporation
model    : GP107 [GeForce GTX 1050 Ti]
driver   : nvidia-driver-410 - third-party free
driver   : nvidia-driver-415 - third-party free
driver   : nvidia-driver-390 - distro non-free
driver   : nvidia-driver-418 - third-party free
driver   : nvidia-driver-396 - third-party free
driver   : nvidia-driver-430 - third-party free recommended
driver   : xserver-xorg-video-nouveau - distro free builtin
Selecting previously unselected package nvidia-dkms-430.
```

最后安装

```shell
$ sudo apt install nvidia-driver-430
```

### 或者下载安装

sudo ./Nivida....

## 安装cuda

sudo ./....run

![在这里插入图片描述](https://tva1.sinaimg.cn/large/006tNbRwly1g9pbd0kysnj30e108e0t9.jpg)

### 添加环境变量

`vi ~/.bashrc`

### 在文件末尾添加

```shell
export PATH="/usr/local/cuda-10.1/bin:$PATH" 
export LD_LIBRARY_PATH="/usr/lcoal/cuda-10.1/lib64:$LD_LIBRARY_PATH"
```

### 最后使其生效

`source ~/.bashrc`

### 检查

`Nvcc -V`

## 安装cudnn

### 下载

### 进入解压后的cudnn目录 应该能看到cuda文件夹

```
sudo cp cuda/include/cudnn.h /usr/local/cuda/include/ 
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/ 
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

### 查看cudnn版本

`cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2`

从上到下输出7 6 5 即表示cudnn7.6.5

## 安装anaconda

## 开机自动挂载硬盘

### 查看挂载信息

#### 查看UUID

sudo blkid

#### 挂载目录

磁盘挂载的路径，习惯上设置为media分区下的目录，可使用“ sudo mkdir /media/xxx"创建；

#### 挂载类型

linux 下一般是ext4,windows一般是nfts

#### 挂载参数

默认default

#### 是否备份

0或1

#### 开机自检

一般设置为2，不想自检就设置为0；挂载点为根目录的设备，设置为1；其他需要自检设置为2；

### 修改fstab文件

打开 /etc/fstab文件，填写挂载信息；

`sudo gedit /etc/fstab`

添加

`UUID = ****  /meida/jf/space/ ntfs default 0 0`

