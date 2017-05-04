[sripagadala@ip-172-31-11-85 root]$ time hadoop jar /opt/cloudera/parcels/CDH-5.9.1-1.cdh5.9.1.p0.4/lib/hadoop-mapreduce/hadoop-mapreduce-examples-2.6.0-cdh5.9.1.jar teragen -Dmapreduce.job.maps=4 -D dfs.block.size=33554432 100000000 /user/sripagadala/teragen.out

real    2m24.434s
user    0m6.063s
sys     0m0.261s
[sripagadala@ip-172-31-11-85 root]$ hadoop fs -du -s -h /user/sripagadala/teragen.out
9.3 G  18.6 G  /user/sripagadala/teragen.out

[sripagadala@ip-172-31-11-85 root]$ time sudo -u hdfs hadoop jar /opt/cloudera/parcels/CDH-5.9.1-1.cdh5.9.1.p0.4/lib/hadoop-mapreduce/hadoop-mapreduce-examples-2.6.0-cdh5.9.1.jar  terasort /user/sripagadala/teragen.out /user/hduser/terasort-output.out

real    6m16.941s
user    0m9.119s
sys     0m0.354s
