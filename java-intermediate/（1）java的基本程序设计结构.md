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

二、输入输出





三、数组



