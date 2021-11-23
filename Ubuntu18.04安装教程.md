# 无人驾驶工程配置说明



## 一、安装 ubuntu18.04 



### 1.下载 Ubuntu 镜像

```shell
http://mirrors.aliyun.com/ubuntu-releases/18.04.4/
```

![image-20210621155220701](/home/lxf/Downloads/x86/image/1.png)

### 2.制作U盘启动盘

1）安装制作工具：rufus

```shell
http://rufus.ie/en_US/
```

![2](/home/lxf/Downloads/x86/image/2.png)

2）插入用来做启动盘的U盘（最好是usb3.0接口，16GB或以上），并清空里面的文件
3）打开安装好的rufus，需要更改的第一点就是device是否是你插入的U盘启动盘，第二点选择你下载好的镜像文件，其他默认即可。
4）点击start写入过程大概会持续几分钟，
至此，启动盘制作完成！

### 3.给 Ubuntu 分配硬盘空间(尽可能大)，分区根据自己电脑内存合理调整

这一步也可以在安装过程中分区的时候执行，不过最好安装前弄好，省得到时候出岔子需要从头开始。

1）鼠标右键计算机，在弹出来选项卡中选择管理，接着在弹出来的窗口左侧点击 存储/磁盘管理，进入磁盘管理界面，如下图所示：



![在这里插入图片描述](/home/lxf/Downloads/x86/image/3.png)



2）在你要安装的目标磁盘中，通过删除卷和删除分区操作腾出一块未分配的磁盘空间作为安装区，我要安装的位置是 磁盘1，所以我在 磁盘1 中整合出了 256GB 的空间用来安装 Ubuntu18.04.1（安装区的大小依磁盘总的空间以及你的需要而定），这一步弄好后如下图所示：

![4](/home/lxf/Downloads/x86/image/4.png)



### 4.安装 Ubuntu18.04

#### 1.设置启动项

1）关闭你要安装 Ubuntu18.04.1 的目标主机，然后插入启动盘，接着开机，迅速的按住 **F12**直到进入 bios 设置界面（不同的电脑进入 bios 的按键不同，一般为 F12 或者 Delete 键），通过方向键选择**Boot Menu**，然后回车

 <img src="https://img-blog.csdnimg.cn/20190119005811646.jpg" alt="在这里插入图片描述" style="zoom:80%;" />



2）进入Boot Manager后，选择 **EFI USB** 作为启动项，回车

![在这里插入图片描述](https://img-blog.csdnimg.cn/201901190059151.jpg)



3)至此我们就进入了安装程序，选择 **Install Ubuntu**， 回车直接安装

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190119013933270.jpg)





#### 2.正式安装

1）选择语言默认即可（英文）

2）键盘布局默认即可（英文）

3）无线连网不需要

4）更新选项正常安装

5）选择安装类型最后一个自定义分区

![Ubuntu18.04桌面版自定义分区安装](https://imgconvert.csdnimg.cn/aHR0cDovL2ltYWdlLmlkYW5ueXd1LmNvbS9INmszS0dZLnBuZw?x-oss-process=image/format,png)

接下来需要我们手动分区，前面我们给在磁盘1给 Ubuntu18.04.1 预留了 256GB 的磁盘空间，下面对这 256GB 的空间进行分区。

下图中的sd+字母+number， 其中字母表示磁盘的编号，bumber表示分区的编号
例如：sda3 表示磁盘 a 的第三个分区，sdc1 表示磁盘 c 的第一个分区
前面我们给在磁盘1给 Ubuntu18.04.1 预留了 256GB 的磁盘空间，对应于下图的 /dev/sdc下的 空闲区

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190119014530755.jpg)





#### 3. 手动分区：(500G分区建议)

#### 一般四个就够了：  /、/boot、/home、 /swap



| 挂载点 | 建议大小     | 格式 | 描述               |
| ------ | ------------ | ---- | ------------------ |
| /      | 100G         | ext4 | 主分区、起始位置   |
| swap   | 物理内存两倍 | swap | 逻辑分区、起始位置 |
| /boot  | 3G左右       | ext4 | 主分区、起始位置   |
| /home  | 剩下的所有   | ext4 | 主分区、起始位置   |
|        |              |      |                    |



