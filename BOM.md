# 一、什么是BOM

## 1.1 BOM 概述

BOM(Browser Object Model) 即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是 window。

BOM 由一系列相关对象组成，并且每个对象都提供了很多方法与属性。

BOM 缺乏标准，JavaScript 语法的标准化组织是 ECMA，DOM 的标准化组织是 W3C，BOM 最初是 Netscape 浏览器标准的一部分。

| DOM                              | BOM                                              |
| -------------------------------- | ------------------------------------------------ |
| 文档对象模型                     | 浏览器对象模型                                   |
| DOM 就是把文档当成一个对象来看待 | 把浏览器当成一个对象来看待                       |
| DOM 的顶级对象是 document        | BOM 的顶级对象是 window                          |
| DOM 主要学习的是操作页面元素     | BOM 学习的是浏览器窗口交互的一些对象             |
| DOM 是 W3C 标准规范              | BOM 是浏览器厂商在各自浏览器上定义的，兼容性较差 |

## 1.2 BOM 的构成

 window 对象是浏览器的顶级对象，它具有双层角色。

1. 它是 JS 访问浏览器窗口的一个接口
2. 它是一个全局对象。定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法。在调用时可以省略 window，前面学习的对话框都属于 window 对象方法，如 alert()，prompt() 等。

> 注意：window 下有一个特殊属性 window.name。所以我们在定义全局变量时就不要使用 name 作为变量名。

# 二、window 对象常用事件

## 2.1 窗口加载事件

```javascript
// 传统方式
window.onload = function() {}
// 事件监听方式
window.addEventListener('load', function(){})
```

`window.onload` 是窗口(页面)加载事件，当文档内容(包括图像、脚本文件、CSS文件等)全部加载完成会触发该事件。

> 注意：
>
> 1. 有了`window.onload`就可以把 JS 代码写到元素定义的上方，因为 onlaod 是等页面内容全部加载完毕，再去执行处理函数。
> 2. `window.onload`传统注册事件方式只能写一次，如果有多个，会以最后一个`window.onload`为准。
> 3. 如果使用`addEventListener`则没有限制。

```javascript
document.addEventListener('DOMContentLoaded', function(){})
```

1. DOMContentLoaded 事件触发时，仅当 DOM 加载完成，不包括样式表、图片、flash等。
2. 需要 IE9 以上才支持。
3. 如果页面图片很多的话，从用户访问到 onload 事件触发可能需要较长的时间，交互效果才能实现，影响用户体验，此时用 DOMContentLoaded 事件比较合适。

## 2.2 调整窗口大小事件

```javascript
window.onresize = function(){}
window.addEventListener('resize', function(){})
```

`window.onresize`是调整窗口大小加载事件，当窗口大小发生变化时触发。

>**注意：**
>
>1. 只要窗口大小发生像素变化，就会触发这个事件
>2. 可以利用这个事件完成响应式布局，用`window.innerWidth`属性来获取当前窗口宽度。

```javascript
window.addEventListener("load", ()=>{
  let div = document.querySelector('div');
  window.addEventListener("resize", ()=>{
    console.log(window.innerWidth);
    if(window.innerWidth < 800) {
      div.style.display = "none";
    } else {
      div.style.display = "block"
    }
  })
})
```

# 三、定时器

## 3.1 两种定时器

window 对象提供了 2 个非常好用的方法——定时器

* setTimeout()
* setInterval()

## 3.2 setTime() 定时器

```javascript
window.setTimeout(调用函数, [延迟毫秒数]);
```

`setTimeout()`方法用于设置一个定时器，访定时器在设定时间到期后调用函数。

> **注意：**
>
> 1. 调用定时器时 window 可以省略
> 2. 调用函数时可以直接写函数，也可以写函数名
> 3. 延迟的毫秒数省略是默认的 0，如果写，是毫秒值
> 4. 多个定时器，可以给每个定时器赋值一个标识符(变量名),如果需要清除定时器，也需要用到定时器的标识符。

```javascript
callback = ()=>{
  console.log('爆炸了');
}
let timer1 = setTimeout(callback, 2000);
let timer2 = setTimeout(callback, 4000);
```

`setTimeout()`这个函数也称为回调函数 callback。

普通函数是按照代码顺序直接调用。

回调函数需要等待时间，时间到了才去调用这个函数，因此称为回调函数。可以理解为上一件事干完回头再调用的意思。之前的事件绑定中的函数也是回调函数。

## 3.3 停止 setTime() 定时器

```javascript
widow.clearTimeout(timeoutID)
```

`clearTimeout()`方法取消了先前通过调用`setTimeout()`建立的定时器。

> **注意：**
>
> 1. 调用时 window 也可以省略
> 2. 需要定时器的标识符作为参数

```javascript
let timer = setTimeout(callback, 5000)
btn.addEventListener('click', ()=>{
	clearTimeout(timer)
}
```

## 3.4 setInterval() 定时器

```javascript
window.setInterval(调用函数, [延迟毫秒数]);
```

