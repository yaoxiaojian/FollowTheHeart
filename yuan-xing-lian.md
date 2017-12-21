## 原型链

---

#### 创建对象的几种方法：

###### 字面量：

```js
var o1 = {name:'o1'};
var o2 = new Object({name:'o2'});
```

###### 通过函数构造：

```js
var a = function(name){this.name = name};
var o3 = new a();
```

Object.create\(\)：

```js
var b = {name:'b'};
var o4 = Object.create(b);
```

#### 原型、实例、构造函数、原型链：

![](/assets/yuanxinglian.jpg)



###### 原型对象：

在JavaScript中，我们创建一个函数A\(就是声明一个函数\), 那么浏览器就会在内存中创建一个对象B，而且每个函数都默认会有一个属性prototype指向了这个对象\( 即：prototype的属性的值是这个对象\)。这个对象B就是函数A的原型对象，简称函数的原型。这个原型对象B 默认会有一个属性constructor指向了这个函数A \( 意思就是说：constructor属性的值是函数A \)。

###### 详细资料：[http://blog.csdn.net/u012468376/article/details/53121081](http://blog.csdn.net/u012468376/article/details/53121081)

###### 

#### instanceof原理：

![](/assets/yuanxinglian2.jpg)

能在实例的原型对象链中找到该构造函数的prototype属性所指向的原型对象，就返回true。

#### new运算符：

一个新对象被创建，他继承自fun.prototype。构造函数 fun 被执行，执行的时候，相应的传参会被传入，同时上下文（this）会被指定为这个新实例。new fun 等同于 new fun\(\)，只能用在不传递任何参数的情况。

如果构造函数返回了一个对象，那么这个对象会取代整个new出来的结果，如果构造函数没有返回对象，那么new出来的结果为步骤1创建的对象。

```js
var new2 = function(func){
    var o = Object.create(function.prototype);
    var k = func.call(o);
    if(typeof k === 'object'){
        return k
    }else{
        return o
    }
}
```



