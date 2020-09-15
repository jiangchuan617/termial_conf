## Conda 环境移植说明

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