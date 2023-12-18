OFD 全称叫做 Open Fixed-layout Document

https://gitee.com/gblfy/ofd-pdf/tree/master


https://sspai.com/post/61716

此外，在印刷流程中，最终页面通常是从更大的印张中切割得来的。由于切割工序不可能完全精确，设计版面时一般都会作「出血」处理，即有意让底色、背景图片等元素向实际尺寸外「溢出」几毫米，以确保经过切割后，背景元素能延伸到纸张边缘而不留下白边。上述流程中，页面内容向外延伸到的边界就是 「出血框」（bleed box），而经过裁切后的预期尺寸就是 「裁切框」（trim box）了


为了处理这些情形，一个 PDF 页面可以定义至多五个不同的边界来控制成像流程的不同方面：
* 媒体框（media box）定义将用于印刷页面的物理介质的边界。它可以包括最终页面外围、用于出血或打印标记等目的的任何延伸区域。它也可以包括靠近介质边缘，但因为输出设备的物理限制而无法标记的区域。丢弃落在媒体框之外的内容是安全的，不会影响 PDF 文件的含义。
 * 裁剪框（crop box）定义页面内容在显示或打印时将被裁剪到的区域。与其他边框不同，裁剪框不定义物理页面的几何形状，也不定义预期用途，仅仅是对页面内容作出裁剪。然而，在没有额外信息（例如在 JDF 或 PJTF 格式作业传票文件中指定的拼版指令）时，裁剪框决定了页面内容在输出介质上的排放方式。裁剪框的默认值与媒体框相同。
* 出血框（bleed box，PDF 1.3 起支持）定义页面内容在印刷环境中输出时应被裁剪到的区域。该区域可能包括任何为适应切割、折叠、裁切设备的物理限制所需的额外出血区域。实际印出的页面可能包含落在出血框之外的打印标记。出血框的默认值与裁剪框相同。
* 裁切框（trim box，PDF 1.3 起支持）定义最终页面在经过裁切后的预期尺寸。该边框可能小于媒体框，以容纳印刷相关的内容，如打印指示、裁切标记、印刷测控条（color bar）等。裁切框的默认值与裁剪框相同。
* 作品框（art box，PDF 1.3 起支持）定义页面上、根据作者意图有意义内容的范围（包括可能存在的留白）。作品框的默认值与裁剪框相同。


A PDF file is structured as a tree of low-level objects, called Cos objects. Cos objects form all PDF document components, such as bookmarks, pages, fonts, images, and annotations. The Acrobat core API contains methods (the Cos layer) that enable you to operate directly on these low-level object.


In addition to basic data types such as integer, fixed, and Boolean values, Cos objects also contain the following object types:
* Array
* Dictionary
* Name
* String
* Stream

一个简单有效的PDF文件按顺序包含四个部分:
* header，提供PDF版本号
* body 包含页面，图形内容和大部分辅助信息的主体，全部编码为一系列对象。
* 交叉引用表，列出文件中每个对象的位置便于随机访问。
* trailer包括trailer字典，它有助于找到文件的每个部分， 并列出可以在不处理整个文件的情况下读取的各种元数据。


流用于存储二进制数据。它们由字典和一大块二进制数据组成。 字典根据流所放置的特定用途列出数据的长度，以及可选的其他参数。

从语法上讲，流由字典组成，后跟stream关键字， 换行符（<LF>或<CR> <LF>），零个或多个字节的数据， 另一个换行符，最后是endstream关键字。

内容流由一系列运算符组成，每个运算符前面都有零个或多个操作数


依照顺序，根据操作符和操作数，来渲染。

pdf中坐标原点时以页面左下角为坐标原点，向右为x轴正方向，向上为y轴正方向 pdf中的时像素密度。


pdf是由一个或者多个由/Contents定义的内容流组成，以及一个由/Resources定义的共享资源集合

odf是以页面的左上角为坐标原点，向右为x轴正方向，向下为y轴正方向，以mm为单位，旋转角度的理解，比如旋转345度的含义


