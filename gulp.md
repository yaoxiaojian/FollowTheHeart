## [GULP](http://www.gulpjs.com.cn/)

###### Gulp 让简单的任务简单，复杂的任务可管理。

### 安装

```
// 全局安装
$ npm install --global gulp
```

### 为什么用
* 最直观的好处就是让我们的工作更有效率。
* Gulp 侧重‘代码优先’的，做同一件事情，代码更为简洁。
* Gulp 基于node streams（流）来构建任务，避免磁盘反复读取/写入。每个任务都是单独执行，这使得它速度更快、更为纯粹。
* 丰富的插件，只需执行一行Gulp命令，就可以执行`语法检查、文件合并、文件压缩、文件监听` 等等功能。

### Gulp 一般的工作流程

读取文件 -&gt; 代码检查 -&gt; 文件合并 -&gt; 文件压缩 -&gt; 输出

### API

> Gulp 提供四个常用的 API，`gulp.task、gulp.src、gulp.dest、gulp.watch`，基本贯穿整个项目。

#### gulp.task

> Gulp 是基于task的方式来运行。
gulp.task(name[, deps], fn)
**name**：任务的名字，如果你需要在命令行中运行你的某些任务，那么，请不要在名字中使用空格。
**deps**：一个包含任务列表的数组，这些任务会在你当前任务运行之前完成。
**fn**：该函数定义任务所要执行的一些操作。通常来说，它会是这种形式：`gulp.src().pipe(someplugin())`。

#### gulp.src

> 输出（Emits）符合所提供的匹配模式（glob）或者匹配模式的数组（array of globs）的文件。
gulp.src(globs[, options])
**globs**:所要读取的 glob 或者包含 globs 的数组。
**options**:对读取的文件进行控制。

#### gulp.dest

> 能被 pipe 进来，并且将会写文件。并且重新输出（emits）所有数据，因此你可以将它 pipe 到多个文件夹。如果某文件夹不存在，将会自动创建它。 
gulp.dest(path[, options])
**path**:文件将被写入的路径（输出目录）。
**options**:对输出的目录进行控制。

#### gulp.watch

> gulp.watch(glob [, opts], tasks) 或 gulp.watch(glob [, opts, cb])
监视文件，并且可以在文件发生改动时候做一些事情。它总会返回一个 EventEmitter 来发射（emit） `change` 事件。
**glob**:一个 glob 字符串，或者一个包含多个 glob 字符串的数组，用来指定具体监控哪些文件的变动。
**opts**:传给 `gaze` 的参数。
**tasks**:需要在文件变动后执行的一个或者多个通过 `gulp.task()` 创建的 task 的名字。



### 示例
```
├─ gulp/
│  ├─ build.js
│  ├─ style.js
│  ├─ script.js
│  └─ template.js
└─ src/
   ├─ api/
   ├─ fonts/
   ├─ img/
   ├─ js/
   ├─ pages/
   │  └─ layouts/
   │     ├─ includes/
   │     └─ templates/
   └─ styles/
└─ gulpfile.js
```



首先要创建一个gulpfile.js文件，gulp默认是调用这个文件，并定义好内容，通常情况下是这样的：

```
// gulpfile.js

'use strict';

var fs = require('fs');
var gulp = require('gulp');

/**
 *  This will load all js or coffee files in the gulp directory
 *  in order to load all gulp tasks
 *  一个项目会有很多 `gulp.task()`，为了方便管理，把不同的task命令写进不同的js文件。并读取 `gulp/` 下的文件。  
 */
fs.readdirSync('./gulp').filter(function(file) {
  return (/\.(js|coffee)$/i).test(file);
}).map(function(file) {
  require('./gulp/' + file);
});


/**
 *  Default task clean temporaries directories and launch the
 *  main optimization build task
 *  下面写法，默认情况下，执行 `gulp` 或者 `gulp.build` 是一样的。
 */
gulp.task('default', ['build']);

```

##### build.js

```
// build.js

'use strict';

// 执行 gulp.build 时会先执行 gulp.inject、gulp.images
gulp.task('images', function() { 
  return gulp.src('src/img/**/*')
    .pipe(cache(imagemin({ optimizationLevel: 3, progressive: true, interlaced: true })))
    .pipe(gulp.dest('dist/images'))
    .pipe(notify({ message: 'Images task complete' }));
});
gulp.task('build', ['inject', 'images']);

```

