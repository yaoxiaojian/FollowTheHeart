## CSS盒模型

---

#### 概念

标准模型：宽高 = content 宽高  
![](/assets/图片1.png)  
IE模型：宽高 = content 宽高 + padding + border   
![](/assets/图片2.png)

#### CSS如何设置这两种模型

box-sizing:content-box;（默认，标准模型）  
box-sizing:border-box;（IE模型）

#### JS如何设置获取盒模型对应的宽和高

dom.style.width/height 只能获取内联样式  
dom.currentStyle.width/height 只有IE有效  
window.getComputedStyle\(dom\).width/height 其他浏览器  
dom.getBoundingClientRect\(\).width/height \(top,left,width,height\)

#### 根据盒模型解释边距重叠

边距重叠是一个相当简单的概念。在实践中对网页进行布局时，它会造成许多混淆。简单地说，当两个垂直边界相遇时，它们将形成一个边界。这个边界的高度等于两个发生叠加的边界的高度中的较大者。

#### 边距重叠解决方案

BFC：块级格式化上下文  
即使用：overflow:hidden/auto;

#### BFC作用

1.解决垂直方向边距重叠  
2.独立的容器，互不影响  
3.浮动元素参与计算

#### 如何创建BFC

1.float 属性不为 none  
2.position 不为 static 或 relative  
3.display 为 inline-block、table-cell、table-caption  
4.overflow 不为 visible

#### 应用场景

1.垂直方向边距重叠  
2.清除内部浮动，使浮动元素参与高度计算  
3.不与浮动元素重叠

---

#### 参考资料：

BFC详解：[http://www.html-js.com/article/1866](http://www.html-js.com/article/1866)

盒模型详解：[https://github.com/chokcoco/iCSS/issues/5](https://github.com/chokcoco/iCSS/issues/5)

