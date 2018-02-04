## 渲染机制

---

#### DOCTYPE及作用：

DTD（docunment type definition,文档类型定义）是一系列的语法规则，用来定义XML或（X）HTML的文件类型。浏览器会使用它来判断文档类型，决定使用何种协议来解析，以及切换浏览器模式。

DOCTYPE是用来声明文档类型和DTD规范的，一个主要用途是文件的合法性验证。如果文件代码不合法，那么浏览器解析时便会出一些差错。

```html
// HTML5
<!DOTYPE html>

// HTML4.01 Strict,该DTD包含所有HTML元素和属性，但不包括展示性的弃用的元素（比如 font）
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/loose.dtd">

//HTML4.01 Transitional,该DTD包含所有HTML元素和属性，包括展示性的弃用的元素（比如 font）
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN""http://www.w3.org/TR/html4/loose.dtd">
```

#### 浏览器渲染过程：

![](/assets/xuanran.jpg)

#### 重排Reflow：

DOM结构中的各个元素都有自己的盒子（模型），这些都需要浏览器根据各种样式来计算并根据计算结果将元素放到他该出现的位置。

###### 触发Reflow：

* 增加、删除、修改DOM节点时，会导致Reflow 或 Repaint
* 移动DOM的位置，或者有动画效果
* 修改CSS样式
* Resize窗口的时候，或是滚动的时候
* 修改页面默认字体时

#### 重绘Repaint：

当各种盒子的位置、大小以及其他属性，例如颜色、字体大小等都确定下来后，浏览器于是便把这些元素都按照各自的特性绘制了一遍，于是页面的内容出现。

###### 触发Repaint：

* DOM改动
* CSS改动

#### 布局Layout：

![](/assets/xuanran01.jpg)

