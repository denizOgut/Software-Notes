

# PART I Strategic Design

The domain-driven design (DDD) methodology can be divided into two main parts: strategic design and tactical design. **==The strategic aspect of DDD deals with answering the questions of “what?” and “why?”—what software we are building and why we are building it. The tactical part is all about the “how”—how each component is implemented.==**

## Analyzing Business Domains

### What Is a Business Domain?

A business domain defines a company’s main area of activity. Generally speaking, it’s the service the company provides to its clients.

### What Is a Subdomain?

A subdomain is a fine-grained area of business activity. All of a company’s subdomains form its business domain: the service it provides to its customers. Implementing a single subdomain is not enough for a company to succeed; it’s just one building block in the overarching system.

#### Types of Subdomains

**Core subdomains**

**==A core subdomain is what a company does differently from its competitors==**

 - **==A core subdomain that is simple to implement can only provide a short-lived competitive advantage. Therefore, core subdomains are naturally complex**==
 - ==**It’s important to note that core subdomains are not necessarily technical. Not all business problems are solved through algorithms or other technical solutions. A company’s competitive advantage can come from various sources.==**

**Generic subdomains**

Generic subdomains are business activities that all companies are performing in the same way. Like core subdomains, generic subdomains are generally complex and hard to implement. However, **==generic subdomains do not provide any competitive edge for the company==**. There is no need for innovation or optimization here: battletested implementations are widely available, and all companies use them.

**Supporting subdomains**

contrary to core subdomains, **==supporting subdomains do not provide any competitive advantage.==**

The distinctive characteristic of supporting subdomains is the complexity of the solution’s  business logic. Supporting subdomains are simple. Their business logic resembles mostly data entry screens and ETL (extract, transform, load) operations; that is, the so-called CRUD (create, read, update, and delete) interfaces.

#### Comparing Subdomains

**Competitive advantage**

**==Only core subdomains provide a competitive advantage to a company. Core subdomains are the company’s strategy for differentiating itself from its competitors.==**

The more complex the problems a company is able to tackle, the more business value it can provide. The complex problems are not limited to delivering services to consumers. A complex problem can be, for example, making the business more optimized and efficient.

**Complexity**

identifying subdomains is essential for designing a sound software solution. Supporting subdomains’ business logic is simple

Generic subdomains are much more complicated. There should be a good reason why others have already invested time and effort in solving these problems.

From a knowledge availability perspective, **==generic subdomains are “known unknowns.” These are the things that you know you don’t know. Furthermore, this knowledge is readily available==**

Core subdomains are complex. They should be as hard for competitors to copy as possible—the company’s profitability depends on it. That’s why strategically, companies are looking to solve complex problems as their core subdomains.

it’s important to identify the core subdomains whose complexity will affect software design. Another useful guiding principle for identifying software-related core subdomains is to evaluate the complexity of the business logic that you will have to model and implement in code. Does the business logic resemble CRUD interfaces for data entry, or do you have to implement complex algorithms or business processes orchestrated by complex business rules and invariants?

![[Pasted image 20250614181319.png]]

**==core subdomains can change often==**. If a problem can be solved on the first attempt, it’s probably not a good competitive advantage—competitors will catch up fast. Consequently, solutions for core subdomains are emergent. Different implementations have to be tried out, refined, and optimized. Moreover, the work on core subdomains is never done. Companies continuously innovate and evolve core subdomains

supporting subdomains do not change often. They do not provide any competitive advantage for the company, and therefore the evolution of a supporting subdomain provides a minuscule business value compared to the same effort invested in a core subdomain.

Despite having existing solutions, generic subdomains can change over time. The changes can come in the form of security patches, bug fixes, or entirely new solutions to the generic problems.

**Solution strategy**

All subdomains are required for the company to work in its business domain. The subdomains are like foundational building blocks: take one away and the whole structure may fall down.

**==Core subdomains have to be implemented in-house. They cannot be bought or adopted==**; that would undermine the notion of competitive advantage, as the company’s competitors would be able to do the same.

**==Since core subdomains’ requirements are expected to change often and continuously, the solution must be maintainable and easy to evolve==**. Thus, core subdomains require implementation of the most advanced engineering techniques.

Since generic subdomains are hard but already solved problems, it’s more cost-effective to buy an off-the-shelf product or adopt an open source solution than invest time and effort into implementing a generic subdomain in-house

| Subdomain Type | Competitive Advantage | Complexity | Volatility | Implementation     | Problem     |
|----------------|------------------------|------------|------------|--------------------|-------------|
| Core           | Yes                    | High       | High       | In-house           | Interesting |
| Generic        | No                     | High       | Low        | Buy/adopt          | Solved      |
| Supporting     | No                     | Low        | Low        | In-house/outsource | Obvious     |

#### Identifying Subdomain Boundaries

The subdomains and their types are defined by the company’s business strategy: its business domains and how it differentiates itself to compete with other companies in the same field.

==**A good starting point is the company’s departments and other organizational units.**==

**Distilling subdomains**

Coarse-grained subdomains are a good starting point, but the devil is in the details. We have to make sure we are not missing important information hidden in the intricacies of the business function.

![[Pasted image 20250614182739.png]]

**Subdomains as coherent use cases**

From a technical perspective, subdomains resemble sets of interrelated, coherent use cases. Such sets of use cases usually involve the same actor, the business entities, and they all manipulate a closely related set of data.

**==the definition of “subdomains as a set of coherent use cases” as a guiding principle for when to stop looking for finer-grained subdomains. These are the most precise boundaries of the subdomains.==**

![[Pasted image 20250614182830.png]]

Should you always strive to identify such laser-focused subdomain boundaries? It is definitely necessary for core subdomains. Core subdomains are the most important, volatile, and complex. **==It’s essential that we distill them as much as possible since that will allow us to extract all generic and supporting functionalities and invest the effort on a much more focused functionality.==**

**Focus on the essentials**

Subdomains are a tool that alleviates the process of making software design decisions

When looking for subdomains, it’s important to identify business functions that are not related to software, acknowledge them as such, and focus on aspects of the business that are relevant to the software system you are working on.

### Who Are the Domain Experts?

Domain experts are subject matter experts who know all the intricacies of the business that we are going to model and implement in code. In other words, domain experts are knowledge authorities in the software’s business domain.

Domain experts represent the business. They are the people who identified the business problem in the first place and from whom all business knowledge originates.

As a rule of thumb, domain experts are either the people coming up with requirements or the software’s end users. The software is supposed to solve their problems.

### Conclusion

- **Core subdomains**
  - The interesting problems.
  - These are the activities the company is performing differently
    from its competitors and from which it gains its competitive advantage.

- **Generic subdomains**
  - The solved problems.
  - These are the things all companies are doing in the same
    way. There is no room or need for innovation here; rather than creating in-house
    implementations, it’s more cost-effective to use existing solutions.

- **Supporting subdomains**
  - The problems with obvious solutions.
  - These are the activities the company likely
    has to implement in-house, but that do not provide any competitive advantage.


## Discovering Domain Knowledge

> It’s developers’ (mis)understanding, not domain experts’ knowledge, that gets released in production.

### Business Problems

In the context of business domains, “problem” has a broader meaning. A business problem can be challenges associated with optimizing workflows and processes, minimizing manual labor, managing resources, supporting decisions, managing data, and so on

### Knowledge Discovery

To design an effective software solution, we have to grasp at least the basic knowledge of the business domain.

To be effective, the software has to mimic the domain experts’ way of thinking about the problem—their mental models. Without an understanding of the business problem and the reasoning behind the requirements, our solutions will be limited to “translating” business requirements into source code. What if the requirements miss a crucial edge case? Or fail to describe a business concept, limiting our ability to implement a model that will support future requirements?

**==software development is a learning process; working code is a side effect.==**

### Communication

effective communication is essential for knowledge sharing and project success

![[Pasted image 20250615113800.png]]

In any translation, information is lost; in this case, domain knowledge that is essential for solving business problems gets lost on its way to the software engineers.

![[Pasted image 20250615113934.png]]

### What Is a Ubiquitous Language?

Using a ubiquitous language is the cornerstone practice of domain-driven design. The idea is simple and straightforward: if parties need to communicate efficiently, instead of relying on translations, they have to speak the same language.

The traditional software development lifecycle implies the following translations:
• Domain knowledge into an analysis model
• Analysis model into requirements
• Requirements into system design
• System design into source code

Instead of continuously translating domain knowledge, domain-driven design calls for cultivating a single language for describing the business domain: the ubiquitous language

### Language of the Business

**==It’s crucial to emphasize that the ubiquitous language is the language of the business. As such, it should consist of business domain–related terms only==**. No technical jargon!

#### Consistency

**Ambiguous terms**

Ubiquitous language demands a single meaning for each term, so “policy” should be modeled explicitly using the two terms regulatory rule and insurance contract.

**Synonymous terms**

Two terms cannot be used interchangeably in a ubiquitous language ***user.*** domain experts’ lingo may reveal that user and other terms are used interchangeably: for example, user, visitor, administrator, account, etc.

Synonymous terms can seem harmless at first. However, in most cases, they denote different concepts

Understanding the differences between the terms in use allows for building simpler and clearer models and implementations of the business domain’s entities.

### Model of the Business Domain

#### What Is a Model?

> A model is a simplified representation of a thing or phenomenon that intentionally emphasizes certain aspects while ignoring others. Abstraction with a specific use in mind.

A model is not a copy of the real world but a human construct that helps us make sense of real-world systems.

#### Effective Modeling

All models have a purpose, and an effective model contains only the details needed to fulfill its purpose

**==a useful model is not a copy of the real world. Instead, a model is intended to solve a problem, and it should provide just enough information for that purpose==**

#### Modeling the Business Domain

The model is supposed to capture the domain experts’ mental models— their thought processes about how the business works to implement its function. The model has to reflect the involved business entities and their behavior, cause and effect relationships, and invariants.

**==the model is supposed to include just enough aspects of the business domain to make it possible to implement the required system; that is, to address the specific problem the software is intended to solve==**

Effective communication between engineering teams and domain experts is vital. The importance of this communication grows with the complexity of the business domain. The more complex the business domain is, the harder it is to model and implement its business logic in code.

#### Continuous Effort

All stakeholders should consistently use the ubiquitous language in all project-related communications to spread knowledge about and foster a shared understanding of the business domain. The language should be continuously reinforced throughout the project: requirements

Most importantly, cultivation of a ubiquitous language is an ongoing process. It should be constantly validated and evolved.

#### Tools

It’s important to make glossary maintenance a shared effort. When a ubiquitous language is changed, all team members should be encouraged to go ahead and update the glossary. That’s contrary to a centralized approach, in which only team leaders or architects are in charge of maintaining the glossary.

Despite the obvious advantages of maintaining a glossary of project-related terminology, it has an inherent limitation. Glossaries work best for “nouns”: names of entities, processes, roles, and so on. Although nouns are important, capturing the behavior is crucial.

Automated tests written in the Gherkin language are not only great tools for capturing the ubiquitous language but also act as an additional tool for bridging the gap between domain experts and software engineers

```gherken
Scenario: Notify the agent about a new support case
	Given Vincent Jules submits a new support case saying:
	"""
	I need help configuring AWS Infinidash
	"""
	When the ticket is assigned to Mr. Wolf
	Then the agent receives a notification about the new ticket
```

#### Challenges

The only reliable way to gather domain knowledge is to converse with domain experts. Quite often, the most important knowledge is tacit. It’s not documented or codified but resides only in the minds of domain experts. The only way to access it is to ask questions.

As you gain experience in this practice, you will notice that frequently, this process involves not merely discovering knowledge that is already there, but rather co-creating the model in tandem with domain experts. There may be ambiguities and even white spots in domain experts

### Conclusion

Effective communication and knowledge sharing are crucial for a successful software project

Domain-driven design’s ubiquitous language is an effective tool for bridging the  knowledge gap between domain experts and software engineers. It fosters communication and knowledge sharing by cultivating a shared language that can be used by all the stakeholders throughout the project: in conversations, documentation, tests, diagrams, source code, and so on.

All of a language’s terms have to be consistent—no ambiguous terms and no synonymous terms

Cultivating a ubiquitous language is a continuous process

Tools such as wiki-based glossaries and Gherkin tests can greatly alleviate the process of documenting and maintaining a ubiquitous language. However, the main prerequisite for an effective ubiquitous language is usage: the language has to be used consistently in all project-related communications

## Managing Domain Complexity

### Inconsistent Models

The term lead has different meanings in the marketing and sales departments:

On the one hand, we know the ubiquitous language has to be consistent—each term should have one meaning. On the other hand, we know the ubiquitous language has to reflect the domain experts’ mental models. In this case, the mental model of the “lead” is inconsistent among the domain experts

