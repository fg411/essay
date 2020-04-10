　　之前同事写过把剪切板内容粘贴到富文本框编辑器，当时只想当咸鱼就没有研究，最近研究`FileReader`时发现一个例子也是粘贴图片内容，闲来无事就写个demo试一试，顺便还发现了很多不常见的知识点

``` html
<div id="preview" contenteditable="true">
    江湖笑，<br />
    恩怨了，<br />
    人过招，<br />
    笑藏刀。 <br />
</div>
```
``` javascript
document.addEventListener('paste', function(event){
    let items = (event.clipboardData || window.clipboardData).items;
    let blob = null;
    let str = null;
    if(items && items.length) {
        for(let i = 0; i < items.length; i++) {
            if(items[i].kind == 'file' && items[i].type.indexOf('image') !== -1) {
                blob = items[i].getAsFile();
                break;
            } else if(items[i].kind === "string" && items[i].type.indexOf('text/plain') != -1) {
                items[i].getAsString(function (str) {
                    insertHtmlAtCaret(document.createTextNode(str)); // 插入文本到光标处并移动光标到新位置
                })
                return;
            }
        }
    }
    var reader = new FileReader();
    reader.onload = function(event) {
        var img = document.createElement('img');
        img.src = event.target.result;
        insertHtmlAtCaret(img);

        // document.getElementById('preview').innerHTML = '<img src="' + event.target.result + '" class="upload-image">';
        event.preventDefault();
    }
    reader.readAsDataURL(blob)
})

function insertHtmlAtCaret(childElement){
    var selection, range;
    if(window.getSelection) { // IE11 and non-IE
        selection = window.getSelection();
        if(selection.getRangeAt && selection.rangeCount) {
            range = selection.getRangeAt(0);
            range.deleteContents();
            var el = document.createElement("div");
            el.appendChild(childElement);
            // document.createDocumentFragment() 创建一个新的空白的文档片段
            var frag = document.createDocumentFragment(), node, lastNode;
            while ((node = el.firstChild)) {
                lastNode = frag.appendChild(node);
            }
            range.insertNode(frag);
            if (lastNode) {
                range = range.cloneRange();
                range.setStartAfter(lastNode);
                range.collapse(true);
                selection.removeAllRanges();
                selection.addRange(range);
            }
        }
    } else if(document.selection && document.selection.type != "Control") { // IE < 9
        //document.selection.createRange().pasteHTML(html);
    }
}
```
　　看demo说可以兼容IE10，写了半天还是不行，*我TM心态都崩了啊*。其实获取剪切板的内容并难，把剪切板内容添加到光标处才是全篇最麻烦的地方，demo里的`insertHtmlAtCaret`是网上看到的，内容我也没太明白，等哪天需要再好好研究

---

### 知识点：
 - [ClipboardEvent.clipboardData](https://developer.mozilla.org/zh-CN/docs/Web/API/ClipboardEvent/clipboardData)
 - [Document.createDocumentFragment](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createDocumentFragment)
 - [FileReader.readAsDataURL](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader/readAsDataURL)

------

### 资料

 - [js实现ctrl+v粘贴上传图片](https://www.jb51.net/article/80657.htm)
 - [HTML-DOM-createDocumentFragment方法](https://www.runoob.com/jsref/met-document-createdocumentfragment.html)
 - [Element: paste事件](https://developer.mozilla.org/zh-CN/docs/Web/Events/paste)
 - [div中粘贴图片并上传服务器 div中拖拽图片文件并上传服务器](https://www.cnblogs.com/fj99/p/5499233.html)
 - [Window.getSelection](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/getSelection)
 - [FileReader获取上传图片的宽高](http://www.mamicode.com/info-detail-2579337.html)
