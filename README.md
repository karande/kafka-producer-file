##Introduction
Code to add data from file line by line into Kafka

##Prequisites- Set up KAFKA
###Step 1: Download the code
Download the 0.8.2.0 release and un-tar it.
```
> tar -xzf kafka_2.10-0.8.2.0.tgz
> cd kafka_2.10-0.8.2.0
```

###Step 2: Start the server
Kafka uses ZooKeeper so you need to first start a ZooKeeper server if you don't already have one. You can use the convenience script packaged with kafka to get a quick-and-dirty single-node ZooKeeper instance.

```
> bin/zookeeper-server-start.sh config/zookeeper.properties
[2013-04-22 15:01:37,495] INFO Reading configuration from: config/zookeeper.properties (org.apache.zookeeper.server.quorum.QuorumPeerConfig)
...
```
Now start the Kafka server:
```
> bin/kafka-server-start.sh config/server.properties
```
[2013-04-22 15:01:47,028] INFO Verifying properties (kafka.utils.VerifiableProperties)
[2013-04-22 15:01:47,051] INFO Property socket.send.buffer.bytes is overridden to 1048576 (kafka.utils.VerifiableProperties)

###Step 3: Create a topic

Let's create a topic named "test" with a single partition and only one replica:
```
> bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
```

We can now see that topic if we run the list topic command:
```
> bin/kafka-topics.sh --list --zookeeper localhost:2181
test
```

##Details:
KafkaFileProducer performs following tasks:

1) Read data from dataset/Processed_subject101.dat file

2) For each line in the file it creates a message of type  (Key,Value) where key is line number and
value is actual line


Following default variables can be changed to add data for your choice into kafka.

Default Topic name: test

Default file used: dataset/Processed_subject101.dat 

##Validate:
Run KafkaFileProducer and verify that data is loaded into Kafka using following command
```
> bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning
30.25,2.80333,9.5201,4.86089,2.66338,10.2871,5.16317,-0.0774208,-0.117665,0.105727,-9.46798,-54.505,-33.3918,1,0,0,0,33.625,-0.210245,9.76588,-1.38721,-0.335559,9.77131,-1.22859,0.0896249,-0.0378112,-0.037197,0.276133,-59.7344,16.1858,1,0,0,0,33,9.84219,0.511835,-0.651625,9.82576,0.682181,-0.182073,-0.00553086,-0.0257234,0.00726291,-131.076,10.6035,-6.78933,1,0,0,0,5
30.25,2.62452,10.5845,4.9316,2.42503,10.5305,5.25349,0.641135,-0.0649068,0.133527,-8.6943,-54.1086,-33.8593,1,0,0,0,33.625,-0.13506,9.80304,-1.42469,-0.230575,9.68045,-1.18415,0.0136997,-0.0642584,-0.034991,0.381789,-59.5145,16.1877,1,0,0,0,33,9.76984,0.359471,-0.535653,9.84071,0.667041,-0.197239,-0.0178811,0.0137628,0.0107517,-130.856,10.6022,-7.28625,1,0,0,0,5
30.25,2.36427,10.6255,5.04302,2.07469,9.67259,5.67855,1.01104,-0.0771391,0.180579,-8.80487,-53.8846,-33.8556,1,0,0,0,33.625,-0.0571406,9.5774,-1.3451,-0.140908,9.57458,-1.16989,0.0564232,-0.0479727,-0.0264942,0.254743,-59.1773,16.4314,1,0,0,0,33,9.80826,0.549077,-0.536436,9.82569,0.667038,-0.197159,-0.0389267,-0.00497049,0.0120961,-131.191,10.3966,-7.53326,1,0,0,0,5
```

###Works Cited
<https://github.com/apache/kafka>
