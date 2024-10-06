
Apache Kafka is an open-source event streaming platform that can transport huge volumes of data at very low latency. It is an open-source distributed system consisting of servers and clients. Apache Kafka is used primarily to build real-time data streaming pipelines.

# Data Integration Challenges

A typical business collects data through a variety of applications, e.g., accounting, billing, CRM, websites, etc. Each of these applications have their own processes for data input and update. In order to get a unified view of their business, engineers have to develop bespoke integrations between these different applications.

Each integration comes with difficulties around

- ==**Protocol** – how the data is transported (TCP, HTTP, REST, FTP, JDBC…)==
    
- ==**Data format** – how the data is parsed (Binary, CSV, JSON, Avro…)==
    
- ==**Data schema & evolution** – how the data is shaped and may change==

Kafka lets you:

- ==**Publish and subscribe to streams of events**==
- ==**Store streams of events in the same order they happened**==
- ==**Process streams of events in real time==**

The main thing Kafka does is help you efficiently connect diverse data sources with the many different systems that might need to use that data.

>==**Decoupling Different Data Systems**==
  ==**Apache Kafka allows us to decouple data streams and systems.**==


![[Pasted image 20241006124351.png]]


## What is a data stream in Apache Kafka?

A data stream is typically thought of as a potentially unbounded sequence of data. The name streaming is used because we are interested in the data being accessible as soon as it is produced. 

Data created as part of data streams are typically small. The data throughput to data streams is highly variable: some streams will receive tens of thousands of records per second, and some will receive one or two records per hour.

Apache Kafka is used to store these data streams (also called topics), which then allows systems to perform stream processing - an act of performing continual calculations on a potentially endless and constantly evolving source of data. Once the stream is processed and stored in Apache Kafka, it may be transferred to another system, e.g., a database.

![[Pasted image 20241006125006.png]]

## Examples of Data streams

- **Log Analysis**. Modern applications include tens to thousands of microservices - all of which constantly produce logs. These logs are full of information that can be mined for business intelligence, failure prediction, and debugging. The challenge then is how to process these large volumes of log data being produced in one place. Companies push log data into a data stream to perform stream processing.
    
- **Web Analytics**. Another common use for streaming data is web analytics. Modern web applications measure almost every user activity on their site, e.g., button clicks, page views. These actions add up fast. Stream processing allows companies to process data as it is generated and not hours later.

## Where is Apache Kafka not a great fit?

- **Proxying millions of clients** for mobile apps or IoT: the Kafka protocol is not made for that, but some proxies exist to bridge the gap.
    
- **A database with indexes:** Kafka is an event streaming log with no analytical capability built in and no complex query model.
    
- **An embedded real-time technology for IoT:** there are lower level and lighter alternatives to perform these use cases on embedded systems.
    
- **Work queues:** Kafka is made of topics, not queues (unlike RabbitMQ, ActiveMQ, SQS). Queues are meant to scale to millions of consumers and to delete messages once processed. In Kafka data is not deleted once processed and consumers cannot scale beyond the number of partitions in a topic.
    
- **Kafka as a blockchain**: Kafka topics present some characteristics of a blockchain, where data is appended in a log, and Kafka topics can be immutable, but lack some key properties of blockchains such as the cryptographic verification of the data, as well as full history preservation.

# Core Kafka Concepts

## Event Messages in Kafka

When you write data to Kafka, or read data from it, you do this in the form of messages.

A message consists of:

- a key
- a value
- a timestamp
- a compression type
- headers for metadata (optional)
- partition and offset id (once the message is written to a topic)

![[Pasted image 20241006130701.png]]

Every event in Kafka is, at its simplest, a key-value pair. These are serialized into binary, **==since Kafka itself handles arrays of bytes rather than complex language-specific objects.==**

**Keys** are usually strings or integers and aren't unique for every message. Instead, they point to a particular entity in the system, such as a specific user, order, or device. **==Keys can be null, but when they are included they are used for dividing topics into partitions==** 

The message **value** contains details about the event that happened. This could be as simple as a string or as complex as an object with many nested properties.

Messages are usually small (less than 1 MB) and sent in a standard data format, such as JSON, Avro, or Protobuf. Even so, they can be compressed to save on data. The **compression type** can be set to `gzip`, `lz4`, `snappy`, `zstd`, or `none`.

