###### 一、Java中已有的排序方法  
import.java.util.*;    
Arrarys.sort(arr);//对arr数组进行排序。   
###### 二、冒泡排序法与选择排序法的区别     
- 选择排序法是按顺序将一个数与后面所有数比较，每趟选出一个最值。内循环结束一次，最值出现在第一位。从前往后确定顺序。   
 for(int x=0;x<arr.length-1;x++)     
 for(int y=x+1;y<arr.length;y++)   
- 冒泡排序法是相邻的两个元素进行比较，如果符合条件换位。最值出现在最后一位。从后往前确定顺序。    
for(int x=0;x<arr.length-1;x++)    
for(int y=0;y<arr.length-x-1;y++)     
###### 三、数组   
- 对于二维数组“数组名.length”的值是它含有的一维数组的个数。   
- 与C语言不同的是，Java允许使用int型变量的值指定数组的元素的个数。  
- 索引越界时，编译可以通过，但是运行时会发生ArrayIndexOutOfBoundsException异常。 
- 易错：int[]a,b[];等价于int a[],b[][];  一维数组a,二维数组b;
###### 四、成员变量与局部变量的区别    
- 作用范围：成员变量作用于整个类中，局部变量作用于函数或者语句中。   
- 在内存中的位置：局部变量在堆内存中，成员变量在栈内存中。   
###### 五、匿名对象使用方式    
- 对对象的方法仅进行一次调用时   
- 作为实际参数进行传递

###### 六、类的封装性  
好处：a.将变化隔离  b.便于使用  c.提高重用性，安全性  

**私有仅仅是封装的一种表现形式**。
###### 七、StringBuffer类 
创建一个StringBuffer对象s      
StringBuffer s=new StringBuffer();   
- StringBuffer类的常用方法：
 
   - StringBuffer append(String s):将String对象s的字符序列追加到当前StringBuffer对象的字符序列中，并返回当前StringBuffer对象的引用。
   - public StringBuffer reverse():将对象实体中的字符序列翻转，并返回当前对象的引用。   

###### 八、构造函数与构造代码块 
- 构造代码块优先于构造函数执行。   
- 构造代码块给所有对象进行统一初始化，而构造函数给对应的对象初始化。   
###### 九、this关键字   
- 可以区分成员变量和局部变量同名的情况。 
- this代表它所在函数所属对象的引用。