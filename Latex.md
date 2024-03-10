
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



https://www.ctan.org/pkg/newtx

https://zhuanlan.zhihu.com/p/138586028

https://github.com/xiaohanyu/awesome-tikz

https://www.tug.org/mactex/


http://tug.ctan.org/info/visualtikz/VisualTikZ.pdf


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



Separation of form and content