嫌麻烦直接淘宝找人帮忙安的，这里记录下来安装过程，以后可以自己弄  
（现在自己按这个方法安装了三四次， 基本是没问题的）。  
我的电脑目前是两个500g固态，一个自带的一个后安的，给Ubuntu分了250G。  
以下全程断网！！！！  
1、制作系统盘  
这里我格式化U盘选择的是fat32方式，虽然不知道到底影不影响，但是NTFS方式格式化的我没有成功过。  
2、分区  
以上两个部分教程很多，这里就不写了，给个链接[分区和制作系统盘教程][Link 1]，最好选择ubuntu20版本下最新的镜像文件，目前最新是20.04.5，那么基本可以解决接下来我遇到的很多问题。我当时安的是20.04.3，网卡驱动是没有的，要手动更新。  
3、插上制作好系统的U盘，重启电脑按F2（华硕电脑是F2，其他型号自己百度一下）  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a1f19c5ed3d1e164cb90e017221ff2ac.jpeg)  
4、按F7切换到Advanced Mode  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/84946394c90e9ce776e8d70554473681.jpeg)  
5、右键切换到Boot页面  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/528233265934c83834b63deae82977c2.jpeg)  
6、  
Fast boot回车改成Disabled  
Boot option1的位置，回车改成UEFI  
如下图所示：  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/10975336d22653dc1a2e2118db202d9d.jpeg)  
7、切换到Security页面

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0c0775de607eae25b5a060c44cbbb4b1.jpeg)  
8、secure boot选项点开，secure boot control改为Disabled  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/53244134956533b513d4665598e3e144.jpeg)  
9、按F10保存，选Yes回车  
10、等待进入Ubuntu安装页面  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b56a4d9ecf382a9135c237f016cdc5aa.jpeg)  
11、选语言，安装。键盘布局，继续。下一步。正常安装，继续。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/01488e56ec6e4127878e6dbfe26c7db4.jpeg)  
11、安装类型这里，选择其他选项进行手动分区，点继续后，见下图：  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0d3da725eab913cb5e750660f513e8e8.jpeg)  
12、我这里给Ubuntu分了250g，采用的分区方法要看[教程][Link 2]。  
如果是双硬盘，需要先在C盘（按理来说就是电脑的第一块硬盘，部分电脑系统装得比较奇怪，装到了第二块硬盘）分出200M的空白分区用来安装ubuntu的启动项，然后再在另一块硬盘选择最后一个盘（比如 CD两个盘的最后一个是D盘，CDE盘的最后一个是E盘，CDEF盘的最后一个是F盘，以此类推），在该盘点击右键，选择压缩卷，输入压缩空间量，单位为M，即给ubunru分配的大小。  
在这里，我们进行手动分区，假设你留出的空闲分区为 80G，点击空闲盘符，点击"+"进行分区，如下：

1）efi：如果是单硬盘，在唯一的一个空闲分区上添加，大小200M，逻辑分区，空间起始位置，用于efi；如果是双硬盘，找到事先分好的200M空闲分区添加，逻辑分区，空间起始位置，用于efi。这个分区必不可少，用于安装ubuntu启动项。以下步骤单双硬盘就一样了，都在自己给ubuntu分配的空闲分区上添加  
2）swap:中文是"交换空间"，充当ubuntu的虚拟内存，一般的大小为电脑物理内存的2倍左右，可以将其分为 8G，逻辑分区，空间起始位置，用于"swap"或"交换空间"。  
3) /:这是ubuntu 的根目录,用于安装系统和软件，相当于windows的C盘，我分了100G，主分区，空间起始位置，用于"ext4日志文件系统"，挂载点为"/“（根据你的磁盘空间调整，可以大一点，毕竟ubuntu装软件都是默认装在根目录的）  
4）/home:相当于windows的其他盘，剩下的全分给它，逻辑分区，空间起始位置，用于"ext4日志文件系统”，挂载点为"/home"

分区完毕，下面的这一步很重要：在分区界面的下方，选择安装启动项的位置，我们刚刚不是创建了200M的efi分区吗，现在你看看这个区前面的编号是多少，比如是/dev/sda1,不同的机子会有不同的编号，下拉列表选择这个efi分区编号（这里一定要注意，windows的启动项也是efi文件，大小大概是500M，而我们创建的ubuntu的efi大小是200M，一定要选对），之后点击"Install Now"  
我自己的设置如下(打算给ubuntu260G)：  
交换空间：逻辑分区 32768MB(32G)  
挂载点/：主分区 Ext4日志文件系统 102400MB（100G）  
挂载点/home：逻辑分区 Ext4日志文件系统 150177MB（剩下的全部）  
安装启动引导器的设备：/dev/mvme0n1p8(最开始创建了200M的efi分区)  
13、断网，右上角这个图标给它断开，不要联网。  
![[Pasted image 20251106194549.png]]
14、点击“现在安装”，默认上海，设置用户名与密码，等待一段时间后重启。  
15、重启后选择Ubuntu，成功进入就可以拔掉U盘了。  
问题来了，我的电脑无法成功进入：  
![[Pasted image 20251106194606.png]]
大概是网卡配置的问题，总之我又去找了客服，进行如下操作：  
1、按电脑电源开关重启，进入时选择Unbuntu高级选项。  
2、选择第二项，恢复模式（recovery mode)启动，然后在出现一堆英文选项时候快速点两次回车：  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/174454451924504cf5a5adaedd83afba.jpeg)  
3、回车后等一小下就成功进入Ubuntu了。  
4、终端输入如下命令，密码是你进入ubuntu时自己设置的密码：

