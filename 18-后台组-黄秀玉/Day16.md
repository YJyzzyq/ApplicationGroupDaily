[toc]
##  System类   
System类是系统类，系统级的很多属性和控制方法都放置在该类的内部。该类位于java.lang包。
 
public final class System extends Object 

System类包含一些有用的类字段和方法。它不能被实例化。方法均为静态方法。   

#### 方法
1、static Properties **getProperties**()： 确定当前的系统属性。

```
//获取系统所有属性信息
Properties prop = System.getProperties(); 
for(Object obj :prop.keySet())
{
    String value = (String)prop.get(obj);
    System.out.println(obj+"::"+value);
}
```
2、static String **getProperty**(String key)：获取指定键指示的系统属性。


```
//获取指定属性信息
String value = System.getProperty("os.name"); 
System.out.println("value="+value);
```
3、static String **setProperty**(String key, String value)：设置指定键指示的系统属性。   

```
//在系统中自定义特有信息
System.setProperty("mykey","myvalue");
```
## Runtime类   
该类位于java.lang包。    
每个 Java 应用程序都有一个 Runtime 类实例，使应用程序能够与其运行的环境相连接。

应用程序不能创建自己的 Runtime 类实例。  
#### 方法   
1、static Runtime **getRuntime**()：返回与当前 Java 应用程序相关的运行时对象。   
2、Process **exec**(String command)：在单独的进程中执行指定的字符串命令。  

```
Runtime r = Runtime.getRuntime();
r.exec("C:\\winmine.exe");
//注意需要抛异常
```

## Date类  
该类位于java.util包。
Date类中的很多方法均已过时。   

```
Date d = new Date();
System.out.println(d);
```

DateFormat类中的format方法提供格式，由于该类是抽象的，还需要其子类SimpleDateFormat用给定的模式和默认语言环境的日期格式符号构造SimpleDateFormat对象，再去格式化指定Date对象。     

String **format**(Date date)：将一个 Date 格式化为日期/时间字符串。    

```
SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 E hh:mm:ss");//将模式封装到SimpleDateFormat对象中
String time = sdf.format(d); //调用format方法让模式格式化指定Date对象
System.out.println("time="+time);
```
## Calendar类   
该类位于Java.util包中。
#### 方法  
1、int **get**(int field)：返回给定日历字段的值。    
2、static Calendar **getInstance**()：使用默认时区和语言环境获得一个日历。   
3、void **set**(int year, int month, int date)：设置日历字段 YEAR、MONTH 和 DAY_OF_MONTH 的值。   
4、abstract void **add**(int field, int amount)：根据日历的规则，为给定的日历字段添加或减去指定的时间量。


```
Calendar c = Calendar.getInstance();
sop(c.get(Calendar.YEAR)+"年");
sop((c.get(Calendar.MONTH)+1)+"月");
sop(c.get(Calendar.DAY_OF_MONTH)+"日");

String[] mos = {"一月","二月","三月","四月"
,"五月","六月","七月","八月"
,"九月","十月","十一月","十二月"};
int index = c.get(Calendar.MONTH);
sop(mos[index]); 
		
		
String [] weeks = {"","星期日","星期一","星期二","星期三","星期四","星期五","星期六"};
int index1 = c.get(Calendar.DAY_OF_WEEK);
sop(weeks[index1]);
```

## Math类    
该类位于java.lang包。方法均为静态的。    
#### 方法
static double **random**()：返回带正号的 double 值，该值大于等于 0.0 且小于 1.0。 

```
//产生0-10（不包括）中的十个double型随机数。
for(int x=0; x<10; x++)
{
    double d = Math.random();
    System.out.println(d);
}

//产生1-10（包括）中的十个整形随机数。
for(int x=0; x<10; x++)
{
    int d = (int)(Math.random()*10+1);
    System.out.println(d);
}
```
## Random类   
该类位于java.util包。此类的实例用于生成伪随机数流。   

#### 方法
int **nextInt**(int n)：返回一个伪随机数，它是取自此随机数生成器序列的、在 0（包括）和指定值（不包括）之间均匀分布的 int 值。

```
Random r = new Random();  
for(int x=0; x<10; x++)
{
    int d = r.nextInt(10)+1;
    System.out.println(d);
}
```
## IO流
- IO流用来处理设备之间的数据传输。
- Java对数据的操作是通过流的方式。
- Java用于操作流的对象都在IO包中。
- 流按操作数据分为：字节流和字符流。
- 流按流向分为：输入流和输出流。

### 流常用基类   

- 字节流的抽象基类   
   - InputStream
   - OutputStream
- 字符流的抽象基类    
   - Reader
   - Writer   

 
#### Writer类   
该类位于java.io包中。   
#### 方法   
1、void **write**(int c)：写入单个字符。  
2、abstract void **flush**()：刷新该流的缓冲。  
3、abstract  void **close**()：关闭此流，但要先刷新它。  

```
FileWriter fw = null;
try
{
    fw = new FileWriter("demo.txt");
    fw.write("abcdefg");
}
catch(IOException e)
{
    System.out.println("catch:"+e.toString());
}
finally
{
    try
    {
        if(fw!=null)
        fw.close();
    }
    catch(IOException e)
    {
        System.out.println("catch:"+e.toString());
    }
}
```
