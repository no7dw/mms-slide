# MMS关键指标意义&各数值区间意义

------
# What's MMS
MongoDB Management Service (MMS) is a suite of services for managing MongoDB deployments.

# 统计图表的数据来源
all statistics can show in mongo shell by:

    >db.serverStatus()

## 

 1. opcounters
意义：The average number of commands performed per second since the last data point
代表忙不忙，越小越好。（看业务）
 2. queue
The number of operations queued waiting for any lock －－ 排队未执行的命令
越小越好，平时<1
 3. connection
The number of currently active connections to this server. A stack is allocated per connection; thus very many connections can result in significant RAM usage.
越小越好。
=client (connected) * 集群server 数目
 4. lock
The percent of time write locked. The effective lock % is the percent of time in the global lock plus the percent of time locked by the hottest database. Because the data is sampled and combined, it is possible to see values over 100%.
越小越好。
造成锁增加的行为：update delete insert ...
 5. Btree
A large number of misses means that you are indexes are too big to fit in RAM, which can cause a significant performance penalty －－ 因为数据不再mem,从disk 加载到mem。
mongodb 使用 btree index
missratio ＝ misses/access 最好是0
access:  The number of times the btree indexes have been accessed. 
hits:The number of times a btree page was in memory
misses: The number of times a btree page was not in memory
注意：不要只看一条线
 6. Asserts
The number of regular asserts raised since this process started
"asserts" : {
        "regular" : <num>,
        "warning" : <num>,
        "msg" : <num>,
        "user" : <num>,
        "rollovers" : <num>
},
不要只看一条线
 7. Page faults
The number of page faults on this process. In non-Windows environments this is hard page faults only.
越小越好。

ref:[link][1]


  [1]: http://www.cnblogs.com/no7dw/archive/2013/02/20/2918372.html
 
