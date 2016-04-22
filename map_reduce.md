**How to run a map reduce job**

https://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html#Walk-through

1.

become hdfs user
sudo -u hdfs -i

2.

Create a folder for the input

hdfs dfs -mkdir /wc_input

If you want to generate data:
yarn jar /usr/hdp/2.4.0.0-169/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen 1000000 /teragenOut
else:

2.

Download and/or copy your file to input folder
$ hdfs dfs -moveFromLocal pg11.txt /wc_input
$ hdfs dfs -ls /

3.

Create java project

4.

set environment variables are set as follows:

export JAVA_HOME=/usr/java/default
export PATH=${JAVA_HOME}/bin:${PATH}
export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar

5.

Compile WordCount.java and create a jar:

$ hadoop com.sun.tools.javac.Main WordCount.java
$ jar cf wc.jar WordCount*.class  (in our case: $ yarn jar wc.jar WordCount /wc_input /wc_output)

6.

Create external tabble using hive:

create external table movies(
userid INT,

movieID INT,
rating INT,
unixtime STRING,
row format delimited
fields terminated by ':',
LOCATION '/datasets/'
)

7.

Execute this command in hive to order your output records

hive -e 'select * from warcount order by count;' > warcount.tsv



