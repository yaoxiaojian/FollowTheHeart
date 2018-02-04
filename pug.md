# [Pug](https://pugjs.org/zh-cn/api/getting-started.html "https://pugjs.org/zh-cn/api/getting-started.html")


###### Pug 可以代替 Html 作为模版

### 安装

```
$ npm install pug
```
### 优势

* pug没有结束标签，代码更加简洁高效。

```
// html
<!DOCTYPE html>
<html>
<head>
</head>
</html>

// pug
doctype html
html
head
```

* 强制缩进原则，使得团队中所有人的风格都统一。

```
//html (忽略缩进，阅读困难)
<div class="a">
<div class="b">
<div class="c">
</div>
</div>
</div>

//pug (div可以省略)
.a
  .b
    .c
```

* 模板继承，可以不再一遍又一遍地写相同的代码。Pug 支持使用 block 和 extends 关键字进行模板的继承。一个称之为“块”（block）的代码块，可以被子模板覆盖、替换。这个过程是递归的。

```
// index.pug
html
  head
    title
    block scripts
        script(src='/jquery.js')
  body
    block content
    block foot
        #foot

// a.pug
extends index.pug //指出被继承的模板的路径

block content //覆盖父模板里对应的块，添加该页面的内容
    .a
      .b
        .c
```

### 示例

项目结构：

```
src/  // 网站源文件
    └─ pages/  // 页面文件夹（存放 Pug 模板）
      └─ layouts/  // 共享模板组件
         ├─ includes/
         |  ├─ nav.pug  // 页面的导航
         |  ├─ head.pug  // 页面的 head 里的标签
         |  └─ footer.pug  // 页面的底部导航
         ├─ templates/
         |  └─ page.pug  // 页面模版
         └─ index.pug  // 网站首页
```

> includes / head.pug

head.pug 里包含了各种的 `<meta name=name content=content>` 标签，使用 `Mixin` 方法，只需 `+meta` 就可方便重复使用一整个代码块。

```
mixin meta(name, content)
  meta(name=name content=content)

meta(charset="utf8")
title= ""
+meta("keywords", "")
+meta("description", "")
+meta("viewport", "user-scalable=no, width=device-width, initial-scale=1, maximum-scale=1")
+meta("msapplication-tap-highlight", "no")
+meta("apple-mobile-web-app-capable", "yes")
+meta("applicable-device","mobile")
link(rel="shortcut icon" href="favicon.ico" mce_href="favicon.ico" type="image/x-icon")
```

> .. / includes / nav.pug

nav.pug 是页面的公共导航部分。

```
nav.nav-global(role="navigation")
  .logo
      img(src="img/shared/logo.png", alt="logo")
  .nav-content
    ul
      li
        a(title="导航") 导航
      li
        ...
  .nav-menu
......
```

> .. / includes / footer.pug

footer.pug 是页面的公共的底部导航。

```
footer
.links
  .tel
    ...
  .copyright 
    ...
  .icp 
    ...
  .police
      ...
......
```

> .. / templates / page.pug

page.pug 相当于是一整个页面的父模板，通过 `include` 方法，分别把 `head.pug` `nav.pug` `footer.pug` 三个部分导入进来。有 `block` 的地方，相当于占位符，子模版可通过 `block` 让真正的内容覆盖掉父模板中对应的 `block` 的位置。

```
doctype html
html
  head
    include ../includes/head.pug
  body
    include ../includes/nav.pug
    .outer
      block content
    include ../includes/footer.pug
    block scripts
    block tracking
```

> index.pug

index.pug 是一个子模版，通过 `extends` 方法继承 `page.pug`，相当于把 `page.pug` 的内容复制到当前页面， 并通过 `block` 对应的把内容进行覆盖替换。

```
extends layouts/templates/page.pug
block content
    .kv
        ...
    .events
        ...
    .links
        ...
```



