
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

# Chapter 12 Microkernel Architecture Style

This architecture style is a natural fit for product-based applications (packaged and made available for download and installation as a single, monolithic deployment, typically installed on the customer’s site as a third-party product) but is widely used in many nonproduct custom business applications as well.

## Topology

The microkernel architecture style is a relatively simple monolithic architecture consisting of two architecture components: a core system and plug-in components. Application logic is divided between independent plug-in components and the basic core system, providing extensibility, adaptability, and isolation of application features and custom processing logic

![[Pasted image 20250505172641.png]]

## Core System

The core system is formally defined as the minimal functionality required to run the system. The Eclipse IDE is a good example of this. The core system of Eclipse is just a basic text editor: open a file, change some text, and save the file. It’s not until you add plug-ins that Eclipse starts becoming a usable product. However, another definition of the core system is the happy path (general processing flow) through the application, with little or no custom processing. Removing the cyclometric complexity of the core system and placing it into separate plug-in components allows for better extensibility and maintainability, as well as increased testability

```java
public void assessDevice(String deviceID) {
    if (deviceID.equals("iPhone6s")) {
        assessiPhone6s();
    } else if (deviceID.equals("iPad1")) {
        assessiPad1();
    } else if (deviceID.equals("Galaxy5")) {
        assessGalaxy5();
    } else {
        // Handle other cases here
    }
}
```

```java
public void assessDevice(String deviceID) {
    String plugin = pluginRegistry.get(deviceID);
    try {
        Class<?> theClass = Class.forName(plugin);
        Constructor<?> constructor = theClass.getConstructor();
        DevicePlugin devicePlugin = (DevicePlugin) constructor.newInstance();
        devicePlugin.assess();
    } catch (Exception e) {
        e.printStackTrace();
        // Optionally handle specific exceptions like ClassNotFoundException, etc.
    }
}
```

Depending on the size and complexity, the core system can be implemented as a layered architecture or a modular monolith (as illustrated in Figure 12-2). In some cases, the core system can be split into separately deployed domain services, with each domain service containing specific plug-in components specific to that domain.

![[Pasted image 20250505173032.png]]

## Plug-In Components

Plug-in components are standalone, independent components that contain specialized processing, additional features, and custom code meant to enhance or extend the core system. Additionally, they can be used to isolate highly volatile code, creating better maintainability and testability within the application. Ideally, plug-in components should be independent of each other and have no dependencies between them.

The communication between the plug-in components and the core system is generally point-to-point, meaning the “pipe” that connects the plug-in to the core system is usually a method invocation or function call to the entry-point class of the plug-in component. In addition, the plug-in component can be either compile-based or runtime-based. Runtime plug-in components can be added or removed at runtime without having to redeploy the core system or other plug-ins, and they are usually managed through frameworks

## Registry

The core system needs to know about which plug-in modules are available and how to get to them. One common way of implementing this is through a plug-in registry. This registry contains information about each plug-in module, including things like its name, data contract, and remote access protocol details

The registry can be as simple as an internal map structure owned by the core system containing a key and the plug-in component reference, or it can be as complex as a registry and discovery tool either embedded within the core system or deployed externally Consul). Using the electronics recycling example, the following Java code implements a simple registry within the core system, showing a point-to-point entry, a messaging entry, and a RESTful entry example for assessing an iPhone 6S device:

```java
Map<String, String> registry = new HashMap<>();

static {
    // point-to-point access example
    registry.put("iPhone6s", "Iphone6sPlugin");

    // messaging example
    registry.put("iPhone6s", "iphone6s.queue");

    // restful example
    registry.put("iPhone6s", "https://atlas:443/assess/iphone6s");
}
```

## Contracts

The contracts between the plug-in components and the core system are usually standard across a domain of plug-in components and include behavior, input data, and output data returned from the plug-in component. Custom contracts are typically found in situations where plug-in components are developed by a third party where you have no control over the contract used by the plug-in. In such cases, it is common to create an adapter between the plug-in contract and your standard contract so that the core system doesn’t need specialized code for each plug-in.

Plug-in contracts can be implemented in XML, JSON, or even objects passed back and forth between the plug-in and the core system.

```java
public interface AssessmentPlugin {
	public AssessmentOutput assess();
	public String register();
	public String deregister();
}
public class AssessmentOutput {
	public String assessmentReport;
	public Boolean resell;
	public Double value;
	public Double resellPrice;
}
```

## Examples and Use Cases

Most of the tools used for developing and releasing software are implemented using the microkernel architecture. Some examples include the Eclipse IDE, PMD, Jira, and Jenkins, to name a few). Internet web browsers such as Chrome and Firefox are another common product example using the microkernel architecture: viewers and other plug-ins add additional capabilities that are not otherwise found in the basic browser representing the core system. The examples are endless for product-based software,

Another example of a large and complex business application that can leverage the microkernel architecture is tax preparation software.

# CHAPTER 13 Service-Based Architecture Style

**==Service-based architecture is a hybrid of the microservices architecture style and is considered one of the most pragmatic architecture styles, mostly due to its architectural flexibility. Although service-based architecture is a distributed architecture, it doesn’t have the same level of complexity and cost as other distributed architectures, such as microservices or event-driven architecture, making it a very popular choice for many business-related applications==**

## Topology

The basic topology of service-based architecture follows a distributed macro layered structure consisting of a separately deployed user interface, separately deployed remote coarse-grained services, and a monolithic database.

**==Services within this architecture style are typically coarse-grained “portions of an application” (usually called domain services) that are independent and separately deployed. Services are typically deployed in the same manner as any monolithic application would be (such as an EAR file, WAR file, or assembly) and as such do not require containerization (although you could deploy a domain service in a container such as Docker). Because the services typically share a single monolithic database==**, the number of services within an application context generally range between 4 and 12 services, with the average being about 7 services.

![[Pasted image 20250505174446.png]]

In most cases there is only a single instance of each domain service within a service based architecture. However, based on scalability, fault tolerance, and throughput needs, multiple instances of a domain service can certainly exist. Multiple instances of a service usually require some sort of load-balancing capability between the user interface and the domain service so that the user interface can be directed to a healthy and available service instance.

Services are accessed remotely from a user interface using a remote access protocol. While REST is typically used to access services from the user interface, messaging, remote procedure call (RPC), or even SOAP could be used as well. While an API layer consisting of a proxy or gateway can be used to access services from the user interface (or other external requests), in most cases the user interface accesses the services directly using a service locator pattern embedded within the user interface, API gateway, or proxy.

