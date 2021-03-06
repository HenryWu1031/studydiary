## Linux踩坑笔记一

#### 前情提要

最近在学习linux，然后我在学习linux中的时候也是遇到了很多的坑，下面写出来一方面是自己记录一下，也是提醒自己，并且希望能够给予观看到这篇文章的人一些帮助

#### 第一个坑

我这边用的是VMware装的centOS7，然后VMware的版本是15.0，也不知道是不是VMware版本的问题还是win10的问题，反正我遇到的一个很无语的事情就是只要是把linux关闭之后，然后我们再开启虚拟机就会蓝屏，直接提示我们重启，后来发展到了连新建虚拟机都不可以，只要是开启就是蓝屏。所以这个是要小心的，那么怎么解决的呢，我把VMware的版本升到了15.5，然后就ok了，至于另一个要注意的就是，不要shutdown了，就算一定要关机，也一定要shutdown -r，这样linux就是重启而不是关机，此外对于VMware的话就是用挂起代替关闭！（至于现在关闭了是否能开，我实在是不敢再去试了，因为一次蓝屏就意味着一次重装虚拟机）

#### 如何解决安装了centOS7虚拟机之后没有网络

这个问题网上也有很多回答，我一开始也是参照网络上面的回答，现在我自己对于这个问题也算有一定的话语权，首先我们要进入到root用户模式

![image-20210511191352646](C:\Users\why19991031\Desktop\写作中间站\1.png)

2、然后我们进入一个目录  命令如下  cd /etc/sysconfig/network-scripts

结果如下

![image-20210511191600125](C:\Users\why19991031\Desktop\写作中间站\2.png)

3、之后进入文本编辑模式，编辑期中的一个文件，命令为 vi ifcfg-ens33

![image-20210511191747095](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\3.png)

4、我们要把着最后一行的ONBOOT=no改成ONBOOT=yes（进入修改模式要按i）

5、修改完之后 要按下： 继续按wq，之后回车，退出编辑模式

6、之后我们要重启网络服务 命令如下   systemctl restart network

7、这个时候我们基本上已经完成了工作，这个时候我们可以去放心的上网啦！

#### 安装图形界面

我们大家都知道一开始虚拟机装好之后是黑不拉几的界面，那么我们看这个模式其实是不太爽的，并且笔者用的电脑只有14寸，看起来特别的不舒服，而且很多操作都不好完成，并且我们都是先接触的windows操作系统，我们对于图形界面其实是有比较严重的依赖的，那么我们就开始准备centOS7的图形界面安装

1、安装的命令主要是下面的两个 yum groupinstall "X Window System" (途中会题型我们输入y，那个时候就只要输入y就可以啦) 当然我们这一步的安装需要上一步网络的配合，如果没有网络的配合我们的安装肯定会失败的。

2、第二个安装的命令主要是 yum groupinstall "GNOME Desktop"(同上)

3、安装完毕后我们使用命令 startx 进入图形界面如下

![image-20210511192423263](C:\Users\why19991031\Desktop\写作中间站\4.png)

4、这个时候我们的安装基本上就结束啦，至于其他