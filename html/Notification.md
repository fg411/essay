试水H5的Notification特性

看到微博有使用桌面通知功能，感觉还挺酷，本文就来研究研究

## 了解用户权限 - Notification.permission
`Notification.permission`是一个静态属性，用于表明当前通知显示授权状态，返回一个`string`类型的字符串，可以根据返回值判断用户是否授予了通知权限。
返回值有三种情况：

- default

  用户还未被询问是否授权，所以通知不会被显示
+ granted
  
  表示之前已经询问过用户，并且用户已经授予了显示通知的权限
* denied
  
  表示用户已经明确的拒绝了显示通知的权限

当值为`default`或者`denied`时都不会显示通知消息, 只有明确的被设置成`granted`才会显示通知消息


## 请求权限 - Notification.requestPermission(callback)

应用发送通知之前必须要取得发送通知的权限，才能成功进行通知. `Notification.requestPermission(callback)`是请求获取权限的方法，允许传入一个回调，回调会返回用户选择的何种权限，返回两个值，`granted`代表允许，`denied`代表拒绝。 并且`Notification.requestPermission()`支持then方式的链式调用，也就意味着可以异步调用它

## 创建通知
`new Notification(title, options)`方法创建可以创建一个通知实例，允许参入参数两个参数`title`和`options`。 注意默认情况下（实际可以通过`options`中的`timestamp`参数控制）一旦通知实例被创建出来，它会立即被显示出来

- title 参数

 表示通知的标题。必须参数，允许数字、字符串和空
- options 参数

 非必须参数，必须为一个对象，参数如下:
 ```
 {
    //通知显示正文。非必须，默认为空
    body: '你的好友XX上线了！',
    //通知显示正文的图片地址。非必须，默认为空
    image: 'imgae url',
    //通知左侧图标。非必须，默认为空
    icon: 'imgae url',
    //通知的分类标记（ID）。非必须，默认为空
    tag: 'test',
    //通知相关联的数据，通常用于方法的回调，传参。非必须，默认为空
    data: '可以是任意数据类型',
    //通知显示延迟的时间。非必须，默认通知实例创建完成就显示
    timestamp: '',
    //通知主体内容的水平展示顺序，有点类似direction属性。非必须，默认值是auto, 可以是ltr或rtl
    dir: 'auto',
    //当没有足够的空间来显示通知本身时，用于表示通知的图像的URL。非必须，默认为空
    badge: 'xxx',
    //通知的语言。非必须默认为空
    lang: '',
    //通知显示时，设备的振动模式。非必须，默认为空
    vibrate: [200, 100, 200],
    //新通知出现是否覆盖旧的通知，覆盖（true）则永远只显示一条通知，不覆盖（false）则会多条通知重叠。非必须，默认为true
    renotify: true,
    //通知是否静音。非必须，默认为false，表示无声
    silent: false,
    //通知声源文件地址。非必须，默认为空
    sound: 'mp3',
    //是否不在屏幕上显示通知信息。非必须，默认为false表示要显示
    noscreen: false,
    //指定通知是否应该粘滞性，即不容易被用户清理。非必须，默认false表示不具粘滞性
    sticky: false,
    //指定通知是否保持活性，知道用户点击或关闭。非必须，默认为false
    requireInteraction: false
 }
 ```

## 事件处理

* Notification.onclick

  处理 click 事件的处理。每当用户点击通知时被触发
* Notification.onshow

  处理 show 事件的处理。当通知显示的时候被触发
* Notification.onerror

  处理 error 事件的处理。每当通知遇到错误时被触发
* Notification.onclose

  处理 close 事件的处理。当用户关闭通知时被触发

 ## Demo

``` javascript
if(!("Notification" in window)) {
        alert("This browser does not support desktop notification");
    } else if(Notification.permission === "granted") {
        CreatNotification();
    } else if(Notification.permission !== 'denied') {
        Notification.requestPermission(function(permission){
            if(permission === "granted") {
                // 已同意,开始搞事情
            CreatNotification()
        } else{
            console.log('已被拒绝通知')
        }
    })
}

function CreatNotification() {
    var notification = new Notification('您有一条新的消息', {
        dir: 'ltr',
        body: '你的朋友有新状态啦，快去围观吧!',
        lang: "zh-CN",
        tag: 'test',
        icon: 'https://avatars1.githubusercontent.com/u/13994859?s=400&u=cb75cc71c389595460be474937e7b4b93ed280ed&v=4',
        timestamp: 3000
    });

    notification.onshow = function() {
        console.log('show')
    }
}
```
该API伴随服务器操作，打开浏览器，运行localhost，会出现一个弹窗

*注意：如果这段代码放在html中执行，一定要创建虚拟服务器，即用域名访问，如：localhost，不能直接用file:index.html 这样的路径访问，因为这个不是http协议，浏览器不接受本地文件的通知设置*


### 参考：

-----------------
 - [H5的Notification特性 - Web的桌面通知功能](https://segmentfault.com/a/1190000012127653)
 - [Notification-MDN-CN](https://developer.mozilla.org/zh-CN/docs/Web/API/notification)