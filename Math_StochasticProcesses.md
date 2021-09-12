
* 相关（Correlation） Linear: Gaussian Processes
   * Time Domain
   * Frequency Domain   
* 马尔可夫过程(Markov Property) Poisson Processes
   * Discrete Time
   * Continuous Time
* 鞅(martingale)： Financial App
   * Optional Theorem

相关的两种定义

E(XY)

Mean Square Error

E(Y-aX)^2

a=E(XY)/E(X^2)

E(X-E(X))E(Y-E(Y))=E(XY)-E(X)E(Y)

Linear correction

不相关（Uncorrelated) E(XY)=E(X)E(Y)=0

independence更强


几何上的看法 （Geometric View）：相关可以看作某种内积

E(XY)=<X,Y> Inner Product

<x,y>: H*H->R

1. 对称性 <X,Y>=<Y,X>
2. 非负性 <X,X>>=0, <X,X>=0 <=> X=0
3. Bilinear <X,aY+bZ>=a<X,Y>+b<X,Z>, <aX+bY,Z>=a<X,Z>+b<Y,Z>