#### 6）选择时区-上海

#### 7）创建用户名、密码

#### 8）安装系统软件

用户名创建完成后，安装程序会安装一些必要的系统软件，整个过程会持续大概 20～30分钟，完成后，会弹出如下的对话框。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190119032729512.jpg)

至此，Ubuntu18.04.1 安装完成！此时拔出 U盘，接着重启电脑即可。





#### 4、安装完成后的优化工作

1.完成上面的步骤后，Ubuntu18.04 就可以正常使用了。但是为了更加方便快捷的使用，建议再对装好的 Ubuntu 系统做以下的更改。

Ubuntu 的源存放在在 /etc/apt/ 目录下的 sources.list 文件中，修改前我们先备份，在终端中执行以下命令：

    sudo cp /etc/apt/sources.list /etc/apt/sources.list.bcakup

打开软件更新**software & update**：

配置如下果所示，download from选择china里的阿里云或者清华源即可

![image-20210621165825102](/home/lxf/Downloads/x86/image/5.png)



2.进入”System Setting->Software&Updates”,勾选 Ubuntu Software 中的所有选项,
并勾选 Other Software 中的”Canonical Partners”和”Canonical Partners(Source Code)”,
单击”Colse”,然后弹出信息提示框,单击”Reload”即可。

接着在终端上执行以下命令更新软件列表，检测出可以更新的软件：

    sudo apt-get update
    sudo apt-get upgrade



## 四、安装ROS、CUDA、CUDNN



### 1.设置软件源：

清华的：

```shell
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list'
```

设置最新的密钥：

```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F42ED6FBAB17C654
```

### 2.安装：

    sudo apt-get update
    sudo apt-get install ros-melodic-desktop-full
    sudo apt-get install ros-melodic-rqt*

初始化rosdep:

    sudo rosdep init
    rosdep update

如果出现下面情况，基本是网络问题，换个网络尝试下（PS：我用手机热点解决的）：

    lee@lee-TM1801:~$ sudo rosdep init
    ERROR: cannot download default sources list from:
    https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/sources.list.d/20-default.list
    Website may be down.



安装rosinstall

```shell
sudo apt-get install python-rosinstall
```


加载环境设置文件

```shell
source /opt/ros/melodic/setup.bash
```


创建并初始化工作目录

 ROS使用一个名为catkin的ROS专用构建系统。为了使用它，用户需要创建并初始化

catkin工作目录，如下所示。除非用户创建新的工作目录，否则此设置只需设置一次。

    mkdir -p ~/catkin_ws/src
     
    cd ~/catkin_ws/src
     
    catkin_init_workspace




  目前，只有src目录和CMakeLists.txt文件在catkin工作目录中，使用catkin_make命令来构建

    cd ~/catkin_ws/
     
    catkin_make

设置环境变量：

    sudo apt install net-tools
    gedit ~/.bashrc




    # Set ROS melodic
    source /opt/ros/melodic/setup.bash
    source ~/catkin_ws/devel/setup.bash
     
    # Set ROS Network
    #ifconfig查看你的电脑ip地址
    export ROS_HOSTNAME= 本机ip
    export ROS_MASTER_URI=http://${ROS_HOSTNAME}:11311

小海龟测试，打开三个终端：

    roscore
    rosrun turtlesim turtlesim_node
    rosrun turtlesim turtle_teleop_key



### 3.安装显卡驱动

安装显卡驱动: “System Setting->Software&Updates->Additional Drivers”。
请先添加 NVIDIA 下载源打开新的终端, 执行以下指令:

```shell
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
```

​		可以打开驱动管理程序 UI 界面,勾选版本号为 41x.xx 的 NVIDIA 显卡驱动进行安装,例
如:410.78,415.27,418.56,详见图：

​	![image-20210920115459306](/home/lxf/Downloads/x86/image/6.png)



### 4.安装CUDA

