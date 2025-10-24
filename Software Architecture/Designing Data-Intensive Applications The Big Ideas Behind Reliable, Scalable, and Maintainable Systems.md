
# PART I Foundations of Data Systems

## CHAPTER 1 Reliable, Scalable, and Maintainable Applications

Many applications today are data-intensive, as opposed to compute-intensive. Raw CPU power is rarely a limiting factor for these applications—bigger problems are usually the amount of data, the complexity of data, and the speed at which it is changing.

A data-intensive application is typically built from standard building blocks that provide commonly needed functionality.

• Store data so that they, or another application, can find it again later (databases)
• Remember the result of an expensive operation, to speed up reads (caches)
• Allow users to search data by keyword or filter it in various ways (search indexes)
• Send a message to another process, to be handled asynchronously (stream processing)
• Periodically crunch a large amount of accumulated data (batch processing)

There are many database systems with different characteristics, because different applications have different requirements

### Thinking About Data Systems

We typically think of databases, queues, caches, etc. as being very different categories of tools. Although a database and a message queue have some superficial similarity— both store data for some time—they have very different access patterns, which means different performance characteristics, and thus very different implementations

Many new tools for data storage and processing have emerged in recent years. They are optimized for a variety of different use cases, and they no longer neatly fit into traditional categories

Secondly, increasingly many applications now have such demanding or wide-ranging requirements that a single tool can no longer meet all of its data processing and storage needs. Instead, the work is broken down into tasks that can be performed efficiently on a single tool, and those different tools are stitched together using application code.

![[Pasted image 20251008152458.png]]

When you combine several tools in order to provide a service, the service’s interface or application programming interface (API) usually hides those implementation details from clients. Now you have essentially created a new, special-purpose data system from smaller, general-purpose components. Your composite data system may provide certain guarantees: e.g., that the cache will be correctly invalidated or updated on writes so that outside clients see consistent results

If you are designing a data system or service, a lot of tricky questions arise. How do you ensure that the data remains correct and complete, even when things go wrong internally? How do you provide consistently good performance to clients, even when parts of your system are degraded? How do you scale to handle an increase in load? What does a good API for the service look like?

Those factors depend very much on the situation.

- Reliability
	The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults, and even human error)

- Scalability
	As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth

- Maintainability 
	Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively.


### Reliability

• The application performs the function that the user expected.
• It can tolerate the user making mistakes or using the software in unexpected ways.
• Its performance is good enough for the required use case, under the expected load and data volume.
• The system prevents any unauthorized access and abuse.

If all those things together mean “working correctly,” then we can understand reliability as meaning, roughly, “continuing to work correctly, even when things go wrong.”

The things that can go wrong are called faults, and systems that anticipate faults and can cope with them are called fault-tolerant or resilient.

**==it only makes sense to talk about tolerating certain types of faults. A fault is usually defined as one component**== ==**of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user.==** It is impossible to reduce the probability of a fault to zero; therefore it is usually best to design fault-tolerance mechanisms that prevent faults from causing failures.

Counterintuitively, in such fault-tolerant systems, it can make sense to increase the rate of faults by triggering them deliberately—for example, by randomly killing individual processes without warning. Many critical bugs are actually due to poor error handling [3]; by deliberately inducing faults, you ensure that the fault-tolerance machinery is continually exercised and tested, which can increase your confidence that faults will be handled correctly when they occur naturally.

Although we generally prefer tolerating faults over preventing faults, there are cases where prevention is better than cure (e.g., because no cure exists). This is the case with security matters, for example: if an attacker has compromised a system and gained access to sensitive data, that event cannot be undone.

#### Hardware Faults

When we think of causes of system failure, hardware faults quickly come to mind. Hard disks crash, RAM becomes faulty, the power grid has a blackout, someone unplugs the wrong network cable.

Hard disks are reported as having a mean time to failure (MTTF) of about 10 to 50 years [5, 6]. Thus, on a storage cluster with 10,000 disks, we should expect on average one disk to die per day.

Our first response is usually to add redundancy to the individual hardware components in order to reduce the failure rate of the system

This approach cannot completely prevent hardware problems from causing failures, but it is well understood and can often keep a machine running uninterrupted for years.

As long as you can restore a backup onto a new machine fairly quickly, the downtime in case of failure is not catastrophic in most applications. Thus, multi-machine redundancy was only required by a small number of applications for which high availability was absolutely essential.

However, as data volumes and applications’ computing demands have increased, more applications have begun using larger numbers of machines, which proportionally increases the rate of hardware faults.

Hence there is a move toward systems that can tolerate the loss of entire machines, by using software fault-tolerance techniques in preference or in addition to hardware redundancy. Such systems also have operational advantages: a single-server system requires planned downtime if you need to reboot the machine (to apply operating system security patches, for example), whereas a system that can tolerate machine failure can be patched one node at a time, without downtime of the entire system

#### Software Errors

Another class of fault is a systematic error within the system [8]. Such faults are harder to anticipate, and because they are correlated across nodes, they tend to cause many more system failures than uncorrelated hardware faults

- A software bug that causes every instance of an application server to crash when given a particular bad input.

- A runaway process that uses up some shared resource—CPU time, memory, disk
- space, or network bandwidth.

- A service that the system depends on that slows down, becomes unresponsive, or starts returning corrupted responses.

- Cascading failures, where a small fault in one component triggers a fault in another component, which in turn triggers further faults

There is no quick solution to the problem of systematic faults in software. Lots of small things can help: carefully thinking about assumptions and interactions in the system; thorough testing; process isolation; allowing processes to crash and restart; measuring, monitoring, and analyzing system behavior in production. If a system is expected to provide some guarantee it can constantly check itself while it is running and raise an alert if a discrepancy is found

#### Human Errors

Even when they have the best intentions, humans are known to be unreliable.
 
 - Design systems in a way that minimizes opportunities for error

- Decouple the places where people make the most mistakes from the places where they can cause failures. In particular, provide fully featured non-production sandbox environments where people can explore and experiment safely, using real data, without affecting real users.

- Test thoroughly at all levels, from unit tests to whole-system integration tests and manual tests

- Allow quick and easy recovery from human errors, to minimize the impact in the case of a failure. For example, make it fast to roll back configuration changes, roll out new code gradually

- Set up detailed and clear monitoring, such as performance metrics and error rates.

- Implement good management practices and training—a complex and important aspect


#### How Important Is Reliability?

Bugs in business applications cause lost productivity (and legal risks if figures are reported incorrectly), and outages of ecommerce sites can have huge costs in terms of lost revenue and damage to reputation.

Even in “noncritical” applications we have a responsibility to our users. Consider a parent who stores all their pictures and videos of their children in your photo application [15]. How would they feel if that database was suddenly corrupted? Would they know how to restore it from a backup?

There are situations in which we may choose to sacrifice reliability in order to reduce development cost but we
should be very conscious of when we are cutting corners.

### Scalability

Even if a system is working reliably today, that doesn’t mean it will necessarily work reliably in the future. **==One common reason for degradation is increased load:==** Scalability is the term we use to describe a system’s ability to cope with increased load.

scalability means considering questions like “If the system grows in a particular way, what are our options for coping with the growth?” and “How can we add computing resources to handle the additional load

#### Describing Load

Load can be described with a few numbers which we call load parameters. The best choice of parameters depends on the architecture of your system: it may be requests per second to a web server, the ratio of reads to writes in a database, the number of simultaneously active users in a chat room, the hit rate on a cache, or something else.

#### Describing Performance

- When you increase a load parameter and keep the system resources (CPU, memory, network bandwidth, etc.) unchanged, how is the performance of your system affected?

- When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged?

Both questions require performance numbers

> **==Latency and response time are often used synonymously, but they are not the same. The response time is what the client sees: besides the actual time to process the request (the service time), it includes network delays and queueing delays. Latency is the duration that a request is waiting to be handled—during which it is latent, awaiting service==**

Even if you only make the same request over and over again, you’ll get a slightly different response time on every try. In practice, in a system handling a variety of requests, the response time can vary a lot. We therefore need to think of response time not as a single number, but as a distribution of values that you can measure

It’s common to see the average response time of a service reported However, the mean is not a very good metric if you want to know your “typical” response time, because it doesn’t tell you how many users actually experienced that delay. Usually it is better to use percentiles. If you take your list of response times and sort it from fastest to slowest, then the median is the halfway point

This makes the median a good metric if you want to know how long users typically have to wait: half of user requests are served in less than the median response time, and the other half take longer than the median. The median is also known as the 50th percentile, and sometimes abbreviated as p50. Note that the median refers to a single request; if the user makes several requests (over the course of a session, or because several resources are included in a single page), the probability that at least one of them is slower than the median is much greater than 50%.

High percentiles of response times, also known as tail latencies, are important because they directly affect users’ experience of the service.

On the other hand, optimizing the 99.99th percentile (the slowest 1 in 10,000 requests) was deemed too expensive and to not yield enough benefit for Amazon’s purposes. Reducing response times at very high percentiles is difficult because they are easily affected by random events outside of your control, and the benefits are diminishing.

Queueing delays often account for a large part of the response time at high percentiles. As a server can only process a small number of things in parallel

When generating load artificially in order to test the scalability of a system, the load generating client needs to keep sending requests independently of the response time. If the client waits for the previous request to complete before sending the next one, that behavior has the effect of artificially keeping the queues shorter in the test than they would be in reality, which skews the measurements

#### Approaches for Coping with Load

An architecture that is appropriate for one level of load is unlikely to cope with 10 times that load. If you are working on a fast-growing service, it is therefore likely that you will need to rethink your architecture on every order of magnitude load increase —or perhaps even more often than that.

People often talk of a dichotomy between scaling up (vertical scaling, moving to a more powerful machine) and scaling out (horizontal scaling, distributing the load across multiple smaller machines). Distributing load across multiple machines is also known as a shared-nothing architecture. A system that can run on a single machine is often simpler, but high-end machines can become very expensive, so very intensive workloads often can’t avoid scaling out. **==In reality, good architectures usually involve a pragmatic mixture of approaches: for example, using several fairly powerful machines can still be simpler and cheaper than a large number of small virtual machines.==**

While distributing stateless services across multiple machines is fairly straightforward, taking stateful data systems from a single node to a distributed setup can introduce a lot of additional complexity.

As the tools and abstractions for distributed systems get better, this common wisdom may change, at least for some kinds of applications. It is conceivable that distributed data systems will become the default in the future, even for use cases that don’t handle large volumes of data or traffic.

The architecture of systems that operate at large scale is usually highly specific to the application—there is no such thing as a generic, one-size-fits-all scalable architecture (informally known as magic scaling sauce). The problem may be the volume of reads, the volume of writes, the volume of data to store, the complexity of the data, the response time requirements, the access patterns, or (usually) some mixture of all of these plus many more issues.

### Maintainability

It is well known that the majority of the cost of software is not in its initial development, but in its ongoing maintenance—fixing bugs, keeping its systems operational, investigating failures, adapting it to new platforms, modifying it for new use cases, repaying technical debt, and adding new features. 
pay particular attention to three design principles for software systems:

- Operability
	Make it easy for operations teams to keep the system running smoothly.
- Simplicity
	Make it easy for new engineers to understand the system, by removing as much complexity as possible from the system. (Note this is not the same as simplicity of the user interface.)
- Evolvability
	Make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change. Also known as extensibility, modifiability, or plasticity.


#### Operability: Making Life Easy for Operations

good operations can often work around the limitations of bad (or incomplete) software, but good software cannot run reliably with bad operations

Operations teams are vital to keeping a software system running smoothly. A good operations team typically is responsible for the following, and more

• Monitoring the health of the system and quickly restoring service if it goes into a bad state
• Tracking down the cause of problems, such as system failures or degraded performance
• Keeping software and platforms up to date, including security patches
• Keeping tabs on how different systems affect each other, so that a problematic change can be avoided before it causes damage
• Anticipating future problems and solving them before they occur (e.g., capacity planning)
• Establishing good practices and tools for deployment, configuration management, and more
• Performing complex maintenance tasks, such as moving an application from one platform to another
• Maintaining the security of the system as configuration changes are made
• Defining processes that make operations predictable and help keep the production environment stable
• Preserving the organization’s knowledge about the system, even as individual people come and go

**==Good operability means making routine tasks easy, allowing the operations team to focus their efforts on high-value activities.==**

• Providing visibility into the runtime behavior and internals of the system, with good monitoring
• Providing good support for automation and integration with standard tools
• Avoiding dependency on individual machines
• Providing good documentation and an easy-to-understand operational model
• Providing good default behavior, but also giving administrators the freedom to override defaults when needed
• Self-healing where appropriate, but also giving administrators manual control over the system state when needed
• Exhibiting predictable behavior, minimizing surprises

#### Simplicity: Managing Complexity

There are various possible symptoms of complexity: explosion of the state space, tight coupling of modules, tangled dependencies, inconsistent naming and terminology, hacks aimed at solving performance problems, special-casing to work around issues elsewhere, and many more.

When complexity makes maintenance hard, budgets and schedules are often overrun. In complex software, there is also a greater risk of introducing bugs when making a change: when the system is harder for developers to understand and reason about, hidden assumptions, unintended consequences, and unexpected interactions are more easily overlooked.

Making a system simpler does not necessarily mean reducing its functionality; it can also mean removing accidental complexity

One of the best tools we have for removing accidental complexity is abstraction. A good abstraction can hide a great deal of implementation detail behind a clean, simple-to-understand façade. A good abstraction can also be used for a wide range of different applications. Not only is this reuse more efficient than reimplementing a similar thing multiple times, but it also leads to higher-quality software, as quality improvements in the abstracted component benefit all applications that use it.

However, finding good abstractions is very hard. In the field of distributed systems,
although there are many good algorithms, it is much less clear how we should be
packaging them into abstractions that help us keep the complexity of the system at a
manageable level.

#### Evolvability: Making Change Easy

It’s extremely unlikely that your system’s requirements will remain unchanged forever. They are much more likely to be in constant flux

In terms of organizational processes, Agile working patterns provide a framework for adapting to change. The Agile community has also developed technical tools and patterns that are helpful when developing software in a frequently changing environment, such as test-driven development (TDD) and refactoring.

### Summary

An application has to meet various requirements in order to be useful

Reliability means making systems work correctly, even when faults occur. Faults can be in hardware (typically random and uncorrelated), software (bugs are typically systematic and hard to deal with), and humans (who inevitably make mistakes from time to time). Fault-tolerance techniques can hide certain types of faults from the end user.

Scalability means having strategies for keeping performance good, even when load increases. In order to discuss scalability, we first need ways of describing load and performance quantitatively. We briefly looked at Twitter’s home timelines as an example of describing load, and response time percentiles as a way of measuring performance. In a scalable system, you can add processing capacity in order to remain reliable under high load.

Maintainability has many facets, but in essence it’s about making life better for the engineering and operations teams who need to work with the system. Good abstractions can help reduce complexity and make the system easier to modify and adapt for new use cases. Good operability means having good visibility into the system’s health, and having effective ways of managing it.

## CHAPTER 2 Data Models and Query Languages

Data models are perhaps the most important part of developing software, because they have such a profound effect: not only on how the software is written, but also on how we think about the problem that we are solving.

1. As an application developer, you look at the real world (in which there are people, organizations, goods, actions, money flows, sensors, etc.) and model it in terms of objects or data structures, and APIs that manipulate those data structures.
2. When you want to store those data structures, you express them in terms of a general-purpose data model, such as JSON or XML documents, tables in a relational database, or a graph model.
3. The engineers who built your database software decided on a way of representing that JSON/XML/relational/graph data in terms of bytes in memory, on disk, or on a network.
4. On yet lower levels, hardware engineers have figured out how to represent bytes in terms of electrical currents, pulses of light, magnetic fields, and more.

the basic idea is still the same: each layer hides the complexity of the layers below it by providing a clean data model.

It can take a lot of effort to master just one data model (think how many books there are on relational data modeling). Building software is hard enough, even when working with just one data model and without worrying about its inner workings. But since the data model has such a profound effect on what the software above it can and can’t do, it’s important to choose one that is appropriate to the application.

### Relational Model Versus Document Model

The goal of the relational model was to hide that implementation detail behind a cleaner interface.
relational databases turned out to generalize very well, beyond their original scope of business data processing, to a broad variety of use cases

#### The Birth of NoSQL

There are several driving forces behind the adoption of NoSQL databases, including:
• A need for greater scalability than relational databases can easily achieve, including very large datasets or very high write throughput
• A widespread preference for free and open source software over commercial database products
• Specialized query operations that are not well supported by the relational model
• Frustration with the restrictiveness of relational schemas, and a desire for a more dynamic and expressive data model 

#### The Object-Relational Mismatch

if data is stored in relational tables, an awkward translation layer is required between the objects in the application code and the database model of tables, rows, and columns. The disconnect between the models is sometimes called an impedance mismatch.

![[Pasted image 20251010151013.png]]

• In the traditional SQL model (prior to SQL:1999), the most common normalized representation is to put positions, education, and contact information in separate tables, with a foreign key reference to the users table,

• Later versions of the SQL standard added support for structured datatypes and XML data; this allowed multi-valued data to be stored within a single row, with support for querying and indexing inside those documents

• A third option is to encode jobs, education, and contact info as a JSON or XML document, store it on a text column in the database, and let the application interpret its structure and content. In this setup, you typically cannot use the database to query for values inside that encoded column.

```json
{
  "user_id": 251,
  "first_name": "Bill",
  "last_name": "Gates",
  "summary": "Co-chair of the Bill & Melinda Gates... Active blogger.",
  "region_id": "us:91",
  "industry_id": 131,
  "photo_url": "/p/7/000/253/05b/308dd6e.jpg",
  "positions": [
    {
      "job_title": "Co-chair",
      "organization": "Bill & Melinda Gates Foundation"
    },
    {
      "job_title": "Co-founder, Chairman",
      "organization": "Microsoft"
    }
  ],
  "education": [
    {
      "school_name": "Harvard University",
      "start": 1973,
      "end": 1975
    },
    {
      "school_name": "Lakeside School, Seattle",
      "start": null,
      "end": null
    }
  ],
  "contact_info": {
    "blog": "http://thegatesnotes.com",
    "twitter": "http://twitter.com/BillGates"
  }
}
```

Some developers feel that the JSON model reduces the impedance mismatch between the application code and the storage layer. there are also problems with JSON as a data encoding format. The lack of a schema is often cited as an advantage

The JSON representation has better locality than the multi-table schema in Figure 2-1. If you want to fetch a profile in the relational example, you need to either perform multiple queries (query each table by ``user_id``) or perform a messy multiway join between the users table and its subordinate tables. In the JSON representation, all the relevant information is in one place, and one query is sufficient.

The one-to-many relationships from the user profile to the user’s positions, educational history, and contact information imply a tree structure in the data, and the JSON representation makes this tree structure explicit

![[Pasted image 20251010151311.png]]

#### Many-to-One and Many-to-Many Relationships

Whether you store an ID or a text string is a question of duplication. When you use an ID, the information that is meaningful to humans is stored in only one place, and everything that refers to it uses an ID (which only has meaning within the database). When you store the text directly, you are duplicating the human-meaningful information in every record that uses it.

**==The advantage of using an ID is that because it has no meaning to humans, it never needs to change: the ID can remain the same, even if the information it identifies changes. Anything that is meaningful to humans may need to change sometime in the future—and if that information is duplicated, all the redundant copies need to be updated.==** That incurs write overheads, and risks inconsistencies Removing such duplication is the key idea behind normalization in databases

Unfortunately, normalizing this data requires many-to-one relationships which don’t fit nicely into the document model. In relational databases, it’s normal to refer to rows in other tables by ID, because joins are easy. In document databases, joins are not needed for one-to-many tree structures, and support for joins is often weak

If the database itself does not support joins, you have to emulate a join in application code by making multiple queries to the database. 

Moreover, even if the initial version of an application fits well in a join-free document model, data has a tendency of becoming more interconnected as features are added to applications.

**Organizations and schools as entities**

Instead of storing `organization` and `school_name` as plain strings, make them references to separate entities. This allows:

- Each organization/school to have its own page with logo, news feed, etc.
- Résumés can link to these entities and display their information
- Logos and details automatically stay up-to-date

**Recommendations**

New feature where users can write recommendations for each other:

- Recommendation appears on the recommended user's résumé
- Shows recommender's name and photo
- If recommender updates their photo, it automatically updates in all their recommendations
- Solution: Store a reference to the author's profile rather than copying their data

![[Pasted image 20251010152003.png]]

*Figure 2-4. Extending résumés with many-to-many relationships.*


#### Are Document Databases Repeating History?

The debate around many-to-many relationships and joins in document databases isn't new—it dates back to the earliest computerized database systems. In the 1970s, IBM's Information Management System (IMS), developed for the Apollo space program, used a hierarchical model that closely resembles today's JSON structure in document databases. Like modern document databases, IMS handled one-to-many relationships well but struggled with many-to-many relationships and didn't support joins. Developers faced the same choices we see today: either duplicate data or manually resolve references between records.

**The network model**

The network model, standardized by CODASYL, attempted to solve the hierarchical model's limitations by allowing records to have multiple parents instead of just one. This enabled many-to-one and many-to-many relationships. Records were linked using pointers similar to those in programming languages. However, accessing data required following an "access path"—traversing chains of links from a root record. In a many-to-many world, multiple paths could lead to the same record, forcing programmers to mentally track all these different routes. Querying meant moving a cursor through the database, iterating over record lists and following access paths. While this approach efficiently used 1970s hardware limitations, it made querying and updating code extremely complicated and inflexible. If you needed data but didn't have a path to it, you had to restructure access paths and rewrite significant amounts of handwritten database code, making changes to the data model very difficult.

**The relational model**

What the relational model did, by contrast, was to lay out all the data in the open: a relation (table) is simply a collection of tuples (rows), and that’s it. There are no labyrinthine nested structures, no complicated access paths to follow if you want to look at the data. You can read any or all of the rows in a table, selecting those that match an arbitrary condition.

In a relational database, the query optimizer automatically decides which parts of the query to execute in which order, and which indexes to use. Those choices are effectively the “access path,” but the big difference is that they are made automatically by the query optimizer, not by the application developer, so we rarely need to think about them.

But a key insight of the relational model was this: you only need to build a query optimizer once, and then all applications that use the database can benefit from it. If you don’t have a query optimizer, it’s easier to hand code the access paths for a particular query than to write a general-purpose optimizer—but the general-purpose solution wins in the long run.

**Comparison to document databases**

when it comes to representing many-to-one and many-to-many relationships, relational and document databases are not fundamentally different: in both cases, the related item is referenced by a unique identifier, which is called a foreign key in the relational model and a document reference in the document model. That identifier is resolved at read time by using a join or follow-up queries

#### Relational Versus Document Databases Today

**==The main arguments in favor of the document data model are schema flexibility, better performance due to locality, and that for some applications it is closer to the data structures used by the application. The relational model counters by providing better support for joins, and many-to-one and many-to-many relationships.==**

**Which data model leads to simpler application code?**

If the data in your application has a document-like structure (i.e., a tree of one-to-many relationships, where typically the entire tree is loaded at once), then it’s probably a good idea to use a document model. The relational technique of shredding— splitting a document-like structure into multiple tables can lead to cumbersome schemas and unnecessarily complicated application code.

The document model has limitations: for example, you cannot refer directly to a nested item within a document, but instead you need to say something like “the second item in the list of positions for user 251” (much like an access path in the hierarchical model). However, as long as documents are not too deeply nested, that is not usually a problem.

The poor support for joins in document databases may or may not be a problem, depending on the application.

However, if your application does use many-to-many relationships, the document model becomes less appealing. It’s possible to reduce the need for joins by denormalizing, but then the application code needs to do additional work to keep the denormalized data consistent. Joins can be emulated in application code by making multiple requests to the database, but that also moves complexity into the application and is usually slower than a join performed by specialized code inside the database. In such cases, using a document model can lead to significantly more complex application code and worse performance

**Schema flexibility in the document model**

Most document databases, and the JSON support in relational databases, do not enforce any schema on the data in documents. XML support in relational databases usually comes with optional schema validation. **==No schema means that arbitrary keys and values can be added to a document, and when reading, clients have no guarantees as to what fields the documents may contain.==**

there is an implicit schema, but it is not enforced by the database [20]. A more accurate term is schema-on-read (the structure of the data is implicit, and only interpreted when the data is read), in contrast with schema-on-write (the traditional approach of relational databases, where the schema is explicit and the database ensures all written data conforms to it)

**==Schema-on-read is similar to dynamic (runtime) type checking in programming languages, whereas schema-on-write is similar to static (compile-time) type checking. Just as the advocates of static and dynamic type checking have big debates about their relative merits [22], enforcement of schemas in database is a contentious topic, and in general there’s no right or wrong answer.==**

The difference between the approaches is particularly noticeable in situations where an application wants to change the format of its data. For example, say you are currently storing each user’s full name in one field, and you instead want to store the first name and last name separately [23]. In a document database, you would just start writing new documents with the new fields and have code in the application that handles the case when old documents are read.

```java
if (user && user.name && !user.first_name) {
	// Documents written before Dec 8, 2013 don't have first_name
	user.first_name = user.name.split(" ")[0];
}
```

On the other hand, in a “statically typed” database schema, you would typically perform a migration along the lines of:

```sql
ALTER TABLE users ADD COLUMN first_name text;
UPDATE users SET first_name = split_part(name, ' ', 1); -- PostgreSQL
UPDATE users SET first_name = substring_index(name, ' ', 1); -- MySQL
```

Running the UPDATE statement on a large table is likely to be slow on any database, since every row needs to be rewritten. If that is not acceptable, the application can leave `first_name` set to its default of `NULL` and fill it in at read time, like it would with a document database.

The schema-on-read approach is advantageous if the items in the collection don’t all have the same structure for some reason (i.e., the data is heterogeneous)—for example, because:  
• There are many different types of objects, and it is not practical to put each type of object in its own table.  
• The structure of the data is determined by external systems over which you have no control and which may change at any time.

**Data locality for queries**

A document is usually stored as a single continuous string, encoded as JSON, XML, or a binary variant thereof (such as MongoDB’s BSON). If your application often needs to access the entire document (for example, to render it on a web page), there is a performance advantage to this storage locality. If data is split across multiple tables, like in Figure 2-1, multiple index lookups are required to retrieve it all, which may require more disk seeks and take more time.

**==The locality advantage only applies if you need large parts of the document at the same time. The database typically needs to load the entire document, even if you access only a small portion of it, which can be wasteful on large documents==**. On updates to a document, the entire document usually needs to be rewritten—only modifications that don’t change the encoded size of a document can easily be performed in place [19]. For these reasons, it is generally recommended that you keep documents fairly small and avoid writes that increase the size of a document

It’s worth pointing out that the idea of grouping related data together for locality is not limited to the document model.

**Convergence of document and relational databases**

It seems that relational and document databases are becoming more similar over time, and that is a good thing: the data models complement each other. If a database is able to handle document-like data and also perform relational queries on it, applications can use the combination of features that best fits their needs.
A hybrid of the relational and document models is a good route for databases to take in the future.

