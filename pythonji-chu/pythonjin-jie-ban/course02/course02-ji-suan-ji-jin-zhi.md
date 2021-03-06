# \[course\]02 —— 计算机进制

十进制：逢十进一 二级制：逢二进一

## 二进制：

二进制只有0和1两个数字，基数为2，在加减法运算中，逢二进一，借一当二。 表示数值：0、1、10、111、100、1000001 加法：1+0=1、1+1=10、10+110=1000、111+111=1110、 减法：1-0=1、10-1=1、100-11=1、1010-101=101

二进制和十进制的对应关系： ![](http://ossp.pengjunjie.com/mweb/15904618153750.jpg)

1\) 二进制加法：0001 + 0001 = 0010 ![](http://ossp.pengjunjie.com/mweb/15904618494056.jpg)

2\) 二进制减法：0010 - 0001 = 0001 ![](http://ossp.pengjunjie.com/mweb/15904618650218.jpg)

## 二进制的物理原因

计算机要处理的信息是多种多样的，如十进制数、文字、符号、图形、音频、视频等，这些信息在人们的眼里是不同的。但对于计算机来说，它们在存储中都是一样的，都是以二进制的形式来表示。

内存条是一个非常精密的部件，包含了上亿个电子元器件，它们很小，达到了纳米级别。这些元器件，实际上就是电路；电路的电压会变化，要么是 0V，要么是 5V，只有这两种电压。5V 是通电，用1来表示，0V 是断电，用0来表示。所以，一个元器件有2种状态，0 或者 1。

我们通过电路来控制这些元器件的通断电，会得到很多0、1的组合。例如，8个元器件有 28=256 种不同的组合，16个元器件有 216=65536 种不同的组合。虽然一个元器件只能表示2个数值，但是多个结合起来就可以表示很多数值了。

我们可以给每一种组合赋予特定的含义，例如，可以分别用 1101000、00011100、11111111、00000000、01010101、10101010 来表示 C、语、言、中、文、网 这几个字，那么结合起来 1101000 00011100 11111111 00000000 01010101 10101010 就表示”C语言中文网“。

一般情况下我们不一个一个的使用元器件，而是将8个元器件看做一个单位，即使表示很小的数，例如 1，也需要8个，也就是 00000001。

1个元器件称为1比特（Bit）或1位，8个元器件称为1字节（Byte），那么16个元器件就是2Byte，32个就是4Byte，以此类推： 8×1024个元器件就是1024Byte，简写为1KB； 8×1024×1024个元器件就是1024KB，简写为1MB； 8×1024×1024×1024个元器件就是1024MB，简写为1GB。

现在，你知道1GB的内存有多少个元器件了吧。我们通常所说的文件大小是多少KB、多少MB，就是这个意思。

单位换算： 8 Bit = 1Byte 1024Byte = 1KB 1024KB = 1MB 1024MB = 1GB 1024GB = 1TB

你看，在内存中没有abc这样的字符，也没有gif、jpg这样的图片，只有0和1两个数字，计算机也只认识0和1。所以，计算机使用二进制，而不是我们熟悉的十进制，写入内存中的数据，都会被转换成0和1的组合。

## 二进制和十进制的转换

![](http://ossp.pengjunjie.com/mweb/15904620255118.jpg)

## 二进制和八进制的转换

![](http://ossp.pengjunjie.com/mweb/15904621412138.jpg)

## 二进制和十六进制的转换

![](http://ossp.pengjunjie.com/mweb/15904623510301.jpg)

## 八进制和十六进制的意义？

## 二进制表示图

![](http://ossp.pengjunjie.com/mweb/15904621854577.jpg)

## 应用

1. 二进制
   1. 存储
   2. 计算——移位运算
2. 十进制
   1. 人计算
3. 八进制
   1. 部分编程语言的字节
4. 十六进制
   1. 颜色表示
   2. 字符表示
   3. 

IP地址

