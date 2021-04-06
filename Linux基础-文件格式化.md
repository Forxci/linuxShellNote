# Linux基础-文件格式化

## 格式化输出函数printf

```txt
printf '%s\t%s\t%s\t%s\t\n' $(cat wei.txt)
和C语言相似，可以控制字符长度，如%+10s，将使用符号分割的字符作为单独的字符串（空格或者tab分割开）

```

## 数据处理awk命令

```txt
awk自带的变量，在awk内不需要添加$符号

NF  每一行拥有的字段总数，$0也表示这个意思（number ）
NR  目前awk处理的是第几行（number row）
FS  处理字段时的分隔符，默认为空字符（file split）

awk的格式   awk '条件1{操作1} 条件2{操作2}'
例：last -n 5 | awk 'NR==2  {printf $1"\t"} NR!=2 {printf "\t"} {printf $7"\n"}'

条件也可以写成if形式if (NR==2)，以;号分割指令
```

## 文件对比命令

### 用于行比对的diff命令

> diff [-bBi] \<sourcefile> \<newfile>

1. -b表示忽略同行之间多个连续的空白之间的差异
2. -B忽略空白行差异
3. -i忽略大小写差异


### 用于二进制比对的cmp命令

```txt
默认输出第一个不同点，使用-l来输出所有的不同之处
```

### 用于更新旧版本的patch命令

使用diff命令可以制作patch文件用于更新旧文件
> diff -Naur passwd.old passwd.new > passwd.patch

> patch -pN < passwd.patch  //N放在p后面表示可以取消几层目录的意思

> patch -R -pN < passwd.patch // 还原文件



sed命令暂时未研究