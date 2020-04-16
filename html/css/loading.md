　　在UI库中都会有加载提示，一直想学着写，两三个月前在网上看了几个常见的，也尝试写了一遍，突然翻出来发现又看不懂了，重新再看一遍，加深点印象

### 准备工作

　　因为内容多，先把`html`部分整体贴上吧，就不分开了
``` html
<body>
    <div class="box">
        loader_01
        <div class="load_1"></div>
    </div>
    <div class="box">
        loader_02
        <div class="load_2"></div>
    </div>
    <div class="box">
        loader_03
        <div class="load_3"></div>
    </div>
    <div class="box">
        loader_04
        <div class="load_4"></div>
    </div>
    <div class="box">
        loader_05
        <div class="load_5"></div>
    </div>
    <div class="box">
        loader_06
        <div class="load_6"></div>
    </div>
    <div class="box">
            loader_07
        <div class="load_7"></div>
    </div>
    <div class="box">
        loader_08
        <div class="load_8"></div>
    </div>
    <div class="box">
        loader_09
        <div class="load_9">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
        </div>
    </div>
    <div class="box">
            loader_10
        <div class="load_10"></div>
    </div>
    <div class="box">
        loader_11
        <div class="load_11">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
        </div>
    </div>
</body>
```

　　现在再贴共用的`CSS`样式

``` css
body{
    background: #333333;
    text-align: center;
    width: 960px;
    max-width: 100%;
    margin: 0 auto;
    box-sizing: border-box;
    font-family: sans-serif;
    color: rgba(200, 200, 200, 0.1);
}
body *, body *:before, body *:after {
    box-sizing: inherit;
}
.box {
    display: inline-block;
    width: 200px;
    height: 200px;
    border: solid 1px currentcolor;
    border-radius: 3px;
    font-size: 30px;
    color: rgba(200, 200, 200, 0.9);
    padding: 1em;
    margin-bottom: .25em;
    vertical-align: top;
    -webkit-transition: .3s color, .3s border;
    transition: .3s color, .3s border;
}
[class*="load_"] {
    display: inline-block;
    width: 1em;
    height: 1em;
    color: inherit;
    vertical-align: middle;
    pointer-events: none;
}
```

### 重点部分

　　load_1 样式

```
.load_1{
    border: .1em dotted currentcolor;
    border-radius: 50%;
    animation: 1s loader-01 linear infinite;
}
@keyframes loader-01 {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    100% {
        -webkit-transform: rotate(360deg);
        transform: rotate(360deg);
    }
}
```

　　load_2 样式

``` css
.load_2{
    background-color: currentcolor;
    animation: loader-02 2s infinite ease-in-out;
}
@keyframes loader-02 {
    0% {
        transform: perspective(120px) rotateX(0deg) rotateY(0deg);
    }
    50% {
        transform: perspective(120px) rotateX(-180deg) rotateY(0deg);
    }
    100% {
        transform: perspective(120px) rotateX(-180deg) rotateY(-179.9deg);
    }
}
```
　　load_3 样式

``` css
.load_3{
    /* background-color: currentColor; */
    position: relative;
}
.load_3:before,
.load_3:after {
    content: '';
    display: block;
    position: absolute;
    background-color: currentColor;
    left: 50%;
    right: 0;
    top: 0;
    bottom: 50%;
    box-shadow: -.5em 0 0 currentcolor;
    animation: load-3 1s linear infinite;
}
.load_3:after {
    top: 50%;
    bottom: 0;
    animation-delay: .25s;
}
@keyframes load-3 {
    0%, 100% {
        box-shadow: -.5em 0 0 transparent;
        background-color: currentcolor;
    }
    50% {
        box-shadow: -.5em 0 0 currentcolor;
        background-color: transparent;
    }
}
```
　　load_4 样式

``` css
.load_4:before, .load_4:after, .load_4{
    border-radius: 50%;
    animation-fill-mode: both;
    animation: load-4 1.8s infinite ease-in-out;
}
.load_4{
    color: currentcolor;
    position: relative;
    transform: translateZ(0);
    animation-delay: -0.16s;
    top: -1em;
}
.load_4:before{
    right: 100%;
    animation-delay: -0.32s;
}
.load_4:after{
    left: 100%;
}
.load_4:before, .load_4:after {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    width: inherit;
    height: inherit;
}
@keyframes load-4 {
    0%, 80%, 100% {
        box-shadow: 0 1em 0 -1em;
    }
    40% {
        box-shadow: 0 1em 0 -.2em;
    }
}
```
　　load_5 样式