1. 进入${rs_sdk_dependency}/cuda10.0 文件夹内, 打开新的终端, 执行以下指令:

   ```shell
   $ sudo chmod +x cuda_10.0.130_410.48_linux.run
   $ sudo ./cuda_10.0.130_410.48_linux.run
   ```

2. 出现以下界面后, 长按空格键直到 100%

3. 选项：

   ```shell
   accept
   N
   Y
   回车
   N
   N
   ```

   

4. 安装完成后, 添加 cuda 环境变量到~/.bashrc 中:

   ```shell
   $ sudo gedit ~.bashrc
   
   #将以下两句话添加进去
   export PATH=/usr/local/cuda-10.0/bin:$PATH
   export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64:$LD_LIBRARY_PATH
   
   $ source ~/.bashrc
   ```



### 5.安装cudnn

 进入${rs_sdk_dependency}/cudnn 文件夹内, 打开新的终端, 执行以下指令:

```shell
$ sudo dpkg -i ./libcudnn7_7.4.2.24-1+cuda10.0_amd64.deb
$ sudo dpkg -i ./libcudnn7-dev_7.4.2.24-1+cuda10.0_amd64.deb
$ sudo dpkg -i ./libcudnn7-doc_7.4.2.24-1+cuda10.0_amd64.deb
```



### 6.安装protobuf

```shell
$ sudo apt-get install -y libprotobuf-dev protobuf-compiler
```



### 7.安装 USB-KEY 驱动

进入${rs_sdk_dependency}/key 文件夹, 打开新的终端, 执行以下指令:

```shell
$ sudo chmod a+x install_key.sh
$ ./install_key.sh
```



### 8.安装依赖工具脚本

进入${rs_sdk_dependency}文件夹, 打开新的终端, 执行以下指令:

```shell
$ sudo chmod a+x install_dependency.sh
$ ./install_dependency.sh
```



### 9. pcl安装

#### 1、安装依赖项

1.在home目录下创建pcl文件夹，创建依赖项脚本文件pcl_dependences.sh并给文件赋予执行权限

```shell
mkdir pcl && cd pcl && touch pcl_dependences.sh && chmod +x *.sh
```

2.打开脚本文件将以下内容复制进去并保存

```shell
sudo apt-get update  
sudo apt-get -y install git build-essential linux-libc-dev
sudo apt-get -y install cmake cmake-gui
sudo apt-get -y install libusb-1.0-0-dev libusb-dev libudev-dev
sudo apt-get -y install mpi-default-dev openmpi-bin openmpi-common 
sudo apt-get -y install libpcap-dev
sudo apt-get -y install libflann1.9 libflann-dev
sudo apt-get -y install libeigen3-dev 
sudo apt-get -y install libboost-all-dev
sudo apt-get -y install vtk6 libvtk6.3 libvtk6-dev libvtk6.3-qt libvtk6-qt-dev
sudo apt-get -y install libvtk7.1-qt libvtk7.1 libvtk7-qt-dev
sudo apt-get -y install libqhull* libgtest-dev
sudo apt-get -y install freeglut3-dev pkg-config
sudo apt-get -y install libxmu-dev libxi-dev
sudo apt-get -y install mono-complete
sudo apt-get -y install openjdk-8-jdk openjdk-8-jre
sudo apt-get -y install libopenni-dev libopenni2-dev
```

3.执行脚本文件

```shell
sudo sh pcl_dependences.sh
```



#### 2、下载pcl源码

```shell
#git pcl源码
git clone https://github.com/PointCloudLibrary/pcl.git 

#若没有git，先安装git
sudo apt-get install git

#进入目录编译
cd pcl && mkdir release && cd release

# 配置cmake(bashrc配置好cuda环境变量，否则这一步无法编译)
cmake -DCMAKE_BUILD_TYPE=None  -DCMAKE_INSTALL_PREFIX=/usr \ -DBUILD_GPU=ON-DBUILD_apps=ON  -DBUILD_examples=ON \  -DCMAKE_INSTALL_PREFIX=/usr ..
      
#进行编译,也可以`make -j11`11为内核数 按自己的cpu内核填写 不写数字默认使用全部核心编译make需要等待较久的时间
make
```


#### 3、将程序安装至系统中

