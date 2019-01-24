# GIAC-2019
Global Artificial Intelligence Conf demo 2019

# Install Everything
```shell
mkdir ~/GIAC-DW-demo
cd ~/GIAC-DW-demo
wget http://mirror.reverse.net/pub/apache/kafka/2.0.0/kafka_2.11-2.0.0.tgz 
tar -xzf kafka_2.11-2.0.0.tgz

git clone https://github.com/Data-Whisperers/GIAC-2019.git
cd GIAC-2019/tailer2kafka/
mvn clean install
cd ../kafkaConsumerMeetup/
mvn clean install
```

# Run Everything
- **Kafka**
  - Window 1: `cd ~/GIAC-DW-demo/kafka_2.11-2.0.0;bin/zookeeper-server-start.sh config/zookeeper.properties`
  - Window 2: `cd ~/GIAC-DW-demo/kafka_2.11-2.0.0;bin/kafka-server-start.sh config/server.properties`
  - Window 3: `cd ~/GIAC-DW-demo/kafka_2.11-2.0.0;bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic meetupstream`
- **Meetup Kafka demo**
  - Window 1: `cd ~/GIAC-DW-demo/GIAC-2019/tailer2kafka;bin/run_curl_meetup_stream.sh`
  - Window 2: `cd ~/GIAC-DW-demo/GIAC-2019/tailer2kafka;bin/run_tailer2kafka.sh`
  - Window 3: `cd ~/GIAC-DW-demo/GIAC-2019/kafkaConsumerMeetup;bin/run_kafkaConsumerMeetup.sh`
  - Window 4: `tail -F /var/tmp/meetupstream`
  - Window 5: `tail -F /var/tmp/tailer2kafka.log`
  - Window 6: `tail -F /var/tmp/kafkaConsumerMeetup.log`
