## StringBuffer简介
- 字符串的组成原理就是通过该类实现的。
- StringBuffer可以对字符串内容进行增删。
- StringBuffer是一个容器。
- 很多方法和String相同。
- StringBuffer是可变长度的。

## StringBuilder   
与StringBuffer没什么区别，主要是StringBuilder线程不同步，而StringBuffer线程同步。   

## StringBuffer常见方法
- 存储
   - append
   - insert
- 删除
   - delete
   - deleteCharAat
- 获取
   - CharAt
   - indexOf
   - lastIndexOf
   - length
   - substring
- 修改
   - replace
   - setCharAt
- 反转
   - reverse 

方法细讲：   
**存储：**    
1、StringBuffer **append**(基本数据类型 d)：将指定数据作为参数添加到已有数据结尾处。     
注意：参数没有byte和short类型。        
2、StringBuffer **insert**(int offset,数据)：将数据插入到指定offset位置。    
**删除：**     
1、StringBuffer **delete**(int start, int end)：删除数据，包含start，不包含end。     
2、StringBuffer **deleteCharAt**(int index)：移除指定位置的数据。     
**获取：**        
1、char **charAt**(int index)：返回此序列中指定索引index处的char值。      
2、int	**indexOf**(String str)：返回第一次出现的指定子字符串str在该字符串中的索引。          
3、int	indexOf(String str, int fromIndex)：从指定的索引fromIndex处开始，返回第一次出现的指定子字符串str在该字符串中的索引。  
4、int **lastIndexOf**(String str)： 返回最右边出现的指定子字符串str在此字符串中的索引。        
5、int lastIndexOf(String str, int fromIndex)：返回最后一次出现的指定子字符串在此字符串中的索引。       
6、int **length**()：返回长度。       
7、String **substring**(int start)：返回一个从start位置开始的新的String。       
8、String substring(int start, int end)：返回一个从start位置开始，结束于end位置的新的String（不包含end)。   
**修改：**     
1、StringBuffer **replace**(int start, int end, String str)：使用给定Str中的字符替换此序列中从start位置开始end位置结束中的字符。           
2、void	**setCharAt**(int index, char ch)：将给定索引index处的字符改为ch。    
**反转：**    
1、StringBuffer **reverse**()：将此字符序列用其反转形式取代。       
**另外：**   
void **getChars**(int srcBegin, int srcEnd, char[] dst, int dstBegin)：将字符从此序列复制到目标字符数组dst。   

## 基本数据类型对象包装类    
最常见作用：用于基本数据类型与字符串类型之间的转换。      
基本数据类型转成字符串：基本数据类型。toString(基本数据类型值);         
字符串转成基本数据类型：xxx a = Xxx.parseXxx(String);      
十进制转成其他进制：     
toBinaryString();     
toHexString();     
toOctalString();     
其他进制转换成十进制：   
parseInt(string,redix);