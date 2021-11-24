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

![](https://gitee.com/jaydensoong/imgsrc/raw/master/scroll.png)

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

![](https://gitee.com/jaydensoong/imgsrc/raw/master/offset.png)

![](https://gitee.com/jaydensoong/imgsrc/raw/master/client.png)

![](https://gitee.com/jaydensoong/imgsrc/raw/master/scroll1.png)

## 4.2 应用场景

1. offset 系列经常用于获得元素位置 offsetLeft、offsetTop
2. client 系列经常用于获取元素大小 clientWidth、clientHeight
3. scroll 系列经常用于获取滚动距离 scrollTop、scrollLeft
4. 页面的滚动和元素不同，通过 `window.pageYOffset`、`window.pageXOffset`获得

# 五、动画函数封装

## 5.1 动画实现原理

**核心原理：**通过定时器 setInterval() 不断移动盒子位置

实现步骤：

1. 获取盒子当前位置
2. 让盒子在当前位置加上 1 个移动距离
3. 利用定时器不断重复步骤 2 中的动作
4. 设置一个结束定时器的条件

```javascript
let div = document.querySelector('div');
let timer = setInterval(() => {
  // 到达指定位置，清除定时器
  if(div.offsetLeft >= 400) {
    clearInterval(timer);
  }
  // 获取位置用 offsetXXX，设置用 style
  div.style.left = div.offsetLeft + 1 + 'px';
}, 30)
```



> 注意：这里设置动画的元素需要添加定位，设置``postion: absolute`才能使用`element.style.left`等。

## 5.2 动画函数简单封装

封装函数时定义两个形参：**动画对象**和**移动距离**。

```javascript
function animate(obj, target) {
  let timer = setInterval(() => {
    // 到达指定位置，清除定时器
    if(obj.offsetLeft >= target) {
      clearInterval(timer);
    }
    // 获取位置用 offsetXXX，设置用 style
    obj.style.left = obj.offsetLeft + 1 + 'px';
  }, 30);
}
```

## 5.3 给不同元素设置不同定时器

如果多个元素都使用上一节定义的动画函数，每次都要使用`let`声明定时器，这样程序的效率是很低的。这里应该给不同元素设置不同的定时器，让每一个元素使用自己的定时器。这里需要的核心思想就是利用javascript的动态语言特性。将定时器设置为元素的一个属性。

如果需要通过某个事件的触发来开启动画，比如点击按钮。每点击一次就相当于给元素添加了一个定时器，最后元素运动越来越快。与我们的预期不符。这时可以在函数最前面先清除定时器。

最后动画函数改为：

```javascript
function animate(obj, target) {
  //先清除定时器
  clearInterval(obj.timer);
  //直接将定时器设定为元素的一个属性
  obj.timer = setInterval(() => {
    // 到达指定位置，清除定时器
    if(obj.offsetLeft >= target) {
      clearInterval(obj.timer);
    }
    // 获取位置用 offsetXXX，设置用 style
    obj.style.left = obj.offsetLeft + 1 + 'px';
  }, 30);
}
```

## 5.4 缓动动画

缓动动画就是让元素的运动速度有所变化，最常见的就是让速度慢慢停下来。可以这样理解：

匀速动画就是盒子当前的位置 + 固定值(比如 10)

缓动动画就是盒子当前的位置 + 变化的值(设定步长 = (目标 - 现在的位置) / 10)

 所以，缓动动画的实现可以分为下面几步：

1. 让盒子每次移动的距离慢慢变小，速度就会慢慢落下来
2. 核心算法：步长 = (目标值 - 现在的位置) / 10
3. 停止条件，当盒子位置等于目标位置
4. 步长值需要取整。取整思路：如果步长值为正，往上取整，如果步长值为负，往下取整
5. 当步长值为正时，盒子会往前移动，当步长值为负时，盒子会往后移动

所以现在动画函数变为：

```javascript
function animate(obj, target) {
  clearInterval(obj.timer);
  obj.timer = setInterval(() => {
    // 确定缓动动画步长值
    let step = (target - obj.offsetLeft) / 10;
    // 将步长值调整为整数。如果是正数，就往大取整，如果为负数，就往小取整。
    step = step > 0 ? Math.ceil(step) : Math.floor(step);
    // 到达指定位置，清除定时器
    if(obj.offsetLeft === target) {
      clearInterval(obj.timer);
    }
    // 获取位置用 offsetXXX，设置用 style
    obj.style.left = obj.offsetLeft + step + 'px';
  }, 15); // 定时器的时间一般间隔 15 毫秒
}
```

## 5.5 动画函数添加回调函数

**回调函数原理：**将一个函数作为一个参数传递到另一个函数调用里面，当那个函数执行完毕后再去调用传递进去的这个函数，这个过程就是回调。

所以，可以给我们的动画函数增加一个回调函数参数，让其可以在动画完成后执行其它任务。

> 注意：在封装好的动画函数里面，执行回调函数的位置应该在清除定时器的位置，即动画完成后。

这个时候，动画函数变为：

```javascript
function animate(obj, target, callback) {
  clearInterval(obj.timer);
  obj.timer = setInterval(() => {
    // 确定缓动动画步长值
    let step = (target - obj.offsetLeft) / 10;
    // 将步长值调整为整数。如果是正数，就往大取整，如果为负数，就往小取整。
    step = step > 0 ? Math.ceil(step) : Math.floor(step);
    // 到达指定位置，清除定时器
    if(obj.offsetLeft === target) {
      clearInterval(obj.timer);
      // 清除定时器，动画执行完毕，如果有回调函数，开始执行回调函数
      if(callback) {
        callback();
      }
    }
    // 获取位置用 offsetXXX，设置用 style
    obj.style.left = obj.offsetLeft + step + 'px';
  }, 15); // 定时器的时间一般间隔 15 毫秒
}
```

现在，调用动画函数时就可以传递一个函数参数了。

```javascript
// 动画完成后，将盒子改变颜色
btn800.addEventListener('click', ()=>animate(span, 800, ()=>span.style.backgroundColor='pink'));
```

## 5.6 动画函数的使用

现在，就可以把我们封装好的动画函数单独放在一个 js 文件中，在需要使用到该动画函数的时候，直接在页面中引用该 js 文件就可以了。
