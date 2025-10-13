---
date: 2024-09-16
tags: 
link:
---



# Kafka

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.


## Kafka with Zookeeper [[Kafka with zookeeper]]

1.  Go to kafka > config folder 
2.  Open zookeeper.properites file, change the dataDir to `dataDir=C:/kafka/zookeeper-data` create `zookeeper-data` folder if it is not there.
3.  Open server.properties file, change the log.dirs to `log.dirs=C:/kafka/logs` 
4. Go to kafka folder and execute those below command
```shell
# start zookeeper
.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

# start kafka
.\bin\windows\kafka-server-start.bat .\config\server.properties

# create topic
.\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092  --create --topic kafkaLearning-topic --partitions 3 --replication-factor 1
# list of topic you have created
.\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --list
# describe the topic
.\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --describe --topic kafkaLearning-topic

# Create producer and enter the value you need to send to the consumer
.\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic kafkaLearning-topic

# Create consumer and consume the things which the consumer send
.\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic kafkaLearning-topic

```


## Kafka without Zookeeper [[Kafka without zookeeper]]

1.  Go to kafka > config > kraft folder 
2.  Open server.properties file, change the `log.dirs=/tmp/kraft-combined-logs` to `log.dirs=C:/kafka/logs` so that logs will be stored in this folder.
3.  Go to kafka folder and execute those below command
```shell
# Generate a Cluster UUID
$KAFKA_CLUSTER_ID = & "bin\windows\kafka-storage.bat" random-uuid

# Format Log Directories
& "bin\windows\kafka-storage.bat" format -t $KAFKA_CLUSTER_ID -c config\kraft\server.properties

# start kafka
.\bin\windows\kafka-server-start.bat .\config\kraft\server.properties

# create topic
.\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092  --create --topic kafkaLearningKraft-topic --partitions 3 --replication-factor 1

# list of topic you have created
.\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --list
# describe the topic
.\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --describe --topic kafkaLearningKraft-topic

# Create producer and enter the value you need to send to the consumer
.\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic kafkaLearningKraft-topic

# Create consumer and consume the things which the consumer send
.\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic kafkaLearningKraft-topic
```