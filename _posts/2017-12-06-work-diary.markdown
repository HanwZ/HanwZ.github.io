---
layout:       post
title:        "工作日志"
subtitle:     "oracle 改造性能测试"
date:         2017-12-06 23:00:00
author:       "Han"
header-img:   "img/in-post/post-eleme-pwa/eleme-at-io.jpg"
header-mask:  0.3

---

# 近期的工作
## 性能测试
>近期在单位主要的工作就是性能测试，用**[Loadrunner](https://baike.baidu.com/item/loadrunner/1926633?fr=aladdin)**跑脚本，监控系统性能参数.过程中遇到了各种各样的问题，先简单总结一下

* ###数据库索引

    刚迁移完数据时发现性能测试很慢，后来排查发现是部分索引没有建。
* ###oracle统计信息

    oracle查询计划依赖统计信息，在数据量变化较大的时候就需要更新统计信息，否则可能用不到索引导致查询缓慢。
* ###性能测试产生的数据对测试结果有影响

    测试过程中，由于oracle是新环境，测试的次数也比sybase要多不少，每次跑测试产生的数据在十万量级，积累下来，sybase与oracle的数据量差距达到几百万，并且都是交易相关的数据，导致oracle部分sql的查询结果集很大，速度受到影响。今天手动清除了数据并更新了统计信息，明天计划搞一个脚本每天自动处理
    
* ###loadrunner脚本配置不一致

    loadrunner运行时参数选择忽略思考时间，不记录log。脚本中可以选择action的iteration次数与用户的选择方案，测试过程中这两项选择的不同也会导致测试结果不同。
    
>测试过程中也遇到了一些坑，记录一下

###1. 申请的测试机性能不一致

sybase数据库为8c16G，oracle为4c8G，应用服务器也分别是这个配置。导致测试的oracle的性能比sybase还差。

	
	

 
	
	
