
# CHAPTER 1 Introduction

### ==**Architecture is about the important stuff…whatever that is.**==

the role of software architect embodies a massive amount and scope of responsibility that continues to expand. A decade ago, software architects dealt only with the purely technical aspects of architecture, like modularity, components, and patterns. Since then, because of new architectural styles that leverage a wider swath of capabilities (like microservices), the role of software architect has expanded.

![[Pasted image 20250429114224.png]]

Third, software architecture is a constantly moving target because of the rapidly evolving software development ecosystem. Any definition cast today will be hopelessly outdated in a few years.

Fourth, much of the material about software architecture has only historical relevance. Readers of the Wikipedia page won’t fail to notice the bewildering array of acronyms and cross-references to an entire universe of knowledge. Yet, many of these acronyms represent outdated or failed attempts. Even solutions that were perfectly valid a few years ago cannot work now because the context has changed.

Software architects must make decisions within this constantly changing ecosystem. Because everything changes, including foundations upon which we make decisions, architects should reexamine some core axioms that informed earlier writing about software architecture.

## Defining Software Architecture

definition, software architecture consists of the structure of the system (denoted as the heavy black lines supporting the architecture), combined with architecture characteristics (“-ilities”) the system must support, architecture decisions, and finally design principles.

![[Pasted image 20250429114534.png]]

**==The structure of the system, refers to the type of architecture style (or styles) the system is implemented in (such as microservices, layered, or microkernel).==** Describing an architecture solely by the structure does not wholly elucidate an architecture. For example, suppose an architect is asked to describe an architecture, and that architect responds “it’s a microservices architecture.” Here, the architect is only talking about the structure of the system, but not the architecture of the system. Knowledge of the architecture characteristics, architecture decisions, and design principles is also needed to fully understand the architecture of the system

![[Pasted image 20250429114646.png]]

Architecture characteristics are another dimension of defining software architecture. The architecture characteristics define the success criteria of a system, which is generally orthogonal to the functionality of the system 

![[Pasted image 20250429114817.png]]

The next factor that defines software architecture is architecture decisions. **==Architecture decisions define the rules for how a system should be constructed==**. For example, an architect might make an architecture decision that only the business and services layers within a layered architecture can access the database, restricting the presentation layer from making direct database calls. **==Architecture decisions form the constraints of the system and direct the development teams on what is and what isn’t allowed==**

![[Pasted image 20250429114946.png]]

If a particular architecture decision cannot be implemented in one part of the system due to some condition or other constraint, that decision (or rule) can be broken through something called a variance

The last factor in the definition of architecture is design principles. **==A design principle differs from an architecture decision in that a design principle is a guideline rather than a hard-and-fast rule.==** For example, the design principle illustrated in Figure 1-6 states that the development teams should leverage asynchronous messaging between services within a microservices architecture to increase performance. An architecture decision (rule) could never cover every condition and option for communication between services, so a design principle can be used to provide guidance for the preferred method (in this case, asynchronous messaging) to allow the developer to choose a more appropriate communication protocol (such as REST or gRPC) given a specific circumstance.

![[Pasted image 20250429115154.png]]

## Expectations of an Architect

There are eight core expectations placed on a software architect

• Make architecture decisions
• Continually analyze the architecture
• Keep current with latest trends
• Ensure compliance with decisions
• Diverse exposure and experience
• Have business domain knowledge
• Possess interpersonal skills
• Understand and navigate politics

### Make architecture decisions

> An architect is expected to define the architecture decisions and design principles used to guide technology decisions within the team, the department, or across the enterprise

An architect should guide rather than specify technology choices The key to making effective architectural decisions is asking whether the architecture decision is helping to guide teams in making the right technical choice or whether the architecture decision makes the technical choice for them.

### Continually Analyze the Architecture

> An architect is expected to continually analyze the architecture and current technology environment and then recommend solutions for improvement. 

This expectation of an architect refers to architecture vitality, which assesses how viable the architecture that was defined three or more years ago is today, given changes in both business and technology.

### Keep Current with Latest Trends

> An architect is expected to ensure compliance with architecture decisions and design principles.

The decisions an architect makes tend to be long-lasting and difficult to change. Understanding and following key trends helps the architect prepare for the future and make the correct decision.

### Ensure Compliance with Decisions

> An architect is expected to ensure compliance with architecture decisions and design principles.

Ensuring compliance means that the architect is continually verifying that development teams are following the architecture decisions and design principles defined, documented, and communicated by the architect.

### Diverse Exposure and Experience

> An architect is expected to have exposure to multiple and diverse technologies, frameworks, platforms, and environments.

This expectation does not mean an architect must be an expert in every framework, platform, and language, but rather that an architect must at least be familiar with a variety of technologies.

One of the best ways of mastering this expectation is for the architect to stretch their comfort zone. Focusing only on a single technology or platform is a safe haven. An effective software architect should be aggressive in seeking out opportunities to gain experience in multiple languages, platforms, and technologies.

### Have Business Domain Knowledge

> An architect is expected to have a certain level of business domain expertise.

Effective software architects understand not only technology but also the business domain of a problem space. Without business domain knowledge, it is difficult to understand the business problem, goals, and requirements, making it difficult to design an effective architecture to meet the requirements of the business.

The most successful architects we know are those who have broad, hands-on technical knowledge coupled with a strong knowledge of a particular domain.

### Possess Interpersonal Skills

> An architect is expected to possess exceptional interpersonal skills, including teamwork, facilitation, and leadership.

### Understand and Navigate Politics

> An architect is expected to understand the political climate of the enterprise and be able to navigate the politics.

The main point is that almost every decision an architect makes will be challenged. Architectural decisions will be challenged by product owners, project managers, and business stakeholders due to increased costs or increased effort (time) involved. Architectural decisions will also be challenged by developers who feel their approach is better.

## Laws of Software Architecture

### ==**Everything in software architecture is a trade-off.**==

### ==**If an architect thinks they have discovered something that isn’t a trade-off, more likely they just haven’t identified the trade-off yet.**==

### ==**Why is more important than how.**==


# CHAPTER 2 Architectural Thinking

There are four main aspects of thinking like an architect. 
- First, it’s understanding the difference between architecture and design and knowing how to collaborate with development teams to make architecture work. 
- Second, it’s about having a wide breadth of technical knowledge while still maintaining a certain level of technical depth, allowing the architect to see solutions and possibilities that others do not see. 
- Third, it’s about understanding, analyzing, and reconciling trade-offs between various solutions and technologies. 
- Finally, it’s about understanding the importance of business drivers and how they translate to architectural concerns.

## Architecture Versus Design

The difference between architecture and design is often a confusing one. As shown in the diagram, an architect is responsible for things like analyzing business requirements to extract and define the architectural characteristics (“-ilities”), selecting which architecture patterns and styles would fit the problem domain, and creating components (the building blocks of the system). The artifacts created from these activities are then handed off to the development team, which is responsible for creating class diagrams for each component, creating user interface screens, and developing and testing source code.

![[Pasted image 20250501133640.png]]

Decisions an architect makes sometimes never make it to the development teams, and decisions development teams make that change the architecture rarely get back to the architect. **==In this model the architect is disconnected from the development teams, and as such the architecture rarely provides what it was originally set out to do.==**

