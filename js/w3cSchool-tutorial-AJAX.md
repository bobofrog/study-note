## AJAX Introduction

### 什么是AJAX?
AJAX = Asynchronous JavaScript and XML.
> AJAX这个名字会误导你, 其实你并不需要懂XML.

AJAX是用来建立快速, 动态网页的一种技术.

以往的网页在内容发生改变时必须重载整个页面, 而AJAX不需要. 用AJAX的产品: Google Maps, Gmail, YouTube and Facebook

### AJAX如何工作的?
Browser中有事件发生时, Browser就创建一个XMLHttpReques Object, 然后发送HttpRequest给Server. Server接受到HttpRequest后开始处理, 创建相应的response并且发还数据给Browser. Browser用JavaScript code来处理接收到的数据(response)来更新页面内容.

AJAX 用了:
- **XMLHttpRequest** object (to retrieve data from a web server)
- **JavaScript/DOM** (to display/use the data)
> XMLHttpRequest这个名字同样误导你, 其实你并不需要懂XML.

Example 1:

```html
<!DOCTYPE html>
<html>
<body>

<div id="demo"><h2>Let AJAX change this text</h2></div>

<!--The <button> calls a function (if it is clicked)-->
<button type="button" onclick="loadDoc()">Change Content</button>

<script>
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (xhttp.readyState == 4 && xhttp.status == 200) {
      document.getElementById("demo").innerHTML = xhttp.responseText;
    }
  };
  xhttp.open("GET", "ajax_info.txt", true);
  xhttp.send();
}
</script>

</body>
</html>

```
Example 2:
> Google Suggest: 谷歌搜索栏里当你输入一些词时显示的search suggestion是JavaScript发送这些词给server, 然后server返回一系列的suggestions, 即动态地加载页面.

## AJAX XMLHttp
> XMLHttpRequest Object是AJAX的keystone, 所有的现代Browser(Chrome, IE7+, Firefox, Safari, Opera)都支持

创建一个XMLHttpRequest Object:

```javascript
var xhttp = new XMLHttpRequest();
```

## AJAX request
向server发送请求:

```javascript
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();
```

Method | Description
---|---
**open**(method, url, async) | **method**: the type of request: GET or POST, **url**: the server (file) location, **async**: true/false
**send**() | Sends the request to the server (used for GET)
**send**(string) | Sends the request to the server (used for POST)

### GET or POST?
GET比POST简单而且快速, 大多数情况下用GET. 但是, 应该在如下情况下使用POST 请求:
- A cached file is not an option (update a file or database on the server).
- Sending a large amount of data to the server (POST has no size limitations).
- Sending user input (which can contain unknown characters), POST is more robust and secure than GET.

### GET请求
一个基本的GET请求:

```javascript
xhttp.open("GET", "demo_get.asp", true);
xhttp.send();
```
### POST请求
一个基本的POST请求:
```javascript
xhttp.open("POST", "demo_post.asp", true);
xhttp.send();
```
如果要POST类似于HTML格式的数据, 需要用setRequestHeader()添加HTTP头, 然后在send()方法中指定数据内容.

```javascript
xhttp.open("POST", "ajax_test.asp", true);
xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhttp.send("fname=Henry&lname=Ford");
```

Method | Description
---|---
**setRequestHeader**(header, value) | Adds HTTP headers to the request, **header**: specifies the header name, **value**: specifies the header value

## AJAX Response
 我们用XMLHttpRequest对象的responseText或者responseXML属性来获取来自server的response. 如果response是纯文本, 我们用responseText属性, 若是XML, 则用responseXML.


Property | Description
---|---
responseText | get the response data as a string
responseXML | get the response data as XML data

## AJAX Events
### onreadystatechange, readyState & status
当向server发送一个请求, 我们希望能进行一些操作. **onreadystatechange** 事件在**readyState**改变时触发. readyState = 4, status = 200, response is ready.

> If you have more than one AJAX task on your website, you should create ONE standard function for creating the XMLHttpRequest object, and call this for each AJAX task. [w3cSchool](http://www.w3schools.com/ajax/ajax_xmlhttprequest_onreadystatechange.asp)

## AJAX Reference
[AJAX——核心XMLHttpRequest对象](http://blog.csdn.net/liujiahan629629/article/details/17126727)
