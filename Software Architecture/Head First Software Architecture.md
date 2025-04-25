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

# Chapter-5 architectural styles Categorization and Philosophies

## The world of architectural styles

The first deals with how the code is divided: either by technical concerns or by domain (business) concerns. The second category is about how the system is deployed: is all the code in the system delivered as one unit, or as multiple units?

![[Pasted image 20250420195400.png]]

Each category reveals some of the architectural characteristics of its styles. For example, architectural styles delivered as one unit are easier to understand, but those delivered as multiple units tend to scale better.

## Partitioning: Technical versus domain

In a technically partitioned architecture, code is divvied up by technical concerns— there might be a presentation tier, a business (services) layer, and so on. The principle at play here is separation by concern—which most people think about in horizontal layers.

![[Pasted image 20250420195455.png]]

In domain-partitioned architectures, the structure of the system is aligned with the domain. Rather than by roles, the code (and systems) are separated in ways that align with the problem you’re attempting to solve.

![[Pasted image 20250420195524.png]]

## Deployment model: Monolithic versus distributed

In a monolithic architecture, you deploy all the logical components that make up your application as one unit. This also means that your entire applications runs as one process.

![[Pasted image 20250420195609.png]]

In a distributed architecture, by contrast, you split up the logical components that make up the application across many (usually smaller) units. These units each run in their own process and communicate with each other over the network.

![[Pasted image 20250420195632.png]]

## Monolithic deployment models: The pros

**Simplicity**  
Typically, monolithic applications have a single codebase, which makes them easier to develop and to understand.

**Cost**  
Monoliths are cheaper to build and operate because they tend to be simpler and require less infrastructure.

**Feasibility**  
Rushing to market? Monoliths are simple and relatively cheap, freeing you to experiment and deliver systems faster.

**Debuggability**  
If you spot a bug or get an error stack trace, debugging is easy, since all the code is in one place.

**Reliability**  
A monolith is an island. It makes few or no network calls, which usually means more reliable applications.

## Monolithic: The cons

**Scalability**  
If you ever need to scale one part of the application independently of the others, well, you’re in trouble. It’s all or nothing with monoliths.

**Evolvability**  
As monolithic applications grow, making changes becomes harder. Furthermore, since the whole application is one codebase, you can’t adapt different technology stacks to different domains if you need to.

**Deployability**  
Implementing any change will require redeploying the whole application, which could introduce a lot of risk.

**Reliability**  
Because monolithic applications deploy as a single unit, any bug that degrades the service will affect the whole monolith.

## Distributed deployment models: The pros

**Deployability**  
Distributed architectures encourage lots of small units. They evolved after modern engineering principles like continuous integration, continuous deployments, and automated testing became the norm.

**Testability**  
Each deployment only serves a select group of logical components. This makes testing a lot easier—even as the application grows. Distributed architectures are a lot more testable than monolithic applications.  
Having lots of small units with good testability reduces the risk associated with deploying changes.

**Fault Tolerance**  
Distributed systems can be designed to tolerate failure in individual components without taking down the entire system.

**Scalability**  
Distributed architectures deploy different logical components separately from one another. Need to scale one? Go ahead!

**Modularity**  
Distributed architectures encourage a high degree of modularity because their logical components must be loosely coupled.

## Distributed deployment models: The cons

**Performance**  
Distributed architectures involve lots of small services that communicate with each other over the network to do their work. This can affect performance, and although there are ways to improve this, it’s certainly something you should keep in mind.

**Cost**  
Deploying multiple units means more servers. Not to mention, these services need to talk to one another—which entails setting up and maintaining network infrastructure.

**Simplicity**  
Distributed systems are the opposite of simple. Everything from understanding how they work to debugging errors becomes challenging.

**Debuggability**  
Errors could happen in any service involved in servicing a request. Since logical components are deployed in separate units, tracing errors can get very tricky.

## Bullet Points

- There are a lot of architectural styles—in fact, too many to count.
- Architectural styles can be categorized in multiple ways:
  
  **By Partitioning Style:**
  - **Technically Partitioned**:
    - Code is split by technical concern (e.g., presentation layer, services layer).
  - **Domain Partitioned**:
    - Code is split by problem domain.

  **By Deployment Model:**
  - **Monolithic Architectural Styles**:
    - All logical components are deployed as a single unit.
    - Easier to understand and debug.
    - Often cheaper to build initially.
    - Good choice for quickly bringing a product to market.
    - Harder to scale as they grow—scaling is all-or-nothing.
    - Can be unreliable—a single bug may crash the entire application.

  - **Distributed Architectural Styles**:
    - Logical components are deployed separately as multiple units.
    - Highly scalable—different parts can scale independently.
    - Encourages modularity, making testing easier.
    - Expensive to develop, maintain, and debug.
    - Requires network communication between services, adding complexity.

# Chapter-6 layered architecture Separating Concerns

## Design patterns redux

Model-View-Controller (MVC) design pattern, which separates capabilities based on their purpose

In MVC, the model represents business logic and entities in the application; the view represents the user interface; and the controller handles the workflow, stitching model elements together to provide the application’s functionality

