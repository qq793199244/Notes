### 聚集索引与非聚集索引的区别

可以按以下四个维度回答：

（1）一个表中只能拥有一个聚集索引，而非聚集索引一个表可以存在多个。

（2）聚集索引，索引中键值的逻辑顺序决定了表中相应行的物理顺序；非聚集索引，索引中索引的逻辑顺序与磁盘上行的物理存储顺序不同。

（3）索引是通过二叉树的数据结构来描述的，聚集索引的叶节点就是数据节点，而非聚簇索引的叶节点仍然是索引节点，只不过有一个指针指向对应的数据块（非聚集索引的叶节点保存指向数据项的指针）。

（4）聚集索引的插入、更新数据速度比非聚集索引慢，但查询数据的速度更快。
