[toc]


# 集合类    
1. 数组和集合类均为容器，二者的不同点： 集合只能存储对象，而数组既可以存储对象，也可以存储基本数据类型，只不过一个数组只能存储同种数据类型；集合长度可变，而数组长度是固定的。      
2. 集合类的特点：只用于存储对象，集合长度是可变的，集合可以存储不同类型的对象。    
3. 集合框架中分多种容器的原因：每一个容器对数据的存储方式（数据结构）不同。  

导包： 
```

import java.util.*;
```

使用Collection接口的子类ArrayList创建一个集合容器。   

```
ArrayList al = new ArrayList();   
Person p = new Person();
al.add(p);

注意：集合中存放的是对象的引用(地址)。 
```

## collection接口中常用的共性方法   
#### 1、add()
添加元素，参数类型是Object，以便接收任何类型的数据。
#### 2、size()
获取元素个数，集合长度。  
#### 3、remove()
删除元素。   
#### 4、clear()
清空集合。   
#### 5、contains()
判断集合中是否存在某个元素。
#### 6、isEmpty()
判断集合是否为空，空时即为True,长度为0。

#### 7、retainAll()
取交集。  

```
ArrayList a = new ArrayList();    
ArrayList b = new ArrayList();   
a.add("123");    
a.add("456");    
b.add("123");     
b.add("789");    
a.retainAll(b);
结果为[123]，a中只保留与b共同拥有的部分。
```
#### 8、removeAll()
去掉共有的部分元素。  


```
System.out.println(a);
打印所有的元素。
```

```
Iterator it = a.iterator();//获取迭代器，用于取出集合中的元素。
接口型引用只能指向自己的子类对象。
该对象是通过集合a的iterator方法获取的。  
while(it.hasNext())  
{
    System.out.println(it.next());
}
等同于：
for(Iterator it = a.iterator();it.hasNext())
{
    System.out.println(it.next());
}

```
 
## 接口Iterator中的方法 
#### 1、hasNext()
如果仍有元素可以迭代，则返回 true。
#### 2、next()
返回迭代的下一个元素。
#### 3、remove()
从迭代器指向的 collection 中移除迭代器返回的最后一个元素（可选操作）。 

## Collection的子接口-List中的特有方法    


```
ArrayList a = new ArrayList();   
a.add("C语言");   
a.add("C++");    
a.add("数据库");    
```

#### 1、add(index,element)
在指定位置index处添加元素。 

```
a.add(1,"java");   
[C语言, java, C++, 数据库]
```

#### 2、addAll(index,Collection)
#### 3、remove(index)
删除指定位置的元素。   

```
a.remove(2);
[C语言, C++]
```

#### 4、set(index,element)
修改指定位置处的元素。

```
a.set(1,"hello");
[C语言, hello, 数据库]
```

#### 5、get(index)
返回列表中指定位置的元素。

```
a.get(2);
数据库
```

#### 6、subList(fromIndex,toIndex)
返回列表中指定的 

fromIndex（包括）和toIndex（不包括）之间的部分视图。  返回值为List。


```
List sub = a.subList(0,2);
System.out.printl(sub);
[C语言, C++]
```

#### 7、indexOf(Object)
返回此列表中第一次出现的指定元素的索引；如果此列表不包含该元素，则返回-1。

```
a.indexOf("C++");
1
```
## Iterator的子接口-ListIteror中的方法  

```
ArrayList al = new ArrayList();   
al.add("java01");
al.add("java02");   
al.add("java03");
sop(al);
ListIterator li = al.listIterator();
while(li.hasNext())
{
    Object obj = li.next();
    if(obj.equals("java02"))
    可更改内容;
}
sop(al);
```



####  1、Object previous()
返回列表中的前一个元素。
#### 2、boolean hasPrevious()
如果以逆向遍历列表，列表迭代器有多个元，则返回 true。




```
while(li.hasPrevious())
{
    sop(li.previous());
}
```



####  3、void set(Object e) 
用指定元素替换next或previous返回的最后一个元素。
```
li.set("java006");

[java01, java02, java03]
[java01, java006, java03]
```

#### 4、void add(Object e) 
将指定的元素插入列表。

```
li.add("java009");

[java01, java02, java03]
[java01, java02, java009, java03]

```
注意：   
在迭代时，不可以通过集合对象的方法操作集合中的元素，不然会发生ConcurrentModificationException异常。    
Iterator的方法有限，只能对元素进行判断，取出，删除的操作。所以需要ListIterator子接口进行添加、修改的操作。

## Enumeration接口中的方法
#### 1、boolean	hasMoreElements() 
测试此枚举是否包含更多的元素。
#### 2、Object nextElement() 
如果此枚举对象至少还有一个可提供的元素，则返回此枚举的下一个元素。   

```
Vector v = new Vector();
v.add("java01");
v.add("java02");
v.add("java03");
v.add("java04");
Enumeration en = v.elements();
while(en.hasMoreElements())
{
 System.out.println(en.nextElement());
}

```
## LinkedList特有方法
#### 1、addFirst(Object e)
将指定元素插入此列表的开头。
#### 2、addLast(Object e) 
将指定元素添加到此列表的结尾。   

```
LinkedList link= new LinkedList();
link.addLast("java01");
link.addLast("java02");
link.addLast("java03");
link.addLast("java04");
sop(link);

```

#### 3、Object getFirst() 
返回此列表的第一个元素。  

```
sop(link.getFirst());
```

#### 4、Object getLast() 
返回此列表的最后一个元素。   

```
sop(link.getLast());
```

#### 5、Object removeFirst() 
移除并返回此列表的第一个元素。  

```
sop(link.removeFirst());
```

#### 6、Object removeLast() 
移除并返回此列表的最后一个元素。  

注意：3、4、5、6种方法，如果集合中没有元素，则会出现NoSuchElementException异常。

JDK1.6出现了替代方法：offerFirst()和peekFirst()。