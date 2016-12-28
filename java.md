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
import org.apache.storm.scheduler.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.List;
import java.util.Map;

public void writeFile(String str) {
    String fileName = "/home/jason/stormScheduleLog.txt";
    try {
        BufferedWriter out=new BufferedWriter(new FileWriter(fileName));
        out.write(str);
        out.close();
    } catch (IOException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
    }
}

```












```

```