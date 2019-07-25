[toc]
## 转换流  
1. InputStreamReader:字节到字符的桥梁
2. OutputStreamWriter:字符到字节的桥梁

## 改变输入输出设备 
Java.lang包中的System类中的**setIn**和**setOut**方法。

```
System.setIn(new FileInputStream("PersonDemo.java"));
System.setOut(new PrintStream("zzz.txt"));
```

## 异常信息日志输出   
当程序运行异常时，e.printStackTrace()会在控制台打印出异常。  
将这些异常输出到日志示例：
```
import java.io.*;
class ExceptionInfo
{
    public static void main(String[] args) throws IOException
    {
        try
        {
            int arr[] = new int[2];
            System.out.println(arr[3]);
        }
        catch(Exception e)
        {
            try
            {
                System.setOut(new PrintStream("execption.log"));
            }
            catch(IOException a)
            {
                throw new RuntimeException("日志文件创建失败");
            }
            e.printStackTrace(System.out);
        }
    }
}
```
## 流操作规律 
一、明确数据源和目的     
源：输入流     InputStream    Reader    
目的：输出流    OutputStream    Writer    
二、操作的数据是否为纯文本    
纯文本：字符流    
非纯文本：字节流    
三、明确体系后，再明确要使用的具体对象    
通过设备区分：   
源设备：内存、硬盘、键盘   
目的设备：内存、硬盘、控制台      

# File类
该类位于java.io包中  

- 用来将文件或者文件夹封装成对象
- 方便对文件和文件夹的属性信息进行操作
- File对象可以作为参数传递给流的构造函数

字段    
static String separator：与系统有关的默认名称分隔符，为了方便，它被表示为一个字符串。

```
File f = new File("c:"+File.separator+"abc"+File.separator+"a.txt");
```
构造函数     
File(String pathname)：通过将给定路径名字符串转换为抽象路径名来创建一个新 File 实例。   

## File类常见方法  

```
1、创建
//在指定位置创建文件，如果文件已存在则不创建，返回false
boolean createNewFile()

//创建一级文件夹
boolean mkdir()

//创建多级文件夹
boolean mkdirs() 

2、删除
//删除文件，失败则返回false
boolean	delete() 

//在程序退出时删除指定文件
void deleteOnExit() 

3、判断
//文件是否存在
boolean exists() 

//是否是文件
boolean isFile() 

//是否是目录
boolean isDirectory() 

//是否是隐藏文件
boolean	isHidden()

//是否是绝对路径名
boolean	isAbsolute() 

4、获取 
//文件或者目录的名称
String getName() 

//文件最后一次被修改的时间
long lastModified() 

//绝对路径名字符串  
String getAbsolutePath() 

//路径名数组
File[] listFiles() 

//字符串数组
String[] list()
```

