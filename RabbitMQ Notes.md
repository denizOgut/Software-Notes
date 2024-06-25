
# Queues
In computer science, queue is a ***collection of entities*** maintained in a ***sequence***. Sequence can be modified by
- **adding** entities to the **beginning** or to the **end**
- **removing** from the **beginning** or from the **end**
## Use Cases for Queues
Among others, queues are mostly used to:

1. **Decompose two systems**
	- Integrate systems written in different technologies
1. **Estimate desired system performance**,
	- Throttle or speed up data flows
2. **Increase fault tolerance level (not the same as high availability)**,
	- Persistent queues, “packet lost” issues, single data responsibility principle
3. **Increases loose coupling and scalability (horizontal scaling, auto-scaling)**
	- Many consumers for the same publisher, components don’t know each-other (scale-in and scale-out components)
4. **Increase system’s inbound traffic**
	- Asynchronous communication, “fire-and-forget” scenarios
5. **Buffer system’s outbound bytes**
	- Video streaming, ppv data streaming, notifications


# RabbitMQ

RabbitMQ is an open-source **message-broker** software (sometimes just called queuing software) that originally implemented the **Advanced Message Queuing Protocol (AMQP)**

A message broker is an intermediary that facilitates communication between applications by handling the sending and receiving of messages.

- **Receives Messages**: Accepts messages from producers.
- **Stores Messages**: Holds messages temporarily until they can be delivered.
- **Routes Messages**: Directs messages to the appropriate consumer based on routing rules.
- **Delivers Messages**: Ensures messages reach the intended recipients.

## Advanced Message Queuing Protocol (AMQP)

AMQP is is an open standard application layer protocol.

- Designed for asynchronous communication
- AMQP standardizes the behavior of the messaging publisher and consumer
-  Platform independent
-  Technology independent (many SDKs)

![[Pasted image 20240625094940.png]]

An AMQP message is a package of information that consists of three main parts:

- **Header**: Contains key-value pairs used for routing and other metadata.
- **Properties**: Includes additional metadata like message priority, timestamp, and content type.
- **Body**: The payload, which is the actual content of the message being transmitted.

![[Pasted image 20240625095311.png]]

## Core Concepts

![[Pasted image 20240625100001.png]]

- **Producer:** Application that sends the messages. **==Producer never send messages directly to the queue==**
- **Consumer:** Application that receives the messages.
- **Message:** Information that is sent from the producer to a consumer through RabbitMQ.
- ==**Queue:** Buffer that stores messages.==
- ==**Exchange:** Receives messages from producers and pushes them to queues depending on rules defined by the exchange type. To receive messages, a queue needs to be bound to at least one exchange.==
- ==**Binding:** A binding is a link between a queue and an exchange.==
- ==**Routing key:** A key that the exchange looks at to decide how to route the message to queues. Think of the routing key like an _address for the message._==
- **Connection:** A TCP connection between your application and the RabbitMQ broker.
- **Channel:** A virtual connection inside a connection. When publishing or consuming messages from a queue – it’s all done over a channel.
- **Users:** It is possible to connect to RabbitMQ with a given username and password. Every user can be assigned permissions such as rights to read, write and configure privileges within the instance. Users can also be assigned permissions for specific virtual hosts.

![[Pasted image 20240625101611.png]]

###  Type of exchanges

#### Direct Exchange

 The direct exchange routes messages to queues **==based on the message routing key==**. This is the simplest and most common type of exchange. It’s like sending a letter to a specific address, the letter will be delivered only to that specific address. A direct exchange can function similarly to a fanout exchange if multiple queues are bound to it with the same routing key. In this case, messages sent to the exchange with that routing key will be routed to all queues bound with the same routing key.
 
![[Pasted image 20240625102247.png]]

####  Fanout Exchange

The fanout exchange **==routes messages to all queues that are bound to it==**. It’s like sending a letter to a post office box, and all the people who have a key to that box will get it.

![[Pasted image 20240625102359.png]]

#### Topic Exchange

The topic exchange routes messages to queues **==based on a pattern that the queue and message routing key must match==**. This type of exchange is like sending a letter with a specific topic and only the people who are interested in that topic will get the letter.

![[Pasted image 20240625102518.png]]