The traditional solution to this problem is to design a single model that can be used for all kinds of problems. Such models result in enormous entity relationship diagrams (ERDs) spanning whole office walls

![[Pasted image 20250616200936.png]]

Such models are supposed to be suitable for everything but eventually are effective for nothing. No matter what you do, you are always facing complexity: the complexity of filtering out extraneous details, the complexity of finding what you do need, and most importantly, the complexity of keeping the data in a consistent state.

Another solution would be to prefix the problematic term with a definition of the context: “marketing lead” and “sales lead.” That would allow the implementation of the two models in code. However, this approach has two main disadvantages. 
- First, it induces cognitive load. When should each model be used? The closer the implementations of the conflicting models are, the easier it is to make a mistake. 
- Second, the implementation of the model won’t be aligned with the ubiquitous language. No one would use the prefixes in conversations

### What Is a Bounded Context?

The solution in domain-driven design is trivial: divide the ubiquitous language into multiple smaller languages, then assign each one to the explicit context in which it can be applied: its bounded context.

![[Pasted image 20250616201253.png]]

The term lead exists in both bounded contexts As long as it bears a single meaning in each bounded context, each fine-grained ubiquitous language is consistent and follows the domain experts’ mental models.

#### Model Boundaries

**==a model is not a copy of the real world but a construct that helps us make sense of a complex system. The problem it is supposed to solve is an inherent part of a model—its purpose.==** A model cannot exist without a boundary; it will expand to become a copy of the real world. That makes defining a model’s boundary—its bounded contexts—an intrinsic part of the modeling process.

#### Ubiquitous Language Refined

A ubiquitous language is not universal.

**==Instead, a ubiquitous language is ubiquitous only in the boundaries of its bounded context. The language is focused on describing only the model that is encompassed by the bounded context. As a model cannot exist without a problem it is supposed to address, a ubiquitous language cannot be defined or used without an explicit context of its applicability.==**

#### Scope of a Bounded Context

Different domain experts held conflicting mental models of the same business entity. To model the business domain, we had to divide the model and define a strict applicability context for each fine-grained model—its bounded context.

![[Pasted image 20250616201659.png]]

Defining the scope of a ubiquitous language—its bounded context—is a strategic design decision. Boundaries can be wide, following the business domain’s inherent contexts, or narrow, further dividing the business domain into smaller problem domains.

**==A bounded context’s size, by itself, is not a deciding factor. Models shouldn’t necessarily be big or small. Models need to be useful.==** The wider the boundary of the ubiquitous language is, the harder it is to keep it consistent. It may be beneficial to divide a large ubiquitous language into smaller, more manageable problem domains, but striving for small bounded contexts can backfire too. The smaller they are, the more integration overhead the design induces.

keep your models useful and align the bounded contexts’ sizes with your business needs and organizational constraints. One thing to beware of is splitting a coherent functionality into multiple bounded contexts. Such division will hinder the ability to evolve each context independently. Instead, the same business requirements and changes will simultaneously affect the bounded contexts and require simultaneous deployment of the changes. To avoid such ineffective decomposition, use the rule of thumb to find subdomains: identify sets of coherent use cases that operate on the same data and avoid decomposing them into multiple bounded contexts.

### Bounded Contexts Versus Subdomains

#### Subdomains

To comprehend a company’s business strategy, we have to analyze its business domain. According to domain-driven design methodology, the analysis phase involves identifying the different subdomains (core, supporting, and generic). That’s how the organization works and plans its competitive strategy.

a subdomain resembles a set of interrelated use cases. The use cases are defined by the business domain and the system’s requirements

#### Bounded Contexts

Bounded contexts, on the other hand, are designed. Choosing models’ boundaries is a strategic design decision. We decide how to divide the business domain into smaller, manageable problem domains.

#### The Interplay Between Subdomains and Bounded Contexts

Theoretically, though impractically, a single model could span the entire business domain. This strategy could work for a small system

![[Pasted image 20250616202953.png]]

When conflicting models arise, we can follow the domain experts’ mental models and decompose the systems into bounded contexts

![[Pasted image 20250616203005.png]]

If the models are still large and hard to maintain, we can decompose them into even smaller bounded contexts; for example, by having a bounded context for each subdomain

![[Pasted image 20250616203029.png]]

Having a one-to-one relationship between bounded contexts and subdomains can be perfectly reasonable in some scenarios. In others, however, different decomposition strategies can be more suitable

**==It’s crucial to remember that subdomains are discovered and bounded contexts are designed.==**

### Boundaries

> Architectural design is system design. System design is contextual design—it is inherently about boundaries (what’s in, what’s out, what spans, what moves between), and about trade-offs. It reshapes what is outside, just as it shapes what is inside

The bounded context pattern is the domain-driven design tool for defining physical and ownership boundaries.

#### Physical Boundaries

Bounded contexts serve not only as model boundaries but also as physical boundaries of the systems implementing them. Each bounded context should be implemented as an individual service/project, meaning it is implemented, evolved, and versioned independently of other bounded contexts.

**==a bounded context can contain multiple subdomains. In such a case, the bounded context is a physical boundary, while each of its subdomains is a logical boundary. Logical boundaries bear different names in different programming languages: namespaces, modules, or packages.==**

#### Ownership Boundaries

The division of work between teams is another strategic decision that can be made using the bounded context pattern.

A bounded context should be implemented, evolved, and maintained by one team only. No two teams can work on the same bounded context. This segregation eliminates implicit assumptions that teams might make about one another’s models. Instead, they have to define communication protocols for integrating their models and systems explicitly.

![[Pasted image 20250616203640.png]]

### Conclusion

While subdomains are discovered, bounded contexts are designed. The division of the domain into bounded contexts is a strategic design decision.

A bounded context and its ubiquitous language can be implemented and maintained by one team. No two teams can share the work on the same bounded context. However, one team can work on multiple bounded contexts.

Bounded contexts decompose a system into physical components—services, subsystems, and so on. Each bounded context’s lifecycle is decoupled from the rest. Each bounded context can evolve independently from the rest of the system. However, the bounded contexts have to work together to form a system. Some of the changes will inadvertently affect another bounded context. In the next chapter, we’ll talk about the different patterns for integrating bounded contexts that can be used to protect them from cascading changes.

## Integrating Bounded Contexts

You cannot build a model without specifying its purpose—its boundary. The boundary divides the responsibility of languages. ==**A language in one bounded context can model the business domain to solve a particular problem. Another bounded context can represent the same business entities but model them to solve a different problem**.==

there will always be touchpoints between bounded contexts. These are called ***contracts***.

by definition, two bounded contexts are using different ubiquitous languages. Which language will be used for integration purposes? These integration concerns should be evaluated and addressed by the solution’s design.

### Cooperation

Cooperation patterns relate to bounded contexts implemented by teams with well established communication. the main criterion here is the quality of the teams’ communication and collaboration.

#### Partnership

In the partnership model, the integration between bounded contexts is coordinated in an ad hoc manner. One team can notify a second team about a change in the API, and the second team will cooperate and adapt—no drama or conflicts

![[Pasted image 20250621142213.png]]

Well-established collaboration practices, high levels of commitment, and frequent synchronizations between teams are required for successful integration in this manner. From a technical perspective, continuous integration of the changes applied by both teams is needed to further minimize the integration feedback loop.

#### Shared Kernel

there still can be cases when the same model of a subdomain, or a part of it, will be implemented in multiple bounded contexts. **==It’s crucial to stress that the shared model is designed according to the needs of all of the bounded contexts. Moreover, the shared model has to be consistent across all of the bounded contexts that are using it.==**

![[Pasted image 20250621142552.png]]

**Shared scope**

The overlapping model couples the lifecycles of the participating bounded contexts. A change made to the shared model has an immediate effect on all the bounded contexts. Hence, to minimize the cascading effects of changes, the overlapping model should be limited, exposing only that part of the model that has to be implemented by both bounded contexts.

**Implementation**

The shared kernel is implemented so that any modification to its source code is immediately reflected in all the bounded contexts using it.

If the organization uses the mono-repository approach, these can be the same source files referenced by multiple bounded contexts. If using a shared repository is not possible, the shared kernel can be extracted into a dedicated project and referenced in the bounded contexts as a linked library.

**When to use shared kernel**

The overarching applicability criterion for the shared kernel pattern is the cost of duplication versus the cost of coordination. Since the pattern introduces a strong dependency between the participating bounded contexts, it should be applied only when the cost of duplication is higher than the cost of coordination—**==in other words, only when integrating changes applied to the shared model by both bounded contexts will require more effort than coordinating the changes in the shared codebase==**

The difference between the integration and duplication costs depends on the volatility of the model. The more frequently it changes, the higher the integration costs will be. Therefore, the shared kernel will naturally be applied for the subdomains that change the most: the core subdomains.

If the participating bounded contexts are not implemented by the same team, introducing a shared kernel contradicts the principle that a single team should own a bounded context. The overlapping model—the shared kernel—is, in effect, being developed by multiple teams

That’s the reason why the use of a shared kernel has to be justified. It’s a pragmatic exception that should be considered carefully. A common use case for implementing a shared kernel is when communication or collaboration issues prevent implementing the partnership pattern

Another common use case for applying the shared kernel pattern, albeit a temporary one, is the gradual modernization of a legacy system. In such a scenario, the shared codebase can be a pragmatic intermediate solution for gradually decomposing the system into bounded contexts.

Finally, a shared kernel can be a good fit for integrating bounded contexts owned and implemented by the same team. In such a case, an ad hoc integration of the bounded contexts—a partnership—can “wash out” the contexts’ boundaries over time. A shared kernel can be used for explicitly defining the bounded contexts’ integration contracts.

### Customer–Supplier

one of the bounded contexts—the supplier—provides a service for its customers. The service provider is “upstream” and the customer or consumer is “downstream.”

![[Pasted image 20250621143256.png]]

Unlike in the cooperation case, both teams (upstream and downstream) can succeed independently. **==Consequently, in most cases we have an imbalance of power: either the upstream or the downstream team can dictate the integration contract.==**

#### Conformist

In some cases, the balance of power favors the upstream team, which has no real motivation to support its clients’ needs. Instead, it just provides the integration contract, defined according to its own model—take it or leave it. Such power imbalances can be caused by integration with service providers that are external to the organization or simply by organizational politics.

**==If the downstream team can accept the upstream team’s model, the bounded contexts’ relationship is called conformist==**

![[Pasted image 20250621143353.png]]

The downstream team’s decision to give up some of its autonomy can be justified in multiple ways

#### Anticorruption Layer

the balance of power in this relationship is still skewed toward the upstream service. However, in this case, the downstream bounded context is not willing to conform. Instead, it can translate the upstream bounded context’s model into a model tailored to its own needs via an anticorruption layer

![[Pasted image 20250621144802.png]]

The anticorruption layer pattern addresses scenarios in which it is not desirable or worth the effort to conform to the supplier’s model, such as the following:

**==From a modeling perspective, the translation of the supplier’s model isolates the downstream consumer from foreign concepts that are not relevant to its bounded context.==**

#### Open-Host Service

the power is skewed toward the consumers. The supplier is interested in protecting its consumers and providing the best service possible.

To protect the consumers from changes in its implementation model, the upstream supplier decouples the implementation model from the public interface. This decoupling allows the supplier to evolve its implementation and public models at different rates,

![[Pasted image 20250621144920.png]]

In a sense, the open-host service pattern is a reversal of the anticorruption layer pattern: instead of the consumer, the supplier implements the translation of its internal model.

Decoupling the bounded context’s implementation and integration models gives the upstream bounded context the freedom to evolve its implementation without affecting the downstream contexts.

Furthermore, the integration model’s decoupling allows the upstream bounded context to simultaneously expose multiple versions of the published language, allowing the consumer to migrate to the new version gradually

![[Pasted image 20250621145215.png]]

### Separate Ways

The last collaboration option is not to collaborate at all. This pattern can arise for different reasons, in cases where the teams are unwilling or unable to collaborate

#### Communication Issues

A common reason for avoiding collaboration is communication difficulties driven by the organization’s size or internal politics. When teams have a hard time collaborating and agreeing, it may be more cost-effective to go their separate ways and duplicate functionality in multiple bounded contexts.

#### Generic Subdomains

The nature of the duplicated subdomain can also be a reason for teams to go their separate ways. **==When the subdomain in question is generic, and if the generic solution is easy to integrate, it may be more cost-effective to integrate it locally in each bounded context.==**

#### Model Differences

Differences in the bounded contexts’ models can also be a reason to go with a separate ways collaboration. The models may be so different that a conformist relationship is impossible, and implementing an anticorruption layer would be more expensive than duplicating the functionality

