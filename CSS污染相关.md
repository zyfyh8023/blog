CSS没有局部作用域的概念，所有的样式规则都是全局作用域的，任何一个样式规则，都会对整个页面有效。因此，我们定义的每一个类样式都可能在特定的环境下与其他的元素相互冲突，引发样式间的污染，尤其是在大的项目中，最终在页面上产生意料之外的效果。虽然CSS是前端领域中进化较慢的领域，但在于CSS样式污染的战斗中，我们从未有停歇过。。。


## 目前主要包括以下几种方案：
* 通过对CSS类名进行规范约定的方式，主要包括：BEM、OOCSS和SMACSS等。
  * BEM（Block Element Modifier）,BEM具体使用介绍和优缺点分析详见：[BEM](http://www.baidu.com)
  * OOCSS（Object Oriented CSS）,OOCSS的具体使用介绍和优缺点分析详见：[OOCSS](http://www.baidu.com)
  * SMACSS（Scalable and Modular Architecture for CSS），BEM具体使用介绍和优缺点分析详见：[SMACSS](http://www.baidu.com)
* 通过对CSS类名进行编译的方式，主要包括CSS Modules和PostCSS等。
  * CSS Modules，CSS Modules具体使用介绍和优缺点分析详见：[CSS Modules](http://www.baidu.com)
  * PostCSS，PostCSS具体使用介绍和优缺点分析详见：[PostCSS](http://www.baidu.com)
* 通过对CSS代码原子拆分的方式，如ACSS。
  * ACSS，ACSS具体使用介绍和优缺点分析详见：[ACSS](http://www.baidu.com)
* 通过CSS in JSDE方式，主要包括polished.js等。
  * polished，polished具体使用介绍和优缺点分析详见：[polished](http://www.baidu.com)
* 通过style的局部作用域的方式，如scoped。
  * scoped，scoped具体使用介绍和优缺点分析详见：[scoped](http://www.baidu.com)


## 个人改进方案：
* 基于scoped原理的CSS样式冲突解决法
* 源码 -> 中间编译 -> 最后编译，增加一个中间编译的过程
* 具体操作步骤详见：[CS](https://github.com/zyfyh8023/blog/blob/master/CS.md)


