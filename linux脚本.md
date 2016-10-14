
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

 	find . | xargs  grep -i   myproc