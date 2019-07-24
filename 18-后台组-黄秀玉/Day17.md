[toc]
# 字符流的缓冲区 
- 缓冲区的出现提高了对数据的读写效率。
- 缓冲区需要结合流才可以使用。
- 在流的基础上对流的功能进行了增强。

## BufferedWriter类
java.io包
```
public class BufferedWriter extends Writer
```
将文本写入字符输出流，缓冲各个字符，从而提供单个字符、数组和字符串的高效写入。  

```
常用的方法：   

// 关闭此流，但要先刷新它，实际上调用了Writer类的close方法       
public void close() throws IOException

// 刷新该流的缓冲    
public void flush() throws IOException 

// 写入字符数组的某一部分 
public void write(char[] cbuf, int off, int len) throws IOException  

// 写入单个字符 
public void write(int c) throws IOException

特有的方法：

// 写入一个行分隔符。行分隔符字符串由系统属性 line.separator 定义     
public void newLine() throws IOException
```

```
示例：
BufferedWriter bufw = new BufferedWriter(fw);
//使用缓冲区中的方法将数据写入到缓冲区中。
bufw.write("hello world !");
bufw.newLine();
bufw.write("!hello world !");
bufw.write("!hello world !");
//使用缓冲区中的方法，将数据刷新到目的地文件中去。
bufw.flush();
//关闭缓冲区,同时关闭了fw流对象
bufw.close();	
```

## BufferedReader类  
java.io包  
从字符输入流中读取文本，缓冲各个字符，从而实现字符、数组和行的高效读取。  

```
public class BufferedReader extends Reader
```

```
构造方法：
1、BufferedReader public BufferedReader(Reader in)
创建一个使用默认大小输入缓冲区的缓冲字符输入流。
2、BufferedReader public BufferedReader(Reader in,int sz)
创建一个使用指定大小输入缓冲区的缓冲字符输入流。
参数：
in - 一个 Reader
sz - 输入缓冲区的大小
```

```
常用的方法：

// 关闭该流并释放与之关联的所有资源 
public void close() throws IOException 

// 将字符读入数组的某一部分 
public int read(char[] cbuf, int off, int len) throws IOException  

// 读取单个字符  
public int read() throws IOException

特有的方法：

// 读取一个文本行。通过下列字符之一即可认为某行已终止：换行 ('\n')、回车 ('\r') 或('\r\n') 
public String readLine() throws IOException  
```

```
示例：

public static void main(String[] args) throws Exception 
{        
    //创建字符缓冲输入流对象
    BufferedReader br = new BufferedReader(new FileReader("bw.txt"));        
    //读数据
    //一次读取一个字符数组
    char[] chs = new char[1024] ;
    int len = 0 ;
    while((len=br.read(chs))!=-1)
    {
        System.out.println(new String(chs,0,len));
    }
    //释放资源
    br.close();
}


public static void main(String args[]) throws IOException
{
    String mystring;
    int myint;
    BufferedReader buf=new BufferedReader(new InputStreamReader(System.in));
    System.out.println("input an integer");
    mystring=buf.readLine();
    myint=Integer.parseInt(mystring);
    System.out.println("the integer is="+myint);
}

```
## 用BufferedReader和BufferedWriter复制文本文件示例   

```
public class TextCopyByBuf 
{
    public static void main(String[] args) throws IOException 
    {
        BufferedReader bufr = new BufferedReader(new FileReader("C:\\demo.txt"));
        BufferedWriter bufw = new BufferedWriter(new FileWriter("D:\\love.txt"));
        //一行一行的寫。
        String line = null;
        while((line = bufr.readLine()) != null)
        {
            bufw.write(line);
            bufw.newLine();
            bufw.flush();
            
        }
        /*
        一個字節一個字節的寫。
        int ch = 0;
        while((ch = bufr.read())!=-1)
        {
            bufw.write(ch);
        }
        */
        bufr.close();
        bufw.close();
    }
}
```

