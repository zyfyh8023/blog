# OOCSS的简要介绍


## 什么是OOCSS？
OOCSS（Object Oriented CSS），即面向对象的CSS。OOCSS不是什么新技术，更不是CSS的新框架，它只是CSS的一种新写法，一种设计模式。即用面向对象的思想去定义样式，抽离出CSS的公共代码，提高CSS 类的重复使用率，减少对HTML结构的依赖等。


## OOCSS的核心思想和所要解决的问题是什么？
OOCSS的核心思想主要包括：
* 容器与内容的分离；
* 样式与结构的分离。

OOCSS旨在通过以上两个主要思想，编写高可复用、低耦合的CSS代码，使得最终的样式灵活性高、扩展性好，更快地更有效地添加和维护。


## OOCSS的两个小例子：
* 例一，样式和结构的分离：
在同一个页面或不同页面的不同位置，可能会使用到两种button，取消button和确认button，一般我们会分别直接写出两种button的结构样式，如下所示：
```css
<style>
.btn-cancle{
    display:inline-block;
    padding: 5px 10px;
    font-size: 15px;
    color:#aaa;
    background: #eee;
}
.btn-confirm{
    display:inline-block;
    padding: 5px 10px;
    font-size: 15px;
    color: #fff;
    background: blue;
}
</style>
```

OOCSS结构和样式分离的思想，换句话说就是分离描述布局结构的css代码和描述皮肤样式的css代码。用这个例子来描述就是，可能在不同位置我们需要的button的样式不一样，但是button的结构都基本一样。于是，我们就把描述结构的css代码和描述样式的css代码分离开来，写在不同的两个类里面，这样我们描述结构的css类就可以被多次的复用（在需要button的位置），当然我们描述样式的类也可被复用，在不满足被复用的情况下，我们可以更好的进行扩展新的样式类，类似于bootstrap，amazeUI等前端UI库一样。用OOCSS结构与样式分离思想的写法如下所示：

```css

<style>
.btn{
    display:inline-block;
    padding: 5px 10px;
    font-size: 15px;
}
.btn-cancle{
    color:#aaa;
    background: #eee;
}
.btn-confirm{
    color: #fff;
    background: blue;
}
</style>
```

上面的这个例子虽然很简单，但是却透出了OOCSS结构和样式分离的精髓，分离常用UI的样式css代码
和结构css代码，提高复用和可扩展灵活性。这种分离在一定程度上可以减少CSS代码的重复，当然这种分离还不彻底，比如常用的描述结构布局的css属性有：margin/padding/width/height/text-align/display/position/float等，常用的描述样式的css属性有：color/font/background/shadow等，因为并没有十分明确的分离界限，这种分离方法还有可能出现css代码的重复或覆盖。比如上面button的分离就把font-size分离到了.btn类里面。更彻底的分离请看基于原子拆分的ACSS。

* 例二：容器和内容的分离：
承接第一个例子，left-content和right-content两个div里面都有一个confirm button，但是需求要求，right-content里面的button字体大小和常用的不同，这时我们一般会通过如下的方式来解决：

```css
<style>
.btn{
    display:inline-block;
    padding:5px 10px;
    font-size:15px;
}
.btn-cancle{
    color: #fff;
    background: blue;
}
.btn-confirm{
    color: #fff;
    background: blue;
}
.right-content a{
    font-size:18px;
}
</style>
```
```html
<div class="left-content"> 
    <a class="btn btn-confirm"></a>
</div>
<div class="right-content">
    <a class="btn btn-confirm"></a>
</div>
```

OOCSS分离容器和内容的思想，换句话说就是尽量避免使用子选择器和后代选择器，避免样式代码过多的依赖布局结构和上下文。用这个例子描述，就是通过直接扩展对应元素类的形式来解决差异，不应该通过父容器+（子/后代）选择器的方式。因为，如果后面还有类似用到18px字体的button的情况时，我们可以直接使用btn-large-18，而不用在通过父容器的方式添加样式。另外，如果父容器的结构类改变时，我们也不用担心是否修改样式的嵌套关系。

```css
<style>
.btn{
    display:inline-block;
    padding:5px 10px;
    font-size:15px;
}
.btn-cancle{
    color: #fff;
    background: blue;
}
.btn-confirm{
    color: #fff;
    background: blue;
}
.btn-large-18{
    font-size:18px;
}
</style>
```
```html
<div class="left-content"> 
    <a class="btn btn-confirm btn-small"></a>
</div>
<div class="right-content">
    <a class="btn btn-confirm btn-large-18"></a>
</div>
```

## OOCSS的优点
* 在一定程度上，减少css代码的重复，进而减少css代码的量；
* css代码灵活性高、扩展性强，语义更明确，更便于修改与维护。


## OOCSS的缺点
* 结构和样式的分离思想，并没有明显的分离界限和规范，很难去把握，而且过多的分离，容易导致代码换乱，不清楚每个类的使用场景和情况；
* 容器和内容的分离思想，在直接引用模块化模板代码，而非复制代码的时候，不通过父容器的方式修改样式不易实现。
* 在实际开发中没必要严格追求OOCSS，因为有可能会矫枉过正，可以把OOCSS的核心思想作为每次开发前的思考和习惯，在适当的地方使用即可，可以是项目站点级，页面级甚至是模块级的使用。


## OOCSS和CSS样式污染的关系是什么？
OOCSS的思想并未涉及解决CSS样式污染的问题。



