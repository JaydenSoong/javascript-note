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

## 2.2 与 style 的区别

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
