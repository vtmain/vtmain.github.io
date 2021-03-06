---
title: 寄存器-1
date: 2017-04-13 18:23:54
tags:
categories: 汇编
---

8086CPU(16位)的寄存器

<!-- more -->

16位CPU有以下几方面的结构特性：
> 1. 运算器一次最多可处理16位数据
> 2. 寄存器的最大宽度为16位
> 3. 寄存器和运算器之间的通路为16位

8086CPU的所有寄存器都是16位的，可以存放两个字节
8086CPU内部，能够一次性处理、传输、暂时存储的信息最大长度是16位的（内存单元的地址在送上地址总线之前）
8086CPU有20位地址总线，可以传送20位地址，达到1MB寻址能力

  | 通用寄存器 | 段寄存器  |
  |:----------|:---------|
  |    AX     |    CS    |
  |    BX     |    DS    |
  |    CX     |    SS    |
  |    DX     |    ES    |

* 当8086CPU要访问内存时由这4个段寄存器提供内存单元的段地址

8086CPU物理地址的表示:
"段地址 * 16 + 偏移地址 = 物理地址"
"   基础地址  + 偏移地址 = 物理地址"
"        CS      :       IP "

CS和IP是8086CPU中两个最关键的寄存器，它们指示了CPU当前要读取指令的地址
>CS：代码段寄存器  
>IP：指令指针寄存器  

任意时刻，设CS中M，IP中N，8086CPU将从M*16+N单元开始，读取一条指令并执行
也可以这样表述：任意时刻，8086CPU取CS:IP指向的内容当做指令执行

8086CPU工作过程概要：
1. 从CS:IP内存单元读取指令，读取的指令进入指令缓冲器;  
2. IP = IP + Length(指令长度);  
3. 执行指令;  
4. 转到1继续执行  

8086CPU加电或复位后(即CPU刚开始工作时)CS和IP被设置为CS = FFFFH，IP = 0000H，即在8086PC机启动时，CPU从内存FFFF0H单元中
读取指令，FFFF0H单元中的指令是8086PC机开机后执行的第一条指令

可以通过改变CS:IP中的内容来控制CPU执行目标指令
>mov：传送指令(可以修改大部分寄存器的值，但是不能用于设置CS、IP)

能够修改CS、IP的指令统称为转移指令，例如jmp
>格式："jmp 段地址:偏移地址"  
>功能：用指令中给出的段地址修改CS，偏移地址修改IP  
>例如：jmp 2AE3:3, 执行后CS = 2AE3H， IP = 0003H，CPU将从2AE33H处读取指令

若单独修改IP内容，可用"jmp 某一合法寄存器"，功能为"用寄存器中的值修改IP"
例如："jmp ax"
>执行前: ax = 1000H, CS = 2000H, IP = 0003H  
>执行后: ax = 1000H, CS = 2000H, IP = 1000H  

其功能类似于"mov IP, ax"指令

关于代码段（16位8086PC机）
代码段长度≤64KB，因为偏移地址最大16位，16位寻址能力为64KB
