<!-- GFM-TOC -->
* [一、字符串](#一字符串)
    * [子串](#子串)
    * [拼接](#拼接)
    * [不可变的字符串](#不可变的字符串)
    * [检测字符串是否相等](#检测字符串是否相等)
    * [空串与Null串](#空串与null串)
    * [码点与代码单元](#码点与代码单元)
    * [构造字符串](#构造字符串)
* [二、输入输出](#二输入输出)
* [三、数组](#三数组)
    * [for each循环](#for&nbsp;each循环)
    * [数组拷贝](#数组拷贝)
    * [数组排序](#数组排序)
    * [多维数组](#多维数组)
    * [不规则数组](#不规则数组)
<!-- GFM-TOC -->
# 一、字符串
在标准java类库中提供了一个预定义类，叫String；每个用双引号括起来的字符串都是String类的一个实例：
```java
String e = "";//一个空的字符串
String greeting = "Hello";
```
## 子串
String类的substring方法可以从一个较大的字符串提取出一个子串。
```java
String greeting="Hello";
String s = greeting.substring(0,3);//创建了一个由字符"Hel"组成的字符串。
```
## 拼接
java语言运行使用+号连接（拼接）连个字符串；
```java
String expletive = "Expletive";
String PG13 = "deleted";
String message = expletive + PG13;
```
当将一个字符串与一个非字符串的值进行拼接时，后者被转换成字符串
```java
int age = 13;
String rating = "PG" + age;//reting设置为“PG13”；
```
这种特性通常用在输出语句中,会打印出希望的结果
```java
System.out.println("The answer is"+anser);
```
如果需要把多个字符串放在一起，用一个定界符分割，可以使用静态的join方法：
```java
String all = String.join("/","S","M","L","XL");//结果为"S/M/L/XL";
```
## 不可变的字符串
String类没有提供用于修改字符串的方法；由于不能修改java字符串中的字符，所以java文档将String类对象称为不可变字符串。
如果希望修改内容，首先需要提取需要的字符，然后再拼接上替换的字符串：
```java
String greeting = "Hello";
greeting = greeting.substring(0,3)+"P!";//当前值修改为"Help!";
```
## 检测字符串是否相等
使用equals方法检测两个字符串是否相等
```java
s.equals(t)//如果字符串s与字符串t相等，则返回true;否则，返回false;
```
注意：s与t可以是字符串变量，也可以是字符串字面量；
```java
eg "Hello".equals(greeting)
```

要想检测两个字符串是否相等，而不区分大小写，可以使用equalsIgnoreCase方法。
```java
"Hello".equalsIgnoreCase("Hello")
```
（一定不要使用==运算符检测两个字符串是否相等！这个运算符只能够确定两个字符串是否放置在同一个位置上；

java中的compareTo方法用==对字符串进行比较：
```java
if(greeting.compareTo("Hello")==0)....
```
## 空串与Null串
空串""是长度为0的字符串；检查一个字符串是否为空：
```java
if(str.length()==0)  //第一种方法
if(str.equals(""))   //第二种方法
```
注意区分：要检查一个字符串是否为null，要使用一下条件：
```java
if(str == null)
```
有时要检查一个字符串既不是null也不为空串，这种情况需要使用以下条件：
```java
if(str!=null&&str.length()!=0)
```
首先要检查str不为null;

## 码点与代码单元
大多数常用的Unicode字符使用一个代码单元就可以表示，而辅助字符需要一对代码单元表示。

## 构造字符串
如果需要用许多小段的字符串构建一个字符串，首先构建一个空的字符串构建器：
```java
StringBuilder builder = new StringBuilder();
builder.append(ch);//每当需要添加一部分内容时，就调用append方法。
builder.append(str);
String completedString = builder.toString();//在需要构建字符串时就调用toString方法，将可以得到一个String对象，其中包含了构建器中的字符序列。
```
JDK5.0中引入StringBuilder类，这个类的前身是StringBuffer（效率较低）;如果所有字符在一个单线程中编辑（通常都是这样），则应该用StringBuilder替代它。

# 二、输入输出





# 三、数组
创建一个数字数组时，所有元素都初始化为0；Boolean数组的元素会初始化为false;对象数组的元素则初始化为一个特殊值null，表示这些元素还未存放任何对象。
一旦创建了数组，就不能改变它的大小（尽管可以改变每一个数组元素）；
如果经常需要运行过程扩展数组的大小，就应该使用另一种数据结构——数组列表（array list）;
## for each循环
这种增强的for循环的语句格式：
```java
for(variable:collection) 
    statement
```
定义一个变量用于暂存集合中的每一个元素，并执行相应的语句；collection这一集合表达式必须是一个数组或者是一个实现了Iterable接口的类对象。
```java
for(init element:a)
    System.out.println(element);//打印数组a的每一个元素，一个元素占一行。
```
这个循环应该读作“循环a中的每一个元素”；
注意：for each循环语句的循环变量将会遍历数组中的每个元素，而不需要使用下标值。
有个更简单的方式打印数组中的所有值，即利用Arrays类的toString方法；调用Arrays.toString(a),返回一个包含数组元素的字符串，这些元素被放置在括号内，并逗号分隔，例如“[2,3,,5,7,11,13]”。要想打印数组，可以调用System.out.println(Arrays.toString(a));


## 数组拷贝
在java中允许将一个数组变量拷贝给另一个数组变量；这时，两个变量将引用同一个数组：
```java
int[] luckyNumbers = smallPrimes;
lunckNumbers[5] = 12;
```
如果希望将一个数组的所有值拷贝到一个新的数组中去，就要使用Arrays类的copyOf方法：
```java
int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers,luckyNumbers.length);//第二个参数是新数组的长度，这个方法常用来增加数组的大小。
luckyNumbers = Arrays.copyOf(lunckyNumbers,2*luckyNumbers.length);         
```
## 数组排序
对数值型数组进行排序，可以使用Arrays类的sort方法：
```java
int[] a = new int[10000];
....
Arrays.sort(a)       //这个方法使用了优化的快速排序算法
```

## 多维数组
如果想要访问二维数组a的所有元素，需要使用两个嵌套的循环：
```java
for(double[] row:a)
    for(doubel value:row)
        do something with value
```
要想快速的打印一个二维数组的数据元素列表，可以调用：
```java
System.out.println(Arrays.deepToString(a));//输出格式[[1,3,3],[1,3,5],[1,3,7]]
```
## 不规则数组
java实际上没有多维数组，只有一维数组；多维数组被解释为“数组的数组”。