To make architecture work, both the physical and virtual barriers that exist between architects and developers must be broken down, thus forming a strong bidirectional relationship between architects and development teams.

![[Pasted image 20250501133739.png]]

A tight collaboration between the architect and the development team is essential for the success of any software project.

## Technical Breadth

![[Pasted image 20250501134033.png]]

Stuff you know includes the technologies, frameworks, languages, and tools a technologist uses on a daily basis to perform their job, such as knowing Java as a Java programmer. Stuff you know you don’t know includes those things a technologist knows a little about or has heard of but has little or no expertise in. A good example of this level of knowledge is the Clojure programming language. Most technologists have heard of Clojure and know it’s a programming language based on Lisp, but they can’t code in the language. S**==tuff you don’t know you don’t know is the largest part of the knowledge triangle and includes the entire host of technologies, tools, frameworks, and languages that would be the perfect solution to a problem a technologist is trying to solve, but the technologist doesn’t even know those things exist.==**

A developer’s early career focuses on expanding the top of the pyramid, to build experience and expertise. This is the ideal focus early on, because developers need more perspective, working knowledge, and hands-on experience. Expanding the top incidentally expands the middle section; as developers encounter more technologies and related artifacts, it adds to their stock of stuff you know you don’t know

![[Pasted image 20250501134217.png]]

the top of the pyramid is beneficial because expertise is valued. However, the stuff you know is also the stuff you must maintain—nothing is static in the software world. If a developer becomes an expert in Ruby on Rails, that expertise won’t last if they ignore Ruby on Rails for a year or two. The things at the top of the pyramid require time investment to maintain expertise. **==Ultimately, the size of the top of an individual’s pyramid is their technical depth.==**

A large part of the value of an architect is a broad understanding of technology and how to use it to solve particular problems.

The most important parts of the pyramid for architects are the top and middle sections; how far the middle section penetrates into the bottom section represents an architect’s technical breadth

![[Pasted image 20250501134418.png]]

**==for an architect, the wise course of action is to sacrifice some hard-won expertise and use that time to broaden their portfolio==**

![[Pasted image 20250501134558.png]]

Developers spend their whole careers honing expertise, and transitioning to the architect role means a shift in that perspective, which many individuals find difficult. This in turn leads to two common dysfunctions: first, an architect tries to maintain expertise in a wide variety of areas, succeeding in none of them and working themselves ragged in the process. Second, it manifests as stale expertise —the mistaken sensation that your outdated information is still cutting edge.

## Analyzing Trade-Offs

Thinking like an architect is all about seeing trade-offs in every solution, technical or otherwise, and analyzing those trade-offs to determine what is the best solution. To quote Mark (one of your authors):

> ***Architecture is the stuff you can’t Google.***


Everyone’s environment, situation, and problem is different, hence why architecture is so hard. To quote Neal (another one of your authors):

>***There are no right or wrong answers in architecture—only trade-offs.***

Programmers know the benefits of everything and the trade-offs of nothing. Architects need to understand both
Thinking architecturally is looking at the benefits of a given solution, but also analyzing the negatives, or trade-offs, associated with a solution.

## Balancing Architecture and Hands-On Coding

One of the difficult tasks an architect faces is how to balance hands-on coding with software architecture. We firmly believe that every architect should code and be able to maintain a certain level of technical depth

**==The first tip in striving for a balance between hands-on coding and being a software architect is avoiding the bottleneck trap. The bottleneck trap occurs when the architect has taken ownership of code within the critical path of a project (usually the underlying framework code) and becomes a bottleneck to the team. This happens because the architect is not a full-time developer and therefore must balance between playing the developer role (writing and testing source code) and the architect role (drawing diagrams, attending meetings, and well, attending more meetings).==**

One way to avoid the bottleneck trap as an effective software architect is to delegate the critical path and framework code to others on the development team and then focus on coding a piece of business functionality (a service or a screen) one to three iterations down the road. Three positive things happen by doing this. First, the architect is gaining hands-on experience writing production code while no longer becoming a bottleneck on the team. Second, the critical path and framework code is distributed to the development team (where it belongs), giving them ownership and a better understanding of the harder parts of the system. Third, and perhaps most important, the architect is writing the same business-related source code as the development team and is therefore better able to identify with the development team in terms of the pain they might be going through with processes, procedures, and the development environment

here are four basic ways an architect can still remain hands-on at  work without having to *“practice coding from home”*

- The first way is to do frequent proof-of-concepts or POCs. This practice not only requires the architect to write source code, but it also helps validate an architecture decision by taking the implementation details into account
- Another way an architect can remain hands-on is to tackle some of the technical debt stories or architecture stories, freeing the development team up to work on the critical functional user stories. These stories are usually low priority, so if the architect does not have the chance to complete a technical debt or architecture story within a given iteration, it’s not the end of the world and generally does not impact the success of the iteration
- A final technique to remain hands-on as an architect is to do frequent code reviews. While the architect is not actually writing code, at least they are involved in the source code. Further, doing code reviews has the added benefits of being able to ensure compliance with the architecture and to seek out mentoring and coaching opportunities on the team.

# CHAPTER 3 Modularity

> 95% of the words about software architecture are spent extolling the benefits of “modularity” and that little, if anything, is said about how to achieve it.

Different platforms offer different reuse mechanisms for code, but all support some way of grouping related code together into modules.

Understanding modularity and its many incarnations in the development platform of choice is critical for architects. Many of the tools we have to analyze architecture (such as metrics, fitness functions, and visualizations) rely on these modularity concepts. Modularity is an organizing principle.

software systems model complex systems, which tend toward entropy (or disorder). Energy must be added to a physical system to preserve order. The same is true for software systems: architects must constantly expend energy to ensure good structural soundness, which won’t happen by accident.

## Definition

use modularity to describe a logical grouping of related code, which could be a group of classes in an object-oriented language or functions in a structured or functional language

Languages now feature a wide variety of packaging mechanisms, making a developer’s chore of choosing between them difficult.

**==Architects must be aware of how developers package things because it has important implications in architecture. For example, if several packages are tightly coupled together, reusing one of them for related work becomes more difficult==**

Developers often need precise, fully qualified names for software assets to separate different software assets (components, classes, and so on) from each other.

## Measuring Modularity

### Cohesion

Cohesion refers to what extent the parts of a module should be contained within the same module. In other words, **==it is a measure of how related the parts are to one another==**. Ideally, a cohesive module is one where all the parts should be packaged together, because breaking them into smaller pieces would require coupling the parts together via calls between modules to achieve useful results.

> Attempting to divide a cohesive module would only result in increased coupling and decreased readability.


- **Functional Cohesion**  
    Every part of the module is related to the other, and the module contains everything essential to function.
    
- **Sequential Cohesion**  
    Two modules interact, where one outputs data that becomes the input for the other.
    
- **Communicational Cohesion**  
    Two modules form a communication chain, where each operates on information and/or contributes to some output.  
    _Example:_ Add a record to the database and generate an email based on that information.
    
- **Procedural Cohesion**  
    Two modules must execute code in a particular order.
    
- **Temporal Cohesion**  
    Modules are related based on timing dependencies.  
    _Example:_ Initializing seemingly unrelated tasks during system startup.
    