### Query Languages for Data

SQL is a declarative query language, whereas IMS and CODASYL queried the database using imperative code. What does that mean?  
Many commonly used programming languages are imperative.

```javascript
function getSharks() {
    var sharks = [];
    for (var i = 0; i < animals.length; i++) {
        if (animals[i].family === "Sharks") {
            sharks.push(animals[i]);
        }
    }
    return sharks;
}
```

When SQL was defined, it followed the structure of the relational algebra fairly closely

```sql
SELECT * FROM animals WHERE family = 'Sharks';
```

**==An imperative language tells the computer to perform certain operations in a certain order.**==

==**In a declarative query language, like SQL or relational algebra, you just specify the pattern of the data you want—what conditions the results must meet, and how you want the data to be transformed (e.g., sorted, grouped, and aggregated)—but not how to achieve that goal.==** It is up to the database system’s query optimizer to decide which
indexes and which join methods to use, and in which order to execute various parts of the query.

Finally, declarative languages often lend themselves to parallel execution. Today, CPUs are getting faster by adding more cores, not by running at significantly higher clock speeds than before [31]. Imperative code is very hard to parallelize across multiple cores and multiple machines, because it specifies instructions that must be performed in a particular order. Declarative languages have a better chance of getting faster in parallel execution because they specify only the pattern of the results, not the algorithm that is used to determine the results.

#### Declarative Queries on the Web

The advantages of declarative query languages are not limited to just databases

```html
<ul>
    <li class="selected">
        <p>Sharks</p>
        <ul>
            <li>Great White Shark</li>
            <li>Tiger Shark</li>
            <li>Hammerhead Shark</li>
        </ul>
    </li>
    <li>
        <p>Whales</p>
        <ul>
            <li>Blue Whale</li>
            <li>Humpback Whale</li>
            <li>Fin Whale</li>
        </ul>
    </li>
</ul>
```

Imagine what life would be like if you had to use an imperative approach. In Java‐ Script, using the core Document Object Model (DOM) API

```js
var liElements = document.getElementsByTagName("li");

for (var i = 0; i < liElements.length; i++) {
    if (liElements[i].className === "selected") {
        var children = liElements[i].childNodes;
        for (var j = 0; j < children.length; j++) {
            var child = children[j];
            if (child.nodeType === Node.ELEMENT_NODE && child.tagName === "P") {
                child.setAttribute("style", "background-color: blue");
            }
        }
    }
}
```

This JavaScript imperatively sets the element `<p>Sharks</p>` to have a blue background, but the code is awful. Not only is it much longer and harder to understand than the CSS and XSL equivalents, but it also has some serious problems:

• If the `selected` class is removed (e.g., because the user clicks a different page), the blue color won’t be removed, even if the code is rerun—and so the item will remain highlighted until the entire page is reloaded. With CSS, the browser automatically detects when the `li.selected > p` rule no longer applies and removes the blue background as soon as the `selected` class is removed.  
• If you want to take advantage of a new API, such as `document.getElementsByClassName("selected")` or even `document.evaluate()`—which may improve performance—you have to rewrite the code. On the other hand, browser vendors can improve the performance of CSS and XPath without breaking compatibility.

#### MapReduce Querying

MapReduce is a programming model for processing large amounts of data in bulk across many machines, popularized by Google [33]. A limited form of MapReduce is supported by some NoSQL datastores, including MongoDB and CouchDB, as a mechanism for performing read-only queries across many documents.

MapReduce is neither a declarative query language nor a fully imperative query API, but somewhere in between: **==the logic of the query is expressed with snippets of code, which are called repeatedly by the processing framework. It is based on the map (also known as collect) and reduce (also known as fold or inject) functions that exist in many functional programming languages.==**


```sql
SELECT date_trunc('month', observation_timestamp) AS observation_month,
sum(num_animals) AS total_animals
FROM observations
WHERE family = 'Sharks'
GROUP BY observation_month;
```

The `date_trunc('month', timestamp)` function determines the calendar month containing `timestamp`, and returns another timestamp representing the beginning of that month. In other words, it rounds a timestamp down to the nearest month.

This query first filters the observations to only show species in the Sharks family, then groups the observations by the calendar month in which they occurred, and finally adds up the number of animals seen in all observations in that month. The same can be expressed with MongoDB’s MapReduce feature:

```javascript
db.observations.mapReduce(
    function map() {
        var year = this.observationTimestamp.getFullYear();
        var month = this.observationTimestamp.getMonth() + 1;
        emit(year + "-" + month, this.numAnimals);
    },
    function reduce(key, values) {
        return Array.sum(values);
    },
    {
        query: { family: "Sharks" },
        out: "monthlySharkReport"
    }
);
```

The filter to consider only shark species can be specified declaratively (this is a MongoDB-specific extension to MapReduce).  
The JavaScript function `map` is called once for every document that matches `query`, with `this` set to the document object.  
The `map` function emits a key (a string consisting of year and month, such as `"2013-12"` or `"2014-1"`) and a value (the number of animals in that observation).  
The key-value pairs emitted by `map` are grouped by key. For all key-value pairs with the same key (i.e., the same month and year), the `reduce` function is called once.  
The `reduce` function adds up the number of animals from all observations in a particular month.  
The final output is written to the collection `monthlySharkReport`.

The map and reduce functions are somewhat restricted in what they are allowed to do. They must be pure functions, which means they only use the data that is passed to them as input, they cannot perform additional database queries, and they must not have any side effects. These restrictions allow the database to run the functions anywhere, in any order, and rerun them on failure. However, they are nevertheless powerful: they can parse strings, call library functions, perform calculations, and more.

### Graph-Like Data Models

Many-to-many relationships are an important distinguishing feature between different data models. If your application has mostly one-to-many relationships (tree-structured data) or no relationships between records, the document model is appropriate.

But what if many-to-many relationships are very common in your data? The relational model can handle simple cases of many-to-many relationships, but as the connections within your data become more complex, it becomes more natural to start modeling your data as a graph.

A graph consists of two kinds of objects: **vertices** (also known as nodes or entities) and **edges** (also known as relationships or arcs). Many kinds of data can be modeled as a graph.

Social graphs
	Vertices are people, and edges indicate which people know each other.
The web graph
	Vertices are web pages, and edges indicate HTML links to other pages.
Road or rail networks
	Vertices are junctions, and edges represent the roads or railway lines between them.

Well-known algorithms can operate on these graphs: for example, car navigation systems search for the shortest path between two points in a road network, and PageRank can be used on the web graph to determine the popularity of a web page and thus its ranking in search results.

**==graphs are not limited to such homogeneous data: an equally powerful use of graphs is to provide a consistent way of storing completely different types of objects in a single datastore==**. For example, Facebook maintains a single graph with many different types of vertices and edges: vertices represent people, locations, events, checkins, and comments made by users; edges indicate which people are friends with each other, which checkin happened in which location, who commented on which post, who attended which event, and so on

![[Pasted image 20251010164051.png]]

There are several different, but related, ways of structuring and querying data in graphs.

#### Property Graphs

In the property graph model, each vertex consists of:  
• A unique identifier  
• A set of outgoing edges  
• A set of incoming edges  
• A collection of properties (key-value pairs)

Each edge consists of:  
• A unique identifier  
• The vertex at which the edge starts (the tail vertex)  
• The vertex at which the edge ends (the head vertex)  
• A label to describe the kind of relationship between the two vertices  
• A collection of properties (key-value pairs)

You can think of a graph store as consisting of two relational tables, one for vertices and one for edges.

```sql
CREATE TABLE vertices (
	vertex_id integer PRIMARY KEY,
	properties json
);
CREATE TABLE edges (
	edge_id integer PRIMARY KEY,
	tail_vertex integer REFERENCES vertices (vertex_id),
	head_vertex integer REFERENCES vertices (vertex_id),
	label text,
	properties json
);
CREATE INDEX edges_tails ON edges (tail_vertex);
CREATE INDEX edges_heads ON edges (head_vertex);
```

1. Any vertex can have an edge connecting it with any other vertex. There is no schema that restricts which kinds of things can or cannot be associated.
    
2. Given any vertex, you can efficiently find both its incoming and its outgoing edges, and thus traverse the graph—i.e., follow a path through a chain of vertices—both forward and backward.
    
3. By using different labels for different kinds of relationships, you can store several different kinds of information in a single graph, while still maintaining a clean data model.

Those features give graphs a great deal of flexibility for data modeling

#### The Cypher Query Language

Cypher is a declarative query language for property graphs, created for the Neo4j graph database

the Cypher query to insert the left-hand portion of Figure 2-5 into a graph database. The rest of the graph can be added similarly and is omitted for readability. Each vertex is given a symbolic name like USA or Idaho, and other parts of the query can use those names to create edges between the vertices, using an arrow notation:

```cypher
CREATE
    (NAmerica:Location {name: 'North America', type: 'continent'}),
    (USA:Location {name: 'United States', type: 'country'}),
    (Idaho:Location {name: 'Idaho', type: 'state'}),
    (Lucy:Person {name: 'Lucy'}),
    (Idaho)-[:WITHIN]->(USA)-[:WITHIN]->(NAmerica),
    (Lucy)-[:BORN_IN]->(Idaho);
```

When all the vertices and edges of Figure 2-5 are added to the database, we can start asking interesting questions: for example, find the names of all the people who emigrated from the United States to Europe. To be more precise, here we want to find all the vertices that have a BORN_IN edge to a location within the US, and also a LIVING_IN edge to a location within Europe, and return the name property of each of those vertices.

```cypher
MATCH
    (person)-[:BORN_IN]->()-[:WITHIN*0..]->(us:Location {name: 'United States'}),
    (person)-[:LIVES_IN]->()-[:WITHIN*0..]->(eu:Location {name: 'Europe'})
RETURN person.name;
```

The query can be read as follows:

Find any vertex (call it `person`) that meets both of the following conditions:

1. `person` has an outgoing `BORN_IN` edge to some vertex. From that vertex, you can follow a chain of outgoing `WITHIN` edges until eventually you reach a vertex of type `Location`, whose `name` property is equal to `"United States"`.
    
2. That same `person` vertex also has an outgoing `LIVES_IN` edge. Following that edge, and then a chain of outgoing `WITHIN` edges, you eventually reach a vertex of type `Location`, whose `name` property is equal to `"Europe"`.

As is typical for a declarative query language, you don’t need to specify such execution details when writing the query: the query optimizer automatically chooses the strategy that is predicted to be the most efficient, so you can get on with writing the rest of your application

#### Graph Queries in SQL

In a relational database, you usually know in advance which joins you need in your query. In a graph query, you may need to traverse a variable number of edges before you find the vertex you’re looking for— that is, the number of joins is not fixed in advance.

```sql
WITH RECURSIVE
-- in_usa is the set of vertex IDs of all locations within the United States
in_usa(vertex_id) AS (
    SELECT vertex_id FROM vertices WHERE properties->>'name' = 'United States'
    UNION
    SELECT edges.tail_vertex
    FROM edges
    JOIN in_usa ON edges.head_vertex = in_usa.vertex_id
    WHERE edges.label = 'within'
),
-- in_europe is the set of vertex IDs of all locations within Europe
in_europe(vertex_id) AS (
    SELECT vertex_id FROM vertices WHERE properties->>'name' = 'Europe'
    UNION
    SELECT edges.tail_vertex
    FROM edges
    JOIN in_europe ON edges.head_vertex = in_europe.vertex_id
    WHERE edges.label = 'within'
),
-- born_in_usa is the set of vertex IDs of all people born in the US
born_in_usa(vertex_id) AS (
    SELECT edges.tail_vertex
    FROM edges
    JOIN in_usa ON edges.head_vertex = in_usa.vertex_id
    WHERE edges.label = 'born_in'
),
-- lives_in_europe is the set of vertex IDs of all people living in Europe
lives_in_europe(vertex_id) AS (
    SELECT edges.tail_vertex
    FROM edges
    JOIN in_europe ON edges.head_vertex = in_europe.vertex_id
    WHERE edges.label = 'lives_in'
)
SELECT vertices.properties->>'name'
FROM vertices
-- join to find those people who were both born in the US *and* live in Europe
JOIN born_in_usa ON vertices.vertex_id = born_in_usa.vertex_id
JOIN lives_in_europe ON vertices.vertex_id = lives_in_europe.vertex_id;
```

Explanation:

1. **in_usa**: Start with the vertex whose `name` property is `"United States"`, then recursively follow all incoming `within` edges to include all locations within the United States.
    
2. **in_europe**: Similarly, start with `"Europe"` and recursively include all locations within Europe.
    
3. **born_in_usa**: For every vertex in `in_usa`, follow incoming `born_in` edges to find people born in the US.
    
4. **lives_in_europe**: For every vertex in `in_europe`, follow incoming `lives_in` edges to find people living in Europe.
    
5. **Final SELECT**: Intersect the two sets of people (born in the US and living in Europe) by joining them to find those who satisfy both conditions.

#### Triple-Stores and SPARQL

The triple-store model is mostly equivalent to the property graph model, using different words to describe the same ideas. It is nevertheless worth discussing, because there are various tools and languages for triple-stores that can be valuable additions to your toolbox for building applications.

In a triple-store, all information is stored in the form of very simple three-part statements: (subject, predicate, object).

The subject of a triple is equivalent to a vertex in a graph. The object is one of two
things:
1. A value in a primitive datatype, such as a string or a number. In that case, the predicate and object of the triple are equivalent to the key and value of a property on the subject vertex
2. 2. Another vertex in the graph. In that case, the predicate is an edge in the graph, the subject is the tail vertex, and the object is the head vertex.

It’s quite repetitive to repeat the same subject over and over again, but fortunately you can use semicolons to say multiple things about the same subject

**The semantic web**

The semantic web is fundamentally a simple and reasonable idea: websites already publish information as text and pictures for humans to read, so why don’t they also publish information as machine-readable data for computers to read? The Resource Description Framework (RDF) [41] was intended as a mechanism for different websites to publish data in a consistent format, allowing data from different websites to be automatically combined into a web of data—a kind of internet-wide “database of everything.”

Unfortunately, the semantic web was overhyped in the early 2000s but so far hasn’t shown any sign of being realized in practice, which has made many people cynical about it. It has also suffered from a dizzying plethora of acronyms, overly complex standards proposals, and hubris.

### Summary

Historically, data started out being represented as one big tree (the hierarchical model), but that wasn’t good for representing many-to-many relationships, so the relational model was invented to solve that problem. More recently, developers found that some applications don’t fit well in the relational model either. New nonrelational “NoSQL” datastores have diverged in two main directions:

1. **Document databases** target use cases where data comes in self-contained documents and relationships between one document and another are rare.
    
2. **Graph databases** go in the opposite direction, targeting use cases where anything is potentially related to everything.
    

All three models (document, relational, and graph) are widely used today, and each is good in its respective domain.

One thing that document and graph databases have in common is that they typically don’t enforce a schema for the data they store, which can make it easier to adapt applications to changing requirements. However, your application most likely still assumes that data has a certain structure; it’s just a question of whether the schema is explicit.

## CHAPTER 3 Storage and Retrieval

On the most fundamental level, a database needs to do two things: when you give it some data, it should store the data, and when you ask it again later, it should give the data back to you.

In order to tune a storage engine to perform well on your kind of workload, you need to have a rough idea of what the storage engine is doing under the hood.

In particular, there is a big difference between storage engines that are optimized for transactional workloads and those that are optimized for analytics

### Data Structures That Power Your Database

```bash
#!/bin/bash
db_set () {
	echo "$1,$2" >> database
}
db_get () {
	grep "^$1," database | sed -e "s/^$1,//" | tail -n 1
}
```

These two functions implement a key-value store. You can call ``db_set`` key value, which will store key and value in the database. The key and value can be (almost) anything you like

```bash
$ db_set 123456 '{"name":"London","attractions":["Big Ben","London Eye"]}'
$ db_set 42 '{"name":"San Francisco","attractions":["Golden Gate Bridge"]}'
$ db_get 42 {"name":"San Francisco","attractions":["Golden Gate Bridge"]}
```

The underlying storage format is very simple: a text file where each line contains a key-value pair, separated by a comma (roughly like a CSV file, ignoring escaping issues). Every call to ``db_set`` appends to the end of the file, so if you update a key several times, the old versions of the value are not overwritten—you need to look at the last occurrence of a key in a file to find the latest value

```bash
$ db_set 42 '{"name":"San Francisco","attractions":["Exploratorium"]}'
$ db_get 42 {"name":"San Francisco","attractions":["Exploratorium"]}
$ cat database 123456,{"name":"London","attractions":["Big Ben","London Eye"]}
42,{"name":"San Francisco","attractions":["Golden Gate Bridge"]}
42,{"name":"San Francisco","attractions":["Exploratorium"]}
```

Similarly to what ``db_set`` does, many databases internally use a log, which is an append-only data file. Real databases have more issues to deal with (such as concurrency control, reclaiming disk space so that the log doesn’t grow forever, and handling errors and partially written records), but the basic principle is the same.

On the other hand, our ``db_get`` function has terrible performance if you have a large number of records in your database. Every time you want to look up a key, ``db_get`` has to scan the entire database file from beginning to end, looking for occurrences of the key. In algorithmic terms, the cost of a lookup is O(n): if you double the number of records n in your database, a lookup takes twice as long. That’s not good

In order to efficiently find the value for a particular key in the database, we need a different data structure: an index. the general idea behind them is to keep some additional metadata on the side, which acts as a signpost and helps you to locate the data you want. If you want to search the same data in several different ways, you may need several different indexes on different parts of the data.

**==An index is an additional structure that is derived from the primary data. Many databases allow you to add and remove indexes, and this doesn’t affect the contents of the database; it only affects the performance of queries. Maintaining additional structures incurs overhead, especially on writes. For writes, it’s hard to beat the performance of simply appending to a file, because that’s the simplest possible write operation. Any kind of index usually slows down writes, because the index also needs to be updated every time data is written.==**

This is an important trade-off in storage systems: well-chosen indexes speed up read queries, but every index slows down writes. For this reason, databases don’t usually index everything by default, but require you—the application developer or database administrator—to choose indexes manually, using your knowledge of the application’s typical query patterns

#### Hash Indexes

Key-value stores are quite similar to the dictionary type that you can find in most programming languages, and which is usually implemented as a hash map

Let’s say our data storage consists only of appending to a file, as in the preceding example. Then the simplest possible indexing strategy is this: keep an in-memory hash map where every key is mapped to a byte offset in the data file—the location at which the value can be found, as illustrated in Figure 3-1. Whenever you append a new key-value pair to the file, you also update the hash map to reflect the offset of the data you just wrote (this works both for inserting new keys and for updating existing keys). When you want to look up a value, use the hash map to find the offset in the data file, seek to that location, and read the value

![[Pasted image 20251012170710.png]]

This may sound simplistic, but it is a viable approach. A storage engine like ``Bitcask`` is well suited to situations where the value for each key is updated frequently. In this kind of workload, there are a lot of writes, but there are not too many distinct keys—you have a large number of writes per key, but it’s feasible to keep all keys in memory.

![[Pasted image 20251012170754.png]]

Moreover, since compaction often makes segments much smaller (assuming that a key is overwritten several times on average within one segment), we can also merge several segments together at the same time as performing the compaction, as shown in Figure 3-3. Segments are never modified after they have been written, so the merged segment is written to a new file. The merging and compaction of frozen segments can be done in a background thread, and while it is going on, we can still continue to serve read and write requests as normal, using the old segment files. After the merging process is complete, we switch read requests to using the new merged segment instead of the old segments—and then the old segment files can simply be deleted.

![[Pasted image 20251012170818.png]]

Each segment now has its own in-memory hash table, mapping keys to file offsets. In order to find the value for a key, we first check the most recent segment’s hash map; if the key is not present we check the second-most-recent segment, and so on. The merging process keeps the number of segments small, so lookups don’t need to check many hash maps.

Briefly, some of the issues that are important in a real implementation are:

- **File format**  
  - CSV is not ideal for logs.  
  - Binary format is faster and simpler: first encode the string length in bytes, then write the raw string (no escaping needed).

- **Deleting records**  
  - To delete a key-value pair, append a special **tombstone** record to the log.  
  - During log segment merging, the tombstone signals that older values for that key should be discarded.

- **Crash recovery**  
  - When the database restarts, in-memory hash maps are lost.  
  - They can be rebuilt by scanning each segment file from start to end and noting offsets of the latest key values.  
  - This can be slow for large files, so **``Bitcask``** stores a snapshot of each segment’s hash map on disk for faster recovery.

- **Partially written records**  
  - Crashes can occur mid-write.  
  - ``Bitcask`` detects and ignores corrupted parts using **checksums** embedded in log files.

- **Concurrency control**  
  - Writes are strictly sequential — typically handled by a single writer thread.  
  - Log segments are append-only and immutable, enabling concurrent reads by multiple threads.


An append-only log seems wasteful at first glance: why don’t you update the file in place, overwriting the old value with the new value? But an append-only design turns out to be good for several reasons:

- Appending and segment merging are sequential write operations, which are generally much faster than random writes, especially on magnetic spinning-disk hard drives. To some extent sequential writes are also preferable on flash-based solid state drives (SSDs)
- Concurrency and crash recovery are much simpler if segment files are append only or immutable. For example, you don’t have to worry about the case where a crash happened while a value was being overwritten, leaving you with a file containing part of the old and part of the new value spliced together.
-  Merging old segments avoids the problem of data files getting fragmented over time.

- **Memory limitation of hash tables**  
  - The hash table must fit entirely in memory.  
  - If there are too many keys, the system cannot handle them efficiently.  
  - While an on-disk hash map is possible, it performs poorly due to:  
    - Heavy **random access I/O** requirements.  
    - **High cost of resizing** when full.  
    - **Complex handling of hash collisions**.

- **Inefficient range queries**  
  - Range queries (e.g., scanning keys from `kitty00000` to `kitty99999`) are inefficient.  
  - Each key must be looked up individually in the hash maps — sequential scanning is not supported.

#### SSTables and LSM-Trees

we require that the sequence of key-value pairs is sorted by key. At first glance, that requirement seems to break our ability to use sequential writes,

SSTables have several big advantages over log segments with hash indexes:
1. Merging segments is simple and efficient, even if the files are bigger than the available memory. The approach is like the one used in the merge-sort algorithm

What if the same key appears in several input segments? Remember that each segment contains all the values written to the database during some period of time. This means that all the values in one input segment must be more recent than all the values in the other segment (assuming that we always merge adjacent segments). When multiple segments contain the same key, we can keep the value from the most recent segment and discard the values in older segments.

2. In order to find a particular key in the file, you no longer need to keep an index of all the keys in memory. However, you do know the offsets for the keys handbag and handsome, and because of the sorting you know that handiwork must appear between those two. This means you can jump to the offset for handbag and scan from there until you find handiwork

You still need an in-memory index to tell you the offsets for some of the keys, but it can be sparse: one key for every few kilobytes of segment file is sufficient, because a few kilobytes can be scanned very quickly.

3. Since read requests need to scan over several key-value pairs in the requested range anyway, it is possible to group those records into a block and compress it before writing it to disk Each entry of the sparse in-memory index then points at the start of a compressed block. Besides saving disk space, compression also reduces the I/O bandwidth use.

**Constructing and maintaining SSTables**

Fine so far—but how do you get your data to be sorted by key in the first place? Our incoming writes can occur in any order. Maintaining a sorted structure on disk is possible but maintaining it in memory is much easier. There are plenty of well-known tree data structures that you can use, such as red-black trees or AVL trees

- **Handling writes**  
  - Incoming writes are added to an in-memory balanced tree structure (e.g., a **red-black tree**).  
  - This structure is known as a **memtable**.

- **Flushing to disk**  
  - When the memtable exceeds a certain size threshold (typically a few MB), it is written to disk as an **SSTable** (Sorted String Table).  
  - The memtable’s sorted nature allows efficient SSTable creation.  
  - The new SSTable becomes the **most recent segment** of the database.  
  - During this process, new writes go to a **fresh memtable**.

- **Handling reads**  
  - To serve a read request:
    1. Check the **memtable** (in-memory).  
    2. If not found, check the **most recent SSTable** on disk.  
    3. Continue searching in **older SSTables** if necessary.

- **Merging and compaction**  
  - Periodically, a **background process** merges and compacts SSTables.  
  - This removes **overwritten** or **deleted** values and reduces storage fragmentation.

This scheme works very well. It only suffers from one problem: if the database crashes, the most recent writes (which are in the memtable but not yet written out to disk) are lost. In order to avoid that problem, we can keep a separate log on disk to which every write is immediately appended, just like in the previous section

#### B-Trees

The most widely used indexing structure is quite different: the B-tree. B-trees keep key-value pairs sorted by key, which allows efficient key-value lookups and range queries. But that’s where the similarity ends: B-trees have a very different design philosophy

The log-structured indexes we saw earlier break the database down into variable-size segments, typically several megabytes or more in size, and always write a segment sequentially. **==By contrast, B-trees break the database down into fixed-size blocks or pages, traditionally 4 KB in size (sometimes bigger), and read or write one page at a time==**. This design corresponds more closely to the underlying hardware, as disks are also arranged in fixed-size blocks.

Each page can be identified using an address or location, which allows one page to refer to another—similar to a pointer, but on disk instead of in memory

![[Pasted image 20251012172405.png]]

One page is designated as the root of the B-tree; whenever you want to look up a key in the index, you start here. The page contains several keys and references to child pages. Each child is responsible for a continuous range of keys, and the keys between the references indicate where the boundaries between those ranges lie.

The number of references to child pages in one page of the B-tree is called the branching factor. In practice,
the branching factor depends on the amount of space required to store the page references and the range boundaries, but typically it is several hundred.

If you want to update the value for an existing key in a B-tree, you search for the leaf page containing that key, change the value in that page, and write the page back to disk If you want to add a new key, you need to find the page whose range encompasses the new key and add it to that page. If there isn’t enough free space in the page to accommodate the new key, it is split into two half-full pages, and the parent page is updated to account for the new subdivision of key ranges

![[Pasted image 20251012172712.png]]

This algorithm ensures that the tree remains balanced: a B-tree with n keys always has a depth of O(log n). Most databases can fit into a B-tree that is three or four levels deep, so you don’t need to follow many page references to find the page you are looking for.

**Making B-trees reliable**

The basic underlying write operation of a B-tree is to overwrite a page on disk with new data. It is assumed that the overwrite does not change the location of the page; i.e., all references to that page remain intact when the page is overwritten. This is in stark contrast to log-structured indexes such as LSM-trees, which only append to files (and eventually delete obsolete files) but never modify files in place

You can think of overwriting a page on disk as an actual hardware operation. On a magnetic hard drive, this means moving the disk head to the right place, waiting for the right position on the spinning platter to come around, and then overwriting the appropriate sector with new data.

Moreover, some operations require several different pages to be overwritten

