# Linux基础-ShellScript

## Bash的基础指令

```txt
set
export
locale
read -p [提示语] -t [second] [变量]
declare/typeset 无跟随与set功能相同
declare/typeset -[aixr] variable
-a 表示数组
-i 表示整型
-x 表示环境变量
-r 表示只读变量
bash变量默认为字符串，所以不会进行计算，并且只能进行整型计算，若有小数则直接缺省
对于数组，需要对每一个索引位置进行赋值

ulimit 用于限制某个账号对于主机的资源占用
ulimit [-SHacdfltu] [配额]
```

```txt
${变量#关键字} 从前往后匹配最短的那一个删除
${变量##关键字} 从前往后匹配最长的那一个删除

${变量%关键字}  从后往前匹配最短的那一个删除
${变量%%关键字} 从后往前匹配最长的那一个删除

${变量/旧关键字/新}  从前往后匹配第一个进行替换
${变量//旧关键字/新} 从前往后匹配所有进行替换
```

```txt
username=${username-root}
若username存在则将username的值赋值给他，否则username的值为root，若username为空字符串，可以使用下面命令
username=$z{username:-root}
除此之外还有+、=、？有类似的操作，请查表

alias，unalias 设置和取消设置别名
alias lm='ls -al'
```


``` txt
history 
-c
-a
-w
-r
-n
!10 往前数第10个命令
!! 前一个命令
!al 执行最近的以al开头的命令
历史指令文件为~/bash_history
```

## Bash的基本构成及配置

### 路径搜索顺序

```txt
1. 以相对路径、绝对路径执行的指令，如/bin/ls
2. 由alias来寻找的指令
3. 由bash内置的指令来执行, 如ls、cd
4. 通过$PATH这个变量的顺寻搜寻到的第一个指令来执行的
```

### 开始界面展示

```txt
/etc/issue      /打开bash时的开始
/etc/motd      /仅root可以修改，motd会有通知信息，如何时维护
```
### 环境配置

```txt
login shell 例如tty工作台下的shell
nonlogin shell 例如图形界面下的shell
这两个bash启动时读取的配置文件不相同
login shell读取两个配置文件
/etc/profile：系统整体配置文件
~/.bash_profile或~/.bash_login或/.profile：这个属于个人设置
nonlogin还读取一个~/bashrc文件
```

```txt
重定向
0标准输入
1标准输出
2标准错误输出
使用>、>>进行输出重定向，单符号表示直接覆盖文件，双符号表示添加，对于标准输出无影响
使用<、<<进行输入重定向，单符号表示文件输入，双符号表示键盘输入，后面接结束标志（自定义）

管道
使用|把上一个指令的操作结果从标准输入中传递给下一个指令，若中间有指令不执行，则不产生输出，会跳过该指令进行传递，&?即表示上一个指令的输出，
&&、||分别表示上一个指令执行成功、失败时继续执行下一个指令，否则不执行，;表示不管如何继续执行。
```

cut 

grep 匹配文件中的一段字符，并且将所在行显示在屏幕上