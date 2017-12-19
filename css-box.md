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
window.getComputedStyle(dom).width/height 其他浏览器
dom.getBoundingClientRect().width/height (top,left,width,height)

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
### 延伸

##### IFC

IFC(Inline Formatting Contexts)直译为"内联格式化上下文"，IFC的line box（线框）高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响)

IFC中的line box一般左右都贴紧整个IFC，但是会因为float元素而扰乱。float元素会位于IFC与与line box之间，使得line box宽度缩短。 同个ifc下的多个line box高度会不同。 IFC中时不可能有块级元素的，当插入块级元素时（如p中插入div）会产生两个匿名块与div分隔开，即产生两个IFC，每个IFC对外表现为块级元素，与div垂直排列。

那么IFC一般有什么用呢？

水平居中：当一个块要在环境中水平居中时，设置其为inline-block则会在外层产生IFC，通过text-align则可以使其水平居中。

垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle，其他行内元素则可以在此父元素下垂直居中。

##### GFC

GFC(GridLayout Formatting Contexts)直译为"网格布局格式化上下文"，当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。

那么GFC有什么用呢，和table又有什么区别呢？首先同样是一个二维的表格，但GridLayout会有更加丰富的属性来控制行列，控制对齐以及更为精细的渲染语义和控制。

##### FFC

FFC(Flex Formatting Contexts)直译为"自适应格式化上下文"，display值为flex或者inline-flex的元素将会生成自适应容器（flex container），可惜这个牛逼的属性只有谷歌和火狐支持，不过在移动端也足够了，至少safari和chrome还是OK的，毕竟这俩在移动端才是王道。

Flex Box 由伸缩容器和伸缩项目组成。通过设置元素的 display 属性为 flex 或 inline-flex 可以得到一个伸缩容器。设置为 flex 的容器被渲染为一个块级元素，而设置为 inline-flex 的容器则渲染为一个行内元素。

伸缩容器中的每一个子元素都是一个伸缩项目。伸缩项目可以是任意数量的。伸缩容器外和伸缩项目内的一切元素都不受影响。简单地说，Flexbox 定义了伸缩容器内伸缩项目该如何布局。
