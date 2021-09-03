Gakhov, Andrii, Probabilistic data structures and algorithms for big data applications, Books on Demand, 2019


Marcello La Rocca, Advanced Algorithms and Data Structures, Manning Publications, 2021

Sequential and Parallel Algorithms and Data Structures: The Basic Toolbox

Peter Brass, Advanced Data Structures, Cambridge University Press,2008


# Hash Tables（散列表）

slots/buckets/segement(槽/桶/段)


# Slides


[Data Structures and Algorithms for Big Databases](https://www.slideshare.net/omnidba/data-structures-and-algorithms-for-big-databases)

For on-disk data, one sees funny tradeoffs in the speeds of data ingestion, query speed, and freshness of data.

Better data structures significantly mitigate the insert/query/freshness tradeoff.

These strunctures scale to much larger sizes while efficiently using the memory-hierarchy.


Module1: I/O Model and Cache-Oblivious Analysis

How computation works
* Data is transferred in blocks between RAM and disk.
* The number of block transfers dominates the running time.

Goal: Minimize number of block transfers
* Performance bounds are parameterized by block size B, memorysize M, data size N.

Module 2: Write-Optimized Data Structures

* Write-optimized structures significantly mitigate the insert/query/freshness tradeoff.
* One can insert 10x~100x faster than B-Trees while achieving similar point query performance.


