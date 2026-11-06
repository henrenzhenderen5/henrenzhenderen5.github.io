---
layout: single
title: "视觉引导的井字棋机械臂"
permalink: /portfolio-zh/tic-tac-toe-robot/
author_profile: true
lang: zh-CN
---

[返回中文作品集]({{ '/portfolio-zh/' | relative_url }}) · [English project page]({{ '/portfolio/tic-tac-toe-robot/' | relative_url }})

## 项目概述

我们做了一台能和人对弈的井字棋机械臂。OpenMV 相机识别棋盘、棋子和备用棋的位置，嵌入式程序判断下一步落子，再由机械臂完成实际抓放。系统也支持手动指定棋子颜色和目标格。

![视觉引导的井字棋机械臂]({{ '/images/portfolio/tic-tac-toe-cover.jpg' | relative_url }})

## 我的工作

- 在 OpenMV 上用 MicroPython 编写棋盘和棋子识别程序。
- 参与嵌入式模块间通信、PCB 装配与焊接。
- 参与视觉识别、游戏逻辑和机械执行的整机联调。

## 技术实现

1. **棋盘与棋子识别。** 检测并筛选两个方向的棋盘网格线，计算交点和九个格心，再用多帧坐标平滑减小抖动。棋子通过圆检测定位，通过局部亮度区分黑白。
2. **落子决策。** 将实体棋盘转成三行三列的棋局。对弈程序在后续机器回合用 Minimax 评估可落子的位置，并把目标格号交给运动模块。
3. **运动与抓放。** 把取棋点和目标格心的像素坐标换算成机械臂工作平面上的坐标，再通过二连杆逆运动学求两个水平关节角。水平舵机将末端移动到取棋点和落棋点，末端舵机带动磁吸机构完成抓放。

## 使用工具

OpenMV、MicroPython、SolidWorks、串口通信、PCB 装配与焊接。

## 演示和源码

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 8px;">
  <iframe title="视觉引导的井字棋机械臂演示" loading="lazy" src="https://player.bilibili.com/player.html?bvid=BV17ju56cEC8&page=1&high_quality=1&danmaku=0" 
          scrolling="no" 
          border="0" 
          frameborder="no" 
          framespacing="0" 
          allowfullscreen="true" 
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

- [Bilibili 项目演示](https://www.bilibili.com/video/BV17ju56cEC8/)
- [GitHub 团队项目源码](https://github.com/Yuxuan0919/Automatic-Chess-Robot-Arm-for-Tic-Tac-toe)