```java
sudo mv /etc/grub.d/30_os-prober /etc/grub.d/08_s-prober
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d0b404760dadbba2388edb9badcd0756.jpeg)  
5、继续输入：

```java
sudo gedit /etc/default/grub
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/69cc3e2ad7c1c13bcfc58bbbbb80b584.jpeg)

6、在弹出的文本页面中的第10行代码修改为如下语句：

```java
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
修改为：
GRUB_CMDLINE_LINUX_DEFAULT="uiet splash nouveau.modeset=0"
```

保存后退出。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/57d7e090f7b36f709d864422ffa8c65b.jpeg)  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/273e09dd021a6afe278a89cf89126a47.jpeg)  
7、终端继续输入如下命令，更新刚刚修改的配置文件：

```java
sudo update-grub
```

这样电脑重启就可以正常选择Ubuntu进入了，然后就可以联网。  
以上的过程中如果联网我这个型号的电脑会出问题，简单了解一下大概是网卡的事儿，目前还没找到合适的网卡驱动。如果联网电脑会自动安个不匹配的驱动，重启无法成功开机，所以我这电脑目前还不能用wifi，只能宽带拨号上网(但是过了几个月之后发现可以用无线了，右上角自动出现，估计是update的时候有更新到网卡配置)。

8、重启后，拨号上网的设置，终端输入：

```java
nm-connection-editor
```

点加号，创建一个DSL/PPPOE连接，输入帐号密码即可。

9、好换成国内源，不然以后软件的下载速度很慢。换源要选择适用你的Ubuntu版本的，我这里是20.04（百度的话最好找最新的源，有的太旧不能用）

```java
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo gedit /etc/apt/sources.list
```

打开的文件修改为：

```java
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
```

更新源和软件：

```java
sudo apt-get update
sudo apt-get upgrade
```

10、最后，如果没有wifi图标，说明你的镜像文件比较老，里面不带网卡驱动，这时候自己系统更新一下就好了，[参考链接][Link 3]：

```java
#第一步：检查系统更新 
$ sudo apt update
#第二步：列出需要更新的软件包 
$ sudo apt list --upgradable
#第三步：更新 
$ sudo apt upgrade -y
```

可能出现的另一个问题：  
那就是你的ubuntu明明什么都没有下载，还没有开始用，硬盘就被自动占满了。一点儿空间都没有，直接标红爆满！  
淘宝客服和我说他两年没碰到这种情况了，重新安装n次也没有办法解决。  
原因总结一下就是我的这台电脑有问题，换配置一模一样的另一台电脑九成都不会出错。还好我的电脑刚刚在京东买的，立马退货换一台（第一台电脑本身外放有些爆音，我一开始想忍忍算了懒得换，毕竟疫情快递很麻烦。不过双系统没法安真的就不行了，最后是以爆音的理由换掉的），换了一台之后果然成功安装，硬盘也没被占满（另外爆音也没有了）。  
总之我到手的第一台笔记本身就是有点儿问题的，目前第二台就成功安装了！

补充的安装：  
[anaconda][]  
sudo apt install git  
sudo apt-get install vim  
sudo apt-get install gcc  
sudo apt-get install g++  
sudo apt-get install make  
cmake（别太新，3.15够了）[下载链接][Link 4]：

```java
./bootstrap
make -j8
sudo make install
```

验证版本：

```java
cmake --version
```

[orbslam2配置][orbslam2]：pangolin一定要安装这个教程里的 ，有的0.6不稳定，频繁报错。  
sudo ldconfig  
测试：

```java
cd Pangolin
cd examples/HelloPangolin
mkdir build && cd build
cmake ..
make
./HelloPangolin
```

pytorch:  
[官网获取下载命令][Link 5]

```java
pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113
```

虽然我是11.4的cuda，但是没有这个版本的，安了11.3的，运行没问题。

```java
python
>>>import torch
>>>import torchvision
>>>torch.cuda.is_available()
如果输出位True则代表pytorch成功识别cuda。
```


[Link 1]: https://blog.csdn.net/hwh295/article/details/113409389
[Link 2]: https://www.cnblogs.com/masbay/p/11627727.html
[Link 3]: https://blog.csdn.net/qq_58862767/article/details/123089269
[anaconda]: https://www.bilibili.com/read/cv14076200
[Link 4]: https://gitlab.kitware.com/cmake/cmake/-/tags?page=5
[orbslam2]: https://blog.csdn.net/qq_44195329/article/details/124197681?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-3-124197681-blog-124184774.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-3-124197681-blog-124184774.pc_relevant_paycolumn_v3&utm_relevant_index=5
[Link 5]: https://pytorch.org/get-started/locally/