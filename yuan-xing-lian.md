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

## 面向对象

---

#### 类与实例：

###### 类的声明：

```js
function animal(){
    this.name = 'name';
}

//ES6 中 class 声明
class animal2(){
    constructor(){
        this.name = name;
    }
}
```

###### 生成实例：

```js
console.log(new animal() , new animal2());
```

#### 类与继承：

```js
// 父对象
function Animal(){
    this.species = "动物";
}

// 子对象
function Cat(name,color){
    this.name = name;
    this.color = color;
}
```

* 借助构造函数实现继承

```js
function Cat(name,color){
    Animal.apply(this, arguments); // call() 同理;
    this.name = name;
    this.color = color;
}
var cat1 = new Cat("大毛","黄色");
alert(cat1.species); // 动物
```

缺点：那就是对于每一个实例对象，属性和方法都是一模一样的内容，每一次生成一个实例，都必须为重复的内容，多占用一些内存。这样既不环保，也缺乏效率。



* 借助原型链：

```js
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
var cat1 = new Cat("大毛","黄色");
alert(cat1.species); // 动物
```

缺点：Cat、cat1的 constructor 都会指向 Animal，但 cat1 是由 Cat 构造函数生成的。导致无法判断对象与实例之间的关系。



* 组合方式：

```js
function Cat(name,color){
    Animal.call(this); 
    this.name = name;
    this.color = color;
}
Cat.prototype = new Animal();
var cat1 = new Cat();
```

优点：弥补了上述两种方法的不足

缺点：父类的构造函数执行了两次



* 直接继承prototype

```js
// 改写 Animal()；
function Animal(){ }
Animal.prototype.species = "动物";

// 将Cat的prototype对象，然后指向Animal的prototype对象
Cat.prototype = Animal.prototype;
Cat.prototype.constructor = Cat;
var cat1 = new Cat("大毛","黄色");
alert(cat1.species); // 动物
```

缺点： Cat.prototype 和 Animal.prototype 现在指向了同一个对象，那么任何对 Cat.prototype 的修改，都会反映到Animal.prototype。



* 利用空对象作为中介

```js
Cat.prototype = Object.create(Animal.prototype);
Cat.prototype.constructor = Cat;
var cat1 = new Cat("大毛","黄色");
```

---

#### 参考资料：

Javascript 面向对象编程（一）：封装：[http://www.ruanyifeng.com/blog/2010/05/object-oriented\_javascript\_encapsulation.html](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html)

Javascript面向对象编程（二）：构造函数的继承：[http://www.ruanyifeng.com/blog/2010/05/object-oriented\_javascript\_encapsulation.html](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html)

Javascript面向对象编程（三）：非构造函数的继承[http://www.ruanyifeng.com/blog/2010/05/object-oriented\_javascript\_inheritance\_continued.html](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)

Javascript定义类（class）的三种方法：[http://www.ruanyifeng.com/blog/2012/07/three\_ways\_to\_define\_a\_javascript\_class.html](http://www.ruanyifeng.com/blog/2012/07/three_ways_to_define_a_javascript_class.html)

