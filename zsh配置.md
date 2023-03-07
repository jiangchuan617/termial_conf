

# zsh的安装

```shell
# 切换bash
chsh -s /bin/bash
# 切换zsh
chsh -s /bin/zsh
# 查看所有shell
cat /etc/shells
# 查看当前shell
echo $SHELL
```

# conda配置

在 .zshrc最后加上 

```shell
# 使conda 生效
source .bash_profile 
#  进入虚拟环境
conda activate t
```



## 代码补全(不建议)

### inrc

下载地址：http://mimosa-pudica.net/zsh-incremental.html

文件位置：

```shell
/Users/jiangfeng/.oh-my-zsh/plugins/incr
```

在`.zshrc`中添加`source $ZSH/plugins/incr/incr*.zsh`



### zsh-autosuggestions

https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

.zshrc中添加

```
plugins=(zsh-autosuggestions)
```

### zsh-syntax-highlighting

https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

.zshrc中添加

```
plugins=( [plugins...] zsh-syntax-highlighting)
```

直接复制

```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