> **==The separate ways pattern should be avoided when integrating core subdomains. Duplicating the implementation of such subdomains would defy the company’s strategy to implement them in the most effective and optimized way.==**

### Context Map

![[Pasted image 20250621145439.png]]

High-level design
A context map provides an overview of the system’s components and the models they implement.

Communication patterns
A context map depicts the communication patterns among teams—for example, which teams are collaborating and which prefer “less intimate” integration patterns, such as the anticorruption layer and separate ways patterns.

Organizational issues
A context map can give insight into organizational issues. For example, what does it mean if a certain upstream team’s downstream consumers all resort to implementing an anticorruption layer, or if all implementations of the separate ways pattern are concentrated around the same team?

#### Maintenance

Ideally, a context map should be introduced into a project right from the get-go, and be updated to reflect additions of new bounded contexts and modifications to the existing one.

Since the context map potentially contains information originating from the work of multiple teams, it’s best to define the maintenance of the context map as a shared effort: each team is responsible for updating its own integrations with other bounded contexts.

#### Limitations

It’s important to note that charting a context map can be a challenging task. When a system’s bounded contexts encompass multiple subdomains, there can be multiple integration patterns at play.

![[Pasted image 20250621145621.png]]

Moreover, even if bounded contexts are limited to a single subdomain, there still can be multiple integration patterns at play—for example, if the subdomains’ modules require different integration strategies.

### Conclusion

Bounded contexts are not independent. They have to interact with one another

Partnership
	Bounded contexts are integrated in an ad hoc manner.
Shared kernel
	Two or more bounded contexts are integrated by sharing a limited overlapping model that belongs to all participating bounded contexts.
Conformist
	The consumer conforms to the service provider’s model.
Anticorruption layer
	The consumer translates the service provider’s model into a model that fits the consumer’s needs.
Open-host service
	The service provider implements a published language—a model optimized for its consumers’ needs.
Separate ways
	It’s less expensive to duplicate particular functionality than to collaborate and integrate it.


# PART II Tactical Design

## Implementing Simple Business Logic

Business logic is the most important part of software. It’s the reason the software is being implemented in the first place.

### Transaction Script

> Organizes business logic by procedures where each procedure handles a single request from the presentation.

A system’s public interface can be seen as a collection of business transactions that consumers can execute, as shown in Figure 5-1. These transactions can retrieve information managed by the system, modify it, or both. The pattern organizes the system’s business logic based on procedures, where each procedure implements an operation that is executed by the system’s consumer via its public interface. In effect, the system’s public operations are used as encapsulation boundaries.

![[Pasted image 20250622122544.png]]

#### Implementation

Each procedure is implemented as a simple, straightforward procedural script. It can use a thin abstraction layer for integrating with storage mechanisms, but it is also free to access the databases directly.

**==The only requirement procedures have to fulfill is transactional behavior. Each operation should either succeed or fail but can never result in an invalid state==**

```java
DB.StartTransaction();
var job = DB.LoadNextJob();
var json = LoadFile(job.Source);
var xml = ConvertJsonToXml(json);
WriteFile(job.Destination, xml.ToString();
DB.MarkJobAsCompleted(job);
DB.Commit()
```

#### It’s Not That Easy!

the transaction script pattern is a foundation for the more advanced business logic implementation patterns you will learn in the forthcoming chapters. Furthermore, despite its apparent simplicity, it is the easiest pattern to get wrong. A considerable number of production issues I have helped to debug and fix, in one way or another, often boiled down to a miss-implementation of the transactional behavior of the system’s business logic.

**Lack of transactional behavior**

```java
public class LogVisit
{
    public void Execute(Guid userId, DateTime visitedOn)
    {
        _db.Execute("UPDATE Users SET last_visit=@p1 WHERE user_id=@p2",
            visitedOn, userId);
        _db.Execute(@"INSERT INTO VisitsLog(user_id, visit_date)
            VALUES(@p1, @p2)", userId, visitedOn);
    }
}
```

The issue can be due to anything from a network outage to a database timeout or deadlock, or even a crash of the server executing the process.

This can be fixed by introducing a proper transaction encompassing both data changes:

```java
public class LogVisit
{
    public void Execute(Guid userId, DateTime visitedOn)
    {
        try
        {
            _db.StartTransaction();
            _db.Execute(@"UPDATE Users SET last_visit=@p1
                WHERE user_id=@p2",
                visitedOn, userId);
            _db.Execute(@"INSERT INTO VisitsLog(user_id, visit_date)
                VALUES(@p1, @p2)",
                userId, visitedOn);
            _db.Commit();
        }
        catch
        {
            _db.Rollback();
            throw;
        }
    }
}
```

**Distributed transactions**

In modern distributed systems, it’s a common practice to make changes to the data in a database and then notify other components of the system about the changes by publishing messages into a message bus.

```java
public class LogVisit
{
    public void Execute(Guid userId, DateTime visitedOn)
    {
        _db.Execute("UPDATE Users SET last_visit=@p1 WHERE user_id=@p2",
            visitedOn, userId);
        _messageBus.Publish("VISITS_TOPIC",
            new { UserId = userId, VisitDate = visitedOn });
    }
}
```

Distributed transactions spanning multiple storage mechanisms are complex, hard to scale, error prone, and therefore are usually avoided

**Implicit distributed transactions**

```java
public class LogVisit
{
    public void Execute(Guid userId)
    {
        _db.Execute("UPDATE Users SET visits=visits+1 WHERE user_id=@p1",
            userId);
    }
}
```

Instead of tracking the last visit date as in the previous examples, this method maintains a counter of visits for each user. Calling the method increases the corresponding counter’s value by 1. All the method does is update one value, in one table, residing in one database. Yet this is still a distributed transaction that can potentially lead to inconsistent state.

This example constitutes a distributed transaction because it communicates information to the databases and the external process that called the method

Although the execute method is of type void, that is, it doesn’t return any data, it still communicates whether the operation has succeeded or failed: if it failed, the caller will get an exception. What if the method succeeds, but the communication of the result to the caller fails?

As in the previous example, there is no simple fix for this issue. It all depends on the business domain and its needs. In this specific example, one way to ensure transactional behavior is to make the operation idempotent: that is, leading to the same result even if the operation repeated multiple times.

```java
public class LogVisit
{
    public void Execute(Guid userId, long visits)
    {
        _db.Execute("UPDATE Users SET visits = @p1 WHERE user_id=@p2",
            visits, userId);
    }
}
```

Another way to address such an issue is to use optimistic concurrency control: prior to calling the ``LogVisit`` operation, the caller has read the counter’s current value and passed it to ``LogVisit`` as a parameter. ``LogVisit`` will update the counter’s value only if it equals the one initially read by the caller:

```java
public class LogVisit
{
    public void Execute(Guid userId, long expectedVisits)
    {
        _db.Execute(@"UPDATE Users SET visits=visits+1
            WHERE user_id=@p1 and visits = @p2",
            userId, expectedVisits);
    }
}
```

#### When to Use Transaction Script

The transaction script pattern is well adapted to the most straightforward problem domains in which the business logic resembles simple procedural operation

![[Pasted image 20250622123317.png]]

**==The transaction script pattern naturally fits supporting subdomains where, by definition, the business logic is simple. It can also be used as an adapter for integration with external systems==**

**==The main advantage of the transaction script pattern is its simplicity. It introduces minimal abstractions and minimizes the overhead both in runtime performance and in understanding the business logic. That said, this simplicity is also the pattern’s disadvantage. The more complex the business logic gets, the more it’s prone to duplicate business logic across transactions, and consequently, to result in inconsistent behavior— when the duplicated code goes out of sync. As a result, transaction script should never be used for core subdomains, as this pattern won’t cope with the high complexity of a core subdomain’s business logic.==**

### Active Record

> An object that wraps a row in a database table or view, encapsulates the database access, and adds domain logic on that data.

active record supports cases where the business logic is simple. Here, however, the business logic may operate on more complex data structures.

![[Pasted image 20250622124455.png]]

Operating on such data structures via a simple transaction script would result in lots of repetitive code. The mapping of the data to an in-memory representation would be duplicated all over.

#### Implementation

Consequently, this pattern uses dedicated objects, known as active records, to represent complicated data structures. Apart from the data structure, these objects also implement data access methods for creating, reading, updating, and deleting records—the so-called CRUD operations. As a result, the active record objects are coupled to an object-relational mapping (ORM) or some other data access framework. The pattern’s name is derived from the fact that each data structure is “active”; that is, it implements data access logic.

```java
public class CreateUser
{
    public void Execute(UserDetails userDetails)
    {
        try
        {
            _db.StartTransaction();
            var user = new User();
            user.Name = userDetails.Name;
            user.Email = userDetails.Email;
            user.Save();
            _db.Commit();
        }
        catch
        {
            _db.Rollback();
            throw;
        }
    }
}
```

The pattern’s goal is to encapsulate the complexity of mapping the in-memory object to the database’s schema. In addition to being responsible for persistence, the active record objects can contain business logic; for example, validating new values assigned to the fields, or even implementing business-related procedures that manipulate an object’s data

#### When to Use Active Record

**==Because an active record is essentially a transaction script that optimizes access to databases, this pattern can only support relatively simple business logic, such as CRUD operations, which, at most, validate the user’s input.**==

==**The active record pattern is also known as an anemic domain model antipattern; in other words, an improperly designed domain model==**

>It’s important to stress that in this context, active record refers to the design pattern, not the Active Record framework. The pattern name was coined in Patterns of Enterprise Application Architecture by Martin Fowler. The framework came later as one way to implement the pattern. In our context, we are talking about the design pattern and the concepts behind it, not a specific implementation.

### Conclusion

Transaction script
	This pattern organizes the system’s operations as simple, straightforward procedural scripts. The procedures ensure that each operation is transactional—either it succeeds or it fails. The transaction script pattern lends itself to supporting subdomains, with business logic resembling simple, ETL-like operations.

Active record
	When the business logic is simple but operates on complicated data structures, you can implement those data structures as active records. An active record object is a data structure that provides simple CRUD data access methods.

## Tackling Complex Business Logic

### History

The pattern is “domain model,” and the aggregates and value objects are its building blocks.

### Domain Model

The domain model pattern is intended to cope with cases of complex business logic. Here, instead of CRUD interfaces, we deal with complicated state transitions, business rules, and invariants: rules that have to be protected at all times.

#### Implementation

A domain model is an object model of the domain that incorporates both behavior and data.1 DDD’s tactical patterns—aggregates, value objects, domain events, and domain services—are the building blocks of such an object model.

All of these patterns share a common theme: they put the business logic first

**Complexity**

The domain’s business logic is already inherently complex, so the objects used for modeling it should not introduce any additional accidental complexities. The model should be devoid of any infrastructural or technological concerns, such as implementing calls to databases or other external components of the system. This restriction requires the model’s objects to be plain old objects, objects implementing business logic without relying on or directly incorporating any infrastructural components or frameworks

**Ubiquitous language**

The emphasis on business logic instead of technical concerns makes it easier for the domain model’s objects to follow the terminology of the bounded context’s ubiquitous language. In other words, **==this pattern allows the code to “speak” the ubiquitous language and to follow the domain experts’ mental models==**

#### Building Blocks

**Value object**

A value object is an object that can be identified by the composition of its values

```java
public class Color
{
    private int _red;
    private int _green;
    private int _blue;
}
```

**Ubiquitous language**

Relying exclusively on the language’s standard library’s primitive data types—such as strings, integers, or dictionaries—to represent concepts of the business domain is known as the ***primitive obsession*** code smell

```java
class Person
{
	private int _id;
	private string _firstName;
	private string _lastName;
	private string _landlinePhone;
	private string _mobilePhone;
	private string _email;
	private int _heightMetric;
	private string _countryCode;
	public Person(...) {...}
}
static void Main(string[] args)
{
	var dave = new Person(
	id: 30217,
	firstName: "Dave",
	lastName: "Ancelovici",
	landlinePhone: "023745001",
	mobilePhone: "0873712503",
	email: "dave@learning-ddd.com",
	heightMetric: 180,
	countryCode: "BG");
}
```

**==This approach presents multiple design risks. First, the validation logic tends to be duplicated. Second, it’s hard to enforce calling the validation logic before the values are used. It will become even more challenging in the future, when the codebase will be evolved by other engineers.==**

