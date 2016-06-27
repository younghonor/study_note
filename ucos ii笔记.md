![ucosii文件框图](http://i.imgur.com/Mi148RK.jpg)  
#ucos ii system
##文件结构
####上层：  
应用软件，用户代码  
###中层：   
与处理器无关代码(core,flag,mbox,mem,q,task,time,sem,mutex,ucos ii)  
与应用程序相关配置文件(cfg,includes)  
与处理器有关代码(cpu,cpu_a,cpu_c)
###下层：
硬件(cpu,interupt,timer,gpio,iis...)
##内核结构
###核心功能函数
OS_ENTER_CRITICAL()/OS_EXIT_CRITICAL()  开中断/关中断  
OSInit()  
OSStart()  
OSIntEnter()  
OSIntExit()  
OSSchedLock()/Unlock()  
OSVersion()  
###任务
任务状态：睡眠，就绪，等待，运行，中断。  
任务控制块(TCB)：一个数据结构，保存任务的状态，用来恢复任务  
就绪表：每个就绪的任务都保存在就绪表中，两个变量OSRdyGrp和OSRdyTbl[]  
使任务进入就绪表：  
			
任务调度 根据任务优先级  
任务切换  
任务通常是无限循环。  
###调度
上锁，开锁
###空闲任务
优先级最低，必须存在
###统计任务
优先级次低，选择  
每秒运行一次计算CPU利用率，精度1%。
###中断
###时钟节拍
提供周期性信号源，用于时间延迟和确认超时。
###流程
    `
	OSInit();//ucos的初始化,空闲任务，统计任务，系统变量及数据结构         
	OSStart();//ucos的启动,必须建立一个任物  
	`
##任务管理
##时间管理
##事件管理
##信号量管理
##消息管理
##内存管理
##ucos ii的移植
###ucos ii给实时系统开发提供一个简易的框架，其实现基本的系统管理功能。
###开发者需要做的是根据自己的平台修改和剪裁。
###需要设计中修改的如处理器的位数，开中断和关中断实现等。
###调通基本的系统，就可以在上面根据需要开发更多的功能。