**==One important aspect of service-based architecture is that it typically uses a centrally shared database. This allows services to leverage SQL queries and joins in the same way a traditional monolithic layered architecture would==**. Because of the small number of services (4 to 12), database connections are not usually an issue in service-based architecture. Database changes, however, can be an issue. The section “Database Partitioning” on page 169 describes techniques for addressing and managing database change within a service-based architecture.

## Service Design and Granularity

Because domain services in a service-based architecture are generally coarse-grained, each domain service is typically designed using a layered architecture style consisting of an API façade layer, a business layer, and a persistence layer. Another popular design approach is to domain partition each domain service using sub-domains similar to the modular monolith architecture style.

![[Pasted image 20250505174609.png]]

Regardless of the service design, a domain service must contain some sort of API access facade that the user interface interacts with to execute some sort of business functionality. The API access facade typically takes on the responsibility of orchestrating the business request from the user interface.

Because domain services are coarse-grained, regular ACID (atomicity, consistency, isolation, durability) database transactions involving database commits and rollbacks are used to ensure database integrity within a single domain service. Highly distributed architectures like microservices, on the other hand, usually have fine-grained
services and use a distributed transaction technique known as BASE transactions (basic availability, soft state, eventual consistency) that rely on eventual consistency and hence do not support the same level of database integrity as ACID transactions in a service-based architecture

Domain services, being coarse-grained, allow for better data integrity and consistency, but there is a trade-off.

## Database Partitioning

Although not required, services within a service-based architecture usually share a single, monolithic database due to the small number of services (4 to 12) within a given application context. This database coupling can present an issue with respect to database table schema changes. If not done properly, a table schema change can potentially impact every service, making database changes a very costly task in terms of effort and coordination.

Within a service-based architecture, the shared class files representing the database table schemas (usually referred to as entity objects) reside in a custom shared library used by all the domain services (such as a JAR file or DLL). Shared libraries might also contain SQL code. The practice of creating a single shared library of entity objects is the least effective way of implementing service-based architecture. Any change to the database table structures would also require a change to the single shared library containing all of the corresponding entity objects, thus requiring a change and redeployment to every service, regardless of whether or not the services actually access the changed table. Shared library versioning can help address this issue, but nevertheless, with a single shared library it is difficult to know which services are actually impacted by the table change without manual, detailed analysis

![[Pasted image 20250505175131.png]]

One way to mitigate the impact and risk of database changes is to logically partition the database and manifest the logical partitioning through federated shared libraries.

![[Pasted image 20250505175147.png]]

> ==**Make the logical partitioning in the database as fine-grained as possible while still maintaining well-defined data domains to better control database changes within a service-based architecture.==**

## When to Use This Architecture Style

The flexibility of this architecture style (see “Topology Variants” on page 165) combined with the number of three-star and four-star architecture characteristics ratings make service-based architecture one of the most pragmatic architecture styles available. While there are certainly other distributed architecture styles that are much more powerful, some companies find that power comes at too steep of a price, while others find that they quite simply don’t need that much power. It’s like having the power, speed, and agility of a Ferrari used only for driving back and forth to work in rush-hour traffic at 50 kilometers per hour—sure it looks cool, but what a waste of resources and money

**==Service-based architecture is also a natural fit when doing domain-driven design. Because services are coarse-grained and domain-scoped, each domain fits nicely into a separately deployed domain service. Each service in service-based architecture encompasses a particular domain (such as recycling in the electronic recycling application), therefore compartmentalizing that functionality into a single unit of software, making it easier to apply changes to that domain.==**

Maintaining and coordinating database transactions is always an issue with distributed architectures in that they typically rely on eventual consistency rather than traditional ACID (atomicity, consistency, isolation, and durability) transactions. However, service-based architecture preserves ACID transactions better than any other distributed architecture due to the coarse-grained nature of the domain services. There are cases where the user interface or API gateway might orchestrate two or more domain services, and in these cases the transaction would need to rely on sagas and BASE transactions. However, in most cases the transaction is scoped to a particular domain service, allowing for the traditional commit and rollback transaction functionality found in most monolithic applications.

Lastly, service-based architecture is a good choice for achieving a good level of architectural modularity without having to get tangled up in the complexities and pitfalls of granularity. As services become more fine-grained, issues surrounding orchestration and choreography start to appear. Both orchestration and choreography are required when multiple services must be coordinated to complete a certain business transaction. Orchestration is the coordination of multiple services through the use of a separate mediator service that controls and manages the workflow of the transaction (like a conductor in an orchestra). Choreography, on the other hand, is the coordination of multiple services by which each service talks to one another without the use of a central mediator (like dancers in a dance). As services become more fine grained, both orchestration and choreography are necessary to tie the services together to complete the business transaction. However, because services within a service-based architecture tend to be more coarse-grained, they don’t require coordination nearly as much as other distributed architectures

# CHAPTER 14 Event-Driven Architecture Style

The event-driven architecture style is a popular distributed asynchronous architecture style used to produce highly scalable and high-performance applications. It is also highly adaptable and can be used for small applications and as well as large, complex ones. Event-driven architecture is made up of decoupled event processing components that asynchronously receive and process events. It can be used as a standalone architecture style or embedded within other architecture styles (such as an event-driven microservices architecture).

In this model, requests made to the system to perform some sort of action are send to a request orchestrator. The request orchestrator is typically a user interface, but it can also be implemented through an API layer or enterprise service bus. The role of the request orchestrator is to deterministically and synchronously direct the request to various request processors. The request processors handle the request, either retrieving or updating information in a database.

An event-based model, on the other hand, reacts to a particular situation and takes action based on that event. An example of an event-based model is submitting a bid for a particular item within an online auction. Submitting the bid is not a request made to the system, but rather an event that happens after the current asking price is announced. The system must respond to this event by comparing the bid to others received at the same time to determine who is the current highest bidder

![[Pasted image 20250505191000.png]]

## Topology

There are two primary topologies within event-driven architecture: the mediator topology and the broker topology. **==The mediator topology is commonly used when you require control over the workflow of an event process, whereas the broker topology is used when you require a high degree of responsiveness and dynamic control over the processing of an event.==** Because the architecture characteristics and implementation strategies differ between these two topologies, it is important to understand each one to know which is best suited for a particular situation.

### Broker Topology

The broker topology differs from the mediator topology in that there is no central event mediator. Rather, **==the message flow is distributed across the event processor components in a chain-like broadcasting fashion through a lightweight message broker (such as ``RabbitMQ``, ``ActiveMQ``, ``HornetQ``, and so on). This topology is useful when you have a relatively simple event processing flow and you do not need central event orchestration and coordination.==**

