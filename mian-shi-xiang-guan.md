## 面试

---

> #### [JS闭包](https://zhuanlan.zhihu.com/p/25311403)

闭包是指可以访问另一个函数作用域变量的函数，一般是定义在外层函数中的内层函数。局部变量无法共享和长久的保存，而全局变量可能造成变量污染，所以我们希望有一种机制既可以长久的保存变量又不会造成全局污染。

```js
function f1() {
   var n = 999;

   function f2() {
      return n = n + 1
   };

   return f2;  //return 是为了外部函数可以调用，与闭包无关。
}
var a = f1();
a(); // 1000
```

> #### [原型链](https://zhuanlan.zhihu.com/p/22189387)

每个对象都有一个指向它的原型（prototype）对象的内部链接。这个原型对象又有自己的原型，直到某个对象的原型为 null 为止（也就是不再有原型指向），组成这条链的最后一环。这种一级一级的链结构就称为**原型链（prototype chain）**。

**只有函数对象才有 prototype属性，prototype属性也叫原型对象,主要是为了实现继承和共享属性;**

**\_\_proto\_\_ 、prototype傻傻分不清楚？ 记住以下两点:**
1. __proto__是每个对象都有的一个属性，而prototype是函数才会有的属性。
2. __proto__指向的是当前对象的原型对象，而prototype指向的，是以当前函数作为构造函数构造出来的对象的原型对象。
prototype与__proto__的关系就是：你的__proto__来自你构造函数的prototype

**由function创造出来的函数对象：**

```js
function a(){};
var b=function(){};
```

**系统内置的函数对象：**

```js
Function,Object,Array,String,Number,
```

**除开函数对象之外的对象都是普通对象：**

```js
var b='qwe'; // b 是字符串类型,属于普通对象
var c=123;; // c 是数字类型,属于普通对象
```

* 每个函数都有一个原型属性prototype指向自身的原型

* 由这个函数创建的对象也有一个\_\_proto\_\_属性指向这个原型

* 函数的原型是一个对象，所以这个对象也会有一个\_\_proto\_\_指向自己的原型，这样逐层深入直到Object对象的原型，这样就形成了原型链。

* JS在创建对象（不论是普通对象还是函数对象）的时候，都有一个叫做\_\_proto\_\_的内置属性，用于指向创建它的函数对象的原型对象prototype。

* **普通对象的\_\_proto\_\_**

```js
var o = {name:"tsrot"};
console.log(o.__proto__); //Object{}
console.log(o.prototype); //undefined
console.log(o.__proto__ === Object.prototype);  //true
```

* **构造对象的\_\_proto\_\_**

```js
function Parent(){
    this.name = "i am parent";
}
Parent.prototype = {age:24};
function Child(){
    this.name = "i am child";
}
Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;
var child = new Child();
console.log(child.__proto__); //Object{}
console.log(Child.prototype); //Object{}
console.log(child.__proto__ === Child.prototype); //true
console.log(Parent.prototype.__proto__ === Object.prototype); //true
```

* **数组的\_\_proto\_\_**

```js
var arr = [1,2,3];
console.log(arr.__proto__);  //[Symbol(Symbol.unscopables): Object]
console.log(Array.prototype); //[Symbol(Symbol.unscopables): Object]
console.log(arr.__proto__ === Array.prototype); //true
```

* **函数的\_\_proto\_\_**

```js
var fun = function(){
    var hello = "i am function"
}
fun.prototype = {name:"tsrot"};
console.log(fun.prototype); //Object {name: "tsrot"}
console.log(fun.__proto__); //function(){}
console.log(fun.prototype === fun.__proto__); //false
console.log(fun.__proto__ === Function.prototype); //true
```

> #### [JS继承](https://zhuanlan.zhihu.com/p/32194154)

* #### 原型链继承
* #### 借用构造函数
* #### 组合式继承：前两种方式的结合
* #### 寄生组合式继承
* #### ES 6 继承

