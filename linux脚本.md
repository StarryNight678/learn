
# fortran 代码对齐

-大小写互换

sed -i 's/[A-Z]/\l&/g' *.f90


- 代码对齐
[findent](https://sourceforge.net/projects/findent/files/)
使用方法
findent < prog.f90 > prog1.f90

```
for code in `ls *.f90 `;
do
echo $code
findent < $code > $code.new
done

rm *.f90

rename 's/\.new//' *.new
```


# ctags

```
ctags -R -f .tags
```

# 查找特定字符
```
 	find . | xargs  grep -i   myproc
```

- 输出特定列
```
	awk '{printf $1 "\n"}'
```
- 死循环
```
	while true
	do
	echo "hi"
	done
```
- 查看每个命令的运行时间
```
	#/bin/bash
	while true
	do
	        for num in `squeue | awk '{printf $1 "\n"}' | tail -n +2 `;
	        do
	                squeue | grep $num  > $num.txt
	        done
	        sleep 1
	done
```
-

- 查看提交时间定期清理的程序 
```
#/bin/bash
while true
do
        for name  in `ls *.txt `;
        do 
        flag="f1"
                for num in `squeue | awk '{printf $1 "\n"}' | tail -n +2 `;
                do
                        if [ $num = $name ] ; then     
                        flag="t1"
                fi
                    
                done
                if [ $flag = "f1" ] ; then     
                   cat $name >>  log.time
                   rm  $name
                fi  
        done
        sleep 1200
done
```

 