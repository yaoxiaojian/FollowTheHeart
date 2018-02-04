## DOM事件

---

#### DOM事件的级别：

DOM0：element.onclick=function\(\){}

DOM2：element.addEventListener\('click',function\(\){},false\);

DOM3：element.addEventListener\('keyup',function\(\){}.false\);

#### DOM事件模型：

捕获和冒泡

#### DOM事件流：

![](/assets/dom01.png)

#### DOM事件捕获的流程：

window &gt; document &gt; html &gt; body &gt; ... &gt; 目标元素

#### Event对象的常见应用

* ##### Event.preventDefault\(\)

取消浏览器对当前事件的默认行为，比如点击链接后，浏览器跳转到指定页面，或者按一下空格键，页面向下滚动一段距离。该方法生效的前提是，事件对象的cancelable属性为true，如果为false，则调用该方法没有任何效果。

该方法不会阻止事件的进一步传播（stopPropagation方法可用于这个目的）。只要在事件的传播过程中（捕获阶段、目标阶段、冒泡阶段皆可），使用了preventDefault方法，该事件的默认方法就不会执行。

* ##### Event.stopPropagation\(\)

阻止事件在 DOM 中继续传播，防止再触发定义在别的节点上的监听函数，但是不包括在当前节点上新定义的事件监听函数

* ##### Event.stoplmmediatePropagation\(\)

阻止同一个事件的其他监听函数被调用。如果同一个节点对于同一个事件指定了多个监听函数，这些函数会根据添加的顺序依次调用。只要其中有一个监听函数调用了stopImmediatePropagation方法，其他的监听函数就不会再执行了。

* ##### Event.currentTarget

返回事件当前所在的节点，即正在执行的监听函数所绑定的那个节点。

* ##### Event.target

返回触发事件的那个节点，即事件最初发生的节点。如果监听函数不在该节点触发，那么它与currentTarget属性返回的值是不一样的。

#### 自定义事件：

##### Event\(\)

```js
// 新建事件实例
var event = new Event('build');

// 添加监听函数
elem.addEventListener('build', function (e) { ... }, false);

// 触发事件
elem.dispatchEvent(event);
```

##### CustomEvent\(\)

Event构造函数只能指定事件名，不能在事件上绑定数据。如果需要在触发事件的同时，传入指定的数据，需要使用CustomEvent构造函数生成自定义的事件对象。

```js
var event = new CustomEvent('build', { 'detail': 'hello' });
function eventHandler(e) {
  console.log(e.detail);
}
```

---

DOM详细资料：[http://javascript.ruanyifeng.com/dom/event.html](http://javascript.ruanyifeng.com/dom/event.html)