`setInterval()`方法用于重复调用一个函数，每隔固定时间，就去调用一次回调函数。

> **注意：**
>
> 1. 调用定时器时 window 可以省略
> 2. 调用函数时可以直接写函数，也可以写函数名
> 3. 延迟的毫秒数省略是默认的 0，如果写，是毫秒值
> 4. 多个定时器，可以给每个定时器赋值一个标识符(变量名),如果需要清除定时器，也需要用到定时器的标识符。

> **两种定时的区别：**
>
> 1. `setTimeout()`延时时间到了就去调用回调函数，只调用一次。
> 2. `setInterval()`每隔固定时间就去调用回调函数，会重复调用多次。

简单时间显示：

```html
<div class="time">
  <div class="h"></div>
  <div class="m"></div>
  <div class="s"></div>
</div>
<script>
  setInterval(()=>{
    let h = document.querySelector('.h');
    let s = document.querySelector('.s');
    let m = document.querySelector('.m');
    let time = new Date();
    h.innerHTML = time.getHours();
    m.innerHTML = time.getMinutes();
    s.innerHTML = time.getSeconds();
  }, 1000);
</script>
```

## 3.5 停止 setInterval() 定时器

```javascript
widow.clearInterval(timeoutID)
```

`clearInterval()`方法取消了先前通过调用`setInterval()`建立的定时器。

> **注意：**
>
> 1. 调用时 window 也可以省略
> 2. 需要定时器的标识符作为参数

```javascript
let start = document.getElementById("start");
let stop = document.getElementById("stop");
// 需要同时设置开始与停止的定时器，可将标识符定义在外面，并赋值为 null(避免返回 undefined)。
let timer = null;
start.addEventListener("click", ()=>{
  timer = setInterval(()=>{console.log("定时器内容")}, 1000);
})
stop.addEventListener("click", ()=>clearInterval(timer)); 
```

案例：

![倒计时](.\images\djs.png)

```html
<div class="container">
  <input type="text">
  <button id="btn">获取验证码</button>
</div>
<script>
  let btn = document.getElementById("btn");
  // 等待时间
  let i=60;
  btn.addEventListener("click", () => {
    btn.disabled = true;
    let timer = setInterval(()=>{
      // 时间减少到 0 时复原按钮，清除定时器，重置时间
      if(i==0){
        btn.disabled = false;
        btn.innerHTML = '获取验证码'
        clearInterval(timer);
        i = 60;
      } else {
        btn.innerHTML = '请等待 ' + i-- + ' 秒';
      }
    }, 1000);
  })
</script>
```

## 3.6 this 指向问题

1. 全局作用域或者普通函数中 this 指向全局对象 window，定时器中的 this 也是指向 window。
2. 方法调用中指向调用它的对象。
3. 构造函数中的 this 指向创建的实例。
4. 箭头函数会默认帮我们绑定外层 this。

```javascript
// 全局作用域 this => window
console.log(this);
// 普通函数 this => window
function fn() {
  console.log(this);
}
fn();
// 定时器 this => window
setTimeout(fn, 1000);

let obj = {
  logThis: function fn(){
    console.log(this);
  }
}
//方法调用 this => obj
obj.logThis()
let btn = document.querySelector('button');
// this => btn
btn.addEventListener('click', function(){
  console.log(this);
})


function Cat() {
  console.log(this);
}
//构造函数 this => Cat{}
let cat = new Cat();

//箭头函数 this=>window
let fnx = () => {console.log(this);}
btn.addEventListener('click', fnx);
```

# 四、JS 执行机制

## 4.1 JS 的单线程特性

javaScript 语言的一大特点就是==单线程==，也就是同一个时间只能做一件事情。这就意味着，所有任务需要排队，前一个任务执行结束才会执行后一个任务。这样就会导致：如果 JS 执行的时间过长，就会造成页面渲染不连贯，导致页面渲染加载阻塞的感觉。

## 4.2 同步和异步

为了解决单线程问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 创建多个线程，于是，JS 中出现了==同步==和==异步==。

### 4.2.1 同步

前一个任务结束的再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。

同步任务都在主线程上执行，形成一个==执行栈==。

### 4.2.2 异步

执行一个任务时，因为这个任务执行时间较长，所以在这个期间，还可以去处理其它任务。

JS 的异步任务是通过回调函数实现的。

一般而言，异步任务有以下有三种类型

1. 普通事件，如 click，resize 等
2. 资源加载，如 load，error 等
3. 定时器，包括 setInterval、setTimeout 等

异步任务相关的回调函数将会被添加到==任务队列==中(任务队列也称消息队列)。

> 他们的本质区别：流水线上各个流程的执行顺序不同。

## 4.3 JS 执行机制

![JS 执行机制](.\images\test.drawio.png)

1. 先执行执行栈中的同步任务。
2. 遇到异步任务(回调函数)就提交给对应的异步处理进程，由异步处理进程将其放到任务队列中。
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按顺序读取任务队列中的异步任务，使被读取的异步任务结束等待状态，进行执行栈，开始执行。
4. 主线程会不断地查询任务队列，获取任务，再执行。这种机制被称为==事件循环(event loop)==。