There are four primary architecture components within the broker topology that work together to manage and process events. In this topology, the flow begins with an initiating event, which represents a specific action or occurrence such as placing a bid in an online auction or more complex life changes in systems like health benefits platforms—for example, getting married or switching jobs. This initiating event is sent to the event broker, which uses an event channel to pass it along for further handling. Notably, the broker topology does not include a central mediator to manage events. Instead, a single event processor picks up the initiating event from the broker and handles the associated task. After the task is complete, the event processor broadcasts the result asynchronously to the rest of the system in the form of a processing event.

- **Initiating Event**  
    The first trigger in the event-driven flow, such as placing a bid or reporting a life change, which sets the entire process in motion.
    
- **Event Broker**  
    A communication mechanism that receives the initiating event and passes it along via an event channel for processing, without centralized control.
    
- **Event Processor**  
    A single component responsible for receiving the initiating event from the broker and performing the related processing task.
    
- **Processing Event**  
    A resulting event that represents the outcome of the event processor’s task, which is asynchronously shared with the system.

This processing event is then asynchronously sent to the event broker for further processing, if needed. Other event processors listen to the processing event, react to that event by doing something, then advertise through a new processing event what they did. This process continues until no one is interested in what a final event processor did. Figure 14-2 illustrates this event processing flow.

The event broker component is usually federated (meaning multiple domain-based clustered instances), where each federated broker contains all of the event channels used within the event flow for that particular domain. Because of the decoupled asynchronous fire-and-forget broadcasting nature of the broker topology, topics (or topic exchanges in the case of AMQP) are usually used in the broker topology using a publish-and-subscribe messaging model.

![[Pasted image 20250505191537.png]]

It is always a good practice within the broker topology for each event processor to advertise what it did to the rest of the system, regardless of whether or not any other event processor cares about what that action was. This practice provides architectural extensibility if additional functionality is required for the processing of that event.

 **Table 14-1. Trade-offs of the Broker Topology**

| Advantages                  | Disadvantages              |
|----------------------------|----------------------------|
| Highly decoupled event processors | Workflow control           |
| High scalability           | Error handling             |
| High responsiveness        | Recoverability             |
| High performance           | Restart capabilities       |
| High fault tolerance       | Data inconsistency         |

### Mediator Topology

The mediator topology of event-driven architecture addresses some of the shortcomings of the broker topology described in the previous section. **==Central to this topology is an event mediator, which manages and controls the workflow for initiating events that require the coordination of multiple event processors. The architecture components that make up the mediator topology are an initiating event, an event queue, an event mediator, event channels, and event processors.==**

Like in the broker topology, the initiating event is the event that starts the whole eventing process. Unlike the broker topology, the initiating event is sent to an initiating event queue, which is accepted by the event mediator. The event mediator only knows the steps involved in processing the event and therefore generates corresponding processing events that are sent to dedicated event channels (usually queues) in a point-to-point messaging fashion. Event processors then listen to dedicated event channels, process the event, and usually respond back to the mediator that they have completed their work. Unlike the broker topology, event processors within the mediator topology do not advertise what they did to the rest of the system

![[Pasted image 20250505191805.png]]

In most implementations of the mediator topology, there are multiple mediators, usually associated with a particular domain or grouping of events. This reduces the single point of failure issue associated with this topology and also increases overall throughput and performance.

The event mediator can be implemented in a variety of ways, depending on the nature and complexity of the events it is processing.

The mediator component has knowledge and control over the workflow, something the broker topology does not have. Because the mediator controls the workflow, it can maintain event state and manage error handling, recoverability, and restart capabilities.

While the mediator topology addresses the issues associated with the broker topology, there are some negatives associated with the mediator topology. First of all, it is very difficult to declaratively model the dynamic processing that occurs within a complex event flow. As a result, many workflows within the mediator only handle the general processing, and a hybrid model combining both the mediator and broker topologies is used to address the dynamic nature of complex event processing (such as out-of-stock conditions or other nontypical errors). Furthermore, although the event processors can easily scale in the same manner as the broker topology, the  mediator must scale as well, something that occasionally produces a bottleneck in the overall event processing flow. Finally, event processors are not as highly decoupled in the mediator topology as with the broker topology, and performance is not as good due to the mediator controlling the processing of the event

 **Table 14-2. Trade-offs of an Alternative Topology**

| Advantages             | Disadvantages                       |
|------------------------|-------------------------------------|
| Workflow control       | More coupling of event processors   |
| Error handling         | Lower scalability                   |
| Recoverability         | Lower performance                   |
| Restart capabilities   | Lower fault tolerance               |
| Better data consistency| Modeling complex workflows          |
The choice between the broker and mediator topology essentially comes down to a trade-off between workflow control and error handling capability versus high performance and scalability. Although performance and scalability are still good within the mediator topology, they are not as high as with the broker topology.

## Asynchronous Capabilities

The event-driven architecture style offers a unique characteristic over other architecture  styles in that it relies solely on asynchronous communication for both fire-and forget processing (no response required) as well as request/reply processing (response required from the event consumer). Asynchronous communication can be a powerful technique for increasing the overall responsiveness of a system.

![[Pasted image 20250505192306.png]]

When the user does not need any information back (other than an acknowledgement or a thank you message), why make the user wait? Responsiveness is all about notifying the user that the action has been accepted and will be processed momentarily, whereas performance is about making the end-to-end process faster. Notice that nothing was done to optimize the way the comment service processes the text—in both cases it is still taking 3,000 milliseconds. Addressing performance would have been optimizing the comment service to run all of the text and grammar parsing engines in parallel with the use of caching and other similar techniques.

The main issue with asynchronous communications is error handling. While responsiveness is significantly improved, it is difficult to address error conditions, adding to the complexity of the event-driven system. The next section addresses this issue with a pattern of reactive architecture called the workflow event pattern.

## Error Handling

The workflow event pattern of reactive architecture is one way of addressing the issues associated with error handling in an asynchronous workflow. This pattern is a reactive architecture pattern that addresses both resiliency and responsiveness. In other words, the system can be resilient in terms of error handling without an impact to responsiveness.

