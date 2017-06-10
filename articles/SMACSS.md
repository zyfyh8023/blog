# SMACSS的简要介绍

## 什么是SMACSS？
SMACSS（Scalable and Modular Architecture for CS），可扩展和模块化的CSS。用一句话概括，SMACSS就是一种组织和管理CSS代码的规范。SMACSS主要从CSS代码分类、CSS类的命名规范和最小化适配深度三个层面来规范CSS代码，最终使CSS代码结构化、模块化、可扩展和明确化。

## CSS代码的分类：
CSS代码分类是SAMCSS最核心的部分，它提出了一种CSS的分类方法，其横向的把CSS切分为基础（Base）、布局（Layout）、模块（Module）、状态（State）、主题（Theme）五种类型。
* 基础（Base）， 基础规范样式，即在任何页面下，页面元素的默认外观样式，作为其他类别样式的基础。这里面的css样式代码主要以元素标签本身为主，可能会用到属性选择器或伪类，但不会用到css类和ID选择器。最直观的理解就是，我们项目站点的css reset样式文件代码或css normalize文件代码，只要用于统一元素标签在各浏览器中的的默认样式预设值的差异性。
* 布局（Layout），布局一般指一个网站的结构布局和外观走向，是用来组织分布排列模块元件的大容器，而非某一个小元件或者功能模块。常见的网站的布局，如上（header）中（main）下（footer）布局，其中中间部分又分为左分栏（left Column）右分栏（Right Column）布局等，以及栅格系统（Grid System），响应式布局（Responsive Web Design）等都属于布局。该类别中只包含这些与页面布局相关的CSS样式代码。
* 模块（Module），就是用于放置在布局（layout）中的一个个功能独立的可被复用的模块，具体来说一个网站的菜单、产品列表、分页组件等都是一个个的模块。该类别中只包含这些公共、独立、可复用的模块的CSS样式代码。
* 状态（State），该类别只包含对布局、模块和任何元素不同表现行为或状态修饰的样式代码。比如，在不同的屏幕尺寸下，布局的不同外观；消息提示框模块在成功和失败不同状态下的外观；以及元素的点击和非点击状态或显示与隐藏等。另外，状态样式一般和JavaScript代码一起结合使用的居多。
* 主题（Theme），主题规范描述了页面的主体外观，用来设置页面整体的视觉效果，可以说是一种皮肤。一般指border-color、background-image和font-family等。主题规范可以修改前面4个类别的样式，且应和前面4个类别分离开来，便于换肤。主题规范不要求使用单独的class命名，也就是说，主题规范里的css类基本都可以在上面4个类别中找到定义，这样做的好处就是后加载主题样式文件可以对前面4类的样式进行覆盖，进而切换皮肤。

## CSS类的命名规范：
按照前面5种的划分:
* 基础（Base），基础规范样式，一般就是css reset之类样式文件，直接引入即可。文件内容如下所示：
```css
* {}
input[type=text] {}
a {}
a:hover {}
```

* 布局（Layout）,用l-或layout-这样的前缀，如下所示：
```css
.l-header {}
.l-navigator {}
.l-container {}
.l-sidebar {}
.l-content {}
.l-footer {}
```

* 模块（Module），用模块本身的命名，如下所示：
```css
.product-list {}
.product-list-title {}
.product-list-image {}
.product-list-article {}
```

* 状态（State），用is-前缀，如下所示：
```css
.is-error {}
.is-success{}
.is-show{}
.is-hidden{}
.is-active{}
```

* 主题（Theme），主题规范一般不要求单独class，如果是单独的class用theme-前缀，如下所示：
```css
.theme-a-backgroun{}
.theme-a-shadow{}
```

## 最小化适配深度：
最小化适配深度，换句话说就是，尽量不要使用子选择器和后代选择器，减少css代码和html结构的耦合度。如下例子所示：
```html
<div class="l-header">
  <div class="product-title"></div>
</div>
```
```css
.l-header .product-title{}
.product-title{}
```
上面两端代码的区别是一个使用了子选择器，一个没有使用。由于第一个使用了子选择器，所以其与html结构就绑在了一起，如果html结构发生改变，该样式就不在起作用了。
当然，子选择器或后代选择器是有用的，它可以减少因相同命名引发的样式冲突。但是不应过度使用，在不造成样式冲突的允许范围内，应尽量不要使用。这也是SMACSS的最小化适配深度的意义所在。

## SMACSS的优点是什么？


## SMACSS的缺点是什么？


## SMACSS和CSS样式污染的关系是什么？