- **Logical Cohesion**  
    The data within modules is related logically but not functionally.  
    _Example:_ A module that converts information from text, serialized objects, or streams.  
    Commonly seen in `StringUtils` packages in Java.
    
- **Coincidental Cohesion**  
    Elements in a module are not related other than being in the same source file; this represents the most negative form of cohesion.
    

### Coupling

Afferent coupling measures the number of incoming connections to a code artifact (component, class, function, and so on). Efferent coupling measures the outgoing connections to other code artifacts.

### Abstractness, Instability, and Distance from the Main Sequence

While the raw value of component coupling has value to architects, several other derived metrics allow a deeper evaluation.

Abstractness is the ratio of abstract artifacts (abstract classes, interfaces, and so on) to concrete artifacts (implementation). It represents a measure of abstractness versus implementation

The instability metric determines the volatility of a code base. A code base that exhibits high degrees of instability breaks more easily when changed because of high coupling

# CHAPTER 4 Architecture Characteristics Defined

Architects may collaborate on defining the domain or business requirements, but one key responsibility entails defining, discovering, and otherwise analyzing all the things the software must do that isn’t directly related to the domain functionality: architectural characteristics

**==An architecture characteristic meets three criteria:**==
==**• Specifies a nondomain design consideration**==
==**• Influences some structural aspect of the design**==
==**• Is critical or important to application success==**

![[Pasted image 20250502142754.png]]

 **Specifies a nondomain design consideration**

When designing an application, the requirements specify what the application should do; architecture characteristics specify operational and design criteria for success, concerning how to implement the requirements and why certain choices were made.

 **Influences some structural aspect of the design**

The primary reason architects try to describe architecture characteristics on projects concerns design considerations: does this architecture characteristic require special structural consideration to succeed?

 **Critical or important to application success**

Applications could support a huge number of architecture characteristics…but shouldn’t. Support for each architecture characteristic adds complexity to the design. Thus, a critical job for architects lies in choosing the fewest architecture characteristics rather than the most possible.

## Architectural Characteristics (Partially) Listed

Architecture characteristics exist along a broad spectrum of the software system, ranging from low-level code characteristics, such as modularity, to sophisticated operational concerns, such as scalability and elasticity.

Despite the volume and scale, architects commonly separate architecture characteristics into broad categories

### Operational Architecture Characteristics

| **Term**        | **Definition**                                                                                                                                                   |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Availability** | How long the system will need to be available (if 24/7, steps need to be in place to allow the system to be up and running quickly in case of any failure).      |
| **Continuity**   | Disaster recovery capability.                                                                                                                                    |
| **Performance**  | Includes stress testing, peak analysis, analysis of the frequency of functions used, capacity required, and response times. Performance acceptance sometimes requires an exercise of its own, taking months to complete. |
| **Recoverability** | Business continuity requirements (e.g., in case of a disaster, how quickly is the system required to be online again?). This will affect the backup strategy and requirements for duplicated hardware. |
| **Reliability / Safety** | Assess if the system needs to be fail-safe, or if it is mission critical in a way that affects lives. If it fails, will it cost the company large sums of money? |
| **Robustness**   | Ability to handle error and boundary conditions while running if the internet connection goes down or if there’s a power outage or hardware failure.             |
| **Scalability**  | Ability for the system to perform and operate as the number of users or requests increases.                                                                      |

### Structural Architecture Characteristics

Architects must concern themselves with code structure. In many cases, the architect has sole or shared responsibility for code quality concerns, such as good modularity, controlled coupling between components, readable code, and a host of other internal quality assessments

| **Term**             | **Definition**                                                                                                                                                           |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Configurability**  | Ability for the end users to easily change aspects of the software’s configuration (through usable interfaces).                                                          |
| **Extensibility**    | How important it is to plug new pieces of functionality in.                                                                                                               |
| **Installability**   | Ease of system installation on all necessary platforms.                                                                                                                   |
| **Leverageability / Reuse** | Ability to leverage common components across multiple products.                                                                                             |
| **Localization**     | Support for multiple languages on entry/query screens in data fields; on reports, multibyte character requirements and units of measure or currencies.                  |
| **Maintainability**  | How easy it is to apply changes and enhance the system?                                                                                                                   |
| **Portability**      | Does the system need to run on more than one platform? (For example, does the frontend need to run against Oracle as well as SAP DB?)                                    |
| **Supportability**   | What level of technical support is needed by the application? What level of logging and other facilities are required to debug errors in the system?                    |
| **Upgradeability**   | Ability to easily/quickly upgrade from a previous version of this application/solution to a newer version on servers and clients.                                        |

### Cross-Cutting Architecture Characteristics

While many architecture characteristics fall into easily recognizable categories, many fall outside or defy categorization yet form important design constraints and considerations.

| **Term**                | **Definition**                                                                                                                                                                      |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Accessibility**        | Access to all your users, including those with disabilities like colorblindness or hearing loss.                                                                                   |
| **Archivability**        | Will the data need to be archived or deleted after a period of time? (e.g., customer accounts deleted after three months or archived to a secondary database for future access). |
| **Authentication**       | Security requirements to ensure users are who they say they are.                                                                                                                   |
| **Authorization**        | Security requirements to ensure users can access only certain functions within the application (by use case, subsystem, webpage, business rule, field level, etc.).              |
| **Legal**                | What legislative constraints is the system operating in (data protection, Sarbanes Oxley, GDPR, etc.)? Any regulations on how the application is to be built or deployed?         |
| **Privacy**              | Ability to hide transactions from internal company employees (e.g., encrypted so even DBAs and network architects cannot see them).                                                |
| **Security**             | Does the data need to be encrypted in the database? Encrypted for network communication? What type of authentication is required for remote access?                              |
| **Supportability**       | What level of technical support is needed by the application? What level of logging and other facilities are required to debug errors in the system?                             |
| **Usability / Achievability** | Level of training required for users to achieve their goals with the application. Usability requirements need to be treated as seriously as other architectural issues.   |

## Trade-Offs and Least Worst Architecture

Applications can only support a few of the architecture characteristics we’ve listed for a variety of reasons. First, each of the supported characteristics requires design effort and perhaps structural support. Second, the bigger problem lies with the fact that each architecture characteristic often has an impact on others

**==architects rarely encounter the situation where they are able to design a system and maximize every single architecture characteristic. More often, the decisions come down to trade-offs between several competing concerns==**.

> ==**Never shoot for the best architecture, but rather the least worst architecture.==**

Too many architecture characteristics leads to generic solutions that are trying to solve every business problem, and those architectures rarely work because the design becomes unwieldy.

This suggests that architects should strive to design architecture to be as iterative as possible. If you can make changes to the architecture more easily, you can stress less about discovering the exact correct thing in the first attempt. One of the most important lessons of Agile software development is the value of iteration; this holds true at all levels of software development, including architecture.

# CHAPTER 5 Identifying Architectural Characteristics

Identifying the driving architectural characteristics is one of the first steps in creating an architecture or determining the validity of an existing architecture. Identifying the correct architectural characteristics (“-ilities”) for a given problem or application requires an architect to not only understand the domain problem, but also collaborate with the problem domain stakeholders to determine what is truly important from a domain perspective.

## Extracting Architecture Characteristics from Domain Concerns

