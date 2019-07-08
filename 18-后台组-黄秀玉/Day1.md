一、基本常识
##### 1、软件开发：
软件：一系列按照特定顺序组织的计算机数据和指令的集合。

常见软件：系统软件（如DOS、windows、Linux）和应用软件（扫雷、迅雷、QQ）等。
开发：即制作软件。
##### 2、人机交互方式：
图形化界面：简单直观、容易上手操作。

命令行方式：在控制台输入特定指令，由计算机完后才能操作。较为麻烦，需要记住命令。

##### 3、常见dos命令行：
==dir==：列出当前目录下的文件以及文件夹 

==md==:创建目录  

==rd==:删除目录（必须保证是空文件夹）

==cd==:进入指定目录

==cd..==:退回到上一级目录

==cd/==:退回到根目录

==del==:删除文件   

del *.txt：删除该目录下txt格式文件 

==exi==t:退出dos命令行

==echo==可用于创建文档

例如：C:\abc>echo haha>1.txt 创建abc目录下的haha.txt文本

二、

##### 1、Java语言的三种技术架构：
J2EE企业版、J2SE标准版、J2ME小型版

Java5.0版本后改名为JavaEE、JavaSE、JavaME

##### 2、Java语言的特点：跨平台性
通过在操作系统上安装java虚拟机实现（分版本）。

##### 3、Java语言的环境搭建： 
JRE：java运行环境、
JDK：java开发工具包


三、

使用记事本通过class关键字定义一个类，在类中定义主函数并保存成一个扩展名为java的文件。

class Demo  
{
public static void main(String[] args)
{
System.out.println(“hello world”);
}
}

在dos控制台中通过javac工具对java文件进行编译。
==D:\java0217\day01\javac 123.java==
通过java命令对生成的class文件进行执行。
==D:\java0217\day01\java Demo==


四、
临时配置方式

set classpath=D:\java0217\day01

set classpath=         清空环境变量 

D:\java0217\day01>set classpath=c:\ （不加分号）

D:\java0217\day01>set classpath=c:\;d:\

先在classpath中寻找可执行文件找不到再在当前目录找，而使用set path时先在当前目录中寻找可执行文件找不到再在path中寻找。
可执行文件用path，java文件用classpath。

五、注释

单行注释//

多行注释/*内容 */ 
 
文档注释/** 内容 */

作用：注解说明程序，调试程序。
注意：多行注释里面不要嵌套多行注释。


