## tmux教程

- session会话

  1. 新建session

     ```
     ## 直接新建一会话，并进入
     tmux
     ## 记编号总是不那么容易的，所以一般会在新建会话时，给会话命名，方便记忆，以后也好操作
     ## 新建一命名为 abc 的会话
     tmux new -s abc
     ```

  2. 当前session

     ```
     ## 在正常终端模式下，列出当前有哪些tmux会话
     tmux ls
     ```

  3. 退出(暂时)session

     ```
     C-a d
     ```

  4. 恢复session

     ```
     ## 连接回以前的某个编号的 tmux 会话，编号用的是 tmux ls 命令时所列出的每一行的最前面的那个编号
     tmux attach -t 编号
     ## 也可简写成
     tmux a -t 编号
     ## 连接上 abc 会话
     tmux attach -t abc
     ## 或者
     tmux a -t abc
     ```

     

  5. 重命名session

     ```
     ## 重命名 abc 会话名称为 cba
     tmux rename -t abc cba
     ```

  6. kill session

     ```
     ##  杀死整个 cba 会话
     tmux kill-session -t cba
     ```

  7. 休眠

     ```
     ## 在正常终端模式下，使某个编号的会话强制休眠，编号用的是 tmux ls 命令时所列出的每一行的最前面的那个编号
     tmux detach -t 编号
     tmux detach -s 名称
     ## 休眠 abc 会话
     tmux detach -s abc
     ```

     

- window

  ```
  {前缀} c           创建新窗口
  {前缀} n           选择下一个窗口
  {前缀} p           选择前一个窗口
  {前缀} l           最近一次活跃窗口之间进行切换
  {前缀} 0~9         选择几号窗口
  {前缀} ,           重命名窗口
  {前缀} .           更改窗口的编号，但只能更改成未使用的编号，所以要交换窗口的话，得更改多次进行交换
  {前缀} &           关闭窗口
  {前缀} w           以菜单方式显示及选择窗口
  {前缀} f           在所有窗口中查找内容
  ```

  

- pane

   ```
  {前缀} "           模向分隔面板
  {前缀} %           纵向分隔面板
  {前缀} o           跳到下一个分隔面板
  {前缀} x           关闭面板
  {前缀} ;           切换到最后一个使用的面板
  {前缀} 上下键      上一个及下一个分隔面板
  {前缀} 空格键      切换面板布局

  ```

- ~/.tmux.conf

  1. 配置文件参考连接:

  <https://learnxinyminutes.com/docs/zh-cn/tmux-cn/>

  <http://blog.kissdata.com/2014/07/29/tmux.html#section-4>

  2. 我的配置文件

     ```
     
     ### 通用设置
     ###########################################################################
     # 启用鼠标
     set-option -g -q mouse on
     
     # 取消默认的前缀键 C-b
     unbind C-b
     
     # 设置新的前缀键 C-a
     set-option -g prefix C-a
     
     # 较易于使用的窗格分割快捷键
     bind = split-window -h
     bind - split-window -v
     unbind '"'
     unbind %
     ```

     

  
