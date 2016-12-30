
# java

<<疯狂Java讲义  第3版 >>
2016-09

##1 java语言概述和开发环境

- PATH环境设置
添加java javac环境

JAVA_HOME = C:\Program Files\Java\jdk1.8.0_101

Path = %JAVA_HOME%\bin

- ubuntu下更改Java版本
```
update-alternatives --config java
update-alternatives --config javac
```
- CLASSPATH 
作用搜索java类
jdk 1.5以上版本完全不需要设置CLASSPATH
会自动搜索当前路径和lib\dt.jar  lib\tools.jar


-  编译程序

```
javac -d destdir srcdir
```
程序被java执行. 必须包含main方法,方法是public static void 修饰. main方法的形参必须是 `String[] args`.
**public static void 修饰符中,public 和static 修饰符位置可以互换,其余部分固定**

对于有包的问题编译运行

```
package a.c
public class Test{
	
}
```
方法1:
javac example.java 
需要将class文件放到 ./a/c 
java a.c.Test

方法2:
javac -d . example.java  
将会自动创建 a/c 目录.

- 程序打包,运行

	- 打包

	```
	jar
    -c  创建新档案
    -t  列出档案目录
    -x  从档案中提取指定的 (或所有) 文件
    -u  更新现有档案
    -v  在标准输出中生成详细输出
    -f  指定档案文件名
    -m  包含指定清单文件中的清单信息
    -n  创建新档案后执行 Pack200 规范化
    -e  为捆绑到可执行 jar 文件的独立应用程序指定应用程序入口点
    -0  仅存储; 不使用任何 ZIP 压缩
    -P  保留文件名中的前导 '/' (绝对路径) 和 ".." (父目录) 组件
    -M  不创建条目的清单文件
    -i  为指定的 jar 文件生成索引信息
    -C  更改为指定的目录并包含其中的文件(可以理解为首先cd到指定目录)

    打包
    jar -cvf HelloWorld.jar HelloWorld.class   #将HelloWorld.class文件打入jar包
    查看文档内容:
    jason@jason-HP:~/code$ jar tf t.jar 
	META-INF/
	META-INF/MANIFEST.MF
	a/
	a/c/
	a/c/Test.class
	jason@jason-HP:~/code$ 
	```

	- 运行

	```
	生成可以运行的jar包需要 指定应用程序入口点，用-e选项
	jason@jason-HP:~/code$ jar cvfe t.jar a.c.Test ./a
	added manifest
	adding: a/(in = 0) (out= 0)(stored 0%)
	adding: a/c/(in = 0) (out= 0)(stored 0%)
	adding: a/c/Test.class(in = 418) (out= 288)(deflated 31%)
	jason@jason-HP:~/code$ java -jar t.jar 
	hello world!
	jason@jason-HP:~/code$ 
	```

源文件的文件名必须与public类的类名相同，一个java源文件最多定义一个public类。

##2 理解面向对象

成员变量(状态数据)+方法(行为)= 类定义

面向对象的基本特征:

1. 封装：对象细节隐藏起来
1. 继承：继承父类
1. 多态：子类对象可以直接赋给父类变量，**运行时依然是子类行为特征**。

java不支持多继承

类间的三种关系：
关联：  组合  聚合
泛化：



##3 数据类型和运算符

- 注释语句

1. 单行注释 `//`
1. 多行注释 `/*   */`
1. 文档注释 `/**   */`
javadoc 默认处理public 和protected   内容.

javadoc 选项  java源文件|包

- 标识符

一个语句可以跨多行,只要最后已分号结尾就好.字符串和变量名不能跨多行.
开头:字母 下划线 $.**数字不能打头**

**java所有的关键字都是小写.**


- java类型

	- 基本类型8种
	boolean类型和数值类型(整数类型和浮点类型)


	整数类型： byte short char int long 
	浮点类型：float double

	**char 也是一种整数类型，相当于无符号整数类型**

	java 的8种基本类型对应了包装类
	1. boolean Boolean
	1. byte Byte       1字节
	1. short Short     2字节
	1. int Integer     4字节
	1. long Long       8字节
	1. float Float     4字节
	1. double Double   8字节
	1. char Character  2字节

	- 引用类型4种
	类  接口  数组类型  null

	**引用类型相当于一个指针**

	字符串不是基本的数据类型，字符串是一个应用类型。字符串是一个类。 
	java 使用16bit的Unicode字符作为编码方式。
	java默认浮点类型是double
	boolean 不能使用0和非0来替换

	直接给个整数,默认类型int.
    `long  c=99999999999999 `是错误.无法将一个超出int范围的值赋给long类型.
    应该为`long  longNum=99999999999999L;`


