---
title: BLAST
author: Zerong Feng
date: 2024-02-14
parent: BASICS
layout: default
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

## 本地BLAST的基本步骤
1. 用makeblastdb为BLAST提供数据库
2. 选择blast工具，blastn,blastp
3. 运行工具，有必要的还可以对输出结果进行修饰

## 第一步：建立检索所需数据库
BLAST数据库分为两类，核酸数据库和氨基酸数据库，可以用makeblastbd创建。可以用help参数简单看下说明。

> 具体以拟南芥基因组作为案例，介绍使用方法：
> 注： 拟南芥的基因组可以在TAIR上下在，也可在ensemblgenomes下载。后者还可以下载其他植物的基因组

### 下载基因组
`wget ftp://ftp.ensemblgenomes.org/pub/plants/release-36/fasta/arabidopsis_thaliana/dna/Arabidopsis_thaliana.TAIR10.dna.toplevel.fa.gz`

`gzip -d Arabidopsis_thaliana.TAIR10.dna.toplevel.fa.gz`
### 构建核酸BLAST数据库
`makeblastdb -in Arabidopsis_thaliana.TAIR10.dna.toplevel.fa -dbtype nucl -out TAIR10 -parse_seqids`

### 下载拟南芥protein数据
`wget ftp://ftp.ensemblgenomes.org/pub/plants/release-36/fasta/arabidopsis_thaliana/pep/Arabidopsis_thaliana.TAIR10.pep.all.fa.gz`

### 构建蛋白BLAST数据库
`gzip -dArabidopsis_thaliana.TAIR10.pep.all.fa.gz`

`makeblastdb -in Arabidopsis_thaliana.TAIR10.pep.all.fa -dbtype prot -out TAIR10 -parse_seqids`


## 第二步：运行blast，调整输出格式

```shell
blastn -db BLAST/TAIR10 -query query.fa
# 还可以指定检索序列的位置
blastn -db BLAST/TAIR10 -query query.fa  -query_loc 20-100
# 或者使用远程数据库
blastn -db nr -remote -query query.fa
blastn -db nt -remote -query query.fa
```
## Reference
[这或许是我写的最全的BLAST教程][1]

[1]: https://www.jianshu.com/p/de28be1a3bea