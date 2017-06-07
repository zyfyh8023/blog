# Scoped的简要介绍

## 什么是Scoped？
scoped属性是HTML5中的新增属性，它允许我们通过style标签的方式，为文档的指定部分定义样式，而不是整个文档。使用style的"scoped"属性，可以让CSS样式只对局部元素生效，具体说，就是所规定的样式只能应用到style元素的父元素及其子元素。而且在scoped样式里可以使用任何合法的CSS样式规则。:scope是CSS4新增的伪类，目前主要用于匹配添加了scoped属性的style标签的父元素作用域。由于:scope还属于试验阶段，所以:scope暂时只能配合scoped属性一起使用。

## Scoped的一个例子
* 例：

```html
<div>
    <p>段落一（style标签父元素外的p）</p>
    <div>
        父元素中的普通文字
        <style scoped>
        p {
            color: blue;
        }
        :scope {
            background: #999;
            color: red;
        }
        </style>
        <style>
        p {
            color: green;
        }
        :scope {
            background: yellow;
            font-size: 50px;
        }
        </style>
        <p>段落一（style标签父元素内的p）</p>
    </div>
</div>
```
以上代码的效果如下所示：

![result](https://github.com/zyfyh8023/blog/raw/master/imgs/result.png)


scoped属性的兼容性如下所示：

![brower](https://github.com/zyfyh8023/blog/raw/master/imgs/brower.png)


由于scoped属性尚未被浏览器广泛支持，所以可以使用脚本的方式：jquery.scoped.js https://github.com/thingsinjars/jQuery-Scoped-CSS-plugin
这种方式可以使用一个方法$.scoped()检索页面中的<style scoped>标签，把其中的css代码限定在父标签范围内。

## Scoped的核心思想和所解决的问题是什么？
通过让style标签支持局部作用域的方式（CSS规范），来解决CSS样式污染的问题。

## Scoped的优点是什么？
* Scoped属性是css局部作用域的尝试，在极少情况下可以解决css局部作用域和样式污染的问题。
* jQuery插件的方式提供了解决css局部作用域的思路。

## Scoped的缺点是什么？
* Scoped属性的浏览兼容性非常差
* 只适用于style标签，并不适合外联css文件
* jQuery插件的方式，需要js去动态添加渲染

## Scoped与CSS样式污染的关系是什么？
通过上面的分析可知：Scoped只能在极少情况下解决CSS样式冲突的问题。
