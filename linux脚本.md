## 递归下载文件

wget -r -l 3 -p -np -k  xxx.com/xxx

不可以写 http
wget加上参数之后，即可成为相当强大的下载工具。
wget命令详解
wget -r -l 3 -p -np -k http://xxx.com/xxx
-r, --recursive（递归） specify recursive download.（指定递归下载）
-k, --convert-links（转换链接） 
make links in downloaded HTML point to local files.
（将下载的HTML页面中的链接转换为相对链接即本地链接）
-p, --page-requisites（页面必需元素） get all images,
 etc. needed to display HTML page.（下载所有的图片等页面显示所需的内容）
-np, --no-parent（不追溯至父级） don't ascend to 
the parent directory.
-l  递归下载的层数 否则会把整个网络下载下来

## linux 远程执行脚本
```
#!/bin/bash
for node in `cat nodelist`
do
echo "--------"$node"--------"
#ssh $node "date" > /dev/null 2>&1 
ssh $node "date;ls"  
echo done!
done
```
or
```
#!/bin/bash
for node in `cat nodelist`
do
echo $node
ssh $node  > /dev/null 2>&1 << eeooff
cd /home/asc16
hostname >>/home/asc16/zjhua/log
date >>/home/asc16/zjhua/log
exit
eeooff
echo done!
done
```




 nodelist include node name
 like:
 cu01
 cu02



# fortran 代码对齐

-大小写互换

sed -i 's/[A-Z]/\l&/g' *.f90

```
for name in `cat a.txt`;
do
echo "$name.o:  $name.f90"
printf  "\t\${FC}  -shared-intel -autodouble \${FLAG} -c  $name.f90"
printf "\n"
done
```

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
            
                        if [ $num.txt = $name ] ; then     
                        flag="t1"
                        fi    
                done
                if [ $flag = "f1" ] ; then     
                   cat $name >>  log.time
                   rm  $name
                fi  
        done
        sleep 300
done
```

 