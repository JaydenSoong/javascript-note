# 一、元素偏移量 offset 系列属性

## 1.1 offset 概述

offset：偏移量。

offsetXXX 是元素的系列属性，可以通过 `dir(node)`在元素节点的所有属性中找到 offsetXXX 系列属性。通过该系列属性可以动态得到元素的位置(偏移)，大小等。作用：

1. 获得距离元素最近的带定位的父元素(设置了 postion 属性)，如果所有父元素都没有定位，则返回 body 元素。
2. 获得元素相对于在定位父元素的位置(偏移量)。
3. 获得元素自身大小信息。

> 注意：该系列属性的返回值都不带单位。

| offsetXXX 系列属性   | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.offsetParent | 返回距离元素最近的带定位的父元素，如果所有父元素都没有定位，返回 body 元素 |
| element.offsetTop    | 返回元素相对于定位父元素上方的偏移量                         |
| element.offsetLeft   | 返回元素相对于定位父元素左方的偏移量                         |
| element.offsetWidth  | 返回元素宽度，包含 padding、border 的值                      |
| element.offsetHeight | 返回元素高度，包含 padding、border 的值                      |

## 1.2 与 style 的区别

| offsetXXX                                            | style                                     |
| ---------------------------------------------------- | ----------------------------------------- |
| offset 可以得到任意样式表中的样式值                  | style 只能得到行内样式表中样式的值        |
| offset 系列的返回值是不带单位的                      | style 获得的值是带有单位的字符串          |
| offset 系列获取的元素大小包含了 padding、border 的值 | style 获得的值不包含 padding、border 的值 |
| offset 系列属性只读属性，不能用于赋值                | style 是可读写的，可以给元素样式赋值      |

> ==总结：==
> 如果只是想要获取元素的位置和大小，使用 offsetXXX 更合适，如果需要更改元素样式，则需要使用 style 属性。

案例 1：鼠标在盒子中的位置

```javascript
let con = document.querySelector('.container');
con.addEventListener('mousemove', ()=>{
  // 1. 通过 e.pageX, e.pageY 获取鼠标相对于页面的坐标
  // 2. e.target.offsetTop, e.target.offsetLeft 可以获取盒子相对于页面的坐标
  // 3. 两都分别相减就可以得到鼠标相对于盒子的坐标
  let x = event.pageX - event.target.offsetLeft;
  let y = event.pageY - event.target.offsetTop;
  con.innerHTML = '鼠标d盒子的位置是 ('+ x + ', ' + y + ')';
});
```

# 二、元素可视区 client 系列

## 2.1 client 相关概念

client(客户端)，使用 client 系列的相关属性可以用来获取元素可视区的相关信息，比如边框大小、元素大小等。同样也可以通过 `dir(node)`在元素节点的所有属性中找到 clinetXXX 系列属性。

| clientXXX 属性       | 作用                                         |
| -------------------- | -------------------------------------------- |
| element.clientTop    | 返回元素上边框的大小                         |
| element.clientLeft   | 返回元素左边框的大小                         |
| element.clientWidth  | 返回元素自身宽度，包含 padding，但不包含边框 |
| element.clientHeight | 返回元素自身高度，包含 padding，但不包含边框 |

> **注意：**
>
> client 系列的返回值也是不带单位的

## 2.2 立及执行函数

立即执行函数 `(function(){})()` 或 `(function(){}())`，主要作用是创建一个独立的作用域，避免了命名冲突的问题。下面是两种立即函数的代码举例。

```javascript
// (3, 4) 相当于函数调用，在前面括号中的函数可以是匿名函数，也可以是有名字的函数
(function fn(a, b){
    var num = 10; //局部变量
  	console.log(a + b)
})(3, 4);
// (6, 9) 相当于函数调用，在前面括号中的函数可以是匿名函数，也可以是有名字的函数
(function fn(a, b){
    var num = 10; //局部变量
    console.log(a + b)
}(6,9));
```

## 2.3 load 事件与pageshow 事件的区别

