[toc]
# IO包中的其他类 
## 打印流  

可以将各种数据类型的数据原样打印。  

- 字节打印流  PrintStream
- 字符打印流  PrintWriter 

PrintWriter类实现了在PrintStream类中的所有print方法。 

PrintSteam构造函数可以接收的参数类型：  
File类型、字符串文件名、字节输出流OutputStream    

PrintWriter构造函数可以接收的参数类型：  
File类型、字符串文件名、字节输出流OutputStream、字符输出流Writer

## SequenceInputStream类
表示其他输入流的逻辑串联。它从输入流的有序集合开始，并从第一个输入流开始读取，直到到达文件末尾，接着从第二个输入流读取，依次类推，直到到达包含的最后一个输入流的文件末尾为止。  


## 对象的序列化  
- 序列化：把对象转换为字节序列的过程称为对象的序列化。
- 反序列化：把字节序列恢复为对象的过程称为对象的反序列化。

对象的序列化主要有两种用途：    
1）把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中。    
2）在网络上传送对象的字节序列。

### serialVersionUID的取值
serialVersionUID的取值是Java运行时环境根据类的内部细节自动生成的。如果对类的源代码作了修改，再重新编译，新生成的类文件的serialVersionUID的取值有可能也会发生变化。

为了提高serialVersionUID的独立性和确定性，强烈建议在一个可序列化类中显示的定义serialVersionUID，为它赋予明确的值。

显式定义serialVersionUID有如下两种用途： 

1） 希望类的不同版本对序列化兼容时，需要确保类的不同版本具有相同的serialVersionUID。     
2） 不希望类的不同版本对序列化兼容时，需要确保类的不同版本具有不同的serialVersionUID。

```
public static final long serialVersionUID = 10L;
```
使用**writeObject**() 和**readObject**()方法的对象必须已经被序列化。   

类实现**Serializable**接口（标记接口）才能进行序列化。

将不需要序列化的属性前添加关键字**transient**，序列化对象的时候，这个属性就不会序列化到指定的目的地中。
## 管道流
管道流是用来在多个线程之间进行信息传递的Java流，它提供了多线程间信息传输的一种有效手段。   
管道流包括两个类PipedOutputStream和PipedInputStream。  

```
void connect(PipedOutputStream src)
使此管道输入流连接到管道输出流 src。
```
注意：    
- 管道流仅用于多个线程之间传递信息，若用在同一个线程中可能会造成死锁
- 管道流的输入输出是成对的，一个输出流只能对应一个输入流，使用构造函数或者connect函数进行连接
- 一对管道流包含一个缓冲区，其默认值为1024个字节，若要改变缓冲区大小，可以使用带有参数的构造函数
- 管道的读写操作是互相阻塞的，当缓冲区为空时，读操作阻塞；当缓冲区满时，写操作阻塞
- 管道依附于线程，因此若线程结束，则虽然管道流对象还在，仍然会报错“read dead end”
- 管道流的读取方法与普通流不同，只有输出流正确close时，输出流才能读到-1值


## RandomAccessFile类
特点：
不算是IO体系中子类，该类直接继承自Object，是IO包成员，具备读写功能，内部封装了一个数组，可以通过指针对数组的元素进行操作，直接跳到文件的任意位置来读写数据。 

以下两个方法用来操作文件的记录指针.
- long **getFilePointer**()：     
返回文件记录指针的当前位置
- void **seek**(long pos)：  
将文件记录指针定位到pos位置

RandomAccessFile类包含了一系列的readXXX()和writeXXX()方法来完成输入和输出。（XXX）表示各种数据类型。  

RandomAccessFile有两个构造函数，二者指定文件的形式不同，一个使用String参数来指定文件名，一个使用File参数来指定文件本身。而且还需要指定一个mode参数。   

mode参数指定RandomAccessFile的访问模式，有以下4个值：  
- **"r"** 以只读方式打开。调用结果对象的任何 write 方法都将导致抛出 IOException。  
- **"rw"** 打开以便读取和写入。如果该文件尚不存在，则尝试创建该文件。
- **"rws"**	打开以便读取和写入，对于 "rw"，还要求对文件的内容或元数据的每个更新都同步写入到底层存储设备。
- **"rwd"** 打开以便读取和写入，对于 "rw"，还要求对文件内容的每个更新都同步写入到底层存储设备。  

## ByteArrayInputStream类  
继承了抽象类InputStream，本质上也是一个存储在堆内存中的byte数组，这个数组必须在构造时传入并直接被使用而不是复制，之后大小无法改变。

包含一个内部缓冲区，该缓冲区包含从流中读取的字节。内部计数器跟踪read方法要提供的下一个字节。

关闭 ByteArrayInputStream 无效。此类中的方法在关闭此流后仍可被调用，而不会产生任何 IOException。

## ByteArrayInputStream类  
继承了抽象类OutputStream，本质是一个存在于堆内存中的可扩展byte数组，因为所有操作都在内存中所以flush()也什么都没做。

此类实现了一个输出流，其中的数据被写入一个 byte 数组。缓冲区会随着数据的不断写入而自动增长。可使用 toByteArray() 和 toString() 获取数据。

关闭ByteArrayOutputStream无效。此类中的方法在关闭此流后仍可被调用，而不会产生任何 IOException。


```
public static void main(String[] args) 
{
    ByteArrayInputStream bis = new ByteArrayInputStream("ABCDEFG".getBytes());
    ByteArrayOutputStream bos = new ByteArrayOutputStream();
    int by = 0;
    while((by=bis.read())!=-1)
    {
        bos.write(by);
    }
    System.out.println(bos.size());
    System.out.println(bos.toString());
}
```



