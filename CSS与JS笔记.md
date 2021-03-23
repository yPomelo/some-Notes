

# 1、CSS基本入门

## 第一种  内部样式 ：

在<head>标签里 写<style></style>

```html
<style>
    h1{
        color: red;
    }
</style>
```

选择器 {

}

## 第二种  外部样式：

（最好使用这种）在<link rel="stylesheet" href="css/style.css">

![image-20210317184102552](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210317184102552.png)

## 第三种 行内样式：

``` html
<h1 style="clolr:red">我是标题</h1>
```

## 优先级：

就近原则，谁离这行代码最近就用谁  比如行内样式优先级最高

# 2、选择器

作用：选择页面上的一个或者一类元素





## 基本选择器

###  标签选择器

选择一类标签

标签{}

![image-20210317191704187](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210317191704187.png)

选择了所有的h1标签

### 类选择器

选择class名称一致的标签

格式 .类名{}

```html
<style>
    .yyy{
        color: crimson;
    }
</style>
```

```html
<h2 class="yyy">
    Hello yyy 这是h2标签
</h2>
<h3 class="yyy">
    Hello yyy 这是h3标签
</h3>
```

选择了yyy类的标签会改变颜色

### id选择器

全局唯一

格式 #id名{}

```html
<style>
        #idyyy{
            color: coral;
        }
</style>
```

```html
<h1 id="idyyy">
    Hello yyy 这是第一个h1标签
</h1>
```

### 优先级

id选择器>类选择器>标签选择器





## 层次选择器

### 1、后代选择器

选择body后面的所有p标签

```html
/*后代选择器*/
p{
    background: coral;
}
```

### 2、子选择器

```html
/*子选择器 */
body>p{
    background: cadetblue;
}
```

### 3、相邻兄弟选择器 

当前选择元素的（向下）相邻的一个兄弟元素

```html
/*相邻兄弟选择器*/
.active+p{
    background: blueviolet;

}
```

### 4、通用兄弟选择器

```html
/*通用兄弟选择器*/
.active~p{
    background: blueviolet;

}
```

当前选择元素的（向下）所有兄弟元素

## 属性选择器（常用）（重要）

```html
a[href^=http]{
    background: blue;
}
```

选择了以http开头的a标签

```html
a[id]{
    background: blue;
}
```

选择了带有id属性的a标签

= 绝对等于 

*= 包含这个元素

^= 以这个开头

$= 以这个结尾

# 3、CSS基本样式

## a标签

<a> 标签定义超链接，用于从一张页面链接到另一张页面。

<a> 元素最重要的属性是 href 属性，它指示链接的目标。

## span标签

使用 <span> 元素对文本中的一部分进行着色

```html
<p>我的母亲有 <span style="color:blue">蓝色</span> 的眼睛。</p>
```

<span> 标签没有固定的格式表现。当对它应用样式时，它才会产生视觉上的变化。如果不对 <span> 应用样式，那么 <span> 元素中的文本与其他文本不会任何视觉上的差异。

<span> 标签提供了一种将文本的一部分或者文档的一部分独立出来的方式。

## 字体样式