An architect must be able to translate domain concerns to identify the right architectural characteristics.
Understanding the key domain goals and domain situation allows an architect to translate those domain concerns to “-ilities,” which then forms the basis for correct and justifiable architecture decisions

**==A common anti-pattern in architecture entails trying to design a generic architecture, one that supports all the architecture characteristics. Each architecture characteristic the architecture supports complicates the overall system design; supporting too many architecture characteristics leads to greater and greater complexity before the architect and developers have even started addressing the problem domain, the original motivation for writing the software. Don’t obsess over the number of characteristics, but rather the motivation to keep design simple.==**

Rarely will all stakeholders agree on the priority of each and every characteristic. A better approach is to have the domain stakeholders select the top three most important characteristics from the final list (in any order). Not only is this much easier to gain consensus on, but it also fosters discussions about what is most important and helps the architect analyze trade-offs when making vital architecture decisions.

Most architecture characteristics come from listening to key domain stakeholders and collaborating with them to determine what is important from a domain perspective. While this may seem like a straightforward activity, the problem is that architects and domain stakeholders speak different languages. Architects talk about scalability, interoperability, fault tolerance, learnability, and availability. Domain stakeholders talk about mergers and acquisitions, user satisfaction, time to market, and competitive advantage.

**==One important thing to note is that agility does not equal time to market. Rather, it is agility + testability + deployability. This is a trap many architects fall into when translating domain concerns==**

### Extracting Architecture Characteristics from Requirements

Some architecture characteristics come from explicit statements in requirements documents.

# CHAPTER 6 Measuring and Governing Architecture Characteristics

## Measuring Architecture Characteristics

Several common problems exist around the definition of architecture characteristics in organizations:

They aren’t physics  
Many architecture characteristics in common usage have vague meanings. For example, how does an architect design for agility or deployability? The industry has wildly differing perspectives on common terms, sometimes driven by legitimate differing contexts, and sometimes accidental.

Wildly varying definitions  
Even within the same organization, different departments may disagree on the definition of critical features such as performance. Until developers, architecture, and operations can unify on a common definition, a proper conversation is difficult.

Too composite  
Many desirable architecture characteristics comprise many others at a smaller scale. For example, developers can decompose agility into characteristics such as modularity, deployability, and testability.

### Operational Measures

Many architecture characteristics have obvious direct measurements, such as performance or scalability. However, even these offer many nuanced interpretations, depending on the team’s goals.

High-level teams don’t just establish hard performance numbers; they base their definitions on statistical analysis.
The kinds of characteristics that teams can now measure are evolving rapidly, in conjunction with tools and nuanced understanding

### Structural Measures

Some objective measures are not so obvious as performance. What about internal structural characteristics, such as well-defined modularity? Unfortunately, comprehensive metrics for internal code quality don’t yet exist. However, some metrics and common tools do allow architects to address some critical aspects of code structure, albeit along narrow dimensions.
An obvious measurable aspect of code is complexity, defined by the cyclometric complexity metric.

Architects and developers universally agree that overly complex code represents a code smell; it harms virtually every one of the desirable characteristics of code bases: modularity, testability, deployability, and so on. Yet if teams don’t keep an eye on gradually growing complexity, that complexity will dominate the code base.

### Process Measures

Some architecture characteristics intersect with software development processes. For example, agility often appears as a desirable feature. However, it is a composite architecture characteristic that architects may decompose into features such as testability, and deployability.

Testability is measurable through code coverage tools for virtually all platforms that assess the completeness of testing. Like all software checks, it cannot replace thinking and intent.

However, testability is clearly an objectively measurable characteristic. Similarly, teams can measure deployability via a variety of metrics: percentage of successful to failed deployments

## Governance and Fitness Functions

### Governing Architecture Characteristics
 
 Governance, derived from the Greek word ``kubernan`` (to steer) is an important responsibility of the architect role. As the name implies, the scope of architecture governance covers any aspect of the software development process that architects (including roles like enterprise architects) want to exert an influence upon

Fortunately, increasingly sophisticated solutions exist to relieve this problem from architects, a good example of the incremental growth in capabilities within the software development ecosystem.

**Architecture fitness function**

> **Any mechanism that provides an objective integrity assessment of some architecture characteristic or combination of architecture characteristics**

Fitness functions are not some new framework for architects to download, but rather a new perspective on many existing tools. Notice in the definition the phrase any mechanism—the verification techniques for architecture characteristics are as varied as the characteristics are. Fitness functions overlap many existing verification mechanisms, depending on the way they are used: as metrics, monitors, unit testing libraries, chaos engineering,

![[Pasted image 20250503150833.png]]

#### Cyclic dependencies

Modularity is an implicit architecture characteristic that most architects care about, because poorly maintained modularity harms the structure of a code base; thus, architects should place a high priority on maintaining good modularity.

![[Pasted image 20250503150901.png]]

each component references something in the others. Having a network of components such as this damages modularity because a developer cannot reuse a single component without also bringing the others along. And, of course, if the other components are coupled to other components, the architecture tends more and more toward the Big Ball of Mud anti-pattern. How can architects govern this behavior without constantly looking over the shoulders of trigger-happy developers? Code reviews help but happen too late in the development cycle to be effective. If an architect allows a development team to rampantly import across the code base for a week until the code review, serious damage has already occurred in the code base. The solution to this problem is to write a fitness function to look after cycles

```java
public class CycleTest {

    private JDepend jdepend;

    @BeforeEach
    void init() {
        jdepend = new JDepend();
        jdepend.addDirectory("/path/to/project/persistence/classes");
        jdepend.addDirectory("/path/to/project/web/classes");
        jdepend.addDirectory("/path/to/project/thirdpartyjars");
    }

    @Test
    void testAllPackages() {
        Collection packages = jdepend.analyze();
        assertEquals("Cycles exist", false, jdepend.containsCycles());
    }
}
```

```java
@Test
void AllPackages() {
    double ideal = 0.0;
    double tolerance = 0.5; // project-dependent
    Collection packages = jdepend.analyze();
    Iterator iter = packages.iterator();

    while (iter.hasNext()) {
        JavaPackage p = (JavaPackage) iter.next();
        assertEquals("Distance exceeded: " + p.getName(),
                     ideal, p.distance(), tolerance);
    }
}
```

In the code, the architect uses ``JDepend`` to establish a threshold for acceptable values, failing the test if a class falls outside the range.

This is both an example of an objective measure for an architecture characteristic and the importance of collaboration between developers and architects when designing and implementing fitness functions. The intent is not for a group of architects to ascend to an ivory tower and develop esoteric fitness functions that developers cannot understand.

> **Architects must ensure that developers understand the purpose of the fitness function before imposing it on them.**

One such tool is ``ArchUnit``, a Java testing framework inspired by and using several parts of the ``JUnit`` ecosystem. ``ArchUnit`` provides a variety of predefined governance rules codified as unit tests and allows architects to write specific tests that address modularity.

![[Pasted image 20250503151146.png]]

how can the architect ensure that developers will respect those layers? Some developers may not understand the importance of the patterns, while others may adopt a “better to ask forgiveness than permission” attitude because of some overriding local concern such as performance. But allowing implementers to erode the reasons for the architecture hurts the long-term health of the architecture.

