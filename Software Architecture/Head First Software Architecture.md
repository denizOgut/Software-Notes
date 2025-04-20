# Chapter-1 software architecture demystified

## Building your understanding of software architecture

The structure of the home is its architecture—things like its shape, how many rooms and floors it has, its dimensions, and so on. A house is usually represented through a building plan, which contains all the lines and boxes necessary to know how to build the house. Structural things like those shown below are hard and expensive to change later and are the important stuff about the house.

## Building plans and software architecture

So what does the “building plan” of a software system look like? Lines and boxes, of course.

in the same way a software architecture diagram specifies its structure (user interfaces, services, databases, and communication protocols). Both artifacts provide guidelines and constraints, as well as a vision of the final result.

## The dimensions of software architecture

Most things around us are multidimensional. software architecture has **four dimensions**.

1. **Architectural characteristics**
	-  This dimension **==describes what aspects of the system the architecture needs to support==**—things like scalability, testability, availability, and so on.
2. **Architectural decisions**
	- **==This dimension includes important decisions that have long-term or significant implications for the system==**—for example, the kind of database it uses, the number of services it has, and how those services communicate with each other
3. **Logical components** 
	- **==This dimension describes the building blocks of the system’s functionality and how they interact with each other.==** For example, an ecommerce system might have components for inventory management, payment processing, and so on.
4. **Architectural style**
	- This dimension defines the overall physical shape and structure of a software system in the same way a building plan defines the overall shape and structure of your home.

![[Pasted image 20250409194844.png]]

## Puzzling out the dimensions

While each piece has its own unique shape and properties, they must all fit together and interact to build a complete picture.

### Everything is interconnected.

That’s exactly how software architecture works: each dimension must align. 

The architectural style must align with the architectural characteristics you choose as well as the architectural decisions you make. Similarly, the logical components you define must align with the characteristics and the architectural style as well as the decisions you make.

## The first dimension: Architectural characteristics

Architectural characteristics form the foundation of the architecture in a software system
**Which characteristic is more important to you**. Without knowing that, you can’t make the right choice

what kind of database to use for your new system. Should it be a relational database, a simple key/value database, or a complex graph database? The answer will be based on what architectural characteristics are critical to you. For example, you might choose a graph database if you need high-speed search capability (we’ll call that performance), whereas a traditional relational database might be better if you need to preserve data relationships (we’ll call that data integrity).

The term architectural characteristics, things like performance, scalability, reliability, and availability are also **==known as nonfunctional requirements, system quality attributes, and simply “the ``-ilities``” because most end with the suffix ``-ility``.==**

> Architectural characteristics are capabilities that are critical or important to the success of the system

## The second dimension: Architectural decisions

**Architectural decisions** are choices you make about structural aspects of the system that have long-term or significant implications.

![[Pasted image 20250409200445.png]]

It’s not uncommon to have several dozen or more documented architectural decisions within any system. Generally, the larger and more complicated the system, the more architectural decisions it will have.

## The third dimension: Logical components

Logical components are the building blocks of a system, much in the same way rooms are the building blocks of your home. A logical component performs some sort of function, such as processing the payment for an order, managing item inventory, or tracking orders. Logical components in a system are usually represented through a directory or namespace. For example, the directory app/order/ payment with the corresponding namespace ``app.order.payment`` identifies a logical component named Payment Processing. The source code that allows users to pay for an order is stored in this directory and uses this namespace.

**==A logical component should always have a well defined role and responsibility in the system—in other words, a clear definition of what it does.==**

## The fourth dimension: Architectural Styles

**==Architectural styles define the overall shape and structure of a software system, each with its own unique set of characteristics==**. For example, the microservices architectural style scales very well and provides a high level of agility—the ability to respond quickly to change—whereas the layered architectural style is less complex and less costly. The event-driven architectural style provides high levels of scalability and is very fast and responsive.

![[Pasted image 20250409200945.png]]

**==Because the architectural style defines the overall shape and characteristics of the system, it’s important to get it right the first time.==**

Software architecture is no different. It’s not easy changing from a monolithic layered architecture to microservices. Like the house example, this would be quite an undertaking.

## A design perspective

