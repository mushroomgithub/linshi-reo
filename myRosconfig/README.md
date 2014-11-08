#Ros配置文件使用说明

>安装ros机器人的linux操作系统是ubuntu,最开始使用的是ubuntu14.04安装ros最新版indigo版,但是不知怎么回事,软件安装配置完成之后,总是不能实现多目kinect的深度图.rgb,视差图,骨骼跟踪图,估计是我学艺不精吧,网上关于最新版本的ros配置,学习资源也不是很多,所以造成了学习起来有点吃力,之后,看到听linux社区中的一位也在研究这方面的经验人士的建议,最终决定卸载ros indigo,改重新安装ros groovy版,下面是一些配置方法:实现多目kinect的配置.

##配置方法
>1.首先根据Ros.pdf第四章,第五章,第十章,将Ros groovy配置完成,
----
>2.配置完成ros groovy之后,此时无论我们怎么操作,都能实现一个kinect的rgb,深度图,视差图,等等功能一般实现,现在实验室需要在ros系统下使用多目kinect实现实验室骨骼跟踪,深度图,rgb图的建模,对实验室内的人物,根据这些信息,分析人的行为,可用点云实现.
----
>3.为了实现多目,需要将myRosconfig目录下的launch.txt,clone到本地家目录,之后将launch.txt拷贝到ros安装路径下,默认是安装在/opt/ros/groovy目录下,此时我们需要将此文件拷贝到路径/opt/ros/groovy/share/openni_launch/launch目录下,并将其更名为mytest.launch.
----------

可以使用以下命令实现:
====================
cp ~/myRosconfig/launch.txt /opt/ros/groovy/share/openni_launch/launch/mytest.launch
--------
**最后一步,具体操作**
---
#For example:
##打开两个节点:
     roslaunch openni_launch openni.launch camera:=kinect_1 device_id:=1@0
     roslaunch openni_launch openni.launch camera:=kinect_2 device_id:=2@0

Then simply use the normal functions but with kinect_1 instead of camera.

#For example:
##rgb,视差图和深度图
rosrun image_view image_view image:=/kinect_1/rgb/image_color 
rosrun image_view disparity_view image:=/kinect_1/depth/disparity rosrun image_view image_view image:=/kinect_1/depth/image
