![GitHub](https://img.shields.io/github/license/Thomas-George-T/Kafka-Twitter-Streaming?style=plastic)
![GitHub top language](https://img.shields.io/github/languages/top/Thomas-George-T/Kafka-Twitter-Streaming?style=plastic)
![GitHub last commit](https://img.shields.io/github/last-commit/Thomas-George-T/Kafka-Twitter-Streaming?style=plastic)




# Kafka Twitter Streaming
<br>
<p align="center">
	<a href="#">
		<img src="https://cdn.svgporn.com/logos/kafka.svg" width="300" />
    <img src="https://cdn.svgporn.com/logos/twitter.svg" width="175" /> 
	</a>
</p>
<br>

This project aims at streaming Tweets using a high throughput Kafka Producer. To ensure a high throughput, idempotence, safe and compression configurations are enabled with respect to **Kafka 2.0.0 version**.
In the TwitterProducer class, the variable `terms` can be updated to stream tweets about Current affairs. In this example, `coronavirus, covid-19, pandemic` are being used. The prerequisite to running this project is to procure Twitter API credentials. To do this, sign up for twitter Developer account [here](https://developer.twitter.com/en/apply-for-access). After creating the app and getting the OAuth credentials,`consumerKey`,`consumerSecret`,`token`,`tokenSecret` are to be used to set the variables in `config.java`. Set these Strings to be static. Follow the below template for `config.java`

```java
static String consumerKey= "";
static String consumerSecret = "";
static String token = "";
static String tokenSecret = "";
```

To integrate Twitter streaming with Kafka, we use the Horsebird Client which is a Java HTTP client for consuming Twitter's standard streaming API [Learn more](https://github.com/twitter/hbc).

## Environment
- Java JDK 1.8
- Twitter Developer Account
- Kafka 2.12
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

## Installation

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

## Execution

### To execute the TwitterProducer class

1. Create a `topic` called TwitterTopic. Always have a replication factor equal or lesser than the number of available brokers.

```
kafka-topics --bootstrap-server localhost:9092 --topic TwitterTopic --create --partitions 3 --replication-factor 1
```

2. Run the kafka console consumer in another terminal window with the following `topic` and `group` parameters

```
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TwitterTopic --group Twitter-Consumer-Group
```

3. Execute the TwitterProducer class from the shaded jar

```
java -cp Kakfa-Streaming-1.0-shaded.jar com.github.thomas.kafka.TwitterProducer
```

4. You should now be able to see the output in your Kafka console consumer terminal.

## License

This repository is under Apache License 2.0 - see [License](LICENSE.md) for more details

## Acknowledgement

This was inspired by Stephane Maarek. Check out his [Apache Kafka Series course](https://www.udemy.com/course/apache-kafka/) 
