## JS运行机制

---

#### JS是单线程：

一个时间内只能做一件事

#### 任务队列：

###### 异步任务：

* setTimeout和setInterval（setTimeout 设置为 0，也会有4ms的延迟）
* DOM事件
* ES6中的Promise

###### 同步任务（优先处理同步任务）

#### Event Loop：

[http://www.ruanyifeng.com/blog/2013/10/event\_loop.html](http://www.ruanyifeng.com/blog/2013/10/event_loop.html)

