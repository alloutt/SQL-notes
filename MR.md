* Mapreduce is a prgramming module.
    * language used in MR:java,scala,python,R
    * MR is outdated and succeded by Spark,which is almost 10 times faster than MR.
* Sqoop is advanced,vast.

**HDFS deamons**: 
* NN
* DN
* SNN(secondaryNN)

**MR deamons**:
 * JobTracker ----which later become ---> RescourceManager
 * TaskTracker ----which later became --->NodeManager
 
 JT is master which is present in NN.
 TT is slave running in DN.
 
 **_lets see count words example_**

* a request is sent to NN,JT attents request later ask NN deamon to locate the required data
* NN gives DN's location,each DN has TT(like tt1,tt2,etc.),JT sends the written program by dev(java,scala,python,R) of word count to each DN
* DN creates container(container is a allocation of memory(RAM) and core(CPU) for processing of program.).then container is executed,at last result which is word count of specific words are merged and given back to NN.and displayed to user.

| | HDFS | input split | record reader | mapper	| shuffle & sort | Reducer | record writer
|---|---|---|---|---|---|---|---|
| | |(loaded in RAM)|(reads data line by line)|(apply logic,i.e.split data by " ")| |(aggregation)|(writing result in HDFS)
|DN1<br><br><br>DN2|this is java<br>this is scala<br><br>this is python|this is java<br>this is scala<br><br>this is python|this is java<br><br>this is scala<br><br>this is python|this,1<br>is,1<br>java,1<br>this,1<br>is,1<br>scala,1<br>this,1<br>is,1<br>python,1|this,1<br>this,1<br>this,1<br>is,1<br>is,1<br>is,1<br>java,1<br>scala,1<br>python,1|this,3<br>is,3<br>java,1<br>scala,1<br>python,1| |

**MapReduce**:

Phases--
* Map:Applies logic
* Reduce:Aggregates Result
<pre>
 HDFS--->input split : Data is loaded in memory(RAM)
 input split --->Record reader: Reads data sends to Mapper.
 record reader---->Mapper : Applies logic on data
 Mapper--->Shuffle,sort : Shuffle multiple node to single node,and sort asc or desc
 optional(combiner): mini reducer,combines result per node,reduceing load of suffling.
 optional(partitioner): partitioner makes sure combiner result goes is specific reducer machine
 shuffle,sort--->reducer : collect data from mapper and aggregate sends to record writer.
 reducer--->record writer : write data to HDFS.(reducer can be single machine or multiple)
</pre>
 e.g.Wordcount:
 	https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html
 Activity:Google this topic ,see diagramatic representration for reference.
 
