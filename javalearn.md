
# Java 学习

<<疯狂Java讲义第3版 >>
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
**public static void 修饰符中,public 和static 修饰符位置可以互换,其余部分固定***

对于有包的问题编译运行


```
package a.c
public class Test{PP
	
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


```java
    public void info(String... str) {
        for (String s : str) {
            System.out.println(s);
        }
    }
```

- 方法重载

函数名相同.参数个数或者参数类型不同.

系统会为成员变量初始化.  局部变量必须初始化后才可以使用.


 ##5.4 隐藏和封装


  访问控制符 private default protected  private

  default 包访问权限.protected 可以 被包内类访问.**也可以被子类访问.**
 java 默认导入 java.lang 下的类


import static 导入.可以连类名都不写.



final 与 abstract 只能出现一次.
可以与static 组合起来修饰方法.



静态方法属于类. 不能直接访问非静态成员.

子类可以转换成父类.
父类不可转换成子类.

下面本来就是子类.可以转换.
```
Father father = new Son();
在这里Son 对象实例被向上转型为father了，但是请注意这个Son对象实例在内存中的本质还是Son类型的，只不过它的能力临时被消弱了而已，如果我们想变强怎么办？将其对象类型还原！
Son son = (Son)father;
```

## 继承extends

未指明则继承java.lang.Object

- 方法重写: 子类包含和父类同名方法.成为方法覆盖.
- **如果父类的方法是私有的,子类同名方法不是重写.而是新方法**

原则: 
两同: 参数名,形参列表.
两小: 返回值,抛出异常应该小或相等.
一大: 访问权限比父类大或相等.

- super关键

super调用父类的方法.

```java
   void fun(){
       super.fun();
       System.out.println("this is son.");
   }
```
java创建子类时,不仅为类中定义的实例变量分配内存,也为父类继承的所有实例变量分配内存.子类和父类相同的变量,只是隐藏.都会分配内存.


- 调用父类构造器的时机.

1. 子类使用super显示调用对应实参的构造器.
2. 子类使用this,使用本类中另一个构造器.执行另一个构造器前调用父类构造器.
3. 没有super,也没this调用,使用父类的无参数构造器.

父类构造器总会在子类构造器前执行.




 ## 多态

Java变量有两种类型,编译类型和运行类型.
编译类型和运行类型不同,就是多态.


```
 Base a = new sub();
```
将子类赋值给父类.运行时是子类,编译是父类.

1. 方法,因为子类覆盖了父类方法,呈现多态性.调度子类的方法.
2. 对象的实例变量,没有多态线性.调度的是父类的实例变量.

引用变量只能调动编译时所具有的方法.

- 引用变量间的强制类型转换.
引用类型的转换,只能在具有继承关系的两个类型间进行.


- instanceof
 判断前面是否是后面的类,或者子类.

- 继承和组合

	- 继承最大的坏处,破坏封装
	- 组合,提供更好的封装性

不希望子类重写的方法,使用final修饰.
希望被子类重写的方法使用protected修饰.
父类构造器,调用被子类重写的方法,最后也将使用子类覆盖的方法.

把类设置为最终类,不能被当成父类.使用final修饰.
使用private修饰所有构造器,保证子类无法使用该类的构造器器.无法继承该类.


何时需要派生新类?

1. 子类需要增加新的属性.
2. 子类需要增加特有的行为方式.

- 组合实现复用


组合:将新类作为新类的成员变量组合进来.实现新类的功能.

组合相比继承没有增加开销.

##5.9 初始化模块

java类中的4 中成员,成员变量 方法  构造器 初始化模块.

**初始化模块,修饰符只能是static**

```
[修饰符]{
//初始化代码
	
}
```
初始化模块在构造器前执行.每次创建对象时都执行.

static 修饰的在类加载后,进行初始化.静态初始化模块.
先执行静态初始化模块,再执行普通初始化模块.

```
Base static  初始化模块
Son static 初始化模块
Base初始化模块
Base creae
Son 初始化模块
son create.
```

静态初始化块和声明静态成员变量所指定的初始化代码.按照先后顺序执行.

##6 面向对象(下)
P163-P238


常量池
保证相同的常量 直接量只有一个.


static 无法修饰构造器.

- 单例类: 只能创建一个对象

- final 方法
不能被重写.

- 抽象方法
有抽象方法的类只能被定义成抽象类,抽象类中可以没有抽象方法.

抽象类无法实例化.
没有完全实现接口的类,只能被定义为抽象类.


static 不能修饰变量.
static和abstract不能同时修饰某个方法,没有所谓的类抽象方法.
static和abstract 可以同时修饰内部类.
private和abstract 不能同时修饰方法.

作用:
模板,避免子类的随意性.


- 更加特殊的抽象类 接口
接口里所有的方法都是抽象方法.

接口只能继承接口,不能继承类.



java8 允许定义默认的方法.

接口不包含构造器和初始化定义,只能是静态常量.

方法:
抽象方法,类方法,默认方法.

默认方法是default修饰,有实现.默认方法不能使用static修饰.


成员变量自动使用 public static final.  必须定义时指定初始值.

普通方法自动使用 public abstract 修饰.



###6.1 java增强包装类



###6.2 处理对象


###6.3 类成员


###6.4 final修饰符
###6.5 抽象类
###6.6 Java8改进的接口

接口支持多继承。
继承是 extends 实现是implement。

- 面向接口编程

通过接口降低耦合
	
	- 简单工厂模式
	- 命令模式
	
	将处理方法和处理行为相互分离。
	


###6.7 内部类

非静态内部类，不能拥有静态成员。


局部内部类和匿名内部类不是类成员。

内部类可以直接使用外部了的成员.
外部类无法直接访问,内部类的实例变量.

- 非静态内部类,不能定义静态方法变量


- 静态内部类

创建内部类对象前,需要创建外部类对象.


- 匿名内部类






###6.8 Lambda表达式

代码块作为方法的参数.

**Lamda表达式的目标类型必须是函数式接口** 

函数时接口:只含有有个抽象方法的接口.可以有其他的方法,类方法.

###6.9 枚举类

枚举类不能派生子类.


###6.10 对象和垃圾回收

可达  可恢复  不可达状态

只有处于不可达状态时,才会进行垃圾回收.

通过两种方式通知,系统进行垃圾回收.

```
    System.gc();
    Runtime.getRuntime().gc();