```java
layeredArchitecture()
    .layer("Controller").definedBy("..controller..")
    .layer("Service").definedBy("..service..")
    .layer("Persistence").definedBy("..persistence..")
    
    .whereLayer("Controller").mayNotBeAccessedByAnyLayer()
    .whereLayer("Service").mayOnlyBeAccessedByLayers("Controller")
    .whereLayer("Persistence").mayOnlyBeAccessedByLayers("Service");

```

# CHAPTER 7 Scope of Architecture Characteristics

When evaluating many operational architecture characteristics, an architect must consider dependent components outside the code base that will impact those characteristics. Thus, architects need another method to measure these kinds of dependencies. That lead the Building Evolutionary Architectures authors to define the term architecture quantum. To understand the architecture quantum definition, we must preview one key metric here, connascence.

## Coupling and Connascence

**Connascence**
>Two components are connascent if a change in one would require the other to be modified in order to maintain the overall correctness of the system

To define the architecture quantum, we needed a measure of how components are “wired” together, which corresponds to the connascence concept. For example, if two services in a microservices architecture share the same class definition of some class, like address, we say they are statically connascent with each other—changing the shared class requires changes to both services.

For dynamic connascence, we define two types: synchronous and asynchronous. Synchronous calls between two distributed services have the caller wait for the response from the callee. On the other hand, asynchronous calls allow fire-and-forget semantics in event-driven architectures, allowing two different services to differ in operational architecture

## Architectural Quanta and Granularity

Component-level coupling isn’t the only thing that binds software together. Many business concepts semantically bind parts of the system together, creating functional cohesion. To successfully design, analyze, and evolve software, developers must consider all the coupling points that could break.

**Architecture quantum**
An independently deployable artifact with high functional cohesion and synchronous connascence

- Independently deployable
- High functional cohesion
- Synchronous connascence

## CHAPTER 8 Component-Based Thinking

Developers physically package modules in different ways, sometimes depending on their development platform. We call physical packaging of modules components

## Component Scope

Components offer a language-specific mechanism to group artifacts together, often nesting them to create stratification the simplest component wraps code at a higher level of modularity than classes (or functions, in non object oriented languages). This simple wrapper is often called a library, which tends to run in the same memory address as the calling code and communicate via language function call mechanisms. Libraries are usually compile-time dependencies

![[Pasted image 20250503182513.png]]

Nothing requires an architect to use components—it just so happens that it’s often useful to have a higher level of modularity than the lowest level offered by the language. For example, in microservices architectures, simplicity is one of the architectural principles. Thus, a service may consist of enough code to warrant components or may be simple enough to just contain a small bit of code

Components form the fundamental modular building block in architecture, making  them a critical consideration for architects. In fact, one of the primary decisions an architect must make concerns the top-level partitioning of components in the architecture.

## Architect Role

architecture is independent from the development process. The primary exception to this rule entails the engineering practices pioneered in the various flavors of Agile software development, particularly in the areas of deployment and automating governance. However, in general, software architecture exists separate from the process. Thus, architects ultimately don’t care where requirements originate: a formal Joint Application Design (JAD) process, lengthy waterfall-style analysis and design, Agile story cards…or any hybrid variation of those.

Generally the component is the lowest level of the software system an architect interacts directly with, with the exception of many of the code quality metrics Components consist of classes or functions (depending on the implementation platform), whose design falls under the responsibility of tech leads or developers. It’s not that architects shouldn’t involve themselves in class design (particularly when discovering or applying design patterns), but they should avoid micromanaging each decision from top to bottom in the system. If architects never allow other roles to make decisions of consequence, the organization will struggle with empowering the next generation of architects

###  Architecture Partitioning

components represent a general containership mechanism, an architect can build any type of partitioning they want. Several common styles exist, with different sets of tradeoffs.

![[Pasted image 20250503182847.png]]

![[Pasted image 20250503182854.png]]

the architect has partitioned the functionality of the system into technical capabilities: presentation, business rules, services, persistence, and so on. This way of organizing a code base certainly makes sense. All the persistence code resides in one layer in the architecture, making it easy for developers to find persistence-related code. Even though the basic concept of layered architecture predates it by decades, the Model-View-Controller design pattern matches with this architectural pattern, making it easy for developers to understand. Thus, it is often the default architecture in many organizations.

An interesting side effect of the predominance of the layered architecture relates to how companies seat different project roles. When using a layered architecture, it makes some sense to have all the backend developers sit together in one department, the DBAs in another, the presentation team in another, and so on

domain partitioning, inspired by the Eric Evan book Domain-Driven Design, which is a modeling technique for decomposing complex software systems. In DDD, the architect identifies domains or workflows independent and decoupled from each other. The microservices architecture style (discussed in Chapter 17) is based on this philosophy. In a modular monolith, the architect partitions the architecture around domains or workflows rather than technical capabilities. As components often nest within one another, each of the components in Figure 8-4 in the domain partitioning (for example, Catalog‐ Checkout) may use a persistence library and have a separate layer for business rules, but the top-level partitioning revolves around domains

**==One of the fundamental distinctions between different architecture patterns is what type of top-level partitioning each supports, which we cover for each individual pattern. It also has a huge impact on how an architect decides how to initially identify components==**—does the architect want to partition things technically or by domain?

Architects using technical partitioning organize the components of the system by technical capabilities: presentation, business rules, persistence, and so on. Thus, one of the organizing principles of this architecture is separation of technical concerns. This in turn creates useful levels of decoupling: if the service layer is only connected to the persistence layer below and business rules layer above, then changes in persistence will only potentially affect those layers. This style of partitioning provides a decoupling technique, reducing rippling side effects on dependent components.

The separation enforced by technical partitioning enables developers to find certain categories of the code base quickly, as it is organized by capabilities. However, most realistic software systems require workflows that cut across technical capabilities.

## Component Identification Flow

Component identification works best as an iterative process, producing candidates and refinements through feedback

![[Pasted image 20250503183358.png]]

This cycle describes a generic architecture exposition cycle. Certain specialized domains may insert other steps in this process or change it altogether. For example, in some domains, some code must undergo security or auditing steps in this process.

### Identifying Initial Components

Before any code exists for a software project, the architect must somehow determine what top-level components to begin with, based on what type of top-level partitioning they choose. Outside that, an architect has the freedom to make up whatever components they want, then map domain functionality to them to see where behavior should reside. While this may sound arbitrary, it’s hard to start with anything more concrete if an architect designs a system from scratch

### Assign Requirements to Components

Once an architect has identified initial components, the next step aligns requirements (or user stories) to those components to see how well they fit. This may entail creating new components, consolidating existing ones, or breaking components apart because they have too much responsibility. This mapping doesn’t have to be exact— the architect is attempting to find a good coarse-grained substrate to allow further design and refinement by architects, tech leads, and/or developers

### Analyze Roles and Responsibilities

When assigning stories to components, the architect also looks at the roles and responsibilities elucidated during the requirements to make sure that the granularity matches. Thinking about both the roles and behaviors the application must support allows the architect to align the component and domain granularity. One of the greatest challenges for architects entails discovering the correct granularity for components, which encourages the iterative approach described here.

### Analyze Architecture Characteristics