![[Pasted image 20250420200622.png]]

## Layering MVC

Design patterns represent logical solutions to problems, but architecture must deal with real-world constraints like databases, user interfaces, and other implementation details.

**Presentation**

The V for “view” in MVC concerns the UI and how the user interacts with the system. In a layered architecture, UI elements appear in the presentation layer.

**Workflow**

The workflow layer contains most of the application’s code. Business logic, workflows, validations, and other domain activities reside in this layer

**Persistence**

Many teams use a special persistence layer in their architecture to map code-based hierarchies (such as object oriented languages) into set based relational databases

---

How does a user request fit into the layered structure we’ve been building?

In a layered monolithic architecture, when a user asks the system to do something, the user interface initiates the request. Then that request flows through each layer in the architecture. If the database is involved in persisting something, then the request goes from top to bottom and back.

![[Pasted image 20250420200840.png]]

---

### ==**the domain behavior lives across the layers in this architecture.**==

The domain, as you’ll recall, represents logical components based on the problem you’re trying to solve. However, the layers in this architecture represent technical capabilities— user interface, business logic, and so on.

## Drivers for layered architecture

**Specialization**

Using a layered architecture allows organizations to split teams into specialists, sharing their capabilities between different projects.

**Ease of (technical) reuse**
 
 Splitting the architecture by technical capabilities allows better opportunities to reuse code. For example, if all persistence code resides in a single layer, it’s easier for developers to find, update, and reuse it.

**Matches physical separation**

The layered architecture typically
separates the logical components to match the physical separation. For example, it’s common for teams to implement different layers in different technology stacks (such as JavaScript, Java, and MySQL)

**Conceptual twin of MVC**

Simplicity and concerns about feasibility are driving forces in many architectures. Developers find it easier to understand and work within an architecture that matches familiar design patterns, such as MVC.

## One final cave at about domain changes
 
 The power to change things in isolation is the layered architecture’s superpower, but it’s not a silver bullet. This architectural style’s big trade-off is that the problem domain is smeared across the layers in the architecture.

That means that technical capabilities are easy to change and enhance, but domain changes can create side effects that ripple through the layers.

### **==Layered architectures facilitate technical changes but make domain change s more difficult.==**


If continual, significant domain changes are expected or suddenly become a higher priority, there are other architectural styles to consider.

## Layered architecture superpowers

**Feasibility**

If time and budget are overwhelmingly important, the simplicity of this architecture is quite appealing

**Technical partitioning**

Architects design components around technical capabilities, making it easier for them to reuse common capabilities. For example, if several teams need the same data functionality, they could implement it once in a persistence layer and then share it across teams.

**Data-intensive**

Systems that do a lot of data-level processing may benefit from a layered architecture because it isolates data processing in a single database that’s optimized for the task.

**Performance**

Well-designed layered monoliths can demonstrate high performance—making no network calls and processing data in a single place (the monolithic database) means there’s no need for network calls that could decrease performance.

**Quick to build**

Simplicity plus a single work/deployment unit means that teams can build small systems quite rapidly

**Lean and mean**

Keeping these systems small helps avoid some of the kryptonite on the next page

## Layered architecture kryptonite

**Scalability**

Probably the biggest problem with monoliths is that when you only have one bucket and you keep adding things to it, it will eventually fill up. The same is true for monoliths generally, which eventually become constrained by some resource (memory bandwidth, and so on).

**Elasticity**
A single process has a harder time dealing with sudden bursts of users.

**Testability**
High coupling and a large codebase make testing harder and harder over time

**Deployability**
As monolithic systems get bigger, deployments tend to become more complex—especially when developers keep adding behavior

**Big ball of mud**
Because everything is connected to everything else, this architecture can become a highly coupled mess without careful governance

**Testability**
High coupling and a large codebase make testing harder and harder over time.

## Bullet Points

- A layered architecture is monolithic: the entire system (code and database) is deployed as a single unit.
- The layers are separated by technical capabilities. Typical layers in this architecture include presentation (for the user interface), business rules (for the workflow and logic of the application), and persistence (facilities to support databases for systems that need persistent data).
- The layered architecture supports feasibility well; it is easy to understand and it lets you build simple systems fast.
- The layered architecture supports excellent separation of technical concerns, making it easy to add new capabilities like user interfaces or databases.
- The layered architecture mimics some of the same concerns as the Model-View-Controller design pattern, but translated into physical layers and subject to real-world constraints.
- User requests flow through the user interface and through each layer before a response is returned to the user.
- Each request in this architecture goes through each layer.
- A layered architecture’s capabilities degrade over time if teams continue to add functionality due to eventual resource limits (for example, they run out of capacity).
- The layered architecture provides excellent support for specialization (user interface designers, coders, database experts, and so on).
- Logical components represent the problem domain, yet layers focus on technical capabilities, requiring translation between the domain and architecture layers.
- A layered architecture may manifest in several physical architectures, including two-tier (also known as client/server), three-tier (web), and embedded/mobile.
- Changing and adding to the technical capabilities represented in layers is easy; the layered architecture facilitates this.
- Changing the problem domain requires coordination across the layers of the architecture, making domain changes more difficult.

