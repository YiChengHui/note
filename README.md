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

## <center> axios表单提交方法

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
    
##  angular.js(ng1)中如何监控dom渲染完毕

-   当我们使用AngulraJs使用的时候，希望在render完table后，执行一段js脚本

-   在实际开发中，会经常碰到这样的需求，希望能够捕获到AngularJs渲染完成页面的事件。

-   要达到这个目的，我们需要为当前的app自定义directive:

    ```javascript
    app.directive('onFinishRenderFilters', function ($timeout) {
        return {
            restrict: 'A',
            link: function(scope, element, attr) {
            if (scope.$last === true) {
                $timeout(function() {
                scope.$emit('ngRepeatFinished');
                });
            }
            }
        };
    });
    ```
-   然后，在我们需要监控的地方，加上该directive:
    ```html
    <tr ng-repeat="user in users" on-finish-render-filters>
        <td>{{user.Id}}</td>
        <td>{{user.Name}}</td>
        <td>{{user.Salary}}</td>
    </tr>
    ```    

-   最后，补充上我们需要render完成之后的业务逻辑
    ```javascript
    $scope.$on('ngRepeatFinished', function (ngRepeatFinishedEvent) {
        /*
            在这里可以做ng-repeat完成之后的下一个业务逻辑
            因为ng的指令执行也是有先后顺序的
        */
    });
    ```        
## <center> php操作mysql
-   创建连接
```php
$conn = new mysqli('servername','username', 'password','userInfo');
if ($conn->connect_error) {
    die("连接失败: " . $conn->connect_error);
} 
```


-   数据库创建
```php
$sql = "CREATE DATABASE userInfo";
    if ($conn->query($sql) === TRUE) {
        echo "数据库创建成功";
    } else {        
        echo "Error creating database: " . $conn->error;
    }
```

-   使用 sql 创建数据表
```php
$sql = "CREATE TABLE MyGuests (
    id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, 
    firstname VARCHAR(30) NOT NULL,
    lastname VARCHAR(30) NOT NULL,
    email VARCHAR(50),
    reg_date TIMESTAMP
)";    
if ($conn->query($sql) === TRUE) {
    echo "Table MyGuests created successfully";
} else {
    echo "创建数据表错误: " . $conn->error;
}
```

-   插入数据
```php
    $sql = "INSERT INTO MyGuests (firstname, lastname, email)
    VALUES ('John', 'Doe', 'john@example.com');";
    $sql .= "INSERT INTO MyGuests (firstname, lastname, email)
    VALUES ('Mary', 'Moe', 'mary@example.com');";
    $sql = "INSERT INTO MyGuests (firstname, lastname, email)
    VALUES ('one', 'two', 'three@example.com')";
```
-   查询数据
    -   语法
    ```
    SELECT column_name(s) FROM table_name WHERE column_name operator value
    ```
    -   示例代码：
    ```php
    $sql = "SELECT id, firstname, lastname FROM MyGuests";
    $result = $conn->query($sql);    
    if ($result->num_rows > 0) {
            // 输出数据
        while($row = $result->fetch_assoc()) {
            echo "id: " . $row["id"]. " - Name: " . $row["firstname"]. " " . $row["lastname"]."<br>";
        }
    } else {
        echo "0 结果";
    }
    ```
   
-   删除数据

```php
    $con=mysqli_connect($servername, $username, $password,'userInfo');
    // 检测连接
    if (mysqli_connect_errno())
    {
        echo "连接失败: " . mysqli_connect_error();
    }

    mysqli_query($con,"DELETE FROM MyGuests WHERE LastName='yyyyyy'");
```    

-   修改数据
    -   语法
    ```php
    UPDATE table_name SET column1=value,  column2=value2,... WHERE some_column=some_value
    ```
    -   示例代码：
    ```php
    mysqli_query($con,"UPDATE MyGuests SET lastname='hhhhhhh' WHERE firstname='Julie' AND lastname='Doe'");

    // mysqli_query($con,"UPDATE MyGuests SET lastname='Doe' WHERE firstname='Julie'");
    ```    
-   关闭连接
```php
mysqli_close($con);
```
## <center> input标签checked选中
-   jquery
    ```javascript
    $('.checkbox input').prop('checked')
    ```
-   原生JavaScript
    ```javascript
    domObj.checked
    ```
-   返回值： 均为boolean值(true|false)

-   注意，只要标签中有checked属性，那么这个input就会被选中:
    ```javascript
    <input type='checked' checked>
    ```    
## <center> ES6 Promise
-   一个 Promise 就是一个代表了异步操作最终完成或者失败的对象。大多数人都在使用由其他函数创建并返回的promise

-   本质上，一个promise是某个函数返回的对象，你可以把回调函数绑定在这个对象上，而不是把回调函数当作参数传进函数。 

-   一个最简单的Promise例子：生成一个0-2之间的随机数，如果小于1，则等待一段时间后返回成功，否则返回失败：

    -   异步方法
    ```javascript
    function test(resolve, reject) {
        var timeOut = Math.random() * 2;
        log('set timeout to: ' + timeOut + ' seconds.');
        setTimeout(function () {
            if (timeOut < 1) {
                log('call resolve()...');
                resolve('200 OK');
            }
            else {
                log('call reject()...');
                reject('timeout in ' + timeOut + ' seconds.');
            }
        }, timeOut * 1000);
    }
    ```
    -   Promise
    ```javascript
    var p1 = new Promise(test);
    var p2 = p1.then(function (result) {
        console.log('成功：' + result);
    });
    var p3 = p2.catch(function (reason) {
        console.log('失败：' + reason);
    });

    /*上面代码简写如下*/
    new Promise(test).then(function (result) {
    console.log('成功：' + result);
    }).catch(function (reason) {
        console.log('失败：' + reason);
    });
    ```
-   参考链接
    -   廖雪峰Promise:```https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014345008539155e93fc16046d4bb7854943814c4f9dc2000```
    -   MDN Promise:```https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_promises``` 
