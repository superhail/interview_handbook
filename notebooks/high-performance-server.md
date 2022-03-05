**一致性哈希，一致性哈希的一致性是什么意思**


一种常用的负载均衡方式是，对资源o的请求使用`hash(o) = o mod n`来映射到某一台缓存服务器。当增加或减少一台缓存服务器时这种方式可能会改变所有资源对应的hash值，也就是所有的缓存都失效了，这会使得缓存服务器大量集中地向原始内容服务器更新缓存

But, more importantly, **if a server fails and is removed from the circle, only the BLOBs that were mapped to the failed server need to be reassigned to the next server in clockwise order**. Likewise, if a new server is added, it is added to the unit circle, and only the BLOBs mapped to that server need to be reassigned.