```shell
sudo make install
```

#### 4、测试

```shell
cd ~/pcl/test 
pcl_viewer office1.pcd

显示点云图即安装完成！！！
```



### 10.标定配置

```shell
# 进入压缩包lidars_calibration_v3.3.0.tar.gz目录
tar -zxvf lidars_calibration_v3.3.0.tar.gz
cd lidars_calibration_v3.3.0
sudo chmod +x install.sh
./install.sh
```



### 11.项目工程编译

进入rs_pseries_3工程包，打开终端：

```shell
cd /module/rs_perception
sudo chmod a+x install_dependency.sh
./install_dependency.sh

cd ../../
mkdir build && cd build
cmake ..&& make all
```



### 12.建图配置

#### 1 简介

**RS_MAPPING** 为构建 *3D* 高精度点云地图的软件，以 *RSLIDAR* 为主，融合多传感器数据 ( *IMU*，车速，*GNSS* )，获取在统一坐标系下，每帧 *LIDAR* 点云数据的六自由度的姿态信息，同时会生成融合后的全局 *3D* 点云地图，以及可供 **RS_localization** 使用的定位特征地图。

**RS_MAPPING** 包含：

- 数据解析模块（在线和离线）: **data_capture** 及 **rosbag_parser**
- 前端模块: **frontend**
- 后端模块: **mapping**
- 地图生成模块: **map_generate**
- 点云在线标定模块: **lidar_calibrator**
- 人工优化模块: **manual_optimization**
- 地图协同优化模块: **map_collaborative_optimization**
- 批量建图模块: **map_batch**



#### 2 硬件需求和软件依赖

#### 2.1 硬件需求

- X86 平台 (笔记本、台式电脑)

***注意 :***

      1. **RS_MAPPING** 是在 **Ubuntu**操作系统下在 **ROS** 系统的辅助下开发的，所以推荐使用相同的配置；
      2. **RS_MAPPING** 依赖于 *ROS* ，且使用 *ROS* 可以方便地录包&播包，并且可以使用 *RVIZ* 直观地看到运行结果。

#### 2.2 软件依赖

在开始部署RS_MAP之前，请确保如下库已经正确安装并配置好。

- cmake (最低版本3.5)
- PCL 1.7.x
- Boost 1.54 或者更高版本
- Eigen 3.x 或者更高版本
- yaml 0.5.x
- OpenCV 2.x 或者 3.x
- Qt 5.5.1

#### 3 安装

- 进入rs_mapping_release-v1.2.2，运行依赖库安装脚本

```
$ sudo chmod +x install.sh
$ ./install.sh
```

- 等待依赖安装完毕，即可通过建图界面工具来执行建图模块

#### 4 建图数据采集说明

- 建图数据采集说明文档介绍传感器的数据类型，安装平台，数据采集要求

  [建图数据采集说明](./doc/RS_MAPPING_DATA_README.md)

#### 5 快速启动

#### 5.1 获取密钥

   密钥为 *USB* 形式，即插即用。

#### 5.2 建图使用

- 建图工具文档介绍如何通过建图界面工具 **执行** 建图模块

  [建图工具](./doc/RS_MAPPING_UI_README.md)

- 建图模块详解文档介绍建图每个模块的详细参数配置，含义及生成数据

  

### 13.环境配置

```shell
sudo gedit .bashrc

用户lxf改为本机用户
export LD_LIBRARY_PATH=/home/lxf/rs_pseries_3/module/rs_common/third_party/lib/x86_64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/home/lxf/rs_pseries_3/module/rs_localization/lib/x86_64_bionic:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/home/lxf/rs_pseries_3/module/rs_perception/distribute/lib/x86_64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/home/lxf/rs_pseries_3/module/rs_perception/external/cuda/x86_64/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/home/lxf/rs_pseries_3/module/rs_perception/external/tensorRT/x86_64/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/home/lxf/rs_pseries_3/module/rs_perception/external/trt_infer/x86_64/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/home/lxf/rs_pseries_3/module/rs_preprocessing/lib/x86_64/1804:$LD_LIBRARY_PATH
```