From a design perspective, you might build a Unified Modeling Language (UML) class diagram like the one below to show how the classes interact with each other to implement the payment functionality. While you could write source code to implement these class files, this design says nothing about the physical structure of the source code—in other words, how these class files would be organized and deployed.

![[Pasted image 20250409201455.png]]

## An architectural perspective

Unlike design, architecture is about the structure of the system—things like services, databases, and how services communicate with each other and the user interface.

![[Pasted image 20250409201530.png]]

## The spectrum bet ween architecture and design

In reality, most decisions you encounter will fall between these two examples, within a spectrum of architecture and design.  knowing where along the spectrum between architecture and design your decision lies helps determine who should be responsible for ultimately making that decision. There are some decisions that the development team should make (such as designing the classes to implement a certain feature), some decisions that an architect should make (such as choosing the most appropriate architectural style for a system), and others that should be made together (such as breaking apart services or putting them back together).

## Bullet Points

- **Software architecture** is less about appearance and more about **structure**, whereas **design** is more about **appearance** and less about **structure**.

- To understand and describe software architecture, you need to consider four dimensions:
  1. **Architectural characteristics**
  2. **Architectural decisions**
  3. **Logical components**
  4. **Architectural style**

- **Architectural characteristics** form the **foundation** of software architecture.
  - You must identify the **most important characteristics** for your system.
  - This helps in analyzing **trade-offs** and making the **right decisions**.

- **Architectural decisions** act as **guideposts**.
  - They help development teams understand the **constraints** and **conditions** of the architecture.

- **Logical components** are the **building blocks** of the system.
  - They represent **what the system does**.
  - They are implemented through **class files** or **source code**.

- Just like houses, software can have many **architectural styles**.
  - Each style supports a **specific set of architectural characteristics**.
  - It's important to choose the **right style or combination of styles** for your system.

- It's important to **distinguish between architecture and design decisions**.
  - This helps determine **who should make the decision** and **how important it is**.


# Chapter - 2 architectural  characteristics Know Your Capabilities

What does your architecture need to support? Architectural characteristics (the capabilities of an architecture) are the fundamental building blocks of any system. Without them, you cannot make architectural decisions, select an architectural style, or in many cases even create a logical architecture.

## What are architectural characteristics?

The thing you’re writing software about is called the domain, and designing for it will occupy much of your effort—that is, after all, why you’re writing software. However, it’s not the only thing an architect must consider—they must also analyze architectural characteristics.

## Defining architectural characteristics

Part of your job as an architect is structural design for software systems, for which there are two parts: logical components and architectural characteristics. Logical components represent the domain of the application—the motivation for writing the software system If you combine architectural characteristics with logical components, you have the structural considerations for an architecture.

Architectural characteristics are the important parts of the construction process of a software system or application, irrespective of the problem domain. They represent its operational capabilities, internal structure decisions, and other necessary characteristics.

define architectural characteristics in three parts,

![[Pasted image 20250413105727.png]]

## Characteristics are nondomain de sign considerations

**==To define architectural characteristics, we first need to look at what they are not. The requirements specify what the application should do; architectural characteristics specify operational and design criteria for success, how to implement the requirements, and why certain choices were made.==**

Structural design in architecture can be divided into domain and non-domain considerations. Architectural characteristics represent your design effort to create the capabilities necessary for the project to succeed.

## Characteristics influence architectural structure

The primary reason architects try to describe architectural characteristics has to do with architectural considerations: does this characteristic require special structural support to succeed?

An architect could design this as a monolithic architecture—one with a single deployable unit and matching database—or as a series of independent services.

For the monolithic architecture, the entire application would have to be redeployed when the promotion rules change, because monoliths are built and deployed as a single unit. However, in a distributed architecture, only the Promotions service would be affected, and it could be redeployed in dependently.

![[Pasted image 20250413110106.png]]

## Limit characteristics to prevent overengineering

**==Applications could support a huge number of architectural characteristics…but they shouldn’t. Every architectural characteristic the system must support adds complexity==**

**Impossible to standardize**

Different organizations use different terms for the same architectural characteristics. For example, performance and responsiveness might indicate the same behavior.

**Synergistic**

