

[Natural Language Processing with Python](https://www.nltk.org/book/)

[Stanford CoreNLP – Natural language software](https://stanfordnlp.github.io/CoreNLP/)

[Speech and Language Processing (3rd ed. draft)](https://web.stanford.edu/~jurafsky/slp3/)


The Part-Of-Sp eech Tagging Guidelines for the Penn Chinese Treebank (3.0)

https://catalog.ldc.upenn.edu/docs/LDC2010T07/ctb-segguide.pdf

https://fancyerii.github.io/books/stanfordnlp/


[句法结构](https://baike.baidu.com/item/%E5%8F%A5%E6%B3%95%E7%BB%93%E6%9E%84/65242499)

```
mvn install:install-file -Dfile=/location/of/stanford-spanish-corenlp-models-current.jar -DgroupId=edu.stanford.nlp -DartifactId=stanford-corenlp -Dversion=4.5.4 -Dclassifier=models-spanish -Dpackaging=jar
```


# 术语
[句法分析树标注集](https://www.cnblogs.com/Patrick-L/p/6500639.html)

https://www.cs.cornell.edu/courses/cs474/2004fa/lec1.pdf

分词手册（segmentation guidelines），词性标注手册（POS guidelines）和句法分析手册（bracketing guidelines）。

词性标注（Part-Of-Speech tagging, POS tagging）

句法结构(英语：syntactic structure)

Noun 名词
1. Noun 名词 
   * Proper Noun——NR，专有名词
   * Temporal Noun——NT，时间名词
   * Other Noun: NN
4. Localizer——LC，定位词：如“内”，“左右”
5. Pronoun——PN，代词
6. Determiner——DT，限定词：如“这”，“全体”
7. Cardinal Number——CD，基数词
8. Ordinal Number——OD，序数词：如“第三十一”
9. Measure word——M，衡量词：如“杯”
10. Verb：VA，VC，VE，VV，动词
   * Predicative adjective: VA 谓语形容词(状态动词)
   * Copula: VC 系动词
   * you2 as the Main Verb:有作为助动词 VE， 有、没、无
   * Other verb: VV。情态动词、提昇谓语、置动词、动作动词、心理动词
11. Adverb：AD，副词：如“近”，“极大”
12. Preposition：P，介词：如“随着”
13. Subordinating conjunctions：CS，从属连词
14. Conjuctions：
   * Cordinating Conjunction: CC，并列连词
   * Subordinating Conjunction CS 从属连词
15. Particle：
   * de5 as a complementizer or a nominalizer DEC, 的作为补语或名词化，包括“之”和“的”
   * de5 as a genitive marker and an associative marker: DEG, 的作为属格标记和关联标注 
   * Resultation de: DER 
   * Manner de5: DEV
   * Aspect Particle :AS
   * Sentence-final Particle: SP，句末助词
   * ETC, 等和等等
   * 其他小品词：MSP，小品词
Others：其他   
   * Interjections：IJ，感叹词, 如“哈”
   * onomatopoeia：ON，象声词，如“哗啦啦”
   * bei4 in long b ei-construction: LB
   * bei4 in short b ei-construction: SB
   * ba3 in ba-construction: BA
   * Other Noun-modifier：JJ，名词修饰语，如“发稿/JJ 时间/NN”
   * Punctuation：PU，标点符号】
   * Foreign word：FW，外国词语】如“OK”
21. Others,包括idioms（习语），telescopic string（没明白什么意思）

[宾州汉语词性标注指南 树库(3.0) 中文整理版](https://bbs.hanlp.com/t/3-0/1580)