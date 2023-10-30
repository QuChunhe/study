

1. 切词 word segmentation
2. 规范化 normalization
3. 去重 distinct
4. 字典序 sorted

FST

Trie树（字典树）

* 正向索引：doc中查询keyword
* 倒排索引：从keyword查找doc。

倒排索引的数据结构包括
1. DocID：文档id
2. TF：词频，即在文档中出现的次数
3. Pos：在文档中的位置


int有序数组，匹配某个term的所有id。压缩算法
* FOR算法（Frame Of Reference）稠密数组的压缩
* RBM算法（Roaring Bit Map）稀疏数组


在创建索引之前，会对文档中的字符串进行分词。ES中字符串有两种类型，keyword和text。
* keyword类型的字符串不会被分词，搜索时全匹配查询
* text类型的字符串会被分词，搜索时是包含查询

ES倒排索引包括
* Term Index
* Term Dictionary：索引的最小单位，记录term到posting list的关联关系
* Postig List：有倒排索posting组成，包括
  * 文档id
  * 词频TF
  * position，term在文档中分词的位置，用于phrase query
  * offset，记录单词的开始结束位置，实现高亮显示

其中Term Index在内存中存储，Term Dictionary和Posting List在磁盘中。一次搜索的步骤就是：
1. 搜索Term Index树找到对应Term Dictionary中的offset，因为匹配到的可能只是一个前缀，需要再顺序往后找，直到匹配
2. 通过Term Dictionary找到对应的Posting List


term index是一个抽象的数据结构，为了加速当前词项检索的，底层是用的FST(Finite State Transducer)数据结构。


ES针对还额外做了两点优化：
1. Term Dictionary 在磁盘上面是分 block 保存的，一个 block 内部利用公共前缀压缩，比如都是 Ab 开头的单词就可以把 Ab 省去
2. Term Index 在内存中是以 FST（finite state transducers）的数据结构保存的
3. posting list。


term index存储在.tip文件。Term Dictionary 存储在.tim文件中


联合索引
* 使用skip list
* 使用bitset

Elasticsearch 支持以上两种的联合索引方式，如果查询的 filter 缓存到了内存中（以 bitset 的形式），那么合并就是两个 bitset 的 AND。如果查询的 filter 没有缓存，那么就用 skip list 的方式去遍历两个 on disk 的 posting list。

对于使用Elasticsearch进行索引时需要注意:
* 不需要索引的字段，一定要明确定义出来，因为默认是自动建索引的，"index": false
* 对于text类型的字段，不需要analysis的也需要明确定义出来，因为默认也是会analysis的，可以使用keyword
* 选择有规律的ID很重要，随机性太大的ID(比如java的UUID)不利于查询


单词词典有两种数据结构实现
* B+数
* Hash


score
* BM25：7.0以后默认
* TF-IDF

三个指标
* 速度：高效的压缩和快速的编码和解码
* 准确（相关度）：两种算法BM25和TF-IDF
* 召回率


