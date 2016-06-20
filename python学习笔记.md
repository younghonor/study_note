#1.关于#!/usr/bin/env python
这只是告诉操作系统这个脚本的解释、执行程序的具体位置，加了这个头，在"X"类操作系统中就直接可以这样执行脚本了“hello.py”,否则的话就得这样执行“python hello.py”.
区别：  
	`#!/usr/bin/python `  直接告诉计算机执行程序的具体位置  
	`#!/usr/bin/env python` 告诉计算机执行程序在系统环境变量中的名字，详细位置在环境变量中设置好了  

这些都是非必要的，因为在执行脚本时，可以用详细路径来标明：
   ` /usr/bin/python hello.py`  
在windows中也可以这样，不过一般设置了环境变量后可以直接“hello.py”.
#2.格式化输出
指定占位符宽度：
    `print ("Name:%-10s Age:%08d Height:%8.2f"%("Aviad",25,1.83))`  
科学计数法
	`format(0.0015,'.2e')`
#3.关于#-*- coding:utf-8 -*-
用来程序指定编码格式
#4.关于缩进4个空格
对于函数，循环，判断都需要正确的缩进
#5.关于注释
单行使用#开头  
多行使用'''或者"""  
#6.异常处理和捕获
try...except:   
  
	try：  
		file("hello.txt", "r")#如果文件不存在，引发异常  
		print "读文件"  
	except IOError:  #捕获IO异常  
		print "文件不存在"  
	except： #其它异常  
		print "程序异常"  
 
try...finally:    

	try:   
    	f = open("hello.txt", "r")  
     	try:  
        	print f.read(5)  
     	except:  
        	print "读文件异常"  
     	finally:  
        	print "释放资源"  
        	f.close()  
	except IOError:
     	print "文件不存在"  

使用raise抛出异常:

	try:
    	s = None
     	if s is None:
        	print "s 是空对象"
         	raise NameError #如果引发NameError异常，后面的代码将不能执行
     	print len(s)
	except TypeError:
    	print "空对象没有长度"

自定义异常：  
assert断言语句:  

#7.基本数据类型

> |整形| int| 1,2|   
> |----|---|----|  
> |浮点| float| 1.20|   
> |布尔| bool| b == True|      
> |字符串| str| 'str'或者"str"|    
> |列表| list| [1,2,4,5]|    
> |元组| tuple| ('d', 300)|    
> |字典| dirt| {'name':'coco','country':'china'}|    

#8.pygame
开发游戏软件很不错的库
