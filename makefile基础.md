# MakeFile基础

## 基本格式

``` txt
Target(目标文件): Prerequisites(依赖文件)

command(操作格式)

...

\<end>

举例：
main : main.o aaa.o
    gcc -o main.o aaa.o \
        -o main


main.o: main.c main.h
    gcc -c main.c -o main.o

aaa.o: aaa.c aaa.h
    gcc -c aaa.c -o aaa.o

```

写在最前面的目标文件是默认最终要得到的文件，操作必须以一个tab开头

使用变量:

``` txt
obj = main.o aaa.o

main : main.o aaa.o
    gcc -o ${obj}(大小括号均可) -o main
```

清除中间文件的方法:

``` txt
1、简便
clean: 
    rm edit ${obj}

2、稳健
.PHONY:clean
clean:
    -rm edit ${obj}
```

二者择一，使用#进行注释，文件名推荐使用Makefile

make

make clean