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


1. Designer 
https://designer.microsoft.com
2. Copilot
https://github.com/features/copilot/
3. Azure Speech Studio
https://azure.microsoft.com/zh-cn/free/cognitive-services/
4. VALL-E (目前尚未开放，GitHub已开源)
https://valle-demo.github.io/