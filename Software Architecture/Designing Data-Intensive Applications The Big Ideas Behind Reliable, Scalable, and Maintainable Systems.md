
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