原码: 数值转换成二进制.
实际按照补码保存二进制数.
**正数的补码和原码完全相同,负数的补码是反码+1**

 1. 二进制  0B10
 1. 八进制  010
 1. 十进制   10
 1. 十六进制 0X10

java使用unicode 进行编码,使用两个字节.16位.


- 强制类型转换
(type)value

经常出问题的地方,3.2为double类型.
float a=3.2;

- 字符串转成int类型
	String c="45";
	int nc=Integer.parseInt(c);

每个对应的包装类提供相应方法parseXxx(String c).转换成基本类型.

- 类型自动提升
System.out.println("hello"+'a'+7);  //输出 helloa7
System.out.println('a'+7+"hello");  //输出 104hello

- 常量池
java使用常量池来缓存字符串直接量.后面再使用,直接使用常量池中的字符串直接量.
常量池,指在编译期间被确定.并被保存在.class文件中.包括类 方法 接口中的常量和字符串常量.

- 运算符

`++自加运算`

       int a=5;
       int b=a++ + 6;

输出 a=6  b=11   

 	   int a=5;
       int b=++a + 6;

输出 a=6  b=12 


	- 位运算符

	<<   左移.左边补0
	>>   有符号右移,移出的操作数使用符号位补充.
	>>>  无符号右移.
	注意: 

	1. 低于int类型的类型.操作数自动转换为int再移位.
	1. 一个数过多,自动取余.
	1. 并不会改变操作数本身,只是得到新的结果.

	- 3目运算符
	(if操作)  ? if-true: if-false;


##4 流程控制和数组

- 选择
if,switch

```
if (){

}else if (){
	
}else{
	
}
```

switch语句.
注意:
switch后面的表达式,只能是 byte,short,char,int 四种整数类型. String(java 7)
或者是枚举类型.
```
switch()
{
	case a:
	{

		xx;
		break;
	}
	default:
	{

	}
}
```

- 枚举类型
```
public class Test {
    public enum rainbowColor {RED, ORANGE, YELLOW, GREEN, CYAN, BLUE, PURPLE}
    public static void main(String[] args) {
        rainbowColor c = rainbowColor.BLUE;
        System.out.println(c.toString());
        //遍历操作
        EnumSet<rainbowColor> EnumSetJz = EnumSet.range(rainbowColor.RED, rainbowColor.PURPLE);
        for (rainbowColor t : EnumSetJz) {
            System.out.println(t.toString());
        }
    }
}
```


- 循环
while ,do while ,for 三种
foreach 新的循环.

foreach 循环.循环变量只是临时变量.

- while

初始化语句.
while(循环条件){
语句.
迭代语句.
}


初始化语句.
do{
语句.
迭代语句.
}while(循环条件)

- 数组类型

数组是一种数据类型. int[]

定义数组不能指定数组长度.

- 静态初始化
int[] arr=new int[]{1,2,3};

简单方式:
int[] arr={1,2,3};

- 动态初始化

intp[] arr=new int[6];

分配初值. 默认  false,0,0.0;

- 深入数组

局部变量放到栈内存中.数组放到堆(heap)内存中.
每个方法都建立自己的内存栈,局部变量保存在栈中.程序创建对象,开销大,放到数据区(堆)便于反复使用.堆内存用来存放所有new 创建的对象和 数组的数据.

