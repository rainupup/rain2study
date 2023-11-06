

# Kiel的使用

## Debug

![1677648637908](STM32卷一.assets/1677648637908.png)

1. 重置程序到最初

2. 跳转到断点处

3. 停止程序

4. 单步运行

5. 跳过函数

6. 跳出函数

7. 跳转到光标处

8. 开启/关闭命令行(软件下面的窗口)

9. 开启/关闭汇编窗口

10. 符号窗口:在这个窗口可以看到变量的变化

    ![image-20230301134159726](STM32卷一.assets/image-20230301134159726.png)

11. 在Debug模式下，使用Peripherals可以查看寄存器

    ![bdd05e7dc7498f004dc8e0061527791](STM32卷一.assets/bdd05e7dc7498f004dc8e0061527791.png)

## 新建项目

**工程架构**

![1677302026302](STM32卷一.assets/1677302026302.png)





**新建项目**

1. 创建文件夹：用来存放以后所有的STM32程序，例如`D:\Code\STM32`

2. 进入软件：`Project->new Project` 在`D:\Code\STM32`目录中再次创建文件夹用于存放本次的项目，进入此文件夹创建工程名称

![18f867acc2c4f71c90830c74bcd26c7](STM32卷一.assets/18f867acc2c4f71c90830c74bcd26c7.png)

3. 选择相应的器件型号

   ![eff93557e7a620282cf8dbf361a109d](STM32卷一.assets/eff93557e7a620282cf8dbf361a109d.png)

4. 现在进入`D:\Code\STM32\Template`文件夹可以看到已经创建了一些文件。但是此时还不能使用keil来编写程序

5. 引入标准库启动文件

   1. 在`D:\Code\STM32\Template`创建文件夹`Start`(名称可以随便定义，方便后期理解)

   2. 引入`\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\CMSIS\CM3\DeviceSupport\ST\STM32F10x\startup\arm`文件夹下的启动文件`startup_stm32f10****`等到`D:\Code\STM32\Template\Start`
      ![1677225069611](STM32卷一.assets/1677225069611.png)

   3. 引入`\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\CMSIS\CM3\DeviceSupport\ST\STM32F10x`文件夹下的`stm32f10x.h`、`system_stm32f10x.c/.h`文件到`D:\Code\STM32\Template\Start`

      1. `stm32f10x.h`:外设寄存器描述
      2. `system_stm32f10x.c/.h`:时钟

   4. 引入`\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\CMSIS\CM3\CoreSupport`文件夹下的内核寄存器描述文件`core_cm3.c/.h`到`D:\Code\STM32\Template\Start`

   5. 进入keil软件，添加新组`Start`![d1fdc032da1d4539380c72606904d4c](STM32卷一.assets/d1fdc032da1d4539380c72606904d4c.png)

      1. 右击Start组->add Existing Files to Group 'Start'

      2. 进入`D:\Code\STM32\Template\Start`目录，选择文件类型为`All file`

         - 引入`startup_stm32f***`开头的启动文件(在下方表格中说明了具体引入什么文件)，本次引入的是`startup_stm32f10x_md.s`，点击`Add`
         - 引入所有`.c .h`文件，就是刚才添加到`D:\Code\STM32\Template\Start`目录的`.c.h`文件
         - 支持`Start`文件夹的文件添加完毕![1e41d6fc393e4bf8873be6213eb6b48](STM32卷一.assets/1e41d6fc393e4bf8873be6213eb6b48.png)

      3. 在工程选项中添加文件夹的头文件路径：依次点击 魔法棒、C/C++、Include Paths旁边三个点按钮、新建、三个点按钮、选择`D:\Code\STM32\Template\Start`文件夹

         ![ede567fbe8e3211ad753d72797b94fb](STM32卷一.assets/ede567fbe8e3211ad753d72797b94fb.png)

6. 在`D:\Code\STM32\Template`创建`User`文件夹

   1. 进入keil软件，添加新组`User`
   2. 右键User组->Add New Item to Group  'User'
   3. 添加C File，文件名为main，注意选择`D:\Code\STM32\Template\User`目录![c2aeb25f3ee17465db26bce1c6a0d7a](STM32卷一.assets/c2aeb25f3ee17465db26bce1c6a0d7a.png)
      1. **一定要选择到对应的文件夹**
   4. 到此处就可以使用寄存器来开发了

7. 库开发

   1. 在`D:\Code\STM32\Template`创建`Library`文件夹

   2. 引入`\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\STM32F10x_StdPeriph_Driver\src`文件夹下的`misc.c` 和`stm32f10x_xxx.c`文件到`D:\Code\STM32\Template\Library`文件夹

      ![1677227734565](STM32卷一.assets/1677227734565.png)

   3. 引入`\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Libraries\STM32F10x_StdPeriph_Driver\inc`文件夹下的`misc.h` 和`stm32f10x_xxx.h`文件到`D:\Code\STM32\Template\Library`文件夹

      ![bd7aa879680c1978b02605ee2e0be0b](STM32卷一.assets/bd7aa879680c1978b02605ee2e0be0b.png)

   4. 进入keil软件，添加新组`Library`组，右击->add Existing Files to Group 'Library',全选`D:\Code\STM32\Template\Library`中的文件，点添加

   5. 将`\固件库\STM32F10x_StdPeriph_Lib_V3.5.0\Project\STM32F10x_StdPeriph_Template`文件夹下的`stm32f10x_conf.h`、`stm32f10x_it.h`引入到main所在的文件夹，也就是`D:\Code\STM32\Template\User`

      ![1677228221024](STM32卷一.assets/1677228221024.png)

      - 再将文件添加到`User`组中

   6. 点击魔法棒、C/C++ 

      1. 将`USE_STDPERIPH_DRIVER`添加到Define栏中
      2. 再将`User`、`Library`利用Include Paths添加到




**启动文件的选择**

| **缩写** | **释义**           | **Flash容量 ** | **型号**          |
| -------- | ------------------ | -------------- | ----------------- |
| LD_VL    | 小容量产品超值系列 | 16~32K         | STM32F100         |
| MD_VL    | 中容量产品超值系列 | 64~128K        | STM32F100         |
| HD_VL    | 大容量产品超值系列 | 256~512K       | STM32F100         |
| LD       | 小容量产品         | 16~32K         | STM32F101/102/103 |
| MD       | 中容量产品         | 64~128K        | STM32F101/102/103 |
| HD       | 大容量产品         | 256~512K       | STM32F101/102/103 |
| XL       | 加大容量产品       | 大于512K       | STM32F101/102/103 |
| CL       | 互联型产品         | -              | STM32F105/107     |





**总结**：

1. 建立工程文件夹，Keil中新建工程，选择型号
2. 工程文件夹里建立Start、Library、User等文件夹，复制固件库里面的文件到工程文件夹
3. 工程里对应建立Start、Library、User等同名称的分组，然后将文件夹内的文件添加到工程分组里
4. 工程选项，C/C++，Include Paths内声明所有包含头文件的文件夹
5. 工程选项，C/C++，Define内定义`USE_STDPERIPH_DRIVER`
6. 工程选项，Debug，下拉列表选择对应调试器，Settings，Flash Download里勾选Reset and Run

# 简介

**认识STM32**

ST 是意法半导体，M 是 Microelectronics 的缩写，32 表示 32 位，即STM32 指的是ST公司开发的基于ARM Cortex-M内核的32位微控制器。

ARM既指ARM公司，也指ARM处理器内核

![01d4276e020723964cf3fc04b93e2cf](STM32卷一.assets/01d4276e020723964cf3fc04b93e2cf.png)

![image-20230224134306270](STM32卷一.assets/image-20230224134306270.png)

**命名规则**

![1677217462967](STM32卷一.assets/1677217462967.png)

**STM32F103C8T6**
CPU：STM32F103RCT6，LQFP64，FLASH:64KB，RAM:20KB
flash起始地址为0x8000000，大小为0x10000(16进制)—>65536字节(10进制)—>**64KB**
RAM起始地址为0x2000000，大小为0x5000(16进制)—>20480字节(10进制)—>**20KB**
![ ](STM32卷一.assets/20210410140645583.png)





**片上资源/外设**

| **英文缩写** |      **名称**      | **英文缩写** |      **名称**      |
| :----------: | :----------------: | :----------: | :----------------: |
|     NVIC     | 嵌套向量中断控制器 |     CAN      |      CAN通信       |
|   SysTick    |   系统滴答定时器   |     USB      |      USB通信       |
|     RCC      |   复位和时钟控制   |     RTC      |      实时时钟      |
|     GPIO     |      通用IO口      |     CRC      |      CRC校验       |
|     AFIO     |      复用IO口      |     PWR      |      电源控制      |
|     EXTI     |      外部中断      |     BKP      |     备份寄存器     |
|     TIM      |       定时器       |     IWDG     |     独立看门狗     |
|     ADC      |     模数转换器     |     WWDG     |     窗口看门狗     |
|     DMA      |    直接内存访问    |     DAC      |     数模转换器     |
|    USART     | 同步/异步串口通信  |     SDIO     |      SD卡接口      |
|     I2C      |      I2C通信       |     FSMC     | 可变静态存储控制器 |
|     SPI      |      SPI通信       |   USB OTG    |    USB主机接口     |

**系统结构**

![1677218047915](STM32卷一.assets/1677218047915.png)

1. ICode总线：该总线将Cortex™-M3内核的指令总线与闪存指令接口相连接。指令预取在此总线上完成。
2. DCode总线：该总线将Cortex™-M3内核的DCode总线与闪存存储器的数据接口相连接(常量加载和调试访问)。
3. 系统总线：此总线连接Cortex™-M3内核的系统总线(外设总线)到总线矩阵，总线矩阵协调着内核和DMA间的访问。
4. DMA总线：此总线将DMA的AHB主控接口与总线矩阵相联，总线矩阵协调着CPU的DCode和DMA到SRAM、闪存和外设的访问。
5. 总线矩阵：总线矩阵协调内核系统总线和DMA主控总线之间的访问仲裁，仲裁利用轮换算法。在互联型产品中，总线矩阵包含5个驱动部件(CPU的DCode、系统总线、以太网DMA、DMA1总线和DMA2总线)和3个从部件(闪存存储器接口(FLITF)、SRAM和AHB2APB桥)。在其它产品中总线矩阵包含4个驱动部件(CPU的DCode、系统总线、DMA1总线和DMA2总线)和4个被动部件(闪存存储器接口(FLITF)、SRAM、FSMC和AHB2APB桥)。AHB外设通过总线矩阵与系统总线相连，允许DMA访问。
6. AHB/APB桥(APB)：两个AHB/APB桥在AHB和2个APB总线间提供同步连接。APB1操作速度限于36MHz，APB2操作于全速(最高72MHz)。有关连接到每个桥的不同外设的地址映射请参考表1。在每一次复位以后，所有除SRAM和FLITF以外的外设都被关闭，在使用一个外设之前，必须设置寄存器RCC_AHBENR来打开该外设的时钟。



**引脚定义**

![image-20230224135446187](STM32卷一.assets/image-20230224135446187.png)

| 引脚号 |    引脚名称     | 类型 | I/O口电平 | 主功能     |              默认复用功能               |           重定义功能           |
| :----: | :-------------: | :--: | :-------: | :--------- | :-------------------------------------: | :----------------------------: |
|   1    |      VBAT       |  S   |           | VBAT       |                                         |                                |
|   2    | PC13-TAMPER-RTC | I/O  |           | PC13       |               TAMPER-RTC                |                                |
|   3    |  PC14-OSC32_IN  | I/O  |           | PC14       |                OSC32_IN                 |                                |
|   4    | PC15-OSC32_OUT  | I/O  |           | PC15       |                OSC32_OUT                |                                |
|   5    |     OSC_IN      |  I   |           | OSC_IN     |                                         |                                |
|   6    |     OSC_OUT     |  O   |           | OSC_OUT    |                                         |                                |
|   7    |      NRST       | I/O  |           | NRST       |                                         |                                |
|   8    |      VSSA       |  S   |           | VSSA       |                                         |                                |
|   9    |      VDDA       |  S   |           | VDDA       |                                         |                                |
|   10   |    PA0-WKUP     | I/O  |           | PA0        | WKUP/USART2_CTS/ADC12_IN0/TIM2_CH1_ETR  |                                |
|   11   |       PA1       | I/O  |           | PA1        |      USART2_RTS/ADC12_IN1/TIM2_CH2      |                                |
|   12   |       PA2       | I/O  |           | PA2        |      USART2_TX/ADC12_IN2/TIM2_CH3       |                                |
|   13   |       PA3       | I/O  |           | PA3        |      USART2_RX/ADC12_IN3/TIM2_CH4       |                                |
|   14   |       PA4       | I/O  |           | PA4        |      SPI1_NSS/USART2_CK/ADC12_IN4       |                                |
|   15   |       PA5       | I/O  |           | PA5        |           SPI1_SCK/ADC12_IN5            |                                |
|   16   |       PA6       | I/O  |           | PA6        |      SPI1_MISO/ADC12_IN6/TIM3_CH1       |           TIM1_BKIN            |
|   17   |       PA7       | I/O  |           | PA7        |      SPI1_MOSI/ADC12_IN7/TIM3_CH2       |           TIM1_CH1N            |
|   18   |       PB0       | I/O  |           | PB0        |           ADC12_IN8/TIM3_CH3            |           TIM1_CH2N            |
|   19   |       PB1       | I/O  |           | PB1        |           ADC12_IN9/TIM3_CH4            |           TIM1_CH3N            |
|   20   |       PB2       | I/O  |    FT     | PB2/BOOT1  |                                         |                                |
|   21   |      PB10       | I/O  |    FT     | PB10       |           I2C2_SCL/USART3_TX            |            TIM2_CH3            |
|   22   |      PB11       | I/O  |    FT     | PB11       |           I2C2_SDA/USART3_RX            |            TIM2_CH4            |
|   23   |      VSS_1      |  S   |           | VSS_1      |                                         |                                |
|   24   |      VDD_1      |  S   |           | VDD_1      |                                         |                                |
|   25   |      PB12       | I/O  |    FT     | PB12       | SPI2_NSS/I2C2_SMBAI/USART3_CK/TIM1_BKIN |                                |
|   26   |      PB13       | I/O  |    FT     | PB13       |      SPI2_SCK/USART3_CTS/TIM1_CH1N      |                                |
|   27   |      PB14       | I/O  |    FT     | PB14       |     SPI2_MISO/USART3_RTS/TIM1_CH2N      |                                |
|   28   |      PB15       | I/O  |    FT     | PB15       |           SPI2_MOSI/TIM1_CH3N           |                                |
|   29   |       PA8       | I/O  |    FT     | PA8        |         USART1_CK/TIM1_CH1/MCO          |                                |
|   30   |       PA9       | I/O  |    FT     | PA9        |           USART1_TX/TIM1_CH2            |                                |
|   31   |      PA10       | I/O  |    FT     | PA10       |           USART1_RX/TIM1_CH3            |                                |
|   32   |      PA11       | I/O  |    FT     | PA11       |    USART1_CTS/USBDM/CAN_RX/TIM1_CH4     |                                |
|   33   |      PA12       | I/O  |    FT     | PA12       |    USART1_RTS/USBDP/CAN_TX/TIM1_ETR     |                                |
|   34   |      PA13       | I/O  |    FT     | JTMS/SWDIO |                                         |              PA13              |
|   35   |      VSS_2      |  S   |           | VSS_2      |                                         |                                |
|   36   |      VDD_2      |  S   |           | VDD_2      |                                         |                                |
|   37   |      PA14       | I/O  |    FT     | JTCK/SWCLK |                                         |              PA14              |
|   38   |      PA15       | I/O  |    FT     | JTDI       |                                         |   TIM2_CH1_ETR/PA15/SPI1_NSS   |
|   39   |       PB3       | I/O  |    FT     | JTDO       |                                         | PB3/TRACESWO/TIM2_CH2/SPI1_SCK |
|   40   |       PB4       | I/O  |    FT     | NJTRST     |                                         |     PB4/TIM3_CH1/SPI1_MISO     |
|   41   |       PB5       | I/O  |           | PB5        |               I2C1_SMBAI                |       TIM3_CH2/SPI1_MOSI       |
|   42   |       PB6       | I/O  |    FT     | PB6        |            I2C1_SCL/TIM4_CH1            |           USART1_TX            |
|   43   |       PB7       | I/O  |    FT     | PB7        |            I2C1_SDA/TIM4_CH2            |           USART1_RX            |
|   44   |      BOOT0      |  I   |           | BOOT0      |                                         |                                |
|   45   |       PB8       | I/O  |    FT     | PB8        |                TIM4_CH3                 |        I2C1_SCL/CAN_RX         |
|   46   |       PB9       | I/O  |    FT     | PB9        |                TIM4_CH4                 |        I2C1_SDA/CAN_TX         |
|   47   |      VSS_3      |  S   |           | VSS_3      |                                         |                                |
|   48   |      VDD_3      |  S   |           | VDD_3      |                                         |                                |





其中红色为电源引脚，蓝色为最小系统引脚，绿色为IO口、功能口等

I/O口电平：FT表明为5V的电压，没有FT则表明只能容忍3.3V电压。没有FT要想接5V电平则需要加装电平转换电路

STM32F103C8T6有两组GPIO,分别为GPIOA,GPIOB



**启动配置**

在STM32F10xxx里，可以通过BOOT[1:0]引脚选择三种不同启动模式。

![1677218569816](STM32卷一.assets/1677218569816.png)

在系统复位后，SYSCLK的第4个上升沿，BOOT引脚的值将被锁存。用户可以通过设置BOOT1和BOOT0引脚的状态，来选择在复位后的启动模式。



**最小系统**

最小系统是指，为了确保单片机正常工作的最基本电路

![image-20230224140650740](STM32卷一.assets/image-20230224140650740.png)

**STM32F103C8T6**

- 系列：主流系列STM32F1
- 内核：ARM Cortex-M3
- 主频：72MHz
- RAM：20K（SRAM）
- ROM：64K（Flash）
- 供电：2.0~3.6V（标准3.3V）
- 封装：LQFP48

![image-20230224134648410](STM32卷一.assets/image-20230224134648410.png)



![STM32F103C8T6最小系统板](STM32卷一.assets/TB2opyqoFXXXXXVXXXXXXXXXXXX_!!2876359570.jpg)







1. 





# 时钟RCC

RCC： Reset and Clock Control，即复位和时钟控制



**过程**

![image-20230718152440931](STM32卷一.assets/image-20230718152440931.png)

**时钟系统框图**

![image-20230718154003785](STM32卷一.assets/image-20230718154003785.png)

深蓝色为时钟源输入：有四个时钟源

* 内部时钟源:两个
  * HSI是高速内部时钟，RC振荡器，频率为8MHz，精度不高。(最多能产生64MHz的脉冲)
  * LSI是低速内部时钟，RC振荡器，频率为40kHz，提供低功耗时钟。独立看门狗的时钟源只能是 LSI ，同时LSI 还可以作为 RTC 的时钟源。
* 外部时钟源:两个
  * HSE是高速外部时钟，可接石英/陶瓷谐振器，或者接外部时钟源，频率范围为4MHz~16MHz。多数是: 8MHZ
  * LSE是低速外部时钟，频率范围为0-1000KHZ，接频率为32.768kHz的石英晶体。是主要的**实时时钟RTC**时钟源。

黄色为外部接口: 

* 外部接口是芯片内部与外界连接的通道(单片机引脚)，这类接口能够输入时钟信号到单片机或从单片机输出。
* 注意：高速外部时钟HSE的引脚是OSC_OUT和OSC_IN这两个引脚芯片是独立引出的，可以接外部的晶振电路，而低速外部时钟LSE的引脚OSC32_IN和OSC32_OUT两个引脚不是独立的，而是在PC14和PC15上，对应关系为OSC32_IN-->PC14 ; OSC32_OUT-->PC15

棕色为预分频器: 预分频器(Prescaler-PSC)用来将输入的时钟源进行分频输出。例如72Mhz的时钟信号经过1.5分频(/1.5)，得到48Mhz时钟信号。

绿色为选择器: 可对输入的多个时钟信号进行选择，选择其中的一个时钟信号输出

红色位倍频器: 锁相倍频器（phase locked frequency multiplier） 是完成倍频功能的锁相环。用来将输入的时钟源进行倍频输出。例如8Mhz时钟源进行9倍频，得到72Mhz时钟信号。

浅蓝色为与门：为降低能耗，默认一端低电平，即关闭状态(disable)，当需要使用相关外设时钟时，通过程序控制该端高电平使时钟信号导通。



最高频率: 72MHZ



**时钟去向讲解**

![image-20230718151749735](STM32卷一.assets/image-20230718151749735.png)

APB1 分频器输出一路供 APB1 外设使用 (PCLK1 最大频率 36MHz)，另一路送给定时器 Timer倍频器使用。
APB2 分频器输出一路供 APB2 外设使用 (PCLK2 最大频率 72MHz)，另一路送给定时器 Timer倍频器使用 或ADC预分频器使用。



**以定时器和ADC为例**



![image-20230718152320965](STM32卷一.assets/image-20230718152320965.png)

## **系统时钟配置**

**步骤：**

1. 配置HSE_VALUE：告诉HAL库外部晶振频率，stm32xxxx_hal_conf.h
2. 调用SystemInit()函数（可选）：在启动文件中调用， 在system_stm32xxxx.c定义
   1. 不想调用：可以在startup_stm32f103xe.s中的Reset_Handler注释掉
3. 选择时钟源，配置PLL：通过`HAL_RCC_OscConfig()`函数设置
4. 选择系统时钟源，配置总线分频器：通过`HAL_RCC_ClockConfig()`函数设置
5. 配置扩展外设时钟（可选）：通过`HAL_RCCEx_PeriphCLKConfig()`函数设置



**时钟源，配置PLL**

````c
HAL_StatusTypeDef HAL_RCC_OscConfig(RCC_OscInitTypeDef  *RCC_OscInitStruct)   //选择时钟源，配置PLL
````

````c
typedef struct { 
	uint32_t  OscillatorType; 		/* 选择需要配置的振荡器 */ 
	uint32_t  HSEState; 			/* HSE 状态 */ 
	uint32_t  HSEPredivValue; 		/* HSE 预分频值 */ 
	uint32_t  LSEState; 			/* LSE 状态 */ 
	uint32_t  HSIState; 			/* HSI状态 */ 
	uint32_t  HSICalibrationValue; 	/* HSI 校准值 */ 
	uint32_t  LSIState; 			/* LSI 状态 */ 
	RCC_PLLInitTypeDef  PLL; 		/* PLL 结构体 */ 
}RCC_OscInitTypeDef;
/* PLL 结构体 */ 
typedef struct { 
	uint32_t  PLLState; 	/* PLL 状态 */ 
	uint32_t  PLLSource; 	/* PLL 时钟源 */ 
	uint32_t  PLLMUL; 		/* PLL 倍频系数 */ 
}RCC_PLLInitTypeDef;
````

**系统时钟源，配置总线分频器**

````c
/** 选择系统时钟源，配置总线分频器
*	参数2FLatency:闪存访问控制寄存器(FLASH_ACR) 
*	LATENCY：时延
*	这些位表示SYSCLK(系统时钟)周期与闪存访问时间的比例
*	000：零等待状态，当 0 < SYSCLK ≤ 24MHz               FLASH_LATENCY_0 
*	001：一个等待状态，当 24MHz < SYSCLK ≤ 48MHz         FLASH_LATENCY_1 
*	010：两个等待状态，当 48MHz < SYSCLK ≤ 72MHz         FLASH_LATENCY_2
**/
HAL_StatusTypeDef HAL_RCC_ClockConfig(RCC_ClkInitTypeDef  *RCC_ClkInitStruct, uint32_t FLatency) 
````

````c
typedef struct { 
	uint32_t  ClockType; 		/* 要配置的时钟（SYSCLK/HCLK/PCLK1/PCLK2） (HCLK:AHB，PCLK1:APB1，PCLK2:APB2)*/ 
	uint32_t  SYSCLKSource; 	/* 系统时钟源 */ 
	uint32_t  AHBCLKDivider; 	/* AHB  时钟预分频系数 */ 
	uint32_t  APB1CLKDivider; 	/* APB1 时钟预分频系数 */ 
	uint32_t  APB2CLKDivider; 	/* APB2 时钟预分频系数 */ 
}RCC_ClkInitTypeDef;
````

**例：**

使用外部8MHz晶振

````c
#if !defined  (HSE_VALUE)
#if defined(USE_STM3210C_EVAL)
#define HSE_VALUE    25000000U /*!< Value of the External oscillator in Hz */
#else
#define HSE_VALUE    8000000U /*!< Value of the External oscillator in Hz */
#endif
#endif /* HSE_VALUE */
````

````c
RCC_OscInitTypeDef rcc_osc_init = {0};
rcc_osc_init.OscillatorType = RCC_OSCILLATORTYPE_HSE;       /* 选择要配置HSE */
rcc_osc_init.HSEState = RCC_HSE_ON;                         /* 打开HSE */
rcc_osc_init.HSEPredivValue = RCC_HSE_PREDIV_DIV1;          /* HSE预分频系数 */
rcc_osc_init.PLL.PLLState = RCC_PLL_ON;                     /* 打开PLL */
rcc_osc_init.PLL.PLLSource = RCC_PLLSOURCE_HSE;             /* PLL时钟源选择HSE */
rcc_osc_init.PLL.PLLMUL = RCC_PLL_MUL9;                     /* PLL倍频系数 */
ret = HAL_RCC_OscConfig(&rcc_osc_init);                     /* 初始化 */

RCC_ClkInitTypeDef rcc_clk_init = {0};
/* 选中PLL作为系统时钟源并且配置HCLK,PCLK1和PCLK2*/
rcc_clk_init.ClockType = (RCC_CLOCKTYPE_SYSCLK | RCC_CLOCKTYPE_HCLK | RCC_CLOCKTYPE_PCLK1 | RCC_CLOCKTYPE_PCLK2);
rcc_clk_init.SYSCLKSource = RCC_SYSCLKSOURCE_PLLCLK;        /* 设置系统时钟来自PLL,注意： 别选成RCC_OSCILLATORTYPE_HSE*/
rcc_clk_init.AHBCLKDivider = RCC_SYSCLK_DIV1;               /* AHB分频系数为1 */
rcc_clk_init.APB1CLKDivider = RCC_HCLK_DIV2;                /* APB1分频系数为2 */
rcc_clk_init.APB2CLKDivider = RCC_HCLK_DIV1;                /* APB2分频系数为1 */
ret = HAL_RCC_ClockConfig(&rcc_clk_init, FLASH_LATENCY_2);  /* 同时设置FLASH延时周期为2WS，也就是3个CPU周期。 */
````



**外设时钟使和失能**

使能某外设时钟：`__HAL_RCC_XXX_CLK_ENABLE();  `

禁止某外设时钟：`__HAL_RCC_XXX_CLK_DISABLE();  `

```c
__HAL_RCC_GPIOA_CLK_ENABLE();      		/* 使能 GPIOA 时钟 */
__HAL_RCC_GPIOA_CLK_DISABLE();      	/* 禁止 GPIOA 时钟 */
```






#   GPIO

## 简介

**GPIO**(general porpose intput output):通用输入输出端口的简称。可以通过软件控制其输出和输入。stm32芯片的GPIO引脚与外部设备连接起来，从而实现与外部通信，控制以及数据采集的功能。



GPIO管脚： PA、PB、PC、PD 等均属于 GPIO 引脚。GPIO 占用了 STM32 芯片大部分的引脚。并且每一个端口都有 16 个引脚，比如 PA 端口，它有 PA0-PA15。其他的 PB、PC 等端口是一样的。



**GPIO基本结构**

![1677302313792](STM32卷一.assets/1677302313792.png)



**GPIO位结构**



![image-20230718121155201](STM32卷一.assets/image-20230718121155201.png)



绿色区域为输入，蓝色区域为输出

1. 保护二极管
   - 引脚内部加上这两个保护二级管可以防止引脚外部过高或过低的电压输入。
   - 当引脚电压高于 VDD_FT 或 VDD 时，上方的二极管导通吸收这个高电压。
   - 当引脚电压低于 VSS 时，下方的二极管导通，防止不正常电压引入芯片导致芯片烧毁。
2. 上下拉电阻
   - 上拉和下拉电阻上都有一个开关，通过配置上下拉电阻开关，可以控制引脚的默认状态电平。
   - 当开启上拉时引脚默认电压为高电平
   - 开启下拉时，引脚默认电压为低电平，这样就可以消除引脚不定状态的影响。
   - 将上拉和下拉的开关都关断，这种状态我们称为浮空模式，一旦配置成这个模式，引脚的电压是不确定的，如果用万用表测量此模式下管脚电压时会发现只有 1 点几伏，而且还不时改变，所以一般情况下我们都会给引脚设置成上拉或者下拉模式，使它有一个默认状态。
   - STM32 上下拉及浮空模式的配置是通过GPIOx_CRL 和 GPIOx_CRH 寄存器控制的。 
   - STM32 内部的上拉其实是一个弱上拉，也就是说通过此上拉电阻输出的电流很小，如果想要输出一个大电流，那么就需要外接上拉电阻了。
3. TTL肖特基触发器(施密特触发器)
   - 施密特触发电路是一种波形整形电路，当任何波形的信号进入电路时，输出在正、负饱和之间跳动，产生方波或脉波输出。不同于比较器，施密特触发电路有两个临界电压且形成一个滞后区，可以防止在滞后范围内之噪声干扰电路的正常工作。如遥控接收线路，传感器输入电路都会用到它整形。
4. 输入数据寄存器
   - 输入数据寄存器是由 IO 口经过上下拉电阻、施密特触发器引入。当信号经过触发器，模拟信号将变为数字信号 0 或 1，然后存储在输入数据寄存器中，通过读取输入数据寄存器 GPIOx_IDR 就可以知道 IO 口的电平状态。
5. 复用功能输入
   - 此模式与复用功能输出类似。在复用功能输入模式时，GPIO 引脚的信号传输到 STM32 其他片上外设，由该外设读取引脚的状态。同样，如我们使用 USART 串口通讯时，需要用到某个 GPIO 引脚作为通讯接收引脚，这个时候就可以把该 GPIO 引脚配置成 USART 串口复用功能，使 USART 可以通过该通讯引脚的接收远端数据。
6. 模拟输入输出
   - 当 GPIO 引脚用于 ADC 采集电压的输入通道时，用作“模拟输入”功能，此时信号是不经过施密特触发器的，因为经过施密特触发器后信号只有 0、1 两种状态，ADC 外设要采集到原始的模拟信号，信号源输入必须在施密特触发器之前。类似地，当 GPIO 引脚用于 DAC 作为模拟电压输出通道时，此时作为“模拟输出”功能， DAC 的模拟信号输出就不经过双 MOS 管结构了，模拟信号直接通过管脚输出。
7. P-MOS 和 SN-MOS 
   - GPIO 引脚经过两个保护二极管后就分成两路，上面一路是“输入模式”，下面一路是“输出模式”。
   - 输出模式，线路经过一个由 P-MOS 和 N-MOS管组成的单元电路，这让 GPIO 引脚具有了推挽和开漏两种输出模式。
   - 推挽输出模式，是根据 P-MOS 和 N-MOS 管的工作方式命名的。
     - 在该结构单元输入一个高电平时，P-MOS 管导通，N-MOS 管截止，对外输出高电平（3.3V）。
     - 在该单元输入一个低电平时，P-MOS 管截止，N-MOS 管导通，对外输出低电平（0V）。
     - 如果当切换输入高低电平时，两个 MOS 管将轮流导通，一个负责灌电流（电流输出到负载），一个负责拉电流（负载电流流向芯片），使其负载能力和开关速度都比普通的方式有很大的提高。
   - 在开漏输出模式时，不论输入是高电平还是低电平，P-MOS 管总处于关闭状态。
     - 当给这个单元电路输入低电平时，N-MOS 管导通，输出即为低电平。
     - 当输入高电平时，N-MOS 管截止，这个时候引脚状态既不是高电平，又不是低电平，我们称之为高阻态。
     - 如果想让引脚输出高电平，那么引脚必须外接一个上拉电阻，由上拉电阻提供高电平。
   - 在开漏输出模式中还有一个特点，引脚具有“线与”关系。即多个开漏输出模式的引脚接在一起，只要有一个引脚为低电平，其他所有管脚都为低电平，即把所有引脚连接在一起的这条总线拉低了。
     - 只有当所有引脚输出高阻态时这条总线的电平才由上拉电阻的 VDD 决定。如果 VDD 连接的是 3.3V，那么引脚输出的就是 3.3V，如果 VDD 连接的是 5V，那么引脚输出的就是 5V。因此如果想要让 STM32 管脚输出 5V，可以选择开漏输出模式，然后在外接上拉电阻的电源 VDD 选择 5V 即可，前提是这个 STM32 引脚是容忍 5V 的。开漏输出模式一般应用在 I2C、SMBUS 通讯等需要“线与”功能的总线电路中。还可以用在电平不匹配的场合中，就如上面说的输出 5V 一样。
     - 推挽输出模式一般应用在输出电平为 0-3.3V 而且需要高速切换开关状态的场合。除了必须要用开漏输出模式的场合，我们一般选择推挽输出模式。要配置引脚是开漏输出还是推挽输出模式可以使用GPIOx_CRL 和 GPIOx_CRH 寄存器。
8. 输出数据寄存器
   - 双 MOS 管结构电路的输入信号，是由 GPIO“输出数据寄存器GPIOx_ODR”提供的，因此我们通过修改输出数据寄存器的值就可以修改 GPIO 引脚的输出电平。而“置位/复位寄存器 GPIOx_BSRR”可以通过修改输出数据寄存器的值从而影响电路的输出。
9. 复用功能输出
   - 由于 STM32 的 GPIO 引脚具有第二功能，因此当使用复用功能的时候，也就是通过其他外设复用功能输出信号与 GPIO 数据寄存器一起连接到双 MOS 管电路的输入，其中梯形结构是用来选择使用复用功能还是普通 IO 口功能。例如我们使用 USART 串口通讯时，需要用到某个 GPIO 引脚作为通讯发送引脚，这个时候就可以把该 GPIO 引脚配置成 USART 串口复用功能，由串口外设控制该引脚，发送数据。

## **GPIO模式**

| **模式名称** | **性质** | **特征**                                                     | **编码**              |
| :----------: | :------: | :----------------------------------------------------------- | --------------------- |
|   浮空输入   | 数字输入 | 可读取引脚电平，若引脚悬空，则电平不确定                     | GPIO_Mode_IN_FLOATING |
|   上拉输入   | 数字输入 | 可读取引脚电平，内部连接上拉电阻，悬空时默认高电平           | GPIO_Mode_IPU         |
|   下拉输入   | 数字输入 | 可读取引脚电平，内部连接下拉电阻，悬空时默认低电平           | GPIO_Mode_IPD         |
|   模拟输入   | 模拟输入 | GPIO无效，引脚直接接入内部ADC                                | GPIO_Mode_AIN         |
|   开漏输出   | 数字输出 | 可输出引脚电平，高电平为高阻态，低电平接VSS  （高电平没有驱动能力） | GPIO_Mode_Out_OD      |
|   推挽输出   | 数字输出 | 可输出引脚电平，高电平接VDD，低电平接VSS      （高电平有驱动能力,25mA） | GPIO_Mode_Out_PP      |
| 复用开漏输出 | 数字输出 | 由片上外设控制，高电平为高阻态，低电平接VSS(硬件IIC)         | GPIO_Mode_AF_PP       |
| 复用推挽输出 | 数字输出 | 由片上外设控制，高电平接VDD，低电平接VSS（SPI）              | GPIO_Mode_AF_OD       |

输入：Input

输出：Output

上拉：Pull-up

下拉：Pull-down

推挽：Push-Pull

开漏：Open-Drain

复用：Alternate-Function

### 输入

![image-20230718121542076](STM32卷一.assets/image-20230718121542076.png)

在输入模式时，施密特触发器打开，输出被禁止，可通过输入数据寄存器 GPIOx_IDR读取 I/O 状态

由于电阻阻值很大这里的上拉下拉输入都是弱上拉 弱下拉，为了对外部输入产生很大的影响



**浮空/上拉/下拉输入**

上拉输入：默认的高电平，当没有外部输入时默认输入高电平

下拉输入：默认的低电平，当没有外部输入时默认输入低电平

浮空输入：输入引脚啥都不接，此时输入电平极易受外界的干扰导致输入电平不确定，完全由外部的输入决定。



**模拟输入**

![1689654341062](STM32卷一.assets/1689654341062.png)



这模式主要为片上外设ADC而配置，从外部读取模拟信号

- 模拟信号：测试信号未经过采样前，均是时间和幅值均是连续的信号称为模拟信号，例如连续变化的电压，电流，温度等等。
- 数字信号：模拟信号经等间隔“采样”及幅值量化以后，时间和幅值均是不连续的（离散）的信号,例如0 /1

他的目的就是获取模拟量，没有经过施密特触发器

### 输出

* 输出寄存器只会记录0和1，再通过驱动器来输出3.3V电平
* 出现在I/O脚上的数据在每个APB2时钟被采样到输入数据寄存器
* 在开漏模式时，对输入数据寄存器的读访问可得到I/O状态
* 在推挽式模式时，对输出数据寄存器的读访问得到最后一次写的值
* 除了模拟输入的这种模式会关闭数字输入功能其他七种模式，都可以通过输入寄存器读取I/O状态，例：在模拟I2C实验中把GPIO的工作模式配置为开漏输出时同时也可以读取引脚电平状态，现在不知道不要紧后面会详细讲解
* 在输出模式中，推挽模式时双 MOS 管以轮流方式工作，输出数据寄存器 GPIOx_ODR可控制 I/O 输出高低电平。开漏模式时，只有 N-MOS 管工作，输出数据寄存器可控制 I/O输出高阻态或低电平。

**推挽输出**

![image-20230718123753925](STM32卷一.assets/image-20230718123753925.png)



当输出寄存器输出高电平，则引脚也输出高电平

![image-20230718124406534](STM32卷一.assets/image-20230718124406534.png)

当输出寄存器输出低电平，则引脚也输出低电平

![image-20230718124458462](STM32卷一.assets/image-20230718124458462.png)



**开漏输出**

当输出寄存器输出高电平，则引脚输出高阻态；IIC就是利用引脚高阻态特性。

![image-20230718125400407](STM32卷一.assets/image-20230718125400407.png)



当输出寄存器输出低电平，则引脚输出低电平

![image-20230718125345988](STM32卷一.assets/image-20230718125345988.png)



**复用推挽开漏输出**

复用功能模式中，输出使能，输出速度可配置，可工作在开漏及推挽模式， 但是输出信号源于其它外设
输出数据寄存器 GPIOx_ODR 无效；输入可用，通过输入数据寄存器可获取 I/O 实际状态，但一般直接用外设的寄存器来获取该数据信号

![image-20230718130026938](STM32卷一.assets/image-20230718130026938.png)

复用输出与其他输出一样，只是控制源来自其他外设，不来自输出数据寄存器





## GPIO寄存器

| **CRL\CRH**            | **IDR**  | **ODR**  | **BSRR**          | **BRR**                                            | **LCKR**           |
| ---------------------- | -------- | -------- | ----------------- | -------------------------------------------------- | ------------------ |
| 配置工作模式，输出速度 | 输入数据 | 输出数据 | 设置ODR寄存器的值 | F4之后没有这个寄存器，考虑代码兼容性的话不建议使用 | 配置锁定，用得不多 |

## HAL库

### 初始化GPIO

**GPIO初始化结构体**

````C
typedef struct { 
  uint32_t Pin;    /* 引脚号 */ 
  uint32_t Mode;   /* 模式设置 */ 
  uint32_t Pull;   /* 上拉下拉设置 */ 
  uint32_t Speed;  /* 速度设置 */ 
} GPIO_InitTypeDef;
````

````C
//Mode参数：模式设置
#define GPIO_MODE_INPUT             (0x00000000U) /* 输入模式 */
#define GPIO_MODE_OUTPUT_PP         (0x00000001U) /* 推挽输出 */
#define GPIO_MODE_OUTPUT_OD         (0x00000011U) /* 开漏输出 */
#define GPIO_MODE_AF_PP             (0x00000002U) /* 推挽式复用 */
#define GPIO_MODE_AF_OD             (0x00000012U) /* 开漏式复用 */
#define GPIO_MODE_AF_INPUT          GPIO_MODE_INPUT
#define GPIO_MODE_ANALOG            (0x00000003U) /* 模拟模式 */

#define GPIO_MODE_IT_RISING         (0x10110000u) /* 外部中断，上升沿触发检测 */
#define GPIO_MODE_IT_FALLING        (0x10210000u) /* 外部中断，下降沿触发检测 */
/* 外部中断，上升和下降双沿触发检测 */
#define GPIO_MODE_IT_RISING_FALLING (0x10310000u) 
#define GPIO_MODE_EVT_RISING        (0x10120000U) /*外部事件，上升沿触发检测 */
#define GPIO_MODE_EVT_FALLING       (0x10220000U) /*外部事件，下降沿触发检测 */
/* 外部事件，上升和下降双沿触发检测 */
#define GPIO_MODE_EVT_RISING_FALLING (0x10320000U)

//成员 Pull 用于配置输入模式时的上下拉电阻，有以下选择项：
#define GPIO_NOPULL                 (0x00000000U) /* 无上下拉 */
#define GPIO_PULLUP                 (0x00000001U) /* 上拉 */
#define GPIO_PULLDOWN               (0x00000002U) /* 下拉 */
//成员 Speed 用于配置 GPIO 的速度，有以下选择项：
#define GPIO_SPEED_FREQ_LOW         (0x00000002U) /* 低速 */
#define GPIO_SPEED_FREQ_MEDIUM      (0x00000001U) /* 中速 */
#define GPIO_SPEED_FREQ_HIGH        (0x00000003U) /* 高速 */
````

**开启时钟宏**

````c
__HAL_RCC_XXX_CLK_ENABLE();  //使能某外设时钟
__HAL_RCC_XXX_CLK_DISABLE(); //禁止某外设时钟
````

**初始化函数**

````c
void HAL_GPIO_Init(GPIO_TypeDef  *GPIOx, GPIO_InitTypeDef *GPIO_Init)
````

### 常用函数

````c
/**
*	形参 3 是要设置输出的状态，是枚举型有两个选择：GPIO_PIN_SET 表示高电平，GPIO_PIN_RESET 表示低电平。
**/
void HAL_GPIO_WritePin(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin,GPIO_PinState PinState);  // 写
void HAL_GPIO_TogglePin(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin);           // 反转
GPIO_PinState HAL_GPIO_ReadPin(GPIO_TypeDef *GPIOx, uint16_t GPIO_Pin)     // 读
````



## 标准库

### 初始化GPIO

**GPIO初始化结构体**

````c
GPIO_InitTypeDef GPIO_InitStructure;   //此代码最好放在程序的开头，否则有些编译器报错 C99规范不会报错
````

此结构体的定义是在`stm32f10x_gpio.h`文件中，其中包括3个成员。

````c
typedef struct{
  uint16_t GPIO_Pin;             /*!< Specifies the GPIO pins to be configured.
                                      This parameter can be any value of @ref GPIO_pins_define */
  GPIOSpeed_TypeDef GPIO_Speed;  /*!< Specifies the speed for the selected pins.
                                      This parameter can be a value of @ref GPIOSpeed_TypeDef */
  GPIOMode_TypeDef GPIO_Mode;    /*!< Specifies the operating mode for the selected pins.
                                      This parameter can be a value of @ref GPIOMode_TypeDef */
}GPIO_InitTypeDef;
````

1. `uint16_t GPIO_Pin;`:来指定GPIO的哪个或哪些引脚，取值参见`stm32f10x_gpio.h`头文件的宏定义。使用Ctrl+F查找`GPIO_pins_define`

   ````c
   #define GPIO_Pin_0                 ((uint16_t)0x0001)  /*!< Pin 0 selected */
   #define GPIO_Pin_1                 ((uint16_t)0x0002)  /*!< Pin 1 selected */
   #define GPIO_Pin_2                 ((uint16_t)0x0004)  /*!< Pin 2 selected */
   #define GPIO_Pin_3                 ((uint16_t)0x0008)  /*!< Pin 3 selected */
   #define GPIO_Pin_4                 ((uint16_t)0x0010)  /*!< Pin 4 selected */
   #define GPIO_Pin_5                 ((uint16_t)0x0020)  /*!< Pin 5 selected */
   #define GPIO_Pin_6                 ((uint16_t)0x0040)  /*!< Pin 6 selected */
   #define GPIO_Pin_7                 ((uint16_t)0x0080)  /*!< Pin 7 selected */
   #define GPIO_Pin_8                 ((uint16_t)0x0100)  /*!< Pin 8 selected */
   #define GPIO_Pin_9                 ((uint16_t)0x0200)  /*!< Pin 9 selected */
   #define GPIO_Pin_10                ((uint16_t)0x0400)  /*!< Pin 10 selected */
   #define GPIO_Pin_11                ((uint16_t)0x0800)  /*!< Pin 11 selected */
   #define GPIO_Pin_12                ((uint16_t)0x1000)  /*!< Pin 12 selected */
   #define GPIO_Pin_13                ((uint16_t)0x2000)  /*!< Pin 13 selected */
   #define GPIO_Pin_14                ((uint16_t)0x4000)  /*!< Pin 14 selected */
   #define GPIO_Pin_15                ((uint16_t)0x8000)  /*!< Pin 15 selected */
   #define GPIO_Pin_All               ((uint16_t)0xFFFF)  /*!< All pins selected */
   
   //将16进制转为2进制，可以发现GPIO_Pin_1 就是 GPIO_Pin_0 左移一位的结果
   ````

2. `GPIOSpeed_TypeDef GPIO_Speed;`:GPIO的速度配置，此项的取值参见`stm32f10x_gpio.h`头文件`GPIOSpeed_TypeDef`枚举的定义，其中对应3个速度：10MHz、2MHz、50MHz；

   ````c
   typedef enum
   { 
     GPIO_Speed_10MHz = 1,
     GPIO_Speed_2MHz, 
     GPIO_Speed_50MHz
   }GPIOSpeed_TypeDef;
   ````

3. `GPIOMode_TypeDef GPIO_Mode;`:为GPIO的工作模式配置，其取值参见`stm32f10x_gpio`头文件`GPIOMode_TypeDef`枚举的定义，即GPIO的8种工作模式。

   ````c
   typedef enum
   { GPIO_Mode_AIN = 0x0,
     GPIO_Mode_IN_FLOATING = 0x04,
     GPIO_Mode_IPD = 0x28,
     GPIO_Mode_IPU = 0x48,
     GPIO_Mode_Out_OD = 0x14,
     GPIO_Mode_Out_PP = 0x10,
     GPIO_Mode_AF_OD = 0x1C,
     GPIO_Mode_AF_PP = 0x18
   }GPIOMode_TypeDef;
   ````

````c
GPIO_InitTypeDef GPIO_InitStruct;                 //定义结构体
GPIO_InitStruct.GPIO_Pin = GPIO_Pin_0;			  //使用引脚0
GPIO_InitStruct.GPIO_Mode = GPIO_Mode_Out_PP;     //使用推挽输出
GPIO_InitStruct.GPIO_Speed = GPIO_Speed_50MHz;    //50MHz
````



**使能时钟**

> Q:为什么要设置时钟？

任何外设都需要时钟，51单片机，stm32，430等等，因为寄存器是由触发器组成的，往触发器里面写东西，前提条件是有时钟输入。stm32是低功耗，他将所有的门都默认设置为disable(不使能)，在你需要用哪个门的时候，开哪个门就可以，也就是说用到什么外设，只要打开对应外设的时钟就可以，其他的没用到的可以还是disable(不使能)，这样耗能就会减少。

> Q:为什么 STM32 要有多个时钟源呢？

因为首 先 STM32 本身非常复杂，外设非常的多，但是并不是所有外设都需要系统时钟这么高的频率， 比如看门狗以及 RTC 只需要几十 k 的时钟即可。同一个电路，时钟越快功耗越大，同时抗电磁干扰能力也会越弱，所以对于较为复杂的 MCU 一般都是采取多时钟源的方法来解决这些问题。

ARM与C51单片机不同的是，不用外设的时候，如IO口、ADC、定时器等等，都是禁止时钟的，以达到节能的目的，只有要用到的外设，才开启它的时钟。

在`stm32f10x_rcc.h`中声明了

````c
void RCC_AHBPeriphClockCmd(uint32_t RCC_AHBPeriph, FunctionalState NewState);
void RCC_APB2PeriphClockCmd(uint32_t RCC_APB2Periph, FunctionalState NewState);
void RCC_APB1PeriphClockCmd(uint32_t RCC_APB1Periph, FunctionalState NewState);
````

其中第一个参数指要打开哪一组GPIO的时钟，取值参见`stm32f10x_rcc.h`文件中的宏定义，第二个参数为打开或关闭使能，取值参见`stm32f10x.h`文件中的定义，其中`ENABLE`代表开启使能，`DISABLE`代表关闭使能。



**初始化GPIO**

````c
void GPIO_Init(GPIO_TypeDef* GPIOx, GPIO_InitTypeDef*  GPIO_InitStruct);
````

函数配置GPIO，此函数是在`stm32f10x_gpio.c`文件中定义的，其中第一个参数代表要配置哪组GPIO，取值参见`stm32f10x.h`文件中的定义，第二个参数是第1步定义的GPIO的初始化类型结构体。

### 输出

**GPIO电平输出**

| 函数                                                         | 作用                                              |
| ------------------------------------------------------------ | ------------------------------------------------- |
| GPIO_SetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);        | 设置高电平                                        |
| GPIO_ResetBits(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);      | 设置低电平                                        |
| GPIO_WriteBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin, BitAction BitVal); | 根据第三个参数的值，进行写入`Bit_RESET`/`Bit_SET` |
| GPIO_Write(GPIO_TypeDef* GPIOx, uint16_t PortVal);           | 同时对16个端口进行写入                            |

**闪烁**

![3-1 LED闪烁](STM32卷一.assets/3-1 LED闪烁.jpg)

````c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"                      //引入Delay延迟

int main(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);  //使GPIOA使能
	
	GPIO_InitTypeDef GPIO_InitStructure;                   //结构体
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;       //推挽输出
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;              //引脚0
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);                 //使用结构体初始化GPIO
	
	while (1)
	{
        //方式一
		GPIO_ResetBits(GPIOA, GPIO_Pin_0);                 //使GPIOA的GPIO_Pin_0为0
		Delay_ms(500);
		GPIO_SetBits(GPIOA, GPIO_Pin_0);                   //使GPIOA的GPIO_Pin_0为1
		Delay_ms(500);
		//方式二
		GPIO_WriteBit(GPIOA, GPIO_Pin_0, Bit_RESET);       //使GPIOA的GPIO_Pin_0为0
		Delay_ms(500);
		GPIO_WriteBit(GPIOA, GPIO_Pin_0, Bit_SET);         //使GPIOA的GPIO_Pin_0为1
		Delay_ms(500);
		
        //方式三
		GPIO_WriteBit(GPIOA, GPIO_Pin_0, Bit_RESET);
        //GPIO_WriteBit(GPIOA, GPIO_Pin_0, (BitAction)0);
		Delay_ms(500);
		GPIO_WriteBit(GPIOA, GPIO_Pin_0, Bit_SET);
        //GPIO_WriteBit(GPIOA, GPIO_Pin_0, (BitAction)1);
		Delay_ms(500);
	}
}
````

**流水灯**

![3-2 LED流水灯](STM32卷一.assets/3-2 LED流水灯.jpg)

````c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"

int main(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_All;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	while (1)
	{
		GPIO_Write(GPIOA, ~0x0001);	//0000 0000 0000 0001 -->1111 1111 1111 1110 使0号引脚灯亮
		Delay_ms(100);
		GPIO_Write(GPIOA, ~0x0002);	//0000 0000 0000 0010 -->1111 1111 1111 1101 使1号引脚灯亮
		Delay_ms(100);
		GPIO_Write(GPIOA, ~0x0004);	//0000 0000 0000 0100
		Delay_ms(100);
		GPIO_Write(GPIOA, ~0x0008);	//0000 0000 0000 1000
		Delay_ms(100);
		GPIO_Write(GPIOA, ~0x0010);	//0000 0000 0001 0000
		Delay_ms(100);
		GPIO_Write(GPIOA, ~0x0020);	//0000 0000 0010 0000
		Delay_ms(100);
		GPIO_Write(GPIOA, ~0x0040);	//0000 0000 0100 0000
		Delay_ms(100);
		GPIO_Write(GPIOA, ~0x0080);	//0000 0000 1000 0000
		Delay_ms(100);
	}
}
````



**蜂鸣器**

![3-3 蜂鸣器](STM32卷一.assets/3-3 蜂鸣器.jpg)

````c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"

int main(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);   //使用GPIOB接口
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_12;              //使用12引脚
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOB, &GPIO_InitStructure);                  //初始化GPIOB
	
	while (1)
	{
		GPIO_ResetBits(GPIOB, GPIO_Pin_12);
		Delay_ms(100);
		GPIO_SetBits(GPIOB, GPIO_Pin_12);
		Delay_ms(100);
		GPIO_ResetBits(GPIOB, GPIO_Pin_12);
		Delay_ms(100);
		GPIO_SetBits(GPIOB, GPIO_Pin_12);
		Delay_ms(700);
	}
}
````





### 输入

#### 电路即模块介绍

**传感器模块**：传感器元件（光敏电阻/热敏电阻/红外接收管等）的电阻会随外界模拟量的变化而变化，通过与定值电阻分压即可得到模拟电压输出，再通过电压比较器进行二值化即可得到数字电压输出

![c510534f471c4736fc39535699f883a](STM32卷一.assets/c510534f471c4736fc39535699f883a.png)

1. 光敏电阻
2. 比较器

光敏传感器内装有一个高精度的光电管， 光电管内有一块由”针式二管”组成的小平板， 当向光电管两端施加一个反向的固定压时， 任何光了对它的冲击都将导致其释放出电子， 结果是， 当光照强度越高， 光电管的电流也就越大， 电流通过一个电阻时， 电阻两端的电压被转换成可被采集器的数模转换器接受的0-5V 电压， 然后采集以适当的形式把结果保存下来。 简单的说，光敏传感器就是利用光敏电阻受光线强度影响而阻值发生变化的原理向机器人主机发送光线强度的模拟信号。

光敏电阻是利用半导体的光电效应制成的一种电阻值随入射光的强弱而改变的电阻器；入射光强，电阻减小，入射光弱，电阻增大。



**硬件电路**

![082cf282a0444f184d16adff6a315df](STM32卷一.assets/082cf282a0444f184d16adff6a315df.png)

1. 图一：按键接地，必须为上拉输入模式，当按键按下为低电平，松开为高电平
2. 图二：按键接地，可以为浮空输入也可以为上拉输入，当按键按下为低电平，松开为高电平
3. 图三：按键接电源，必须为下拉输入模式，当按键按下为高电平，松开为第电平
4. 图三：按键接电源，可以为浮空输入也可以为下拉输入，当按键按下为高电平，松开为第电平



#### 输入

**GPIO电平输入**

| 函数                                                         | 作用                                            |
| ------------------------------------------------------------ | ----------------------------------------------- |
| uint8_t GPIO_ReadInputDataBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin) | 读取指定端口引脚的输入电平，针对引脚，并返回0/1 |
| uint16_t GPIO_ReadInputData(GPIO_TypeDef* GPIOx)             | 读取指定GPIO端口的输入电平，针对端口            |
| uint8_t GPIO_ReadOutputDataBit(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin) | 读取指定端口引脚的输出电平，针对引脚，并返回0/1 |
| uint16_t GPIO_ReadOutputDate(GPIO_TypeDef* GPIOx)            | 读取指定GPIO端口的输出电平，针对端口            |

**按键控制LED**

![3-4 按键控制LED](STM32卷一.assets/3-4 按键控制LED.jpg)

led程序

````c
#include "stm32f10x.h"                  // Device header
void LED_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);         //GPIOA端口使能
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_2;       //GPIO_Pin_1和GPIO_Pin_2引脚
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	GPIO_SetBits(GPIOA, GPIO_Pin_1 | GPIO_Pin_2);                //GPIO_Pin_1和GPIO_Pin_2引脚为1，即灯熄灭
}

void LED1_ON(void)
{
	GPIO_ResetBits(GPIOA, GPIO_Pin_1);                           //点亮GPIO_Pin_1 的LED
}

void LED1_OFF(void)                                              //关闭GPIO_Pin_1 的LED
{
	GPIO_SetBits(GPIOA, GPIO_Pin_1);
}

//转变，当按键按下 亮，松开 灭
void LED1_Turn(void)                                             
{
	if (GPIO_ReadOutputDataBit(GPIOA, GPIO_Pin_1) == 0)          //读取GPIOA端口GPIO_Pin_1引脚的高低电平，进行反转
	{
		GPIO_SetBits(GPIOA, GPIO_Pin_1);
	}
	else
	{
		GPIO_ResetBits(GPIOA, GPIO_Pin_1);
	}
}
void LED2_ON(void)
{
	GPIO_ResetBits(GPIOA, GPIO_Pin_2);
}

void LED2_OFF(void)
{
	GPIO_SetBits(GPIOA, GPIO_Pin_2);
}

void LED2_Turn(void)
{
	if (GPIO_ReadOutputDataBit(GPIOA, GPIO_Pin_2) == 0)
	{
		GPIO_SetBits(GPIOA, GPIO_Pin_2);
	}
	else
	{
		GPIO_ResetBits(GPIOA, GPIO_Pin_2);
	}
}
````

````c
#ifndef __LED_H
#define __LED_H
void LED_Init(void);
void LED1_ON(void);
void LED1_OFF(void);
void LED1_Turn(void);
void LED2_ON(void);
void LED2_OFF(void);
void LED2_Turn(void);
#endif
````

按键程序

````c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"

void Key_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);       //使能GPIOB
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;               //上拉输入
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_11;     //引脚GPIO_Pin_1和GPIO_Pin_11
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;           //输入模式下GPIO_Speed没用，随便填写
	GPIO_Init(GPIOB, &GPIO_InitStructure);
}

uint8_t Key_GetNum(void)
{
	uint8_t KeyNum = 0;
	if (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_1) == 0)
	{
		Delay_ms(20);                                            //消除抖动
		while (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_1) == 0);
		Delay_ms(20);
		KeyNum = 1;
	}
	if (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_11) == 0)
	{
		Delay_ms(20);
		while (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_11) == 0);
		Delay_ms(20);
		KeyNum = 2;
	}
	
	return KeyNum;
}
````

````c
#ifndef __KEY_H
#define __KEY_H

void Key_Init(void);
uint8_t Key_GetNum(void);

#endif
````

主程序

````c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"
#include "LED.h"
#include "Key.h"

uint8_t KeyNum;

int main(void)
{
	LED_Init();
	Key_Init();
	
	while (1)
	{
		KeyNum = Key_GetNum();
		if (KeyNum == 1)
		{
			LED1_Turn();
		}
		if (KeyNum == 2)
		{
			LED2_Turn();
		}
	}
}
````



**光敏传感器控制蜂鸣器**

![3-5 光敏传感器控制蜂鸣器](STM32卷一.assets/3-5 光敏传感器控制蜂鸣器.jpg)

蜂鸣器程序

````c
#include "stm32f10x.h"                  // Device header

void Buzzer_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_12;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOB, &GPIO_InitStructure);
	
	GPIO_SetBits(GPIOB, GPIO_Pin_12);
}

void Buzzer_ON(void)
{
	GPIO_ResetBits(GPIOB, GPIO_Pin_12);
}

void Buzzer_OFF(void)
{
	GPIO_SetBits(GPIOB, GPIO_Pin_12);
}

void Buzzer_Turn(void)
{
	if (GPIO_ReadOutputDataBit(GPIOB, GPIO_Pin_12) == 0)
	{
		GPIO_SetBits(GPIOB, GPIO_Pin_12);
	}
	else
	{
		GPIO_ResetBits(GPIOB, GPIO_Pin_12);
	}
}
````

````c
#ifndef __BUZZER_H
#define __BUZZER_H

void Buzzer_Init(void);
void Buzzer_ON(void);
void Buzzer_OFF(void);
void Buzzer_Turn(void);

#endif
````

光敏电阻传感器程序,遮住输出1，否则

````c
#include "stm32f10x.h"                  // Device header

void LightSensor_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;               //上拉输入
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_13;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOB, &GPIO_InitStructure);
}

uint8_t LightSensor_Get(void)
{
	return GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_13);           //读取GPIO_Pin_13引脚的光敏电阻
}
````

````c
#ifndef __LIGHT_SENSOR_H
#define __LIGHT_SENSOR_H

void LightSensor_Init(void);
uint8_t LightSensor_Get(void);

#endif
````

主程序

````c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"
#include "Buzzer.h"
#include "LightSensor.h"

int main(void)
{
	Buzzer_Init();
	LightSensor_Init();
	
	while (1)
	{
		if (LightSensor_Get() == 1)
		{
			Buzzer_ON();
		}
		else
		{
			Buzzer_OFF();
		}
	}
}
````



### OLED

使用事先提供好的OLED程序代码,引入到分组中

| **函数**                               | **作用**             |
| -------------------------------------- | -------------------- |
| OLED_Init();                           | 初始化               |
| OLED_Clear();                          | 清屏                 |
| OLED_ShowChar(1, 1, 'A');              | 显示一个字符         |
| OLED_ShowString(1, 3,  "HelloWorld!"); | 显示字符串           |
| OLED_ShowNum(2, 1, 12345, 5);          | 显示十进制数字       |
| OLED_ShowSignedNum(2, 7, -66, 2);      | 显示有符号十进制数字 |
| OLED_ShowHexNum(3, 1, 0xAA55, 4);      | 显示十六进制数字     |
| OLED_ShowBinNum(4, 1, 0xAA55, 16);     | 显示二进制数字       |

其中参数1表示起始行，参数2表示起始行

![b4a78f8967748eea9141eac9304c1e9](STM32卷一.assets/b4a78f8967748eea9141eac9304c1e9.png)

````c
int main(void)
{	
	OLED_Init();
	while(1){
		OLED_ShowChar(1, 1, 'A');
		OLED_ShowNum(2, 1, 12345, 5);
		
		OLED_ShowString(1, 3, "HelloWorld!");
		Delay_ms(500);
		OLED_ShowString(1, 3, "RAINUPUP!  ");
		Delay_ms(500);
	}
}
````

# 中断系统

## 简介

硬件级别的函数跳转

**中断：**在主程序运行过程中，出现了特定的中断触发条件（中断源），使得CPU暂停当前正在运行的程序，转而去处理中断程序，处理完成后又返回原来被暂停的位置继续运行

**中断优先级：**当有多个中断源同时申请中断时，CPU会根据中断源的轻重缓急进行裁决，优先响应更加紧急的中断源

**中断嵌套：**当一个中断程序正在运行时，又有新的更高优先级的中断源申请中断，CPU再次暂停当前中断程序，转而去处理新的中断程序，处理完成后依次进行返回



**STM32中断**

STM32F103中最多有68个可屏蔽中断通道，包含EXTI、TIM、ADC、USART、SPI、I2C、RTC等多个外设

使用NVIC统一管理中断，每个中断通道都拥有16个可编程的优先等级，可对优先级进行分组，进一步设置**抢占优先级**和**响应优先级**



下图为STM32F10XX产品（小容量、中容量和大容量）的向量表； **灰色标住的是体现在内核水平的（异常），其余的是外设水平的（外部中断）。**



![image-20230718160149226](STM32卷一.assets/image-20230718160149226.png)

## NVIC

NVIC：嵌套向量中断控制器(Nested Vectored Interrupt Controller)，它属于M3内核的一个外设，控制着芯片的中断相关功能。由于ARM给NVIC预留了非常多的功能，但对于使用M3内核设计芯片的公司可能就不需要这么多功能，于是就需要在NVIC上裁剪。ST公司的STM32F103芯片内部中断数量就是NVIC裁剪后的结果。对于几乎所有的微控制器，中断都是一种常见的特性。中断一般是由硬件(如外设和外部输人引脚)产生的事件，它会引起程序流偏离正常的流程(如给外设提供服务)。

NVIC相当于一个小助手，接收EXTI、TIM、ADC、USART等中断源的信号，它最终会选择一个中断传送给CPU进行处理

**NVIC基本结构**

![1677758773580](STM32卷一.assets/1677758773580.png)





**NVIC优先级分组**

1. STM32F103芯片支持60个可屏蔽中断通道，每个中断通道都具备自己的中断优先级控制字节（8位，但是STM32F103中只使用4位，高4位有效），用于表达优先级的高4位又被分为组成抢占式优先级和响应式优先级，通常也把响应优先级称为“亚优先级”或“副优先级”，每个中断源都需要被指定这两种优先级。
2. NVIC的中断优先级由优先级寄存器的4位（0~15）决定，这4位可以进行切分，分为高n位的抢占优先级和低4-n位的响应优先级；抢占优先级高的可以中断嵌套，响应优先级高的可以优先排队，抢占优先级和响应优先级均相同的按中断号排队

   * 抢占优先级：高抢占式优先级的中断事件会打断当前的主程序或中断程序运行，俗称中断嵌套。
   * 响应优先级: 等待其他中断，在抢占式优先级相同的情况下，高响应优先级的中断优先被响应(响应优先级无法被打断)。
   * 当两个中断源的抢占式优先级相同时，这两个中断将没有嵌套关系，当一个中断到来后，如果正在处理另一个中断，这个后到来的中断就要等待前一个中断处理完之后才能被处理。如果这两个中断同时到达，则中断控制器根据他们的响应优先级高低来决定先处理哪一个；如果他们的抢占式优先级和响应优先级都相等，则根据他们在中断表(上面的向量表)中的排位顺序决定先处理哪一个。
   * 自然优先级：中断向量表中的默认优先级

STM32F103中指定中断优先级的寄存器位有4位，这4位的分组方式如下：（4个优先级描述位可以有5中组合方式）

无论是抢占优先级（主优先级）还是响应优先级（子优先级），优先级数值越小，就代表优先级越高。这一点与FreeRTOS不同

| **分组方式** |    **优先级分组**    | **抢占优先级**  | **响应优先级**  |
| :----------: | :------------------: | :-------------: | :-------------: |
|    分组0     | NVIC_PriorityGroup_0 |  0位，取值为0   | 4位，取值为0~15 |
|    分组1     | NVIC_PriorityGroup_1 | 1位，取值为0~1  | 3位，取值为0~7  |
|    分组2     | NVIC_PriorityGroup_2 | 2位，取值为0~3  | 2位，取值为0~3  |
|    分组3     | NVIC_PriorityGroup_3 | 3位，取值为0~7  | 1位，取值为0~1  |
|    分组4     | NVIC_PriorityGroup_4 | 4位，取值为0~15 |  0位，取值为0   |

**NVIC寄存器**

| NVIC相关寄存器                        | 位数 | 寄存器个数 | 备注                                  |
| ------------------------------------- | ---- | ---------- | ------------------------------------- |
| 中断使能寄存器（ISER）                | 32   | 8          | 每个位控制一个中断                    |
| 中断除能寄存器（ICER）                | 32   | 8          | 每个位控制一个中断                    |
| 应用程序中断及复位控制寄存器（AIRCR） | 32   | 1          | 位[10:8]控制优先级分组                |
| 中断优先级寄存器（IPR）               | 8    | 240        | 8个位对应一个中断，而STM32只使用高4位 |

| **优先级分组** | **AIRCR[10:8]** | **IPRxbit[7:4]分** |         **分配结果**         |
| :------------: | :-------------: | :----------------: | :--------------------------: |
|       0        |       111       |    None ：[7:4]    | 0位抢占优先级，4位响应优先级 |
|       1        |       110       |    [7] ：[6:4]     | 1位抢占优先级，3位响应优先级 |
|       2        |       101       |   [7:6] ：[5:4]    | 2位抢占优先级，2位响应优先级 |
|       3        |       100       |   [7:5]   ：[4]    | 3位抢占优先级，1位响应优先级 |
|       4        |       011       |    [7:4] ：None    | 4位抢占优先级，0位响应优先级 |

## HAL库

定义在stm32f1xx_hal_cortex.c下

````c
/**设置中断优先级分组函数
* NVIC_PRIORITYGROUP_0 
* NVIC_PRIORITYGROUP_1
* NVIC_PRIORITYGROUP_2
* NVIC_PRIORITYGROUP_3
* NVIC_PRIORITYGROUP_4
**/
void HAL_NVIC_SetPriorityGrouping(uint32_t PriorityGroup); 
/**	设置某个中断的抢占/响应优先级
*	参数1：设置中断
*	参数2：抢占优先级
*	参数3：响应优先级
**/
void HAL_NVIC_SetPriority(IRQn_Type IRQn, uint32_t PreemptPriority,uint32_t SubPriority);
/**	使能某个中断
**/
void HAL_NVIC_EnableIRQ(IRQn_Type IRQn);
void HAL_NVIC_disableIRQ(IRQn_Type IRQn);
````

````c
typedef enum{
  //…………
  EXTI0_IRQn                  = 6,      /*!< EXTI Line0 Interrupt                                 */
  TIM5_IRQn                   = 50,     /*!< TIM5 global Interrupt                                */
} IRQn_Type;
````

## 标准库

**NVIC**

NVIC需要的函数被定义在了`misc.c`中

| 函数                                                         | 作用                                                |
| ------------------------------------------------------------ | --------------------------------------------------- |
| void NVIC_PriorityGroupConfig(uint32_t NVIC_PriorityGroup);  | 设置抢断优先级分组，NVIC_PriorityGroup_0……          |
| void NVIC_Init(NVIC_InitTypeDef* NVIC_InitStruct);           | 根据NVIC_InitStruct结构体变量中的参数初始化NVIC外设 |
| void NVIC_SetVectorTable(uint32_t NVIC_VectTab, uint32_t Offset); | 设置向量表的位置和偏移量                            |
| void NVIC_SystemLPConfig(uint8_t LowPowerMode, FunctionalState NewState); | 配置系统进入低功耗模式的条件                        |
| void SysTick_CLKSourceConfig(uint32_t SysTick_CLKSource);    | 配置SysTick时钟源                                   |

**NVIC_InitTypeDef结构体**

````c
typedef struct
{
  //指定要启用或禁用的IRQ通道。该参数是@ref IRQn_Type的值(有关完整的STM32设备IRQ通道列表，请参考stm32f10x.h文件)
  uint8_t NVIC_IRQChannel;                      //指定中断源  
  
  //指定IRQ通道的优先级NVIC_IRQChannel中指定。该参数可以是一个值在0到15之间，如表@ref NVIC_Priority_Table所述   
  //设置抢占优先级，中断优先级分组不同，抢占优先级的位数不同。如NVIC_PriorityGroup_2，则添0~3
  uint8_t NVIC_IRQChannelPreemptionPriority;   
    
  //为指定的IRQ通道指定子优先级在NVIC_IRQChannel。该参数可以是一个值在0到15之间，如表@ref NVIC_Priority_Table所述
  //设置响应优先级，中断优先级分组不同，响应优先级的位数不同。如NVIC_PriorityGroup_2，则添0~3
  //无论是抢占优先级（主优先级）还是响应优先级（子优先级），优先级数值越小，就代表优先级越高。
  uint8_t NVIC_IRQChannelSubPriority;        

  //指定是否在NVIC_IRQChannel中定义的IRQ通道将启用或禁用。可设置为“ENABLE”或“DISABLE”
  FunctionalState NVIC_IRQChannelCmd;           //使能或者失能
} NVIC_InitTypeDef; 
````

NVIC_IRQChannel被定义在了`stm32f10x.h`中，定义了很多STM32F1XX的IRQChannel，我们只需要选择对应的型号

这个就是一个外部中断的入口通道(定时中断、外部中断……)，每个中断对应一个通道，中断发生后查询这个通道值就可以知道是哪个通道发生了中断 

例如：`NVIC_IRQChannel = EXTI15_10_IRQn ` 外部中断10~15号

````c
typedef enum IRQn{
#ifdef STM32F10X_CL
  //…………
  TIM1_UP_IRQn                = 25,     /*!< TIM1 Update Interrupt                                */
  TIM4_IRQn                   = 30,     /*!< TIM4 global Interrupt                                */
  I2C1_EV_IRQn                = 31,     /*!< I2C1 Event Interrupt                                 */
  SPI1_IRQn                   = 35,     /*!< SPI1 global Interrupt                                */
  USART1_IRQn                 = 37,     /*!< USART1 global Interrupt                              */
  EXTI15_10_IRQn              = 40,     /*!< External Line[15:10] Interrupts                      */
  //…………
#endif /* STM32F10X_CL */     
} IRQn_Type;
````

例如

````c
// 整个STM32中只能有一种分组，所以在main程序中定义一次就行。如果在模块函数中定义，那么每个模块函数都只能是一种分组
NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);            //设置优先级分组为2
NVIC_InitTypeDef NVIC_InitStructure;                       //定义NVIC初始化结构体
NVIC_InitStructure.NVIC_IRQChannel = EXTI15_10_IRQn;       //外部中断EXTI10~15_IRQn
NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;            //使能外部中断

//由于使用的NVIC_PriorityGroup_2优先级，取值为0~3；不同优先级取值不同，详细见上表
NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 1;  //抢占优先级1
NVIC_InitStructure.NVIC_IRQChannelSubPriority = 1;         //抢占优先级1
NVIC_Init(&NVIC_InitStructure);                            //初始化NVIC
````



# EXTI

## **简介**

1. EXTI（Extern Interrupt）：外部中断
2. EXTI可以监测指定GPIO口的电平信号，当其指定的GPIO口产生电平变化时，EXTI将立即向NVIC发出中断申请，经过NVIC裁决后即可中断CPU主程序，使CPU执行EXTI对应的中断程序
3. EXTI管理了控制器的20个中断/事件线。每个中断/事件线都对应有一个边沿检测器，可以实现输入信号的上升沿检测和下降沿的检测。EXTI可以实现对每个中断/事件线进行单独配置，可以单独配置为中断或者事件，以及触发事件的属性。
4. 支持的触发方式：上升沿/下降沿/双边沿(上下沿)/软件触发
5. 支持的GPIO口：所有GPIO口，但**相同的Pin不能同时触发中断**
6. 通道数：16个GPIO_Pin，外加PVD输出、RTC闹钟、USB唤醒、以太网唤醒；一共20个
7. 触发响应方式：中断响应 / 事件响应（响应事件，触发外部设备等）



**EXTI基本结构**

![d0299987b70c0486dd84ca43dc94e46](STM32卷一.assets/d0299987b70c0486dd84ca43dc94e46.png)



GPIOA/B/C……等中的16个引脚进入AFIO中进行中断引脚选择，AFIO的中的16个接口+PVD/RTC/USB/ETH一共20个进入EXTI，最终通往NVIC或其他外设(事件中断)



## **AFIO复用IO口**

AFIO主要用于引脚复用功能的选择和重定义，在STM32中，AFIO主要完成两个任务：复用功能引脚重映射、中断引脚选择



![5cc6e021654f4204d903a8134ef8c5e](STM32卷一.assets/5cc6e021654f4204d903a8134ef8c5e.png)

解释：AFIO选择GPIOA/B等端口中的其中一个引脚进行输出；如EXTI0，它会选择PA0~PG0其中一个进行输出；这就是为什么相同的Pin不能同时触发中断

**寄存器**

1. 调试IO配置：AFIO_MAPR[26:24]，配置JTAG/SWD的开关状态
2. 重映射配置：AFIO_MAPR，部分外设IO重映射配置
3. 外部中断配置：AFIO_EXTICR1\~4，配置EXTI中断线0~15对应具体哪个IO口



**特别注意**：配置AFIO寄存器之前要使能AFIO时钟，方法如下：

* HAL库：__HAL_RCC_AFIO_CLK_ENABLE();  
* 标准库：RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE); 
* F4/F7/H7系列：__HAL_RCC_SYSCFG_CLK_ENABLE();

## **EXTI框图**

![1677761523931](STM32卷一.assets/1677761523931.png)

经过GPIO判断后，最终进入输入线



软件中断事件寄存器：可以模拟软件中断，可见他没有连接到输入线

请求挂起寄存器：就是对应中断标记位

* 调用`EXTI_GetITStatus(uint32_t EXTI_Line)`函数，查看该寄存器的对应位是否为1
* 调用`EXTI_ClearITPendingBit(uint32_t )`函数，清除寄存器对应位



其中蓝色线为中断触发，红色线为事件触发。

1. 输入线：EXTI 0-15是连接到GPIO（每一个GPIO端口都有16个引脚），当我们使用EXTI0的时候，控制的是所有端口的第0个引脚。具体是哪个端口，在AFIO_EXTICR1、2、3、4这4个寄存器的EXTIx[3:0]位控制。（x属于0-15）
2. 边沿检测电路：检测上升沿还是下降沿，由上升沿触发选择寄存器(EXTI_RTSR)和下降沿触发选择寄存器(EXTI_FTSR)控制。
3. 或门：收到边沿检测电路传出的信号和软件中断事件寄存器(EXTI_SWIER)控制。软件中断事件寄存器返回1之后，就不受边沿检测电路控制。
4. 在经过或门之后，分为两路：
   - 当中断屏蔽寄存器和请求挂起寄存器相关位都置1的时候就会产生中断，交给NVIC，再交给内核相应。
   - 如果事件屏蔽寄存器相关位置1，就会把这个1信号给脉冲发生器，产生脉冲（脉冲就是高电平）。脉冲：ITM定时器开始计数、触发ADC的采集。【作为触发信号】



EXTI和NVIC不需要开启时钟，EXTI一直是开着的，在寄存器中没有控制他时钟的定义。NVIC是内核外设，不需要开启时钟



## HAL库

**步骤：**

1. 使能GPIO时钟：__HAL_RCC_GPIOx_CLK_ENABLE
2. GPIO/AFIO(SYSCFG)/EXTI：HAL_GPIO_Init，一步到位
3. 设置中断分组：HAL_NVIC_SetPriorityGrouping，此函数仅需设置一次！
4. 设置中断优先级：HAL_NVIC_SetPriority
5. 使能中断：HAL_NVIC_EnableIRQ
6. 设计中断服务函数：EXTIx_IRQHandler，中断服务函数，清中断标志！

**HAL库中断回调处理机制介绍**

![image-20230802142508465](STM32卷一.assets/image-20230802142508465.png)

中断服务函数：就是产生中断后处理的函数，如EXTI2_IRQHandler

HAL库中断处理公用函数：HAL_GPIO_EXTI_IRQHandler,清除中断标志位

HAL库数据处理回调函数：最终调用此函数，这个函数是弱定义函数，在这个函数中写中断处理

````c
//stm32f1xx_hal_gpio.c
void HAL_GPIO_EXTI_IRQHandler(uint16_t GPIO_Pin){
  /* EXTI line interrupt detected */
  if (__HAL_GPIO_EXTI_GET_IT(GPIO_Pin) != 0x00u){
    __HAL_GPIO_EXTI_CLEAR_IT(GPIO_Pin);             //清除中断
    HAL_GPIO_EXTI_Callback(GPIO_Pin);               //调用回调函数
  }
}
__weak void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)//弱定义
{
}
````

**案例**：中断控制LED

````c
//GPIO_Pin2的中断函数
void EXTI2_IRQHandler (void){
    HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_2);       // 调用HAL库中断处理公用函数，在里面会调用回调函数，并清除中断标志位
    __HAL_GPIO_EXTI_CLEAR_IT(GPIO_PIN_2);
}
void EXTI3_IRQHandler (void){
    HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_3);
    __HAL_GPIO_EXTI_CLEAR_IT(GPIO_PIN_3); 
}
void EXTI4_IRQHandler (void){
    HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_4);
    __HAL_GPIO_EXTI_CLEAR_IT(GPIO_PIN_4);
}
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin){ // 中断回调函数，在这个函数中写中断处理的内容
    delay_ms(20);
    switch(GPIO_Pin){
        case GPIO_PIN_2:
            if(HAL_GPIO_ReadPin(GPIOE,GPIO_PIN_2) == 0){
                LED0_TOGGLE();
                LED1_TOGGLE();
            }
            break;
        case GPIO_PIN_3:
            if(HAL_GPIO_ReadPin(GPIOE,GPIO_PIN_3) == 0){
                LED0_TOGGLE();
            }
            break;
        case GPIO_PIN_4:
            if(HAL_GPIO_ReadPin(GPIOE,GPIO_PIN_4) == 0){
                LED1_TOGGLE();
            }
            break;
        default:break;
    }
}
void EXTI_Init(void){ 
    GPIO_InitTypeDef GPIO_InitStructure;
    __HAL_RCC_GPIOE_CLK_ENABLE();                                // 使能GPIOE
    
    GPIO_InitStructure.Mode = GPIO_MODE_IT_FALLING;              // 下降沿触发中断
    GPIO_InitStructure.Pin = GPIO_PIN_2 | GPIO_PIN_3 |GPIO_PIN_4;
    GPIO_InitStructure.Pull = GPIO_PULLUP;                       // 默认为上拉输入
    GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH;
    
    HAL_GPIO_Init(GPIOE,&GPIO_InitStructure);                    // 使用GPIO一步定义GPIO/AFIO/EXTI
    
    //设置NVIC
    HAL_NVIC_SetPriorityGrouping(NVIC_PRIORITYGROUP_2);
    HAL_NVIC_SetPriority(EXTI2_IRQn,2,2);
    HAL_NVIC_SetPriority(EXTI3_IRQn,2,2);
    HAL_NVIC_SetPriority(EXTI4_IRQn,2,2);
    HAL_NVIC_EnableIRQ(EXTI2_IRQn);
    HAL_NVIC_EnableIRQ(EXTI3_IRQn);
    HAL_NVIC_EnableIRQ(EXTI4_IRQn);
}
int main(void){
    //……
    LED_init();                             /* 初始化LED */
    EXTI_Init();
   
    while(1)
    {
    }
}
````









## 标准库

### 函数

| 函数                                                         | 作用                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| void GPIO_EXTILineConfig(uint8_t GPIO_PortSource, uint8_t GPIO_PinSource) | 配置AFIO的数据选择器，选择某个GPIO端口，选择一个中断线路 |

| 函数                                                    | 作用                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| void EXTI_DeInit(void)                                  | 将EXTI外设寄存器重置为默认值                                 |
| void EXTI_Init(EXTI_InitTypeDef* EXTI_InitStruct)       | 根据EXTI_InitStruct结构体中所配置的参数来初始化EXTI外设      |
| void EXTI_StructInit(EXTI_InitTypeDef* EXTI_InitStruct) | 将EXTI_InitStruct结构体中各成员按默认值填充                  |
| void EXTI_GenerateSWInterrupt(uint32_t EXTI_Line)       | 产生一个软件中断                                             |
| FlagStatus EXTI_GetFlagStatus(uint32_t EXTI_Line)       | 获取普通标志位,检查指定的标志是否被置位                      |
| void EXTI_ClearFlag(uint32_t EXTI_Line)                 | 清除普通标志位                                               |
| ITStatus EXTI_GetITStatus(uint32_t EXTI_Line)           | 获取中断标志位,检查指定的中断标志是否被置位；返回值SET/RESET |
| void EXTI_ClearITPendingBit(uint32_t )                  | 清除中断标志位                                               |



**EXTI_InitTypeDef结构体**

````c
typedef struct
{
  //指定要启用或禁用的EXTI行。用于设置外部线路,如使用外部中断14，则取值EXTI_Line14
  uint32_t EXTI_Line;                
  
  //指定EXTI行模式。
  //取值：  EXTI_Mode_Interrupt 外部中断
  //       EXTI_Mode_Event     事件中断
  EXTIMode_TypeDef EXTI_Mode;    
    
  //为EXTI行指定触发信号活动边缘。
  //取值：EXTI_Trigger_Rising          设置上升沿为中断请求
  //     EXTI_Trigger_Falling         设置上升沿为中断请求
  //     EXTI_Trigger_Rising_Falling  设置上升/下降沿都能触发中断请求
  EXTITrigger_TypeDef EXTI_Trigger; 
    
  //指定所选EXTI行的新状态。可设置为“ENABLE”或“DISABLE”
  FunctionalState EXTI_LineCmd;
}EXTI_InitTypeDef;
````

初始化一个EXTI

````c
GPIO_EXTILineConfig(GPIO_PortSourceGPIOB, GPIO_PinSource14);   //APIO设置，使用GPIOB，14号引脚作为中断源触发

EXTI_InitTypeDef EXTI_InitStructure;                      //定义一个EXTI结构体	
EXTI_InitStructure.EXTI_Line = EXTI_Line14;               //使用外部中断线14 
EXTI_InitStructure.EXTI_LineCmd = ENABLE;                 //使能线路
EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;       //中断请求模式
EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Falling;   //下降沿触发
EXTI_Init(&EXTI_InitStructure);                           //使用结构体初始化EXTI
````



每次中断程序结束后，都应该清除一下中断标志位,因为如果不清除中断标志位，那么这个中断会一直申请中断;使用`EXTI_ClearFlag(EXTI_Line) / EXTI_ClearITPendingBit(EXTI_Line）`



中断程序的名字都是固定的，参考`startup_stm32f10x_md.s`的100行左右（这个文件不是固定的，不同的型号对应不同的文件，参考上方笔记）

例如使用10~15号中断，则中断程序名为`EXTI15_10_IRQHandler`

| 中断      | 对应函数             |
| --------- | -------------------- |
| EXTI0     | EXTI0_IROHandler     |
| EXTI1     | EXTI1_IROHandler     |
| EXTI2     | EXTI2_IROHandler     |
| EXTI3     | EXTI3_IROHandler     |
| EXTI4     | EXTI4_IROHandler     |
| EXTI9_5   | EXTI9_5_IROHandler   |
| EXTI15_10 | EXTI15_10_IRQHandler |

### 程序演示

注意：在中断程序中不要操作外部设备，可能会照成错误(例如：在中断程序中操作OLED，那么OLED会出现错误)

步骤：

1. RCC开启时钟
2. 配置GPIO
3. 配置AFIO
4. 配置EXTI
5. 配置NVIC

![5-1 对射式红外传感器计次](STM32卷一.assets/5-1 对射式红外传感器计次.jpg)

````c
#include "stm32f10x.h"                  // Device header

uint16_t CountSensor_Count;

void CountSensor_Init(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE); 
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);              //使能AFIO的时钟
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_14;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOB, &GPIO_InitStructure);
	
	GPIO_EXTILineConfig(GPIO_PortSourceGPIOB, GPIO_PinSource14);      //配置AFIO的数据选择器，选择GPIOB端口，选择14号引脚作为中断线路
	 
	EXTI_InitTypeDef EXTI_InitStructure;                              //EXTI初始化结构体
	EXTI_InitStructure.EXTI_Line = EXTI_Line14;                       //使用Line14作为中断线路
	EXTI_InitStructure.EXTI_LineCmd = ENABLE;                         //使能EXTI
	EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;               //使用中断模式
	EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Falling;           //使用下降沿触发
	EXTI_Init(&EXTI_InitStructure);                                   //初始化EXTI
	
	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);                   //选择NVIC的优先级
	 
	NVIC_InitTypeDef NVIC_InitStructure;                              //NVIC初始化结构体
	NVIC_InitStructure.NVIC_IRQChannel = EXTI15_10_IRQn;              //10~15外部中断
	NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;                   //使能NVIC
	NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 1;         //抢占优先级，我们设置的是NVIC_PriorityGroup_2优先级，抢占优先级为0~3
	NVIC_InitStructure.NVIC_IRQChannelSubPriority = 1;                //中断优先级，我们设置的是NVIC_PriorityGroup_2优先级，中断优先级为0~3
	NVIC_Init(&NVIC_InitStructure);                                   //初始化EXTI
}

uint16_t CountSensor_Get(void)
{
	return CountSensor_Count;
}

void EXTI15_10_IRQHandler(void)                                        //中断函数，此函数名固定
{
	if (EXTI_GetITStatus(EXTI_Line14) == SET)                          //获得外部中断标记
	{
		/*如果出现数据乱跳的现象，可再次判断引脚电平，以避免抖动*/
		if (GPIO_ReadInputDataBit(GPIOB, GPIO_Pin_14) == 0)
		{
			CountSensor_Count ++;
		}
		EXTI_ClearITPendingBit(EXTI_Line14);                            //清除外部中断标记，否则会持续发起中断
	}
}
````

````c
#include "stm32f10x.h"                  // Device header
#include "Delay.h"
#include "OLED.h"
#include "CountSensor.h"

int main(void)
{
	OLED_Init();
	CountSensor_Init();
	
	OLED_ShowString(1, 1, "Count:");
	
	while (1)
	{
		OLED_ShowNum(1, 7, CountSensor_Get(), 5);
	}
}
````



# 定时中断

**STM32定时器分类**

![image-20230803120920087](STM32卷一.assets/image-20230803120920087.png)

## 简介

1. TIM（Timer）定时器

2. 定时器可以对输入的时钟进行计数，并在计数值达到设定值时触发中断

3. 16位计数器、预分频器、自动重装寄存器的时基单元，在72MHz计数时钟下可以实现最大59.65s的定时

4. 不仅具备基本的定时中断功能，而且还包含内外时钟源选择、输入捕获、输出比较、编码器接口、主从触发模式等多种功能

5. 根据复杂度和应用场景分为了**高级定时器**、**通用定时器**、**基本定时器**三种类型


|  **类型**  |        **编号**        | **总线** | **计数模式**         |                           **功能**                           |
| :--------: | :--------------------: | :------: | -------------------- | :----------------------------------------------------------: |
| 高级定时器 |       TIM1、TIM8       |   APB2   | 递增、递减、中央对齐 | 拥有通用定时器全部功能，并额外具有重复计数器、死区生成、互补输出、刹车输入等功能 |
| 通用定时器 | TIM2、TIM3、TIM4、TIM5 |   APB1   | 递增、递减、中央对齐 | 拥有基本定时器全部功能，并额外具有内外时钟源选择、输入捕获、输出比较、编码器接口、主从触发模式等功能(DAC/ADC) |
| 基本定时器 |       TIM6、TIM7       |   APB1   | 递增                 |  拥有定时中断、主模式触发DAC的功能、常用作时基，即定时功能   |

**基本定时器**

![1681382319303](STM32卷一.assets/1681382319303.png)



**通用定时器**

![1681382381310](STM32卷一.assets/1681382381310.png)

STM32的众多定时器中我们使用最多的是高级定时器和通用定时器，而高级定时器一般也是用作通用定时器的功能，下面我们就以通用定时器为例进行讲解，其功能和特点包括：

1. 位于低速的APB1总线上(APB1)

2. 16 位向上、向下、向上/向下(中心对齐)计数模式，自动装载计数器（TIMx_CNT）。

3. 16 位可编程(可以实时修改)预分频器(TIMx_PSC)，计数器时钟频率的分频系数 为 1～65535 之间的任意数值。

4. 4 个独立通道（TIMx_CH1~4），这些通道可以用来作为： 

   1. 输入捕获 
   2. 输出比较
   3. PWM 生成(边缘或中间对齐模式) 
   4. 单脉冲模式输出 

5. 可使用外部信号（TIMx_ETR）控制定时器和定时器互连（可以用 1 个定时器控制另外一个定时器）的同步电路。

6. 如下事件发生时产生中断/DMA（6个独立的IRQ/DMA请求生成器）： 

   1. 更新：计数器向上溢出/向下溢出，计数器初始化(通过软件或者内部/外部触发) 
   2. 触发事件(计数器启动、停止、初始化或者由内部/外部触发计数) 
   3. 输入捕获 
   4. 输出比较 
   5. 支持针对定位的增量(正交)编GGGGGG码器和霍尔传感器电路 
   6. 触发输入作为外部时钟或者按周期的电流管理

7. STM32 的通用定时器可以被用于：测量输入信号的脉冲长度(输入捕获)或者产生输出波形(输出比较和 PWM)等。   

8. 使用定时器预分频器和 RCC 时钟控制器预分频器，脉冲长度和波形周期可以在几个微秒到几个毫秒间调整。STM32 的每个通用定时器都是完全独立的，没有互相共享的任何资源。

   

**高级定时器**

![1681383994101](STM32卷一.assets/1681383994101.png)



### **计数器模式**

通用定时器可以向上计数、向下计数、向上向下双向计数模式。

1. 向上计数模式：计数器从0计数到自动加载值(TIMx_ARR)，然后重新从0开始计数并且产生一个计数器溢出事件。
2. 向下计数模式：计数器从自动装入的值(TIMx_ARR)开始向下计数到0，然后从自动装入的值重新开始，并产生一个计数器向下溢出事件。
3. 中央对齐模式（向上/向下计数）：计数器从0开始计数到自动装入的值-1，产生一个计数器溢出事件，然后向下计数到1并且产生一个计数器溢出事件；然后再从0开始重新计数。

![img](STM32卷一.assets/20200408201830677.png)



### 工作原理

![1681384695364](STM32卷一.assets/1681384695364.png)

主要分为四大部分：时钟产生器部分，时基单元部分，输入捕获部分、输出比较部分。

**时钟产生器部分**

STM32定时器有四种时钟源选择，分别是：

1. 内部时钟(CK_INT)
2. 外部时钟模式：外部触发输入(ETR)
3. 内部触发输入(ITRx)：使用一个定时器作为另一个定时器的预分频器，如可以配置一个定时器Timer1而作为另一个定时器Timer2的预分频器。
4. 外部时钟模式：外部输入脚(TIx)

**时基单元部分**

包括三个寄存器：计数器寄存器（TIMx_CNT)、预分频器寄存器（TIMx_PSC)、自动装载寄存器（TIMx_ARR)。

1. 计数器寄存器（TIMx_CNT)：向上计数、向下计数或者中心对齐计数；
2. 预分频器寄存器（TIMx_PSC)：可将时钟频率按1到65535之间的任意值进行分频，可在运行时改变其设置值；
3. 自动装载寄存器（TIMx_ARR)：如果TIMx_CR1寄存器中的ARPE位为0，ARR寄存器的内容将直接写入影子寄存器；如果ARPE为1，ARR寄存器的那日同将在每次的更新时间UEV发生时，传送到影子寄存器；

如果TIM1_CR1中的UDIS位为0，当计数器产生溢出条件时，产生更新事件。

**输入捕获部分**

1. IC1、2和IC3、4可以分别通过软件设置将其映射到TI1、TI2和TI3、TI4;
2. 4个16位捕捉比较寄存器可以编程用于存放检测到对应的每一次输入捕捉时计数器的值;
3. 当产生一次捕捉，相应的CCxIF标志位被置1;同时如果中断或DMA请求使能，则产生中断或DMA请求。
4. 如果当CCxIF标志位已经为1，当又产生一个捕捉，则捕捉溢出标志位CCxOF将被置1。

**输出比较部分**

1. PWM模式运行产生:

   1. 定时器2、3和4可以产生4独立的信号

   2. 频率和占空比可以进行如下设定:

      1. 一个自动重载寄存器用于设定PWM的周期;

      2. 每个PWM通道有一个捕捉比较寄存器用于设定占空时间。

         例如:产生一个40KHz的PWM信号:在定时器2的时钟为72MHz下，占空比为50% :

         预分频寄存器设置为0 (计数器的时钟为TIM1CLK/(O+1))，自动重载寄存器设为1799，CCRx寄存器设为899。

2. 两种可设置PWM模式:

   1. 边沿对齐模式
   2. 中心对齐模式

### 定时中断基本结构

![1681385764245](STM32卷一.assets/1681385764245.jpg)



### 时序

**预分频器时序**：以预分频从1变为2为例，本来一个振荡计数器加1，变为两个振荡计数器加1

![image-20230718192627946](STM32卷一.assets/image-20230718192627946.png)

* **计数器计数频率**：CK_CNT = CK_PSC / (PSC + 1)   计数器频率 = 时钟 / (预分频 + 1)
  * 以时钟频率为72Mhz，预分频为7199为例，计数器频率为1s计数10000次

**计数器时序**

![image-20230718193727514](STM32卷一.assets/image-20230718193727514.png)

* **计数器溢出频率**：CK_CNT_OV = CK_CNT / (ARR + 1) = CK_PSC / (PSC + 1) / (ARR + 1)  计数器溢出 = 时钟 / (预分频 + 1) / (自动重装值 + 1)
  * 以时钟频率为72Mhz，预分频为7199为例，计数器频率为9999次，每秒溢出一次，即产生一个更新中断



**计数器无预装时序**

更改计数器自动重装值立即生效

![image-20230718194957769](STM32卷一.assets/image-20230718194957769.png)

**计数器有预装时序**

更改自动重装值，先写入影子寄存器，等到下一个计数器溢出，自动重装值才生效

![image-20230718195030406](STM32卷一.assets/image-20230718195030406.png)



## 基本定时器

### HAL库

基本定时器

#### **配置步骤**

1. 配置定时器基础工作参数：HAL_TIM_Base_Init()
2. 定时器基础MSP初始化：HAL_TIM_Base_MspInit()   配置NVIC、CLOCK等
3. 使能更新中断并启动计数器：HAL_TIM_Base_Start_IT()
4. 设置优先级，使能中断：HAL_NVIC_SetPriority()、 HAL_NVIC_EnableIRQ()
5. 编写中断服务函数：TIMx_IRQHandler()等  --> HAL_TIM_IRQHandler()
6. 编写定时器更新中断回调函数：HAL_TIM_PeriodElapsedCallback()

|              函数               |  主要寄存器   |               主要功能               |
| :-----------------------------: | :-----------: | :----------------------------------: |
|       HAL_TIM_Base_Init()       | CR1、ARR、PSC |         初始化定时器基础参数         |
|     HAL_TIM_Base_MspInit()      |      无       |   存放NVIC、CLOCK、GPIO初始化代码    |
|     HAL_TIM_Base_Start_IT()     |   DIER、CR1   |       使能更新中断并启动计数器       |
|      HAL_TIM_IRQHandler()       |      SR       | 定时器中断处理公用函数，处理各种中断 |
| HAL_TIM_PeriodElapsedCallback() |      无       | 定时器更新中断回调函数，由用户重定义 |

````c
/* 定时器溢出中断中断回调函数 */
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim);
/* 使能TIM */    
__HAL_RCC_TIMX_CLK_ENABLE();

/* 软件产生中断，参数1：TIM句柄，参数2：中断类型 */
HAL_StatusTypeDef HAL_TIM_GenerateEvent(TIM_HandleTypeDef *htim, uint32_t EventSource)
````



**句柄结构体**：基本定时器、通用定时器、高级定时器都是使用的同一个句柄结构体

````c
typedef struct { 
    TIM_TypeDef *Instance;         /* 外设寄存器基地址 */ 
    TIM_Base_InitTypeDef Init;     /* 定时器初始化结构体 */
   HAL_TIM_ActiveChannel Channel;  /* 外设的哪个通道 */
     ...
}TIM_HandleTypeDef;
typedef struct { 
    uint32_t Prescaler;            /* 预分频系数 */ 
    uint32_t CounterMode;          /* 计数模式 */ 
    uint32_t Period;               /* 自动重载值 ARR */ 
    uint32_t ClockDivision;        /* 时钟分频因子，高级定时器 */ 
    uint32_t RepetitionCounter;    /* 重复计数器寄存器的值，高级定时器 */ 
    uint32_t AutoReloadPreload;    /* 自动重载预装载使能，高级定时器 */
} TIM_Base_InitTypeDef;
//CounterMode参数
#define TIM_COUNTERMODE_UP                 0x00000000U    /* 向上计数  */
#define TIM_COUNTERMODE_DOWN               TIM_CR1_DIR    /* 向下计数  */                       
#define TIM_COUNTERMODE_CENTERALIGNED1     TIM_CR1_CMS_0  /* 中间计数  */                      
#define TIM_COUNTERMODE_CENTERALIGNED2     TIM_CR1_CMS_1                        
#define TIM_COUNTERMODE_CENTERALIGNED3     TIM_CR1_CMS                         
````

#### 案例

使用定时器6，实现500ms定时器更新中断，在中断里翻转LED0

````c
TIM_HandleTypeDef g_timx_handle;

/* 定时器中断初始化函数 */
void btim_timx_int_init(uint16_t arr, uint16_t psc){
    g_timx_handle.Instance = TIM6;
    g_timx_handle.Init.Prescaler = psc;           // 预分频
    g_timx_handle.Init.Period = arr;              // 自动重装
    HAL_TIM_Base_Init(&g_timx_handle);

    HAL_TIM_Base_Start_IT(&g_timx_handle);        // 开启更新中断，内部自动调用__HAL_TIM_ENABLE_IT(htim, TIM_IT_UPDATE);
}
/* 定时器基础MSP初始化函数 */
void HAL_TIM_Base_MspInit(TIM_HandleTypeDef *htim){
    if (htim->Instance == TIM6){
        __HAL_RCC_TIM6_CLK_ENABLE();              // 使能TIM6
        HAL_NVIC_SetPriority(TIM6_IRQn, 1, 3);
        HAL_NVIC_EnableIRQ(TIM6_IRQn);
    }
}
/* 定时器6中断服务函数 */
void TIM6_IRQHandler(void){
    HAL_TIM_IRQHandler(&g_timx_handle);
}

/* 定时器溢出中断中断回调函数 */
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
    if (htim->Instance == TIM6){
        LED0_TOGGLE();
    }
}
int main(void){
    HAL_Init();                                 /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9);         /* 设置时钟,72M */
    delay_init(72);                             /* 初始化延时函数 */
    led_init();                                 /* 初始化LED */
    btim_timx_int_init(5000 - 1, 7200 - 1);     /* 10Khz的计数频率，计数5K次为500ms */
    
    while(1){
        delay_ms(500);
    }
}
````





### 标准库

#### **常用函数**

````c
void RCC_APB1PeriphClockCmd(uint32_t RCC_APB1Periph, FunctionalState NewState);   //使用APB1使能Timer
````

````c
// 初始化
void TIM_TimeBaseInit(TIM_TypeDef* TIMx, TIM_TimeBaseInitTypeDef* TIM_TimeBaseInitStruct);  //初始化时基单元
void TIM_TimeBaseStructInit(TIM_TimeBaseInitTypeDef* TIM_TimeBaseInitStruct); //配置时基单元为默认配置 
void TIM_Cmd(TIM_TypeDef* TIMx, FunctionalState NewState);                    //使能计数器 
void TIM_ITConfig(TIM_TypeDef* TIMx, uint16_t TIM_IT, FunctionalState NewState); //使能中断输出信号 

//下面6个为定时器时钟选择信号，通用定时器以上才拥有
void TIM_InternalClockConfig(TIM_TypeDef* TIMx);  //选择内部时钟
void TIM_ITRxExternalClockConfig(TIM_TypeDef* TIMx, uint16_t TIM_InputTriggerSource);  //选择ITR其他定时器的时钟
void TIM_TIxExternalClockConfig(TIM_TypeDef* TIMx, uint16_t TIM_TIxExternalCLKSource,  //选择TIX捕获通道时钟
                                uint16_t TIM_ICPolarity, uint16_t ICFilter);
void TIM_ETRClockMode1Config(TIM_TypeDef* TIMx, uint16_t TIM_ExtTRGPrescaler, uint16_t TIM_ExtTRGPolarity,
                             uint16_t ExtTRGFilter);  //选择ETR外部时钟模式1输入的时钟
void TIM_ETRClockMode2Config(TIM_TypeDef* TIMx, uint16_t TIM_ExtTRGPrescaler, 
                             uint16_t TIM_ExtTRGPolarity, uint16_t ExtTRGFilter);  //选择ETR外部时钟模式2输入的时钟
void TIM_ETRConfig(TIM_TypeDef* TIMx, uint16_t TIM_ExtTRGPrescaler, uint16_t TIM_ExtTRGPolarity,
                   uint16_t ExtTRGFilter); // 单独配置ETR时钟的相关配置


//下面几个函数为单独配置某一参数（避免了为了修改某一参数而重新初始化）
void TIM_PrescalerConfig(TIM_TypeDef* TIMx, uint16_t Prescaler, uint16_t TIM_PSCReloadMode);  //单独配置预分频值的
void TIM_CounterModeConfig(TIM_TypeDef* TIMx, uint16_t TIM_CounterMode); //改变计数器的计数模式 
void TIM_ARRPreloadConfig(TIM_TypeDef* TIMx, FunctionalState NewState); //自动重装器预装功能配置 
void TIM_SetCounter(TIM_TypeDef* TIMx, uint16_t Counter);       //给计数器写入值 
void TIM_SetAutoreload(TIM_TypeDef* TIMx, uint16_t Autoreload); //给自动重装器写入值 

//下面两个函数获取计数器和预分频值
uint16_t TIM_GetCounter(TIM_TypeDef* TIMx);  //获取当前计数器的值
uint16_t TIM_GetPrescaler(TIM_TypeDef* TIMx); // 获取当前预分频的值

//下面4个为获取标志位和清除标志位的函数
FlagStatus TIM_GetFlagStatus(TIM_TypeDef* TIMx, uint16_t TIM_FLAG);
void TIM_ClearFlag(TIM_TypeDef* TIMx, uint16_t TIM_FLAG);
ITStatus TIM_GetITStatus(TIM_TypeDef* TIMx, uint16_t TIM_IT);
void TIM_ClearITPendingBit(TIM_TypeDef* TIMx, uint16_t TIM_IT);
````

**时基单元结构体**

````c
void TIM_TimeBaseInit(TIM_TypeDef* TIMx, TIM_TimeBaseInitTypeDef* TIM_TimeBaseInitStruct);//定时器参数初始化
typedef struct
{
  uint16_t TIM_CounterMode;      //计数模式  
  uint16_t TIM_Prescaler;        //预分频系数的设置  0x0000 and 0xFFFF；如分频为2，则来两次脉冲才计数1次
  uint16_t TIM_Period;           //自动装载值  0x0000 and 0xFFFF
  uint16_t TIM_ClockDivision;    //输入捕获会用到,也是分频，但不是对时基单元分频，滤波用到
  uint8_t TIM_RepetitionCounter; //重复计数器，高级定时器会用到;直接给0
} TIM_TimeBaseInitTypeDef; 
````

````c
// TIM_CounterMode
#define TIM_CounterMode_Up                 ((uint16_t)0x0000)   // 向上计数
#define TIM_CounterMode_Down               ((uint16_t)0x0010)   // 向下计数
#define TIM_CounterMode_CenterAligned1     ((uint16_t)0x0020)   // 中间计数
#define TIM_CounterMode_CenterAligned2     ((uint16_t)0x0040)
#define TIM_CounterMode_CenterAligned3     ((uint16_t)0x0060)
//TIM_ClockDivision 输入捕获会用到,也是分频，但不是对时基单元分频，滤波用到
#define TIM_CKD_DIV1                       ((uint16_t)0x0000)
#define TIM_CKD_DIV2                       ((uint16_t)0x0100)
#define TIM_CKD_DIV4                       ((uint16_t)0x0200)
````

**选择中断**

````c
/**
  *	  参数2
  *   This parameter can be any combination of the following values:
  *     @arg TIM_IT_Update: TIM update Interrupt source          // 更新中断，计数器每溢出一次更新一次
  *     @arg TIM_IT_CC1: TIM Capture Compare 1 Interrupt source  // 输入捕获中断，当CNT的值转运到CCR一次，产生一次
  *     @arg TIM_IT_CC2: TIM Capture Compare 2 Interrupt source
  *     @arg TIM_IT_CC3: TIM Capture Compare 3 Interrupt source
  *     @arg TIM_IT_CC4: TIM Capture Compare 4 Interrupt source
  *     @arg TIM_IT_COM: TIM Commutation Interrupt source
  *     @arg TIM_IT_Trigger: TIM Trigger Interrupt source
  *     @arg TIM_IT_Break: TIM Break Interrupt source
  */
void TIM_ITConfig(TIM_TypeDef* TIMx, uint16_t TIM_IT, FunctionalState NewState);
````

**选择时钟**

````c
void TIM_InternalClockConfig(TIM_TypeDef* TIMx);  //选择内部时钟
// 选择外部时钟模式2
/**
  * 参数2：设置外部时钟预分频
  * @param  TIM_ExtTRGPrescaler: The external Trigger Prescaler.
  *   This parameter can be one of the following values:
  *     @arg TIM_ExtTRGPSC_OFF: ETRP Prescaler OFF.           // 不分频
  *     @arg TIM_ExtTRGPSC_DIV2: ETRP frequency divided by 2.
  *     @arg TIM_ExtTRGPSC_DIV4: ETRP frequency divided by 4.
  *     @arg TIM_ExtTRGPSC_DIV8: ETRP frequency divided by 8.
  * 参数3：选择极性
  * @param  TIM_ExtTRGPolarity: The external Trigger Polarity.
  *   This parameter can be one of the following values:
  *     @arg TIM_ExtTRGPolarity_Inverted: active low or falling edge active.  极性反转
  *     @arg TIM_ExtTRGPolarity_NonInverted: active high or rising edge active. 极性不反转
  * 参数4：外部时钟滤波
  * @param  ExtTRGFilter: External Trigger Filter.
  *   This parameter must be a value between 0x00 and 0x0F
  * @retval None
  */
void TIM_ETRClockMode2Config(TIM_TypeDef* TIMx, uint16_t TIM_ExtTRGPrescaler, 
                             uint16_t TIM_ExtTRGPolarity, uint16_t ExtTRGFilter)
````



**其他函数**

````c
void TIM_DeInit(TIM_TypeDef* TIMx);  //恢复缺省配置

//定时器输出比较模块初始化，注意不同的通道对应不同的GPIO口（将对应定时器产生的PWM波形传到选择的GPIO口）
void TIM_OC1Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);
void TIM_OC2Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);
void TIM_OC3Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);
void TIM_OC4Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);

void TIM_ICInit(TIM_TypeDef* TIMx, TIM_ICInitTypeDef* TIM_ICInitStruct);
void TIM_PWMIConfig(TIM_TypeDef* TIMx, TIM_ICInitTypeDef* TIM_ICInitStruct);
void TIM_BDTRConfig(TIM_TypeDef* TIMx, TIM_BDTRInitTypeDef *TIM_BDTRInitStruct);
void TIM_OCStructInit(TIM_OCInitTypeDef* TIM_OCInitStruct);
void TIM_ICStructInit(TIM_ICInitTypeDef* TIM_ICInitStruct);
void TIM_BDTRStructInit(TIM_BDTRInitTypeDef* TIM_BDTRInitStruct);

void TIM_CtrlPWMOutputs(TIM_TypeDef* TIMx, FunctionalState NewState);

void TIM_GenerateEvent(TIM_TypeDef* TIMx, uint16_t TIM_EventSource);
void TIM_DMAConfig(TIM_TypeDef* TIMx, uint16_t TIM_DMABase, uint16_t TIM_DMABurstLength);
void TIM_DMACmd(TIM_TypeDef* TIMx, uint16_t TIM_DMASource, FunctionalState NewState);
void TIM_SelectInputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_InputTriggerSource);

// 定时器编码器接口模式
void TIM_EncoderInterfaceConfig(TIM_TypeDef* TIMx, uint16_t TIM_EncoderMode,
                                uint16_t TIM_IC1Polarity, uint16_t TIM_IC2Polarity);

//配置强制输出模式，只输出高or低电平，用的不多
void TIM_ForcedOC1Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);
void TIM_ForcedOC2Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);
void TIM_ForcedOC3Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);
void TIM_ForcedOC4Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);

void TIM_SelectCOM(TIM_TypeDef* TIMx, FunctionalState NewState);
void TIM_SelectCCDMA(TIM_TypeDef* TIMx, FunctionalState NewState);
void TIM_CCPreloadControl(TIM_TypeDef* TIMx, FunctionalState NewState);

//配置CCR预装功能（影子寄存器），用的不多
void TIM_OC1PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);
void TIM_OC2PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);
void TIM_OC3PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);
void TIM_OC4PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);

//配置快速使能的，用的不多
void TIM_OC1FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);
void TIM_OC2FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);
void TIM_OC3FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);
void TIM_OC4FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);

//外部事件清除REF信号，用的不多
void TIM_ClearOC1Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);
void TIM_ClearOC2Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);
void TIM_ClearOC3Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);
void TIM_ClearOC4Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);

//单独设置输出比较的极性的（结构体初始化时也会设置极性，这里用的不多），带N的是高级定时器互补通道的配置
void TIM_OC1PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);
void TIM_OC1NPolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCNPolarity);
void TIM_OC2PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);
void TIM_OC2NPolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCNPolarity);
void TIM_OC3PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);
void TIM_OC3NPolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCNPolarity);
void TIM_OC4PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);

//输出使能，带N为高级定时器互补通道的配置
void TIM_CCxCmd(TIM_TypeDef* TIMx, uint16_t TIM_Channel, uint16_t TIM_CCx);
void TIM_CCxNCmd(TIM_TypeDef* TIMx, uint16_t TIM_Channel, uint16_t TIM_CCxN);

//单独更改输出比较模式的函数
void TIM_SelectOCxM(TIM_TypeDef* TIMx, uint16_t TIM_Channel, uint16_t TIM_OCMode);

void TIM_UpdateDisableConfig(TIM_TypeDef* TIMx, FunctionalState NewState);
void TIM_UpdateRequestConfig(TIM_TypeDef* TIMx, uint16_t TIM_UpdateSource);
void TIM_SelectHallSensor(TIM_TypeDef* TIMx, FunctionalState NewState);
void TIM_SelectOnePulseMode(TIM_TypeDef* TIMx, uint16_t TIM_OPMode);
void TIM_SelectOutputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_TRGOSource);
void TIM_SelectSlaveMode(TIM_TypeDef* TIMx, uint16_t TIM_SlaveMode);
void TIM_SelectMasterSlaveMode(TIM_TypeDef* TIMx, uint16_t TIM_MasterSlaveMode);
void TIM_SetAutoreload(TIM_TypeDef* TIMx, uint16_t Autoreload);

//单独更改CCR寄存器值的函数（更改占空比时用到，很重要）
void TIM_SetCompare1(TIM_TypeDef* TIMx, uint16_t Compare1);
void TIM_SetCompare2(TIM_TypeDef* TIMx, uint16_t Compare2);
void TIM_SetCompare3(TIM_TypeDef* TIMx, uint16_t Compare3);
void TIM_SetCompare4(TIM_TypeDef* TIMx, uint16_t Compare4);

//分别配置通道1，2，3，4的分频器
void TIM_SetIC1Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);
void TIM_SetIC2Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);
void TIM_SetIC3Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);
void TIM_SetIC4Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);
void TIM_SetClockDivision(TIM_TypeDef* TIMx, uint16_t TIM_CKD);

//读取CCR寄存器
uint16_t TIM_GetCapture1(TIM_TypeDef* TIMx);
uint16_t TIM_GetCapture2(TIM_TypeDef* TIMx);
uint16_t TIM_GetCapture3(TIM_TypeDef* TIMx);
uint16_t TIM_GetCapture4(TIM_TypeDef* TIMx);
````

#### 案例

步骤：

1. 使能定时器时钟。调用函数：RCC_APB1PeriphClockCmd()；
2. 选择定时器时钟源
3. 初始化定时器，配置ARR、PSC。调用函数：TIM_TimeBaseInit()；
4. 开启定时器中断，配置NVIC。调用函数：void TIM_ITConfig()；NVIC_Init()；
5. 使能定时器。调用函数：TIM_Cmd()；
6. 编写中断服务函数。调用函数：TIMx_IRQHandler()。

**案例1**：定时器内部中断，每1s使num++

````c
#include "stm32f10x.h"                  // Device header

void Timer_Init(void){
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2,ENABLE);                  // 使能TIM2时钟
	
	TIM_InternalClockConfig(TIM2);                                       // 选择内部时钟源
    
	TIM_TimeBaseInitTypeDef Tim_TimeBaseInitSturcture;                   
	Tim_TimeBaseInitSturcture.TIM_CounterMode = TIM_CounterMode_Up;      // 向上计数
    // 1s = 1hz = 72MHZ / 100000 / 7200
	Tim_TimeBaseInitSturcture.TIM_Period = 10000-1;                      // 计数10000次，即每10000次进入一次中断 
	Tim_TimeBaseInitSturcture.TIM_Prescaler = 7200-1;                    // 分频7200，即每振动7200次计时器加1
    Tim_TimeBaseInitSturcture.TIM_ClockDivision = TIM_CKD_DIV1 ; 
	Tim_TimeBaseInitSturcture.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM2,&Tim_TimeBaseInitSturcture);                   // 初始化Timer
	
	TIM_ITConfig(TIM2,TIM_IT_Update,ENABLE);                             // 定时器中断使能，触发方式更新触发

	
	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
	
	NVIC_InitTypeDef NVIC_InitStucture;
	NVIC_InitStucture.NVIC_IRQChannel = TIM2_IRQn;
	NVIC_InitStucture.NVIC_IRQChannelCmd = ENABLE;
	NVIC_InitStucture.NVIC_IRQChannelPreemptionPriority = 2;
	NVIC_InitStucture.NVIC_IRQChannelSubPriority = 1;
	NVIC_Init(&NVIC_InitStucture);
	
	TIM_Cmd(TIM2,ENABLE);                                                // 使能定时器计数器
}
void TIM2_IRQHandler(void){
	if(TIM_GetITStatus(TIM2,TIM_IT_Update) == SET){
		num++;
		TIM_ClearITPendingBit(TIM2,TIM_IT_Update);
	}
}
int main(void){	
	OLED_Init();
	Timer_Init();
	OLED_ShowString(1,1,"NUM:");
	OLED_ShowString(2,1,"count:");
	while(1){
		OLED_ShowNum(1, 5, num, 4);
		OLED_ShowNum(2, 7, TIM_GetCounter(TIM2), 4);
	}
}
````



**案例2**：使用外部时钟，这里使用红外对射传感器模拟时钟

![6-2 定时器外部时钟](STM32卷一.assets/6-2 定时器外部时钟.jpg)

````c
#include "stm32f10x.h"                  // Device header

void Timer_Init(void){
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2,ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA,ENABLE);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	
	GPIO_Init(GPIOA,&GPIO_InitStructure);
	
	//TIM_InternalClockConfig(TIM2);
    // 使用外部时钟，不分频，极性不反转，没有滤波
	TIM_ETRClockMode2Config(TIM2, TIM_ExtTRGPSC_OFF, TIM_ExtTRGPolarity_NonInverted,0x0F);

	TIM_TimeBaseInitTypeDef Tim_TimeBaseInitSturcture;
	Tim_TimeBaseInitSturcture.TIM_ClockDivision = TIM_CKD_DIV1 ;
	Tim_TimeBaseInitSturcture.TIM_CounterMode = TIM_CounterMode_Up;
	Tim_TimeBaseInitSturcture.TIM_Period = 10-1;                   // 计数10次进入一次中断
	Tim_TimeBaseInitSturcture.TIM_Prescaler = 1-1;                 // 不分频
	Tim_TimeBaseInitSturcture.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM2,&Tim_TimeBaseInitSturcture);
	
	TIM_ITConfig(TIM2,TIM_IT_Update,ENABLE);

	
	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
	
	NVIC_InitTypeDef NVIC_InitStucture;
	NVIC_InitStucture.NVIC_IRQChannel = TIM2_IRQn;
	NVIC_InitStucture.NVIC_IRQChannelCmd = ENABLE;
	NVIC_InitStucture.NVIC_IRQChannelPreemptionPriority = 2;
	NVIC_InitStucture.NVIC_IRQChannelSubPriority = 1;
	NVIC_Init(&NVIC_InitStucture);
	
	TIM_Cmd(TIM2,ENABLE);
}
// 其他函数与案例1一致
````



## 通用定时器

* 16位递增、递减、中心对齐计数器（计数值：0~65535）~
* 16位预分频器（分频系数：1~65536）
* 可用于触发DAC、ADC
* 在更新事件、触发事件、输入捕获、输出比较时，会产生中断/DMA请求
* 4个独立通道，可用于：输入捕获、输出比较、输出PWM、单脉冲模式
* 使用外部信号控制定时器且可实现多个定时器互连的同步电路
* 支持编码器和霍尔传感器电路等

### 输出比较

#### **简介**

* OC（Output Compare）输出比较

* 输出比较可以通过比较CNT与CCR寄存器值的关系，来对输出电平进行置1、置0或翻转的操作，用于输出一定频率和占空比的PWM波形

* 每个高级定时器和通用定时器都拥有4个输出比较通道

* 高级定时器的前3个通道额外拥有死区生成和互补输出的功能

* 在更新事件、触发事件、输入捕获、输出比较时，会产生中断/DMA请求

  

#### PWM简介 

* PWM（Pulse Width Modulation）脉冲宽度调制
* 在具有惯性的系统中，可以通过对一系列脉冲的宽度进行调制，来等效地获得所需要的模拟参量，常应用于电机控速等领域
* PWM参数：
  * $频率 = 1 / T_S    $  
  * $占空比 = T_ON / T_S$      
  * $分辨率 = 占空比变化步距$

​	![1688613340712](STM32卷一.assets/1688613340712.png)



#### 输出比较通道

**通用**

![image-20230706113015647](STM32卷一.assets/image-20230706113015647.png)

经过输出模式控制器输出ref，CC1P极性控制，为0时：输出ref的电平，为1时：输出ref的相反电平



**高级**

![image-20230706113905082](STM32卷一.assets/image-20230706113905082.png)

高级比通用多了死区生成：作用OC1导通时OC1N延迟导通，OC1N导通时OC1延时导通

#### 输出比较模式

|     **模式**     |                           **描述**                           |
| :--------------: | :----------------------------------------------------------: |
|       冻结       |                  CNT=CCR时，REF保持为原状态                  |
| 匹配时置有效电平 |                  CNT=CCR时，REF置有效电平1                   |
| 匹配时置无效电平 |                  CNT=CCR时，REF置无效电平0                   |
|  匹配时电平翻转  |                    CNT=CCR时，REF电平翻转                    |
|  强制为无效电平  |               CNT与CCR无效，REF强制为无效电平                |
|  强制为有效电平  |               CNT与CCR无效，REF强制为有效电平                |
|     PWM模式1     | 向上计数：CNT<CCR时，REF置有效电平，CNT≥CCR时，REF置无效电平  向下计数：CNT>CCR时，REF置无效电平，CNT≤CCR时，REF置有效电平 |
|     PWM模式2     | 向上计数：CNT<CCR时，REF置无效电平，CNT≥CCR时，REF置有效电平  向下计数：CNT>CCR时，REF置有效电平，CNT≤CCR时，REF置无效电平 |

````c
#define TIM_OCMode_Timing                  ((uint16_t)0x0000)    //冻结 
#define TIM_OCMode_Active                  ((uint16_t)0x0010)    //匹配时置有效电平
#define TIM_OCMode_Inactive                ((uint16_t)0x0020)    //匹配时置无效电平
#define TIM_OCMode_Toggle                  ((uint16_t)0x0030)    //匹配时电平翻转
#define TIM_OCMode_PWM1                    ((uint16_t)0x0060)    //PWM模式1
#define TIM_OCMode_PWM2                    ((uint16_t)0x0070)    //PWM模式2
````

#### PWM基本结构

![1688614643345](STM32卷一.assets/1688614643345.png)

**参数计算**

* PWM频率： Freq = CK_PSC / (PSC + 1) / (ARR + 1)
* PWM占空比： Duty = CCR / (ARR + 1)
* PWM分辨率： Reso = 1 / (ARR + 1)

标准库

* 通过`TIM_TimeBaseInitTypeDef.TIM_Prescaler` 设置PSC
* 通过`TIM_TimeBaseInitTypeDef.TIM_Period` 设置ARR
* 通过`TIM_OCInitTypeDef.TIM_Pulse` 设置CCR

HAL库

* 通过`TIM_HandleTypeDef.Init.Prescale` 设置PSC
* 通过`TIM_HandleTypeDe.Init.Period` 设置ARR
* 通过`TIM_OC_InitTypeDef.Pulse` 设置CCR

#### HAL库

##### **配置步骤**

1. 配置定时器基础工作参数：HAL_TIM_PWM_Init()
2. 定时器PWM输出MSP初始化：HAL_TIM_PWM_MspInit()   配置NVIC、CLOCK、GPIO等
3. 配置PWM模式/比较值等：HAL_TIM_PWM_ConfigChannel()
4. 使能输出并启动计数器：HAL_TIM_PWM_Start()
5. 修改比较值控制占空比(可选)：__HAL_TIM_SET_COMPARE()
6. 使能通道预装载(可选)：__HAL_TIM_ENABLE_OCxPRELOAD()

|             函数              |    主要寄存器     |            主要功能             |
| :---------------------------: | :---------------: | :-----------------------------: |
|      HAL_TIM_PWM_Init()       |   CR1、ARR、PSC   |      初始化定时器基础参数       |
|     HAL_TIM_PWM_MspInit()     |        无         | 存放NVIC、CLOCK、GPIO初始化代码 |
|  HAL_TIM_PWM_ConfigChannel()  | CCMRx、CCRx、CCER | 配置PWM模式、比较值、输出极性等 |
|      HAL_TIM_PWM_Start()      |     CCER、CR1     |    使能输出比较并启动计数器     |
|    __HAL_TIM_SET_COMPARE()    |       CCRx        |           修改比较值            |
| __HAL_TIM_ENABLE_OCxPRELOAD() |       CCER        |         使能通道预装载          |

````c
HAL_StatusTypeDef HAL_TIM_PWM_Init(TIM_HandleTypeDef *htim);     // 和基本定时器的HAL_TIM_Base_Init()一样
````

HAL_TIM_OC_Init() 、 HAL_TIM_OC_ConfigChannel()  、  HAL_TIM_OC_Start()  

**输出比较结构体**

````c
typedef struct { 
   uint32_t OCMode; 	    /* 输出比较模式选择 */
   uint32_t Pulse; 	        /* 设置CCR */
   uint32_t OCPolarity;     /* 设置输出比较极性 */
   uint32_t OCNPolarity;    /* 设置互补输出比较极性 */
   uint32_t OCFastMode;     /* 使能或失能输出比较快速模式 */
   uint32_t OCIdleState;    /* 空闲状态下OC1输出 */
   uint32_t OCNIdleState;   /* 空闲状态下OC1N输出 */ 
} TIM_OC_InitTypeDef;
````

````c
//输出比较模式选择
#define TIM_OCMODE_TIMING                   0x00000000U
#define TIM_OCMODE_ACTIVE                   TIM_CCMR1_OC1M_0  
#define TIM_OCMODE_INACTIVE                 TIM_CCMR1_OC1M_1 
#define TIM_OCMODE_TOGGLE                   (TIM_CCMR1_OC1M_1 | TIM_CCMR1_OC1M_0)  
#define TIM_OCMODE_PWM1                     (TIM_CCMR1_OC1M_2 | TIM_CCMR1_OC1M_1) 
#define TIM_OCMODE_PWM2                     (TIM_CCMR1_OC1M_2 | TIM_CCMR1_OC1M_1 | TIM_CCMR1_OC1M_0)
#define TIM_OCMODE_FORCED_ACTIVE            (TIM_CCMR1_OC1M_2 | TIM_CCMR1_OC1M_0)
#define TIM_OCMODE_FORCED_INACTIVE          TIM_CCMR1_OC1M_2     

//设置输出比较极性
#define TIM_OCPOLARITY_HIGH                0x00000000U
#define TIM_OCPOLARITY_LOW                 TIM_CCER_CC1P
````



##### 重映射

stm32f1xx_hal_gpio_ex.h内部有众多AFIO重映射宏定义

````c
__HAL_RCC_AFIO_CLK_ENABLE();

**
  * @brief Enable the remapping of TIM3 alternate function channels 1 to 4
  * @note  PARTIAL: Partial remap (CH1/PB4, CH2/PB5, CH3/PB0, CH4/PB1)
  */
__HAL_AFIO_REMAP_TIM3_PARTIAL() 
````

##### 输出比较模式

![image-20230803212626025](STM32卷一.assets/image-20230803212626025.png)

翻转：PWM波由ARR的值决定，占空比固定位50%，而CCR控制的是相位。相位：产生上升沿的位置

函数

|             函数              |    主要寄存器     |               主要功能               |
| :---------------------------: | :---------------: | :----------------------------------: |
|       HAL_TIM_OC_Init()       |   CR1、ARR、PSC   |         初始化定时器基础参数         |
|      HAL_TIM_OC_MspInit       |        无         |   存放NVIC、CLOCK、GPIO初始化代码    |
|  HAL_TIM_OC_ConfigChannel()   | CCMRx、CCRx、CCER | 设置输出比较模式、比较值、输出极性等 |
| __HAL_TIM_ENABLE_OCxPRELOAD() |       CCMRx       |            使能通道预装载            |
|      HAL_TIM_OC_Start()       |  CR1、CCER、BDTR  |   使能输出比较、主输出、启动计数器   |
|    __HAL_TIM_SET_COMPARE()    |       CCRx        |       修改捕获/比较寄存器的值        |



案例：通过定时器8通道1/2/3/4输出相位分别为25%、50%、75%、100%的PWM，注意：PWM固定为50%，只是相位发生了变化

````c
TIM_HandleTypeDef g_timx_comp_pwm_handle;       /* 定时器x句柄 */

/* 高级定时器 输出比较模式 初始化函数 */
void atim_timx_comp_pwm_init(uint16_t arr, uint16_t psc){
    TIM_OC_InitTypeDef timx_oc_comp_pwm = {0};
    
    g_timx_comp_pwm_handle.Instance = TIM8;                       /* 定时器8 */
    g_timx_comp_pwm_handle.Init.Prescaler = psc  ;                /* 定时器分频 */
    g_timx_comp_pwm_handle.Init.CounterMode = TIM_COUNTERMODE_UP; /* 递增计数模式 */
    g_timx_comp_pwm_handle.Init.Period = arr;                     /* 自动重装载值 */
    HAL_TIM_OC_Init(&g_timx_comp_pwm_handle);                     /* 输出比较模式初始化 */

    timx_oc_comp_pwm.OCMode = TIM_OCMODE_TOGGLE;
    timx_oc_comp_pwm.OCPolarity = TIM_OCPOLARITY_HIGH;
    HAL_TIM_OC_ConfigChannel(&g_timx_comp_pwm_handle, &timx_oc_comp_pwm, TIM_CHANNEL_1);
    HAL_TIM_OC_ConfigChannel(&g_timx_comp_pwm_handle, &timx_oc_comp_pwm, TIM_CHANNEL_2);
    HAL_TIM_OC_ConfigChannel(&g_timx_comp_pwm_handle, &timx_oc_comp_pwm, TIM_CHANNEL_3);
    HAL_TIM_OC_ConfigChannel(&g_timx_comp_pwm_handle, &timx_oc_comp_pwm, TIM_CHANNEL_4);
    
    __HAL_TIM_ENABLE_OCxPRELOAD(&g_timx_comp_pwm_handle, TIM_CHANNEL_1);
    __HAL_TIM_ENABLE_OCxPRELOAD(&g_timx_comp_pwm_handle, TIM_CHANNEL_2);
    __HAL_TIM_ENABLE_OCxPRELOAD(&g_timx_comp_pwm_handle, TIM_CHANNEL_3);
    __HAL_TIM_ENABLE_OCxPRELOAD(&g_timx_comp_pwm_handle, TIM_CHANNEL_4);
    
    HAL_TIM_OC_Start(&g_timx_comp_pwm_handle, TIM_CHANNEL_1);
    HAL_TIM_OC_Start(&g_timx_comp_pwm_handle, TIM_CHANNEL_2);
    HAL_TIM_OC_Start(&g_timx_comp_pwm_handle, TIM_CHANNEL_3);
    HAL_TIM_OC_Start(&g_timx_comp_pwm_handle, TIM_CHANNEL_4);
}
/* 定时器 输出比较 MSP初始化函数 */
void HAL_TIM_OC_MspInit(TIM_HandleTypeDef *htim)
{
    if (htim->Instance == TIM8)
    {
        GPIO_InitTypeDef gpio_init_struct;

        __HAL_RCC_TIM8_CLK_ENABLE();
        __HAL_RCC_GPIOC_CLK_ENABLE();

        gpio_init_struct.Pin = GPIO_PIN_6;
        gpio_init_struct.Mode = GPIO_MODE_AF_PP;
        gpio_init_struct.Pull = GPIO_NOPULL;
        gpio_init_struct.Speed = GPIO_SPEED_FREQ_HIGH;
        HAL_GPIO_Init(GPIOC, &gpio_init_struct);

        gpio_init_struct.Pin = GPIO_PIN_7;
        HAL_GPIO_Init(GPIOC, &gpio_init_struct);

        gpio_init_struct.Pin = GPIO_PIN_8;
        HAL_GPIO_Init(GPIOC, &gpio_init_struct);

        gpio_init_struct.Pin = GPIO_PIN_9;
        HAL_GPIO_Init(GPIOC, &gpio_init_struct);
    }
}
int main(void)
{
    uint8_t t = 0;

    HAL_Init();                         /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9); /* 设置时钟, 72Mhz */
    delay_init(72);                     /* 延时初始化 */
    usart_init(115200);                 /* 串口初始化为115200 */
    led_init();                         /* 初始化LED */
    atim_timx_comp_pwm_init(1000 - 1, 72 - 1);
    
    __HAL_TIM_SET_COMPARE(&g_timx_comp_pwm_handle, TIM_CHANNEL_1, 250 - 1);        // 25%相位
    __HAL_TIM_SET_COMPARE(&g_timx_comp_pwm_handle, TIM_CHANNEL_2, 500 - 1);
    __HAL_TIM_SET_COMPARE(&g_timx_comp_pwm_handle, TIM_CHANNEL_3, 750 - 1);
    __HAL_TIM_SET_COMPARE(&g_timx_comp_pwm_handle, TIM_CHANNEL_4, 1000 - 1);

    while (1)
    {
        delay_ms(10);
        t++;

        if (t >= 20)
        {
            LED0_TOGGLE(); /* LED0(RED)闪烁 */
            t = 0;
        }
    }
}
````



##### **案例**

通过定时器输出的PWM控制LED0，实现类似手机呼吸灯的效果，配置输出比较模式为：PWM模式1，通道输出极性为：低电平有效

````c
TIM_HandleTypeDef TIM_Handle;
TIM_OC_InitTypeDef TIM_OC_InitStructure;
void TIM_PWM_Init(void){
    TIM_Handle.Instance = TIM3;
    TIM_Handle.Init.CounterMode = TIM_COUNTERMODE_UP;     // 向上计数
    TIM_Handle.Init.Period = 499;                         // 自动重置ARR
    TIM_Handle.Init.Prescaler = 71;                       // 预分频
    
    HAL_TIM_PWM_Init(&TIM_Handle);                        // 初始化，和HAL_TIM_Base_Init()一样
    
    TIM_OC_InitStructure.OCMode = TIM_OCMODE_PWM1;        // 模式1
    TIM_OC_InitStructure.OCPolarity = TIM_OCPOLARITY_LOW; // 极性，低电平有效
    TIM_OC_InitStructure.Pulse = 300;                     // CCR

    HAL_TIM_PWM_ConfigChannel(&TIM_Handle,&TIM_OC_InitStructure,TIM_CHANNEL_2);  // 初始化OC
    
    HAL_TIM_PWM_Start(&TIM_Handle,TIM_CHANNEL_2);         // 使能定时器
}
void HAL_TIM_PWM_MspInit(TIM_HandleTypeDef *htim){
    if(htim->Instance == TIM3){
        __HAL_RCC_GPIOB_CLK_ENABLE();
        __HAL_RCC_TIM3_CLK_ENABLE();
        GPIO_InitTypeDef GPIO_InitStructure;
        GPIO_InitStructure.Mode = GPIO_MODE_AF_PP;
        GPIO_InitStructure.Pin = GPIO_PIN_5;
        GPIO_InitStructure.Pull =  GPIO_PULLUP;
        GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH 
        HAL_GPIO_Init(GPIOB,&GPIO_InitStructure);
        
//        HAL_NVIC_SetPriorityGrouping(NVIC_PRIORITYGROUP_2);   
//        HAL_NVIC_SetPriority(TIM3_IRQn,2,2);
//        HAL_NVIC_EnableIRQ(TIM3_IRQn);
        
        __HAL_RCC_AFIO_CLK_ENABLE();                  // 开启AFIO
        __HAL_AFIO_REMAP_TIM3_PARTIAL();              // AFIO复用，TIM3的CH2复用到PB5
    }
}
int main(void){
    HAL_Init();                                 /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9);         /* 设置时钟,72M */
    delay_init(72);                             /* 初始化延时函数 */
    UART_Init();
    LED_init();   
    TIM_PWM_Init();
    int cnt = 0;
    while(1){
        if(cnt > 499) cnt = 0;
        cnt++;
        delay_ms(10);
        __HAL_TIM_SET_COMPARE(&TIM_Handle,TIM_CHANNEL_2,cnt);    
    }
}
````



#### 标准库

##### 常用函数

````c
void TIM_DeInit(TIM_TypeDef* TIMx);  //恢复缺省配置

//定时器输出比较模块初始化，注意不同的通道对应不同的GPIO口（将对应定时器产生的PWM波形传到选择的GPIO口）
void TIM_OC1Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);
void TIM_OC2Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);
void TIM_OC3Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);
void TIM_OC4Init(TIM_TypeDef* TIMx, TIM_OCInitTypeDef* TIM_OCInitStruct);

//给TIM_OCInitTypeDef结构体赋初始值
void TIM_OCStructInit(TIM_OCInitTypeDef* TIM_OCInitStruct);

//配置强制输出模式，只输出高or低电平，用的不多
void TIM_ForcedOC1Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);
void TIM_ForcedOC2Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);
void TIM_ForcedOC3Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);
void TIM_ForcedOC4Config(TIM_TypeDef* TIMx, uint16_t TIM_ForcedAction);

//配置CCR预装功能（影子寄存器），用的不多
void TIM_OC1PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);
void TIM_OC2PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);
void TIM_OC3PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);
void TIM_OC4PreloadConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPreload);

//配置快速使能的，用的不多
void TIM_OC1FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);
void TIM_OC2FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);
void TIM_OC3FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);
void TIM_OC4FastConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCFast);

//外部事件清除REF信号，用的不多
void TIM_ClearOC1Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);
void TIM_ClearOC2Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);
void TIM_ClearOC3Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);
void TIM_ClearOC4Ref(TIM_TypeDef* TIMx, uint16_t TIM_OCClear);

//单独设置输出比较的极性的（结构体初始化时也会设置极性，这里用的不多），带N的是高级定时器互补通道的配置
void TIM_OC1PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);
void TIM_OC1NPolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCNPolarity);
void TIM_OC2PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);
void TIM_OC2NPolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCNPolarity);
void TIM_OC3PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);
void TIM_OC3NPolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCNPolarity);
void TIM_OC4PolarityConfig(TIM_TypeDef* TIMx, uint16_t TIM_OCPolarity);

//输出使能，带N为高级定时器互补通道的配置
void TIM_CCxCmd(TIM_TypeDef* TIMx, uint16_t TIM_Channel, uint16_t TIM_CCx);
void TIM_CCxNCmd(TIM_TypeDef* TIMx, uint16_t TIM_Channel, uint16_t TIM_CCxN);

//单独更改输出比较模式的函数
void TIM_SelectOCxM(TIM_TypeDef* TIMx, uint16_t TIM_Channel, uint16_t TIM_OCMode);

void TIM_UpdateDisableConfig(TIM_TypeDef* TIMx, FunctionalState NewState);
void TIM_UpdateRequestConfig(TIM_TypeDef* TIMx, uint16_t TIM_UpdateSource);
void TIM_SelectHallSensor(TIM_TypeDef* TIMx, FunctionalState NewState);
void TIM_SelectOnePulseMode(TIM_TypeDef* TIMx, uint16_t TIM_OPMode);
void TIM_SelectOutputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_TRGOSource);
void TIM_SelectSlaveMode(TIM_TypeDef* TIMx, uint16_t TIM_SlaveMode);
void TIM_SelectMasterSlaveMode(TIM_TypeDef* TIMx, uint16_t TIM_MasterSlaveMode);
void TIM_SetAutoreload(TIM_TypeDef* TIMx, uint16_t Autoreload);

//单独更改CCR寄存器值的函数（更改占空比时用到，很重要）
void TIM_SetCompare1(TIM_TypeDef* TIMx, uint16_t Compare1);    //控制的是TIMx的CH1
void TIM_SetCompare2(TIM_TypeDef* TIMx, uint16_t Compare2);    //控制的是TIMx的CH2
void TIM_SetCompare3(TIM_TypeDef* TIMx, uint16_t Compare3);
void TIM_SetCompare4(TIM_TypeDef* TIMx, uint16_t Compare4);

//仅高级定时器使用，使能主输出，否则PWM将不能正常输出
void TIM_CtrlPWMOutputs(TIM_TypeDef* TIMx, FunctionalState NewState);
````



**输出比较结构体**

````c
typedef struct{
  uint16_t TIM_OCMode;       //输出比较模式
  uint16_t TIM_OutputState;  //输出使能


  uint16_t TIM_Pulse;         // 设置CCR
  uint16_t TIM_OCPolarity;    // 极性选择

  uint16_t TIM_OutputNState;  /*!< Specifies the TIM complementary Output Compare state.
                                   This parameter can be a value of @ref TIM_Output_Compare_N_state
                                   @note This parameter is valid only for TIM1 and TIM8. */
  uint16_t TIM_OCNPolarity;   /*!< Specifies the complementary output polarity.
                                   This parameter can be a value of @ref TIM_Output_Compare_N_Polarity
                                   @note This parameter is valid only for TIM1 and TIM8. */

  uint16_t TIM_OCIdleState;   /*!< Specifies the TIM Output Compare pin state during Idle state.
                                   This parameter can be a value of @ref TIM_Output_Compare_Idle_State
                                   @note This parameter is valid only for TIM1 and TIM8. */

  uint16_t TIM_OCNIdleState;  /*!< Specifies the TIM Output Compare pin state during Idle state.
                                   This parameter can be a value of @ref TIM_Output_Compare_N_Idle_State
                                   @note This parameter is valid only for TIM1 and TIM8. */
} TIM_OCInitTypeDef;

````

TIM_OCPolarity极性选择：

````c
#define TIM_OCPolarity_High                ((uint16_t)0x0000)                       //ref直接输出
#define TIM_OCPolarity_Low                 ((uint16_t)0x0002)                       //极性反转，输出ref相反
#define IS_TIM_OC_POLARITY(POLARITY) (((POLARITY) == TIM_OCPolarity_High) || \
                                      ((POLARITY) == TIM_OCPolarity_Low))
````

TIM_OutputState

````c
#define TIM_OutputState_Disable            ((uint16_t)0x0000)
#define TIM_OutputState_Enable             ((uint16_t)0x0001)          //使能
````

##### 重映射

![1688619331914](STM32卷一.assets/1688619331914.png)
![1688620748737](STM32卷一.assets/1688620748737.png)

TIM2_CH1_ETR默认在PA0端口，他还可以重映射到PA15，这需要AFIO

````c
RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);         //使能AFIO
GPIO_PinRemapConfig(GPIO_PartialRemap1_TIM2, ENABLE);        //外设复用引脚
GPIO_PinRemapConfig(GPIO_Remap_SWJ_JTAGDisable, ENABLE);     //解除调试引脚，如果复用引脚不是调试引脚则不需要这行代码
````

##### PWM呼吸灯

````c
#include "stm32f10x.h"                  // Device header

void PWM_Init(void){
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
		
	//RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);   //引脚重映射
	//GPIO_PinRemapConfig(GPIO_PartialRemap1_TIM2, ENABLE);
	//GPIO_PinRemapConfig(GPIO_Remap_SWJ_JTAGDisable, ENABLE);
	
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP;           //必须使用复用开漏/推挽输出，使用复用推挽输出才能将控制权交给片上外设,PWM波形才能通过引脚输出
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;                 //TIM2的CH1只能用在PA0，当然也可以重映射
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	TIM_InternalClockConfig(TIM2);          // 使用内部定时器
	
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
	TIM_TimeBaseInitStructure.TIM_Period = 100 - 1;             //ARR
	TIM_TimeBaseInitStructure.TIM_Prescaler = 720 - 1;           //PSC
	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM2, &TIM_TimeBaseInitStructure);
	
	//输出比较初始化
	TIM_OCInitTypeDef TIM_OCInitStructure;  
	TIM_OCStructInit(&TIM_OCInitStructure);   //先对结构体初始化，以免发生小错误

	TIM_OCInitStructure.TIM_OCMode = TIM_OCMode_PWM1;               //使用PWM1
	TIM_OCInitStructure.TIM_OCPolarity = TIM_OCPolarity_High;       //ref不反转
	TIM_OCInitStructure.TIM_OutputState = TIM_OutputState_Enable;
	TIM_OCInitStructure.TIM_Pulse = 0;                             //CCR
	TIM_OC1Init(TIM2, &TIM_OCInitStructure);                       //使用1号通道，对应GPIO PA0
	
	TIM_Cmd(TIM2, ENABLE);
}
void PWM_SetCompare1(uint16_t pulse){
	TIM_SetCompare1(TIM2,pulse);
}
------------------------------------------------------------------------
uint8_t pulse;
int main(void)
{
	PWM_Init();
	while (1)
	{
		for(pulse = 0; pulse < 100;pulse++){
			PWM_SetCompare1(pulse);
			Delay_ms(10);
		}
		for(pulse = 0; pulse < 100;pulse++){
			PWM_SetCompare1(100-pulse);
			Delay_ms(10);
		}
	}
}
````



### 输入捕获

#### 简介

* IC（Input Capture）输入捕获
* 输入捕获模式下，当通道输入引脚出现指定电平跳变时，**当前CNT的值将被锁存到CCR中**，可用于测量PWM波形的频率、占空比、脉冲间隔、电平持续时间等参数（CCR有多个，CNT只有一个）
* 每个高级定时器和通用定时器都拥有4个输入捕获通道
* 可配置为PWMI模式，同时测量频率和占空比
* 可配合主从触发模式，实现硬件全自动测量

对于同一个定时器输入捕获和输出比较只能用一个，不能同时使用

工作原理：在输入捕获模式下，当捕获单元捕捉到外部信号的有效边沿(上升沿/下降 沿/双边沿)时，将计数器的当前值锁存到捕获/比较寄存器TIMx_CCR， 供用户读取。

例：每来一次上升沿CNT的值就会转运到CCR一次，同时产生一个更新事件，也可以产生一个中断



**频率测量**

![image-20230706160909319](STM32卷一.assets/image-20230706160909319.png)

* 测频法：在闸门时间T内，对上升/下降  沿计次，得到N，则频率$f_x=N / T$；适合测高频信号
  * 比如1s内，计次10次，就是10hz

* 测周法：两个上升沿内，以标准频率fc计次，得到N ，则频率$f_x=f_c / N$：适合测低频信号
  * 每来一个上升沿，取一下CNT的值，自动存在CCR中，CCR捕获到的值,就是计数值N，CNT的驱动时钟就是$f_c$。每次捕获计数值清零一次

* 中界频率：测频法与测周法误差相等的频率点$f_m=√(f_c / T)$





![1688631708030](STM32卷一.assets/1688631708030.png)

TIMx_CH1经过输入滤波器和边沿检测器输出TI1FP1到IC1的预分频器或输出TI1FP2到IC2的预分频器(交叉)





**详细图**

![image-20230706162411803](STM32卷一.assets/image-20230706162411803.png)

TI1FP1还会触发从模式，我们可以在从模式中触发一次CNT Reset操作，使计数器清零



#### **主从触发模式**

为了完成硬件自动化

![1688632140908](STM32卷一.assets/1688632140908.png)

* 主模式：可以将定时器内部的信号，映射到TRGO引脚，用于触发别的外设
  * ![1689747373662](STM32卷一.assets/1689747373662.png)

* 从模式：接收其他外设信号或自身外设的信号，用于控制自身定时器的运行，也就是被别的信号控制
  * 触发源选择：选择从模式的触发信号源
  * **例如**：想要让TI1FP1信号自动触发CNT清零，触发源选择TI1FP1,从模式选择执行Reset
  * ![1689747401114](STM32卷一.assets/1689747401114.png)
* 注意：要想使用主从触发模式只能用通道1和通道2，通道3和通道4无法作为触发源（如果使用通道34可以使用手动中断）

**HAL库**

````c
/** 开启从触发
*	参数1：TIM句柄
* 	参数2：从触发结构体
**/
HAL_StatusTypeDef HAL_TIM_SlaveConfigSynchro(TIM_HandleTypeDef *htim, TIM_SlaveConfigTypeDef *sSlaveConfig)
````

````c
typedef struct{
  uint32_t  SlaveMode;         // 选择从模式
  uint32_t  InputTrigger;      // 选择从模式的触发源 
  uint32_t  TriggerPolarity;   // 极性
  uint32_t  TriggerPrescaler;  //
  uint32_t  TriggerFilter;     // 滤波
} TIM_SlaveConfigTypeDef;
````

````c
void gtim_timx_cnt_chy_init(uint16_t psc){
    TIM_SlaveConfigTypeDef tim_salve_config = {0};
    TIM_HandleTypeDef g_timx_cnt_chy_handle; 
    
    g_timx_cnt_chy_handle.Instance = TIM2;
    g_timx_cnt_chy_handle.Init.Prescaler = psc;
    g_timx_cnt_chy_handle.Init.CounterMode = TIM_COUNTERMODE_UP;
    g_timx_cnt_chy_handle.Init.Period = 65535;
    HAL_TIM_IC_Init(&g_timx_cnt_chy_handle);
    
    tim_salve_config.SlaveMode = TIM_SLAVEMODE_EXTERNAL1;                 // 触发定时器通道1
    tim_salve_config.InputTrigger = TIM_TS_TI1F_ED;                       // 双边沿触发
    tim_salve_config.TriggerPolarity = TIM_TRIGGERPOLARITY_RISING;
    tim_salve_config.TriggerFilter = 0;
    
    HAL_TIM_SlaveConfigSynchro(&g_timx_cnt_chy_handle, &tim_salve_config);
    HAL_TIM_IC_Start(&g_timx_cnt_chy_handle, TIM_CHANNEL_1);
}
````





**标准库**

````c
void TIM_SelectOutputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_TRGOSource);         //选择主模式的触发源

void TIM_SelectInputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_InputTriggerSource);  //选择从模式的触发源
void TIM_SelectSlaveMode(TIM_TypeDef* TIMx, uint16_t TIM_SlaveMode);              //选择从模式
````





#### 输入捕获基本结构

注意：获得的是一整个PWM周期，不是获得高电平周期；比如设置成上升沿触发，只是说在每一次上升沿触发一次CNT搬运，而不是说上升沿后开始计数

![image-20230706163617278](STM32卷一.assets/image-20230706163617278.png)

例：

1. GPIO得到信号，经过滤波器边沿检测极性选择，选择上升沿触发
2. TI1FP1信号分为两路
   1. 路径一：最终触发CCR捕获
   2. 路径二：作为从模式的触发源，触发CNT计数器清零

小图：

1. CCR1 = CNT由硬件自动完成
2. CNT = 0 由从模式触发

注意：清零操作，如上升沿清零之后，CNT++，直到下一个上升沿，CCR=CNT，最终CCR的值就是这两个上升沿之间CNT++的值

#### PWMI基本结构

![image-20230706164139034](STM32卷一.assets/image-20230706164139034.png)



使用两个通道捕获一个引脚，在上升沿清零CNT，通道1直连输入，通道2交叉输入

多了一个通道，通道1上升沿触发搬运，通道2下降沿触发搬运；CCR1记录**整个周期**的计数值，CCR2记录高电平周期的计数值；$占空比=CCR2/CCR1$







#### HAL库

##### **配置步骤**

1. 配置定时器基础工作参数：HAL_TIM_IC_Init()
2. 定时器输入捕获MSP初始化：HAL_TIM_IC_MspInit()   配置NVIC、CLOCK、GPIO等
3. 配置输入通道映射、捕获边沿等：HAL_TIM_IC_ConfigChannel()
4. 设置优先级，使能中断：HAL_NVIC_SetPriority()、 HAL_NVIC_EnableIRQ()
5. 使能定时器更新中断：__HAL_TIM_ENABLE_IT()
6. 使能捕获、捕获中断及计数器：HAL_TIM_IC_Start_IT()
7. 编写中断服务函数：TIMx_IRQHandler()等  --> HAL_TIM_IRQHandler()
8. 编写更新中断和捕获回调函数：HAL_TIM_PeriodElapsedCallback()、 HAL_TIM_IC_CaptureCallback()

|              函数               |   主要寄存器    |               主要功能               |
| :-----------------------------: | :-------------: | :----------------------------------: |
|        HAL_TIM_IC_Init()        |  CR1、ARR、PSC  |         初始化定时器基础参数         |
|      HAL_TIM_IC_MspInit()       |       无        |   存放NVIC、CLOCK、GPIO初始化代码    |
|   HAL_TIM_IC_ConfigChannel()    |   CCMRx、CCER   | 配置通道映射、捕获边沿、分频、滤波等 |
|      __HAL_TIM_ENABLE_IT()      |      DIER       |            使能更新中断等            |
|      HAL_TIM_IC_Start_IT()      | CCER、DIER、CR1 |  使能输入捕获、捕获中断并启动计数器  |
|      HAL_TIM_IRQHandler()       |       SR        | 定时器中断处理公用函数，处理各种中断 |
| HAL_TIM_PeriodElapsedCallback() |       无        | 定时器更新中断回调函数，由用户重定义 |
|  HAL_TIM_IC_CaptureCallback()   |       无        | 定时器输入捕获回调函数，由用户重定义 |

**输入捕获结构体**

````c
typedef struct{ 
    uint32_t ICPolarity;    /* 输入捕获触发方式选择，比如上升、下降沿捕获 */ 
    uint32_t ICSelection;   /* 输入捕获选择，用于设置映射关系 直连、交叉 */ 
    uint32_t ICPrescaler;   /* 输入捕获分频系数，即捕获几次上升下/降沿生效一个 */ 
    uint32_t ICFilter;      /* 输入捕获滤波器设置 */ 
} TIM_IC_InitTypeDef;
````

````c
#define  TIM_ICPOLARITY_RISING             TIM_INPUTCHANNELPOLARITY_RISING      
#define  TIM_ICPOLARITY_FALLING            TIM_INPUTCHANNELPOLARITY_FALLING     
#define  TIM_ICPOLARITY_BOTHEDGE           TIM_INPUTCHANNELPOLARITY_BOTHEDGE   

#define TIM_ICPSC_DIV1                     0x00000000U                          
#define TIM_ICPSC_DIV2                     TIM_CCMR1_IC1PSC_0                   
#define TIM_ICPSC_DIV4                     TIM_CCMR1_IC1PSC_1                   
#define TIM_ICPSC_DIV8                     TIM_CCMR1_IC1PSC 

#define TIM_ICSELECTION_DIRECTTI           TIM_CCMR1_CC1S_0    // 直接链接
#define TIM_ICSELECTION_INDIRECTTI         TIM_CCMR1_CC1S_1                                                         
#define TIM_ICSELECTION_TRC                TIM_CCMR1_CC1S   
````



##### 案例

**案例1：**通过定时器5通道1来捕获按键高电平脉宽时间，通过串口打印出来，配置输入捕获方式：上升沿捕获、输入通道1映射在TI1上、不分频、不滤波

````c
TIM_HandleTypeDef g_timx_cap_chy_handle;     /* 定时器x句柄 */

/* 通用定时器通道y 输入捕获 初始化函数 */
void gtim_timx_cap_chy_init(uint16_t arr, uint16_t psc){
    TIM_IC_InitTypeDef timx_ic_cap_chy = {0};

    g_timx_cap_chy_handle.Instance = TIM5;                              /* 定时器5 */
    g_timx_cap_chy_handle.Init.Prescaler = psc;                         /* 定时器分频 */
    g_timx_cap_chy_handle.Init.CounterMode = TIM_COUNTERMODE_UP;        /* 递增计数模式 */
    g_timx_cap_chy_handle.Init.Period = arr;                            /* 自动重装载值 */
    HAL_TIM_IC_Init(&g_timx_cap_chy_handle);

    timx_ic_cap_chy.ICPolarity = TIM_ICPOLARITY_RISING;                 /* 上升沿捕获 */
    timx_ic_cap_chy.ICSelection = TIM_ICSELECTION_DIRECTTI;             /* 映射到TI1上 */
    timx_ic_cap_chy.ICPrescaler = TIM_ICPSC_DIV1;                       /* 配置输入分频，不分频 */
    timx_ic_cap_chy.ICFilter = 0;                                       /* 配置输入滤波器，不滤波 */
    HAL_TIM_IC_ConfigChannel(&g_timx_cap_chy_handle, &timx_ic_cap_chy, TIM_CHANNEL_1);  /* 配置TIM5通道1 */

    __HAL_TIM_ENABLE_IT(&g_timx_cap_chy_handle, TIM_IT_UPDATE);         /* 使能更新中断 */
    //__HAL_TIM_ENABLE_IT(&TIM_Handle,TIM_IT_CC1);              // 使能捕获中断
    
    
    /* 使能捕获中断，其实就是__HAL_TIM_ENABLE_IT(&TIM_Handle,TIM_IT_CC1); */
    HAL_TIM_IC_Start_IT(&g_timx_cap_chy_handle, TIM_CHANNEL_1); 
}

/* 定时器 输入捕获 MSP初始化函数 */
void HAL_TIM_IC_MspInit(TIM_HandleTypeDef *htim){
    if (htim->Instance == TIM5)                             /*输入通道捕获*/
    {
        GPIO_InitTypeDef gpio_init_struct;
        __HAL_RCC_TIM5_CLK_ENABLE();                        /* 使能TIM5时钟 */
        __HAL_RCC_GPIOA_CLK_ENABLE();                       /* 开启捕获IO的时钟 */

        gpio_init_struct.Pin = GPIO_PIN_0;
        gpio_init_struct.Mode = GPIO_MODE_AF_PP;            /* 复用推挽输出 */
        gpio_init_struct.Pull = GPIO_PULLDOWN;              /* 下拉 */
        gpio_init_struct.Speed = GPIO_SPEED_FREQ_HIGH;      /* 高速 */
        HAL_GPIO_Init(GPIOA, &gpio_init_struct);

        HAL_NVIC_SetPriority(TIM5_IRQn, 1, 3);              /* 抢占1，子优先级3 */
        HAL_NVIC_EnableIRQ(TIM5_IRQn);                      /* 开启ITMx中断 */
    }
}

/* 输入捕获状态(g_timxchy_cap_sta)
 * [7]  :0,没有成功的捕获;1,成功捕获到一次.
 * [6]  :0,还没捕获到高电平;1,已经捕获到高电平了.
 * [5:0]:捕获高电平后溢出的次数,最多溢出63次,所以最长捕获值 = 63*65536 + 65535 = 4194303
 *       注意:为了通用,我们默认ARR和CCRy都是16位寄存器,对于32位的定时器(如:TIM5),也只按16位使用
 *       按1us的计数频率,最长溢出时间为:4194303 us, 约4.19秒
 *
 *      (说明一下：正常32位定时器来说,1us计数器加1,溢出时间:4294秒)
 */
uint8_t g_timxchy_cap_sta = 0;    /* 输入捕获状态 */
uint16_t g_timxchy_cap_val = 0;   /* 输入捕获值 */

/* 定时器5中断服务函数 */
void TIM5_IRQHandler(void){
    HAL_TIM_IRQHandler(&g_timx_cap_chy_handle);  /* 定时器HAL库共用处理函数 */
}

/* 定时器输入捕获中断处理回调函数 */
void HAL_TIM_IC_CaptureCallback(TIM_HandleTypeDef *htim)
{
    if (htim->Instance == TIM5)
    {
        if ((g_timxchy_cap_sta & 0X80) == 0)                /* 还没有成功捕获 */
        {
            if (g_timxchy_cap_sta & 0X40)                   /* 捕获到一个下降沿 */
            {
                /* 标记成功捕获到一次高电平脉宽 */
                g_timxchy_cap_sta |= 0X80; 
                /* 获取当前的捕获值 */
                g_timxchy_cap_val = HAL_TIM_ReadCapturedValue(&g_timx_cap_chy_handle, TIM_CHANNEL_1); 
                /* 一定要先清除原来的设置 */
                TIM_RESET_CAPTUREPOLARITY(&g_timx_cap_chy_handle, TIM_CHANNEL_1);
                /* 配置TIM5通道1上升沿捕获,这一次是下降沿触发，下一次改上升沿触发 */
                TIM_SET_CAPTUREPOLARITY(&g_timx_cap_chy_handle, TIM_CHANNEL_1, TIM_ICPOLARITY_RISING); 
            }
            else /* 还未开始,第一次捕获上升沿 */
            {
                g_timxchy_cap_sta = 0;                              /* 清空 */
                g_timxchy_cap_val = 0;
                g_timxchy_cap_sta |= 0X40;                          /* 标记捕获到了上升沿 */
                __HAL_TIM_DISABLE(&g_timx_cap_chy_handle);          /* 关闭定时器5 */
                __HAL_TIM_SET_COUNTER(&g_timx_cap_chy_handle, 0);   /* 定时器5计数器清零 */
                TIM_RESET_CAPTUREPOLARITY(&g_timx_cap_chy_handle, TIM_CHANNEL_1);   /* 一定要先清除原来的设置！！ */
                /* 定时器5通道1设置为下降沿捕获，这一次是上升沿触发，下一次改下降沿触发 */
                TIM_SET_CAPTUREPOLARITY(&g_timx_cap_chy_handle, TIM_CHANNEL_1, TIM_ICPOLARITY_FALLING); 
                __HAL_TIM_ENABLE(&g_timx_cap_chy_handle);           /* 使能定时器5 */
            }
        }
    }
}
/* 定时器更新中断回调函数 */
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
{
    if (htim->Instance == TIM5)
    {
        if ((g_timxchy_cap_sta & 0X80) == 0)            /* 还未成功捕获 */
        {
            if (g_timxchy_cap_sta & 0X40)               /* 已经捕获到高电平了 */
            {
                if ((g_timxchy_cap_sta & 0X3F) == 0X3F) /* 高电平太长了 */
                {
                    TIM_RESET_CAPTUREPOLARITY(&g_timx_cap_chy_handle, TIM_CHANNEL_1);                     /* 一定要先清除原来的设置 */
                    TIM_SET_CAPTUREPOLARITY(&g_timx_cap_chy_handle, TIM_CHANNEL_1, TIM_ICPOLARITY_RISING);/* 配置TIM5通道1上升沿捕获 */
                    g_timxchy_cap_sta |= 0X80;          /* 标记成功捕获了一次 */
                    g_timxchy_cap_val = 0XFFFF;
                }
                else      /* 累计定时器溢出次数 */
                {
                    g_timxchy_cap_sta++;
                }
            }
        }
    }
}
````

**案例2：PWMI模式测频率占空比**

通过定时器3通道2（PB5）输出PWM

将PWM输入到定时器8通道1（PC6），测量PWM的频率/周期、占空比等信息（通道1获得整个周期，通道2获得高电平周期）

````c
TIM_HandleTypeDef MyTIM_IC_Handle;
TIM_IC_InitTypeDef MyTIM_IC_InitSturcture;
void MyIC_Init(void){

    MyTIM_IC_Handle.Instance = TIM8;
    MyTIM_IC_Handle.Init.Prescaler = 0;
    MyTIM_IC_Handle.Init.Period = 65535;
    MyTIM_IC_Handle.Init.CounterMode = TIM_COUNTERMODE_UP;
   
    HAL_TIM_IC_Init(&MyTIM_IC_Handle);

    TIM_SlaveConfigTypeDef TIM_SlaveInitStructure;
    TIM_SlaveInitStructure.SlaveMode = TIM_SLAVEMODE_RESET;             // 从模式：复位
    TIM_SlaveInitStructure.InputTrigger = TIM_TS_TI1FP1;                // 触发方式：TI1
    TIM_SlaveInitStructure.TriggerFilter = 0;
    TIM_SlaveInitStructure.TriggerPolarity = TIM_TRIGGERPOLARITY_RISING;
    HAL_TIM_SlaveConfigSynchro(&MyTIM_IC_Handle,&TIM_SlaveInitStructure);
    
    MyTIM_IC_InitSturcture.ICFilter = 0;
    MyTIM_IC_InitSturcture.ICPolarity = TIM_ICPOLARITY_RISING;          // 上升沿触发搬运
    MyTIM_IC_InitSturcture.ICPrescaler = TIM_ICPSC_DIV1 ;
    MyTIM_IC_InitSturcture.ICSelection = TIM_ICSELECTION_DIRECTTI;      // 直连
    HAL_TIM_IC_ConfigChannel(&MyTIM_IC_Handle,&MyTIM_IC_InitSturcture,TIM_CHANNEL_1);  // 通道1获得整个周期

    MyTIM_IC_InitSturcture.ICPolarity = TIM_ICPOLARITY_FALLING;         // 下降沿触发搬运
    MyTIM_IC_InitSturcture.ICPrescaler = TIM_ICPSC_DIV1 ;
    MyTIM_IC_InitSturcture.ICSelection = TIM_ICSELECTION_INDIRECTTI;    // 交叉连接
    HAL_TIM_IC_ConfigChannel(&MyTIM_IC_Handle,&MyTIM_IC_InitSturcture,TIM_CHANNEL_2);  // 通道2获得高电平周期
    
    //HAL_TIM_IC_Start(&MyTIM_IC_Handle,TIM_CHANNEL_1);    // 不产生中断，可以自己写个函数获取PWM比例
    HAL_TIM_IC_Start_IT(&MyTIM_IC_Handle,TIM_CHANNEL_1);   // 本次使用中断，在中断函数中获取PWM比例
    HAL_TIM_IC_Start(&MyTIM_IC_Handle,TIM_CHANNEL_2);
}
void HAL_TIM_IC_MspInit(TIM_HandleTypeDef *htim){
    if(htim->Instance == TIM8){
        GPIO_InitTypeDef gpio_init_struct = {0};

        __HAL_RCC_TIM8_CLK_ENABLE();
        __HAL_RCC_GPIOC_CLK_ENABLE();

        gpio_init_struct.Pin = GPIO_PIN_6;
        gpio_init_struct.Mode = GPIO_MODE_AF_PP;
        gpio_init_struct.Pull = GPIO_PULLDOWN;
        gpio_init_struct.Speed = GPIO_SPEED_FREQ_HIGH;
        HAL_GPIO_Init(GPIOC, &gpio_init_struct);
        
        /* TIM1/TIM8有独立的输入捕获中断服务函数 */
        HAL_NVIC_SetPriority(TIM8_CC_IRQn, 1, 3);
        HAL_NVIC_EnableIRQ(TIM8_CC_IRQn);
    }
}
// 中断服务函数：TIM8捕获中断
void TIM8_CC_IRQHandler(void){
    HAL_TIM_IRQHandler(&MyTIM_IC_Handle);
}
uint32_t PWMHigh = 0;
uint32_t PWMDown = 0;
void HAL_TIM_IC_CaptureCallback(TIM_HandleTypeDef *htim){
    if(htim->Instance == TIM8){
        if(htim->Channel == HAL_TIM_ACTIVE_CHANNEL_1){
            PWMHigh = HAL_TIM_ReadCapturedValue(htim,TIM_CHANNEL_1);   // 获得整个周期
            PWMDown = HAL_TIM_ReadCapturedValue(htim,TIM_CHANNEL_2);   // 获得高电平周期
        }
    }
}
````

#### 标准库

##### 常用函数

````c
//初始化IC，但是和OC不同的是，IC只有这一个函数，在TIM_ICInitTypeDef结构体中选择初始化通道；而OC有4个函数TIM_OCXInit初始化不同的通道
void TIM_ICInit(TIM_TypeDef* TIMx, TIM_ICInitTypeDef* TIM_ICInitStruct);    
// 配置PWMI模式：快速配置两个IC通道，不需要我们手动配置两个通道，内部会根据通道1的直连/交叉输入，自动配置通道2为相反的直连/交叉输入
void TIM_PWMIConfig(TIM_TypeDef* TIMx, TIM_ICInitTypeDef* TIM_ICInitStruct);
// 给结构体附初始值
void TIM_ICStructInit(TIM_ICInitTypeDef* TIM_ICInitStruct);

// 设置PSC，参数3TIM_PSCReloadMode：
//                              1、TIM_PSCReloadMode_Update:在更新事件后执行
//								2、TIM_PSCReloadMode_Immediate：立刻执行
void TIM_PrescalerConfig(TIM_TypeDef* TIMx, uint16_t Prescaler, uint16_t TIM_PSCReloadMode);



void TIM_SelectOutputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_TRGOSource);         //选择主模式的触发源

void TIM_SelectInputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_InputTriggerSource);  //选择从模式的触发源
void TIM_SelectSlaveMode(TIM_TypeDef* TIMx, uint16_t TIM_SlaveMode);              //选择从模式

//配置通道的分频器，在结构体中也可以配置
void TIM_SetIC1Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);
void TIM_SetIC2Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);
void TIM_SetIC3Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);
void TIM_SetIC4Prescaler(TIM_TypeDef* TIMx, uint16_t TIM_ICPSC);

//读取对应通道的CCR
uint16_t TIM_GetCapture1(TIM_TypeDef* TIMx);
uint16_t TIM_GetCapture2(TIM_TypeDef* TIMx);
uint16_t TIM_GetCapture3(TIM_TypeDef* TIMx);
uint16_t TIM_GetCapture4(TIM_TypeDef* TIMx);
uint16_t TIM_GetCounter(TIM_TypeDef* TIMx);
````

**从模式函数**

````c
/**
  * @brief  选择从模式触发源
  * @param  TIMx: where x can be  1, 2, 3, 4, 5, 8, 9, 12 or 15 to select the TIM peripheral.
  * @param  TIM_InputTriggerSource: The Input Trigger source.
  *   This parameter can be one of the following values:
  *     @arg TIM_TS_ITR0: Internal Trigger 0
  *     @arg TIM_TS_ITR1: Internal Trigger 1
  *     @arg TIM_TS_ITR2: Internal Trigger 2
  *     @arg TIM_TS_ITR3: Internal Trigger 3
  *     @arg TIM_TS_TI1F_ED: TI1 Edge Detector
  *     @arg TIM_TS_TI1FP1: Filtered Timer Input 1       TI1FP1 触发
  *     @arg TIM_TS_TI2FP2: Filtered Timer Input 2
  *     @arg TIM_TS_ETRF: External Trigger input
  */
void TIM_SelectInputTrigger(TIM_TypeDef* TIMx, uint16_t TIM_InputTriggerSource)
    
/**
  * @brief  选择触发模式
  * @param  TIMx: where x can be 1, 2, 3, 4, 5, 8, 9, 12 or 15 to select the TIM peripheral.
  * @param  TIM_SlaveMode: specifies the Timer Slave Mode.
  *   This parameter can be one of the following values:
  *     @arg TIM_SlaveMode_Reset:     重置CNT
  *     @arg TIM_SlaveMode_Gated:     The counter clock is enabled when the trigger signal (TRGI) is high.
  *     @arg TIM_SlaveMode_Trigger:   The counter starts at a rising edge of the trigger TRGI.
  *     @arg TIM_SlaveMode_External1: Rising edges of the selected trigger (TRGI) clock the counter.
  */
void TIM_SelectSlaveMode(TIM_TypeDef* TIMx, uint16_t TIM_SlaveMode)
````



**初始化结构体**

````c
typedef struct{
  uint16_t TIM_Channel;          // 选择通道
  uint16_t TIM_ICPolarity;       // 选择极性
  uint16_t TIM_ICSelection;      // 选择直连、交叉
  uint16_t TIM_ICPrescaler;      // 选择分频
  uint16_t TIM_ICFilter;         // 滤波
} TIM_ICInitTypeDef;
````

````c
//TIM_Channel参数：选择通道
#define TIM_Channel_1                      ((uint16_t)0x0000)
#define TIM_Channel_2                      ((uint16_t)0x0004)
#define TIM_Channel_3                      ((uint16_t)0x0008)
#define TIM_Channel_4                      ((uint16_t)0x000C)

//TIM_ICPolarity参数：选择极性，上升沿触发、下降沿触发、上升下降都触发
#define  TIM_ICPolarity_Rising             ((uint16_t)0x0000)            
#define  TIM_ICPolarity_Falling            ((uint16_t)0x0002)
#define  TIM_ICPolarity_BothEdge           ((uint16_t)0x000A)

//参数uint16_t TIM_ICPrescaler：选择分频
#define TIM_ICPSC_DIV1                     ((uint16_t)0x0000)    //1就是1
#define TIM_ICPSC_DIV2                     ((uint16_t)0x0004)    //除2
#define TIM_ICPSC_DIV4                     ((uint16_t)0x0008)
#define TIM_ICPSC_DIV8                     ((uint16_t)0x000C)
    
//TIM_ICSelection参数：选择直连、交叉通道
#define TIM_ICSelection_DirectTI           ((uint16_t)0x0001)
#define TIM_ICSelection_IndirectTI         ((uint16_t)0x0002)

//TIM_ICFilter参数:0x0 ~ 0xf   滤波
````

##### 案例

**案例1：输入捕获模式测频率**

该工程使用了2块stm32芯片，一块产生PWM方波，一块检测PWM方波

产生PWM方波STM32

````c
void PWM_Init(void){
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
		
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP;           //必须使用复用开漏/推挽输出，使用复用推挽输出才能将控制权交给片上外设,PWM波形才能通过引脚输出
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;                 //TIM2的CH1只能用在PA0，当然也可以重映射
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	TIM_InternalClockConfig(TIM2);
	
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
	TIM_TimeBaseInitStructure.TIM_Period = 100 - 1;              //ARR
	TIM_TimeBaseInitStructure.TIM_Prescaler = 720 - 1;           //PSC
	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM2, &TIM_TimeBaseInitStructure);
	
	//输出比较初始化
	TIM_OCInitTypeDef TIM_OCInitStructure;  
	TIM_OCStructInit(&TIM_OCInitStructure);   //先对结构体初始化，以免发生小错误

	TIM_OCInitStructure.TIM_OCMode = TIM_OCMode_PWM1;               //使用PWM1
	TIM_OCInitStructure.TIM_OCPolarity = TIM_OCPolarity_High;       //ref不反转
	TIM_OCInitStructure.TIM_OutputState = TIM_OutputState_Enable;
	TIM_OCInitStructure.TIM_Pulse = 0;                              //CCR
	TIM_OC1Init(TIM2, &TIM_OCInitStructure);
	
	TIM_Cmd(TIM2, ENABLE);
}
void PWM_SetCompare1(uint16_t pulse){                //设置CCR
	TIM_SetCompare1(TIM2,pulse);
}
void PWM_SetPrescalerConfig(uint16_t Prescaler){     //设置PSC
	TIM_PrescalerConfig(TIM2, Prescaler, TIM_PSCReloadMode_Immediate);
}
````

检测PWM方波STM32

````c
#include "stm32f10x.h"                  // Device header

void IC_Init(void){
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
		
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;           
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;                     //读取PA0引脚
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	TIM_InternalClockConfig(TIM2);
	
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
	TIM_TimeBaseInitStructure.TIM_Period = 65536 - 1;             //ARR
	TIM_TimeBaseInitStructure.TIM_Prescaler = 72 - 1;             //PSC
	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM2, &TIM_TimeBaseInitStructure);
	
	TIM_ICInitTypeDef TIM_ICInitStructure;
	TIM_ICInitStructure.TIM_Channel = TIM_Channel_1;                 //通道1
	TIM_ICInitStructure.TIM_ICFilter = 0xF;                          //滤波
	TIM_ICInitStructure.TIM_ICPolarity = TIM_ICPolarity_Rising;      //上升沿触发
	TIM_ICInitStructure.TIM_ICPrescaler = TIM_ICPSC_DIV1;            //1分频
	TIM_ICInitStructure.TIM_ICSelection = TIM_ICSelection_DirectTI;  //直连通道
	
	TIM_ICInit(TIM2,&TIM_ICInitStructure);                           //初始化IC
	
    // 自动完成CNT清零操作
	TIM_SelectInputTrigger(TIM2, TIM_TS_TI1FP1);                     //触发源选择，选择TI1FP1作为从模式触发源
	TIM_SelectSlaveMode(TIM2,TIM_SlaveMode_Reset);                   //从触发，使CNT清零
	
	TIM_Cmd(TIM2, ENABLE);
}

uint32_t IC_GetCapture1(void){            
	//fc = 72M / (PSC+1)
    //Freq = 72M / (PSC+1) / CCR             CCR就是CNT
	return 72000000 / 72 / TIM_GetCapture1(TIM2);   //读取CCR的值，计算频率
}

int main(void)
{
	IC_Init();
	OLED_Init();
	
	OLED_ShowString(1, 1, "Freq:00000Hz");
	while (1)
	{
		OLED_ShowNum(1, 6, IC_GetCapture1(), 5);
	}
}
````

**案例2：PWMI模式测频率占空比**

通道1获得整个周期，通道2获得高电平周期

````c
void IC_Init(void){
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);
		
	GPIO_InitTypeDef GPIO_InitStructure;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;           
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;                     //读取PA0引脚
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitStructure);
	
	TIM_InternalClockConfig(TIM2);
	
	TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure;
	TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
	TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
	TIM_TimeBaseInitStructure.TIM_Period = 65536 - 1;             //ARR
	TIM_TimeBaseInitStructure.TIM_Prescaler = 72 - 1;             //PSC
	TIM_TimeBaseInitStructure.TIM_RepetitionCounter = 0;
	TIM_TimeBaseInit(TIM2, &TIM_TimeBaseInitStructure);
	
	TIM_ICInitTypeDef TIM_ICInitStructure;
	TIM_ICInitStructure.TIM_Channel = TIM_Channel_1;                 //通道1
	TIM_ICInitStructure.TIM_ICFilter = 0xF;                          //滤波
	TIM_ICInitStructure.TIM_ICPolarity = TIM_ICPolarity_Rising;      //上升沿触发
	TIM_ICInitStructure.TIM_ICPrescaler = TIM_ICPSC_DIV1;            //1分频
	TIM_ICInitStructure.TIM_ICSelection = TIM_ICSelection_DirectTI;  //直连通道

    // 可以手动的配置通道1的直连输入 和通道2的交叉输入，但是有更方便的函数
	//	TIM_ICInit(TIM2,&TIM_ICInitStructure);
	//	TIM_ICInitStructure.TIM_Channel = TIM_Channel_2;                   //通道2
	//	TIM_ICInitStructure.TIM_ICFilter = 0xF;                            //滤波
	//	TIM_ICInitStructure.TIM_ICPolarity = TIM_ICPolarity_Falling;       //下降沿触发
	//	TIM_ICInitStructure.TIM_ICPrescaler = TIM_ICPSC_DIV1;              //1分频
	//	TIM_ICInitStructure.TIM_ICSelection = TIM_ICSelection_IndirectTI;  //交叉通道
	//	TIM_ICInit(TIM2,&TIM_ICInitStructure);
	
	// 自动完成通道12的配置
	TIM_PWMIConfig(TIM2,&TIM_ICInitStructure);                       //初始化通道1和2，函数内部会判断
	                     
	TIM_SelectInputTrigger(TIM2, TIM_TS_TI1FP1);                     //触发源选择
	TIM_SelectSlaveMode(TIM2,TIM_SlaveMode_Reset);                   //从触发
	
	TIM_Cmd(TIM2, ENABLE);
}

uint32_t IC_GetCapture1(void){
	//fc = 72M / (PSC+1)
	return 1000000 / TIM_GetCapture1(TIM2);
}
//获得占空比
uint32_t IC_GetDuty(void){
	return TIM_GetCapture2(TIM2) * 100 / TIM_GetCapture1(TIM2);  // 乘100 为了完成百分制
}

int main(void)
{
	IC_Init();
	OLED_Init();
	
	OLED_ShowString(1, 1, "Freq:00000Hz");
	OLED_ShowString(2, 1, "Duty:00000Hz");
	while (1)
	{
		OLED_ShowNum(1, 6, IC_GetCapture1(), 5);
		OLED_ShowNum(2, 6, IC_GetDuty(), 5);
	}
}
````



### 编码器接口

#### 编码器接口简介

* Encoder Interface 编码器接口
* 编码器接口可接收增量（正交）编码器的信号，根据编码器旋转产生的正交信号脉冲，自动控制CNT自增或自减，从而指示编码器的位置、旋转方向和旋转速度
* 每个高级定时器和通用定时器都拥有1个编码器接口
* 两个输入引脚借用了输入捕获的通道1和通道2
* 硬件级别的自增或自减，不需要像以前那样进入中断实现自增自减的(降低了软件内存的消耗)
* 抗毛刺：抗干扰

#### 正交编码器

![image-20230706184859486](STM32卷一.assets/image-20230706184859486.png)

#### 编码器接口基本结构



![image-20230706185033765](STM32卷一.assets/image-20230706185033765.png)



#### 工作模式

![image-20230706185052101](STM32卷一.assets/image-20230706185052101.png)

#### 实例（均不反相）

即边沿极性选择都为正

![image-20230706185156357](STM32卷一.assets/image-20230706185156357.png)

#### 实例（TI1反相）

对TI1的极性进行反转

![image-20230706185300088](STM32卷一.assets/image-20230706185300088.png)

对TI1的极性进行反转，才能得到图中的结果

如果正反自增自减不是想要的结果，可以选择更改其中一个极性

#### HAL库

##### **常用函数**

````c
//编码器初始化
HAL_StatusTypeDef HAL_TIM_Encoder_Init(TIM_HandleTypeDef *htim,  TIM_Encoder_InitTypeDef *sConfig)
//编码器解初始化
HAL_StatusTypeDef HAL_TIM_Encoder_DeInit(TIM_HandleTypeDef *htim)

__weak void HAL_TIM_Encoder_MspInit(TIM_HandleTypeDef *htim)

__weak void HAL_TIM_Encoder_MspDeInit(TIM_HandleTypeDef *htim)

//开启编码器
HAL_TIM_Encoder_Start(TIM_HandleTypeDef *htim, uint32_t Channel)
//关闭编码器
HAL_TIM_Encoder_Stop(TIM_HandleTypeDef *htim, uint32_t Channel)

    
//开启成功中断
HAL_TIM_Encoder_Start_IT(TIM_HandleTypeDef *htim, uint32_t Channel)   //内部__HAL_TIM_ENABLE_IT(htim, TIM_IT_CCx);
//关闭成功中断
HAL_TIM_Encoder_Stop_IT(TIM_HandleTypeDef *htim, uint32_t Channel)

//开启DMA
HAL_StatusTypeDef HAL_TIM_Encoder_Start_DMA(TIM_HandleTypeDef *htim, uint32_t Channel, uint32_t *pData1,uint32_t *pData2, uint16_t Length)
//关闭DMA
HAL_StatusTypeDef HAL_TIM_Encoder_Stop_DMA(TIM_HandleTypeDef *htim, uint32_t Channel)

//获得counter值
__HAL_TIM_GET_COUNTER(__HANDLE__);
//获取编码器方向
__HAL_TIM_IS_TIM_COUNTING_DOWN(__HANDLE__);
````

**编码器结构体**

````c
typedef struct{
  uint32_t EncoderMode;     // 编码器计数模式，TI1,TI2,TI12
  uint32_t IC1Polarity;     // 极性
  uint32_t IC1Selection;    // 选择方向
  uint32_t IC1Prescaler;    // 分频：即多少个脉冲计数一次
  uint32_t IC1Filter;    
  uint32_t IC2Polarity;  
  uint32_t IC2Selection;  
  uint32_t IC2Prescaler;  
  uint32_t IC2Filter;     
} TIM_Encoder_InitTypeDef;
````

````c
//EncoderMode 编码器计数模式
#define TIM_ENCODERMODE_TI1                                                 
#define TIM_ENCODERMODE_TI2                                                                    
#define TIM_ENCODERMODE_TI12

// IC1Polarity 极性
#define  TIM_ENCODERINPUTPOLARITY_RISING     // 不反转
#define  TIM_ENCODERINPUTPOLARITY_FALLING    // 反转

// IC1Selection 
#define TIM_ICSELECTION_DIRECTTI
#define TIM_ICSELECTION_INDIRECTTI
#define TIM_ICSELECTION_TRC   

// IC1Prescaler 分频：即多少个脉冲计数一次
#define TIM_ICPSC_DIV1
#define TIM_ICPSC_DIV2
#define TIM_ICPSC_DIV4
#define TIM_ICPSC_DIV8  
````

##### 编码器接口测速

使用TIM2的CH1和CH2（PA0,PA1）

````c
TIM_HandleTypeDef TIM_HandleStructure;
TIM_Encoder_InitTypeDef TIM_Encoder_InitStructure;
void Encoder_Init(void){
    TIM_HandleStructure.Instance = TIM2;
    TIM_HandleStructure.Init.Prescaler = 0;
    TIM_HandleStructure.Init.Period = 65535;
    TIM_HandleStructure.Init.CounterMode = TIM_COUNTERMODE_UP;
    
    TIM_Encoder_InitStructure.EncoderMode = TIM_ENCODERMODE_TI12 ;           // 通道12都计数
    TIM_Encoder_InitStructure.IC1Filter = 0;                                 // 无滤波
    TIM_Encoder_InitStructure.IC1Polarity = TIM_ENCODERINPUTPOLARITY_RISING; // 极性不反转
    TIM_Encoder_InitStructure.IC1Prescaler =  TIM_ICPSC_DIV1;                // 不分频，一个上升沿产生一个计数
    TIM_Encoder_InitStructure.IC1Selection = TIM_ICSELECTION_DIRECTTI;       // 不反转
    TIM_Encoder_InitStructure.IC2Filter = 0;
    TIM_Encoder_InitStructure.IC2Polarity = TIM_ENCODERINPUTPOLARITY_RISING;
    TIM_Encoder_InitStructure.IC2Prescaler = TIM_ICPSC_DIV1;
    TIM_Encoder_InitStructure.IC2Selection = TIM_ICSELECTION_DIRECTTI;
    
    HAL_TIM_Encoder_Init(&TIM_HandleStructure,&TIM_Encoder_InitStructure);   // 初始化
    HAL_TIM_Encoder_Start(&TIM_HandleStructure,TIM_CHANNEL_ALL);             // 使能
}
void HAL_TIM_Encoder_MspInit(TIM_HandleTypeDef *htim){
    if(htim->Instance == TIM2){   
        GPIO_InitTypeDef gpio_init_struct;
        __HAL_RCC_TIM2_CLK_ENABLE();                  

        gpio_init_struct.Pin = GPIO_PIN_0 | GPIO_PIN_1;
        gpio_init_struct.Mode = GPIO_MODE_INPUT;           
        gpio_init_struct.Pull = GPIO_NOPULL;       
        gpio_init_struct.Speed = GPIO_SPEED_FREQ_HIGH;
        HAL_GPIO_Init(GPIOA, &gpio_init_struct);
    }
}
// 获得速度
int Get_Encoder(void){
    int cnt = __HAL_TIM_GET_COUNTER(&TIM_HandleStructure);
    __HAL_TIM_SET_COUNTER(&TIM_HandleStructure,0);
    return cnt;
}
// 获取方向
int Get_Direction(void){
    return __HAL_TIM_IS_TIM_COUNTING_DOWN(&TIM_HandleStructure);
}
int main(void){
    HAL_Init();                                 /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9);         /* 设置时钟,72M */
    delay_init(72);                             /* 初始化延时函数 */
    UART_Init();
    Encoder_Init();
    int cnt = 0;
    uint32_t temp = 0;
    while(1){
        cnt = Get_Encoder();
        printf("encoder:%d \r\n",cnt);
        printf("direction:%d \r\n",Get_Direction());
        delay_ms(1000);
    }
}
````









#### 标准库

##### 常用函数

````c
//初始化编码器接口
/* 参数2
*          #define TIM_EncoderMode_TI1                ((uint16_t)0x0001)    TI1计数
*          #define TIM_EncoderMode_TI2                ((uint16_t)0x0002)    TI2计数
*          #define TIM_EncoderMode_TI12               ((uint16_t)0x0003)    TI12都计数
*  参数3、参数4 
*          @arg TIM_ICPolarity_Falling: IC Falling edge.  反转
*          @arg TIM_ICPolarity_Rising: IC Rising edge.    不反转
*/
void TIM_EncoderInterfaceConfig(TIM_TypeDef* TIMx, uint16_t TIM_EncoderMode,
                                uint16_t TIM_IC1Polarity, uint16_t TIM_IC2Polarity);

uint16_t TIM_GetCounter(TIM_TypeDef* TIMx);               //获取Counter的值
void TIM_SetCounter(TIM_TypeDef* TIMx, uint16_t Counter); //设置Counter的值
````

##### 编码器接口测速

````c
void Encoder_Init(void){
	RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM3, ENABLE);           //使用TIM3
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	
	
	GPIO_InitTypeDef GPIO_InitSturcture;
	GPIO_InitSturcture.GPIO_Mode = GPIO_Mode_IPU;      
	GPIO_InitSturcture.GPIO_Pin = GPIO_Pin_6 | GPIO_Pin_7;         //TIM3的CH1对应PA6，CH2对应PA7
	GPIO_InitSturcture.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitSturcture);
	

	TIM_TimeBaseInitTypeDef TIM_TimeInitSturcture;
	TIM_TimeInitSturcture.TIM_ClockDivision = TIM_CKD_DIV1;
	TIM_TimeInitSturcture.TIM_CounterMode = TIM_CounterMode_Up;
	TIM_TimeInitSturcture.TIM_Period = 65536 - 1;
	TIM_TimeInitSturcture.TIM_Prescaler = 1 - 1;
	TIM_TimeInitSturcture.TIM_RepetitionCounter =  0;
	TIM_TimeBaseInit(TIM3,&TIM_TimeInitSturcture);
	
	TIM_ICInitTypeDef TIM_ICinitStructure;                         //结构体配置，只需要配置极个别属性
	TIM_ICStructInit(&TIM_ICinitStructure);
	TIM_ICinitStructure.TIM_Channel = TIM_Channel_1;
	TIM_ICinitStructure.TIM_ICFilter = 0xf;
	TIM_ICInit(TIM3, &TIM_ICinitStructure);
	
	TIM_ICinitStructure.TIM_Channel = TIM_Channel_2;
	TIM_ICinitStructure.TIM_ICFilter = 0xf;
	TIM_ICInit(TIM3, &TIM_ICinitStructure);
	
	TIM_EncoderInterfaceConfig(TIM3, TIM_EncoderMode_TI12,TIM_ICPolarity_Rising, TIM_ICPolarity_Falling);  //编码器接口初始化
	
	TIM_Cmd(TIM3,ENABLE);
}

int16_t Get_Encoder(void){
	int16_t Temp = TIM_GetCounter(TIM3);
	//TIM_SetCounter(TIM3,0);
	return Temp;                 //获得Count值
}

int main(void)
{
	OLED_Init();
	Encoder_Init();
	OLED_ShowString(1,1,"Speed:");
	while (1)
	{
		OLED_ShowSignedNum(1,7, Get_Encoder(), 5);
		Delay_ms(1000);
	}
}
````

## 高级定时器

TIM1/TIM8

**主要特性**

* 16位递增、递减、中心对齐计数器（计数值：0~65535）~
* 16位预分频器（分频系数：1~65536）
* 可用于触发DAC、ADC
* 在更新事件、触发事件、输入捕获、输出比较时，会产生中断/DMA请求
* 4个独立通道，可用于：输入捕获、输出比较、输出PWM、单脉冲模式
* 使用外部信号控制定时器且可实现多个定时器互连的同步电路
* 支持编码器和霍尔传感器电路等
* **重复计数器**
* **死区时间带可编程的互补输出**
* **断路输入，用于将定时器的输出信号置于用户可选的安全配置中**



**高级定时器的中断函数**：TIM1和TIM8有多个中断函数

    TIM1_BRK_IRQHandler        ; TIM1 Break
    TIM1_UP_IRQHandler         ; TIM1 Update
    TIM1_TRG_COM_IRQHandler    ; TIM1 Trigger and Commutation
    TIM1_CC_IRQHandler         ; TIM1 Capture Compare

**框图**

![image-20230803204344106](STM32卷一.assets/image-20230803204344106.png)

### **重复计数器**

重复计数器RCR

* 在基本/通用定时器发生上溢/下溢事件时直接就生成更新时间，但对于高级定时器却不是这样，高级控制定时器在硬件结构上多出了重复计数器，计数器每次上溢或下溢都能使重复计数器减1，当重复计数器减到0时，再发生一次溢出就会产生更新事件
* 如果设置RCR为N，更新事件将在N+1次溢出时发生
* 通过TIM1/8->RCR 设置RCR的值

可用于输出指定个数PWM：比如TIM8->RCR = 10，当溢出11次后，产生更新中断，在更新中断中停止TIM：TIM8->CR1 &= ~(1 << 0);





### 互补输出**死区控制**

互补输出：即OCx和OCxN，一路输出高电平时另一路输出低电平

死区控制：输出的两路PWM(互补),存在延迟，一路输出PWM高电平时，另一路延迟输出PWM低电平；

![image-20230804120952380](STM32卷一.assets/image-20230804120952380.png)

刹车控制：停止所有PWM的输出

![image-20230804121754707](STM32卷一.assets/image-20230804121754707.png)

#### 常用函数



**带死区控制的互补输出应用之H桥**

![image-20230804121137098](STM32卷一.assets/image-20230804121137098.png)

OC1导通：Q1和Q4分别导通，电机正转

OC1N导通：Q2和Q3分别导通，电机反转



互补输出：常用与控制电机正反转

死区控制：由于元器件是有延迟特性，所以需要加上死区时间控制；即控制电机正反转时，正转切换反转时要有一个延迟，防止短路



**框图**

![image-20230804121424367](STM32卷一.assets/image-20230804121424367.png)

**死区时间计算**

![image-20230804122937402](STM32卷一.assets/image-20230804122937402.png)



|              函数               |    主要寄存器     |             主要功能             |
| :-----------------------------: | :---------------: | :------------------------------: |
|       HAL_TIM_PWM_Init()        |   CR1、ARR、PSC   |       初始化定时器基础参数       |
|      HAL_TIM_PWM_MspInit()      |        无         | 存放NVIC、CLOCK、GPIO初始化代码  |
|   HAL_TIM_PWM_ConfigChannel()   | CCMRx、CCRx、CCER | 配置PWM模式、比较值、输出极性等  |
| HAL_TIMEx_ConfigBreakDeadTime() |       BDTR        |     配置刹车功能、死区时间等     |
|       HAL_TIM_PWM_Start()       |     CCER、CR1     |   使能输出、主输出、启动计数器   |
|     HAL_TIMEx_PWMN_Start()      |     CCER、CR1     | 使能互补输出、主输出、启动计数器 |

````c
typedef struct { 
   uint32_t OCMode; 	    /* 输出比较模式选择 */
   uint32_t Pulse; 	        /* 设置比较值 */
   uint32_t OCPolarity;     /* 设置输出比较极性 */
   uint32_t OCNPolarity;    /* 设置互补输出比较极性 */
   uint32_t OCFastMode;     /* 使能或失能输出比较快速模式 */
   uint32_t OCIdleState;    /* 空闲状态下OCx输出 */
   uint32_t OCNIdleState;   /* 空闲状态下OCxN输出 */ 
} TIM_OC_InitTypeDef;
typedef struct {
    uint32_t OffStateRunMode;    /* 运行模式下的关闭状态选择 */ 
    uint32_t OffStateIDLEMode;   /* 空闲模式下的关闭状态选择 */ 
    uint32_t LockLevel; 		 /* 寄存器锁定设置 */ 
    uint32_t DeadTime; 	         /* 死区时间设置 */ 
    uint32_t BreakState; 	     /* 是否使能刹车功能 */ 
    uint32_t BreakPolarity;		 /* 刹车输入极性 */ 
    uint32_t BreakFilter; 		 /* 刹车输入滤波器(F1/F4系列没有) */ 
    uint32_t AutomaticOutput; 	 /* 自动恢复输出使能，即使能AOE位 */
} TIM_BreakDeadTimeConfigTypeDef;
````



#### **案例**

互补输出带死区控制实验

* 通过定时器1通道1输出频率为1KHz，占空比为70%的PWM，使用PWM模式1：PSC=71，ARR=999，CCR = 700

* 使能互补输出并设置死区时间控制：设置DTG为100(5.56us),进行验证死区时间是否正确

  ​	以4分频为例：100转二进制01100100，根据上方图表的公式：100*1/72000000/4 = 5.56us

* 使能刹车功能：刹车输入信号高电平有效（当有高电平输入时，停止PWM输出），配置输出空闲状态等，最后用示波器验证

* TIM1_CH1复用在了PE9,TIM1_CH1N -->PE8,TIM1_BKIN-->PE15

````c
TIM_HandleTypeDef g_timx_cplm_pwm_handle;                                  /* 定时器x句柄 */
TIM_BreakDeadTimeConfigTypeDef g_sbreak_dead_time_config;                  /* 死区时间设置 */

/* 高级定时器 互补输出 初始化函数（使用PWM模式1） */
void atim_timx_cplm_pwm_init(){
    TIM_OC_InitTypeDef tim_oc_cplm_pwm = {0};

    g_timx_cplm_pwm_handle.Instance = TIM1;                                 /* 定时器x */
    g_timx_cplm_pwm_handle.Init.Prescaler = 72-1;                           /* 定时器预分频系数 */
    g_timx_cplm_pwm_handle.Init.CounterMode = TIM_COUNTERMODE_UP;           /* 递增计数模式 */
    g_timx_cplm_pwm_handle.Init.Period = 1000-1;                            /* 自动重装载值 */
    /* CKD[1:0] = 10, tDTS = 4 * tCK_INT = Ft / 4 = 18Mhz */
    g_timx_cplm_pwm_handle.Init.ClockDivision = TIM_CLOCKDIVISION_DIV4;    
    HAL_TIM_PWM_Init(&g_timx_cplm_pwm_handle);

    tim_oc_cplm_pwm.OCMode = TIM_OCMODE_PWM1;                               /* PWM模式1 */
    tim_oc_cplm_pwm.Pulse = 700 - 1;                                        /* CCR */
    tim_oc_cplm_pwm.OCPolarity = TIM_OCPOLARITY_HIGH;                       /* OCy 高电平有效 */
    tim_oc_cplm_pwm.OCNPolarity = TIM_OCNPOLARITY_HIGH;                     /* OCyN 高电平有效 */
    tim_oc_cplm_pwm.OCIdleState = TIM_OCIDLESTATE_RESET;                    /* 当MOE=0，OCx=0 */
    tim_oc_cplm_pwm.OCNIdleState = TIM_OCNIDLESTATE_RESET;                  /* 当MOE=0，OCxN=0 */
    HAL_TIM_PWM_ConfigChannel(&g_timx_cplm_pwm_handle, &tim_oc_cplm_pwm, TIM_CHANNEL_1);

    /* 设置死区参数，开启死区中断 */
    g_sbreak_dead_time_config.DeadTime = 100 - 1;                           /* 死区时间 */
    g_sbreak_dead_time_config.OffStateRunMode = TIM_OSSR_DISABLE;           /* 运行模式的关闭输出状态 */
    g_sbreak_dead_time_config.OffStateIDLEMode = TIM_OSSI_DISABLE;          /* 空闲模式的关闭输出状态 */
    g_sbreak_dead_time_config.LockLevel = TIM_LOCKLEVEL_OFF;                /* 不用寄存器锁功能 */
    g_sbreak_dead_time_config.BreakState = TIM_BREAK_ENABLE;                /* 使能刹车输入 */
    g_sbreak_dead_time_config.BreakPolarity = TIM_BREAKPOLARITY_HIGH;       /* 刹车输入有效信号极性为高 */
    g_sbreak_dead_time_config.AutomaticOutput = TIM_AUTOMATICOUTPUT_ENABLE; /* 使能AOE位，允许刹车结束后自动恢复输出 */
    HAL_TIMEx_ConfigBreakDeadTime(&g_timx_cplm_pwm_handle, &g_sbreak_dead_time_config); //配置刹车功能、死区时间等

    HAL_TIM_PWM_Start(&g_timx_cplm_pwm_handle, TIM_CHANNEL_1);              /* OCy 输出使能 */
    HAL_TIMEx_PWMN_Start(&g_timx_cplm_pwm_handle,TIM_CHANNEL_1);            /* OCyN 输出使能 */
}

/* 定时器 PWM输出 MSP初始化函数 */
void HAL_TIM_PWM_MspInit(TIM_HandleTypeDef *htim)
{
    if (htim->Instance == TIM1)
    {
        GPIO_InitTypeDef gpio_init_struct = {0};

        __HAL_RCC_TIM1_CLK_ENABLE();
        __HAL_RCC_GPIOE_CLK_ENABLE();

        gpio_init_struct.Pin = GPIO_PIN_9;
        gpio_init_struct.Mode = GPIO_MODE_AF_PP; 
        gpio_init_struct.Pull = GPIO_PULLDOWN;
        gpio_init_struct.Speed = GPIO_SPEED_FREQ_HIGH ;
        HAL_GPIO_Init(GPIOE, &gpio_init_struct);

        gpio_init_struct.Pin = GPIO_PIN_8;
        HAL_GPIO_Init(GPIOE, &gpio_init_struct);

        gpio_init_struct.Pin = GPIO_PIN_15;
        HAL_GPIO_Init(GPIOE, &gpio_init_struct);

        __HAL_RCC_AFIO_CLK_ENABLE();
        __HAL_AFIO_REMAP_TIM1_ENABLE();       // 复用AFIO
    }
}
int main(void){
    HAL_Init();                                /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9);        /* 设置时钟, 72Mhz */
    delay_init(72);                            /* 延时初始化 */

    atim_timx_cplm_pwm_init();
    while (1){
    }
}
````

# RTC

## RTC简介

实时时钟(Real Time Clock，RTC)，本质是一个计数器，计数频率常为秒，专门用来记录时间,在相应软件配置下，可提供时钟日历的功能。修改计数器的值可以重新设置系统当前的时间和日期。

![image-20230808175034278](STM32卷一.assets/image-20230808175034278.png)

实时时钟与定时器的区别：

* 实时时钟：能提供时间（秒钟数）、能在MCU掉电后运行、低功耗
* 普通定时器无法掉电运行！

**常用的RTC方案**

![image-20230808175347939](STM32卷一.assets/image-20230808175347939.png)

| **对比因素** | **内部RTC**      | **外置RTC**      |
| ------------ | ---------------- | ---------------- |
| **信息差异** | 提供秒/亚秒信号  | 提供秒信号和日历 |
| **功耗**     | 功耗高           | 功耗低           |
| **体积**     | 不用占用额外体积 | 体积大           |
| **成本**     | 成本低           | 成本高           |

1. 一般都需要设计RTC外围电路；
2. 一般都可以给RTC设置独立的电源；
3. 多数RTC的寄存器采用BCD码存储时间信息；

**RTC特性**

* 可编程的预分频系数：分频系数最高为2^20
* 32位的可编程计数器，可用于较长时间段的测量。（若最小单位为秒：=4,294,967,295秒=49,710天  大概136年。）
* 2个分离的时钟：用于APB1接口的PCLK1和RTC时钟(RTC时钟的频率必须小于PCLK1时钟频率的四分之一以上)。
* 可以选择以下三种RTC的时钟源：
  * HSE时钟除以128 
  * LSE振荡器时钟 32.768kHz（常用的是外部低速，稳定精准，重要的是VDD掉电后可有后备供电区域给它供电）
  * LSI振荡器时钟 40kHz
* 2个独立的复位类型：
  * APB1接口由系统复位；
  * RTC核心(预分频器、闹钟、计数器和分频器)只能由后备域复位。（可导致后备区域复位：侵入事件、软件复位、VBAT掉电）

* 3个专门的可屏蔽中断：
  * 闹钟中断，用来产生一个软件可编程的闹钟中断。
  * 秒中断，用来产生一个可编程的周期性中断信号(最长可达1秒)。
  * 溢出中断，指示内部可编程计数器溢出并回转为0的状态。



**RTC框图**

![1691489160175](STM32卷一.assets/1691489160175.png)

* 系统通过APB1总线对后备区域的RTC进行通信，三斜杠的意思是可断开，因为在系统掉电的时候RTC是独立的，只有在系统运行时才有可能会相通。RTCCLK（RTC时钟输入）必须小于PCLK1（低速AHB时钟）的三分之一以上。
* RTC_PRL（预分频装载寄存器）的值决定TR_CLK脉冲产生的周期，RTC_DIV（预分频器余数寄存器）可读不可写，当RTCCLK的一个上升沿到来，RTC_DIV的值减1，减到0后硬件重载为RTC_PRL的值同时产生一个TR_CLK脉冲，一个TR_CLK脉冲的到来会使RTC_CNT（计数器寄存器）的值加1，同时产生一个RTC_Second中断（由软件配置是否使能，“秒中断”并不一定是一秒触发一次，具体是根据RTC时钟和RTC_PRL的值决定）。
* 当RTC_CNT的值溢出后从0开始，并产生一个溢出中断（由软件配置是否使能）。当RTC_CNT等于RTC_CNTRTC_ALR（闹钟寄存器）时，产生一个闹钟中断（由软件配置是否使能，可在用在系统待机模式下唤醒系统）。
* RTC_CR（RTC控制寄存器）不在后备区域，所以它的数据会随系统复位而复位，也就是说当系统下电是，秒中断、溢出中断、闹钟中断就不存在了，在下一次系统上电时需要重新初始化。图中“退出待机模式”有两种方法：RTC闹钟、WKUP引脚。

## 寄存器

### RTC寄存器

**RTC 控制寄存器（RTC_CRH/CRL）**：RTC 控制寄存器共有两个控制寄存器 RTC_CRH 和 RTC_CRL，两个都是 16 位的。

![1691490453835](STM32卷一.assets/1691490453835.png)

![1691490436494](STM32卷一.assets/1691490436494.png)

该寄存器是 RTC 控制寄存器低位，本章我们用到的是该寄存器的 0，3~5 这几个位，

第 0位是秒钟标志位，我们在进入闹钟中断的时候，通过判断这位来决定是不是发生了秒钟中断。然后必须通过软件将该位清零（写零）。

第 3 位为寄存器同步标志位，我们在修改控制寄存器RTC_CRH/RTC_CRL 之前，必须先判断该位，是否已经同步了，如果没有则需要等待同步，在没同步的情况下修改 RTC_CRH/RTC_CRL 的值是不行的。

第 4 位为配置标志位，在软件修改RTC_CNT/RTC_PRL 的值的时候，必须先软件置位该位，以允许进入配置模式。

第 5 位为 RTC操作位，该位由硬件操作，软件只读。通过该位可以判断上次对 RTC 寄存器的操作是否完成，如果没有，我们必须等待上一次操作结束才能开始下一次操作。

**RTC 预分频装载寄存器（RTC_PRLH/RTC_PRLL）**

RTC 预分频装载寄存器也是有两个寄存器组成，RTC_PRLH 和 RTC_PRLL。这两个寄存器用来配置 RTC 时钟的分频数的，比如我们使用外部 32.768K 的晶振作为时钟的输入频率，那么我们要设置这两个寄存器的值为 32767，得到一秒钟的计数频率。

![1691490700885](STM32卷一.assets/1691490700885.png)

![1691490738891](STM32卷一.assets/1691490738891.png)

该寄存器是 RTC 预分频装载寄存器低位，存放 RTC 预分频装载值低位。如果输入时钟是32.768kHz，这个预分频寄存器中写入 7FFFF 可获得周期 1 秒钟的信号。

与RTC_PRL相似的寄存器RTC_DIV可以在不停止分频计数器的工作，获得预分频计数器的当前值。



**RTC 计数器寄存器（RTC_CNTH/RTC_CNTL）**

RTC 计数器寄存器 RTC_CNT，由 2 个 16 位寄存器组成 RTC_CNTH 和 RTC_CNTL，总共32 位，用来记录秒钟值。注意的是，修改这两个寄存器的时候要先进入配置模式。

![1691490834270](STM32卷一.assets/1691490834270.png)

**RTC 闹钟寄存器（RTC_ALRH/RTC_ALRL）**

RTC 闹钟寄存器，该寄存器也是由 2 个 16 位的寄存器组成 RTC_ALRH 和 RTC_ALRL。总共 32 位，用来标记闹钟产生的时间（以秒为单元）。对于 STM32F1 系列的芯片来说，RTC 外设没有专门的年月日寄存器来分别存放这些信息，全部日期信息以秒的格式存储在这两个寄存器中，可以在编程中对时间进行特殊处理。如果 RTC_CNT 的值与 RTC_ALR 的值相等，并使能了中断的话，会产生一个闹钟中断。注意：该寄存器的修改也是要进入配置模式才能进行。

**备份数据寄存器（BKP_DRx）**

![1691490982697](STM32卷一.assets/1691490982697.png)

该寄存器是一个 16 位寄存器，可以用来存储用户数据，可在 VDD 电源关闭时，通过 VBAT保持上电状态。备份数据寄存器不会在系统复位、电源复位、从待机模式唤醒时复位。

那么在 MCU 复位后，对 RTC 和备份数据寄存器的写访问就被禁止，需要执行以下操作才可以对 RTC 及备份数据寄存器进行写访问：

1) 通过设置寄存器 RCC_APB1ENR 的 PWREN 和 BKPEN 位来打开电源和后备接口时钟
2) 电源控制寄存器(PWR_CR)的 DBP 位来使能对后备寄存器和 RTC 访问



### 相关寄存器

**RCC_APB1ENR寄存器**：使能PWR && BKP时钟

![image-20230808182230536](STM32卷一.assets/image-20230808182230536.png)

**PWR_CR寄存器**：使能后备域和RTC的访问权限

![image-20230808182355187](STM32卷一.assets/image-20230808182355187.png)

**备份区域控制寄存器（RCC_BDCR）**

![1691491087460](STM32卷一.assets/1691491087460.png)

RTC 的时钟源选择及使能设置都是通过这个寄存器来实现的，所以我们在 RTC 操作之前先要通过这个寄存器选择 RTC 的时钟源，然后才能开始其他的操作。

## 常用函数

|            驱动函数            |    关联寄存器     |       功能描述        |
| :----------------------------: | :---------------: | :-------------------: |
|       HAL_RTC_Init(...)        | CRL/CRH/PRLH/PRLL |       初始化RTC       |
|       HAL_RTC_MspInit(…)       |    初始化回调     |      使能RTC时钟      |
|      HAL_RCC_OscConfig(…)      |   RCC_CR/PWR_CR   |     开启LSE时钟源     |
| HAL_RCCEx_PeriphCLKConfig(...) |     RCC_BDCR      |  设置RTC时钟源为LSE   |
| HAL_PWR_EnableBkUpAccess(...)  |      PWR_CR       | 使能备份域的访问权限  |
|   HAL_RTCEx_BKUPWrite/Read()   |      BKP_DRx      | 读/写备份域数据寄存器 |

````c
typedef struct{
    RTC_TypeDef *Instance;   		/* 寄存器基地址 指向 RTC 寄存器基地址*/
    RTC_InitTypeDef Init;    		/* RTC 配置结构体 */
    RTC_DateTypeDef DataToUpdata;   /* RTC 日期结构体 */
    HAL_LockTypeDef Lock; 			/* RTC 锁定对象 */
    __IO HAL_RTCStateTypeDef State; /* RTC 设备访问状态 */
}RTC_HandleTypeDef;
typedef struct{
	uint32_t AsynchPrediv;				/* 异步预分频系数 */
	uint32_t OutPut;					/* 被发送到 RTC Tamper 引脚的信号 */ 
}RTC_InitTypeDef;
````

* AsynchPrediv 用来设置 RTC 的异步预分频系数，也就是设置两个预分频重载寄存器的相关位，因为异步预分频系数是 19 位，所以最大值为 0x7FFFF，不能超过这个值。
* OutPut 用来选择 RTC 输出到 Tamper 引脚的信号，取值为：RTC_OUTPUTSOURCE_NONE（没有输出），RTC_OUTPUTSOURCE_CALIBCLOCK（RTC时钟经过64分频输出到TAMPER），RTC_OUTPUTSOURCE_ALARM（闹钟脉冲信号输出）和 RTC_ OUTPUTSOURCE_SECOND（秒脉冲信号输出）。本实验选择没有输出，不配置即默认值，RTC_OUTPUTSOURCE_NONE。



开启时钟

````c
__HAL_RCC_RTC_ENABLE()
__HAL_RCC_PWR_CLK_ENABLE()
__HAL_RCC_BKP_CLK_ENABLE()
````

中断

````c
__HAL_RTC_ALARM_ENABLE_IT();
#define RTC_IT_OW            RTC_CRH_OWIE       /*!< Overflow interrupt */
#define RTC_IT_ALRA          RTC_CRH_ALRIE      /*!< Alarm interrupt */
#define RTC_IT_SEC           RTC_CRH_SECIE      /*!< Second interrupt */
#define RTC_IT_TAMP1         BKP_CSR_TPIE       /*!< TAMPER Pin interrupt enable */
__HAL_RTC_ALARM_GET_FLAG();
__HAL_RTC_ALARM_CLEAR_FLAG();
#define RTC_FLAG_RTOFF       RTC_CRL_RTOFF      /*!< RTC Operation OFF flag */
#define RTC_FLAG_RSF         RTC_CRL_RSF        /*!< Registers Synchronized flag */
#define RTC_FLAG_OW          RTC_CRL_OWF        /*!< Overflow flag */
#define RTC_FLAG_ALRAF       RTC_CRL_ALRF       /*!< Alarm flag */
#define RTC_FLAG_SEC         RTC_CRL_SECF       /*!< Second flag */
#define RTC_FLAG_TAMP1F      BKP_CSR_TEF        /*!< Tamper Interrupt Flag */
````



**案例**

````c
RTC_HandleTypeDef g_rtc_handle; /* RTC控制句柄 */
_calendar_obj calendar;         /* 时钟结构体 */

// 主要为了掉电重启后，不让他初始化RTC 计数器寄存器（RTC_CNTH/RTC_CNTL）的值，初始化的话不就是和掉电丢失一样嘛。
/** 
 * @brief       RTC写入后备区域SRAM
 * @param       bkrx : 后备区寄存器编号,范围:0~41 对应 RTC_BKP_DR1~RTC_BKP_DR42
 */
void rtc_write_bkr(uint32_t bkrx, uint16_t data){
    HAL_PWR_EnableBkUpAccess(); /* 取消备份区写保护 */
    HAL_RTCEx_BKUPWrite(&g_rtc_handle, bkrx + 1, data);
}
/**
 * @brief       RTC读取后备区域SRAM
 * @param       bkrx : 后备区寄存器编号,范围:0~41对应 RTC_BKP_DR1~RTC_BKP_DR42
 */
uint16_t rtc_read_bkr(uint32_t bkrx){
    uint32_t temp = 0;
    temp = HAL_RTCEx_BKUPRead(&g_rtc_handle, bkrx + 1);
    return (uint16_t)temp; /* 返回读取到的值 */
}

/**
 *              默认尝试使用LSE,当LSE启动失败后,切换为LSI.
 *              通过BKP寄存器0的值,可以判断RTC使用的是LSE/LSI:
 *              当BKP0==0X5050时,使用的是LSE
 *              当BKP0==0X5051时,使用的是LSI
 *              注意:切换LSI/LSE将导致时间/日期丢失,切换后需重新设置.
 */
uint8_t rtc_init(void){
    /* 检查是不是第一次配置时钟 */
    uint16_t bkpflag = 0;
   
    __HAL_RCC_PWR_CLK_ENABLE(); /* 使能电源时钟 */
    __HAL_RCC_BKP_CLK_ENABLE(); /* 使能备份时钟 */
    HAL_PWR_EnableBkUpAccess(); /* 取消备份区写保护 */

    g_rtc_handle.Instance = RTC;
    g_rtc_handle.Init.AsynchPrediv = 32767; /*时钟周期设置,理论值：32767, 这里也可以用 RTC_AUTO_1_SECOND */
    g_rtc_handle.Init.OutPut = RTC_OUTPUTSOURCE_NONE;

	bkpflag = rtc_read_bkr(0);  /* 读取BKP0的值 */
    
    // 只有第一次初始化，掉电重启后，不进行初始化
    if ((bkpflag != 0X5050) && (bkpflag != 0x5051)){        /* 之前未初始化过，重新配置 */
        rtc_set_time(2020, 4, 25, 20, 25, 35);              /* 设置时间 */
    }

    __HAL_RTC_ALARM_ENABLE_IT(&g_rtc_handle, RTC_IT_SEC);   /* 允许秒中断 */
    
    HAL_NVIC_SetPriority(RTC_IRQn, 0x2, 0);                 /* 优先级设置 */
    HAL_NVIC_EnableIRQ(RTC_IRQn);                           /* 使能RTC中断通道 */
    rtc_get_time(); /* 更新时间 */
    
    return 0;
}

void HAL_RTC_MspInit(RTC_HandleTypeDef *hrtc){
    uint16_t retry = 200;
    
    __HAL_RCC_RTC_ENABLE(); /* RTC时钟使能 */

    RCC_OscInitTypeDef rcc_oscinitstruct;
    RCC_PeriphCLKInitTypeDef rcc_periphclkinitstruct;
    
    /* 使用寄存器的方式去检测LSE是否可以正常工作 */
    RCC->BDCR |= 1 << 0;    /* 开启外部低速振荡器LSE */
    
    while (retry && ((RCC->BDCR & 0X02) == 0)){  /* 等待LSE准备好 */
        retry--;
        delay_ms(5);
    }
    // 如果LSE能起作用，就用LSE，否则使用LEI 
    if (retry == 0){     /* LSE起振失败 使用LSI */
        rcc_oscinitstruct.OscillatorType = RCC_OSCILLATORTYPE_LSI;  /* 选择要配置的振荡器 */
        rcc_oscinitstruct.LSEState = RCC_LSI_ON;                    /* LSI状态：开启 */
        rcc_oscinitstruct.PLL.PLLState = RCC_PLL_NONE;              /* PLL无配置 */
        HAL_RCC_OscConfig(&rcc_oscinitstruct);                      /* 配置设置的rcc_oscinitstruct */

        rcc_periphclkinitstruct.PeriphClockSelection = RCC_PERIPHCLK_RTC;   /* 选择要配置的外设 RTC */
        rcc_periphclkinitstruct.RTCClockSelection = RCC_RTCCLKSOURCE_LSI;   /* RTC时钟源选择 LSI */
        HAL_RCCEx_PeriphCLKConfig(&rcc_periphclkinitstruct);                /* 配置设置的rcc_periphClkInitStruct */
        rtc_write_bkr(0, 0X5051);        /* 将值写入BKP */ 
    }
    else{
        rcc_oscinitstruct.OscillatorType = RCC_OSCILLATORTYPE_LSE ; /* 选择要配置的振荡器 */
        rcc_oscinitstruct.LSEState = RCC_LSE_ON;                    /* LSE状态：开启 */
        rcc_oscinitstruct.PLL.PLLState = RCC_PLL_NONE;              /* PLL不配置 */
        HAL_RCC_OscConfig(&rcc_oscinitstruct);                      /* 配置设置的rcc_oscinitstruct */
        
        rcc_periphclkinitstruct.PeriphClockSelection = RCC_PERIPHCLK_RTC;   /* 选择要配置外设 RTC */
        rcc_periphclkinitstruct.RTCClockSelection = RCC_RTCCLKSOURCE_LSE;   /* RTC时钟源选择LSE */
        HAL_RCCEx_PeriphCLKConfig(&rcc_periphclkinitstruct);                /* 配置设置的rcc_periphclkinitstruct */
        rtc_write_bkr(0, 0X5050);
    }
}

void RTC_IRQHandler(void)
{
    if (__HAL_RTC_ALARM_GET_FLAG(&g_rtc_handle, RTC_FLAG_SEC) != RESET){     /* 秒中断 */
        rtc_get_time();                         /* 更新时间 */
        __HAL_RTC_ALARM_CLEAR_FLAG(&g_rtc_handle, RTC_FLAG_SEC);            /* 清除秒中断 */
        //printf("sec:%d\r\n", calendar.sec);   /* 打印秒钟 */
    }

    /* 顺带处理闹钟标志 */
    if (__HAL_RTC_ALARM_GET_FLAG(&g_rtc_handle, RTC_FLAG_ALRAF) != RESET){   /* 闹钟标志 */
        __HAL_RTC_ALARM_CLEAR_FLAG(&g_rtc_handle, RTC_FLAG_ALRAF);          /* 清除闹钟标志 */
        printf("Alarm Time:%d-%d-%d %d:%d:%d\n", calendar.year, calendar.month, calendar.date, calendar.hour, calendar.min, calendar.sec);
    }
    __HAL_RTC_ALARM_CLEAR_FLAG(&g_rtc_handle, RTC_FLAG_OW);                 /* 清除溢出中断标志 */
    while (!__HAL_RTC_ALARM_GET_FLAG(&g_rtc_handle, RTC_FLAG_RTOFF));       /* 等待RTC寄存器操作完成, 即等待RTOFF == 1 */
}


/**
 * @brief       设置时间, 包括年月日时分秒
 *   @note      以1970年1月1日为基准, 往后累加时间
 *              合法年份范围为: 1970 ~ 2105年
                HAL默认为年份起点为2000年
 */
uint8_t rtc_set_time(uint16_t syear, uint8_t smon, uint8_t sday, uint8_t hour, uint8_t min, uint8_t sec)
{
    uint32_t seccount = 0;

    seccount = rtc_date2sec(syear, smon, sday, hour, min, sec); /* 将年月日时分秒转换成总秒钟数 */

    __HAL_RCC_PWR_CLK_ENABLE(); /* 使能电源时钟 */
    __HAL_RCC_BKP_CLK_ENABLE(); /* 使能备份域时钟 */
    HAL_PWR_EnableBkUpAccess(); /* 取消备份域写保护 */
    /* 上面三步是必须的! */
    
    RTC->CRL |= 1 << 4;         /* 允许配置 */
    
    RTC->CNTL = seccount & 0xffff;
    RTC->CNTH = seccount >> 16;
    
    RTC->CRL &= ~(1 << 4);      /* 配置更新 */

    while (!__HAL_RTC_ALARM_GET_FLAG(&g_rtc_handle, RTC_FLAG_RTOFF));       /* 等待RTC寄存器操作完成, 即等待RTOFF == 1 */

    return 0;
}

/**
 * @brief       设置闹钟, 具体到年月日时分秒
 *   @note      以1970年1月1日为基准, 往后累加时间
 *              合法年份范围为: 1970 ~ 2105年
 */
uint8_t rtc_set_alarm(uint16_t syear, uint8_t smon, uint8_t sday, uint8_t hour, uint8_t min, uint8_t sec){
    uint32_t seccount = 0;

    seccount = rtc_date2sec(syear, smon, sday, hour, min, sec); /* 将年月日时分秒转换成总秒钟数 */

    __HAL_RCC_PWR_CLK_ENABLE(); /* 使能电源时钟 */
    __HAL_RCC_BKP_CLK_ENABLE(); /* 使能备份域时钟 */
    HAL_PWR_EnableBkUpAccess(); /* 取消备份域写保护 */
    /* 上面三步是必须的! */
    
    RTC->CRL |= 1 << 4;         /* 允许配置 */
    
    RTC->ALRL = seccount & 0xffff;
    RTC->ALRH = seccount >> 16;
    
    RTC->CRL &= ~(1 << 4);      /* 配置更新 */

    while (!__HAL_RTC_ALARM_GET_FLAG(&g_rtc_handle, RTC_FLAG_RTOFF));       /* 等待RTC寄存器操作完成, 即等待RTOFF == 1 */
    return 0;
}

/**
 * @brief       得到当前的时间
 *   @note      该函数不直接返回时间, 时间数据保存在calendar结构体里面
 */
void rtc_get_time(void){
    static uint16_t daycnt = 0;
    uint32_t seccount = 0;
    uint32_t temp = 0;
    uint16_t temp1 = 0;
    const uint8_t month_table[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31}; /* 平年的月份日期表 */

    seccount = RTC->CNTH;       /* 得到计数器中的值(秒钟数) */
    seccount <<= 16;
    seccount += RTC->CNTL;

    temp = seccount / 86400;    /* 得到天数(秒钟数对应的) */

    if (daycnt != temp)         /* 超过一天了 */
    {
        daycnt = temp;
        temp1 = 1970;           /* 从1970年开始 */

        while (temp >= 365){
            if (rtc_is_leap_year(temp1)) /* 是闰年 */
            {
                if (temp >= 366){
                    temp -= 366; /* 闰年的秒钟数 */
                }
                else{
                    break;
                }
            }else{
                temp -= 365;    /* 平年 */
            }

            temp1++;
        }

        calendar.year = temp1;  /* 得到年份 */
        temp1 = 0;

        while (temp >= 28){      /* 超过了一个月 */
            if (rtc_is_leap_year(calendar.year) && temp1 == 1){ /* 当年是不是闰年/2月份 */
                if (temp >= 29){
                    temp -= 29; /* 闰年的秒钟数 */
                }
                else{
                    break;
                }
            }
            else{
                if (temp >= month_table[temp1]){
                    temp -= month_table[temp1]; /* 平年 */
                }else{
                    break;
                }
            }
            temp1++;
        }

        calendar.month = temp1 + 1; /* 得到月份 */
        calendar.date = temp + 1;   /* 得到日期 */
    }

    temp = seccount % 86400;                                                    /* 得到秒钟数 */
    calendar.hour = temp / 3600;                                                /* 小时 */
    calendar.min = (temp % 3600) / 60;                                          /* 分钟 */
    calendar.sec = (temp % 3600) % 60;                                          /* 秒钟 */
    calendar.week = rtc_get_week(calendar.year, calendar.month, calendar.date); /* 获取星期 */
}

/**
 * @brief       将年月日时分秒转换成秒钟数
 *   @note      输入公历日期得到星期(起始时间为: 公元0年3月1日开始, 输入往后的任何日期, 都可以获取正确的星期)
 *              使用 基姆拉尔森计算公式 计算, 原理说明见此贴:
 *              https://www.cnblogs.com/fengbohello/p/3264300.html
 */
uint8_t rtc_get_week(uint16_t year, uint8_t month, uint8_t day){
    uint8_t week = 0;
    if (month < 3){
        month += 12;
        --year;
    }
    week = (day + 1 + 2 * month + 3 * (month + 1) / 5 + year + (year >> 2) - year / 100 + year / 400) % 7;
    return week;
}
/**
 * @brief       将年月日时分秒转换成秒钟数
 * @note        以1970年1月1日为基准, 1970年1月1日, 0时0分0秒, 表示第0秒钟
 *              最大表示到2105年, 因为uint32_t最大表示136年的秒钟数(不包括闰年)!
 *              本代码参考只linux mktime函数, 原理说明见此贴:
 *              http://www.openedv.com/thread-63389-1-1.html
 */
static long rtc_date2sec(uint16_t syear, uint8_t smon, uint8_t sday, uint8_t hour, uint8_t min, uint8_t sec){
    uint32_t Y, M, D, X, T;
    signed char monx = smon;    /* 将月份转换成带符号的值, 方便后面运算 */

    if (0 >= (monx -= 2)){       /* 1..12 -> 11,12,1..10 */
        monx += 12;             /* Puts Feb last since it has leap day */
        syear -= 1;
    }

    Y = (syear - 1) * 365 + syear / 4 - syear / 100 + syear / 400; /* 公元元年1到现在的闰年数 */
    M = 367 * monx / 12 - 30 + 59;
    D = sday - 1;
    X = Y + M + D - 719162;                      /* 减去公元元年到1970年的天数 */
    T = ((X * 24 + hour) * 60 + min) * 60 + sec; /* 总秒钟数 */
    return T;
}

/**
 * @brief       判断年份是否是闰年
 *   @note      月份天数表:
 *              月份   1  2  3  4  5  6  7  8  9  10 11 12
 *              闰年   31 29 31 30 31 30 31 31 30 31 30 31
 *              非闰年 31 28 31 30 31 30 31 31 30 31 30 31
 * @param       year : 年份
 * @retval      0, 非闰年; 1, 是闰年;
 */
static uint8_t rtc_is_leap_year(uint16_t year)
{
    /* 闰年规则: 四年闰百年不闰，四百年又闰 */
    if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)){
        return 1;
    }else{
        return 0;
    }
}
````



# ADC数模转换

## ADC简介

* ADC（Analog-Digital Converter）模拟-数字转换器
* ADC可以将引脚上连续变化的模拟电压转换为内存中存储的数字变量，建立模拟电路到数字电路的桥梁
* 12位逐次逼近型ADC，1us转换时间
* 输入电压范围：`0~3.3V`，转换结果范围：`0~4095`
* STM32f103系列有3个ADC，精度为12位，每个ADC最多有16个外部通道。
  * 18个输入通道，可测量16个外部和2个内部信号源
  * 各通道的A/D转换可以单次、连续、扫描或间断执行
* ADC转换的结果可以左对齐或右对齐储存在16位数据寄存器中
* 规则组和注入组两个转换单元
* 模拟看门狗自动监测输入电压范围
* ADC的输入时钟不得超过14MHz，其时钟频率由PCLK2分频产生。



STM32F103C8T6 ADC资源：ADC1、ADC2，10个外部输入通道



### **ADC类型**

| ADC电路类型 | 优点             | 缺点                     |
| ----------- | ---------------- | ------------------------ |
| 并联比较型  | 转换速度最快     | 成本高、功耗高，分辨率低 |
| 逐次逼近型  | 结构简单，功耗低 | 转换速度较慢             |

**并联比较型**

![image-20230810133100517](STM32卷一.assets/image-20230810133100517.png)

假设参考电压为8V，模拟输入电压为2V，则会进入下方第二个比较器中，最终编码器输出010

**逐次逼近型**

![image-20230810133342480](STM32卷一.assets/image-20230810133342480.png)

以3位为例：数码寄存器先将高位D2置1，经过D/A转换器输出V0，比较器比较V0和模拟电压的输入，如果模拟电压大于V0，则D2位的1被锁存，否则D2位为0。再次将D2位置1，进行比较……

### ADC特性参数

* 分辨率：表示ADC能辨别的最小模拟量，用二进制位数表示，比如：8、10、12、16位等
* 转换时间：表示完成一次A/D转换所需要的时间，转换时间越短，采样率就可以越高
* 精度(物理量的精准程度)：最小刻度基础上叠加各种误差的参数，精度受ADC性能、温度和气压等影响
* 量化误差：用数字量近似表示模拟量，采用四舍五入原则，此过程产生的误差为量化误差

**各系列ADC特性**

![image-20230810133949153](STM32卷一.assets/image-20230810133949153.png)

### 转换模式

![image-20230810140133004](STM32卷一.assets/image-20230810140133004.png)

一种比较少用的模式：不连续采样模式（F1手册称为：间断模式），只适用在扫描模式下。比如：设置成2，这第一次扫描1 2通道，第二次扫描3 4通道



### 数据对齐

由于ADC为12位，而数据寄存器为32位(低16位有效)

**数据右对齐**

![image-20230707114027665](STM32卷一.assets/image-20230707114027665.png)

**数据左对齐**

![image-20230707114038191](STM32卷一.assets/image-20230707114038191.png)

###  校准

* ADC有一个内置自校准模式。校准可大幅减小因内部电容器组的变化而造成的准精度误差。校准期间，在每个电容器上都会计算出一个误差修正码(数字值)，这个码用于消除在随后的转换中每个电容器上产生的误差
* 建议在每次上电后执行一次校准
* 启动校准前， ADC必须处于关电状态超过至少两个ADC时钟周期

### 过采样

STM32F103 自带的 ADC 分辨率只有 12 位，虽然可以满足一般的应用，但是有些场合可能需要更高的分辨率，怎么办呢？可以使用外部专用的 ADC，或者换一个带更高分辨率 ADC 的主控芯片。这样做往往会增加额外的成本，那么有没有其它办法呢？答案是有的，可以通过引入过采样技术来实现。ADC 过采样技术，是利用 ADC 多次采集的方式，来提高 ADC 分辨率。 查看正点原子教学

## ADC框图

![image-20230707115925371](STM32卷一.assets/image-20230707115925371.png)

### 1. 电压输入范围

VREF+ / VREF-：ADC的参考电压

VDDA / VSS：ADC的供电电压

### 2. 输入通道

ADC的信号输入就是通过通道来实现，信号通过通道输入到单片机中，单片机经过转换后，将模拟信号输出为数字信号。STM32中的ADC有着18个输入通道，可测量16个外部和2个内部信号源



**通道选择**

| **通道** |   **ADC1**   | **ADC2** | **ADC3** |
| :------: | :----------: | :------: | :------: |
|  通道0   |     PA0      |   PA0    |   PA0    |
|  通道1   |     PA1      |   PA1    |   PA1    |
|  通道2   |     PA2      |   PA2    |   PA2    |
|  通道3   |     PA3      |   PA3    |   PA3    |
|  通道4   |     PA4      |   PA4    |   PF6    |
|  通道5   |     PA5      |   PA5    |   PF7    |
|  通道6   |     PA6      |   PA6    |   PF8    |
|  通道7   |     PA7      |   PA7    |   PF9    |
|  通道8   |     PB0      |   PB0    |   PF10   |
|  通道9   |     PB1      |   PB1    |          |
|  通道10  |     PC0      |   PC0    |   PC0    |
|  通道11  |     PC1      |   PC1    |   PC1    |
|  通道12  |     PC2      |   PC2    |   PC2    |
|  通道13  |     PC3      |   PC3    |   PC3    |
|  通道14  |     PC4      |   PC4    |          |
|  通道15  |     PC5      |   PC5    |          |
|  通道16  |  温度传感器  |          |          |
|  通道17  | 内部参考电压 |          |          |

注意：

* 通道对应的接口
* STM32F103C8T6 只有ADC1、ADC2，因为只有PA、PB，没有PC，所有只有10个外部输入通道

外部的16个通道在转换时又分为规则通道和注入通道，其中规则通道最多有16路，注入通道最多有4路（注入通道使用不多）



### 3. 转换顺序

**规则通道**
规则通道顾名思义就是，最平常的通道、也是最常用的通道，平时的ADC转换都是用规则通道实现的。

需要注意的是：规则通道最多可以同时接通16个通道，但是规则通道寄存器只能记录一个值(16位)，需要使用DMA转移数据来完成16个通道的记录

还能触发DMA



**注入通道**
注入通道是相对于规则通道的，注入通道可以在规则通道转换时，强行插入转换，相当于一个“中断通道”吧。当有注入通道需要转换时，规则通道的转换会停止，优先执行注入通道的转换，当注入通道的转换执行完毕后，再回到之前规则通道进行转换。



注意：输入通道从0开始，转换顺序从1开始





### 4. 触发源

ADC需要一个触发信号来实行模/数转换。
其一就是通过直接配置寄存器触发，通过配置控制寄存器CR2的ADON位，写1时开始转换，写0时停止转换。在程序运行过程中只要调用库函数，将CR2寄存器的ADON位置1就可以进行转换，比较好理解。
另外，还可以通过内部定时器或者外部IO触发转换，也就是说可以利用内部时钟让ADC进行周期性的转换，也可以利用外部IO使ADC在需要时转换，具体的触发由控制寄存器CR2决定。

**触发控制**

![image-20230707114000122](STM32卷一.assets/image-20230707114000122.png)

对于规则通道，选中EXTI线路11或TIM8_TRGO作为外部触发事件，可以分别通过设置ADC1和ADC2的ADC1_ETRGREG_REMAP位和ADC2_ETRGREG_REMAP位实现。

![image-20230810134645793](STM32卷一.assets/image-20230810134645793.png)



### 5.转换时间

AD转换的步骤：**采样，保持，量化，编码**

ADC的每一次信号转换都要时间，这个时间就是转换时间，转换时间由输入时钟和采样周期来决定。
**输入时钟**
由于ADC在STM32中是挂载在APB2总线上的，所以ADC得时钟是由PCLK2（72MHz）经过分频得到的，分频因子由 RCC 时钟配置寄存器RCC_CFGR 的位 15:14 ADCPRE[1:0]设置，可以是 2/4/6/8 分频，一般配置分频因子为8，即8分频得到ADC的输入时钟频率为9MHz。ADC最大时钟频率为**14MHz**
**采样周期**
采样周期是确立在输入时钟上的，配置采样周期可以确定使用多少个ADC时钟周期来对电压进行采样，采样的周期数可通过 ADC采样时间寄存器 ADC_SMPR1 和 ADC_SMPR2 中的 SMP[2:0]位设置，ADC_SMPR2 控制的是通道 0~9， ADC_SMPR1 控制的是通道 10~17。每个通道可以配置不同的采样周期，但最小的采样周期是1.5个周期，也就是说如果想最快时间采样就设置采样周期为1.5.

![image-20230810134928727](STM32卷一.assets/image-20230810134928727.png)



**转换时间**
$TCONV = 采样时间 + 12.5个ADC周期$
12.5个周期是固定的，一般我们设置 PCLK2=72M，经过 ADC 预分频器能分频到最大的时钟只能是 12M，采样周期设置为 1.5 个周期，算出最短的转换时间为 1.17us。



举个例子：ADC时钟频率为12MHz时，ADC最短的转换时间是多少？

TCONV = 采样时间 + 12.5个周期 = 1.5个周期 + 12.5个周期 = 14个周期 = (1/12000000)∗14 s = 1.17us

### 6. 数据寄存器

转换完成后的数据就存放在数据寄存器中，但数据的存放也分为规则通道转换数据和注入通道转换数据的。

**规则数据寄存器**
规则数据寄存器负责存放规则通道转换的数据，通过32位寄存器ADC_DR来存放。

当使用ADC独立模式（也就是只使用一个ADC，可以使用多个通道）时，数据存放在低16位中，当使用ADC多模式时高16位存放ADC2的数据。需要注意的是

ADC转换的精度是12位，而寄存器中有16个位来存放数据，所以要规定数据存放是左对齐还是右对齐。



当使用多个通道转换数据时，会产生多个转换数据，然鹅数据寄存器只有一个，多个数据存放在一个寄存器中会覆盖数据导致ADC转换错误，所以我们经常在一个通道转换完成之后就立刻将数据取出来，方便下一个数据存放。一般开启DMA模式将转换的数据，传输在一个数组中，程序对数组读操作就可以得到转换的结果。



**注入数据寄存器**
注入通道转换的数据寄存器有4个，由于注入通道最多有4个，所以注入通道转换的数据都有固定的存放位置，不会跟规则寄存器那样产生数据覆盖的问题。 ADC_JDRx 是 32 位的，低 16 位有效，高 16 位保留，数据同样分为左对齐和右对齐，具体是以哪一种方式存放，由ADC_CR2 的 11 位 ALIGN 设置。



### 7. 中断

![1688703114803](STM32卷一.assets/1688703114803.png)

| 中断事件               | 事件标志 | 使能控制位 |
| ---------------------- | -------- | ---------- |
| 规则通道转换结束       | EOC      | EOCIE      |
| 注入通道转换结束       | JEOC     | JEOCIE     |
| 设置了模拟看门狗状态位 | AWD      | AWDIE      |
| 溢出（F1没有）         | OVR      | OVRIE      |

**规则通道转换完成中断**
规则通道数据转换完成之后，可以产生一个中断，可以在中断函数中读取规则数据寄存器的值。这也是单通道时读取数据的一种方法。
**注入通道转换完成中断**
注入通道数据转换完成之后，可以产生一个中断，并且也可以在中断中读取注入数据寄存器的值，达到读取数据的作用。
**模拟看门狗事件**
当输入的模拟量（电压）不再阈值范围内就会产生看门狗事件，就是用来监视输入的模拟量是否正常。

以上中断的配置都由ADC_SR寄存器决定



**DMA请求**（只适用于规则组）:规则组每个通道转换结束后，除了可以产生中断外，还可以产生DMA请求，我们利用DMA及时把转换好的数据传输到指定的内存里，防止数据被覆盖。

### 8. 电压转换

要知道，转换后的数据是一个12位的二进制数，我们需要把这个二进制数代表的模拟量（电压）用数字表示出来。比如测量的电压范围是0~3.3V，转换后的二进制数是x，因为12位ADC在转换时将电压的范围大小（也就是3.3）分为4096（2^12）份，所以转换后的二进制数x代表的真实电压的计算方法就是：
$y=3.3* x / 4096$

### 简易框图

![image-20230707112230878](STM32卷一.assets/image-20230707112230878.png)

* 16个外部GPIO通道和2个内部通道
* START触发控制可以软件触发或硬件触发
* RCC CLOCK内部时钟驱动完成ADC记录，
* 规则通道最多可以同时接通16个通道，但是只能记录一个值(16位)，需要使用DMA转移数据来完成16个通道的记录
* 触发后会标记EOC
* 开关控制CMD，开启ADC
* 模拟看门狗

## 相关寄存器

**ADC控制寄存器1(ADC_CR1)**

![image-20230810140730545](STM32卷一.assets/image-20230810140730545.png)

**ADC控制寄存器2(ADC_CR2)**

![image-20230810141006945](STM32卷一.assets/image-20230810141006945.png)

**ADC 采样事件寄存器 1（ADC_SMPR1）**

![image-20230810141113091](STM32卷一.assets/image-20230810141113091.png)

**ADC 采样事件寄存器 2（ADC_SMPR2）**

![image-20230810141128889](STM32卷一.assets/image-20230810141128889.png)

ADC 采样时间设置需要由两个寄存器设置，ADC_SMPR1 和 ADC_SMPR1，分别设置通道10~17 和通道 0~9 的采样时间，每个通道用 3 个位设置。可以看出 ADC 的每个通道的采样时间是支持单独设置的。



**ADC规则序列寄存器1(ADC_SQR1)**

![image-20230810141315507](STM32卷一.assets/image-20230810141315507.png)

**ADC规则序列寄存器 2(ADC_SQR2)**

![image-20230810141346803](STM32卷一.assets/image-20230810141346803.png)

**ADC规则序列寄存器3(ADC_SQR3)**

![image-20230810141430170](STM32卷一.assets/image-20230810141430170.png)

**ADC规则数据寄存器(ADC_DR)**

![image-20230810141449237](STM32卷一.assets/image-20230810141449237.png)

**ADC状态寄存器(ADC_SR)** 

![image-20230810141624030](STM32卷一.assets/image-20230810141624030.png)

## HAL库

### 常用函数

|             函数              | 主要寄存器  |             主要功能             |
| :---------------------------: | :---------: | :------------------------------: |
|        HAL_ADC_Init()         |  CR1、CR2   |         配置ADC工作参数          |
| HAL_ADCEx_Calibration_Start() |     CR2     |             ADC校准              |
|       HAL_ADC_MspInit()       |     无      | 存放NVIC、CLOCK、GPIO初始化代码  |
|  HAL_RCCEx_PeriphCLKConfig()  |  RCC_CFGR   | 设置扩展外设时钟，如：ADC、RTC等 |
|    HAL_ADC_ConfigChannel()    | SQRx、SMPRx |    配置ADC相应通道的相关参数     |
|        HAL_ADC_Start()        |     CR2     |           启动A/D转换            |
|  HAL_ADC_PollForConversion()  |     SR      |       等待规则通道转换完成       |
|      HAL_ADC_GetValue()       |     DR      |     获取规则通道A/D转换结果      |

````c
typedef struct __ADC_HandleTypeDef{
	ADC_TypeDef *Instance; 			/* ADC 寄存器基地址 */ 
	ADC_InitTypeDef Init; 			/* ADC 参数初始化结构体变量 */ 
	DMA_HandleTypeDef *DMA_Handle; 	/* DMA 配置结构体 */
	…… 
}ADC_HandleTypeDef;
typedef struct{ 
	uint32_t DataAlign; 					/* 设置数据的对齐方式 */ 
	uint32_t ScanConvMode; 					/* 扫描模式 */ 
	FunctionalState ContinuousConvMode; 	/* 开启单次转换模式或者连续转换模式 ENABLE or DISABLE */ 	
    uint32_t NbrOfConversion; 				/* 设置转换通道数目 Min_Data = 1 and Max_Data = 16 */ 
	FunctionalState DiscontinuousConvMode; 	/* 是否使用规则通道组间断模式 ENABLE or DISABLE */ 
	uint32_t NbrOfDiscConversion; 			/* 配置间断模式的规则通道个数 Min_Data = 1 and Max_Data = 8*/ 
	uint32_t ExternalTrigConv; 				/* ADC 外部触发源选择 */ 
} ADC_InitTypeDef;
/* 设置数据的对齐方式 */ 
#define ADC_DATAALIGN_RIGHT
#define ADC_DATAALIGN_LEFT
/* 扫描模式 */ 
#define ADC_SCAN_DISABLE
#define ADC_SCAN_ENABLE
/* ADC 外部触发源选择 */ 
#define ADC_EXTERNALTRIGCONV_T1_CC1
#define ADC_EXTERNALTRIGCONV_EXT_IT11
......
#define ADC_SOFTWARE_START            /* 软件触发 */ 
 
    
typedef struct { 
	uint32_t Channel; 		/* ADC 转换通道*/ 
	uint32_t Rank; 			/* ADC 转换顺序 */ 
	uint32_t SamplingTime; 	/* ADC 采样周期 */ 
}  ADC_ChannelConfTypeDef;
/* ADC 转换通道*/ 
#define ADC_CHANNEL_0
......
#define ADC_CHANNEL_TEMPSENSOR   /* 温度 */ 
#define ADC_CHANNEL_VREFINT

/* ADC 转换顺序 */  
#define ADC_REGULAR_RANK_1 
......
    
/* ADC 采样周期 */   
#define ADC_SAMPLETIME_1CYCLE_5
......    
#define ADC_SAMPLETIME_239CYCLES_5
````

**外围时钟**

````c
HAL_StatusTypeDef HAL_RCCEx_PeriphCLKConfig(RCC_PeriphCLKInitTypeDef  *PeriphClkInit)  /* 设置外围时钟 */

typedef struct{
    uint32_t PeriphClockSelection;      /* 外围设备时钟选择 */
    uint32_t RTCClockSelection;         /* RTC时钟分频 */
    uint32_t AdcClockSelection;			/* ADC时钟分频 */
} RCC_PeriphCLKInitTypeDef;

/* 外围设备时钟选择 */
#define RCC_PERIPHCLK_RTC
#define RCC_PERIPHCLK_ADC
#define RCC_PERIPHCLK_USB
/* ADC时钟分频 */
#define RCC_ADCPCLK2_DIV2
#define RCC_ADCPCLK2_DIV4
#define RCC_ADCPCLK2_DIV6
#define RCC_ADCPCLK2_DIV8
````

### 实例

#### ADC单通道转换

````c
ADC_HandleTypeDef ADC_HandleStructure;
void ADC_Init(void){
    ADC_ChannelConfTypeDef ADC_ChConf;
    
    ADC_HandleStructure.Instance = ADC1;								/* 选择ADC1 */
    ADC_HandleStructure.Init.ContinuousConvMode = DISABLE;				/* 非连续模式 */   
    ADC_HandleStructure.Init.DataAlign = ADC_DATAALIGN_RIGHT;			/* 右对齐 */
    ADC_HandleStructure.Init.ScanConvMode = ADC_SCAN_DISABLE;			/* 非扫描模式 */
    ADC_HandleStructure.Init.NbrOfConversion = 1;						/* 使用1个通道 */
    ADC_HandleStructure.Init.DiscontinuousConvMode = DISABLE;			/* 间断模式关闭 */
    ADC_HandleStructure.Init.NbrOfDiscConversion = 0;					/* 间断模式关闭 */
    ADC_HandleStructure.Init.ExternalTrigConv = ADC_SOFTWARE_START ; 	/* 软件触发 */
    HAL_ADC_Init(&ADC_HandleStructure);
    
    HAL_ADCEx_Calibration_Start(&ADC_HandleStructure);		/* 校准 */
    
    ADC_ChConf.Channel = ADC_CHANNEL_1;						/* 通道1 PA1 */
    ADC_ChConf.Rank = ADC_REGULAR_RANK_1 ;					/* 序列1 */
    ADC_ChConf.SamplingTime = ADC_SAMPLETIME_239CYCLES_5;	/* 采样时间 */
    HAL_ADC_ConfigChannel(&ADC_HandleStructure,&ADC_ChConf);/* 初始化ADC通道 */
}
void HAL_ADC_MspInit(ADC_HandleTypeDef* hadc){
    if(hadc->Instance == ADC1){
        __HAL_RCC_GPIOA_CLK_ENABLE();
        __HAL_RCC_ADC1_CLK_ENABLE();                                  /* 使能ADC */
        
        RCC_PeriphCLKInitTypeDef RCC_PeriphInitStructure = {0};       		/* RCC配置外设时钟 */
        RCC_PeriphInitStructure.AdcClockSelection = RCC_ADCPCLK2_DIV6;		/* ADC分频 */
        RCC_PeriphInitStructure.PeriphClockSelection = RCC_PERIPHCLK_ADC;	/* 选择配置ADCADC分频 */
        HAL_RCCEx_PeriphCLKConfig(&RCC_PeriphInitStructure);				/* 初始化外围时钟 */
        
        GPIO_InitTypeDef GPIO_InitStructure;
        GPIO_InitStructure.Mode = GPIO_MODE_ANALOG;    /* 模拟输入，ADC专属 */
        GPIO_InitStructure.Pin = GPIO_PIN_1;
        GPIO_InitStructure.Pull = GPIO_PULLDOWN;
        GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH;
        HAL_GPIO_Init(GPIOA,&GPIO_InitStructure);
    }
}
uint32_t ADC_Get_Result(void){
    HAL_ADC_Start(&ADC_HandleStructure);                 // 开启ADC，即软件触发
    HAL_ADC_PollForConversion(&ADC_HandleStructure,10);  // 等待规则通道转换完成,内部等待ADC_SR->EOC位,参数2：等待转换时间
    return (uint16_t)HAL_ADC_GetValue(&ADC_HandleStructure);  // 只有低16位用到了
}
int main(void){
    HAL_Init();                         /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9); /* 设置时钟, 72Mhz */
    delay_init(72);                     /* 延时初始化 */
    usart_init(115200);                 /* 串口初始化为115200 */
    
    lcd_init();                         /* 初始化LCD */
    ADC_Init();
    
    lcd_show_string(30, 110, 200, 16, 16, "ADC1_CH1_VAL:", RED);
    lcd_show_string(30, 130, 200, 16, 16, "ADC1_CH1_VOL:0.000V", BLUE); /* 先在固定位置显示小数点 */
    int16_t adcnum;
    float temp;
    while (1){
        adcnum = ADC_Get_Result();
        lcd_show_xnum(134, 110, adcnum, 5, 16, 0, BLUE);    /* 显示ADCValue */
        
        temp = (float)adcnum * (3.3 / 4096);	/* 计算电压 */
        adcnum = temp;							/* 显示整数，float转到int会将小数位舍弃 */		
        lcd_show_xnum(134, 130, adcnum, 1, 16, 0, BLUE);
        
        temp -=adcnum;							/* 显示小数 */
        temp *= 1000;
        lcd_show_xnum(150, 130, temp, 3, 16, 0X80, BLUE);
    }
}
````



## 标准库

### 常用函数

````c
//在stm32f10x_rcc.h下，配置ADC时钟分频
/**
  * @brief  Configures the ADC clock (ADCCLK).
  * @param  RCC_PCLK2: defines the ADC clock divider. This clock is derived from 
  *   the APB2 clock (PCLK2).
  *   This parameter can be one of the following values:
  *     @arg RCC_PCLK2_Div2: ADC clock = PCLK2/2
  *     @arg RCC_PCLK2_Div4: ADC clock = PCLK2/4
  *     @arg RCC_PCLK2_Div6: ADC clock = PCLK2/6
  *     @arg RCC_PCLK2_Div8: ADC clock = PCLK2/8
  * @retval None
  */
void RCC_ADCCLKConfig(uint32_t RCC_PCLK2);
````

````c
void ADC_DeInit(ADC_TypeDef* ADCx);
void ADC_Init(ADC_TypeDef* ADCx, ADC_InitTypeDef* ADC_InitStruct);       // 初始化函数
void ADC_StructInit(ADC_InitTypeDef* ADC_InitStruct);
void ADC_Cmd(ADC_TypeDef* ADCx, FunctionalState NewState);               // 使能函数
void ADC_DMACmd(ADC_TypeDef* ADCx, FunctionalState NewState);            // DMA使能
void ADC_ITConfig(ADC_TypeDef* ADCx, uint16_t ADC_IT, FunctionalState NewState);  // 中断使能

// 校准
void ADC_ResetCalibration(ADC_TypeDef* ADCx);                            // 复位校准
FlagStatus ADC_GetResetCalibrationStatus(ADC_TypeDef* ADCx);             // 获得复位校准标准位，SET为正在复位校准
void ADC_StartCalibration(ADC_TypeDef* ADCx);                            // 开始校准
FlagStatus ADC_GetCalibrationStatus(ADC_TypeDef* ADCx);                  // 获得校准标志位，SET表示正在开始校准

// 软甲触发
void ADC_SoftwareStartConvCmd(ADC_TypeDef* ADCx, FunctionalState NewState);  // 软件转换函数
FlagStatus ADC_GetSoftwareStartConvStatus(ADC_TypeDef* ADCx);
void ADC_DiscModeChannelCountConfig(ADC_TypeDef* ADCx, uint8_t Number);
void ADC_DiscModeCmd(ADC_TypeDef* ADCx, FunctionalState NewState);
// 规则通道配置函数
void ADC_RegularChannelConfig(ADC_TypeDef* ADCx, uint8_t ADC_Channel, uint8_t Rank, uint8_t ADC_SampleTime);
void ADC_ExternalTrigConvCmd(ADC_TypeDef* ADCx, FunctionalState NewState);
uint16_t ADC_GetConversionValue(ADC_TypeDef* ADCx);                          // 获取转换结果函数
uint32_t ADC_GetDualModeConversionValue(void);
void ADC_AutoInjectedConvCmd(ADC_TypeDef* ADCx, FunctionalState NewState);
void ADC_InjectedDiscModeCmd(ADC_TypeDef* ADCx, FunctionalState NewState);
void ADC_ExternalTrigInjectedConvConfig(ADC_TypeDef* ADCx, uint32_t ADC_ExternalTrigInjecConv);
void ADC_ExternalTrigInjectedConvCmd(ADC_TypeDef* ADCx, FunctionalState NewState);
void ADC_SoftwareStartInjectedConvCmd(ADC_TypeDef* ADCx, FunctionalState NewState);
FlagStatus ADC_GetSoftwareStartInjectedConvCmdStatus(ADC_TypeDef* ADCx);
void ADC_InjectedChannelConfig(ADC_TypeDef* ADCx, uint8_t ADC_Channel, uint8_t Rank, uint8_t ADC_SampleTime);
void ADC_InjectedSequencerLengthConfig(ADC_TypeDef* ADCx, uint8_t Length);
void ADC_SetInjectedOffset(ADC_TypeDef* ADCx, uint8_t ADC_InjectedChannel, uint16_t Offset);
uint16_t ADC_GetInjectedConversionValue(ADC_TypeDef* ADCx, uint8_t ADC_InjectedChannel);
// 看门狗
void ADC_AnalogWatchdogCmd(ADC_TypeDef* ADCx, uint32_t ADC_AnalogWatchdog);
void ADC_AnalogWatchdogThresholdsConfig(ADC_TypeDef* ADCx, uint16_t HighThreshold, uint16_t LowThreshold);
void ADC_AnalogWatchdogSingleChannelConfig(ADC_TypeDef* ADCx, uint8_t ADC_Channel);
void ADC_TempSensorVrefintCmd(FunctionalState NewState);

FlagStatus ADC_GetFlagStatus(ADC_TypeDef* ADCx, uint8_t ADC_FLAG);           //获取标志位状态
void ADC_ClearFlag(ADC_TypeDef* ADCx, uint8_t ADC_FLAG);
ITStatus ADC_GetITStatus(ADC_TypeDef* ADCx, uint16_t ADC_IT);
void ADC_ClearITPendingBit(ADC_TypeDef* ADCx, uint16_t ADC_IT);
````

````C
/**
  * 配置通道
  * @param  ADCx: ADC1~3
  * @param  ADC_Channel: 选择通道 ADC_Channel_0~17
  * @param  Rank: 存放的序列位置 1~16
  * @param  ADC_SampleTime: 通道采样时间
  */
void ADC_RegularChannelConfig(ADC_TypeDef* ADCx, uint8_t ADC_Channel, uint8_t Rank, uint8_t ADC_SampleTime)
````

````c
typedef struct{
 uint32_t ADC_Mode;                // ADC 工作模式选择
 FunctionalState ADC_ScanConvMode; // ADC 扫描（多通道）或者单次（单通道）模式选择 ，ENABLE 扫描模式，DISABLE 非扫描模式
 FunctionalState ADC_ContinuousConvMode; // ADC 单次转换或者连续转换选择，ENABLE 连续模式，DISABLE 单次模式
 uint32_t ADC_ExternalTrigConv;    // ADC 外部转换触发信号选择
 uint32_t ADC_DataAlign;           // ADC 数据寄存器对齐格式
 uint8_t ADC_NbrOfChannel;         // ADC 采集通道数，from 1 to 16；非扫描模式为1
} ADC_InitTypeDef;
````

````c
//ADC_Mode参数： ADC 工作模式选择
#define ADC_Mode_Independent                       ((uint32_t)0x00000000)       // 独立模式         
#define ADC_Mode_RegInjecSimult                    ((uint32_t)0x00010000)       // 以下为双ADC模式
#define ADC_Mode_RegSimult_AlterTrig               ((uint32_t)0x00020000)
#define ADC_Mode_InjecSimult_FastInterl            ((uint32_t)0x00030000)
#define ADC_Mode_InjecSimult_SlowInterl            ((uint32_t)0x00040000)
#define ADC_Mode_InjecSimult                       ((uint32_t)0x00050000)
#define ADC_Mode_RegSimult                         ((uint32_t)0x00060000)
#define ADC_Mode_FastInterl                        ((uint32_t)0x00070000)
#define ADC_Mode_SlowInterl                        ((uint32_t)0x00080000)
#define ADC_Mode_AlterTrig                         ((uint32_t)0x00090000)

//ADC_DataAlign参数：ADC 数据寄存器对齐格式
#define ADC_DataAlign_Right                        ((uint32_t)0x00000000)       // 右对齐
#define ADC_DataAlign_Left                         ((uint32_t)0x00000800)       //左对齐

//ADC_ExternalTrigConv参数：外部触发源选择
#define ADC_ExternalTrigConv_T1_CC1                ((uint32_t)0x00000000)
#define ADC_ExternalTrigConv_T1_CC2                ((uint32_t)0x00020000) 
#define ADC_ExternalTrigConv_T2_CC2                ((uint32_t)0x00060000)
#define ADC_ExternalTrigConv_T3_TRGO               ((uint32_t)0x00080000)
#define ADC_ExternalTrigConv_T4_CC4                ((uint32_t)0x000A0000)
#define ADC_ExternalTrigConv_Ext_IT11_TIM8_TRGO    ((uint32_t)0x000C0000)

#define ADC_ExternalTrigConv_T1_CC3                ((uint32_t)0x00040000)
#define ADC_ExternalTrigConv_None                  ((uint32_t)0x000E0000)     // 不使用外部触发，（使用软件触发）

#define ADC_ExternalTrigConv_T3_CC1                ((uint32_t)0x00000000)
#define ADC_ExternalTrigConv_T2_CC3                ((uint32_t)0x00020000) 
#define ADC_ExternalTrigConv_T8_CC1                ((uint32_t)0x00060000)
#define ADC_ExternalTrigConv_T8_TRGO               ((uint32_t)0x00080000) 
#define ADC_ExternalTrigConv_T5_CC1                ((uint32_t)0x000A0000)
#define ADC_ExternalTrigConv_T5_CC3                ((uint32_t)0x000C0000) 
````

### 实例

**ADC一般步骤**

* 实例要求：利用ADC1的通道1（PA1）采集外部电压值。
* 开启PA口时钟和ADC1时钟，设置PA1为模拟输入。调用函数：GPIO_Init()；APB2PeriphClockCmd()；
* 复位ADC1，同时设置ADC1分频因子。调用函数：ADC_DeInit(ADC1)；RCC_ADCCLKConfig(RCC_PCLK2_Div6)；
* 初始化ADC1参数，设置ADC1的工作模式以及规则序列的相关信息。调用函数：void ADC_Init()；
* 使能ADC并校准。调用函数：ADC_Cmd()；
* 配置规则通道参数。调用函数：ADC_RegularChannelConfig()；
* 开启软件转换：ADC_SoftwareStartConvCmd(ADC1)；
* 等待转换完成，读取ADC值。调用函数：ADC_GetConversionValue(ADC1)。

#### AD单通道转换

````c
void AD_Init(void){
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_ADC1, ENABLE);
	
	RCC_ADCCLKConfig(RCC_PCLK2_Div6);              //ADCCLK = 72MHz / 6 = 12MHz
	
	GPIO_InitTypeDef GPIO_InitSturcture;
	GPIO_InitSturcture.GPIO_Mode = GPIO_Mode_AIN;  //模拟输入模式，ADC的专属模式，断开GPIO口的输入输出对模拟电压照成的干扰
	GPIO_InitSturcture.GPIO_Pin = GPIO_Pin_0;
	GPIO_InitSturcture.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitSturcture);
	
    //重要
	ADC_RegularChannelConfig(ADC1, ADC_Channel_0, 1,ADC_SampleTime_55Cycles5);   //使用通道1，放到序列1位置，采样时间55
	//ADC_RegularChannelConfig(ADC1, ADC_Channel_1, 2,ADC_SampleTime_55Cycles5); //使用通道2，放到序列2位置，采样时间55
	
	ADC_InitTypeDef ADC_InitStructure;
	ADC_InitStructure.ADC_Mode = ADC_Mode_Independent;        // 独立模式
	ADC_InitStructure.ADC_DataAlign = ADC_DataAlign_Right;    // 右对齐
	ADC_InitStructure.ADC_ExternalTrigConv = ADC_ExternalTrigConv_None;   //不使用外部触发
	ADC_InitStructure.ADC_ContinuousConvMode = DISABLE;       //单此触发
	ADC_InitStructure.ADC_ScanConvMode = DISABLE;             //非连续扫描
	ADC_InitStructure.ADC_NbrOfChannel = 1;                   //1号通道
	ADC_Init(ADC1, &ADC_InitStructure);
	
    ADC_Cmd(ADC1,ENABLE);
	
	ADC_ResetCalibration(ADC1);        // 复位校准
	while(ADC_GetResetCalibrationStatus(ADC1) == SET);    //返回复位校准状态，为SET则表示正在初始化校准寄存器
	ADC_StartCalibration(ADC1);        // 开始校准
	while(ADC_GetCalibrationStatus(ADC1) == SET);          //返回校准状态，为SET则表示正在开始校准
    
    //软件触发，连续触发，因为本段所在的函数AD_Init()只会调用一次
    //ADC_SoftwareStartConvCmd(ADC1, ENABLE);                
}

uint16_t Get_Value(void){
	ADC_SoftwareStartConvCmd(ADC1, ENABLE);        // 软件触发，如果是连续触发，则这一行可以只执行一次，可放在AD_Init函中
	while(ADC_GetFlagStatus(ADC1, ADC_FLAG_EOC) == RESET);  // 获得EOC标志位状态
	return ADC_GetConversionValue(ADC1);
}
//--------------------------------------------------------------------------------------------

uint16_t ADValue;
float Voltage;

int main(void)
{	
	OLED_Init();
	AD_Init();
	
	OLED_ShowString(1, 1, "ADValue:");
	OLED_ShowString(2, 1, "Volatge:0.00V");
	while(1){
		ADValue =Get_Value();
		Voltage = (float)ADValue / 4095 * 3.3;
		
		OLED_ShowNum(1, 9, ADValue, 4);
		
		OLED_ShowNum(2, 9, Voltage, 1);                              //显示整数
		OLED_ShowNum(2, 11, (uint16_t)(Voltage * 100) % 100, 2);     //显示小数
		Delay_ms(100);
	}	
}
````

#### AD多通道转换

使用规则通道，会掩盖数据，由于没有DMA转移数据，可以采用其他方式

使用函数`void ADC_RegularChannelConfig(ADC_TypeDef* ADCx, uint8_t ADC_Channel, uint8_t Rank, uint8_t ADC_SampleTime)`更改参数2，选择不同的通道

````c
//其他代码与上方代码相似
//每次调用这个函数可以选择不同的通道
uint16_t Get_Value(uint8_t ADC_Channel){
    //使用main函数传递来的通道，放到序列1位置，采样时间55
	ADC_RegularChannelConfig(ADC1, ADC_Channel, 1,ADC_SampleTime_55Cycles5);  
	
	ADC_SoftwareStartConvCmd(ADC1, ENABLE); // 软件触发，如果是连续触发，则这一行可以只执行一次，可放在AD_Init函中
	while(ADC_GetFlagStatus(ADC1, ADC_FLAG_EOC) == RESET);  // 获得EOC标志位状态
	return ADC_GetConversionValue(ADC1);
}
uint16_t AD1;
uint16_t AD2;
uint16_t AD3;
uint16_t AD4;
int main(void)
{	
	OLED_Init();
	AD_Init();
	
	OLED_ShowString(1, 1, "AD1:");
	OLED_ShowString(2, 1, "AD2:");
	OLED_ShowString(3, 1, "AD3:");
	OLED_ShowString(4, 1, "AD4:");

	while(1){
        //选择不同的通道
		AD1 = Get_Value(ADC_Channel_0);  //选择通道1
		AD2 = Get_Value(ADC_Channel_1);  //选择通道2
		AD3 = Get_Value(ADC_Channel_2);
		AD4 = Get_Value(ADC_Channel_3);
		
		OLED_ShowNum(1,4,AD1,4);
		OLED_ShowNum(2,4,AD2,4);
		OLED_ShowNum(3,4,AD3,4);
		OLED_ShowNum(4,4,AD4,4);
	}	
}
````

## 内部温度

![image-20230810201331106](STM32卷一.assets/image-20230810201331106.png)

![image-20230810201451786](STM32卷一.assets/image-20230810201451786.png)

**代码**

````c
ADC_HandleTypeDef ADCTemp_HandleStructure;
void ADCTemp_Init(void){
    ADC_ChannelConfTypeDef ADC_ChConf;
  
    ADCTemp_HandleStructure.Instance = ADC1;
    ADCTemp_HandleStructure.Init.ContinuousConvMode = DISABLE;
    ADCTemp_HandleStructure.Init.DataAlign = ADC_DATAALIGN_RIGHT;
    ADCTemp_HandleStructure.Init.ScanConvMode = ADC_SCAN_DISABLE;
    ADCTemp_HandleStructure.Init.NbrOfConversion = 1;
    ADCTemp_HandleStructure.Init.DiscontinuousConvMode = DISABLE;
    ADCTemp_HandleStructure.Init.NbrOfDiscConversion = 0;
    ADCTemp_HandleStructure.Init.ExternalTrigConv = ADC_SOFTWARE_START ;
    
    HAL_ADC_Init(&ADCTemp_HandleStructure);
    
    HAL_ADCEx_Calibration_Start(&ADCTemp_HandleStructure);
    
    ADC_ChConf.Channel = ADC_CHANNEL_16;                   // 通道16 内部温度
    ADC_ChConf.Rank = ADC_REGULAR_RANK_1 ;                 // 序列1
    ADC_ChConf.SamplingTime = ADC_SAMPLETIME_239CYCLES_5;  // 采样时间
    HAL_ADC_ConfigChannel(&ADCTemp_HandleStructure,&ADC_ChConf);
}
void HAL_ADC_MspInit(ADC_HandleTypeDef* hadc){
    if(hadc->Instance == ADC1){
        __HAL_RCC_ADC1_CLK_ENABLE(); 
        RCC_PeriphCLKInitTypeDef RCC_PeriphInitStructure = {0};             // RCC配置外设时钟
        RCC_PeriphInitStructure.AdcClockSelection = RCC_ADCPCLK2_DIV6;     // ADC分频
        RCC_PeriphInitStructure.PeriphClockSelection = RCC_PERIPHCLK_ADC;  // 选择配置ADC
        HAL_RCCEx_PeriphCLKConfig(&RCC_PeriphInitStructure);
    }
}
uint32_t ADC_Get_Result(void){
    HAL_ADC_Start(&ADCTemp_HandleStructure);                 // 开启ADC
    // 等待规则通道转换完成,内部等待ADC_SR->EOC位,参数2：等待转换时间
    HAL_ADC_PollForConversion(&ADCTemp_HandleStructure,10);  
    return (uint16_t)HAL_ADC_GetValue(&ADCTemp_HandleStructure);  // 只有低16位用到了
}
uint32_t ADC_GetTemp(void){
    uint32_t adcx;
    double temperature;
    
    adcx = ADC_Get_Result();          // 获得上方函数的ADC_GetValue
    
    temperature = adcx * (3.3 / 4096);// 计数电压
    temperature = (1.43 - temperature) / 0.0043 +25; // 计数温度
    return temperature * 100; // 扩大100倍，方便显示
}
int main(void){
    HAL_Init();                         /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9); /* 设置时钟, 72Mhz */
    delay_init(72);                     /* 延时初始化 */
    usart_init(115200);                 /* 串口初始化为115200 */
    lcd_init();                         /* 初始化LCD */
	ADCTemp_Init();						/* 初始化ADC */

    lcd_show_string(30, 120, 200, 16, 16, "TEMPERATE: 00.00C", RED);
    int32_t temper;
    while(1){
        temper = ADC_GetTemp();
        lcd_show_xnum(30 + 11 * 8, 120, temper / 100, 2, 16, 0, BLUE);    /* 显示整数部分 */
        lcd_show_xnum(30 + 14 * 8, 120, temper % 100, 2, 16,0X80, BLUE);  /* 显示小数部分 */
    }
}
````



# DAC

## DAC简介

* DAC，全称：Digital-to-Analog Converter，指数字/模拟转换器
* 2 个 DAC 转换器：每个转换器对应 1 个输出通道
* 8 位或者 12 位单调输出
* 12 位模式下数据左对齐或者右对齐
* 同步更新功能
* 噪声\三角波形生成
* 双 DAC 双通道同时或者分别转换
* 每个通道都有 DMA 功能
* DAC供电电源：VSSA、 VDDA （2.4V≤VDDA≤3.6V ）
* DAC输出电压范围：VREF–≤VOUT≤VREF+（即0V≤VOUT≤3.3V ）
* 在精度要求不高的场合，可以用一种廉价的解决方案实现DAC输出：PWM + RC滤波器

### **DAC特性参数**

* 分辨率：表示模拟电压的最小增量，常用二进制位数表示，比如：8、12位等
* 建立时间：表示将一个数字量转换为稳定模拟信号所需的时间
* 精度：转换器实际特性曲线与理想特性曲线之间的最大偏差（误差源：比例系统误差、失调误差、非线性误差 原因：元件参数误差、基准电压不稳定、运算放大器零漂等）

**各系列DAC特性**

![image-20230811113519726](STM32卷一.assets/image-20230811113519726.png)

### DAC数据格式

![image-20230811114444712](STM32卷一.assets/image-20230811114444712.png)

![image-20230811114732788](STM32卷一.assets/image-20230811114732788.png)

### 触发源

三种触发转换的方式：自动触发、软件触发、外部事件触发

![image-20230811114837919](STM32卷一.assets/image-20230811114837919.png)

![image-20230811115252786](STM32卷一.assets/image-20230811115252786.png)



如果没有选中硬件触发（寄存器 DAC_CR 的 TENx 位置 0），存入寄存器 DAC_DHRx 的数据会在1个APB1时钟周期后自动传至寄存器DAC_DORx。如果选中硬件触发（寄存器DAC_CR的 TENx 位置 1），数据传输在触发发生以后 3 个 APB1 时钟周期后完成。一旦数据从 DAC_DHRx寄存器装入 DAC_DORx 寄存器，在经过时间 tSETTLING 之后，输出即有效，这段时间的长短依电源电压和模拟输出负载的不同会有所变化。tSETTLING 的典型值为 3us，最大是 4us



**不使用硬件触发（TEN=0），其转换的时间框图**

可以看到经过了一个APB1时钟周期，DHR将数据转移到DOR寄存器上，DOR经过Tsettling建立后进行输出

![image-20230811115018519](STM32卷一.assets/image-20230811115018519.png)

### **DAC输出电压**

12位模式下，DAC输出电压计算方法：DAC输出电压 = ( DORx / 4096 ) ∗ VREF+     DORx为数据保持寄存器的值，VREF+为参考电压

8位模式下，DAC输出电压计算方法：DAC输出电压 = ( DORx / 256 ) ∗ VREF+





## DAC框图

![image-20230811113611618](STM32卷一.assets/image-20230811113611618.png)

1. 参考电压/模拟部分电压
2. DA转换器
3. 输出通道
4. 数据输出寄存器
5. 数据保持寄存器
6. 控制逻辑(噪声波/三角波)
7. DAC控制寄存器
8. 触发源：可以是自动触发，软件触发，外部事件触发

如：外部中断触发后，DAC控制寄存器输出到 控制逻辑 最终将 数据保持寄存器的值 转移到 数据输出寄存器，数据输出寄存器 到 DA转换器，DA转换器输出

## 相关寄存器

**DAC 控制寄存器（DAC_CR）**

![image-20230811115600162](STM32卷一.assets/image-20230811115600162.png)

DAC_CR 的低 16 位用于控制通道 1，高 16 位用于控制通道 2



**DAC 通道 1 12 位右对齐数据保持寄存器（DAC_DHR12R1）**

![1691726287633](STM32卷一.assets/1691726287633.png)

该寄存器用来设置 DAC 输出，通过写入 12 位数据到该寄存器

## HAL库

### 常用函数

|          函数           | 主要寄存器  |             主要功能             |
| :---------------------: | :---------: | :------------------------------: |
|     HAL_DAC_Init()      |     无      | 配置DAC工作状态（HAL库内部使用） |
|    HAL_DAC_MspInit()    |     无      | 存放NVIC、CLOCK、GPIO初始化代码  |
| HAL_DAC_ConfigChannel() |     CR      |    配置DAC相应通道的相关参数     |
|     HAL_DAC_Start()     | CR、SWTRIGR |           启动D/A转换            |
|   HAL_DAC_SetValue()    |   DHR12Rx   |          设置输出数字量          |
|   HAL_DAC_GetValue()    |    DORx     |        读取通道输出数字量        |

````c
typedef struct { 
	DAC_TypeDef *Instance; 				/* DAC 寄存器基地址 */
 	__IO HAL_DAC_StateTypeDef State; 	/* DAC 工作状态 */
 	HAL_LockTypeDef Lock; 				/* DAC 锁定对象 */
 	DMA_HandleTypeDef *DMA_Handle1; 	/* 通道 1 的 DMA 处理句柄指针 */
 	DMA_HandleTypeDef *DMA_Handle2; 	/* 通道 2 的 DMA 处理句柄指针 */
 	__IO uint32_t ErrorCode; 			/* DAC 错误代码 */ 
} DAC_HandleTypeDef
typedef struct {
 	uint32_t DAC_Trigger; 				/* DAC 触发源的选择 */
 	uint32_t DAC_OutputBuffer; 			/* 启用或者禁用 DAC 通道输出缓冲区 */
} DAC_ChannelConfTypeDef;
/* DAC 触发源的选择 */
#define DAC_TRIGGER_NONE				/* 自动触发 */
#define DAC_TRIGGER_T6_TRGO				/* 定时器触发 */
#define DAC_TRIGGER_T7_TRGO
#define DAC_TRIGGER_T2_TRGO
#define DAC_TRIGGER_T4_TRGO
#define DAC_TRIGGER_EXT_IT9				/* 中断触发 */
#define DAC_TRIGGER_SOFTWARE			/* 软件触发 */

/* 启用或者禁用 DAC 通道输出缓冲区 */
#define DAC_OUTPUTBUFFER_ENABLE			/* 使用缓冲区 */
#define DAC_OUTPUTBUFFER_DISABLE		/* 不使用缓冲区 */

/**
*	参数1：DAC句柄
*	参数2：DAC通道初始化
*	参数3：
*		DAC_CHANNEL_1: DAC Channel1 selected
*		DAC_CHANNEL_2: DAC Channel2 selected
**/
HAL_StatusTypeDef HAL_DAC_ConfigChannel(DAC_HandleTypeDef *hdac, DAC_ChannelConfTypeDef *sConfig, uint32_t Channel)
/**
*	参数1：DAC句柄
*	参数2：
*		DAC_CHANNEL_1: DAC Channel1 selected
*		DAC_CHANNEL_2: DAC Channel2 selected
**/
HAL_StatusTypeDef HAL_DAC_Start(DAC_HandleTypeDef *hdac, uint32_t Channel)

    
/**	 设置输出数字量 
*	参数3：
*       DAC_ALIGN_8B_R: 8位
*       DAC_ALIGN_12B_L: 12位左对齐
*       DAC_ALIGN_12B_R: 12位右对齐
**/
HAL_StatusTypeDef HAL_DAC_SetValue(DAC_HandleTypeDef *hdac, uint32_t Channel, uint32_t Alignment, uint32_t Data)
````







### 案例

#### 案例1

在DAC1通道1(PA4) 输出设定电压

````c
DAC_HandleTypeDef DAC_HandleStructure;
void DAC_Init(void){
    DAC_ChannelConfTypeDef DAC_ChannelConf;
    
    DAC_HandleStructure.Instance = DAC1;                   /* F1只有1个DAC，所以直接写DAC也行 */
    HAL_DAC_Init(&DAC_HandleStructure);
    
    DAC_ChannelConf.DAC_Trigger = DAC_TRIGGER_NONE;                 /* 触发方式，自动触发 */  
    DAC_ChannelConf.DAC_OutputBuffer =  DAC_OUTPUTBUFFER_DISABLE;   /* 不使用缓冲 */
    HAL_DAC_ConfigChannel(&DAC_HandleStructure,&DAC_ChannelConf,DAC_CHANNEL_1);      /* 初始化DAC1的通道1，PA4 */
    
    HAL_DAC_Start(&DAC_HandleStructure,DAC_CHANNEL_1);
}
void HAL_DAC_MspInit(DAC_HandleTypeDef *hdac){
    if(hdac->Instance == DAC1){
        __HAL_RCC_GPIOA_CLK_ENABLE();
        __HAL_RCC_DAC_CLK_ENABLE();
        
        GPIO_InitTypeDef GPIO_InitStructure;
        GPIO_InitStructure.Mode = GPIO_MODE_ANALOG;                 /* 模拟 */
        GPIO_InitStructure.Pin = GPIO_PIN_4;                        /* DAC_Channel1 复用在PA4上 */
        GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH;
        
        HAL_GPIO_Init(GPIOA,&GPIO_InitStructure);     
    }

}
void DAC_SetValue(float v){
    v = v * 4096 / 3.3;      /* DORx = DAC输出电压* 4096 / 3.3V */
    HAL_DAC_SetValue(&DAC_HandleStructure,DAC_CHANNEL_1,DAC_ALIGN_12B_R,v);  /* DAC1通道1,12位右对齐 */
}
int main(void){
    HAL_Init();                         /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9); /* 设置时钟, 72Mhz */
    delay_init(72);                     /* 延时初始化 */
    usart_init(115200);                 /* 串口初始化为115200 */
    led_init();                         /* 初始化LED */
    lcd_init();                         /* 初始化LCD */
    
    DAC_Init();
    DAC_SetValue(2.2);					/* 设置输出电压*/
    while(1){
    }
}
````











# DMA

## DMA简介

* DMA（Direct Memory Access）直接存储器存取

* DMA传输将数据从一个地址空间复制到另一个地址空间，提供在外设和存储器之间或者存储器和存储器之间的高速数据传输，无须CPU干预，节省了CPU的资源

* 12个独立可配置的通道： DMA1（7个通道）， DMA2（5个通道）

* 每个通道都支持软件触发和特定的硬件触发


STM32F103C8T6 DMA资源：DMA1（7个通道）



**DMA传输方式**
DMA的作用就是实现数据的直接传输，而去掉了传统数据传输需要CPU寄存器参与的环节，主要涉及四种情况的数据传输，但本质上是一样的，都是从内存的某一区域传输到内存的另一区域（外设的数据寄存器本质上就是内存的一个存储单元）。四种情况的数据传输如下：

* 外设到内存
* 内存到外设
* 内存到内存
* 外设到外设



**DMA传输参数**

涉及源地址、目标地址、传输数据量这三个，DMA控制器就会启动数据传输，当剩余传输数据量为0时 达到传输终点，结束DMA传输 ，当然，DMA 还有循环传输模式 当到达传输终点时会重新启动DMA传输。
也就是说只要剩余传输数据量不是0，而且DMA是启动状态，那么就会发生数据传输。



**DMA的主要特征**
每个通道都直接连接专用的硬件DMA请求，每个通道都同样支持软件触发。这些功能通过软件来配置；

* 在同一个DMA模块上，多个请求间的优先权可以通过软件编程设置（共有四级：很高、高、中等和低），优先权设置相等时由硬件决定（请求0优先于请求1，依此类推）；
* 独立数据源和目标数据区的传输宽度（字节8、半字16、全字32），模拟打包和拆包的过程。源和目标地址必须按数据传输宽度对齐；
* 支持循环的缓冲器管理；
* 每个通道都有3个事件标志（DMA半传输、DMA传输完成和DMA传输出错），这3个事件标志逻辑或成为一个单独的中断请求；
* 存储器和存储器间的传输、外设和存储器、存储器和外设之间的传输；
* 闪存、SRAM、外设的SRAM、APB1、APB2和AHB外设均可作为访问的源和目标；
* 可编程的数据传输数目：最大为65535。

## 存储器映像

| **类型** | **起始地址** |   **存储器**    |             **用途**             |
| :------: | :----------: | :-------------: | :------------------------------: |
|   ROM    | 0x0800 0000  | 程序存储器Flash |    存储C语言编译后的程序代码     |
|   ROM    | 0x1FFF F000  |   系统存储器    |   存储BootLoader，用于串口下载   |
|   ROM    | 0x1FFF F800  |    选项字节     | 存储一些独立于程序代码的配置参数 |
|   RAM    | 0x2000 0000  |  运行内存SRAM   |     存储运行过程中的临时变量     |
|   RAM    | 0x4000 0000  |   外设寄存器    |      存储各个外设的配置参数      |
|   RAM    | 0xE000 0000  | 内核外设寄存器  |    存储内核各个外设的配置参数    |

0x1FFF F800 选项字节：可以配置读保护

**关于BootLoader**

小知识：只要将 C语言编译后的程序代码 放到0x0800 0000地址的存储器中，STM32就会执行此程序。可以使用串口通信 + 烧录软件完成下载，这就需要BootLoader作为加载程序，加载想要通过串口下载的程序了

![image-20230709173132861](STM32卷一.assets/image-20230709173132861.png)

* 当BOOT0为0时 在0x0800 0000地址运行，启动主程序
* 当BOOT1为0，当BOOT0为1时，在0x1FFF F000地址运行，启动厂家编写的BootLoader,BootLoader最终引导至0x0800 0000；(串口下载就是用的这个)

![image-20231025141056428](STM32卷一.assets/image-20231025141056428.png)







**熟悉存放机制**

````c
#define ADC_DR         (uint32_t *)0x4001244C 
uint8_t x;
uint32_t x2;
const uint8_t cx;      //常量

int main(void){	
	OLED_Init();
	
	OLED_ShowHexNum(1,1,(uint32_t)&x,8);             // 20000000       变量存储在SRAM中
	OLED_ShowHexNum(2,1,(uint32_t)&x2,8);            // 20000004       32位占4个字节
	
	OLED_ShowHexNum(3,1,(uint32_t)&cx,8);            // 08000838       因为cx为常量，存储在Flash中
	
	OLED_ShowHexNum(4,1,(uint32_t)&ADC1->DR,8);      // 4001244C       外设寄存器，地址固定
	
	//查询数据手册，DR偏移4C
	//#define ADC1                ((ADC_TypeDef *) ADC1_BASE)
	//#define ADC1_BASE           (APB2PERIPH_BASE + 0x2400)
	//#define APB2PERIPH_BASE     (PERIPH_BASE + 0x10000)
	//#define PERIPH_BASE         ((uint32_t)0x40000000)
	//4001244C  = 0x40000000 + 0x10000 + 0x2400 + 4C
	
    //使用自己定义的 *ADC_DR也可以访问到ADC的DR
	while(1){
	}
}
````

## DMA框图

### 基本介绍

![image-20230809162125038](STM32卷一.assets/image-20230809162125038.png)



上方的框图，我们可以看到STM32内核，存储器，外设及DMA的连接，这些硬件最终通过各种各样的线连接到总线矩阵中，硬件结构之间的数据转移都经过总线矩阵的协调，使各个外设和谐的使用总线来传输数据。



注意：**用的是AHB**

* AHB(Advanced High-performance Bus), 高速总线，用来接高速外设的。APB (Advanced Peripheral Bus) 低速总线，用来接低速外设的。
* 使能时使用`RCC_AHBPeriphClockCmd()`函数

**DMA 请求**

如果外设想要通过 DMA 来传输数据，必须先给 DMA 控制器发送 DMA 请求，DMA 收到请求信号之后，控制器会给外设一个应答信号，当外设应答后且 DMA 控制器收到应答信号之后，就会启动 DMA 的传输，直到传输完毕。

![image-20230809162025633](STM32卷一.assets/image-20230809162025633.png)

STM32F103 共有 DMA1 和 DMA2 两个控制器，DMA1 有 7 个通道，DMA2 有 5 个通道，不同的 DMA 控制器的通道对应着不同的外设请求

![image-20230809161404273](STM32卷一.assets/image-20230809161404273.png)

![image-20230809161429634](STM32卷一.assets/image-20230809161429634.png)

**通道**

DMA 具有 12 个独立可编程的通道，其中 DMA1 有 7 个通道，DMA2 有 5 个通道，每个通道对应不同的外设的 DMA 请求。虽然每个通道可以接收多个外设的请求，但是同一时间只能接收一个，不能同时接收多个。

**仲裁器**

当发生多个 DMA 通道请求时，就意味着有先后响应处理的顺序问题，这个就由仲裁器管理。仲裁器管理 DMA 通道请求分为两个阶段。第一阶段属于软件阶段，可以在 DMA_CCRx寄存器中设置，有 4 个等级：非常高，高，中和低四个优先级。第二阶段属于硬件阶段，如果两个或以上的 DMA 通道请求设置的优先级一样，则他们优先级取决于通道编号，编号越低优先权越高，比如通道 0 高于通道 1。在大容量产品和互联型产品中，DMA1 控制器拥有高于 DMA2 控制器的优先级。

### 有DMA和没有DMA的区别

下面看有与没有DMA的情况下，ADC采集的数据是怎样存放到SRAM中的？

**没有DMA**

如果没有DMA,CPU传输数据还要以内核作为中转站，比如要将ADC采集的数据转移到到SRAM中，这个过程是这样的：

1. 内核通过DCode经过总线矩阵协调，从获取AHB存储的外设ADC采集的数据，
2. 然后内核再通过DCode经过总线矩阵协调把数据存放到内存SRAM中。

![image-20230707165200190](STM32卷一.assets/image-20230707165200190.png)

**有DMA传输**

1. DMA传输时外设对DMA控制器发出请求。
2. DMA控制器收到请求，触发DMA工作。
3. DMA控制器从AHB外设获取ADC采集的数据，存储到DMA通道中
4. DMA控制器的DMA总线与总线矩阵协调，使用AHB把外设ADC采集的数据经由DMA通道存放到SRAM中，这个数据的传输过程中，完全不需要内核的参与，也就是不需要CPU的参与
   ![image-20230707165648894](STM32卷一.assets/image-20230707165648894.png)





### DMA基本结构

![image-20230707165847970](STM32卷一.assets/image-20230707165847970.png)



M2M 0：硬件触发 1：为软件触发

传输计数器：设置好值后，每传输一次，值减一

主要配置：

* 起始位置
* 数据宽度
* 地址是否自增

### DMA触发源

![image-20230707170053710](STM32卷一.assets/image-20230707170053710.png)



* 不同通道的硬件请求信号不一样，软件触发相同
* M2M 0：硬件触发 1：为软件触发

* 使用硬件触发时，除了设置M2M为Disable外，还需要使用`XXX_DMACmd()`函数
  * 如使用ADC1触发DMA通道1：`ADC_DMACmd(ADC1,ENABLE); `  

````c
void ADC_DMACmd(ADC_TypeDef* ADCx, FunctionalState NewState);
void TIM_DMACmd(TIM_TypeDef* TIMx, uint16_t TIM_DMASource, FunctionalState NewState);
void USART_DMACmd(USART_TypeDef* USARTx, uint16_t USART_DMAReq, FunctionalState NewState);
……
````

### 数据宽度与对齐

![image-20230707170311669](STM32卷一.assets/image-20230707170311669.png)

* 同宽度直接复制
* 小宽度转大宽度补零
* 大宽度转小宽度保留高位

## 相关寄存器

| **寄存器** |         **名称**         |             **作用**             |
| :--------: | :----------------------: | :------------------------------: |
|  DMA_CCRx  |    DMA通道x配置寄存器    |  用于配置DMA（核心控制寄存器）   |
|  DMA_ISR   |    DMA中断状态寄存器     |     用于查询当前DMA传输状态      |
|  DMA_IFCR  |  DMA中断标志清除寄存器   |      用来清除DMA_ISR对应位       |
| DMA_CNDTRx |  DMA通道x传输数量寄存器  | 用于控制DMA通道x每次传输的数据量 |
| DMA_CPARx  |  DMA通道x外设地址寄存器  |      用于存储STM32外设地址       |
| DMA_CMARx  | DMA通道x存储器地址寄存器 |       用于存放存储器的地址       |
| USART_CR3  |     USART控制寄存器3     |       用于使能串口DMA发送        |

**DMA 中断状态寄存器（DMA_ISR）**

![image-20230809162802276](STM32卷一.assets/image-20230809162802276.png)

该寄存器是查询当前 DMA 传输的状态，我们常用的是 TCIFx 位，即通道 DMA 传输完成与否的标志。注意此寄存器为只读寄存器，所以在这些位被置位之后，只能通过其他的操作来清除。

**DMA 中断标志清除寄存器（DMA_IFCR）**

![image-20230809162853141](STM32卷一.assets/image-20230809162853141.png)

该寄存器是用来清除 DMA_ISR 的对应位的，通过写 0 清除。在 DMA_ISR 被置位后，我们必须通过向该寄存器对应的位写 0 来清除。



**DMA 通道 x 传输数量寄存器（DMA_CNDTRx）**

![image-20230809162932519](STM32卷一.assets/image-20230809162932519.png)

该寄存器控制着 DMA 通道 x 的每次传输所要传输的数据量。其设置范围为 0~65535。并且该寄存器的值随着传输的进行而减少，当该寄存器的值为 0 的时候就代表此次数据传输已经全部发送完成。所以可以通过这个寄存器的值来获取当前 DMA 传输的进度。

非循环模式下传输结束后，要开始新的DMA传输，需要在关闭DMA通道情况下，在该寄存器中重新写入传输数目。

**DMA 通道 x 配置寄存器（DMA_CCRx）**

![image-20230809162717603](STM32卷一.assets/image-20230809162717603.png)

该寄存器控制着 DMA 很多相关信息，包括数据宽度、外设及存储器宽度、通道优先级、增量模式、传输方向、中断允许、使能等，所以说 DMA_CCRx 是 DMA 传输的核心控制寄存器。

**DMA 通道 x 外设地址寄存器（DMA_CPARx）**

![image-20230809163201879](STM32卷一.assets/image-20230809163201879.png)

该寄存器是用来存储 STM32 外设的地址，比如我们平常使用串口 1，那么该寄存器必须写入 0x40013804（其实就是&USART1_DR）。其他外设就可以修改成其他对应外设地址就好了。

**DMA 通道 x 存储器地址寄存器（DMA_CMARx）**

![image-20230809163214352](STM32卷一.assets/image-20230809163214352.png)

## HAL库

### 常用函数

|           驱动函数           |       关联寄存器        |       功能描述        |
| :--------------------------: | :---------------------: | :-------------------: |
| __HAL_RCC_DMAx_CLK_ENABLE(…) |       RCC_AHBENR        |     使能DMAx时钟      |
|       HAL_DMA_Init(…)        |         DMA_CCR         |       初始化DMA       |
|     HAL_DMA_Start_IT(…)      | DMA_CCR/CPAR/CMAR/CNDTR |      开始DMA传输      |
|    __HAL_DMA_GET_FLAG(…)     |         DMA_ISR         | 查询DMA传输通道的状态 |
|     __HAL_DMA_ENABLE(…)      |       DMA_CCR(EN)       |      使能DMA外设      |
|     __HAL_DMA_DISABLE(…)     |       DMA_CCR(EN)       |      失能DMA外设      |

__HAL_RCC_DMAx_CLK_ENABLE(…)要在HAL_DMA_Init(…)之前完成，这也许就是DMA没有MspInit的缘故



使用其他外设触发DMA

|         驱动函数         |          关联寄存器           |          功能描述          |
| :----------------------: | :---------------------------: | :------------------------: |
|     __HAL_LINKDMA(…)     |                               |   用来连接DMA和外设句柄    |
| HAL_UART_Transmit_DMA(…) | CCR/CPAR/CMAR/CNDTR/USART_CR3 | 使能UART DMA发送，启动传输 |
|   HAL_UART_DMAStop(…)    |                               |  传输完成以后关闭串口DMA   |
|   HAL_ADC_Start_DMA(…)   |                               |                            |
|            ……            |              ……               |             ……             |

````C
/**	将DMA句柄连接到外设句柄中的关于DMA的参数
*	参数1：外设句柄
*	参数2：外设句柄中关于DMA的参数
*			如串口外设句柄中
*				DMA_HandleTypeDef             *hdmatx;      发送则用hdmatx
*				DMA_HandleTypeDef             *hdmarx;      接受则用hdmarx
*	参数3：DMA句柄
**/
__HAL_LINKDMA(__HANDLE__, __PPP_DMA_FIELD__, __DMA_HANDLE__);

/** 开启DMA
*	参数1：DMA句柄
*	参数2：来源地址
*	参数3：目标地址
*	参数4：传输的长度
**/
HAL_StatusTypeDef HAL_DMA_Start(DMA_HandleTypeDef *hdma, uint32_t SrcAddress, uint32_t DstAddress, uint32_t DataLength);

/** 使用UART激活DMA
*	内部实际上还是调用HAL_DMA_Start_IT()
**/
HAL_StatusTypeDef HAL_UART_Transmit_DMA(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size)
````

````C
typedef struct __DMA_HandleTypeDef{
    DMA_Channel_TypeDef   *Instance;
    DMA_InitTypeDef       Init;
} DMA_HandleTypeDef; 
typedef struct{
    uint32_t Direction			    /* DMA传输方向 */
    uint32_t PeriphInc			    /* 外设地址(非)增量 */
    uint32_t MemInc			    	/* 存储器地址(非)增量*/
    uint32_t PeriphDataAlignment	/* 外设数据宽度 */
    uint32_t MemDataAlignment		/* 存储器数据宽度 */
    uint32_t Mode					/* 操作模式 */
    uint32_t Priority				/* DMA通道优先级 */
} DMA_InitTypeDef;
/* DMA传输方向 */
#define DMA_PERIPH_TO_MEMORY
#define DMA_MEMORY_TO_PERIPH
#define DMA_MEMORY_TO_MEMORY
/* 外设地址(非)增量 */
#define DMA_PINC_ENABLE
#define DMA_PINC_DISABLE
/* 存储器地址(非)增量*/
#define DMA_MINC_ENABLE
#define DMA_MINC_DISABLE
/* 外设数据宽度 */
#define DMA_PDATAALIGN_BYTE
#define DMA_PDATAALIGN_HALFWORD
#define DMA_PDATAALIGN_WORD
/* 存储器数据宽度 */
#define DMA_MDATAALIGN_BYTE
#define DMA_MDATAALIGN_HALFWORD
#define DMA_MDATAALIGN_WORD
/* 操作模式 */
#define DMA_NORMAL           // 正常模式，只传输一次
#define DMA_CIRCULAR         // 连续模式
/* DMA通道优先级 */
#define DMA_PRIORITY_LOW
#define DMA_PRIORITY_MEDIUM
#define DMA_PRIORITY_HIGH
#define DMA_PRIORITY_VERY_HIGH

````

### 实例

#### 数据传送DMA

将一个数组中的内容传输的另一个数组

````c
uint8_t Memory[10] = {0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09};
uint8_t Periph[10] = {0};
DMA_HandleTypeDef DMA_HandleStructure;
void DMA_Init(void){

    __HAL_RCC_DMA1_CLK_ENABLE();          // 使能DMA1
    
    DMA_HandleStructure.Instance = DMA1_Channel1;              /*使用DMA1的通道1*/
    DMA_HandleStructure.Init.Direction = DMA_MEMORY_TO_MEMORY;
    DMA_HandleStructure.Init.Mode = DMA_NORMAL;                /*使用标准模式，存储器到存储器无法使用连续模式*/
    DMA_HandleStructure.Init.Priority = DMA_PRIORITY_MEDIUM ;  /*使用中等优先级*/
    DMA_HandleStructure.Init.MemInc = DMA_MINC_ENABLE ;
    DMA_HandleStructure.Init.MemDataAlignment = DMA_MDATAALIGN_BYTE ;
    DMA_HandleStructure.Init.PeriphInc = DMA_PINC_ENABLE;
    DMA_HandleStructure.Init.PeriphDataAlignment = DMA_PDATAALIGN_BYTE;
    
    HAL_DMA_Init(&DMA_HandleStructure);
    HAL_DMA_Start(&DMA_HandleStructure,(uint32_t)Memory, (uint32_t)Periph,0);    // 参数3:传输数据个数
    
    __HAL_DMA_ENABLE(&DMA_HandleStructure);
}
// 设置传输多少数据，就是HAL_DMA_Start参数4
void DMA_Set_DataLeng(int leng){
    __HAL_DMA_DISABLE(&DMA_HandleStructure);    // 操作寄存器必须先失能
    DMA_HandleStructure.Instance->CNDTR = leng;
    __HAL_DMA_ENABLE(&DMA_HandleStructure);
}
int main(void){
    HAL_Init();                                 /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9);         /* 设置时钟,72M */
    delay_init(72);                             /* 初始化延时函数 */
    UART_Init();
    key_init();
    DMA_Init();
    
    uint8_t key;
    while(1){
        key = key_scan(0);
        if(key == 1){
            DMA_Set_DataLeng(10);     // 开始传输
            while(__HAL_DMA_GET_FLAG(&DMA_HandleStructure,DMA_FLAG_TC1)!=RESET);
            printf("传输完成 \r\n");
            for(int i = 0;i < 10;i++){
                printf("Memory[%d] :%d \r\n",i,Memory[i]);
                printf("Periph[%d] :%d \r\n",i,Periph[i]);
            }  
        }
    }
}
````

#### 串口+DMA

将数组(存储器)中的内容通过串口外设调用DMA直接发送到上位机

````c
UART_HandleTypeDef UART_Handle;	               // 串口句柄
void UART_Init(void){
    UART_Handle.Instance = USART1;	                     // 使用USART1
    
    UART_Handle.Init.BaudRate = 115200;           
    UART_Handle.Init.Mode =  UART_MODE_TX_RX;            // 读写
    UART_Handle.Init.Parity = UART_PARITY_NONE;          // 不使用校验
    UART_Handle.Init.StopBits = UART_STOPBITS_1;         // 停止位1
    UART_Handle.Init.WordLength = UART_WORDLENGTH_8B;    // 数据位8
    UART_Handle.Init.HwFlowCtl = UART_HWCONTROL_NONE ;
    
    HAL_UART_Init(&UART_Handle);                         // 初始化
    
    __HAL_RCC_GPIOA_CLK_ENABLE();
    __HAL_RCC_USART1_CLK_ENABLE();
    
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.Mode = GPIO_MODE_AF_PP;
    GPIO_InitStructure.Pin = GPIO_PIN_9;
    GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH;
    HAL_GPIO_Init(GPIOA,&GPIO_InitStructure);
    
    GPIO_InitStructure.Mode = GPIO_MODE_INPUT;
    GPIO_InitStructure.Pin = GPIO_PIN_10;
    GPIO_InitStructure.Pull = GPIO_PULLUP;
    GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH;
    HAL_GPIO_Init(GPIOA,&GPIO_InitStructure);
}
DMA_HandleTypeDef DMA_HandleStructure;
void DMA_Init(void){
    __HAL_RCC_DMA1_CLK_ENABLE();
    /*  将DMA与USART1联系起来(发送DMA)
    *   参数2：hdmatx，就是UART_HandleTypeDef->hdmatx; 发送
    *              与之对应UART_HandleTypeDef->hdmarx; 接收
    */
    __HAL_LINKDMA(&UART_Handle,hdmatx,DMA_HandleStructure);             
    
    DMA_HandleStructure.Instance = DMA1_Channel4;                      /* USART1_TX使用的DMA通道为: DMA1_Channel4 */
    DMA_HandleStructure.Init.Direction = DMA_MEMORY_TO_PERIPH;         /* DIR = 1 , 存储器到外设模式 */
    DMA_HandleStructure.Init.MemDataAlignment = DMA_MDATAALIGN_BYTE;   /* 存储器数据长度:8位 */
    DMA_HandleStructure.Init.MemInc = DMA_MINC_ENABLE;                 /* 存储器增量模式 */
    DMA_HandleStructure.Init.PeriphDataAlignment = DMA_PDATAALIGN_BYTE;/* 外设数据长度:8位 */
    DMA_HandleStructure.Init.PeriphInc = DMA_PINC_DISABLE;             /* 外设非增量模式 */
    DMA_HandleStructure.Init.Priority = DMA_PRIORITY_MEDIUM;           /* 中等优先级 */
    DMA_HandleStructure.Init.Mode = DMA_NORMAL;                        /* 正常模式，非连续 */
    
    HAL_DMA_Init(&DMA_HandleStructure);
}
uint8_t data[] = {"rainupup 雨神"};     // 一共13个字节

int main(void){
    HAL_Init();                                 /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9);         /* 设置时钟,72M */
    delay_init(72);                             /* 初始化延时函数 */
    key_init();
    UART_Init();
    DMA_Init();
    uint8_t keynum;   
    while(1){
        keynum = key_scan(0);
        if(keynum == 1){
            HAL_UART_Transmit_DMA(&UART_Handle,data, sizeof(data));                // UART 开启DMA传送       
            while(__HAL_DMA_GET_FLAG(&DMA_HandleStructure,DMA_FLAG_TC4) == RESET);
            __HAL_DMA_CLEAR_FLAG(&DMA_HandleStructure,DMA_FLAG_TC4);               // 清除标志位
            HAL_UART_DMAStop(&UART_Handle);                                        // 关闭UART DMA通道
        }       
    }
}
````

#### ADC单通道DMA

ADC单通道连续非扫描：连续检测100次电压，并对这100次电压取平均

````c
ADC_HandleTypeDef ADC_HandleStructure;
DMA_HandleTypeDef DMA_HandleStructure;
/** 初始化ADC,DMA
*   参数:DMA目标地址，即ADC存放的位置
**/
void ADC_DMA_Init(uint32_t data){  
    __HAL_RCC_DMA1_CLK_ENABLE();  /* 开启DMA时钟，注意：要在HAL_DMA_Init之前完成 */
    
    DMA_HandleStructure.Instance = DMA1_Channel1;               /* ADC使用DMA1的通道1 */
    DMA_HandleStructure.Init.Direction = DMA_PERIPH_TO_MEMORY;  /* 外设到内存 */
    DMA_HandleStructure.Init.Mode = DMA_NORMAL;                 /* 使用标准模式，非连续传输 */
    DMA_HandleStructure.Init.Priority = DMA_PRIORITY_MEDIUM;    /* 使用中等优先级 */
    DMA_HandleStructure.Init.MemInc = DMA_MINC_ENABLE ;         /* 内存自增 */
    DMA_HandleStructure.Init.MemDataAlignment = DMA_MDATAALIGN_HALFWORD;    /* ADC采集的数据是16为长度，故采用半字 */
    DMA_HandleStructure.Init.PeriphInc = DMA_PINC_DISABLE;      /* 外设不自增 */
    DMA_HandleStructure.Init.PeriphDataAlignment = DMA_PDATAALIGN_HALFWORD; /* ADC采集的数据是16为长度 */
    HAL_DMA_Init(&DMA_HandleStructure); 
    
    
    ADC_ChannelConfTypeDef ADC_ChConf;
    
    ADC_HandleStructure.Instance = ADC1;								/* 选择ADC1 */
    ADC_HandleStructure.Init.ContinuousConvMode = ENABLE;				/* 连续模式 */   
    ADC_HandleStructure.Init.DataAlign = ADC_DATAALIGN_RIGHT;			/* 右对齐 */
    ADC_HandleStructure.Init.ScanConvMode = ADC_SCAN_DISABLE;			/* 非扫描模式 */
    ADC_HandleStructure.Init.NbrOfConversion = 1;						/* 使用1个通道 */
    ADC_HandleStructure.Init.DiscontinuousConvMode = DISABLE;			/* 间断模式关闭 */
    ADC_HandleStructure.Init.NbrOfDiscConversion = 0;					/* 间断模式关闭 */
    ADC_HandleStructure.Init.ExternalTrigConv = ADC_SOFTWARE_START ; 	/* 软件触发 */
    
    HAL_ADC_Init(&ADC_HandleStructure);
    HAL_ADCEx_Calibration_Start(&ADC_HandleStructure);		/* 校准 */

    ADC_ChConf.Channel = ADC_CHANNEL_1;						/* 通道1 PA1 */
    ADC_ChConf.Rank = ADC_REGULAR_RANK_1 ;					/* 序列1 */
    ADC_ChConf.SamplingTime = ADC_SAMPLETIME_239CYCLES_5;	/* 采样时间 */
    
    HAL_ADC_ConfigChannel(&ADC_HandleStructure,&ADC_ChConf);/* 初始化ADC通道 */
    
    __HAL_LINKDMA(&ADC_HandleStructure,DMA_Handle,DMA_HandleStructure);     /* DMA句柄连接到ADC句柄 */
    
    HAL_NVIC_SetPriorityGrouping(2);
    HAL_NVIC_SetPriority(DMA1_Channel1_IRQn,2,2);           /* 设置DMA中断 */
    HAL_NVIC_EnableIRQ(DMA1_Channel1_IRQn);
    
    /* 开启DMA，并开启DMA中断
    *  参数2：DMA数据来源
    *  参数3：DMA目标
    */
    HAL_DMA_Start_IT(&DMA_HandleStructure,(uint32_t)&ADC1->DR,data,0); 
    HAL_ADC_Start_DMA(&ADC_HandleStructure,&data,0);        /* 开启ADC,并连接DMA */
}
/**
*	初始化外围时钟，ADC的GPIO
**/
void HAL_ADC_MspInit(ADC_HandleTypeDef* hadc){
    if(hadc->Instance == ADC1){
        __HAL_RCC_GPIOA_CLK_ENABLE();
        __HAL_RCC_ADC1_CLK_ENABLE();

        RCC_PeriphCLKInitTypeDef RCC_PeriphInitStructure = {0};            // RCC配置外设时钟
        RCC_PeriphInitStructure.AdcClockSelection = RCC_ADCPCLK2_DIV6;     // ADC分频
        RCC_PeriphInitStructure.PeriphClockSelection = RCC_PERIPHCLK_ADC;  // 选择配置ADC
        HAL_RCCEx_PeriphCLKConfig(&RCC_PeriphInitStructure);
        
        GPIO_InitTypeDef GPIO_InitStructure;
        GPIO_InitStructure.Mode = GPIO_MODE_ANALOG;    //模拟输入，ADC专属
        GPIO_InitStructure.Pin = GPIO_PIN_1;
        GPIO_InitStructure.Pull = GPIO_PULLDOWN;
        GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH;
        
        HAL_GPIO_Init(GPIOA,&GPIO_InitStructure);    
    }
}
/** 开启ADC转换
*   参数：传输的长度
**/
void MyADC_DMAEnable(uint16_t length){
//    ADC1->CR2 &= ~(1 << 0);
//    DMA1_Channel1->CCR &= ~(1 << 0);
//    while (DMA1_Channel1->CCR & (1 << 0));
//    DMA1_Channel1->CNDTR = length;
//    DMA1_Channel1->CCR |= 1 << 0;
//    ADC1->CR2 |= 1 << 0;
//    ADC1->CR2 |= 1 << 22;
    
    __HAL_ADC_DISABLE(&ADC_HandleStructure);        /* 操作寄存器必须失能 */
    __HAL_DMA_DISABLE(&DMA_HandleStructure);
    
    DMA_HandleStructure.Instance->CNDTR = length;   /* 设置传输的长度 */
    
    __HAL_ADC_ENABLE(&ADC_HandleStructure);
    __HAL_DMA_ENABLE(&DMA_HandleStructure);
    HAL_ADC_Start(&ADC_HandleStructure);            /* 软件开启ADC */
}
/**
*   传输完成，将标志位置1，方便main函数读取
**/
int DMA_TC_Flag = 0;
void DMA1_Channel1_IRQHandler(void){
//    if (DMA1->ISR & (1<<1))
//    {
//        DMA_TC_Flag = 1;
//        DMA1->IFCR |= 1 << 1;        //DMA只能使用IFCR来消除ISR的标记
//    } 
    if(__HAL_DMA_GET_FLAG(&DMA_HandleStructure,DMA_FLAG_TC1) != SET){ /* 等待传输完成 */
        DMA_TC_Flag = 1;
        __HAL_DMA_CLEAR_FLAG(&DMA_HandleStructure,DMA_FLAG_TC1);
    }
}

#define ADC_DMA_LENGHT 100
uint16_t adc_dma_buffer[ADC_DMA_LENGHT];
int main(void){
    HAL_Init();                         /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9); /* 设置时钟, 72Mhz */
    delay_init(72);                     /* 延时初始化 */
    usart_init(115200);                 /* 串口初始化为115200 */
    led_init();                         /* 初始化LED */
    lcd_init();                         /* 初始化LCD */
    
    ADC_DMA_Init((uint32_t)&adc_dma_buffer); /* 初始化ADC和DMA */
    
    lcd_show_string(30, 110, 200, 16, 16, "ADC1_CH1_VAL:", RED);
    lcd_show_string(30, 130, 200, 16, 16, "ADC1_CH1_VOL:0.000V", BLUE); /* 先在固定位置显示小数点 */

    uint32_t adcsum,i;
    float temp;
   	MyADC_DMAEnable(ADC_DMA_LENGHT);   	/* 先开启一次ADC和DMA转换 */
    while (1){   
        adcsum = 0;
        if(DMA_TC_Flag == 1){			/* 等待传输完成 */
            for(i = 0;i < 100;i++){
                adcsum += adc_dma_buffer[i];
            }
            adcsum /= ADC_DMA_LENGHT;	/* 取平均 */
            lcd_show_xnum(134, 110, adcsum, 5, 16, 0, BLUE);
        
            temp = (float)adcsum * (3.3 / 4096);            
            adcsum = temp;            
            lcd_show_xnum(134, 130, adcsum, 1, 16, 0, BLUE);            
            temp -=adcsum;
            temp *= 1000;
            lcd_show_xnum(150, 130, temp, 3, 16, 0X80, BLUE);
            
            DMA_TC_Flag = 0;					/* 清除传输完成 */
            MyADC_DMAEnable(ADC_DMA_LENGHT);    /* 再次开启一次ADC和DMA转换 */     
        }
    }
}
````

#### ADC多通道DMA

连续扫描3个通道100次

````c
ADC_HandleTypeDef ADC_HandleStructure;
DMA_HandleTypeDef DMA_HandleStructure;
/** 初始化ADC,DMA
*   参数:DMA目标地址，即ADC存放的位置
**/
void ADC_DMA_Init(uint32_t data){  
    __HAL_RCC_DMA1_CLK_ENABLE();  /* 开启DMA时钟，注意：要在HAL_DMA_Init之前完成 */
    
    DMA_HandleStructure.Instance = DMA1_Channel1;               /* ADC使用DMA1的通道1 */
    DMA_HandleStructure.Init.Direction = DMA_PERIPH_TO_MEMORY;  /* 外设到内存 */
    DMA_HandleStructure.Init.Mode = DMA_NORMAL;                 /* 使用标准模式，非连续传输 */
    DMA_HandleStructure.Init.Priority = DMA_PRIORITY_MEDIUM;    /* 使用中等优先级 */
    DMA_HandleStructure.Init.MemInc = DMA_MINC_ENABLE ;         /* 内存自增 */
    DMA_HandleStructure.Init.MemDataAlignment = DMA_MDATAALIGN_HALFWORD;    /* ADC采集的数据是16为长度，故采用半字 */
    DMA_HandleStructure.Init.PeriphInc = DMA_PINC_DISABLE;      /* 外设不自增 */
    DMA_HandleStructure.Init.PeriphDataAlignment = DMA_PDATAALIGN_HALFWORD; /* ADC采集的数据是16为长度 */
    HAL_DMA_Init(&DMA_HandleStructure); 
    
    
    ADC_ChannelConfTypeDef ADC_ChConf;
    
    ADC_HandleStructure.Instance = ADC1;								/* 选择ADC1 */
    ADC_HandleStructure.Init.ContinuousConvMode = ENABLE;				/* 非连续模式 */   
    ADC_HandleStructure.Init.DataAlign = ADC_DATAALIGN_RIGHT;			/* 右对齐 */
    ADC_HandleStructure.Init.ScanConvMode = ADC_SCAN_ENABLE;			/* 扫描模式 */
    ADC_HandleStructure.Init.NbrOfConversion = 3;						/* 使用3个通道 */
    ADC_HandleStructure.Init.DiscontinuousConvMode = DISABLE;			/* 间断模式关闭 */
    ADC_HandleStructure.Init.NbrOfDiscConversion = 0;					/* 间断模式关闭 */
    ADC_HandleStructure.Init.ExternalTrigConv = ADC_SOFTWARE_START ; 	/* 软件触发 */
    
    HAL_ADC_Init(&ADC_HandleStructure);
    HAL_ADCEx_Calibration_Start(&ADC_HandleStructure);		/* 校准 */


    ADC_ChConf.Channel = ADC_CHANNEL_0;						/* 通道0 PA0 */
    ADC_ChConf.Rank = ADC_REGULAR_RANK_1 ;					/* 序列1 */
    ADC_ChConf.SamplingTime = ADC_SAMPLETIME_239CYCLES_5;	/* 采样时间 */
    HAL_ADC_ConfigChannel(&ADC_HandleStructure,&ADC_ChConf);/* 初始化ADC通道 */
    ADC_ChConf.Channel = ADC_CHANNEL_1;
    ADC_ChConf.Rank = ADC_REGULAR_RANK_2 ;
    HAL_ADC_ConfigChannel(&ADC_HandleStructure,&ADC_ChConf); 
    
    ADC_ChConf.Channel = ADC_CHANNEL_2;	
    ADC_ChConf.Rank = ADC_REGULAR_RANK_3;
    HAL_ADC_ConfigChannel(&ADC_HandleStructure,&ADC_ChConf);
    
    
    __HAL_LINKDMA(&ADC_HandleStructure,DMA_Handle,DMA_HandleStructure);     /* DMA句柄连接到ADC句柄 */
    
    HAL_NVIC_SetPriorityGrouping(2);
    HAL_NVIC_SetPriority(DMA1_Channel1_IRQn,2,2);           /* 设置DMA中断 */
    HAL_NVIC_EnableIRQ(DMA1_Channel1_IRQn);
    
    /* 开启DMA，并开启DMA中断
    *  参数2：DMA数据来源
    *  参数3：DMA目标
    */
    HAL_DMA_Start_IT(&DMA_HandleStructure,(uint32_t)&ADC1->DR,data,0);
    HAL_ADC_Start_DMA(&ADC_HandleStructure,&data,0);        /* 开启ADC,并连接DMA */
}
void HAL_ADC_MspInit(ADC_HandleTypeDef* hadc){
    if(hadc->Instance == ADC1){
        __HAL_RCC_GPIOA_CLK_ENABLE();
        __HAL_RCC_ADC1_CLK_ENABLE();
        
        
        RCC_PeriphCLKInitTypeDef RCC_PeriphInitStructure = {0};                  // RCC配置外设时钟

        RCC_PeriphInitStructure.AdcClockSelection = RCC_ADCPCLK2_DIV6;     // ADC分频
        RCC_PeriphInitStructure.PeriphClockSelection = RCC_PERIPHCLK_ADC;  // 选择配置ADC
        HAL_RCCEx_PeriphCLKConfig(&RCC_PeriphInitStructure);
        
        
        GPIO_InitTypeDef GPIO_InitStructure;
        GPIO_InitStructure.Mode = GPIO_MODE_ANALOG;    //模拟输入，ADC专属
        GPIO_InitStructure.Pin = GPIO_PIN_0 | GPIO_PIN_1 | GPIO_PIN_2;
        GPIO_InitStructure.Pull = GPIO_PULLDOWN;
        GPIO_InitStructure.Speed = GPIO_SPEED_FREQ_HIGH;
        
        HAL_GPIO_Init(GPIOA,&GPIO_InitStructure);    
    }
}
/** 开启ADC转换
*   参数：传输的长度
**/
void MyADC_DMAEnable(uint16_t length){
    __HAL_ADC_DISABLE(&ADC_HandleStructure);        /* 操作寄存器必须失能 */
    __HAL_DMA_DISABLE(&DMA_HandleStructure);
    
    DMA_HandleStructure.Instance->CNDTR = length;   /* 设置传输的长度 */
    
    __HAL_ADC_ENABLE(&ADC_HandleStructure);
    __HAL_DMA_ENABLE(&DMA_HandleStructure);
    HAL_ADC_Start(&ADC_HandleStructure);            /* 软件开启ADC */
}
/**
*   传输完成，将标志位置1，方便main函数读取
**/
int DMA_TC_Flag = 0;
void DMA1_Channel1_IRQHandler(void){
    if(__HAL_DMA_GET_FLAG(&DMA_HandleStructure,DMA_FLAG_TC1) != SET){
        DMA_TC_Flag = 1;
        __HAL_DMA_CLEAR_FLAG(&DMA_HandleStructure,DMA_FLAG_TC1);
    }
}
#define ADC_DMA_LENGHT 100 * 3                /* 连续转换100次，扫描3个通道*/
uint16_t adc_dma_buffer[ADC_DMA_LENGHT];
int main(void){
    HAL_Init();                         /* 初始化HAL库 */
    sys_stm32_clock_init(RCC_PLL_MUL9); /* 设置时钟, 72Mhz */
    delay_init(72);                     /* 延时初始化 */
    usart_init(115200);                 /* 串口初始化为115200 */
    led_init();                         /* 初始化LED */
    lcd_init();                         /* 初始化LCD */
    ADC_DMA_Init((uint32_t)&adc_dma_buffer);
    
    lcd_show_string(30, 50, 200, 16, 16, "STM32", RED);
    lcd_show_string(30, 70, 200, 16, 16, "WWW.RAINUPUP.CN", RED);
    lcd_show_string(30, 90, 200, 16, 16, "@RAINyy", RED);
    
    lcd_show_string(30, 110, 200, 16, 16, "ADC1_CH1_VAL:", RED);
    lcd_show_string(30, 130, 200, 16, 16, "ADC1_CH1_VOL:0.000V", BLUE); /* 先在固定位置显示小数点 */

    lcd_show_string(30, 150, 200, 16, 16, "ADC1_CH2_VAL:", RED);
    lcd_show_string(30, 170, 200, 16, 16, "ADC1_CH2_VOL:0.000V", BLUE); /* 先在固定位置显示小数点 */
    
    lcd_show_string(30, 190, 200, 16, 16, "ADC1_CH3_VAL:", RED);
    lcd_show_string(30, 210, 200, 16, 16, "ADC1_CH3_VOL:0.000V", BLUE); /* 先在固定位置显示小数点 */
    
    uint32_t adcsum;
    float temp;
    
    int i,j;
    MyADC_DMAEnable(ADC_DMA_LENGHT); 
    while (1)
    {   
        adcsum = 0;
        if(DMA_TC_Flag == 1){
            /*每次扫描3个通道，连续100次，数组下标 0 3 6……存放通道0的数据, 1 4 7……存放通道1的数据 */
            for(i = 0;i < 3;i++){
                for(j = 0;j < 100;j++){
                    adcsum += adc_dma_buffer[j * 3 + i];
                }
                adcsum  /= (ADC_DMA_LENGHT / 3);
                
                lcd_show_xnum(134, 110 + (i * 40), adcsum, 5, 16, 0, BLUE);
          
                temp = (float)adcsum * (3.3 / 4096);            
                adcsum = temp;            
                lcd_show_xnum(134, 130 + (i * 40), adcsum, 1, 16, 0, BLUE);            
                temp -=adcsum;
                temp *= 1000;
                lcd_show_xnum(150, 130 + (i * 40), temp, 3, 16, 0X80, BLUE);
                
                DMA_TC_Flag = 0;
                MyADC_DMAEnable(ADC_DMA_LENGHT);    
            }
        }
    }
}
````





## 标准库

### 常用函数

````c
/* 初始化参数DMAy_Channelx：
   参数DMAy_Channelx: y选择DMA，x选择通道
*/
void DMA_Init(DMA_Channel_TypeDef* DMAy_Channelx, DMA_InitTypeDef* DMA_InitStruct);
void DMA_DeInit(DMA_Channel_TypeDef* DMAy_Channelx);
void DMA_StructInit(DMA_InitTypeDef* DMA_InitStruct);
// 使能DMA
void DMA_Cmd(DMA_Channel_TypeDef* DMAy_Channelx, FunctionalState NewState);
// 使能中断
void DMA_ITConfig(DMA_Channel_TypeDef* DMAy_Channelx, uint32_t DMA_IT, FunctionalState NewState);
// 设置传送大小，即传输计数器
void DMA_SetCurrDataCounter(DMA_Channel_TypeDef* DMAy_Channelx, uint16_t DataNumber); 
// 获取传输计数器的值，即还有几次传输完毕
uint16_t DMA_GetCurrDataCounter(DMA_Channel_TypeDef* DMAy_Channelx);

// 获取传输的状态
/**
  *     @arg DMA1_FLAG_GL1: 获取 DMA1通道1的 组标志
  *     @arg DMA1_FLAG_TC1: 获取 DMA1通道1的 传输完成标志
  *     @arg DMA1_FLAG_HT1: 获取 DMA1通道1的 传输一半标志
  *     @arg DMA1_FLAG_TE1: 获取 DMA1通道1的 错误标志
  *     …………
  */
FlagStatus DMA_GetFlagStatus(uint32_t DMAy_FLAG);
// 清空传输完成标志位
void DMA_ClearFlag(uint32_t DMAy_FLAG);

ITStatus DMA_GetITStatus(uint32_t DMAy_IT);
void DMA_ClearITPendingBit(uint32_t DMAy_IT);
````



**结构体**

````c
typedef struct{
  uint32_t DMA_PeripheralBaseAddr; // 外设地址
  uint32_t DMA_PeripheralInc;      // 外设地址是否自增
  uint32_t DMA_PeripheralDataSize; // 外设数据长度
  uint32_t DMA_MemoryBaseAddr;     // 内存地址(要传输的变量的指针)
  uint32_t DMA_MemoryDataSize;     // 内存数据长度
  uint32_t DMA_MemoryInc;          // 内存地址是否自增

  uint32_t DMA_DIR;                // 传送方向
  uint32_t DMA_BufferSize;         // 传输内容的大小
    
  uint32_t DMA_Mode;               // DMA模式：一次传输，循环  注意：连续或是和DMA_M2M属性的软件触发只能二选一
  uint32_t DMA_M2M;                // 硬件触发、软件触发
  uint32_t DMA_Priority;           // 优先级
}DMA_InitTypeDef;
````

````c
/** DMA_DIR 传输方向
  * 它还是取决于结构体中的DMA_PeripheralBaseAddr和DMA_MemoryBaseAddr
  */
#define DMA_DIR_PeripheralDST              ((uint32_t)0x00000010)    // 外部设备寄存器为目标
#define DMA_DIR_PeripheralSRC              ((uint32_t)0x00000000)    // 外部设备寄存器为来源


/** DMA_PeripheralInc 外设地址是否自增
  */
#define DMA_PeripheralInc_Enable           ((uint32_t)0x00000040)
#define DMA_PeripheralInc_Disable          ((uint32_t)0x00000000)

/** DMA_MemoryInc 内存地址是否自增
  */
#define DMA_MemoryInc_Enable               ((uint32_t)0x00000080)
#define DMA_MemoryInc_Disable              ((uint32_t)0x00000000)

/** DMA_PeripheralDataSize;  外设数据长度
  */
#define DMA_PeripheralDataSize_Byte        ((uint32_t)0x00000000)
#define DMA_PeripheralDataSize_HalfWord    ((uint32_t)0x00000100)
#define DMA_PeripheralDataSize_Word        ((uint32_t)0x00000200)

/** DMA_MemoryDataSize;      内存数据长度
  */
#define DMA_MemoryDataSize_Byte            ((uint32_t)0x00000000)
#define DMA_MemoryDataSize_HalfWord        ((uint32_t)0x00000400)
#define DMA_MemoryDataSize_Word            ((uint32_t)0x00000800)

/** DMA_Mode;  DMA模式：一次传输，循环
  */
#define DMA_Mode_Circular                  ((uint32_t)0x00000020)   // 循环
#define DMA_Mode_Normal                    ((uint32_t)0x00000000)   // 一次

/** DMA_Priority;        优先级
  */
#define DMA_Priority_VeryHigh              ((uint32_t)0x00003000)
#define DMA_Priority_High                  ((uint32_t)0x00002000)
#define DMA_Priority_Medium                ((uint32_t)0x00001000)
#define DMA_Priority_Low                   ((uint32_t)0x00000000)

/**  DMA_M2M;            硬件触发、软件触发
  */
#define DMA_M2M_Enable                     ((uint32_t)0x00004000)   // 软件触发
#define DMA_M2M_Disable                    ((uint32_t)0x00000000)   // 硬件触发
````

### 实例

#### 数据传送DMA

![](STM32卷一.assets/image-20230707190235641.png)

目的：将DataA数组中的值传送到DataB数组中，都使用自增，



````c
uint32_t MySize;
void MyDMA_Init(uint32_t AddA,uint32_t AddB,uint32_t Size){
	MySize = Size;
	
	RCC_AHBPeriphClockCmd(RCC_AHBPeriph_DMA1,ENABLE);      // DMA需要RCC_AHBPeriphClockCmd()函数使能
	
	DMA_InitTypeDef DMA_InitStructure;
	DMA_InitStructure.DMA_PeripheralBaseAddr = AddA;                         // 串口数据寄存器地址
	DMA_InitStructure.DMA_PeripheralDataSize = DMA_PeripheralDataSize_Byte;  // 外设数据单位
	DMA_InitStructure.DMA_PeripheralInc = DMA_PeripheralInc_Enable;          // 外设地址自增
	
	DMA_InitStructure.DMA_MemoryBaseAddr = AddB;                             // 内存地址(要传输的变量的指针)
	DMA_InitStructure.DMA_MemoryDataSize = DMA_MemoryDataSize_Byte ;         // 内存数据单位
	DMA_InitStructure.DMA_MemoryInc = DMA_MemoryInc_Enable  ;                // 内存地址自增
	
	DMA_InitStructure.DMA_Mode = DMA_Mode_Normal;                            // 单次传送
	DMA_InitStructure.DMA_BufferSize = Size;                                 // 传输内容的大小
	DMA_InitStructure.DMA_DIR = DMA_DIR_PeripheralSRC;                       // 方向(从外设到内存)，外设作为来源
	DMA_InitStructure.DMA_M2M = DMA_M2M_Enable;                              // 使用软件触发(禁止内存到内存的传输)
	DMA_InitStructure.DMA_Priority = DMA_Priority_Medium;                    // 优先级：中
	
	DMA_Init(DMA1_Channel1, &DMA_InitStructure);                             // 配置DMA1的1通道,DMAy_Channelx
	 
	//DMA_Cmd(DMA1_Channel1,ENABLE);                                         // 使能DMA1_Channel1
	DMA_Cmd(DMA1_Channel1,DISABLE);                                          // 不使能DMA1_Channel1
}
void DMA_Transfer(void){
	// 设置传输内容的大小，必须先不使能DMA，设置完后，使能DMA，传送
	DMA_Cmd(DMA1_Channel1,DISABLE);                       // 先不使能
	DMA_SetCurrDataCounter(DMA1_Channel1, MySize);        // 传输内容的大小，与DMA_InitStructure.DMA_BufferSize一样
	DMA_Cmd(DMA1_Channel1,ENABLE);                        // 使能
	
	while(DMA_GetFlagStatus(DMA1_FLAG_TC1) == RESET);     // 等待传送完成
	DMA_ClearFlag(DMA1_FLAG_TC1);	                      // 清除标志位
}
//----------------------------------------------------------------
uint8_t DataA[4] = {0x01,0x02,0x03,0x04};
uint8_t DataB[4] = {0,0,0,0};

int main(void)
{	
	OLED_Init();
	
	MyDMA_Init((uint32_t)DataA,(uint32_t)DataB,4);
	
	OLED_ShowString(1, 1, "DataA:");
	OLED_ShowString(3, 1, "DataB:");
	OLED_ShowHexNum(1, 6, (uint32_t)DataA, 8);
	OLED_ShowHexNum(3, 6, (uint32_t)DataB, 8);
	
	while(1){
		OLED_ShowHexNum(2, 1, DataA[0], 2);
		OLED_ShowHexNum(2, 4, DataA[1], 2);
		OLED_ShowHexNum(2, 7, DataA[2], 2);
		OLED_ShowHexNum(2, 10, DataA[3], 2);
		Delay_ms(1000);
		
		DataA[0]++;
		DataA[1]++;
		DataA[2]++;
		DataA[3]++;
		
		DMA_Transfer();
		
		OLED_ShowHexNum(4, 1, DataB[0], 2);
		OLED_ShowHexNum(4, 4, DataB[1], 2);
		OLED_ShowHexNum(4, 7, DataB[2], 2);
		OLED_ShowHexNum(4, 10, DataB[3], 2);
		Delay_ms(1000);
	}
}
````



#### ADC多通道DMA



![image-20230707200643800](STM32卷一.assets/image-20230707200643800.png)

ADC为软件触发，DMA的触发源为ADC，不需要获取ADC的值，直接使用DMA将ADC寄存器的DR中的值转移到数组

````c
uint16_t rainData[4];
void AD_DMA_Init(void){
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_ADC1, ENABLE);     //开启ADC
	RCC_AHBPeriphClockCmd(RCC_AHBPeriph_DMA1,ENABLE);        //开启DMA
	
	RCC_ADCCLKConfig(RCC_PCLK2_Div6);                        //分频ADCCLK = 72MHz / 6 = 12MHz
	
	GPIO_InitTypeDef GPIO_InitSturcture;
	GPIO_InitSturcture.GPIO_Mode = GPIO_Mode_AIN;            //模拟输入模式，ADC的专属模式，断开GPIO口的输入输出对模拟电压照成的干扰
	GPIO_InitSturcture.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 |GPIO_Pin_3;
	GPIO_InitSturcture.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOA, &GPIO_InitSturcture);
	
	ADC_RegularChannelConfig(ADC1, ADC_Channel_0, 1,ADC_SampleTime_55Cycles5);     //使用ADC1的通道1，放到序列1位置，采样时间55
	ADC_RegularChannelConfig(ADC1, ADC_Channel_1, 2,ADC_SampleTime_55Cycles5);     //使用ADC1的通道2，放到序列2位置，采样时间55
	ADC_RegularChannelConfig(ADC1, ADC_Channel_2, 3,ADC_SampleTime_55Cycles5);     //使用ADC1的通道3，放到序列3位置，采样时间55
	ADC_RegularChannelConfig(ADC1, ADC_Channel_3, 4,ADC_SampleTime_55Cycles5);     //使用ADC1的通道3，放到序列4位置，采样时间55
	
	ADC_InitTypeDef ADC_InitStructure;
	ADC_InitStructure.ADC_Mode = ADC_Mode_Independent;                    // 独立模式
	ADC_InitStructure.ADC_DataAlign = ADC_DataAlign_Right;                // 右对齐
	ADC_InitStructure.ADC_ExternalTrigConv = ADC_ExternalTrigConv_None;   // 不使用外部触发
	ADC_InitStructure.ADC_ContinuousConvMode = ENABLE;                    // 连续触发
	ADC_InitStructure.ADC_ScanConvMode = ENABLE;                          // 扫描模式
	ADC_InitStructure.ADC_NbrOfChannel = 4;                               // 4个通道
	ADC_Init(ADC1, &ADC_InitStructure);
	
	DMA_InitTypeDef DMA_InitStructure;
	DMA_InitStructure.DMA_PeripheralBaseAddr = (uint32_t)&ADC1->DR;       // 外部寄存器为ADC1的DR
	DMA_InitStructure.DMA_PeripheralDataSize = DMA_PeripheralDataSize_HalfWord;
	DMA_InitStructure.DMA_PeripheralInc = DMA_PeripheralInc_Disable;      // 外部寄存器不自增
	DMA_InitStructure.DMA_MemoryBaseAddr = (uint32_t)rainData;            // 存放到rainData;  数组
	DMA_InitStructure.DMA_MemoryDataSize = DMA_MemoryDataSize_HalfWord;
	DMA_InitStructure.DMA_MemoryInc = DMA_MemoryInc_Enable;               // 数组自增
	DMA_InitStructure.DMA_DIR = DMA_DIR_PeripheralSRC;
	DMA_InitStructure.DMA_BufferSize = 4;
	DMA_InitStructure.DMA_Mode = DMA_Mode_Circular;                       // 循环转移
	DMA_InitStructure.DMA_M2M = DMA_M2M_Disable;                          // 硬件触发，使用ADC触发
	DMA_InitStructure.DMA_Priority = DMA_Priority_Medium;
	DMA_Init(DMA1_Channel1, &DMA_InitStructure);
	
	DMA_Cmd(DMA1_Channel1,ENABLE);                                        // 使能DMA
	ADC_DMACmd(ADC1,ENABLE);                                              // 使ADC作为DMA的触发源，DMA1_Channel1的触发源之一是ADC1
	ADC_Cmd(ADC1,ENABLE);                                                 // 使能ADC
	
	ADC_ResetCalibration(ADC1);        // 复位校准
	while(ADC_GetResetCalibrationStatus(ADC1) == SET);    //返回复位校准状态，为SET则表示正在初始化校准寄存器
	ADC_StartCalibration(ADC1);        // 开始校准
	while(ADC_GetCalibrationStatus(ADC1) == SET);         //返回校准状态，为SET则表示正在开始校准

	ADC_SoftwareStartConvCmd(ADC1, ENABLE);                                // 软件触发ADC
}
//-----------------------------------------------------------------------------------------------------
int main(void)
{	
	OLED_Init();
	AD_DMA_Init();
	OLED_ShowString(1, 1, "AD1:");
	OLED_ShowString(2, 1, "AD2:");
	OLED_ShowString(3, 1, "AD3:");
	OLED_ShowString(4, 1, "AD4:");
	while(1){
		OLED_ShowNum(1, 5, rainData[0], 4);
		OLED_ShowNum(2, 5, rainData[1], 4);
		OLED_ShowNum(3, 5, rainData[2], 4);
		OLED_ShowNum(4, 5, rainData[3], 4);
		Delay_ms(100);
	}
}
````

