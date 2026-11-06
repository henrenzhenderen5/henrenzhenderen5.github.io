---
layout: single
title: "超外差频谱分析仪"
permalink: /portfolio-zh/superheterodyne-spectrum-analyzer/
author_profile: true
lang: zh-CN
---

[返回中文作品集]({{ '/portfolio-zh/' | relative_url }}) · [English project page]({{ '/portfolio/superheterodyne-spectrum-analyzer/' | relative_url }})

## 项目概述

我们三人组队参加 2025 年复旦大学电子设计竞赛，搭建了一台基于超外差架构的频谱分析仪。仪器把射频输入变换到固定中频，逐点测量信号功率，并在 LCD 上绘制频谱。项目获一等奖，题目组第一。

![超外差频谱分析仪]({{ '/images/portfolio/spectrum-analyzer-cover.jpg' | relative_url }})

## 我的工作

我参与系统方案设计、电路集成、测量和迭代调试。我们联调了射频链路、嵌入式控制和显示，并用信号发生器在不同频率与功率下提供已知输入，检验仪器的读数。

## 信号链

1. **前端放大。** 两级 SPF5189Z 低噪声放大器对微弱输入信号进行放大。
2. **扫频与变频。** STM32 控制 ADF4351 合成扫频本振。AD831 将输入射频与本振混频，随后由 10.7 MHz 晶体滤波器选择所需的中频分量。
3. **检波与采集。** AD8307 将中频信号转换成反映功率的直流电压，STM32 通过 ADC 采样，并用标定关系换算输入功率。
4. **频谱显示。** 将各扫频点的频率与功率对应起来，在 LCD 上绘制频谱，并提供频率标记和峰值指示。

## 关键设计

- 本振输出通过九阶巴特沃斯低通滤波器，以抑制谐波。
- 两级低噪声放大器的实测总电压增益约为 50 倍。PE4302 数字衰减器支持可编程衰减。
- 显示界面可调整中心频率、扫频范围和信号源电平，并提供频率标记和峰值指示。

## 标定与验证

比赛测试使用已知频率和功率的单音信号。验证频段为 **80–100 MHz**，扫频步进为 **100 kHz**，验证输入范围为 **10 µV–10 mV RMS**，约对应 **−87 至 −27 dBm**。

我们用已知输入功率标定 ADC 读数，得到拟合关系：

```text
输入功率（dBm）= 0.04043 × ADC 读数 − 148.78
```

按项目报告的测试样本，超过 70% 的样本功率误差小于 0.5 dB，超过 80% 小于 1 dB。在上述测试条件下，超过 98% 的样本识别出了正确的频点。

## 使用工具

STM32、信号发生器、示波器、PCB 设计及焊接工具。

## 项目演示

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 8px;">
  <iframe title="超外差频谱分析仪演示" loading="lazy" src="https://player.bilibili.com/player.html?bvid=BV1Eju56cEPi&page=1&high_quality=1&danmaku=0" 
          scrolling="no" 
          border="0" 
          frameborder="no" 
          framespacing="0" 
          allowfullscreen="true" 
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

- [Bilibili 项目演示](https://www.bilibili.com/video/BV1Eju56cEPi/)
