# Linux下常用的 tar 命令
Linux下压缩文件有很多，让人混淆：`*.tar` 、`*.tar.gz` 、`*.tgz` 、`*.gz `、`*.Z` 、`*.bz2`

##  基础概念
- 打包：将一堆文件或目录什么的变成一个总的文件
- 压缩：将一个大的文件经过某种压缩算法变成一个小文件
因为Linux中的很多压缩程序只能针对一个文件进行压缩，所以当你想要压缩一大堆文件时，首先需要打个包(tar 命令)，然后压缩（gzip、bzip2）

`tar`常见命令参数
```
-c 建立新的压缩文件
-x 从压缩的文件中提取文件
-t 显示压缩文件的内容
-r 添加文件到已经压缩的文件
-u 添加改变了和现有的文件到已经存在的压缩文件
```
在参数的中， `c`/`x`/`t`/`r`/`u` 这五个参数是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用，但一次只能用其中一个


```
-z 支持gzip解压文件
-j 支持bzip2解压文件
-Z 支持compress解压文件
-v 显示操作过程
-f 指定包的文件名，用在最后一个参数

-A 新增压缩文件到已存在的压缩
-d 记录文件的差别
-l 文件系统边界设置
-k 保留原有文件不覆盖
-m 保留文件不被覆盖
-W 确认压缩文件的正确性
```

tar命令的选项有很多(用man tar可以查看到)，下面列出常用的


``` shell
>tar -cf all.tar *.jpg
```
将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包 ，-f指定包的文件名


``` shell
>tar -rf all.tar *.jpeg
```
将所有.jpeg的文件增加到all.tar的包里面去。-r是表示增加文件的意思


``` shell
>tar -uf all.tar wz.jpeg
```
更新原来tar包all.tar中wz.jpeg文件，-u是表示更新文件的意思

``` shell
>tar -tf all.tar
```
列出all.tar包中所有文件，-t是列出文件的意思


``` shell
>tar -xf all.tar
```
解压出all.tar包中所有文件，-x是解开的意思

-----------
### tar 调用 gzip
gzip是GNU组织开发的一个压缩程序，.gz结尾的文件就是gzip压缩的结果。与gzip 相对的解压程序是gunzip。tar中使用-z这个参数来调用gzip

``` shell
>tar -czf all.tar.gz *.jpg
```
将所有.jpg的文件打成一个tar包，并且将其用gzip压缩，生成一个gzip压缩过的包，包名为all.tar.gz

------------
### tar 调用 bzip2

bzip2是一个压缩能力更强的压缩程序，.bz2结尾的文件就是bzip2压缩的结果，与bzip2相对的解压程序是bunzip2。tar中使用-j这个参数来调用gzip

``` shell
>tar -cjf all.tar.bz2 *.jpg
```
将所有.jpg的文件打成一个tar包，并且将其用bzip2压缩，生成一个bzip2压缩过的包，包名为all.tar.bz2


``` shell
>tar -xjf all.tar.bz2
```
将上面产生的包解压打开

-------------
### zip

linux下提供了zip和unzip程序，zip是压缩程序，unzip是解压程序
``` shell
>zip all.zip *.jpg
```
将所有.jpg的文件压缩成一个zip包

``` shell
>unzip all.zip
```
将all.zip中的所有文件解压出来