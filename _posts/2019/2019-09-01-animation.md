---
layout: post
title: 给力的css3 animation动画
category:  arch
tags: [arch]
excerpt: animation常用属性总结与效果举例
---

## 动画animation常用属性总结

动画就是由一个个的关键帧组成的。

#### 1.帧的使用介绍
 > 帧设置从0-100，例子如下：
```
main{
    width: 100px;
    height: 100px;
    background: white;
    animation-name: hd;
    animation-duration: 2s;
}

@keyframes hd{
    0%{
        background: white
    }
    25%{
        transform: scale(2);
    }
    65%{
        transform: scale(1);
        background: #9b59b6;
    }
    100%{
        background: #e74c3c
    }
}
```

#### 2.起始与终点帧特性
 > 系统会默认设置起始帧和终点帧为初始状态。若有设置，设置起始帧会代替掉初始状态，设置终点帧会执行，两者最后都回归到初始状态。

#### 3.同时声明关键帧
  > 组合声明，例子如下：
 ```
 @keyframes hd{
     25%{
         transform: translateX(300px);
     }
     75%{
        transform: translateY(300px);
     }
     25%,75%{
         background: #9b59b6;
         border-radius: 50%;
     }
 }
 ```

#### 4.多个动画使用与时间配置
 ```
 div{
    width: 100px;
    height: 100px;
    background: #f1c40f;
    animation-name: translate,background,radius;
    animation-duration: 4s,2s;/*radius是4s,从头开始*/
}

@keyframes translate{
    25%{
        transform: translateX(300px);
    }
    50%{
        transform: translate(300px,300px);
    }
    75%{
       transform: translateY(300px);
    }

}
 @keyframes background{
    25%{
        background: #2ecc71;
    }
    50%{
        background: #e67e22;
    }   
}
@keyframes radius{
    25%{
        border-radius: 50%;
    }
    50%{
        border-radius: 0%;
    }
}
 ```
#### 5.属性重叠对动画的影响
 ```
div{
    width: 100px;
    height: 100px;
    background: #f1c40f;
    animation-name: translate,background,radius;
    animation-duration: 4s,2s,1s;/*如果没有1s,radius是4s,从头开始*/
}

@keyframes translate{
    25%{
        transform: translateX(300px);
    }
    50%{
        transform: translate(300px,300px);
    }
    75%{
       transform: translateY(300px);
    }

}
 @keyframes background{
    25%{
        background: #2ecc71;
        transform: translateX(300px);/*当background和translate出现相同属性，以后面那个为准，先执行background的动画，消耗两秒之后，translate在4-2=2秒的时候开始执行动画*/
    }
    50%{
        background: #e67e22;
    }
    75%{
       background: #9b59b6;
    }

}
@keyframes radius{
    from,to{
        background: #95a5a6;
    }
    25%{
        border-radius: 50%;
    }
    50%{
        border-radius: 0%;
    }
    75%{
        border-radius: 50%;
    }
}
 ```
#### 6.动画属性中间值详解
 ```
div{
     width: 100px;
     height: 100px;
     background: #f1c40f;
     animation-name: scale;
     animation-duration: 2s;
     border:solid 2px white;
 }

 @keyframes scale{
     to{
         width: 300px; /*100px到300px有中间值*/
         height: 300px;
         border:solid 30px #fff;/*2px到30px有中间值*/
     }
 }
 ```
#### 7.控制动画播放次数
 ```
div{
    width: 100px;
    height: 100px;
    background: #f1c40f;
    animation-name: translate,background,radius;
    animation-duration: 2s;
    animation-iteration-count: infinite,2;/*infinite是无限循环的意思，同样次数不够名字的时候，radius是以前面的数字为准*/
}

@keyframes translate{
    25%{
        transform: translateX(300px);
    }
    50%{
        transform: translate(300px,300px);
    }
    75%{
       transform: translateY(300px);
    }
}
...
 ```
#### 8.控制动画方向的四种模式
 ```
...
i.fa{
    font-size: 3em;
    animation-name: hd;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    position: absolute;
}
li:nth-child(1)>i{
    animation-direction: normal;/*从0到100*/
}
li:nth-child(2)>i{
    animation-direction: reverse;/*从100到0*/
}
li:nth-child(3)>i{
    animation-direction: alternate;/*从0到100，然后慢慢回*/
}
li:nth-child(4)>i{
    animation-direction: alternate-reverse;/*从100到0，然后慢慢回*/
}
 @keyframes hd{
    to{
        transform:scale(3);
    }
}
 ```
#### 9.贝塞尔曲线控制动画速率
 ```
...
ul{
    display: grid;
    grid-template:1fr/repeat(6,1fr);
    list-style: none;
    gap:10px;
}
li{
    background: #e67e22;
    height: 50px;
    animation-name: move;
    animation-duration: 3s;
    animation-iteration-count: infinite;
}
li:nth-child(1){
    animation-timing-function: ease;
}
li:nth-child(2){
    animation-timing-function: ease-in;
}
li:nth-child(3){
    animation-timing-function: ease-out;
}
li:nth-child(4){
    animation-timing-function: ease-in-out;
}
li:nth-child(5){
    animation-timing-function: linear;
}
 li:nth-child(6){
    animation-timing-function: cubic-bezier(.26,.53,1,.3);
}


@keyframes move{
    to{
        transform: translateY(90vh);
    }
}
 ```
