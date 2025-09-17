# CHAPTER 1: SCALE FROM ZERO TO MILLIONS OF USERS

## Single server setup

To start with something simple, everything is running on a single server

![[Pasted image 20250909133202.png]]

1. Users access websites through domain names, such as api.mysite.com. Usually, the Domain Name System (DNS) is a paid service provided by 3rd parties and not hosted by our servers.
2. Internet Protocol (IP) address is returned to the browser or mobile app
3. Once the IP address is obtained, Hypertext Transfer Protocol (HTTP) [1] requests are sent directly to your web server.
4. The web server returns HTML pages or JSON response for rendering

## Database

With the growth of the user base, one server is not enough, and we need multiple servers: one for web/mobile traffic, the other for the database (Figure 1-3). Separating web/mobile traffic (web tier) and database (data tier) servers allows them to be scaled independently.

![[Pasted image 20250909133412.png]]

### Which databases to use?

Relational databases represent and store data in tables and rows. You can perform join operations using SQL across different database tables. 

Non-Relational databases are also called NoSQL databases These databases are grouped into four categories: key-value stores, graph stores, column stores, and document stores. Join operations are generally not supported in non-relational databases.

if relational databases are not suitable for your specific use cases, it is critical to explore beyond relational databases. Non-relational databases might be the right choice if:
**==• Your application requires super-low latency.**==
==**• Your data are unstructured, or you do not have any relational data.**==
==**• You only need to serialize and deserialize data (JSON, XML, YAML, etc.).**==
==**• You need to store a massive amount of data.==**

### Vertical scaling vs horizontal scaling

- Vertical scaling, referred to as “scale up”, means the process of adding more power to your servers
- Horizontal scaling, referred to as “scale-out”, allows you to scale by adding more servers into your pool of resources.

**==When traffic is low, vertical scaling is a great option, and the simplicity of vertical scaling is its main advantage. Unfortunately, it comes with serious limitations:**==  

- ==**Vertical scaling has a hard limit: It is impossible to add unlimited CPU and memory to a single server.**==  
- ==**Vertical scaling lacks failover and redundancy: If one server goes down, the website or application goes down completely.**==  

==**Horizontal scaling is more desirable for large-scale applications due to the limitations of vertical scaling.==**


## Load balancer

A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set

![[Pasted image 20250909133833.png]]

users connect to the public IP of the load balancer directly. With this setup, web servers are unreachable directly by clients anymore. For better security, private IPs are used for communication between servers. **==A private IP is an IP address reachable only between servers in the same network; however, it is unreachable over the internet. The load balancer communicates with web servers through private IPs.==**

- If server 1 goes offline, all the traffic will be routed to server 2.
- If the website traffic grows rapidly, and two servers are not enough to handle the traffic, the load balancer can handle this problem gracefully. You only need to add more servers to the web server pool, and the load balancer automatically starts to send requests to them.


## Database replication

Database replication can be used in many database management systems, usually with a master/slave relationship between the original (master) and the copies (slaves)

A master database generally only supports write operations. A slave database gets copies of the data from the master database and only supports read operations. **==All the data-modifying commands like insert, delete, or update must be sent to the master database.==**

![[Pasted image 20250909134015.png]]

Advantages of database replication:

- Better performance
- Reliability:
- High availability


• If only one slave database is available and it goes offline, read operations will be directed to the master database temporarily. As soon as the issue is found, a new slave database will replace the old one.

• If the master database goes offline, a slave database will be promoted to be the new master. All the database operations will be temporarily executed on the new master database. A new slave database will replace the old one for data replication immediately.

![[Pasted image 20250909134200.png]]

• A user gets the IP address of the load balancer from DNS.
• A user connects the load balancer with this IP address.
• The HTTP request is routed to either Server 1 or Server 2.
• A web server reads user data from a slave database.
• A web server routes any data-modifying operations to the master database. This includes write, update, and delete operations.

## Cache

A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent requests are served more quickly.

### Cache tier

The cache tier is a temporary data store layer, much faster than the database. The benefits of having a separate cache tier include better system performance, ability to reduce database workloads, and the ability to scale the cache tier independently

![[Pasted image 20250909134327.png]]

After receiving a request, a web server first checks if the cache has the available response. If it has, it sends data back to the client. If not, it queries the database, stores the response in cache, and sends it back to the client. This caching strategy is called a read-through cache. Other caching strategies are available depending on the data type, size, and access patterns.

### Considerations for using cache

- **==Decide when to use cache. Consider using cache when data is read frequently but modified infrequently. Since cached data is stored in volatile memory, a cache server is not ideal for persisting data.==**
- Expiration policy. It is a good practice to implement an expiration policy. Once cached data is expired, it is removed from the cache. **==When there is no expiration policy, cached data will be stored in the memory permanently. It is advisable not to make the expiration date too short as this will cause the system to reload data from the database too frequently. Meanwhile, it is advisable not to make the expiration date too long as the data can become stale.==**
- Consistency: This involves keeping the data store and the cache in sync. Inconsistency can happen because data-modifying operations on the data store and cache are not in a single transaction.
- Mitigating failures: A single cache server represents a potential single point of failure (SPOF), defined in Wikipedia as follows: “A single point of failure (SPOF) is a part of a system that, if it fails, will stop the entire system from working” [8]. As a result, multiple cache servers across different data centers are recommended to avoid SPOF.
- Eviction Policy: Once the cache is full, any requests to add items to the cache might cause existing items to be removed. This is called cache eviction. Least-recently-used (LRU) is the most popular cache eviction policy. Other eviction policies, such as the Least Frequently Used (LFU) or First in First Out (FIFO), can be adopted to satisfy different use cases.

## Content delivery network (CDN)

A CDN is a network of geographically dispersed servers used to deliver static content. **==CDN servers cache static content like images, videos, CSS, JavaScript files, etc.==**

how CDN works at the high-level: when a user visits a website, a CDN server closest to the user will deliver static content. Intuitively, the further users are from CDN servers, the slower the website loads.

![[Pasted image 20250909134729.png]]

![[Pasted image 20250909134734.png]]

### Considerations of using a CDN

• Cost: CDNs are run by third-party providers, and you are charged for data transfers in and out of the CDN. Caching infrequently used assets provides no significant benefits so you should consider moving them out of the CDN.
• Setting an appropriate cache expiry: For time-sensitive content, setting a cache expiry time is important.
CDN fallback: You should consider how your website/application copes with CDN failure. If there is a temporary CDN outage, clients should be able to detect the problem and request resources from the origin
• Invalidating files: You can remove a file from the CDN before it expires by performing one of the following operations:
	• Invalidate the CDN object using APIs provided by CDN vendors.
	• Use object versioning to serve a different version of the object.

![[Pasted image 20250909134850.png]]

## Stateless web tier

A good practice is to store session data in the persistent storage such as relational database or NoSQL. Each web server in the cluster can access state data from databases. This is called stateless web tier.

### Stateful architecture

A stateful server and stateless server has some key differences. A stateful server remembers client data (state) from one request to the next. A stateless server keeps no state information.

![[Pasted image 20250909135434.png]]

The issue is that every request from the same client must be routed to the same server. This can be done with sticky sessions in most load balancers [10]; however, this adds the overhead. Adding or removing servers is much more difficult with this approach. It is also challenging to handle server failures.

### Stateless architecture

![[Pasted image 20250909135516.png]]

In this stateless architecture, HTTP requests from users can be sent to any web servers, which fetch state data from a shared data store. State data is stored in a shared data store and kept out of web servers. **==A stateless system is simpler, more robust, and scalable.==**

![[Pasted image 20250909135608.png]]

move the session data out of the web tier and store them in the persistent data store. The shared data store could be a relational database, ``Memcached/Redis``, NoSQL, etc. **==The NoSQL data store is chosen as it is easy to scale.==**

After the state data is removed out of web servers, auto-scaling of the web tier is easily achieved by adding or removing servers based on traffic load.

To improve availability and provide a better user experience across wider geographical areas, supporting multiple data centers is crucial.

## Data centers

In normal operation, users are geoDNS-routed, also known as geo-routed, to the closest data center, with a split traffic of x% in US-East and (100 – x)% in US-West. geoDNS is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user

![[Pasted image 20250909135733.png]]

In the event of any significant data center outage, we direct all traffic to a healthy data center.

![[Pasted image 20250909135745.png]]

Several technical challenges must be resolved to achieve multi-data center setup:
• Traffic redirection: Effective tools are needed to direct traffic to the correct data center 
• Data synchronization: Users from different regions could use different local databases or caches. In failover cases, traffic might be routed to a data center where data is unavailable. A common strategy is to replicate data across multiple data centers
• Test and deployment: With multi-data center setup, it is important to test your website/application at different locations. Automated deployment tools are vital to keep services consistent through all the data centers

## Message queue

A message queue is a durable component, stored in memory, that supports asynchronous communication. It serves as a buffer and distributes asynchronous requests. The basic architecture of a message queue is simple. Input services, called producers/publishers, create messages, and publish them to a message queue. Other services or servers, called consumers/subscribers, connect to the queue, and perform actions defined by the messages.

![[Pasted image 20250909135917.png]]

Decoupling makes the message queue a preferred architecture for building a scalable and reliable application. With the message queue, the producer can post a message to the queue when the consumer is unavailable to process it. The consumer can read messages from the queue even when the producer is unavailable.

## Logging, metrics, automation