```java
public class Person
{
    private PersonId _id;
    private Name _name;
    private PhoneNumber _landline;
    private PhoneNumber _mobile;
    private EmailAddress _email;
    private Height _height;
    private CountryCode _country;

    public Person(PersonId id, Name name, PhoneNumber landline, PhoneNumber mobile, 
                  EmailAddress email, Height height, CountryCode country)
    {
        _id = id;
        _name = name;
        _landline = landline;
        _mobile = mobile;
        _email = email;
        _height = height;
        _country = country;
    }
}

public static void Main(string[] args)
{
    var dave = new Person(
        id: new PersonId(30217),
        name: new Name("Dave", "Ancelovici"),
        landline: PhoneNumber.Parse("023745001"),
        mobile: PhoneNumber.Parse("0873712503"),
        email: EmailAddress.Parse("dave@learning-ddd.com"),
        height: Height.FromMetric(180),
        country: CountryCode.Parse("BG"));
}
```

First, notice the increased clarity.

Second, there is no need to validate the values before the assignment, as the validation logic resides in the value objects themselves. However, a value object’s behavior is not limited to mere validation. **==Value objects shine brightest when they centralize the business logic that manipulates the values.==**

```java
var heightMetric = Height.Metric(180); var heightImperial = Height.Imperial(5, 3); var string1 = heightMetric.ToString(); // "180cm" 
var string2 = heightImperial.ToString(); // "5 feet 3 inches" 
var string3 = heightMetric.ToImperial().ToString(); // "5 feet 11 inches" 
var firstIsHigher = heightMetric > heightImperial; // true

var phone = PhoneNumber.Parse("+359877123503"); 
var country = phone.Country; // "BG" 
var phoneType = phone.PhoneType; // "MOBILE" 
var isValid = PhoneNumber.IsValid("+972120266680"); // false

var red = Color.FromRGB(255, 0, 0); 
var green = Color.Green; 
var yellow = red.MixWith(green);
var yellowString = yellow.ToString(); // "#FFFF00"
```

**Implementation**. **==Since a change to any of the fields of a value object results in a different value, value objects are implemented as immutable objects==**. A change to one of the value object’s fields conceptually creates a different value—a different instance of a value object.

```java

public class Color
{
    public readonly byte Red;
    public readonly byte Green;
    public readonly byte Blue;

    public Color(byte r, byte g, byte b)
    {
        this.Red = r;
        this.Green = g;
        this.Blue = b;
    }

    public Color MixWith(Color other)
    {
        return new Color(
            r: (byte)Math.Min(this.Red + other.Red, 255),
            g: (byte)Math.Min(this.Green + other.Green, 255),
            b: (byte)Math.Min(this.Blue + other.Blue, 255)
        );
    }
}
```

**==When to use value objects. The simple answer is, whenever you can==**. Not only do value objects make the code more expressive and encapsulate business logic that tends to spread apart, but the pattern makes the code safer. Since value objects are immutable, the value objects’ behavior is free of side effects and is thread safe.

**==From a business domain perspective, a useful rule of thumb is to use value objects for the domain’s elements that describe properties of other objects==**

**Entities**
**==An entity is the opposite of a value object. It requires an explicit identification field to distinguish between the different instances of the entity.==**

```java
class Person
{
	public Name Name { get; set; }
	public Person(Name name)
	{
		this.Name = name;
	}
}


class Person
	{
	public readonly PersonId Id;
	public Name Name { get; set; }
	public Person(PersonId id, Name name)
	{
		this.Id = id;
		this.Name = name;
	}
}
```

**==The central requirement for the identification field is that it should be unique for each instance of the entity==**: for each person, in our case (Figure 6-2). Furthermore, except for very rare exceptions, the value of an entity’s identification field should remain immutable throughout the entity’s lifecycle. This brings us to the second conceptual difference between value objects and entities.

**==Contrary to value objects, entities are mutable and expected to change over time==**. Another key difference is that value objects describe an entity’s properties. For example, as shown earlier in the chapter, the `Person` entity includes two value objects, `PersonId` and `Name`, which define characteristics of each `Person` instance.

Entities are an essential building block of any business domain we don’t implement entities independently, but only in the context of the aggregate pattern.

**Aggregates**

**==An aggregate is an entity: it requires an explicit identification field and its state is expected to change during an instance’s lifecycle==**. However, it is much more than just an entity. The goal of the pattern is to protect the consistency of its data. Since an aggregate’s data is mutable, there are implications and challenges that the pattern has to address to keep its state consistent at all times

**Consistency enforcement**

Since an aggregate’s state can be mutated, it creates an opening for multiple ways in which its data can become corrupted. To enforce consistency of the data, the aggregate pattern draws a clear boundary between the aggregate and its outer scope: the aggregate is a consistency enforcement boundary. The aggregate’s logic has to validate all incoming modifications and ensure that the changes do not contradict its business rules.

From an implementation perspective, the consistency is enforced by allowing only the aggregate’s business logic to modify its state. All processes or objects external to the aggregate are only allowed to read the aggregate’s state. Its state can only be mutated by executing corresponding methods of the aggregate’s public interface.

**==The state-modifying methods exposed as an aggregate’s public interface are often referred to as commands, as in “a command to do something.” A command can be implemented in two ways. First, it can be implemented as a plain public method of the aggregate object:==**

```java
public class Ticket
{
...
	public void AddMessage(UserId from, string body)
	{
		var message = new Message(from, body);
		_messages.Append(message);
	}
...
}
```

Alternatively, a command can be represented as a parameter object that encapsulates all the input required for executing the command:

```java
public class Ticket
{
...
	public void Execute(AddMessage cmd)
	{
		var message = new Message(cmd.from, cmd.body);
		_messages.Append(message);
	}
...
}
```

How commands are expressed in an aggregate’s code is a matter of preference

**==An aggregate’s public interface is responsible for validating the input and enforcing all of the relevant business rules and invariants. This strict boundary also ensures that all business logic related to the aggregate is implemented in one place: the aggregate itself.==**

```java

### Properly Indented Code:

```csharp
public class TicketService
{
    private readonly ITicketRepository _ticketRepository;

    public TicketService(ITicketRepository ticketRepository)
    {
        _ticketRepository = ticketRepository;
    }

    public ExecutionResult Escalate(TicketId id, EscalationReason reason)
    {
        try
        {
            var ticket = _ticketRepository.Load(id);
            var cmd = new Escalate(reason);
            ticket.Execute(cmd);
            _ticketRepository.Save(ticket);
            return ExecutionResult.Success();
        }
        catch (ConcurrencyException ex)
        {
            return ExecutionResult.Error(ex);
        }
    }
}
```

It’s vital to protect the consistency of an aggregate’s state

When committing a change to the database, we have to ensure that the version that is being overwritten matches the one that was originally read.

**Transaction boundary**. Since an aggregate’s state can only be modified by its own business logic, the aggregate also acts as a transactional boundary. All changes to the aggregate’s state should be committed transitionally as one atomic operation. If an aggregate’s state is modified, either all the changes are committed or none of them is.

**==Furthermore, no system operation can assume a multi-aggregate transaction. A change to an aggregate’s state can only be committed individually, one aggregate per database transaction.==**

**Hierarchy of entities**

we don’t use entities as an independent pattern, only as part of an aggregate. Let’s see the fundamental difference between entities and aggregates, and why entities are a building block of an aggregate rather than of the overarching domain model.

DDD prescribes that a system’s design should be driven by its business domain. Aggregates are no exception. To support changes to multiple objects that have to be applied in one atomic transaction, the aggregate pattern resembles a hierarchy of entities, all sharing transactional consistency

The hierarchy contains both entities and value objects, and all of them belong to the same aggregate if they are bound by the domain’s business logic.

**==That’s why the pattern is named “aggregate”: it aggregates business entities and value objects that belong to the same transaction boundary.==**

```java
public class Ticket
{
    private readonly TicketId _id;
    private readonly PersonId _ownerId;
    private List<Message> _messages;
    private UserId _agent;
    private bool _isEscalated;
    private double _remainingTimePercentage;

    public Ticket(TicketId id, PersonId ownerId)
    {
        _id = id;
        _ownerId = ownerId;
        _messages = new List<Message>();
        _isEscalated = false;
        _remainingTimePercentage = 1.0; // 100% remaining time initially
    }

    public bool IsEscalated => _isEscalated;
    public double RemainingTimePercentage => _remainingTimePercentage;
    public UserId AssignedAgent => _agent;

    public void Execute(Escalate cmd)
    {
        _isEscalated = true;
        // Additional escalation logic (from previous context)
    }

    public void Execute(EvaluateAutomaticActions cmd)
    {
        if (this.IsEscalated && this.RemainingTimePercentage < 0.5 &&
            GetUnreadMessagesCount(for: AssignedAgent) > 0)
        {
            _agent = AssignNewAgent();
        }
    }

    public int GetUnreadMessagesCount(UserId id)
    {
        return _messages.Where(x => x.To == id && !x.WasRead).Count();
    }

    private UserId AssignNewAgent()
    {
        // Placeholder: Logic to assign a new agent (e.g., from a service or repository)
        return new UserId(Guid.NewGuid().ToString());
    }
}
```

The aggregate ensures that all the conditions are checked against strongly consistent data, and it won’t change after the checks are completed by ensuring that all changes to the aggregate’s data are performed as one atomic transaction.

**Referencing other aggregates**. Since all objects contained by an aggregate share the same transactional boundary, performance and scalability issues may arise if an aggregate grows too large.

The consistency of the data can be a convenient guiding principle for designing an aggregate’s boundaries. Only the information that is required by the aggregate’s business logic to be strongly consistent should be a part of the aggregate. All information that can be eventually consistent should reside outside of the aggregate’s boundary

![[Pasted image 20250623203753.png]]

**==The rule of thumb is to keep the aggregates as small as possible and include only objects that are required to be in a strongly consistent state by the aggregate’s business logic:==**

```java
public class Ticket
{
	private UserId _customer;
	private List<ProductId> _products;
	private UserId _assignedAgent;
	private List<Message> _messages;
	...
}
```

**==The reasoning behind referencing external aggregates by ID is to reify that these objects do not belong to the aggregate’s boundary, and to ensure that each aggregate has its own transactional boundary==**

To decide whether an entity belongs to an aggregate or not, examine whether the aggregate contains business logic that can lead to an invalid system state if it will work on eventually consistent data.

**The aggregate root**

an aggregate’s state can only be modified by executing one of its commands. Since an aggregate represents a hierarchy of entities, only one of them should be designated as the aggregate’s public interface—the aggregate root,

![[Pasted image 20250623203956.png]]

In addition to the aggregate root’s public interface, there is another mechanism through which the outer world can communicate with aggregates: domain events.

**Domain events**. A domain event is a message describing a significant event that has occurred in the business domain. For example:
• Ticket assigned
• Ticket escalated
• Message received

**==Since domain events describe something that has already happened, their names should be formulated in the past tense.**==

==**The goal of a domain event is to describe what has happened in the business domain and provide all the necessary data related to the event==**

```json
{
"ticket-id": "c9d286ff-3bca-4f57-94d4-4d4e490867d1",
"event-id": 146,
"event-type": "ticket-escalated",
"escalation-reason": "missed-sla",
"escalation-time": 1628970815
}
```

Domain events are part of an aggregate’s public interface. An aggregate publishes its domain events. Other processes, aggregates, or even external systems can subscribe to and execute their own logic in response to the domain events

![[Pasted image 20250623204350.png]]

```java
public class Ticket
{
    private List<DomainEvent> _domainEvents;

    public void Execute(RequestEscalation cmd)
    {
        if (!this.IsEscalated && this.RemainingTimePercentage <= 0)
        {
            this.IsEscalated = true;
            var escalatedEvent = new TicketEscalated(_id, cmd.Reason);
            _domainEvents.Append(escalatedEvent);
        }
    }
}
```

**Ubiquitous language**. Last but not least, aggregates should reflect the ubiquitous language. The terminology that is used for the aggregate’s name, its data members, its actions, and its domain events all should be formulated in the bounded context’s ubiquitous language. As Eric Evans put it, the code must be based on the same language the developers use when they speak with one another and with domain experts. This is especially important for implementing complex business logic.

**Domain services**

Sooner or later, you may encounter business logic that either doesn’t belong to any aggregate or value object, or that seems to be relevant to multiple aggregates. In such cases, domain-driven design proposes to implement the logic as a domain service. A domain service is a stateless object that implements the business logic. In the vast majority of cases, such logic orchestrates calls to various components of the system to perform some calculation or analysis

```java
public class ResponseTimeFrameCalculationService
{
    public ResponseTimeframe CalculateAgentResponseDeadline(UserId agentId, Priority priority, bool escalated, DateTime startTime)
    {
        var policy = _departmentRepository.GetDepartmentPolicy(agentId);
        var maxProcTime = policy.GetMaxResponseTimeFor(priority);
        if (escalated) {
            maxProcTime = maxProcTime * policy.EscalationFactor;
        }
        var shifts = _departmentRepository.GetUpcomingShifts(agentId, startTime, startTime.Add(policy.MaxAgentResponseTime));
        return CalculateTargetTime(maxProcTime, shifts);
    }
}
```

**==Domain services make it easy to coordinate the work of multiple aggregates==**. However, it is important to always keep in mind the aggregate pattern’s limitation of modifying only one instance of an aggregate in one database transaction. Domain services are not a loophole around this limitation. The rule of one instance per transaction still holds true. Instead, domain services lend themselves to implementing calculation logic that requires reading the data of multiple aggregates.

### Managing Complexity

A system’s degrees of freedom are the data points needed to describe its state

```java
public class ClassA
{
    public int A { get; set; }
    public int B { get; set; }
    public int C { get; set; }
    public int D { get; set; }
    public int E { get; set; }
}