#### Headers Exchange

The headers exchange routes messages **==based on the message header attributes rather than the routing key==**. This type of exchange allows for more complex routing logic because it evaluates the headers of the message against the arguments specified in the binding. It’s like sending a letter that will only be delivered if it has the correct combination of labels or stamps. For example, a message might be routed based on headers like `x-match`, `department`, and `priority`. Depending on how these headers match the criteria set by the queue, the message will be delivered to one or more queues.

##  Queue Properties

- **Name**: Custom or auto-generated identifier.
- **Durable or not**: Queue persistence across restarts.
- **Auto Delete feature**: Auto-deletes when consumers disconnect.
- **Classic or Quorum**: Choice of queue type for availability.
- **Exclusive**: Single-connection usage and auto-deletion.
- **Priority**: Message prioritization with performance trade-offs.
- **Expiration time (TTL)**: Sets lifespan for messages and queues.

##  Queue Types

###  Quorum Queues

Quorum queues adopt a different replication and consensus protocol and give up support for certain ***transient*** in nature features, which results in some limitations. 

#### What is a Quorum?[​](https://www.rabbitmq.com/docs/quorum-queues#what-is-quorum "Direct link to What is a Quorum?")

If intentionally simplified, quorum in a distributed system can be defined as an agreement between the majority of nodes (`(N/2)+1` where `N` is the total number of system participants).

When applied to queue mirroring in RabbitMQ clusters this means that the majority of replicas (including the currently elected queue leader) agree on the state of the queue and its contents.

#### Quorum Queues Use Cases

Quorum queues are designed for critical systems requiring high fault tolerance and data safety, where the longevity and reliability of queues are essential. They are not suited for every scenario, especially where low latency and advanced features are prioritized.

**Best Practices**:

- **Publishers**: Use publisher confirms for ensuring messages are safely replicated across nodes.
- **Consumers**: Use manual acknowledgements to requeue unprocessed messages for retry.

#### When Not to Use Quorum Queues

Quorum queues should be avoided in the following scenarios:

- **Temporary Queues**: Transient or exclusive queues with high rates of creation and deletion.
- **Low Latency Requirements**: Scenarios needing the lowest possible latency, as quorum queues have higher latency due to data safety features.
- **Data Safety Not a Priority**: Applications not using manual acknowledgements or publisher confirms.
- **Very Long Queue Backlogs**: Streams are a better fit for handling extensive backlogs.

###  Classic Queues

A RabbitMQ classic queue (the original queue type) is a versatile queue type suitable for use cases where data safety is not a priority because the data stored in classic queues is not replicated. Classic queues uses the **non-replicated** FIFO queue implementation.

If data safety is a priority, the recommendation is to use quorum queues and streams instead of classic queues.
Classic queues are the default queue type as long as the default queue type is not overridden for the virtual host.

####  Classic Queue Features