The workflow event pattern leverages delegation, containment, and repair through the use of a workflow delegate, as illustrated in Figure 14-14. The event producer asynchronously passes data through a message channel to the event consumer. If the event consumer experiences an error while processing the data, it immediately delegates that error to the workflow processor and moves on to the next message in the event queue. In this way, overall responsiveness is not impacted because the next message is immediately processed. If the event consumer were to spend the time trying to figure out the error, then it is not reading the next message in the queue, therefore impacting the responsiveness not only of the next message, but all other messages waiting in the queue to be processed.

Once the workflow processor receives an error, it tries to figure out what is wrong with the message. This could be a static, deterministic error, or it could leverage some machine learning algorithms to analyze the message to see some anomaly in the data. Either way, the workflow processor programmatically (without human intervention) makes changes to the original data to try and repair it, and then sends it back to the originating queue. The event consumer sees this message as a new one and tries to process it again, hopefully this time with some success. Of course, there are many times when the workflow processor cannot determine what is wrong with the message. In these cases the workflow processor sends the message off to another queue, which is then received in what is usually called a “dashboard,” an application that looks similar to the Microsoft’s Outlook or Apple’s Mail. This dashboard usually resides on the desktop of a person of importance, who then looks at the message, applies manual fixes to it, and then resubmits it to the original queue (usually through a reply-to message header variable).

![[Pasted image 20250505192432.png]]

One of the consequences of the workflow event pattern is that messages in error are processed out of sequence when they are resubmitted.

## Preventing Data Loss

**==Data loss is always a primary concern when dealing with asynchronous communications.==** Unfortunately, there are many places for data loss to occur within an event-driven architecture. By data loss we mean a message getting dropped or never making it to its final destination. Fortunately, there are basic out-of-the-box techniques that can be leveraged to prevent data loss when using asynchronous messaging.

1. The message never makes it to the queue from **Event Processor A**, or even if it does, the **broker goes down** before the next event processor can retrieve the message.

2. **Event Processor B** de-queues the next available message but **crashes before processing** the event.

3. **Event Processor B** is **unable to persist the message to the database** due to a data error.

![[Pasted image 20250505192748.png]]

Each of these areas of data loss can be mitigated through basic messaging techniques. Issue 1 (the message never makes it to the queue) is easily solved by leveraging persistent message queues, along with something called synchronous send. Persisted message queues support what is known as guaranteed delivery. When the message broker receives the message, it not only stores it in memory for fast retrieval, but also persists the message in some sort of physical data store (such as a filesystem or database). If the message broker goes down, the message is physically stored on disk so that when the message broker comes back up, the message is available for processing. Synchronous send does a blocking wait in the message producer until the broker has acknowledged that the message has been persisted. With these two basic techniques there is no way to lose a message between the event producer and the queue because the message is either still with the message producer or persisted within the queue.

## Broadcast Capabilities

One of the other unique characteristics of event-driven architecture is the capability to broadcast events without knowledge of who (if anyone) is receiving the message and what they do with it. This technique, which is illustrated in Figure 14-18, shows that when a producer publishes a message, that same message is received by multiple subscribers.

![[Pasted image 20250505192837.png]]

Broadcasting is perhaps the highest level of decoupling between event processors because the producer of the broadcast message usually does not know which event processors will be receiving the broadcast message and more importantly, what they will do with the message. Broadcast capabilities are an essential part of patterns for eventual consistency, complex event processing (CEP), and a host of other situations.

## Request-Reply

In event-driven architecture, synchronous communication is accomplished through  request-reply messaging (sometimes referred to as pseudo synchronous communications). Each event channel within request-reply messaging consists of two queues: a request queue and a reply queue. The initial request for information is asynchronously sent to the request queue, and then control is returned to the message producer. The message producer then does a blocking wait on the reply queue, waiting for the response. The message consumer receives and processes the message and then sends the response to the reply queue.

![[Pasted image 20250505193215.png]]

There are two primary techniques for implementing request-reply messaging. The first (and most common) technique is to use a correlation ID contained in the message header. A correlation ID is a field in the reply message that is usually set to the message ID of the original request message

The other technique used to implement request-reply messaging is to use a temporary queue for the reply queue. A temporary queue is dedicated to the specific request, created when the request is made and deleted when the request ends

![[Pasted image 20250505193259.png]]

## Choosing Between Request-Based and Event-Based

The request-based model and event-based model are both viable approaches for designing software systems. However, choosing the right model is essential to the overall success of the system. We recommend choosing the request-based model for well-structured, data-driven requests (such as retrieving customer profile data) when certainty and control over the workflow is needed. We recommend choosing the event-based model for flexible, action-based events that require high levels of responsiveness and scale, with complex and dynamic user processing.

 **Table 14-3. Event-Based Architecture: Advantages over Request-Based and Trade-offs**

| Advantages                                 | Trade-offs                             |
|-------------------------------------------|-----------------------------------------|
| Better response to dynamic user content   | Only supports eventual consistency      |
| Better scalability and elasticity         | Less control over processing flow       |
| Better agility and change management      | Less certainty over outcome of event flow |
| Better adaptability and extensibility     | Difficult to test and debug             |
| Better responsiveness and performance     |                                         |
| Better real-time decision making          |                                         |
| Better reaction to situational awareness  |                                         |
## Hybrid Event-Driven Architectures

While many applications leverage the event-driven architecture style as the primary overarching architecture, in many cases event-driven architecture is used in conjunction with other architecture styles, forming what is known as a hybrid architecture. Some common architecture styles that leverage event-driven architecture as part of another architecture style include microservices and space-based architecture. Other hybrids that are possible include an event-driven microkernel architecture and an event-driven pipeline architecture.

Adding event-driven architecture to any architecture style helps remove bottlenecks, provides a back pressure point in the event requests get backed up, and provides a level of user responsiveness not found in other architecture styles. Both microservices and space-based architecture leverage messaging for data pumps, asynchronously sending data to another processor that in turn updates data in a database. Both also leverage event-driven architecture to provide a level of programmatic scalability to services in a microservices architecture and processing units in a space-based architecture when using messaging for inter-service communication.

# CHAPTER 15 Space-Based Architecture Style

Most web-based business applications follow the same general request flow: a request from a browser hits the web server, then an application server, then finally the database server. While this pattern works great for a small set of users, bottlenecks start appearing as the user load increases, first at the web-server layer, then at the application-server layer, and finally at the database-server layer. The usual response to bottlenecks based on an increase in user load is to scale out the web servers. This is relatively easy and inexpensive, and it sometimes works to address the bottleneck issues. However, in most cases of high user load, scaling out the web-server layer just moves the bottleneck down to the application server. Scaling application servers can be more complex and expensive than web servers and usually just moves the bottleneck down to the database server, which is even more difficult and expensive to scale.

