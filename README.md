# 深度学习远程端开发分享

深度学习研究是一个非常注重实践的研究，所以即使对一些理论非常了解，论文读过不少，但可能实践的时候就会发现伤透了头脑。

因为实际开发中都会用服务器来进行开发，因此就要熟练掌握远程开发，这里面也有很多坑，很多经验都得自己摸索，才能得到自己最熟练的一套流程。为了节省大家探索的时间，于是就想分享一下自己的一套流程。

当前最主要想分享的是两个工具。

## Remote VSCode：利用编辑器进行远程编辑

首先我们要考虑的是，如何编辑服务器端的文件。当然硬核点的玩家是直接就用 Vim 来进行编辑，但是我想大家都知道 Vim 学习的难度，基本上学了很久还只会几个基础命令。

相比之下，诸如Sublime，VSCode，还有Atom这样的编辑器，以其美观的界面，各种各样的插件，还有友好的交互，慢慢获得人们的青睐。我这三个都用过，现在主要用 VSCode 了。

用这些编辑器来编辑也有两种方法，一种是拷到本地来编辑，之后再上传同步，所以可以用ftp，scp，或者rsync (最早我主要用这个)，甚至是git来进行同步。

当然还有一种直接点的方法，那就是用这些编辑器上的插件，直接进行编辑。

这里就展示 VSCode 远程编辑的配置过程，简单来说就是这几步：

- VSCode 安装 Remote VSCode 插件

  ![image.png](https://upload-images.jianshu.io/upload_images/4787675-bf86a53fd4fca1e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 服务器端安装 rmate，可以用下面脚本，也可以直接从本库的`scripts`里面拷`rmate`文件，当然不要忘了拷了之后要添加PATH路径

  ```bash
  curl -Lo ~/bin/rmate https://raw.githubusercontent.com/textmate/rmate/master/bin/rmate
  chmod a+x ~/bin/rmate
  export PATH="$PATH:$HOME/bin"
  ```

- 接着使用的时候，先 ctr+shift+p 输入`Start Server` 确定，然后 ctrl + ` 打开终端里的bash，最后输入

  ```
  ssh -R 52698:localhost:52698 远程端IP
  ```

  登录完成之后就连接成功了。

- 最后就直接在命令行里面rmate需要编辑的文件就行了。

## Tmux 终端多窗口

还有一个非常好用的工具便是 Tmux，有的时候训练模型需要丢到后台，或者要开好几个窗口，这个时候用tmux就非常方便。这也是我接触 linux 后最喜欢的一个工具了。

官方点的介绍就是

> Tmux 是个在终端窗口中分屏，运行**多个终端会话**的工具，同时还能随时断开会话放入后台，或者接入。

![img](https://upload-images.jianshu.io/upload_images/4787675-7310a85107dbef8c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

学习的话，可以去下一个[备忘单](https://link.jianshu.com/?t=https%3A%2F%2Fgist.github.com%2FMohamedAlaa%2F2961058)，然后边用边查。

常用的几个命令也就创建，分屏，还有切换。

这样对于跑程序相关的就一切都 OK 啦，无论是想跑一个，还是同时跑 n 个，随你喜欢。

#### 如何安装

安装的时候，如果没有管理员权限会比较麻烦，所以要只安装在自己用户下面。

这里就直接给出[安装脚本](scripts/tmux_local_install.sh)，在bash里面运行`scripts/tmux_local_install.sh` 就好了。