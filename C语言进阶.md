![C](http://i.imgur.com/kvDV6sE.jpg)
#C Language 进阶 
###1.非局部跳转语句---setjmp和longjmp函数
特点  
	非togo语句在函数内实施跳转,而是在栈上跳过若干调用帧,返回到当前函数调用路径上的某一语句.  
	头文件包含#include<setjmp.h>.  
    `Void longjmp(jmp_buf env,int val);`  
    返回值：若直接调用则返回0，若从longjmp调用返回则返回非0值  
	注: setjmp参数evn的类型是一个特殊的类型jmp_buf,这一数据类型是某种形式的数组，其中存放在调用longjmp时能用来恢复栈状态的所有信息.因为需要在另一个函数中引用env变量，所以规范的处理方式是将env变量定义为全局变量。  
	  
使用方法  
	在希望返回到的位置调用setjmp, 当检查到一个错误时,则以两个参数调用longjmp函数,第一个就是在调用setjmp时所用的env，第二个参数是具有非0值的val，它将成为从setjmp处返回的值.使用第二个参数的原因是对于一个setjmp可以有多个longjmp。  
    注:在使用longjmp跳转到setjmp中时，程序主动的退出了！相当于抛出一个异常退出！  
使用setjmp和longjmp要注意以下几点:
	
1. setjmp与longjmp结合使用时，它们必须有严格的先后执行顺序，也即先调用setjmp函数，之后再调用longjmp函数，以恢复到先前被保存的“程序执行点”。
2. 不要假设寄存器类型的变量将总会保持不变.在调用longjmp之后，通过setjmp所返回的控制流中，程序中寄存器类型的变量将不会被恢复。 寄存器类型的变量一般都是临时变量，在C语言中，通过register定义，或直接嵌入汇编代码的程序。
3.  longjmp必须在setjmp调用之后，而且longjmp必须在setjmp的作用域之内.




 
	