Logging: Monitoring error logs is important because it helps to identify errors and problems in the system. You can monitor error logs at per server level or use tools to aggregate them to a centralized service for easy search and viewing.

Metrics: Collecting different types of metrics help us to gain business insights and understand the health status of the system. Some of the following metrics are useful:
	• Host level metrics: CPU, Memory, disk I/O, etc.
	• Aggregated level metrics: for example, the performance of the entire database tier, cache tier, etc.
	• Key business metrics: daily active users, retention, revenue, etc.

Automation: When a system gets big and complex, we need to build or leverage automation tools to improve productivity

![[Pasted image 20250909140106.png]]

## Database scaling

### Vertical scaling
Vertical scaling, also known as scaling up, is the scaling by adding more power (CPU, RAM, DISK, etc.) to an existing machine. There are some powerful database servers.

vertical scaling comes with some serious drawbacks:
**==• You can add more CPU, RAM, etc. to your database server, but there are hardware limits. If you have a large user base, a single server is not enough.**==
==**• Greater risk of single point of failures.**==
==**• The overall cost of vertical scaling is high. Powerful servers are much more expensive.==**

### Horizontal scaling

Horizontal scaling, also known as sharding, is the practice of adding more servers

![[Pasted image 20250909140224.png]]

Sharding separates large databases into smaller, more easily managed parts called shards. Each shard shares the same schema, though the actual data on each shard is unique to the shard.

![[Pasted image 20250909140245.png]]

![[Pasted image 20250909140248.png]]

**==The most important factor to consider when implementing a sharding strategy is the choice of the sharding key. Sharding key (known as a partition key) consists of one or more columns that determine how data is distributed==**

Sharding is a great technique to scale the database but it is far from a perfect solution. It introduces complexities and new challenges to the system:

**Resharding data:** Resharding data is needed when 1) a single shard could no longer hold more data due to rapid growth. 2) Certain shards might experience shard exhaustion faster than others due to uneven data distribution. When shard exhaustion happens, it requires updating the sharding function and moving data around. Consistent hashing, which will be discussed in Chapter 5, is a commonly used technique to solve this problem.

**Celebrity problem:** This is also called a hotspot key problem. Excessive access to a specific shard could cause server overload. Imagine data for Katy Perry, Justin Bieber, and Lady Gaga all end up on the same shard. For social applications, that shard will be overwhelmed with read operations. To solve this problem, we may need to allocate a shard for each celebrity. Each shard might even require further partition.

**Join and de-normalization:** Once a database has been sharded across multiple servers, it is hard to perform join operations across database shards. A common workaround is to de-normalize the database so that queries can be performed in a single table.

![[Pasted image 20250909140441.png]]

## Millions of users and beyond

**==• Keep web tier stateless**==
==**• Build redundancy at every tier**==
==**• Cache data as much as you can**==
==**• Support multiple data centers**==
==**• Host static assets in CDN**==
==**• Scale your data tier by sharding**==
==**• Split tiers into individual services**==
==**• Monitor your system and use automation tools==**

# CHAPTER 2: BACK-OF-THE-ENVELOPE ESTIMATION

## Power of two

Although data volume can become enormous when dealing with distributed systems, calculation all boils down to the basics. To obtain correct calculations, it is critical to know the data volume unit using the power of 2. A byte is a sequence of 8 bits. An ASCII character uses one byte of memory (8 bits).

![[Pasted image 20250910160508.png]]

## Availability numbers

High availability is the ability of a system to be continuously operational for a desirably long period of time. High availability is measured as a percentage, with 100% means a service that has 0 downtime. Most services fall between 99% and 100%.

A service level agreement (SLA) is a commonly used term for service providers. This is an agreement between you (the service provider) and your customer, and this agreement formally defines the level of uptime your service will deliver.

![[Pasted image 20250910160605.png]]

## Tips

Back-of-the-envelope estimation is all about the process. Solving the problem is more
important than obtaining results. Interviewers may test your problem-solving skills. Here are a few tips to follow:

• Rounding and Approximation. It is difficult to perform complicated math operations during the interview. For example, what is the result of “99987 / 9.1”? There is no need to spend valuable time to solve complicated math problems. Precision is not expected. Use round numbers and approximation to your advantage. The division question can be simplified as follows: “100,000 / 10”.
• Write down your assumptions. It is a good idea to write down your assumptions to be referenced later.
• Label your units. When you write down “5”, does it mean 5 KB or 5 MB? You might confuse yourself with this. Write down the units because “5 MB” helps to remove ambiguity.
• Commonly asked back-of-the-envelope estimations: QPS, peak QPS, storage, cache, number of servers, etc. You can practice these calculations when preparing for an interview. Practice makes perfect

# CHAPTER 3: A FRAMEWORK FOR SYSTEM DESIGN INTERVIEWS

The system design interview simulates real-life problem solving where two co-workers collaborate on an ambiguous problem and come up with a solution that meets their goals. The problem is open-ended, and there is no perfect answer. The final design is less important compared to the work you put in the design process. This allows you to demonstrate your design skill, defend your design choices, and respond to feedback in a constructive manner.

An effective system design interview gives strong signals about a person's ability to collaborate, to work under pressure, and to resolve ambiguity constructively. The ability to ask good questions is also an essential skill, and many interviewers specifically look for this skill.

**==Over-engineering is a real disease of many engineers as they delight in design purity and ignore tradeoffs. They are often unaware of the compounding costs of over-engineered systems, and many companies pay a high price for that ignorance.==**

## A 4-step process for effective system design interview

### Step 1 - Understand the problem and establish design scope

**==In a system design interview, giving out an answer quickly without thinking gives you no bonus points. Answering without a thorough understanding of the requirements is a huge red flag as the interview is not a trivia contest. There is no right answer.==**

When you ask a question, the interviewer either answers your question directly or asks you to make your assumptions. If the latter happens, write down your assumptions on the whiteboard or paper. You might need them later.

What kind of questions to ask? Ask questions to understand the exact requirements. Here is a
list of questions to help you get started:
**==• What specific features are we going to build?**==
==**• How many users does the product have?**==
==**• How fast does the company anticipate to scale up? What are the anticipated scales in 3 months, 6 months, and a year?**==
==**• What is the company’s technology stack? What existing services you might leverage to simplify the design?==**

### Step 2 - Propose high-level design and get buy-in

It is a great idea to collaborate with the interviewer during the process. 

• Come up with an initial blueprint for the design. Ask for feedback. Treat your interviewer as a teammate and work together.
• Draw box diagrams with key components on the whiteboard or paper. This might include clients (mobile/web), APIs, web servers, data stores, cache, CDN, message queue, etc.
• Do back-of-the-envelope calculations to evaluate if your blueprint fits the scale constraints. Think

**==If possible, go through a few concrete use cases.==** This will help you frame the high-level design.

### Step 3 - Design deep dive

• Agreed on the overall goals and feature scope
• Sketched out a high-level blueprint for the overall design
• Obtained feedback from your interviewer on the high-level design
• Had some initial ideas about areas to focus on in deep dive based on her feedback

**==Time management is essential as it is easy to get carried away with minute details that do not demonstrate your abilities. You must be armed with signals to show your interviewer.==**

### Step 4 - Wrap up

In this final step, the interviewer might ask you a few follow-up questions or give you the freedom to discuss other additional points.

• The interviewer might want you to identify the system bottlenecks and discuss potential improvements. **==Never say your design is perfect and nothing can be improved. There is always something to improve upon.==**

• It could be useful to give the interviewer a recap of your design. This is particularly important if you suggested a few solutions. Refreshing your interviewer’s memory can be helpful after a long session.

• Error cases (server failure, network loss, etc.) are interesting to talk about.

• Operation issues are worth mentioning. How do you monitor metrics and error logs?

• How to handle the next scale curve is also an interesting topic

• Propose other refinements you need if you had more time.

## Tips

### ==**Dos**==
==**• Always ask for clarification. Do not assume your assumption is correct.**==
==**• Understand the requirements of the problem.**==
==**• There is neither the right answer nor the best answer. A solution designed to solve the**==
==**problems of a young startup is different from that of an established company with millions of users. Make sure you understand the requirements.**==
==**• Let the interviewer know what you are thinking. Communicate with your interview. • Suggest multiple approaches if possible.**==
==**• Once you agree with your interviewer on the blueprint, go into details on each component. Design the most critical components first.**==
==**• Bounce ideas off the interviewer. A good interviewer works with you as a teammate.**==
==**• Never give up.**==

### ==**Don’ts**==
==**• Don't be unprepared for typical interview questions.**==
==**• Don’t jump into a solution without clarifying the requirements and assumptions.**==
==**• Don’t go into too much detail on a single component in the beginning. Give the high level design first then drills down.**==
==**• If you get stuck, don't hesitate to ask for hints.**==
==**• Again, communicate. Don't think in silence.**== 
==**• Don’t think your interview is done once you give the design. You are not done until your interviewer says you are done. Ask for feedback early and often.==**

# CHAPTER 4: DESIGN A RATE LIMITER

- Prevent resource starvation caused by Denial of Service (DoS) attack. Almost all APIs published by large tech companies enforce some form of rate limiting A rate limiter prevents DoS attacks, either intentional or unintentional, by blocking the excess calls.
- Reduce cost. Limiting excess requests means fewer servers and allocating more resources to high priority APIs. Rate limiting is extremely important for companies that use paid third party APIs. For example, you are charged on a per-call basis for the following external APIs
- Prevent servers from being overloaded. To reduce server load, a rate limiter is used to filter out excess requests caused by bots or users’ misbehavior.