Architectural characteristics affect other architectural characteristics and domain concerns. For example, if you want to make an application more secure, the required changes will almost certainly affect performance negatively (more on-the-fly encryption and other similar changes will lead to performance overhead).

**Overabundant**

Possible architectural characteristics are extraordinarily abundant, and new ones appear all the time.


A common hazard for architects is overengineering: supporting too many architectural characteristics and complicating the overall design to little or no benefit. Knowing which architectural characteristics are critical or important to application success acts as a filtering tool. It help us eliminate features that would be nice to have but just end up adding needless complexity to the system.

## Consider explicit and implicit capabilities

Some things are explicit—stated clearly—whereas others are implicit— assumed based on context or other knowledge.

Explicit architectural characteristics are specified in the requirements for the application.

Implicit architectural characteristics are factors that influence an architect’s decisions but aren’t explicitly called out in the requirements. Security is often an implicit architectural characteristic: even if it isn’t mentioned in the requirements, architects know that we shouldn’t design an insecure system.

## The International Zoo of “-ilities”

architectural characteristics range from low-level code characteristics, such as modularity, to sophisticated operational concerns, such as scalability and elasticity. Unfortunately, there is no “universal list” of architectural characteristics, nor are there any real standards for what many of these terms mean

## Process architectural characteristics

**modularity**
The degree to which the software is composed of discrete components. Modularity affects how architects partition behavior and organize logical building blocks.

**testability**
How complete the system’s testing is and how easy these tests are to run, including unit, functional, user acceptance, and exploratory tests.

**agility**
A composite architectural characteristic that encompasses testability, deployability, modularity, and a host of other architectural characteristics that facilitate and enable agile software development practices.

**extensibility**
How easy it is for developers to extend the system. This may encompass architectural structure, engineering practices, internal design, and governance.

**deployability**
How easy and efficient it is to deploy the software system.

**decouple-ability**
Coupling describes how parts of the system are joined together. Some architectures define how to decouple parts in specific ways to achieve certain benefits; this architectural characteristic measures the extent to which this is possible in a software system.

## Structural architectural characteristics

**security**
How secure the system is, holistically. Does the data need to be encrypted in the database? How about for network communication between internal systems? What type of authentication needs to be in place for remote user access?

**maintainability**
How easy it is for architects and developers to apply changes to enhance the system and/or fix bugs.

**extensibility**
How easy it is for developers to extend the system. This may encompass architectural structure, engineering practices, internal design, and governance.

**portability**
How easy it is to run the system on more than one platform (for example, Windows and macOS).

**localization**
How well the system supports multiple languages, units of measurement, currencies, and other factors that allow it to be used globally.

## Sourcing architectural characteristics from the problem domain

Architects derive many of the necessary architectural characteristics from the problem domain—it is, after all, the motivation for writing the software in the first place. That means you must translate the items stated in requirements documents into their corresponding architectural characteristics.

## Sourcing architectural characteristics from environmental awareness

It is important to understand organizational priorities so we can make more durable decisions. Architects can’t make decisions in a vacuum— context is always important.

## Sourcing architectural characteristics from holistic domain know ledge

domain knowledge: information that isn’t explicitly spelled out in the requirements but that you implicitly understand about important aspects of the domain.

Architects must make use of all available information sources to understand the full range of trade-offs inherent in our architectural decisions.

## Composite architectural characteristics

A composite is a combination of two or more things, and often architectural characteristics combine with each other to create (seemingly) new ones. We call these composite architectural characteristics.

## More requirements are NOT better.

Remember, architectural characteristics are synergistic with each other and with the problem domain. That means **==the more architectural characteristics the system must support, the more complex its design must be.==**

## Architectural characteristics and logical components

architectural characteristics and logical components are two sides of the same coin.

**Architectural characteristics ≈ capabilities**

Architectural characteristics describe the kinds of capabilities your solution will support, rather than the behavior of the application, which is based on requirements.

**Logical components = behavior**

represent the design of the system you are attempting to implement in software in order to solve the fundamental problem at hand.

## Balancing domain considerations and architectural characteristics

**No architectural characteristics**

Sometimes we don’t take the time to analyze architectural characteristics before designing the system, leading to expensive and time-consuming rework as we discover that our system fails to exhibit the necessary architectural characteristics.

**Good balance between…**

