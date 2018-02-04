## 页面性能

---

#### 提升页面性能的方法：

* 资源压缩合并，减少HTTP请求
* 非核心代码异步加载
  ###### 异步加载的方式：

  * 动态脚本加载
  * defer
  * async

  ###### 异步加载的区别：

  * defer是在HTML解析完之后才会执行，如果是多个，按照加载的顺序执行
  * async是在加载完之后立即执行，如果是多个，执行顺序和加载顺序无关

* 利用浏览器缓存
  ###### 强缓存

  * Expires/Cache-Control

  ###### 协商缓存

  * Last-Modified/If-Modified-Since
  * Etag/If-None-Match

* 使用CDN
* 预解析DNS
  * &lt;meta http-equiv="x-dns-prefetch-control" content="on"&gt;
  * &lt;link rel="dns-prefetch" href="//host\_name_\__to\_prefetch.com"&gt;