## Step 1 - Understand the problem and establish design scope

Rate limiting can be implemented using different algorithms, each with its pros and cons.

- What kind of rate limiter are we going to design? Is it a client-side rate limiter or server-side API rate limiter?
- Does the rate limiter throttle API requests based on IP, the user ID, or other properties?
- What is the scale of the system? Is it built for a startup or a big company with a large user base?
- Will the system work in a distributed environment?
 
 Requirements
Here is a summary of the requirements for the system:

- ==**Accurately limit excessive requests.**==  
- ==**Low latency. The rate limiter should not slow down HTTP response time.**==  
- ==**Use as little memory as possible.**==  
- ==**Distributed rate limiting. The rate limiter can be shared across multiple servers or processes.**==  
- ==**Exception handling. Show clear exceptions to users when their requests are throttled.**==  
- ==**High fault tolerance. If there are any problems with the rate limiter (for example, a cache server goes offline), it does not affect the entire system.==**  

## Step 2 - Propose high-level design and get buy-in

### Where to put the rate limiter?

• Client-side implementation. Generally speaking, client is an unreliable place to enforce rate limiting because client requests can easily be forged by malicious actors.

• Server-side implementation. Figure 4-1 shows a rate limiter that is placed on the server side

![[Pasted image 20250911134534.png]]

Besides the client and server-side implementations, there is an alternative way. Instead of putting a rate limiter at the API servers, we create a rate limiter middleware, which throttles requests to your APIs

**==Instead of putting a rate limiter at the API servers, we create a rate limiter middleware, which throttles requests to your APIs==**

![[Pasted image 20250911134626.png]]

Cloud microservices [4] have become widely popular and rate limiting is usually implemented within a component called API gateway. API gateway is a fully managed service that supports rate limiting, SSL termination, authentication, IP whitelisting, servicing static content,

While designing a rate limiter, an important question to ask ourselves is: where should the rater limiter be implemented, on the server-side or in a gateway? There is no absolute answer. It depends on your company’s current technology stack, engineering resources, priorities, goals

• Evaluate your current technology stack, such as programming language, cache service, etc.
• Identify the rate limiting algorithm that fits your business needs. When you implement everything on the server-side, you have full control of the algorithm
• If you have already used microservice architecture and included an API gateway in the design to perform authentication, IP whitelisting, etc., you may add a rate limiter to the API gateway
• Building your own rate limiting service takes time. If you do not have enough engineering resources to implement a rate limiter, a commercial API gateway is a better option

### Algorithms for rate limiting

#### Token bucket algorithm

The token bucket algorithm is widely used for rate limiting. It is simple, well understood and commonly used by internet companies. Both Amazon [5] and Stripe [6] use this algorithm to throttle their API requests. The token bucket algorithm work as follows

• A token bucket is a container that has pre-defined capacity. Tokens are put in the bucket at preset rates periodically. Once the bucket is full, no more tokens are added

• Each request consumes one token. When a request arrives, we check if there are enough tokens in the bucket.
	• If there are enough tokens, we take one token out for each request, and the request goes through.
	• If there are not enough tokens, the request is dropped.

![[Pasted image 20250911140010.png]]

The token bucket algorithm takes two parameters:
**==• Bucket size: the maximum number of tokens allowed in the bucket**==
==**• Refill rate: number of tokens put into the bucket every second==**

 **Pros**

- The algorithm is easy to implement.  
- Memory efficient.  
- Token bucket allows a burst of traffic for short periods. A request can go through as long as there are tokens left.  

 **Cons**

- Two parameters in the algorithm are bucket size and token refill rate. However, it might be challenging to tune them properly.  

#### Leaking bucket algorithm

except that requests are processed at a fixed rate. **==It is usually implemented with a first-in-first-out (FIFO) queue.==**

• When a request arrives, the system checks if the queue is full. If it is not full, the request is added to the queue.
• Otherwise, the request is dropped.
• Requests are pulled from the queue and processed at regular intervals

![[Pasted image 20250911140019.png]]

Leaking bucket algorithm takes the following two parameters:
**==• Bucket size: it is equal to the queue size. The queue holds the requests to be processed at a fixed rate.**==
==**• Outflow rate: it defines how many requests can be processed at a fixed rate, usually in seconds.==**

**Pros**  
- Memory efficient given the limited queue size.  
- Requests are processed at a fixed rate therefore it is suitable for use cases that a stable outflow rate is needed.  

**Cons**  
- A burst of traffic fills up the queue with old requests, and if they are not processed in time, recent requests will be rate limited.  
- There are two parameters in the algorithm. It might not be easy to tune them properly.  

#### Fixed window counter algorithm

==**• The algorithm divides the timeline into fix-sized time windows and assign a counter for each window.**==
==**• Each request increments the counter by one.**==
==**• Once the counter reaches the pre-defined threshold, new requests are dropped until a new time window starts.**==

![[Pasted image 20250911140238.png]]

**==A major problem with this algorithm is that a burst of traffic at the edges of time windows could cause more requests than allowed quota to go through==**

#### Sliding window log algorithm

**==• The algorithm keeps track of request timestamps. Timestamp data is usually kept in cache, such as sorted sets of ``Redis``**==
==**• When a new request comes in, remove all the outdated timestamps. Outdated timestamps are defined as those older than the start of the current time window.**==
==**• Add timestamp of the new request to the log.**==
==**• If the log size is the same or lower than the allowed count, a request is accepted. Otherwise, it is rejected.==**

![[Pasted image 20250911140536.png]]


**Pros**  
- Rate limiting implemented by this algorithm is very accurate. In any rolling window, requests will not exceed the rate limit.  

**Cons**  
- The algorithm consumes a lot of memory because even if a request is rejected, its timestamp might still be stored in memory.  

### High-level architecture

The basic idea of rate limiting algorithms is simple. At the high-level, we need a counter to keep track of how many requests are sent from the same user, IP address, etc. If the counter is larger than the limit, the request is disallowed.

Where shall we store counters? **==Using the database is not a good idea due to slowness of disk access. In-memory cache is chosen because it is fast and supports time-based expiration strategy.==**

![[Pasted image 20250911140820.png]]

• The client sends a request to rate limiting middleware.
• Rate limiting middleware fetches the counter from the corresponding bucket in ``Redis`` and checks if the limit is reached or not.
	• If the limit is reached, the request is rejected.
	• If the limit is not reached, the request is sent to API servers. Meanwhile, the system
	increments the counter and saves it back to ``Redis``.

## Step 3 - Design deep dive

**==• How are rate limiting rules created? Where are the rules stored?**==
==**• How to handle requests that are rate limited?==**

### Rate limiting rules

```yaml
domain: messaging
descriptors:
- key: message_type
Value: marketing
rate_limit:
unit: day
requests_per_unit: 5
```

```yaml
domain: auth
descriptors:
- key: auth_type
Value: login
rate_limit:
unit: minute
requests_per_unit: 5
```

**==Rules are generally written in configuration files and saved on disk.==**

### Exceeding the rate limit

In case a request is rate limited, APIs return a HTTP response code 429 (too many requests) to the client. Depending on the use cases, we may enqueue the rate-limited requests to be processed later

**Rate limiter headers**

The client knows whether it is being throttled and how many requests remain through HTTP response headers.  
The rate limiter returns the following headers:  

- **X-Ratelimit-Remaining**: The remaining number of allowed requests within the window.  
- **X-Ratelimit-Limit**: Indicates how many calls the client can make per time window.  
- **X-Ratelimit-Retry-After**: The number of seconds to wait until you can make a request again without being throttled.  

When a user has sent too many requests, a **429 Too Many Requests** error and the **X-Ratelimit-Retry-After** header are returned to the client.  

![[Pasted image 20250911141249.png]]

- ==**Rules are stored on the disk. Workers frequently pull rules from the disk and store them in the cache.**==  
- ==**When a client sends a request to the server, the request is sent to the rate limiter middleware first.**==  
- ==**Rate limiter middleware loads rules from the cache. It fetches counters and last request timestamp from ``Redis`` cache. Based on the response, the rate limiter decides:**==  
  - ==**If the request is not rate limited, it is forwarded to API servers.**==  
  - ==**If the request is rate limited, the rate limiter returns 429 Too Many Requests error to the client. In the meantime, the request is either dropped or forwarded to the queue.==**  

### Rate limiter in a distributed environment

There are two challenges:
• Race condition
• Synchronization issue

**Race condition**

• Read the counter value from ``Redis``.
• Check if ( counter + 1 ) exceeds the threshold.
• If not, increment the counter value by 1 in ``Redis``.

**==Locks are the most obvious solution for solving race condition. However, locks will significantly slow down the system.==** Two strategies are commonly used to solve the problem: Lua script [13] and sorted sets data structure in ``Redis`` [8].

**Synchronization issue**

Synchronization is another important factor to consider in a distributed environment. To support millions of users, one rate limiter server might not be enough to handle the traffic. When multiple rate limiter servers are used, synchronization is required.

One possible solution is to use sticky sessions that allow a client to send traffic to the same rate limiter. This solution is not advisable because it is neither scalable nor flexible. A better approach is to use centralized data stores like ``Redis``.

![[Pasted image 20250911141629.png]]

### Performance optimization

