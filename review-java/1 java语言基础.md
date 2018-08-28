# 一、数据类型

## 基本数据类型：

字符型char、布尔类型boolean以及数值类型byte、short、int、long、float、double;

（数值类型分为整数类型byte、short、int、long和浮点数类型float、double；）

（1）整型 int(基本型）、short（短整型）、long（长整型）、byte（字节型）

（2）浮点型 float（单精度）、double（双精度）

（3）字符型 char
（4）布尔型 boolean

## 常量

常量在定义时被赋值，以后它的值再也不能被改变
eg final int MALE=1; 习惯上符号常量名用大写，普通变量名用小写；

## 变量

eg int student；
变量使用匈牙利命名法——如果只有一个单词，整个单词小写；如果有两个以上的单词，则第一个单词小写，其余各单词的首字母大写；

## 整型数据

### 整型常量

（1）十进制整数；

（2）八进制整数——规定以0开头的都是八进制数

（3）十六进制整数——规定以0X或0x开头的都是十六进制数

当整型常数后面跟有L或l时，表示该数是长整型常量，如4987L和0X4987L（加上后缀，强迫计算机用八个字节存放）;

### 整型变量——先定义后赋值

byte byteVariable;byteVariable=128;定义一个字节型变量，为它赋值127；

short shortVariable;shortVariable=0100;定义一个短整型变量，为它赋一个八进制的值；

int baseVariable;baseVariable=0x1234;定义一个基本型变量，为它赋一个十六进制的值；

long longVariable;longVariable=-123456789987654L;定义一个长整型变量，为它赋一个长整型的值；

### 浮点型数据

（1）浮点型常量
两种形式：
一、由数字和小数字组成 eg0.123；
二、指数形式，比如1.5E5表示1.5*105（字母E或e之前必须有数字，且E后面的指数必须为整数）

java规定浮点型常量默认为双精度，如果需要指定单精度数，需要在末尾加上F或f,比如12.5F或12E5f;

(2) 浮点型变量 float和double

### 字符型数据

（1）字符常量 用单引号括起来的一个字符，如‘a’、‘D’、‘$’
（2）字符变量 
short shTemp;shTemp=0x41;定义一个short型变量，将short型变量赋一个整型的数值；

char ch;ch=(char)shTemp;定义一个char型变量，将short型变量转换为char型；

eg char ch='A';ch=(char)(ch+32);32是小写字母a与大写字母A的Unicode码的差值；

### 布尔型数据——布尔型数据有两个值true和false

eg boolean bool;bool=(1<2);定义一个boolean型变量，1<2是一个关系表达式，它会计算出一个布尔值；

### 变量赋初值

int i;i=100;等价于int i=100;

### 数据类型转换——范围小的转换为范围大的；精度小的转换为精度大的；

（1）扩展转换——可以由系统自动进行
byte、short、int、long、float、double从左往右转换
char 、int、long、float、double从左往右转换
（2）缩减转换——会损失精度，必须使用强制类型转换（除非有十足的把握，不要进行缩减转换）


# 二、运算符与表达式

（1）取余运算
5%3=2;
5%-3=2；
-5%3=-2；
-5%-3=-2；
（2）自加、自减运算
a=1;
b=++a;先加一，再赋值；
b=--a;先减一，再赋值；
b=a++;先赋值，再加一；
b=a--;先赋值，再减一；
c=10;
b=++a*c;先加一再乘，然后赋值；
b=--a*c;先减一再乘，然后赋值；
b=(a++)*c; //先加一，原值做乘法，然后赋值；
b=(a--)*c;//先减一，原值做乘法，然后赋值；
//++与--运算符的结合规则是从右往左；
（3）相等与不相等运算符
5==3；//两侧的值不相等返回false;
5！=3；//如果！=两侧的值相等，则返回true;
（4）逻辑运算符和逻辑表达式
&&与、||或、！非
（5）条件运算符和条件表达式
三目条件运算符表达式：（x%2==1）?1:0 当x为奇数时，表达式的值为1；当为偶数时，值为0；
（6）位运算符与位表达式
&——参与运算的两数各对应的二进制位作“与”运算；
|——参与运算的两数各对应的二进位作“或”运算
^——参与运算的两数各对应的二进制位作“异或”运算
~——取反运算符‘~’为单目运算符，具有右结合型；取反运算符的功能是对参与运算的数的各二进位按位取反；
<<——左移运算符，功能是将运算符“<<”左边的操作数的各二进位全部左移指定的位数；
>>——右移运算符，功能是晶运算符"<<"右边的操作数的各二进位全部右移指定的位数
>>>——不带符号的右移运算符，运算符左边的操作数的各二进位全部右移指定的位数；
（7）赋值运算符和赋值表达式
x=y+10;
赋值表达式的求解过程是：先计算赋值运算右操作数的值，然后将右操作数的值存放到左操作数指定的存储位置；
（8）表达式的求值顺序
...java
x+=6.0;等效于x=x+6.0;
z*=x+y;等效于z=z*(x+y);
a+=a-=b+5;等效于a=a+(a=a-(b+5));
...
# 三、流程控制语句

三种基本控制结构：顺序结构、选择结构、循环结构；
（1）if~else分支语句
...java
if(exp)   #exp可以是任意合法的关系表达式、逻辑表达式或者boolean值
    statement;
...
（2）if~else
...java
if(exp)
    stat1;
else
    stat2;
...
(3)if~else if~else语句
...java
if（exp）
    stat1;
else if
    stat2;
else if
    stat3;
.....
else
    stat n;
...
(4)if语句的嵌套
...java
if(exp1)
    if(exp2)
    else
else
    if(exp3)
    else
这种形式加花括号更安全
if(exp1)
{
    if(exp2)
}else
    if(exp3)
    else
...
(5)多路分支switch~case语句
...java
switch(exp){
    case exp1:
             语句1；
             break;
    case exp2:
             语句2；
             break;
    .......
    case expn:
             语句n；
             break；
   default:
           语句n+1;
           break;
   ...
(6)当型循环while语句
...java
while(exp)
    stat;
...
(7)直到型循环do~while语句
...java
do
   stat
while(exp);
或者
do{
    stat
}while(exp);
...
(8)当型循环for语句
...java
for(exp1;exp2;exp3)
    stat
或者
while(exp2){
    stat
    exp3;
}
...
(9)for的各种形式
...java
for(;cnt<=100;cnt++) sum+=cnt;
for(cnt=1;;cnt++) sum+=cnt;
for(cnt=1;cnt<=100;){
    sum+=cnt;
    cnt++；
}
for(;cnt<=100;){
    sum+=cnt;
    cnt++;
}
for(;;)语句（三个表达式都省略，无终止的执行循环体）
for(sum=0;cnt<=100;cnt++) sum+=cnt;
for(sum=0,cnt=1;cnt<=100;cnt++) sum+sum+cnt;
for(i=0,j=100;i<=j;i++,j--) k=i+j;
...
（10）增强的for循环
...java
eg  Random rand = new Random(15);//定义一个产生随机数的Random对象
float f[] = new float[10]; //定义一个大小为10的float数组空间
for(int i=0;i<10;i++)
    f[i] = rand.nextFloat();//使用普通的for循环，为数组赋随机值；
for(float x:f)
    System.out.println(x);//使用增强的for循环实现数组遍历；
...
标准语法格式
...java
for(ElementType element:arrayName){
    stat;
};//注意此处加了;号；
...
（11）循环的嵌套
...java
while(exp1){
    ....
    while(exp2){
        ....
    }
}
do{
    for(exp1;exp2;exp3){
         ....
    }
}while(exp);
for(exp1;exp2;exp3){
    ....
    for(exp4;exp5;exp6){
        ....
    }
}
...
(12)跳转语句break
break;
在switch结构中，break语句使控制跳转到该switch结构之后；在循环结构中，break语句使控制跳出包含它当前的循环层，并从循环之后的第一条语句继续执行；
break语句不能用于循环体和switch语句之外的任何地方；
...java
eg outer:  //加上标记outer
        while(true)
            for(int i=0;i<=10;i++){
                System.out.println(i+"");
                if(i>4)
                    break outer;
             }
  ...
 外层的while是一个无限的循环。由于被outer所标记，所以当执行到内层循环的break outer时，仍然可以跳出该循环；
（13）跳转语句continue

continue语句的功能是使当前执行的循环体中止，即跳过continue语句后面尚未执行的该循环中的所有语句，但不结束整个循环，而是继续下一轮循环；
...java
eg for(int num=100;num<=200;num++){
       if(num%3==0)
           continue;
       System.out.println(num+"");
    }
...
