
---
title: 监听scroll，判断是否在视口？
date: 2019-05-31 21:05:33 +0800
tags: []
categories: 
---
<a name="Jc7eO"></a>
### 写在前面
今天碰到一个诉求，网页性能太慢，需要优化首屏加载速度。网页由10个视频资源，加10个图片资源构成，所有资源在同一时间加载（真不是我写的，我不接这个锅）。<br />立马想到的方案是，延迟加载，通过判断元素中心点的位置，来赋予src属性。同时要保证，视频超出视窗一半及暂停，反之则自动开始播放。毫无疑问，监听scroll事件来做了，scroll搭配setTimeout也还行，节流，功能也能实现。但是我觉得可以更好，一顿骚气搜索以后找到一个api[ ](https://developers.google.com/web/updates/2016/04/intersectionobserver)[`Intersection observer`](https://developers.google.com/web/updates/2016/04/intersectionobserver)，简直了，百分百契合我的诉求。
<a name="hRRzW"></a>
### 调试过程

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        html,body{
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
        }


        .box{
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            align-content: center;
            align-items: center;
            justify-content: center;
            font-size: 50px;
            border: 1px solid red;
            box-sizing: border-box;
            margin: 10px 0;
        }
        </style>
</head>
<body>
    <div class="box" id="box1">1</div>
    <div class="box" id="box2">2</div>
    <div class="box" id="box3">3</div>
    <div class="box" id="box4">4</div>
    <div class="box" id="box5">5</div>
</body>
</html>
```

```javascript
var option ={
  root:null, // 你要监听的taget的父元素，不填为window
  threshold:0.5 // 可以理解为一个阈值，0-1，默认是0，就是只要露头就触发callback，1是完全显示才触发callback
}
var callback =function(entries,observer){
  // 这里的参数比较多,这里只需要isIntersecting
  //entires是一个数组，包含了每个监听对象的IntersectionObserverEntry
  //我们要用的是entry.isIntersecting 
  //返回一个布尔值, 如果目标元素与交叉区域观察者对象(intersection observer) 的根相交，
  //则返回 true .如果返回 true, 则 IntersectionObserverEntry 描述了变换到交叉时的状态; 
  //如果返回 false, 那么可以由此判断,变换是从交叉状态到非交叉状态.
  entries.forEach(function(entry){
  	if(entry.isIntersecting) {
    	// 露头了 搞事情，播放视频，src赋值什么的
    } else{
    	//开溜了 ，暂停视频，节约资源
    }
  })
}
var target1 = document.querySelector('#box1');
var target2 = document.querySelector('#box2');
var target3 = document.querySelector('#box3');
var target4 = document.querySelector('#box4');
var target5 = document.querySelector('#box5');
var observer = new IntersectionObserver(callback,option);
observer.observe(target1);
observer.observe(target2);
observer.observe(target3);
observer.observe(target4);
observer.observe(target5);
```
[**IntersectionObserverEntry**](https://developer.mozilla.org/zh-CN/docs/Web/API/IntersectionObserverEntry)**的详细解释可以点击链接去到MDN查看**
<a name="tkzjj"></a>
#### IntersectionObserver其他方法

- disconnect 使`IntersectionObserver`对象停止监听工作
- takeRecords 返回所有观察目标的[`IntersectionObserverEntry`](https://developer.mozilla.org/zh-CN/docs/Web/API/IntersectionObserverEntry)对象数组
- unobserver 使`IntersectionObserver`停止监听特定目标元素。
<a name="Gvpq9"></a>
### 小结
以往的方法都是监听scroll再结合`[getBoundingClientRect](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect)`，这个新的api可以省去很多东西，性能方面，肯定是比scroll监听要好，如果实现了你的目的，没有后续的，可以直接停止监听。