**==In any high-volume application with a large concurrent user load, the database will usually be the final limiting factor in how many transactions you can process concurrently==**. While various caching technologies and database scaling products help to address these issues, the fact remains that scaling out a normal application for extreme loads is a very difficult proposition.

![[Pasted image 20250510124648.png]]

The space-based architecture style is specifically designed to address problems involving high scalability, elasticity, and high concurrency issues. It is also a useful architecture style for applications that have variable and unpredictable concurrent user volumes.

## General Topology

Space-based architecture gets its name from the concept of tuple space, the technique of using multiple parallel processors communicating through shared memory. **==High scalability, high elasticity, and high performance are achieved by removing the central database as a synchronous constraint in the system and instead leveraging replicated in-memory data grids==**. Application data is kept in-memory and replicated among all the active processing units. When a processing unit updates data, it asynchronously sends that data to the database, usually via messaging with persistent queues. Processing units start up and shut down dynamically as user load increases and decreases, thereby addressing variable scalability. Because there is no central database involved in the standard transactional processing of the application, the database bottleneck is removed, thus providing near-infinite scalability within the application.

There are several architecture components that make up a space-based architecture: a processing unit containing the application code, virtualized middleware used to manage and coordinate the processing units, data pumps to asynchronously send updated data to the database, data writers that perform the updates from the data pumps, and data readers that read database data and deliver it to processing units upon startup.

![[Pasted image 20250510124813.png]]

### Processing Unit

The processing unit (illustrated in Figure 15-3) contains the application logic (or portions of the application logic). This usually includes web-based components as well as backend business logic

![[Pasted image 20250510124851.png]]

### Virtualized Middleware

The virtualized middleware handles the infrastructure concerns within the architecture that control various aspects of data synchronization and request handling. The components that make up the virtualized middleware include a messaging grid, data grid, processing grid, and deployment manager. These components, which are described in detail in the next sections, can be custom written or purchased as third party products.

#### Messaging grid

manages input request and session state. When a request comes into the virtualized middleware, the messaging grid component determines which active processing components are available to receive the request and forwards the request to one of those processing units. The complexity of the messaging grid can range from a simple round-robin algorithm to a more complex next-available algorithm that keeps track of which request is being processed by which processing unit

![[Pasted image 20250510125026.png]]

#### Data grid

**==The data grid component is perhaps the most important and crucial component in this architecture style. In most modern implementations the data grid is implemented solely within the processing units as a replicated cache. However, for those replicated caching implementations that require an external controller, or when using a distributed cache, this functionality would reside in both the processing units as well as in the data grid component within the virtualized middleware.==**

![[Pasted image 20250510125122.png]]

Data is synchronized between processing units that contain the same named data grid.

```java
HazelcastInstance hz = Hazelcast.newHazelcastInstance();
Map<String, CustomerProfile> profileCache = hz.getReplicatedMap("CustomerProfile");
```

All processing units needing access to the customer profile information would contain this code.

Data replication within the processing units also allows service instances to come up and down without having to read data from the database, providing there is at least one instance containing the named replicated cache. When a processing unit instance comes up, it connects to the cache provider (such as ``Hazelcast``) and makes a request to get the named cache. Once the connection is made to the other processing units, the cache will be loaded from one of the other instances.

Each processing unit knows about all other processing unit instances through the use of a member list. The member list contains the IP address and ports of all other processing units using that same named cache.

#### Processing grid

an optional component within the virtualized middleware that manages orchestrated request processing when there are multiple processing units involved in a single business request. If a request comes in that requires coordination between processing unit types (e.g., an order processing unit and a payment processing unit), it is the processing grid that mediates and orchestrates the request between those two processing units.

![[Pasted image 20250510125415.png]]

#### Deployment manager

The deployment manager component manages the dynamic startup and shutdown of processing unit instances based on load conditions. This component continually monitors response times and user loads, starts up new processing units when load increases, and shuts down processing units when the load decreases.

### Data Pumps

A data pump is a way of sending data to another processor which then updates data in a database. Data pumps are a necessary component within space-based architecture, as processing units do not directly read from and write to a database. **==Data pumps within a space-based architecture are always asynchronous, providing eventual consistency with the in-memory cache and the database==**. When a processing unit instance receives a request and updates its cache, that processing unit becomes the owner of the update and is therefore responsible for sending that update through the data pump so that the database can be updated eventually. 

![[Pasted image 20250510125622.png]]

In most cases there are multiple data pumps, each one usually dedicated to a particular domain or subdomain (such as customer or inventory). Data pumps can be dedicated to each type of cache containing a much larger and general cache.

### Data Writers

The data writer component accepts messages from a data pump and updates the database with the information contained in the message of the data pump

A domain-based data writer contains all of the necessary database logic to handle all regardless of the number
of data pumps it is accepting the updates within a particular domain

![[Pasted image 20250510125815.png]]

### Data Readers

Whereas data writers take on the responsibility for updating the database, data readers take on the responsibility for reading data from the database and sending it to the processing units via a reverse data pump. In space-based architecture, data readers are only invoked under one of three situations: a crash of all processing unit instances of the same named cache, a redeployment of all processing units within the same named cache, or retrieving archive data not contained in the replicated cache. 

In a space-based architecture, if all instances go down due to a crash or redeployment, data must be reloaded from the database—though typically avoided. As instances restart, each attempts to acquire a lock on the cache; the first to succeed becomes the temporary cache owner, while others wait. The cache owner sends a request to a queue for data. A data reader component processes this request, queries the database, and streams the data back through a reverse data pump. The cache owner receives and loads this data into the cache, then releases the lock. Other instances then sync up and resume processing. Data readers, like data writers, can be domain-specific or tied to a particular processing unit and are implemented similarly—as services, applications, or data hubs. Together, data readers and writers form the data abstraction layer, with the key distinction being the processing unit’s awareness of database schema.

## Data Collisions

When using replicated caching in an active/active state where updates can occur to any service instance containing the same named cache, there is the possibility of a data collision due to replication latency. A data collision occurs when data is updated in one cache instance (cache A), and during replication to another cache instance (cache B), the same data is updated by that cache (cache B). In this scenario, the local update to cache B will be overridden through replication by the old data from cache A, and through

## Cloud Versus On-Premises Implementations
 
 Space-based architecture offers some unique options when it comes to the environments in which it is deployed. The entire topology, including the processing units, virtualized middleware, data pumps, data readers and writers, and the database, can be deployed within cloud-based environments on-premises (“on-prem”). However, this architecture style can also be deployed between these environments, offering a unique feature not found in other architecture styles.

