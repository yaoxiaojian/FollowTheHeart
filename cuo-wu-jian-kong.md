## 错误监控

---

#### 前端错误的分类：

* 即时运行错误：代码错误
* 资源加载错误

#### 错误的捕获方式：

###### 即时运行错误的捕获方式：

* try...catch
* window.onerror

###### 资源加载错误：

* object.onerror
* performance.getEntries\(\)
* Error事件捕获

#### 捕获跨域JS的错误：

* 在script标签增加crossorigin属性
* 设置js资源响应头Access-Control-Allow-Origin:\*

#### 上报错误的基本原理：

* 采用Ajax通信上报
* 利用Image对象上报

```js
（new Image()).src='htpp://xxxxx.com';
```



