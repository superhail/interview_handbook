## cflushopt,clwb

说下我一般的用法，不一定能代表Intel官方（主要是我也没看到过官方有这块的详细说明, @吴国安 你有啥信息，可以帮忙补充下):

 1. 对于大块数据的写，如果后续不会马上有读它的操作，可以考虑用non-temporal write指令去做，避免先读了污染CPU cache。不过non-temporal write后也需要调用下mfence，来确保数据在其它CPU或者core上可见。
 2. 对于需要小块数据 (cacheline大小)，或者写后马上可能被读的大块数据，我一般用clwb + mfence

另外，我理解即使调用clflush，如果要保证跟后续指令的顺序关系，中间也是要调用下fence的。



关于clwb效率比clflush/clflushopt高的问题：
 1. clwb在cascade平台上，不会保留cacheline在cache中，所以跟clflushopt是一样的。我记得是在icelake后，clwb才会在flush后，保留数据在cacheline上
 2. clwb/clflushopt效率比clflush高的主要原因是他们可以pipline执行，不像clflush，必须要等前一个flush结束，才能执行下一个