A powerful feature of this architecture style (as illustrated in Figure 15-11) is to deploy applications via processing units and virtualized middleware in managed cloud-based environments while keeping the physical databases and corresponding data on-prem. This topology supports very effective cloud-based data synchronization due to the asynchronous data pumps and eventual consistency model of this architecture style. Transactional processing can occur on dynamic and elastic cloud-based environments while preserving physical data management, reporting, and data analytics within secure and local on-prem environments


![[Pasted image 20250510130627.png]]

## Replicated Versus Distributed Caching

Space-based architecture relies on caching for the transactional processing of an application. Removing the need for direct reads and writes to a database is how space-based architecture is able to support high scalability, high elasticity, and high performance. Space-based architecture mostly relies on replicated caching, although distributed caching can be used as well.

With replicated caching, as illustrated in Figure 15-12, each processing unit contains its own in-memory data grid that is synchronized between all processing units using that same named cache. When an update occurs to a cache within any of the processing units, the other processing units are automatically updated with the new
information.

![[Pasted image 20250510130720.png]]

Replicated caching is not only extremely fast, but it also supports high levels of fault tolerance. Since there is no central server holding the cache, replicated caching does not have a single point of failure. There may be exceptions to this rule, however, based on the implementation of the caching product used. Some caching products require the presence of an external controller to monitor and control the replication of data between processing units, but most product companies are moving away from this model.

While replicated caching is the standard caching model for space-based architecture, there are some cases where it is not possible to use replicated caching.

Distributed caching, as illustrated in Figure 15-13, requires an external server or service dedicated to holding a centralized cache. In this model the processing units do not store data in internal memory, but rather use a proprietary protocol to access the data from the central cache server. Distributed caching supports high levels of data 

| Decision Criteria   | Replicated Cache                   | Distributed Cache                    |
|---------------------|------------------------------------|--------------------------------------|
| Optimization        | Performance                        | Consistency                          |
| Cache Size          | Small (<100 MB)                    | Large (>500 MB)                      |
| Type of Data        | Relatively static                  | Highly dynamic                       |
| Update Frequency    | Relatively low                     | High update rate                     |

## Near-Cache Considerations

A near-cache is a type of caching hybrid model bridging in-memory data grids with a distributed cache. In this model (illustrated in Figure 15-14) the distributed cache is referred to as the full backing cache, and each in-memory data grid contained within each processing unit is referred to as the front cache. The front cache always contains a smaller subset of the full backing cache, and it leverages an eviction policy to remove older items so that newer ones can be added. The front cache can be what is known as a most recently used (MRU) cache containing the most recently used items or a most frequently used (MFU) cache containing the most frequently used items. Alternatively, a random replacement eviction policy can be used in the front cache so that items are removed in a random manner when space is needed to add a new item. Random replacement (RR) is a good eviction policy when there is no clear analysis of the data with regard to keeping either the latest used versus the most frequently used.

![[Pasted image 20250510130906.png]]

# CHAPTER 16 Orchestration-Driven Service-Oriented Architecture

## History and Philosophy

This style of service-oriented architecture appeared just as companies were becoming enterprises in the late 1990s: merging with smaller companies, growing at a breakneck pace, and requiring more sophisticated IT to accommodate this growth. However, computing resources were scarce, precious, and commercial. Distributed computing had just become possible and necessary, and many companies needed the variable scalability and other beneficial characteristics

Many external drivers forced architects in this era toward distributed architectures with significant constraints. Before open source operating systems were thought reliable enough for serious work, operating systems were expensive and licensed per machine. Similarly, commercial database servers came with Byzantine licensing schemes, which caused application server vendors (which offered database connection pooling) to battle with database vendors. Thus, architects were expected to reuse as much as possible. In fact, reuse in all forms became the dominant philosophy in this architecture

![[Pasted image 20250510132147.png]]

Service-oriented architecture is a distributed architecture; the exact demarcation of boundaries isn’t shown in Figure 16-1 because it varied based on organization.

## Taxonomy

The architect’s driving philosophy in this architecture centered around enterprise level reuse. Many large companies were annoyed at how much they had to continue to rewrite software, and they struck on a strategy to gradually solve that problem. Each layer of the taxonomy supported this goal.

### Business Services

Business services sit at the top of this architecture and provide the entry point. These service definitions contained no code—just input, output, and sometimes schema information. They were usually defined by business users, hence the name business services

### Enterprise Services

The enterprise services contain fine-grained, shared implementations. Typically, a team of developers is tasked with building atomic behavior around particular business domains: 

This separation of responsibility flows from the reuse goal in this architecture. If developers can build fine-grained enterprise services at just the correct level of granularity, the business won’t have to rewrite that part of the business workflow again. Gradually, the business will build up a collection of reusable assets in the form of reusable enterprise services.

### Application Services

Not all services in the architecture require the same level of granularity or reuse as the enterprise services. Application services are one-off, single-implementation services.

### Infrastructure Services

Infrastructure services supply the operational concerns, such as monitoring, logging, authentication, and authorization. These services tend to be concrete implementations, owned by a shared infrastructure team that works closely with operations.

### Orchestration Engine

The orchestration engine forms the heart of this distributed architecture, stitching together the business service implementations using orchestration, including features like transactional coordination and message transformation. This architecture is typically tied to a single relational database, or a few, rather than a database per service as in microservices architectures. Thus, transactional behavior is handled declaratively in the orchestration engine rather than in the database.

The orchestration engine defines the relationship between the business and enterprise services, how they map together, and where transaction boundaries lie. It also acts as an integration hub, allowing architects to integrate custom code with package and legacy software systems.

While this approach might sound appealing, in practice it was mostly a disaster. Offloading transaction behavior to an orchestration tool sounded good, but finding the correct level of granularity of transactions became more and more difficult. While building a few services wrapped in a distributed transaction is possible, the architecture becomes increasingly complex as developers must figure out where the appropriate transaction boundaries lie between services

### Message Flow

All requests go through the orchestration engine—it is the location within this architecture where logic resides. Thus, message flow goes through the engine even for internal calls,

![[Pasted image 20250510132705.png]]

## Reuse…and Coupling

A major goal of this architecture is reuse at the service level—the ability to gradually build business behavior that can be incrementally reused over time. Architects in this architecture were instructed to find reuse opportunities as aggressively as possible.

![[Pasted image 20250510132747.png]]

![[Pasted image 20250510132750.png]]

