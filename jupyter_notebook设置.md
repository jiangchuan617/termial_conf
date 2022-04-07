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



