
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

