Gakhov, Andrii, Probabilistic data structures and algorithms for big data applications, Books on Demand, 2019


Marcello La Rocca, Advanced Algorithms and Data Structures, Manning Publications, 2021

[repo](https://github.com/mlarocca/AlgorithmsAndDataStructuresInAction#trie)

Sequential and Parallel Algorithms and Data Structures: The Basic Toolbox

Peter Brass, Advanced Data Structures, Cambridge University Press,2008


* O-notation characterizes an upper bound on the asymptotic behavior of a function.
* \Omega-notation characterizes a lower bound on the asymptotic behavior of a function
* \Theta-notation characterizes a tight bound on the asymptotic behavior of a function.

# Hash Tables（散列表）

slots/buckets/segement(槽/桶/段)


SHA（Secure Hash Algorithm），安全哈希算法，包括SHA-1、SHA-256、SHA-512等。

* MD5（Message Digest Algorithm 5），消息摘要算法第五版。128-bits的算法。经过程序流程，生成四个32位数据，最后联合起来成为一个128-bits散列

* SHA-1：Secure Hash Algorithm 1 安全散列算法1。SHA-1可以生成一个被称为消息摘要的160位（20字节）散列值，散列值通常的呈现形式为40个十六进制数。

* SHA-2。 SHA-224, SHA-256, SHA-384, SHA-512, SHA-512/224, and SHA-512/256并称为SHA-2。

* SHA-3。之前名为Keccak算法，是一个加密杂凑算法

Typically, an ordered set is implemented with a binary search tree or a btree, and an unordered set is implemented with a hash table.

# Tree（树）

是否有序
* 无序树：树中的节点之间没有顺序关系
* 有序树：树中的节点之间存在预先定义的顺序关系

按照节点包含子树个数：
* 二叉树：每个节点最多含有两个子树的树称为二叉树;
   * 二叉查找树：首先它是一颗二叉树，若左子树不空，则左子树上所有结点的值均小于它的根结点的值;若右子树不空，则右子树上所有结点的值均大于它的根结点的值;左、右子树也分别为二叉排序树;
   * 满二叉树：叶节点除外的所有节点均含有两个子树的树被称为满二叉树;
   * 完全二叉树：如果一颗二叉树除去最后一层节点为满二叉树，且最后一层的结点依次从左到右分布
   * 霍夫曼树：带权路径最短的二叉树。
   * 红黑树：红黑树是一颗特殊的二叉查找树，每个节点都是黑色或者红色，根节点、叶子节点是黑色。如果一个节点是红色的，则它的子节点必须是黑色的。
   * 平衡二叉树(AVL)：一 棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树
* B树和B+树




二叉查找树（Binary Search Tree），平衡二叉查找树（Balanced Binary Search Tree），红黑树(Red-Black Tree )是典型的二叉查找树结构，其查找的时间复杂度O(log2N)与树的深度相关

B-tree/B+-tree/ B*-tree (B~Tree)。B 树是为了磁盘或其它存储设备而设计的一种多叉平衡查找树



平衡二叉树balanced binary tree

AVL 树得名于它的发明者 G. M. Adelson-Velsky 和 Evgenii Landis，他们在1962年的论文《An algorithm for the organization of information》中公开了这一数据结构


* 节点的层次：从根开始定义，根为第一层，根的子节点为第二层，以此类推。
* 深度：对于任意节点n，n的深度为从根到n的唯一路径长，根的深度为0（从上往下看）
* 高度：对于任意节点n，n的高度为从n到一片树叶的最长路径长，所有树叶的高度为0；（从下往上看）


# Finite State Machine (FSM)

[Index 1,600,000,000 Keys with Automata and Rust](https://blog.burntsushi.net/transducers/)

* Finite State Acceptor (abbreviated FSA).
* FST(Finite state transducer)

The only difference between a trie and the FSAs shown in this article is that a trie permits the sharing of prefixes between keys while an FSA permits the sharing of both prefixes and suffixes.

# Slides


[Data Structures and Algorithms for Big Databases](https://www.slideshare.net/omnidba/data-structures-and-algorithms-for-big-databases)

For on-disk data, one sees funny tradeoffs in the speeds of data ingestion, query speed, and freshness of data.

Better data structures significantly mitigate the insert/query/freshness tradeoff.

These strunctures scale to much larger sizes while efficiently using the memory-hierarchy.


Module 1: I/O Model and Cache-Oblivious Analysis

How computation works
* Data is transferred in blocks between RAM and disk.
* The number of block transfers dominates the running time.

Goal: Minimize number of block transfers
* Performance bounds are parameterized by block size B, memorysize M, data size N.

Module 2: Write-Optimized Data Structures

* Write-optimized structures significantly mitigate the insert/query/freshness tradeoff.
* One can insert 10x~100x faster than B-Trees while achieving similar point query performance.

A balanced binary tree with buffers of size B


Module 4: Paging

Goal: minimize number block transfers

When a blaock is cached, the access cost is 0. Otherwise it's 1.

Paging Algorithms
* LRU (least recently used): Discard block whose most recent access is earliest.
* FIFO (first in, first out): Discard the block brought in longest ago.
* LFU (least frequently used): Discard the least popular block.
* Random
* LFD (longest forward distance)=OPT: Discard block whose next access is farthest in the future.

Module 5: What to Index

1. Indexes can reduce the amount of retrieved.
2. Indexes can improved locality
   * Not all data access cost is the same
   * Sequential access is MUCH faster than random access
3. Indexes can presort data
   * GROUP BY and ORDER BY queries do post-retrieval work
   * Indexing can help get rid of this work.


An index can select needed rows.

Module 6: Log Structured Merge Trees


Module &: Bloom Filters

[Probabilistic algorithms for fun and pseudorandom profit](https://bravenewgeek.com/tag/count-min-sketch/)

[Data Stream Algorithms](http://keshavbashyal.github.io/blog/2015/12/19/data-stream-algorithms/)

[CS 598: Algorithms for Big Data](https://courses.engr.illinois.edu/cs598csc/fa2014/)

[CMPSCI 711: More Advanced Algorithms](https://people.cs.umass.edu/~mcgregor/courses/CS711S12/index.html)

#  

Nearest neighbor search

GEOHASH

# common method

## Decrease and Conquer 减而治之

[Decrease and Conquer](https://iq.opengenus.org/decrease-and-conquer/)


## Backtracking 回溯

Backtracking can be defined as a general algorithmic technique that considers searching every possible combination in order to solve a computational problem


## Greedy Algorithm