In this scenario, we have achieved a balance in our design decisions between architectural characteristics and domain considerations

**Too many architectural characteristics**

Unfortunately, architects sometimes retreat to an ivory tower and spend too much time analyzing architectural characteristics, or identifying too many of them to be useful. This leads to overengineering, wasting time and effort that could be spent on implementation and ongoing maintenance.

## Limiting architectural characteristics

**The magical number 7**

One useful guideline for the conversation between architects and business analysts is to limit the number of architectural characteristics they can choose to seven

## Bullet Points

- Architectural characteristics represent one part of the structural analysis that architects use to design software systems.  
  *(The other part, logical components, is discussed in Chapter 4.)*

- Architectural characteristics describe a system’s capabilities.

- Some architectural characteristics overlap with operational concerns, such as:
  - Availability
  - Scalability
  - And more

- There are many categories of architectural characteristics.  
  *No comprehensive list exists because the software development ecosystem is constantly evolving.*

- When identifying architectural characteristics, architects look for factors that influence structural design.

- Architects should avoid specifying too many architectural characteristics because they are synergistic—changing one often impacts others.

- Some architectural characteristics are **implicit**:  
  *Not explicitly stated in requirements, yet considered during design.*

- Architectural characteristics may appear in **multiple categories**.

- Many architectural characteristics are **cross-cutting**:  
  *They interact with other parts of the system or organizational decisions.*

- Architects must derive many architectural characteristics from:
  - Requirements
  - Domain design considerations

- Some characteristics come from domain and/or environmental knowledge, not just from application-specific requirements.

- Some architectural characteristics are **composites**:  
  *Made up of a combination of other characteristics.*

- Architects must learn to translate **“business speak”** into architectural characteristics.

- Architects should **limit** the number of architectural characteristics they focus on to a small number (e.g., seven).

# Chapter - 3 the two laws of software architecture Everything’s a Trade-Off

What happens when there are no “best practices”? The nice thing about best practices is that they’re relatively risk-free ways to achieve certain goals. They’re called “best” (not “better” or “good”) for a reason—you know they work, so why not just use them? But one thing you’ll quickly learn about software architecture is that it has no best practices. You’ll have to analyze every situation carefully to make a decision, and you’ll need to communicate not just the “what” of the decision, but the “why.”

## Communicating with downstream services

Most messaging platforms offer two models for a publisher of a message (in this case, that’s the trading service) to communicate with one or more consumers (the downstream services).

The first option is a queue, or a point-to-point communication protocol. Here, the publisher knows who is receiving the message. To reach multiple consumers, the publisher needs to send a message to one queue for each consumer. If the trading service wants to use queues to tell the analytics service and the reporting service about trades

![[Pasted image 20250414224448.png]]

When using the second option, topics, you are signing on for a broadcasting model. The publisher simply produces and sends a message. If another service downstream wants to hear from the publisher, it can subscribe to the topic to receive messages. The publisher doesn’t know (or care) how many services are listening.

![[Pasted image 20250414224544.png]]

## Analyzing trade-offs

Software architecture is no different. Every choice you make involves significant compromises or, as we like to call them, trade-offs. So what exactly does this mean for you?

If you know which architectural characteristics are most important to your project, you can start thinking of solutions that will maximize some of those attributes. But if a solution lets you maximize one characteristic (or more), it will come at the cost of other characteristics.

No matter what solution you come up with, it will come with tradeoffs—upsides and downsides.

Your job is twofold: know the trade-offs associated with every solution you come up with, and then pick the solution that best serves the most important architectural characteristics.

**==You can’t have it all. You’ll have to decide which architectural characteristics are most important, and choose the solution that best allows for those characteristics.==**

## Trade-off analysis: Queue edition

Trade-off analysis isn’t just about finding the benefits of a particular approach. **==It’s also about seeking out the negatives to get the full picture.==**

![[Pasted image 20250414224946.png]]

## Trade-off analysis: Topic edition

![[Pasted image 20250414225102.png]]

## The first law of software architecture

**==it depends!==** The key takeaway is that in software architecture, you’ll always be balancing trade-offs. That leads us to the First Law of Software Architecture.

**==EVERYTHING IN SOFTWARE ARCHITECTURE IS A TRADE-OFF==**