## Topics in Kafka

Kafka stores messages in a **topic**, an ordered sequence of events, also called an event log. Kafka uses the concept of topics to organize related messages.

![[Pasted image 20241006131441.png]]

Different topics are identified by their names and will store different kinds of events. For example a social media application might have `posts`, `likes`, and `comments` topics to record every time a user creates a post, likes a post, or leaves a comment.

**==One important feature of topics is that they are append-only. When you write a message to a topic, it's added to the end of the log. Events in a topic are immutable. Once they're written to a topic, you can't change them.==**

![[Pasted image 20241006131542.png]]

## Partitions in Kafka

In order to help Kafka to scale, topics can be divided into **partitions**. This breaks up the event log into multiple logs, each of which lives on a separate node in the Kafka cluster. **==This means that the work of writing and storing messages can be spread across multiple machines.==**

![[Pasted image 20241006132302.png]]

 The partitions are themselves numbered, starting at 0. When a new event is written to a topic, it's appended to one of the topic's partitions.

If messages have no key, they will be evenly distributed among partitions in a round robin manner: partition 0, then partition 1, then partition 2, and so on. This way, all partitions get an even share of the data but there's no guarantee about the ordering of messages.

Messages that have the same key will always be sent to the same partition, and in the same order. The key is run through a hashing function which turns it into an integer. This output is then used to select a partition.

![[Pasted image 20241006132430.png]]

**==Messages within each partition are guaranteed to be ordered.==** For example, all messages with the same `customer_id` as their key will be sent to the same partition in the order in which Kafka received them.

## Offsets in Kafka

Each message in a partition gets an id that is an incrementing integer, called an **offset**. Offsets start at 0 and are incremented every time Kafka writes a message to a partition. This means that each message in a given partition has a unique offset.

![[Pasted image 20241006134554.png]]

**==Offsets are not reused, even when older messages get deleted.==** They continue to increment, giving each new message in the partition a unique id.

## Brokers in Kafka

A single "server" running Kafka is called a **broker**. In reality, this might be a Docker container running in a virtual machine.

![[Pasted image 20241006134743.png]]

Multiple brokers working together make up a Kafka cluster. There might be a handful of brokers in a cluster, or more than 100. When a client application connects to one broker, Kafka automatically connects it to every broker in the cluster.

By running as a cluster, Kafka becomes more scalable and fault-tolerant. If one broker fails, the others will take over its work to ensure there is no downtime or data loss.

Each broker manages a set of partitions and handles requests to write data to or read data from these partitions. Partitions for a given topic will be spread evenly across the brokers in a cluster to help with load balancing. Brokers also manage replicating partitions to keep their data backed up.

![[Pasted image 20241006134845.png]]

## Replication in Kafka

To protect against data loss if a broker fails, Kafka writes the same data to copies of a partition on multiple brokers. This is called **replication**.

![[Pasted image 20241006134919.png]]

When a topic is created, you set a replication factor for it. This controls how many replicas get written to. A replication factor of three is common, meaning data gets written to one leader and replicated to two followers. So even if two brokers failed, your data would still be safe.

Whenever you write messages to a partition, you're writing to the leader partition. Kafka then automatically copies these messages to the followers. As such, the logs on the followers will have the same messages and offsets as on the leader.

Followers that are up to date with the leader are called **In-Sync Replicas** (ISRs). Kafka considers a message to be committed once a minimum number of replicas have saved it to their logs.

## Producers in Kafka

Producers are client applications that write events to Kafka topics. These apps aren't themselves part of Kafka – you write them.

![[Pasted image 20241006140613.png]]

Producers are totally decoupled from consumers, which read from Kafka. They don't know about each other and their speed doesn't affect each other. Producers aren't affected if consumers fail, and the same is true for consumers.

**==Producers take a key-value pair, generate a Kafka message, and then serialize it into binary for transmission across the network.==**

It's the producer that decides which partition of a topic to send each message to.

## Consumers in Kafka

Consumers are client applications that read messages from topics in a Kafka cluster.

![[Pasted image 20241006140936.png]]

