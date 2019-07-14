# ubuntu 搭建shadowsocks服务

更新软件源

```
>sudo apt-get update
```

安装PIP环境

```
>sudo apt-get install python-pip
```
安装shadowsocks

```
>sudo pip install shadowsocks
```
后台运行

```
>sudo ssserver -p 23564 -k password -m rc4-md5 --user nobody -d start
```
端口号：23564
密码：password
加密方法：rc4-md5