When assigning requirements to components, the architect should also look at the architecture characteristics discovered earlier in order to think about how they might impact component division and granularity. For example, while two parts of a system might deal with user input, the part that deals with hundreds of concurrent users will need different architecture characteristics than another part that needs to support only a few. Thus, while a purely functional view of component design might yield a single component to handle user interaction, analyzing the architecture characteristics will lead to a subdivision.

### Restructure Components

Feedback is critical in software design. Thus, architects must continually iterate on their component design with developers. Designing software provides all kinds of unexpected difficulties—no one can anticipate all the unknown issues that usually occur during software projects. Thus, an iterative approach to component design is key. First, it’s virtually impossible to account for all the different discoveries and edge cases that will arise that encourage redesign. Secondly, as the architecture and developers delve more deeply into building the application, they gain a more nuanced understanding of where behavior and roles should lie.

### Component Granularity

Finding the proper granularity for components is one of an architect’s most difficult tasks. Too fine-grained a component design leads to too much communication between components to achieve results. Too coarse-grained components encourage high internal coupling, which leads to difficulties in deployability and testability, as well as modularity-related negative side effects.

## Component Design

No accepted “correct” way exists to design components. Rather, a wide variety of techniques exist, all with various trade-offs. In all processes, an architect takes requirements and tries to determine what coarse-grained building blocks will make up the application. Lots of different techniques exist, all with varying trade-offs and coupled to the software development process used by the team and organization. Here, we talk about a few general ways to discover components and traps to avoid.

### Discovering Components

Architects, often in collaboration with other roles such as developers, business analysts, and subject matter experts, create an initial component design based on general knowledge of the system and how they choose to decompose it, based on technical or domain partitioning. The team goal is an initial design that partitions the problem space into coarse chunks that take into account differing architecture characteristics.

#### Entity trap

While there is no one true way to ascertain components, a common anti-pattern lurks: the entity trap. Say that an architect is working on designing components for our kata Going, Going, Gone and ends up with a design resembling Figure 8-9.

![[Pasted image 20250503183731.png]]

**==The entity trap anti-pattern arises when an architect incorrectly identifies the database relationships as workflows in the application, a correspondence that rarely manifesting the real world. Rather, this anti-pattern generally indicates lack of thought about the actual workflows of the application.==** Components created with the entity trap also tend to be too coarse-grained, offering no guidance whatsoever to the development team in terms of the packaging and overall structuring of the source code.

#### Actor/Actions approach

The actor/actions approach is a popular way that architects use to map requirements to components. In this approach, originally defined by the Rational Unified Process, architects identify actors who perform activities with the application and the actions those actors may perform. It provides a technique for discovering the typical users of the system and what kinds of things they might do with the system.

The actor/actions approach became popular in conjunction with particular software development processes, especially more formal processes that favor a significant portion of upfront design. It is still popular and works well when the requirements feature distinct roles and the kinds of actions they can perform. This style of component decomposition works well for all types of systems, monolithic or distributed.

#### Event storming

Event storming as a component discovery technique comes from domain-driven design (DDD) and shares popularity with microservices, also heavily influenced by DDD. In event storming, the architect assumes the project will use messages and/or events to communicate between the various components. To that end, the team tries to determine which events occur in the system based on requirements and identified roles, and build components around those event and message handlers.

#### Workflow approach

An alternative to event storming offers a more generic approach for architects not using DDD or messaging. The workflow approach models the components around workflows, much like event storming, but without the explicit constraints of building a message-based system. A workflow approach identifies the key roles, determines the kinds of workflows these roles engage in, and builds components around the identified activities.

None of these techniques is superior to the others; all offer a different set of tradeoffs. If a team uses a waterfall approach or other older software development processes, they might prefer the Actor/Actions approach because it is general. When using DDD and corresponding architectures like microservices, event storming matches the software development process exactly.

## Architecture Quantum Redux: Choosing Between Monolithic Versus Distributed Architectures

should the architecture be monolithic or distributed?

A monolithic architecture typically features a single deployable unit, including all functionality of the system that runs in the process, typically connected to a single database. Types of monolithic architectures include the layered and modular monolith, discussed fully in Chapter 10. A distributed architecture is the opposite—the application consists of multiple services running in their own ecosystem, communicating via networking protocols. Distributed architectures may feature finer-grained deployment models, where each service may have its own release cadence and engineering practices, based on the development team and their priorities. 

Each architecture style offers a variety of trade-offs, covered in Part II. However, the fundamental decision rests on how many quanta the architecture discovers during the design process. If the system can manage with a single quantum (in other words, one set of architecture characteristics), then a monolith architecture offers many advantages. On the other hand, differing architecture characteristics for components, as illustrated in the GGG component analysis, requires a distributed architecture to accommodate differing architecture characteristics. For example, the ``VideoStreamer`` and ``BidStreamer`` both offer read-only views of the auction to bidders. From a design standpoint, an architect would rather not deal with read-only streaming mixed with high-scale updates. Along with the aforementioned differences between bidder and auctioneer, these differing characteristics lead an architect to choose a distributed architecture. 

The ability to determine a fundamental design characteristic of architecture (monolith versus distributed) early in the design process highlights one of the advantages of using the architecture quantum as a way of analyzing architecture characteristics scope and coupling.

# CHAPTER 9 Foundations

Understanding architecture styles occupies much of the time and effort for new architects because they share importance and abundance. Architects must understand the various styles and the trade-offs encapsulated within each to make effective decisions; each architecture style embodies a well-known set of trade-offs that help an architect make the right choice for a particular business problem.

Architecture styles, sometimes called architecture patterns, describe a named relationship of components covering a variety of architecture characteristics. An architecture style name, similar to design patterns, creates a single name that acts as shorthand between experienced architects

Each name captures a wealth of understood detail, one of the purposes of design patterns. An architecture style describes the topology, assumed and default architecture characteristics, both beneficial and detrimental.

## Fundamental Patterns

Several fundamental patterns appear again and again throughout the history of software architecture because they provide a useful perspective on organizing code, deployments, or other aspects of architecture.

### Big Ball of Mud

Architects refer to the absence of any discernible architecture structure as a Big Ball of Mud, named after the eponymous anti-pattern defined in a paper released in 1997 by Brian Foote and Joseph Yoder:

>A Big Ball of Mud is a haphazardly structured, sprawling, sloppy, duct-tape-and-baling wire,
spaghetti-code jungle. These systems show unmistakable signs of unregulated growth, and repeated, expedient repair. Information is shared promiscuously among distant elements of the system, often to the point where nearly all the important information becomes global or duplicated. The overall structure of the system may never have been well defined. If it was, it may have eroded beyond recognition. Programmers with a shred of architectural sensibility shun these quagmires. Only those who are unconcerned about architecture, and, perhaps, are comfortable with the inertia of the day-to-day chore of patching the holes in these failing dikes, are content to work on such systems.

—Brian Foote and Joseph Yoder


**==In modern terms, a big ball of mud might describe a simple scripting application with event handlers wired directly to database calls, with no real internal structure==**. Many trivial applications start like this then become unwieldy as they continue to grow.

In general, architects want to avoid this type of architecture at all costs. The lack of structure makes change increasingly difficult. This type of architecture also suffers from problems in deployment, testability, scalability, and performance.

![[Pasted image 20250504104112.png]]

### Unitary Architecture

