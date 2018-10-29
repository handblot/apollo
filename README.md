# Apollo

[![Build Status](https://travis-ci.org/ApolloAuto/apollo.svg?branch=master)](https://travis-ci.org/ApolloAuto/apollo) [![Simulation Status](https://azure.apollo.auto/dailybuildstatus.svg)](https://azure.apollo.auto/dailybuild)

```
We choose to go to the moon in this decade and do the other things,
not because they are easy, but because they are hard.
-- John F. Kennedy, 1962
```

Welcome to the Apollo GitHub.

[Apollo](http://apollo.auto) 开源自动驾驶平台. 
It is a high performance flexible architecture which supports fully autonomous driving capabilities.
For business contact, please visit http://apollo.auto

**Apollo Team now proudly presents to you the latest [version 2.5](https://github.com/ApolloAuto/apollo/releases/tag/v2.5.0).**

## 安装

推荐在 Docker environment 中安装

The steps are:
 - 1. Run a machine that runs linux (tested on Ubuntu 16.04 with and without an nVidia GPU)
 - 2. Create a docker environment
 - 3. Build Apollo from source
 - 4. Bootstrap start Apollo
 - 5. Download the demonstration loop and run it
 - 6. Start a browser session and see the Dreamview user interface

More instructions are below

###  docker environment 安装

First, you need to [install docker-ce properly](https://github.com/ApolloAuto/apollo/blob/master/docker/scripts/README.md#install-docker).
The following scripts will get you into the container

```
docker ps  # to verify docker works without sudo
bash docker/scripts/dev_start.sh
# if in China, you had better use:bash docker/scripts/dev_start.sh -C to download from the server of docker in china.
bash docker/scripts/dev_into.sh

```

### 源码编译 apollo
    First check and make sure you are in development docker container before you proceed. 
    Now you will need to build from the source. 
    If you want to run the entire system, make sure you have an
    nVidia GPU and that you have installed the Linux nVidia drivers.

```
# To get a list of build commands
./apollo.sh
# To make sure you start clean
./apollo.sh clean
# This will build the full system and requires that you have an nVidia GPU with nVidia drivers loaded
bash apollo.sh build
```

If you do not have an nVidia GPU, the system will run but with the CUDA-based perception and other modules. 

You mustspecify either `dbg` for debug mode or `opt` for optimized code

```
./apollo.sh build_no_perception dbg
```

If you make modifications to the Dreamview frontend, then you must run `./apollo.sh build_fe`  before you run the
full build.


## 运行 Apollo

Follow the steps below to launch Apollo. Note that you must build the system first before you run it.
Note that the bootstrap.sh will actually succeed but the user interface will not come up if you skip the build step.

### Start Apollo

Running Apollo will start the ROS core and then startup a web user interface called Dreamview, 
this is handled by the bootstrap script, so from within the docker container, you should run:

```
# start module monitor
bash scripts/bootstrap.sh
```

### Access Dreamview
    Access Dreamview by opening your favorite browser, e.g. Chrome, go to http://localhost:8888 
    and you should see this screenHowever, there will be nothing running in the system.

![Access Dreamview](docs/demo_guide/images/apollo_bootstrap_screen.png)

### Select Drive Mode
From the dropdown box selet "Navigation" mode.

![Navigation Mode](docs/demo_guide/images/dreamview_2_5_setup_profile.png)


### Replay demo rosbag

To see if the system works, use the demo 'bag' which feeds the system.

```
# get rosbag note that the command download is required
python ./docs/demo_guide/rosbag_helper.py demo_2.5.bag

# You can now replay this demo "bag" in a loop with the '-l' flag
rosbag play -l demo_2.5.bag
```

Dreamview should show a running vehicle now. (The following image might be different due to changes in frontend.)

![Dreamview with Trajectory](docs/demo_guide/images/dv_trajectory_2.5.png)

## Documents

Apollo documents can be found under the [docs](https://github.com/ApolloAuto/apollo/blob/master/docs/) repository.
   * [quickstart](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/): the quickstart tutorial.
   * [demo_guide](https://github.com/ApolloAuto/apollo/blob/master/docs/demo_guide/): the guide for demonstration.
   * [![Apollo Offline Demo](https://img.youtube.com/vi/Q4BawiLWl8c/0.jpg)](https://www.youtube.com/watch?v=Q4BawiLWl8c)
   * [how to contribute code](https://github.com/ApolloAuto/apollo/blob/master/CONTRIBUTING.md): the guide for contributing code to Apollo.
   * [howto](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/): tutorials on how to build, run and modify codes.
   * [specs](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/): Specification documents of Apollo.
   * [Doxygen APIs](https://apolloauto.github.io/doxygen/apollo/): Apollo Doxygen pages

## Ask Questions

You are welcome to submit questions and bug reports as [Github Issues](https://github.com/ApolloAuto/apollo/issues).

## Copyright and License

Apollo is provided under the [Apache-2.0 license](LICENSE).

## Disclaimer
Please refer the Disclaimer of Apollo in [Apollo official website](http://apollo.auto/docs/disclaimer.html).

# Apollo具体内容说明

## 软件
- [Apollo 2.0软件系统架构](Apollo_2.0_Software_Architecture.md)
- [Apollo 3.0软件系统架构](Apollo_3.0_Software_Architecture_cn.md)
- [Planning模块架构概述](Class_Architecture_Planning_cn.md)

## Apollo硬件开发平台

我们强烈建议使用者在阅读硬件开发平台文档前浏览我们的免责声明。

- [Apollo传感器单元（ASU）](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Apollo_Sensor_Unit/Apollo_Sensor_Unit_Installation_Guide_cn.md)
- [摄像机](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Camera/README.md)
- [激光雷达](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Lidar/README.md)
- [雷达](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Radar/README.md)
- [导航](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Navigation/README_cn.md)
- [IPC](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/IPC/Nuvo-6108GC_Installation_Guide_cn.md)
- [软件系统和内核安装指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Software_and_Kernel_Installation_guide_cn.md)

## 感知

- [Apollo 2.5感知系统](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/perception_apollo_2.5.md)
- [Apollo 2.5传感器安装指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Guideline_sensor_Installation_apollo_2.5.md)
- [Apollo 3.0感知系统]https://github.com/ApolloAuto/apollo/tree/master/docs/specs/(perception_apollo_3.0_cn.md)
- [Apollo 3.0传感器安装指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Guideline_sensor_Installation_apollo_3.0_cn.md)
- [激光雷达校准英文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/lidar_calibration.pdf)
- [激光雷达校准中文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/lidar_calibration_cn.pdf)

## HMI
- [Dreamview使用方法](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/dreamview_usage_table_cn.md)

## 算法
- [三维障碍物感知英文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/3d_obstacle_perception.md)
- [三维障碍物感知中文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/3d_obstacle_perception_cn.md)
- [二次规划路径样条优化](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/qp_spline_path_optimizer_cn.md)
- [二次规划st速度样条优化](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/qp_spline_st_speed_optimizer_cn.md)
- [参考线平滑设定](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/reference_line_smoother_cn.md)
- [交通信号灯感知](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/traffic_light_cn.md)

## 其他通用知识
- [坐标系统](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/coordination_cn.md)
- [Apollo安全更新SDK用户指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/apollo_secure_upgrade_user_guide-CN.md)



# Apollo 3.0 软件架构

自动驾驶Apollo3.0核心软件模块包括：

- **感知** — 感知模块识别自动驾驶车辆周围的世界。感知中有两个重要的子模块：障碍物检测和交通灯检测。
- **预测** — 预测模块预测感知障碍物的未来运动轨迹。
- **路由** — 路由模块告诉自动驾驶车辆如何通过一系列车道或道路到达其目的地。
- **规划** — 规划模块规划自动驾驶车辆的时间和空间轨迹。
- **控制** — 控制模块通过产生诸如油门，制动和转向的控制命令来执行规划模块产生的轨迹。
- **CanBus** — CanBus是将控制命令传递给车辆硬件的接口。它还将底盘信息传递给软件系统。
- **高精地图** — 该模块类似于库。它不是发布和订阅消息，而是经常用作查询引擎支持，以提供关于道路的特定结构化信息。
- **定位** — 定位模块利用GPS，LiDAR和IMU的各种信息源来定位自动驾驶车辆的位置。
- **HMI** — Apollo中的HMI和DreamView是一个用于查看车辆状态，测试其他模块以及实时控制车辆功能的模块.
- **监控** — 车辆中所有模块的监控系统包括硬件。
- **Guardian** — 新的安全模块，用于干预监控检测到的失败和action center相应的功能。
执行操作中心功能并进行干预的新安全模块应监控检测故障。

```
注意：下面列出了每个模块的详细信息。
```

这些模块的交互如下图所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/Apollo_3.0_SW.png)

每个模块都作为单独的基于CarOS的ROS节点运行。每个模块节点都发布和订阅特定topic。订阅的topic用作数据输入，而发布的topic用作数据输出。以下各节详细介绍了各模块情况。

## 感知

感知依赖LiDAR点云数据和相机原始数据。除了这些传感器数据输入之外，交通灯检测依赖定位以及HD-Map。由于实时ad-hoc交通灯检测在计算上是不可行的，因此交通灯检测需要依赖定位确定何时何地开始通过相机捕获的图像检测交通灯。
对Apollo 3.0的更改：
  - CIPV检测/尾随 - 在单个车道内移动。
  - 全线支持 - 粗线支持，可实现远程精确度。相机安装有高低两种不同的安装方式。
  - 异步传感器融合 – 因为不同传感器的帧速率差异——雷达为10ms，相机为33s，LiDAR为100ms，所以异步融合LiDAR，雷达和相机数据，并获取所有信息并得到数据点的功能非常重要。
  - 在线姿态估计 - 在出现颠簸或斜坡时确定与估算角度变化，以确保传感器随汽车移动且角度/姿态相应地变化。
  - 视觉定位 – 基于相机的视觉定位方案正在测试中。
  - 超声波传感器 – 作为安全保障传感器，与Guardian一起用于自动紧急制动和停车。

## 预测

预测模块负责预测所有感知障碍物的未来运动轨迹。输出预测消息封装了感知信息。预测订阅定位和感知障碍物消息，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/prediction.png)

当接收到定位更新时，预测模块更新其内部状态。当感知发出其发布感知障碍物消息时，触发预测实际执行。

## 定位

定位模块聚合各种数据以定位自动驾驶车辆。有两种类型的定位模式：OnTimer和多传感器融合。

第一种基于RTK的定位方法，通过计时器的回调函数“OnTimer”实现，如下所示。
![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/localization.png)

另一种定位方法是多传感器融合（MSF）方法，其中注册了一些事件触发的回调函数，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/localization_2.png)

## 路由
为了计算可通行车道和道路，路由模块需要知道起点和终点。通常，路由起点是自动驾驶车辆位置。重要的数据接口是一个名为`OnRoutingRequest`的事件触发函数，其中`RoutingResponse`的计算和发布如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/routing.png)

## 规划
Apollo 2.0需要使用多个信息源来规划安全无碰撞的行驶轨迹，因此规划模块几乎与其他所有模块进行交互。

首先，规划模块获得预测模块的输出。预测输出封装了原始感知障碍物，规划模块订阅交通灯检测输出而不是感知障碍物输出。
然后，规划模块获取路由输出。在某些情况下，如果当前路由结果不可执行，则规划模块还可以通过发送路由请求来触发新的路由计算。

最后，规划模块需要知道定位信息（定位：我在哪里）以及当前的自动驾驶车辆信息（底盘：我的状态是什么）。规划模块由固定频率触发，主数据接口是调用`RunOnce`函数的`OnTimer`回调函数。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/planning_1.png)

底盘，定位，交通灯和预测等数据依赖关系通过`AdapterManager`类进行管理。核心软件模块同样也由`AdapterManager`类管理。例如，定位通过`AdapterManager :: GetLocalization()`管理，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/planning_2.png)

## 控制
如规划模块中所述，控制将规划轨迹作为输入，并生成控制命令传递给CanBus。它有三个主要的数据接口：OnPad，OnMonitor和OnTimer。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/control_1.png)

`OnPad`和`OnMonitor`是仿真和HMI的交互接口。 主要数据接口是`OnTimer`，它定期产生实际的控制命令，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/control_2.png)

## CanBus

CanBus有两个数据接口。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/canbus_1.png)

第一个数据接口是基于计时器的发布者，回调函数为“OnTimer”。如果启用，此数据接口会定期发布底盘信息。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/canbus_2.png)

第二个数据接口是一个基于事件的发布者，回调函数为“OnControlCommand”，当CanBus模块接收到控制命令时会触发该函数。


## HMI
Apollo中的HMI或DreamView是一个Web应用程序：
     - 可视化自动驾驶模块的输出，例如，规划轨迹，汽车定位，底盘状态等。
     - 为用户提供人机交互界面，以查看硬件状态，打开/关闭模块，以及启动自动驾驶汽车。
     - 提供调试工具，如PnC Monitor，以有效跟踪模块问题。

## 监控
包括硬件在内的，车辆中所有模块的监控系统。监控模块从其他模块接收数据并传递给HMI，以便司机查看并确保所有模块都正常工作。如果模块或硬件发生故障，监控会向Guardian（新的操作中心模块）发送警报，然后决定需要采取哪些操作来防止系统崩溃。

## Guardian
这个新模块根据Monitor发送的数据做出相应决定。Guardian有两个主要功能：
     - 所有模块都正常工作 - Guardian允许控制模块正常工作。控制信号被发送到CANBus，就像Guardian不存在一样。
     - 监控检测到模块崩溃 - 如果监控检测到故障，Guardian将阻止控制信号到达CANBus并使汽车停止。 Guardian有三种方式决定如何停车并会依赖最终的Gatekeeper——超声波传感器，
         - 如果超声波传感器运行正常而未检测到障碍物，Guardian将使汽车缓慢停止
         - 如果传感器没有响应，Guardian会硬制动，使车马上停止。
         - 这是一种特殊情况，如果HMI通知驾驶员即将发生碰撞并且驾驶员在10秒内没有干预，Guardian会使用硬制动使汽车立即停止。

```
注意: 
1.在上述任何一种情况下，如果Monitor检测到任何模块或硬件出现故障，Guardian将始终停止该车。
2.监控器和Guardian解耦以确保没有单点故障，并且可以为Guardian模块添加其他行为且不影响监控系统，监控还与HMI通信。
```



# =========================================
# 感知
Apollo 3.0
June 27, 2018

## 简介
    Apollo 3.0 主要针对采用低成本传感器的L2级别自动驾驶车辆。
    在车道中的自动驾驶车辆通过一个前置摄像头和前置雷达要与关键车辆（在路径上最近的车辆）保持一定的距离。
    Apollo 3.0 支持在高速公路上不依赖地图的高速自动驾驶。
    深度网路学习处理图像数据，随着搜集更多的数据，深度网络的性能随着时间的推移将得到改善。


***安全警告***
    Apollo 3.0 不支持没有包含本地道路和说明标示的急转弯道路。
    感知模块是基于采用深度网络并结合有限数据的可视化检测技术。
    因此，在我们发布更好的网络之前，驾驶员应该小心驾驶并控制好车辆方向而不能依赖与自动驾驶。
    请在安全和限制区域进行试驾。

- ***推荐道路***
	- ***道路两侧有清晰的白色车道线***

- ***禁止***
	- ***急转弯道路***
	- ***没有车道线标记的道路***
	- ***路口***
	- ***对接点或虚线车道线***
	- ***公共道路***

## 感知模块
每个模块的流程图如下所示。

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_flow_chart_apollo_3.0.png)

**图 1: Apollo 3.0的流程图**

### 深度网络
    深度网络摄取图像并为Apollo 3.0提供两个检测输出，车道线和对象。
    目前，对深度学习中使用单一任务还是协同训练任务还存在一些争议。
    诸如车道检测网络或物体检测网络的单一网络通常比一个协同训练的多任务网络执行得更好。
    然而，在给定有限资源的情况下，多个单独的网络将是昂贵的并且在处理中消耗更多时间。
    因此，对于经济设计而言，协同训练是不可避免的，并且在性能上会有一些妥协。
    在 Apollo 3.0, YOLO [1][2] 被用作对象和车道线检测的基础网络。
    该对象具有车辆、卡车、骑车人和行人类别，并由表示成具有方向信息的2-D边界框。
    通过使用具有一些修改的相同网络进行分段来检测车道线。
    对于整条车道线，我们有一个单独的网络，
    以提供更长的车道线，无论是车道线是离散的还是连续的。


### 物体识别/跟踪
    在交通场景中，有两类物体: 静态物体和动态物体。
    静态物体包括车道线、交通信号灯以及数以千计的以各种语言写成的交通标示。
    除了驾驶之外，道路上还有多个地标，主要用于视觉定位，包括路灯，障碍物，道路上的桥梁或任何天际线。
    对于静态物体，Apollo 3.0将仅检测车道线.

    在动态物体中，Apollo在路上关心乘用车，卡车，骑自行车者，行人或任何其他物体，包括动物或身体部位。
    Apollo还可以根据物体所在的车道对物体进行分类。
    最重要的物体是CIPV（路径中最近的物体）。下一个重要对象将是相邻车道中的物体。


#### 2D-to-3D 边界框
    给定一个2D盒子，其3D大小和相机方向，该模块搜索相机坐标系统中的3D位置，
    并使用该2D盒子的宽度，高度或2D区域估计精确的3D距离。
    该模块可在没有准确的外部相机参数的情况下工作。

#### 对象跟踪
    对象跟踪模块利用多种信息，例如3D位置，2D图像补丁，2D框或深度学习ROI特征。
    跟踪问题通过有效地组合线索来表达为多个假设数据关联，
    以提供路径和检测到的对象之间的最正确关联，从而获得每个对象的正确ID关联。

### 车道检测/追踪
    在静态对象中，我们在Apollo 3.0中将仅处理通道线。
    该车道用于纵向和横向控制。
    车道本身引导横向控制，并且在车道内的对象引导纵向控制。

#### 车道线
    我们有两种类型的车道线，车道标记段和整个车道线。
    车道标记段用于视觉定位，整个车道线用于使车辆保持在车道内。
    该通道可以由多组折线表示，例如下一个左侧车道线，左侧线，右侧线和下一个右侧线。
    给定来自深度网络的车道线热图，通过阈值化生成分段的二进制图像。
    该方法首先找到连接的组件并检测内部轮廓。
    然后，它基于自我车辆坐标系的地面空间中的轮廓边缘生成车道标记点。
    之后，它将这些车道标记与具有相应的相对空间（例如，左（L0），右（R0），下左（L1），下（右）（L2）等）标签的若干车道线对象相关联。

### CIPV (最近路径车辆)
    CIPV是当前车道中最接近的车辆。
    对象由3D边界框表示，其从上到下视图的2D投影将对象定位在地面上。
    然后，检查每个对象是否在当前车道中。
    在当前车道的对象中，最接近的一个将被选为CIPV。

### 跟车
    跟车是跟随前车的一种策略。
    从跟踪对象和当前车辆运动中，估计对象的轨迹。
    该轨迹将指导对象如何在道路上作为一组移动并且可以预测未来的轨迹。
    有两种跟车尾随，一种是跟随特定车辆的纯尾随，
    另一种是CIPV引导的尾随，当检测到无车道线时，当前车辆遵循CIPV的轨迹。 

输出可视化的快照如图2所示。 
![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_visualization_apollo_3.0.png)

**图 2: Apollo 3.0中感知输出的可视化。左上角是基于图像的输出。左下角显示了对象的3D边界框。左图显示了车道线和物体的三维俯视图。CIPV标有红色边框。黄线表示每辆车的轨迹**

### 雷达 + 摄像头融合
    给定多个传感器，它们的输出应以协同方式组合。
    Apollo 3.0，介绍了一套带雷达和摄像头的传感器。
    对于此过程，需要校准两个传感器。每个传感器都将使用Apollo 2.0中介绍的相同方法进行校准。
    校准后，输出将以3-D世界坐标表示，每个输出将通过它们在位置，大小，时间和每个传感器的效用方面的相似性进行融合。
    在学习了每个传感器的效用函数后，摄像机对横向距离的贡献更大，雷达对纵向距离测量的贡献更大。
    异步传感器融合算法也作为选项提供。

### 伪车道
    所有车道检测结果将在空间上临时组合以诱导伪车道，
    该车道将被反馈到规划和控制模块。
    某些车道线在某帧中不正确或缺失。
    为了提供平滑的车道线输出，使用车辆里程测量的历史车道线。
    当车辆移动时，保存每个帧的里程表，并且先前帧中的车道线也将保存在历史缓冲器中。
    检测到的与历史车道线不匹配的车道线将被移除，历史输出将替换车道线并提供给规划模块。

### 超声波传感器
    Apollo 3.0支持超声波传感器。每个超声波传感器通过CAN总线提供被检测对象的距离。
    来自每个超声波传感器的测量数据被收集并作为ROS主题广播。
    将来，在融合超声波传感器后，物体和边界的地图将作为ROS的输出发布。

## 感知输出
PnC的输入将与之前基于激光雷达的系统的输入完全不同。

- 车道线输出
	- 折线和/或多项式曲线
	- 车道类型按位置：L1（左下车道线），L0（左车道线），R0（右车道线），R1（右下车道线

- 对象输出
	- 3D长方体
	- 相对速度和方向
	- 类型：CIPV，PIHP，其他
	- 分类：汽车，卡车，自行车，行人
	- Drops：物体的轨迹

世界坐标是3D中的当前车辆坐标，其中后中心轴是原点。

## 参考
[1] J Redmon, S Divvala, R Girshick, A Farhadi, "你只看一次：统一的实时物体检测" CVPR 2016

[2] J Redmon, A Farhadi, "YOLO9000: 更好, 更快, 更强," arXiv preprint


3D 障碍物感知
=======================================

Apollo解决的障碍物感知问题：

- 高精地图ROI过滤器（HDMap ROI Filter）
- 基于卷积神经网络分割（CNN Segmentation）
- MinBox 障碍物边框构建（MinBox Builder）
- HM对象跟踪（HM Object Tracker）

高精地图ROI过滤器
-------------------------------------

ROI（The Region of Interest）指定从高精地图检索到包含路面、路口的可驾驶区域。高精地图 ROI 过滤器（往下简称“过滤器”）处理在ROI之外的激光雷达点，去除背景对象，如路边建筑物和树木等，剩余的点云留待后续处理。

给定一个高精地图，每个激光雷达点的关系意味着它在ROI内部还是外部。
每个激光雷达点可以查询一个车辆周围区域的2D量化的查找表（LUT）。过滤器模块的输入和输出汇总于下表。

  |输入                                                                     |输出                                                                     |
  |------------------------------------------------------------------------- |---------------------------------------------------------------------------|
  |点云: 激光雷达捕捉的3D点数据集           | 由高精地图定义的ROI内的输入点索引。      |
  |高精地图: 多边形集合，每个多边形均含有一个有序的点集。     |                                       |
 
一般来说，Apollo 高精地图 ROI过滤器有以下三步：

1. 坐标转换
2. ROI LUT构造
3. ROI LUT点查询

### 坐标转换

对于（高精地图ROI）过滤器来说，高精地图数据接口被定义为一系列多边形集合，每个集合由世界坐标系点组成有序点集。高精地图ROI点查询需要点云和多边形处在相同的坐标系，为此，Apollo将输入点云和HDMap多边形变换为来自激光雷达传感器位置的地方坐标系。

### ROI LUT构造

Apollo采用网格显示查找表（LUT），将ROI量化为俯视图2D网格，以此决定输入点是在ROI之内还是之外。

如图1所示，该LUT覆盖了一个矩形区域，该区域位于高精地图边界上方，以普通视图周围的预定义空间范围为边界。它代表了与ROI关联网格的每个单元格（如用1/0表示在ROI的内部/外部）。 为了计算效率，Apollo使用 **扫描线算法**和 **位图编码**来构建ROI LUT。

<img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/roi_lookup_table.png">
<div align=center>图 1 ROI显示查找表（LUT）</div>

蓝色线条标出了高精地图ROI的边界，包含路表与路口。红色加粗点表示对应于激光雷达传感器位置的地方坐标系原始位置。2D网格由8*8个绿色正方形组成，在ROI中的单元格，为蓝色填充的正方形，而之外的是黄色填充的正方形。

### ROI LUT点查询

基于ROI LUT，查询每个输入点的关系使用两步认证。对于点查询过程，Apollo数据编译输出如下，:

1. 检查点在ROI LUT矩形区域之内还是之外。
2. 查询LUT中相对于ROI关联点的相应单元格。
3. 收集属于ROI的所有点，并输出其相对于输入点云的索引。

用户定义的参数可在配置文件`modules/perception/model/hdmap_roi_filter.config`中设置，HDMap ROI Filter 参数使用参考如下表格：

  |参数名称      |使用                                                                          |默认     |
  |------------------- |------------------------------------------------------------------------------ |------------|
  |range           | 基于LiDAR传感器点的2D网格ROI LUT的图层范围），如(-70, 70)*(-70, 70) |70.0 米 |
  |cell_size           | 用于量化2D网格的单元格的大小。                                   |0.25 米  |
  |extend_dist         | 从多边形边界扩展ROI的距离。                 |0.0 米   |

基于CNN的障碍物分割
------------------------------------------------
高精地图 ROI过滤之后，Apollo得到已过滤、只包含属于ROI内的点云，大部分背景障碍物，如路侧的建筑物、树木等均被移除，ROI内的点云被传递到分割模块。分割模块检测和划分前景障碍物，例如汽车，卡车，自行车和行人。

  |输入                                                                        |输出                             |
  |----------------------------------------------------------------------------|---------------------------------------------------------------|
  |点云（3D数据集）                                         |对应于ROI中的障碍物对象数据集    |
  |表示在HDMap中定义的ROI内的点的点索引       |                               |                                                                              
Apollo 使用深度卷积神经网络提高障碍物识别与分割的精度，障碍物分割包含以下四步：
- 通道特征提取
- 基于卷积神经网络的障碍物预测
- 障碍物集群
- 后期处理

卷积神经网络详细介绍如下：

### 通道特征提取

给定一个点云框架，Apollo在地方坐标系中构建俯视图（即投影到X-Y平面）2D网格。 基于点的X、Y坐标，相对于LiDAR传感器原点的预定范围内，每个点被量化为2D网格的一个单元。 量化后，Apollo计算网格内每个单元格中点的8个统计测量，这将是下一步中传递给CNN的输入通道特征。 

计算的8个统计测量：

1. 单元格中点的最大高度
2. 单元格中最高点的强度
3. 单元格中点的平均高度
4. 单元格中点的平均强度
5. 单元格中的点数
6. 单元格中心相对于原点的角度
7. 单元格中心与原点之间的距离
8. 二进制值标示单元格是空还是被占用

### 基于卷积神经网络的障碍物预测

基于上述通道特征，Apollo使用深度完全卷积神经网络（FCNN）来预测单元格障碍物属性，包括潜在物体中心的偏移位移（称为中心偏移）、对象性
积极性和物体高度。如图2所示，网络的输入为 *W* x *H* x *C* 通道图像，其中：

- *W* 代表网格中的列数
- *H* 代表网格中的行数
- *C* 代表通道特征数

完全卷积神经网络由三层构成：
- 下游编码层（特征编码器）
- 上游解码层（特征解码器）
- 障碍物属性预测层（预测器）

特征编码器将通道特征图像作为输入，并且随着特征抽取的增加而连续**下采样**其空间分辨率。 然后特征解码器逐渐对特征图像 **上采样**到输入2D网格的空间分辨率，可以恢复特征图像的空间细节，以促进单元格方向的障碍物位置、速度属性预测。 根据具有非线性激活（即ReLu）层的堆叠卷积/分散层来实现 **下采样**和 **上采样**操作。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/FCNN.png" width="99%"></div>

<div align=center>图 2 FCNN在单元格方向上的障碍物预测</div>

### 障碍物聚类
在基于CNN的预测之后，Apollo获取单个单元格的预测信息。利用四个单元对象属性图像，其中包含：

- 中心偏移
- 对象性
- 积极性
- 对象高度

为生成障碍物，Apollo基于单元格中心偏移，预测构建有向图，并搜索连接的组件作为候选对象集群。

如图3所示，每个单元格是图的一个节点，并且基于单元格的中心偏移预测构建有向边，其指向对应于另一单元的父节点。

如图3，Apollo采用压缩的联合查找算法（Union Find algorithm ）有效查找连接组件，每个组件都是候选障碍物对象集群。对象是单个单元格成为有效对象的概率。因此，Apollo将非对象单元定义为目标小于0.5的单元格。因此，Apollo过滤出每个候选对象集群的空单元格和非对象集。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/obstacle_clustering.png" width="99%"></div>

<div align=center>图 3 障碍聚类</div>

(a) 红色箭头表示每个单元格对象中心偏移预测；蓝色填充对应于物体概率不小于0.5的对象单元。

(b) 固体红色多边形内的单元格组成候选对象集群。

由五角星填充的红色范围表示对应于连接组件子图的根节点（单元格）。 

一个候选对象集群可以由其根节点彼此相邻的多个相邻连接组件组成。

### 后期处理

聚类后，Apollo获得一组候选对象集，每个候选对象集包括若干单元格。 

在后期处理中，Apollo首先对所涉及的单元格的积极性和物体高度值，平均计算每个候选群体的检测置信度分数和物体高度。 然后，Apollo去除相对于预测物体高度太高的点，并收集每个候选集中的有效单元格的点。 最后，Apollo删除具有非常低的可信度分数或小点数的候选聚类，以输出最终的障碍物集/分段。

用户定义的参数可以在`modules/perception/model/cnn_segmentation/cnnseg.conf`的配置文件中设置。 下表说明了CNN细分的参数用法和默认值：


 |参数名称             |使用说明                                           |默认值    |
 |-----------------------------------|--------------------------------------------------------------------------------------------|-----------|
 |objectness_thresh                  |用于在障碍物聚类步骤中过滤掉非对象单元的对象的阈值。 |0.5        |
 |use_all_grids_for_clustering       |指定是否使用所有单元格在障碍物聚类步骤中构建图形的选项。如果不是，则仅考虑占用的单元格。   |true   |
 |confidence_thresh                  |用于在后期处理过程中滤出候选聚类的检测置信度得分阈值。    |0.1    |
 |height_thresh                      |如果是非负数，则在后处理步骤中将过滤掉高于预测物体高度的点。 |0.5 meters |
 |min_pts_num                        |在后期处理中，删除具有小于min_pts_num点的候选集群。 |3   |
 |use_full_cloud                     |如果设置为true，则原始点云的所有点将用于提取通道特征。 否则仅使用输入点云的点（即，HDMap ROI过滤器之后的点）。  |true |
 |gpu_id                             |在基于CNN的障碍物预测步骤中使用的GPU设备的ID。            |0          |
 |feature_param {width}              |2D网格的X轴上的单元格数。                      |512        |
 |feature_param {height}             |2D网格的Y轴上的单元格数。                     |512        |
 |feature_param {range}              |2D格栅相对于原点（LiDAR传感器）的范围。             |60 meters  |

**注意：提供的模型是一个样例，仅限于实验所用。**

MinBox 障碍物边框构建
--------------

对象构建器组件为检测到的障碍物建立一个边界框。因为LiDAR传感器的遮挡或距离，形成障碍物的点云可以是稀疏的，并且仅覆盖一部分表面。因此，盒构建器将恢复给定多边形点的完整边界框。即使点云稀疏，边界框的主要目的还是预估障碍物（例如，车辆）的方向。同样地，边框也用于可视化障碍物。

算法背后的想法是找到给定多边形点边缘的所有区域。在以下示例中，如果AB是边缘，则Apollo将其他多边形点投影到AB上，并建立具有最大距离的交点对，这是属于边框的边缘之一。然后直接获得边界框的另一边。通过迭代多边形中的所有边，在以下图4所示，Apollo确定了一个6边界边框，将选择具有最小面积的方案作为最终的边界框。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/object_building.png"></div>

<div align=center>图 4 MinBox 对象构建</div>

HM对象跟踪
-----------------

HM对象跟踪器跟踪分段检测到的障碍物。通常，它通过将当前检测与现有跟踪列表相关联，来形成和更新跟踪列表，如不再存在，则删除旧的跟踪列表，并在识别出新的检测时生成新的跟踪列表。 更新后的跟踪列表的运动状态将在关联后进行估计。 在HM对象跟踪器中，**匈牙利算法**(Hungarian algorithm)用于检测到跟踪关联，并采用 **鲁棒卡尔曼滤波器**(Robust Kalman Filter) 进行运动估计。

### 检测跟踪关联（Detection-to-Track Association）

当将检测与现有跟踪列表相关联时，Apollo构建了一个二分图，然后使用 **匈牙利算法**以最小成本（距离）找到最佳检测跟踪匹配。

**计算关联距离矩阵**

首先，建立一个关联距离矩阵。根据一系列关联特征（包括运动一致性，外观一致性等）计算给定检测和一条轨迹之间的距离。HM跟踪器距离计算中使用的一些特征如下所示：

  |关联特征名称 |描述                       |
  |-------------------------|----------------------------------|
  |location_distance        |评估运动一致性                      |
  |direction_distance       |评估运动一致性                       |
  |bbox_size_distance       |评估外观一致性 |
  |point_num_distance       |评估外观一致性 |
  |histogram_distance       |评估外观一致性 |

此外，还有一些重要的距离权重参数，用于将上述关联特征组合成最终距离测量。

**匈牙利算法的二分图匹配**

给定关联距离矩阵，如图5所示，Apollo构造了一个二分图，并使用 **匈牙利算法**通过最小化距离成本找到最佳的检测跟踪匹配。它解决了O(n\^3)时间复杂度中的赋值问题。 为了提高其计算性能，通过删除距离大于合理的最大距离阈值的顶点，将原始的二分图切割成子图后实现了匈牙利算法。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/bipartite_graph_matching.png"></div>

<div align=center>图 5 二分图匹配（Bipartite Graph Matching）</div>

### 跟踪动态预估 （Track Motion Estimation）

在检测到跟踪关联之后，HM对象跟踪器使用 **鲁棒卡尔曼滤波器**来利用恒定速度运动模型估计当前跟踪列表的运动状态。 运动状态包括锚点和速度，分别对应于3D位置及其3D速度。 为了克服由不完美的检测引起的可能的分心，在跟踪器的滤波算法中实现了鲁棒统计技术。

**观察冗余**

在一系列重复观测中选择速度测量，即滤波算法的输入，包括锚点移位、边界框中心偏移、边界框角点移位等。冗余观测将为滤波测量带来额外的鲁棒性， 因为所有观察失败的概率远远小于单次观察失败的概率。

**分解**

高斯滤波算法 （Gaussian Filter algorithms）总是假设它们的高斯分布产生噪声。 然而，这种假设可能在运动预估问题中失败，因为其测量的噪声可能来自直方分布。 为了克服更新增益的过度估计，在过滤过程中使用故障阈值。

**更新关联质量**

原始卡尔曼滤波器更新其状态不区分其测量的质量。 然而，质量是滤波噪声的有益提示，可以估计。 例如，在关联步骤中计算的距离可以是一个合理的测量质量估计。 根据关联质量更新过滤算法的状态，增强了运动估计问题的鲁棒性和平滑度。

HM对象跟踪器的高级工作流程如图6所示。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/hm_object_tracker.png"></div>

<div align=center>图 6 HM对象跟踪器工作流</div>

1）构造跟踪对象并将其转换为世界坐标。

2）预测现有跟踪列表的状态，并对其匹配检测。

3）在更新后的跟踪列表中更新运动状态，并收集跟踪结果。

## 参考
- [匈牙利算法](https://zh.wikipedia.org/zh-cn/%E5%8C%88%E7%89%99%E5%88%A9%E7%AE%97%E6%B3%95)
- [地方坐标系](https://baike.baidu.com/item/%E5%9C%B0%E6%96%B9%E5%9D%90%E6%A0%87%E7%B3%BB/5154246)
- [Fully Convolutional Networks for Semantic Segmentation](https://people.eecs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf)



# ===========================================
# Planning模块架构和概述

## 数据输入和输出

### 输出数据

Planning模块的输出数据类型定义在`planning.proto`，如下图所示：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image001.png)

#### *planning.proto*

在proto数据的定义中，输出数据包括总时间、总长度和确切的路径信息，输出数据由控制单元解析执行，输出数据结构定义在`repeated apollo.common.TrajectoryPointtrajectory_point`。

`trajectory point`类继承自`path_point`类，并新增了speed、acceleration和timing属性。
定义在`pnc_point.proto`中的`trajectory_point`包含了路径的详细属性。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image002.png)

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image003.png)

除了路径信息，Planning模块输出了多种注释信息。主要的注释数据包括：

- Estop
- DecisionResult
- 调试信息

`Estop`是标示了错误和异常的指令。例如，当自动驾驶的车辆碰到了障碍物或者无法遵守交通规则时将发送estop信号。`DecisionResult`主要用于展示模拟的输出结果以方便开发者更好的了解Planning模块的计算结果。更多详细的中间值结果会被保存并输出作为调试信息供后续的调试使用。

## 输入数据

为了计算最终的输出路径，Planning模块需要统一的规划多个输入数据。Planning模块的输入数据包括：

- Routing
- 感知和预测
- 车辆状态和定位
- 高清地图

Routing定义了概念性问题“我想去哪儿”，消息定义在`routing.proto`文件中。`RoutingResponse`包含了`RoadSegment`，`RoadSegment`指明了车辆到达目的地应该遵循的路线。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image004.png)

关于概念性问题“我周围有什么”的消息定义在`perception_obstacles.proto`和`traffic_light_detection.proto`中。`perception_obstacles.proto`定义了表示车辆周围的障碍物的数据，车辆周围障碍物的数据由感知模块提供。`traffic_light_detection`定义了信号灯状态的数据。除了已被感知的障碍物外，动态障碍物的路径预测对Planning模块也是非常重要的数据，因此`prediction.proto`封装了`perception_obstacle`消息来表示预测路径。请参考下述图片：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image005.png)

