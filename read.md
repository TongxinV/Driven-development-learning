##UBOOT

获取uboot源码包，解压，配置``make xxx_config`` `` 交叉编译工具事先要装好并检查Makefile的交叉编译工具的名称是否正确``make 编译得到uboot.bin

###uboot根目录下的各个文件的含义
......

###uboot配置和编译过程详解<先看地图 再看源代码>
``mkconfig脚本`` ``Makefile文件``
结构：

    <主Makefile分析>
        ├── 1. U_BOOT_VERSION
        ├── 2. HOSTARCH和HOSTOS  主机架构（i386）和操作系统（linux）  得出来干嘛用？
        ├── 3. 静默编译
        ├── 4. 指定文件夹编译 BUILD_DIR = ...
        ├── 5. export OBJTREE SRCTREE TOPDIR MKCONFIG := $(SRCTREE)/mkconfig
        ├── 6. include $(obj)

###uboot源码分析
flags:JiuDing移植的uboot

结构：

    project
        ├── start.S
        │   ├── 1.包含头文件
        │   ├── 2.定义4个4字节变量填充占位
        │   ├── 3.构建异常向量表，程序跳转到reset符号处
        │   └── 4.reset
        │       ├── msr cpsr_c, #0xd3           将CPU设置为禁止 FIQ\IRQ.ARM状态.SVC模式
        │       ├── cpu_init_crit               CPU初始化，完成L2Cache.L1Cache.MMU设置
        │       ├── Read booting information    加载启动信息，主要完成了识别并暂存启动介质类型
        │       ├── 设置栈.为了在内部96KB的iRAM中使用栈；并调用lowlevel_init
        │       │   lowlevel_init
        │       │       push {lr}
        │       │       check reset statue
        │       │       IO Retension release
        │       │       Disable Watchdog
        │       │       供电锁存
        │       │       判断当前代码是在SRAM中还是DDR中执行 以决定是否跳过下面的时钟和DDR初始化
        │       │           system_clock_init
        │       │           mem_ctrl_asm_init
        │       │       初始化串口，并打印‘OK’
        │       │       pop {pc}
        │       │
        │       ├── 设置栈. 为了将来重定位之后能在内存中使用栈；判断当前代码是在SRAM中还是DDR中执行以决定是否进行重定位movi_bl2_copy
        │       ├── after_copy：构建虚拟地址映射表，并设置基地址，同时开启MMU
        │       ├── 设置栈. 这次设置栈还是在内存中，但是本次设置栈的目的是将栈放在比较合适的位置
        │       └── ldr pc, __start_armboot
        │ 
        └──start_armboot函数
            ├── init_sequence
            │       cpu_init	空的
            │       board_init	网卡、机器码、内存传参地址
            │       dm9000_pre_init			网卡
            │       gd->bd->bi_arch_number	机器码
            │       gd->bd->bi_boot_params	内存传参地址
            │       interrupt_init	定时器
            │       env_init
            │       init_baudrate	gd数据结构中波特率
            │       serial_init		空的
            │       console_init_f	空的
            │       display_banner	打印启动信息
            │       print_cpuinfo	打印CPU时钟设置信息
            │       checkboard		检验开发板名字
            │       dram_init		gd数据结构中DDR信息
            │       display_dram_config	打印DDR配置信息表
            │
            ├── mem_malloc_init		初始化uboot自己维护的堆管理器的内存
            ├── mmc_initialize		inand/SD卡的SoC控制器和卡的初始化
            ├── env_relocate		环境变量重定位
            ├── gd->bd->bi_ip_addr	gd数据结构赋值
            ├── gd->bd->bi_enetaddr	gd数据结构赋值
            ├── devices_init			空的
            ├── jumptable_init		不用关注的
            ├── console_init_r		真正的控制台初始化
            ├── enable_interrupts	空的
            ├── loadaddr、bootfile 	环境变量读出初始化全局变量
            ├── board_late_init		空的
            ├── eth_initialize		空的
            ├── x210_preboot_init	LCD初始化和显示logo
            ├── check_menu_update_from_sd	检查自动更新
            └── main_loop			主循环
                ├── do_bootm
                    ......
                    └── do_boot_linux -> theKernel(0,machid,bd->bi_boot_params)
		
###详细代码分析
略（日后补充）

###uboot如何启动内核
事先设置好`bootcmd`和`bootargs`
> 例: bootcmd 'movi read kernel 30008000; bootm 30008000'
 例：bootargs = 'xxx'

1. 将内核镜像从启动介质加载到DDR中，执行`do_bootm`函数
2. 启动内核并同时传递参数给内核
 







