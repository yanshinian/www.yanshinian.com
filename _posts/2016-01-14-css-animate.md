---
layout: post
title: "CSS3动画效果[整理自网络]"
category: Web前端
date: 2016-01-07 12:15
---
一.动画简介





CSS3 提供的 animation 是一个复合属性,它包含了很多子属性。如下表所示:

属性值 | 说明
--|--
animation-name|animation-name
animation-timing-function|用来设置动画的播放方式
animation-delay|用来指定动画的延迟时间
animation-iteration-count|用来指定动画播放的循环次数
animation-direction|用来指定动画的播放方向
animation-play-state|用来控制动画的播放状态
animation-fill-mode|用来设置动画的时间外属性
animation|以上的简写形式

除了这 9 个属性之外,动画效果还有一个重要的属性,就是关键帧属性:@keyframes。 它的作用是声明一个动画,然后在 animation 调用关键帧声明的动画。

//基本格式,“name”可自定义

```
 @keyframes name {
}



```


```

@keyframes myani {

@keyframes myani {
		} 
}


--|--



//从什么状态过渡到什么状态 

```
@keyframes myani {


```
--|--
linear|元素样式从初始状态过渡到终止状态速度是恒速。等同 于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)
ease-in|元素样式从初始状态过渡到终止状态时,速度越来越 快,呈一种加速状态。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0)
ease-out|元素样式从初始状态过渡到终止状态时,速度越来越 慢,呈一种减速状态。等同于贝塞尔曲线(0, 0, 0.58, 1.0)
ease-in-out|元素样式从初始状态过渡到终止状态时,先加速,再减 速。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)
cubic-bezier|自定义三次贝塞尔曲线

5.animation-delay


```
```

6.animation-iteration-count


```
```

属性值 | 说明
--|--
次数|默认值为 1
infinite|表示无限次循环

7.animation-direction


```
```

属性值 | 说明
--|--
normal|默认值,每次播放向前
alternate|一次向前,一次向后,一次向前,一次向后这样交替

8.animation-play-state


```
```

9.animation-fill-mode


```
```

属性值 | 说明
--|--
forwards|动画结束后继续应用最后关键帧位置,即不返回
backforwards|动画结束后迅速应用起始关键帧位置,即返回
both|根据情况产生 forwards 或 backforwards 的效果

//both 需要结合,次数和播放方向 

```
animation-iteration-count: 4; 
animation-direction: alternate;
```




```
```
为了兼容旧版本,需要加上相应的浏览器前缀,版本信息如下表:

&nbsp;|Opera|Firefox|Chrome|Safari|IE

//兼容完整版,Opera 在这个属性上加入 webkit,所以没有-o-

```
-webkit-animation: myani 1s ease 2 alternate 0s both; 
-moz-animation: myani 1s ease 2 alternate 0s both; 
-ms-animation: myani 1s ease 2 alternate 0s both; 
transition: all 1s ease 0s;
```

//@keyframes 也需要加上前缀 

```
@-webkit-keyframes myani {...} 

@-moz-keyframes myani {...} 

@-o-keyframes myani {...} 

@-ms-keyframes myani {...} 

keyframes myani {...}
```

参考链接：

* 《李炎恢老师HTML5第一季视频教程》<http://edu.51cto.com/course/course_id-3148.html>







