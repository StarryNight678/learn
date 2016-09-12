
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