``` css
.load_5{
    background-color: currentColor;
    position: relative;
    width: .3em;
    height: .6em;
    animation: load-5 1s ease-in-out infinite;
    animation-delay: .4s;
}
.load_5:before, .load_5:after{
    content: '';
    position: absolute;
    width: inherit;
    height: inherit;
    background: inherit;
    animation: inherit;
}
.load_5:before {
    right: .6em;
    animation-delay: 0.2s;
}
.load_5:after {
    left: .6em;
    animation-delay: 0.6s;
}
@keyframes load-5 {
    0%, 100% {
        box-shadow: 0 0 0 currentcolor, 0 0 0 currentcolor;
    }
    50% {
        box-shadow: 0 -.3em 0 currentcolor, 0 .3em 0 currentcolor;
    }
}
```
　　load_6 样式

``` css
.load_6 {
    /* width: 20px; */
    /* height: 24px; */
    border: 1px rgba(255, 255, 255, 1) solid;
    border-radius: 0 0 5px 5px;
    position: relative;
    margin: 1em auto;
}
.load_6:after, .load_6:before{
    position: absolute;
    content: ' ';
}
.load_6:after{
    width: .3em;
    height: .7em;
    border: 1px #fff solid;
    border-left: none;
    border-radius: 0px 1em 1em 0px;
    left: 1em;
    top: .05em;
}

.load_6:before{
    width: .05em;
    height: .5em;
    background-color: rgba(255, 255, 255, 1);
    top: -.3em;
    left: .2em;
    box-shadow: .25em 0 0 0 rgba(255,255,255,1),
        .25em -.25em 0 0 rgba(255,255,255,1),
        .5em 0 0 0 rgba(255,255,255,1);
    animation: load-6 1s linear infinite alternate;
}

@keyframes load-6 {
    0%{height: 0px}
    100%{height: 6px;}
}
```
　　load_7 样式

``` css
.load_7{
    border: solid 1px #FFF;
    border-radius: 50%;
    margin: 30px auto;
    animation: load-7 2s ease-in-out infinite;
}
.load_7:after{
    content: '';
    width: 5px;
    height: 5px;
    border-radius: 100%;
    background-color: rgba(255,255,255,1);
    position: absolute;
}
@keyframes load-7 {
    0%{transform: rotate(0deg);}
    100%{transform: rotate(360deg);}
}
```
　　load_8 样式

``` css
.load_8{
    transform: rotateZ(45deg);
    perspective: 1000px;
    border-radius: 50%;
}
.load_8:before, .load_8:after {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    width: inherit;
    height: inherit;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}
.load_8:before {
    transform: rotateX(70deg);
}
.load_8:after{
    transform: rotateY(70deg);
    animation-delay: .4s;
}
@keyframes spin {
    0%, 100% {
        box-shadow: .2em 0px 0 0px currentcolor;
    }
    12% {
        box-shadow: .2em .2em 0 0 currentcolor;
    }
    25% {
        box-shadow: 0 .2em 0 0px currentcolor;
    }
    37% {
        box-shadow: -.2em .2em 0 0 currentcolor;
    }
    50% {
        box-shadow: -.2em 0 0 0 currentcolor;
    }
    62% {
        box-shadow: -.2em -.2em 0 0 currentcolor;
    }
    75% {
        box-shadow: 0px -.2em 0 0 currentcolor;
    }
    87% {
        box-shadow: .2em -.2em 0 0 currentcolor;
    }
}
```
　　load_9 样式

``` css
.load_9{
    width: 2.5em;
    height: 2.5em;
}
.load_9 span{
    display: inline-block;
    vertical-align: middle;
    width: .2em;
    height: .2em;
    margin: .01em;
    background: #007DB6;
    border-radius: .6em;
    animation: load-9 1s infinite alternate;
}
.load_9 span:nth-of-type(2) {
    background: #009B9E;
    animation-delay: 0.2s;
}
.load_9 span:nth-of-type(3) {
    background: #00B247;
    animation-delay: 0.4s;
}
.load_9 span:nth-of-type(4) {
    background: #5AB027;
    animation-delay: 0.6s;
}
.load_9 span:nth-of-type(5) {
    background: #A0B61E;
    animation-delay: 0.8s;
}

@keyframes load-9 {
    0%{
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
```
　　load_10 样式