# Chapter 7- modular monoliths Driven by the Domain

## Modular monolith?

==**A modular monolithic architecture, like a layered architecture, is deployed as a single unit, usually with its own database.**==

That’s where the similarity ends. **==In a modular monolith, rather than partitioning your application by technical concerns, you partition it by functionality==**. Every business operates within a certain domain—like banking, education, or retail

You organize your application according to these subdomains, separating them into modules.

![[Pasted image 20250423150756.png]]

What is a module? At a high level, it’s just how you organize your code. In some languages, you might have support like packages or namespaces. But it doesn’t start or stop there.

as mentioned in the previous chapter, in a technically partitioned architecture the business domain gets *smeared* across multiple layers. This is great if you’re implementing a technical change, like changing the view technology or swapping out the database. But it’s not so great if the change affects the domain—you’ll have to round up folks from multiple teams to figure out how to implement it.

## Why modular monoliths?

You don’t organize the application in horizontal layers separated by technical concern, but in vertical slices scoped by business concern. Each vertical slice aligns with a piece of the domain and is encapsulated in a module. Every module contains a set of business functions—for example, order placement, order completion, and order delivery would all be part of the Order Placement module.

![[Pasted image 20250423151007.png]]

Changes to the domain that affect many or all layers require lots of coordination between different teams

Now, rather than having teams that specialize in the presentation layer or the persistence layer, you have **cross-functional teams**, each specializing in a domain. The result? It’s far easier to coordinate domain changes when one team takes full ownership.

**how a module is laid out internally isn’t how the architecture is partitioned.**

## Keeping modules modular

Modular monoliths are, well, monoliths, so they’re generally contained in one codebase. That makes it easy for someone working in one module to inadvertently reach into another module and end up coupling the two modules together

**==The philosophy of the modular monolith centers on partitioning by domain within a monolithic deployment model.==** Your objective should be to create loosely coupled modules so that changing one doesn’t affect others. So how do you avoid the big ball of mud? 

From a code design perspective, it’s best to think of each module as a separate service. Just to be clear, though, they aren’t really separate—they all still constitute one monolithic deployment.

![[Pasted image 20250423152215.png]]

Some languages, like Java, have built-in support to build modules.

Another approach is to break up your project code so that each module is a separate folder in your repository. These subprojects (or, as many build systems call them, multimodule projects) force isolation by virtue of being different projects. You might even consider creating different repositories to contain individual modules, then stitching the complete application together at build time.

Of course, you are still deploying a monolith, so you’ll probably need to bring all the modules together using your build tool of choice. A monolithic deployment model doesn’t have to mean a monolithic codebase!

## Taking modularity all the way t o the database

The modular monolith is still a monolithic deployment, typically with a monolithic database backing it. There is a lot of power here: having a single database can make things a lot simpler. You don’t have to worry about transactions or eventual consistency, and most developers are very comfortable working with just one database. However, if you intend to maintain modularity at all levels, then you should consider modularizing your data.

For every module in your application, you define a schema and a set of tables. Any and all data that belongs to a particular module will reside only in the tables for that module

## Beware of joins

Keeping different tables, perhaps even in different schemas, does partition the data belonging to different modules—but it’s easy to slip up and accidentally perform a SQL join across tables that belong to different modules. Then you’re back to tight coupling! It’s OK to store the IDs of records that belong to one module in another module’s tables.

## Modular monolith superpowers

**Domain partitioning**
Architects can design components around domain concerns, then build teams that specialize in one or more of these domains (as opposed to a technical specialization). Domain partitioning is the key superpower of this architectural style

**Domain-based alignment**
Modular monoliths encourage cross functional teams, which are better aligned with the domain than the technically partitioned teams used in layered architectures.

**Performance**
Performance is usually very good, like for most monolithic architectures. There are no network calls between modules, and all data processing happens in a single place.

**Maintainability**
Modular monoliths separate business concerns from one another, with cross functional teams each specializing in a subdomain. This makes it easier to maintain the code, as long as changes don’t cross into other domains.

**Testability**
Since the scope of changes is limited to one module, testing is much easier. And since a cross-functional team’s members understand their subdomain really well, they can build out an entire testing suite, including integration, smoke, and end-to-end tests.

## Modular monolith kryptonite

**Hard to reuse**

Modular organization makes it hard to reuse logic and utilities across modules. For example, you can’t share common functionality between modules without extracting it as a dependency, increasing the coupling between the modules.

**(Still) a single set of architectural characteristics**

Even though modular monoliths are organized by modules, you still get a single set of architectural characteristics for the entire application—even if one business concern has a different set of needs than others.

**Modularity can be fragile**

It’s easy to dilute module boundaries accidentally. Avoiding the big ball of mud takes a lot of governance—and the database is even harder to govern.

**Operational characteristics**

Despite its focus on business concerns, a modular monolith is still, well, a monolith. And as with any monolith, operational characteristics like elasticity and fault tolerance tend to be hard to attain.