## It always come s back to trade-offs

Some people always pick a particular technique, approach, or tool regardless of the problem at hand. Often they choose something they’ve had a lot of success with in the past. Sometimes they have what we affectionately call “shiny object syndrome,” where they think that some new technology or method will solve all their problems.

Regardless of past achievements or future promises, just remember—for every upside, there’s a downside. The only questions you need to answer are “**==Will the upsides help you implement a successful application?” and “Can you live with the downsides?”==**

## Making an architectural decision

Debating the pros and cons with your team in front of a whiteboard is fun  and all, but at some point, you must make an architectural decision.

In most cases, any choice you make that affects the structure of your system is an architectural decision. Here are a couple of example decisions:

- We will use a cache to reduce the load on the database and improve performance.
- We will build the reporting service as a modular monolith.

## What else makes a decision architectural?

Usually, architectural decisions affect the structure of an architecture—are we going with a monolith, or will we leverage microservices? But every so often, you might decide to maintain a particular architectural characteristic.

- We will use queues for asynchronous communication between services.
- We will use Node.js as the development framework for the MVP.

while the decision itself is important, why we made that decision might be even more important. Which leads us to...

## The second law of software architecture

Making decisions is one of the most important things software architects do.
The result of your analysis is that your system starts using a cache somewhere. The what is easy to spot.

That decision is important, but so are the circumstances in which you made the decision, its impact on the team implementing it, and why, of all the options available to you, you chose what you did.

This leads us to the Second Law of Software Architecture.

**==WHY IS MORE IMPORTANT THAN HOW==**

future architects (or even “future you”) might be able to discern what you did and even how you did it—but it’ll be very hard for them to tell why you did it that way. Without knowing that, they might waste time exploring solutions you’ve already rejected for good reasons, or miss a key factor that swayed your decision. This is why we have the Second Law. You need to understand and record the “why” of each decision so it doesn’t get lost in the sands of time. So how do we go about capturing architectural decisions?

## Architectural decision records (ADRs)

it’s important to document stuff—especially the important stuff.

Architects use architectural decision records (ADRs) to record such decisions because it gives us a specific template to work with

An ADR is a document that describes a specific architectural decision. You write one for every architectural decision you make. Over time, they’ll build up into an architectural decision log. Remember that architectural decisions form the second dimension to describe your architecture. ADRs are the documentation that supports this dimension.

![[Pasted image 20250414230340.png]]

An ADR has seven sections: Title, Status, Context, Decision, Consequences, Governance, and finally Notes. Every aspect of an architectural decision, including the decision itself, is captured in one of these sections.

## Writing ADRs: Getting the title r ight

Every ADR starts with a title that describes the decision. Craft this title carefully. It should be meaningful, yet concise. **==A good title makes it easy to figure out what the ADR is about, which is especially handy when you’re frantically searching for an answer!==**

The title should consist mostly of nouns. It should describe what the ADR is about, much like the headline of a news article or blog post. Get that right, and the rest will follow

The title should start with a number—we suggest using three digits, with leading zeros where needed. This allows you to number your ADRs sequentially, starting with 001 for your first ADR, all the way to 999.

## Writing ADRs: What’s your status?

**==making decisions is a process. ADRs do record architectural decisions, but they also act as documentation, making it easier to share and collaborate.==** Others might need to look at or even sign off on an ADR. Let’s start by considering the different statuses an ADR can have.

**Request for Comment (RFC)**

- Use this status for ADRs that need additional input—perhaps from other teams or some sort of advisory board. Usually, these ADRs affect multiple teams or address a cross-cutting concern like security. An ADR in RFC status is typically a draft, open for commentary and critique from anyone invited to do so. An ADR in RFC status should always have a “respond by” deadline.

**Proposed**

- After everyone has a chance to comment, the ADR’s status moves to Proposed. This means the ADR is waiting for approvals. You might edit it or even overhaul the decision if you discover a limitation that makes it a no-go. In other words, you still haven’t made a decision, but you’re getting there.

**Accepted**

- Does exactly what it says on the tin. A decision has been made, and everyone is on board who needs to be. An Accepted status also tells the team tasked with implementing this decision that they can get started.

