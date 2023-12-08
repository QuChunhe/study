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


页面空间规定页面的左上角为原点,X 轴向右增长,Y 轴向下增长,以毫米为单位。整个页面空间的大小由 PageArea节点(见7.5文档根节点)中的 PhysicalBox确定

https://blog.csdn.net/li_tengfei/article/details/6098093


1. Designer 
https://designer.microsoft.com
2. Copilot
https://github.com/features/copilot/
3. Azure Speech Studio
https://azure.microsoft.com/zh-cn/free/cognitive-services/
4. VALL-E (目前尚未开放，GitHub已开源)
https://valle-demo.github.io/


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


三类操作
* Shape operations
* Text Operations
* Image operations

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