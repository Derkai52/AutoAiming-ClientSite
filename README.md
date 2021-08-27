# Yolo-AutoAiming

![image-20210828013134657](https://gitee.com/Derkai52/image/raw/master/image/202108280131844.png)



# 一、概述

**这是一个处理屏幕推流图像和虚拟键鼠自动控制的程序**



我们使用了两台计算机去运行这个项目。其中一台负责进行游戏的被称为**客户端**；另外一台负责图像处理的被称为**运算端**。

> 当然你也可以用一台计算机完成这个项目。但与此同时你需要更高的硬件配置才能达到同等的效果。





**整体流程图参考如下：**

![image-20210828004132579](https://gitee.com/Derkai52/image/raw/master/image/202108280041639.png)

1、启动程序后，**客户端**获取画面并通过网络通信推流给**运算端**。

2、**运算端**处理画面帧后通过网络通信返回目标信息给**客户端**。

3、此时**客户端**根据监听到的目标信息自动完成键鼠控制。



# 二、测试信息概览

**1、平台环境：**

> Ubuntu 16.04 LST 及以上

**2、运算端主要硬件参数：**

> CPU: i7-9750H 3.9GHz
>
> GPU: GTX1650 Max-Q 4G

**3、网络模型：YoloV4-Tiny**

> 网络模型信息详见：ReadMe_Model.txt



在改善了各环节的处理瓶颈后，最新版本的测试结果大约为 **40 FPS**

**4、部分测试效果展示(仅供预览，非最终效果)：**

[Auto-Aiming测试部分展示](https://www.bilibili.com/video/BV17f4y1L7N4)



# 三、使用:
1. 保证两台机器(或本地处理)都处于同一局域网下。
2. 关闭防火墙和代理；保证网络通信正常。
3. 保证首先启动 Display-server.py 并根据提示输入**运算端** IP号 和 端口。再启动 pil_test.py 和 virtual_keyboard.py
4. 检查**运算端**环境(详见 readme.txt )，启动**运算端** predict.py



# 四、方案的补充说明

## 1、屏幕捕捉

尝试了3种方案，可在 **prtScr** 中找到，最开始使用 **Pillow** 的库，但是帧率只能到 20 FPS，且截图区域的大小和速度关系不大，**pyqt** 的方案也大概是 20 FPS，**mss** 的帧率和截图区域有比较强的关系，选择合适大小后，最终裁切后的画面采集帧率能保证 40 FPS

## 2、推流

Display_sent.py 通过 TCP 发送图像至 Display-server.py, Display-server.py 通过 web 推到局域网

## 3、键鼠控制

使用的是 [DD虚拟鼠标][http://www.ddxoft.com/]，免费版，会偶发性出现按键控制失效，同时每次使用需要联网验证激活，必须管理员权限运行。暂时先这样，有时间试试 [pydirectinput](https://github.com/learncodebygaming/pydirectinput)