每个预测的路径都有其单独的可能性，而且每个动态障碍物可能有多个预测路径。

除了概念性问题“我想去哪儿”和“我周围有什么”，另外一个重要的概念性问题是“我在哪”。关于该问题的数据通过高清地图和定位模块获得。定位信息和车辆车架信息被封装在`VehicleState`消息中，该消息定义在`vehicle_state.proto`，参考下述图片：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image009.png)

## 代码结构和类层次

代码组织方式如下图所示：Planning模块的入口是`planning.cc`。在Planning模块内部，重要的类在下图中展示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image006.png)

`ReferenceLineInfo`对`ReferenceLine`类进行了封装，为Planning模块提供了平滑的指令执行序列。
**Frame**包含了所有的数据依赖关系，例如包含了预测路径信息的障碍物，自动驾驶车辆的状态等。
**HD-Ma**p在Planning模块内作为封装了多个数据的库使用，提供不同特点的地图数据查询需求。
**EM Planne**r执行具体的Planning任务，继承自**Planner**类。Apollo2.0中的**EM Planner**类和之前发布的**RTK Planner**类都继承自Planner类。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image007.png)

例如，在EM Planner执行的一次planning循环的内部，采用迭代执行的方法，tasks的三个类别交替执行。“**决策/优化**”类的关系在下述图片中展示：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image008.png)

