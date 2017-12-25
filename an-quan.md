## 安全

---

#### CSRF：

跨站域请求伪造，Cross Site Request Forgery

###### 原理：

![](/assets/anquan.jpg)

###### 防御措施：

* Token验证
* Referer验证
* 隐藏令牌



#### XSS：

跨域脚本攻击，Cross-site scripting

###### 原理：

攻击者在网页中嵌入客户端脚本，通常是Javascript编写的恶意代码，当用户使用浏览器浏览被嵌入恶意代码的网页时，恶意代码将在用户的浏览器上被解析执行。重点在"脚本"这两个字上，脚本主要有两个：JavaScript和ActionScript。

###### 防御：

编码

过滤

校正

---

CSRF：[https://www.jianshu.com/p/7f33f9c7997b](https://www.jianshu.com/p/7f33f9c7997b)

XSS：[https://www.jianshu.com/p/790fb57f3acb](https://www.jianshu.com/p/790fb57f3acb)

