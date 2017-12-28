## MVVM框架

---

#### MVVM框架：

Vue.js  React.js  Angular.js

#### MVVM的认识：

###### MVC:

* 视图（View）：用户界面。
* 控制器（Controller）：业务逻辑
* 模型（Model）：数据保存

![](/assets/mvc.png)

* View 传送指令到 Controller
* Controller 完成业务逻辑后，要求 Model 改变状态
* Model 将新的数据发送到 View，用户得到反馈
* 所有通信都是单向的

###### MVP:

MVP 模式将 Controller 改名为 Presenter，同时改变了通信方向。

* 各部分之间的通信，都是双向的。
* View 与 Model 不发生联系，都通过 Presenter 传递。
* View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而 Presenter非常厚，所有逻辑都部署在那里。

![](/assets/mvp.png)

###### MVVM:

![](/assets/mvvm.png)

双向绑定。View/Model的变动，自动反映在 ViewModel，反之亦然。

* View 接收用户交互请求
* View 将请求转交给ViewModel
* ViewModel 操作Model数据更新
* Model 更新完数据，通知ViewModel数据发生变化
* ViewModel 更新View数据

#### 双向绑定原理：



---

mvc、mvp、mvvm使用关系总结：[http://blog.csdn.net/hudan2714/article/details/50990359](http://blog.csdn.net/hudan2714/article/details/50990359)

剖析Vue原理&实现双向绑定MVVM：[https://segmentfault.com/a/1190000006599500](https://segmentfault.com/a/1190000006599500)

Object.defineProperty\(\)：[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Object/defineProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)