页面空间规定页面的左上角为原点,X 轴向右增长,Y 轴向下增长,以毫米为单位。整个页面空间的大小由 PageArea节点(见7.5文档根节点)中的 PhysicalBox确定

https://blog.csdn.net/li_tengfei/article/details/6098093

Cap数 	含义
* 0 	对接帽。在线的尽头摆平
* 1 	圆帽。每条线末端附有半圆形
* 2 	投射方帽。在线末端的项目为线宽的一半，然后平


DashPattern指定虚线的线段和间隔长度,有两个或多个值,其中第一个值指定了虚线线段的长
度,第二个值指定了线段间隔的长度,以此类推


1. Designer 
https://designer.microsoft.com
2. Copilot
https://github.com/features/copilot/
3. Azure Speech Studio
https://azure.microsoft.com/zh-cn/free/cognitive-services/
4. VALL-E (目前尚未开放，GitHub已开源)
https://valle-demo.github.io/


cm运算符有六个参数，表示要与CTM组成的矩阵。以下是基本的变换：
* 从起始点 (0, 0) 向 (0+dx, 0+dy) 平移可由 1, 0, 0, 1, dx, dy 六个参数指定
* 长宽由 (1, 1) 缩放至 (sx, sy) 可由 sx, 0, 0, sy, 0, 0 六个参数指定
* 围绕 (0, 0) 逆时针旋转 x 弧度可以由 cos x, sin x, -sin x, cos x, 0, 0 六个参数指定

ST_Box矩形区域,以空格分割,前两个值代表了该矩形的左上角的坐标,后两个值依次表示该矩形的宽和高,可以是整数或者浮点数,后两个值应大于0

# OFD

文件OFD.xml
OFD.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ofd:OFD Version="1.0" DocType="OFD" xmlns:ofd="http://www.ofdspec.org/2016">
  <ofd:DocBody>
    <ofd:DocInfo>
      <ofd:DocID>f5f666fd1be2459587a66a237783c86c</ofd:DocID>
      <ofd:Author>SoWise</ofd:Author>
      <ofd:CreationDate>11/29/2023 9:30:20 AM</ofd:CreationDate>
      <ofd:Creator>SoWise</ofd:Creator>
      <ofd:Keywords>
        <ofd:Keyword>
        </ofd:Keyword>
      </ofd:Keywords>
      <ofd:Subject>
      </ofd:Subject>
      <ofd:ModDate>1/1/0001 12:00:00 AM</ofd:ModDate>
      <ofd:Title>
      </ofd:Title>
    </ofd:DocInfo>
    <ofd:DocRoot>Doc_0/Document.xml</ofd:DocRoot>
  </ofd:DocBody>
