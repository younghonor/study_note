#cygwin添加到有右键菜单
##前提
为了在windows中使用cygwin编译指定文件代码更为方便，所以动心思琢磨把cygwin添加到右键菜单，百度了一下，发现很多这样的教程，但是有问题，比如添加了但是右键点击文件夹名并没有cd跳转到该文件名目录下,不断尝试后发现了更好的路径方法。
##添加右键菜单
开始->运行->regedit;  
在`HKEY_CLASSES_ROOT\Directory\Background\shell\` 下新建项自由命名如cygwin，在新命名的cygwin下新建项命名为command，双击command选项右边的默认，输入`D:\cygwin\Cygwin.bat  %V`其中`D:\cygwin\Cygwin.bat`为cygwin的安装路径。  
现在你在文件的目录下右键菜单就会出现cygwin.但是如果你想在文件名上右键菜单出现cygwin，你需要在`HKEY_CLASSES_ROOT\Directory\folder\shell\`路径下重新做以上步骤。
##修改cygwin.bat

	```c
    @echo off  
	set _T=%* 

	D:  
	chdir D:\cygwin\bin  
    
	@rem bash --login -i  
	```
如上，修改的目的是为了能够cd到_T指定的路径下。  
需要注意：**_T=%***之间不能有空格。
##修改.bash_profile
一般位于安装目录/home/(用户名)下,如果安装路径下没有home文件，你需要去c:/user/(用户名)下，并把安装路径下\etc\skel中的文件拷贝过去。
修改如下：

	```c
	export _T=${_T//\\//}  
	if [ $_T == "" ]; then  
	export _T="&{HOME}"  
	fi  
	cd "$_T"
	``` 