Perhaps the most damaging revelation from this architecture came with the realization of the impractically of building an architecture so focused on technical partitioning. While it makes sense from a separation and reuse philosophy standpoint, it was a practical nightmare.

## Architecture Characteristics Ratings

Many of the modern criteria we use to evaluate architecture now were not priorities when this architecture was popular. In fact, the Agile software movement had just started and had not penetrated into the size of organizations likely to use this architecture.

# CHAPTER 17 Microservices Architecture

**==Microservices is heavily inspired by the ideas in domain-driven design (DDD), a logical design process for software projects. One concept in particular from DDD, bounded context, decidedly inspired microservices==**. The concept of bounded context represents a decoupling style. When a developer defines a domain, that domain includes many entities and behaviors, identified in artifacts such as code and database schemas.

Within a bounded context, the internal parts, such as code and data schemas, are coupled together to produce work; but they are never coupled to anything outside the bounded context, such as a database or class definition from another bounded context. This allows each context to define only what it needs rather than accommodating other constituents.

While reuse is beneficial, remember the First Law of Software Architecture regarding trade-offs. **==The negative trade-off of reuse is coupling.==** When an architect designs a system that favors reuse, they also favor coupling to achieve that reuse, either by inheritance or composition.

However, if the architect’s goal requires high degrees of decoupling, then they favor duplication over reuse. The primary goal of microservices is high decoupling, physically modeling the logical notion of bounded context.

## Topology

![[Pasted image 20250510175658.png]]

due to its single-purpose nature, the service size in microservices is much smaller than other distributed architectures, such as the orchestration-driven service-oriented architecture. Architects expect each service to
include all necessary parts to operate independently, including databases and other dependent components.

## Distributed

Microservices form a distributed architecture: each service runs in its own process, which originally implied a physical computer but quickly evolved to virtual machines and containers. Decoupling the services to this degree allows for a simple solution to a common problem in architectures that heavily feature multitenant infrastructure for hosting applications.

Separating each service into its own process solves all the problems brought on by sharing. Before the evolutionary development of freely available open source operating systems, combined with automated machine provisioning, it was impractical for each domain to have its own infrastructure. Now, however, with cloud resources and container technology, teams can reap the benefits of extreme decoupling, both at the domain and operational level.

**==Performance is often the negative side effect of the distributed nature of microservices. Network calls take much longer than method calls, and security verification at every endpoint adds additional processing time, requiring architects to think carefully about the implications of granularity when designing the system.==**

Because microservices is a distributed architecture, experienced architects advise against the use of transactions across service boundaries, making determining the granularity of services the key to success in this architecture.

## Bounded Context

The driving philosophy of microservices is the notion of bounded context: each service models a domain or workflow. Thus, each service includes everything necessary to operate within the application, including classes, other subcomponents, and database schemas. This philosophy drives many of the decisions architects make within this architecture. However, microservices try to avoid coupling, and thus an architect building this architecture style prefers duplication to coupling. 

Microservices take the concept of a domain-partitioned architecture to the extreme. **==Each service is meant to represent a domain or subdomain; in many ways, microservices is the physical embodiment of the logical concepts in domain-driven design.==**

### Granularity

Architects struggle to find the correct granularity for services in microservices, and often make the mistake of making their services too small, which requires them to build communication links back between the services to do useful work.

**==The purpose of service boundaries in microservices is to capture a domain or workflow==**. In some applications, those natural boundaries might be large for some parts of the system—some business processes are more coupled than others. Here are some guidelines architects can use to help find the appropriate boundaries:

Purpose
- The most obvious boundary relies on the inspiration for the architecture style, a domain. Ideally, each microservice should be extremely functionally cohesive, contributing one significant behavior on behalf of the overall application. 

Transactions 

- Bounded contexts are business workflows, and often the entities that need to cooperate in a transaction show architects a good service boundary. Because transactions cause issues in distributed architectures, if architects can design their system to avoid them, they generate better designs.

Choreography
- If an architect builds a set of services that offer excellent domain isolation yet require extensive communication to function, the architect may consider bundling these services back into a larger service to avoid the communication overhead.

**==Iteration is the only way to ensure good service design. Architects rarely discover the perfect granularity, data dependencies, and communication styles on their first pass. However, after iterating over the options, an architect has a good chance of refining their design.==**

### Data Isolation

Another requirement of microservices, driven by the bounded context concept, is data isolation. Many other architecture styles use a single database for persistence. However, microservices tries to avoid all kinds of coupling, including shared schemas and databases used as integration points

## API Layer

While an API layer may be used for variety of things, it should not be used as a mediator or orchestration tool if the architect wants to stay true to the underlying philosophy of this architecture

## Operational Reuse

One of the philosophies in the traditional service-oriented architecture was to reuse as much functionality as possible, domain and operational alike. In microservices, architects try to split these two concerns.

Once a team has built several microservices, they realize that each has common elements that benefit from similarity ***The sidecar pattern*** offers a solution to this problem

![[Pasted image 20250510180745.png]]

In Figure 17-2, the common operational concerns appear within each service as a separate component, which can be owned by either individual teams or a shared infrastructure team. The sidecar component handles all the operational concerns that teams benefit from coupling together. Thus, when it comes time to upgrade the monitoring tool, the shared infrastructure team can update the sidecar, and each microservices receives that new functionality.

Once teams know that each service includes a common sidecar, they can build a service mesh, allowing unified control across the architecture for concerns like logging and monitoring. The common sidecar components connect to form a consistent operational interface across all microservices, as shown in Figure 17-3.

![[Pasted image 20250510180930.png]]

![[Pasted image 20250510180940.png]]

Each service forms a node in the overall mesh, as shown in Figure 17-4. The service mesh forms a console that allows teams to globally control operational coupling, such as monitoring levels, logging, and other cross-cutting operational concerns.

Architects use service discovery as a way to build elasticity into microservices architectures. Rather than invoke a single service, a request goes through a service discovery tool, which can monitor the number and frequency of requests, as well as spin up new instances of services to handle scale or elasticity concerns. Architects often include service discovery in the service mesh, making it part of every microservice. The API layer is often used to host service discovery, allowing a single place for user interfaces or other calling systems to find and create services in an elastic, consistent way.

## Frontends

Microservices favors decoupling, which would ideally encompass the user interfaces as well as backend concerns. In fact, the original vision for microservices included the user interface as part of the bounded context, faithful to the principle in DDD. However, practicalities of the partitioning required by web applications and other external constraints make that goal difficult

