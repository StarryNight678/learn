# java学习

- 栈stack

```
public class Test2 {

	private Stack<Integer> stackData;
	private Stack<Integer> stackMin;

	public Test2() {
		this.stackData = new Stack<Integer>();
		this.stackMin = new Stack<Integer>();
	}
}

peek
public E peek()
查看堆栈顶部的对象，但不从堆栈中移除它。

pop

public E pop()
移除堆栈顶部的对象，并作为此函数的值返回该对象。

```



## java 写文件

```
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

    String fileName = "/home/jason/code/01_test/jz_1/wordCountBolt.txt";
    try {
        BufferedWriter out=new BufferedWriter(new FileWriter(fileName));
        // 打开一个写文件器，构造函数中的第二个参数true表示以追加形式写文件      
        //     FileWriter writer = new FileWriter(fileName, true);
        out.write(str);
        out.close();
    } catch (IOException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
    }
```














```

```