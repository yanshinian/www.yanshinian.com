---
layout: post
title: "CSS3过渡效果[整理自网络]"
category: Web前端
date: 2016-01-07 12:15
---



 
属性 | 说明
--|--
transition-property|指定过渡或动态模拟的 CSS 属性 
transition-timing-function|指定过渡的函数
transition-delay|指定过渡开始出现的延迟时间
transition|简写形式,按照上门四个属性值连写

我们先创建一个没有过渡效果的元素,然后通过:hover 来触发它。在没有任何过渡效 果的触发,会立即生硬的执行触发。

//设置元素样式 

```
div {
```

//鼠标悬停后背景变黑,文字变白 

```
div:hover {
```

二.transition-property

首先,设置过渡的第一个属性就是指定过渡的属性。同样,你需要指定你要过渡某个元

属性值 | 说明
--|--
none|没有指定任何样式
all|默认值,指定元素所支持 transition-property 属性 的样式
指定样式|指定支持 transition-property 的样式

从上门的列表中来看,一般来说,none 用于本身有过渡样式从而取消。而 all,则是 支持所有 transition-property 样式,还有一种是指定 transition-property 中的某些 样式。那么 transition-proerty 支持的样式有哪些?如下表所示:

样式名称|样式类型
--|--
background-color |color(颜色)
background-image|only gradients(渐变)
background-position|percentage, length(百分比,长度值)
border-bottom-color|color
border-bottom-width|length
border-color|color
border-left-color|color
border-left-width|length
border-right-color|color
border-right-width|length
border-spacing|length
border-top-color|color
border-top-width|length
border-width|length
bottom|length, percentage
color|color
max-height|length, percentage
opacity|number
outline-color|color
outline-offset|integer
outline-width|length
padding-bottom|length
padding-left|length
padding-right|length
padding-top|length
right|length, percentage
text-indent|length, percentage
text-shadow|shadow
top|length, percentage
vertical-align|keywords, length, percentage
visibility|visibility
width|length, percentage
word-spacing|length, percentage
z-index|integer
zoom|number

//设置背景和文字颜色采用过渡效果
```		
```

三.transition-duration 

如果单纯设置过渡的样式,还不能够立刻实现效果。必须加上过渡所需的时间,因为默


```

四.transition-timing-function 

当过渡效果运行时,比如产生缓动效果。默认情况下的缓动是:元素样式从初始状态过

--|--
linear|元素样式从初始状态过渡到终止状态速度是恒速。等同 于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)
ease-in-out|元素样式从初始状态过渡到终止状态时,先加速,再减 速。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)

```


```
```



//跳跃 10 次至结束 

```
transition-timing-function: steps(10,end);
```

五.transition-delay 

这个属性可以设置一个过渡延迟效果,就是效果在设置的延迟时间后再执行。使用


```
```

六.简写和版本


//单独声明

```
```
//如果每个样式都是统一的,直接使用 all

```
transition: all 1s ease 0s;
```
为了兼容旧版本,需要加上相应的浏览器前缀,版本信息如下表:

&nbsp;|Opera|Firefox|Chrome|Safari|IE

//兼容完整版

```




```

参考链接：

* 《Css3制作变形与动画效果》<http://www.jb51.net/article/69974.htm>
* 《李炎恢老师HTML5第一季视频教程》<http://edu.51cto.com/course/course_id-3148.html>


 