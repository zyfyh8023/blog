# SMACSS的简要介绍

## 什么是SMACSS？
SMACSS（Scalable and Modular Architecture for CS），可扩展和模块化的CSS。用一句话概括，SMACSS就是一种组织和管理CSS代码的规范。SMACSS从三个层面来规范CSS代码，即：CSS代码分类、CSS类的命名规范和最小化适配深度。其中CSS代码分类是SAMCSS最核心的部分，它提出了一种CSS的分类方法，其横向的把CSS切分为五种类型：基础（Base）、布局（Layout）、模块（Module）、状态（State）、主题（Theme）。最终使CSS代码结构化、模块化、可扩展和明确化。
* 基础（Base）， 基础规范样式，即在任何项目任意页面下，页面元素的默认外观。这里面的样式主要以元素标签本身为主，可能会用到属性选择器或伪类，但不会用到css类和ID选择器。最直观的理解就是，我们项目站点的css reset样式文件或css normalize文件，只要用于统一元素标签在各浏览器中的的默认样式预设值的差异性。
* 布局（Layout），布局一般指一个网站的结构布局和外观走向，是用来组织分布模块元件的大容器，而非某一个小元件或者功能模块。常见的网站的布局，如上（header）中（main）下（footer）布局，其中中间部分又分为左分栏（left Column）右分栏（Right Column）布局等，以及栅格系统（Grid System），响应式布局（Responsive Web Design）等都属于布局。
* 模块（Module），就是用于放置在布局（layout）中的一个个功能独立的可被复用的模块。具体说就是一个网站的菜单、产品列表、分页组件等。
* 状态（State）
* 主题（Theme）


## SMACSS的优点是什么？


## SMACSS的缺点是什么？


## SMACSS和CSS样式污染的关系是什么？
