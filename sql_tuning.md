## SQL Tuning


#### Uncovering bottlenecks:

It is important to figure out what is going wrong and where it is going wrong, we need to find the bottle necks in our system.

##### Benchmarking

Testing a single operation on a quite system isn't benchmarking, it is how a set of operations work over a period of time, benchmarks are typically long running and eloborate perf tests, where the results could dictate high-level choices such as hardware and storage config, or how soon to upgrade and stuff.

Whenever you're bench marking MySQL, make sure you test with some features turned on and off, most importantly `adaptive hash index` for InnoDB tables.

Read about above adaptive hash index [here](https://www.percona.com/blog/2016/04/12/is-adaptive-hash-index-in-innodb-right-for-my-workload/).

##### Slow query log

Enable MySQL's slow query log and find out which queries are taking more amount of time than expected.

#### Improving the schema

1. CHAR instead of VARCHAR wherever possible.
2. Use TEXT for larger blocks of text like blog posts.
3. Use INT for numbers upto 2^32 or 4 Billion
4. Use DECIMAL for currently to avoid floating point representation errors.
5. Avoid BLOBS, use object store and store location.
6. Set the NOT NULL constraint where application to improve search performance.
7. Use good indices, columns that you are querying could be faster with them in indices.

Indices are represented using self balancing B-trees that keeps data sorted and allows searches, sequential access, insertions and deletions in log time. Placing an index keeps the data in memory, requiring more space, writes might get slower 'cos indices needs to be updated. When loading larger amount of data, disable indices, load, then rebuild might help.

8. Denormalize when performance demands it.
9. Query cache might lead to perf issues. 