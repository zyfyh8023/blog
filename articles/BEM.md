# BEM的简要介绍

## 什么是BEM?
BEM是由Yandex团队提出的一种CSS类的命名方法规范。BEM所约定的CSS类命名规范较严格，这种命名方法不仅在一定程度上可以解决CSS样式污染的问题，而且有助于帮助开发者实现模块化，高维护性和结构化的css代码。

BEM（Block Element Modifier），BEM定义的css class命名规范，每个名称由块（Block）、元素（Element）和修饰符（Modifier）这三个模块组合而成，当然并非一定全部包含这三个模块。每个类名称的每个组成部分都有着不同的意义。一般情况，块、元素和修饰符的名称都由拉丁字母、数字和\-（中划线）组成。
* 块（Block），块即Web开发中我们常说的组件或模块，作为CSS类名称的命名空间。块在逻辑和功能上都是相互独立的，每个块中封装了模块相关的JavaScript、CSS和HTML模板，是一个独立的实体。由于块是相互独立的，所以块可以在开发被多次复用，从而降低代码的重复和提高项目的开发效率。块可以被放置在页面的任意位置，块之间也可以任意嵌套，同一页面中可以包含任意多的块，甚至是相同块的不同实例。
* 元素（Element），元素是相对于块来说的，是块的组成部分，元素的CSS类名都会包含块的名称作为前缀，块内部的元素是兄弟的关系，BEM不推荐元素之间的嵌套使用。元素和块之间通过\_\_（两个下划线）连接。
* 修饰符（Modifier），修饰符是用来修饰块或元素的外观、行为和状态的。同样的块或元素在不同的应用场景下经过不同的修饰符之后，会有不同的表现。修饰符
  和块或元素之间通过\-\-（两个中划线）连接。

## BEM的一个小例子
通过上面的介绍，我们了解了BEM的命名规范，下面通过下面的这个小例子来看看BEM到底是如何使用的：
* 例：
```html
<div class="dialog-component">
    <div class="dialog-component__header">
        <div class="dialog-component__close"></div>
        <h2 class="dialog-component__title">登录</h2>
    </div>
    <div class="dialog-component__body">
        <div class="dialog-component__ipt">
            <input type="text" class="dialog-component__id-ipt"/>
            <input type="password" class="dialog-component__pwd-ipt"/>
        </div>
        <div class="dialog-component__tip dialog-component__tip--error">
            用户名或密码输入有误！
        </div>
        <div class="dialog-component__btn dialog-component__btn--reset">重置</div>
        <div class="dialog-component__btn dialog-component__btn--submit">提交</div>
    </div>
</div>
```
其中，dialog-component代表分页模块；dialog-component__header、dialog-component__close、dialog-component__title、dialog-component__body、dialog-component__tip和dialog-component__btn等为dialog-component模块的子孙元素，用于形成一个完整的dialog-component组件模块；dialog-component__tip--error代表元素dialog-component__tip的错误提醒状态。之所以使用/_/_连接块和元素，使用/-/-连接元素和修饰符，是为了能够让我们使用-和_命名块、元素和修饰符的名称。当然，具体使用什么符号连接块、元素和修饰符，可以根据自己的需求情况而定，无论使用什么样的符号连接，它们其实都是基于同样的BEM原则。

另外，由上面的例子可知，dialog-component模块内部有多个元素，而且这些元素之间还存在父子关系，如：dialog-component__body元素和dialog-component__ipt，这里很容易被误写为下面的样子，BEM命名规范规定css class名称的一般组成为block，block--modifier，block--modifier__element，block--modifier__element--modifier，block__element，block__element--modifier。BEM不允许dialog-component__body元素和dialog-component__body__ipt元素之间的这种嵌套命名方式。可以另起一个元素的名字如dialog-component__body和dialog-component__ipt，也可以dialog-component__body和dialog-component__ipt-body等多种方式。
```html
<!-- ... -->
<div class="dialog-component__body">
     <div class="dialog-component__body__ipt">
         <input type="text" class="dialog-component__id-ipt"/>
         <input type="password" class="dialog-component__pwd-ipt"/>
     </div>
 <!-- ... -->
 </div>
<!-- ... -->
```
当然，BEM也不允许块中的元素或元素内部的子元素不采用BEM的命名方式（如下所示）,我们不仅要在开发组件模块的时候使用BEM，在页面的开发中也要使用BEM，不然乱起的一个名字很可能就和某一组件冲突了，导致样式相互覆盖。只有都按照BEM的规范来开发，这样才能够达到更好的效果。
```html
<!-- ... -->
<div class="dialog-component__ipt">
    <input type="text" class="id-ipt"/>
    <input type="password" class="pwd-ipt"/>
</div>
<!-- ... -->
```
像上面的这种写法（在内部元素不使用BEM的命名规范），很容易在我们写对应样式的时候（如下所示），和页面其他模块的样式之间引起冲突污染。比如，其他的一个模块叫id-ipt,或者其他组件模块内部也有一个id-ipt。避免使用级联选择器(如下所示)，HTML元素同样也不要用作CSS选择器（如.dialog-component__ipt input)，因为这样的选择器并非是完全上下文无关的。另外，块内部也最好不要使用ID选择器，因为块的独立性，可以在同一页面出现任意多次。

```css
<style>
.id-ipt{
    height:30px;
}
.pwd-ipt{
    height:40px;
}
.dialog-component__ipt .id-ipt{
    width:200px;
}
.dialog-component__ipt .pwd-ipt{
    width:300px;
}
</style>
```
在样式书写中，BEM不推荐使用CSS子选择器和后代选择器的方式，推荐直接通过元素的样式类进行开发的方式，这样有利于样式的维护和管理，在更新优化样式时，不需要关注上下文结构，直接修改覆盖对应块的对应元素的样式类即可。

## 为什么推崇BEM？以及BEM的核心思想和所解决的问题是什么？
CSS没有局部作用的概念，所有的样式规则都是全局效果的，以往我们在给元素起类名时，都会根据元素的用途等，给元素起一个自认为不会重名的类，来避免样式间的污染。很明显这是不可靠的，尤其在大型单页面应用中。
BEM解决这一问题的依据是块名的唯一性，只要块名唯一，元素的样式就不会引用污染，当然，这里有个大前提，就是所有代码都按照BEM的规范开发。BEM解决块名唯一的依据是操作系统中，同一目录下不可能有相同的文件夹或文件名。由于每个块的唯一，进而每个元素的类名也唯一，因此在开发样式时都只使用一个类别选择器即可，可以避免传统做法中由于多个类别选择器嵌套带来的复杂的属性级联问题。

## BEM的优点是什么？
* 在一定程度上解决了CSS样式污染的问题；
* 避免了多个子后代选择器的复杂嵌套；
* 通过模块化的方式，开发一套可复用易维护和结构化的代码；
* 由BEM的命名规范可知，代码的结构更具有语义性，更明确，易阅读和理解。

## BEM的缺点是什么？
* 并没有完全解决CSS样式污染的问题；
* 手动添加过长的类名；
* 适合新项目使用。

## BEM和CSS样式污染问题的关系是什么？
通过上面的分析可知，BEM并没有完全解决CSS样式污染的问题。它必须在一定的前提下才可以：
* 块哦名称一定要保证唯一；
* 所有的代码都遵循BEM的命名规范。



