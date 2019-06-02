
---
title: orientaton= 0, 不一定是竖屏
date: 2019-05-30 20:59:41 +0800
tags: []
categories: 
---
<a name="bXpp6"></a>
### 写在前面
最近在做一个东西，有这么一个需求，希望在平板下的横屏时，改变一个盒子的padding。<br />看起来很简单，那就动手干

```javascript
window.addEventListenser('orientationchange', handle);
function handle() {
  if(Math.abs(window.orientation) === 90) {
    // 加类名等改样式操作，横屏
  } else {
  	// 去掉样式 
  }
}
```

<a name="3l5ym"></a>
### 碰到麻烦
就上述这么一个简单的逻辑，碰到了两个难题，一个一个来说一下
<a name="dOB3d"></a>
#### 1.`orientationchange` 不是 change after 而是ing
希望是在屏幕方向变换后，再去改变样式，但是这个事件是发生时就会触发。那么可能就会有个问题，拿到的`window.orientation`不是屏幕方向变换后的，而是旧的。怎么解决呢。有两个方案，一个是设置个定时器，而是设置个延时器。我这里采用第二种。

```javascript
function handle() {
  // 假设用户不会频繁切换横竖屏，如果有 设置一个timer 然后依据情况clearTimer
  setTimeout(function(){
    if(Math.abs(window.orientation) === 90) {
    // 加类名等改样式操作，横屏
  } else {
  	// 去掉样式 
  }
  },0); // 利用事件队列机制，放到宏任务队列中
}
```

<a name="o9YKM"></a>
#### 2.一般情况下`orientation` 可以通过0，180，90，-90等判断横竖屏，但总有例外
现在的pad都支持分屏，横屏pad，分屏后，就变成了两个“竖屏”（场景A），但是orientation还是0或者180。同理，pad竖屏状态下，分屏后，就变成了两个“横屏”（场景B），但是orientation还是90或-90。懵逼了。这怎么玩。<br />给一下问题分析的过程<br />1.场景A，虽然js里面log的window.orientation是“横屏”，但是生效的样式（写了@media screen and (orientation:portrait))是竖屏的。那证明css层面展示的屏幕是对的。<br />2.搜索一下media这个东西有没有什么相关的jsapi可以用，找到了`matchMedia`这个api<br />matchMedia(_mediaQueryString_); 返回一个对象，我们用到的是`matchMedia(``_mediaQueryString_``).matches`表示的是是否匹配：就好比，我们css里面写的媒体查询一样，这例就是这个_mediaQueryString生效的结果Boolean值_<br />_那么代码就可以改造一下了_<br />_
```javascript
var mediaQueryLandscape = window.matchMeida('(orientation:landscape)');
function handle() {
  // 假设用户不会频繁切换横竖屏，如果有 设置一个timer 然后依据情况clearTimer
  setTimeout(function(){
    if(mediaQueryLandscape.matches) {
    // 加类名等改样式操作，横屏
  } else {
  	// 去掉样式 
  }
  },0); // 利用事件队列机制，放到宏任务队列中
}
```
 两个问题完美解决
<a name="i7aNq"></a>
### 小结一下
1.`orientation`其实准确来说不能算是“横竖屏”的判断依据，要看设备设计的理念了，有个pad，默认形态是竖着，有的则是横着。<br />2.我们web里面提到的横竖屏，其实跟设备形态无关，至于视口的宽高有关，竖屏：宽<高，横屏：高<=宽，其实真的有正方形的设备，不管怎么旋转都是横屏。<br />3.要准确的判断横竖屏，要么通过宽高，要么通过matchMedia（移动端推荐使用，PC旧浏览器不兼容）

