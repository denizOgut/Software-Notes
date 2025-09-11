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
