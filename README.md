# MapReduceExample
This project contains the files to run a map and reducer to follow the tutorial on how to run a MapReduce job in Azure. This tutorial is based on Chapter 16 of Python for Programmers. 

The tutorial video:
https://youtu.be/H9J6pIHbuJw 

The text file used can be downloaded here:

https://www.gutenberg.org/files/1513/1513-0.txt

Command to move files to your cluster:

```scp length_mapper.py length_reducer.py romeojulieta.txt sshuser@clustername-ssh.azurehdinsight.net:```

Command to connect to your cluster:

```ssh sshuser@clustername-ssh.azurehdinsight.net```

Command to move the files in your cluster to the HDFS

```hadoop fs -copyFromLocal romeojulieta.txt /example/data/romeojulieta.txt```



Command to run your MapReduce job:

``` yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar
   -D mapred.output.key.comparator.class=org.apache.hadoop.mapred.lib.KeyFieldBasedComparator   
   -D mapred.text.key.comparator.options=-n  
   -files length_mapper.py,length_reducer.py   
   -mapper length_mapper.py
   -reducer length_reducer.py   
   -input /example/data/romeojulieta.txt   
   -output /example/wordlengthsoutput   
```
