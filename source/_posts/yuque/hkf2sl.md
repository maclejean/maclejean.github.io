
---
title: Talkback的问题
date: 2019-03-05 21:49:25 +0800
tags: []
categories: 
---
![](https://cdn.nlark.com/yuque/0/2019/png/273716/1557145243063-7fd36cf7-9845-4680-afad-e9795ea0c34c.png#align=left&display=inline&height=42&originHeight=170&originWidth=553&status=done&width=138)<br />最近在做的一个hybrid项目，碰到一个talkback问题：webview上的评分控件在talkback模式下无法选中，<br />实现方式就是span标签加背景图，touch事件监听选中与取消选中。

```javascript
//代码仅做展示demo，无实际逻辑
star.ontouchstart = fn1
star.ontouchend = fn2;
```
[Accessible Rich Internet Applications ](https://developer.mozilla.org/zh-CN/docs/Web/Accessibility/ARIA)[**(ARIA)**]()[ 是能够让残障人士更加便利的访问 Web 内容和使用 Web 应用（特别是那些由 Ajax 和 JavaScript 开发的）的一套机制。]()<br />MDN 上有比较详尽的介绍，其实感觉一般的公司都碰不到这样的场景，也不会顾忌这些。但是既然碰到了，就mark一下。<br />介绍了很多适配的规则跟方法，`<span aria-label="button" />`,这里talkback选中时，就会播报“button”。<br />那就有新的问题了，难道我还要根据语种设置不同的value吗？可以是可以，但是没必要。HTML讲究语义化，我直接把`span`换成`button`，试了一下，中文下说“按钮”，英文说“button”，正好，至于其他语种，因为是中文rom，其他小语种都没支持，至于国外rom，没试过。<br />选中播报的问题解决了，还有一个问题，就是talkback下，“星星”选中与取消选中不生效了。MMP，真的是不明所以，定位咯，“touchstart”，“touchend”事件全部加log，看下是什么原因。<br />未开启talkback，全部正常打印log，开启talkback，一个都不响应了。百度谷歌搜了个遍，当然英文的 我也不会看那么细，没养成习惯，反正结果就是没有结果。<br />那就开启各种试了，第一个想到的就是改成“click”事件，忽略300ms延时吧。结果一试就可以了。人品爆发。<br />反正后面还要各种改，冒泡改成捕获，捕获还要根据结果决定是否阻止继续捕获。

```javascript
//代码仅做展示demo，无实际逻辑
star.onclick = fn4;
```

总而言之感觉就是，talkback对“click”支持的是比较好的，touch事件，在webview的talkback下，简直被废了。先码一文，等待后续有新的发现再自己打自己脸,ORZ.

