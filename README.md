# hadoop-windows-config
Hadoop configuration files for Windows

In computing, reactive programming is a declarative programming paradigm concerned 
with data streams and the propagation of change. With this paradigm it is possible 
to express static (e.g., arrays) or dynamic (e.g., event emitters) data streams 
with ease, and also communicate that an inferred dependency within the associated 
execution model exists, which facilitates the automatic propagation of the changed 
data flow. Using this approach, we can eliminate a great deal of overhead by creating
systems which amount to applications running on micro-services.

Hadoop has the capability to manage large datasets by distributing the dataset into 
smaller chunks and performing parallel computation on it. Hadoop is an essential 
component of the Big Data industry as it provides the most reliable storage layer, 
HDFS, which can scale massively. Companies like Yahoo and Facebook use HDFS to 
store their data.

For this capstone project, we will be installing single node pseudo-distributed hadoop cluster on windows 10.

Configuration
=============

hdfs-site.xml
-------------
C:\Users\Edward\hadoop-3.1.0\hadoop-3.1\hadoop-3.1.0\data\namenode
C:\Users\Edward\hadoop-3.1.0\hadoop-3.1\hadoop-3.1.0\data\datanode

JDK Path
========
C:\Program Files\Java\jdk1.8.0_102
changed to (because of space)
C:\PROGRA~1\Java\jdk1.8.0_102

Formatting NameNode
-------------------
hdfs namenode –format

Start DFS
---------
cd C:\Users\Edward\hadoop-3.1.0\hadoop-3.1\hadoop-3.1.0\sbin

Start namenode and datanode with this command –

Deprecated
----------
start-dfs.cmd

Two more cmd windows will open for NameNode and DataNode

Now start yarn through this command-

start-yarn.cmd

Navigate to http://localhost:8088/cluster

===============================================================================
===============================================================================


Windows Configuration
=====================
https://cwiki.apache.org/confluence/display/HADOOP2/Hadoop2OnWindows


Start Hadoop
------------
C:\Users\Edward\hadoop-3.1.0\hadoop-3.1\hadoop-3.1.0\etc\hadoop\hadoop-env.cmd
%HADOOP_PREFIX%\bin\hdfs namenode -format
%HADOOP_PREFIX%\sbin\start-dfs.cmd

Format NameNode
---------------
%HADOOP_PREFIX%/bin/hadoop namenode -format -clusterID CID-1b36fd02-731b-4873-8e03-26cb4f9d7240


New Commands 
------------
hdfs namenode
hdfs datanode


Verify Daemons Are Running
--------------------------

(from root folder)
hdfs dfs -put myFile.txt /

%HADOOP_PREFIX%\bin\hdfs dfs -ls /


Start Yarn
----------
// don't need
%HADOOP_PREFIX%\sbin\start-all.cmd

// deprecated
%HADOOP_PREFIX%\sbin\start-dfs.cmd

// use this
%HADOOP_PREFIX%\sbin\start-yarn.cmd (Windows + x => run as administrator)


Set File Permissions
--------------------
$ chmod g-w c:/my/hadoop-2.7.1/tmp-nm/filecache
chmod u+rwx "C:\tmp\hadoop-Edward\nm-local-dir\nmPrivate"


Verify Cluster is Running
-------------------------
%HADOOP_PREFIX%\bin\yarn jar %HADOOP_PREFIX%\share\hadoop\mapreduce\hadoop-mapreduce-example
s-2.5.0.jar wordcount /myfile.txt /out


Test Cluster
------------
%HADOOP_PREFIX%\bin\yarn jar %HADOOP_PREFIX%\share\hadoop\mapreduce\hadoop-mapreduce-example
s-2.5.0.jar wordcount /myfile.txt /out


Temp Folder
-----------
C:\Users\Edward\AppData\Local\Temp


Stop All
--------
stop-dfs.cmd


Kill Process
------------
netstat -ano | findstr :yourPortNumber
taskkill /PID typeyourPIDhere /F

Start Solr
==========

cd "C:\Users\Edward\solr-6.3.0\bin"
cd "C:\Users\Edward\hadoop-3.1.0\hadoop-3.1\hadoop-3.1.0\solr-6.3.0"
./solr start –f

Start Solr Using HDFS
=====================
solr start -Dsolr.directoryFactory=HdfsDirectoryFactory -Dsolr.lock.type=hdfs -Dsolr.data.dir=hdfs://0.0.0.0:19000/datanode -Dsolr.updatelog=hdfs://0.0.0.0:19000/logs

