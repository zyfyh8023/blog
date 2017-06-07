# Scoped的简要介绍

## 什么是Scoped？
scoped属性是HTML5中的新属性，它允许我们通过style标签的方式，为文档的指定部分定义样式，而不是整个文档。如果使用style的"scoped"属性，可以让CSS样式只对局部元素生效，具体说，就是所规定的样式只能应用到style元素的父元素及其子元素。而且在scoped样式里可以使用任何合法的CSS样式规则。

## Scoped的一个例子
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

## Scoped的核心思想和所解决的问题是什么？

## Scoped的优点是什么？

## Scoped的缺点是什么？

## Scoped与CSS样式污染的关系是什么？
Scoped CSS规范是Web组件产生不污染其他组件，也不被其他组件污染的CSS规范。
