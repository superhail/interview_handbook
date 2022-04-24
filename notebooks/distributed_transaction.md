## percolator

被设计用来incremental processing

1. prewrite

   写入每个lock，包含[start_ts]，包含一个primary lock

2. commit

   写入primary lock的data write，[start_ts, commit_ts]。其他的异步进行

读

取一个读的ts

检查一下，看看是否在[0, ts]有写的lock，如果有就abort



rocksdb的优化，检查一下，看看transaction record(primary record)是否真的还没提交

## polardb-x

