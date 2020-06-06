
![](http://latex.codecogs.com/gif.latex?\\sigma=\sqrt{\frac{1}{n}{\sum_{k=1}^n(x_i-\bar{x})^2}})


# Probability


[复旦大学 概率论](https://www.bilibili.com/video/av11918653)



概率公理

There are many interpretations of P(A). The two common interpretations are frequencies and degrees of beliefs.
* In the frequency interpretation, P(A) is the long run proportion of times that A is true in repetitions.
* The degree-of-belief interpretation is that P(A) measures an observer’s strength of belief that A is true.

条件概率(Conditional Probability): multiplication rule for probabilities   

独立事件   
independent, statistically independent, independent in a probability sense

全概率公式(total probablity formula, law of total probability)   

mutually independent相互独立   

independent experiments


贝叶斯公式：先验概率，后验概率, Bayer's theorem   


random variables   


Probability Mass Function (pmf):

Probability Density Function (pdf):

Cumulative Distribution Function (cdf):

The moments are a set of constants that represent some important properties　of the distributions. The most commonly used such constants are measures of central tendency　(mean, median, and mode),  and measures of dispersion (variance and mean deviation). Two other important measures are the coefficient of skewness and the coefficient of kurtosis. The coefficient of skewness measures the degree of asymmetry of the distribution, whereas the　coefficient of kurtosis measures the degree of flatness of the distribution.

Moments about the Origin (Raw Moments):

Moments about the Mean (Central Moments):

Coefficient of Variation: Coefficient of variation is the ratio of the standard deviation to the mean, that is, (sigma/μ).

Mean Deviation: Mean deviation is a measure of variability of the possible values of the random variable X. It is defined as the expectation of absolute difference between X and its mean.

Moment Generating Function:

Characteristic Function:


We shall describe here two classical methods of estimation, namely, the moment estimation and the method of maximum likelihood estimation.

Level α Test:


liberal or anti conservative test.


统计中矩E[(X-A)^k]的定义是各点对某一固定点A离差幂的平均值。如果A=0，则是原点矩，A=均值，则是中心距。K是阶数。统计中引入矩是为了描述随机变量的分布的形态。数学期望是一阶原点矩（表示分布重心）方差是二阶中心距（表示分布对重心的离散程度）偏态是三阶中心矩（表示分布偏离对称的程度）峰态是四阶中心距（描述分布的尖峰程度，例如正态分布峰态系数=0）


图灵数学·统计学丛书30-损失模型：从数据到决策(第2版)【英文版暂代】-[美]斯图尔特·A·克卢格曼-Wiley出版-2004


[中国科技大学·缪柏其·概率论与数理统计](https://mp.weixin.qq.com/s?__biz=MzI3OTM0NTU3NQ==&mid=2247491588&idx=1&sn=88caec9e14700105827e1389c26a6df6&chksm=eb4b80ccdc3c09da36e5482570cb1b5f63c22cb056cd9a9dae5c368cf4bf79de733ca83cfbe6&mpshare=1&scene=1&srcid=&sharer_sharetime=1581605935230&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AaXBbDJteA%2FYnjehKiZ8AIk%3D&pass_ticket=LEguntyz1PWNMmRC%2FEyyrSNOvCpywEX3DB73r7jUcAZBdsNR5%2FkTGTgFjY0%2BCCq9#rd)


[[中国科学技术大学精品课程：概率论与数理统计].(缪柏其).2009](https://www.bilibili.com/video/BV17x411e7rn?p=3)

事件的蕴含、包含及相等

事件的互斥和对立

事件的和（事件的并）

事件的并、交、补和差 

不可能事件和必然事件 

集合的分割和划分   


概率的加法定理

事件的积（事件的交）

事件的差

基本事件空间   
样本空间   
事件

事件与集合一一对应
* Ｓ  空间
* 事件  集合
* 基本事件  空间中的点
事件的运算《==》集合的运算


概率是随机事件发生大小可能性的数学表征，即概率是事件的函数。

概率空间   
 
古典概率定义：有限和等概论的结果（基本事件）。实验有许多可能的结果，每个结果叫做一个基本事件。
* 有限性：存在有限个基本事件
* 等概率：基本事件的概率相等

如果基本事件的个数为n，则事件A的概率定义为P(A)=m/n,其中m为事件A包含的基本事件个数。

几何概率，基于等长度/等面积/等体积，等概论，通过计算长度、面积和体积计算出来的概论。集合概率突破了古典概率有限性的约束。 


概论的统计定义：频率．   即一事件出现的可能性大小，应由在多次重复实验中其出现的频率程度去刻画。  

独立重复做n次实验，若在这n次实验中，事件A出现m次，则称f=m/n为事件A发生的频率。若n无限增大时，则f在某值p附近摆动，则称事件A的概率P(A)=p

概率的公理化定义：定义概率必须满足的一般性质。

集合$\Omega$，其元素$\omega$称为基本事件， 集类S的元素是$\Omega$的子集，S为一个sigma代数，其任意一个元素A称为一个事件事件，概率P满足
* 0<=P<=1，即概率介于0和1之间
* P($\Omega$)=1，即必然事件概率为1
* P满足完全可列可加性
($\Omega$,S,P)为一个特殊的测度空间

加法原理　

乘法原理

排列和组合

盒子模型：r个球放入n个盒子
* 球可辨，每盒至少一球　P^n_r
* 球可变，每盒球数不限 n^r
* 球不可变，每盒至少一球 C^n_r
* 球不可变，每盒球数不限 C^{n+r-1}_r


随机性　　均匀性
* 均匀性具有排他性


a个红球，b个白球，依次取出，第k次摸出红球的概率a/(a+b)


条件概率：在一次实验中，在某个时间B发生的条件下事件A发生的概率，称为条件概率，记为P(A|B).

B为实验前知道的某些信息

全概论公式  划分 partition

贝叶斯公式 
* 因果关系互换
* 每个告诉划分，则B和其对立事件即为一个自然的划分

独立性

若事件A发生与否与事件B发生与否无关，则称A和B是独立的

A1,A2,...,An中任意k个事件都相互独立

独立和不相容是两个不同的概念

随机变量(random variable)

陈希孺<<概率论与数理统计>>

* 放回有序样本
* 放回无序样本
* 不放回有序抽样
* 不放回无序抽样

[放回无序样本](https://zhuanlan.zhihu.com/p/48248142)


[Unordered Sampling without Replacement: Combinations](https://www.probabilitycourse.com/chapter2/2_1_3_unordered_without_replacement.php)



按箱分配质点。将n个质点(小球)分配到M个箱子中。   

(有序抽样）<-->(质点可以辩)    
(无序抽样)<-->(质点不可辩)   

在“自盛有M个球的箱中抽选n个球”的问题中，有序(无序)抽样相当于，可辩质点(不可辩质点)分配到M个箱中的分配问题。   

(放回抽样)<-->(箱中可容纳任意多质点)   
(不放回抽样)<-->(箱中最多可容纳一个质点)   

  

二项式分布   
多项式分布   

乘法定理的作用与加法定理一样：把复杂事件的概率计算归结为更简单的事件概率的计算，这当然要有条件：加法是互斥，相乘是独立

[概率论与数理统计 - 中国科学院大学](https://www.bilibili.com/video/BV1q7411L75X/?spm_id_from=333.788.videocard.15)


[Non-transitive Dice](https://www.microsoft.com/en-us/research/project/non-transitive-dice/)


频率与概率

蒲丰投针

古典概型的两个特点
* 样本空间仅仅包含有限个基本事件
* 每个基本事件发生的可能性相同

标记重捕法

对立事件


条件概率P(A)与无条件概率之间P(A|B)的大小无确定关系，即可能
* P(A)<P(A|B)
* P(A)=P(A|B)
* P(A)>P(A|B)

波利亚罐子模型（传染模型）

[【数学系专业课】 概率论与数理统计 讲解视频](https://www.bilibili.com/video/BV1cb411j7Mm?from=search&seid=15835382154082768770)


[統計學 陳鄰安](https://04.phf-site.com/2015/06/blog-post_119.html)


Hogg,.Craig,.Introduction.to.Mathematical.Statistics,.5ed,.Pearson.1995,.HEP.2004,

Random Experiment : An experiment whose outcomes are determined only by chance factors is called a random experiment.   
Sample Space: The set of all possible outcomes of a random experiment is called a sample space.  
Event : The collection of none, one, or more than one outcomes from a sample space is called an event.
Random Variable: A variable whose numerical values are determined by chance factors is called a random variable. Formally, it is a function from the sample space to a set of real numbers.


Sample Space S：Set of possible outcomes of a random experiment/survey.

Event: Every subset of is an Event

Probability Set  Function P

A Random Variable X is a real valued function defined on S

X: S-->R



[在线西北工业大学的数理统计课程](https://www.bilibili.com/video/av80041910)


总体

样本

样本值（观察值）






# Statistics


Introduction to mathematical statistics Eighth edition


Stephen M. Stigler, The Seven Pillars of Statistical Wisdom (统计学七支柱), Harvard university Press, 2016 

第一根支柱——聚合.：把数据集中的个体值进行统计汇总，概括出的信息可以超越个体

均值的3 种类型：算术平均值、几何平均值和调和平均值

第二根支柱——信息度量

数据中的信息可以度量，其精度在某种程度上与数据的数量有关，在某些情况下能够精确处理。

[算术平均、几何平均、调和平均、平方平均和移动平均](https://www.cnblogs.com/liuning8023/p/3525920.html)

似然：概率尺度上的校准


概率本身是一种度量

相互比较：作为标准的样本内变异

回归：多元分析、贝叶斯推断和因果推断


设计包括积极实验的计划、研究规模的决定、问题的设计以及处理的安排，还包括田野试验和抽样调查、质量监督和临床试验，以及在实验科学中的政策和策略评价

残差：科学逻辑、模型比较以及诊断展示


[Difference Between Time Series and Cross Sectional Data](https://www.differencebetween.com/difference-between-time-series-and-cross-sectional-data/)
Panel Data,面板数据,“纵向数据(Longitudinal Data)”，“平行数据”，“TS-CS数据(Time Series-Cross Section)”

Cross-sectional data,截面数据 


Time-series data,时序数据

The key difference between time series and cross sectional data is that the time series data focuses on the same variable over a period of time while the cross sectional data focuses on several variables at the same point of time. Furthermore, the time series data consist of observations of a single subject at multiple time intervals whereas, the cross sectional data consist of observations of many subjects at the same point in time.

[Experimental Design and Analysis](https://www.stat.cmu.edu/~hseltman/309/Book/Book.pdf)

[Handbook of Statistical Methods](https://www.itl.nist.gov/div898/handbook/index.htm)

Sampling: Design and Analysis by Sharon L. Lohr (1999).

[Type I and type II errors](https://en.wikipedia.org/wiki/Type_I_and_type_II_errors)

* A type I error occurs when the null hypothesis (H0) is true, but is rejected. It is asserting something that is absent, a false hit. A type I error may be likened to a so-called false positive (a result that indicates that a given condition is present when it actually is not present).The type I error rate or significance level is the probability of rejecting the null hypothesis given that it is true. It is denoted by the Greek letter α (alpha) and is also called the alpha level. Often, the significance level is set to 0.05 (5%), implying that it is acceptable to have a 5% probability of incorrectly rejecting the null hypothesis
* A type II error occurs when the null hypothesis is false, but erroneously fails to be rejected. It is failing to assert what is present, a miss. A type II error may be compared with a so-called false negative (where an actual 'hit' was disregarded by the test and seen as a 'miss') in a test checking for a single condition with a definitive result of true or false. A Type II error is committed when we fail to believe a true alternative hypothesis.The rate of the type II error is denoted by the Greek letter β (beta) and related to the power of a test (which equals 1−β). 


Type I error (False Positive) (Probability = α) 

Type II error(False Negative) (Probability = β)


Type I Error: Wrongly rejecting H0 when it is actually true is called the type I error.

Type II Error: Wrongly accepting H0 when it is false is called the type II error.

Level of Significance: The maximum probability of making type I error is called the level or level of significance; this is usually specified  before carrying out a test.

Power Function: The power function is defined as the probability of rejecting null hypothesis. That is,



[Null Hypothesis (原假设或者零假设) and Alternative Hypothesis (备择假设)](https://www.thoughtco.com/null-hypothesis-vs-alternative-hypothesis-3126413)



[Causality](https://en.wikipedia.org/wiki/Causality)

Causality (also referred to as causation, or cause and effect) is what connects one process, the cause, with another process or state, the effect, where the cause is wholly or partially responsible for the effect; the former is hence said to be a cause of the latter. In general, a process has many causes, which are also said to be causal factors for it, and all lie in its past. An effect can in turn be a cause of, or causal factor for, many other effects, which all lie in its future.



[What Educated Citizens Should Know About Statistics and Probability](https://www.ics.uci.edu/~jutts/AmerStat2003.pdf)


1. Cause and Effect: When it can be concluded that a relationship is one of cause and effect, and when it cannot, including the difference between randomized experiments and observational studies.
2. Statistical Significance and Practical Importance: The difference between statistical signicance and practical importance, especially when using large sample sizes
3. Low Power versus No Effect: The difference between finding "no effect" or "no difference" and finding no statistically significant effect or difference, expecially when using small sample size.
4. Biases In Surveys: Common sources of bias in surveys and experiments, such as poor wording of questions, volunteer response, and socially desirable answers.
5.Probable conincidences: The idea that coincidences and seemingly very improbable events are not uncommon because there are so many possibilities.
6. Confusion of the Inverse: "Confusion of the inverse" in which a conditional probability in one direction is confused with the conditional probability in the other direction.
7. Averge versus Normal: Understading that variability is natural, and that "normal" is not the same as "average".




<<统计学方法与数据分析引论>>(R. Lyman Ott and Michael Longnecker， An Introduction to Statistical Methods and Data Analysis Seventh Edition,Texas A&M University, 2016)
  
  总体：所有测量值的集合   
  样本：从总体中挑选出来的测量值集合 
  
  
  clinical trial（临床实验）
  
  
  统计学的目标在于基于从感兴趣的总体抽得的样本的测量信息，对该总体作出推断。
  
  数据收集方案的设计，数据的概括和统计分析，解释研究结果
  
  That is, statistics is the science of Learning from Data.
  
  Learning from Data: (1) defining the problem, (2) collecting the data, (3) summarizing
the data, and (4) analyzing the data, interpreting the analyses, and communicating
the results.


Someone has defined the problem to be examined (Step 1), developed a plan for collecting
data to address the problem (Step 2), and summarized the data and prepared the
data for analysis (Step 3). Then following the analysis of the data, the results of the
analysis must be interpreted and communicated either verbally or in written form
to the intended audience (Step 4).

A population is the set of all measurements of interest to the sample collector.

A sample is any subset of measurements selected from the population.


The patterns and trends discovered in the analysis of the data are defined as data mining models.

Data collection processes include surveys, experiments, and the examination of existing data from business records, censuses,
government records, and previous studies. The theory of sample surveys and the theory of experimental designs
provide excellent methodology for data collection.


We will also make a distinction between an experimental study and an observational study.

In an observational study, the researcher records information concerning the subjects under study without any interference with the process that is generating the information. The researcher is a passive observer of the transpiring events. In an experimental study, the researcher actively manipulates certain variables associated with the study, called the explanatory variables, and then records their effects on the response variables associated with the experimental subjects. A severe limitation of observational studies is that the recorded values of the response variables may be affected by variables other than the explanatory variables. These variables are not under the control of the researcher. They are called confounding variables. The effects of the confounding variables and the explanatory variables on the response variable cannot be separated due to the lack of control the researcher has over the physical setting in which the observations are made.

* explanatory variables:Explanatory variable (or independent variable) is one that may explain or may cause differences in a response variable (or outcomeor dependent variable)
* response variables
* confounding variables: A confounding variable is a variable that: Affects the response variable and also is related to the explanatory variable.A potential confounding variable not measured in the study is called a lurking variable.


[confounding variable](https://en.wikipedia.org/wiki/Confounding)

混淆变量(confounding variable):混淆变量是在研究中无法控制的变量(uncontrolled variable)，有时亦称为「额外变量」(extraneous variable)，这些变量可能会影响到自变量与因变量，但因为未受到控制，因此，其影响力多大是个未知数，故称为混淆变量。

潜变量(Latent variables)，与可观察变量相对，是不直接观察但是通过观察到的其他变量推断（通过数学模型）的变量（直接测量）。潜变量可分为内生潜变量和外生潜变量，外生潜变量在模型不受其他任何一个变量的影响但影响其他变量的变量，内生潜变量在模型中总会受到一个其他变量影响的变量。



Observational studies may be dichotomized into either a comparative study or a descriptive study. In a comparative study, two or more methods of achieving a result are compared for effectiveness. In a descriptive study, the major purpose is to characterize
a population or process based on certain attributes in that population or process.

A problem that may occur in observational studies is assigning cause-and-effect relationships to spurious associations between factors.

Observational studies are of three basic types:
* A sample survey is a study that provides information about a population at a particular point in time (current information).
* A prospective study is a study that observes a population in the present using a sample survey and proceeds to follow the subjects in the sample forward in time in order to record the occurrence of specific outcomes.
* A retrospective study is a study that observes a population in the present using a sample survey and also collects information about the subjects in the sample regarding the occurrence of specific outcomes that have already taken place.

Both prospective and retrospective studies are often comparative in nature. Two specific types of such studies are cohort studies and case-control studies.

A crucial element in any survey is the manner in which the sample is selected from the population.

Target population: The complete collection of objects whose description is the major goal of the study.  
Sample: A subset of the target population.   
Sampled population: The complete collection of objects that have the potential of being selected in the sample; the population from which the sample is actually selected.   
Observation unit: The object about which data are collected.   
Sampling unit: The object that is actually sampled.
Sampling frame: The list of sampling units.     



* simple random sampling: The basic design (simple random sampling) consists of selecting a group of n units in such a way that each sample of size n has the same chance of being selected.
* stratified random sample:
* Ratio estimation
* cluster sampling
* systematic sample

Although we divide the population into groups for both cluster sampling and stratified random sampling, the techniques differ. In
stratified random sampling, we take a simple random sample within each group, whereas in cluster sampling, we take a simple random sample of groups and then sample all items within the selected groups (clusters).

[What Is a Survey](https://www.whatisasurvey.info/downloads/pamphlet_current.pdf)


Problems Associated with Surveys
* Survey nonresponse
* Measurement problems

The most commonly used methods of data collection in sample surveys
* personal interviews
* telephone interviews
* self-administered questionnaire
* direct observation


designed experiment: A designed experiment is an investigation in which a specified framework is provided in order to observe, measure, and evaluate groups with respect to a designated response.

There are two types of variables in a experimental study.
* Controlled variables called factors are selected by the researcher for comparison. 
* Response variables are measurements or observations that are recorded but not controlled by the researcher. 
The controlled variables form the comparison groups defined by the research hypothesis.

The treatments in an experimental study are the conditions constructed from the factors.

In most cases, we will have several factors, and the treatments are formed by combining levels of the factors. This type of treatment design is called a factorial treatment design.     

This type of experiment has a fractional factorial treatment structure, since only a fraction of the possible treatments are actually used in the experiment.    

A special treatment is called the control treatment. This treatment is the benchmark to which the effectiveness of each remaining treatment is compared.   

The experimental unit is the physical entity to which the treatment is randomly assigned or the subject that is randomly selected from one of the treatment populations.   

Distinct from the experimental unit is the measurement unit. This is the physical entity upon which a measurement is taken. In many experiments, the experimental and measurement units are identical.   

The term experimental error is used to describe the variation in the responses among experimental units that are assigned the same treatment and are observed under the same experimental conditions.   

In general, a completely randomized design is used when we are interested n comparing t “treatments” . For each of the treatments, we obtain a sample of observations. The sample sizes would be different for the individual treatments.   

In a randomized block design, each treatment appears in every block.  

A design having two blocking variables is called a Latin square design.   

The randomized block and Latin square designs are both extensions of the completely randomized design in which the objective is to compare t treatments. The analysis of data for a completely randomized design and for block designs.

One approach for examining the effects of two or more factors on a response is called the one-at-a-time approach. To examine the effect of a single variable, an experimenter varies the levels of this variable while holding the levels of the other independent variables fixed. This process is continued until the effect of each variable on the response has been examined.

Thus, this type of experimentation may produce incorrect results whenever the effect of one factor on the response does not remain the same at all levels of the second factor. In this situation, the factors are said to interact.

When interaction exists among the factors, the lines will either cross or diverge.

Factorial treatment structures are useful for examining the effects of two or more factors on a response, whether or not interaction exists. As before, the choice of the number of levels of each variable and the actual settings of these variables is important.


A covariate is a variable that is related to the response variable.

协变量：在实验的设计中，协变量是一个独立变量（解释变量），不为实验者所操纵，但仍影响实验结果。

The covariate needs to have a relationship to the response variable, it must be measurable, and it cannot be affected by the treatment.


analysis of covariance


The field of statistics can be divided into two major branches: descriptive statistics and inferential statistics.

Good descriptive statistics enable us to make sense of the data by reducing a large set of measurements to a few summary measures that provide a good, rough picture of the original measurements.

sampling error

nonsampling error


Whether we are describing an observed population or using sampled data to draw an inference from the sample to the population, an insightful description of the data is an important step in drawing conclusions from it.

The two major methods for describing a set of measurements are graphical techniques and numerical descriptive techniques.


pie chart(饼图). It is used to display the percentage of the total number of measurements falling into each of the categories of the variable by partitioning a circle. The pie chart can be used to display percentages associated with each category of the variable. 
* Choose a small number (five or six) of categories for the variable because too many make the pie chart difficult to interpret.
* Whenever possible, construct the pie chart so that percentages are in either ascending or descending order.

bar chart(条形图)和column chart(柱形图)
* Label frequencies on one axis and categories of the variable on the other axis.
* Construct a rectangle at each category of the variable with a height equal to the frequency (number of observations) in the category.
* Leave a space between each category to connote distinct, separate categories and to clarify the presentation.


frequency histogram(频率直方图)and the relative frequency histogram(相对频率直方图)


There are several comments that should be made concerning histograms. First, the distinction between bar charts and histograms is based on the distinction between qualitative and quantitative variables. Pie charts and bar charts are used to display
frequency data from qualitative variables; histograms are appropriate for displaying frequency data for quantitative variables.


Histograms are most useful for describing data sets when the number of data points is fairly large—say, 50 or more.

* unimodal(单峰)
* bimodal(双峰)
* uniform（均匀）
* symmetric(对称)
* skewed to the right(偏向右边)
* skewed to the left(偏向左边)


exploratory data analysis(探索性数据分析)

stem-and-leaf plot(茎叶图)


General Guidelines for Developing Successful Graphics
1. Before constructing a graph, set your priorities. What messages should the viewer get?
2. Choose the type of graph (pie chart, bar graph, histogram, and so on).
3. Pay attention to the title. One of the most important aspects of a graph is its title. The title should immediately inform the viewer of the point of the graph and draw the eye toward the most important elements of the graph.
4. Fight the urge to use many type sizes, styles, and colors. The indiscriminate and excessive use of different type sizes, styles, and colors will confuse the viewer. Generally, we recommend using only two typefaces; color changes and italics should be used in only one or two places.
5. Convey the tone of your graph by using colors and patterns. Intense, warm colors (yellows, oranges, reds) are more dramatic than the
blues and purples and help to stimulate enthusiasm by the viewer. On the other hand, pastels (particularly grays) convey a conservative, businesslike tone. Similarly, simple patterns convey a conservative tone, whereas busier patterns stimulate more excitement.
6. Don’t underestimate the effectiveness of a simple, straightforward graph.


* graphical descriptive measures(图形描述方法)
* Numerical descriptive measures(数字描述方法)

Describing Data on a Single Variable: Measures of Central Tendency

The two most common numerical descriptive measures are measures of central tendency(集中趋势) and measures of variability(波动性); that is, we seek to describe the center of the distribution of measurements and also how the measurements vary about the center of the distribution. 

We will draw a distinction between numerical descriptive measures for a population, called parameters, and numerical descriptive
measures for a sample, called statistics.In problems requiring statistical inference, we will not be able to calculate values for various parameters, but we will be able to compute corresponding statistics from the sample and use these quantities to estimate
the corresponding population parameters.


The mode（众数） of a set of measurements is defined to be the measurement that occurs most often (with the highest frequency).

The mode is also commonly used as a measure of popularity that reflects central tendency or opinion.

The median(中位数) of a set of measurements is defined to be the middle value when the measurements are arranged from lowest to highest.

The median is most often used to measure the midpoint of a large set of measurements.

However, we may use the definition of median for small sets of measurements by using the following convention: The median for an even number of measurements is the average of the two middle values when the measurements are arranged from lowest to highest. When there are an odd number of measurements, the median is still the middle value.


grouped data median


![grouped data median](https://github.com/QuChunhe/study/blob/master/pics/grouped_data_median.jpg)


The arithmetic mean, or mean(均值), of a set of measurements is defined to be the sum of the measurements divided by the total number of measurements.


The population mean is denoted by the Greek letter m (read “mu’’), and the sample mean is denoted by the symbol y (read
“y-bar’’).

![grouped data mean](https://github.com/QuChunhe/study/blob/master/pics/grouped_data_mean.jpg)

the extreme values (called outliers) pull the mean in the direction of the outliers to find the balancing point, thus distorting the mean as a measure of the central value.

A variation of the mean, called a trimmed mean(切尾均值), drops the highest and lowest extreme values and averages the rest.


The answer depends on the skewness of the data. If the distribution is mound-shaped and symmetrical about a single peak, the mode (Mo), median (Md), mean (m), and trimmed mean (TM) will all be the same.

If the distribution is skewed, having a long tail in one direction and a single peak, the mean is pulled in the direction of the tail; the median falls between the mode and the mean; and depending on the degree of trimming, the trimmed mean usually falls between
the median and the mean.

For some data sets, it will be necessary to use more than one of these measures to provide an accurate descriptive summary of
central tendency for the data.
* Mode
1. It is the most frequent or probable measurement in the data set.
2. There can be more than one mode for a data set.
3. It is not influenced by extreme measurements.
4. Modes of subsets cannot be combined to determine the mode of the complete data set.
5. For grouped data, its value can change depending on the categories used.
6. It is applicable for both qualitative and quantitative data.
* Median
1. It is the central value; 50% of the measurements lie above it and 50% fall below it.
2. There is only one median for a data set.
3. It is not influenced by extreme measurements.
4. Medians of subsets cannot be combined to determine the median of the complete data set.
5. For grouped data, its value is rather stable even when the data are organized into different categories.
6. It is applicable to quantitative data only.
* Mean
1. It is the arithmetic average of the measurements in a data set.
2. There is only one mean for a data set.
3. Its value is influenced by extreme measurements; trimming can help to reduce the degree of influence.
4. Means of subsets can be combined to determine the mean of the complete data set.
5. It is applicable to quantitative data only.


Describing Data on a Single Variable: Measures of Variability

The simplest but least useful measure of data variation is the range(范围/幅度).

The pth percentile(第p百分位数) of a set of n measurements arranged in order of magnitude is that value that has at most p% of the measurements below it and at most (100-p)% above it.

Specific percentiles of interest are the 25th, 50th, and 75th percentiles, often called the lower quartile, the middle quartile (median), and the upper quartile, respectively

The interquartile range (IQR)(四分位间距或者四分差) of a set of measurements is defined to be the difference between the upper and lower quartiles;

IQR = 75th percentile - 25th percentile


In most data sets, we would typically need a minimum of five summary values to provide a minimal description of the data set: smallest value, y(1); lower quartile, Q(.25); median; upper quartile, Q(.75); and largest value, y(n).

To do this, we work with the deviation y_i - ybar of a measurement y_i from the mean y of the set of measurements

The variance of a set of n measurements y1, y2, . . . , yn with mean ybar is the sum of the squared deviations divided by n-1:



# Bayesian Statistics

Bradley P. Carlin and Thomas A. Louis,  Bayesian Methods for Data Analysis third edition, Taylor & Francis Group 2009  

Three principal approaches to inference guide modern data analysis: frequentist, Bayesian, and likelihood.  


empirical Bayes (EB)  

In a nutshell, the Likelihood Principle states that once the data value x has been observed, the likelihood function L(θ|x) contains all relevant experimental information delivered by x about the unknown parameter θ.  

Many of these advantages are presented in detail in the popular textbook by Berger
* Bayesian methods provide the user with the ability to formally incorporate prior information.
* Inferences are conditional on the actual data.
* The reason for stopping the experimentation does not affect Bayesian inference.
* Bayesian answers are more easily interpretable by nonspecialists.
* All Bayesian analyses follow directly from the posterior; no separate theories of estimation, testing, multiple comparisons, etc. are needed.
* Any question can be directly answered through Bayesian analysis.
* Bayes and EB procedures possess numerous optimality properties.


The most basic Bayesian model has two stages, with a likelihood specification Y |θ ∼ f(y|θ) and a prior specification θ ∼ π(θ), where either Y or θ can be vectors.

K. Krishnamoorthy， Handbook of Statistical Distributions with Applications Second Edition，CRC Press， 2016  


Peter D. Hoff，A First Course in Bayesian Statistical Methods，Springer， 2009  


Bradley Efron and Trevor Hastie, Computer Age Statistical Inference: Algorithms, Evidence, and Data Science, Cambridge University Press, 2016


[Bayesian Inference](http://www.stat.cmu.edu/~larry/=sml/Bayes.pdf)


# Statistical Inference

[Statistical inference for data science](https://leanpub.com/LittleInferenceBook/read)


[迴歸分析 Regression Analysis - Introduction](http://ocw.nctu.edu.tw/course_detail-v.php?bgid=1&gid=4&nid=528)

Introduction to Linear Regression Analysis (5th Edition). Wiley. (ILRA)




A
absolute value 绝对值

accept 接受

acceptable region 接受域

additivity 可加性

adjusted 调整的

alternative hypothesis 对立假设

analysis 分析

analysis of covariance 协方差分析

analysis of variance 方差分析

arithmetic mean 算术平均值

association 相关性

assumption 假设

assumption checking 假设检验

availability 有效度

average 均值

B
balanced 平衡的

band 带宽

bar chart 条形图

beta-distribution 贝塔分布

between groups 组间的

bias 偏倚

binomial distribution 二项分布

binomial test 二项检验

C
calculate 计算

case 个案

category 类别

causal factors 因果要素

center of gravity 重心

central tendency 中心趋势

chi-square distribution 卡方分布

chi-square test 卡方检验

classify 分类

cluster analysis 聚类分析

coefficient 系数

coefficient of correlation 相关系数

collinearity 共线性

column 列

compare 比较

comparison 对照

components 构成，分量

compound 复合的

confidence interval 置信区间

consistency 一致性

constant 常数

continuous variable 连续变量

control charts 控制图

correlation 相关

covariance 协方差

covariance matrix 协方差矩阵

critical point 临界点

critical value 临界值

crosstab 列联表

cubic 三次的，立方的

cubic term 三次项

cumulative distribution function 累加分布函数

curve estimation 曲线估计

D
data 数据

default 默认的

definition 定义

deleted residual 剔除残差

density function 密度函数

dependent variable 因变量

description 描述

design of experiment 试验设计

deviations 差异

df.(degree of freedom) 自由度

diagnostic 诊断

dimension 维

discrete variable 离散变量

discriminant function 判别函数

discriminatory analysis 判别分析

distance 距离

distribution 分布

D-optimal design D-优化设计

E
eaqual 相等

effects of interaction 交互效应

efficiency 有效性

eigenvalue 特征值

equal size 等含量

equation 方程

error 误差

estimate 估计

estimation of parameters 参数估计

estimations 估计量

evaluate 衡量

exact value 精确值

expectation 期望

expected value 期望值

exponential 指数的

exponential distributon 指数分布

extreme value 极值

F
factor 因素，因子

factor analysis 因子分析

factor score 因子得分

factorial designs 析因设计/因子设计

factorial experiment 析因试验/因子实验

fit 拟合

fitted line 拟合线

fitted value 拟合值

fixed model 固定模型

fixed variable 固定变量

fractional factorial design 部分析因设计

frequency 频数

F-test F检验

full factorial design 完全析因设计

function 函数

G
gamma distribution 伽玛分布

geometric mean 几何均值

group 组

H
harmomic mean 调和均值

heterogeneity 不齐性

histogram 直方图

homogeneity 齐性

homogeneity of variance 方差齐性

hypothesis 假设

hypothesis test 假设检验

I
independence 独立

independent variable 自变量

independent-samples 独立样本

index 指数

index of correlation 相关指数

interaction 交互作用

interclass correlation 组内相关

interval estimate 区间估计

intraclass correlation 组间相关

inverse 倒数的

iterate 迭代

K
kernal 核

Kolmogorov-Smirnov test

柯尔莫哥洛夫-斯米诺夫检验

kurtosis 峰度

L
large sample problem 大样本问题

layer 层

least-significant difference 最小显著差数

least-square estimation 最小二乘估计

least-square method 最小二乘法

level 水平

level of significance 显著性水平

leverage value 中心化杠杆值

life 寿命

life test 寿命试验

likelihood function 似然函数

likelihood ratio test 似然比检验

linear 线性的

linear estimator 线性估计

linear model 线性模型

linear regression 线性回归

linear relation 线性关系

linear term 线性项

logarithmic 对数的

logarithms 对数

logistic 逻辑的

lost function 损失函数

M
main effect 主效应

matrix 矩阵

maximum 最大值

maximum likelihood estimation 极大似然估计

mean squared deviation(MSD) 均方差

mean sum of square 均方和

measure 衡量

media 中位数

M-estimator M估计

minimum 最小值

missing values 缺失值

mixed model 混合模型

mode 众数

model 模型

Monte Carle method 蒙特卡罗法

moving average 移动平均值

multicollinearity 多元共线性

multiple comparison 多重比较

multiple correlation 多重相关

multiple correlation coefficient 复相关系数

multiple correlation coefficient 多元相关系数

multiple regression analysis 多元回归分析

multiple regression equation 多元回归方程

multiple response 多响应

multivariate analysis 多元分析

N
negative relationship 负相关

nonadditively 不可加性

nonlinear 非线性

nonlinear regression 非线性回归

noparametric tests 非参数检验

normal distribution 正态分布

null hypothesis 零假设

number of cases 个案数

O
one-sample 单样本

one-tailed test 单侧检验

one-way ANOVA 单向方差分析

one-way classification 单向分类

optimal 优化的

optimum allocation 最优配制

order 排序

order statistics 次序统计量

origin 原点

orthogonal 正交的

outliers 异常值

P
paired observations 成对观测数据

paired-sample 成对样本

parameter 参数

parameter estimation 参数估计

partial correlation 偏相关

partial correlation coefficient 偏相关系数

partial regression coefficient 偏回归系数

percent 百分数

percentiles 百分位数

pie chart 饼图

point estimate 点估计

poisson distribution 泊松分布

polynomial curve 多项式曲线

polynomial regression 多项式回归

polynomials 多项式

positive relationship 正相关

power 幂

P-P plot P-P概率图

predict 预测

predicted value 预测值

prediction intervals 预测区间

principal component analysis 主成分分析

proability 概率

probability density function 概率密度函数

probit analysis 概率分析

proportion 比例

Q
qadratic 二次的

Q-Q plot Q-Q概率图

quadratic term 二次项

quality control 质量控制

quantitative 数量的，度量的

quartiles 四分位数

R
random 随机的

random number 随机数

random number 随机数

random sampling 随机取样

random seed 随机数种子

random variable 随机变量

randomization 随机化

range 极差

rank 秩

rank correlation 秩相关

rank statistic 秩统计量

regression analysis 回归分析

regression coefficient 回归系数

regression line 回归线

reject 拒绝

rejection region 拒绝域

relationship 关系

reliability 可*性

repeated 重复的

report 报告，报表

residual 残差

residual sum of squares 剩余平方和

response 响应

risk function 风险函数

robustness 稳健性

root mean square 标准差

row 行

run 游程

run test 游程检验

S
sample 样本

sample size 样本容量

sample space 样本空间

sampling 取样

sampling inspection 抽样检验

scatter chart 散点图

S-curve S形曲线

separately 单独地

sets 集合

sign test 符号检验

significance 显著性

significance level 显著性水平

significance testing 显著性检验

significant 显著的，有效的

significant digits 有效数字

skewed distribution 偏态分布

skewness 偏度

small sample problem 小样本问题

smooth 平滑

sort 排序

soruces of variation 方差来源

space 空间

spread 扩展

square 平方

standard deviation 标准离差

standard error of mean 均值的标准误差

standardization 标准化

standardize 标准化

statistic 统计量

statistical quality control 统计质量控制

std. residual 标准残差

stepwise regression analysis 逐步回归

stimulus 刺激

strong assumption 强假设

stud. deleted residual 学生化剔除残差

stud. residual 学生化残差

subsamples 次级样本

sufficient statistic 充分统计量

sum 和

sum of squares 平方和

summary 概括，综述

T
table 表

t-distribution t分布

test 检验

test criterion 检验判据

test for linearity 线性检验

test of goodness of fit 拟合优度检验

test of homogeneity 齐性检验

test of independence 独立性检验

test rules 检验法则

test statistics 检验统计量

testing function 检验函数

time series 时间序列

tolerance limits 容许限

total 总共，和

transformation 转换

treatment 处理

trimmed mean 截尾均值

true value 真值

t-test t检验

two-tailed test 双侧检验

U
unbalanced 不平衡的

unbiased estimation 无偏估计

unbiasedness 无偏性

uniform distribution 均匀分布

V
value of estimator 估计值

variable 变量

variance 方差

variance components 方差分量

variance ratio 方差比

various 不同的

vector 向量

W
weight 加权，权重

weighted average 加权平均值

within groups 组内的

Z
Z score Z分数


2. 最优化方法词汇英汉对照表


A
active constraint 活动约束

active set method 活动集法

analytic gradient 解析梯度

approximate 近似

arbitrary 强制性的

argument 变量

attainment factor 达到因子

B
bandwidth 带宽

be equivalent to 等价于

best-fit 最佳拟合

bound 边界


C
coefficient 系数

complex-value 复数值

component 分量

constant 常数

constrained 有约束的

constraint 约束

constraint function 约束函数

continuous 连续的

converge 收敛

cubic polynomial interpolation method

三次多项式插值法

curve-fitting 曲线拟合

D
data-fitting 数据拟合

default 默认的，默认的

define 定义

diagonal 对角的

direct search method 直接搜索法

direction of search 搜索方向

discontinuous 不连续

E
eigenvalue 特征值

empty matrix 空矩阵

equality 等式

exceeded 溢出的

F
feasible 可行的

feasible solution 可行解

finite-difference 有限差分

first-order 一阶

G
Gauss-Newton method 高斯-牛顿法

goal attainment problem 目标达到问题

gradient 梯度

gradient method 梯度法

H

handle 句柄

Hessian matrix 海色矩阵

I
independent variables 独立变量

inequality 不等式

infeasibility 不可行性

infeasible 不可行的

initial feasible solution 初始可行解

initialize 初始化

inverse 逆

invoke 激活

iteration 迭代

iteration 迭代

J
Jacobian 雅可比矩阵

L
Lagrange multiplier 拉格朗日乘子

large-scale 大型的

least square 最小二乘

least squares sense 最小二乘意义上的

Levenberg-Marquardt method

列文伯格-马夸尔特法

line search 一维搜索

linear 线性的

linear equality constraints 线性等式约束

linear programming problem 线性规划问题

local solution 局部解

M
medium-scale 中型的

minimize 最小化

mixed quadratic and cubic polynomial interpolation and extrapolation method

混合二次、三次多项式内插、外插法

multiobjective 多目标的

N
nonlinear 非线性的

norm 范数

O
objective function 目标函数

observed data 测量数据

optimization routine 优化过程

optimize 优化

optimizer 求解器

over-determined system 超定系统

P
parameter 参数

partial derivatives 偏导数

polynomial interpolation method

多项式插值法

Q
quadratic 二次的

quadratic interpolation method 二次内插法

quadratic programming 二次规划

R
real-value 实数值

residuals 残差

robust 稳健的

robustness 稳健性，鲁棒性

S
scalar 标量

semi-infinitely problem 半无限问题

Sequential Quadratic Programming method

序列二次规划法

simplex search method 单纯形法

solution 解

sparse matrix 稀疏矩阵

sparsity pattern 稀疏模式

sparsity structure 稀疏结构

starting point 初始点

step length 步长

subspace trust region method 子空间置信域法

sum-of-squares 平方和

symmetric matrix 对称矩阵

T
termination message 终止信息

termination tolerance 终止容限

the exit condition 退出条件

the method of steepest descent 最速下降法

transpose 转置

U
unconstrained 无约束的

under-determined system 负定系统

V
variable 变量

vector 矢量

W
weighting matrix 加权矩阵



样条词汇英汉对照表


A
approximation 逼近

array 数组

a spline in b-form/b-spline b样条

a spline of polynomial piece /ppform spline

分段多项式样条

B
bivariate spline function 二元样条函数

break/breaks 断点

C
coefficient/coefficients 系数

cubic interpolation 三次插值/三次内插

cubic polynomial 三次多项式

cubic smoothing spline 三次平滑样条

cubic spline 三次样条

cubic spline interpolation

三次样条插值/三次样条内插

curve 曲线

D
degree of freedom 自由度

dimension 维数

E
end conditions 约束条件

I
input argument 输入参数

interpolation 插值/内插

interval 取值区间

K
knot/knots 节点

L
least-squares approximation 最小二乘拟合

M
multiplicity 重次

multivariate function 多元函数

O
optional argument 可选参数

order 阶次

output argument 输出参数

P
point/points 数据点

R
rational spline 有理样条

rounding error 舍入误差（相对误差）

S
scalar 标量

sequence 数列（数组）

spline 样条

spline approximation 样条逼近/样条拟合

spline function 样条函数

spline curve 样条曲线

spline interpolation 样条插值/样条内插

spline surface 样条曲面

smoothing spline 平滑样条

T
tolerance 允许精度

U
univariate function 一元函数

V
vector 向量

W
weight/weights 权重



4 偏微分方程数值解词汇英汉对照表


A    
absolute error 绝对误差

absolute tolerance 绝对容限

adaptive mesh 适应性网格

B   
boundary condition 边界条件

C
contour plot 等值线图

converge 收敛

coordinate 坐标系

D    
decomposed 分解的

decomposed geometry matrix 分解几何矩阵

diagonal matrix 对角矩阵

Dirichlet boundary conditions

Dirichlet边界条件

E     
eigenvalue 特征值

elliptic 椭圆形的

error estimate 误差估计

exact solution 精确解

G     
generalized Neumann boundary condition

推广的Neumann边界条件

geometry 几何形状

geometry description matrix 几何描述矩阵

geometry matrix 几何矩阵

H   
hyperbolic 双曲线的

I    
initial mesh 初始网格

J   
jiggle 微调

L   
Lagrange multipliers 拉格朗日乘子

Laplace equation 拉普拉斯方程

linear interpolation 线性插值

loop 循环

M   
machine precision 机器精度

mixed boundary condition 混合边界条件

N   
Neuman boundary condition Neuman边界条件

node point 节点

nonlinear solver 非线性求解器

normal vector 法向量

P   
Parabolic 抛物线型的

partial differential equation 偏微分方程

plane strain 平面应变

plane stress 平面应力

Poisson's equation 泊松方程

polygon 多边形

positive definite 正定

Q   
quality 质量

R   
refined triangular mesh 加密的三角形网格

relative tolerance 相对容限

relative tolerance 相对容限

residual 残差

residual norm 残差范数

S    
singular 奇异的