#### 10.提交按钮加载动画效果
```
...
button{
    width: 200px;
    height: 50px;
    background: #ecf0f1;
    color: #34495e;
    border:solid 1px #ddd;
    justify-self: center;
    align-self: center;
}
button::after{
    content: '';
    width: 3px;
    height: 3px;
    display: inline-block;
    animation-name: hd;
    animation-duration: 2s;
    animation-iteration-count: infinite;
}
@keyframes hd{
    from{
        box-shadow: none;
    }
    30%{
        box-shadow: 3px 0 0 currentColor;
    }
    60%{
        box-shadow: 3px 0 0 currentColor, 9px 0 0 currentColor;
    }
    90%{
        box-shadow: 3px 0 0 currentColor, 9px 0 0 currentColor, 15px 0 0 currentColor;
    }
}
 ```
#### 11.steps步进动画规则详情
```
main{
    align-self: center;
    justify-self: center;
    width: 400px;
    height: 200px;
    display: grid;
    grid-template:repeat(2,1fr)/repeat(4,1fr);

}
div{
    text-align: center;
    background: #f1c40f;
    border:solid 1px #2c3e50;
    box-sizing: border-box;
    position: relative;
}
div:nth-child(1)::before, div:nth-child(5)::before{
    animation-name: hd;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    z-index: 2;
}

div:nth-child(1)::before{
    content: 'START';
    width: 100px;
    height: 100px;
    background: #8e44ad;
    position: absolute;
    left: 0;
    top: 0;
    animation-timing-function: steps(4,start);/*第一时间点就开始运动*/
}
div:nth-child(5)::before{
    content: 'END';
    width: 100px;
    height: 100px;
    background: #27ae60;
    position: absolute;
    left: 0;
    top: 0;
    animation-timing-function: steps(4,end);/*第一时间点是初始状态*/
}
@keyframes hd{
    to{
        transform: translateX(400px);
    }
}
 ```
#### 12.step-start与step-end单步处理
```
div:nth-child(1)::before{
    content: 'START';
    width: 100px;
    height: 100px;
    background: #8e44ad;
    position: absolute;
    left: 0;
    top: 0;
    animation-timing-function: step-start;/*第一时间点就开始运动,相当于steps(1,start);*/
}
div:nth-child(5)::before{
    content: 'END';
    width: 100px;
    height: 100px;
    background: #27ae60;
    position: absolute;
    left: 0;
    top: 0;
    animation-timing-function:step-end;/*第一时间点是初始状态,相当于steps(1,end);两帧之间的变换*/
}
@keyframes hd{
    50%{
        transform: translateX(100px);
    }
    to{
        transform: translateX(0px);
    }
}
 ```
#### 13.控制动画播放与暂停
```
div:nth-child(1)::before, div:nth-child(5)::before{
    animation-name: hd;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    z-index: 2;
    animation-play-state: paused;
}
...同11知识点
@keyframes hd{
    to{
        transform: translateX(400px);
    }
}
main:hover div::before{
    animation-play-state: running;
}
 ```
#### 14.动画填充模式详解
```
ul{
    list-style: none;
    width: 400px;
    height: 100px;
    align-self: center;
    justify-self: center;
    display: grid;
    grid-template:1fr/repeat(4,1fr);
}
li{
     width: 100px;
     height: 100px;
     border-radius: 50%;
     background: #e67e22;
     animation-duration: 2s;
     animation-delay: 2s;
     display: grid;
     align-items: center;
     justify-items: center;
}
li:nth-child(1){
    animation-name: hd;
}
li:nth-child(2){
    animation-name: hd;
    animation-fill-mode: backwards;/*起始状态是0帧*/
}
li:nth-child(3){
    animation-name: hd;
    animation-fill-mode: forwards;/*到100帧就不动了*/
}
li:nth-child(4){
    animation-name: hd;
    animation-fill-mode: both;/*兼顾backwards和forwards，起始状态是0帧，到100帧就不动了*/
}
@keyframes hd{
    from{
        transform:scale(0);
    }
    to{
        transform:scale(1);
        background: #2ecc71;
    }
}
 ```
#### 15.animation动画组合定义语法
```
li{
     width: 100px;
     height: 100px;
     border-radius: 50%;
     background: #e67e22;
     /*animation-name: hd;*/
     /* animation-duration: 2s;
     animation-delay: 2s;*/
     display: grid;
     align-items: center;
     justify-items: center;
}

li:nth-child(1){
    /*animation-name: hd;*/
    animation: hd 2s 2s;/*组合定义，第一个是名字 第二个是动画时间 第三个是延迟时间*/
}
li:nth-child(2){
   /* animation-name: hd;
    animation-fill-mode: backwards;*/
    animation: hd backwards 2s 2s;/*backwards放哪都可以*/
}
li:nth-child(3){
   /* animation-name: hd;
    animation-fill-mode: forwards;*/
    animation: hd forwards 2s 2s;/*backwards放哪都可以*/
}
li:nth-child(4){
    /*animation-name: hd;
    animation-fill-mode: both;*/
    animation: hd both 2s 2s;/*backwards放哪都可以*/
}
 ```