First, multi-data center setup is crucial for a rate limiter because latency is high for users located far away from the data center. Most cloud service providers build many edge server locations around the world

### Monitoring

After the rate limiter is put in place, it is important to gather analytics data to check whether the rate limiter is effective. Primarily, we want to make sure:
• The rate limiting algorithm is effective.
• The rate limiting rules are effective.

For example, if rate limiting rules are too strict, many valid requests are dropped. In this case, we want to relax the rules a little bit. In another example, we notice our rate limiter becomes ineffective when there is a sudden increase in traffic like flash sales. In this scenario, we may replace the algorithm to support burst traffic. Token bucket is a good fit here.

## Step 4 - Wrap up

• Token bucket
• Leaking bucket
• Fixed window
• Sliding window log
• Sliding window counter

• Hard vs soft rate limiting.
• Hard: The number of requests cannot exceed the threshold.
• Soft: Requests can exceed the threshold for a short period

 Avoid being rate limited. Design your client with best practices:  
  - ==**Use client cache to avoid making frequent API calls.**==  
  - ==**Understand the limit and do not send too many requests in a short time frame.**==  
  - ==**Include code to catch exceptions or errors so your client can gracefully recover from exceptions.**==  
  - ==**Add sufficient back off time to retry logic.==**  

# CHAPTER 5: DESIGN CONSISTENT HASHING

To achieve horizontal scaling, it is important to distribute requests/data efficiently and evenly across servers

## The rehashing problem
If you have n cache servers, a common way to balance the load is to use the following hash
method: 
serverIndex = hash(key) % N, where N is the size of the server pool.

![[Pasted image 20250913195429.png]]

To fetch the server where a key is stored, we perform the modular operation f(key) % 4. For instance, hash(key0) % 4 = 1 means a client must contact server 1 to fetch the cached data.

![[Pasted image 20250913195518.png]]

This approach works well when the size of the server pool is fixed, and the data distribution is even. **==However, problems arise when new servers are added, or existing servers are removed.==**

Consistent hashing is an effective technique to mitigate this problem.

## Consistent hashing

Consistent hashing is a special kind of hashing such that when a hash table is re-sized and consistent hashing is used, only k/n keys need to be remapped on average, where k is the number of keys, and n is the number of slots. In contrast, in most traditional hash tables, a change in the number of array slots causes nearly all keys to be remapped
![[Pasted image 20250913195642.png]]

![[Pasted image 20250913195647.png]]

## Hash servers

Using the same hash function f, we map servers based on server IP or name onto the ring.

![[Pasted image 20250913195715.png]]

## Hash keys

One thing worth mentioning is that hash function used here is different from the one in “the rehashing problem,” and there is no modular operation.

![[Pasted image 20250913195731.png]]

## Server lookup

To determine which server a key is stored on, we go clockwise from the key position on the ring until a server is found. Figure 5-7 explains this process. Going clockwise, key0 is stored on server 0; key1 is stored on server 1; key2 is stored on server 2 and key3 is stored on server 3.

![[Pasted image 20250913195800.png]]

## Add a server

Using the logic described above, adding a new server will only require redistribution of a fraction of keys

![[Pasted image 20250913200109.png]]

## Remove a server
When a server is removed, only a small fraction of keys require redistribution with consistent hashing.

![[Pasted image 20250913200124.png]]

## Two issues in the basic approach
The consistent hashing algorithm was introduced by Karger et al. at MIT [1]. The basic steps
are:
**==• Map servers and keys on to the ring using a uniformly distributed hash function.**==
==**• To find out which server a key is mapped to, go clockwise from the key position until the first server on the ring is found.==**

## Wrap up

The benefits of consistent hashing include:
**==• Minimized keys are redistributed when servers are added or removed.**==
==**• It is easy to scale horizontally because data are more evenly distributed.**==
==**• Mitigate hotspot key problem. Excessive access to a specific shard could cause server**==
==**overload. Imagine data for Katy Perry, Justin Bieber, and Lady Gaga all end up on the same shard. Consistent hashing helps to mitigate the problem by distributing the data more evenly.==**

# CHAPTER 6: DESIGN A KEY-VALUE STORE

A key-value store, also referred to as a key-value database, is a non-relational database. Each unique identifier is stored as a key with its associated value. This data pairing is known as a “key-value” pair.

**==a key-value pair, the key must be unique, and the value associated with the key can be accessed through the key==**. Keys can be plain text or hashed values. For performance reasons, a short key works better.

you are asked to design a key-value store that supports the following
operations:
- put(key, value) // insert “value” associated with “key”
- get(key) // get “value” associated with “key”

## Understand the problem and establish design scope

• The size of a key-value pair is small: less than 10 KB.
• Ability to store big data.
• High availability: The system responds quickly, even during failures.
• High scalability: The system can be scaled to support large data set.
• Automatic scaling: The addition/deletion of servers should be automatic based on traffic.
• Tunable consistency.
• Low latency

## Single server key-value store

An intuitive approach is to store key-value pairs in a hash table, which keeps everything in memory. Even though memory access is fast, fitting everything in memory may be impossible due to the space constraint. Two optimizations can be done to fit more data in a single server:

**==• Data compression**==
==**• Store only frequently used data in memory and the rest on disk==**

Even with these optimizations, a single server can reach its capacity very quickly. **==A distributed key-value store is required to support big data.==**

## Distributed key-value store

When designing a distributed system, it is important to understand CAP (**C**onsistency, **A**vailability, **P**artition Tolerance) theorem

## CAP theorem
**==CAP theorem states it is impossible for a distributed system to simultaneously provide more than two of these three guarantees: consistency, availability, and partition tolerance.==**

- **Consistency**: consistency means all clients see the same data at the same time no matter which node they connect to.
- **Availability**: availability means any client which requests data gets a response even if some of the nodes are down.
- **Partition** Tolerance: a partition indicates a communication break between two nodes. Partition tolerance means the system continues to operate despite network partitions

![[Pasted image 20250914115042.png]]

- **CP (consistency and partition tolerance)** systems: a CP key-value store supports consistency and partition tolerance while sacrificing availability.
- **AP (availability and partition tolerance)** systems: an AP key-value store supports availability and partition tolerance while sacrificing consistency.
- **CA (consistency and availability)** systems: a CA key-value store supports consistency and availability while sacrificing partition tolerance

**==Since network failure is unavoidable, a distributed system must tolerate network partition. Thus, a CA system cannot exist in real world applications.==**

**Ideal situation**
In the ideal world, network partition never occurs. Data written to n1 is automatically replicated to n2 and n3. Both consistency and availability are achieved.

**Real-world distributed systems**
**==In a distributed system, partitions cannot be avoided, and when a partition occurs, we must choose between consistency and availability==**

![[Pasted image 20250914115527.png]]

**==If we choose consistency over availability (CP system), we must block all write operations to n1 and n2 to avoid data inconsistency among these three servers, which makes the system unavailable.==** Bank systems usually have extremely high consistent requirements.

**==However, if we choose availability over consistency (AP system), the system keeps accepting reads, even though it might return stale data. For writes, n1 and n2 will keep accepting writes, and data will be synced to n3 when the network partition is resolved==**

**System components**

Data partition
• Data replication
• Consistency
• Inconsistency resolution
• Handling failures
• System architecture diagram
• Write path
• Read path

## Data partition

For large applications, it is infeasible to fit the complete data set in a single server. The simplest way to accomplish this is to split the data into smaller partitions and store them in multiple servers. There are two challenges while partitioning the data:
	• Distribute data across multiple servers evenly.
	• Minimize data movement when nodes are added or removed.

**==Consistent hashing==** discussed in Chapter 5 is a great technique to solve these problems.

**Automatic scaling**: servers could be added and removed automatically depending on the load.
**Heterogeneity**: the number of virtual nodes for a server is proportional to the server capacity.
For example, servers with higher capacity are assigned with more virtual nodes

## Data replication

To achieve high availability and reliability, data must be replicated asynchronously over N servers, where N is a configurable parameter. These N servers are chosen using the following logic: after a key is mapped to a position on the hash ring, walk clockwise from that position and choose the first N servers on the ring to store data copies

With virtual nodes, the first N nodes on the ring may be owned by fewer than N physical servers. To avoid this issue, we only choose unique servers while performing the clockwise walk logic.

Nodes in the same data center often fail at the same time due to power outages, network issues, natural disasters, etc. For better reliability, replicas are placed in distinct data centers, and data centers are connected through high-speed networks

## Consistency

Since data is replicated at multiple nodes, it must be synchronized across replicas. Quorum consensus can guarantee consistency for both read and write operations. Let us establish a few definitions first.

N = The number of replicas
W = A write quorum of size W. For a write operation to be considered as successful, write operation must be acknowledged from W replicas.
R = A read quorum of size R. For a read operation to be considered as successful, read operation must wait for responses from at least R replicas.

![[Pasted image 20250914120029.png]]

Depending on the requirement, we can tune the values of W, R, N to achieve the desired level of consistency

**Consistency models**

Consistency models are an important factor to consider when designing a key-value store. A consistency model defines the degree of data consistency, and a wide spectrum of possible consistency models exist:

- **Strong consistency**: any read operation returns a value corresponding to the result of the most updated write data item. A client never sees out-of-date data.
    
- **Weak consistency**: subsequent read operations may not see the most updated value.
    
