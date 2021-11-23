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
