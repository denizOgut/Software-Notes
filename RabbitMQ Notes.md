
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

## Exchange

An Exchange is a structure that routes a message produced by the producer to either a recipient or a queue. The producer sends the produced message to the Exchange, which then adds the incoming message to the relevant queue along with its contained information. If there is a listening consumer, it takes the next message from the queue to process. In short, its task is to deliver the message it receives to the relevant Queue according to the specified Routing Key.
### Direct Exchange

 The direct exchange routes messages to queues **==based on the message routing key==**. This is the simplest and most common type of exchange. It’s like sending a letter to a specific address, the letter will be delivered only to that specific address. A direct exchange can function similarly to a fanout exchange if multiple queues are bound to it with the same routing key. In this case, messages sent to the exchange with that routing key will be routed to all queues bound with the same routing key.
 
![[Pasted image 20240729221910.png]]

###  Fanout Exchange

The fanout exchange **==routes messages to all queues that are bound to it==**. It’s like sending a letter to a post office box, and all the people who have a key to that box will get it.

![[Pasted image 20240729221931.png]]

### Topic Exchange

The topic exchange routes messages to queues **==based on a pattern that the queue and message routing key must match==**. This type of exchange is like sending a letter with a specific topic and only the people who are interested in that topic will get the letter.


![[Pasted image 20240729222002.png]]

### Headers Exchange

The headers exchange routes messages **==based on the message header attributes rather than the routing key==**. This type of exchange allows for more complex routing logic because it evaluates the headers of the message against the arguments specified in the binding. It’s like sending a letter that will only be delivered if it has the correct combination of labels or stamps. For example, a message might be routed based on headers like `x-match`, `department`, and `priority`. Depending on how these headers match the criteria set by the queue, the message will be delivered to one or more queues.

![[Pasted image 20240729222135.png]]

##  Queue Properties

- **Name**: Custom or auto-generated identifier.
- **Durable or not**: Queue persistence across restarts.
- **Auto Delete feature**: Auto-deletes when consumers disconnect.
- **Classic or Quorum**: Choice of queue type for availability.
- **Exclusive**: Single-connection usage and auto-deletion.
- **Priority**: Message prioritization with performance trade-offs.
- **Expiration time (TTL)**: Sets lifespan for messages and queues.

## Dead Letter Exchange & Queue

A Dead Letter Exchange (DLX) is a special type of Exchange to which a message is routed when it cannot be consumed for specific reasons. The Dead Letter Queue (DLQ) is a special queue that receives messages through this Exchange.

Situations where this mechanism is needed: 
- If a message's TTL (Time-To-Live) has expired. 
- If the queue is full and there is no space for new messages. 
- If the message is rejected by the Consumer in any way (Nack or Reject).

In such cases, instead of being deleted outright, messages are processed through the DLX and DLQ, allowing for different actions to be taken on these messages later. RabbitMQ offers this mechanism built-in. The only requirement is to provide the ***x-dead-letter-exchange*** tag as an argument when defining the Queue. In Queues where this tag is provided, if any of the above conditions occur, the message will be routed to the DLQ through the DLX. Messages that cannot be delivered through the DLQ can be used later for their intended purpose.

![[Pasted image 20240729232031.png]]

## Advantages & Disadvantages
### Advantages

- **Reliability**: RabbitMQ ensures message delivery even in the event of system failures or network issues. Features like message acknowledgment and persistence prevent messages from being lost. In the event of damage to the queue or RabbitMQ Broker for any reason, the system allows for messages to be recorded or backed up on disk, preventing message loss.

- **Flexibility**: RabbitMQ supports multiple messaging protocols such as AMQP, MQTT, and STOMP, providing versatility for different types of applications and integration scenarios. For example, consider a service communicating with various applications through message queues. Given that other applications might use different messaging protocols, RabbitMQ allows messages to be sent by queues specific to the application's protocol, facilitating easy adaptation of services.

- **Scalability**: RabbitMQ can handle large message volumes and can be scaled horizontally by adding more nodes to clusters. This scalability ensures load distribution within the system, enabling queues to operate more efficiently.
  
- **Routing and Filtering**: RabbitMQ offers advanced message routing and filtering capabilities. As previously mentioned in routing methods, it allows messages to be routed to specific queues based on criteria such as message headers, routing keys, or message content. This makes it easier to separate messages by services and functions, ensuring clarity and purpose-specific usage.

- **Management and Monitoring**: RabbitMQ provides a web-based management interface and comprehensive monitoring capabilities. This makes it easy to manage and monitor the messaging infrastructure.

### Disadvantages

- **Complexity**: Setting up and configuring RabbitMQ can be complex, especially for users unfamiliar with message queue systems. Configuring Exchanges, queues, bindings, and understanding routing keys can be challenging for beginners. This requires significant developer effort for effective use.
    
- **Scalability**: Although RabbitMQ can be scaled horizontally by adding more nodes to a cluster, managing this scalability can be difficult and requires careful planning to ensure high availability and performance. Additionally, this can increase the complexity of the infrastructure, requiring extra resources or effort for troubleshooting.
    
- **Resource Intensity-Performance**: Running RabbitMQ, especially as message load increases, requires significant resources such as CPU and memory. Configuration, fine-tuning, and monitoring are essential for optimal performance. Increased message size and volume can become a major issue if not supported by a well-planned and robust infrastructure. 

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

------------------------------

**``application.yml``**

```java
spring:  
  application:  
    name:rabbitmq.producer  
  
  rabbitmq:  
    host:localhost  
    port:5672  
    username:guest  
    password:guest
```

**``RabbitmqConfig``**

```java
@Configuration  
public class RabbitmqConfig {  
    @Bean("objectMapper-1")  
    ObjectMapper objectMapper() {  
        return JsonMapper.builder().findAndAddModules().build();  
    }  
}
```

**``EmployeeJsonProducer``**

```java
@Component  
@Data  
@Slf4j  
public class EmployeeJsonProducer {  
  
    private final RabbitTemplate rabbitTemplate;  
    private final ObjectMapper objectMapper;  
  
    public void sendEmployee(Employee employee)  {  
        try {  
            var json = objectMapper.writeValueAsString(employee);  
            log.info("Sending message: {}", json);  
            rabbitTemplate.convertAndSend("course.employee", json);  
        } catch (JsonProcessingException e) {  
            throw new RuntimeException(e);  
        }  
    }  
  
}
```

**``EmployeeJsonConsumer``**

```java
@Component  
@Slf4j  
@Data  
public class EmployeeJsonConsumer {  
  
    private final ObjectMapper objectMapper;  
  
    @RabbitListener(queues = "course.employee")  
    public void receiveMessage(String message) throws JsonProcessingException {  
        var employee = objectMapper.readValue(message, Employee.class);  
        log.info("Consumer received: {}", employee);  
    }  
}
```

