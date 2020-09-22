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
Azure RTOS ThreadX服务|典型大小（以字节为单位）
:---:|:---:
核心服务（必填）|2,000
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
  Azure RTOS ThreadX服务|服务时间（以微秒为单位）
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
***
## ThreadX的安装和使用
### 主机注意事项
嵌入式软件通常在Windows或Linux（Unix）主机上开发。在编译，链接并放置在主机上的应用程序之后，将其下载到目标硬件以执行。<br>
通常，目标下载是从开发工具调试器中完成的。下载后，调试器负责提供目标执行控制（执行，停止，断点等）以及对内存和处理器寄存器的访问。<br>
大多数开发工具调试器通过诸如JTAG（IEEE 1149.1）和后台调试模式（BDM）的片上调试（OCD）连接与目标硬件进行通信。调试器还通过在线仿真（ICE）连接与目标硬件进行通信。OCD和ICE连接都提供了可靠的解决方案，并且对目标驻留软件的入侵最少。<br>
至于主机上使用的资源，ThreadX的源代码以ASCII格式提供，并且在主机计算机的硬盘上大约需要1 MB的空间。<br>
### 目标机注意事项
ThreadX在目标上需要2 KB到20 KB的只读内存（ROM）。ThreadX系统堆栈和其他全局数据结构还需要目标内存的另外1至2 KB。<br>
为了使与计时器相关的功能（如服务调用超时，时间分片和应用程序计时器）正常运行，底层目标硬件必须提供周期性的中断源。如果处理器具有此功能，则ThreadX将利用它。否则，如果目标处理器没有能力生成定期中断，则用户的硬件必须提供该中断。计时器中断的设置和配置通常位于ThreadX发行版的 tx_initialize_low_level汇编文件中。<br>
### 安装ThreadX
通过将GitHub存储库克隆到本地计算机来安装ThreadX。以下是在您的PC上创建ThreadX存储库的克隆的典型语法：<br>
```
git clone https://github.com/azure-rtos/threadx
```
以下是存储库中几个重要文件的列表：<br>
文档名称|描述
:---:|:---:
tx_api.h|C头文件，包含所有系统等式，数据结构和服务原型
tx_port.h|C头文件，包含所有开发工具和特定于目标的数据定义和结构
demo_threadx.c|包含一个小型演示应用程序的C文件
tx.a（或tx.lib）|随标准包一起分发的ThreadX C库的二进制版本
### 使用ThreadX
使用ThreadX很容易。基本上，应用程序代码在编译期间必须包含 tx_api.h并与ThreadX运行时库tx.a（或tx.lib）链接。<br>
构建ThreadX应用程序需要四个步骤：<br>
1. 在使用ThreadX服务或数据结构的所有应用程序文件中包括tx_api.h文件。
2. 创建标准的C main函数。该函数最终必须调用tx_kernel_enter来启动ThreadX。在进入内核之前，可以添加不涉及ThreadX的特定于应用程序的初始化。
  > 注：ThreadX入口函数 tx_kernel_enter不返回。因此，请确保不要在其后放置任何处理或函数调用。
3. 创建tx_application_define函数。这是创建初始系统资源的地方。系统资源的示例包括线程，队列，内存池，事件标志组，互斥锁和信号灯。
4. 编译应用程序源，并与ThreadX运行时库 tx.lib链接。生成的图像可以下载到目标并执行！