## LineNumberReader类
跟踪行号的缓冲字符输入流。默认情况下，行编号从0开始。   
java.io包 BufferedReader类的子类

```
public class LineNumberReader extends BufferedReader
```

```
常用方法：

//获得当前行号。
public int getLineNumber()

//设置当前行号。  
public LineNumberReader(Reader in,int sz)
```

```
示例：
FileReader fr=new FileReader("fos.txt");
LineNumberReader lnr=new LineNumberReader(fr);
String line=null;
lnr.setLineNumber(1000);
while((line=lnr.readLine())!=null)
{
    System.out.println(lnr.getLineNumber()+":"+line);
}
lnr.close();
```

     

## 自定义字符流缓冲区   

```
import java.io.*;

class MyBufferedReader extends Reader   
{
	private Reader r;     
	MyBufferedReader(Reader r)
	{
		this.r = r;
	}
	public String myReadLine() throws IOException     
	{
		StringBuilder sb = new StringBuilder();  
		int ch = 0;
		while((ch=r.read())!=-1)  
		{
			if(ch=='\r')
				continue;
			if(ch=='\n')
				return sb.toString();  
			else 
				sb.append((char)ch);  
		}
		if(sb.length()!=0)    
			return sb.toString();
		return null;
	}
	public void myClose() throws IOException
	{
		r.close();
	}
	
	public int read(char[] cbuf , int off, int len) throws IOException
	{
		return r.read(cbuf,off,len);
	}
	public void close() throws IOException
	{
		r.close();
	}
}

public class MyBufferedReaderDemo 
{
	public static void main(String[] args) throws IOException
	{
		FileReader fr = new FileReader("fos.txt");
		MyBufferedReader myBuf = new MyBufferedReader(fr);
		String line = null;
		while((line = myBuf.myReadLine())!=null)
		{
			System.out.println(line);
		}
		myBuf.myClose();
	}
}
```
## OutputStream类  
java.io包    
此抽象类是表示输出字节流的所有类的超类。输出流接受输出字节并将这些字节发送到某个接收器。

需要定义 OutputStream 子类的应用程序必须始终提供至少一种可写入一个输出字节的方法。
```
public abstract class OutputStream extends Object implements Closeable, Flushable
```

```
public static void main(String[] args) throws IOException 
{
    FileOutputStream fos = new FileOutputStream("fos.txt");
    fos.write("hello,io".getBytes()); 
    //参数是byte数组，需要调用String的getBytes()方法
    fos.close();
}
```


## InputStream类   
java.io包  
此抽象类是表示字节输入流的所有类的超类。

需要定义 InputStream 子类的应用程序必须总是提供返回下一个输入字节的方法。
```
public abstract class InputStream extends Object implements Closeable
     
```

```
方法：
available public int available() throws IOException
//返回此输入流下一个方法调用可以不受阻塞地从此输入流读取（或跳过）的估计字节数。下一个调用可能是同一个线程，也可能是另一个线程。一次读取或跳过此估计数个字节不会受阻塞，但读取或跳过的字节数可能小于该数。
```

```

FileInputStream fis = new FileInputStream("fos.txt");
byte [] buf = new byte[fis.available()];
fis.read(buf);
System.out.println(new String(buf));
fis.close();
```


## 装饰设计模式   
装饰模式指的是在不必改变原类文件和使用继承的情况下，动态地扩展一个对象的功能。它是通过创建一个包装对象，也就是装饰来包裹真实的对象。
### 装饰和继承的区别
- 装饰是构造函数参数传递进行增强。
- 装饰模式比继承要灵活。避免了继承体系臃肿。    
- 降低了类于类之间的关系。    
- 装饰类因为增强已有对象，具备的功能和已有的是相同的，只不过提供了更强功能。    
- 装饰类和被装饰类通常是都属于一个体系中的。   