可以这样理解：

![](.\images\lijie.png)

代码举例：

```javascript
// 显然地，下面代码的打印顺序是 1，2，3。
// 1. 主线程执行第一句，打印 1。
// 2. 执行第二句，定时器中的回调函数属于异步任务，由异步处理机制将其加入到队列中。
// 3. 执行第三句，打印 2。
// 4. 执行栈中的主线程执行完毕，开始检查任务队列中的任务，打印 3。
// 如果将定时器中的等待时间设置为0，执行顺序依然是一样的，只是不需要等待 1000 毫秒
console.log(1);
setTimeout(() => console.log(3), 1000);
//setTimeout(() => console.log(3), 0);
console.log(2);
```

```javascript
// 1. 主线程执行第一句，打印 1。
// 2. 事件监听中的回调函数也属于异步任务，由异步处理机制将其加入到队列中。
// 3. 执行第三句，打印 2。
// 4. 执行第四句，定时器中的回调函数属于异步任务，由异步处理机制将其加入到队列中
// 5. 执行栈中的主线程执行完毕，开始检查任务队列中的任务，打印 3。
// 主线程会反复查询任务队列，只要触发了 click，就会开始执行第二句中的回调函数。这个过程是循环的。
console.log(1);
document.addEventListener('click', () => console.log('click'));
console.log(2);
setTimeout(() => console.log(3), 1000);
```

# 五、location 对象

## 5.1 什么是 location 对象

window 对象提供了一个 location 属性用于获取或设置窗体的 URL，也可以用于解析 URL。因为这个属性返回的是一个对象，所以这个属性也称为 location 对象。

## 5.2 URL

==统一资源定位符(Uniform Resource Locator, URL)==是互联网上标准的资源地址，互联网上每一个文件都有一个唯一的 URL，它包含的信息指出文件的位置及浏览器应该怎么处理它。

URL 的一般语法格式为：

```htm
protocol://host[:port]/path/[?query#fragment]
https://www.tangwai.com/ver6/home/index.htm?name=songdailiang&age=23#link
```

| 组成     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| protocol | 通信协议，常用的有 http、https、ftp等                        |
| host     | 主机(域名) 如 www.baidu.com                                  |
| port     | 端口号，可选，如果没写表示使用默认端口号 80                  |
| path     | 路径，由零个或多个"/"符号隔开的字符串，一般用来表示主机上的一个目录或文件地址 |
| query    | 参数，在"?"后面，以键值对的形式通过"&"连接多个键值对         |
| fragment | 片段，在"#"后面，常用于链接锚点                              |

## 5.3 location 对象的常用属性

| 常用属性            | 返回值                                      |
| ------------------- | ------------------------------------------- |
| ==location.href==   | 获取或设置整个 URL                          |
| ==location.host==   | 返回主机(域名) 如 www.baidu.com             |
| location.port       | 返回端口号，如果没有写则返回空字符串        |
| location.pathname   | 返回路径                                    |
| ==location.search== | 返回参数                                    |
| location.hash       | 返回片段，即 "#" 后面的内容，通常是链接锚点 |

代码举例：获取前一个页面表单的 get 方式提交的用户名。

```javascript
let p = document.querySelector('p');
// 获取参数并且通过 substr()，截取”？“以后的内容
let searchStr = location.search.substr(1);
// 将参数字符通过"="切割为数组，第二个元素就是用户名
let username = searchStr.split('=')[1]
p.innerHTML = username + ', 你好。'
```

## 5.4 location 对象的常用方法

| 常用方法           | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟 location.href 属性一样，可以跳转页面(也称为页面重定向)，会记录历史，可以后退 |
| location.replace() | 替换当前页面，因为不记录历史，所以不能后退                   |
| location.reload()  | 重新加载页面，相当于刷新按钮或 F5，如果参数为 true 表示强制刷新，相当于 Ctrl + F5 |

# 六、navigator 对象

navigator 对象包含有关浏览器的信息，它有很多属性，最常用的是 userAgent，该属性可以返回由客户端发送的 user-agent 头部信息的值。比如，例用下面的信息可以判断用户是用什么终端访问的，并作出相应处理。

```javascript
if(navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i)){
	// 移动端处理
    window.location.href = '';
} else {
    // pc端处理
	window.location.href = '';
}
```

# 七、 history 对象

window 对象提供了一个 history 对象，与浏览器历史记录进行交互。该对象包含用户在浏览器中访问的 URL。

| 常用方法          | 作用                                                         |
| ----------------- | ------------------------------------------------------------ |
| history.back()    | 可以实现后退功能                                             |
| history.forward() | 可以实现前进功能                                             |
| history.go(参数)  | 可以实现前进和后退功能，参数为正整数表示前进，参数为负整数表示后退 |

实际开发中，history 使用得比较少，因为浏览器本身就有前进和后退，只是左开发一些类似 OA 系统时，需要在页面中用按钮实现前进和后退。
