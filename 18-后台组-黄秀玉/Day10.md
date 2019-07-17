### String类    
- 字符串是一个特殊的对象。
- 字符串一旦初始化就不可以被改变。

#### String类的常用方法    
##### 1. 获取    
1.1 **int length()**：返回此字符串的长度。   

1.2 **char charAt(int index)**：返回指定索引处的char值。  

1.3 **int indexof(int ch)**：返回指定字符在此字符串中第一次出现处的索引。    

1.4 **int indexOf(int ch,int fromIndex)**：返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。    

1.5 **int indexOf(String str)**：返回指定子字符串在此字符串中第一次出现处的索引。   

1.6 **int indexOf(String str,int fromIndex)**：返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。  

1.7 **int lastIndexOf(int ch)**：返回指定字符在此字符串中最后一次出现处的索引。

1.8 **int lastIndexOf(int ch,int fromIndex)**：返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索。    

1.9 **int lastIndexOf(String str)**：返回指定子字符串在此字符串中最右边出现处的索引。    

1.10 **int lastIndexOf(string str, int fromIndex)**：返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。

##### 2. 判断   

2.1 **boolean contains(CharSequence s)**：当且仅当此字符串包含指定的char值序列时，返回 true。

2.2 **boolean isEmpty()**：当且仅当length()为0时返回 true。

2.3 **boolean startsWith(String prefix)**：测试此字符串是否以指定的前缀开始。

2.4 **boolean endsWith(String suffix)**：测试此字符串是否以指定的后缀结束。

2.5 **boolean	equals(Object anObject)** ：将此字符串与指定的对象比较。

2.6 **boolean	equalsIgnoreCase(String anotherString)**：将此String与另一个String比较，不考虑大小写。
##### 3. 转换
3.1 将字符数组转换成字符串   
构造函数：   
 3.1.1 **String(char[])**   
 
 3.1.2
 **String(char[],offset,count)**
 
 静态方法：     
 3.1.3 **static String copyValueOf(char[])**   
 
 3.1.4 **static String copyValueOf(char[] date,int offset,int count)**   
 
 3.1.5
 **static String valueOf(char[])**
 
 3.2 **char[] toCharArray()**：将此字符串转换为一个新的字符数组。
 
 3.3 **String(byte[])**    
**String(byte[],offset,count)**
 
 3.4 **byte[] getBytes(String charsetName)**：使用指定的字符集将此 String编码为byte序列，并将结果存储到一个新的byte 数组中。  
 
 3.5 **static String valueOf(char c)**：返回 char 参数的字符串表示形式。
 
4. 替换    
 **String	replace(char oldChar, char newChar)**：返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。
5. 切割    
**String[] split(String regex)**： 根据给定正则表达式的匹配拆分此字符串。

6. 子串  

6.1 **String substring(int beginIndex)**： 返回一个新的字符串，它是此字符串的一个子字符串。

6.2 **String substring(int beginIndex, int endIndex)**：返回一个新字符串，它是此字符串的一个子字符串。

7. **String toLowerCase(Locale locale)**： 使用给定Locale的规则将此String中的所有字符都转换为小写。
8. **String toLowerCase()**：使用默认语言环境的规则将此String中的所有字符都转换为小写。
9. **String trim()**：返回字符串的副本，忽略前导空白和尾部空白。
10. **int compareTo(String anotherString)**：按字典顺序比较两个字符串。