下面三种情况刷新页面都会触发 load 事件。

1. 通过 a 标签的超链接打开页面
2. F5 或者刷新按钮强制刷新页面
3. 通过前进或后退打开页面

但是，火狐浏览器有个"往返缓存"，这个缓存中不仅保存着页面数据，还保存了 DOM 和 JavaScript 的状态，实际上是将整个页面都保存在了内存里，所以此时后退按钮不能刷新页面。

这个时候如果希望刷新页面就可以通过触发 pageshow 事件来实现。pageshow 在页面显示时触发，无论页面是否来自缓存。在重新加载页面时，pageshow 会在 load 后触发。pageshow 会根据对象中的 persisted 来判断是否是缓存中的页面触发的 pageshow 事件。

> ==注意：==
>
> **pageshow 事件是给 window 添加的**

# 三、元素滚动 scroll 系列

## 3.1 元素 scroll 系列属性

scroll(滚动)，scroll 系列的相关属性可以动态的得到该元素的大小、滚动距离等。同样也可以通过 `dir(node)`在元素节点的所有属性中找到 scrollXXX 系列属性。该系列的**返回值也是不带单位**的。

| scroll 系列属性      | 作用                         |
| -------------------- | ---------------------------- |
| element.scrollTop    | 返回被卷去的上侧距离         |
| element.scrollLeft   | 返回被卷去的左侧距离         |
| element.scrollWidth  | 返回自身实际的宽度，不含边框 |
| element.scrollHeight | 返回自身实际的高度，不含边框 |

![](.\images\scroll.png)

## 3.2 页面被卷去头部的处理

如果浏览器的高(宽)不足以显示整个页面时，会自动出现滚动条。当滚动条向下滚动时，页面上部被隐藏的高度，就称为页面被卷去的头部。滚动条在滚动时会触发 onscroll 事件。

应用分析：

1. 经常需要用到滚动事件 scroll 是页面滚动，所以事件源是 document。
2. 如果需要在滚动到某个值做某件事情(比如淘宝页面的固定侧边栏)，就判断卷去的头部的值是否大于某个预设值。
3. **页面**被卷去的头部可以通过 `widow.pageYOffset`获得，如果是被卷去的左侧则通过 `window.pageYOffset`获得。
4. **元素**被卷去的头部是`element.scrollTop`，与**页面**被卷去的头部获得是不一样的。

**兼容问题：**

需要注意的是，获取页面被卷去的头部的方式`window.pageYOffset`有兼容性问题，通常有如下处理方式：

1. 声明了 DTD，使用 `document.documentElement.scrollTop`
2. 未声明 DTD，使用 `document.body.scrollTop`
3. 新的方法 `window.pageYOffset` 和 `window.pageXOffset` 是从 IE9 开始支持的。

下面的自定义函数可以处理该兼容性问题(如果不考虑 IE9 以下的浏览器，下面函数只作了解)

```javascript
function getScroll() {
  return {
    left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft || 0,
    top: window.pageXOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
  };
}
// 调用该函数
let left = getScroll().left
let top = getScroll().top
```

# 四、offset、client 与 scroll 三大系列总结

## 4.1 三大系列大小对比，以 width 举例

| xxxWidth            | 作用                                   |
| ------------------- | -------------------------------------- |
| element.offsetWidth | 返回自身宽度，包含 padding、边框       |
| element.clientWidth | 返回自身宽度，包含 padding，不包含边框 |
| element.scrollWidth | 返回自身宽度，包含 padding，不包含边框 |

![offset](.\images\offset.png)

![client](.\images\client.png)

![scroll](https://gitee.com/jaydensoong/javascript-note/blob/main/images/scroll1.png)

## 4.2 应用场景

1. offset 系列经常用于获得元素位置 offsetLeft、offsetTop
2. client 系列经常用于获取元素大小 clientWidth、clientHeight
3. scroll 系列经常用于获取滚动距离 scrollTop、scrollLeft
4. 页面的滚动和元素不同，通过 `window.pageYOffset`、`window.pageXOffset`获得

