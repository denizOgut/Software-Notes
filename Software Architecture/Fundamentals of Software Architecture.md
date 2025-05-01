
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

