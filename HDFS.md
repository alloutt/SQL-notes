### NN :
master
* work with DN
* receive HB(HeartBeat) from DN
* receive Block report from DN 
* Metadata fsimage geditlog 
* metadata will RAM 

### DN :
Slave 
* Accept cmds from NN 
* Data will store in DN 
* send HB to NN 
* Send Block report to NN 
HDD

### SNN: secondary namenode / checkpoint node 
* accept fsimage + geditlog  merge every 8-10 min interval
updated

NN required that --> SNN -> send 

**_eXTRA study:_** High Availability,Single point of access

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++==

### Failure Scenarios:
If DATANODE goes DOWN ,blocks become inaccessible...to overcome this _**REPLICATION**_ concept is used.
## Replication:
* Replication -factor default 3 means each block have 3 copies
* if a block fails the NN will tell DN to again maintain replication factor and create copies further

    Extra study:RackAwarness

## Rack Awareness:
 ```(Rack is collection of servers in data stores)```
* Its an algorithm that suggest of u have replication factor applied store 2 block in same rack on different node/server and 1 block in totally different rack

* _**scene:**_ if node fails it will access another node in same rack because of high performance compare too the node in another rack
* _**scene2**_ :if any rack fails data will still be accessible even if its slow
<pre>
_ r1 _  _ r2 _   _r3 _
|     | |     | |     |
| dn1 | | dn4 | | nn  |        same block in dn1,dn2,dn4
|     | |     | |     |
| dn2 | | dn5 | |     |
|     | |     | |     |
| dn3 | |     | |     |
</pre>
* https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/RackAwareness.html
## NameNode SafeMode:
It is a state/phase of NN when it does not allow in write operation or replication operation
At initial phase NN is updating metadata in safemode.

* to check safemode state
```
hadoop dfsadmin -safemode get
```
* to enter safemode state
```
hadoop dfsadmin -safemode enter
```
* to leave safemode state
 ```
hadoop dfsadmin -safemode leave
```
> [!NOTE]
> read data is allowed

**Scenario:** NameNode failure,which is SPOF(SinglePointOfFailure) in version 1 to overcome this in version 2
## High Availability:
* Placing one more server as NameNode,but only one will be active at a time.
* Two Nodes switches in between sharing common metadeta storage called Journal nodes,each node has FailoverController which reports Heartbeat of NN to ZooKeeper,Zookerper send signal to FailoverController of another node after failure of namenode,vice versa.
* one fail another start,another fail,first start. 
* https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HDFSHighAvailabilityWithNFS.html

## HDFS federation:
* for every block stored in datanodes,150byte of metadeta is stored in namenode.
* if no. of block increase,metadata will also increase.this metadata will take load on NameNode.this was overcome with **HDFS Federation**
* Multiple NameNodes are used ,with all active having shared block pool of all datanodes.the data will be stored all across datanodes but the metadata will be stored at specific namenode called **namespace**.
* **Block pool** responsible to manage the block.
* https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/Federation.html