public class ClassB
{
    private int _a, _d;

    public int A
    {
        get => _a;
        set
        {
            _a = value;
            B = value / 2;
            C = value / 3;
        }
    }

    public int B { get; private set; }
    public int C { get; private set; }

    public int D
    {
        get => _d;
        set
        {
            _d = value;
            E = value * 2;
        }
    }

    public int E { get; private set; }
}
```

An aggregate can only be modified by its own methods. Its business logic encapsulates and protects business invariants, thus reducing the degrees of freedom.

Since the domain model pattern is applied only for subdomains with complex business logic, it’s safe to assume that these are core subdomains—the heart of the software.

### Conclusion

- **Value objects**
  - Concepts of the business domain that can be identified exclusively by their values and thus do not require an explicit ID field.
  - Since a change in one of the fields semantically creates a new value, value objects are immutable.
  - Value objects model not only data, but behavior as well: methods manipulating the values and thus initializing new value objects.
- **Aggregates**
  - A hierarchy of entities sharing a transactional boundary.
  - All of the data included in an aggregate’s boundary has to be strongly consistent to implement its business logic.
  - The state of the aggregate, and its internal objects, can only be modified through its public interface, by executing the aggregate’s commands.
  - The data fields are read-only for external components for the sake of ensuring that all the business logic related to the aggregate resides in its boundaries.
  - The aggregate acts as a transactional boundary.
  - All of its data, including all of its internal objects, has to be committed to the database as one atomic transaction.
  - An aggregate can communicate with external entities by publishing domain events—messages describing important business events in the aggregate’s lifecycle.
  - Other components can subscribe to the events and use them to trigger the execution of business logic.
- **Domain services**
  - A stateless object that hosts business logic that naturally doesn’t belong to any of the domain model’s aggregates or value objects.


## Modeling the Dimension of Time

The difference between these implementation patterns lies in the way the aggregates’ state is persisted. The event-sourced domain model uses the event sourcing pattern to manage the aggregates’ states: instead of persisting an aggregate’s state, the model generates domain events describing each change and uses them as the source of truth for the aggregate’s data.

### Event Sourcing

> Show me your flowchart and conceal your tables, and I shall continue to be mystified. Show me your tables, and I won’t usually need your flowchart; it’ll be obvious.

**==The table’s data documents the leads’ current states, but it misses the story of how each lead got to their current state==**. We can’t analyze what was happening during the lifecycles of leads

From a business standpoint, it’s crucial to analyze the data and optimize the process based on the experience. One of the ways to fill in the missing information is to use event sourcing.

The event sourcing pattern introduces the dimension of time into the data model. Instead of the schema reflecting the aggregates’ current state, an event sourcing– based system persists events documenting every change in an aggregate’s lifecycle.

```json
{
"lead-id": 12,
"event-id": 0,
"event-type": "lead-initialized",
"first-name": "Casey",
"last-name": "David",
"phone-number": "555-2951",
"timestamp": "2020-05-20T09:52:55.95Z"
},
{
"lead-id": 12,
"event-id": 1,
"event-type": "contacted",
"timestamp": "2020-05-20T12:32:08.24Z"
},
{
"lead-id": 12,
"event-id": 2,
"event-type": "followup-set",
"followup-on": "2020-05-27T12:00:00.00Z",
"timestamp": "2020-05-20T12:32:08.24Z"
},
{
"lead-id": 12,
"event-id": 3,
"event-type": "contact-details-updated",
"first-name": "Casey",
"last-name": "Davis",
"phone-number": "555-8101",
"timestamp": "2020-05-20T12:32:08.24Z"
},
{
"lead-id": 12,
"event-id": 4,
"event-type": "contacted",
"timestamp": "2020-05-27T12:02:12.51Z"
},
{
"lead-id": 12,
"event-id": 5,
"event-type": "order-submitted",
"payment-deadline": "2020-05-30T12:02:12.51Z",
"timestamp": "2020-05-27T12:02:12.51Z"
},
{
"lead-id": 12,
"event-id": 6,
"event-type": "payment-confirmed",
"status": "converted",
"timestamp": "2020-05-27T12:38:44.12Z"
}
```

The events in the listing tell the customer’s story. As we saw earlier, the customer’s state can easily be projected out from these domain events.

```java
public class LeadSearchModelProjection

{

    public long LeadId { get; private set; }

    public HashSet<string> FirstNames { get; private set; }

    public HashSet<string> LastNames { get; private set; }

    public HashSet<PhoneNumber> PhoneNumbers { get; private set; }

    public int Version { get; private set; }

  

    public void Apply(LeadInitialized @event)

    {

        LeadId = @event.LeadId;

        FirstNames = new HashSet<string>();

        LastNames = new HashSet<string>();

        PhoneNumbers = new HashSet<PhoneNumber>();

        FirstNames.Add(@event.FirstName);

        LastNames.Add(@event.LastName);

        PhoneNumbers.Add(@event.PhoneNumber);

        Version = 0;

    }

  

    public void Apply(ContactDetailsChanged @event)

    {

        FirstNames.Add(@event.FirstName);

        LastNames.Add(@event.LastName);

        PhoneNumbers.Add(@event.PhoneNumber);

        Version += 1;

    }

  

    public void Apply(Contacted @event)

    {

        Version += 1;

    }

  

    public void Apply(FollowupSet @event)

    {

        Version += 1;

    }

  

    public void Apply(OrderSubmitted @event)

    {

        Version += 1;

    }

  

    public void Apply(PaymentConfirmed @event)

    {

        Version += 1;

    }

}
```

Pay attention to the Version field that is incremented after applying each event. Its value represents the total number of modifications made to the business entity. Moreover, suppose we apply a subset of events. In that case, we can “travel through time”: we can project the entity’s state at any point of its lifecycle by applying only the relevant events

#### Search

You have to implement a search. However, since a lead’s contact information can be updated—first name, last name, and phone number—sales agents may not be aware of the changes applied by other agents and may want to locate leads using their contact information, including historical values. We can easily project the historical information:

```java
public class LeadSearchModelProjection

{

    public long LeadId { get; private set; }

    public HashSet<string> FirstNames { get; private set; }

    public HashSet<string> LastNames { get; private set; }

    public HashSet<PhoneNumber> PhoneNumbers { get; private set; }

    public int Version { get; private set; }

  

    public void Apply(LeadInitialized @event)

    {

        LeadId = @event.LeadId;

        FirstNames = new HashSet<string>();

        LastNames = new HashSet<string>();

        PhoneNumbers = new HashSet<PhoneNumber>();

        FirstNames.Add(@event.FirstName);

        LastNames.Add(@event.LastName);

        PhoneNumbers.Add(@event.PhoneNumber);

        Version = 0;

    }

  

    public void Apply(ContactDetailsChanged @event)

    {

        FirstNames.Add(@event.FirstName);

        LastNames.Add(@event.LastName);

        PhoneNumbers.Add(@event.PhoneNumber);

        Version += 1;

    }

  

    public void Apply(Contacted @event)

    {

        Version += 1;

    }

  

    public void Apply(FollowupSet @event)

    {

        Version += 1;

    }

  

    public void Apply(OrderSubmitted @event)

    {

        Version += 1;

    }

  

    public void Apply(PaymentConfirmed @event)