[堆和栈的解释](https://my.oschina.net/megan/blog/135280)


没有多维数组.


Arrays



##5 面向对象(上)

- 注意
static 修饰的成员不能访问没有static修饰的成员.
- private protected public

- 构造器
没有返回值. 返回值也不是void类型.没有return.

- this引用
构造器中引用正在初始化的对象.
方法中引用调用该方法的对象.
谁调用这个this,就代表谁.

static 修饰的方法中,不能使用this引用.

返回类型是对象.
```
public class Test {

    public int n;

    public Test grow() {
        n = 1;
        return this;
    }
}
```

- 参数传递
java中参数传递机制.使用值传递.副本传递.

- 形参个数可变方法

可变的形参只能位于形参列表的最后.

参数变化例子.

```
    public void info(String... str) {
        for (String s : str) {
            System.out.println(s);
        }
    }
```
- 方法重载

P121

- super关键字

- 继承和多态

- 继承和组合



final 与 abstract 只能出现一次.
可以与static 组合起来修饰方法.


静态方法属于类. 不能直接访问非静态成员.


##6 面向对象(下)
##7 java基础类库
##8 java集合
##9 范型
##10 异常处理
##11 AWT编程
##12 Swing编程
##13 MySQL数据库与JDBC
##14 Annotation(注释)
##15 输入/输出
##16 多线程
##17 网络编程
##18 类加载机制与反射

##19 垃圾回收机制(GC)
主要做两件事:
1. 发现无用的对象
1. 回收被无用对象占用的内存空间

建议进行垃圾回收.`System.gc();`

##20 常用库使用


##21 异常处理

##22 String操作

**字符串是常量,创建后不能改变**
两种创建
```
        String str = "abc";
        char data[] = {'a', 'b', 'c'};
        String s2 = new String(data);
        System.out.println(str);
        System.out.println(s2);
```

java split使用

```
 String[]	split(String regex) 
          根据给定正则表达式的匹配拆分此字符串。
 String[]	split(String regex, int limit) 
          根据匹配给定的正则表达式来拆分此字符串。
根据空格划分字符串
       String str1 = "a b csad fjasj";
        String str3[] = str1.split(" ");
         for (int i=0;i<str3.length;i++) {
            System.out.println(str3[i]);
        }

```


##23 其他
1	基本说明

依赖：






2.1	类型转换
8个包装类提供parseXXX将字符串转变成相应基本类型.
parseInt(String s)

不可变类


>> 右移   空出来的用符号位补充
>>> 无符号右移	空出来的用0补充


3	流程控制与数组
int[] 也是一种数据类型

int[]=new int[5];
默认初始化
boolean  初始化为false

foreache循环,不需要数组长度和数组索引
		int[] arr = { 1, 2, 3 };
		for (int c : arr)
			System.out.println(c);
不能改变数组的值不能赋值.


数组被存储在堆中

栈内存:局部变量
堆内存:对象创建,创建难度较高,




# java
2016-09
1	基本说明
源文件的文件名必须与public类的类名相同，一个java源文件最多定义一个public类。

封装：对象细节隐藏起来
继承：继承父类
多态：子类对象可以直接赋给父类变量，运行时依然是子类行为特征。
java不支持多继承

类间的三种关系：
关联：  组合  聚合
泛化：
依赖：

java所有的关键字都是小写的
2	java类型
1)	基本类型
boolean类型
数值类型:整数类型和浮点类型
整数类型： byte short int long char
浮点类型：float double
char 也是一种整数类型，相当于无符号整数类型
2)	引用类型
类 接口  数组 nul
字符串不是基本的数据类型，字符串是一个应用类型。字符串是一个类。 
java 使用16bit的Unicode字符作为编码方式。
java默认浮点类型是double
boolean 不能使用0和非0来替换


java 的8种基本类型对应了包装类
1)	boolean Boolean
2)	byte Byte
3)	short Short
4)	int Integer
5)	long Long
6)	float Float
7)	double Double
8)	char Character

2.1	类型转换
8个包装类提供parseXXX将字符串转变成相应基本类型.
parseInt(String s)

不可变类


>> 右移   空出来的用符号位补充
>>> 无符号右移	空出来的用0补充


3	流程控制与数组
int[] 也是一种数据类型

int[]=new int[5];
默认初始化
boolean  初始化为false

foreache循环,不需要数组长度和数组索引
		int[] arr = { 1, 2, 3 };
		for (int c : arr)
			System.out.println(c);
不能改变数组的值不能赋值.


数组被存储在堆中

栈内存:局部变量
堆内存:对象创建,创建难度较高,





final和finally 区别?
native
