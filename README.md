# Franka-Research-3-Practice

最近入门robotics，环境编译问题真的搞得我焦头烂额。而且网上的资料又乱又繁杂。我在这里整理一下以便后人乘凉。

#### 我的配置

ubuntu 20.04 （强烈建议）

显卡RTX A2000

Franka Research 3

#### ubuntu、Win10双系统安装

https://blog.csdn.net/kuwola/article/details/127618930

#### ROS安装

[ROS/Installation - ROS Wiki](http://wiki.ros.org/ROS/Installation)

#### libfranka和franka ros安装

https://frankaemika.github.io/docs/installation_linux.html

ubuntu实时内核不要在根据这条链接做，这里的安装方法已经过时了。而且如果你的内核版本很新，而且还装的5.9.1，会导致屏幕亮度，wifi等一些功能的丧失。

#### ubuntu实时内核（realtime kernel）

rt kernel 安装：https://davidaugustat.com/linux/how-to-compile-linux-kernel-on-ubuntu

显卡驱动：https://codeleading.com/article/88935871644/

太有用了这篇文章，救我狗命啊！实时内核的安装一定会导致显卡驱动不兼容的问题，这篇文章很好地解决了如何在实时内核下安装显卡驱动的问题。

而且请严格遵循步骤，先装实时内核，再装驱动（在非实时上），再在实时内核上迁移驱动。

#### 如何使用ROS对franka进行控制

1、建立catkin_ws

2、从libfranka找example（.h .cpp）全部扒下来放到source code里面

3、修改package.xml，建立依赖库（Eigen、franka_ws）

4、修改checklist，编译头文件和可执行文件，然后catkin_make

5、source devel/setup.bash

5、开启roscore，使用rosrun执行可执行文件

#### 系统全部烂掉了，想重开怎么办

https://www.cnblogs.com/yangyezhuang/p/16896923.html

#### Realsense深度摄像头安装

https://robots.uc3m.es/installation-guides/install-realsense2.html

RealSense的github：https://github.com/IntelRealSense/librealsense

#### Moveit!安装（panda_moveit_config）

首先尝试一下：

sudo apt-get install ros-noetic-moveit

或者

sudo apt-get install ros-noetic-moveit-full

如果缺乏依赖，应该先把依赖装上：https://packages.ubuntu.com/

如果不行，可以尝试源码编译：

https://moveit.ros.org/install/source/

如果编译不了的包，在 ./ws_moveit/src 里直接删掉就好了

#### 手眼标定（Eye-hand Calibration）

[GitHub - IFL-CAMP/easy_handeye: Automated, hardware-independent Hand-Eye Calibration](https://github.com/IFL-CAMP/easy_handeye)

操作指南：

1、https://blog.csdn.net/gyxx1998/article/details/122238052

2、https://zhuanlan.zhihu.com/p/576861119

#### Troubleshooting

###### 1、安装了实时内核之后wifi无法使用了\触控板无法使用\屏幕亮度无法调节

找与你当前内核版本相近的实时内核进行编译。

如果想直接恢复wifi，参考：

https://blog.csdn.net/Liture_Gogh/article/details/128102322

https://blog.csdn.net/weixin_42897032/article/details/125895103

###### 2、Incompatible version (server version 6; library version 5)

从源码安装libfranka和franka_ros。

查看libfranka版本：rosversion franka_hw

###### 3、缺乏依赖怎么办

用deb安装：

sudo dpkg -i *.deb

deb包地址：https://packages.ubuntu.com/

###### 4、在实时内核下不能开双屏幕

切换为非实时就可以开双屏幕了，控制机器人的时候再切换回来就好。

如果你用：make ubuntu-drivers autoinstall

然后你就会发现你实时内核开机黑屏了。So, don't do that.

###### 5、如何删除内核

https://askubuntu.com/questions/594443/how-can-i-remove-compiled-kernel