| [font](https://www.runoob.com/cssref/pr-font-font.html)      | 在一个声明中设置所有的字体属性       |
| ------------------------------------------------------------ | ------------------------------------ |
| [font-family](https://www.runoob.com/cssref/pr-font-font-family.html) | 指定文本的字体系列                   |
| [font-size](https://www.runoob.com/cssref/pr-font-font-size.html) | 指定文本的字体大小                   |
| [font-style](https://www.runoob.com/cssref/pr-font-font-style.html) | 指定文本的字体样式                   |
| [font-variant](https://www.runoob.com/cssref/pr-font-font-variant.html) | 以小型大写字体或者正常字体显示文本。 |
| [font-weight](https://www.runoob.com/cssref/pr-font-weight.html) | 指定字体的粗细。                     |

## 文本样式

1、颜色 color

2、文本对齐的方式 text-align:center 排版，居中

3、首行缩进 text-indent:2em 段落首行缩进

4、行高 line-height

5、装饰 text-decoration 

6、文本图片水平对齐：vertical-align:middle

## 超链接伪类

比较常使用的 a,  a:hover

```html
/*鼠标悬浮的颜色*/
a:hover{
    color: orange;
    font-size: 25px;
}
/*鼠标按住未释放的颜色*/
a:active{
    color: green;
}
a:visited{
    color: red;
}
```

## 列表

div可定义文档中的分区或节（division/section）。

div 标签可以把文档分割为独立的、不同的部分。它可以用作严格的组织工具，并且不使用任何格式与其关联。


如果用 id 或 class 来标记 <div>，那么该标签的作用会变得更加有效。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>假京东</title>
    <link href="css/style.css" rel="stylesheet" type="text/css">
</head>
<body>
<div id="nav">
    <h2 class="title">全部商品分类</h2>

    <ul>
        <li>
            <a href="#">图书</a>
            <a href="#">音像</a>
            <a href="#">数字商品</a>
        </li>
        <li>
            <a href="#">家用电器</a>
            <a href="#">手机</a>
            <a href="#">数码</a>
        </li>
        <li>
            <a href="#">电脑</a>
            <a href="#">办公</a>
        </li>
        <li>
            <a href="#">家居</a>
            <a href="#">家装</a>
            <a href="#">厨具</a>
        </li>
        <li>
            <a href="#">服饰鞋帽</a>
            <a href="#">个性化妆</a>
        </li>
        <li>
            <a href="#">礼品箱包</a>
            <a href="#">钟表</a>
            <a href="#">珠宝</a>
        </li>
        <li>
            <a href="#">食品饮料</a>
            <a href="#">保健食品</a>
        </li>
        <li>
            <a href="#">彩票</a>
            <a href="#">旅行</a>
            <a href="#">充值</a>
            <a href="#">票务</a>
        </li>
    </ul>

</div>

</body>
</html>
```

```css
#nav{
    width: 300px;
    background: gray;
}
.title{
    font-size: 18px;
    font-weight: bold;
    text-indent: 3em;
    line-height: 35px;
    background: red;
}
/*
list-style:
    none 去掉圆点
    circle 空心圆
    decimal 数字
    square 正方形
*/
/*ul{*/
/*    background: gray;*/
/*}*/
ul li{
    height: 30px;
    list-style: none;
    text-indent: 1em;
}
a{
    text-decoration: none;
    font-size: 14px;
    color: black;
}
a:hover{
    color: orange;
    text-decoration: underline;
}
```

![image-20210319145036496](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210319145036496.png)

# 4、盒子模型

margin ：外边距

padding：内边距

border：边框

![image-20210319154518886](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210319154518886.png)

div结合display：inline 或者span 结合display：inline可以实现同行排列





暂时学到18P

# 5、JavaScript

## 引入JavaScript

可以放在head标签或者body标签内

1、内部引入

```html
<script>
    alert("yyy HelloWorld")
</script>
```

2、外部引入

```html
<!--注意 script必须成对出现  自闭合标签有可能会失效-->
<script src="yyy.js"></script>
```

yyy.js

```javascript
alert("HelloWorld")
```

## 基本语法

定义变量 var score = 71

console.log(score)可以在浏览器的控制台打印变量 相当于sout

## 数据类型

### number

js不区分小数和整数

![image-20210321103608428](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210321103608428.png)

### 字符串

'abc'   "abc"

### 布尔值

ture false

### 逻辑运算

&&   ||   ！

### 比较运算符

= 赋值

== 等于 （类型不一样，值一样，也会判断为ture）

=== 绝对等于（类型一样 值一样 结果为ture） （与Java不同） 

### 数组

Java的数组必须是相同类型的对象，JS中不需要这样

![image-20210321153338961](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210321153338961.png)

去数组下标如果越界了就会 undefined

### 对象

对象是大括号 {} 数组用中括号[]



对象的每个属性之间用逗号隔开

```javascript
var person = {
    name:"yyy",
    age:3,
    tags:['js','java','web','...']
}
```

 ```bash
person.age
3
person.name
"yyy"
 ```

### 字符串

菜鸟教程 比较详细

https://www.runoob.com/js/js-strings.html

### 数组

1 .长度 arr.length

2 .arr.indexof(2) 通过元素获得下标索引

3 .slice() 截取array的一部分，返回一个新的数组

4 .push()压入到尾部, pop()弹出尾部的一个元素

5 .unshift()压入到头部 shift()弹出头部的一个元素

6 .排序sort()

 

### map和set

```javascript
var map = new Map([["tom",100],["jack",90],["yyy",100]])
var set = new Set([5,6,7])
```

菜鸟教程

遍历set和map，用

```javascript 
for(let x of set){
    console.log(x)
}
```

### 函数



```javascript
function abs(x){
    if(x>=0){
        return x;
    }else{
        return -x;
    }
}
```

等同于

```javascript
var abs = founction(x){
    if(x>=0){
        return x;
    }else{
        return -x;
    }
}
```

arguments是JS免费赠送的一个关键词

ES6引入的新特性，获取除了已经定义的参数之外的所有参数

```javascript
function aaa(a,b,...rest){
    console.log("a is"+a);
    console.log("b is"+b);
    console.log(rest);
}
```

rest 参数只能写在最后面，必须用...标识

### 变量的作用域

所有的全局变量都会绑定到window上，如果不同的js文件，使用了相同的全局变量，就会造成冲突

把自己的代码全部放到自己定义的唯一空间名字中，降低全局命名冲突的问题

```javascript
//全局唯一变量
var yyy = {}
//定义全局变量
yyy.name = "yyy";
yyy.add() = founction(a,b){
    return a+b;
}
```

jQuery中大量使用这种方法，由于jQuery不好写，它使用$来替代

### const

定义常量的标识符

### 方法

方法就是把函数放到对象里面，对象只有两个东西，属性和方法

```javascript
var yyy = {
    name:'yyy';
    birth:1996;
    //方法
    age:function(){
        var now = Date().getFullYear();
        return now - this.birth;
    }
}
//属性
yyy.name
//方法调用一定要带()
yyy.age()
```

# 6、JSON

JSON是JavaScript Object Notation

# 7、面向对象

### 原型对象继承

```javascript
var xiaoming = {
    name:"xiaoming"
};
var student = {
    name:"yyy",
    age:3,
    run:function(){
        console.log(this.name + "run...");
    }
};
//原型对象 ，小明的原型是学生
xiaoming.__proto__ = student;
```

此时调用xiaoming.run  可以发现打印 xiaoming run...

### class关键字

是在ES6之后引入的

定义类、属性、方法

```javascript
class Student{
    //构造器与Java不同
    constructor(name){
        this.name = name;
    }
    hello(){
        alert("hello");;
    }
}
var xiaoming = new Student("xiaoming");
var xiaohong = new Student("xiaohong");
xiaoming.hello();
```

# 8、操作BOM对象（重点）

BOM学名: Browser Object Model 翻译为 浏览器 对象 模型。 其实就是专门操作浏览器窗口的一组对象和函数 如果想操作浏览器窗口或访问浏览器软件的信息,就用BOM。

JavaScript和浏览器的关系？

JavaScript的诞生就是为了让它能在浏览器中运行



window代表浏览器窗口

![image-20210322203043904](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210322203043904.png)

Navigator ,封装了浏览器的信息

screen 代表屏幕

<img src="C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210322203355158.png" alt="image-20210322203355158" style="zoom:50%;" />

location代表当前页面URL信息

```bash
location.href
"https://www.baidu.com/"
location.protocol
"https:"
location.host
"www.baidu.com"
//刷新网页
location.reload()
//设置新的地址
location.assign("www.yyy.com")
```

document代表当前页面，html DOM树

```bash
document.title
"百度一下，你就知道"
document.title = "yyy"
"yyy"
```

document.getElementById("xxx")可以获取到代码段

![image-20210322205543663](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210322205543663.png)

可以获取cookie

```bash
document.cookie
"BIDUPSID=792154E585733A30C543C6D7FD92BC14; PSTM=1595435097; ......"
```

一些网页病毒原理就是这样，在JS代码中获取到COOKIE上传到他的服务器，一点击就会执行他的js文件

# 9、操作DOM对象

浏览器网页就是一个DOM树形结构

操作DOM类似于前端的增删改查

### 获取

用document.getElementByXxx()来获取DOM节点 可以用标签名、ID名、类名

### 修改

document.getElementById("id1");

id1.innerText='456' 修改id1文本的值

<img src="C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210322211652182.png" alt="image-20210322211652182" style="zoom:50%;" />

删除节点

通过父节点 删除子节点

<img src="C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210322211927153.png" alt="image-20210322211927153" style="zoom:50%;" />

# 10、jQuery

## 引入

可以官网下载jQuery文件，通过src引入或者直接引入文件

```html
<!--百度的CDN-->
<!--<script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>-->
<script src="lib/jquery-3.6.0.js"></script>
```

## 选择器

```html
<body>
 <a href="" id="test-jquery">点我</a>
<script>
    document.getElementById('id');
    //jQuery公式   $(selector).action()  选择器就是CSS的选择器
    $('#test-jquery').click(function () {
        alert('hello,jquery');
    })
</script>
```

正常获取id 标签需要用document.getElementById  通过jQuery可以$('#test-jquery').click

文档工具站 :http://jquery.cuishifeng.cn

## 事件

在div区域中移动鼠标，jQuery获取到移动鼠标事件，将鼠标坐标写到span标签上

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="lib/jquery-3.6.0.js"></script>
    <style>
        #divMove{
            width: 500px;
            height: 500px;
            border: 1px solid red;
        }
    </style>
</head>
<body>
mouse : <span id="mouseMove"></span>
<div id="divMove">
    在这里移动鼠标
</div>
<script>
    $(function(){
        $('#divMove').mousemove(function (e) {
            $('#mouseMove').text('x:'+e.pageX + 'y:'+e.pageY);
        })
    });
</script>
</body>
</html>
```

