## 类型转换

---

最新的ECMAScript标准定义了7种数据类型

原始类型：Boolean null undefined number string symbol

对象：Object

#### 显示类型转换：

##### Number函数

###### 原始类型转换：

```js
// 数值：转换后还是原来的值。
Number(123) // 123

//字符串：如果可以被解析为数值，则转换为相应的数值，否则为NaN，空字符串转为 0。
Number('123abc') // NaN

 //布尔值：true转成1，false转成0。
 Number(true) // 1 
 
 //undefined：转成NaN。
 Number(undefined) // NaN 
 
 //null：转成0。
 Number(null) // 0
```

###### 对象类型转换：

先调用对象自身的 valueOf 方法，如果该方法返回原始类型的值（数值、字符串和布尔值），则直接对该值使用 Number 方法，不再进行后续步骤。

如果 valueOf 方法返回复合类型的值，再调用对象自身的 toString 方法，如果 toString 方法返回原始类型的值，则对该值使用 Number 发放，不再进行后续步骤。

如果 toString 发放返回的是复合类型的值，则报错。



##### String函数

###### 原始类型转换：

```js
// 数值：转为相应的字符串。
String(123) // "123"

//字符串：转换为相应的数值。
String('123abc') // "123abc"

 //布尔值：true转成"true"，false转成"false"。
 String(true) // "true" 
 
 //undefined：转成"undefined"。
 String(undefined) // "undefined"
 
 //null：转成"null"。
 String(null) // "null"
```

###### 对象类型转换：

先调用 toString 方法，如果 toString 方法返回的是原始类型的值，则对该值使用 String 方法，不再进行以下步骤。

如果 toString 方法返回的是复合类型的值，再调用 valueOf 方法，如果 valueOf 方法返回的是原始类型的值，则对该值使用 String 方法，不再进行以下步骤。

如果 valueOf 方法返回的是复合类型的值，则报错。



##### Boolean函数

```js
Boolean(undefined || null || -0 || 0 || NaN || '') // false，除此之外都为 true。
```

#### 隐式类型转换：

* 四则运算
* 判断语句
* Native调用 如:alert

---

详细资料：[http://blog.csdn.net/yangjvn/article/details/48284163](http://blog.csdn.net/yangjvn/article/details/48284163)



































