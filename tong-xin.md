## 通信

---

#### 同源策略及限制：

同源策略限制从一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的关键的安全机制。

源：协议 域名 端口（默认是80）

* Cookie、LocalStorage和IndexDB 无法读取
* DOM无法获得
* Ajax请求不能发送

#### 前后端如何通信：

* Ajax\(请求受到同源策略的限制。\)
* websocket\(不受到同源策略的限制。\)
* CORS\(可以跨域\)

#### 如何创建Ajax：

* XMLHttpRequest对象的工作流程
* 兼容性处理
* 事件的触发条件
* 事件的触发顺序

```js
// 声明对象，兼容性处理
var xhr =XMLHttpRequest ? new XMLHttpRequest() : new window.ActiveXObject("Microsoft.XMLHTTP");

// 发送,method:post/get,url:请求地址,async:true(异步)或false(同步)
// 如果为 GET，url后直接加参数：xxxxxx?xxx=xxx&xxx=xxx,
// 如果为 POST，send(xxx=xxx&xxx=xxx)
xhr.open(method,url,async);
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded"); // 如果是 POST 方法 
xhr.send() // GET

// 响应
xhr.onload = function(){
    if(xhr.status === 200){
        ...
    }else{
        ...
    }
}
```

#### 跨域通信的几种方式：

###### JSONP：

最常见的一种跨域方式，其背后原理就是利用了script标签不受同源策略的限制，在页面中动态插入了script，script标签的src属性就是后端api接口的地址，并且以get的方式将前端回调处理函数名称告诉后端，后端在响应请求时会将回调返还，并且将数据以参数的形式传递回去。

```js
var script = document.createElement('script');
script.src = 'xxxx?callback=_callback'
document.body.appendChild(script);      //插入script标签
//回调处理函数 _callback
script.onload = script.onreadystatechange = function(){
  if(!this.readyState || this.readyState=='loaded' || this.readyState=='complete'){
    func();
    script.onload = script.onreadystatechange = null;
  }
};
```

###### Hash：

```js
var b = document.getElementsByTagName('iframe');
b.src = b.src + '#' + 'data';
window.onhashchange = funcion(){
    var data = window.location.hash;
}
```

###### postMessage：

```
// 窗口A向跨域的窗口B发送信息
window.postMessage('data','http://b.com');
// 在B窗口中监听
window.addEventListener('message', function(event){
    console.log(event.origin); // http://a.com
    console.log(event.source); // a窗口
    console.log(event.data); // data
},false);
```

###### WebSocket：

```js
// 加密：wss
var ws = new WebSocket("wss://echo.websocket.org");

ws.onopen = function(evt) { 
  console.log("Connection open ..."); 
  ws.send("Hello WebSockets!");
};

ws.onmessage = function(evt) {
  console.log( "Received Message: " + evt.data);
  ws.close();
};

ws.onclose = function(evt) {
  console.log("Connection closed.");
};   
```

###### CORS：

```js
fetch(url,{
    method: 'get', 
}).then(function(response){
    ...
}).catch(function(err){
    ...
});
```

---

参考资料：

浏览器同源政策及其规避方法：[http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)

跨域资源共享 CORS 详解：[http://www.ruanyifeng.com/blog/2016/04/cors.html](http://www.ruanyifeng.com/blog/2016/04/cors.html)

WebSocket 教程：[http://www.ruanyifeng.com/blog/2017/05/websocket.html?utm\_source=tuicool&utm\_medium=referral](http://www.ruanyifeng.com/blog/2017/05/websocket.html?utm_source=tuicool&utm_medium=referral)



