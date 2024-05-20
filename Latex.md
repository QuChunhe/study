
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


# Latex学习

TeX Live:
* WWW: https://www.tug.org/texlive/
* SVN: svn://tug.org/texlive/
* SVN web interface (ViewVC): https://tug.org/svn/texlive/
* Mirror: https://github.com/TeX-Live/texlive-source

XeTeX:
* WWW: https://xetex.sourceforge.net/
* Git: https://git.code.sf.net/p/xetex/code
* Git web interface: https://sourceforge.net/p/xetex/code

LuaTeX
* WWW: http://www.luatex.org
* Main Git repo: https://gitlab.lisn.upsaclay.fr/texlive/luatex
* Git mirror: https://github.com/TeX-Live/luatex

MetaPost
* WWW: https://www.tug.org/metapost.html
* SVN: https://serveur-svn.lri.fr/svn/modhel/metapost (anonsvn / anonsvn)

pdfTeX
* WWW: https://www.tug.org/applications/pdftex/
* SVN: svn://tug.org/pdftex
* SVN web interface (ViewVC): https://tug.org/svn/pdftex/


There are two types of packages; styles (.sty) and classes (.cls). 


\newcommand 或者 \newenvironment 这样一两个特殊命令。
使用的方式就是 \input{mydef.tex}；而如果保存成文件名 mydef.sty，就可以用 \usepackage{mydef} 使用了.

一些专用于写宏包的命令，也就是 \ProvidesPackage、\NeedsTeXFormat 这些驼峰式命名的命令。这些命令在 clsguide 文档 [1] 中描述，用来提供宏包信息、设置宏包选项、控制代码使用、处理错误信息等等。而一个 LaTeX2e 的宏包的标准格式是怎么样的，标准的示例是什么样的，也可以在 [1] 中找到。


https://blog.csdn.net/qq_39926919/article/details/85097925

document class or a package

If the commands could be used with any document class, then make them a package; and if not, then make them a class.

L3 programming layer but also often called expl3. interface3

category codes, tokens/tokenization and “expansion” of commands or macros

[How TeX macros actually work: Part 1](https://www.overleaf.com/learn/latex/How_TeX_macros_actually_work%3A_Part_1)

不要用\input加载文件
* 不能被\listfiles
* 加载多次

book
* LATEX:A Document Preparation System, 
* The LATEX Companion 
* LATEX 2ε for Authors

[LaTeX3: Programming in LaTeX with Ease](https://www.alanshawn.com/latex3-tutorial/)


[clsguide – Documentation of LaTeX class and package writing](https://ctan.org/pkg/clsguide)

[The LaTeX3 Interfaces](https://mirrors.cqu.edu.cn/CTAN/macros/latex/contrib/l3kernel/interface3.pdf)

The two modes of TeX engines: INI mode and production mode； 初始模式和生产模式

category codes, tokens/tokenization and “expansion” of commands or macros.

expansion
* text
* primitive

概念
* character code
* category code
* character token

“tokenization process”, “token lists” and related concepts such as “macro expansion” and “expandable commands”. 

三个概念
* primitives： 引擎的内置命令
* command codes ：内部处理机制，Tex用户不可访问
* command modifiers. 

 command codes is split into two main sets:
* non-expandable commands: have command codes less than or equal to 100;
* expandable commands: have command codes greater than 100, up to a maximum value of 120. 

all commands that TeX reads from your input, whether they are primitives or user-defined macros, are eventually converted into a numeric representation called a token. 


Strictly speaking, the term control sequence has two sub-categories: control word and control symbol:


character token  && command token

string pool

TeX’s internal “filing cabinet” is called the equivalents table and is the topic of the next section.


The integer (calculated hash value) is referred to as the current control sequence, but TeX gives it the shorter name of curcs.

TeX stores the value of the current token (most recently calculated) in a variable called curtok. 

a character token is calculated from 256*catcode + (ASCII value) whereas a control sequence token is calculated from 4095 + curcs where curcs is the hash value of the control word


TeX engines have three sources of input—two that you may know:
* physical text files stored on disk;
* text that a user types into the terminal (command line);
* but it also has a third way of reading/obtaining input: token lists!


two types of command:
* multi-letter commands called control words: 
* single-letter commands called control symbols:


hash值
 curcs (current control sequence)
* curcmd: (current command)
* curchr: (current character) 
* curcs: (current control sequence) 
* curtok: (current token) 

区分功能差不多但名字不同的命令
* command code：the command codes vary from 0 to 120
* command modifier: 两种类型
   * Type 1：标识符
   * Type 2：指针，内存位置。command codes between 111 and 114 with a command modifier that is a pointer into memory telling TeX where its replacement text (the macro definition) is stored. 


 TeX primitive command \def: we won’t use the, perhaps more familiar, LaTeX command \newcommand.


macro parameters and macro arguments


Macros as token lists, token register 


TeX’s internal “filing cabinet” is called the equivalents table.

[](http://www.readytext.co.uk/?p=3590)

[What is a "TeX token"?](https://www.overleaf.com/learn/latex/Articles/What_is_a_%22TeX_token%22%3F)

[A New Series of Articles: TeX Tokens and Related Concepts—But Why (and How)?](https://www.overleaf.com/learn/latex/Articles/A_New_Series_of_Articles%3A_TeX_Tokens_and_Related_Concepts%E2%80%94But_Why_(and_How)%3F)


# 设计
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

# package conflicts

[Latex Package Conflicts: Detection And Resolution Strategies](https://latexum.com/latex-package-conflicts-detection-and-resolution-strategies/)


\newcommand will flag an error if the macro already exists. providecommand will create your definition of the macro, provided that there was no previous definition; otherwise it will leave the original definition alone.