``` css
.load_10 {
    width: .2em;
    height: .2em;
    position: relative;
    transform: rotateZ(0);
    border-radius: 100%;
    animation: load-10 1s infinite linear;
}

@keyframes load-10 {
    0%,100% {
    box-shadow: 0 -.9em 0 0.05em, .6em -.6em 0 0em, .9em 0 0 -.3em, .6em .6em 0 -.3em, 0 .9em 0 -.3em, -.6em .6em 0 -.3em, -.9em 0 0 -.3em, -.6em -.6em 0 0;
    }
    12.5% {
        box-shadow: 0 -.9em 0 0, .6em -.6em 0 0.05em, .9em 0 0 0, .6em .6em 0 -.3em, 0 .9em 0 -.3em, -.6em .6em 0 -.3em, -.9em 0 0 -.3em, -.6em -.6em 0 -.3em;
    }
    25% {
        box-shadow: 0 -.9em 0 -0.5em, .6em -.6em 0 0, .9em 0 0 0.05em, .6em .6em 0 0, 0 .9em 0 -.3em, -.6em .6em 0 -.3em, -.9em 0 0 -.3em, -.6em -.6em 0 -.3em;
    }
    37.5% {
        box-shadow: 0 -.9em 0 -.3em, .6em -.6em 0 -.3em, .9em 0em 0 0, .6em .6em 0 0.05em, 0 .9em 0 0em, -.6em .6em 0 -.3em, -.9em 0em 0 -.3em, -.6em -.6em 0 -.3em;
    }
    50% {
        box-shadow: 0 -.9em 0 -.3em, .6em -.6em 0 -.3em, .9em 0 0 -.3em, .6em .6em 0 0em, 0 .9em 0 0.05em, -.6em .6em 0 0, -.9em 0em 0 -.3em, -.6em -.6em 0 -.3em;
    }
    62.5% {
        box-shadow: 0 -.9em 0 -.3em, .6em -.6em 0 -.3em, .9em 0 0 -.3em, .6em .6em 0 -.3em, 0 .9em 0 0, -.6em .6em 0 0.05em, -.9em 0 0 0, -.6em -.6em 0 -.3em;
    }
    75% {
        box-shadow: 0em -.9em 0 -.3em, .6em -.6em 0 -.3em, .9em 0em 0 -.3em, .6em .6em 0 -.3em, 0 .9em 0 -.3em, -.6em .6em 0 0, -.9em 0em 0 0.05em, -.6em -.6em 0 0;
    }
    87.5% {
        box-shadow: 0em -.9em 0 0, .6em -.6em 0 -.3em, .9em 0 0 -.3em, .6em .6em 0 -.3em, 0 .9em 0 -.3em, -.6em .6em 0 0, -.9em 0em 0 0, -.6em -.6em 0 0.05em;
    }
}
```
　　load_11 样式

``` css
.load_11{
    width: 100px;
    height: 100px;
    position: relative;
    margin: 0 auto;
}
.load_11 span{
    display: inline-block;
    width: 16px;
    height: 16px;
    background-color: lightgreen;
    border-radius: 50%;
    position: absolute;
    animation: load-11 1.04s ease infinite;
}
@keyframes load-11 {
    0% {
        opacity: 1;
    }
    100% {
        opacity: 0.2;
    }
}
.load_11 span:nth-child(1) {
    left: 0;
    top: 50%;
    margin-top:-8px;
    animation-delay:0.13s;
}
.load_11 span:nth-child(2) {
    left: 14px;
    top: 14px;
    animation-delay:0.26s;
}
.load_11 span:nth-child(3) {
    left: 50%;
    top: 0;
    margin-left: -8px;
    animation-delay:0.39s;
}
.load_11 span:nth-child(4) {
    top: 14px;
    right:14px;
    animation-delay:0.52s;
}
.load_11 span:nth-child(5) {
    right: 0;
    top: 50%;
    margin-top:-8px;
    animation-delay:0.65s;
}
.load_11 span:nth-child(6) {
    right: 14px;
    bottom:14px;
    animation-delay:0.78s;
}
.load_11 span:nth-child(7) {
    bottom: 0;
    left: 50%;
    margin-left: -8px;
    animation-delay:0.91s;
}
.load_11 span:nth-child(8) {
    bottom: 14px;
    left: 14px;
    animation-delay:1.04s;
}
```

　　11个常见的loading样式，基本够用了。例子在 [这里](https://github.com/fg411/essay/blob/master/Demo/html/loading.html)

### 知识点

 - [伪类](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes)
 - [:nth-of-type](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-of-type)
 - [CSS3 animation 属性](https://www.w3school.com.cn/cssref/pr_animation.asp)
