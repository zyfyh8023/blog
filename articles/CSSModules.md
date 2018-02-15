# CSS Modules
  CSS Modules不是W3C的什么标准，他只是项目构建过程的一部分。通过编译你的项目，重新命名css的class和id名称，使它变得独一无二。使得css样式规则仅作用于某个组件或元素。样式被限制在这些局部范围内，不能被其他地方所使用，除非有特别需求和特别处理。
## CSS Modules的主要功能介绍
- 局部作用域：
  使用了CSS Modules后，就相当于给每个class名外加了一个:local，以此来实现样式的局部化。且默认情况这些类都是局部的唯一的，不需要添加:local。然后生成一个JSON文件来存储原始类和映射出来的类。
- 全局作用域：
  CSS Modules允许使用:global(.className)的语法，声明一个全局规则。凡是这样声明的class，都不会被编译成哈希字符串。
- 定制哈希类名
  CSS Modules默认的哈希算法是[hash:base64]，
- CSS Modules的组合
  在 CSS Modules 中，一个选择器可以通过composes继承另一个选择器的规则。
- 输入变量和其他模块
  CSS Modules支持使用变量，和继承其他CSS文件里面的样式规则。
## CSS Modules的例子
  比如，以下常见的样式规则
  ```css
  .title{
    font-size: 16px;
    height: 40px;
    line-height: 40px;
    color: rgba(0,0,0,.86);
  }
 .myinput{
    font-size:16px;
    border-radius:4px;
    border:1px solid #c8cccf;
    color:#6a6f77;
  }
  ```
  ```html
  <div class="title"></div>
  <input type="text" class="myinput"/>
  ```
  使用CSS Modules，这个样式类将被重新命名为如下所示：
  ```css
  .xkpkb{
    font-size: 16px;
    height: 40px;
    line-height: 40px;
    color: rgba(0,0,0,.86);
  }
  .We30p{
    font-size:16px;
    border-radius:4px;
    border:1px solid #c8cccf;
    color:#6a6f77;
  }
  ```
  编译后的类名映射关系JSON文件：
  ```javascript
  { 
    "title": "xkpkb",
    "myinput": "We30p" 
  }
  ```
  转换之后，你可以读取上面生成的JSON对象并使用它替换对应html中的类名
  ```html
  <div class="xkpkb"></div>
  <input type="text" class="We30p"/>
  ```
## CSS Modules的优缺点
### 优点
- 所有样式规则默认都是local的，解决了命名冲突和全局污染问题
- class 名生成规则配置灵活，可以生成更短的class名，来提高CSS的压缩率 
- 可以减少使用css样式规则的层叠和优先级的嵌套
### 缺点
- CSS Modules只会编译替换css文件中的类名，然后生成对应名称的映射json文件。html中真正使用的类名还需要人工自行替换，且比较繁琐。
## CSS Modules和CSS样式污染的关系总结
通过上面的简要分析，发现通过使用CSS Modules可以有效解决css样式污染的问题。
