[toc]

# Set
集合Set没有特有方法，与父接口Collection的方法相同。

    |--Set:元素是无序的（存入和取出的顺序不一定一致），不可以有重复元素。

       |--HashSet:底层数据结构是哈希表。  
       |--TreeSet:底层数据结构是二叉树。
       
## HashSet
HashSet通过 **hashCode** 和 **equals** 两个方法保证元素的唯一性。       
先判断元素的HashCode是否相同，相同才判断equals是否为true。这两个方法都是在底层被自动调用的。判断元素是否存在以及删除都依赖这两个方法。 
## TreeSet
可以对Set集合中的元素进行排序。  
TreeSet通过 **compareTo** 方法 **return 0** 保证元素的唯一性。    
1、TreeSet排序的第一种方式（元素的 **自然顺序** 或者 **默认顺序** ）：让元素自身具备比较性。   
元素所属的类需要实现Comparable接口，覆盖comparaTo方法。    
2、TreeSet排序的第二种方式：让集合自身具备比较性。   
需要定义一个类，实现Comparator接口，覆盖compare方法，将该类实例化的比较器对象作为参数传递给TreeSet集合的构造函数。    
**注意**：当两种排序都存在时，以比较器为主。   
# 泛型   
#### 好处  
1、将运行时期出现的异常ClassCastException转移到了编译时期，便于程序员解决问题。   
2、避免了强制类型转换的麻烦。 
#### 格式  
通过<>来定义要操作的引用数据类型。 
#### 泛型类
当类中要操作的引用数据类型不确定时，定义泛型类来完成扩展。  


```
class Demo<T>
{
    public void show(T t)
    {
        System.out.println("show:"+t);
    }
}

Demo<Integer> d = new Demo<Integer>();
d.show(new Integer(4));
```

注意:泛型类定义的泛型，在整个类中有效。   
#### 泛型方法 
为了让不同方法可以操作不同的类型。

```
class Demo
{
    public <T> void print(T t)
    {
        System.out.println("print:"+t);
    }
}
Demo d = new Demo();
d.print("haha");
d.print(new Integer(4));
```

注意：静态方法不可以访问类上定义的泛型。  

#### 泛型接口  

```
interface Inter<T>
{
    void show(T t);
}

class InterImpl<T> implements Inter<T>
{
    public void show(T t)
    {
        System.out.println("show:"+t);
    }
}

InterImpl<Integer> i = new InterImpl<Integer>();
i.show(new Integer(4));
InterImpl<String> s = new InterImpl<String>();
s.show("hhhhhh");
```

#### 泛型限定
? 通配符（占位符）   
? extends E :
可以接收E类型或者E类型的子类型。上限。  
? super E：
可以接收E类型或者E类型的父类型。下限。