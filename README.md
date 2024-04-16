# HumanGestureRadarDetection

人体姿态识别软件项目

负责内容：

  1、将雷达采集的数据从串口接收并展示的QT开发

  2、软件的UI设计和测试

功能包括：

  1、雷达3D点云[25fps]、Kinect人体骨架[30fps][采集的数据用于算法部去训练模型]和深度信息数据的并发显示

  2、数据回放显示、数据保存、雷达串口数据帧解析

  3、TcpSocket数据通信[数据发送，支持1000fps]

  4、点云数据的累积显示、时间累积显示和距离筛选显示，窗口坐标的绘制

难点：

  1、数据的并发显示。对于同一个窗口要同时显示来自两个不同设备的雷达点云和人体骨架信息，
    解决方法：这里采用上锁同步的形式，当两种数据都采集了准备好的时候才会更新并发窗口AllOpenglWidget，
    缺点是这里是只有一种数据的时候并发窗口不会显示，不过在独立的窗口会显示。

  2、数据的定时保存。目的采取定时保存的策略能解决采集的数据占满内存资源的问题。
    解决方法：1️⃣、采用定时器来定时保存；2️⃣、采用累积帧的数量来触发保存；