## Writing ADRs: What’s your status? (continued)

Well, you write another ADR. The old ADR is superseded by the new one, and you record it as such. Suppose the customer survey team realizes that a relational database is no longer fulfilling their needs, so they do another trade-off analysis and decide to switch to a document store. Here are the titles and statuses of the old and new ADRs:

![[Pasted image 20250414230925.png]]

An accepted ADR can move into Superseded status if a future ADR changes the decision it documents. It’s important for both ADRs to highlight which ADR did the superseding and which ADR has been superseded. This bidirectional linking allows anyone looking at a superseded ADR to quickly realize that it’s no longer relevant, and tells them exactly where to look for details on the new decision.

## Writing ADRs: What’s your status? (recap)

![[Pasted image 20250414231024.png]]

## Writing ADRs: Establishing the context

**==Context matters. Every decision you’ve ever made, you made within a certain context and with certain constraints.==**

The Context section in the ADR template is your place to explain the circumstances that drove you to make the decision the ADR is capturing. It should also capture any and all factors that influenced your decision. While technological reasons will usually find their way onto this list, it’s not unusual to include cultural or political factors to help the reader understand where you’re coming from.

## Writing ADRs: Communicating the decision

![[Pasted image 20250414231328.png]]

 If this ADR’s status is RFC or Proposed, the decision hasn’t been made (yet). Even so, the Decision section starts by clearly expressing the decision being made. The tone of the writing should reflect that. It’s best to use an authoritative voice when stating the decision, with

The Decision section is also the place to explain why you’re making this decision, paying tribute to the Second Law of Software Architecture: “Why is more important than how.” Future you, or anyone else who reads the ADR, will then understand not just the decision but the justification for it.

## Writing ADRs: Considering the consequences

Every decision has consequences

It’s important to realize the consequences—good and bad—of architectural decisions and document them. This increases transparency by ensuring that everyone understands what the decision entails, including the team(s) affected by it. Most importantly, it allows everyone to assess whether the decision’s positive consequences will outweigh its negative consequences.

The consequences of an ADR can be limited in scope or have huge ramifications. Architectural decisions can affect all kinds of things—teams, infrastructure, budgets, even the implementation of the ADR itself. Here’s an incomplete list of questions to ask:

- How does this ADR affect the implementing team? For instance, does it change the algorithms? Does it make testing harder or easier? How will we know when we’re “done” implementing it?

- Does this ADR introduce or decommission infrastructure? What does that entail?

- Are cross-cutting concerns like security or observability affected? If so, what effects will that have across the organization?

- How will the decision affect your time and budget? Does it introduce costs or save money? Will it take arduous effort to implement or make things easier?

- Does the ADR introduce any one-way paths? (For example, using queues means we can’t control the order of messages.) If so, elaborate on this.


Collaborating with others is a great way to make sure your assessment is thorough. No matter how hard you think through the consequences of the ADR, you’re likely to miss a few things; multiple perspectives will reveal more potential consequences. Here’s a sample Consequences section

![[Pasted image 20250414231537.png]]

## Writing ADRs: Ensuring governance

Sure, you and your team spent a bunch of time analyzing trade-offs and writing an ADR to record the decision. Now what? How do you ensure that the decision is correctly implemented—and that it stays that way?

This is the role of the Governance section, which is vital in any ADR. Here, you outline how you’ll ensure that your organization doesn’t deviate from the decision— now or in the future. You could use manual techniques like pair programming or code reviews, or automated means like specialized testing frameworks.

## Writing ADRs: Closing notes

The Notes section contains metadata about the ADR itself. Here’s a list of fields we like to include in our ADRs:
• Original author
• Approval date
• Approved by
• Superseded date
• Last modified date
• Modified by
• Last modification

## Bullet Points

- There is nothing “static” about architecture. It’s constantly changing and evolving.

- Requirements and circumstances change. It’s up to you to modify your architecture to meet new goals.

- For every decision, you will be faced with multiple solutions. To find the best (or least worst), do a trade-off analysis. This collaborative exercise helps you identify the pros and cons of every possible option.

- The First Law of Software Architecture is: Everything in software architecture is a trade-off.