    {

        Version += 1;

    }

}
```

```json
LeadId: 12
FirstNames: ['Casey']
LastNames: ['David', 'Davis']
PhoneNumbers: ['555-2951', '555-8101']
Version: 6
```

#### Analysis

Your business intelligence department asks you to provide a more analysis-friendly representation of the leads data. For their current research, they want to get the number of follow-up calls scheduled for different leads. Later they will filter the converted and closed leads data and use the model to optimize the sales process

#### Source of Truth

**==For the event sourcing pattern to work, all changes to an object’s state should be represented and persisted as events==**. These events become the system’s source of truth

![[Pasted image 20250628105354.png]]

The database that stores the system’s events is the only strongly consistent storage: the system’s source of truth. The accepted name for the database that is used for persisting events is event store.

#### Event Store

**==The event store should not allow modifying or deleting the events since it’s append only storage==**. To support implementation of the event sourcing pattern, at a minimum the event store has to support the following functionality: fetch all events belonging to a specific business entity and append the events. For example

```java
interface IEventStore
{
	IEnumerable<Event> Fetch(Guid instanceId);
	void Append(Guid instanceId, Event[] newEvents, int expectedVersion);
}
```

> In essence, the event sourcing pattern is nothing new. The financial industry uses events to represent changes in a ledger. A ledger is an append-only log that documents transactions. A current state (e.g., account balance) can always be deduced by “projecting” the ledger’s records.

### Event-Sourced Domain Model

**==The original domain model maintains a state representation of its aggregates and emits select domain events. The event-sourced domain model uses domain events exclusively for modeling the aggregates’ lifecycles. All changes to an aggregate’s state have to be expressed as domain events.==**

• Load the aggregate’s domain events.
• Reconstitute a state representation—project the events into a state representation that can be used to make business decisions.
• Execute the aggregate’s command to execute the business logic, and consequently, produce new domain events.
• Commit the new domain events to the event store.

**Why “Event-Sourced Domain Model”?**

---

I feel obliged to explain why I use the term event-sourced domain model rather than just event sourcing. Using events to represent state transitions—the event sourcing pattern—is possible with or without the domain model’s building blocks. Therefore, I prefer the longer term to explicitly state that we are using event sourcing to represent changes in the lifecycles of the domain model’s aggregates.

---

#### Advantages

Compared to the more traditional model, in which the aggregates’ current states are persisted in a database, the event-sourced domain model requires more effort to model the aggregates. However, this approach brings significant advantages that make the pattern worth considering in many scenarios:

**Time traveling**
	Just as the domain events can be used to reconstitute an aggregate’s current state, they can also be used to restore all past states of the aggregate. In other words, you can always reconstitute all the past states of an aggregate.
	This is often done when analyzing the system’s behavior, inspecting the system’s decisions, and optimizing the business logic.
	Another common use case for reconstituting past states is retroactive debugging: you can revert the aggregate to the exact state it was in when a bug was observed


**Deep insight**
	optimizing core subdomains is strategically important for the business. Event sourcing provides deep insight into the system’s state and behavior. As you learned earlier in this chapter, event sourcing provides the flexible model that allows for transforming the events into different state representations— you can always add new projections that will leverage the existing events’ data to provide additional insights.


**Audit log**
	The persisted domain events represent a strongly consistent audit log of everything that has happened to the aggregates’ states. Laws oblige some business domains to implement such audit logs, and event sourcing provides this out of the box.
	This model is especially convenient for systems managing money or monetary transactions. It allows us to easily trace the system’s decisions and the flow of funds between accounts.

**Advanced optimistic concurrency management**
	The classic optimistic concurrency model raises an exception when the read data becomes stale—overwritten by another process—while it is being written.
	 When using event sourcing, we can gain deeper insight into exactly what has happened between reading the existing events and writing the new ones. You can query the exact events that were concurrently appended to the event store and make a business domain–driven decision as to whether the new events collide with the attempted operation or the additional events are irrelevant and it’s safe to proceed.


#### Disadvantages

**Learning Curve**  
	The obvious disadvantage of the pattern is its sharp difference from traditional techniques of managing data. Successful implementation of the pattern demands training of the team and time to get used to the new way of thinking. Unless the team already has experience implementing event-sourced systems, the learning curve has to be taken into account.

**Evolving the Model**  
	Evolving an event-sourced model can be challenging. The strict definition of event sourcing says that events are immutable. But what if you need to adjust the event’s schema? The process is not as simple as changing a table’s schema. In fact, a whole book was written on this subject alone: *Versioning in an Event Sourced System* by Greg Young.

**Architectural Complexity**  
	Implementation of event sourcing introduces numerous architectural “moving parts,” making the overall design more complicated. This topic will be covered in more detail in the next chapter, when we discuss the CQRS architecture.


### Frequently Asked Questions

#### Performance

Reconstituting an aggregate’s state from events will negatively affect the system’s performance. It will degrade as events are added. How can this even work?

In most systems, the performance hit will be noticeable only after 10,000+ events per aggregate. That said, in the vast majority of systems, **==an aggregate’s average lifespan won’t go over 100 events.==**

- A process continuously iterates new events in the event store, generates corresponding projections, and stores them in a cache.
    
- An in-memory projection is needed to execute an action on the aggregate. In this case:
    
    - The process fetches the current state projection from the cache.
        
    - The process fetches the events that came after the snapshot version from the event store.
        
    - The additional events are applied in-memory to the snapshot.


![[Pasted image 20250628111524.png]]

It’s worth reiterating that the snapshot pattern is an optimization that has to be justified. If the aggregates in your system won’t persist 10,000+ events, implementing the snapshot pattern is just an accidental complexity. But before you go ahead and implement the snapshot pattern,

This model generates enormous amounts of data. Can it scale?
	The event-sourced model is easy to scale. Since all aggregate-related operations are done in the context of a single aggregate, the event store can be sharded by aggregate

![[Pasted image 20250628111606.png]]

#### Deleting Data

Handling Data Deletion in an Event Store for GDPR Compliance

The event store is an append-only database, which poses challenges when physical data deletion is required, such as for GDPR compliance. This need can be addressed with the forgettable payload pattern: all sensitive information is included in the events in encrypted form. The encryption key is stored in an external key–value store, referred to as the key storage, where the key is the specific aggregate’s ID and the value is the encryption key. When sensitive data must be deleted, the encryption key is removed from the key storage, rendering the sensitive information in the events inaccessible.

### Conclusion

In an event-sourced domain model, all changes to an aggregate’s state are expressed as a series of domain events. That’s in contrast to the more traditional approaches in which a state change just updates a record in the databases. The resultant domain events can be used to project the aggregate’s current state. Moreover, the event-based model gives us the flexibility to project the events into multiple representation models, each optimized for a specific task.

This pattern fits cases in which it’s crucial to have deep insight into the system’s data, whether for analysis and optimization or because an audit log is required by law.

## Architectural Patterns

### Business Logic Versus Architectural Patterns

To implement functional and nonfunctional requirements, the codebase has to fulfill more responsibilities. It has to interact with users to gather input and provide output, and it has to use different storage mechanisms to persist state and integrate with external systems and information providers.

The variety of concerns that a codebase has to take care of makes it easy for its business logic to become diffused among the different components

Architectural patterns introduce organizational principles for the different aspects of a codebase and present clear boundaries between them: how the business logic is wired to the system’s input, output, and other infrastructural components. This affects how these components interact with each other: what knowledge they share and how the components reference each other.

Choosing the appropriate way to organize the codebase, or the correct architectural pattern, is crucial to support implementation of the business logic in the short term and alleviate maintenance in the long term.

### Ports & Adapters

#### Terminology

Essentially, both the presentation layer and data access layer represent integration with external components: databases, external services, and user interface frameworks. These technical implementation details do not reflect the system’s business logic

![[Pasted image 20250628200833.png]]

#### Dependency Inversion Principle

The dependency inversion principle (DIP) states that high-level modules, which implement the business logic, should not depend on low-level modules. However, that’s precisely what happens in the traditional layered architecture.

![[Pasted image 20250628200838.png]]

Instead of being sandwiched between the technological concerns, now the business logic layer takes the central role. It doesn’t depend on any of the system’s infrastructural components.

![[Pasted image 20250628200904.png]]

#### Integration of Infrastructural Components

The core goal of the ports & adapters architecture is to decouple the system’s business logic from its infrastructural components.

Instead of referencing and calling the infrastructural components directly, the business logic layer defines “ports” that have to be implemented by the infrastructure layer. The infrastructure layer implements “adapters”: concrete implementations of the ports’ interfaces for working with different technologies

![[Pasted image 20250628200940.png]]

The abstract ports are resolved into concrete adapters in the infrastructure layer, either through dependency injection or by bootstrapping.

#### Variants

The ports & adapters architecture is also known as hexagonal architecture, onion architecture, and clean architecture. All of these patterns are based on the same design principles, have the same components, and have the same relationships between them, but as in the case of the layered architecture, the terminology may differ:

• Application layer = service layer = use case layer
• Business logic layer = domain layer = core layer

#### When to Use Ports & Adapters

The decoupling of the business logic from all technological concerns makes the ports & adapters architecture a perfect fit for business logic implemented with the domain model pattern.

### Command-Query Responsibility Segregation

The command-query responsibility segregation (CQRS) pattern is based on the same organizational principles for business logic and infrastructural concerns as ports & adapters. **==It differs, however, in the way the system’s data is managed. This pattern enables representation of the system’s data in multiple persistent models.==**

#### Polyglot Modeling

In many cases, it may be difficult, if not impossible, to use a single model of the system’s business domain to address all of the system’s needs.

Another reason for working with multiple models may have to do with the notion of polyglot persistence. There is no perfect database. Or, as Greg Young6 says, all databases are flawed, each in its own way: we often have to balance the needs for scale, consistency, or supported querying models. An alternative to finding a perfect database is the polyglot persistence model: using multiple databases to implement different data-related requirements.

**==Finally, the CQRS pattern is closely related to event sourcing. Originally, CQRS was defined to address the limited querying possibilities of an event-sourced model: it is only possible to query events of one aggregate instance at a time==**

#### Implementation

As the name suggests, the pattern segregates the responsibilities of the system’s models. There are two types of models: the command execution model and the read models.

**Command execution model**

CQRS devotes a single model to executing operations that modify the system’s state (system commands). This model is used to implement the business logic, validate rules, and enforce invariants.

**Read models (projections)**

A read model is a precached projection. It can reside in a durable database, flat file, or in-memory cache. Proper implementation of CQRS allows for wiping out all data of a projection and regenerating it from scratch. This also enables extending the system with additional projections in the future—models that couldn’t have been foreseen originally

#### Projecting Read Models

For the read models to work, the system has to project changes from the command execution model to all its read models

![[Pasted image 20250628201727.png]]

The projection of read models is similar to the notion of a materialized view in relational databases: whenever source tables are updated, the changes have to be reflected in the precached views

#### Challenges

Despite the apparent scaling and performance advantages of the asynchronous projection method, it is more prone to the challenges of distributed computing. If the messages are processed out of order or duplicated, inconsistent data will be projected into the read models. This method also makes it more challenging to add new projections or regenerate existing ones.

#### Model Segregation

In the CQRS architecture, the responsibilities of the system’s models are segregated according to their type. A command can only operate on the strongly consistent command execution model. A query cannot directly modify any of the system’s persisted state—neither the read models nor the command execution model.

A common misconception about CQRS-based systems is that a command can only modify data, and data can be fetched for display only through a read model. **==In other words, the command executing the methods should never return any data. This is wrong. This approach produces accidental complexities and leads to a bad user experience.==**

**==The only limitation here is that the returned data should originate from the strongly consistent model—the command execution model—as we cannot expect the projections, which will eventually be consistent, to be refreshed immediately.==**

### When to Use CQRS

The CQRS pattern can be useful for applications that need to work with the same data in multiple models, potentially stored in different kinds of databases. From an operational perspective, the pattern supports domain-driven design’s core value of working with the most effective models for the task at hand, and continuously improving the model of the business domain. From an infrastructural perspective, CQRS allows for leveraging the strength of the different kinds of databases

### Conclusion

The layered architecture decomposes the codebase based on its technological concerns. Since this pattern couples business logic with data access implementation, it’s a good fit for active record–based systems.

The ports & adapters architecture inverts the relationships: it puts the business logic at the center and decouples it from all infrastructural dependencies. This pattern is a good fit for business logic implemented with the domain model pattern.

The CQRS pattern represents the same data in multiple models. Although this pattern is obligatory for systems based on the event-sourced domain model, it can also be used in any systems that need a way of working with multiple persistent models.

## Communication Patterns


### Model Translation

A bounded context is the boundary of a model—a ubiquitous language there are different patterns for designing communication across different bounded contexts. Suppose the teams implementing two bounded contexts are communicating effectively and willing to collaborate. In this case, the bounded contexts can be integrated in a partnership: the protocols can be coordinated in an ad hoc manner, and any integration issues can be effectively addressed through communication between the teams. Another cooperation-driven integration method is shared kernel: the teams extract and co-evolve a limited portion of a model; for example, extracting the bounded contexts’ integration contracts into a co-owned repository.

In a customer–supplier relationship, the balance of power tips toward either the upstream (supplier) or the downstream (consumer) bounded context. Suppose the downstream bounded context cannot conform to the upstream bounded context’s model. In this case, a more elaborate technical solution is required that can facilitate communication by translating the bounded contexts’ models.

This translation can be handled by one, or sometimes both, sides: the downstream bounded context can adapt the upstream bounded context’s model to its needs using an anticorruption layer (ACL), while the upstream bounded context can act as an open-host service (OHS) and protect its consumers from changes to its implementation model by using an integration-specific published language. Since the translation logic is similar for both the anticorruption layer and the open-host service,

The model’s translation logic can be either stateless or stateful. Stateless translation happens on the fly, as incoming (OHS) or outgoing (ACL) requests are issued, while stateful translation involves a more complicated translation logic that requires a database. Let’s see design patterns for implementing both types of model translation

#### Stateless Model Translation

For stateless model translation, the bounded context that owns the translation (OHS for upstream, ACL for downstream) implements the proxy design pattern to interject the incoming and outgoing requests and map the source model to the bounded context’s target model.

![[Pasted image 20250711201617.png]]

Implementation of the proxy depends on whether the bounded contexts are communicating synchronously or asynchronously

**Synchronous**
The typical way to translate models used in synchronous communication is to embed the transformation logic in the bounded context’s codebase, as shown in Figure 9-2. In an open-host service, translation to the public language takes place when processing incoming requests, and in an anticorruption layer, it occurs when calling the upstream bounded context.

![[Pasted image 20250711201651.png]]

In some cases, it can be more cost-effective and convenient to offload the translation logic to an external component such as an API gateway pattern

For bounded contexts implementing the open-host pattern, the API gateway is responsible for converting the internal model into the integration-optimized published language. Moreover, having an explicit API gateway can alleviate the process of managing and serving multiple versions of the bounded context’s API

![[Pasted image 20250711201728.png]]

Anticorruption layers implemented using an API gateway can be consumed by multiple downstream bounded contexts. In such cases, the anticorruption layer acts as an integration-specific bounded context

![[Pasted image 20250711201739.png]]

Such bounded contexts, which are mainly in charge of transforming models for more convenient consumption by other components, are often referred to as interchange contexts.

**Asynchronous**

To translate models used in asynchronous communication you can implement a message proxy: an intermediary component subscribing to messages coming from the source bounded context. The proxy will apply the required model transformations and forward the resultant messages to the target subscriber

![[Pasted image 20250711201816.png]]

In addition to translating the messages’ model, the intercepting component can also reduce the noise on the target bounded context by filtering out irrelevant messages.

Asynchronous model translation is essential when implementing an open host service. It’s a common mistake to design and expose a published language for the model’s objects and allow domain events to be published as they are, thereby exposing the bounded context’s implementation model. Asynchronous translation can be used to intercept the domain events and convert them into a published language, thus providing better encapsulation of the bounded context’s implementation details

Moreover, translating messages to the published language enables differentiating between private events that are intended for the bounded context’s internal needs and public events that are designed for integration with other bounded contexts

![[Pasted image 20250711201848.png]]

#### Stateful Model Translation

**Aggregating incoming data**

Let’s say a bounded context is interested in aggregating incoming requests and processing them in batches for performance optimization. In this case, aggregation may be required both for synchronous and asynchronous requests

![[Pasted image 20250711201920.png]]

Another common use case for aggregation of source data is combining multiple fine grained messages into a single message containing the unified data

![[Pasted image 20250711201940.png]]

Model transformation that aggregates incoming data cannot be implemented using an API gateway, and thus requires more elaborate, stateful processing. To track the incoming data and process it accordingly, the translation logic requires its own persistent storage

![[Pasted image 20250711202000.png]]

In some use cases, you can avoid implementing a custom solution for a stateful translation by using off-the-shelf products; for example, a stream-process platform

**Unifying multiple sources**

A bounded context may need to process data aggregates from multiple sources, including other bounded contexts. A typical example for this is the backend-for frontend pattern, in which the user interface has to combine data originating from multiple services.

Another example is a bounded context that must process data from multiple other contexts and implement complex business logic to process all the data. In this case, it can be beneficial to decouple the integration and business logic complexities by fronting the bounded context with an anticorruption layer that aggregates data from all other bounded contexts

![[Pasted image 20250711202057.png]]

### Integrating Aggregates

one of the ways aggregates communicate with the rest of the system is by publishing domain events. External components can subscribe to these domain events and execute their logic. But how are domain events published to a message bus?

```java
public class Campaign
{
    ...
    List<DomainEvent> _events;
    IMessageBus _messageBus;
    ...

