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
> 4. 如果有多个定时器，可以给每个定时器赋值一个标识符(变量名)

```javascript
callback = ()=>{
  console.log('爆炸了');
}
let timer1 = setTimeout(callback, 2000);
let timer2 = setTimeout(callback, 4000);
```