When software originated, there was only the computer, and software ran on it. Through the various eras of hardware and software evolution, the two started as a single entity, then split as the need for more sophisticated capabilities grew

Few unitary architectures exist outside embedded systems and other highly constrained environments. Generally, software systems tend to grow in functionality over time, requiring separation of concerns to maintain operational architecture characteristics, such as performance and scale.

### Client/Server

**==fundamental style in architecture separates technical functionality between frontend and backend, called a two-tier, or client/server, architecture.==** Many different flavors of this architecture exist, depending on the era and computing capabilities.

**Three-tier**

An architecture that became quite popular during the late 1990s was a three-tier architecture, which provided even more layers of separation

The three-tier architecture corresponded with network-level protocols such as Common Object Request Broker Architecture (CORBA) and Distributed Component Object Model (DCOM) that facilitated building distributed architectures.

Just as developers today don’t worry about how network protocols like TCP/IP work (they just work), most architects don’t have to worry about this level of plumbing in distributed architectures. The capabilities offered by such tools in that era exist today as either tools (like message queues) or architecture patterns (such as event-driven architecture)

## Monolithic Versus Distributed Architectures

Architecture styles can be classified into two main types: monolithic (single deployment unit of all code) and distributed (multiple deployment units connected through remote access protocols). While no classification scheme is perfect, distributed architectures all share a common set of challenges and issues not found in the monolithic architecture styles, making this classification scheme a good separation between the various architecture styles.

- **Monolithic**
  - Layered architecture
  - Pipeline architecture
  - Microkernel architecture

- **Distributed**
  - Service-based architecture
  - Event-driven architecture
  - Space-based architecture
  - Service-oriented architecture
  - Microservices architecture

Distributed architecture styles, while being much more powerful in terms of performance, scalability, and availability than monolithic architecture styles, have significant trade-offs for this power. The first group of issues facing all distributed architectures are described in the fallacies of distributed computing

### Fallacy #1: The Network Is Reliable

![[Pasted image 20250504104538.png]]

**==Developers and architects alike assume that the network is reliable, but it is not==**. While networks have become more reliable over time, the fact of the matter is that networks still remain generally unreliable. This is significant for all distributed architectures because all distributed architecture styles rely on the network for communication to and from services, as well as between services. As illustrated in Figure 9-2,Service B may be totally healthy, but Service A cannot reach it due to a network problem; or even worse, Service A made a request to Service B to process some data and does not receive a response because of a network issue. This is why things like timeouts and circuit breakers exist between services. The more a system relies on the network (such as microservices architecture), the potentially less reliable it becomes.

### Fallacy #2: Latency Is Zero

![[Pasted image 20250504104642.png]]

when that same call is made through a remote access protocol (such as REST, messaging, or RPC), the time measured to access that service (``t_remote``) is measured in milliseconds. Therefore, ``t_remote`` will always be greater that ``t_local``. Latency in any distributed architecture is not zero, yet most architects ignore this fallacy, insisting that they have fast networks.

==**When using any distributed architecture, architects must know this latency average. It is the only way of determining whether a distributed architecture is feasible, particularly when considering microservices (see Chapter 17) due to the fine-grained nature of the services and the amount of communication between those services.**==

### Fallacy #3: Bandwidth Is Infinite

![[Pasted image 20250504104829.png]]

