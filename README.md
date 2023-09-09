# NSDI24-SIEVE
The repo for NSDI24 paper: SIEVE is Simpler than LRU: an Efficient Turn-Key Eviction Algorithm for Web Caches

<div style="text-align: center;">
  <img src="/doc/diagram/Sieve_illustration.svg" alt="diagram" width="480"/>
</div>

## Abstract
Caching is an indispensable technique for low-cost and fast data serving. The eviction algorithm, at the heart of a cache, has been primarily designed to maximize efficiency— reducing the cache miss ratio. Many eviction algorithms have been designed in the past decades. However, they all tradeoff throughput and/or simplicity to achieve high efficiency. Such a tradeoff often hinders adoption in production systems.

This work presents SIEVE, *an algorithm that is simpler than LRU and provides better than state-of-the-art efficiency and scalability* for web cache workloads. We implemented SIEVE in five production cache libraries, and it requires fewer than 20 lines of code change on average. Our evaluation using 1559 cache traces from 7 sources shows that SIEVE achieves up to 63.2% lower miss ratio than ARC. Moreover, SIEVE has lower miss ratio than 9 state-of-the-art algorithms on more than 45% of the 1559 traces, while the next best algorithm only achieves 15%. SIEVE’s simplicity comes with superior scalability as cache hits require no locking. Our prototype in Cachelib achieves twice the throughput of an optimized LRU at 16 threads. SIEVE is more than an eviction algorithm; it can be used as a cache primitive to build advanced eviction algorithms just like FIFO and LRU.


## Repo structure
The repo is a snapshot of [libCacheSim](https://github.com/1a1a11a/libCacheSim).


## Traces
The traces we used can be downloaded [here](https://ftp.pdl.cmu.edu/pub/datasets/twemcacheWorkload/cacheDatasets/).

The binary traces are [zstd](https://github.com/facebook/zstd) compressed and have the following format:
```c
struct {
    uint32_t timestamp;
    uint64_t obj_id;
    uint32_t obj_size;
    int64_t next_access_vtime;  // -1 if no next access
}
```
The compressed traces can be used with libCacheSim without decompression. And libCacheSim provides a tracePrint tool to print the trace in human-readable format.


### Citation
```bibtex
@inproceedings{zhang2024-sieve,
  title={SIEVE is Simpler than LRU: an Efficient Turn-Key Eviction Algorithm for Web Caches},
  author={Zhang, Yazhuo and Yang, Juncheng and Yue, Yao and Vigfusson, Ymir and Rashmi, K.V.},
  booktitle={USENIX Symposium on Networked Systems Design and Implementation (NSDI'24)},
  year={2024}
}
``` 