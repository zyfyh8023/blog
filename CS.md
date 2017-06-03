# CS

## 引用CSS代码的方式？
* 外联（通过link标签的外联方式）
    * 外联的文件以.css结尾的
    * 外联的文件以.scss结尾的
* 内联（通过style标签的方式写在html文件中）
* 内嵌（标签上内嵌style的方式不会引起css样式冲突问题，不考虑）
* js代码中通过调用css接口或addClass接口的方式都是间接的内嵌或外联，不需单独考虑


## CSS样式污染解决方案依据：
* 基于scoped原理的CSS命名冲突解决法
* 源码 -> 中间编译 -> 最后编译，增加一个中间编译的过程


## 方案步骤：
* 提取所有html文件或模板文件中以内联方式引用的css内容，在当前目录下新建.scss的文件并放到其中，然后把对应的style标签替换成inline文件类型的标签；
    * 源代码
        ```css
        <div>
            <link rel="stylesheet" href="./component1.scss" />
            <h2>标题</h2>
            
            <style>
                p {color: blue;}
            </style>
            
            <div>
                <h1>标题</h1>
                <p>段落</p>
            </div>
        </div>
        ```
    * 编译后的代码
        ```html
        <div>
            <link rel="stylesheet" href="./component1.scss" />
            <h2>标题</h2>
            
            <link rel="import" href="./2m4k3jk3ir.scss?__inline" />
            
            <div>
                <h1>标题</h1>
                <p>段落</p>
            </div>
        </div>
        ```
* 统一将所有的.css文件转换成.scss文件，并生成对应的css2scss.json文件；
    * 生成的css2scss.json文件如下所示：
        ```javascript
        {
            "src/index.css": "src/index.scss",
            "src/components/component1.css": "src/components/component1.scss"
        }
        ```
* 统一处理所有的.scss文件，根据每个文件的内容生成对应的文件指纹编码，并作为最外层的css类名包裹里面的内容，同时产出对应的scss2md5.json文件；
    * 生成的scss2md5.json文件如下所示：
        ```javascript
        {
            "src/index.scss": "1k2hj3j4i5bq",
            "src/components/component1.scss": "2e9s8w7d8ssd",
            "src/components/2m4k3jk3ir.scss": "3dfi9dd0s3ki",
            "src/components/mycomponent.scss": "4s9ds7ew9tds"
        }
        ```
    * 处理前的index.scss文件如下所示：
        ```css
        h2{
            color: red;
            font-size: 14px;
        }
        ```
    * 处理之后的index.scss文件如下所示：
        ```css
        .1k2hj3j4i5bq{
            h2{
                color: red;
                font-size: 14px;
            }
        }
        ```
* 统一处理所有的html文件或模板文件，根据css2scss.json文件替换对应文件的新路径；
    * 处理前的某个html文件如下所示：
        ```html
        <div>
            <link rel="stylesheet" href="./index.css" />
            <link rel="stylesheet" href="./mycomponent.scss" />
            <h2>标题</h2>
            <div>
                <h1>标题</h1>
                <p>段落</p>
            </div>
        </div>
        ```
    * 处理之后的如下所示：
        ```html
        <div>
            <link rel="stylesheet" href="./index.scss" />
            <link rel="stylesheet" href="./mycomponent.scss" />
            <h2>标题</h2>
            <div>
                <h1>标题</h1>
                <p>段落</p>
            </div>
        </div>
        ```
* 统一处理所有的html文件或模板文件，把文件中所有引入的scss文件给最外层标签添加className，className的值就是scss2md5.json文件中对应文件的md5值。
    * 处理之前的某个html文件
        ```html
        <div>
            <link rel="stylesheet" href="./index.css" />
            <link rel="stylesheet" href="./mycomponent.scss" />
            <h2>标题</h2>
            <div>
                <h1>标题</h1>
                <p>段落</p>
            </div>
        </div>
        ```
    * 处理之后的如下所示：
        ```html
        <div class="1k2hj3j4i5bq 4s9ds7ew9tds">
            <link rel="stylesheet" href="./index.css" />
            <link rel="stylesheet" href="./mycomponent.scss" />
            <h2>标题</h2>
            <div>
                <h1>标题</h1>
                <p>段落</p>
            </div>
        </div>
        ```

## 方案涉及的主要技术：
* 常用的前端构建工具，如FIS，Gulp等
* 支持嵌套的css预编译语言，比如：SCSS，LESS等
* 支持inline的构建工具，比如：FIS，当然也可以自己开发插件来支持


## 该方案的优点：
* 可以解决CSS样式冲突的问题，前提是所有代码都使用该方案；
* 编译生成的最外层className名称为乱码，具有唯一性；
* 只对页面或模块最外层容器的className进行编译，不会影响标签类的语义性；
* 不需要手动命名很长的类名称，每个模块内部的类名称随意取，如.title,.name均可。


## 该方案的缺点：
* 编译后的代码，在原来的嵌套基础上又统一增加了一层；
* 独立项目完全可以解决CSS样式污染问题，多个交叉项目情况可以确保自己的代码不污染第三方，要保证不被第三方污染，要保证第三方也使用该方案。



