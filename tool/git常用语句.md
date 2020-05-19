
### 配置用户信息

　　安装完 Git 之后，要做的第一件事就是设置你的用户名和邮件地址。 这一点很重要，因为每一个 Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改

　　下面是配置全局的用戶信息

```shell
>git config --global user.name "xxx"        // 修改用户名，xxx 处填写你的用户名
>git config --global user.email "xxx"       // 修改邮箱地址，xxx 处填写你的邮箱地址
```

### 检查配置信息

　　如果想要检查你的配置，可以列出所有 Git 当时能找到的配置，也可以只查看用戶名、郵箱

```shell
>git config --list
>git config user.name
>git config user.email
```

### 修改指定项目的用户名和邮箱地址

　　如果希望在一个特定的项目中使用不同的 `用户名` 和 `邮箱` 来提交，可以使用下面的方法单独设置 `用户名` 和 `邮箱` ，如果不设置就会默认使用上面全局设置的 `用户名` 和 `邮箱`

```shell
>git config user.name "xxx"
>git config user.email "xxx"
```

### clone 项目

　　使用`git`时，常用到 `clone` 命令

```shell
>git clone https://github.com/fg411/suduku.git
```

　　在`clone`的时候如果需要指定其他用户，可以使用下面这个命令

```shell
>git clone http://userName:password@链接
```

　　如下：

```shell
>git clone https://fg411:12345678@github.com/fg411/suduku.git
```

------

附上常用命令速查表

![Git 常用命令速查表](../../Demo/img/git_command.jpg)


------
### 资料

- [1.6 起步 - 初次运行 Git 前的配置](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE)