```

finalize 并不一定会执行.

```
public class T {
    //从可恢复到不可达状态调用 finalize 
    public  void finalize(){
        System.out.println("gc ing");
    }
    public static void main(String[] args) {
        System.out.println("----------");
        for (int i=0;i<4;i++){
            new T();
        }
       System.gc();
      //or Runtime.getRuntime().gc();
    }
}
```


强 软 弱  虚引用.  get()方法.

无法通过虚引用获取引用的对象.

###6.11 修饰符的适用范围

P232


###6.12 Jar文件


##7 java基础类库
P239-P280


正则表达式

^ 开头
$ 行尾
? 出现0次或一次.

日期的格式化器.  忽略.

##8 java集合
P281-P332

###8.1  集合概述

set 无序,不可重复的集合
list 有序 重复集合
queue 
map 映射关系数组

**集合内只能保存对象.**

迭代器发现迭代过程中,集合被修改了.立即失败.

foreach循环时,集合不能被改变.

###8.2  cllection和iterator接口


###8.3  set集合

- set

	- 通过调用hashCode()判断对象是否相等.判断位置,equeue判断是否相等.

	  HastSet:

	- LinkedHashSet 顺序和插入的顺序一致.


- TreeSet

元素处于排序状态.

升序列: 自然排序.

一个类添加到TreeSet必须实现了Comparable接口.(第一个元素添加时不需要实现,取出时依然有问题)

只能添加一种类型的对象.
结果一致.
重写equeue方法时需要和comparaTo




重写 equals() 或hashCode().应使equals()相同,hashCode()也相同.

通过hashSet找到位置. 通过equeue判断是否删除.

- EnumSet

性能分析:

TreeSet 需要通过红黑树来实现排序.

HashSet  TreeSet  EnumSet 都是线程不安全的.


###8.4  list集合

list判断对象相等使用,euquals()方法.

- 排序

```
class Test {
    public static void main(String[] args) {
        List ll = new ArrayList();
        ll.add(1);
        ll.add(2);
        ll.add(8);
        ll.add(6);
        ll.add(3);
        System.out.println(ll);
        ll.sort((o2, o3) -> Integer.parseInt(o3.toString()) - Integer.parseInt(String.valueOf(o2.toString())));
        System.out.println(ll);
    }
}

```

ListIterator 迭代器.


ArrayList 和 Vector 实现类. Vector比较古老,少用.
ArrayList 线程不安全,vector线程安全.vector的性能比ArrayList低.
保证线程安全也不推荐是vector.有Collections工具类.

Stack 继承Vector 古老,性能差.  推荐是ArrayDeque


- 固定长度List
Arrays.ArrayList 固定长度.无法增删元素.



###8.5  Queue集合

- PriorityQueue实现类

元素,按照大小重新排序.

- Deque双端队列.

可以当成stack使用.

addFirst
addLast

- LinkedList 实现类

实现deque 当成双端队列使用. 可以当场栈使用.


###8.6  java 8 增强的map集合

java 首先实现Map,包装一个value都为null的map的集合实现了set.

- HashTable  和 HashMap 区别.

- SortedMap接口实现 TreeMap类.

红黑树,排序.
自然排序,定制排序.

- WeakHashMap

对象的弱引用.便于垃圾回收.


###8.7  hashSet和hashMap性能选项


###8.8  操作集合的工具类: Collections

Collections

返回多线程安全版本

返回不可变集合


###8.9  繁琐的接口: enumeration



##9 范型
P334-P355


###9.1 范型入门

List<String>  sl=new ArrayList<String>

###9.2 深入范型

静态方法或者静态变量的声明和初始化中,不允许使用类型形参.


###9.3 类型通配符

类型通配符<?>

限制通配符  <? extends baseClass >



###9.4 范型方法


范型方法和类型通配符的差别.






###9.5 擦除和转换

###9.6 范型与数组


反射功能


##10 异常处理
P356-P380

-----------------------

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


动态链接库。