- The answer to every question in software architecture is “it depends.” To learn which solutions are best for your situation, you’ll need to identify the top priorities and goals. What are the requirements? What’s most important to your stakeholders and customers? Are you in a rush to get to market, or hoping to get things stable in growth mode?

- The product of a trade-off analysis is an architectural decision: one of the four dimensions needed to describe any architecture.

- An architectural decision involves looking at the pros and cons of every choice in light of other constraints—such as cultural, technical, business, and customer needs—and choosing the option that serves these constraints best.

- Making an architectural decision isn’t just about choosing; it’s also about why you’re choosing that particular option.

- The Second Law of Software Architecture is: Why is more important than how.

- To formalize the process of capturing architectural decisions, use architectural decision records (ADRs). These documents have seven sections: Title, Status, Context, Decision, Consequences, Governance, and Notes.

- Over time, your ADRs will build into a log of architectural decisions that will serve as the memory store of your project.

- An ADR’s title should consist of a three-digit numerical prefix and a noun-heavy, succinct description of the decision being made.

- An ADR can be assigned one of many statuses, depending on the kind of ADR and its place in the decision workflow.

- Once all parties involved in the decision sign off on the ADR, its status becomes Accepted.

- If a future decision supplants an Accepted ADR, you should write a new ADR. The supplanted ADR’s status is marked as Superseded and the new ADR becomes Accepted.

- The Context section of an ADR explains why the decision needed to be made to begin with.

- The Decision section documents and justifies the actual decision being made. It always includes the “why.”

- The Consequences section describes the decision’s expected impact, good and bad. This helps ensure that the good outweighs the bad, and aids the team(s) implementing the ADR.

- The Governance section lists ways to ensure that the decision is implemented correctly and that future actions do not stray away from the decision.

- The final section is Notes, which mostly records metadata about the ADR itself—like its author and when it was created, approved, and last modified.

- ADRs are important tools for abiding by the Second Law of Software Architecture, because they capture the “why” along with the “what.”

- ADRs are necessary for building institutional knowledge and helping teams learn from one another.


# Chapter- 4 The Building Blocks logical components

## Logical components revisited

Logical components are one of the dimensions of software architecture. They are the functional building blocks of a system that make up what is known as the problem domain

Remember that, in most programming languages, logical components are represented through the directory structure of your source code repository

## Logical versus physical architecture

A logical architecture shows all of the logical building blocks of a system and how they interact with each other (known as coupling). 

A physical architecture, on the other hand, shows things like the architectural style, services, protocols, databases, user interfaces, API gateways, and so on.

![[Pasted image 20250419131437.png]]     
![[Pasted image 20250419131511.png]]

## Creating a logical architecture

![[Pasted image 20250419131548.png]]

## This flow continues as long as the system is alive.

Ever wonder why it’s so common for a well-designed system to end up as an unmaintainable mess in no time? It’s because teams don’t pay enough attention to the logical architecture of their systems.

Anytime you make a change or add a new feature to the system, you should always go through each of these steps to ensure that the logical components are the right size and are doing what they are meant to do

## Step 1: Identifying initial core components

The first step in creating a logical architecture is identifying the initial core components. Many times this is purely a guessing game, and you’ll likely refactor the components you initially identify into others.

You don’t know a lot of details about the system or its requirements yet, and the components you initially identify are likely to change as you learn more. That’s why we say it’s a guessing game at this stage—and that’s perfectly okay!

two common approaches for identifying initial core components: **the workflow approach** and the **actor/action approach**.

## Workflow approach

The workflow approach is an effective way to identify an initial set of core components by thinking about the major workflows of the system—in other words, the journey a user might take through the system. Don’t worry about capturing every step; start out with the major processing steps, and then work your way down to more details.

![[Pasted image 20250419132055.png]]

## Names matter.

Pay close attention to how you name your initial core components. A good name should succinctly describe what that component does.

## Actor/action approach

The actor/action approach is particularly helpful if you have multiple actors (users) in the system. You start by identifying the various actors. Then, you identify some of the primary actions they might take and assign each action to a new or existing component.

## The entity trap

the entity trap because it’s very easy to fall into it when identifying the initial core logical components, and you’ll run into lots of issues if you do this.

