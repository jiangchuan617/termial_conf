sftp

```shell
# 登陆
sftp jiangf@166.111.72.220
# 查看本地路径
lpwd
# 查看远程路径
pwd
# 将本地上传给远端
put -r local_path remote_path
# 将远端文件下载
get -r remote_path local_path
```