</ofd:OFD>
```

Doc_0/Document.xml


Page 表 11 创建参数 ST_ID ST_Loc  保存位置 "Pages/Page_%d/Content.xml"

ofd页面区域
* BleedBox： 出血区域
* PhysicalBox：页面物理区域
* ApplicationBox：显示区域
* ContentBox：版心区域

pdf页面区域
* Media Box
* Bleed Box
* Trim Box
* Art Box


pdf两种方式
* PDFGraphicsStreamEngine
* PageDrawer

CT_Layer的type
* Body 正文层
* Foreground 前景层
* Background 背景层


graphics2d为中介实现到ofd的转换

借助标准Graphics2D接口可以复用现有的各类格式文件转换库的转换代码，实现其他类型文件或格式转换为OFD文件.


* Path2D Shape 故名思意就是无数个点连接起来形成的轨迹，这个路径中还包括起点信息、终点信息，方向信息，构造2D图形的一个路径，即一个构造过程
* Graphics2D

PDF文件格式的目的是为了生成所期望的、可视化的打印效果，而它不是为了解析内容。因此，PDF文件不包含语义层。

档中的每一个字符都可以被定位在页面上的某个位置

三类操作
* Shape operations
* Text Operations
* Image operations

基于栈的操作，包括操作数和操作符

ofd
* 图形
* 图像
* 文字
* 视频
* 符合对象




OFDPageDrawer -> drawImage

GeneralPath


字体Type1、TrueType和Type3

在PDF中，字体由字体字典组成， 字体字典定义度量，字符集和编码（将文本字符串中的字符代码映射到字体中的字符）， 以及字体程序（实际的字体文件），以各种格式（Type 1，TrueType等）。


font 是指一个成套的字体，而 glyph 则是文字中字母 (character) 的视觉表现。


Glyph（字形）和 font（字型）


 

221  QDCOYR+txexa

No Unicode mapping for iintegdisplay (34) in font QDCOYR+txexa

showFontGlyph  showGlyph


dash 

As you’re defining your dash and gap sizes, Illustrator will also decide what is a corner.

页面中的所有图元都在坐标空间内进行描述,一个坐标空间包括坐标原点、坐标轴方向、坐标单位长度三个要素。坐标空间根据用途不同分为设备空间、页面空间、对象空间三类。不同的坐标空间之间通过平移、缩放、旋转、切变进行变换。


页面空间规定页面的左上角为原点,X 轴向右增长,Y 轴向下增长,以毫米为单位。整个页面空间的大小由 PageArea节点(见7.5文档根节点)中的 PhysicalBox确定。

缩放、平移、拉伸、旋转

放射变换（Affine Transformation）shear，scaling，rotation，flip，translation

| a b 0 |
| c d 0 |
| e f 1 | 

a – X轴缩放倍数 b – Y轴斜切系数 c – X轴斜切系数 d – Y轴缩放倍数 e – X偏移量（距原点） f – Y偏移量（距原点）

>>a is Scale_x
>>b is Shear_x
>>c is Shear_y
>>d is Scale_y
>>e is offset x
>>f is offset y

跟JDK提供的放射变换类AffineTransform有差异
       [ x']   [  m00  m01  m02  ] [ x ]   [ m00x + m01y + m02 ]
       [ y'] = [  m10  m11  m12  ] [ y ] = [ m10x + m11y + m12 ]
       [ 1 ]   [   0    0    1   ] [ 1 ]   [         1         ]



 Current Transformation Matrix (CTM).
* Translation by (dx, dy) is specified by 1, 0, 0, 1, dx, dy
* Scaling by (sx, sy) about (0, 0) is specified by sx, 0, 0, sy, 0, 0
* Rotating counterclockwise by x radians about (0, 0) is specified by cos x, sin x, -sin x, cos x, 0,

There are two matrices to consider:
* The text matrix, which defines the current transformation for the next glyph. It is altered by the text positioning and text showing operators.
* The text line matrix, which is the state of the text matrix at the beginning of the current line. Thus, lines of text may be aligned vertically by the use of an operator to move to the next line, without manually keeping track of the position of the start of the line

有两个矩阵需要考虑：
* 文本矩阵，定义下一个字形的当前转换。它由文本定位和显示运算符的文本改变。
* 文本行矩阵，它是当前行开头的文本矩阵的状态。因此，通过使用操作员移动到下一行，可以垂直对齐文本行，而无需手动跟踪行的开始位置。


剪切变换(shear transformation)是空间线性变换之一，是仿射变换的一种原始变换。它指的是类似于四边形不稳定性那种性质，方形变平行四边形


表示二维仿射变换，执行从2D坐标到其他2D坐标的线性映射，保持线的“直线性”和“平行性”。仿射变换可以使用平移、缩放、翻转、旋转和平移等序列来构造。

Standard14Fonts
* Times-Roman
* Times-Bold
* Time-Italic
* Time-BoldItalic
* Courier
* Courier
* Courier-Bold
* Courier-Oblique
* Helvetica®
* Helvetica®-Bold
* Helvetica®-Oblique
* Helvetica®-BoldOblique
* Symbol
* ZapfDingbats

Times New Roman Italic。

PDF规范中” base 14″字体的

The Java Platform distinguishes between two kinds of fonts: physical fonts and logical fonts.

采用的是一个开源的软件，但是目前发现了一些问题，已经修复了部分
1. 图片格式转换错误，将不同格式的图片都转换为了png。（已经解决）
2. 无法正常显示虚线显问题（已经解决）
3. 无法正常显示线端样式问题（已经解决）
4. pdf base 14字体显示出现问题（已经解决）。pdf中存在14个标准字体，这14个字体不会在pdf文件中包含对应的字体数据，需要从操作系统本地的字体文件读取，但是在windows下字体文件名称为Times New Roman Italic，而转换程序采用的名称是Times-Italic，从而出现异常。
5. 旋转后文字展示异常，现象包括一些公式错误、坐标图中纵轴说明问题错误


Times New Roman Italic

"Times-Italic"
```
生成字体文件异常:class org.apache.pdfbox.pdmodel.font.PDType1Font
```

pdf中存在14个标准字体，这14个字体不会在pdf文件中包含对应的字体数据，需要从操作系统本地的字体文件读取，但是在windows下字体文件名称为Times New Roman Italic，而转换程序采用的名称是Times-Italic，从而出现异常。

PDFBox 规范声明“标准的 14 种字体集将始终可用于处理 PDF 文档”。在 PDFBox 中，这 14 种字体集被定义为PDType1Font 类中的常量。字体是通过使用PDType1Font API从文件加载的。


现在发现两个问题
1. 图中文字显示异常，如上图所示
2. 有些公式显示异常，如下图所示
其中左图是原图，而右图是转换后的

在每个页面中以流的方式显示内容，采用为一个操作符和操作数。


```
ShowText.process(PDFStreamEngine context)
PDFStreamEngine.showTextString(byte[] string)
OFDPageDrawer.showText(byte[] string)
PDFStreamEngine.showText
OFDPageDrawer.showGlyph
```

ST_Box矩形区域,以空格分割,前两个值代表了该矩形的左上角的坐标,后两个值依次表示该矩形的宽和高,可以是整数或者浮点数,后两个值应大于0 “10 10 50 50"

```java
double cos = Math.cos(angle / Math.PI);
                double sin = Math.sin(angle / Math.PI);
                logger.error((textPosition.getX() / PX2MM) + "   " + ((double)textPosition.getY() / PX2MM));
                $textObj.setCTM(new ST_Array(cos, sin, -sin, cos, 0, 0));

  $textObj.setCTM(new ST_Array(
                    ctm.getScaleX(),
                    -1 * ctm.getShearY(),
                    -1 * ctm.getShearX(),
                    ctm.getScaleY(),
                    0,
                    0));  