Bandwidth is usually not a concern in monolithic architectures, because once processing goes into a monolith, little or no bandwidth is required to process that business request. However, as shown in Figure 9-4, once systems are broken apart into smaller deployment units (services) in a distributed architecture such as microservices, communication to and between these services significantly utilizes bandwidth, causing networks to slow down, thus impacting latency (fallacy #2) and reliability

**==Regardless of the technique used, ensuring that the minimal amount of data is passed between services or systems in a distributed architecture is the best way to address this fallacy.==**

### Fallacy #4: The Network Is Secure

![[Pasted image 20250504104941.png]]

Most architects and developers get so comfortable using virtual private networks (VPNs), trusted networks, and firewalls that they tend to forget about this fallacy of distributed computing: the network is not secure. Security becomes much more challenging in a distributed architecture. As shown in Figure 9-5, each and every endpoint to each distributed deployment unit must be secured so that unknown or bad requests do not make it to that service. The surface area for threats and attacks increases by magnitudes when moving from a monolithic to a distributed architecture

### Fallacy #5: The Topology Never Changes

![[Pasted image 20250504105326.png]]

This fallacy refers to the overall network topology, including all of the routers, hubs, switches, firewalls, networks, and appliances used within the overall network. Architects assume that the topology is fixed and never changes. Of course it changes. It changes all the time. What is the significance of this fallacy?

Architects must be in constant communication with operations and network administrators to know what is changing and when so that they can make adjustments accordingly to reduce the type of surprise previously described. This may seem obvious and easy, but it is not. As a matter of fact, this fallacy leads directly to the next fallacy.

### Fallacy #6: There Is Only One Administrator

Architects all the time fall into this fallacy, assuming they only need to collaborate and communicate with one administrator. As shown in Figure 9-7, there are dozens of network administrators in a typical large company. Who should the architect talk to with regard to latency (“Fallacy #2: Latency Is Zero” on page 125) or topology changes (“Fallacy #5: The Topology Never Changes” on page 128)? This fallacy points to the complexity of distributed architecture and the amount of coordination that must happen to get everything working correctly.

### Fallacy #7: Transport Cost Is Zero

![[Pasted image 20250504105425.png]]

Whenever embarking on a distributed architecture, we encourage architects to analyze the current server and network topology with regard to capacity, bandwidth, latency, and security zones to not get caught up in the trap of surprise with this fallacy.

### Fallacy #8: The Network Is Homogeneous

![[Pasted image 20250504105449.png]]

Most architects and developers assume a network is homogeneous—made up by only one network hardware vendor. Nothing could be farther from the truth. Most companies have multiple network hardware vendors in their infrastructure, if not more.

The significance of this fallacy is that not all of those heterogeneous hardware vendors play together well. Most of it works, but does Juniper hardware seamlessly integrate with Cisco hardware? Networking standards have evolved over the years, making this less of an issue, but the fact remains that not all situations, load, and circumstances have been fully tested, and as such, network packets occasionally get lost.

### Other Distributed Considerations

**Distributed logging**  
Performing root-cause analysis to determine why a particular order was dropped is very difficult and time-consuming in a distributed architecture due to the distribution of application and system logs. In a monolithic application there is typically only one log, making it easier to trace a request and determine the issue. However, distributed architectures contain dozens to hundreds of different logs, all located in a different place and all with a different format, making it difficult to track down a problem.

**Distributed transactions**  
Architects and developers take transactions for granted in a monolithic architecture world because they are so straightforward and easy to manage. Standard commits and rollbacks executed from persistence frameworks leverage ACID (atomicity, consistency, isolation, durability) transactions to guarantee that the data is updated in a correct way to ensure high data consistency and integrity. Such is not the case with distributed architectures.  
Distributed architectures rely on what is called eventual consistency to ensure the data processed by separate deployment units is at some unspecified point in time all synchronized into a consistent state. **==This is one of the trade-offs of distributed architecture: high scalability, performance, and availability at the sacrifice of data consistency and data integrity.==**  

Transactional sagas are one way to manage distributed transactions. Sagas utilize either event sourcing for compensation or finite state machines to manage the state of transaction. In addition to sagas, BASE transactions are used. BASE stands for (B)asic availability, (S)oft state, and (E)ventual consistency. BASE transactions are not a piece of software, but rather a technique. Soft state in BASE refers to the transit of data from a source to a target, as well as the inconsistency between data sources. Based on the basic availability of the systems or services involved, the systems will eventually become consistent through the use of architecture patterns and messaging.

**Contract maintenance and versioning**  
Another particularly difficult challenge within distributed architecture is contract creation, maintenance, and versioning. A contract is behavior and data that is agreed upon by both the client and the service. Contract maintenance is particularly difficult in distributed architectures, primarily due to decoupled services and systems owned by different teams and departments. Even more complex are the communication models needed for version deprecation.

# CHAPTER 10 Layered Architecture Style

The layered architecture, also known as the n-tiered architecture style, is one of the most common architecture styles. **==This style of architecture is the de facto standard for most applications, primarily because of its simplicity, familiarity, and low cost.==**

The layered architecture style also falls into several architectural anti-patterns, including the architecture by implication anti-pattern and the accidental architecture anti-pattern. If a developer or architect is unsure which architecture style they are using, or if an Agile development team “just starts coding,” chances are good that it is the layered architecture style they are implementing.

## Topology

Components within the layered architecture style are organized into logical horizontal layers, with each layer performing a specific role within the application (such as presentation logic or business logic). Although there are no specific restrictions in terms of the number and types of layers that must exist, most layered architectures consist of four standard layers: presentation, business, persistence, and database, as illustrated in Figure 10-1. In some cases, the business layer and persistence layer are combined into a single business layer, particularly when the persistence logic (such as SQL or HSQL) is embedded within the business layer components.

![[Pasted image 20250504110313.png]]

![[Pasted image 20250504110319.png]]

Each layer of the layered architecture style has a specific role and responsibility within the architecture
Each layer in the architecture forms an abstraction around the work that needs to be done to satisfy a particular business request.

This separation of concerns concept within the layered architecture style makes it easy to build effective roles and responsibility models within the architecture. Components within a specific layer are limited in scope, dealing only with the logic that pertains to that layer.

The layered architecture is a technically partitioned architecture (as opposed to a domain-partitioned architecture). Groups of components, rather than being grouped by domain (such as customer), are grouped by their technical role in the architecture (such as presentation or business). As a result, any particular business domain is spread throughout all of the layers of the architecture

## Layers of Isolation

Each layer in the layered architecture style can be either closed or open. **==A closed layer means that as a request moves top-down from layer to layer, the request cannot skip any layers, but rather must go through the layer immediately below it to get to the next layer==**

![[Pasted image 20250504110502.png]]

The layers of isolation concept means that changes made in one layer of the architecture generally don’t impact or affect components in other layers, providing the contracts between those layers remain unchanged. Each layer is independent of the other layers, thereby having little or no knowledge of the inner workings of other layers in the architecture. However, to support layers of isolation, layers involved with the major flow of the request necessarily have to be closed. If the presentation layer can directly access the persistence layer, then changes made to the persistence layer would impact both the business layer and the presentation layer, producing a very tightly coupled application with layer interdependencies between components. This type of architecture then becomes very brittle, as well as difficult and expensive to change.

## Adding Layers

While closed layers facilitate layers of isolation and therefore help isolate change within the architecture, there are times when it makes sense for certain layers to be open.

Suppose there is an architecture decision stating that the presentation layer is restricted from using these shared business objects. This constraint is illustrated in Figure 10-4, with the dotted line going from a presentation component to a shared business object in the business layer. This scenario is difficult to govern and control because architecturally the presentation layer has access to the business layer, and hence has access to the shared objects within that layer.

![[Pasted image 20250504110729.png]]

One way to architecturally mandate this restriction is to add to the architecture a new services layer containing all of the shared business objects. Adding this new layer now architecturally restricts the presentation layer from accessing the shared business objects because the business layer is closed (see Figure 10-5). However, the new services layer must be marked as open; otherwise the business layer would be forced to go through the services layer to access the persistence layer. Marking the services layer as open allows the business layer to either access that layer (as indicated by the solid arrow), or bypass the layer and go to the next one down (as indicated by the dotted arrow in Figure 10-5).

![[Pasted image 20250504110915.png]]

Leveraging the concept of open and closed layers helps define the relationship between architecture layers and request flows. It also provides developers with the necessary information and guidance to understand various layer access restrictions within the architecture.

## Other Considerations

The layered architecture makes for a good starting point for most applications when it is not known yet exactly which architecture style will ultimately be used. This is a common practice for many microservices efforts when architects are still determining whether microservices is the right architecture choice, but development must begin. However, when using this technique, be sure to keep reuse at a minimum and keep object hierarchies
fairly shallow so as to maintain a good level of modularity. This will help facilitate the move to another architecture style later on.

**==One thing to watch out for with the layered architecture is the architecture sinkhole anti-pattern. This anti-pattern occurs when requests move from layer to layer as simple pass-through processing with no business logic performed within each layer==**

Every layered architecture will have at least some scenarios that fall into the architecture sinkhole anti-pattern. The key to determining whether the architecture sinkhole anti-pattern is at play is to analyze the percentage of requests that fall into this category. The 80-20 rule is usually a good practice to follow.

## Why Use This Architecture Style

The layered architecture style is a good choice for small, simple applications or websites. **==It is also a good architecture choice, particularly as a starting point, for situations with very tight budget and time constraints. Because of the simplicity and familiarity among developers and architects, the layered architecture is perhaps one of the lowest-cost architecture styles, promoting ease of development for smaller applications. The layered architecture style is also a good choice when an architect is still analyzing business needs and requirements and is unsure which architecture style would be best.==**

# CHAPTER 11 Pipeline Architecture Style

As soon as developers and architects decided to split functionality into discrete parts, this pattern followed. Most developers know this architecture as this underlying principle behind Unix terminal shell languages, such as ``Bash`` and ``Zsh``.

![[Pasted image 20250504112413.png]]

The pipes and filters coordinate in a specific fashion, with pipes forming one-way communication between filters, usually in a point-to-point fashion.

## Pipes

Pipes in this architecture form the communication channel between filters. Each pipe is typically unidirectional and point-to-point (rather than broadcast) for performance reasons, accepting input from one source and always directing output to another. The payload carried on the pipes may be any data format, but architects favor smaller amounts of data to enable high performance.

## Filters

Filters are self-contained, independent from other filters, and generally stateless. Filters should perform one task only. Composite tasks should be handled by a sequence of filters rather than a single one.
Four types of filters exist within this architecture style:

**Producer**  
The starting point of a process, outbound only, sometimes called the source.

**Transformer**  
Accepts input, optionally performs a transformation on some or all of the data, then forwards it to the outbound pipe. Functional advocates will recognize this feature as *map*.

**Tester**  
Accepts input, tests one or more criteria, then optionally produces output, based on the test. Functional programmers will recognize this as similar to *reduce*.

**Consumer**  
The termination point for the pipeline flow. Consumers sometimes persist the final result of the pipeline process to a database, or they may display the final results on a user interface screen.

The unidirectional nature and simplicity of each of the pipes and filters encourages compositional reuse