**==In order to make the database resilient to crashes, it is common for B-tree implementations to include an additional data structure on disk: a write-ahead log (WAL, also known as a redo log). This is an append-only file to which every B-tree modification must be written before it can be applied to the pages of the tree itself. When the database comes back up after a crash, this log is used to restore the B-tree back to a consistent state==**

An additional complication of updating pages in place is that careful concurrency control is required if multiple threads are going to access the B-tree at the same time —otherwise a thread may see the tree in an inconsistent state. This is typically done by protecting the tree’s data structures with latches (lightweight locks). Log structured approaches are simpler in this regard, because they do all the merging in the background without interfering with incoming queries and atomically swap old segments for new segments from time to time.

**B-tree optimizations**

• Instead of overwriting pages and maintaining a WAL for crash recovery, some databases (like LMDB) use a copy-on-write scheme [21]. A modified page is written to a different location, and a new version of the parent pages in the tree is created, pointing at the new location. This approach is also useful for concur‐ rency control   
• We can save space in pages by not storing the entire key, but abbreviating it. Especially in pages on the interior of the tree, keys only need to provide enough information to act as boundaries between key ranges. Packing more keys into a page allows the tree to have a higher branching factor, and thus fewer levels.iii  
• In general, pages can be positioned anywhere on disk; there is nothing requiring pages with nearby key ranges to be nearby on disk. If a query needs to scan over a large part of the key range in sorted order, that page-by-page layout can be inefficient, because a disk seek may be required for every page that is read. Many Btree implementations therefore try to lay out the tree so that leaf pages appear in sequential order on disk. However, it’s difficult to maintain that order as the tree grows. By contrast, since LSM-trees rewrite large segments of the storage in one go during merging, it’s easier for them to keep sequential keys close to each other on disk.  
• Additional pointers have been added to the tree. For example, each leaf page may have references to its sibling pages to the left and right, which allows scanning keys in order without jumping back to parent pages.  
• B-tree variants such as fractal trees [22] borrow some log-structured ideas to reduce disk seeks  

#### Comparing B-Trees and LSM-Trees

**==As a rule of thumb, LSM-trees are typically faster for writes, whereas B-trees are thought to be faster for read==**

**Advantages of LSM-trees**

A B-tree index must write every piece of data at least twice: once to the write-ahead log, and once to the tree page itself

Log-structured indexes also rewrite data multiple times due to repeated compaction and merging of SSTables. This effect—one write to the database resulting in multiple writes to the disk over the course of the database’s lifetime—is known as write amplification. It is of particular concern on SSDs, which can only overwrite blocks a limited number of times before wearing out. 

In write-heavy applications, the performance bottleneck might be the rate at which the database can write to disk. In this case, write amplification has a direct performance cost: the more that a storage engine writes to disk, the fewer writes per second it can handle within the available disk bandwidth.

Moreover, LSM-trees are typically able to sustain higher write throughput than Btrees, partly because they sometimes have lower write amplification

LSM-trees can be compressed better, and thus often produce smaller files on disk than B-trees. B-tree storage engines leave some disk space unused due to fragmentation: when a page is split or when a row cannot fit into an existing page, some space in a page remains unused. Since LSM-trees are not page-oriented and periodically rewrite SSTables to remove fragmentation, they have lower storage overheads, especially when using leveled compaction

**Downsides of LSM-trees**

A downside of log-structured storage is that the compaction process can sometimes interfere with the performance of ongoing reads and writes. Even though storage engines try to perform compaction incrementally and without affecting concurrent access

Another issue with compaction arises at high write throughput: the disk’s finite write bandwidth needs to be shared between the initial write (logging and flushing a memtable to disk) and the compaction threads running in the background. When writing to an empty database, the full disk bandwidth can be used for the initial write, but the bigger the database gets, the more disk bandwidth is required for compaction. If write throughput is high and compaction is not configured carefully, it can happen that compaction cannot keep up with the rate of incoming writes

An advantage of B-trees is that each key exists in exactly one place in the index, whereas a log-structured storage engine may have multiple copies of the same key in different segments. This aspect makes B-trees attractive in databases that want to offer strong transactional semantics: in many relational databases, transaction isolation is implemented using locks on ranges of keys, and in a B-tree index, those locks can be directly attached to the tree

#### Other Indexing Structures

A primary key uniquely identifies one row in a relational table, or one document in a document database, or one vertex in a graph database. Other records in the database can refer to that row/document/vertex by its primary key (or ID), and the index is used to resolve such references.
It is also very common to have secondary indexes.

A secondary index can easily be constructed from a key-value index. The main difference is that keys are not unique; i.e., there might be many rows (documents, vertices) with the same key. This can be solved in two ways: either by making each value in the index a list of matching row identifiers (like a postings list in a full-text index) or by making each key unique by appending a row identifier to it. Either way, both B-trees and log-structured indexes can be used as secondary indexes.

**Storing values within the index**

The key in an index is the thing that queries search for, but the value can be one of two things: it could be the actual row (document, vertex) in question, or it could be a reference to the row stored elsewhere. In the latter case, the place where rows are stored is known as a heap file, and it stores data in no particular order (it may be append-only, or it may keep track of deleted rows in order to overwrite them with new data later). The heap file approach is common because it avoids duplicating data when multiple secondary indexes are present: each index just references a location in the heap file, and the actual data is kept in one place.

When updating a value without changing the key, the heap file approach can be quite efficient: the record can be overwritten in place, provided that the new value is not larger than the old value. The situation is more complicated if the new value is larger, as it probably needs to be moved to a new location in the heap where there is enough space

In some situations, the extra hop from the index to the heap file is too much of a performance penalty for reads, so it can be desirable to store the indexed row directly within an index. This is known as a clustered index. For example, in MySQL’s ``InnoDB`` storage engine, the primary key of a table is always a clustered index,

A compromise between a clustered index (storing all row data within the index) and a non-clustered index (storing only references to the data within the index) is known as a covering index or index with included columns, which stores some of a table’s columns within the index [33]. This allows some queries to be answered by using the index alone (in which case, the index is said to cover the query)

**Multi-column indexes**

The most common type of multi-column index is called a concatenated index, which simply combines several fields into one key by appending one column to another (the index definition specifies in which order the fields are concatenated). This is like an old-fashioned paper phone book, which provides an index from (last name, first name) to phone number. Due to the sort order, the index can be used to find all the people with a particular last name, or all the people with a particular last name first name combination. However, the index is useless if you want to find all the people with a particular first name. Multi-dimensional indexes are a more general way of querying several columns at once, which is particularly important for geospatial data.

```sql
SELECT * FROM restaurants WHERE latitude > 51.4946 AND latitude < 51.5079
AND longitude > -0.1162 AND longitude < -0.1004;
```

A standard B-tree or LSM-tree index is not able to answer that kind of query efficiently: it can give you either all the restaurants in a range of latitudes (but at any longitude), or all the restaurants in a range of longitudes (but anywhere between the North and South poles), but not both simultaneously. One option is to translate a two-dimensional location into a single number using a space-filling curve, and then to use a regular B-tree index

**Full-text search and fuzzy indexes**

full-text search engines commonly allow a search for one word to be expanded to include synonyms of the word, to ignore grammatical variations of words, and to search for occurrences of words near each other in the same document, and support various other features that depend on linguistic analysis of the text. To cope with typos in documents or queries, Lucene is able to search text for words within a certain edit distance (an edit distance of 1 means that one letter has been added, removed, or replaced)

**Keeping everything in memory**

The data structures discussed so far in this chapter have all been answers to the limitations of disks. Compared to main memory, disks are awkward to deal with. With both magnetic disks and SSDs, data on disk needs to be laid out carefully if you want good performance on reads and writes. However, we tolerate this awkwardness because disks have two significant advantages: they are durable (their contents are not lost if the power is turned off), and they have a lower cost per gigabyte than RAM. As RAM becomes cheaper, the cost-per-gigabyte argument is eroded

### Transaction Processing or Analytics?

> A transaction needn’t necessarily have ACID (atomicity, consistency, isolation, and durability) properties. Transaction processing just means allowing clients to make low-latency reads and writes— as opposed to batch processing jobs, which only run periodically (for example, once per day).

the basic access pattern remained similar to processing business transactions. An application typically looks up a small number of records by some key, using an index. Records are inserted or updated based on the user’s input. Because these applications are interactive, the access pattern became known as online transaction processing (OLTP).

However, databases also started being increasingly used for data analytics, which has very different access patterns. Usually an analytic query needs to scan over a huge number of records, only reading a few columns per record, and calculates aggregate statistics (such as count, sum, or average) rather than returning the raw data to the user

In order to differentiate this pattern of using databases from transaction processing, it has been called online analytic processing (OLAP) [47].iv The difference between OLTP and OLAP is not always clear-cut

![[Pasted image 20251012174941.png]]

#### Data Warehousing

An enterprise may have dozens of different transaction processing systems These OLTP systems are usually expected to be highly available and to process transactions with low latency, since they are often critical to the operation of the business. Database administrators therefore closely guard their OLTP databases. They are usually reluctant to let business analysts run ad hoc analytic queries on an OLTP database, since those queries are often expensive, scanning large parts of the dataset, which can harm the performance of concurrently executing transactions.

A data warehouse, by contrast, is a separate database that analysts can query to their hearts’ content, without affecting OLTP operations [48]. The data warehouse contains a read-only copy of the data in all the various OLTP systems in the company. Data is extracted from OLTP databases (using either a periodic data dump or a continuous stream of updates), transformed into an analysis-friendly schema, cleaned up, and then loaded into the data warehouse. This process of getting data into the warehouse is known as Extract–Transform–Load (ETL)

![[Pasted image 20251012175039.png]]

**The divergence between OLTP databases and data warehouses**

The data model of a data warehouse is most commonly relational, because SQL is generally a good fit for analytic queries. There are many graphical data analysis tools that generate SQL queries, visualize the results, and allow analysts to explore the data

On the surface, a data warehouse and a relational OLTP database look similar, because they both have a SQL query interface. However, the internals of the systems can look quite different, because they are optimized for very different query patterns.

Some databases, such as Microsoft SQL Server and SAP HANA, have support for transaction processing and data warehousing in the same product. However, they are increasingly becoming two separate storage and query engines, which happen to be accessible through a common SQL interface

#### Stars and Snowflakes: Schemas for Analytics