- **Deciders** 包括 traffic decider, path decider and speed decider.

- **Path Optimizers** 为DP/QP path optimizers.

- **Speed Optimizers** 为DP/QP speed optimizers.

| **附注：**                                |
| ---------------------------------------- |
| DP表示动态规划（dynamic programming），QP表示二次规划（quadratic programming）。经过计算步骤后，最终的路径数据经过处理后传递到下一个节点模块进行路径的执行。 |




# ==========================
# Apollo 3.0传感器安装指南

## 需要的硬件

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_required_hardware.png)

外部设备

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_peripherals.png)

## 坐标系

单位：毫米（mm）

原点：车辆后轮轴中心

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure1.png)

**Figure 1. 原点和坐标系**

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure2.png)

**Figure 2. 卡车坐标系和安装摄像机与雷达的示意图**

## 传感器安装指南
###	IMU/GPS
IMU/GPS需要安装在靠近后车轮毂的位置。GPS天线需要安装在车辆顶部。
###	Radar
远程雷达需要安装在车辆前保险杠上，请参考Figure 1 and Figure 2展示的信息。
###	Camera
一个6mm镜头的摄像机应该面向车辆的前方。前向摄像机应当安装在车辆前部的中心位置，离地面高度为1600mm到2000mm（Camera 1），或者安装在车辆挡风玻璃上（Camera 2）。

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure3.png)