## Bullet Points

- A modular monolith is a monolithic architectural style that is partitioned by domains and subdomains that reflect business concerns, not technical concerns.
    
- Each subdomain makes up one module of the application. Each module can contain multiple business use cases.
    
- Each module can be made up of layers to provide better organization. A module may be technically partitioned as a means to organize its functionality.
    
- Avoid having code in one module directly access any functionality in other modules. Allowing this can reduce or eliminate the boundaries between modules.
    
- Each module should have a public API that communicates with other modules while shielding the module’s internal implementation from the rest of the world.
    
- Avoiding inter module communication allows modules to change internally without affecting other modules.
    
- It takes time and effort to ensure that the modules in a modular monolith remain separate and distinct.
    
- You can govern a modular monolith using a variety of techniques. Some languages have built-in support for building modules.
    
- Another approach is to physically break up the codebase into separate subprojects or even different repositories. This usually involves using a build tool to bring all the modules back together when you build the monolith.
    
- Third-party tools can also help with architectural governance.
    
- You may choose to use several techniques in combination to ensure the boundaries of individual modules are maintained.
    
- You can extend modularity all the way to the database, keeping the data for each module separate.
    
- Watch that you don’t accidentally couple modules when inserting or fetching data (for example, when using a SQL join statement across tables that belong to different modules).

# Chapter - 10 microservices architecture

## What’s a microservice?

Generally, a service is a separately deployed unit of software that performs some business or infrastructure process. The prefix micro- in microservice refers not to physical size, but to what the service does.


### **==A microservice is a single-purpose, separately deployed unit of software that does <u>one thing</u> really well.==**

## It’s my data, not yours

Another feature that makes microservices special is that they own their own data. In other words, each microservice is the only one that can directly access its data.

![[Pasted image 20250425131854.png]]

**==The primary reason is to manage change control.==** Say you have 50 microservices, all sharing the same data. If one microservice changes the structure of its data, which the other 49 microservices are also accessing, all of those other services will need to change at the same time.

Physically associating a microservice with its data is known as creating a **physical bounded context**. Physical bounded contexts help manage change and coupling. If other microservices need access to data they don’t own, they must ask the owning service for it.

## How micro is “micro”?

**No, granularity is not a guessing game.**

Granularity—the scope of what a microservice does—is an important factor when identifying microservices. Microservices that are too fine-grained tend to communicate more with each other to complete business functions, leading to high levels of coupling, poor performance, and overall reliability issues. This is commonly referred to as the **==Grains of Sand antipattern==**, in which services are so small that they start to resemble sand on a beach. However, microservices that are too coarse-grained are harder and more expensive to maintain, test, and scale (which defeats the whole purpose of using microservices).

So how do you determine the most appropriate level of granularity for a microservice? By applying forces called **==granularity disintegrators and granularity integrators==**. Granularity disintegrators are forces that tell you to make your service smaller (meaning it’s doing less work), whereas granularity integrators are forces that tell you to make the service bigger (meaning it’s doing more work). Let’s see how these forces work.

![[Pasted image 20250425132254.png]]

## Why should you make microservices smaller?

**Cohesion**  
A single-purpose microservice has functionality that is highly cohesive—meaning all the things it does are closely related to each other. If the functionalities of a microservice lack cohesion, then it might be a good idea to break that microservice apart.

**Code volatility**  
Does one part of the microservice change faster than others? Constant changes to one part of a large microservice mean you have to test the entire microservice, including functionalities you didn’t change. That’s a lot of extra work.  
Moving a frequently changing function into its own separate microservice isolates those changes from other functions, making it much easier to maintain and test functionality.

**Scalability and throughput**  
Do some parts of the microservice need more scalability than others? If so, breaking the service apart allows better control over which portions need to scale and which do not.  
For example, suppose the heart rate monitoring function accepts sensor readings every second, but the temperature monitoring function accepts sensor readings once every 5 minutes. Separating these monitoring functions into distinct services allows each one to accommodate a different throughput rate.

**Fault tolerance and availability**  
Do certain functions in a microservice frequently produce fatal errors? In larger microservices, all functionalities become unavailable when a part of the microservice fails. However, if the faulty functionality is in its own separate microservice, it won’t affect other functions.

**Access control**  
The larger the service, the more difficult it is to control access to sensitive information. For example, a Patient Profile microservice containing functionality to access medical history might inadvertently allow unauthorized staff to access this sensitive (and protected) information.  
Moving sensitive functionalities (like access to medical history) into their own microservices isolates them, making it easier to control access to that information.

**Startup speed**  
Smaller microservices start up much faster than larger ones, making much-needed functionality available to the user sooner.

*This is also referred to as “volatility-based decomposition.”*


## Why should you make microservices bigger?

**Database transactions**  
When requests involve multiple microservices, you can’t perform a single database commit or rollback for all updates. Since each microservice update is in its own separate transaction, it must instead be committed or rolled back separately.  
If data consistency and integrity are more important than any of the disintegrator forces, then it makes sense to combine the functionality into a single microservice so that operations take place in a single database transaction.

