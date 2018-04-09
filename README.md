## <center> 如何给网站设置ICO图标

-  方法1

    直接在站点根目录下放入名为：favicon.ico 的图标文件（必须要为 ICO 文件，BMP 及其他格式的图片文件不行）。还有将 favicon.ico 中的 favicon 命名为你网站域名的名称也可以，例如：你网站的域名为：yichenghui.net，你可以将该 ICO 文件命名为：yichenghui.ico 。

-   方法2

       在网页的 ```<head>...</head>``` 区加入代码：```<link rel="Shortcut Icon" href="favicon.ico" />```，如果用这一种方法的话，其中 ICO 文件的文件名就不一定要用 favicon.ico了，可以用任意的名字来命名，如：aoul.ico，你甚至可以使每一个目录下的每一个网页文件的IE地址栏图标都不同，但前提是 必须做到图标文件的链接地址要正确。还有，在
       ``` <head>...</head> 区加入代码：<link rel="Bookmark" href="favicon.ico" />```，就可以在收藏夹中显示你网页链接的自定义图标。

-   方法3

    在网站首页的源文件<head> </head>之间插入下面的斜体部分代码
    ```<head> ……<link rel="shortcut icon" href="favicon.ico"></head>```

-   方法4

    `动态ico图标的实现方法`
    先把做好的gif动态图标命名为favico.gif <head></head>之间加上：
    ```
    <link rel="icon" href="favicon.gif" type="image/gif" >
    ```
## <center> 移动端input问题

-   父元素没有padding，input没有margin，位置就是不对

-   解决办法：

    -   直接改变盒子模型为block，或者使用其他间接改变盒子模型的方法，比如浮动(float)，或者定位(position)

## <center>  阻止鼠标滚轮滚动
```javascript
window.onload = function () {
    function uninstllMousrScroll(evt) {
        return false;
    }
    if (document.addEventListener) {
        document.addEventListener('DOMMouseScroll', uninstllMousrScroll, false);
    }  
    window.onmousewheel = document.onmousewheel = uninstllMousrScroll;
}    
```

## <center> css溢出省略号
```css
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

## <center> ```animationend```和```transionend```

-   在使用transionend监听动画完成事件是，发现无效，因为用了animated.css，而animated.css用的是
```css
animation-name: slideTop;
animation-duration: 0.5s;
animation-fill-mode: forwards;
```
-   所以transionend会无效，需要用animationend监听
    代码示例:
     -   原生JavaScript
    ```javascript
    domObj.addEventListener('animationend',doSometing ())
    ```
    
    -   jQuery
    ```javascript
     .on('animationend', '.CostList', doSometing ())
    ```   

## axios表单提交方法

-   使用vue的ajax框架中，发现同样的post数据，vue-resource拿到的数据是正确的，axios则不正确
-   对比了这两个ajax框架的所有数据，发现vue-resource发送的是formdata（表单）数据格式，axios则是普通的json
-   所以需要自定义axios的post为表单格式
-   自定义axios表单提交方法如下
```javascript
this.$axios({
          url: '接口地址',
          method: "post",
          data: {
            需要提交的数据
          },
          transformRequest: [
            data=> {
              let ret = "";
              for (let it in data) {
                ret +=`${encodeURIComponent(it)}=${encodeURIComponent(data[it])}&`
              }
              return ret;
            }
          ]
        }).then()
```        

## <center> HTML 5 ```<input> pattern``` 属性

-   只能包含三个字母的文本字段（数字或特殊字符）：

-   示例代码 
```html
<input type="text" name="country_code" pattern="[A-z]{3}" title="Three letter country code" />
```

-   定义和用法
    -   pattern 属性规定用于验证输入字段的模式。

    -   模式指的是正则表达式。您可以在我们的 JavaScript 教程中阅读到这方面的内容。

    -   注释：pattern 属性适用于以下 ```<input>``` 类型：```text, search, url, telephone, email``` 以及 ```password``` 。

-   提示：请使用标准的 "title" 属性来描述模式。

-   oninvalid属性验证表单在html5笔记中有记录，可以到html5页面中CTRL+F搜索关键字```oninvalid```

## <center> 一张图片看懂```scroll client offset```

<center> <img src='http://yichenghui.net/images/gitNote1.png'>
