# CSS布局的几种方法

---

#### 1. 浮动布局

```css
div{
    float:left/right/none;
}
```

> 原理：使当前元素脱离普通流，相当于浮动起来一样，浮动的框可以左右移动，直至它的外边缘遇到包含框或者另一个浮动框的边缘。

优点：兼容性好  
缺点：对附近的元素布局造成改变，使得布局混乱，因为浮动元素脱离了普通流，会出现一种高度坍塌的现象  
解决方法：

* 清除浮动，使用clear元素清除外面浮动，解决外面浮动对自己的影响。

* 使用overflow：hidden解决高度坍塌的现象。

* 使用伪元素：after。

```css
div:after{
    display:block;
    content:"";
    clear:both;
    visibility:hidden;
}
```

#### 2.定位

```css
div{
    position:static/relative/absolute/fixed;
}
```

> 原理：  
> static\(静态\)：没有特别的设定，遵循基本的定位规定，不能通过z-index进行层次分级，在普通流中，各个元素默认的属性。  
> relative\(相对定位\)：对象不可层叠、不脱离文档流，参考自身静态位置通过 top,bottom,left,right 定位。  
> absolute\(绝对定位\)：脱离文档流，通过 top,bottom,left,right 定位。选取其最近一个最有定位设置的父级对象进行绝对定位，如果对象的父级没有设置定位属性，absolute元素将以body坐标原点进行定位。  
> fixed（固定定位）：这里所固定的参照对像是可视窗口而并非是body或是父级元素。使用了fixed的元素不会随着窗口的滚动而滚动。属于absolute的子集。

优点：简单、兼容性好  
缺点：可用性较差，对附近的元素布局造成改变，使得布局混乱

#### 3.Flexbox 布局 / 弹性布局

```css
div{
    display: -webkit-flex;
    display:flex;    
}
```

缺点：IE8不支持

优点：解决上述两点的不足，较完美的布局方法

参考语法：[http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

参考实例：[http://www.ruanyifeng.com/blog/2015/07/flex-examples.html](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

#### 4.表格布局

```css
div{
    display:table;
}

div p{
    display:table-cell;
}
```

优点：水平、垂直剧中，页面自适应，兼容性好

缺点：高度不容易控制

#### 5.网格布局

```css
div{
    display:grid;
}
```

优点：代码简单，自适应好

缺点：目前浏览器支持差

详细参考：[http://www.jianshu.com/p/d183265a8dad](http://www.jianshu.com/p/d183265a8dad)