**Workflow and choreography**  
If a single business request requires separate microservices to communicate with each other, that’s coupling. Too much coupling between microservices can have many negative effects on the system.  
For example, performance is affected by network, security, and data latency. Scalability is affected because each microservice in the call chain must scale as the other microservices scale (something that is hard to coordinate). Fault tolerance is affected because if one of the microservices in the chain becomes unresponsive or unavailable, the request cannot be processed.  
If your workflow involves a lot of coordination between your microservices and these characteristics are important to you, consider combining them.

**Data dependencies**  
When you break a microservice apart, you also have to break its data apart. However, if the data is highly coupled, it will be very difficult to break it apart and form new physical bounded contexts.  
An example of data coupling is when one database table refers to the key of another database table (known as a foreign key constraint). Another example of data coupling is when an entity (like customer information) is spread across multiple tables.  
If your data is highly coupled and functions in the microservice need to share that data, it makes sense to keep the microservice large and combine the functions.

*Data dependencies are one of the most common integration drivers.*

**Too much communication between microservices can make an architecture look like spaghetti.**

## You can still share code in microservices.

Code reuse is a necessary part of software development. Without it, you would have duplicate functionality almost everywhere in your system. Functions like logging, metrics streaming, user authorization, and basic utilities like transforming date formats are common in most (if not all) systems.

In monolithic systems, this is easy—you write the common functionality once and use it everywhere in the system, because it’s all compiled together as one unit. But in distributed architectures like microservices, it’s not that easy. That’s because each microservice is a separately deployed unit of software.

So where does all that common functionality go in microservices? **==Usually into either a shared library or a shared service.==**

## Code reuse with a shared service

**==A shared service is a separate microservice that contains a shared functionality that other microservices can call remotely==**.

**Pros of using a shared service**  
- Changing common code in a shared service doesn’t require changing other microservices.  
- The shared service can be written in any language and on any platform, which is handy when you have microservices implemented in multiple languages.

**Cons of using a shared service**  
- Changing a shared service is risky because it can immediately affect other microservices that call it.  
- Because the shared functionality is remote, network latency can slow its performance.  
- If the shared service is unavailable, microservices that need the shared functions cannot operate.  
- The shared service must scale whenever other microservices that call it scale.

## Code reuse with a shared library

