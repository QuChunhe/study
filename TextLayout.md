
https://adobe-type-tools.github.io/font-tech-notes

标点

半角符号就是只占一个字符的符号

全角符号，顾名思义，是指占两个字符的符号


GB/T15834—201 

末点号
用于句末的点号,表示句末停顿和句子的语气。包括句号、问号、叹号。
3.1.2 句内点号
用于句内的点号,表示句内各种不同性质的停顿。包括逗号、顿号、分号、冒号。


标号的作用是标明,主要标示某些成分(主要是词语)的特定性质和作用。包括引号、括号、破折号、
省略号、着重号、连接号、间隔号、书名号、专名号、分隔号。

句号、问号、叹号。
逗号、顿号、分号、冒号
引号、括号、破折号、省略号、着重号、连接号、间隔号、书名号、专名号、分隔号

https://www.editage.cn/insights/xie-lun-wen-zhe-san-ge-duan-heng-yong-dui-le-ma-5522



# Terms

标点悬挂

「连字处理和两端对齐」（Hyphenation and Justification，常简称为 H&J 处理）

[中文排版的最大迷思——标点悬挂](https://www.sohu.com/a/205635196_204906)

《标点符号用法》（GB/T 15834—2011）有明确规定“5.1.10 标点符号排在一行末尾时，若为全角字符则应占半角字符的宽度（即半个字位置），以使视觉效果更美观。” 

[Requirements for Chinese Text Layout中文排版需求](https://www.w3.org/TR/clreq/)

版心

* 上边距
* 下边距
* 左边距
* 右边距

版心上边缘距离纸张上边缘（称为天头或上白边）

版心左边缘距离纸张左边缘（称为订口或左白边）为28 mm，右白边为26 mm 。

版面它涵盖了版心、书眉、中缝和页码等元素，以及边白部分。版心是书刊版面上专门用来容纳文字的空间，通常不包含书眉、中缝和页码，

Bézier [bezje]

* typesetting/typeset 　排版
* layout 布局/版式
* typography 字体排印
* manuscript 手稿，原稿
* typewriter 打字机
* typeface    。 A typeface is a particular set of glyphs or sorts (an alphabet and its corresponding accessories such as numerals and punctuation) that share a common design. 所谓Typeface指的是一组具有相同设计风格的字形的集合，通常这个集合可以是一套字母表和一些符号、数字。也就是说typeface 得是一套文字，而且这一套字都是用同一种风格或者艺术形式写出来的，微软的“华文行楷”就是一个typeface, 里面的所有字都是看起来“笔走龙蛇”的风格。Helvetica (黑体)也是很有名的typeface。
* type
* glyph 字形。字形是可识别的具体图形符号，用于代表一个或者多个字符，即字形是代表字符的可视化图形，用于展示和印刷等用途，而字符是字形所代表的抽象含义。
* font。字型，指某套具有同样样式、尺寸的字形
* character 字符。 numeric code representing an abstract symbol according to some defined character encoding rule. 根据某种预先定义的对应规则，通过数字来表示抽象的、具有特定含义的符号。在计算机科学中，字符是文本的基本单位，每个字符在计算机内部都是用数字来表示，字符与数字之间的对应关系被称为字符编码（Character Encoding）。字符集（Character Set）是指字符的集合，在同一个字符集中不同的字符对应不同的数字。

码点（Code Point）：有些地方翻译为码值或内码。是指在某个字符集中，根据某种编码规则将字符编码后得到的值。比如在ASCII字符集中，字母A经过ASCII编码得到的值是65，那么65就是字符A在ASCII字符集中的码点。

Unicode引入了码点的概念。这个标准为每个字符分配一个码点，共计1114112个码点。针对于Unicode最流行的编码是UTF-8，其将每个码点编码为一到四个字节。

伴随着Unicode，OpenType字体被引入。针对于选出的Unicode码点，一个OpenType字体包含字形

英文的“Typeface”实际就是指“Font Family”(字体家族)，例如：“HanaMinB”；而“Font”则是“Typeface”的子集，也就是某个“Subfamily”（风格或字重）的单一“Font”

中国大陆地区，“Typeface”翻译成“书体”；“Font”成翻译“字体”；

港澳台地区，“Typeface”翻译成“書體”；“Font”成翻译“字型”。

glyph 字形，character 字符

Typeface—— a design of the letterform. (song)Font——a delivery system of the design. (MP3/cell phone)我的理解是，把typeface作为一个初始设计，而font作为一个承载设计的载体（上面也有人说到了，font最初来源应该和punches压膜倒模字体有关），就像是有一首歌，这首歌本身是typeface，也就是原始数据，而如果你想要听歌的话，就需要把歌放到MP3或者手机里面来听，那这时候typeface就变成了font



Typography字体排印学，或字体排印，又称“文字设计”，是一种涉及对字体、字号、缩进、行间距、字符间距进行设计、安排等方法来进行排版的一种工艺。

Typography(字体排印学)不仅包括“字体设计”，同时也涉及其它与“字”相关的设计，个人认为可以分为三大块
* 字体 (typeface)
* 排版
* 大小

typeface 和 font 分别被翻译为 “字体” 和 “字型”.

ligatures 连字 是叫“合字”，有些字体里面当 字母f 和 字母i 连在一起的时候， f 的一横会跟 i 的一点撞上，导致不好排版。 所以为了方便、美观，有些字体直接会有 fi 连字的字模。在 OpenType 字体格式出现后，字体开发者可以在字体中定义连字。OpenType 格式的字体可以设置一个 字符替换表（GSUB - The Glyph Substitution Table） 来指定哪些字符的组合会被替换成其它字符。

escape character 逃逸字符
* control word
* control symbol

>> LaTeX is usually pronounced /ˈlɑːtɛk/ or /ˈleɪtɛk/ in English (that is, not with the /ks/ pronunciation English speakers normally associate with X, but with a /k/). The characters T, E, X in the name come from capital Greek letters tau, epsilon, and chi, as the name of TeX derives from the Greek: τέχνη (skill, art, technique); for this reason, TeX's creator Donald Knuth promotes a pronunciation of /ˈtɛx/ (tekh) (that is, with a voiceless velar fricative as in Modern Greek, similar to the last sound of the German word "Bach", the Spanish "j" sound, or as ch in loch). Lamport, on the other hand, has said he does not favor or discourage any pronunciation for LaTeX.





点单位是一种度量单位，通常用于设计和字体大小设置。

我们知道 1 英寸 = 96 像素，1 英寸 = 72 点，所以 96 像素 = 72 点！由此，我们有这个等式：

1 点 = 0.75 * 像素

字号就是字体大小，通常在网页端使用px作为字号的单位。移动端兴起后，ios字体单位是pt，Android是sp。


dpi和ppi这两个是密度单位，不是度量单位，而这两个恰恰是我们换算中重要的分母。简单理解一下：

PPI (pixels per inch)：图像分辨率,在图像中，每英寸所包含的像素数目

DPI (dots per inch)： 打印分辨率 ,每英寸所能打印的点数，即打印精度）

dpi主要应用于输出，重点是打印设备上。

PPI是图像分辨率，DPI是打印分辨率


全角是指一个字符占用两个标准字符的位置。中文字符、全角的英文字符、国标GB2312-1980中的图形符号、特殊符号都是全角字符。半角是指一个字符占用一个标准字符的位置。


[探究fontsize与字体height关系](https://juejin.cn/post/7065705281640103966)

line-height行高=fontsize+行距


* 顶线： 文字顶部对齐的线 Ascender
* 中线： 文字中部的画线 
* 基线： 英文字母下端沿线 baseline
* 底线： 文字底部对齐的线 descender






incremental parsing

incremental layouting

a comprehensive caching scheme that aims to retain and reuse results at every layer of a layout tree is proposed

full justification： 两端对齐

indent 缩进

kerning

ragged right 左对齐

[CID vs GID](https://ccjktype.fonts.adobe.com/2012/04/cid-vs-gid.html)

[Adobe CMap and CIDFont Files Specification](https://pdfa.org/wp-content/uploads/2020/07/5014.CIDFont_Spec.pdf)

[字形的度量](https://zhuanlan.zhihu.com/p/364605349)

[字体基础知识](https://www.jianshu.com/p/b788f7b188f8)

[字面到底是什么？曝光字体设计中那些鲜为人知的细节！](https://zhuanlan.zhihu.com/p/28959063)

[Different Font File Types Explained (OTF, TTF, WOFF)](https://design.tutsplus.com/articles/different-font-file-types-explained-ott-ttf-woff--cms-39047)

字体

字号

字面：指字体所占字面框的字面率比例大小

字面框

字身框

字身和字面的概念来自金属活字type face，在金属活字上，字面部分就是凸起的字，铅模外框则是自身。对的，现在字体设计中的自身框、字面框正是由这里演化而来。

字身框和字面框之间的差值距离是半个自然字距的原因

字距＝（字身框－字面框）＊２

字体设计大师谢培元老师总结的“第二中心线”理论也表明，只要测量形旁和声旁这两个部件的中心距离就可以得到相应的字面大小值。

如果把字面形状按照视觉习惯归类为规则的几何图形，我们可以大致把汉字归纳为方形、圆形、三角形和菱形4种典型形状，针对这四种类型作相应处理，就能做到字体在视觉上字面保持一致。

字重就是指字体笔画的粗细，而Light、Regular、Heavy等表明了字体粗细的程度。

字重的英文为Weight，简称为W，国际标准 ISO规定了字重的9种级别，由细到粗依次用W1、W2等等来区别，并用相应的英文ExtraLight、Light等等标识。
* W0: not applicable 不用
* W1: Ultra light. 特细(lowest ratio of glyph stem width to font height)　
* W2: Extra light　非常细
* W3: light　　细
* W4: semilight　稍细
* W5: medium　中等
* W6: semi bold　半粗
* W7: bold　粗
* W8: extra bold　非常粗
* W9: Ultra bold. 特粗　(highest ratio of glyph stem width to font height)

常见到了这样的字重等级：Thin、Light、Regular、Book、Bold、Black、Heavy，通常的简写就用各自英文的首字母。


These font format types are essential for designers to know: 
* Bitmapped or raster fonts 位图字体: each character is made out of pixels. While these fonts are faster for computers to display, they are not scalable. This means that a separate font is needed for each size and style. 
* Vector fonts or scalable fonts 矢量字体: each character is made out of an outline, and this allows for the font to be scalable. This means that a single font file can be used for any point size. It only needs additional code to render the font to a desired size. 



![字体排印的术语](pics/LayoutTerms.png)


There are two basic ones: the height of the type, called the body size, and the width of the metal type sort for each character, called its set-width.

字型术语

Baseline基线:字体排印学中，基线（英语：Baseline）指的是多数字母排列的基准线。如上图所示，大多字母都沿着红色基线排列，唯有“p”向下延伸超过基线，超过的部分称为降部。

ascent升部高： ascender升部是字形位于基线之上部分，其高度被称为升部高，通常用正数表示

descent降部高：descenter降部是字形位于基线以下部分的高度，其高度被称为升部高，通常用负数表示

height 高度，ascent - descent

advance是基线上最左边的idan到最由边点直接的距离

Meanline主线:英语为Mean Line，也称英语：Waist Line，指的是决定无升部的小写字母字体大小的一条线，其与基线的距离称为x字高。

Cap-Height大写高度:大写字高（英语：Cap height）是指某种字体中，位于基线（baseline）以上的大写字母的高度。尤其指相对平顺的字母“H”和“I”的高度。因为圆型的字母“O”和尖形字母“A”等，在设计中为保持视觉观感，其高度会有上下浮动（Overshoot）。而小写字母字高，指的就是X字高。

X-Height（x 字高）:是指字母的基本高度，精确地说，就是基线（英语：baseline）和主线之间的距离。特别的，它指称一个字体中小写字母x的高度（这也是这个词的语源），而实际上这也和字母a、c、e、m、n、o、r、s、u、v、w和z的高度是一样的。尽管如此，在现代字体设计领域里，x字高代表了一个字体的设计因素，因此在一些场合，字母x本身并不完全等于x字高。



Serif衬线:衬线体指的是有衬线的字体，又称为有衬线体、衬线字、曲线描边字，俗称白体字；而与之相对的，没有衬线的称为无衬线体、无描边字，俗称黑体字。衬线指的是字形笔画末端的装饰细节部分。无衬线字体在西文中习惯称sans-serif，其中sans为法语的“无”的意思；而另外一些人习惯把无衬线体称grotesque（德语作grotesk）或“哥特体”，把衬线体称为“罗马体”，但是这些词已经不是很常用了，只保留于字体名称中。


Stem躯干:字体中垂直的主要驱杆

COUNTER封闭区:counter指的就是q, p, b, d, Q, O,o 等字中間的圓型封閉區域


ARM:图中T顶部的伸展称为arm

Beak:图中T端部勾回的部分称为beak(鸟嘴)

Tail是一种下伸笔画，通常指字母下端一些装饰性的笔触

Ear:图中g顶部突出的部分

Terminal:看起来像衬线，泛指没有实际衬线的端部。

Aperture可以理解为圆的一部分，不封闭的圈（强行解释）

Bowl碗状曲线

排版术语

line gap（


Leading行距:字体连续行的基线间的纵向距离。个术语最早起源于手工排版时代，当时为了增大行间的垂直距离需要在行间插入薄铅条
![pics/leading.jpg](leading示意图)



Kerning字距，字间距:就是具体的字符与字符之间的空隙。和字宽不同，因为每个字母之间都有不同的间距，所以最终排印出来的单词，会有多种不同的效果。理論上kerning在fixed-width font上並不需要。

tracking字宽，字宽距离，就是一个单词所有字符占用的整体空间，有时候也称作字宽。大多数的程序都允许你缩小或加大字宽，即整个单词所有字符都伸缩。



* GLYPH（字形）:字型中对于同一个字母可能提供多种字形



英文字体有基线（baseline）和中线（meanline），这两条线之间就是所谓的“x-height”，即小写字母x的高度。基线之上的部分是上伸区域（ascent），基线之下的部分是下伸区域（descent）。小写字母超过中线之上的部分（如d上面的竖划）称字母的上伸部分（ascender），超过基线之下的部分（如字母q下面的竖划）称字母的下伸部分（descender）。英文大写字母都位于基线以上，顶部稍低于小写字母上伸部分的顶线1。

[关于字体、排版设计，有什么好的书籍推荐？](https://www.zhihu.com/question/23778954/answer/2603926735)

字体排印 (Typography) 和字体设计 (Type Design) 


[字体术语集](https://zhuanlan.zhihu.com/p/136840798)

[字形的度量](https://zhuanlan.zhihu.com/p/364605349)


Raster Image即光栅图像，也叫位图、点阵图、像素图。raster display则是通过二维像素数组展示图像。像素即pixel，它是“picture element”的缩写。举个例子就是平常的电视，他们含有二维数组的小像素点，这些像素点可以独立地设置不同颜色以创造任何图像。很多打印机，比如激光打印机、喷墨打印机等也是光栅设备（raster devices）。



Type 0 fonts : composite fonts, 其他类型被称为simple fonts。

pdf支持两类字体相关的对象，分别成为CIDFonts和CMaps。

# Books


1. Fonts & Encodings by Yannis Haralambous, 1039页。这本书涵盖的是编码和字体技术，对于前者，其实还是漏了几种较为罕见的编码，但无所谓了。对于字体技术的，文后涉及了大量工具的使用，包括写PostScript代码。但是值得说的一点是，这书要想完全消化是很难的事。

2. CJKV Information Processing by Ken Lunde, 899页。这个书讲了大量汉字处理的技术细节，不过值得注意的是这本书有一些内容已经算是过时了。对于这些技术细节，在现有的一些软件里面实现的其实也不是很好，很多西方的程序员没有汉字的使用经验，所以这本书对于这些程序员来说，有价值，但是很低。

3. PostScript Language Reference, third edition, 913页。PostScript这种语言呢，是制作字体的基础，所有的曲线都是要画出来的，所以这种语言是肯定要懂的。就一般的开发来讲，手写PostScript是很痛苦的，一般都是通过C/Python生成的。

4. PDF Reference, sixth edition, 1310页。这个PDF呢，写过Quartz程序的，应该会了解，写界面就是在写PDF。PDF本身是作为PostScript的一个子集存在的，但是现如今的PDF和PostScript的关联度就不是太大了。PDF技术，涉及到的是字体的拆分、解析。而排版，则需要控制坐标。所以，如果觉得字体技术和排版技术足够的话，可以写一个PDF试试，这里面有足够的东西检验你的技能。

5. The TeXbook by D. E. Knuth, 494页。这个是我们TeX圈子里面一定要看的一本书。但是这本书能够启发的，并不仅限于TeX。关注点应该在：排版模型，断行模型和切词模型。

6. The METAFONT book，374页。和PostScript不同，METAFONT的编程语言是Algol系，所以在写东西的时候是比较舒服的。这本书面向的是做字体制作支持的人，因为设计师不懂编程是一个大概率事件。如果说METAFONT过时，它的shiping out模块是过时的，将这个模块换成PostScript输出模块，这可以说是个革命了。

GB/T 15834—2011《标点符号用法》


# PDF


PDF is used wherever the exact presentation of the content is important (for examplefor a print advertisement or book). It isn’t normally suitable when the content is to be layed out or reflowed at the last moment, such as in a variable width web page—languages like HTML and CSS which separate content from presentation are more suitable in those circumstances.
PDF被用于那些内容的精确呈现至关重要的场合（例如广告或书籍的印刷）。它通常不适合在最后一刻进行内容布局或重新布局的情况，例如，在可变宽度的网页中——像HTML和CSS将内容与呈现分离的语言更为适用这些情况。

五种图元
* Path object: straight lines, rectangles, and cubic Bezier
* Text object: character strings
* external object (XObject):在内容流之外定义的一个对象，通过命名资源引用。
   * form XObject:完整的内容流，被当作一个单一的图元
   * transparency groups
* inline image object
* shading object

transparency group

table 147
* S: subtype
* CS: colour space
* I: isolated. Isolated Groups
* K: knockout groups


绘制对象（paints objects）
* 填充（fills）
* 画笔（strokes）
* 文本（text）
* 图像（images）

采集路径和透明度

blend model


小写表示标量，大写表示向量
* C： color
* f： form factor
* q： opaqueness

result colour是source colour和backdrop colour的函数。

两个参数 alpha（其控制背景颜色和原始颜色的相对贡献）和blend function

包含在一个组中的图元被看作相互分离的透明栈，被称为组栈。


** 坐标系统

PDF 1.6中引入了3D坐标系统。

坐标系统的三个属性
* 原点的位置
* x和y轴的方向
* 每个坐标轴的单位长度


device space:设备空间


* 72-pixel-per-inch display
* 600-dot-inch printer

点单位是一种度量单位，通常用于设计和字体大小设置。一张图片的打印出来的实际尺寸是由电子图片的像素和分辨率共同决定的，像素（Pixel）是指构成图片的小色点，分辨率（单位 DPI）是指每英寸（Inch）上的像素数量，可以看做是这些小色点的分布密度。像素相同时，分辨率越高则像素密度越大，实际打印尺寸越小，图像也越清晰。

user space: 独立于设备的坐标系统，称为用户空间

通过CropBox指定了在用户空间中可见的、用于输出媒体的长方形区域， 

默认的用户空间
*左下角，
* x向右，y向上
* 单位是1/72 inch


Current Transformation Matrix：CTM， cm操作符

Text space： text matrix

glyph space： font matrix

image space:宽为w，高为h的图像，定义左上角为坐标原点，并且x和y坐标分别向左从0到我和向下从0到h。图像空间与用户空间之前的对应关系是恒定的，用户空间对应于用户坐标(0,0)和(1，1)的一个单位正方形，对应于上面的图像空间图像边界。在用户空间种坐标(0,0)位于正方形的左下角，对应于图像空间的坐标(0,h)

XObject： form matrix

Patter： pattern matrix

仿射变换满足结合律，不满足交换律，不能改变操作的顺序

为了理解坐标变化的数学，非常关键的是需要记下如下两点
* 变换更改的是坐标系统，而不是图元对象。
* 变换矩阵定义了从新坐标系统到原始坐标系统的变换。在等式中x和y表示在变换坐标系统种的坐标值，而x'和y'表示在未变换坐标系统种的坐标。


* marked-content point: MP  DP
* marked-contend sequence : MBC  BDC EMC

将被标记的内容视为一个相关的对象集合，作为一组被当作一个单一的对象被处理。


marked clipping sequence

Marked-content Sequences as content items

 marked content ID (MCID)

https://blog.idrsolutions.com/what-is-marked-content/

https://developer.apple.com/library/archive/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_pdf_scan/dq_pdf_scan.html

Optional Content Groups (OCG)


Optional Content Membership Dictionalries (OCMD)




## Text

typography 排版/排印
* character
* glyph : 
* font: 

Glyphs are organized into fonts. A font defines glyphs for a particular character set.

类型
Type 0：A composite font, a font composed of glyphs from a descendant CIDFont. 

A font is a container for glyphs.


ligature


text matrix -- text space

glyph space：从glyph空间到text空间的变换是通过font矩阵来定义的。 对于大多数类型的字体。，这个矩阵应该预先定义，将glyph空间的1000单元映射到text空间的1个单位。对于Type 3字体，font matrix应该明确在font字典中给出。

Tm： 文本矩阵（text matrix
Tlm：文本行矩阵


# OFD

页面中的所有图元都在坐标空间内进行描述,一个坐标空间包括坐标原点、坐标轴方向、坐标单位长度三个要素。坐标空间根据用途不同分为设备空间、页面空间、对象空间三类。不同的坐标空间之间通过平移、缩放、旋转、切变进行变换。

图元对象使用其外接矩形属性确定在页面或其他容器中的绘制位置。图元对象的内部数据,包括路径数据和裁剪区数据,都以外接矩形的左上角为坐标原点,X 轴向右增长,Y 轴向下增长,并采用毫米为单位,这样的局部坐标空间就称为对象空间。绘制图元时,应首先通过外接矩形参数平移到对象空间内,在对象空间内根据变换矩阵和裁剪设置进行相应绘制。

# PDFBox

是否Italic
```java
if (!doesRotate && !fontDescriptor.isItalic()
                        && (textMatrix.getShearX() > 0 || fontName.contains("italic"))) {
                    $textObj.setItalic(true);
                }
```

```java
private double computeWidth(PDFont font, int code) throws IOException {
        if (font instanceof PDType0Font) {
            PDCIDFont cidFont = ((PDType0Font) font).getDescendantFont();
            Rectangle bbox = cidFont.getNormalizedPath(code).getBounds();
            return bbox.getMaxX();
        } else if (font instanceof PDType1CFont) {
            PDType1CFont pdType1CFont = (PDType1CFont)font;
            if (pdType1CFont.hasGlyph(code)) {
                Rectangle bbox = pdType1CFont.getPath(code).getBounds();
                return bbox.getMaxX();
            }
        } else if (font instanceof PDType3Font) {
            PDType3Font pdType3Font = (PDType3Font) font;
            PDType3CharProc charProc = pdType3Font.getCharProc(code);
            if (charProc != null) {
                BoundingBox fontBBox = pdType3Font.getBoundingBox();
                PDRectangle glyphBBox = charProc.getGlyphBBox();
                if (glyphBBox != null) {
                    // PDFBOX-3850: glyph bbox could be larger than the font bbox
                    return min(fontBBox.getWidth(), glyphBBox.getWidth());
                }
            }
        }
        return font.getWidth(code);
    }
```


```java
    private Pair<Double, Double> computeAscentAndDescent(PDFont font, int code) throws IOException {
        if (font instanceof PDType0Font) {
            PDCIDFont cidFont = ((PDType0Font) font).getDescendantFont();
            Rectangle bbox = cidFont.getNormalizedPath(code).getBounds();
            return Pair.of(bbox.getMinY(), bbox.getMaxY());
        } else if (font instanceof PDType1CFont) {
            PDType1CFont pdType1CFont = (PDType1CFont)font;
            if (pdType1CFont.hasGlyph(code)) {
                Rectangle bbox = pdType1CFont.getPath(code).getBounds();
                return Pair.of(bbox.getMinY(), bbox.getMaxY());
            }
        } else if (font instanceof PDType3Font) {
            PDType3Font pdType3Font = (PDType3Font) font;
            PDType3CharProc charProc = pdType3Font.getCharProc(code);
            if (charProc != null) {
                BoundingBox fontBBox = pdType3Font.getBoundingBox();
                PDRectangle glyphBBox = charProc.getGlyphBBox();
                if (glyphBBox != null) {
                    // PDFBOX-3850: glyph bbox could be larger than the font bbox
                    return Pair.of(
                            max(fontBBox.getLowerLeftY(), glyphBBox.getLowerLeftY()),
                            min(fontBBox.getUpperRightY(), glyphBBox.getUpperRightY()));
                }
            }
        }
        PDFontDescriptor fontDescriptor = font.getFontDescriptor();
        double ascent = fontDescriptor.getAscent();
        double descent = fontDescriptor.getDescent();
        if (isZero(ascent) && isZero(descent)) {
            BoundingBox bbox = font.getBoundingBox();
            return Pair.of((double) bbox.getLowerLeftY(), (double) bbox.getUpperRightY());
        }
        TrueTypeFont ttf = getTrueTypeFont(font);
        if (ttf != null) {
            return Pair.of(
                    1000d * ttf.getHorizontalHeader().getDescender() / ttf.getUnitsPerEm(),
                    1000d * ttf.getHorizontalHeader().getAscender() / ttf.getUnitsPerEm());
        }
        return Pair.of(descent, ascent);
    }

```


typesetting
* Arraging Content on a Page: a）文字 页->段->句->行；b）图表