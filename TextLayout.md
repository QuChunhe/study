
Type 0 fonts : composite fonts, 其他类型被称为simple fonts。

pdf支持两类字体相关的对象，分别成为CIDFonts和CMaps。

P
cell  =
1 ∫ d3
rrρ r
r
()

[字形的度量](https://zhuanlan.zhihu.com/p/364605349)

[字体基础知识](https://www.jianshu.com/p/b788f7b188f8)

[字面到底是什么？曝光字体设计中那些鲜为人知的细节！](https://zhuanlan.zhihu.com/p/28959063)
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


Typography字体排印学，或字体排印，又称“文字设计”，是一种涉及对字体、字号、缩进、行间距、字符间距进行设计、安排等方法来进行排版的一种工艺。

Typography(字体排印学)不仅包括“字体设计”，同时也涉及其它与“字”相关的设计，个人认为可以分为三大块
* 字体 (typeface)
* 排版
* 大小

typeface 和 font 分别被翻译为 “字体” 和 “字型”

![字体排印的术语](pics/LayoutTerms.png)


There are two basic ones: the height of the type, called the body size, and the width of the metal type sort for each character, called its set-width.

字型术语

Baseline基线:字体排印学中，基线（英语：Baseline）指的是多数字母排列的基准线。如上图所示，大多字母都沿着红色基线排列，唯有“p”向下延伸超过基线，超过的部分称为降部。


Meanline主线:英语为Mean Line，也称英语：Waist Line，指的是决定无升部的小写字母字体大小的一条线，其与基线的距离称为x字高。

Cap-Height大写高度:大写字高（英语：Cap height）是指某种字体中，位于基线（baseline）以上的大写字母的高度。尤其指相对平顺的字母“H”和“I”的高度。因为圆型的字母“O”和尖形字母“A”等，在设计中为保持视觉观感，其高度会有上下浮动（Overshoot）。而小写字母字高，指的就是X字高。

X-Height（x 字高）:是指字母的基本高度，精确地说，就是基线（英语：baseline）和主线之间的距离。特别的，它指称一个字体中小写字母x的高度（这也是这个词的语源），而实际上这也和字母a、c、e、m、n、o、r、s、u、v、w和z的高度是一样的。尽管如此，在现代字体设计领域里，x字高代表了一个字体的设计因素，因此在一些场合，字母x本身并不完全等于x字高。

Ascender上伸笔画:上伸超出x字高的部分

Descender下伸笔画:下伸超出基线的部分

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

* Leading行距:字体连续行的基线间的距离。这个词起源于手工排版的年代，铅字之间通过插入铅块来增加垂直距离。

* GLYPH（字形）:字型中对于同一个字母可能提供多种字形
* Kerning字距，字间距:就是具体的字符与字符之间的空隙。和字宽不同，因为每个字母之间都有不同的间距，所以最终排印出来的单词，会有多种不同的效果。

* TRACKING字宽，字宽距离，就是一个单词所有字符占用的整体空间，有时候也称作字宽。大多数的程序都允许你缩小或加大字宽，这就取决于你的项目需求。


英文的“Typeface”实际就是指“Font Family”(字体家族)，例如：“HanaMinB”；而“Font”则是“Typeface”的子集，也就是某个“Subfamily”（风格或字重）的单一“Font”

中国大陆地区，“Typeface”翻译成“书体”；“Font”成翻译“字体”；

港澳台地区，“Typeface”翻译成“書體”；“Font”成翻译“字型”。

glyph 字形，character 字符

Typeface—— a design of the letterform. (song)Font——a delivery system of the design. (MP3/cell phone)我的理解是，把typeface作为一个初始设计，而font作为一个承载设计的载体（上面也有人说到了，font最初来源应该和punches压膜倒模字体有关），就像是有一首歌，这首歌本身是typeface，也就是原始数据，而如果你想要听歌的话，就需要把歌放到MP3或者手机里面来听，那这时候typeface就变成了font

[关于字体、排版设计，有什么好的书籍推荐？](https://www.zhihu.com/question/23778954/answer/2603926735)

字体排印 (Typography) 和字体设计 (Type Design) 


[字体术语集](https://zhuanlan.zhihu.com/p/136840798)

[字形的度量](https://zhuanlan.zhihu.com/p/364605349)


Raster Image即光栅图像，也叫位图、点阵图、像素图。raster display则是通过二维像素数组展示图像。像素即pixel，它是“picture element”的缩写。举个例子就是平常的电视，他们含有二维数组的小像素点，这些像素点可以独立地设置不同颜色以创造任何图像。很多打印机，比如激光打印机、喷墨打印机等也是光栅设备（raster devices）。


# PDF

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