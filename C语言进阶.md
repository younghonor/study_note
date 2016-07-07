![C](http://i.imgur.com/kvDV6sE.jpg)
#C Language 进阶 
#1.非局部跳转语句---setjmp和longjmp函数
特点  
	非togo语句在函数内实施跳转,而是在栈上跳过若干调用帧,返回到当前函数调用路径上的某一语句.  
	头文件包含#include<setjmp.h>.   
```c 
    Void longjmp(jmp_buf env,int val);  
```
    返回值：若直接调用则返回0，若从longjmp调用返回则返回非0值  
	注: setjmp参数evn的类型是一个特殊的类型jmp_buf,这一数据类型是某种形式的数组，其中存放在调用longjmp时能用来恢复栈状态的所有信息.因为需要在另一个函数中引用env变量，所以规范的处理方式是将env变量定义为全局变量。  
	  
使用方法  
	在希望返回到的位置调用setjmp, 当检查到一个错误时,则以两个参数调用longjmp函数,第一个就是在调用setjmp时所用的env，第二个参数是具有非0值的val，它将成为从setjmp处返回的值.使用第二个参数的原因是对于一个setjmp可以有多个longjmp。  
    注:在使用longjmp跳转到setjmp中时，程序主动的退出了！相当于抛出一个异常退出！  
使用setjmp和longjmp要注意以下几点:
	
1. setjmp与longjmp结合使用时，它们必须有严格的先后执行顺序，也即先调用setjmp函数，之后再调用longjmp函数，以恢复到先前被保存的“程序执行点”。
2. 不要假设寄存器类型的变量将总会保持不变.在调用longjmp之后，通过setjmp所返回的控制流中，程序中寄存器类型的变量将不会被恢复。 寄存器类型的变量一般都是临时变量，在C语言中，通过register定义，或直接嵌入汇编代码的程序。
3.  longjmp必须在setjmp调用之后，而且longjmp必须在setjmp的作用域之内.

#2. 位字段(bit-field)

在存储空间很宝贵的情况下,有可能需要将多个对象保存在一个机器字中,一种常用的方法是:使用类似于编译器符号表的单个二进制位标志集合,外部强加的数据格式(如设备接口等寄存器)经常需要从字的分值中读取数值.  
通常采用的方法是:定义一个于相关位的位置对应的"屏蔽码"集合,如:  

```c

	#define KEYWORD  (1<<0)  
	#define EXTRENAL (1<<2)  
	#define STATIC   (1<<3)  
```
或者  
```c

	enum{
		KEYWORD  = 01,  
		EXTRENAL = 02,
		STATIC   = 04
	};
```  
这些数字必须是2的幂,这样就可以用移位运算,屏蔽运算以及补码运算进行简单的操作.比如:  
```c  	

	flags |= EXTEERNAL | STATIC;//置1  
	flags &= ~(EXTEERNAL | STATIC);//置0  
```
尽管这样的方法容易掌握,但是C语言提供了一种可以替代的方法,即直接定义和方位一个位字段的能力,不必通过以上的逻辑运算符,即位字段.通过位字段,以上的#define定义可以用以下的语句替代:  
```c

	struct {
		unsigned int is_keyword : 1;
		unsigned int is_extern : 1;
		unsigned int is_static : 1;
	}flafs;
```
这里定义一个变量flags,它包含3个1位的字段,冒号后的数字表示字段的宽度(用二进制位数表示),字段被声明为unsigned int,以保证它们的无符号量.  
单个字段的引用方式与其他结构成员相同,例如:  
	
	flags.is_keyword,
	flags.is_extern
等;字段的作用与小整数相似,同其他整数一样,字段可以出现在算数表达式中,因此,可以表示为:
```c
	
	flags.is_extern = flags.is_static = 1;//置1
	flags.is_extern = flags.is_static = 0;//置0
	if(flags.is_extern == 0 && flags.is_static == 0)
		...//用于对is_extern和is_static的测试
```
字段的所有属性几乎都同具体的实现有关,字段可以不命名,无名字段(只有冒号和宽度)起填充作用,特殊宽度0可以用来强制在下一边界上对齐.字段不是数组,没有地址,不能做&取地址操作.  


#3. 结构数组

对于大小相同但是类型不同的数组,定义结构体数组对其很有帮组.例如:  
```c

	char *keyword[NKEYS];
	int   keycount[NKEYS];
```
这两个数组大小相同,因此 可以用另一种不同的组织方式,也就是结构数组.形如:  
```c
	
	struct key{
		char *word;
		int   count;
	}keytab[NKEYS];

```  
因此两个数组用一个结构体数组即可定义.  