- **Eventual consistency**: this is a specific form of weak consistency. Given enough time, all updates are propagated, and all replicas are consistent.
    

**==Strong consistency is usually achieved by forcing a replica not to accept new reads/writes until every replica has agreed on the current write. This approach is not ideal for highly available systems because it could block new operations.**==

==**Dynamo and Cassandra adopt eventual consistency, which is the recommended consistency model for our key-value store.**==

==**From concurrent writes, eventual consistency allows inconsistent values to enter the system and forces the client to read the values to reconcile.==**

## Inconsistency resolution: 

**versioning**

Replication gives high availability but causes inconsistencies among replicas. Versioning and vector locks are used to solve inconsistency problems. **==Versioning means treating each data modification as a new immutable version of data.==**

![[Pasted image 20250914120249.png]]

![[Pasted image 20250914120254.png]]

A vector clock is a [server, version] pair associated with a data item. It can be used to check if one version precedes, succeeds, or is in conflict with others.

Assume a vector clock is represented by D([S1, v1], [S2, v2], …, [Sn, vn]), where D is a data item, v1 is a version counter, and s1 is a server number, etc. If data item D is written to server Si, the system must perform one of the following tasks:

- Increment vi if [Si, vi] exists.
    
- Otherwise, create a new entry [Si, 1].

![[Pasted image 20250914120344.png]]

1. A client writes data item D1 to server Sx, which now has the vector clock D1([Sx, 1]).
    
2. Another client reads the latest D1, updates it to D2, and writes it back. D2 descends from D1, so it overwrites D1. The write is handled by the same server Sx, which now has vector clock D2([Sx, 2]).
    
3. Another client reads the latest D2, updates it to D3, and writes it back. The write is handled by server Sy, which now has vector clock D3([Sx, 2], [Sy, 1]).
    
4. Another client reads the latest D2, updates it to D4, and writes it back. The write is handled by server Sz, which now has vector clock D4([Sx, 2], [Sz, 1]).
    
5. When another client reads D3 and D4, it discovers a conflict caused by data item D2 being modified by both Sy and Sz. The conflict is resolved by the client, and the updated data is sent to the server.

## Handling failures

As with any large system at scale, failures are not only inevitable but common. Handling failure scenarios is very important. In this section, we first introduce techniques to detect failures. Then, we go over common failure resolution strategies.

**Failure detection**

In a distributed system, it is insufficient to believe that a server is down because another server says so. Usually, it requires at least two independent sources of information to mark a server down.

![[Pasted image 20250914120517.png]]

A better solution is to use decentralized failure detection methods like gossip protocol.

Gossip protocol works as follows:

- ==**Each node maintains a node membership list, which contains member IDs and heartbeat counters.**==
    
- ==**Each node periodically increments its heartbeat counter.**==
    
- ==**Each node periodically sends heartbeats to a set of random nodes, which in turn propagate to another set of nodes.**==
    
- ==**Once nodes receive heartbeats, membership list is updated to the latest info.**==
    
- ==**If the heartbeat has not increased for more than predefined periods, the member is considered as offline.==**


**Handling temporary failures**
After failures have been detected through the gossip protocol, the system needs to deploy certain mechanisms to ensure availability. In the strict quorum approach, read and write operations could be blocked as illustrated in the quorum consensus section.

A technique called “sloppy quorum” [4] is used to improve availability. Instead of enforcing the quorum requirement, the system chooses the first W healthy servers for writes and first R healthy servers for reads on the hash ring. Offline servers are ignored.
 
 If a server is unavailable due to network or server failures, another server will process requests temporarily. When the down server is up, changes will be pushed back to achieve data consistency. This process is called hinted handoff. Since s2 is unavailable in Figure 6- 12, reads and writes will be handled by s3 temporarily

![[Pasted image 20250914120701.png]]

Hinted handoff is used to handle temporary failures. What if a replica is permanently unavailable? To handle such a situation, we implement an anti-entropy protocol to keep replicas in sync. Anti-entropy involves comparing each piece of data on replicas and updating each replica to the newest version. A Merkle tree is used for inconsistency detection and minimizing the amount of data transferred.

## System architecture diagram

![[Pasted image 20250914120735.png]]

Main features of the architecture are listed as follows:
==**• Clients communicate with the key-value store through simple APIs: get(key) and put(key, value).**==
==**• A coordinator is a node that acts as a proxy between the client and the key-value store.**==
==**• Nodes are distributed on a ring using consistent hashing.**==
==**• The system is completely decentralized so adding and moving nodes can be automatic.**==
==**• Data is replicated at multiple nodes.**==
==**• There is no single point of failure as every node has the same set of responsibilities.**==

## Summary

![[Pasted image 20250914120923.png]]

# CHAPTER 7: DESIGN A UNIQUE ID GENERATOR IN DISTRIBUTED SYSTEMS

``auto_increment`` does not work in a distributed environment because a single database server is not large enough and generating unique IDs across multiple databases with minimal delay is challenging

![[Pasted image 20250915150625.png]]

## Step 1 - Understand the problem and establish design scope

- What are the characteristics of unique IDs?
- For each new record, does ID increment by 1?
- Do IDs only contain numerical values?
- What is the ID length requirement?
- What is the scale of the system?


• IDs must be unique.
• IDs are numerical values only.
• IDs fit into 64-bit.
• IDs are ordered by date.
• Ability to generate over 10,000 unique IDs per second.

## Step 2 - Propose high-level design and get buy-in

• Multi-master replication
• Universally unique identifier (UUID)
• Ticket server
• Twitter snowflake approach

### Multi-master replication

![[Pasted image 20250915150757.png]]

This approach uses the databases’ ``auto_increment`` feature. Instead of increasing the next ID by 1, we increase it by k, where k is the number of database servers in use. As illustrated in Figure 7-2, next ID to be generated is equal to the previous ID in the same server plus 2. This solves some scalability issues because IDs can scale with the number of database servers.
However, this strategy has some major drawbacks:

==**• Hard to scale with multiple data centers**==
==**• IDs do not go up with time across multiple servers.**==
==**• It does not scale well when a server is added or removed.**==

### UUID

A UUID is another easy way to obtain unique IDs. UUID is a 128-bit number used to identify information in computer systems. UUID has a very low probability of getting collusion. **==UUIDs can be generated independently without coordination between servers.==**

![[Pasted image 20250915150952.png]]

**Pros:**  
• Generating UUID is simple. No coordination between servers is needed so there will not be any synchronization issues.  
• The system is easy to scale because each web server is responsible for generating IDs they consume. ID generator can easily scale with web servers.

**Cons:**  
• IDs are 128 bits long, but our requirement is 64 bits.  
• IDs do not go up with time.  
• IDs could be non-numeric.

### Ticket Server
Ticket servers are another interesting way to generate unique IDs. Flicker developed ticket servers to generate distributed primary keys [2]. It is worth mentioning how the system works.

![[Pasted image 20250915151039.png]]

**==The idea is to use a centralized ``auto_increment`` feature in a single database server==**

**Pros:**  
• Numeric IDs.  
• It is easy to implement, and it works for small to medium-scale applications.

**Cons:**  
• Single point of failure. Single ticket server means if the ticket server goes down, all systems that depend on it will face issues.  
• To avoid a single point of failure, we can set up multiple ticket servers. However, this will introduce new challenges such as data synchronization.

### Twitter snowflake approach

Twitter’s unique ID generation system called “snowflake” [3] is inspiring and can satisfy our requirements. Divide and conquer is our friend. Instead of generating an ID directly, we divide an ID into different sections.

![[Pasted image 20250915151204.png]]

==Each section is explained below.==  
==• **Sign bit:** 1 bit. It will always be 0. This is reserved for future uses. It can potentially be used to distinguish between signed and unsigned numbers.==  
==• **Timestamp:** 41 bits. Milliseconds since the epoch or custom epoch. We use Twitter snowflake default epoch 1288834974657, equivalent to Nov 04, 2010, 01:42:54 UTC.==  
==• **Datacenter ID:** 5 bits, which gives us 2 ^ 5 = 32 datacenters.==  
==• **Machine ID:** 5 bits, which gives us 2 ^ 5 = 32 machines per datacenter.==  
==• **Sequence number:** 12 bits. For every ID generated on that machine/process, the sequence number is incremented by 1. The number is reset to 0 every millisecond.==

## Step 3 - Design deep dive

![[Pasted image 20250915151309.png]]

Datacenter IDs and machine IDs are chosen at the startup time, generally fixed once the system is up running. Any changes in datacenter IDs and machine IDs require careful review since an accidental change in those values can lead to ID conflicts. Timestamp and sequence numbers are generated when the ID generator is running.

**Timestamp**

**==The most important 41 bits make up the timestamp section. As timestamps grow with time, IDs are sortable by time.==**

![[Pasted image 20250915151401.png]]

The maximum timestamp that can be represented in 41 bits is 2 ^ 41 - 1 = 2199023255551 milliseconds (ms), which gives us: ~ 69 years = 2199023255551 ms / 1000 seconds / 365 days / 24 hours/ 3600 seconds. This means the ID generator will work for 69 years and having a custom epoch time close to today’s date delays the overflow time.

**Sequence number**

Sequence number is 12 bits, which give us 2 ^ 12 = 4096 combinations. This field is 0 unless more than one ID is generated in a millisecond on the same server. In theory, a machine can support a maximum of 4096 new IDs per millisecond

## Step 4 - Wrap up

