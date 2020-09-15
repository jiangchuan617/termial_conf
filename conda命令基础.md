# conda命令基础 

## 1.conda 管理

```shell
# conda更新
conda update --all
# conda 版本
conda --version
# 升级当前版本的conda
conda update conda
conda update anaconda
conda update anaconda-navigator   # update最新版本的anaconda-navigator   
```

## 2.conda环境管理

```shell

# 查看conda 环境
conda env list
# 新建环境
conda create --name ***
conda create -n *** python=3.6
# 激活环境与退出环境
source activate ****              //开启****环境
source deactivate                  //关闭环境
# 克隆环境
conda create -n *** --clone *** 
# 删除环境
conda remove -n *** --all
```

## 3.包管理

```shell
# 查找包
conda search ***
# 安装包
conda install ***  # 安装在当前环境
conda install --name envs *** 安装到envs环境中
# 卸载包
conda uninstall ***   #卸载xxx文件包
# 在envs环境中移除包
conda remove -n envs ****
# 查看安装了哪些包
conda list
```

## 4.清华镜像的路径设置

修改用户目录下的 `.condarc` 文件:

```
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

## 5.卸载anaconda

```shell
conda install anaconda-clean
anaconda-clean

# 删除备份
rm -r /Users/jiangfeng/.anaconda_backup/
rm -rf ~/anaconda3
# 删除.zshrc .bash_profile中的环境变量
# added by Anaconda3 5.2.0 installer
export PATH="/Users/jiangfeng/anaconda3/bin:$PATH"
```



## 6.jupyter notebook 插件

```shell
conda install -c conda-forge jupyter_contrib_nbextensions
```

参看网站 

<https://github.com/ipython-contrib/jupyter_contrib_nbextensions>

每次新建`env`都需要重新安装`ipython jupyter autopep8`

```shell
conda create -n *** python=3.6
conda activate ***
conda install ipython
conda install jupyter
conda install autopep8
```