First of all, the name “Bid Manager” is too vague. Can you tell what the component does just by looking at the name? Neither can we. A name like this doesn’t tell us enough about the component’s role and responsibilities.

Second, the component has too many responsibilities. All too often, components in the entity trap become convenient dumping grounds for all functionality related to those entities. As a result, they take on too much responsibility and become too big and difficult to maintain, scale, and make fault tolerant.

> **Watch out for words like manager or supervisor when naming your logical components—those are good indicators that you might be in the entity trap.**

## Step 2: Assign requirements

Once you’ve identified some initial core components, it’s time to move on to the next step: assigning requirements to those logical components

you’ll take functional user stories or requirements and figure out which component should be responsible for each one. Remember, each component is represented by a directory structure. Your source code resides in that directory, so it contains that requirement.

## Step 3: Analyze roles and responsibilities

functionality (in other words, user stories or requirements) to logical components, the roles and responsibilities of each component will start to naturally grow. The purpose of this step is to make sure that the component to which you are assigning functionality should actually be responsible for that functionality and that it doesn’t end up doing too much.

## Sticking to cohesion

When you analyze a component’s role and responsibility statement or set of operations, check to see if the functionality is closely related. This is known as cohesion: the degree and manner to which the operations of a component are interrelated. Cohesion is a useful tool for making sure a component has the right responsibilities

When analyzing the role and responsibilities of a component, it’s common to find an outlier (an odd piece of functionality) or a component that is doing too much. In these cases, it’s usually a good idea to shift some of the responsibility to other components.

## Step 4: Analyze characteristics

The final step in identifying initial core components is to verify that each component aligns with the driving architectural characteristics that are critical for success. In most cases this involves breaking apart a component for better scalability, elasticity, or availability, but it could also involve putting components together if their functionalities are tightly coupled.

As you identify the initial core components, it’s important to determine how they interact. This is known as component coupling: the degree to which components know about and rely on each other. The more the components interact, the more tightly coupled the system is and the harder it will be to maintain

That’s why it’s so important to pay attention to how components interact and what dependencies exist between them.

You need to be concerned about two types of coupling when creating logical components: afferent coupling and efferent coupling. Don’t be concerned if you’ve never heard these formal terms before—we’re going to explain them in the following pages.

## Afferent coupling

Afferent coupling is the degree and manner to **==which other components are dependent on some target component==** (in this case, Mom). It’s sometimes referred to as fan-in, or incoming, coupling. In most code analysis tools, it’s simply denoted as CA.

![[Pasted image 20250419133226.png]]

## Efferent coupling

Efferent coupling **==is exactly the opposite of afferent coupling, and it’s measured by the number of components on which a target component depends==**. It’s also known as fan-out coupling or outgoing coupling. In static source code analysis tools, it’s usually denoted as CE.



### **==Two components are coupled if a change in one component might cause a change in the other component.==**


## Bullet Points

- Logical components are the functional building blocks of a system.
- A logical component is represented by a directory structure—the folder where you put your source code.
- When naming a component, be sure to provide a descriptive name to clearly identify what the component does.
- Creating a logical architecture involves four continuous steps: identify components, assign requirements, analyze component responsibilities, and analyze architectural characteristics.
- You can use the workflow approach to identify initial core logical components by assigning the steps in a primary customer journey to components.
- You can use the actor/action approach to identify initial core logical components by identifying the actors in the system and assigning their actions to components.
- The entity trap is an approach that models components after major entities in the system. Avoid using this approach, because it creates ambiguous components that are too large and have too much responsibility.
- When assigning requirements to components, review each component’s role and responsibilities to make sure it should be performing that function.
- Coupling happens when components depend on one other to perform a business function.
- Afferent coupling, also known as incoming coupling, occurs when other components are dependent on a target component.
- Efferent coupling, also known as outgoing coupling, occurs when a target component is dependent on other components.
- Components having too much knowledge about what needs to happen in the system increases component coupling.
- The Law of Demeter states that services or components should have limited knowledge of other services or components. This law is useful for creating loosely coupled systems.
- While loose coupling reduces dependencies between components, it also distributes workflow knowledge, making it harder to manage and control that knowledge.
- Determining the total coupling (CT) of a logical architecture involves adding the afferent and efferent coupling levels for each component (CA + CE).
