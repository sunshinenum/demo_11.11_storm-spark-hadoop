-_11.11_storm-spark-hadoop
==========================

hadoop_storm_spark结合实验的例子，模拟淘宝双11节，根据订单详细信息，汇总出总销售量，各个省份销售排行，以及后期的SQL分析，数据分析，数据挖掘等。
--------大概流程-------
第一阶段（storm实时报表）
(1)用户订单入kafka队列，
(2)经过storm，实时计算出总销售量，和各个省份的的销售量，
(3)将计算结果保存到hbase数据库中。 

第二阶段（离线报表）
(1)用户订单入oracle数据库，
(2)通过sqoop把数据导入hadoop上。
(3)使用mr和rdd对hadoop上的原始订单做etl清洗
(4)建立hive表和sparkSQL内存表。为后期分析做基础
(5)使用HQL实现业务指标分析，和用户画像分析，将结果存在mysql中。供web前台使用

第三阶段（大规模订单即席查询,和多维度查询）
(1)用户订单入oracle数据库，
(2)通过sqoop把数据导入hadoop上。
(3)写mr把hadoop的数据加载到hbase上
(4)使用hbase java api实现订单的即席查询
(5)solr绑定hbase，做多维度的条件查询

第四阶段（数据挖掘和图计算）
(1)用户订单入oracle数据库，
(2)通过sqoop把数据导入hadoop上。
(3)使用mr和rdd对hadoop上的原始订单做etl清洗
(4.1)使用mahout的关联规则做套餐推荐，mllib的als算法做协调过滤推荐。mllib的lr算法做是否购买的分类算法的推荐模块，mllib的kmeans对用户做聚类。寻找优质客户。
(4.2)使用graphX，寻找最热商品。基于图上的随机游走算法等图功能
--------大概流程-------