Classic queues fully support [queue exclusivity](https://www.rabbitmq.com/docs/queues), [queue and message TTL (Time-To-Live)](https://www.rabbitmq.com/docs/ttl), [queue length limits](https://www.rabbitmq.com/docs/maxlength), [message priority](https://www.rabbitmq.com/docs/priority), [consumer priority](https://www.rabbitmq.com/docs/consumer-priority) and adhere to settings [controlled using policies](https://www.rabbitmq.com/docs/parameters#policies).

Classic queues support [dead letter exchanges](https://www.rabbitmq.com/docs/dlx) with the exception of [at-least-once dead-lettering](https://www.rabbitmq.com/docs/quorum-queues#dead-lettering).

Classic queues do not support [poison message handling](https://en.wikipedia.org/wiki/Poison_message), unlike [quorum queues](https://www.rabbitmq.com/docs/quorum-queues). Classic queues also do not support at-least-once dead-lettering, supported by quorum queues.

###  Time-to-Live and Expiration

With RabbitMQ, you can set a TTL (time-to-live) argument or policy for messages and queues. As the name suggests, TTL specifies the time period that the messages and queues "live for".

Message TTL determines how long messages can be retained in a queue. If the retention period of a message in a queue exceeds the message TTL of the queue, the message expires and is discarded.

"Discarded" means that the message will not be delivered to any of subscribed consumers and won't be accessible through `basic.get` method applied directly on queue. Message TTL can be applied to a single queue, a group of queues, or applied on the message-by-message basis.

###  Lazy Queue

A "*lazy queue*" is a classic queue which is running in `lazy` mode. When the "*lazy*" queue mode is set, messages in classic queues are moved to disk as early as practically possible. These messages are loaded into RAM only when they are requested by consumers.

The other queue mode is the `default` mode. If no mode is specified during declaration, then the `default` mode is used.

One of the main reasons for using lazy queues is to support very long queues (many millions of messages). Queues can become very long for various reasons:

- consumers are offline / have crashed / are down for maintenance
- there is a sudden message ingress spike, producers are outpacing consumers
- consumers are slower than normal

By default, queues keep an in-memory cache of messages that is filled up as messages are published into RabbitMQ. The idea of this cache is to be able to deliver messages to consumers as fast as possible. Note that persistent messages can be written to disk as they enter the broker **and** kept in RAM at the same time.

Running classic queues in `lazy` queue mode attempts to move the messages above to disk as early as practically possible. This means significantly fewer messages are kept in RAM in the majority of cases under normal operation. This comes at a cost of increased disk I/O.

###  Dead Letter Exchanges

Messages from a queue can be "dead-lettered", which means these messages are republished to an exchange when any of the following four events occur.

1. The message is [negatively acknowledged](https://www.rabbitmq.com/docs/confirms) by a consumer using `basic.reject` or `basic.nack` with `requeue` parameter set to `false`, or
2. The message expires due to [per-message TTL](https://www.rabbitmq.com/docs/ttl), or
3. The message is dropped because its queue exceeded a [length limit](https://www.rabbitmq.com/docs/maxlength), or
4. The message is returned more times to a quorum queue than the [delivery-limit](https://www.rabbitmq.com/docs/quorum-queues#poison-message-handling).

If an entire [queue expires](https://www.rabbitmq.com/docs/ttl#queue-ttl), the messages in the queue are **not** dead-lettered.

Dead letter exchanges (DLXs) are normal exchanges. They can be any of the usual types and are declared as normal.

Dead-lettered messages are routed to their dead letter exchange either:

- with the routing key specified for the queue they were on; or, _if this was not set_,
- with the same routing keys they were originally published with

By default, dead-lettered messages are re-published _without_ publisher [confirms](https://www.rabbitmq.com/docs/confirms) turned on internally. Therefore using DLX in a clustered RabbitMQ environment is not guaranteed to be safe. Messages are removed from the original queue immediately after publishing to the DLX target queue. This ensures that there is no chance of excessive message build up that could exhaust broker resources. However, messages can be lost if the target queue is not available to accept messages.

Dead-lettering a message modifies its headers:

- the exchange name is replaced with that of the latest dead-letter exchange
- the routing key may be replaced with that specified in a queue performing dead lettering,
- if the above happens, the `CC` header will also be removed, and
- the `BCC` header will be removed as per [Sender-selected distribution](https://www.rabbitmq.com/docs/sender-selected)

###  Priority Queue

RabbitMQ supports adding "priorities" to classic queues. Classic queues with the "priority" feature turned on are commonly referred to as "priority queues". Priorities between 1 and 255 are supported, however, **values between 1 and 5 are highly recommended**. It is important to know that higher priority values require more CPU and memory resources, since RabbitMQ needs to internally maintain a sub-queue for each priority from 1, up to the maximum value configured for a given queue.

By default, RabbitMQ classic queues do not support priorities. When creating priority queues, a maximum priority can be chosen as you see fit. When choosing a priority value, the following factors need to be considered:

- There is some in-memory and on-disk cost per priority level per queue. There is also an additional CPU cost, especially when consuming, so you may not wish to create huge numbers of levels.
    
- The message `priority` field is defined as an unsigned byte, so in practice priorities should be between 0 and 255.
    
- Messages without a `priority` property are treated as if their priority were 0. Messages with a priority which is higher than the queue's maximum are treated as if they were published with the maximum priority

## Spring RabbitMQ Example

**``RabbitMQConfig``**

```java
@Configuration  
public class RabbitMQConfig {  
  
    @Value("${rabbitmq.queue.name}")  
    private String queue;  
  
    @Value("${rabbitmq.queue.json.name}")  
    private String jsonQueue;  
  
    @Value("${rabbitmq.exchange.name}")  
    private String exchange;  
  
    @Value("${rabbitmq.routing.key}")  
    private String routingKey;  
  
    @Value("${rabbitmq.routing.json.key}")  
    private String routingJsonKey;  
  
    // spring bean for rabbitmq queue  
    @Bean  
    public Queue queue(){  
        return new Queue(queue);  
    }  
  
    // spring bean for queue (store json messages)  
    @Bean  
    public Queue jsonQueue(){  
        return new Queue(jsonQueue);  
    }  
  
    // spring bean for rabbitmq exchange  
    @Bean  
    public TopicExchange exchange(){  
        return new TopicExchange(exchange);  
    }  
  
    // binding between queue and exchange using routing key  
    @Bean  
    public Binding binding(){  
        return BindingBuilder  
                .bind(queue())  
                .to(exchange())  
                .with(routingKey);  
    }  
  
    // binding between json queue and exchange using routing key  
    @Bean  
    public Binding jsonBinding(){  
        return BindingBuilder  
                .bind(jsonQueue())  
                .to(exchange())  
                .with(routingJsonKey);  
    }  
  
    @Bean  
    public MessageConverter converter(){  
        return new Jackson2JsonMessageConverter();  
    }  
  
    @Bean  
    public AmqpTemplate amqpTemplate(ConnectionFactory connectionFactory){  
        RabbitTemplate rabbitTemplate = new RabbitTemplate(connectionFactory);  
        rabbitTemplate.setMessageConverter(converter());  
        return rabbitTemplate;  
    }  
}
```

**``RabbitMQProducer``**
```java
@Service  
public class RabbitMQProducer {  
  
    @Value("${rabbitmq.exchange.name}")  
    private String exchange;  
  
    @Value("${rabbitmq.routing.key}")  
    private String routingKey;  
  
    private static final Logger LOGGER = LoggerFactory.getLogger(RabbitMQProducer.class);  
  
    private RabbitTemplate rabbitTemplate;  
  
    public RabbitMQProducer(RabbitTemplate rabbitTemplate) {  
        this.rabbitTemplate = rabbitTemplate;  
    }  
  
    public void sendMessage(String message){  
        LOGGER.info(String.format("Message sent -> %s", message));  
        rabbitTemplate.convertAndSend(exchange, routingKey, message);  
    }  
}
```

**``RabbitMQConsumer``**

```java
@Service  
public class RabbitMQConsumer {  
  
    private static final Logger LOGGER = LoggerFactory.getLogger(RabbitMQConsumer.class);  
  
    @RabbitListener(queues = {"${rabbitmq.queue.name}"})  
    public void consume(String message){  
        LOGGER.info(String.format("Received message -> %s", message));  
    }  
}
```

**``RabbitMQJsonProducer``**

```java
@Service  
public class RabbitMQJsonProducer {  
  
    @Value("${rabbitmq.exchange.name}")  
    private String exchange;  
  
    @Value("${rabbitmq.routing.json.key}")  
    private String routingJsonKey;  
  
    private static final Logger LOGGER = LoggerFactory.getLogger(RabbitMQJsonProducer.class);  
  
    private RabbitTemplate rabbitTemplate;  
  
    public RabbitMQJsonProducer(RabbitTemplate rabbitTemplate) {  
        this.rabbitTemplate = rabbitTemplate;  
    }  
  
    public void sendJsonMessage(User user){  
        LOGGER.info(String.format("Json message sent -> %s", user.toString()));  
        rabbitTemplate.convertAndSend(exchange, routingJsonKey, user);  
    }  
  
}
```

**``RabbitMQJsonConsumer``**

```java
@Service  
public class RabbitMQJsonConsumer {  
  
    private static final Logger LOGGER = LoggerFactory.getLogger(RabbitMQJsonConsumer.class);  
  
    @RabbitListener(queues = {"${rabbitmq.queue.json.name}"})  
    public void consumeJsonMessage(User user){  
        LOGGER.info(String.format("Received JSON message -> %s", user.toString()));  
    }  
}
```

