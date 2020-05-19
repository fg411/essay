
## `Mac`安装

``` shell
>brew install tree
```

## 实用命令

　　我们可以在目录遍历时使用 -L 参数指定遍历层级。例：显示项目三层结构，`tree -l 3`

``` shell
>tree -L n
```

　　如果你想把一个目录的结构树导出到文件 Readme.md ,可以这样操作

``` shell
>tree -L 2 >README.md //然后我们看下当前目录下的 README.md 文件
```

　　只显示文件夹

``` shell
>tree -d
```

　　`tree -I pattern` 用于过滤不想要显示的文件或者文件夹。比如要过滤项目中的node_modules文件夹

``` shell
>tree -I "node_modules"
```

------

## 资料

 - [Mac下的 tree 命令 输出目录树层结构](https://www.jianshu.com/p/9411d60950bf)