    public void Deactivate(string reason)
    {
        for (l in _locations.Values())
        {
            l.Deactivate();
        }

        IsActive = false;

        var newEvent = new CampaignDeactivated(_id, reason);
        _events.Append(newEvent);
        _messageBus.Publish(newEvent);
    }
}
```

```java
public class ManagementAPI
{
    ...
    private readonly IMessageBus _messageBus;
    private readonly ICampaignRepository _repository;
    ...

    public ExecutionResult DeactivateCampaign(CampaignId id, string reason)
    {
        try
        {
            var campaign = _repository.Load(id);
            campaign.Deactivate(reason);
            _repository.CommitChanges(campaign);

            var events = campaign.GetUnpublishedEvents();
            for (IDomainEvent e in events)
            {
                _messageBus.Publish(e);
            }
            campaign.ClearUnpublishedEvents();
        }
        catch (Exception ex)
        {
            ...
        }
    }
}
```

#### Outbox

The outbox pattern (Figure 9-11) ensures reliable publishing of domain events using the following algorithm:

- ==**Both the updated aggregate’s state and the new domain events are committed in the same atomic transaction.**==
- ==**A message relay fetches newly committed domain events from the database.**==
- ==**The relay publishes the domain events to the message bus.**==
- ==**Upon successful publishing, the relay either marks the events as published in the database or deletes them completely.==**

![[Pasted image 20250711202629.png]]

When using a relational database, it’s convenient to leverage the database’s ability to commit to two tables atomically and use a dedicated table for storing the messages

![[Pasted image 20250711202646.png]]

When using a NoSQL database that doesn’t support multi document transactions, the outgoing domain events have to be embedded in the aggregate’s record

```json
{
    "campaign-id": "364b33c3-2171-446d-b652-8e5a7b2be1af",
    "state": {
        "name": "Autumn 2017",
        "publishing-state": "DEACTIVATED",
        "ad-locations": [
            ...
        ],
        ...
    },
    "outbox": [
        {
            "campaign-id": "364b33c3-2171-446d-b652-8e5a7b2be1af",
            "type": "campaign-deactivated",
            "reason": "Goals met",
            "published": false
        }
    ]
}
```

**Fetching unpublished events**

 Pull: Polling Publisher
The relay can continuously query the database for unpublished events. Proper indexes must be in place to minimize the load on the database caused by constant polling.

 Push: Transaction Log Tailing
The publishing relay can be proactively notified of new events by leveraging the database’s feature set. For instance, some relational databases support notifications for updated or inserted records by tailing the transaction log. Certain NoSQL databases, such as AWS DynamoDB Streams, expose committed changes as streams of events.

**==It’s important to note that the outbox pattern guarantees delivery of the messages at least once: if the relay fails right after publishing a message but before marking it as published in the database, the same message will be published again in the next iteration.==**

#### Saga

One of the core aggregate design principles is to limit each transaction to a single instance of an aggregate. This ensures that an aggregate’s boundaries are carefully considered and encapsulate a coherent set of business functionality. But there are cases when you have to implement a business process that spans multiple aggregates.

Consider the following example: when an advertising campaign is activated, it should automatically submit the campaign’s advertising materials to its publisher. Upon receiving the confirmation from the publisher, the campaign’s publishing state should change to Published. In the case of rejection by the publisher, the campaign should be marked as Rejected.

A saga is a long-running business process. It’s long running not necessarily in terms of time, as sagas can run from seconds to years, but rather in terms of transactions: a business process that spans multiple transactions. The transactions can be handled not only by aggregates but by any component emitting domain events and responding to commands. The saga listens to the events emitted by the relevant components and issues subsequent commands to the other components. If one of the execution steps fails, the saga is in charge of issuing relevant compensating actions to ensure the system state remains consistent.

![[Pasted image 20250711202917.png]]

```java
public class CampaignPublishingSaga
{
    private readonly ICampaignRepository _repository;
    private readonly IPublishingServiceClient _publishingService;
    ...

    public void Process(CampaignActivated @event)
    {
        var campaign = _repository.Load(@event.CampaignId);
        var advertisingMaterials = campaign.GenerateAdvertisingMaterials();
        _publishingService.SubmitAdvertisement(@event.CampaignId, advertisingMaterials);
    }

    public void Process(PublishingConfirmed @event)
    {
        var campaign = _repository.Load(@event.CampaignId);
        campaign.TrackPublishingConfirmation(@event.ConfirmationId);
        _repository.CommitChanges(campaign);
    }

    public void Process(PublishingRejected @event)
    {
        var campaign = _repository.Load(@event.CampaignId);
        campaign.TrackPublishingRejection(@event.RejectionReason);
        _repository.CommitChanges(campaign);
    }
}
```

```java
public class CampaignPublishingSaga
{
    private readonly ICampaignRepository _repository;
    private readonly IList<IDomainEvent> _events;
    ...

    public void Process(CampaignActivated activated)
    {
        var campaign = _repository.Load(activated.CampaignId);
        var advertisingMaterials = campaign.GenerateAdvertisingMaterials();
        var commandIssuedEvent = new CommandIssuedEvent(
            target: Target.PublishingService,
            command: new SubmitAdvertisementCommand(activated.CampaignId, advertisingMaterials));
        _events.Append(activated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(PublishingConfirmed confirmed)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            target: Target.CampaignAggregate,
            command: new TrackConfirmation(confirmed.CampaignId, confirmed.ConfirmationId));
        _events.Append(confirmed);
        _events.Append(commandIssuedEvent);
    }

    public void Process(PublishingRejected rejected)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            target: Target.CampaignAggregate,
            command: new TrackRejection(rejected.CampaignId, rejected.RejectionReason));
        _events.Append(rejected);
        _events.Append(commandIssuedEvent);
    }
}
```

 **Consistency**

The saga pattern orchestrates multicomponent transactions, but the states of the involved components are **eventually consistent**. While the saga will eventually execute the relevant commands, no two transactions can be considered atomic. This aligns with a key aggregate design principle: **only the data within an aggregate’s boundaries can be considered strongly consistent**. Everything outside these boundaries is eventually consistent. Use this principle to ensure sagas are not misused to compensate for improperly defined aggregate boundaries. Business operations that require strongly consistent data must belong to the same aggregate. The saga pattern is often confused with the **process manager** pattern. Although their implementations are similar, they are distinct patterns with different purposes.

### Process Manager

The saga pattern manages simple, linear flow. Strictly speaking, a saga matches events to the corresponding commands. In the examples we used to demonstrate saga implementations, we actually implemented simple matching of events to commands:

![[Pasted image 20250711203302.png]]

**==As a simple rule of thumb, if a saga contains if-else statements to choose the correct course of action, it is probably a process manager==**

Another difference between a process manager and a saga is that a saga is instantiated implicitly when a particular event is observed, as in ``CampaignActivated`` in the preceding examples. A process manager, on the other hand, cannot be bound to a single source event. Instead, it’s a coherent business process consisting of multiple steps. Hence, a process manager has to be instantiated explicitly.

![[Pasted image 20250711203352.png]]

```java
public class BookingProcessManager
{
    private readonly IList<IDomainEvent> _events;
    private BookingId _id;
    private Destination _destination;
    private TripDefinition _parameters;
    private EmployeeId _traveler;
    private Route _route;
    private IList<Route> _rejectedRoutes;
    private IRoutingService _routing;
    ...

