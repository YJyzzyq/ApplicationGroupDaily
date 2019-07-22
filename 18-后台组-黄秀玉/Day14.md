[toc]
## 接口Map<K,V>  
存储键值对，双列集合。   
```
|-- 类型参数：   
K- 此映射所维护的键的类型  
V- 映射值的类型
```
```
已实现该接口的常用类：
|-- HashMap：底层是哈希表数据结构，允许使用null键和null键，该集合是不同步的。Jdk1.2效率高。
|-- TreeMap：底层是二叉树数据结构。线程不同步，可以给Map集合中的键进行排序。
|-- Hashtable：底层是哈希表数据结构，不可以存入null键和null值。该集合是同步的。Jdk1.0效率低。
```

键的唯一性：一个映射不能包含重复的键，每个键最多只能映射到一个值。

#### 接口Map中的方法  
##### 添加
###### put(K key,V value)

```
Map<String,String> map = new HashMap<String,String>();
map.put("01", "zhangsan");
```
##### 删除   
###### clear()
从此映射中移除所有映射关系。
###### remove(Object key)
如果存在一个键的映射关系，则将其从此映射中移除。
```
System.out.println("remove:"+map.remove("03"));
```
##### 判断
###### containKey(Object key)
如果此映射包含指定键的映射关系，则返回 true。
```
System.out.println("containsKey:"+map.containsKey("01"));
//返回值类型为boolean型
```
###### containsValue(Object value)
如果此映射将一个或多个键映射到指定值，则返回 true。  

###### isEmpty()
如果此映射未包含键-值映射关系，则返回 true。
```
System.out.println(map.isEmpty());
```
##### 获取
###### get(Object key)
返回指定键所映射的值；如果此映射不包含该键的映射关系，则返回 null。
```
System.out.println("get:"+map.get("01"));
```
###### size()
返回此映射中的键-值映射关系数。
```
System.out.println("size:"+map.size());
```
###### values()
返回此映射中包含的值的 Collection 视图。
```
Collection<String> coll = map.values();
System.out.println(coll);
```
### Map集合的两种取出方式
#### keySet方法
将Map中所有的键存入到set集合中。因为set具备迭代器。所有可以迭代方式取出所有的键，再根据get方法，获取每一个键对应的值。 

```
import java.util.*;
public class keySetDemo 
{
	public static void main(String[] args) 
	{
		Map<String,String> map = new HashMap<String,String>();
		map.put("ab", "zhangsan4");
		map.put("aa", "zhangsan1");
		map.put("ad", "zhangsan2");
		map.put("ac", "zhangsan3");
		
		Set<String> keySet = map.keySet();//获取map集合中的key的Set集合
		for(Iterator<String> it = keySet.iterator();it.hasNext();) 
		{
			String key = it.next();
			System.out.println(map.get(key));
		}
	}
}
```

#### entrySet方法  
**Set<Map.Entry<K,V>> entrySet()**   
返回此映射中包含的映射关系的Set视图。   
迭代后可以用接口Map.Entry中的getKey()，getValue()方法分别取key值和value值。    
Map.Entry是Map的一个内部接口。
```
import java.util.*;
public class EntrySetDemo 
{
	private static void method(Map<Integer, String> map) 
	{
		Set entrySet=map.entrySet();//entrySet()方法返回反应map键值的映射关系，存储在set集合中
		Iterator it=entrySet.iterator();//使用迭代器获得每一个映射关系
		while(it.hasNext())
		{
			Map.Entry me=(Map.Entry) it.next();//映射关系类型为Map.Entry类型，是一个接口类型
			System.out.println(me.getKey()+":::"+me.getValue());
		}
	}
	public static void main(String[] args) 
	{
		Map<Integer, String> map=new HashMap<Integer, String>();
		map.put(8, "wangwu");
		map.put(2, "lisi");
		map.put(7, "zhangsan");
		map.put(6, "xuliu");
		method(map);
	}
}
```