If there is extra time at the end of the interview, here are a few additional talking points:  
• **Clock synchronization.** In our design, we assume ID generation servers have the same clock. This assumption might not be true when a server is running on multiple cores. The same challenge exists in multi-machine scenarios. Solutions to clock synchronization are out of the scope of this book; however, it is important to understand the problem exists. Network Time Protocol is the most popular solution to this problem. For interested readers, refer to the reference material [4].  
• **Section length tuning.** For example, fewer sequence numbers but more timestamp bits are effective for low concurrency and long-term applications.  
• **High availability.** Since an ID generator is a mission-critical system, it must be highly available.

# CHAPTER 8: DESIGN A URL SHORTENER

## Step 1 - Understand the problem and establish design scope

- Can you give an example of how a URL shortener work?
- What is the traffic volume?
- How long is the shortened URL?
- What characters are allowed in the shortened URL?
- Can shortened URLs be deleted or updated?

## Step 2 - Propose high-level design and get buy-in

### API Endpoints

1.URL shortening. To create a new short URL, a client sends a POST request, which contains one parameter: the original long URL. The API looks like this:

```postman
POST api/v1/data/shorten
• request parameter: {longUrl: longURLString}
• return shortURL
```

2.URL redirecting. To redirect a short URL to the corresponding long URL, a client sends a GET request. 

```postman
GET api/v1/shortUrl
• Return longURL for HTTP redirection
```

### URL redirecting

![[Pasted image 20250915220544.png]]

**301 redirect.** A 301 redirect shows that the requested URL is “**==permanently==**” moved to the long URL. Since it is permanently redirected, the browser caches the response, and subsequent requests for the same URL will not be sent to the URL shortening service. Instead, requests are redirected to the long URL server directly.

**302 redirect.** A 302 redirect means that the URL is “**==temporarily==**” moved to the long URL, meaning that subsequent requests for the same URL will be sent to the URL shortening service first. Then, they are redirected to the long URL server.

**Each redirection method has its pros and cons.** If the priority is to reduce the server load, using 301 redirect makes sense as only the first request of the same URL is sent to URL shortening servers. However, if analytics is important, 302 redirect is a better choice as it can track click rate and source of the click more easily.

**==The most intuitive way to implement URL redirecting is to use hash tables==**. Assuming the hash table stores ``<shortURL, longURL>`` pairs, URL redirecting can be implemented by the following:

• Get ``longURL``: ``longURL`` = ``hashTable.get(shortURL)``
• Once you get the ``longURL``, perform the URL redirect

### URL shortening

assume the short URL looks like this: ``www.tinyurl.com/{hashValue}``. To support the URL shortening use case, we must find a hash function ``fx`` that maps a long URL to the ``hashValue``

![[Pasted image 20250915220859.png]]

The hash function must satisfy the following requirements:
• Each ``longURL`` must be hashed to one ``hashValue``.
• Each ``hashValue`` can be mapped back to the ``longURL``.

## Step 3 - Design deep dive

### Data model

In the high-level design, everything is stored in a hash table. This is a good starting point; however, this approach is not feasible for real-world systems as memory resources are limited and expensive. A better option is to store ``<shortURL, longURL>`` mapping in a relational database.

### Hash function
Hash function is used to hash a long URL to a short URL, also known as ``hashValue``

#### Hash value length
The ``hashValue`` consists of characters from [0-9, a-z, A-Z], containing 10 + 26 + 26 = 62 possible characters. To figure out the length of ``hashValue``, find the smallest n such that 62^n ≥ 365 billion. The system must support up to 365 billion URLs based on the back of the envelope estimation

#### Hash + collision resolution

To shorten a long URL, we should implement a hash function that hashes a long URL to a 7- character string. A straightforward solution is to use well-known hash functions like CRC32, MD5, or SHA-1.

![[Pasted image 20250915221129.png]]

**How can we make it shorter?**

The first approach is to collect the first 7 characters of a hash value; however, this method can lead to hash collisions. To resolve hash collisions, we can recursively append a new predefined string until no more collision is discovered

![[Pasted image 20250915221212.png]]

This method can eliminate collision; however, it is expensive to query the database to check if a ``shortURL`` exists for every request. A technique called **==bloom filters==** [2] can improve performance. A bloom filter is a space-efficient probabilistic technique to test if an element is a member of a set

**Base 62 conversion**
Base conversion is another approach commonly used for URL ``shorteners``. Base conversion helps to convert the same number between its different number representation systems. Base 62 conversion is used as there are 62 possible characters for ``hashValue``

**Comparison of the two approaches**

![[Pasted image 20250915221454.png]]

### URL shortening deep dive

As one of the core pieces of the system, we want the URL shortening flow to be logically simple and functional

![[Pasted image 20250915221519.png]]

1. `longURL` is the input.  
2. The system checks if the `longURL` is in the database.  
3. If it is, it means the `longURL` was converted to `shortURL` before. In this case, fetch the `shortURL` from the database and return it to the client.  
4. If not, the `longURL` is new. A new unique `ID` (primary key) is generated by the unique ID generator.  
5. Convert the `ID` to `shortURL` with **base62** conversion.  
6. Create a new database row with the `ID`, `shortURL`, and `longURL`.  

### URL redirecting deep dive

![[Pasted image 20250915221618.png]]

1. A user clicks a short URL link: `https://tinyurl.com/zn9edcu`  
2. The load balancer forwards the request to web servers.  
3. If a `shortURL` is already in the cache, return the `longURL` directly.  
4. If a `shortURL` is not in the cache, fetch the `longURL` from the database. If it is not in the database, it is likely a user entered an invalid `shortURL`.  
5. The `longURL` is returned to the user.  

## Step 4 - Wrap up

• **Rate limiter:** A potential security problem we could face is that malicious users send an overwhelmingly large number of URL shortening requests. Rate limiter helps to filter out requests based on IP address or other filtering rules. If you want to refresh your memory about rate limiting, refer to *“Chapter 4: Design a rate limiter”*.  

• **Web server scaling:** Since the web tier is stateless, it is easy to scale the web tier by adding or removing web servers.  

• **Database scaling:** Database replication and sharding are common techniques.  

• **Analytics:** Data is increasingly important for business success. Integrating an analytics solution to the URL shortener could help to answer important questions like *how many people click on a link? When do they click the link?* etc.  

• **Availability, consistency, and reliability:** These concepts are at the core of any large system’s success. 

# CHAPTER 9: DESIGN A WEB CRAWLER

A web crawler is known as a robot or spider. It is widely used by search engines to discover new or updated content on the web. Content can be a web page, an image, a video, a PDF file, etc. A web crawler starts by collecting a few web pages and then follows links on those pages to collect new content.

A crawler is used for many purposes:
• Search engine indexing:
• Web archiving
• Web mining:
• Web monitoring

## Step 1 - Understand the problem and establish design scope

The basic algorithm of a web crawler is simple:
1. ==**Given a set of URLs, download all the web pages addressed by the URLs.**==
2. ==**Extract URLs from these web pages**==
3. ==**Add new URLs to the list of URLs to be downloaded. Repeat these 3 steps.==**

- What is the main purpose of the crawler? Is it used for search engine indexing, data mining, or something else?
- How many web pages does the web crawler collect per month?
- What content types are included? HTML only or other content types such as PDFs and images as well?
- Shall we consider newly added or edited web pages?
- Do we need to store HTML pages crawled from the web?
- How do we handle web pages with duplicate content?

it is also important to note down the following characteristics of a good web crawler:
• Scalability: The web is very large. There are billions of web pages out there. Web crawling should be extremely efficient using parallelization.
• Robustness: The web is full of traps. Bad HTML, unresponsive servers, crashes, malicious links, etc. are all common. The crawler must handle all those edge cases.
• Politeness: The crawler should not make too many requests to a website within a short time interval.
• Extensibility: The system is flexible so that minimal changes are needed to support new content types. For example, if we want to crawl image files in the future, we should not need to redesign the entire system.

## Step 2 - Propose high-level design and get buy-in

### Seed URLs
A web crawler uses seed URLs as a starting point for the crawl process. For example, to crawl all web pages from a university’s website, an intuitive way to select seed URLs is to use the university’s domain name

To crawl the entire web, we need to be creative in selecting seed URLs. **==A good seed URL serves as a good starting point that a crawler can utilize to traverse as many links as possible. The general strategy is to divide the entire URL space into smaller ones.**== 
- ==**The first proposed approach is based on locality as different countries may have different popular websites.**==  
- ==**Another way is to choose seed URLs based on topics; for example, we can divide URL space into shopping, sports, healthcare, etc. Seed URL selection is an open-ended question.==**

### URL Frontier

Most modern web crawlers split the crawl state into two: to be downloaded and already downloaded. The component that stores URLs to be downloaded is called the URL Frontier. **==You can refer to this as a First-in-First-out (FIFO) queue.==**

### HTML Downloader
The HTML downloader downloads web pages from the internet. Those URLs are provided by the URL Frontier.

### DNS Resolver
To download a web page, a URL must be translated into an IP address. The HTML Downloader calls the DNS Resolver to get the corresponding IP address for the URL.

### Content Parser
After a web page is downloaded, it must be parsed and validated because malformed web pages could provoke problems and waste storage space. Implementing a content parser in a crawl server will slow down the crawling process.

### Content Seen?

To compare two HTML documents, we can compare them character by character. However, this method is slow and time-consuming, especially when billions of web pages are involved. **==An efficient way to accomplish this task is to compare the hash values of the two web pages==**