Consumers can read from one or more partitions within a topic, and from one or more topics. Messages are read in order within a partition, from the lowest available offset to the highest. But if a consumer reads data from several partitions in the same topic, the message order **between** these partitions is not guaranteed.

It's important to remember that reading a message does not delete it. The message is still available to be read by any other consumer that needs to access it. It's normal for multiple consumers to read from the same topic if they each have uses for the data in it.

Consumers deserialize messages, converting them from binary into a collection of key-value pairs that your application can then work with. The format of a message should not change during a topic's lifetime or your producers and consumers won't be able to serialize and deserialize it correctly.

**==One thing to be aware of is that consumers request messages from Kafka, it doesn't push messages to them. This protects consumers from becoming overwhelmed if Kafka is handling a high volume of messages.==**

## Consumer Groups in Kafka

An application that reads from Kafka can create multiple instances of the same consumer to split up the work of reading from different partitions in a topic. These consumers work together as a **consumer group**.

When you create a consumer, you can assign it a group id. All consumers in a group will have the same group id.

![[Pasted image 20241006142254.png]]

If you add another consumer instance to a consumer group, Kafka will automatically redistribute the partitions among the consumers in a process called **rebalancing**.

Kafka brokers use an internal topic called `__consumer_offsets` to keep track of which messages a specific consumer group has successfully processed.

As a consumer reads from a partition, it regularly saves the offset it has read up to and sends this data to the broker it is reading from. This is called the **consumer offset** and is handled automatically by most client libraries.

![[Pasted image 20241006142344.png]]

## Kafka Zookeeper

a service for managing and synchronizing distributed systems. Like Kafka, it's maintained by the Apache Foundation.

Kafka uses Zookeeper to manage the brokers in a cluster, and requires Zookeeper even if you're running a Kafka cluster with only one broker.

Zookeeper keeps track of things like:

- Which brokers are part of a Kafka cluster
- Which broker is the leader for a given partition
- How topics are configured, such as the number of partitions and the location of replicas
- Consumer groups and their members
- Access Control Lists – who is allowed to write to and read from each topic

![[Pasted image 20241006143107.png]]

# Spring Example

```xml
  <dependencies>

    <dependency>

      <groupId>org.springframework.boot</groupId>

      <artifactId>spring-boot-starter</artifactId>

    </dependency>

    <dependency>

      <groupId>org.springframework.kafka</groupId>

      <artifactId>spring-kafka</artifactId>

    </dependency>

    <dependency>

      <groupId>org.springframework.boot</groupId>

      <artifactId>spring-boot-starter-test</artifactId>

      <scope>test</scope>

    </dependency>

    <dependency>

      <groupId>org.springframework.kafka</groupId>

      <artifactId>spring-kafka-test</artifactId>

      <scope>test</scope>

    </dependency>

  </dependencies>
```

```JAVA
public class User {

    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

```yml
server: port: 9000
spring:
   kafka:
     consumer:
        bootstrap-servers: localhost:9092
        group-id: group_id
        auto-offset-reset: earliest
        key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
        value-deserializer: org.apache.kafka.common.serialization.StringDeserializer
     producer:
        bootstrap-servers: localhost:9092
        key-serializer: org.apache.kafka.common.serialization.StringSerializer
        value-serializer: org.apache.kafka.common.serialization.StringSerializer
```

```java
@Service  
public class Producer {  
  
    private static final Logger logger = LoggerFactory.getLogger(Producer.class);  
    private static final String TOPIC = "users";  
  
    @Autowired  
    private KafkaTemplate<String, String> kafkaTemplate;  
  
    public void sendMessage(String message) {  
        logger.info(String.format("#### -> Producing message -> %s", message));  
        this.kafkaTemplate.send(TOPIC, message);  
    }  
  
}
```

```java
@Service  
public class Producer {  
  
    private static final Logger logger = LoggerFactory.getLogger(Producer.class);  
    private static final String TOPIC = "users";  
  
    @Autowired  
    private KafkaTemplate<String, String> kafkaTemplate;  
  
    public void sendMessage(String message) {  
        logger.info(String.format("#### -> Producing message -> %s", message));  
        this.kafkaTemplate.send(TOPIC, message);  
    }  
  
}
```