![[Pasted image 20250510181026.png]]

Developers can implement the micro-frontend pattern in a variety of ways, either using a component-based web framework such as ``React`` or using one of several open source frameworks that support this pattern.

## Communication

In microservices, architects and developers struggle with appropriate granularity, which affects both data isolation and communication. Finding the correct communication style helps teams keep services decoupled yet still coordinated in useful ways.

Fundamentally, architects must decide on synchronous or asynchronous communication. Synchronous communication requires the caller to wait for a response from the callee. Microservices architectures typically utilize protocol-aware heterogeneous interoperability.

Protocol-aware
- Because microservices usually don’t include a centralized integration hub to avoid operational coupling, each service should know how to call other services. Thus, architects commonly standardize on how particular services call each other: a certain level of REST, message queues, and so on. That means that services must know (or discover) which protocol to use to call other services.

Heterogeneous
- Because microservices is a distributed architecture, each service may be written in a different technology stack. Heterogeneous suggests that microservices fully supports polyglot environments, where different services use different platforms.

Interoperability
- Describes services calling one another. While architects in microservices try to discourage transactional method calls, services commonly call other services via the network to collaborate and send/receive information

For asynchronous communication, architects often use events and messages

## Transactions and Sagas

Because the decoupling in the architecture encourages the same level for the databases, atomicity that was trivial in monolithic applications becomes a problem in distributed ones.

Building transactions across service boundaries violates the core decoupling principle of the microservices architecture 

> ==**Don’t do transactions in microservices—fix granularity instead!==**

# CHAPTER 18 Choosing the Appropriate Architecture Style

Nothing is more contextual to a number of factors within an organization and what software it builds. Choosing an architecture style represents the culmination of analysis and thought about tradeoffs for architecture characteristics, domain considerations, strategic goals, and a host of other things.

## Shifting “Fashion” in Architecture

Observations from the past
- New architecture styles generally arise from observations and pain points from past experiences. Architects have experience with systems in the past that influence their thoughts about future systems. Architects must rely on their past experience— it is that experience that allowed that person to become an architect in the first place. Often, new architecture designs reflect specific deficiencies from past architecture styles. For example, architects seriously rethought the implications of code reuse after building architectures that featured it and then realizing the negative trade-offs.

Changes in the ecosystem
- Constant change is a reliable feature of the software development ecosystem— everything changes all the time. The change in our ecosystem is particularly chaotic, making even the type of change impossible to predict. For example, a few years ago, no one knew what Kubernetes was, and now there are multiple conferences around the world with thousands of developers. In a few more years, Kubernetes may be replaced with some other tool that hasn’t been written yet.

New capabilities 
- When new capabilities arise, architecture may not merely replace one tool with another but rather shift to an entirely new paradigm. For example, few architects or developers anticipated the tectonic shift caused in the software development world by the advent of containers such as Docker. While it was an evolutionary step, the impact it had on architects, tools, engineering practices, and a host of other factors astounded most in the industry. The constant change in the ecosystem also delivers a new collection of tools and capabilities on a regular basis. Architects must keep a keen eye open to not only new tools but new paradigms. Something may just look like a new one-of-something-we-already-have, but it may include nuances or other changes that make it a game changer. New capabilities don’t even have to rock the entire development world—the new features may be a minor change that aligns exactly with an architect’s goals.

Acceleration 
- Not only does the ecosystem constantly change, but the rate of change also continues to rise. New tools create new engineering practices, which lead to new design and capabilities. Architects live in a constant state of flux because change is both pervasive and constant.

Domain changes 
- The domain that developers write software for constantly shifts and changes, either because the business continues to evolve or because of factors like mergers with other companies.

Technology changes
- As technology continues to evolve, organizations try to keep up with at least some of these changes, especially those with obvious bottom-line benefits.

External factors
- Many external factors only peripherally associated with software development may drive change within an organizations. For example, architects and developers might be perfectly happy with a particular tool, but the licensing cost has become prohibitive, forcing a migration to another option.

## Decision Criteria

The domain
- Architects should understand many important aspects of the domain, especially those that affect operational architecture characteristics. Architects don’t have to be subject matter experts, but they must have at least a good general understanding of the major aspects of the domain under design.

Architecture characteristics that impact structure
- Architects must discover and elucidate the architecture characteristics needed to support the domain and other external factors.

Data architecture
- Architects and DBAs must collaborate on database, schema, and other data related concerns. We don’t cover much about data architecture in this book; it is its own specialization. However, architects must understand the impact that data design might have on their design, particularly if the new system must interact with an older and/or in-use data architecture.

Organizational factors
- Many external factors may influence design. For example, the cost of a particular cloud vendor may prevent the ideal design. Or perhaps the company plans to engage in mergers and acquisitions, which encourages an architect to gravitate toward open solutions and integration architectures.

Knowledge of process, teams, and operational concerns 
- Many specific project factors influence an architect’s design, such as the software development process, interaction (or lack of) with operations, and the QA process. For example, if an organization lacks maturity in Agile engineering practices, architecture styles that rely on those practices for success will present difficulties.

Domain/architecture isomorphism 
- Some problem domains match the topology of the architecture. For example, the microkernel architecture style is perfectly suited to a system that requires customizability— the architect can design customizations as plug-ins. Another example might be genome analysis, which requires a large number of discrete operations, and space-based architecture, which offers a large number of discrete processors.

Taking all these things into account, the architect must make several determinations:
Monolith versus distributed 
- Using the quantum concepts discussed earlier, the architect must determine if a single set of architecture characteristics will suffice for the design, or do different parts of the system need differing architecture characteristics? A single set implies that a monolith is suitable (although other factors may drive an architect toward a distributed architecture), whereas different architecture characteristics imply a distributed architecture.

Where should data live? 
- If the architecture is monolithic, architects commonly assume a single relational databases or a few of them. In a distributed architecture, the architect must decide which services should persist data, which also implies thinking about how data must flow throughout the architecture to build workflows. Architects must consider both structure and behavior when designing architecture and not be fearful of iterating on the design to find better combinations.

What communication styles between services—synchronous or asynchronous?
- Once the architect has determined data partitioning, their next design consideration is the communication between services—synchronous or asynchronous? Synchronous communication is more convenient in most cases, but it can lead to scalability, reliability, and other undesirable characteristics. Asynchronous communication can provide unique benefits in terms of performance and scale but can present a host of headaches: data synchronization, deadlocks, race conditions, debugging, and so on.

> ==**Use synchronous by default, asynchronous when necessary.==**