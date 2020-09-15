# conda环境U盘移植说明

## 步骤一：清华服务器移植到U盘

1. 将base环境克隆一份，比如克隆成zc_test

   ```shell
   conda create -n zc_test --clone base
   ```

   由于base环境一般在anaconda/bin目录下，直接拷贝bin可能会出现问题，因此建议创建虚拟环境zc_test并拷贝

2. 将环境拷贝到U盘

   ```shell
   # cd U盘路径下
   cd /Volumes/GSP1RMCULFR
   # 拷贝环境
   scp -r zcqz@166.111.73.48:anaconda3/envs/zc_test ./
   ```
   
3. 将清华服务器上的anaconda3/pkgs文件拷贝到U盘

   ```shell
   # 在U盘路径下
   cp -r  zcqz@166.111.73.48:anaconda3/pkgs ./
   ```

   

## 步骤二：从U盘拷贝到中船服务器上

1. 首先将中船服务器中的pkgs文件夹备份，并删除pkgs文件夹

   ```shell
   cp -r anaconda3/pkgs anaconda3/pkgs_bak
   # 删除pkgs，由于部分文件被保护，建议使用sudo删除
   rm -r anaconda3/pkgs
   ```

   

1. 将数据从U盘上拷贝到中船的anacnda/envs目录下

   ```shell
   # 进入U盘路径
   cd linux下/U盘路径
   # 将pkgs文件拷贝至中船服务器上的anaconda3文件夹内
   cp -r pkgs ~/anaconda3/
   conda create -n zc_test --clone ./zc_test --offline
   
   ```

2. 激活该环境

   ```shell
   source activate
   # 等待命令行中显示已处于`(base)`字样，执行
   
   #执行
   conda activate zc_test
   
   # 如果遇到问题，可以尝试重启服务器；
   ```

   

## 下面是服务器网络连接下的conda环境移植说明



假设

​		已部署服务器为`A`，用户为`a_user`;

​		待部署服务器为`B`，用户为`b_user`；

### 步骤一

如果服务器`A`开发环境为虚拟环境，则不需要执行本步骤；

当开发环境为base环境，首先需要对base环境进行clone；

```shell
# 格式为: conda create -n envs_name --clone base
conda create -n zc_test --clone base
```

### 步骤二

在服务器`B`上安装anaconda3

安装路径为：`/home/b_user/anaconda3/`

具体安装可查阅相关教程；

### 步骤三

将服务器`A`中的虚拟环境通过`scp`复制到服务器`B`的anaconda的虚拟环境文件夹下

从服务器B执行 scp命令

```shell
scp username@192.168.73.100:/home/a_user/anaconda3/envs/zc_test /home/b_user/anaconda3/envs/
```

**注意：只能通过scp传输，U盘或者其他传输媒介拷贝会报错。**

### 步骤四

激活服务器`B`上的虚拟环境

执行

```shell
source activate
```

等待命令行中显示已处于`(base)`字样，执行

```
conda activate zc_test
```

激活服务器`B`上的虚拟环境；

如果遇到问题，可以尝试重启服务器；