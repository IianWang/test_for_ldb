# 关于leveldb及以太坊用leveldb作为底层存储细节
 

## leveldb历史及现状
  leveldb 于2011年由google团队设计，起因是Jeff Dean和Sanjay Ghemawat希望创建一个类似于Bigtable平板电脑堆栈的系统，该系统具有最小的依赖性，适用于开放源代码，也适用于Chrome中的IndexedDB实现。现今LevelDB用作Google Chrome的IndexedDB的后端数据库，并且是Riak支持的后端之一。此外，Bitcoin Core和go-ethereum 使用LevelDB数据库存储区块链元数据。
  
## leveldb本质
**leveldb全称为level data base，可以把它理解为一个底层数据库，但它不是关系型数据库，那么啥是"关系型数据库"呢?下面是对"关系型数据库"与非关系型数据库的个人总结。**
- 关系型数据库
  - 操作方便，用户友好。 PS:像我们都可以用sql从关系型数据库中操作数据，sql是一种特定目的编程语言，用于管理关系数据库管理系统（RDBMS），或在关系流数据管理系统（RDSMS）中进行流处理。
  - 存储数据结果清晰，格式易看懂，数据都是按照行列进行存储，统一放在一个或多个表中。
  - 内存占用大。 PS:这也就是为什么许多产品的数据底层存储都是采用非关系型数据库了，当然这一其中的一个原因。
- 非关系型数据库
  - 难操作，新手体验差。 PS:当然了作为数据底层库，根本就不是给你萌新设计的。当时的设计理念为简化存储过程，节约存储空间，提高写入速度，增加可拓展性。
  - 存储结构不固定，格式有是基于文档的，Key-Value键值对的，还有基于图的等。所以说存储形态相当~的灵活。

leveldb存储结构要根据不同的产品进行特定的方式存储，数据格式为Key-Value键值对。

## 以太坊存储与leveldb

![d035d9dcb941d998b8b744d9c4a6d9cc.png](en-resource://database/1365:0)
**那么这个"层级"要怎样解释呢？如上图**