##### inject.js

```
'use strict';

// 执行 gulp.html 时会先执行 gulp.scripts、gulp.styles、gulp.templates
gulp.task('inject', ['scripts', 'styles', 'templates'], function () {
  var injectStyles = gulp.src([
    path.join('.tmp/serve/styles/*.css'),
    path.join('!', '.tmp/serve/styles/global.css')
  ], { read: false });

  var injectScripts = gulp.src([
    path.join('src/scripts/*.js')
  ], { read: false });

  var injectOptions = {
    ignorePath: ['src', path.join('.tmp/serve')],
    addRootSlash: false,
    relative: true
  };

  return gulp.src(path.join('.tmp/serve/index.html'))
    .pipe($.inject(injectStyles, injectOptions))
    .pipe($.inject(injectScripts, _.extend(injectOptions, {
      transform: function(filePath, file, i, length) {
        if (path.extname(filePath) == '.js') {
          filePath = filePath.replace("../../src/", "");
          return '<script src="' + filePath + '"></script>';
        } else {
          return '<link rel="stylesheet" href="' + filePath + '">';
        }
      }
    })))
    .pipe(wiredep(_.extend({}, conf.wiredep)))
    .pipe(gulp.dest(path.join('.tmp/serve')));
});

```


##### scripts.js
```
'use strict';

gulp.task('scripts', function() { 
  return gulp.src('src/js/*.js')
    .pipe(jshint('.jshintrc'))
    .pipe(jshint.reporter('default'))
    .pipe(concat('main.js'))
    .pipe(gulp.dest('dist/scripts'))
    .pipe(rename({ suffix: '.min' }))
    .pipe(uglify())
    .pipe(gulp.dest('dist/scripts'))
    .pipe(notify({ message: 'Scripts task complete' }));
});
```

##### styles.js
```
'use strict';

gulp.task('styles', function() { 
  return gulp.src('src/styles/*.scss')
    .pipe(sass({ style: 'expanded', }))
    .pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))
    .pipe(gulp.dest('dist/styles'))
    .pipe(rename({ suffix: '.min' }))
    .pipe(minifycss())
    .pipe(gulp.dest('dist/styles'))
    .pipe(notify({ message: 'Styles task complete' }));
});
```

##### templates.js
```
gulp.task('templates', function() {
  return buildTemplates();
});

var buildTemplates = function() {
 return gulp.src([
      path.join('src/pages/index.html')
    ])
    .pipe(gulp.dest(path.join('.tmp/serve/')));
};
```

##### watch.js
```
'use strict';

gulp.task('watch', ['inject'], function () {
  gulp.watch([path.join('src/pages/*.html'), 'bower.json'], ['inject-reload']);
  gulp.watch([
    path.join('src/styles/*.css'),
    path.join('src/styles/*.scss')
  ], function(event) {
    if(isOnlyChange(event)) {
      gulp.start('styles-reload');
    } else {
      gulp.start('inject-reload');
    }
  });

  gulp.watch(path.join('src/scripts/*.js'), function(event) {
    if(isOnlyChange(event)) {
      gulp.start('scripts-reload');
    } else {
      gulp.start('inject-reload');
    }
  });

  gulp.watch(path.join('src/pages/*.html'), function(event) {
    gulp.start('inject-reload');
  });
});

```

### 常用插件
* gulp-less：将less编译成css文件
* gulp-load-plugins：在你的package.json文件中自动加载任意的gulp插件
* gulp-ruby-sass：sass的编译
* gulp-autoprefixer：自动添加css前缀
* gulp-minify-css：压缩css
* gulp-jshint：js代码校验
* gulp-concat：合并js文件
* gulp-uglify：压缩js代码
* gulp-imagemin：压缩图片
* gulp-livereload：自动刷新页面 
* gulp-cache：图片缓存，只有图片替换了才压缩
* gulp-notify：更改提醒

更详细的Gulp说明：[https://github.com/Platform-CUF/use-gulp](https://github.com/Platform-CUF/use-gulp)
