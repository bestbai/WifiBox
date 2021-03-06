# PSA 车载 WiFi 协议盒开源说明

一、项目背景：
=======

2008年底，在朋友的介绍下，我买了一辆标致307。买车的时候，4S店送了所谓的DVD导航一体机，把我车上原厂的CD拆走了。当时我对车子不了解，后面才发现没法修改A屏时间了，而A屏的时间每个月大概会快5分钟的样子，只能忍着，然后在做保养的时候，让师傅帮忙调一下时间。后面忍无可忍了，就想通过技术手段解决这个问题。

初期的想法很简单，就是想模拟CD上设置A屏的几个按钮，能改时间就行。结果从了解CAN总线、自己动手制作解码硬件、解析车辆协议、制作协议转换板硬件、制作客户端软件、设计UI、自研UI引擎、支持动态更换主题、支持跨平台、设计WiFi协议盒硬件、重构通讯协议、重新设计UI，一路走来经历了六七个年头。期间还有一些衍生的项目，比如支持VAN总线、V2C项目、CD唤醒板、通过音响手柄控制阿尔派机头等。在整个过程中，得到了广大车友和网友的大力支持，在此一并表示感谢！这些成果或多或少的在xcar和其他网站有所提及，感兴趣的同学可以翻看相关的帖子。

由于个人能力和精力有限，尤其是最近几年忙于处理其他事情，项目基本上是停滞的状态，深感愧对大家。为了能够让项目继续前行，我决定把项目涉及的软硬件开源，把它打造成一款开源的产品，希望有能力、有精力、有热情的同学能够站出来，众人拾柴火焰高。把它做成能够支持多车系的开源产品！

二、项目现状
======

目前基本完成了标致雪铁龙车系的CAN、VAN总线解析，设计并小规模制作了一批硬件，实现了PC端及Android端的UI。

  

三、产品功能
======

  

1WiFi协议盒硬件功能
------------

WiFi协议盒是之前CAN总线协议板的升级。协议盒内置解码板及无线路由器，可以用手机、Pad、及电脑连接协议盒获取车辆信息及对车辆进行必要的控制。利用协议盒配合手机等终端，可以实现车载电脑可以实现的功能

 
 

1）协议盒接口

*   有线网口x1 ，用于配置及固件升级
    
*   TTL电平串口×2，用于固件升级、连接胎压仪或第三方雷达等
    
*   2.4G天线接口X1，用于连接WiFi天线
    
*   USB接口x1，用于连接3G/4G上网卡或者摄像头等设备
    
*   4路AD输入, 用于电压测量，状态监控等扩展功能
    
*   4路继电器控制输出, 用于控制用户自己加装的第三方设备，PCB上预留了7路继电器控制能力
    

2、协议盒基本功能

*   车辆信息获取
    
    *   里程、车速、转速、水温、油量、平均油耗、电瓶电压、灯光状态、车门状态、雷达距离、胎压等。具体的信息要依据车型而定
        
*   车辆告警获取
    
    *   油量过低、手刹未放、安全带未系、气囊关闭、ESP关闭、ABS异常、车门、雷达、胎压等告警
        
*   CAN总线控制报文发送
    
    *   模拟包括按钮在内的各种控制报文，实现对音响、车窗、车门等控制，具体功能要依车型而定
        
*   ACC状态检测
    
*   工作
    
*   通过协议盒协议实现整车WiFi覆盖，随时随地上网
    
    *   支持通过USB插入4G上网卡
        
    *   支持Android手机 USB网络共享
        
*   倒车灯状态检测
    

3、协议盒扩展功能

*   通过板子的扩展IO监控车辆状态
    
*   自带线路电压监控，可以检测输入电压
    
*   可以扩展4路电压监控，需要用户自己接线到被监控设备
    
*   扩展的监控电压也可以作为开关量使用
    
*   通过板子的扩展IO实现第三方设备开关控制
    
*   通过板载的继电器，控制用户自己加装的设备
    
*   位置追踪，已经预留GPS模块安装位置
    

  

