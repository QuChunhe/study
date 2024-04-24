
LaTex的数学公式中插入中文
```
$$ P\{\mbox{拒绝} \mid H_{0} \mbox{为真}\} = \alpha $$
```

textstudio + MiKTex

[LaTeX org](https://latex.org)

中文 TEX 排版
* CCT → 最早支持简体中文的 TEX 扩展, 由张林波教授开发, 比较符合中国人的习惯和中国印刷界标准
* TY → 由华东师范大学肖刚、陈志杰等教授开发
* CJK → 由德国 Lemberg 开发，可以同时处理中、日、韩三国文字


CTEX 宏集 面向中文排版的通用 LATEX 排版框架, 中文排版首选!
* 英文排版建议: PDFLATEX 或 XeLATEX
* 中文排版建议: XeLATEX + CTEX 宏集 宏


Flexible Typesetting (Tim Brown) (Z-Library).

LaTeX Web Companion, The: Integrating TeX, HTML, and XML 

看看TeX的几个基础算法：
1. Donald E. Knuth, Michael F. Plass. Breaking Paragraphs into Lines. 1981
2. Franklin Mark Liang. Word Hy-phen-a-tion by Com-put-er. 1983
3. Michael F. Plass. Optimal Pagination Techniques for Automatic Typesetting Systems. 1981



[Linux-下TeXLive-2016的中文字体](https://www.jianshu.com/p/9f0ea66d7234)

[LaTeX And TrueType Font](https://xpt.sourceforge.net/techdocs/language/latex/latex33-LaTeXAndTrueTypeFont/)

[latex-fonts](http://comdyn.hy.tsinghua.edu.cn/from-web/latex/375-latex-fonts)


https://blog.yfei.page/en/2019/05/how-to-install-fonts-in-texlive/

https://www.ctan.org/pkg/newtx

https://zhuanlan.zhihu.com/p/138586028

https://github.com/xiaohanyu/awesome-tikz

https://www.tug.org/mactex/


http://tug.ctan.org/info/visualtikz/VisualTikZ.pdf

```
\the<font>
where
  <font> −→ \font | <fontdef token> | <family member>
  <family member> −→ <font range><4-bit number>
  <font range> −→ \textfont | \scriptfont | \scriptscriptfont
```

```
/System/Library/Fonts

/Library/Application Support/MiKTeX/texmfs/config/fontconfig/config

 vim localfonts2.conf   
<fontconfig>
<dir>/System/Library/PrivateFrameworks/FontServices.framework/Versions/A/Resources/Fonts/Subsets</dir>
<dir>/System/Library/PrivateFrameworks/FontServices.framework/Versions/A/Resources/Fonts/Subsets</dir>
</fontconfig>

```


```
vim ~/Library/Application\ Support/MiKTeX/texmfs/config/fontconfig/config/localfonts2.conf

 <dir>/System/Library/AssetsV2/com_apple_MobileAsset_Font6</dir>
 
```

[MikTex+TexStudio配置论文写作环境](https://zhuanlan.zhihu.com/p/42844087)


Computer Modern fonts

sudo apt-get install cm-super


Separation of form and content

The benefits in separation are many. Such as, by automating the formatting process, technical writers can spend more time on the words and phrasing rather than on the fonts, alignment and numbering. This leads to better writing quality, and more consistent presentation.

book printing 书面印刷

Ordinary Typing　普通打印

命令
* 原语primitive
* 组合

Hyphens are used for compound words like ‘daughter-in-law’ and ‘X-rated’. En-dashes are used for number ranges like ‘pages 13–34’, and also in contexts like　‘exercise 1.2.6–52’. Em-dashes are used for punctuation in sentences—they are　what we often call simply dashes. And minus signs are used in formulas.


总结为六个原则：对齐，聚拢，重复，对比，强调，留白。我是这样理解的：

一、对齐原则

　　相关内容必须对齐，次级标题必须缩进，方便读者视线快速移动，一眼看到最重要的信息。

二、聚拢原则

　　将内容分成几个区域，相关内容都聚在一个区域中。段间距应该大于段内的行距。

三、留白原则

　　千万不要把页面排得密密麻麻，要留出一定的空白，这本身就是对页面的分隔。这样既减少了页面的压迫感，又可以引导读者视线，突出重点内容。

四、降噪原则

　　颜色过多、字数过多、图形过繁，都是分散读者注意力的"噪音"。

五、重复原则

　　多页面排版时，注意各个页面设计上的一致性和连贯性。另外，在内容上，重要信息值得重复出现。

六、对比原则

　　加大不同元素的视觉差异。这样既增加了页面的活泼，又方便读者集中注意力阅读某一个子区域。


C:\Program Files\MiKTeX\miktex\bin\x64\

C:\Users\QuChunhe\AppData\Local\Programs\MiKTeX\miktex\bin\x64\



https://tex.stackexchange.com/questions/49295/precompile-header-with-xelatex



```
\RequirePackage{etoolbox}
\AtEndPreamble{
    \usepackage{fontspec}
    \setmainfont[Ligatures=TeX]{STIXGeneral}
}
```

```
\usepackage{fontspec,unicode-math}
\endofdump
```

```
\usepackage{fontspec,unicode-math}
\csname endofdump\endcsname
```

(Measure-Command {xetex -ini  -jobname="hello" -interaction=batchmode "&xelatex" mylatexformat.ltx allformula.tex }).ToString()

(Measure-Command {xelatex -initialize -interaction=batchmode D:\xml\zdhxb\accepted\AAS-CN-2023-0585\current\allformula.tex }).ToString()


(Measure-Command { etex -initialize -jobname="hello" "&xelatex" D:\xml\zdhxb\accepted\AAS-CN-2023-0585\current\allformula.tex }).ToString()


(Measure-Command { etex -initialize -jobname="hello" "&pdflatex" "mylatexformat.ltx" D:\xml\zdhxb\accepted\AAS-CN-2023-0585\current\allformula.tex }).ToString()


(Measure-Command { etex -initialize -jobname="hello" "&xelatex" "mylatexformat.ltx" D:\xml\zdhxb\accepted\AAS-CN-2023-0585\current\allformula.tex }).ToString()

[不一样的 LaTeX 教程：使用 listings 宏包美化代码](https://zhuanlan.zhihu.com/p/464141424)