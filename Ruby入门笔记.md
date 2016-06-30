![ruby](http://i.imgur.com/YyupAwF.jpg)
#Ruby入门到精通

##Ruby环境的搭建(windows)
###1.获得和安装Ruby  
从 http://rubyforge.org/frs/?group_id=167 下载最新RubyInstaller    
安装需要勾选"Add Ruby executables to your PATH"  
安装结束后，运行`ruby -v` 显示版本号。如果正常显示Ruby版本号，表示安装成功。  
如没有成功,自行添加环境变量
###2.获得和安装RubyGems  
从 http://rubyforge.org/frs/?group_id=126 下载rubygems最新版本  
把下载文件解压到一个临时目录，假设为F:/temp/rubygems-1.5.2，执行：  

	cd F:/temp/rubygems-1.5.2  
	ruby setup.rb
  
然后通过gem -v 验证安装是否成功.  


##Ruby语法

1. Ruby的输出  
	1. "puts" 输出的时候 结尾带上回车符,就是会自动换行.   
	2. "print" 功能一样,但是没有回车符,不自动换行.   
	3. "printf" 像C和java5一样格式化输出.  
	4. 从控制台读取使用gets.  
2. Ruby的方法
	1. Ruby的方法跟python一样由`def`开头,而由end结尾,没有大括号,没有起始冒号.  
	2. 方法调用时,括号是可以省略.
    3. 方法返回可以不使用return, 且可以有多个返回值.
3. Ruby的class与module  
	Ruby中支持类的概念，支持类的定义、继承（不允许继承多个父类）、限定方法的访问范围、Setter和Getter的设置等.  
	Ruby中提供了 public、private、protected 三个方法访问限定符，可以对单个或批量的方法制定访问的限制条件。可以单独对单个方法进行访问限定，也可以使用批量的方式对多个方法使用访问限定。
    默认情况下，所有的方法都是 public ，除了 initialize 之外，它始终是一个 private 的方法。  

```ruby  
	#类
	class ClassName  
		def   
		end  
	end  
	
	#类的继承   
	class People   
	end  
	class Male < People  
	end 
	 
	#模块的定义
	module moduleName  
	end  
```   
    
	1. ruby中，你可以向已有类库中添加方法.  
	2. ruby字符串处理类中是没有的，要是写的话 `if(mystring != null && mystring != "")` 这样是最普遍的表示方法了.
 
4. Ruby的变量名分类  
	标识符是变量，常量及方法。 Ruby的标识符是区分大小写的。Ram和RAM在Ruby中是两个不同意思的标识符.    
	Ruby的标识符名称可以由字母数字字符和下划线( _ ).  
	1. 全局变量开始以'$'开始.  
	2. 类变量'@@'开始.  
	3. 实例变量以'@'开始.
	4. 局部变量，方法名和方法参数 以小写字母开头.  
	5. 类名称，模块名称和常量以大写字母开始.  
	6. 变量名称由字母，数字和下划线.  
	7. 方法名称可能结束以“？”，“！”，或“=”结尾。“？”结尾的方法 意味着布尔运算（例如，“in​​stance_of？”）。“！” 结尾的方法意味着危险的东西，比如字符串被修改的地方（例如，“UPCASE！”）
5. Ruby语法中的空格
	在Ruby代码一般都忽略空白字符，例如空格和制表符，除非当它们出现在字符串中。但是，有时它们被使用解释模棱两可的报表。诠释这种类型`-w`选项启用时产生警告。  
6. Ruby程序行结尾
	Ruby解释一个语句中以分号和换行符表示结束。但是，如果Ruby遇到运算符，如+，- 或反斜杠结尾的行，则表示语句继续.
7. Ruby保留字  
	![ruby保留字](http://i.imgur.com/MYdgEt6.jpg)    
8. Ruby中heredoc  
	"Here Document" 是指建立多行字符串。继<<可以指定一个字符串或者一个标识符来终止字符串字面，当前行之后的所有行的终止符字符串的值.  
	如果终止符是引用，引号的类型决定面向行的字符串常量的类型。注意<<终止符之间不能有空格.

```ruby    
	print <<EOF     
    This is the first way of creating    
    here document ie. multiple line string.    
	EOF    
```  

9. Ruby BEGIN/END 语句   
	声明代码在程序运行之前被调用.  

```ruby  
	BEGIN {
   		code
	}
```

	声明代码被称为程序的结束. 

```ruby  
	END {
   		code
	}
```

10. Ruby文件的一般开头格式  

	> 	#! /usr/bin/ruby -w   
	> 	# -*- coding: UTF-8 -*-  

11. Ruby运算符  
	1. 操作运算符 +、-、*、/、%、**(乘方)  
	2. 比较运算符 >=、<=、==、<>、===  
	3. 逻辑运算符 &&、||、and、or  
	4. 位运算符   &、|、~、^、>>、<<  

12. Ruby中的真值与假值  
	Ruby中，在进行判断时，false 和 nil 都为假，除此以外的所有值为真。nil 是一个特殊值，用于在正则表达式中表示没有找到匹配的内容。也就是说，**0 在ruby中也是真值**.  
13. Ruby中的Symbol  
	在Ruby中Symbol表示“名字”，比如字符串的名字、标识符的名字，创建一个Symbol对象的方法是在名字或者字符串之前加上":".  
14. Ruby控制语句  
		
> 

 	1. 条件语句  

```ruby   
	if condition then...    
	elsif condition then...    
	else...    
	end      
```  

```ruby       
	unless condition then...    
	else...    
	end      
```  

	2. 分支判断  

```ruby  
	case condition  
	when value1 then...  
	when value2 then...   
	else...  
	end  
```

	3. 循环控制  

	循环控制语句用在我们希望重复执行一些动作时，使用循环控制语句，需要注意两个要点： 一个是循环的条件、一个是循环的次数.    
	Ruby中提供了for、while、until三个循环控制语句，each、times、loop三个循环控制方法，我们可以根据需要选择不同的方式.Ruby同时提供了三个循环控制的语句，包括：break、next、redo.  

```ruby    
	while condition do...  
	end
```  
	
```ruby    
	for var in object do...  
	end
```  

```ruby    
	until condition do...  
	end
```  

```ruby    
	obj.each{|var|, block}  
```  
	
```ruby    
	loop{...}   
```  
 15. Ruby中常用的类

	1. Numeric类  
	2. Array类  
		数组的创建有多种方式：
		1. 使用 []。
		2. 使用 Array.new
		3. 类似于Perl的数组创建方式，使用%w进行创建。
		4. 使用 obj.to_a 方法，将对象转换为数组。
		5. 使用split方法，将字符串分割为数组。


	3. String类  
		String的创建方式有:  
		1. 直接使用"或者'新建
     	2. String.new新建
     	3. 使用%Q和%q的方式新建


	4. Hash类  
	5. 正则表达式类（Regexp）  
	6. IO类  
		IO是每个程序语言必不可少的部分，通常IO有三个，标准输入、标准输出、错误输出。
		对于Console来说，Ruby中使用$stdin、$stdout、$stderr来表示。
		文件IO是我们平时编程中最常用到的一种。
		Ruby和其他语言一样，提供了open、close、seek、popen、gets、readline、read等函数,
		来帮助我们完成文件的读取、修改、保存操作。
	7. File和Dir类  
	8. Time、Date、DateTime类  
	9. Ruby中的进程与线程  


16. 错误与例外处理

错误处理的一般形式:  

```ruby  
	begine

          block

     rescue=> ex #rescue遇到例外时进行错误处理

          print ex.message

          block

     ensure #ensure确保不管在什么情况下它下面的代码部分都会执行

          block

          retry #retry 重新尝试从 begin 开始的代码

     end
```

默认情况下 $!返回例外对象，$@返回例外信息.    
Ruby 提供了catch throw 的语法，但是这个和其他语言貌似区别很大.    
Ruby提供了一个标准的例外类，其下有众多的子类来表示不同的例外情况.    