```js
class Parent {
    constructor(name) {
    this.name = name;
    }
    doSomething() {
    console.log('parent do something!');
    }
    sayName() {
    console.log('parent name:', this.name);
    }
}

class Child extends Parent {
    constructor(name, parentName) {
    super(parentName);
    this.name = name;
    }
    sayName() {
     console.log('child name:', this.name);
    }
}

const child = new Child('son', 'father');
child.sayName();            // child name: son
child.doSomething();        // parent do something!

const parent = new Parent('father');
parent.sayName();           // parent name: father
```

> #### [JS变量提升](https://zhuanlan.zhihu.com/p/23873265)

```js
console.log(c); // ERROR
console.log(a); // undefined
var a = 2;
console.log(a); // 2
```

如果我们没有在任何地方定义要输出的变量，那么就会报错，但是如果我们定义了这个变量，那么这个变量就会被提升到代码段的最上方进行声明，但是并不会赋值，所以才会出现先输出undefined的情况。

**变量会提升以外，函数也是会提升的，而且函数提升的优先级大于变量提升的优先级。**

```js
function f(a){
    console.log(a);// function
    var a = 2;
    console.log(a);//2
    function a(){};
    console.log(a);//2
}

f(1);

//实际代码执行顺序是这样的：
function f(a){
    var a = function(){};
    console.log(a);// function
    var a = 2;
    console.log(a);//2
    console.log(a);//2
}

f(1);
```

> #### [JS重载](https://zhuanlan.zhihu.com/p/29034069)

所谓函数重载，通俗点理解，可以认为一个函数名，可以出现多种参数，实现不同的功能，比如，加法运算，1个数的时候，直接显示，2个数的时候，求2个数的和,3个数的时候，求3个数的和。还有，在强类型\(编译阶段确定类型）语言中，重载的参数是区分类型的。在javascript中，默认是没有函数重载的，同名函数会产生覆盖，最后一个会把前面的函数覆盖。

> #### [JS深浅拷贝](https://zhuanlan.zhihu.com/p/26282765)

**基本数据类型**保存在**栈内存，**栈内存中分别存储着变量的标识符以及变量的值。

**引用类型**的复制：当你在复制引用类型的时候，实际上只是复制了指向堆内存的地址，即原来的变量与复制的新变量指向了同一个东西。

对于仅仅是复制了引用（地址），换句话说，复制了之后，原来的变量和新的变量指向同一个东西，彼此之间的操作会互相影响，为**浅拷贝**。

而如果是在堆中重新分配内存，拥有不同的地址，但是值是一样的，复制后的对象与原来的对象是完全隔离，互不影响，为**深拷贝**。

**深浅拷贝**的主要区别就是：复制的是引用\(地址\)还是复制的是实例。

> #### [Jquery与Zepto区别](https://www.zhihu.com/question/25379207)

* Zepto更轻量级
* Zepto是jQuery的精简，针对移动端去除了大量jQuery的兼容代码
* 部分API的实现方式不同
* 针对移动端程序，Zepto有一些基本的触摸事件可以用来做触摸屏交互（tap事件、swipe事件），Zepto是不支持IE浏览器的。
* DOM操作的区别：添加id时jQuery不会生效而Zepto会生效
* 事件触发的区别：使用jquery时load事件的处理函数不会执行；使用zepto时load事件的处理函数会执行
* 事件委托的区别：zepto中，选择器上所有的委托事件都依次放入到一个队列中，而在jquery中则委托成独立的多个事件
* width\(\) 与 height\(\)的区别：zepto由盒模型（box-sizing）决定，用.width\(\)返回赋值的width，用.css\('width'\)返回border等的结果；jquery会忽略盒模型，始终返回内容区域的宽/高（不包含padding、border）
* offset\(\)的区别：zepto返回{top,left,width,height}; jquery返回{width,height}。zepto无法获取隐藏元素宽高，jquery可以
* zepto中没有为原型定义extend方法而jquery有
* zepto的each方法只能遍历数组，不能遍历JSON对象。



