# Linux基础要点总结

## 基础命令总结

### 简单（选项少，容易记忆，或者较少使用的命令）

``` bash
cd
ls [-lah]
rm [-rf]
mkdir [-p]
rmdir [-p]
mv
head
tail
cat
tac
more
less
nl
echo
which
whereis

```

### 较为熟悉的命令

``` bash
chown
chgrp
chmod
```

### 选项较多、常用需要记忆的命令

```bash
find
locate
grep
awk
sed
wc
ps
```


### 较少使用，但是需要知道的命令

```bash
chattr
lsattr
pstree
du
df
fdisk
mount
alias
unalias
```

### 语法查漏补缺

```bash
#数组
数组的定义有两种方式：
整体赋值
x=("China" "America" "England" "France" "Japan" "Korea" "Austrilia" "Russia")
单独赋值
x[0]="China"
x[1]="America"
x[3]="England"
x[4]="France"
输出数组中的所有内容
echo ${x[*]}    #强调整体
echo ${x[@]}    #强调个体
输出数组的长度
echo ${#x[*]}
echo ${#x[@]}
输出某个索引所索引的值
echo ${x[1]}

$0 表示指令本身，$1表示参数1，$2表示参数2，以此类推，$@、$*表示所有参数，$#表示参数个数，$?表示上一个命令的输出，$$表示pid

$0  代表脚本本身
$1  代表传入脚本的第一个参数
$2  代表传入脚本的第二个参数
...
$n  代表传入脚本的第n个参数

$#  代表参数的个数
$@  代表"$1" "$2" ... "$n"
$*  代表$1<u>c</u>$2<u>c</u>$...<u>c</u>$n，<u>c</u>为分隔符，默认为空格,因此通常与$@同义




#重定向
0标准输入
1标准输出
2标准错误输出
使用>、>>进行输出重定向，单符号表示直接覆盖文件，双符号表示添加，对于标准输出无影响，使用<、<<进行输入重定向，单符号表示文件输入，双符号表示键盘输入，后面接结束标志（自定义）
echo hello,world > file.txt #覆盖原本文件中的内容
echo hello,world >> file.txt #在文件中的内容之后加入新的内容
grep < file.txt #将文件中的内容作为输入
cat << "END" #使用END作为结束符号结束输入，并且将输入输出到屏幕上(cat实现的操作，如果换成其他命令有相应的其他操作)
1>&2 绑定重定向，将1（标准输入）的内容也重定向到2（标准错误）中，为何不直接重定向呢？因为两者同时写入会造成错误，这里应该是做了一些处理，可以两者同时（交替）写入


#管道
使用|把上一个指令的操作结果从标准输入中传递给下一个指令，若中间有指令不执行，则不产生输出，会跳过该指令进行传递，&?即表示上一个指令的输出。&&、||分别表示上一个指令执行成功、失败时继续执行下一个指令，否则不执行，“;”表示不管如何继续执行。

#变量的使用
declare/typeset 无跟随与set功能相同
declare/typeset -[aixr] variable
-a 表示数组
-i 表示整型
-x 表示环境变量
-r 表示只读变量
bash变量默认为字符串，所以不会进行计算，并且只能进行整型计算，若有小数则直接缺省

#括号的使用
小括号()
1、括号中的命令新开一个子shell顺序执行，可以有多个命令，命令之间使用分号进行分隔，最后一个命令可以没有分号，其中的变量是不可以被脚本的其他部分使用的。
(ps | grep a&&echo ok)
2、命令替换，相当于`cmd`，shell会将cmd执行并且将cmd替换为执行结果
`expr 1 + 2` 相当于 $(expr 1 + 2)   #请注意表达式之间必须有空格，命令替换和新开shell是不一样的，新开shell不需要加$符号，且可以多个命令
3、初始化数组
x=(china japan korea thiland vietnam)

双小括号(())
1、整数拓展，支持内部的整数算术表达式((expr))，如果表达式结果为0，返回值为1，表示假，返回值为非零值则表示真。如果是进行逻辑判断，则1为真，0为假。
echo $((2+2))   #无需空格
echo $((2>1))   #条件判断
2、符合C语言的运算规则都可以用在$(())中，输出结果自动转换为10进制
echo $((1>2?1:3)) #使用C语言中的运算符
3、实现变量重定义，如((a++))，没有什么特殊的
4、用于算术比较，双括号支持多个表达式用逗号分开，如if(($i<5))、for((i=0;i<$n;i++))，不需要$符号
if((2>1))
then
{
    echo ok
}
fi

中括号[]
1、[]和test命令是相同的
2、==、!=用于字符串比较，比较大小使用-gt、-lt、-eq、-nq等
if [ China == Korea ]
then
    echo Yes
else
    echo No
fi

if [ 1 -lt 2]
then 
    echo ok
fi

3、正则表达式中会使用
4、数组索引使用
arr=(America China Russia Japan)
echo ${arr[1]} #China

双中括号[[]]
1、[[]]
2、支持正则表达式模式匹配
3、使用[[]]做条件判断可以直接使用逻辑运算符号
if [[ 2>1 ]]
then
    echo ok
fi

4、看作一个整体，返回一个退出码


花括号{}
1、代码块，事实上构建了一个匿名函数，但是不会开一个子shell进行运行，其他部分可以使用其中的变量，最后的命令必须要有分号，左侧必须要有空格。
{ echo ok; ...} #容易理解，不做举例
2、用于使用变量时进行语法分割
arr=(America China Russia Japan)
echo ${arr[1]} #China，使用{}包含数组索引变量
3、拓展用法


#选择条件
case $var in
    "var1")
    ...
    ;;  #以双分号结尾一个段落，不需要像其他语言一样使用break跳出
    "var2")
    ...
    ;;
    *)  #相当于default，兜底条件
    ...
    ;;
esac

select $var in ${x[*]}#不一定要使用数组，也可以使用用空格分隔多个数据
do
    break
done
echo $var   #输出所选中的内容

#两种for循环
for i in ${x[*]}
do
    echo $i
done

for ((i=0;i<${#x[*]};i++))  #for与括号之间的空格可加可不加
do
    echo ${x[$i]}"2"        #与上个for循环做区分
done

fcuntion func () #定义函数时可以不加function字段
{
    echo "this is a func"
}
func  #直接调用，不需要使用括号，需要传参时，与命令行下使用命令一样即可
```