A more common approach to shared functionality is to put it in a custom shared library. A shared library is an independent artifact (like a JAR file in Java or a DLL in C#) that is included with each microservice at compile time. This means that once the microservice is deployed, each microservice has all of the shared functionality available to it.

**Pros of using a shared library**  
Performance, availability, and scalability are better because the shared functionality is not remote. Instead, it’s bound at compile time to each microservice.  
Changing code in a shared library is less risky, because shared libraries can be versioned to provide agility and backward compatibility.

**Cons of using a shared library**  
You’ll need multiple shared libraries if your microservices are written in different programming languages or use different platforms.  
Managing dependencies between microservices and shared libraries can become difficult if you have a lot of microservices (which is typical in this architectural style).  
If you change a shared functionality, you must retest and redeploy the microservices that use it.

## workflow management

A workflow is when fulfilling a single business request—a task request that comes from a user interface—needs more than one microservice. You can manage a workflow in microservices by using either of two techniques:

## Orchestration: Conducting microservices

Orchestration is about coordinating all the microservices needed for a workflow. A centralized microservice—the orchestrator— does this, very much like a conductor coordinates all the musicians performing in a symphony orchestra.

An orchestration service is a separate microservice that is responsible for calling all the microservices involved in the workflow. It also handles errors and passes consolidated data back to the caller (usually the user interface).

**The good...**

**Centralized workflow**  
Request workflows are centralized and well understood. You only need to go to the orchestrator to understand the complete workflow.

**Error handling**  
Error handling is consolidated into the orchestrator, so each microservice doesn’t need to worry about what to do if an error occurs—the orchestrator handles it.

**Workflow state**  
Since the orchestrator always knows where the request is in the workflow, if there’s a failure, restarting the request where the workflow left off is much easier.

**Workflow changes**  
It’s easy to change the workflow because all changes occur in one central place.

**The bad...**

**Performance**  
Orchestration tends to be slowed by communication between the orchestrator and the microservices, and because the orchestrator typically saves the workflow state to a database each time something changes.

**Tight coupling**  
Because the orchestrator and microservices need to communicate constantly, orchestration tends to be highly coupled.

**Scalability**  
The central orchestrator can become a bottleneck as requests increase, because every request must go through it before reaching any microservices.

**Availability**  
If the conductor leaves the orchestra, the concert is over. Similarly, if the orchestration microservice is unavailable, the request cannot be processed. This single point of failure is usually addressed by creating multiple instances of the orchestrator.


## Choreography: Let’s dance

Like dancers, the microservices communicate with each other. Each performs its function, then calls the next microservice to perform its function, until the workflow is complete.

**The good...**

**Responsiveness**  
Since there’s no central orchestrator to communicate with continually, responsiveness and performance tend to be better.

**Loose coupling**  
Since microservices don’t depend on a central orchestration service to direct them, the system tends to be less coupled.

**Scalability**  
Each microservice can scale to meet its throughput demands, independent of other microservices in the workflow.

**The bad...**

**Error handling**  
Each microservice is responsible for managing the error workflow if an error occurs. This can lead to too much communication between services.

**State management**  
It’s hard to know what state the workflow is in when using choreography, because there’s no central conductor controlling the workflow. Usually, one of the microservices (typically the first one in the call chain) is designated the state owner, and other microservices send it their state.

**Recoverability**  
When a user retries a request that has failed or is still in progress, it’s really hard for the system to know where to restart. That’s because no single service is responsible for directing the request to a specific microservice in the workflow—each one only sends it to the next microservice in the call chain.

*Be careful—state management can lead to the Front Controller pattern, described in the “Watch it!” box on the previous page.*

## Microservices architecture superpowers

**Maintainability**  
Because microservices are single-purpose and separately deployed, you can more easily locate code that needs to change for a particular function.

**Testability**  
A microservice’s testing scope is much smaller than that of a larger monolithic application or a system with large services. This limited scope makes it easier to fully test a microservice’s functionality.

**Deployability**  
Because microservices are deployed as separate units of software, there are fewer risks involved with releasing a microservice than with large monolithic systems. You can also deploy microservices more frequently—sometimes daily.

**Evolvability**  
It’s relatively easy to add functionality to a microservices architecture: you create a new service, test it, and deploy it alongside other existing microservices in your system.

**Fault tolerance**  
If a particular microservice fails, it doesn’t bring down the entire system—only that function. Users can continue to use other functions.

**Scalability**  
Microservices scale at a function level rather than a system level. This means that you scale only the functionalities you need to meet increased user load and demand, saving resources and lowering costs.

*Every architectural style has its superpowers. Here are some reasons to use the microservices architectural style.*

## Microservices architecture kryptonite

**Monolithic databases**  
Each microservice must own its own data and form a physical bounded context.  
If your data can’t be broken apart for whatever reason, stay away from this architectural style.

**Performance**  
The more microservices communicate with each other, the worse their performance will be. They may have to wait for the network, undergo additional security checks, and make extra database calls.

**Technically partitioned teams**  
Does your organization consist of siloed teams of user interface developers, backend developers, and database people? If so, microservices won’t work for you (a reflection of Conway’s Law). Microservices architecture requires cross-functional teams. Each team owns its own group of microservices, all the way from the user interface to the database.

**Complex workflows**  
Workflows occur when you need to call multiple microservices for a single business request. If the functionality of your system is too tightly coupled, breaking it into separately deployed services will only result in a big ball of distributed mud. Yuck!

**Complexity**  
Microservices is one of the most complex architectural styles. It involves so many hard decisions—about granularity, transactions, workflow, contracts, shared code, communication protocols, team topologies, and deployment strategies, just to name a few.

*Are there reasons not to use the microservices architectural style? You bet there are. Just like kryptonite diminishes a superhero’s powers, certain business and architectural characteristics diminish the case for using microservices. Watch out for them!*


## Bullet Points

- A microservice is a single-purpose, separately deployed unit of software that does one thing really well.
- A physical bounded context means that a microservice owns its own data and is the only microservice that can access that data. If a microservice needs data that is owned by another microservice, it must ask for it.
- The granularity of a microservice is a measure of its size—not physically, but the scope of what it does.
- Forces that guide you to make your microservices smaller are called granularity disintegrators.
- Forces that guide you to make your microservices bigger are called granularity integrators.
- Balance granularity disintegrators and integrators to find the most appropriate level of granularity for a microservice.
- You can make microservices coarse-grained to start with, then finer-grained as you learn more about them.
- Two techniques for sharing functionality in microservices are shared services and shared libraries.
- A shared service is a microservice that contains functionality shared by multiple microservices. It’s deployed separately and each microservice calls it remotely.
  - Shared services are more agile overall and are good for heterogeneous environments.
  - However, they are not good for scalability, fault tolerance, or performance.
- A shared library is an independent artifact (like a JAR or DLL file) that is bound to a microservice at compile time.
  - Shared libraries offer better operational characteristics, like scalability, performance, and fault tolerance.
  - But they make it harder to manage dependencies and control changes.
- A workflow is when multiple microservices are needed for a single business request or business process.
- Workflows that use orchestration require a central orchestrator microservice, which works like a conductor in a symphony orchestra.
- In workflows that use choreography, the services talk to each other, like dancers performing together.
- Scalability, fault tolerance, evolvability, and overall agility (maintainability, testability, and deployability) are the superpowers of the microservices architectural style.
- Performance, complexity, cost, monolithic databases that can’t be broken apart, and high semantic coupling are kryptonite to microservices.
- Microservices should be as independent as possible; too much communication between them will degrade the benefits of this architectural style.

# Chapter 11 event-driven architecture - Asynchronous Adventures

the fundamental concept behind **event-driven architecture (EDA)**— breaking up processing into separate services, with each of those services performing its function at the same time by responding to an **event** (something that just happened). In EDA, services communicate asynchronously through an **event channel**, meaning they don’t wait for responses from other services to complete their work.

![[Pasted image 20250425193930.png]]

## What is an event?

An event is something that happens, especially something of importance. In software systems, certain user actions trigger events—things that happen, like placing a bid for an item up for auction, filing an insurance claim, or making a purchase.

**==Events are a way for a service to let the rest of the system know that something important has just happened. In EDA, events are the means of passing information to other services.==**

### **==an event is not the same thing as a message.==**

Although they both deliver information to other parts of the system, there are some important differences between them.

**==An event is used to broadcast some action that a service just performed to other services in the system==**. For example, a service  might tell the rest of the system: A customer just placed an order. A service sending an event never waits for a response. The service generally has no knowledge about what other services (if any) are listening for that event, or what they’ll do with that information if they respond to it.

**==A message, on the other hand, is a command==**, such as Apply the payment for this order, or a request, like Give me shipping options for this customer. Because messages are only meant to reach one other service, the other services in the system are unaware of the message. Services sometimes stop and wait for a response (for instance, if they are sending a request for information). Other times, the service might just issue a command and trust that the receiving service will do its job.

## Events versus messages

### **==Events are broadcast to other services using topics, whereas messages are sent to a single service using queues.==**

![[Pasted image 20250425195050.png]]

### **==Events always broadcast something that has already happened, whereas messages request something that needs to be done.==**

![[Pasted image 20250425195127.png]]

## Initiating and derived events

Events that originate from a customer or end user are called initiating events. These are a special type of event that kicks off a business process.

Once a service responds to an initiating event, it might in turn broadcast what it did to the rest of the system, within the scope of that initiating event. These events are called derived events because they are internal events generated in response to the initiating event.

## Is anyone listening?

In EDA, any action a service performs should trigger a derived event. However, there is a chance that no one cares about certain events. So why publish those events? Because this provides architectural extensibility—the ability to extend the system to add new functionality.

## Asynchronous communication

**Event-driven architecture is fast because it uses mostly asynchronous (or “async” for short) communication.**

## Fire-and-forget

Asynchronous communication is one of the foundations of event-driven architecture. When a service broadcasts information to other services, it doesn’t wait for a response, nor does it care whether the services are available or not. **==This is known as fire-and-forget communication—the event is sent (that’s the fire part), and the service moves on to do other things (that’s the forget part).==** Architects usually use a dotted line to represent async communication between services.

**==Event-driven architecture relies on asynchronous communication when sending and receiving events==**

## Asynchronous for the win

Communicating between services asynchronously has a lot of advantages. The first is **==better responsiveness==**—in async, it takes less time to complete a request.

The other big advantage of async is **==availability==**.

## Synchronous for the win

**==The main disadvantage of async communication is error handling==**. With sync communication, if there’s a problem with the payment method, the customer knows right away and has a chance to fix it and resubmit the order. However, with async, the customer thinks everything is fine because the system hasn’t told them otherwise— but the Order Placement service can’t process the order until the customer corrects the payment problem. This makes error handling much more complex.

## Database topologies

Data can be a complex topic in EDA. Because EDA is so asynchronous, services are highly decoupled from one another. However, if all the services share a single database, then they end up being highly coupled to the database. On the other hand, if each service owns its own data, like with microservices (discussed in the previous chapter), then services become highly coupled to each other because they need to synchronously ask each other for the data. In either case, data forms a coupling point—something we try to avoid in EDA

**==monolithic databases, domain-partitioned databases, and the database-per-service pattern.==**

## Monolithic database

In the monolithic database topology, all services share a single database. **==The main advantage is that when services need data they don’t own, they can go directly to the database. This means they don’t have to make synchronous calls to other services to get data==**

![[Pasted image 20250425200810.png]]

However, this decoupling comes with a steep price: managing database changes. Because all services share the same database, when you make a change to the structure of one table, it’s difficult to identify all the services that change will affect. Testing and releasing becomes a tricky game—one you will all too often lose. This leads to brittle systems that are difficult to maintain.

## Domain-partitioned databases

With domain-partitioned databases, each domain in the system has its own database. This means any service that belongs to a particular domain will share the database for that domain.

However, since each domain forms its own broad physical bounded context, a service in one domain can’t directly access a database to get data from another domain. **==This means it must make a synchronous call to another service to get the data—and now these services are coupled.==**

![[Pasted image 20250425201101.png]]

## Database-per-service

The database-per-service pattern is just what it sounds like. Every service has its own database, forming an even tighter physical bounded context than with the domain-partitioned topology. Here, making database changes is a breeze, because the only service affected is the one that owns the data (that is, does writes to the database). You get better fault tolerance and better scalability, too. What’s not to like?

Unfortunately, plenty. You see, whenever services need additional data they don’t have, they have to ask for that data from the service that owns it using synchronous calls. That results in a lot of coupling and communication between services, not to mention much slower performance.

![[Pasted image 20250425201232.png]]

Even though they may appear similar, EDA and microservices are very different. Both are distributed
architectures good for scalability, agility, elasticity, and fault tolerance.

## EDA versus microservices

**Number 6: Performance**

EDA combines asynchronous processing with the ability to do multiple things at once, creating very fast systems. Microservices, however, because of their bounded contexts and fine-grained nature, frequently need to communicate synchronously. This creates a lot of latency, which slows the system down considerably

**Number 5: Physical bounded contexts**

physical bounded contexts. Microservices won’t work without these. In EDA, however, while a physical bounded context is nice to have, it’s certainly not foundational (or even required). Because data sharing is pretty typical in EDA, this architecture doesn’t restrict data ownership as strictly as microservices does.

**Number 4: Data granularity**

By definition, a microservices architecture requires each service to own its own data. This means you have to break apart your data into fine-grained databases or database schemas—collections of tables that a service owns (writes to). But in EDA, you can choose a single monolithic database, domain-partitioned databases, or the database-per-service pattern.

**Number 3: Service granularity**

a microservice is a single-purpose service that does one thing really well. As a result, microservices tend to be fine-grained. EDA has no such restrictions. Services in an event-driven architecture (formally called event processors) can be whatever size they need to be—fine-grained, coarse-grained, it doesn’t matter.

**Number 2: Event versus request processing**

event processing versus request processing. Event-driven architecture is built on event processing—responding to something that has happened, and in turn triggering more events. Microservices architecture, on the other hand, is built on request processing—responding to something that needs to happen, like a command or a request, and processing that request.

**Number 1: Communication style**

the most fundamental difference between EDA and microservices: communication style. EDA typically uses asynchronous communication between services, whereas microservices typically rely on synchronous communication using REST. EDA can occasionally use synchronous calls for things like retrieving data it doesn’t have access to, and microservices can use asynchronous communication when commands don’t require a response. But those are exceptions rather than the rule.

## Event-driven architecture superpowers

- **Maintainability**  
  Services in EDA are highly decoupled, making them fairly independent and therefore easier to maintain.

- **Performance**  
  Because EDA mostly uses asynchronous communication and can multitask, it’s very fast.

- **Evolvability**  
  EDA services always trigger derived events, onto which we can easily add functionality. This makes EDA highly evolvable.

- **Fault tolerance**  
  Because services are highly decoupled in EDA, if one service goes down, it doesn’t bring down other services in the workflow.

- **Scalability**  
  Event-driven architectures are highly scalable because of asynchronous processing and service decoupling. Each service can scale independently of others, with the event channels acting as pressure release valves if bottlenecks occur.

## Event-driven architecture kryptonite

- **Testability**  
  It’s really hard to test asynchronous processing and parallel tasks, making testability a weakness in EDA.

- **Synchronous calls**  
  If you have lots of synchronous calls between services and workflows that require synchronously dependent services, EDA is not for you.

- **Complexity**  
  EDA is highly complex because it typically uses asynchronous communication and parallel event processing, and because of its varied database topologies and their trade-offs.

- **Databases**  
  Regardless of the database topology you choose, services are coupled: either to the database or to each other. There are not a lot of good trade-offs here.

## Bullet Points

- An event is something that happens in the system. Events are the fundamental way services communicate with each other in EDA.

- Events are not the same thing as messages—events broadcast some action a service just performed to other services in the system, whereas messages are commands or requests directed to a single service.

- An initiating event originates from a customer or end user and kicks off a business process.

- A derived event is generated by a service in response to an initiating event.

- Any action a service performs should trigger a derived event to provide architectural extensibility—the ability to extend the system to add new functionality.

- EDA is fast because it generally uses asynchronous (async) communication—services don’t wait for a response or acknowledgment from other services when sending them information.

- Asynchronous communication is sometimes called fire-and-forget.

- Architects usually use a dotted line to represent async communication between services and a solid line to represent sync communication.

- Unlike microservices, event-driven architecture can use a variety of database topologies:
  - With the monolithic database topology, all services share a single database.
  - With the domain-partitioned databases topology, each domain in the system has its own database, shared by all of the services within that domain.
  - In the database-per-service pattern, each service has its own database in a bounded context.

- Event-driven architecture and microservices are very different architectural styles:
  - EDA relies mostly on asynchronous communication between services, whereas microservices typically rely on synchronous communication using REST.
  - EDA is built on event processing—processing things that have already happened. A microservices architecture is built on request processing—processing a command or request about something that needs to happen.
  - Microservices are fine-grained and single-purpose, whereas services in EDA can be any size.
  - Microservices requires each service to own its own data, whereas in EDA services can (and usually do) share data.

- You can combine microservices and EDA to create a hybrid architecture called event-driven microservices.

- EDA is very complex because it uses asynchronous communication and parallel event processing, and has varied database topologies.

- It’s really hard to test asynchronous processing and parallel tasks, making testability a weakness in EDA.

- Derived events provide hooks to add functionality, making EDA highly evolvable.

- EDA is highly scalable because of asynchronous processing and service decoupling.