a wide range of different data models are used in the realm of transaction processing, depending on the needs of the application. On the other hand, in analytics, there is much less diversity of data models. Many data warehouses are used in a fairly formulaic style, known as a star schema (also known as dimensional modeling

![[Pasted image 20251012175219.png]]

Usually, facts are captured as individual events, because this allows maximum flexibility of analysis later

**==The name “star schema” comes from the fact that when the table relationships are visualized, the fact table is in the middle, surrounded by its dimension tables; the connections to these tables are like the rays of a star. A variation of this template is known as the snowflake schema, where dimensions are further broken down into subdimensions==**

In a typical data warehouse, tables are often very wide: fact tables often have over 100 columns, sometimes several hundred [51]. Dimension tables can also be very wide, as they include all the metadata that may be relevant for analysis

### Column-Oriented Storage

you have trillions of rows and petabytes of data in your fact tables, storing and querying them efficiently becomes a challenging problem. Dimension tables are usually much smaller (millions of rows), so in this section we will concentrate primarily on storage of facts.

Although fact tables are often over 100 columns wide, a typical data warehouse query only accesses 4 or 5 of them at one time

```sql
SELECT
dim_date.weekday, dim_product.category,
SUM(fact_sales.quantity) AS quantity_sold
FROM fact_sales
JOIN dim_date ON fact_sales.date_key = dim_date.date_key
JOIN dim_product ON fact_sales.product_sk = dim_product.product_sk
WHERE
dim_date.year = 2013 AND
dim_product.category IN ('Fresh fruit', 'Candy')
GROUP BY
dim_date.weekday, dim_product.category;
```

In most OLTP databases, storage is laid out in a row-oriented fashion: all the values from one row of a table are stored next to each other. Document databases are similar: an entire document is typically stored as one contiguous sequence of bytes

**==The idea behind column-oriented storage is simple: don’t store all the values from one row together, but store all the values from each column together instead. If each column is stored in a separate file, a query only needs to read and parse those columns that are used in that query, which can save a lot of work==**

> Column storage is easiest to understand in a relational data model, but it applies equally to nonrelational data

![[Pasted image 20251012175556.png]]

The column-oriented storage layout relies on each column file containing the rows in the same order. Thus, if you need to reassemble an entire row, you can take the 23rd entry from each of the individual column files and put them together to form the 23rd row of the table.

#### Column Compression

Besides only loading those columns from disk that are required for a query, we can further reduce the demands on disk throughput by compressing data. Fortunately, column-oriented storage often lends itself very well to compression

Often, the number of distinct values in a column is small compared to the number of rows (for example, a retailer may have billions of sales transactions, but only 100,000 distinct products). We can now take a column with n distinct values and turn it into n separate bitmaps: one bitmap for each distinct value, with one bit for each row. The bit is 1 if the row has that value, and 0 if not

those bitmaps can be stored with one bit per row. But if n is bigger, there will be a lot of zeros in most of the bitmaps (we say that they are sparse). In that case, the bitmaps can additionally be run-length encoded, . This can make the encoding of a column remarkably compact

#### Sort Order in Column Storage

In a column store, it doesn’t necessarily matter in which order the rows are stored. It’s easiest to store them in the order in which they were inserted, since then inserting a new row just means appending to each of the column files. However, we can choose to impose an order, like we did with SSTables previously, and use that as an indexing mechanism.

Note that it wouldn’t make sense to sort each column independently, because then we would no longer know which items in the columns belong to the same row.

Rather, the data needs to be sorted an entire row at a time, even though it is stored by column. The administrator of the database can choose the columns by which the table should be sorted, using their knowledge of common queries

A second column can determine the sort order of any rows that have the same value in the first column. For example, if ``date_key`` is the first sort key

Another advantage of sorted order is that it can help with compression of columns. If the primary sort column does not have many distinct values, then after sorting, it will have long sequences where the same value is repeated many times in a row.

That compression effect is strongest on the first sort key. The second and third sort keys will be more jumbled up, and thus not have such long runs of repeated values. Columns further down the sorting priority appear in essentially random order

#### Writing to Column-Oriented Storage

These optimizations make sense in data warehouses, because most of the load consists of large read-only queries run by analysts. Column-oriented storage, compression, and sorting all help to make those read queries faster. However, they have the downside of making writes more difficult.

An update-in-place approach, like B-trees use, is not possible with compressed columns. If you wanted to insert a row in the middle of a sorted table, you would most likely have to rewrite all the column files

All writes first go to an in-memory store, where they are added to a sorted structure and prepared for writing to disk. It doesn’t matter whether the in-memory store is row-oriented or column-oriented. When enough writes have accumulated, they are merged with the column files on disk and written to new files in bulk

#### Aggregation: Data Cubes and Materialized Views

Not every data warehouse is necessarily a column store: traditional row-oriented databases and a few other architectures are also used. However, columnar storage can be significantly faster for ad hoc analytical queries, so it is rapidly gaining popularity

Another aspect of data warehouses that is worth mentioning briefly is materialized aggregates

One way of creating such a cache is a materialized view. In a relational data model, it is often defined like a standard (virtual) view: a table-like object whose contents are the results of some query. The difference is that a materialized view is an actual copy of the query results, written to disk, whereas a virtual view is just a shortcut for writing queries. When you read from a virtual view, the SQL engine expands it into the view’s underlying query on the fly and then processes the expanded query

### Summary


This chapter explored how databases store and retrieve data, focusing on two main types of storage engines:

- **OLTP (Online Transaction Processing):**  
  - Handles many small, key-based queries from user-facing applications.  
  - Disk seek time is the main bottleneck.  

- **OLAP (Online Analytical Processing):**  
  - Handles fewer but larger, scan-heavy queries for analytics.  
  - Disk bandwidth is the main bottleneck.  
  - Uses **column-oriented storage** for efficiency.  

Two major storage philosophies:  
- **Log-structured engines** (e.g., Bitcask, LSM-trees, LevelDB, Cassandra) — append-only design, optimize for sequential writes.  
- **Update-in-place engines** (e.g., B-trees) — modify fixed-size pages directly on disk.  

Log-structured designs improve write throughput; B-trees dominate traditional databases.  
Understanding these concepts helps developers choose and tune the right database for their workloads.

## CHAPTER 4 Encoding and Evolution

In most cases, a change to an application’s features also requires a change to data that it stores: perhaps a new field or record type needs to be captured, or perhaps existing data needs to be presented in a new way.

Relational databases generally assume that all data in the database conforms to one schema: although that schema can be changed (through schema migrations; i.e., ALTER statements), there is exactly one schema in force at any one point in time. By contrast, schema-on-read (“schemaless”) databases don’t enforce a schema, so the database can contain a mixture of older and newer data formats written at different times

When a data format or schema changes, a corresponding change to application code often needs to happen (for example, you add a new field to a record, and the application code starts reading and writing that field). However, in a large application, code changes often cannot happen instantaneously:

With server-side applications you may want to perform a rolling upgrade (also
known as a staged rollout), deploying the new version to a few nodes at a time,
checking whether the new version is running smoothly, and gradually working
your way through all the nodes. This allows new versions to be deployed without
service downtime, and thus encourages more frequent releases and better evolvability.

• With client-side applications you’re at the mercy of the user, who may not install
the update for some time.

This means that old and new versions of the code, and old and new data formats,
may potentially all coexist in the system at the same time. In order for the system to
continue running smoothly, we need to maintain compatibility in both directions:

**Backward compatibility**  
Newer code can read data that was written by older code.

**Forward compatibility**  
Older code can read data that was written by newer code.


Backward compatibility is normally not hard to achieve: as author of the newer code, you know the format of data written by older code, and so you can explicitly handle it (if necessary by simply keeping the old code to read the old data). Forward compatibility can be trickier, because it requires older code to ignore additions made by a newer version of the code.

### Formats for Encoding Data

Programs usually work with data in (at least) two different representations:

1. In memory, data is kept in objects, structs, lists, arrays, hash tables, trees, and so
   on. These data structures are optimized for efficient access and manipulation by
   the CPU (typically using pointers).

2. When you want to write data to a file or send it over the network, you have to
   encode it as some kind of self-contained sequence of bytes (for example, a JSON
   document). Since a pointer wouldn’t make sense to any other process, this
   sequence-of-bytes representation looks quite different from the data structures
   that are normally used in memory.ᵢ

==The translation from the in-memory representation to a byte sequence is called **encoding** (also known as **serialization** or **marshalling**), and the reverse is called **decoding** (**parsing**, **deserialization**, **unmarshalling**)==

#### Language-Specific Formats

Many programming languages come with built-in support for encoding in-memory objects into byte sequences

These encoding libraries are very convenient, because they allow in-memory objects
to be saved and restored with minimal additional code. However, they also have a number of deep problems:

• The encoding is often tied to a particular programming language, and reading the data in another language is very difficult. If you store or transmit data in such an encoding, you are committing yourself to your current programming language for potentially a very long time, and precluding integrating your systems with those of other organizations (which may use different languages).

• In order to restore data in the same object types, the decoding process needs to be able to instantiate arbitrary classes. This is frequently a source of security problems [5]: if an attacker can get your application to decode an arbitrary byte sequence, they can instantiate arbitrary classes, which in turn often allows them to do terrible things such as remotely executing arbitrary code.

• Versioning data is often an afterthought in these libraries: as they are intended for quick and easy encoding of data, they often neglect the inconvenient problems  of forward and backward compatibility.

• Efficiency (CPU time taken to encode or decode, and the size of the encoded structure) is also often an afterthought. For example, Java’s built-in serialization  is notorious for its bad performance and bloated encoding.

#### JSON, XML, and Binary Variants

XML is often criticized for being too verbose and unnecessarily complicated [9]. JSON’s popularity is mainly due to its built-in support in web browsers (by virtue of being a subset of JavaScript) and simplicity relative to XML. CSV is another popular language-independent format, albeit less powerful. JSON, XML, and CSV are textual formats, and thus somewhat human-readable (although the syntax is a popular topic of debate). Besides the superficial syntactic issues, they also have some subtle problems:

• There is a lot of ambiguity around the encoding of numbers. In XML and CSV, you cannot distinguish between a number and a string that happens to consist of digits (except by referring to an external schema). JSON distinguishes strings and numbers, but it doesn’t distinguish integers and floating-point numbers, and it doesn’t specify a precision.

• JSON and XML have good support for Unicode character strings (i.e., human readable text), but they don’t support binary strings (sequences of bytes without a character encoding). Binary strings are a useful feature, so people get around this limitation by encoding the binary data as text using Base64

• There is optional schema support for both XML [11] and JSON [12]. These schema languages are quite powerful, and thus quite complicated to learn and implement. Use of XML schemas is fairly widespread, but many JSON-based tools don’t bother using schemas. Since the correct interpretation of data (such as numbers and binary strings) depends on information in the schema, applications that don’t use XML/JSON schemas need to potentially hardcode the appropriate encoding/decoding logic instead.

• CSV does not have any schema, so it is up to the application to define the meaning of each row and column. If an application change adds a new row or column, you have to handle that change manually.

**Binary encoding**

For data that is used only internally within your organization, there is less pressure to use a lowest-common-denominator encoding format 

JSON is less verbose than XML, but both still use a lot of space compared to binary formats. This observation led to the development of a profusion of binary encodings for JSON 

These formats have been adopted in various niches, but none of them are as widely adopted as the textual versions of JSON and XML. Some of these formats extend the set of datatypes (e.g., distinguishing integers and floating-point numbers, or adding support for binary strings), but otherwise they keep the JSON/XML data model unchanged. In particular, since they don’t prescribe a schema, they need to include all the object field names within the encoded data. That is, in a binary encoding of the JSON document

#### Thrift and Protocol Buffers

Both Thrift and Protocol Buffers require a schema for any data that is encoded.

```json
struct Person {
1: required string userName,
2: optional i64 favoriteNumber,
3: optional list<string> interests
}
```

```json
message Person {
required string user_name = 1;
optional int64 favorite_number = 2;
repeated string interests = 3;
}
```

Thrift and Protocol Buffers each come with a code generation tool that takes a schema definition like the ones shown here, and produces classes that implement the schema in various programming languages

#### The Merits of Schemas

Protocol Buffers, Thrift, and Avro all use a schema to describe a binary encoding format. Their schema languages are much simpler than XML Schema or JSON Schema, which support much more detailed validation rules As Protocol Buffers, Thrift, and Avro are simpler to implement and simpler to use, they have grown to support a fairly wide range of programming languages. The ideas on which these encodings are based are by no means new

We can see that although textual data formats such as JSON, XML, and CSV are widespread, binary encodings based on schemas are also a viable option. They have a number of nice properties:  

• They can be much more compact than the various “binary JSON” variants, since they can omit field names from the encoded data.  
• The schema is a valuable form of documentation, and because the schema is required for decoding, you can be sure that it is up to date (whereas manually maintained documentation may easily diverge from reality).  
• Keeping a database of schemas allows you to check forward and backward compatibility of schema changes, before anything is deployed.  
• For users of statically typed programming languages, the ability to generate code from the schema is useful, since it enables type checking at compile time.

### Modes of Dataflow

whenever you want to send some data to another process with which you don’t share memory—for example, whenever you want to send data over the network or write it to a file—you need to encode it as a sequence of bytes. We then discussed a variety of different encodings for doing this.

there are many ways data can flow from one process to another. Who encodes the data, and who decodes it?

#### Dataflow Through Databases

In a database, the process that writes to the database encodes the data, and the process that reads from the database decodes it. There may just be a single process accessing the database, in which case the reader is simply a later version of the same process—in that case you can think of storing something in the database as sending a message to your future self. Backward compatibility is clearly necessary here; otherwise your future self won’t be able to decode what you previously wrote.  

In general, it’s common for several different processes to be accessing a database at the same time. Those processes might be several different applications or services, or they may simply be several instances of the same service (running in parallel for scalability or fault tolerance). Either way, in an environment where the application is changing, it is likely that some processes accessing the database will be running newer code and some will be running older code—for example because a new version is currently being deployed in a rolling upgrade, so some instances have been updated while others haven’t yet.

This means that a value in the database may be written by a newer version of the code, and subsequently read by an older version of the code that is still running. Thus, forward compatibility is also often required for databases.  

However, there is an additional snag. Say you add a field to a record schema, and the newer code writes a value for that new field to the database. Subsequently, an older version of the code (which doesn’t yet know about the new field) reads the record, updates it, and writes it back. In this situation, the desirable behavior is usually for the old code to keep the new field intact, even though it couldn’t be interpreted.


![[Pasted image 20251015145628.png]]

**Different values written at different times**

A database generally allows any value to be updated at any time. This means that within a single database you may have some values that were written five milliseconds ago, and some values that were written five years ago.  

When you deploy a new version of your application (of a server-side application, at least), you may entirely replace the old version with the new version within a few minutes. The same is not true of database contents: the five-year-old data will still be there, in the original encoding, unless you have explicitly rewritten it since then. This observation is sometimes summed up as **data outlives code**.  

Rewriting (migrating) data into a new schema is certainly possible, but it’s an expensive thing to do on a large dataset, so most databases avoid it if possible. Most relational databases allow simple schema changes, such as adding a new column with a null default value, without rewriting existing data.ᵛ When an old row is read, the database fills in nulls for any columns that are missing from the encoded data on disk.


**Archival storage**

Perhaps you take a snapshot of your database from time to time, say for backup purposes or for loading into a data warehouse (see “Data Warehousing” on page 91). In this case, the data dump will typically be encoded using the latest schema, even if the original encoding in the source database contained a mixture of schema versions from different eras. Since you’re copying the data anyway, you might as well encode the copy of the data consistently .As the data dump is written in one go and is thereafter immutable, formats like Avro object container files are a good fit.

#### Dataflow Through Services: REST and RPC

When you have processes that need to communicate over a network, there are a few different ways of arranging that communication. The most common arrangement is to have two roles: **clients** and **servers**. The servers expose an API over the network, and the clients can connect to the servers to make requests to that API. The API exposed by the server is known as a **service**.  

Web browsers are not the only type of client. For example, a native app running on a mobile device or a desktop computer can also make network requests to a server, and a client-side JavaScript application running inside a web browser can use `XMLHttpRequest` to become an HTTP client.  

Moreover, a server can itself be a client to another service (for example, a typical web app server acts as client to a database). This approach is often used to decompose a large application into smaller services by area of functionality, such that one service makes a request to another when it requires some functionality or data from that other service. This way of building applications has traditionally been called a **service-oriented architecture (SOA)**, more recently refined and rebranded as **microservices architecture** [31, 32].  

In some ways, services are similar to databases: they typically allow clients to submit and query data. However, while databases allow arbitrary queries using the query languages we discussed in Chapter 2, services expose an application-specific API that only allows inputs and outputs that are predetermined by the business logic (application code) of the service.  

A key design goal of a service-oriented/microservices architecture is to make the application easier to change and maintain by making services independently deployable and evolvable.


**Web services**

When HTTP is used as the underlying protocol for talking to the service, it is called a **web service**. This is perhaps a slight misnomer, because web services are not only used on the web, but in several different contexts. For example:  

1. A client application running on a user’s device  
2. One service making requests to another service owned by the same organization, often located within the same datacenter, as part of a service-oriented/microservices architecture  
3. One service making requests to a service owned by a different organization, usually via the internet. This is used for data exchange between different organizations’ backend systems. This category includes public APIs provided by online services, such as credit card processing systems, or OAuth for shared access to user data.  

**REST** is not a protocol, but rather a design philosophy that builds upon the principles of HTTP [34, 35]. It emphasizes simple data formats, using URLs for identifying resources and using HTTP features for cache control, authentication, and content type negotiation. REST has been gaining popularity compared to SOAP, at least in the context of cross-organizational service integration.  

By contrast, **SOAP** is an XML-based protocol for making network API requests.ᵛᶦᶦ Although it is most commonly used over HTTP, it aims to be independent from HTTP and avoids using most HTTP features. Instead, it comes with a sprawling and complex multitude of related standards.  

The API of a SOAP web service is described using an XML-based language called the **Web Services Description Language (WSDL)**. WSDL enables code generation so that a client can access a remote service using local classes and method calls.  

Even though SOAP and its various extensions are ostensibly standardized, interoperability between different vendors’ implementations often causes problems.  

RESTful APIs tend to favor simpler approaches, typically involving less code generation and automated tooling. A definition format such as **``OpenAPI``**, also known as **Swagger**.


**The problems with remote procedure calls (RPCs)**

A network request is very different from a local function call:  

• A local function call is predictable and either succeeds or fails, depending only on parameters that are under your control. A network request is unpredictable: the request or response may be lost due to a network problem, or the remote machine may be slow or unavailable, and such problems are entirely outside of your control. Network problems are common, so you have to anticipate them, for example by retrying a failed request.  

• A local function call either returns a result, or throws an exception, or never returns (because it goes into an infinite loop or the process crashes). A network request has another possible outcome: it may return without a result, due to a timeout. In that case, you simply don’t know what happened: if you don’t get a response from the remote service, you have no way of knowing whether the request got through or not.  

• If you retry a failed network request, it could happen that the requests are actually getting through, and only the responses are getting lost. In that case, retrying will cause the action to be performed multiple times, unless you build a mechanism for deduplication (**idempotence**) into the protocol. Local function calls don’t have this problem.  

• Every time you call a local function, it normally takes about the same time to execute. A network request is much slower than a function call, and its latency is also wildly variable: at good times it may complete in less than a millisecond, but when the network is congested or the remote service is overloaded it may take many seconds to do exactly the same thing.  

• When you call a local function, you can efficiently pass it references (pointers) to objects in local memory. When you make a network request, all those parameters must be serialized. That’s okay if the parameters are primitives like numbers or strings, but quickly becomes problematic with larger objects.  

• The client and the service may be implemented in different programming languages, so the RPC framework must translate datatypes from one language into another.  

All of these factors mean that there’s no point trying to make a remote service look too much like a local object in your programming language, because it’s a fundamentally different thing. Part of the appeal of REST is that it doesn’t try to hide the fact that it’s a network protocol.

#### Message-Passing Dataflow

asynchronous message-passing systems, which are somewhere between RPC and databases. They are similar to RPC in that a client’s request (usually called a message) is delivered to another process with low latency. They are similar to databases in that the message is not sent via a direct network connection, but goes via an intermediary called a message broker

Using a message broker has several advantages compared to direct RPC:  

• It can act as a buffer if the recipient is unavailable or overloaded, and thus improve system reliability.  
• It can automatically redeliver messages to a process that has crashed, and thus prevent messages from being lost.  
• It avoids the sender needing to know the IP address and port number of the recipient (which is particularly useful in a cloud deployment where virtual machines often come and go).  
• It allows one message to be sent to several recipients.  
• It logically decouples the sender from the recipient (the sender just publishes messages and doesn’t care who consumes them).  


However, a difference compared to RPC is that message-passing communication is usually one-way: a sender normally doesn’t expect to receive a reply to its messages. It is possible for a process to send a response, but this would usually be done on a separate channel.

**Message brokers**

The detailed delivery semantics vary by implementation and configuration, but in general, message brokers are used as follows: one process sends a message to a named queue or topic, and the broker ensures that the message is delivered to one or more consumers of or subscribers to that queue or topic. There can be many producers and many consumers on the same topic.

Message brokers typically don’t enforce any particular data model—a message is just a sequence of bytes with some metadata, so you can use any encoding format. If the encoding is backward and forward compatible, you have the greatest flexibility to change publishers and consumers independently and deploy them in any order.

**Distributed actor frameworks**

The actor model is a programming model for concurrency in a single process. Rather than dealing directly with threads (and the associated problems of race conditions, locking, and deadlock), logic is encapsulated in **actors**. Each actor typically represents one client or entity, it may have some local state (which is not shared with any other actor), and it communicates with other actors by sending and receiving asynchronous messages. Message delivery is not guaranteed: in certain error scenarios, messages will be lost. Since each actor processes only one message at a time, it doesn’t need to worry about threads, and each actor can be scheduled independently by the framework.  

In distributed actor frameworks, this programming model is used to scale an application across multiple nodes. The same message-passing mechanism is used, no matter whether the sender and recipient are on the same node or different nodes. If they are on different nodes, the message is transparently encoded into a byte sequence, sent over the network, and decoded on the other side.  

Location transparency works better in the actor model than in RPC, because the actor model already assumes that messages may be lost, even within a single process. Although latency over the network is likely higher than within the same process, there is less of a fundamental mismatch between local and remote communication when using the actor model.  

A distributed actor framework essentially integrates a message broker and the actor programming model into a single framework. However, if you want to perform rolling upgrades of your actor-based application, you still have to worry about forward and backward compatibility, as messages may be sent from a node running the new version to a node running the old version, and vice versa.

### Summary

Rolling upgrades allow new versions of a service to be deployed gradually, avoiding downtime and reducing deployment risks. During these upgrades, different nodes may run different versions of the code, so data must maintain **backward compatibility** (new code can read old data) and **forward compatibility** (old code can read new data).  

**Data encoding formats:**  
- **Language-specific encodings**: restricted to one language, often lack compatibility.  
- **Textual formats (JSON, XML, CSV)**: widely used; optional schemas; somewhat vague about datatypes.  
- **Binary schema-driven formats (Thrift, Protocol Buffers, Avro)**: compact, efficient, with clear forward/backward compatibility; good for documentation and code generation; not human-readable without decoding.  

**Modes of dataflow:**  
- **Databases**: writer encodes, reader decodes.  
- **RPC/REST APIs**: client encodes request, server decodes request and encodes response, client decodes response.  
- **Asynchronous messaging (message brokers, actors)**: sender encodes messages, recipient decodes them.  

With careful design, backward/forward compatibility and rolling upgrades are achievable, enabling rapid evolution and frequent, safe deployments.


# PART II Distributed Data

**Reasons to Distribute a Database Across Multiple Machines**

**Scalability**  
When your data volume, read load, or write load grows beyond the capacity of a single machine, you can distribute the data across multiple machines. This allows the system to handle increased traffic and data more efficiently by spreading the workload.

**Fault Tolerance / High Availability**  
To ensure the application remains operational even if one or more machines fail, multiple machines can be used to provide redundancy. If one node or datacenter goes down, another can take over, preventing downtime and data loss.

**Latency**  
For applications with a global user base, deploying servers in multiple geographic locations helps reduce latency. Users can connect to the datacenter closest to them, avoiding the delays caused by long-distance network communication.

## Scaling to Higher Load

If all you need is to scale to higher load, the simplest approach is to buy a more powerful machine 
The problem with a shared-memory approach is that the cost grows faster than linearly: a machine with twice as many CPUs, twice as much RAM, and twice as much disk capacity as another typically costs significantly more than twice as much. And due to bottlenecks, a machine twice the size cannot necessarily handle twice the load.

Another approach is the shared-disk architecture, which uses several machines with independent CPUs and RAM, but stores data on an array of disks that is shared between the machines, which are connected via a fast network

#### Shared-Nothing Architectures

By contrast, shared-nothing architectures [3] (sometimes called horizontal scaling or scaling out) have gained a lot of popularity. In this approach, each machine or virtual machine running the database software is called a node. Each node uses its CPUs, RAM, and disks independently. Any coordination between nodes is done at the software level, using a conventional network.

No special hardware is required by a shared-nothing system, so you can use whatever machines have the best price/performance ratio. You can potentially distribute data across multiple geographic regions, and thus reduce latency for users and potentially be able to survive the loss of an entire datacenter

While a distributed shared-nothing architecture has many advantages, it usually also
incurs additional complexity for applications and sometimes limits the expressiveness
of the data models you can use

#### Replication Versus Partitioning

There are two common ways data is distributed across multiple nodes:  

Replication  
Keeping a copy of the same data on several different nodes, potentially in different locations. Replication provides redundancy: if some nodes are unavailable, the data can still be served from the remaining nodes. Replication can also help improve performance. We discuss replication in Chapter 5.  

Partitioning  
Splitting a big database into smaller subsets called partitions so that different partitions can be assigned to different nodes (also known as sharding). We discuss partitioning in Chapter 6.
## CHAPTER 5 Replication

Replication means keeping a copy of the same data on multiple machines that are connected via a network

• To keep data geographically close to your users (and thus reduce latency)
• To allow the system to continue working even if some of its parts have failed (and thus increase availability)
• To scale out the number of machines that can serve read queries (and thus increase read throughput)

If the data that you’re replicating does not change over time, then replication is easy: you just need to copy the data to every node once, and you’re done. **==All of the difficulty in replication lies in handling changes to replicated data==**

There are many trade-offs to consider with replication: for example, whether to use synchronous or asynchronous replication, and how to handle failed replicas. Those are often configuration options in databases, and although the details vary by database, the general principles are similar across many different implementations

### Leaders and Followers

Each node that stores a copy of the database is called a replica. With multiple replicas, a question inevitably arises: how do we ensure that all the data ends up on all the replicas? 

Every write to the database needs to be processed by every replica; otherwise, the replicas would no longer contain the same data. The most common solution for this is called leader-based replication

1. **==One of the replicas is designated the leader (also known as master or primary). When clients want to write to the database, they must send their requests to the leader, which first writes the new data to its local storage.**==
    
2. ==**The other replicas are known as followers (read replicas, slaves, secondaries, or hot standbys). Whenever the leader writes new data to its local storage, it also sends the data change to all of its followers as part of a replication log or change stream. Each follower takes the log from the leader and updates its local copy of the database accordingly, by applying all writes in the same order as they were processed on the leader.==**

3. ==**When a client wants to read from the database, it can query either the leader or any of the followers==**

![[Pasted image 20251016164858.png]]

#### Synchronous Versus Asynchronous Replication

An important detail of a replicated system is whether the replication happens synchronously or asynchronously

**==The advantage of synchronous replication is that the follower is guaranteed to have an up-to-date copy of the data that is consistent with the leader. If the leader suddenly fails, we can be sure that the data is still available on the follower. The disadvantage is that if the synchronous follower doesn’t respond (because it has crashed, or there is a network fault, or for any other reason), the write cannot be processed. The leader must block all writes and wait until the synchronous replica is available again.==**

For that reason, it is impractical for all followers to be synchronous: any one node outage would cause the whole system to grind to a halt. In practice, if you enable synchronous replication on a database, it usually means that one of the followers is synchronous, and the others are asynchronous. If the synchronous follower becomes unavailable or slow, one of the asynchronous followers is made synchronous. This guarantees that you have an up-to-date copy of the data on at least two nodes: the leader and one synchronous follower. This configuration is sometimes also called semi-synchronous 

#### Setting Up New Followers

From time to time, you need to set up new followers—perhaps to increase the number of replicas, or to replace failed nodes. How do you ensure that the new follower has an accurate copy of the leader’s data?  
Simply copying data files from one node to another is typically not sufficient: clients are constantly writing to the database, and the data is always in flux, so a standard file copy would see different parts of the database at different points in time. The result might not make any sense.  

You could make the files on disk consistent by locking the database (making it unavailable for writes), but that would go against our goal of high availability. Fortunately, setting up a follower can usually be done without downtime. Conceptually, the process looks like this:

1. ==**Take a consistent snapshot of the leader’s database at some point in time—if possible, without taking a lock on the entire database.**==
    
2. ==**Copy the snapshot to the new follower node.**==
    
3. ==**The follower connects to the leader and requests all the data changes that have happened since the snapshot was taken. This requires that the snapshot is associated with an exact position in the leader’s replication log. That position has various names: for example, PostgreSQL calls it the log sequence number, and MySQL calls it the bin log coordinates.**==
    
4. ==**When the follower has processed the backlog of data changes since the snapshot, we say it has caught up. It can now continue to process data changes from the leader as they happen.==**

#### Handling Node Outages

Any node in the system can go down, perhaps unexpectedly due to a fault, but just as likely due to planned maintenance (for example, rebooting a machine to install a kernel security patch). Being able to reboot individual nodes without downtime is a big advantage for operations and maintenance. Thus, our goal is to keep the system as a whole running despite individual node failures, and to keep the impact of a node outage as small as possible.

**Follower failure: Catch-up recovery**

On its local disk, each follower keeps a log of the data changes it has received from the leader. If a follower crashes and is restarted, or if the network between the leader and the follower is temporarily interrupted, the follower can recover quite easily: from its log, **==it knows the last transaction that was processed before the fault occurred. Thus, the follower can connect to the leader and request all the data changes that occurred during the time when the follower was disconnected.==** When it has applied these changes, it has caught up to the leader and can continue receiving a stream of data changes as before.

**Leader failure: Failover**

Handling a failure of the leader is trickier: one of the followers needs to be promoted to be the new leader, clients need to be reconfigured to send their writes to the new leader, and the other followers need to start consuming data changes from the new leader 
An automatic failover process usually involves:

1. **Detecting leader failure:** Nodes monitor each other, and if the leader doesn’t respond within a timeout (e.g., 30 seconds), it’s assumed to have failed.
    
2. **Selecting a new leader:** The most up-to-date replica is chosen, either through an election or by a controller node.
    
3. **Reconfiguring the system:** Clients redirect writes to the new leader, and the old leader becomes a follower if it recovers.

Failover is fraught with things that can go wrong:

• With **asynchronous replication**, the new leader may miss some writes from the old leader. Those un-replicated writes are usually discarded, which can break durability guarantees.  
• **Discarding writes** is risky if other systems must stay in sync with the database.  
• A **split brain** can occur when two nodes both think they’re the leader, leading to conflicting writes and possible data loss. Some systems shut down one node to prevent this, but poor design can cause both to shut down.  
• **Choosing the right timeout** is tricky: too long delays recovery, too short causes false failovers due to temporary load spikes or network issues.

#### Implementation of Replication Logs

How does leader-based replication work under the hood? Several different replication methods are used in practice, so let’s look at each one briefly.
**Statement-based replication**

In the simplest case, the leader logs every write request (statement) that it executes and sends that statement log to its followers. For a relational database, this means that every INSERT, UPDATE, or DELETE statement is forwarded to followers, and each follower parses and executes that SQL statement as if it had been received from a client.

• **Nondeterministic functions** like `NOW()` or `RAND()` can produce different results on each replica.  
• **Autoincrement columns** or queries depending on existing data must run in the same order across replicas; otherwise, results may diverge.  
• **Statements with side effects** (triggers, stored procedures, user-defined functions) can behave differently on replicas unless they are fully deterministic.

**Write-ahead log (WAL) shipping**

• For a **log-structured storage engine** (SSTables and LSM-Trees), the log is the main storage. Log segments are compacted and garbage-collected in the background.  
• For a **B-tree**, which overwrites disk blocks, every modification is first written to a write-ahead log to ensure consistency after a crash.  
In both cases, the log is an append-only sequence of all writes. The leader writes it to disk and also sends it to followers, allowing them to build an identical copy of the data structures.

This method of replication is used in PostgreSQL and Oracle, among others. The main disadvantage is that the log describes the data on a very low level: a WAL contains details of which bytes were changed in which disk blocks. This makes replication closely coupled to the storage engine. If the database changes its storage format from one version to another, it is typically not possible to run different versions of the database software on the leader and the followers.

**Logical (row-based) log replication**

A logical log for a relational database is typically a sequence of records describing writes to tables at the row level:  
• **Inserted row:** log contains the new values of all columns.  
• **Deleted row:** log contains enough information to uniquely identify the row, usually the primary key, or all column values if no primary key exists.  
• **Updated row:** log contains enough information to identify the row and the new values of all changed columns.

A transaction modifying multiple rows generates multiple log records, followed by a commit record. MySQL’s bin log (with row-based replication) follows this approach. Since a logical log is independent of storage engine internals, it can support backward compatibility, allowing the leader and follower to run different database versions or storage engines.

### Problems with Replication Lag

Being able to tolerate node failures is just one reason for wanting replication. other reasons are scalability and latency

Leader-based replication requires all writes to go through a single node, but read only queries can go to any replica. For workloads that consist of mostly reads and only a small percentage of writes (a common pattern on the web), there is an attractive option: create many followers, and distribute the read requests across those followers. This removes load from the leader and allows read requests to be served by nearby replicas.

In this read-scaling architecture, you can increase the capacity for serving read-only requests simply by adding more followers. However, this approach only realistically works with asynchronous replication—if you tried to synchronously replicate to all followers, a single node failure or network outage would make the entire system unavailable for writing. And the more nodes you have, the likelier it is that one will be down, so a fully synchronous configuration would be very unreliable.

Unfortunately, if an application reads from an asynchronous follower, it may see outdated information if the follower has fallen behind. This leads to apparent inconsistencies in the database: if you run the same query on the leader and a follower at the same time, you may get different results, because not all writes have been reflected in the follower. This inconsistency is just a temporary state—if you stop writing to the database and wait a while, the followers will eventually catch up and become consistent with the leader

#### Reading Your Own Writes

Many applications let the user submit some data and then view what they have submitted. This might be a record in a customer database, or a comment on a discussion thread, or something else of that sort. When new data is submitted, it must be sent to the leader, but when the user views the data, it can be read from a follower. This is especially appropriate if data is frequently viewed but only occasionally written.

if the user views the data shortly after making a write, the new data may not yet have reached the replica. To the user, it looks as though the data they submitted was lost, so they will be understandably unhappy. 

![[Pasted image 20251016205052.png]]

**==In this situation, we need read-after-write consistency, also known as read-your-writes consistency. This is a guarantee that if the user reloads the page, they will always see any updates they submitted themselves. It makes no promises about other users: other users’ updates may not be visible until some later time. However, it reassures the user that their own input has been saved correctly.==**

• **Read from the leader** if the data may have been modified by the user; otherwise, read from a follower. This requires knowing which data might have changed without querying it.  
• If most data is editable, reading from the leader for everything reduces read scaling benefits. Alternative criteria, like reading from the leader for a short time after the last update, can be used.  
• The client can track the timestamp of its most recent write to ensure reads reflect updates at least until that time. If a replica isn’t up to date, the read can be redirected or delayed until it catches up. Timestamps can be logical (e.g., log sequence numbers) or based on system clocks (requiring synchronization).  
• With replicas in multiple datacenters, requests needing the leader must be routed to the datacenter hosting the leader, adding routing complexity.

Another complication arises when the same user is accessing your service from multiple devices, for example a desktop web browser and a mobile app. In this case you may want to provide cross-device read-after-write consistency: if the user enters some information on one device and then views it on another device, they should see the information they just entered.

**==• Tracking the timestamp of a user’s last update is harder across multiple devices, since one device may not know updates made on another. This metadata needs to be centralized.**==  
==**• With replicas in different datacenters, there’s no guarantee that requests from different devices will reach the same datacenter.==**

#### Monotonic Reads

when reading from asynchronous followers is that it’s possible for a user to see things moving backward in time. This can happen if a user makes several reads from different replicas

**==Monotonic reads is a guarantee that this kind of anomaly does not happen. It’s a lesser guarantee than strong consistency, but a stronger guarantee than eventual consistency. When you read data, you may see an old value; monotonic reads only means that if one user makes several reads in sequence, they will not see time go backward— i.e., they will not read older data after having previously read newer data.==**

#### Consistent Prefix Reads

Preventing this anomaly requires **consistent prefix reads**, which ensure that a sequence of writes is always seen in the same order by readers. This issue is common in partitioned (sharded) databases. If writes are applied in the same order, reads see a consistent prefix and the anomaly is avoided. However, many distributed databases have partitions that operate independently, so there’s no global write ordering; a user may see some parts of the database updated while others are stale. One solution is to write causally related updates to the same partition, though this is not always efficient.

#### Solutions for Replication Lag

When using an eventually consistent system, consider how the application behaves if replication lag grows to minutes or hours. If this doesn’t affect users, it’s fine. Otherwise, the system may need stronger guarantees, like **read-after-write**. Treating asynchronous replication as synchronous can lead to problems.

Applications can sometimes enforce stronger guarantees by reading from the leader, but handling this in code is complex and error-prone. Ideally, developers shouldn’t need to manage replication subtleties themselves—this is where **transactions** come in, providing stronger guarantees and simplifying application logic.

While single-node transactions are well-established, many distributed systems have moved away from them, arguing that transactions are costly for performance and availability, and claiming that eventual consistency is inevitable in scalable systems.

### Multi-Leader Replication

Leader-based replication has a key limitation: all writes must go through a single leader. If the leader becomes unreachable, for example due to a network issue, writes cannot proceed.

A natural extension is **multi-leader replication** (also called master–master or active/active), where multiple nodes can accept writes. Each node that processes a write forwards the change to all other nodes. In this setup, each leader also acts as a follower to the other leaders.

#### Use Cases for Multi-Leader Replication

It rarely makes sense to use a multi-leader setup within a single datacenter, because the benefits rarely outweigh the added complexity. However, there are some situations in which this configuration is reasonable.

**Multi-datacenter operation**

In a multi-leader configuration, you can have a leader in each datacenter. Figure 5-6 shows what this architecture might look like. Within each datacenter, regular leader– follower replication is used; between datacenters, each datacenter’s leader replicates its changes to the leaders in other datacenters.

![[Pasted image 20251016210457.png]]

**Comparison of Single-Leader vs. Multi-Leader in Multi-Datacenter Deployments**

**Performance**

- _Single-leader:_ Every write must travel to the datacenter hosting the leader, adding latency and reducing the benefit of multiple datacenters.
    
- _Multi-leader:_ Writes can be processed locally in each datacenter and replicated asynchronously to others, hiding inter-datacenter delays and improving perceived performance.
    

**Tolerance of Datacenter Outages**

- _Single-leader:_ If the leader’s datacenter fails, failover promotes a follower elsewhere to become leader.
    
- _Multi-leader:_ Each datacenter continues independently; replication catches up when the failed datacenter returns.
    

**Tolerance of Network Problems**

- _Single-leader:_ Sensitive to inter-datacenter network issues because writes depend on synchronous communication.
    
- _Multi-leader:_ Asynchronous replication allows continued operation despite network problems between datacenters.

**Clients with offline operation**
Another situation in which multi-leader replication is appropriate is if you have an application that needs to continue to work while it is disconnected from the internet.

**Collaborative editing**

Real-time collaborative editing applications allow several people to edit a document simultaneously

This is similar to the offline editing scenario: when a user edits a document, changes are applied immediately to their local replica and asynchronously replicated to the server and other users.

To prevent editing conflicts, the application must lock the document before editing. Other users must wait until the lock is released after changes are committed. This model is analogous to **single-leader replication with transactions on the leader**.

#### Handling Write Conflicts

**==The biggest problem with multi-leader replication is that write conflicts can occur, which means that conflict resolution is required.==**

**Synchronous vs. Asynchronous Conflict Detection**

- In a **single-leader database**, a second write either blocks until the first completes or aborts, forcing a retry.
    
- In a **multi-leader setup**, both writes succeed initially, and conflicts are detected asynchronously later, potentially too late for user intervention.
    
- Making conflict detection synchronous (waiting for replication to all nodes) negates the main advantage of multi-leader replication—independent writes at each replica—so at that point, single-leader replication would be simpler.
    

**Conflict Avoidance**

- The simplest strategy is to avoid conflicts by ensuring all writes for a record go through the same leader. Since many multi-leader systems handle conflicts poorly, avoiding them is often the recommended approach.

**Custom conflict resolution logic**

Most multi-leader replication systems let applications handle conflict resolution, which can occur **on write** or **on read**:

**On write**

- The conflict handler is invoked as soon as the system detects a conflict in the replication log.
    
- It runs in the background and must execute quickly; it typically cannot prompt the user.
    
- Example: Bucardo allows writing a Perl snippet for this purpose.
    

**On read**

- Conflicting writes are stored, and when the data is next read, all versions are returned.
    
- The application can prompt the user or resolve the conflict automatically, then write the result back.
    
- Example: CouchDB uses this approach.
    

Conflict resolution generally applies at the **row or document level**, not across an entire transaction. Multiple writes within a transaction are treated individually for conflict resolution.

#### Multi-Leader Replication Topologies

**==A replication topology describes the communication paths along which writes are propagated from one node to another==** 

![[Pasted image 20251016211400.png]]

The most general topology is **all-to-all**, where every leader sends writes to every other leader. However, **circular** and **star topologies** are also used.

In circular and star topologies, a write may pass through multiple nodes to reach all replicas. Nodes forward changes they receive, and each write is tagged with the identifiers of nodes it has passed through to prevent infinite loops. If a node fails, it can block replication between other nodes until fixed. Reconfiguring around the failed node is possible but usually requires manual intervention.

All-to-all topologies have better fault tolerance since messages can take multiple paths, avoiding a single point of failure. However, they can still face issues if some network links are slower than others.

### Leaderless Replication

Single-leader and multi-leader replication rely on a leader node that receives client writes and determines their order, with followers applying the writes in the same order.

Some systems take a **leaderless** approach, allowing any replica to accept writes directly. Early replicated systems used this model, but it was largely forgotten during the rise of relational databases and has recently regained popularity. In leaderless systems, clients may send writes to multiple replicas directly, or a coordinator node may do so, but no node enforces a global write order. This design difference has significant implications for how the database is used.

#### Writing to the Database When a Node Is Down

To solve that problem, when a client reads from the database, it doesn’t just send its request to one replica: read requests are also sent to several nodes in parallel. The client may get different responses from different nodes; i.e., the up-to-date value from one node and a stale value from another. Version numbers are used to determine which value is newer

#### Sloppy Quorums and Hinted Handoff

Databases using quorums can tolerate node failures or slow nodes without full failover, making **leaderless replication** attractive for high-availability, low-latency use cases that can tolerate occasional stale reads.

However, standard quorums aren’t fully fault-tolerant: network interruptions can prevent a client from reaching the nodes needed to form a quorum, even if those nodes are alive. In large clusters, a client may reach some nodes but not the designated ones for a particular value.

**Trade-off:**

- Return errors when a quorum cannot be reached.
    
- Accept writes on reachable nodes that aren’t the usual “home” nodes.
    

The latter is called a **sloppy quorum**: writes and reads still require w and r successful responses, but these may include non-home nodes. Once the network is restored, **hinted handoff** moves those writes to their proper home nodes.

Sloppy quorums increase write availability, but they don’t guarantee that a read sees the latest value until hinted handoff completes. They provide durability assurance (data exists on w nodes somewhere) rather than traditional quorum guarantees.

- In Riak, sloppy quorums are enabled by default.
    
- In Cassandra and Voldemort, they are disabled by default.

#### Detecting Concurrent Writes

Dynamo-style databases allow multiple clients to write concurrently to the same key, so conflicts are inevitable, even with strict quorums. This resembles **multi-leader replication**, but conflicts can also arise during **read repair** or **hinted handoff**.

Conflicts occur because events may arrive in different orders at different nodes due to network delays or partial failures. For example, with two clients, A and B, writing to key X in a three-node cluster:

- Node 1 receives A but misses B.
    
- Node 2 receives A then B.
    
- Node 3 receives B then A.
    

If no resolution occurs, nodes become permanently inconsistent: node 2 might consider X = B, while nodes 1 and 3 see X = A.

To achieve **eventual consistency**, replicas must converge to the same value. However, most implementations handle this poorly, so developers must understand the database’s conflict-handling mechanisms to avoid data loss. Conflict resolution techniques, briefly mentioned earlier, are crucial in **leaderless** systems.

### Summary 

Replication serves several purposes:

- **High availability:** Keeps the system running even if machines or entire datacenters fail.
    
- **Disconnected operation:** Allows applications to function during network interruptions.
    
- **Latency:** Stores data closer to users for faster interactions.
    
- **Scalability:** Enables higher read volumes by using replicas.
    

Despite its apparent simplicity, replication is complex, requiring careful handling of concurrency, unavailable nodes, network interruptions, and potential faults like silent data corruption.

**Main approaches to replication:**

- **Single-leader replication:** All writes go to a single leader, which propagates changes to followers. Reads from followers may be stale.
    
- **Multi-leader replication:** Multiple leaders accept writes and propagate changes to each other and followers. Conflicts can occur.
    
- **Leaderless replication:** Clients write to and read from several nodes in parallel to detect and correct stale data.
    

Each approach has trade-offs: single-leader is simple and avoids conflicts; multi-leader and leaderless can be more robust but provide weaker consistency guarantees.

Replication can be **synchronous or asynchronous**, which affects behavior during faults. Asynchronous replication is fast but can risk data loss if a leader fails and a follower is promoted before catching up.

**Consistency models helpful under replication lag:**

- **Read-after-write:** Users always see their own submitted data.
    
- **Monotonic reads:** Users never see older data after seeing newer data.
    
- **Consistent prefix reads:** Users see data in a causally consistent order.
    

Multi-leader and leaderless replication introduce concurrency challenges. Conflicts may occur with concurrent writes, requiring mechanisms to determine the order of operations and merge updates.

## CHAPTER 6 Partitioning

we need to break the data up into partitions, also known as sharding.

Partitions are defined so that each piece of data (record, row, or document) belongs to exactly one partition. Each partition functions as a small database of its own, though the database may support operations that involve multiple partitions.

The main reason for partitioning data is **scalability**. Different partitions can be placed on different nodes in a shared-nothing cluster, allowing a large dataset to be distributed across many disks and the query load across many processors. Queries that operate on a single partition can be handled independently by each node, enabling query throughput to scale by adding more nodes. Large, complex queries can be parallelized across many nodes, though this is significantly more difficult.

### Partitioning and Replication

Partitioning is typically combined with replication so that copies of each partition are stored on multiple nodes for fault tolerance. Although each record belongs to exactly one partition, it may still exist on several nodes. A node can store multiple partitions.

In a leader–follower replication model, each partition’s leader is assigned to one node, and its followers are assigned to other nodes. Each node may act as the leader for some partitions and as a follower for others.

![[Pasted image 20251017171209.png]]

### Partitioning of Key-Value Data

Our goal with partitioning is to spread the data and the query load evenly across nodes. If every node takes a fair share, then—in theory—10 nodes should be able to handle 10 times as much data and 10 times the read and write throughput of a single node 

If the partitioning is unfair, so that some partitions have more data or queries than others, we call it skewed. The presence of skew makes partitioning much less effective. In an extreme case, all the load could end up on one partition, so 9 out of 10 nodes are idle and your bottleneck is the single busy node. A partition with disproportionately high load is called a hot spot.

The simplest approach for avoiding hot spots would be to assign records to nodes randomly. That would distribute the data quite evenly across the nodes, **==but it has a big disadvantage: when you’re trying to read a particular item, you have no way of knowing which node it is on, so you have to query all nodes in parallel.==**

#### Partitioning by Key Range

One method of partitioning is to assign continuous ranges of keys (from a minimum to a maximum) to each partition, similar to how volumes in an encyclopedia are organized. Knowing the range boundaries allows you to determine which partition holds a specific key. If you also know which node each partition resides on, you can directly send the request to the appropriate node.

![[Pasted image 20251017171359.png]]

**==The ranges of keys are not necessarily evenly spaced, because your data may not be evenly distributed.==**

The partition boundaries might be chosen manually by an administrator, or the database can choose them automatically Within each partition, we can keep keys in sorted order This has the advantage that range scans are easy, and you can treat the key as a concatenated index in order to fetch several related records in one query

**==The main drawback of key range partitioning is the risk of hot spots.==** For example, if keys are based on timestamps (such as one partition per day), all incoming writes will target the most recent partition, overloading it while others remain idle. To prevent this, the key design should avoid using the timestamp as the first element of the key.

#### Partitioning by Hash of Key

Because of this risk of skew and hot spots, many distributed datastores use a hash function to determine the partition for a given key.
A good hash function takes skewed data and makes it uniformly distributed. Say you have a 32-bit hash function that takes a string

For partitioning purposes, the hash function need not be cryptographically strong

Once you have a suitable hash function for keys, you can assign each partition a range of hashes (rather than a range of keys), and every key whose hash falls within a partition’s range will be stored in that partition

This technique is good at distributing keys fairly among the partitions. The partition boundaries can be evenly spaced, or they can be chosen pseudo randomly 

Unfortunately however, by using the hash of the key for partitioning we lose a nice property of key-range partitioning: the ability to do efficient range queries. Keys that were once adjacent are now scattered across all the partitions, so their sort order is lost. In MongoDB, if you have enabled hash-based sharding mode, any range query has to be sent to all partitions

#### Skewed Workloads and Relieving Hot Spots

In the extreme case where all reads and writes go to the same key, all requests will still be routed to a single partition, creating a hot spot. This scenario can occur, for example, on a social media platform where a celebrity’s activity triggers massive interaction. Hashing the key doesn’t solve this issue since identical keys always hash to the same value.

Most databases today cannot automatically handle such skewed workloads, so the application must manage it. One common solution is to split writes for a hot key across multiple derived keys—such as appending a random number or shard identifier. However, this creates new challenges: reads must now aggregate data from all derived keys, and additional bookkeeping is required to track which keys are being split. For most keys with low write traffic, this would be unnecessary overhead.

### Partitioning and Secondary Indexes

The partitioning schemes discussed so far depend on a key-value model, where each record is accessed through its primary key. In that case, determining the partition is straightforward—the key directly maps to a partition, allowing efficient routing of reads and writes.

However, things become more complex when **secondary indexes** are introduced. A secondary index doesn’t uniquely identify a single record; instead, it helps find all records that match a certain value—for example:

- finding all actions by a given user,
    
- finding all articles containing a specific word, or
    
- finding all cars with a certain color.
    

Secondary indexes are fundamental to relational databases and also common in document databases. While many key-value stores like **HBase** and **Voldemort** initially avoided secondary indexes due to their complexity, others like **Riak** have begun incorporating them because of their importance in data modeling. In systems like **``Solr``** and **Elasticsearch**, secondary indexes are the central design feature.

**==The problem with secondary indexes is that they don’t map neatly to partitions. There are two main approaches to partitioning a database with secondary indexes: document-based partitioning and term-based partitioning.==**

#### Partitioning Secondary Indexes by Document

In this approach, each partition maintains its own **secondary indexes**, indexing only the data stored within that partition. This setup is known as a **document-partitioned index** (or **local index**). Since each partition is independent, write operations—adding, updating, or removing a document—only affect the partition containing that document’s ID.

However, **reads** are more complex. Because related data (for example, all cars of the same color) might be spread across multiple partitions, a query like “find all red cars” must be sent to **all partitions**. Each partition returns partial results, which are then combined. This process is called **scatter/gather**, and while it allows parallel querying, it can significantly increase **read latency**, especially due to **tail latency amplification**.

Despite these drawbacks, the document-partitioned approach is common in distributed systems such as **MongoDB**, **Riak**, **Cassandra**, **Elasticsearch**, **SolrCloud**, and **VoltDB**. Database designers often try to choose partitioning schemes that let most secondary index queries be served from a single partition, though this is not always possible—particularly when multiple secondary indexes are involved in one query.

#### Partitioning Secondary Indexes by Term

Instead of giving each partition its own secondary index (**local index**), a database can use a **global index** that spans all partitions. However, this global index cannot reside on a single node—doing so would create a **bottleneck** and undermine the purpose of partitioning. Therefore, the global index must itself be **partitioned**, but in a different way from the primary key index.

This design is known as a **term-partitioned index**, where the **term** (such as `color:red`) determines which partition the index entry belongs to. The term “term” originates from full-text search systems, where it represents words found in documents.

The index can be partitioned either by the term itself or by a **hash of the term**:

- **Partitioning by term** allows **range scans** (e.g., for numeric fields like price).
    
- **Hash partitioning** helps **distribute load evenly** across nodes.
    

**==The main advantage of a global (term-partitioned) index is read efficiency: instead of broadcasting a query to all partitions (as in scatter/gather), the client can directly query the partition responsible for the desired term.**== 
==**The disadvantage is write complexity: a single document update may affect many index partitions, since each field or term might reside on a different node. This makes writes slower and more resource-intensive.==**

### Rebalancing

Over time, a database may need to adapt:

- **Increased query throughput** may require adding more CPUs.
    
- **Growing dataset size** may require adding more disks and RAM.
    
- **Machine failures** require other nodes to take over responsibilities.
    

These situations necessitate moving data and requests between nodes, a process called **rebalancing**.

Rebalancing generally aims to meet several requirements:

- **Fair load distribution:** After rebalancing, data storage and read/write requests should be evenly shared across nodes.
    
- **Continuous operation:** The database should continue accepting reads and writes during rebalancing.
    
- **Minimal data movement:** Only the necessary data should be moved to keep rebalancing fast and reduce network and disk I/O.

#### Strategies for Rebalancing

**How not to do it: hash mod ``NWhen`` partitioning by the **hash of a key**, the usual approach is to divide the hash space into ranges and assign each range to a partition.

==The problem with the **mod N** method is that when the number of nodes **N** changes, most keys must be moved to different nodes, causing significant data reshuffling.**==

**Fixed number of partitions**

A practical solution is to create **more partitions than nodes** and assign multiple partitions to each node.

When a new node is added, it can **steal partitions** from existing nodes until the load is balanced. Only entire partitions are moved—**keys remain in their original partitions**, and the total number of partitions does not change. During the transfer, the old partition assignment continues to handle reads and writes.

This approach also allows **accounting for hardware differences**: more powerful nodes can be assigned more partitions to take a larger share of the load.

Typically, the number of partitions is **fixed at setup** and not changed afterward. While splitting or merging partitions is possible, fixed partitions are operationally simpler. The initial number of partitions should be high enough to accommodate future growth, but not so high that management overhead becomes excessive.

Choosing the right partition size is tricky, especially if the dataset grows over time. Large partitions make **rebalancing and recovery** expensive, while very small partitions increase **management overhead**. Optimal performance occurs when partitions are sized “just right,” balancing these trade-offs.

**Dynamic partitioning**

With **fixed key-range partitions**, choosing the wrong boundaries can lead to **data skew**, where one partition holds all the data and others remain empty. Manually reconfiguring boundaries is tedious, so some databases use **dynamic partitioning**.

In systems like **HBase** and **RethinkDB**:

- When a partition exceeds a configured size (e.g., 10 GB in HBase), it is **split** into two roughly equal partitions.
    
- If a partition shrinks below a threshold due to deletions, it can be **merged** with an adjacent partition.  
    This behavior is similar to the **top-level operations in a B-tree**.
    

Each partition is assigned to a node, and nodes can manage multiple partitions. After a split, one of the new partitions can be **moved to another node** to balance the load. In HBase, this transfer happens via **HDFS**.

**==The advantage of dynamic partitioning is that the number of partitions adapts to the total data volume: few partitions when data is small, and controlled partition size when data is large.**==

==**The caveat is that a new, empty database starts with a single partition, so initially all writes go through one node while others remain idle.==**

**Partitioning proportionally to nodes**

With **dynamic partitioning**, the number of partitions grows with the dataset size, as splits and merges keep each partition’s size within a configured minimum and maximum.

With a **fixed number of partitions**, the partition size simply grows proportionally to the dataset size. In both cases, the number of partitions is **independent of the number of nodes**.

A third approach, used by **Cassandra** and **Ketama**, is to make the **number of partitions proportional to the number of nodes**—a fixed number of partitions per node. Here:

- The size of each partition grows with the dataset size if the node count is unchanged.
    
- Adding more nodes reduces the partition size, helping maintain a fairly **stable partition size** as the cluster scales.


#### Operations: Automatic or Manual Rebalancing

Rebalancing can be **automatic** or **manual**, with systems ranging along a spectrum between these extremes.

**Fully automatic rebalancing** is convenient because it reduces operational effort—partitions are moved between nodes without administrator intervention. However, it can be **unpredictable**:

- Rebalancing is **expensive**, involving rerouting requests and transferring large amounts of data.
    
- If not carefully managed, it can **overload the network or nodes**, impacting the performance of other operations.
    
- Automatic rebalancing combined with **automatic failure detection** can be particularly risky, as multiple changes may occur simultaneously.

### Request Routing

Once a dataset is partitioned across multiple nodes, clients need a way to locate the node responsible for a given key. This is a **service discovery** problem. As partitions move during rebalancing, something must keep track of the current assignment so clients know which node to contact.

There are three main approaches:

1. **Any-node contact** – Clients connect to any node (often via a round-robin load balancer). If the node owns the requested partition, it handles the request; otherwise, it forwards the request to the correct node and returns the response.
    
2. **Routing tier** – Clients send all requests to a dedicated routing layer that is partition-aware. The router forwards requests to the appropriate node but does not handle requests itself.
    
3. **Client-side awareness** – Clients know the partitioning scheme and the current assignment of partitions to nodes, allowing them to connect directly to the correct node without intermediaries.

![[Pasted image 20251017174350.png]]

Cassandra and Riak use a **gossip protocol** to share cluster state among nodes. Clients can send requests to any node, which then forwards them to the correct node for the partition (similar to approach 1). This shifts complexity to the database nodes but removes the need for an external coordination service like ZooKeeper.

Couchbase, on the other hand, **does not rebalance automatically**. It typically uses a routing tier called **moxi**, which learns about partition assignments from the cluster nodes.

Even with a routing tier or random-node requests, clients still need node IP addresses. Since these change slowly, **DNS is usually sufficient** for that purpose.

### Summary 

Partitioning aims to **evenly distribute data and query load** across nodes to avoid hot spots. Key points:

**Partitioning approaches:**

- **Key range partitioning:** Keys are sorted; each partition owns a range. Enables efficient range queries but can create hot spots. Usually handled dynamically by splitting large partitions.
    
- **Hash partitioning:** Keys are hashed; partitions own ranges of hashes. Spreads load more evenly but makes range queries inefficient. Fixed or dynamic partitions can be used.
    
- **Hybrid:** Part of the key determines the partition, part determines sort order.
    

**Secondary indexes:**

- **Document-partitioned (local):** Stored with primary data. Easy to update on writes but requires scatter/gather across partitions for reads.
    
- **Term-partitioned (global):** Partitioned by indexed values. Reads can hit a single partition, but writes may need to update multiple index partitions.
    

**Query routing:**

- Can range from simple partition-aware load balancing to parallel query execution.
    

**Caution:** Each partition operates mostly independently, so multi-partition writes can fail partially, making reasoning about consistency more difficult.

## CHAPTER 7 Transactions

**In the harsh reality of data systems, many things can go wrong:**

- Database software or hardware can fail anytime — even mid-write.
    
- Applications might crash during multi-step operations.
    
- Network interruptions can disconnect applications or database nodes.
    
- Multiple clients may write simultaneously, overwriting each other’s data.
    
- Clients might read partially updated or inconsistent data.
    
- Race conditions between clients can lead to unpredictable bugs.

A transaction groups multiple reads and writes into a single logical unit. Conceptually, all operations in a transaction execute as one:

- If successful → **commit**
    
- If something fails → **abort (rollback)**
    

This ensures that applications don’t have to deal with partial failures and can safely retry when errors occur.


Not every application requires transactions, and in some cases, relaxing or removing transactional guarantees can offer benefits like higher performance or availability. Certain safety properties can still be maintained without full transactions.

To determine whether transactions are necessary, it’s important to understand the specific **safety guarantees** they provide and the **costs** that come with them.

### The Slippery Concept of a Transaction

#### The Meaning of ACID

in practice, one database’s implementation of ACID does not equal another’s implementation.

**Atomicity**
In general, atomic refers to something that cannot be broken down into smaller parts

For example, in multi-threaded programming, if one thread performs an **atomic operation**, no other thread can observe a half-finished result. The system is either in the state before or after the operation — never in between.

In contrast, within the **ACID** context, atomicity isn’t about concurrency or multiple processes accessing the same data.

==**Rather, ACID atomicity describes what happens if a client wants to make several writes, but a fault occurs after some of the writes have been processed.**==

If these writes are grouped into an atomic transaction and the transaction cannot be completed (committed) due to a fault, the database **aborts the transaction** and **discards or rolls back** any partial changes made so far.

The ability to abort a transaction on error and have all writes from that transaction discarded is the defining feature of ACID atomicity.

**Consistency**

The idea of **ACID consistency** is that certain statements about the data—called **invariants**—must always hold true. For example, in an accounting system, **total credits and debits must always balance**.

If a transaction begins with a valid database state and its operations preserve these invariants, the database remains consistent. However, this concept of consistency depends entirely on the **application’s logic**. It’s the **application’s responsibility** to design transactions that maintain validity.

==**Atomicity, isolation, and durability are properties of the database, whereas consistency (in the ACID sense) is a property of the application.**==

**Isolation**

Most databases handle requests from multiple clients simultaneously. This works fine when clients read and write to **different parts** of the database. However, when they access the **same records**, **concurrency issues** can arise.

**Isolation** in the context of ACID ensures that concurrently running transactions **don’t interfere** with each other. In database theory, this is formalized as **serializability**, meaning each transaction behaves **as if it were the only one** running on the database.

The database guarantees that once all transactions are committed, the **final result** is the same as if they had executed **one after another** (serially).

**Durability**

The purpose of a database system is to provide a **safe place** to store data without the risk of losing it.

**Durability is the promise that once a transaction has committed successfully, any data it has written will not be forgotten, even if there is a hardware fault or the database crashes.**

In a **single-node database**, durability means data is written to **nonvolatile storage** (like HDDs or SSDs) and often recorded in a **write-ahead log (WAL)** for recovery if corruption occurs.

In a **replicated database**, durability means the data has been **copied to multiple nodes**. To ensure this guarantee, the database must **wait until all writes or replications complete** before confirming a transaction as successfully committed.

#### Single-Object and Multi-Object Operations

Multi-object transactions need a mechanism to identify which read and write operations belong to the same transaction. In **relational databases**, this is usually tied to the client’s **TCP connection** — everything between `BEGIN TRANSACTION` and `COMMIT` is treated as one transaction.

In contrast, many **nonrelational databases** lack such grouping mechanisms. Even if they support multi-object operations (like a key-value store’s `multi-put`), these do not always ensure full transaction semantics — some writes may succeed while others fail, leaving partial updates.

**Single-object writes** still rely on **atomicity** and **isolation**. Most storage engines ensure this by:

- Using **logs** for crash recovery (atomicity)
    
- Using **locks** to prevent concurrent access (isolation)
    

Some databases extend this with operations like **increment** or **compare-and-set**, which eliminate the need for a full read-modify-write cycle and help prevent **lost updates** when multiple clients write to the same object.

However, these **single-object operations are not true transactions**. While sometimes marketed as “lightweight transactions” or even “ACID,” this is misleading — genuine transactions group **multiple operations on multiple objects** into a single, atomic unit of work.


**The need for multi-object transactions**

Multi-object transactions are challenging to implement across partitions and can sometimes hinder systems that require extremely high availability or performance. Still, there’s **no fundamental barrier** to having transactions in a distributed database — implementations of **distributed transactions** are discussed in Chapter 9.

But do we really need multi-object transactions? Could every application be built using only a **key-value model** with **single-object operations**?

While some cases work fine with single-object inserts, updates, or deletes, many real-world scenarios require **coordinated writes** across multiple objects:

- In a **relational model**, a row in one table often references another via a **foreign key**. Multi-object transactions ensure these references remain valid — when inserting or updating related records, the foreign keys must be consistent or the data becomes meaningless.
    
- In a **document model**, fields that need to change together usually reside within one document (a single object), so transactions may not be necessary. However, since document databases often encourage **denormalization**, updating duplicated information across documents requires multi-object transactions to avoid inconsistencies.
    
- In **databases with secondary indexes**, every update must also modify the related indexes — separate database objects from a transaction’s perspective. Without transaction isolation, you might see a record appear in one index but not another.
    

Applications **can** be built without transactions, but doing so makes **error handling complex** and introduces **concurrency risks** due to the absence of atomicity and isolation.**

**Handling errors and aborts**

A key feature of a transaction is that it can be **aborted and safely retried** if an error occurs. ACID databases follow this principle: if executing a transaction risks violating **atomicity, isolation, or durability**, the database will **abort the transaction** rather than leave it half-finished.

However, this retry mechanism has limitations:

- If the transaction actually succeeded but the **network failed** while acknowledging the commit, retrying may **perform the transaction twice**, unless you have **application-level deduplication**.
    
- If the error is due to **overload**, retrying can worsen the problem. To prevent feedback loops, use **retry limits**, **exponential back off**, and differentiate **overload errors** from other transient errors.
    
- Retry is only useful for **transient errors** (e.g., deadlocks, isolation violations, temporary network interruptions). For **permanent errors** (like constraint violations), retrying is pointless.
    
- Transactions with **side effects outside the database** may still execute those effects even if aborted. For instance, sending an email should not repeat on every retry.
    
- If you need multiple systems to **commit or abort together**, **two-phase commit** can help coordinate them.
    
- If the **client process fails** during retry, any data it was writing may be lost.

### Weak Isolation Levels

If two transactions access **different data**, they can safely run in parallel, since neither depends on the other. **Concurrency issues** (race conditions) only arise when one transaction reads data being modified by another, or when two transactions try to **modify the same data simultaneously**.

These bugs are difficult to detect through testing because they depend on unlucky timing.

To address this, databases provide **transaction isolation**, which aims to **hide concurrency from the application**. In theory, **serializable isolation** ensures transactions behave **as if they ran one at a time**, without interference.

In practice, full serializable isolation comes with a **performance cost**, so many databases use **weaker isolation levels**. These protect against some concurrency issues but not all, making them **harder to reason about** and prone to subtle bugs.

Weak isolation has real-world consequences: it has **caused financial losses, auditor investigations, and data corruption**. While ACID databases are recommended for financial data, many popular relational systems use **weaker isolation by default**, so ACID compliance alone doesn’t always prevent concurrency bugs.

#### Read Committed

The **most basic level** of transaction isolation is **read committed**. It provides two guarantees:

1. When reading, you only see **committed data** (**no dirty reads**).
    
2. When writing, you only overwrite **committed data** (**no dirty writes**).
    

**No dirty reads**  
==**Imagine a transaction has written some data to the database, but the transaction has not yet committed or aborted. Can another transaction see that uncommitted data? If yes, that is called a dirty read.**==

Transactions at the **read committed** level prevent dirty reads by making sure **writes only become visible after the transaction commits**.

There are a few reasons why it’s useful to prevent dirty reads:

• If a transaction needs to update several objects, a dirty read means that another transaction may see some of the updates but not others
• If a transaction aborts, any writes it has made need to be rolled back

**No dirty writes**

What happens if two transactions try to update the same object concurrently? Normally, the later write **overwrites the earlier write**.

==**However, what happens if the earlier write is part of a transaction that has not yet committed, so the later write overwrites an uncommitted value? This is called a dirty write.**==

Transactions at the **read committed** level prevent dirty writes, typically by **delaying the second write** until the first transaction has either **committed or aborted**.

By preventing dirty writes, this isolation level avoids some concurrency problems:

- If transactions update multiple objects, dirty writes can cause incorrect results.
    
- However, read committed **does not prevent race conditions**, such as two counter increments happening sequentially after the first transaction commits — it’s still incorrect, but for a different reason.

#### Snapshot Isolation and Repeatable Read

If you look superficially at **read committed** isolation, you might think it handles all transactional needs: it allows **aborts** (for atomicity), prevents reading incomplete transaction results, and stops concurrent writes from intermingling. These are useful features and stronger than a system without transactions.

However, there are still many ways **concurrency bugs** can occur at this isolation level.

==**This anomaly is called a nonrepeatable read or read skew:** if Alice reads the balance of account 1 again later in the transaction, she might see a different value ($600) than before. Read skew is **acceptable under read committed** — the balances Alice saw were indeed committed at the time of her read.==

**Backups**  
Taking a backup requires copying the entire database, which can take hours. During this time, **writes continue**, so some parts of the backup may have **older data** while others have **newer data**. Restoring from such a backup can create **permanent inconsistencies** (e.g., disappearing money).

**Analytic queries and integrity checks**  
Queries that scan large portions of the database — common in **analytics** or **periodic integrity checks** — may return **nonsensical results** if they see parts of the database at different times.

==**Snapshot isolation** is the most common solution. Each transaction reads from a **consistent snapshot** of the database, seeing all data **committed at the start of the transaction**, even if other transactions modify data later.==

#### Preventing Lost Updates

The **read committed** and **snapshot isolation** levels discussed so far focus mainly on **what read-only transactions see** during concurrent writes. They don’t fully address **concurrent writes** themselves.

One common conflict between concurrently writing transactions is the **lost update problem**.

The **lost update problem** occurs when an application performs a **read-modify-write cycle**: it reads a value, modifies it, and writes it back. If two transactions do this at the same time, one modification can be **overwritten** by the other, causing a lost update. Examples include:

- Incrementing a **counter** or updating an **account balance**
    
- Making a local change to a **complex value** (e.g., adding an element to a JSON list)
    
- Two users editing a **wiki page** simultaneously, each sending the full page back
    

To prevent this, many databases offer **atomic write operations**, eliminating the need for manual read-modify-write cycles in application code. These operations are often the most effective solution when your logic can be expressed using them.

**Atomic write operations**

Many databases offer **atomic update operations**, which eliminate the need for manual **read-modify-write cycles** in application code. These are often the best solution when your logic can be expressed using them. For example, this instruction is **concurrency-safe** in most relational databases:

```sql
UPDATE counters SET value = value + 1 WHERE key = 'foo';
```

Atomic operations are typically implemented by taking an **exclusive lock** on the object when it’s read, preventing other transactions from accessing it until the update completes. This technique is sometimes called **cursor stability**.

Alternatively, some systems ensure atomicity by executing all such operations on a **single thread**.

**Explicit locking**

If built-in atomic operations aren’t sufficient, an application can **explicitly lock objects** before updating them. This allows a safe **read-modify-write cycle**: any other transaction attempting to access the locked object must wait until the first transaction completes.

Example in SQL:

```sql
BEGIN TRANSACTION;
SELECT * FROM figures
WHERE name = 'robot' AND game_id = 222
FOR UPDATE;
-- Check whether move is valid, then update the piece
UPDATE figures SET position = 'c4' WHERE id = 1234;
COMMIT;
```

The `FOR UPDATE` clause instructs the database to **lock all rows** returned by the query.

This approach works, but it requires **careful application design**. Missing a necessary lock can easily introduce **race conditions**.

**Automatically detecting lost updates**

Instead of preventing lost updates with **atomic operations** or **locks**, another approach is to let read-modify-write cycles run **in parallel** and detect conflicts afterward. If a lost update is detected, the transaction is **aborted** and must **retry** its cycle.

This method works efficiently with **snapshot isolation**. For example, PostgreSQL’s **repeatable read**, Oracle’s **serializable**, and SQL Server’s **snapshot isolation** automatically detect lost updates and abort the conflicting transaction.

**Compare-and-set**

In databases without full transaction support, an **atomic compare-and-set (CAS)** operation can help prevent **lost updates**. The update only occurs if the current value matches what was previously read. If it doesn’t match, the update fails, and the **read-modify-write cycle must be retried**.

Example: preventing two users from concurrently updating the same wiki page:

```sql
-- May or may not be safe depending on the database
UPDATE wiki_pages SET content = 'new content'
WHERE id = 1234 AND content = 'old content';
```

If the content no longer matches `'old content'`, the update has no effect, so the application must **check the result** and **retry if necessary**.

However, this approach can fail if the database reads from an **old snapshot**, because the condition may appear true even while another write is happening, failing to prevent lost updates.

#### Write Skew and Phantoms

**Characterizing write skew**

This anomaly is called **write skew**. Unlike a dirty write or lost update, it occurs when **two transactions update different objects** (e.g., Alice’s and Bob’s on-call records). It’s a **race condition**: if the transactions had run sequentially, the second doctor would have been prevented from going off call. The anomaly only arises because the transactions run **concurrently**.

Write skew can be seen as a generalization of the **lost update problem**. It happens when two transactions **read the same objects** but then update **different objects**. If they update the same object, it degenerates into a **dirty write** or **lost update**.

Preventing write skew is harder than preventing lost updates:

- **Atomic single-object operations** don’t help, since multiple objects are involved.
    
- **Automatic lost-update detection** in some snapshot isolation implementations doesn’t catch write skew (e.g., PostgreSQL repeatable read, MySQL/InnoDB repeatable read, Oracle serializable, SQL Server snapshot isolation). Preventing write skew requires **true serializable isolation**.
    
- Some databases allow **constraints** (uniqueness, foreign keys, value restrictions), but multi-object constraints like “at least one doctor must be on call” usually require **triggers or materialized views**.
    
- If serializable isolation isn’t available, the next best solution is **explicitly locking rows** the transaction depends on. Example:
    

```sql
BEGIN TRANSACTION;
SELECT * FROM doctors
WHERE on_call = true
AND shift_id = 1234
FOR UPDATE;
UPDATE doctors
SET on_call = false
WHERE name = 'Alice'
AND shift_id = 1234;
COMMIT;
```

Here, `FOR UPDATE` locks all selected rows, preventing concurrent modifications that could cause write skew.

**Phantoms causing write skew**

Many write skew examples follow this pattern:

1. A `SELECT` query checks whether a condition is satisfied (e.g., at least two doctors on call, no existing bookings for a room, a board position is empty, the username is available, or there is sufficient account balance).
    
2. Based on the result, the application decides how to proceed — either performing the operation or aborting with an error.
    
3. If proceeding, the application performs a **write** (`INSERT`, `UPDATE`, or `DELETE`) and commits the transaction.
    

==**The effect of this write changes the precondition of the decision in step 2. In other words, if you were to repeat the SELECT query from step 1 after committing the write, you would get a different result, because the write changed the set of rows matching the search condition.**==

**Materializing conflicts**

If **phantoms** occur because there’s no object to lock, one solution is to **introduce an artificial lock object** in the database.

For example, a transaction creating a booking can `SELECT FOR UPDATE` the rows corresponding to the desired **room and time period**. Once the locks are acquired, it can check for overlapping bookings and insert the new booking. The extra table is **not used to store booking data**, only to enforce locking.

This method is called **materializing conflicts**, as it converts a phantom into a **lock conflict** on actual database rows. However, it can be **difficult and error-prone** to implement correctly and requires **exposing concurrency control** in the application’s data model, which is generally considered undesirable.

### Serializability

Serializable isolation is usually regarded as the strongest isolation level. It guarantees that even though transactions may execute in parallel, the end result is the same as if they had executed one at a time, serially, without any concurrency. Thus, the database guarantees that if the transactions behave correctly when run individually, they continue to be correct when run concurrently—**==in other words, the database prevents all possible race conditions==**

#### Actual Serial Execution

The simplest way of avoiding concurrency problems is to remove the concurrency entirely: to execute only one transaction at a time, in serial order, on a single thread. By doing so, we completely sidestep the problem of detecting and preventing conflicts between transactions: the resulting isolation is by definition serializable

 A system designed for single-threaded execution can sometimes perform better than a system that supports concurrency, because it can avoid the coordination overhead of locking. However, its throughput is limited to that of a single CPU core. In order to make the most of that single thread, transactions need to be structured differently from their traditional form

**Encapsulating transactions in stored procedures**

systems with single-threaded serial transaction processing don’t allow interactive multi-statement transactions. Instead, the application must submit the entire transaction code to the database ahead of time, as a stored procedure

**Pros and Cons of Stored Procedures**

Stored procedures have been part of relational databases for decades and standardized in **SQL/PSM (since 1999)**. While powerful, they come with a mixed reputation due to several drawbacks:

**Cons:**

- Every database vendor has its **own stored procedure language** (PL/SQL, T-SQL, PL/pgSQL, etc.), which are **outdated**, verbose, and lack modern **language features and ecosystems**.
    
- Code inside the database is **harder to manage** — it’s difficult to debug, version control, deploy, test, and monitor compared to application code.
    
- The **database is a shared and performance-sensitive resource**. Poorly written stored procedures (e.g., high CPU or memory use) can degrade performance for all users.
    

**Pro:**  
Despite the drawbacks, with **stored procedures and in-memory data**, it becomes **feasible to execute all transactions on a single thread**, improving consistency and potentially reducing contention.

**Partitioning**

Executing all transactions serially greatly simplifies **concurrency control**, but it also limits throughput to **a single CPU core on one machine**. While **read-only transactions** can still run elsewhere using **snapshot isolation**, applications with **high write throughput** can quickly hit a bottleneck — the single-threaded transaction processor becomes the limiting factor.

**Summary of Serial Execution**  
Serial execution offers a practical path to achieving **serializable isolation**, but only under strict constraints:

- Each **transaction must be small and fast**, since a single slow transaction blocks all others.
    
- The **active dataset must fit in memory**; infrequently accessed data can reside on disk but will slow down single-threaded processing if accessed.
    
- **Write throughput** must be low enough for a single CPU core, or transactions must be **partitioned** to distribute the load without requiring cross-partition coordination.
    
- **Cross-partition transactions** are possible but inherently limited — they reduce the scalability benefits of partitioning.

### Two-Phase Locking (2PL)

Two-phase locking works similarly to other locking mechanisms but enforces **much stricter rules**. It allows **multiple transactions to read** the same object concurrently **as long as no one is writing** to it. However, once a transaction wants to **modify or delete** an object, it requires **exclusive access**:

- If **Transaction A** has **read** an object and **Transaction B** wants to **write** to it, **B must wait** until **A commits or aborts**.  
    _(This prevents B from changing the object behind A’s back.)_
    
- If **Transaction A** has **written** an object and **Transaction B** wants to **read** it, **B must also wait** until **A commits or aborts**.  
    _(Unlike snapshot isolation, reading an old version is not allowed under 2PL.)_
    

In **two-phase locking**, **writers block readers** and **readers block writers** — a strict mutual exclusion.  
By contrast, **snapshot isolation** follows the mantra:

> _“Readers never block writers, and writers never block readers.”_

This distinction is key: while **2PL** can reduce concurrency due to blocking, it also provides **true serializability**, protecting against **all race conditions** — including **lost updates** and **write skew**.

**Implementation of two-phase locking**

In **two-phase locking**, concurrency control is enforced through **locks** on each object in the database.  
Each lock can be held in one of two modes:

- **Shared mode (S-lock)** → allows **reading**
    
- **Exclusive mode (X-lock)** → allows **writing**
    

Here’s how it works:

- 🔹 **Reading an object:**
    
    - The transaction must first **acquire a shared lock (S-lock)**.
        
    - **Multiple transactions** can hold shared locks on the same object **at the same time**,  
        but if **any transaction already holds an exclusive lock**, others must **wait**.
        
- 🔹 **Writing an object:**
    
    - The transaction must **acquire an exclusive lock (X-lock)**.
        
    - **No other transaction** can hold a lock (shared or exclusive) on that object at the same time.
        
    - If there is an existing lock, the writer must **wait**.
        
- 🔹 **Read → Write upgrade:**
    
    - If a transaction first **reads** and later wants to **write** the same object,  
        it must **upgrade its shared lock to an exclusive lock**, following the same waiting rules.
        
- 🔹 **Two phases of locking:**
    
    - **Phase 1 (Growing phase):** Locks are **acquired** as needed during execution.
        
    - **Phase 2 (Shrinking phase):** Locks are **released** only at the **end of the transaction** (commit or abort).
        

This strict acquire-then-release pattern is what gives **two-phase locking** its name —  
and it’s essential to guarantee **serializability** by preventing conflicting interleavings of reads and writes.

### Serializable Snapshot Isolation (SSI)

**Pessimistic vs. Optimistic Concurrency Control**

**Two-phase locking (2PL)** is a **pessimistic concurrency control** mechanism —  
it assumes that conflicts _will_ happen, so it prevents them in advance by making transactions wait.  
If something _might_ go wrong (for example, another transaction holds a conflicting lock),  
the transaction pauses until it’s safe to proceed.  
It’s similar to using **mutual exclusion** in multi-threaded programming.

**Serial execution** represents the extreme form of pessimism:  
it’s as if each transaction held an **exclusive lock on the entire database** (or partition)  
for its entire duration. The pessimism is offset by making transactions **very short and fast**,  
so they hold the "global lock" only briefly.

By contrast, **serializable snapshot isolation (SSI)** uses an **optimistic concurrency control** approach.  
Here, transactions **don’t block** even if potential conflicts might occur.  
Instead, they proceed **optimistically**, assuming everything will work out.  
When a transaction tries to **commit**, the database **checks** whether conflicts actually happened.  
If a violation is detected, the transaction is **aborted and retried** —  
only transactions that can be serialized are allowed to commit.

Optimistic concurrency control is a **well-established technique [52]**  
with long-debated trade-offs [53]:

- ⚠️ **Disadvantage:** Performs poorly under **high contention**,  
    because many transactions may need to abort and retry.  
    In high-load situations, retries add even more pressure to the system.
    
- ✅ **Advantage:** Performs **better under low contention**,  
    especially when there’s **spare capacity**, since transactions rarely need to block.
    

> Contention can often be reduced by using **commutative atomic operations**,  
> which allow multiple transactions to proceed safely without interfering with one another.


**Decisions based on an outdated premise**

A common cause of serialization anomalies occurs when a transaction makes a decision based on data that was **true at the start**, but **no longer valid** by the time it tries to commit.

For example, a transaction might act on the premise:

> “There are currently two doctors on call.”

If, during the course of the transaction, another doctor goes off call, the **premise becomes outdated**, yet the transaction may still proceed with actions that are now invalid.

When the application queries the database (e.g., _“How many doctors are currently on call?”_),  
the **database has no knowledge of how that result is used** by the application’s logic.  
To guarantee **serializable isolation**, the database must therefore **assume** that  
any change in the query result — any alteration to the underlying data —  
means the transaction’s writes might be based on **stale or invalid premises**.

Thus, to remain correct, the database must **detect and abort** transactions that may have acted on outdated information.

There are **two key cases** the database must detect:

1. **Detecting reads of stale MVCC versions** —  
    when an **uncommitted write** happened **before** the transaction’s read,  
    meaning the transaction observed outdated data.
    
2. **Detecting writes that affect prior reads** —  
    when a **write** by another transaction **occurs after** a read,  
    invalidating the earlier read’s assumption.
    

These mechanisms ensure that the system can recognize when a transaction’s logic depends on **obsolete facts** and prevent committing results that would break **serializability**.

### Summary

### Purpose of Transactions

- Transactions act as an abstraction layer that hides concurrency issues and system faults (crashes, network errors, power failures, etc.).
    
- Instead of handling complex errors, the application only needs to retry after an abort.
    
- For simple single-record operations, transactions may be unnecessary, but for complex access patterns they are extremely valuable.
    

---

### Common Concurrency Problems and Their Prevention

|Problem|Description|Prevented by|
|---|---|---|
|**Dirty Reads**|Reading another transaction’s uncommitted data|Read Committed or stronger|
|**Dirty Writes**|Overwriting data written by an uncommitted transaction|Almost all implementations|
|**Read Skew (Nonrepeatable Reads)**|Seeing different parts of the database at different times|Snapshot Isolation (MVCC)|
|**Lost Updates**|Two transactions overwrite each other’s changes|Snapshot Isolation (sometimes requires explicit locking)|
|**Write Skew**|Acting on an outdated premise|Only Serializable Isolation|
|**Phantom Reads**|Results of a query change due to concurrent writes|Snapshot Isolation (partially), Serializable with index-range locks|

---

### Isolation Levels

- Weak isolation levels prevent only a subset of anomalies; developers must handle others manually.
    
- Only **Serializable isolation** protects against all concurrency issues.
    

---

### Implementations of Serializable Transactions

1. **Serial Execution**
    
    - Transactions run one at a time in order.
        
    - Simple and reliable if transactions are short and system load is low.
        
2. **Two-Phase Locking (2PL)**
    
    - Pessimistic approach using shared/exclusive locks.
        
    - Strong consistency but lower performance due to blocking.
        
3. **Serializable Snapshot Isolation (SSI)**
    
    - Optimistic approach allowing transactions to run without blocking.
        
    - Checked at commit; non-serializable transactions are aborted.
        
    - Modern and efficient for systems with moderate contention.
        

---

### Key Points

- Transactions simplify reasoning about concurrency and failures.
    
- Each isolation level has trade-offs between safety and performance.
    
- **Serializable isolation** ensures full correctness.
    
- **SSI** is the preferred modern approach for combining safety and good performance.
    


## CHAPTER 8 The Trouble with Distributed Systems

Working with distributed systems is fundamentally different from writing software on a single computer—and the main difference is that there are lots of new and exciting ways for things to go wrong

### Faults and Partial Failures

An individual computer with good software is usually either fully functional or entirely broken, but not something in between. This is a deliberate choice in the design of computers: if an internal fault occurs, we prefer a computer to crash completely rather than returning a wrong result, because wrong results are difficult and confusing to deal with.

When you are writing software that runs on several computers, connected by a network, the situation is fundamentally different. In distributed systems, we are no longer operating in an idealized system model—we have no choice but to confront the messy reality of the physical world. And in the physical world, a remarkably wide range of things can go wrong

**==In a distributed system, there may well be some parts of the system that are broken in some unpredictable way, even though other parts of the system are working fine. This is known as a partial failure. The difficulty is that partial failures are nondeterministic==**

#### Cloud Computing and Supercomputing

• High-performance computing (HPC) involves supercomputers with thousands of CPUs used for heavy computational tasks like weather forecasting or molecular simulations.  
• Cloud computing sits at the other extreme—using large-scale datacenters with commodity hardware, IP-based networking, elastic resource allocation, and pay-per-use billing.  
• Traditional enterprise datacenters fall between these two extremes.  
• Fault handling differs significantly:

- In HPC, systems use **checkpointing** (saving computation state to durable storage).
    
- If a node fails, the cluster often stops entirely, waits for repairs, and then **restarts from the last checkpoint**.

If we want to make distributed systems work, we must accept the possibility of partial failure and build fault-tolerance mechanisms into the software. In other words, we need to build a reliable system from unreliable components

### Unreliable Networks

• **Shared-nothing architecture**: Each machine has its own memory and disk; communication happens only via the network.  
• Dominant for internet services due to **low cost**, **use of commodity cloud hardware**, and **high reliability through redundancy**.  
• Networks (like Ethernet) are **asynchronous** — messages may be delayed, lost, or duplicated.  
• Possible issues when sending a request:

- Request lost or delayed.
    
- Remote node crashed or paused.
    
- Response lost or delayed on the way back.

The usual way of handling this issue is a timeout: after some time you give up waiting and assume that the response is not going to arrive. However, when a timeout occurs, you still don’t know whether the remote node got your request or not (and if the request is still queued somewhere, it may still be delivered to the recipient, even if the sender has given up on it).

#### Network Faults in Practice

Handling network faults doesn’t necessarily mean tolerating them: if your network is normally fairly reliable, a valid approach may be to simply show an error message to users while your network is experiencing problems. However, you do need to know how your software reacts to network problems and ensure that the system can recover from them

#### Detecting Faults

• Systems often need to **detect faulty nodes** automatically:

- Load balancers remove dead nodes from rotation.
    
- Distributed databases promote a follower if the leader fails.
    

• **Network uncertainty** makes fault detection difficult — you can’t always tell if a node is dead or just slow.

• Sometimes, **explicit feedback** helps:

- OS may send a **RST/FIN** if the process crashed but the host is reachable.
    
- Monitoring scripts can notify others when a process crashes.
    

• However, you **can’t rely** on such signals — a node may crash **after** acknowledging a message.  
→ To be certain a request succeeded, you need a **positive confirmation** from the application itself.

#### Timeouts and Unbounded Delays

Timeouts are the main way to detect node failures, but choosing the right duration is tricky.  
A **long timeout** delays fault detection, causing users to wait longer or see errors.  
A **short timeout** reacts faster but risks **false positives**—declaring a node dead when it’s just slow due to temporary load or network issues.

Prematurely marking a node as dead can lead to duplicated actions (e.g., an email being sent twice) and increases stress on other nodes that take over its work.  
If the system is already under high load, this can trigger a **cascading failure**, where overloaded nodes continually declare each other dead until the entire system fails.

**Network congestion and queueing**

Just like cars face traffic jams, data packets experience **delays due to congestion and queueing** in networks. The main causes are:

- When multiple nodes send packets to the same destination, the **network switch queues them**, leading to **delays or packet drops** if the queue overflows.
    
- At the destination, if all CPU cores are busy, **incoming packets are queued by the OS** until the application can handle them.
    
- In **virtualized environments**, a paused VM cannot process network data, causing **buffering and delay**.
    
- **TCP flow control** slows down sending rates to prevent overload, and **retransmits lost packets** after a timeout—making the network appear reliable to the application but increasing overall delay.
    

In short, most variability in network latency stems from **queueing, congestion, and retransmission delays**, not from total network failure.


#### Synchronous Versus Asynchronous Networks

Distributed systems would be far easier to build if networks always delivered packets on time and never dropped them.  
However, **networks can’t guarantee reliability at the hardware level** because doing so would be too rigid and inefficient for modern, shared environments.

In traditional **telephone networks**, a call establishes a **dedicated circuit**—a fixed bandwidth reserved for the entire duration of the call.  
By contrast, **datacenter and internet networks use packet switching**, where packets dynamically share network links. This allows **efficient resource use** and supports **millions of concurrent connections**, but it also introduces **unpredictable delays, congestion, and packet loss**.

**Can we not simply make network delays predictable?**

Why do datacenter networks and the internet use packet switching? The answer is that they are optimized for bursty traffic. A circuit is good for an audio or video call, which needs to transfer a fairly constant number of bits per second for the duration of the call. On the other hand, requesting a web page, sending an email, or transferring a file doesn’t have any particular bandwidth requirement—we just want it to complete as quickly as possible.

### Unreliable Clocks

Clocks are central to many application functions — from measuring performance to scheduling and logging.  
They help answer questions like:

- Has a request timed out?
    
- How long did a user stay on the site?
    
- When should a reminder or cache expire?
    

In distributed systems, **time becomes complex** because:

- **Message delays vary** — a message is always received later than sent, but by an unknown amount.
    
- **Each machine has its own imperfect clock**, driven by quartz oscillators that drift over time.
    

As a result, it’s hard to **determine the exact order of events across machines**, making coordination and consistency in distributed systems more challenging.

#### Monotonic Versus Time-of-Day Clocks

Modern computers have two main types of clocks:

**Time-of-day clocks**

- Show the _current calendar time_ (e.g., via `System.currentTimeMillis()` or `CLOCK_REALTIME`).
    
- Synchronized via **NTP** so timestamps are comparable across machines.
    
- Can **jump backward or forward** (e.g., during NTP adjustments or leap seconds).
    
- Not reliable for measuring durations or timeouts.
    

**Monotonic clocks**

- Measure **elapsed time** or durations (e.g., `System.nanoTime()`, `CLOCK_MONOTONIC`).
    
- **Never move backward**, making them ideal for measuring performance, delays, and timeouts.
    
- Not tied to real-world dates — only to the passage of time.

#### Relying on Synchronized Clocks

Clock problems are often **hard to detect** because most systems continue functioning normally even when their clocks drift. Unlike CPU or network failures, faulty or misconfigured clocks don’t usually cause crashes — they cause **subtle data inconsistencies or corruption** instead.

Therefore, systems that rely on synchronized clocks must:

- **Continuously monitor clock offsets** between nodes.
    
- **Remove or isolate nodes** whose clocks drift too far from the cluster’s consensus.
    

This proactive monitoring prevents hidden time drift from silently damaging data or coordination logic.

#### Process Pauses

This example illustrates the pitfalls of **lease-based leader election** in distributed systems:

- **Reliance on synchronized clocks:** The lease expiry is based on a remote node’s clock. If clocks drift significantly, a node may incorrectly believe it still holds the lease or has already lost it, causing **split-brain behavior**.
    
- **Assumption of uninterrupted execution:** The code assumes negligible delay between checking the lease and processing a request. Unexpected pauses (e.g., garbage collection, CPU scheduling, or overload) could allow the lease to expire mid-processing, leading to **concurrent leadership** or lost requests.
    

Key takeaway: lease-based leadership must account for **clock uncertainty** and **unpredictable execution pauses** to avoid correctness issues.

In distributed systems, unexpected pauses in a node’s execution—due to scheduling, garbage collection, or other system events—are a major source of complexity:

- A node can be **paused at any moment** and resume later without noticing, similar to arbitrary thread preemption in multi-threaded programs.
    
- Unlike on a single machine, traditional concurrency tools (mutexes, semaphores, atomic operations) **don’t apply**, because distributed systems lack shared memory—nodes communicate only via messages.
    
- During a pause, the rest of the system continues operating and may **declare the paused node dead**, potentially causing duplicate work or leadership conflicts.
    
- When the node resumes, it may be unaware of what it missed until it consults its clock, making **timing assumptions unsafe**.
    

Key point: distributed nodes must **always assume arbitrary pauses and message delays** when designing protocols.

### Knowledge, Truth, and Lies

In distributed systems, nodes **cannot know the true state of other nodes**—they can only make inferences based on messages received (or not received).

- A lack of response does not distinguish between **network failures** and **node failures**.
    
- Nodes rely entirely on communication to infer state, which makes uncertainty inherent.
    

The solution is to **define a system model**:

- Explicitly state the assumptions about node behavior, message delivery, and timing.
    
- Design algorithms that are **provably correct within that model**, ensuring reliable behavior even under uncertainty.
    

Key idea: correctness in distributed systems comes from **designing for the assumptions you make**, not from eliminating uncertainty entirely.

#### The Truth Is Defined by the Majority

In distributed systems, a single node **cannot be fully trusted**—it may fail or be isolated, leaving the system unable to make correct decisions on its own.

- Many algorithms rely on a **quorum** (a minimum number of nodes agreeing) to make decisions, including declaring nodes dead.
    
- Typically, a **majority quorum** is used, ensuring the system can tolerate some node failures while maintaining safety (no conflicting decisions).
    

**Leader and Lock Principles:**

- Only one node should be the leader for a partition to avoid **split-brain**.
    
- Only one transaction or client should hold a lock on a resource to prevent concurrent writes.
    
- Only one user should hold a unique identifier (e.g., username).
    

**Key challenge:**  
Even if a node believes it is “the chosen one,” the **quorum may have elected a different leader** due to network issues or pauses. Acting without quorum approval can lead to **incorrect system behavior**, as other nodes may act on conflicting information.

**Takeaway:** distributed coordination relies on **majority agreement**, not individual node judgment.

**Fencing tokens**

A way to prevent a node that lost a lock or lease from continuing to write is to use **fencing tokens**:

- Every time the lock server grants a lock or lease, it returns a **fencing token**, which increases monotonically.
    
- Clients must include this token in **every write request** to the storage service.
    
- The **resource itself** must check the token, rejecting any write with an older token than what has already been processed.
    

Key points:

- Clients cannot enforce this themselves; the resource must actively validate tokens.
    
- For systems without native fencing token support, workarounds like embedding the token in a filename can be used, but some form of **token checking** is essential to prevent unauthorized writes.

#### Byzantine Faults

Fencing tokens help **prevent accidental misbehavior** by blocking nodes that act after their lease expires.

However, they **cannot stop malicious nodes** that deliberately send fake tokens.

This introduces **Byzantine faults**, where nodes may send arbitrary or incorrect responses.

- Handling this requires **Byzantine fault-tolerant (BFT) systems**, which continue operating correctly even if some nodes are faulty or malicious.
    
- Consensus in such an environment is known as the **Byzantine Generals Problem**.
    

BFT is crucial only in systems where **nodes cannot be fully trusted** or may be attacked.

A bug in the software could be regarded as a Byzantine fault, but if you deploy the same software to all nodes, then a Byzantine fault-tolerant algorithm cannot save you. Most Byzantine fault-tolerant algorithms require a supermajority of more than two thirds of the nodes to be functioning correctly (i.e., if you have four nodes, at most one may malfunction). To use this approach against bugs, you would have to have four independent implementations of the same software and hope that a bug only appears in one of the four implementations.

### System Model and Reality


Algorithms in distributed systems must **not rely heavily on hardware or software details**. To reason about them, we define a **system model** describing assumptions about timing and failures.

**Timing models:**

- **Synchronous:** Network delays, process pauses, and clock errors are bounded. Unrealistic in practice because delays can be unbounded.
    
- **Partially synchronous:** Behaves like synchronous most of the time, but occasionally exceeds bounds. More realistic for real-world systems.
    
- **Asynchronous:** No timing assumptions; algorithms cannot use clocks or timeouts. Very restrictive.
    

**Node failure models:**

- **Crash-stop:** Node may fail by crashing and never returns.
    
- **Crash-recovery:** Node may crash and later recover. Stable storage is preserved; in-memory state is lost.
    
- **Byzantine:** Nodes may behave arbitrarily or maliciously, potentially sending false or misleading information.
    

Understanding these models is essential for designing correct distributed algorithms under realistic conditions.

**Correctness of an algorithm**

Correctness of a distributed algorithm is defined in terms of **properties it must satisfy** under a given system model.

**Example: fencing token generation**

- **Uniqueness:** No two requests return the same token.
    
- **Monotonic sequence:** If request `x` finishes before `y` starts, the token for `x` is smaller than that for `y`.
    
- **Availability:** A non-crashed node requesting a token eventually gets a response.
    

An algorithm is **correct** if it satisfies all its properties **under all conditions allowed by the system model**. Note that this assumes the system model itself is respected—if all nodes crash or network delays are infinite, no algorithm can guarantee progress.

In distributed systems, algorithm properties are classified as **safety** or **liveness**:

**Safety properties**

- Nothing bad happens.
    
- Example: uniqueness or monotonicity of fencing tokens.
    
- If violated, the violation is immediate and irreversible (e.g., a duplicate token has already been issued).
    

**Liveness properties**

- Something good eventually happens.
    
- Example: availability or eventual consistency.
    
- Temporary violations are acceptable, as they may still be satisfied in the future (e.g., a node eventually receives a response).
    

**Key point:**

- Safety must hold **always**, under all conditions, even if all nodes crash or the network fails.
    
- Liveness guarantees eventual success, but can tolerate temporary delays or failures.

### Summary

In distributed systems, partial failures are the norm and must be tolerated, unlike on a single reliable machine. Key points:

- **Message unreliability:** Packets and replies may be lost or delayed, making it impossible to know if a message got through without a response.
    
- **Clock issues:** Node clocks may be out of sync, jump forward/back, or drift unpredictably, making reliance on local time risky.
    
- **Process pauses:** Nodes can pause (e.g., due to GC), be considered dead, and later resume without realizing it.
    

**Fault tolerance challenges:**

- Detecting failures is hard; timeouts are the common mechanism but can falsely suspect slow nodes or network issues.
    
- Degraded nodes (“limping”) can be more difficult than completely failed nodes.
    
- Nodes have no shared memory or global knowledge; all communication is over an unreliable network. Decisions require quorum-based protocols rather than relying on a single node.
    

**Design implications:**

- Distributed systems are messy compared to single-machine deterministic environments.
    
- Whenever possible, keep operations on a single machine to avoid unnecessary complexity.
    
- Distributed systems provide scalability, fault tolerance, and low latency that single nodes cannot.
    

**Trade-offs:**

- Perfect reliability (hard real-time networks, guaranteed clock synchronization) is possible but expensive and inefficient.
    
- Most distributed systems accept cheap, unreliable components and handle faults at the node level.
    
- Supercomputers assume reliable components and restart entirely on failure, whereas distributed systems can continue running despite node-level faults.
    

In short, distributed systems must **expect partial failures, design for quorum-based decision making, and accept trade-offs between reliability, cost, and performance**.

## CHAPTER 9 Consistency and Consensus

The best way of building fault-tolerant systems is to find some general-purpose abstractions with useful guarantees, implement them once, and then let applications rely on those guarantees.

We need to understand the scope of what can and cannot be done: in some situations, it’s possible for the system to tolerate faults and continue working; in other situations, that is not possible. The limits of what is and isn’t possible have been explored in depth, both in theoretical proofs and in practical implementations

### Consistency Guarantees

Most replicated databases guarantee **eventual consistency**, meaning that if updates stop and the system stabilizes, **all replicas will eventually return the same value**. This reflects **temporary inconsistency** that resolves over time as replicas **converge**—hence, “convergence” may be a more accurate term.

However, **eventual consistency is a very weak guarantee**: it doesn’t specify _when_ replicas will converge.

For developers, this model is difficult because it breaks the intuitive behavior of variables in single-threaded programs—where writing a value and reading it right after always returns the new value. Distributed databases behave differently due to replication delays and network faults.

When using weakly consistent systems, developers must remain aware of these limitations; assuming stronger consistency than provided often leads to **subtle, hard-to-reproduce bugs** that may only appear under specific timing or failure conditions.

### Linearizability

In an **eventually consistent** database, **two replicas queried at the same time may return different results**, which can be confusing for clients.

Wouldn’t it be simpler if the database gave the **illusion of a single replica**—so that every client always saw the same, up-to-date data?

That’s the idea behind **linearizability** (also called **atomic consistency**, **strong consistency**, **immediate consistency**, or **external consistency**).

The **core concept**:

> Make the system behave **as if there were only one copy of the data**, and **all operations on it were atomic**.

In a **linearizable system**:

- As soon as one client **completes a write**,
    
- **All other clients must immediately see** that new value on subsequent reads.
    

Thus, linearizability provides a **recency guarantee** — every read reflects the **most recent successful write**, never a stale or outdated value.

#### What Makes a System Linearizable?

The basic idea behind linearizability is simple: to make a system appear as if there is only a single copy of the data. However, nailing down precisely what that means actually requires some care 

It is possible (though computationally expensive) to test whether a system’s behavior is linearizable by recording the timings of all requests and responses, and checking whether they can be arranged into a valid sequential order

#### Relying on Linearizability

In a **single-leader replication** system, it’s crucial to ensure there is **only one leader** at any time to prevent **split brain**. One common method is **leader election via a lock**—each node attempts to acquire the lock, and the one that succeeds becomes the leader. However, this lock must be **linearizable**, so all nodes agree on which node holds it.

Similarly, **uniqueness constraints** (like unique usernames, email addresses, or file paths) also require **linearizability**. When multiple clients try to create the same item concurrently, linearizability ensures that only one operation succeeds and the other correctly fails.

#### Implementing Linearizable Systems

Since **linearizability** means the system behaves as if there were **only one atomic copy of the data**, the simplest way to achieve it would be to actually keep a **single copy**. However, this would make the system **fault-intolerant**—if that node failed, the data would be lost or unavailable. The usual solution is **replication** for fault tolerance.

**Consensus algorithms** (like those used in **ZooKeeper** and **etcd**) provide **linearizable** guarantees by preventing **split brain** and **stale replicas**, allowing safe, fault-tolerant storage.

**Multi-leader replication** is **not linearizable**, since multiple nodes process writes concurrently and replicate them asynchronously, which can cause **conflicting writes**.

**Leaderless replication** (Dynamo-style) also is **not truly linearizable**—even with quorum reads and writes (w + r > n), the guarantee falls short of full strong consistency depending on configuration and definition.

### Ordering Guarantees

#### Ordering and Causality

There are several reasons why ordering keeps coming up, and one of the reasons is that it helps preserve causality

Causality imposes an ordering on events: cause comes before effect; a message is sent before that message is received; the question comes before the answer. And, like in real life, one thing leads to another: one node reads some data and then writes something as a result, another node reads the thing that was written and writes something else in turn, and so on. These chains of causally dependent operations define the causal order in the system

**The causal order is not a total order**

A **total order** allows any two elements to be compared (e.g., numbers like 5 and 13), while a **partial order** allows comparison only when one element clearly precedes another (e.g., sets like {a, b} and {b, c} are incomparable).

In **databases**, these concepts relate to **consistency models**:

- **Linearizability** provides a **total order** of operations. The system behaves as if there were only one atomic copy of data, meaning for any two operations, we can always tell which one happened first—no true concurrency exists.
    
- **Causality** provides only a **partial order**: operations are ordered only if they are causally related, while concurrent operations are **incomparable**.
    

Thus, in a **linearizable datastore**, all operations appear on a **single global timeline**, executed **atomically** and **sequentially**, without concurrency.

**Linearizability is stronger than causal consistency**

**Linearizability implies causality**, meaning any linearizable system automatically preserves the correct causal order of operations—even across multiple communication channels—without needing extra mechanisms like timestamps.

This property makes **linearizable systems simple and intuitive**, but **achieving linearizability harms performance and availability**, especially in the presence of **network delays**.

The **middle ground** is **causal consistency**, which preserves causality **without requiring linearizability**. It is the **strongest consistency model** that remains **available and performant** even during **network partitions**, and unlike linearizability, the **CAP theorem does not apply** to it.

In practice, many systems that seem to need linearizability only require causal consistency. New research explores **causally consistent databases** that offer performance and availability similar to **eventually consistent systems**, though most of these approaches are still experimental and not yet widely used in production.

**Capturing causal dependencies**

To **maintain causality**, the system must know **which operations happened before others**. This forms a **partial order**: concurrent operations can occur in any order, but **causally dependent operations must be applied in order** on every replica.

When a replica processes an operation, it must first ensure that **all causally preceding operations** have been processed; if any are missing, it must **wait** until those arrive.

To track these dependencies, the system needs a way to represent each node’s **“knowledge”**—what operations it has already seen. If a node had seen value **X** before issuing a write **Y**, then **X → Y** (X happened before Y), meaning they are **causally related**.

This analysis mirrors an investigation: _did the system (or node) “know” about X when it made decision Y?_

#### Sequence Number Ordering

Although **causality** is theoretically important, **explicitly tracking all causal dependencies** is often **impractical**, since clients may read large amounts of data before performing a write—making it unclear which reads the write depends on. Tracking every dependency would cause significant **overhead**.

A more practical solution is to use **sequence numbers or timestamps** to order events. These timestamps don’t need to come from physical clocks (which are unreliable) but can come from **logical clocks**—algorithms that generate a sequence of numbers (usually simple **counters** incremented for each operation).

These **sequence numbers or timestamps** are compact and establish a **total order**—every operation has a unique number, and any two can be compared to determine which came later.

In a **single-leader replication** setup, the **replication log** naturally defines this total order of writes consistent with causality: the leader assigns **monotonically increasing sequence numbers** to operations as they are added to the log.

#### Total Order Broadcast

If a program runs on a **single CPU core**, defining a **total order of operations** is straightforward—it’s simply the order in which the CPU executes them.  
However, in a **distributed system**, getting all nodes to agree on a **single total order of operations** is much more difficult.

**Single-leader replication** solves this by letting one node (the leader) **sequence all operations** on its own CPU. The problems then become **scaling throughput** beyond what a single leader can handle and **handling failover** if the leader crashes.

**Total order broadcast** provides a general way to achieve this ordering across multiple nodes. It requires two key **safety properties**:

- **Reliable delivery:** No messages are lost—if one node delivers a message, all nodes eventually do.
    
- **Totally ordered delivery:** All nodes deliver messages **in the same order**.
    

A correct total order broadcast algorithm guarantees these properties even when nodes or networks fail (messages may be delayed but not lost).

**Using total order broadcast**  
It’s the foundation for **database replication**—if each message represents a write and all replicas process writes in the same order, they remain **consistent**. This idea is known as **state machine replication**.  
The same mechanism can also be used to implement **serializable transactions**.

An important rule is that once a message is delivered, its position in the order **cannot change**—no retroactive insertion is allowed. This makes total order broadcast **stronger than timestamp ordering**.

Another way to view it: **total order broadcast creates a log** (like a replication or transaction log). Delivering a message equals **appending to the log**, and since every node sees the same log sequence, they all remain in sync.

### Distributed Transactions and Consensus

Consensus is one of the most important and fundamental problems in distributed computing. On the surface, it seems simple: informally, the goal is simply to get several nodes to agree on something. You might think that this shouldn’t be too hard. Unfortunately, many broken systems have been built in the mistaken belief that this problem is easy to solve

There are several situations in distributed systems where **nodes must reach agreement**—that is, achieve **consensus**.

**Leader election**  
In systems with **single-leader replication**, all nodes must agree on **which node is currently the leader**. Problems arise if network faults prevent some nodes from communicating, causing multiple nodes to believe they are the leader.  
To prevent this **split-brain** scenario, a **consensus mechanism** is required to ensure that leadership is uniquely and consistently assigned.

**Atomic commit**  
In databases supporting **distributed transactions** (spanning multiple nodes or partitions), a transaction might **succeed on some nodes but fail on others**.  
To preserve **transaction atomicity** (i.e., “all or nothing” behavior), nodes must agree on whether to **commit or abort** the transaction.  
Thus, consensus is essential to ensure that **all participants make the same final decision**.

#### Atomic Commit and Two-Phase Commit (2PC)

Atomicity ensures that a transaction’s writes are **all applied or all discarded**, preventing partial updates that could leave the database in an inconsistent state. This is especially important for **multi-object transactions** and databases with **secondary indexes**, as changes must remain consistent across all data structures.

**Single-node atomic commit**  
On a single node, atomicity is handled by the storage engine. The typical process is:

1. Transaction writes are made durable (e.g., in a write-ahead log).
    
2. A **commit record** is appended to disk.
    
3. The commit is considered final once the commit record is successfully written.
    

If the database crashes before the commit record is written, the transaction can be rolled back. The **disk controller of a single node** ensures that this process is atomic.

**Challenges in distributed atomic commit**  
In a distributed system, committing a transaction requires agreement across multiple nodes. Problems include:

- Some nodes may detect conflicts and need to abort, while others are ready to commit.
    
- Commit requests may be lost in the network or delayed, leading to inconsistent outcomes.
    
- Nodes may crash mid-commit, rolling back locally while others commit.
    

Because **a committed transaction cannot be undone**, a node must only commit **once it is certain that all other nodes will also commit**, ensuring the atomicity and irreversibility of distributed transactions. This underpins the **read committed isolation level**.

**Introduction to two-phase commit**

Two-phase commit is an algorithm for achieving atomic transaction commit across multiple nodes—i.e., to ensure that either all nodes commit or all nodes abort. It is a classic algorithm in distributed databases

**Two-Phase Commit (2PC)**

2PC introduces a **coordinator** (or transaction manager), which is not present in single-node transactions. The coordinator can be a library embedded in the application (e.g., in a Java EE container) or a separate service, with examples including Narayana, JOTM, BTM, and MSDTC.

In a 2PC transaction, the application performs reads and writes on multiple **participant** nodes. When it’s ready to commit, the coordinator starts **Phase 1 (prepare phase)** by sending a prepare request to each participant, asking if they can commit.

- If all participants respond **“yes”**, the coordinator proceeds to **Phase 2 (commit phase)**, sending a commit request so the transaction is finalized.
    
- If any participant responds **“no”**, the coordinator sends an **abort** request to all participants, ensuring that the transaction is rolled back everywhere.

**A system of promises**

**How 2PC works:**

1. The application requests a globally unique transaction ID from the coordinator.
    
2. It begins single-node transactions on each participant, tagging them with the transaction ID. If anything fails, the transaction can be aborted.
    
3. The coordinator sends a **prepare** request to all participants. If any request fails, it aborts the transaction.
    
4. Participants ensure they can commit (writing data to disk, checking constraints) and reply “yes” if ready, surrendering the right to abort.
    
5. The coordinator collects all responses and makes a final commit/abort decision, logging it to disk (the commit point).
    
6. The coordinator sends the final commit or abort request to all participants.

**Coordinator failure**

If the coordinator fails before sending the prepare requests, a participant can safely abort the transaction. But once the participant has received a prepare request and voted “yes,” it can no longer abort unilaterally—it must wait to hear back from the coordinator whether the transaction was committed or aborted. If the coordinator crashes or the network fails at this point, the participant can do nothing but wait. A participant’s transaction in this state is called in doubt or uncertain.

Without hearing from the coordinator, the participant has no way of knowing whether to commit or abort. In principle, the participants could communicate among themselves to find out how each participant voted and come to some agreement, but that is not part of the 2PC protocol.

**Three-phase commit**

Two-phase commit is called a blocking atomic commit protocol due to the fact that 2PC can become stuck waiting for the coordinator to recover. In theory, it is possible to make an atomic commit protocol nonblocking, so that it does not get stuck if a node fails. However, making this work in practice is not so straightforward.

In general, nonblocking atomic commit requires a perfect failure detector [67, 71]— i.e., a reliable mechanism for telling whether a node has crashed or not. In a network with unbounded delay a timeout is not a reliable failure detector, because a request may time out due to a network problem even if no node has crashed.

#### Distributed Transactions in Practice

Some implementations of distributed transactions carry a heavy performance penalty

**Types of distributed transactions:**

**Database-internal distributed transactions**  
These occur within a single distributed database that uses replication or partitioning (e.g., VoltDB, MySQL Cluster NDB). All participants run the same database software and can use protocols or optimizations specific to that system.

**Heterogeneous distributed transactions**  
These span multiple different systems, such as databases from different vendors or non-database systems like message brokers. They must ensure atomic commit across entirely different technologies.

#### Fault-Tolerant Consensus

Informally, consensus means getting several nodes to agree on something. The consensus problem is normally formalized as follows: one or more nodes may propose values, and the consensus algorithm decides on one of those values

**Consensus algorithm properties:**

**Uniform agreement** – No two nodes decide differently.  
**Integrity** – No node decides twice.  
**Validity** – Any decided value was proposed by some node.  
**Termination** – Every non-crashed node eventually decides a value.

Uniform agreement and integrity ensure everyone agrees and cannot change their decision. Validity prevents trivial solutions like always deciding `null`. Termination formalizes fault tolerance: even if some nodes fail, the remaining nodes must eventually decide. Two-phase commit (2PC) fails termination because if the coordinator crashes, participants can remain indefinitely uncertain.

#### Membership and Coordination Services

**Linearizable atomic operations** – An atomic compare-and-set can implement a lock; only one node succeeds if multiple try concurrently. Consensus ensures atomicity and linearizability even with node failures or network interruptions. Distributed locks are often leases with expiry times.

**Total ordering of operations** – Fencing tokens prevent conflicts during process pauses. Each lock acquisition increments the token. ZooKeeper provides this with totally ordered operations, giving each a monotonically increasing transaction ID (zxid) and version number (cversion).

**Failure detection** – Clients maintain sessions with ZooKeeper servers and exchange heartbeats. If heartbeats stop beyond the session timeout, the session is declared dead, and any locks can be automatically released (ephemeral nodes).

**Change notifications** – Clients can watch locks and values for changes, allowing them to detect other clients joining or failing without constant polling.

### Summary

In this chapter we examined consistency and consensus from multiple perspectives. Linearizability aims to make replicated data appear as if there is a single copy, with all operations acting atomically. It is simple to understand but can be slow in environments with large network delays. Causality, by contrast, orders events based on cause and effect, allowing concurrent operations and branching timelines. Causal consistency avoids the coordination overhead of linearizability and is less sensitive to network problems.

However, some problems—like ensuring a username is unique—cannot be solved by causality alone, leading to the need for consensus. Achieving consensus means all nodes agree on a decision, and that decision is irrevocable. Many problems reduce to consensus, including linearizable compare-and-set registers, atomic transaction commits, total order broadcast, locks and leases, membership/coordination services, and uniqueness constraints.

Single-leader databases assign decision-making to the leader, enabling linearizable operations and totally ordered replication logs. If the leader fails or becomes unreachable, the system can be blocked. Solutions include waiting for the leader to recover, manual failover by humans, or using an algorithm to automatically elect a new leader—requiring consensus. Even with a leader, consensus is still needed for leadership changes, though less frequently.

Fault-tolerant consensus algorithms exist, and tools like ZooKeeper provide outsourced consensus, failure detection, and membership services. Not all systems need consensus: leaderless and multi-leader replication systems can operate without global consensus, though this introduces conflicts that must be resolved.

The chapter emphasizes that theoretical research on distributed systems, while sometimes abstract, is crucial for understanding what is possible, what is safe, and how to reason about the often counterintuitive behavior of distributed systems.


## CHAPTER 10 Batch Processing


In such online systems, whether it’s a web browser requesting a page or a service calling a remote API, we generally assume that the request is triggered by a human user, and that the user is waiting for the response. They shouldn’t have to wait too long, so we pay a lot of attention to the response time of these systems

The web and HTTP/REST-based APIs have made the request/response style very common, but it’s not the only way to build systems. There are three main types of systems:

**Services (online systems)**  
A service waits for a client request, handles it quickly, and sends back a response. Response time and availability are key performance measures.

**Batch processing systems (offline systems)**  
These take large input data, process it through jobs, and produce output. Jobs run periodically and focus on throughput rather than immediate response.

**Stream processing systems (near-real-time systems)**  
These operate between online and offline modes. They consume and produce data continuously, working on events shortly after they occur for lower latency compared to batch systems.
### Batch Processing with Unix Tools

#### Simple Log Analysis

Various tools can analyze log files and generate reports about website traffic.

```
cat /var/log/nginx/access.log | 
awk '{print $7}' | 
sort | 
uniq -c | 
sort -r -n | 
head -n 5
```

- Read the log file.
    
- Split each line by whitespace and extract the seventh field (the requested URL).
    
- Sort the URLs alphabetically; repeated URLs appear consecutively.
    
- `uniq -c` counts how many times each unique URL appears.
    
- The second `sort` orders the output numerically and in reverse, showing most frequent requests first.
    
- `head -n 5` displays only the top five results.
    

Example output:

```
4189 /favicon.ico
3631 /2013/05/24/improving-security-of-ssh-private-keys.html
2124 /2012/12/05/schema-evolution-in-avro-protocol-buffers-thrift.html
1369 /
915 /css/typography.css
```

**Chain of commands versus custom program**

Instead of the chain of Unix commands, you could write a simple program to do the
same thing 

```
counts = Hash.new(0)
File.open('/var/log/nginx/access.log') do |file|
  file.each do |line|
    url = line.split[6]
    counts[url] += 1
  end
end
top5 = counts.map { |url, count| [count, url] }.sort.reverse[0...5]
top5.each { |count, url| puts "#{count} #{url}" }
```

- `counts` is a hash that tracks how many times each URL appears, starting from zero.
    
- Each line is split by whitespace; the seventh field (index 6) is the URL.
    
- Increment the counter for each URL.
    
- Sort by count in descending order and take the top five results.
    
- Print those top five entries.
    

This Ruby program is less concise than the Unix pipe version but more readable. The main difference lies in their execution flow, especially noticeable on large files.

**Sorting versus in-memory aggregation**

Which approach is better depends on how many different URLs exist. For small to mid-sized websites, all distinct URLs and their counters can usually fit in memory.

However, if the dataset is too large to fit into memory, the sorting approach is better since it can efficiently use disks. Similar to SSTables and LSM-Trees, chunks of data can be sorted in memory, written to disk as segment files, and later merged into larger sorted files.

#### The Unix Philosophy

The Unix philosophy made it easy to analyze a log file using chained commands. This idea dates back to 1964 when Doug McIlroy, the inventor of Unix pipes, described programs as segments of a “garden hose” that could be connected to process data. The plumbing analogy became the foundation of the Unix philosophy, summarized in 1978 as:

1. Make each program do one thing well. To handle new tasks, build new programs instead of overcomplicating existing ones.
    
2. Expect every program’s output to serve as input to another unknown program. Keep outputs clean and simple, avoiding rigid formats or interactive-only input.
    
3. Design software to be tested early and often; rebuild clumsy parts without hesitation.
    
4. Use tools to automate and simplify programming, even if they’re temporary.
    

This mindset—automation, rapid iteration, experimentation, and modular design—closely mirrors modern Agile and DevOps principles.

**A uniform interface**  
For one program’s output to become another’s input, they must share a common format. Most Unix programs use plain ASCII text for this, treating input as a sequence of records separated by the newline (`\n`) character. This convention allowed commands like `awk`, `sort`, `uniq`, and `head` to work together seamlessly. While the choice of `\n` was arbitrary, the ASCII record separator (0x1E) might have been a more intentional design.

**Separation of logic and wiring**

Another characteristic feature of Unix tools is their use of standard input (stdin) and standard output (stdout). If you run a program and don’t specify anything else, stdin comes from the keyboard and stdout goes to the screen. However, you can also take input from a file and/or redirect output to a file

A program can still read and write files directly if it needs to, but the Unix approach works best if a program doesn’t worry about particular file paths and simply uses stdin and stdout. This allows a shell user to wire up the input and output in whatever way they want; the program doesn’t know or care where the input is coming from and where the output is going to. (One could say this is a form of loose coupling, late binding [15], or inversion of control [16].) Separating the input/output wiring from the program logic makes it easier to compose small tools into bigger systems.

### MapReduce and Distributed Filesystems

MapReduce is similar to Unix tools but operates across many machines. Like Unix processes, each MapReduce job takes one or more inputs and produces one or more outputs.

While Unix tools use `stdin` and `stdout` for input and output, MapReduce reads and writes files on a distributed filesystem. In Hadoop, this filesystem is called **HDFS**.

HDFS follows the **shared-nothing** principle, unlike shared-disk systems such as NAS or SAN, which rely on centralized storage hardware. Instead, HDFS uses ordinary datacenter machines connected over a standard network.

Each machine runs a daemon process that exposes local disks as part of a unified storage system. A central **NameNode** tracks which file blocks are stored on which machines, making HDFS appear as a single large filesystem spanning all nodes.

To handle failures, HDFS replicates file blocks across multiple machines, maintaining multiple copies to ensure data reliability.

#### MapReduce Job Execution

MapReduce is a programming framework for processing large datasets in distributed filesystems like HDFS. It’s conceptually similar to the web server log analysis process:

1. Read input files and split them into records (for example, each line in a log file).
    
2. The **mapper** function extracts a key-value pair from each record (like `awk '{print $7}'`, which outputs URLs).
    
3. The system sorts all key-value pairs by key (as done by `sort`).
    
4. The **reducer** function processes each group of identical keys, combining their values (like `uniq -c` counting occurrences).
    

Steps 2 and 4 are user-defined (map and reduce), while step 1 is handled by an input parser and step 3 is automatically managed by MapReduce.

**Mapper**  
Processes one input record at a time, extracting key-value pairs. It’s stateless and independent for each record.

**Reducer**  
Receives all values associated with a given key and processes them, producing new output records (e.g., counts per URL).

**Distributed execution of MapReduce**  
Unlike Unix pipelines, MapReduce automatically parallelizes computation across many machines. Mappers and reducers operate independently on records, while the framework handles data transfer between nodes.

Before execution, the framework distributes the program code (like JAR files) to the machines running map tasks. Each map task reads input, applies the mapper, and outputs sorted key-value pairs locally.

Reducers are assigned based on a hash of the key, ensuring that all data for a given key goes to the same reducer. Sorting happens in stages: each mapper writes sorted partitions to disk, and reducers merge these sorted files while maintaining order.

Finally, the reducer processes each key’s data (which may not fit entirely in memory) and generates any number of output records.

**MapReduce workflows**

The range of problems solvable by a single MapReduce job is limited. For example, one job can count page views per URL but cannot determine the most popular URLs without an additional sorting step.

Because of this, MapReduce jobs are often **chained into workflows**, where the output of one job becomes the input for the next. Hadoop MapReduce doesn’t provide built-in workflow support, so this chaining is managed through directory configurations: one job writes its output to an HDFS directory, and the next reads from that same directory.

From the framework’s perspective, each job is independent.  
These chained jobs resemble a sequence of Unix commands where each step writes to a temporary file and the next reads from it, rather than a direct in-memory pipeline.

#### Reduce-Side Joins and Grouping

In many datasets, records are linked to each other—through foreign keys in relational databases, document references in document stores, or edges in graph models. A **join** is required whenever code needs to access records from both sides of such relationships.

In databases, queries involving few records typically rely on **indexes** to quickly find relevant data. Joins may require multiple index lookups.

MapReduce, however, has **no built-in concept of indexes**. When given input files, it reads their entire contents—essentially performing a full table scan. While inefficient for small queries, this approach is acceptable for **analytic workloads** that aggregate data across large datasets. In those cases, scanning everything is reasonable, especially when computation is parallelized across many machines.

#### Map-Side Joins

Join algorithms that perform the join logic in reducers are called **reduce-side joins**. In this approach, mappers prepare input data by extracting keys and values, assigning them to reducer partitions, and sorting by key.

The benefit of reduce-side joins is flexibility—they work regardless of input structure or data properties. However, they are costly since sorting, shuffling, and merging data across reducers can involve multiple disk writes, depending on memory limits.

If certain assumptions about the input data can be made, a **map-side join** can be used instead. This method skips reducers and sorting entirely. Each mapper reads a block of input data and directly writes an output file, making it much faster and simpler.

#### The Output of Batch Workflows

Where does batch processing fit in? It is not transaction processing, nor is it analytics. It is closer to analytics, in that a batch process typically scans over large portions of an input dataset. However, a workflow of MapReduce jobs is not the same as a SQL query used for analytic purposes

**Building search indexes**

Batch processes are effective for building **full-text search indexes** over a fixed set of documents. Mappers partition documents, reducers build indexes for each partition, and the results are written to the distributed filesystem. These indexes are **immutable**, and if documents change, the entire indexing workflow can be rerun to replace the old indexes. This is simple to reason about, though potentially computationally expensive for small changes.

**Key-value stores as batch process output**  
Batch jobs often produce databases that the web application queries, such as user ID–based friend suggestions or product recommendations. Instead of writing directly to a database one record at a time, a better approach is to build the database inside the batch job, write it as immutable files to the output directory, and then load them in bulk into read-only servers. For example, Voldemort allows atomic switching to new files while keeping old ones for rollback.

**Philosophy of batch process outputs**  
Following the Unix philosophy, MapReduce outputs are immutable and side-effect-free: inputs remain unchanged, previous outputs are replaced, and no external systems are modified. This provides several advantages:

- Bugs can be rolled back by rerunning the job or switching to old outputs, unlike read-write databases where corrupted data cannot be easily undone.
    
- Easier rollback accelerates feature development and supports Agile practices.
    
- Failed map or reduce tasks are automatically retried safely because inputs are immutable and outputs from failed tasks are discarded.
    
- The same input files can serve multiple jobs, including monitoring or validation tasks.
    
- Logic is separated from wiring (input/output configuration), enabling code reuse: one team can focus on processing logic while others manage job scheduling and execution.

#### Comparing Hadoop to Distributed Databases

**Diversity of storage**

Databases require data to follow a specific model (relational, document, etc.), whereas files in a distributed filesystem are just sequences of bytes. These files can represent database records, text, images, videos, sensor readings, sparse matrices, feature vectors, genome sequences, or any other kind of data.

This approach is similar to a **data warehouse**: collecting data from across an organization in one place enables joins across previously disparate datasets. Unlike MPP databases, which require careful schema design, storing data in raw form speeds up collection—this is often called a **data lake** or **enterprise data hub**. The burden of interpreting the data shifts to the consumer, following a **schema-on-read** approach.

**Diversity of processing models**  
MPP databases are monolithic systems optimized for storage layout, query planning, scheduling, and execution. They perform well for the queries they are designed for, and SQL provides expressive, accessible queries compatible with tools like Tableau. However, not all processing can be effectively expressed in SQL. MapReduce allows engineers to run custom code over large datasets.

**Designing for frequent faults**  
Batch processes, like MapReduce jobs, are less sensitive to faults than online systems—they can be retried without affecting users. In MPP databases, a node failure usually aborts the entire query, which is acceptable for short-running queries.

MapReduce tolerates task-level failures by retrying individual map or reduce tasks. It frequently writes data to disk both for fault tolerance and to handle datasets too large for memory. This approach is ideal for large jobs that run long enough to expect task failures, avoiding the inefficiency of rerunning entire jobs. Even though task-level recovery may add overhead in fault-free scenarios, it’s worthwhile when task failures are common.

### Beyond MapReduce

To simplify the complexity of using **MapReduce** directly, higher-level frameworks like **Pig, Hive, Cascading,** and **Crunch** were developed. These abstractions make common batch-processing tasks easier once you understand MapReduce.

However, the **MapReduce execution model itself** has inherent performance limitations that abstractions can’t fix. While MapReduce is extremely **robust**—able to handle massive datasets on unreliable systems—it can also be **very slow**. For certain types of processing, other tools can perform **orders of magnitude faster**.

#### Materialization of Intermediate State

The **input and output directories** of a MapReduce job are its main connection points with the outside world. When one job’s output becomes another’s input, the next job must be configured to read from the previous job’s output and started only after it finishes—typically managed by a **workflow scheduler**.

If the output is meant to be **shared widely**, publishing it to a known filesystem location promotes **loose coupling** between teams. But often, the output is **only used internally** by the next job in the same workflow—these files are just **intermediate state**. Writing such intermediate data to disk is called **materialization** (similar to materialized views).

However, **fully materializing intermediate results** has downsides compared to Unix-style **streaming pipes**:

- Each job must **wait** for the previous one to fully complete, causing slowdowns due to **straggler tasks**.
    
- **Mappers may be redundant**, re-reading recent reducer output when their logic could have been merged.
    
- **Replicating temporary files** across the distributed filesystem adds unnecessary overhead.
    

In short, materialization improves fault tolerance and clarity but sacrifices **speed and efficiency** compared to **streamed, in-memory processing**.

**Dataflow engines**

Dataflow engines explicitly model **data movement through multiple processing stages**, similar to MapReduce but more flexible. They repeatedly apply **user-defined functions (operators)** to records and connect these operators in various ways to define complex workflows.

Key characteristics and advantages:

- Operators can be connected flexibly — not just alternating **map** and **reduce** stages.
    
- Different data transfer options exist:
    
    - **Repartition + sort by key** → for sort-merge joins and grouping (like MapReduce shuffle).
        
    - **Repartition only (no sort)** → for faster **hash joins**, since order doesn’t matter.
        
    - **Broadcast join** → one operator’s output is sent to all partitions of another operator.
        
- Inspired by research systems like **Dryad** and **Nephele**.
    

**Advantages over MapReduce:**

- **Sorting is optional** — done only when necessary, reducing overhead.
    
- **No redundant map tasks** — mappers can often be merged into preceding operators.
    
- **Smarter scheduling** — since data dependencies are explicit, the engine can **optimize data locality**, running related tasks on the same machine to reduce network transfer.
    

In short, **dataflow engines** generalize and optimize the MapReduce model, improving performance and flexibility by explicitly modeling how data moves and is processed through each stage.

**Fault tolerance**

Fully materializing intermediate data to a distributed filesystem makes **fault tolerance simple** in systems like MapReduce — if a task fails, it can just be restarted elsewhere and reread its input from disk.

Modern systems like **Spark** and **Flink** improve this idea using different fault recovery mechanisms:

- **Spark’s RDDs (Resilient Distributed Datasets)** track how data was derived (its “lineage”) so lost partitions can be **recomputed** from their ancestors.
    
- **Flink** instead uses **checkpoints** to save the internal state of operators, allowing it to **resume execution** instead of restarting from scratch.
    

However, recomputation only works reliably if computations are **deterministic** — i.e., they always produce the same output for the same input.

- If an operator is **nondeterministic** (e.g., depends on random numbers, timestamps, or external systems), recomputation can produce inconsistent data, forcing downstream operators to restart too.
    
- To prevent cascading failures, operators should therefore be designed to be deterministic.
    

Finally, recomputation isn’t always ideal: if **intermediate data is small** or **computation is very expensive**, it’s often better to **materialize (save)** the intermediate results to disk instead of recomputing them.

#### Graphs and Iterative Processing

In batch processing, graphs are often analyzed offline for use cases such as **recommendation engines** or **ranking systems**.

Many graph algorithms work by **traversing edges repeatedly**, joining connected vertices to propagate information until a condition is met—like reaching all reachable nodes or achieving convergence (e.g., in a **transitive closure**).

Although a graph can be stored in a distributed filesystem (as files listing vertices and edges), **MapReduce alone cannot handle iterative algorithms**, since it performs only a **single pass** over the data.

To support iterative graph computations, a **scheduler-driven loop** is used:

1. The scheduler runs a batch job that performs one step of the algorithm.
    
2. After completion, it checks whether the algorithm has converged or finished.
    
3. If not, the scheduler triggers another round of the batch job, repeating the process until the stopping condition is met.

#### High-Level APIs and Languages

Dataflow APIs provide **relational-style operations**—such as joins, groupings, filters, and aggregations—to define computations declaratively. Internally, these operations rely on the **join and grouping algorithms** described earlier.

Beyond simplifying code, these **high-level interfaces** enable **interactive and exploratory development**: developers can iteratively write, test, and observe code behavior in a shell environment. This interactive style promotes experimentation and mirrors the **Unix philosophy** of building complex workflows from simple, composable operations.

### Summary

Unix tools like **awk**, **grep**, and **sort** inspired the design of **MapReduce** and modern **dataflow engines**, emphasizing composability, immutability, and simplicity—programs that _“do one thing well”_ and pass data through standardized interfaces.  
In Unix, this interface is **files and pipes**; in MapReduce, it’s a **distributed filesystem** (e.g., HDFS). Dataflow engines extend this model by adding **in-memory, pipe-like mechanisms** to reduce the need for fully materializing intermediate state, though input and output still typically reside in HDFS.

Distributed batch systems mainly address two challenges:

- **Partitioning:**  
    MapReduce partitions data across mappers and repartitions it for reducers so that related records (e.g., same key) end up together. Later dataflow engines keep this concept but minimize unnecessary sorting.
    
- **Fault Tolerance:**  
    MapReduce achieves robustness by frequently writing to disk, enabling retries of failed tasks but at the cost of slower execution. Dataflow engines keep more data in memory, recomputing as needed, relying on **deterministic operators** to ensure consistent results after recovery.
    

Common join strategies illustrate how partitioned algorithms work:

- **Sort-merge joins:** Inputs are partitioned, sorted, and merged so all records with the same key meet in the same reducer.
    
- **Broadcast hash joins:** A small dataset is loaded into a hash table and broadcast to all mappers processing partitions of a larger dataset.
    
- **Partitioned hash joins:** Both inputs are partitioned identically, allowing independent joins per partition.
    

Batch frameworks enforce a **restricted programming model**—stateless functions with no side effects—making retries and fault recovery transparent. This guarantees **consistent final output** even if some tasks fail and restart.

Ultimately, batch jobs:

- **Read bounded input data**,
    
- **Produce new output without modifying inputs**, and
    
- **Eventually complete** once all data is processed.
    

The next step—**stream processing**—extends these ideas to **unbounded, continuously arriving data**, where jobs never truly finish and must handle data incrementally and in real time.

## CHAPTER 11 Stream Processing

In reality, a lot of data is unbounded because it arrives gradually over time: your users produced data yesterday and today, and they will continue to produce more data tomorrow. Unless you go out of business, this process never ends, and so the dataset is never “complete” in any meaningful way. Thus, batch processors must artificially divide the data into chunks of fixed duration—for example, processing a day’s worth of data at the end of every day, or an hour’s worth of data at the end of every hour.

The problem with daily batch processes is that changes in the input are only reflected in the output a day later, which is too slow for many impatient users. To reduce the delay, we can run the processing more frequently—say, every second—or even continuously, processing every event as it happens. That is the idea behind stream processing.

#### Transmitting Event Streams

In batch processing, inputs and outputs are files. When the input is a file (a sequence of bytes), it is first parsed into a sequence of records. In stream processing, a record is called an event—an immutable, self-contained object describing something that happened at a specific time, usually with a timestamp.

Events can be encoded as text, JSON, or binary formats, allowing them to be stored (e.g., in files or databases) or sent across networks. In batch systems, a file is written once and read by multiple jobs. Similarly, in streaming, an event is produced once by a producer (or publisher) and processed by multiple consumers.

A simple approach to connect producers and consumers is for producers to write events to a datastore, and consumers to periodically check for new ones—similar to batch jobs that process daily data. However, traditional databases are not designed for real-time notifications; triggers exist but are limited. Therefore, specialized tools have been created to handle event delivery and notifications efficiently.

#### Messaging Systems

A simple producer–consumer setup can form a basic messaging system, but most systems extend this model. Unlike Unix pipes or TCP, which connect one sender to one recipient, messaging systems allow multiple producers to publish to a topic and multiple consumers to receive from it.

In the publish/subscribe model, systems differ mainly based on two questions:

1. **Handling overload:** What happens when producers send messages faster than consumers can process them? Systems may drop messages, buffer them in a queue, or apply **backpressure** (flow control) to slow producers. Unix pipes and TCP, for instance, use backpressure with fixed-size buffers.
    
2. **Handling failures:** What happens if nodes crash or go offline? Ensuring durability often requires writing to disk or replication, which adds cost. If occasional message loss is acceptable, higher throughput and lower latency are possible.
    

Batch processing systems provide strong reliability: failed tasks are retried automatically, and partial outputs are discarded, ensuring results are as if no failure occurred. Stream processing aims to offer similar reliability guarantees.

**Direct messaging from producers to consumers**

• **UDP multicast** is widely used in finance for low-latency streams like stock market feeds. Although UDP is unreliable, higher-level protocols can recover lost packets if the producer retains and retransmits them on demand.  
• **Brokerless messaging libraries** such as ZeroMQ and nanomsg use TCP or IP multicast to implement publish/subscribe messaging without central brokers.  
• **StatsD** and **Brubeck** use unreliable UDP to collect and monitor metrics across machines. Since UDP doesn’t guarantee delivery, counter metrics become approximate.  
• **Direct HTTP or RPC delivery:** Producers can push messages directly to consumers via network services, as in webhooks, where one service registers a callback URL and receives requests whenever an event occurs.

If a consumer goes offline, it may miss messages sent during downtime. Some protocols retry failed deliveries, but this fails if the producer crashes and loses its retry buffer.

**Message brokers**

A common alternative is to use a **message broker** (or message queue), a specialized database optimized for handling message streams. It runs as a server, with producers and consumers connecting as clients. Producers send messages to the broker, and consumers read them from it.

By centralizing data, brokers handle client disconnections or crashes more gracefully, shifting durability concerns to the broker itself. Some brokers keep messages in memory, while others persist them to disk to prevent loss during crashes. When consumers are slow, brokers typically allow **unbounded queueing** rather than dropping messages or applying backpressure, though this depends on configuration.

Because of this queuing, consumers operate **asynchronously**—producers wait only for the broker’s confirmation that the message is buffered, not for it to be processed. Delivery to consumers happens later, usually within milliseconds, but potentially delayed if a backlog builds up.

**Message brokers compared to databases**

• **Data retention:** Databases keep data until explicitly deleted, while most message brokers automatically delete messages after successful delivery, making them unsuitable for long-term storage.  
• **Working set size:** Because brokers delete messages quickly, they assume short queues. If consumers are slow and the broker must buffer many messages (even spilling to disk), processing latency and overall throughput can degrade.  
• **Data access:** Databases offer secondary indexes and complex queries; message brokers provide topic subscriptions or pattern-based filtering—different mechanisms serving the same purpose of selecting relevant data.  
• **Change awareness:** Database queries return point-in-time snapshots and require polling to detect changes, while brokers don’t support arbitrary queries but **push** new messages to clients when data changes.

**Multiple consumers**

- **Load balancing:** Each message is delivered to only one consumer, allowing parallel processing. The broker distributes messages among consumers (e.g., multiple clients on the same queue in AMQP, or shared subscriptions in JMS).
    
- **Fan-out:** Each message is delivered to all consumers, enabling independent processing—similar to multiple batch jobs reading the same file (e.g., topic subscriptions in JMS or exchange bindings in AMQP).
    

**Acknowledgments and redelivery**

Consumers may crash before fully processing a message. To avoid message loss, brokers require **acknowledgments**—the consumer must confirm successful processing before the broker removes the message from the queue.

#### Partitioned Logs

Sending a network packet or request is usually a **transient operation**—it leaves no permanent record unless explicitly captured. Even message brokers that persist messages to disk delete them soon after delivery, reflecting this transient mindset.

**Databases and filesystems**, on the other hand, treat written data as permanent until explicitly deleted. This fundamental difference affects how **derived data** is created. In batch processing, inputs are immutable, allowing safe reprocessing and experimentation. In contrast, with traditional messaging systems (like AMQP or JMS), message consumption is **destructive**—acknowledging a message deletes it, preventing reprocessing or recovery.

When a new consumer joins a messaging system, it only receives **new messages**, missing all prior ones. Databases and filesystems, however, allow clients to read old data at any time, as long as it hasn’t been overwritten or deleted.

To bridge these worlds, systems emerged that combine **durable storage** with **low-latency messaging**—this concept is known as **log-based message brokers**.

**Consumer offsets**

Consuming a partition sequentially simplifies progress tracking: all messages with offsets lower than the current consumer offset are processed, and those with higher offsets remain unprocessed. This eliminates the need for per-message acknowledgments—only **periodic offset recording** is required. The reduced bookkeeping, along with batching and pipelining, significantly boosts the throughput of log-based systems.

This **offset mechanism** closely resembles the **log sequence number (LSN)** used in single-leader database replication. Just as followers resume replication from the last processed LSN, consumers can resume reading from their last recorded offset after disconnection. Here, the broker functions like a leader database, and the consumer like a follower.

**When consumers cannot keep up with producers**

If a consumer lags so far behind that it needs messages older than the broker’s retention window, those messages are lost—it can no longer read them. Systems typically **monitor consumer lag** and trigger alerts when it grows too large, giving operators time to resolve issues before data loss occurs.

Even if a consumer misses messages, **only that consumer** is affected—other consumers continue uninterrupted. This isolation offers major operational flexibility: developers can safely attach experimental consumers to production logs for testing or debugging without impacting live systems. When a consumer stops or crashes, it simply halts consumption; the only persistent state is its **offset position**.

### Databases and Streams

#### Keeping Systems in Sync

There is no single system that meets all **data storage, querying, and processing** needs. Real-world applications usually combine multiple technologies to fulfill different requirements.

When the same or related data exists in multiple systems, they must be **kept in sync**. For example, updating an item in a database also requires updating the cache, search indexes, and data warehouse. In data warehouses, this synchronization is often done through **ETL processes**, which copy, transform, and bulk-load data—typically as a **batch process**. Similarly, systems like search indexes or recommendation engines often rely on batch jobs to generate derived data.

If full database dumps are too slow, applications may use **dual writes**, where the code updates multiple systems directly (e.g., writing to the database, updating the search index, and invalidating caches). However, this introduces the risk of inconsistencies if one of those writes fails.

In a single-leader replicated database, the leader enforces a **total order of writes**, ensuring consistent replication across followers. But when multiple independent systems each have their own leaders (like a database and a search index), **conflicts** can arise because there is no shared ordering. The situation improves if one system—such as the database—acts as the **leader**, and other systems (like the search index) behave as **followers**. The question then becomes: can we make that practical?

#### Change Data Capture

Most databases treat their **replication logs** as internal implementation details, not public APIs. Clients are expected to interact with the database through its query language—not by reading replication logs directly.

Recently, **change data capture (CDC)** has gained attention. CDC observes all data changes written to a database and extracts them in a streamable form that can be replicated to other systems. This makes it possible to propagate updates in near real time.

**Initial snapshot**

If a complete log of all database changes were available, the entire database state could be **reconstructed by replaying the log**. However, since keeping all history is often impractical due to storage and replay time, logs are usually **truncated**.

When building a new system such as a full-text search index, you need more than recent changes—you need a **consistent snapshot** of the current full database. Once that snapshot is created, the system can then **apply ongoing changes** from the log to stay synchronized.

#### Event Sourcing

Similarly to **change data capture (CDC)**, **event sourcing** records all changes as a log of events, but at a different level of abstraction:

- **CDC:** The application mutates the database (updates, deletes), and a log of changes is extracted from the database (e.g., replication log). This ensures the extracted write order matches the actual order, avoiding race conditions. The application itself doesn’t need to know CDC is happening.
    
- **Event sourcing:** The application explicitly writes immutable events to an **append-only event log**. Updates or deletes are discouraged, and events represent high-level application actions rather than low-level database state changes.
    

Event sourcing resembles the **chronicle data model** and shares similarities with a **fact table** in a star schema. Specialized tools like **Event Store** exist, but conventional databases or log-based message brokers can also support event-sourced applications.

**Deriving current state from the event log**

An event log alone isn’t sufficient; users expect to see **current state**, not the full history. Applications must transform the log of events into **application state** suitable for presentation. This transformation should be deterministic, so replaying the log always produces the same state.

- **CDC compaction:** The most recent event for a key typically determines its current value, so prior events can be discarded.
    
- **Event sourcing compaction:** Events represent user actions, not state mechanics, so prior events usually cannot be discarded. Full history is needed to reconstruct the final state.
    

To avoid reprocessing the full log repeatedly, event-sourced applications often store **snapshots** of derived current state alongside the event log.

**Commands and events**

Event sourcing carefully distinguishes between **commands** and **events**.

- A **command** is a user request that may fail, for example if it violates some integrity constraint. The application must validate the command before execution.
    
- Once validated and accepted, the command becomes an **event**, which is **durable and immutable**.
    

For example, registering a username or reserving a seat requires checking availability first. Once the check succeeds, an event is generated indicating the action (e.g., username registered or seat reserved). That event becomes a **fact**: even if the user later cancels, the original reservation event remains in the log, and the cancellation is recorded as a separate event.

Consumers of the event stream **cannot reject events**; by the time they see it, the event is immutable and may already have been seen by others. Therefore, command validation must happen **synchronously** before the event is published, possibly using a serializable transaction.

Alternatively, a user request can be split into two events: a **tentative event** followed by a **confirmation event** once validation succeeds.
#### State, Streams, and Immutability

**Advantages of immutable events**

In accounting, mistakes are never erased; instead, a **compensating transaction** is added (e.g., refunding an incorrect charge). The original transaction remains in the ledger for auditing. If incorrect figures have been published, future periods include corrections. This **append-only approach** ensures traceability and auditability.

While critical in finance, immutable logs are also valuable in other systems. If buggy code writes bad data, recovery is easier with an **append-only log of events** than with a destructively updated database. Immutable events also capture more information than current state alone—for instance, a shopping cart event log preserves both added and removed items, which is useful for analytics.

**Deriving multiple views from the same event log**

By separating **mutable state** from the **immutable event log**, multiple read-oriented representations can be derived from the same log, just like having multiple consumers of a stream.

**Concurrency control**

A challenge of event sourcing and CDC is that consumers are usually asynchronous. A user may write to the log and then read from a derived view before the write is reflected. One solution is to update the read view **synchronously** with the log append, using a transaction to make the operation atomic—either by storing the log and view together or via a distributed transaction.

Conversely, deriving current state from an event log **simplifies some concurrency issues**, reducing the need for multi-object transactions.

### Processing Streams

1. **Writing to storage:** Extract data from events and write it to a database, cache, search index, or similar system for querying by other clients. This keeps the storage system **in sync** with changes elsewhere, especially if the consumer is the only writer. It is the streaming equivalent of batch workflow outputs.
    
2. **Pushing to users:** Deliver events directly to users via email, push notifications, or real-time dashboards. Here, humans are the ultimate consumers of the stream.
    
3. **Stream processing:** Transform one or more input streams into output streams. Streams may pass through **multiple processing stages** before reaching their final output.

#### Uses of Stream Processing

1. **Writing to storage:** Extract data from events and write it to a database, cache, search index, or similar system for querying by other clients. This keeps the storage system **in sync** with changes elsewhere, especially if the consumer is the only writer. It is the streaming equivalent of batch workflow outputs.
    
2. **Pushing to users:** Deliver events directly to users via email, push notifications, or real-time dashboards. Here, humans are the ultimate consumers of the stream.
    
3. **Stream processing:** Transform one or more input streams into output streams. Streams may pass through **multiple processing stages** before reaching their final output.

### Summary

**AMQP/JMS-style message broker**

- The broker assigns individual messages to consumers.
    
- Consumers acknowledge messages once processed.
    
- Messages are deleted after acknowledgment.
    
- Suitable for asynchronous RPC or task queues where message order and replaying old messages are not required.
    

**Log-based message broker**

- All messages in a partition go to the same consumer, maintaining order.
    
- Parallelism is achieved via partitioning.
    
- Consumers track progress by checkpointing offsets.
    
- Messages are retained on disk, allowing replay of old messages.
    
- Similar to database replication logs and log-structured storage engines.
    
- Ideal for stream processing, generating derived state or output streams.
    

**Sources of streams**

- User activity events, sensor readings, data feeds.
    
- Database writes represented as streams via **change data capture** or **event sourcing**.
    
- Log compaction enables retaining a full database snapshot.
    

**Benefits of stream-based database representation**

- Keeps derived systems (search indexes, caches, analytics) up to date.
    
- Allows building fresh views from the beginning of the log.
    
- Enables **stream joins** and **fault-tolerant processing**.
    

**Stream processing purposes**

- Detecting event patterns (complex event processing).
    
- Computing windowed aggregations (stream analytics).
    
- Maintaining derived data systems (materialized views).
    

**Time considerations**

- Distinguish between **processing time** and **event timestamps**.
    
- Handle **straggler events** that arrive late.
    

**Types of joins**

- **Stream-stream joins:** Match related events from two streams within a time window; can be a self-join.
    
- **Stream-table joins:** Join activity events with a database changelog; outputs enriched events.
    
- **Table-table joins:** Join two database changelogs to produce changes to a materialized view.
    

**Fault tolerance and exactly-once semantics**

- Discard partial output of failed tasks.
    
- Continuous stream processing requires **fine-grained recovery**: microbatching, checkpointing, transactions, or idempotent writes.