**Figure 3. 安装摄像机的示例图**

摄像机安装完成后，摄像机w、r、t的物理坐标x、y、z应该被记录在校准文件里。

#### 安装摄像机后的检验

三个摄像机的方位应当全部设置为0。摄像机安装后，需要车辆在公路以直线开动一段距离并记录一个rosbag，通过rosbag的回放，摄像机的方位需要重新调整以设置间距、偏航角并将角度转置为0度。如果摄像机被正确的安装，地平线应该在画面高度方向上的正中间并且不倾斜。灭点同样应该在画面的正中间。请参考下述图片以将摄像机设置为最佳状态：

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure4.png)

**Figure 4. 摄像机安装后的画面示例。地平线应该在画面高度方向上的正中间并且不倾斜。灭点同样应该在画面的正中间。 红色线段显示了画面高度和宽度方向上的中点。**

估测的平移参数的示例如下所示：
```
header:
    seq: 0
    stamp:
        secs: 0
        nsecs: 0
    frame_id: white_mkz
child_frame_id: onsemi_obstacle
transform:
    rotation:
        x:  0.5
        y: -0.5
        z:  0.5
        w: -0.5
    translation:	
        x: 1.895
        y: -0.235
        z: 1.256 
```
如果角度不为0，则上述数据需要重新校准并在四元数中表示（参考上例中的transform->rotation	）
