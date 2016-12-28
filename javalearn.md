
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
	类 接口  数组类型  null

	**引用类型相当于一个指针**

	字符串不是基本的数据类型，字符串是一个应用类型。字符串是一个类。 
	java 使用16bit的Unicode字符作为编码方式。
	java默认浮点类型是double
	boolean 不能使用0和非0来替换

	直接给个整数,默认类型int.
    `long  c=99999999999999 `是错误.无法将一个超出int范围的值赋给long类型.
    应该为`long  longNum=99999999999999L;`


##4 流程控制和数组
##5 面向对象(上)
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

## 垃圾回收机制(GC)
主要做两件事:
1. 发现无用的对象
1. 回收被无用对象占用的内存空间

建议进行垃圾回收.`System.gc();`

## 常用库使用


## 异常处理

## String操作

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
