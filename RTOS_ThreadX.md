# RTOS ThreadX
[ThreadX 官网](https://azure.microsoft.com/zh-cn/services/rtos/)<br>
[ThreadX 官方文档](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx)<br>
[ThreadX Github 项目链接](https://github.com/azure-rtos)<br>
***
## 概述
Azure RTOS ThreadX是Microsoft的高级工业级实时操作系统（RTOS），专门用于深度嵌入式，实时和IoT应用程序。Azure RTOS ThreadX提供了高级计划，通信，同步，计时器，内存管理和中断管理功能。此外，Azure RTOS ThreadX具有许多高级功能，包括其picokernel™体系结构，抢先阈值™计划，事件链，™执行性能分析，性能指标和系统事件跟踪。结合其卓越的易用性，Azure RTOS ThreadX是最苛刻的嵌入式应用程序的理想选择。截至2017年，Azure RTOS ThreadX已在多种产品中进行了超过62亿次部署，包括消费类设备，医疗电子产品和工业控制设备。<br>
* 最小2KB闪存，1KB RAM占用空间
* 快速的亚微秒上下文切换
* 完全确定性，与线程数无关
* 基于优先级的完全抢占式调度
* 32个默认优先级，可以选择多达1024个级别
* 优先级（FIFO）内的协作调度
* 抢占阈值技术
* 可选的计时器服务，包括：每线程可选的时间片/所有阻塞的可选超时/API需要硬件计时器中断
* 执行性能分析
* 系统级跟踪
* 通过许多标准的安全认证
### 内存占用
Azure RTOS ThreadX需要非常小的2KB指令区和1KB RAM，以实现最小的占用空间。这主要是由于其非分层的picokernel™体系结构和自动缩放。自动缩放意味着在链接时仅将应用程序使用的服务（和支持的基础结构）包括在最终映像中。<br>
以下是一些典型的Azure RTOS ThreadX大小特征：<br>
Azure RTOS ThreadX服务|典型大小(以字节为单位)
:---:|:---:
核心服务(必填)|2,000
队列服务|900
活动标志服务|900
信号量服务|450
互斥服务|1,200
块内存服务|550
字节存储服务|900
### 快速执行
Azure RTOS ThreadX在大多数流行的处理器上实现了亚微秒的上下文切换，并且总体上比其他商用RTOS更快。除了快速之外，Azure RTOS ThreadX还具有高度确定性。无论准备好200个线程还是仅准备一个线程，它都能实现相同的快速性能。<br>
以下是Azure RTOS ThreadX的一些典型性能特征：<br>
* 快速启动：Azure RTOS ThreadX的启动时间少于120个周期。
* 可选删除基本错误检查：可以在编译时跳过基本Azure RTOS ThreadX错误检查。当验证了应用程序代码并且不再需要对每个参数进行错误检查时，这将非常有用。请注意，这可以在编译单元而不是系统范围内完成。
* Picokernel™设计：服务不会彼此分层，从而消除了不必要的函数调用开销。
* \*优化的中断处理：除非需要先占，否则仅在ISR进入/退出时才保存/恢复暂存寄存器。
* 优化的API处理：
  Azure RTOS ThreadX服务|服务时间(以微秒为单位)
  :---:|:---:
  线程挂起|0.6
  线程恢复|0.6
  队列发送|0.3
  队列接收|0.3
  获取信号量|0.2
  放置信号量|0.2
  上下文切换|0.4
  中断响应|0.0-0.6
> 注：性能数据基于在200MHz下运行的典型处理器。
### 支持最受欢迎的架构
* Azure RTOS ThreadX在开箱即用，经过全面测试和完全支持的最受欢迎的32/64位微处理器上运行，包括以下各项：<br>
* ADI公司：SHARC，Blackfin，CM4xx
* 安第斯山脉核心：RISC-V
* Ambiqmicro：Apollo MCU
* ARM：ARM7，ARM9，ARM11，Cortex-M0 / M3 / M4 / M7 / A15 / A5 / A7 / A8 / A9 / A5x 64-bi / A7x 64位/ R4 / R5，TrustZone ARMv8-M
* 踏频：Xtensa，钻石
* CEVA：PSoC，PSoC 4，PSoC 5，PSoC 6，FM0 +，FM3，MF4，WICED WiFi
* 赛普拉斯：RISC-V
* EnSilica：eSi-RISC
* 英飞凌：XMC1000，XMC4000，TriCore
* 英特尔＆英特尔FPGA：x36 /奔腾，XScale，NIOS II，Cyclone，Arria 10
* Microchip：AVR32，ARM7，ARM9，Cortex-M3 / M4 / M7，SAM3 / 4/7/9 / A / C / D / E / G / L / SV，PIC24 / PIC32
* Microsemi：RISC-V
* 恩智浦：LPC，ARM7，ARM9，PowerPC，68K，i.MX，ColdFire，Kinetis Cortex-M3 / M4
* 瑞萨：SH，HS，V850，RX，RZ，Synergy
* Silicon Labs：EFM32
* Synopsys：ARC 600、700，ARC EM，ARC HS
* ST：STM32，ARM7，ARM9，Cortex-M3 / M4 / M7
* Tl：C5xxx，C6xxx，Stellaris，Sitara，Tiva-C
* 波形计算：MIPS32 4K，24K，34K，1004K，MIPS64 5K，microAptiv，interAptiv，proAptiv，M级
* Xilinx：MicroBlaze，PowerPC 405，ZYNQ，ZYNQ UltraSCALE
