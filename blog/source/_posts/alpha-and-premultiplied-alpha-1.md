---
title: Alpha通道工作原理以及ALPHA_PREMULTIPLIED
toc: false
date: 2017-05-17 18:31:54
updated: 2017-05-17 18:31:54
description:
tags: [Alpha]
categories: [Gamedev]
---


- **Alpha**   

计算机图形学中，Alpha指的是颜色的三个分量(RGB)外的第四个分量，用来计算图像透明度。  

<!-- more -->

所以，一个真彩色(指利用RGB分量合成颜色)的像素就变成由四个分量组成：(R、G、B、A)，也称为四个通道。  
> Alpha通道本身并没有透明的意思，不代表透明度，`opacity`和`transparency`才和透明度有关。前者是不透明度，后者是透明度。比如css中的[opacity:0.5]就是设定元素有50%的不透明度。

32位图像最常见的像素表示格式是`RGBA8888`即(R, G, B, A)每个通道占8位(bit)=1个字节(Byte)，值表示为0-255。为了方便表示，也把Alpha通道值记为0-1的浮点数。比如一个像素的红色60%透明度，就可以表示为(255, 0, 0, 0.6)。  
> 16位的图像RGBA，RGB各占用5位bit，alpha占用1位bit  

正常情况下，根据Alpha通道进行混合颜色(图像合成)，只需要把需要组合的颜色计算出不含Alpha通道的原始RGB值，然后分别对应相加即可。  
算法大概是这样的：  
```
A图：(Ra, Ga, Ba, Alpha_a)  
B图：(Rb, Gb, Bb, Alpha_b)  
```
混合后的RGB三元组：
```
C图：(Rc, Gc, Bc)  
```
则有：
```
Rc = Ra * Alpha_a + Rb * Alpha_b
Gc = Ga * Alpha_a + Gb * Alpha_b
Bc = Ba * Alpha_a + Bb * Alpha_b
```
上述计算，即可得出混合后的颜色。  

> `光栅图像` ...  
> `锯齿`是由于光栅寻址而产生的走样，详细内容学习一下再写出来`

- **ALPHA_PREMULTIPLIED**  

Premultiplied Alpha(ALPHA_PREMULTIPLIED)  
做游戏的应该都知道这个，图片渲染时常见到的一个参数。  
依据Alpha的概念描述，可以知道  


图片示例  
![](https://raw.githubusercontent.com/vtmain/vtmain.github.io/hexo-me/blog/extra/img/color-alpha-blend.png)