2UI基本功能
-------

*   车辆数据显示
    
    *   显示来自协议盒的CAN总线各类数据
        
*   车辆控制
    
    *   通过协议盒模拟车上按钮控制门、窗、音响等
        
    *   通过控制协议盒的继电器控制用户扩展设备
        
*   驾驶安全提醒及驾驶辅助：
    
    *   以语音及图文方式提醒用户系好安全带
        
    *   车速过快提醒
        
    *   手刹未放提醒
        
    *   提醒手动档用户换档，帮助新手学习、避免老手走神
        
*   语音控制(目前仅Windows版本支持)
    
    *   通过语言控制车辆音响
        
    *   通过语音控制车门、车窗等
        
    *   播报路况、天气等信息
        

*   油耗统计(待实现)：
    
    *   自动记录加油情况，油价可以通过互联网实时获取，也可以手工输入
        
    *   自动根据车辆油量变化统计每次、每日、每周、每月及每年的油耗及费用开支并
        
*   保养提醒(待实现)
    
    *   根据行驶里程及保养周期自动提醒用户保养
        
*   主题在线下载(待实现)
    

四、协议盒使用场景
=========

1基础篇
----

*   利用手机或者Pad作为车辆的数字显示屏显示车辆状况，提升显示效果
    
*   改造仪表盘，利用闲置旧手机升级为中文显示器
    
*   对于喜欢DIY的车友，可以安装一个专用的Pad或者车载电脑在车上配合协议盒一起使用
    

2遥控器篇
-----

*   通过手机WiFi连接协议盒，使用手机做遥控器
    
*   利用手机模拟车上按钮，遥控车门、车窗及车上的音响，比如在后排遥控收音机换台
    
*   利用手机控制用户自己加装的第三方设备
    

3车载WiFi篇
--------

*   借助3G、4G上网卡，利用WiFi协议盒的WiFi热点功能，实现整车WiFi热点覆盖，满足随时随地上网需求。
    

4远程监控篇
------

*   通过3G上网卡，在远方利用手机或者电脑了解车辆状况，甚至对车辆进行必要的控制。该功能需要搭建服务器。
    
*   可以通过协议盒上自带的USB接口加装支持的USB摄像头，通过手机或者Pad监控车辆
    
*   可以利用这一功能做倒车影像，验证通过
    

四、如何参与
======

产品软硬件后续我会陆续将代码公布在github上。无论是具备开发能力的车友还是普通用户，都可以参与。

**作为软件开发者，您可以：**

*   下载代码，自己修改、编译代码
    
*   提交代码的修改
    
*   创建自己的项目
    

**作为硬件开发者，您可以：**

*   下载原理图，自己修改，制作硬件
    
*   提交对原理图的修改
    
*   创建自己的项目
    

**作为美工开发者，您可以：**

*   下载UI资源，自己修改，制作主题
    
*   提交自己设计的主题
    
*   创建自己的项目
    

**作为普通用户，您可以：**

*   下载已经编译好的软件版本
    
*   自己修改，制作主题
    
*   提交自己设计的主题
    
*   创建自己的项目
    
*   硬件暂时可以从我这里获取（之前项目还有少量存余）
    

五、FAQ
=====

*   协议盒支持哪些车型
    

目前支持PSA集团的标致和雪铁龙的车型：如307、308、408、508、世嘉、C5等。技术上可以支持其它品牌的更多车系。前期尝试过Focus和本田CRV部分数据的解析，取得了部分成功，后面时间关系没有深入开展。

*   协议盒接线是否复杂？
    

基本功能只需要连接ACC、12v常电 、地、CAN总线即可

*   协议盒可以连接几路CAN总线？、
    

提供两路CAN总线

*   协议盒支持VAN总线吗？
    

支持，内置了V2C+功能。

*   手机或Pad怎么固定？
    

这个因车型而异了，建议通过支架将手机或Pad固定在车上。对于喜欢DIY的车友，可以安装一个专用的Pad或者车载电脑在车上配合协议盒一起使用
