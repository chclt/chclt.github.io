+++
title = "Keil uVision 参考工程模板"
description = "使用Keil开发STM32，基于寄存器/固件库的参考工程模板"
summary = ""
toc = true
authors = ['Chclt']
tags = []
categories = []
series = []
date =  "2021-06-14"
lastmod = "2021-06-14"
draft = false
+++

我使用的是正点原子STM32开发板精英版 (STM32F103ZET6)，，在他们提供的配套教程中提供了一种较为复杂的工程目录结构，故简化之，仅供参考。

<!--more-->

## 基于寄存器的参考工程模板

### 目录结构

<table>
<thead>
  <tr>
    <th></th>
    <th>COMMENTS</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><i class="far fa-folder-open"></i> Template</td>
    <td></td>
  </tr>
  <tr>
    <td>└ <i class="far fa-folder-open"></i> Listings</td>
    <td rowspan="2">MDK5.11A 之前的版本不会自动创建这两个文件­夹，所以往往需要手动指定一个输出目录</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-folder-open"></i> Objects</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-alt"></i> template.uvprojx</td>
    <td rowspan="2">Keil 工程文件</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-alt"></i> template.uvoptx</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-folder-open"></i> SYSTEM</td>
    <td>正点原子提供的常用函数库</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> delay.h └ <i class="far fa-file-code"></i> delay.c</td>
    <td>
        延时函数相关函数，寄存器版本的延时函数使用方法：</br>
        <code>
            Stm32_Clock_Init((9);</br>
            delay_init(72);</br>
        </code>
    </td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> sys.h └ <i class="far fa-file-code"></i> sys.c</td>
    <td>IO 口位操作相关函数 (?)</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> usart.h └ <i class="far fa-file-code"></i> usart.c</td>
    <td>串口相关函数</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> startup_stm32f10x_hd.s</td>
    <td>
        启动文件，根据芯片的 Flash 容量选择对应的启动文件:</br>
        <code>
            小容量 ld: FLASH < 32k</br>
            中容量 md: 64K < FLASH < 128K</br>
            大容量 hd: 256K < FLASH</br>
        </code>
        启动文件里是与硬件相关的汇编代码，包括堆栈 (SP) 的初始化、程序计数器 (PC) 的初始化、设置向量表异常事件的入口地址、调用main函数。（正点原子为寄存器版本提供的启动文件经过修改，具体是<mark>屏蔽了复位中断服务函数 <code>Reset_Handler</code> 对函数 <code>SystemInit</code> 的调用，而库函数版本不必要这样做。）
    </td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> main.c</td>
    <td></td>
  </tr>
</tbody>
</table>

### 工程设置

C / C++ - ­Preprocessor Symbols - Define: <code>STM32F10X-HD</code></br>
­C / C++ - Language / Code Generation - Optimization: <code>-O0</code> 值超大,优化越强,但仿真调试效果越差</br>
­C / C++ - Language / Code Generation - One ELF Section per Function <code>✓</code></br>


## 基于固件库的参考工程模板

### 目录结构

<table>
<thead>
  <tr>
    <th></th>
    <th>COMMENT</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td> Template</td>
    <td></td>
  </tr>
  <tr>
    <td>└ <i class="far fa-folder-open"></i> Listings</td>
    <td rowspan="2"></td>
  </tr>
  <tr>
    <td>└ <i class="far fa-folder-open"></i> Objects</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-alt"></i> template.uvprojx</td>
    <td rowspan="2">Keil 工程文件</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-alt"></i> template.uvoptx</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-folder-open"></i> STM32F10x_StdPeriph_Driver</td>
    <td rowspan="3">官方提供的函数库，芯片的每一个外设都有一个 .h 头文件和一个 .c 文件<br><code>STM32F10x_StdPeriph_Lib_V3.5.0\</br>Libraries\STM32F10x_StdPeriph_Driver\</code></td>
  </tr>
  <tr>
    <td>
        &nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-folder-open"></i> inc</br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> ...
    </td>
  </tr>
  <tr>
    <td>
        &nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-folder-open"></i> scr</br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> ...
    </td>
  </tr>
  <tr>
    <td>└ <i class="far fa-folder-open"></i> SYSTEM</td>
    <td rowspan="4">正点原子提供的常用函数库</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> delay.h └ <i class="far fa-file-code"></i> delay.c</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> sys.h └ <i class="far fa-file-code"></i> sys.c</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;&nbsp;└ <i class="far fa-file-code"></i> usart.h └ <i class="far fa-file-code"></i> usart.c</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> core_cm3.h</td>
    <td rowspan="2">CM3内核支持<br><code>STM32F10x_StdPeriph_Lib_V3.5.0\</br>Libraries\CMSIS\CM3\CoreSupport\</code></td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> core_cm3.c</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> startup_stm32f10x_hd.s</td>
    <td>启动文件<br><code>STM32F10x_StdPeriph_Lib_V3.5.0\</br>Libraries\CMSIS\CM3\DeviceSupport\ST\STM32F10x\startup\arm\</code></td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> stm32f10x_it.h</td>
    <td rowspan="3">异常和中断处理、官方函数库配置文件<br><code>STM32F10x_StdPeriph_Lib_V3.5.0\</br>Project\STM32F10x_StdPeriph_Template\</code></td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> stm32f10x_it.c</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> stm32f10x_conf.h</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> system_stm32f10x.h</td>
    <td rowspan="3">外设访问相关<br><code>STM32F10x_StdPeriph_Lib_V3.5.0\</br>Libraries\CMSIS\CM3\</br>DeviceSupport\ST\STM32F10x\</code></td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> system_stm32f10x.c</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> stm32f10x.h</td>
  </tr>
  <tr>
    <td>└ <i class="far fa-file-code"></i> main.c</td>
    <td></td>
  </tr>
</tbody>
</table>

### 工程设置

C / C++ - ­Preprocessor Symbols - Define: <code>STM32F10X-HD, USE_STDPERIPH_DRIVER</code></br>
­C / C++ - Language / Code Generation - Optimization: <code>-O0</code></br>
­C / C++ - Language / Code Generation - One ELF Section per Function <code>✓</code></br>

## 其他

另外需要在工程目录下建立 <code>HARDWARE</code> 文件夹，用来存放外部硬件的初始化代码，如用到了 LED 灯，就在 <code>HARDWARE</code> 文件夹里建立 <code>led.h</code> 和 <code>led.c</code> 两个文件。