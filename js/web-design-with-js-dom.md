## 第2章 JavaScript 语法
> 本章内容: `语句` `变量和数组` `操作符` `条件语句和循环语句` `函数与对象`

### JS应该放在哪儿
在Web端用JavaScript编写的代码必须通过HTML/XHTML文档才能执行。下面的例子能使浏览器更快地加载页面：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Just a test</title>
</head>
<body>
    <script src="example.js"></script>
</body>
</html>
```
### 变量
JS允许程序员直接对变量赋值而无需事先声明

### 数组
数组申明:

```javascript
var a = [];
var b = Array();
var c = Array(4); //[ , , ,  ]
```

关联数组[key: value],
用字符串来代替下标, **不要使用这种数组方式, 其本质是对象**

```javascript
var lennon = [];
lennon["name"] = "John";
lennon["year"] = "1940";
lennon["living"] = "false";
```

### 对象初探
前面提到的关联数组更好的写法如下:

```javascript
var lennon = {name: "John",
              year:1940,
              living: false};
```
用对象来代替传统数组的做法意味着可以通过元素的名字而不是下标数字来引用它们, 这大大提高了脚本的可读性.

包含在对象里的数据可以通过两种形式访问:
- 属性: 隶属于某个特定对象的变量
- 方法: 某个特定对象才能调用的函数

### 内建对象
数组就是一种内建对象:

```javascript
var beatles = new Array();
beatles.length //we can use the lenght method of Array
```
其他内建对象有**Math, Date等** 内建对象的方法能帮助我们快速, 简单地完成任务

### 宿主对象
JS里可以使用的一些已经预定义好的其他对象, 不是由JS语言本身而是由它的运行环境提供的. 在Web应用中,这个环境就是浏览器.如Form, Image, Element等, 用来获取表单, 图像和各种表单元素等信息.

> 另一种宿主对象也能用来获得网页上的任何一个元素的信息, 它就是`document`对象.

---

## 第3章 DOM
> 本章内容: `节点的概念` `5个常用的DOM方法`

### DOM是什么

**"D"**: 当创建了一个网页并把它加载到Web浏览器中时, DOM就产生, 它把你编写的网页文档转换成为一个文档对象.

**"O"**: JS中有三种对象类型:
- **用户定义对象** 由程序员自行创建的对象, 本书不讨论这种对象
- **内建对象** 内建在JS语言中的对象, 如`Array` `Math`和`Date`等
- **宿主对象** 由浏览器提供的对象

    **window对象** 对应着浏览器窗口本身, 通常称为`BOM(Browser Object Model)`
    >window对象方法要为到处滥用的各种弹出窗口和下拉菜单负责! 我们不需要与BOM打太多的交道, 而把注意力放在浏览器窗口内的网页内容上: **DOM**

**"M"**: 加载到浏览器窗口的当前网页的模型, 我们可以通过JavaScript去读取这个模型

DOM把一份文档表示成一课节点树, 非常适合用来表示一份用(X)HTML语言编写出来的文档.

**例子:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Shopping list</title>
</head>
<body>
<h1>What to buy</h1>
<p title="a gentle reminder">Don't forget to buy this stuff.</p>
<ul id="purchases">
    <li>A tin of beans</li>
    <li class="sale">Cheese</li>
    <li class="sale important">Milk</li>
</ul>
</body>
</html>

```

### 节点

**元素节点** DOM的原子, 如body, p和ul之类的元素

**文本节点** p 元素中的"Don't forget to buy this stuff"

**属性节点** title="a gentle reminder"

### getElementById

这个方法将返回一个与那个有着给定id属性值的元素节点对象, 一般来说, 没有必要为文档里的每一个对象都定义一个独一无二的id值.

```
<script src="example.js"></script> //in html5

alert(typeof document.getElementById("purchases")); //in js
```

### getElementByTagName
返回一个对象数组, 每个对象分别对应着文档里有着给定标签的一个元素, 入参是标签名字.

```javascript
for (var i = 0; i < document.getElementsByTagName("li").length; i++) {
    alert(document.getElementsByTagName("li")[i]);
}
```

### getElementsByClassName
通过class属性中的类名来访问元素

### getAttribute
不属于document对象, 只能通过元素节点对象调用, 例如:

```javascript
var paras = document.getElementsByTagName("p");
for (var i=0; i <paras.length; i++) {
    var title_text = paras[i].getAttribute("title");
    if (title_text) alert(title_text);  //放在同一行缩短代码
}
```
### setAttribute
不会改变文档源码里的值(view source)
```javascript
var shopping = document.getElementById("purchases");
alert(shopping.getAttribute("title"));
shopping.setAttribute("title", "a list of goods");
alert(shopping.getAttribute("title"));
```

---

## 第4章 案例研究: JS图片库
### 案例1: 在同一页面显示图片

```html
<!--gallery.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Image Gallery</title>
</head>
<body>
    <h1>Snapshots</h1>
<ul>
    <li>
        <a href="../images/Chrysanthemum.jpg" onclick="showPic(this);
         return false;" title="Chrysanthemum display"> Chrysanthemum</a>
    </li>
    <li>
        <a href="../images/Desert.jpg" onclick="showPic(this); return false;" title="A cup of black coffee"> Desert</a>
    </li>
    <li>
        <a href="../images/Hydrangeas.jpg" onclick="showPic(this); return false;" title="A red, red rose"> Hydrangeas</a>
    </li>
    <li>
        <a href="../images/Jellyfish.jpg" onclick="showPic(this); return false;" title="A famous clock"> Jellyfish</a>
    </li>
</ul>
<img id="placeholder" src="../images/Jellyfish.jpg" alt="my image gallery" />
<script src="./showPic.js"></script>
</body>
</html>
```

```javascript
/* showPic.js */
function showPic(whichpic) {
    var source = whichpic.getAttribute("href");
    var placeholder = document.getElementById("placeholder");
    placeholder.setAttribute("src", source);
}
```
### childNodes属性
用来获取任何一个元素的所有子元素, 返回的是数组