### Content Storage

The choice of storage system depends on factors such as data type, data size, access frequency, life span, etc. Both disk and memory are used.
• Most of the content is stored on disk because the data set is too big to fit in memory.
• Popular content is kept in memory to reduce latency

### URL Extractor
URL Extractor parses and extracts links from HTML pages

###  URL Filter
The URL filter excludes certain content types, file extensions, error links and URLs in “blacklisted” sites.

### URL Seen?
“URL Seen?” is a data structure that keeps track of URLs that are visited before or already in the Frontier. “URL Seen?” helps to avoid adding the same URL multiple times as this can increase server load and cause potential infinite loops.

Bloom filter and hash table are common techniques to implement the “URL Seen?” component

### URL Storage
URL Storage stores already visited URLs

![[Pasted image 20250917111129.png]]

## Step 3 - Design deep dive

### DFS vs BFS
You can think of the web as a directed graph where web pages serve as nodes and hyperlinks (URLs) as edges. The crawl process can be seen as traversing a directed graph from one web page to others. Two common graph traversal algorithms are DFS and BFS. However, DFS is usually not a good choice because the depth of DFS can be very deep. BFS is commonly used by web crawlers and is implemented by a first-in-first-out (FIFO) queue. In a FIFO queue, URLs are dequeued in the order they are enqueued. However, this implementation has two problems:
• Most links from the same web page are linked back to the same host. In Figure 9-5, all the links in wikipedia.com are internal links, making the crawler busy processing URLs from the same host (wikipedia.com). When the crawler tries to download web pages in parallel, **==Wikipedia servers will be flooded with requests. This is considered as “impolite”.==**

![[Pasted image 20250917111315.png]]

• Standard BFS does not take the priority of a URL into consideration. The web is large and not every page has the same level of quality and importance. Therefore, we may want to prioritize URLs according to their page ranks, web traffic, update frequency, etc.

### URL frontier
URL frontier helps to address these problems. A URL frontier is a data structure that stores URLs to be downloaded. The URL frontier is an important component to ensure politeness, URL prioritization, and freshness.

**Politeness**

Generally, a web crawler should avoid sending too many requests to the same hosting server within a short period. Sending too many requests is considered as “impolite” or even treated as denial-of-service (DOS) attack

The general idea of enforcing politeness is to download one page at a time from the same host. A delay can be added between two download tasks. The politeness constraint is implemented by maintain a mapping from website hostnames to download (worker) threads. Each downloader thread has a separate FIFO queue and only downloads URLs obtained from that queue.

![[Pasted image 20250917111435.png]]

**Priority**

random post from a discussion forum about Apple products carries very different weight than posts on the Apple home page. Even though they both have the “Apple” keyword, it is sensible for a crawler to crawl the Apple home page first. We prioritize URLs based on usefulness, which can be measured by PageRank [10], website traffic, update frequency, etc. “Prioritizer” is the component that handles URL prioritization. Refer to the reference materials [5] [10] for in-depth information about this concept.

• Prioritizer: It takes URLs as input and computes the priorities.
• Queue f1 to fn: Each queue has an assigned priority. Queues with high priority are selected with higher probability.
• Queue selector: Randomly choose a queue with a bias towards queues with higher priority.

**Freshness**

Web pages are constantly being added, deleted, and edited. A web crawler must periodically recrawl downloaded pages to keep our data set fresh. Recrawl all the URLs is time consuming and resource intensive. Few strategies to optimize freshness are listed as follows:

**==• Recrawl based on web pages’ update history.**==
==**• Prioritize URLs and recrawl important pages first and more frequently.==**

### HTML Downloader
The HTML Downloader downloads web pages from the internet using the HTTP protocol.

#### Robots.txt

**==Robots.txt, called Robots Exclusion Protocol, is a standard used by websites to communicate with crawlers. It specifies what pages crawlers are allowed to download. Before attempting to crawl a web site, a crawler should check its corresponding robots.txt first and follow its rules.==**

**Performance optimization**

1. Distributed crawl 
	To achieve high performance, crawl jobs are distributed into multiple servers, and each server runs multiple threads. The URL space is partitioned into smaller pieces; so, each downloader is responsible for a subset of the URLs.

2. Cache DNS Resolver
	DNS Resolver is a bottleneck for crawlers because DNS requests might take time due to the synchronous nature of many DNS interfaces. DNS response time ranges from 10ms to 200ms. Once a request to DNS is carried out by a crawler thread, other threads are blocked until the first request is completed.

3. Locality
	Distribute crawl servers geographically. When crawl servers are closer to website hosts, crawlers experience faster download time. Design locality applies to most of the system components: crawl servers, cache, queue, storage, etc.
	
4. Short timeout
	Some web servers respond slowly or may not respond at all. To avoid long wait time, a maximal wait time is specified. If a host does not respond within a predefined time, the crawler will stop the job and crawl some other pages.

### Extensibility
As almost every system evolves, one of the design goals is to make the system flexible enough to support new content types. The crawler can be extended by plugging in new modules.

### Detect and avoid problematic content

#### 1. Redundant content
As discussed previously, nearly 30% of the web pages are duplicates. Hashes or checksums help to detect duplication

#### 2. Spider traps
A spider trap is a web page that causes a crawler in an infinite loop. For instance, an infinite deep directory structure is

Such spider traps can be avoided by setting a maximal length for URLs. However, no one size- fits-all solution exists to detect spider traps. Websites containing spider traps are easy to identify due to an unusually large number of web pages discovered on such websites. It is hard to develop automatic algorithms to avoid spider traps; however, a user can manually verify and identify a spider trap, and either exclude those websites from the crawler or apply some customized URL filters

#### 3. Data noise
Some of the contents have little or no value, such as advertisements, code snippets, spam URLs, etc. Those contents are not useful for crawlers and should be excluded if possible.

## Step 4 - Wrap up

• Server-side rendering: Numerous websites use scripts like JavaScript, AJAX, etc to generate links on the fly. If we download and parse web pages directly, we will not be able to retrieve dynamically generated links. To solve this problem, we perform server-side rendering (also called dynamic rendering) first before parsing a page [12].
• Filter out unwanted pages: With finite storage capacity and crawl resources, an anti-spam component is beneficial in filtering out low quality and spam pages [13] [14].
• Database replication and sharding: Techniques like replication and sharding are used to improve the data layer availability, scalability, and reliability.
• Horizontal scaling: For large scale crawl, hundreds or even thousands of servers are needed to perform download tasks. The key is to keep servers stateless. 
• Availability, consistency, and reliability: These concepts are at the core of any large system’s success. We discussed these concepts in detail in Chapter 1. Refresh your memory on these topics.
• Analytics: Collecting and analyzing data are important parts of any system because data is key ingredient for fine-tuning.

# CHAPTER 10: DESIGN A NOTIFICATION SYSTEM

A notification is more than just mobile push notification. Three types of notification formats are: mobile push notification, SMS message, and Email.

## Step 1 - Understand the problem and establish design scope

- What types of notifications does the system support?
- Is it a real-time system?
- What are the supported devices?
- What triggers notifications?
- Will users be able to opt-out?
- How many notifications are sent out each day?

## Step 2 - Propose high-level design and get buy-in

It is structured as follows:
• Different types of notifications
• Contact info gathering flow
• Notification sending/receiving flow

![[Pasted image 20250917134659.png]]

### Contact info gathering flow

To send notifications, we need to gather mobile device tokens, phone numbers, or email addresses. **==when a user installs our app or signs up for the first time, API servers collect user contact info and store it in the database.==**

Email addresses and phone numbers are stored in the user table, whereas device tokens are stored in the device table

![[Pasted image 20250917134810.png]]

### Notification sending/receiving flow

**Service 1 to N**: A service can be a micro-service, a cron job, or a distributed system that triggers notification sending events. For example, a billing service sends emails to remind customers of their due payment or a shopping website tells customers that their packages will be delivered tomorrow via SMS messages.

**Notification system**: The notification system is the centerpiece of sending/receiving notifications. Starting with something simple, only one notification server is used. It provides APIs for services 1 to N, and builds notification payloads for third party services.

**Third-party services**: Third party services are responsible for delivering notifications to users. While integrating with third-party services, we need to pay extra attention to extensibility. Good extensibility means a flexible system that can easily plugging or unplugging of a third-party service. **==Another important consideration is that a third-party service might be unavailable in new markets or in the future.==**

Three problems are identified in this design:
	==**• Single point of failure (SPOF): A single notification server means SPOF.==**
	**==• Hard to scale: The notification system handles everything related to push notifications in one server. It is challenging to scale databases, caches, and different notification processing components independently.==**
	**==• Performance bottleneck: Processing and sending notifications can be resource intensive. For example, constructing HTML pages and waiting for responses from third party services could take time. Handling everything in one system can result in the system overload, especially during peak hour**==

### High-level design (improved)

**==• Move the database and cache out of the notification server.**==
==**• Add more notification servers and set up automatic horizontal scaling.**==
==**• Introduce message queues to decouple the system components.==**

![[Pasted image 20250917135140.png]]

**Service 1 to N**: They represent different services that send notifications via APIs provided by notification servers.

**Notification servers**: They provide the following functionalities:
• Provide APIs for services to send notifications. Those APIs are only accessible internally
or by verified clients to prevent spams.
• Carry out basic validations to verify emails, phone numbers, etc.
• Query the database or cache to fetch data needed to render a notification.
• Put notification data to message queues for parallel processing

