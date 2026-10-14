# STM32F407 LED Blink Demo

基于 **STM32F407** 的入门点灯工程，使用 **STM32CubeMX + Keil MDK (HAL库)** 开发，附带 USART1 串口打印功能，适合作为嵌入式开发第一个练手项目。

## 功能

* GPIO 输出控制板载 LED 闪烁
* USART1 串口打印调试信息（重定向 printf）
* 工程结构由 CubeMX 自动生成，便于扩展外设

## 硬件需求

* STM32F407 开发板（正点原子 / 野火 / 自绘板均可）
* USB 转 TTL 串口模块（CH340 / CP2102），用于烧录与串口调试
* 杜邦线若干

## 软件环境

* STM32CubeMX（生成工程初始化代码）
* Keil MDK-ARM（编译下载，需安装对应器件包）
* FlyMcu / STM32CubeProgrammer（串口烧录）
* 串口助手（调试串口输出，波特率 115200，8-N-1）

## 引脚说明

> 以下引脚为默认配置，请按你自己的板子实际接线修改 `Core/Src/main.c` 中的 GPIO 初始化与 `main.h` 宏定义。

|功能|引脚|说明|
|-|-|-|
|LED|由开发板原理图确定|推挽输出，低电平点亮或高电平点亮，按板子修改|
|USART1\_TX|PA9|串口发送，接 CH340 的 RX|
|USART1\_RX|PA10|串口接收，接 CH340 的 TX|
|地|GND|必须与串口模块共地|

## 目录结构

```
LED\_Blink/
├── Core/                  # 用户代码（main.c、usart.c、gpio.c）
│   ├── Inc/               # 头文件
│   └── Src/               # 源文件
├── Drivers/               # STM32 HAL 库驱动
├── MDK-ARM/               # Keil 工程目录
│   ├── RTE/               # MDK 运行环境配置
│   ├── F407\_LED\_DEMO.uvprojx   # Keil 工程文件（用这个打开）
│   └── F407\_LED\_DEMO.uvoptx    # Keil 工程选项配置
├── F407\_LED\_DEMO.ioc      # CubeMX 工程文件（可重新生成代码）
├── .gitignore             # Git 忽略编译产物配置
└── embedded\_c\_notes.md    # 第1周嵌入式C语言学习笔记
```

## 使用方法

### 1\. 打开工程

双击 `MDK-ARM/F407\_LED\_DEMO.uvprojx`，用 Keil MDK 打开。

### 2\. 编译

* 魔术棒（Options for Target）→ Output → 勾选 **Create HEX File**
* 点击 Build（F7）编译，生成 hex 文件

### 3\. 烧录

* 使用 ST-Link：Keil 直接下载（Debug → ST-Link）
* 使用串口：FlyMcu 选择生成的 `.hex` 文件，BOOT0 拉高进 Bootloader，烧录后 BOOT0 拉回低电平复位运行

### 4\. 串口验证

* CH340 接 PA9/PA10/GND，打开串口助手，波特率 **115200**
* 复位开发板，串口应输出调试信息

## 更新日志

* **v1.0**：GPIO 点灯 + USART1 串口打印，上传至 GitHub

