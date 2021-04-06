# Linux基础-文件

## Linux文件基础概念

### 文件所有人

``` txt
    所有的文件都有一个所有人，所有群组，一般而言，创建者是这个文件的所有人，他所属的群组为文件的所有组。可以通过命令来修改所有人和所有组：
```

> chown \<filename> \<newowner>

> chgrp \<filename> \<newgroup>

### 文件权限

``` txt
    所有的文件都读写执行三个权限，对于每个对象可以设置为不同，文件所有人（user）、文件所有组（group）、其他人（others）可以设置不同的权限，对于文件夹，这三个权限分别表示查看文件列表、新建或删除文件、进入文件夹，使用命令可以修改权限：
```

> chmod 111 111 111 \<filename>

> chmod u+r+w+x g-w+r+x o-r-w-x \<filename>

### 文件树的构成逻辑

``` txt
    定义了标准FHS，根据这个进行文件树的构建，需要了解每一个文件是用来干什么的，简而言之，/usr是软件安装目录，/var是软件运行目录，相当于Windows的安装文件夹和文件存放文件夹
```

> dirname

> basename


## 文件管理相关命令

### 文件夹

``` bash
touch
rm
cat
echo
more
less
head
tail
od
grep

chattr
lsattr
umask
```

### 文件

``` bash
mkdir
rmdir
ls
cd
ll
find
locate
(updatedb)
whereis
which
```

## Linux文件压缩及打包

``` txt
    Linux的压缩直接将源文件压缩了，因此压缩一个文件之后源文件就不存在了。通常使用tar对多个文件进行打包
```

### 压缩指令

> gzip \[-cdtv]  -[1-9] \<filename>

``` txt
 // c 表示输出文件内容到屏幕
 // d 表示解压缩
 // t 表示用来检验压缩文件的一致性
 // v 显示压缩比信息
 // [1-9] 1最快 9最佳
```


> bzip2 \[-cdkzv] -[1-9] \<filename>

``` bash
 // c 输出信息到屏幕
 // d 解压缩
 // z 压缩
 // v显示压缩比信息
 // k保留源文件
 // [1-9] 1最快 9最佳
```

### 打包指令

> tar xvf \<filename.bz2/gz>  -C [指定目录]// 解压缩

> tar tvf \<filename.bz2/gz>  //查看

> tar cvf \<newfilename>   \<filename>    //打包 
