## jupyter notebook 插件

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

常用的插件

- table of contents
- ExecuteTime 执行时间
- Autopep8
- Highlight select words
- hinterland 自动补全
- Collapsible headings 折叠标题下的内容



## 不显示插件，参考

https://blog.csdn.net/ybw_2569/article/details/129157284



在启动jupyter的终端，查看是否报404 缺少文件的问题

![在这里插入图片描述](./jupyter_notebook%E8%AE%BE%E7%BD%AE.assets/81eac198f59b4eb89336cbec975427bb-8154179.png)

#### 解决办法

##### 1.找到你Python的安装位置

![在这里插入图片描述](./jupyter_notebook%E8%AE%BE%E7%BD%AE.assets/de9305e48c064e039d28f64c3dec94f4.png)

##### 2.搜索marked

![在这里插入图片描述](./jupyter_notebook%E8%AE%BE%E7%BD%AE.assets/b7afd3e1361443819492711015064cd1.png)

##### 3.打开文件位置，按照报错的路径提示没把 marked.js文件放到指定路径下【marker文件夹——lib文件夹——marked js文件】

##### 4.重启jupyter

#### 附录 js文件

链接：https://pan.baidu.com/s/1ECgabAzn1-T5f0fWL6jdEQ
提取码：0jh2





## 修改默认输出

在每个jupyter notebook 开通指定

```
from IPython.core.interactiveshell import InteractiveShell 
InteractiveShell.ast_node_interactivity = "last_expr_or_assign"
```

或者

```
touch ~/.ipython/profile_default/ipython_config.py

open ~/.ipython/profile_default/ipython_config.py
vi ~/.ipython/profile_default/ipython_config.py
```

将下面的代码复制进去，重启jupyter notebook 

```
c = get_config()
c.InteractiveShell.ast_node_interactivity = "last_expr_or_assign"
```

如果代码单元格不想输出，在代码后面加个分号==；==，就能抑制输出了。

参考连接：https://blog.csdn.net/zhuxiao5/article/details/121551087



## 双击打开jupyter notebook 参考

https://goldengrape.github.io/posts/bulabula/double-click-open-ipynb/
## jupyter notebook 主题 参考
https://github.com/dunovank/jupyter-themes