**Cache**: User info, device info, notification templates are cached.
**DB**: It stores data about user, notification, settings, etc.

**Message queues**: Message queues serve as buffers when high volumes of notifications are to be sent out. Each notification type is assigned with a distinct message queue so an outage in one third-party service will not affect other notification types.

**Workers**: Workers are a list of servers that pull notification events from message queues and send them to the corresponding third-party services.

**Third-party services**: Already explained in the initial design.

1. A service calls APIs provided by notification servers to send notifications.
2. Notification servers fetch metadata such as user info, device token, and notification setting from the cache or database.
3. A notification event is sent to the corresponding queue for processing. For instance, an iOS push notification event is sent to the iOS PN queue.
4. Workers pull notification events from message queues.
5. Workers send notifications to third party services.
6. Third-party services send notifications to user devices.

## Step 3 - Design deep dive

### Reliability

**How to prevent data loss?**

One of the most important requirements in a notification system is that it cannot lose data. Notifications can usually be delayed or re-ordered, but never lost. To satisfy this requirement, the notification system persists notification data in a database and implements a retry mechanism. The notification log database is included for data persistence,

![[Pasted image 20250917135523.png]]

**Will recipients receive a notification exactly once?**

To reduce the duplication occurrence, we introduce a dedupe mechanism and handle each failure case carefully. Here is a simple dedupe logic:

**==When a notification event first arrives, we check if it is seen before by checking the event ID. If it is seen before, it is discarded==**. Otherwise, we will send out the notification. For interested readers to explore why we cannot have exactly once delivery, refer to the reference material

**Notification template**

Notification templates are introduced to avoid building every notification from scratch. A notification template is a preformatted notification to create your unique notification by customizing parameters, styling, tracking links, etc. Here is an example template of push notifications.

**Notification setting**

Users generally receive way too many notifications daily and they can easily feel overwhelmed. Thus, many websites and apps give users fine-grained control over notification settings. This information is stored in the notification setting table, with the following fields:

```sql
user_id bigInt
channel varchar # push notification, email or SMS
opt_in boolean # opt-in to receive notification
```

**Rate limiting**

To avoid overwhelming users with too many notifications, we can limit the number of notifications a user can receive. This is important because receivers could turn off notifications completely if we send too often

**Retry mechanism**

When a third-party service fails to send a notification, the notification will be added to the message queue for retrying. If the problem persists, an alert will be sent out to developers

**Security in push notifications**

Only authenticated or verified clients are allowed to send push notifications using our APIs. Interested users should refer to the reference material

**Monitor queued notifications**

**==A key metric to monitor is the total number of queued notifications==**. If the number is large, the notification events are not processed fast enough by workers. To avoid delay in the notification delivery, more workers are needed

**Events tracking**
Notification metrics, such as open rate, click rate, and engagement are important in understanding customer behaviors.

![[Pasted image 20250917140047.png]]

**Updated Design**

![[Pasted image 20250917140645.png]]

• The notification servers are equipped with two more critical features: authentication and rate-limiting.
• We also add a retry mechanism to handle notification failures. If the system fails to send notifications, they are put back in the messaging queue and the workers will retry for a predefined number of times.
• Furthermore, notification templates provide a consistent and efficient notification creation process.
• Finally, monitoring and tracking systems are added for system health checks and future improvements.

## Step 4 - Wrap up

• Reliability: We proposed a robust retry mechanism to minimize the failure rate.
• Security:`` AppKey/appSecret`` pair is used to ensure only verified clients can send notifications.
• Tracking and monitoring: These are implemented in any stage of a notification flow to capture important stats.
• Respect user settings: Users may opt-out of receiving notifications. Our system checks user settings first before sending notifications.
• Rate limiting: Users will appreciate a frequency capping on the number of notifications they receive.


# CHAPTER 11: DESIGN A NEWS FEED SYSTEM

“News feed is the constantly updating list of stories in the middle of your home page. News Feed includes status updates, photos, videos, links, app activity, and likes from people, pages, and groups that you follow on Facebook

## Step 1 - Understand the problem and establish design scope

-  Is this a mobile app? Or a web app? Or both?
- What are the important features?
- Is the news feed sorted by reverse chronological order or any particular order such as topic scores? For instance, posts from your close friends have higher scores.
- How many friends can a user have?
- What is the traffic volume
- Can feed contain images, videos, or just text?

## Step 2 - Propose high-level design and get buy-in

• Feed publishing: when a user publishes a post, corresponding data is written into cache and database. A post is populated to her friends’ news feed.
• Newsfeed building: for simplicity, let us assume the news feed is built by aggregating friends’ posts in reverse chronological order

### Newsfeed APIs

The news feed APIs are the primary ways for clients to communicate with servers. Those APIs are HTTP based that allow clients to perform actions, which include posting a status, retrieving news feed, adding friends,

### Feed publishing API

```json
POST /v1/me/feed
Params:
• content: content is the text of the post.
• auth_token: it is used to authenticate API requests.
```

```json
GET /v1/me/feed
Params:
• auth_token: it is used to authenticate API requests.
```

#### Feed Publishing

- **User**: A user can view news feeds on a browser or mobile app. A user makes a post with content **“Hello”** through API:  
  `/v1/me/feed?content=Hello&auth_token={auth_token}`  

- **Load balancer**: Distributes traffic to web servers.  

- **Web servers**: Redirect traffic to different internal services.  

- **Post service**: Persists post in the **database** and **cache**.  

- **Fanout service**: Pushes new content to friends’ news feed. **Newsfeed data** is stored in the **cache** for fast retrieval.  

- **Notification service**: Informs friends that new content is available and sends out **push notifications**.  


#### Newsfeed building

- **User**: A user sends a request to retrieve her news feed. The request looks like this:  
  `/v1/me/feed`  

- **Load balancer**: Redirects traffic to **web servers**.  

- **Web servers**: Route requests to **newsfeed service**.  

- **Newsfeed service**: Fetches **news feed** from the **cache**.  

- **Newsfeed cache**: Stores **news feed IDs** needed to render the news feed.  


## Step 3 - Design deep dive

### Feed publishing deep dive

![[Pasted image 20250917171322.png]]

- **Web servers**:  
  Besides communicating with clients, web servers enforce **authentication** and **rate-limiting**.  
  - Only users signed in with a valid **``auth_token``** are allowed to make posts.  
  - The system limits the number of posts a user can make within a certain period, which is vital to prevent **spam** and **abusive content**.  

- **Fanout service**:  
  Fanout is the process of delivering a post to all friends. Two types of fanout models are:  
  - **Fanout on write** (push model)  
  - **Fanout on read** (pull model)  

  **Fanout on write**: With this approach, the news feed is pre-computed during **write time**. A new post is delivered to friends’ **cache** immediately after it is published.  
  - **Pros**:  
    • The **news feed** is generated in real-time and can be pushed to friends immediately.  
    • Fetching the **news feed** is fast because it is pre-computed during write time.  
  - **Cons**:  
    • If a user has many friends, fetching the **friend list** and generating news feeds for all of them is slow and time-consuming (**hotkey problem**).  
    • For inactive users or those who rarely log in, pre-computing news feeds **wastes computing resources**.  

  **Fanout on read**: The news feed is generated during **read time**. This is an **on-demand model**. Recent posts are pulled when a user loads her home page.  
  - **Pros**:  
    • For inactive users or those who rarely log in, fanout on read works better because it does not waste **computing resources**.  
    • Data is not pushed to friends so there is no **hotkey problem**.  
  - **Cons**:  
    • Fetching the **news feed** is slow as it is not pre-computed.  


### Newsfeed retrieval deep dive

![[Pasted image 20250917171525.png]]

1. **User** sends a request to retrieve her news feed:  
   `/v1/me/feed`  

2. **Load balancer** redistributes requests to **web servers**.  

3. **Web servers** call the **news feed service** to fetch news feeds.  

4. **News feed service** gets a list of **post IDs** from the **news feed cache**.  

5. A user’s news feed is more than just a list of feed IDs. It contains **username**, **profile picture**, **post content**, **post image**, etc.  
   - Therefore, the **news feed service** fetches the complete **user objects** (from **user cache**) and **post objects** (from **post cache**) to construct the fully hydrated news feed.  

6. The fully hydrated **news feed** is returned in **JSON format** back to the **client** for rendering.  

### Cache architecture

• News Feed: It stores IDs of news feeds.
• Content: It stores every post data. Popular content is stored in hot cache.
• Social Graph: It stores user relationship data.
• Action: It stores info about whether a user liked a post, replied a post, or took other actions on a post.
• Counters: It stores counters for like, reply, follower, following, etc.

## Step 4 - Wrap up

### **Scaling the Database**

- **Vertical scaling vs Horizontal scaling**  
- **SQL vs NoSQL**  
- **Master-slave replication**  
- **Read replicas**  
- **Consistency models**  
- **Database sharding**  

---

### **Other Talking Points**

- **Keep web tier stateless**  
- **Cache data** as much as you can  
- **Support multiple data centers**  
- **Loosely couple components** with **message queues**  
- **Monitor key metrics**:  
  - **QPS** (queries per second) during **peak hours**  
  - **Latency** while users are refreshing their **news feed**  


# CHAPTER 12: DESIGN A CHAT SYSTEM

