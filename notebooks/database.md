## share-nothing与share-storage的区别

传统意义上认为，每个节点有独立的计算和存储功能并且节点之间不共享数据就是 Shared Nothing，计算节点独立并且共享一个不带计算功能的存储集群就是 Shared Storage。

## true time的意义

First, **it uses them as proper timestamps for write transactions without the need for global communication**. Second, it uses them as timestamps for strong reads, which enables strong reads to execute in one round of communication, even strong reads that span multiple servers.