    public void Initialize(Destination destination, TripDefinition parameters, EmployeeId traveler)
    {
        _destination = destination;
        _parameters = parameters;
        _traveler = traveler;
        _route = _routing.Calculate(destination, parameters);
        var routeGenerated = new RouteGeneratedEvent(
            BookingId: _id,
            Route: _route);
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestEmployeeApproval(_traveler, _route)
        );
        _events.Append(routeGenerated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(RouteConfirmed confirmed)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new BookFlights(_route, _parameters)
        );
        _events.Append(confirmed);
        _events.Append(commandIssuedEvent);
    }

    public void Process(RouteRejected rejected)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestRerouting(_traveler, _route)
        );
        _events.Append(rejected);
        _events.Append(commandIssuedEvent);
    }

    public void Process(ReroutingConfirmed confirmed)
    {
        _rejectedRoutes.Append(_route);
        _route = _routing.CalculateAltRoute(_destination, _parameters, _rejectedRoutes);
        var routeGenerated = new RouteGeneratedEvent(
            BookingId: _id,
            Route: _route);
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestEmployeeApproval(_traveler, _route)
        );
        _events.Append(confirmed);
        _events.Append(routeGenerated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(FlightBooked booked)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new BookHotel(_destination, _parameters)
        );
        _events.Append(booked);
        _events.Append(commandIssuedEvent);
    }
    ...
}
```

### Conclusion

The outbox pattern is a reliable way to publish aggregates’ domain events. It ensures that domain events are always going to be published, even in the face of different process failures

The saga pattern can be used to implement simple cross-component business processes. More complex business processes can be implemented using the process manager pattern. Both patterns rely on asynchronous reactions to domain events and the issuing of commands.

# PART III Applying Domain-Driven Design in Practice

## Design Heuristics

“It depends” is the correct answer to almost any question in software engineering, but not really practical

### Heuristic

A heuristic is not a hard rule that is guaranteed and mathematically proven to be correct in 100% of cases. Rather, it’s a rule of thumb: not guaranteed to be perfect, yet sufficient for one’s immediate goals. **==In other words, using heuristics is an effective problem-solving approach that ignores the noise inherent in many cues, focusing instead on the “swamping forces” reflected in the most important cues==**

### Bounded Contexts

The optimal size of a bounded context is a nuanced topic, particularly given the common association of bounded contexts with microservices. Rather than striving for the smallest possible bounded contexts, as Nick Tune suggests, size is one of the least useful heuristics for defining service boundaries. Instead of optimizing for small bounded contexts, it’s more effective to treat the size of a bounded context as a function of the model it encompasses. Software changes that span multiple bounded contexts are costly and require significant coordination, especially when different teams manage the affected contexts. Such changes indicate poorly designed boundaries, as effective bounded contexts should encapsulate related changes. Refactoring these boundaries is often expensive, and neglected ineffective boundaries can lead to accumulating technical debt over time.

![[Pasted image 20250711224032.png]]

boundaries typically occur when the business domain is not well known or the business requirements change frequently.

Broad bounded context boundaries, or those that encompass multiple subdomains, make it safer to be wrong about the boundaries or the models of the included subdomains. **==Refactoring logical boundaries is considerably less expensive than refactoring physical boundaries. Hence, when designing bounded contexts, start with wider boundaries. If required, decompose the wide boundaries into smaller ones as you gain domain knowledge.==**

When creating a bounded context that contains a core subdomain, you can protect yourself against unforeseen changes by including other subdomains that the core subdomain interacts with most often. This can be other core subdomains, or even supporting and generic subdomains

![[Pasted image 20250711224123.png]]

### Business Logic Implementation Patterns

The transaction script and active record patterns are better suited for subdomains with simple business logic, such as supporting subdomains or integrating third-party solutions for generic subdomains. The key difference between these patterns lies in the complexity of the data structures. The transaction script pattern is ideal for simple data structures, while the active record pattern helps encapsulate the mapping of complex data structures to the underlying database.

The domain model, including its event-sourced variant, is more appropriate for subdomains with complex business logic, particularly core subdomains. Core subdomains that involve monetary transactions, require a legally mandated audit log, or need deep analytics of system behavior are best addressed by the event-sourced domain model.

An effective heuristic for selecting the appropriate business logic implementation pattern involves asking the following questions:

- Does the subdomain track money or other monetary transactions, require a consistent audit log, or need deep analysis of its behavior? If so, use the **event-sourced domain model**.
- Is the subdomain’s business logic complex? If so, implement a **domain model**.
- Does the subdomain include complex data structures? If so, use the **active record pattern**.
- Otherwise, implement a **transaction script**.

![[Pasted image 20250711224226.png]]

In general, complex business logic includes complicated business rules, invariants, and algorithms. A simple approach mainly revolves around validating the inputs. Another heuristic for evaluating complexity concerns the complexity of the ubiquitous language itself

### Architectural Patterns

Knowing the intended business logic implementation pattern simplifies the choice of architectural pattern:

- The **event-sourced domain model** requires **CQRS**. Without it, the system is severely limited in its data querying capabilities, restricted to fetching instances by ID only.
- The **domain model** pairs best with the **ports & adapters architecture**. A layered architecture makes it challenging to keep aggregates and value objects ignorant of persistence.
- The **active record pattern** works well with a **layered architecture** that includes an additional application (service) layer to manage the logic controlling active records.
- The **transaction script pattern** can be implemented with a minimal **layered architecture**, consisting of only three layers.

An exception to these heuristics is the **CQRS pattern**, which is beneficial not only for the event-sourced domain model but also for any pattern if the subdomain requires representing its data in multiple persistent models.

![[Pasted image 20250711224410.png]]

### Testing Strategy

![[Pasted image 20250711224429.png]]

#### Testing Pyramid
The classic testing pyramid prioritizes a large number of unit tests, fewer integration tests, and even fewer end-to-end tests. This approach is well-suited for both variants of the domain model patterns. Aggregates and value objects serve as ideal units for effectively testing the business logic.

#### Testing Diamond
The testing diamond emphasizes integration tests over other types. When using the active record pattern, the system’s business logic is distributed across both the service and business logic layers. As a result, focusing on integration tests to verify the interaction between these layers makes the testing diamond the more effective choice.

#### Reversed Testing Pyramid
The reversed testing pyramid places the greatest emphasis on end-to-end tests, which verify the application’s workflow from start to finish. This approach is best suited for codebases implementing the transaction script pattern, where the business logic is simple and the number of layers is minimal, making it more effective to test the end-to-end flow of the system.

![[Pasted image 20250711224508.png]]

### Tactical Design Decision Tree

![[Pasted image 20250711224528.png]]

Identifying subdomain types and following the decision tree provides a solid foundation for making key design decisions. However, these are heuristics, not strict rules. By their nature, heuristics are not guaranteed to be correct in every scenario, and exceptions exist for every rule. The decision tree reflects a preference for using simpler tools, resorting to advanced patterns—such as the domain model, event-sourced domain model, or CQRS—only when they are absolutely necessary.

### Conclusion

Making design decisions is important, but even more so is to verify the decisions’ validity over time. In the next chapter, we will shift our discussion to the next phase of the software design lifecycle: the evolution of design decisions

## CHAPTER 11 Evolving Design Decisions

### Changes in Domains

To design software that is driven by the business domain’s needs, it’s crucial to identify the business subdomains and their types. However, that’s not the whole story. It’s equally important to be alert to the evolution of the subdomains. As an organization grows and evolves, it’s not unusual for some of its subdomains to morph from one type to another.

#### Core to Supporting

A core subdomain can, over time, become a supporting subdomain. This can happen when the subdomain’s complexity isn’t justified. In other words, it’s not profitable. In such cases, the organization may decide to cut the extraneous complexity, leaving the minimum logic needed to support implementation of other subdomains.

#### Generic to Supporting

Finally, for the same reason as a core subdomain, a generic subdomain can turn into a supporting one. Going back to the example of ``BuyIT``’s document management system, assume the company has decided that the complexity of integrating the open source solution doesn’t justify the benefits and has resorted back to the in-house system. As a result, the generic subdomain has turned into a supporting subdomain.

![[Pasted image 20250713163213.png]]

### Strategic Design Concerns

A change in a subdomain’s type directly affects its bounded context and, consequently, corresponding strategic design decisions. different bounded context integration patterns accommodate the different subdomain types. The core subdomains have to protect their models by using anticorruption layers and have to protect consumers from frequent changes in the implementation models by using published languages (OHS).

Another integration pattern that is affected by such changes is the separate ways pattern. As you saw earlier, teams can use this pattern for supporting and generic subdomains. If the subdomain morphs into a core subdomain, duplicating its functionality by multiple teams is no longer acceptable. Hence, the teams have no choice but to integrate their implementations. The customer–supplier relationship will make the most sense in this case, since the core subdomain will only be implemented by one team.

From an implementation strategy standpoint, core and supporting subdomains differ in how they can be implemented. Supporting subdomains can be outsourced or used as “training wheels” for new hires. Core subdomains must be implemented in-house, as close as possible to the sources of domain knowledge. Therefore, when a supporting subdomain turns into a core subdomain, its implementation should be moved inhouse. The same logic works the other way around. If a core subdomain turns into a supporting subdomain, it’s possible to outsource the implementation to let the inhouse R&D teams concentrate on the core subdomains.

### Tactical Design Concerns

The main indicator of a change in a subdomain’s type is the inability of the existing technical design to support current business needs

If complicated rules and invariants are added to the business logic over time, the codebase will become increasingly complex as well. It will be painful to add new functionality, as the design won’t support the new level of complexity. This “pain” is an important signal. Use it as a call to reassess the business domain and design choices. The need for change in the implementation strategy is nothing to fear. It’s normal. We cannot foresee how a business will evolve down the road. We also cannot apply the most elaborate design patterns for all types of subdomains; that would be wasteful and ineffective. We have to choose the most appropriate design and evolve it when needed. If the decision for how to model the business logic is made consciously, and you are aware of all the possible design choices and the differences between them, migrating from one design pattern to another is not that troublesome. The following subsections highlight a few examples.

### Organizational Changes

Another type of change that can affect a system’s design is a change in the organization itself. Chapter 4 looked at different patterns of integrating bounded contexts: partnership, shared kernel, conformist, anticorruption layer, open-host service, and separate ways. Changes in the organization’s structure can affect teams’ communication and collaboration levels and, as a result, the ways the bounded contexts should be integrated.

![[Pasted image 20250713163439.png]]

Moreover, the organization’s development centers are often located in different geographical locations. When the work on the existing bounded contexts is shifted to another location, it may negatively impact the teams’ collaboration. As a result, the bounded contexts’ integration patterns have to evolve accordingly, as described in the following scenarios.

#### Partnership to Customer–Supplier

The partnership pattern assumes there is strong communication and collaboration among teams. As time goes by, that might cease to be the case; for example, when work on one of the bounded contexts is moved to a distant development center.

#### Customer–Supplier to Separate Ways

Unfortunately, it’s not uncommon for teams to have severe communication problems. The issues might be caused by geographical distance or organizational politics. Such teams may experience more and more integration issues over time. At some point, it may become more cost-effective to duplicate the functionality instead of continuously chasing one another’s tails

### Domain Knowledge

The core tenet of domain-driven design is that domain knowledge is essential for designing a successful software system. Acquiring domain knowledge is one of the most challenging aspects of software engineering, especially for the core subdomains. A core subdomain’s logic is not only complicated, but also expected to change often. Moreover, modeling is an ongoing process. Models have to improve as more knowledge of the business domain is acquired. Many times, the business domain’s complexity is implicit. Initially, everything seems simple and straightforward. The initial simplicity is often deceptive and it quickly morphs into complexity. As more functionality is added, more and more edge cases, invariants, and rules are discovered. Such insights are often disruptive, requiring rebuilding the model from the ground up, including the boundaries of the bounded contexts, aggregates, and other implementation details. From a strategic design standpoint, it’s a useful heuristic to design the bounded contexts’ boundaries according to the level of domain knowledge. The cost of decomposing a system into bounded contexts that, over time, turn out to be incorrect can be high. Therefore, when the domain logic is unclear and changes often, it makes sense to design the bounded contexts with broader boundaries. Then, as domain knowledge is discovered over time and changes to the business logic stabilize, those broad bounded contexts can be decomposed into contexts with narrower boundaries, or microservices. When new domain knowledge is discovered, it should be leveraged to evolve the design and make it more resilient. Unfortunately, changes in domain knowledge are not always positive: domain knowledge can be lost. As time goes by, documentation often becomes stale, people who were working on the original design leave the company, and new functionality is added in an ad hoc manner until, at one point, the codebase gains the dubious status of a legacy system. It’s vital to prevent such degradation of domain knowledge proactively. An effective tool for recovering domain knowledge is the ``EventStorming`` workshop, which is the topic of the next chapter.

### Growth

Growth is a sign of a healthy system. When new functionality is continuously added, it’s a sign that the system is successful: it brings value to its users and is expanded to further address users’ needs and keep up with competing products. But growth has a dark side. As a software project grows, its codebase can grow into a big ball of mud: a haphazardly structured, sprawling, sloppy, duct-tape-and-baling-wire, spaghetti-code jungle. These systems show unmistakable signs of unregulated growth, and repeated, expedient repair. The guiding principle for dealing with growth-driven complexity is to identify and eliminate accidental complexity: the complexity caused by outdated design decisions. The essential complexity, or inherent complexity of the business domain, should be managed using domain-driven design tools and practices.

#### Subdomains
 
 the subdomains’ boundaries can be challenging to identify, and as a result, instead of striving for boundaries that are perfect, we must strive for boundaries that are useful. That is, the subdomains should allow us to identify components of different business value and use the appropriate tools to design and implement the solution.
 
As the business domain grows, the subdomains’ boundaries can become even more blurred, making it harder to identify cases of a subdomain spanning multiple, finer grained subdomains. Hence, it’s important to revisit the identified subdomains and follow the heuristic of coherent use cases (sets of use cases working on the same set of data) to try to identify where to split a subdomain

![[Pasted image 20250713163750.png]]

If you are able to identify finer-grained subdomains of different types, this is an important insight that will allow you to manage the business domain’s essential complexity. The more precise the information about the subdomains and their types is, the more effective you will be at choosing technical solutions for each subdomain.

#### Bounded Contexts

The bounded context pattern allows us to use different models of the business domain. Instead of building a “jack of all trades, master of none” model, we can build multiple models, each focused on solving a specific problem. As a project evolves and grows, it’s not uncommon for the bounded contexts to lose their focus and accumulate logic related to different problems. That’s accidental complexity. As with subdomains, it’s crucial to revisit the bounded contexts’ boundaries from time to time. Always look for opportunities to simplify the models by extracting bounded contexts that are laser-focused at solving specific problems. Growth can also make existing implicit design issues explicit.

#### Aggregates

Objects that are required to be in a strongly consistent state by the business domain. As the system’s business requirements grow, it can be “convenient” to distribute new functionalities among the existing aggregates, without revisiting the principle of keeping aggregates small. If an aggregate grows to include data that is not needed to be strongly consistent by all of its business logic, again, that’s accidental complexity that has to be eliminated. Extracting business functionality into a dedicated aggregate not only simplifies the original aggregate, but potentially can simplify the bounded context it belongs to. Often, such refactoring uncovers an additional hidden model that, once made explicit, should be extracted into a different bounded context.

### Conclusion

- When a subdomain’s functionality is expanded, try to identify more finer-grained subdomain boundaries that will enable you to make better design decisions.
- Don’t allow a bounded context to become a “jack of all trades.” Make sure the models encompassed by bounded contexts are focused to solve specific problems.
- Make sure your aggregates’ boundaries are as small as possible. Use the heuristic of strongly consistent data to detect possibilities to extract business logic into new aggregates.

## EventStorming

### What Is EventStorming?

In a sense, EventStorming is a tactical tool for sharing business domain knowledge. An EventStorming session has a scope: the business process that the group is interested in exploring. The participants are exploring the process as a series of domain events, represented by sticky notes, over a timeline. Step by step, the model is enhanced with additional concepts—actors, commands, external systems, and others—until all of its elements tell the story of how the business process works.

### The EventStorming Process

Below is a brief explanation of each step in the EventStorming process, formatted in Markdown:

#### Step 1: Unstructured Exploration
Participants brainstorm and place domain events (significant occurrences in the process) on a large modeling surface, typically using sticky notes, without worrying about order or structure. This encourages free-flowing ideas and captures key events.

#### Step 2: Timelines
The events are organized into a chronological timeline, creating a clear sequence of how things happen in the domain. This helps establish a shared understanding of the process flow.

#### Step 3: Pain Points
Participants identify and mark pain points or inefficiencies in the process, often using a different color (e.g., red sticky notes). This highlights areas that need improvement or cause frustration.

#### Step 4: Pivotal Events
Key events that significantly impact the process or mark critical milestones are identified and highlighted. These pivotal events help focus on what drives the domain forward.

#### Step 5: Commands
Commands (actions or decisions that trigger events) are added to the model. They represent user or system intentions, such as "Place Order," and are linked to the events they cause.

#### Step 6: Policies
Policies or rules that dictate how the system responds to events are defined. These are often automated reactions or business logic, such as "If payment is received, ship the order."

#### Step 7: Read Models
Read models or views are introduced to represent how data is displayed or queried in the system. These help clarify what information users need to make decisions.

#### Step 8: External Systems
External systems or services that interact with the process are identified and added to the model. This clarifies dependencies and integrations, such as a payment gateway or third-party API.

#### Step 9: Aggregates
Aggregates are defined as clusters of domain objects that are treated as a single unit (e.g., an "Order" with its line items). These help structure the model and ensure consistency in the domain.

#### Step 10: Bounded Contexts
The model is divided into bounded contexts, which are distinct areas of the domain with their own models and language. This helps manage complexity by separating different parts of the system.

## Domain-Driven Design in the Real World


