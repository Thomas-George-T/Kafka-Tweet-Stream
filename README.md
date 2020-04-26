# Kafka Twitter Streaming

Twitter Streaming using a Kafka 2.1 producer using safe, idempotence and compression configurations resulting in a high throughput producer.




## Environment
- Java JDK 1.8
- Twitter Developer Account
- Kafka 2.11
- Zookeeper
- Windows/Linux
- Maven

## Prerequisites 

Ensure that Zookeeper & Kafka servers are up and running *( Open in separate terminal windows if necessary )*.

Command to start Zookeeper

```
zookeeper-server-start.sh config/zookeeper.properties
```

Command to start Kafka server

```
kafka-server-start.sh config/server.properties
```

## Installation steps

After cloning this repo,

1. Run the maven `clean install` command

```
mvn clean install
```

Maven will now generate a `target` directory with the jar `Kakfa-Streaming-1.0-shaded.jar`

2. Move into the `target` directory

```
cd target
```

## Execution steps

### To execute the Producer class

1. Run the kafka console consumer in another terminal window with the following `topic` and `group` parameters

```
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TwitterTopic --group Twitter-Consumer-Group
```

2. Execute the TwitterProducer class from the shaded jar

```
java -cp Kakfa-Streaming-1.0-shaded.jar com.github.thomas.kafka.TwitterProducer
```

3. You should now be able to see the output in your Kafka console consumer terminal.

## License

This repository is under Apache License 2.0 - see [License](LICENSE.md) for more details

## Acknowledgement

This was inspired by Stephane Maarek. Check out his [Apache Kafka Series course](https://www.udemy.com/course/apache-kafka/) 