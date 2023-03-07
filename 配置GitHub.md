# 配置GitHub

## 1.设置姓名和邮箱地址

```shell
git config --global user.name "Firstname Lastname"

git config --global user.email "your_email@example.com"
```

这个命令，会在“~/.gitconfig”中以如下形式输出设置文件。

```
[user]

name = Firstname Lastname

email = your_email@example.com
```

想更改这些信息时，可以直接编辑这个设置文件。这里设置的姓名 和邮箱地址会用在 Git 的提交日志中。由于在 GitHub 上公开仓库时，这 里的姓名和邮箱地址也会随着提交日志一同被公开，所以请不要使用不 便公开的隐私信息。

顺便一提，将 color.ui 设置为 auto 可以让命令的输出拥有更高的可 读性。

```
git config --global color.ui auto
```

“~/.gitconfig”中会增加下面一行。

```
[color]
ui = auto
```

这样一来，各种命令的输出就会变得更容易分辨。

## 2.设置 SSH Key

### 运行下面的命令创建 SSH Key。

```
ssh-keygen -t rsa -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key
(/Users/your_user_directory/.ssh/id_rsa):按回车键
Enter passphrase (empty for no passphrase):输入密码
Enter same passphrase again:输入密码
```

id_rsa 文件是私有密钥，id_rsa.pub 是公开密钥。

## 3.添加公开密钥

id_rsa.pub 的内容可以用如下方法查看。

```
cat ~/.ssh/id_rsa.pub
```

粘贴到GitHub上

> 添加成功邮箱会收到信息

#### 4.测试