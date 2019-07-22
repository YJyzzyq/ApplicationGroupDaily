[toc]

## 一、Collections工具类概述  
java.util.Collections   
此类完全由在 collection 上进行操作或返回 collection 的**静态**方法组成。它包含在 collection 上操作的多态算法，即“包装器”，包装器返回由指定 collection 支持的新 collection，以及少数其他内容。

如果为此类的方法所提供的 collection 或类对象为 null，则这些方法都将抛出 NullPointerException。  
## 二、Collections方法  
#### 排序   
1）static <T extends Comparable<? super T>> void **sort**(List<T> list)   
根据元素的**自然顺序**对指定列表按升序进行排序。   
2）static <T> void **sort**(List<T> list, Comparator<? super T> c)    
根据指定**比较器**产生的顺序对指定列表进行排序。    


```

class StrLenComparator implements Comparator<String>   
{
    public int compare(String s1,String s2)
    {
	if(s1.length()>s2.length())
	    return 1;
	if(s1.length()<s2.length())
	    return -1;
	return s1.compareTo(s2);
    }
}
public class CollectionsDemo 
{
    public static void sortDemo()
    {
        List<String> list = new ArrayList<String>();
        list.add("aaa");
        list.add("gf");
        list.add("aya");
        list.add("zz");
        list.add("meos");
        sop(list); //排序前
        Collections.sort(list); //按照自然顺序排序  
        sop(list); 
        Collections.sort(list,new StrLenComparator()); //按照长度排序
        sop(list);
    }

    public static void sop(Object obj)
    {
        System.out.println(obj);
    }
    
    public static void main(String[] args) 
    {
		sortDemo();
    }
}   
运行结果：
[aaa, gf, aya, zz, meos]
[aaa, aya, gf, meos, zz]
[gf, zz, aaa, aya, meos]
```

#### 查找   
1）static<T extends Object & Comparable<? super T>> T **max**(Collection<? extends T> coll)    
根据元素的**自然顺序**，返回给定 collection 的最大元素。   

```
Collections.max(list);
```

2）static <T> T **max**(Collection<? extends T> coll, Comparator<? super T> comp)    
根据指定**比较器**产生的顺序，返回给定 collection 的最大元素。    


```
Collections.max(list,new StrLenComparator());
```

3）static <T> int **binarySearch**(List<? extends Comparable<? super T>> list, T key)   
使用二分搜索法搜索指定列表，以获得指定对象。

```
int index = Collections.binarySearch(list,"zz");//binarySearch返回的是索引
System.out.println(index);
```

#### 替换   
1）static <T> void **fill**(List<? super T> list, T obj)     
使用指定元素替换指定列表中的所有元素。  
```
Collections.fill(list, "pp"); 
```
2）static <T> boolean **replaceAll**(List<T> list, T oldVal, T newVal)   
使用另一个值替换列表中出现的所有某一指定值。

```
Collections.replaceAll(list, "aaa", "pp");   
//"aaa"变为"pp"
```

#### 置换  
1）static void **swap**(List<?> list, int i, int j)   
在指定列表的指定位置处交换元素。  

```
Collections.swap(list,1,2);
System.out.println(list);  
//第2,3个数交换位置
```

#### 反转
1）static void **reverse**(List<?> list)  
反转指定列表中元素的顺序。

2）static <T> Comparator<T> **reverseOrder**()   
返回一个比较器，它强行逆转实现了 Comparable 接口的对象 collection 的自然顺序。   

```
TreeSet<String> ts = new TreeSet<String>(Collections.reverseOrder());    
//逆转按照自然顺序排序的比较器
TreeSet<String> ts = new TreeSet<String>(Collections.reverseOrder(new StrLenComparator()));   
//逆转自定义的比较器
```
## 三、Aarrays工具类概述  
java.util.Arrays   
此类包含用来操作数组（比如排序和搜索）的各种方法。此类还包含一个允许将数组作为列表来查看的静态工厂。

除非特别注明，否则如果指定数组引用为 null，则此类中的方法都会抛出 NullPointerException。  
   
##  四、将数组转为集合  
static <T> List<T> **asList**(T... a)    
返回一个受指定数组支持的固定大小的列表。

注意：不可以使用集合的增删方法，因为数组的长度是固定的。否则会出现UnsupportedOperationException异常。
```
String[]arr = {"abc","cc","kkkkk"};
List<String> list = Arrays.asList(arr);
//[abc, cc, kkkkk]

int [] arr = {1,2,3};
List<int []> list = Arrays.asList(arr);
//[[I@15db9742]

Integer [] arr = {4,5,6};
List<Integer> list = Arrays.asList(arr);
//[4, 5, 6]
```
注意：    
1、如果数组中的元素均为对象，那么变成集合时，数组中的元素就直接转成集合中的元素。      
2、如果数组中的元素都是基本数据类型，那么会将该数组作为集合中的元素存在。   
## 五、将集合转为数组   
Collection接口中的toArray方法     
<T> T[] **toArray**(T[] a)  
返回包含此 collection 中所有元素的数组；返回数组的运行时类型与指定数组的运行时类型相同。   

```
ArrayList<String> al = new ArrayList<String>();
al.add("abc1");
al.add("abc2");
al.add("abc3");
String[]arr = al.toArray(new String[0]);
String[]arr2 = al.toArray(new String[5]);
sop(Arrays.toString(arr));
sop(Arrays.toString(arr2));

//[abc1, abc2, abc3]
//[abc1, abc2, abc3, null, null]
```   
注意：  
1、当指定类型的数组长度小于集合的size时，那么该方法内部会建立一个新的数组，长度为集合的size。    
2、当指定类型的数组长度大于集合的size时，就不会创建新的数组，而是使用传进来的数组。   
3、集合转为数组是为了限定对元素的操作，不允许进行增删操作。

## 六、增强for循环  
从java 5.0开始，Java语言就有加强版的for循环-高级for循环，它是集合（Collection）中迭代器的简写形式。即集合中的迭代器可以使用高级for来代替。  

#### 高级for循环的局限
1、高级for循环只对集合进行遍历。只能获取集合元素，但是不能对集合进行操作。    
2、必须有一个被遍历的目标。   

建议在遍历数组的时候，还是用传统for，因为传统for有角标。

```
格式:
for(数据类型 变量名 ：被遍历的数组或者集合Collection)  
{}

```

```
eg：
HashMap<Integer,String> hm = new HashMap<Integer,String>();
hm.put(1,"a");
hm.put(2,"b");
hm.put(3,"c");	
Set<Integer> kS = hm.keySet();
for(Integer i : kS)
{
    System.out.println(i+":"+hm.get(i));
}

运行结果：
1:a
2:b
3:c
```
## 七、可变参数   
形式：类型... 参数名

示例：public void show(int... a) {};

可变参数在方法中被当作数组来处理。

#### 可变参数传值的四种方式

1、一个值也不传，可变参数会接收到长度为0的数组。      
2、传null，可变参数会接收到null。    
3、传数组，可变参数会接收到数组。   
4、传1个到多个数组元素值，可变参数会接收到数组。     


#### 可变参数和数组作为方法参数时的区别

1、从个数来看，可变参数只能有一个，数组可以有多个

2、从定义位置来看，可变参数只能定义在参数列表的末尾，数组可以在任何位置

3、从传参的形式来看，可变参数可以传数组、null、0个参数、一到多个参数，数组可以传数组引用、数组对象、null。