```


```
pdftk.exe wlxb_23-20231313.pdf output wlxb_23-20231313_output.pdf uncompress
```



https://stackoverflow.com/questions/37862159/pdf-reading-via-pdfbox-in-java
```
12月 14, 2023 1:33:36 下午 org.apache.pdfbox.pdmodel.font.PDSimpleFont toUnicode
警告: No Unicode mapping for hatwide (98) in font HETNVE+CMEX10
12月 14, 2023 1:33:37 下午 org.apache.pdfbox.pdmodel.font.PDSimpleFont toUnicode
警告: No Unicode mapping for vextendsingle (12) in font HETNVE+CMEX10
12月 14, 2023 1:33:37 下午 org.apache.pdfbox.pdmodel.font.PDSimpleFont toUnicode
警告: No Unicode mapping for hatwide (98) in font EPJCTB+CMEX7
```

Current Transformation Matrix


字符存储
OFDCreator 
```java

OFDCreator 
```

PDF文件设计的是可以将字形和字符对应分离；
对于自定义字体，如果编码和标准编码不一样，想要获取字形对应的字符，就需要相应的Cmap（比如/ToUnicode），Cmap就好比密码本一样来映射字形对应的标准的UTF-8等编码。如果没有，或者缺少，或者错误，那么得到的字符就是乱码。


CMEX10