# PostCSS
PostCSS是当前比较流行的一个对CSS进行处理的工具。PostCSS本身的功能比较单一，它提供了一种用JavaScript代码来处理CSS的方式。它负责把CSS代码解析成抽象语法树结构,再交由插件来进行处理。插件基于CSS代码的AST进行多种多样的操作，因此，PostCSS依托其强大的插件体系，为CSS处理增加了无穷的可能性。
## PostCSS的功能简介
PostCSS的主要功能有两个：
- 把CSS解析成AST；
- 调用插件来处理AST并得到结果。

PostCSS一般不单独使用，而是与已有的构建工具进行集成。PostCSS与主流的构建工具，如Webpack、Grunt和Gulp都可以进行集成。完成集成之后，选择满足功能需求的PostCSS插件并进行配置即可。比如，我们比较熟悉的插件Autoprefixer，cssnext和CSS modules等。
  
通过上面对CSS Moduels的缺点分析可知，由于在HTML代码中引用的CSS类名和最终生成的类名并不相同，因此需要一个中间的过程来进行类名的转换。对于React来说，可以使用react-css-modules插件；在其他情况下，可以使用PostHTML对HTML进行处理。postcss-modules插件把CSS模块中的CSS类名的对应关系保存在一个 JavaScript对象中，可以被PostHTML中的posthtml-css-modules插件来使用。
  
在使用postcss-modules插件时提供了一个方法getJSON。当CSS模块的转换完成时，该方法会被调用。该方法的参数json参数表示的是转换结果的JavaScript 对象。该对象被以JavaScript文件的形式保存到cssModules目录下，并添加了模块导出的逻辑，如下代码所示：
  
```javascript
 //保存CSS模块的输出文件
 require('postcss-modules')({
 	getJSON: function(cssFileName, json) {
  	var cssName = path.basename(cssFileName, '.css');
  	var jsonFileName = path.resolve(dist, 'cssModules', cssName + '.js');
  	mkdirp.sync(path.dirname(jsonFileName));
  	fs.writeFileSync(jsonFileName, "module.exports = " + JSON.stringify(json) + ";");
	}
})
```
  
```javascript
//使用PostHTML处理HTML里支持CSS模块
gulp.task('posthtml', function() {
	var posthtml = require('gulp-posthtml');
	return gulp.src('app/**/*.html')
	.pipe(posthtml([ require('posthtml-css-modules')(path.join(dist, 'cssModules')) ]))
 	.pipe(gulp.dest('dist/'));
});
```
  
如上代码所示，使用Gulp的gulp-posthtml来处理HTML文件的任务。posthtml-css-modules可以处理一个目录下的多个 CSS 模块输出文件。
在HTML文件中使用“css-module”属性来指定对应的CSS类名。如下代码所示，名称“header.content”的header表示的是CSS文件名，而content是该文件中定义的CSS类名。
  
```html
使用 CSS 模块的 HTML 文件
<div css-module="header.content">Hello world</div>
```

在经过处理之后，得到的HTML内容如下所示：
```
转换之后的 HTML 文件
<div class="_content_6xmce_5">Hello world</div>
```
