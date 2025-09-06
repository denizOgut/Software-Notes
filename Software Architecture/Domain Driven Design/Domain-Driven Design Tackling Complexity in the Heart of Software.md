# Part I: Putting the Domain Model to Work

Maps are models, and every model represents some aspect of reality or an idea that is of interest. A model is a simplification. It is an interpretation of reality that abstracts the aspects relevant to solving the problem at hand and ignores extraneous detail. Every software program relates to some activity or interest of its user. That subject area to which the user applies the program is the domain of the software

A model is a selectively simplified and consciously structured form of knowledge. An appropriate model makes sense of information and focuses it on a problem. A domain model is not a particular diagram; it is the idea that the diagram is intended to convey. It is not just the knowledge in a domain expert's head; it is a rigorously organized and selective abstraction of that knowledge . A diagram can represent and communicate a model, as can carefully written code, as can an English sentence.

**The Utility of a Model in Domain-Driven Design**

In domain-driven design, three basic uses determine the choice of a model.

1. *The model and the heart of the design shape each other* . It is the intimate link between the model and the implementation that makes the model relevant and ensures that the analysis that went into it applies to the final product, a running program. This binding of model and implementation also helps during maintenance and continuing development, because the code can be interpreted based on understanding the model.
2. *The model is the backbone of a language used by all team members* . Because of the binding of model and implementation, developers can talk about the program in this language. They can communicate with domain experts without translation. And because the language is based on the model, our natural linguistic abilities can be turned to refining the model itself.
3. *The model is distilled knowledge* . The model is the team's agreed-upon way of structuring domain knowledge and distinguishing the elements of most interest. A model captures how we choose to think about the domain as we select terms, break down concepts, and relate them. The shared language allows developers and domain experts to collaborate effectively as they wrestle information into this form. The binding of model and implementation makes experience with early versions of the software applicable as feed-back into the modeling process.

**The Heart of Software**

The heart of software is its ability to solve domain-related problems for its user. All other features, vital though they may be, support this basic purpose.
Complexity in the heart of software has to be tackled head-on. To do otherwise is to risk irrelevance.

## Chapter One. Crunching Knowledge

### Ingredients of Effective Modeling

1. *Binding the model and the implementation* . That crude prototype forged the essential link early, and it was maintained through all subsequent iterations.
2. *Cultivating a language based on the model* . At first, the engineers had to explain elementary PCB issues to me, and I had to explain what a class diagram meant. But as the project proceeded, any of us could take terms straight out of the model, organize them into sentences consistent with the structure of the model, and be un-ambiguously understood without translation.
3. *Developing a knowledge-rich model* . The objects had behavior and enforced rules. The model wasn't just a data schema; it was integral to solving a complex problem. It captured knowledge of various kinds.
4. *Distilling the model* . Important concepts were added to the model as it became more complete, but equally important, concepts were dropped when they didn't prove useful or central. When an unneeded concept was tied to one that was needed, a new model was found that distinguished the essential concept so that the other could be dropped.
5. *Brainstorming and experimenting* . The language, combined with sketches and a brainstorming attitude, turned our discussions into laboratories of the model, in which hundreds of experimental variations could be exercised, tried, and judged. As the team went through scenarios, the spoken expressions themselves provided a quick viability test of a proposed model, as the ear could quickly detect either the clarity and ease or the awkwardness of expression.

### Knowledge Crunching

Effective domain modelers are knowledge crunchers. They take a torrent of information and probe for the relevant trickle. They try one organizing idea after another, searching for the simple view that makes sense of the mass. Many models are tried and rejected or transformed. Success comes in an emerging set of abstract concepts that makes sense of all the detail. This distillation is a rigorous expression of the particular knowledge that has been found most relevant.

Knowledge crunching is not a solitary activity. A team of developers and domain experts collaborate, typically led by developers. Together they draw in information and crunch it into a useful form. The raw material comes from the minds of domain experts, from users of existing systems, from the prior experience of the technical team with a related legacy system or another project in the same domain

The interaction between team members changes as all members crunch the model together. The constant refinement of the domain model forces the developers to learn the important principles of the business they are assisting, rather than to produce functions mechanically. The domain experts often refine their own understanding by being forced to distill what they know to essentials, and they come to understand the conceptual rigor that software projects require.
All this makes the team members more competent knowledge crunchers. They winnow out the extraneous.

### Continuous Learning

When we set out to write software, we never know enough. Knowledge on the project is fragmented, scattered among many people and documents, and it's mixed with other information so that we don't even know which bits of knowledge we really need. Domains that seem less technically daunting can be deceiving: we don't realize how much we don't know. This ignorance leads us to make false assumptions.

### Knowledge-Rich Design

Business activities and rules are as central to a domain as are the entities involved; any domain will have various categories of concepts. Knowledge crunching yields models that reflect this kind of insight. In parallel with model changes, developers refactor the implementation to express the model, giving the application use of that knowledge.

It is with this move beyond entities and values that knowledge crunching can get intense, because there may be actual inconsistency among business rules. Domain experts are usually not aware of how complex their mental processes are as, in the course of their work

#### Example Extracting a Hidden Concept

![[Pasted image 20250714214120.png]]
the booking application's responsibility is to associate each **Cargo** with a **Voyage** , recording and tracking that relationship. So far so good

```java
public int makeBooking(Cargo cargo, Voyage voyage) {
	int confirmation = orderConfirmationSequence.next();
	voyage.addCargo(cargo,confirmation);
	return confirmation;
}
```

Because there are always last-minute cancellations, standard practice in the shipping industry is to accept more cargo than a particular vessel can carry on a voyage. This is called "overbooking."

*Allow 10% overbooking.*

![[Pasted image 20250714214315.png]]

```java
public int makeBooking(Cargo cargo, Voyage voyage) {
    double maxBooking = voyage.capacity() * 1.1;
    if ((voyage.bookedCargoSize() + cargo.size()) > maxBooking) {
        return -1;
    }
    int confirmation = orderConfirmationSequence.next();
    voyage.addCargo(cargo, confirmation);
    return confirmation;
}
```

Now an important business rule is hidden as a guard clause in an application method 

1. As written, it is unlikely that any business expert could read this code to verify the rule, even with the guidance of a developer.
2. It would be difficult for a technical, non-businessperson to connect the requirement text with the code. If the rule were more complex, that much more would be at stake

**==We can change the design to better capture this knowledge. The overbooking rule is a policy. Policy is another name for the design pattern known as *STRATEGY*==**

the concept we are trying to capture does fit the meaning of a policy, which is an equally important motivation in domain-driven design

![[Pasted image 20250714214524.png]]

```java
public int makeBooking(Cargo cargo, Voyage voyage) {
    if (!overbookingPolicy.isAllowed(cargo, voyage)) {
        return -1;
    }
    int confirmation = orderConfirmationSequence.next();
    voyage.addCargo(cargo, confirmation);
    return confirmation;
}
```

```java
public boolean isAllowed(Cargo cargo, Voyage voyage) {
    return (cargo.size() + voyage.bookedCargoSize()) <= (voyage.capacity() * 1.1);
}
```

It will be clear to all that overbooking is a distinct policy, and the implementation of that rule is explicit and separate. Now, I am not recommending that such an elaborate design be applied to every detail of the domain

This example is meant to show that a domain model and corresponding design can be used to secure and share knowledge. The more explicit design has these advantages:
1. In order to bring the design to this stage, the programmers and everyone else involved will have come to understand the nature of overbooking as a distinct and important business rule, not just an obscure calculation.
2. Programmers can show business experts technical artifacts, even code, that should be intelligible to domain experts (with guidance), thereby closing the feedback loop.

### Deep Models

As we come to understand the domain and the needs of the application, we usually discard superficial model elements that seemed important in the beginning, or we shift their perspective. Subtle abstractions emerge that would not have occurred to us at the outset but that pierce to the heart of the matter

Knowledge crunching is an exploration, and you can't know where you will end up.

## Chapter Two. Communication and the Use of Language

On a project without a common language, developers have to translate for domain experts. Domain experts translate between developers and still other domain experts. Developers even translate for each other. Translation muddles model concepts, which leads to destructive refactoring of code. The indirectness of communication conceals the formation of schisms—different team members use terms differently but don't realize it. This leads to unreliable software that doesn't fit together (see Chapter 14 ). The effort of translation prevents the interplay of knowledge and ideas that lead to deep model insights.

**==A project faces serious problems when its language is fractured. Domain experts use their jargon while technical team members have their own language tuned for discussing the domain in terms of design. The terminology of day-to-day discussions is disconnected from the terminology embedded in the code (ultimately the most important product of a software project). And even the same person uses different language in speech and in writing, so that the most incisive expressions of the domain often emerge in a transient form that is never captured in the code or even in writing. Translation blunts communication and makes knowledge crunching anemic. Yet none of these dialects can be a common language because none serves all needs.==**

The vocabulary of that *UBIQUITOUS LANGUAGE* includes the names of classes and prominent operations. The *LANGUAGE* includes terms to discuss rules that have been made explicit in the model. Finally, this language is enriched with the names of patterns the team commonly applies to the domain model

The model-based language should be used among developers to describe not only artifacts in the system, but tasks and functionality. This same model should supply the language for the developers and domain experts to communicate with each other, and for the domain experts to communicate among themselves about requirements, development planning, and features. The more pervasively the language is used, the more smoothly understanding will flow.

Persistent use of the *UBIQUITOUS LANGUAGE* will force the model's weaknesses into the open. The team will experiment and find alternatives to awkward terms or combinations. As gaps are found in the language, new words will enter the discussion. These changes to the language will be recognized as changes in the domain model and will lead the team to update class diagrams and rename classes and methods in the code, or even change behavior, when the meaning of a term changes.
 
 **==Use the model as the backbone of a language. Commit the team to exercising that language relentlessly in all communication within the team and in the code. Use the same language in diagrams, writing, and especially speech. Iron out difficulties by experimenting with alternative expressions, which reflect alternative models. Then refactor the code, renaming classes, methods, and modules to conform to the new model. Resolve confusion over terms in conversation, in just the way we come to agree on the meaning of ordinary words. Recognize that a change in the *UBIQUITOUS LANGUAGE* is a change to the model. Domain experts should object to terms or structures that are awkward or inadequate to convey domain understanding; developers should watch for ambiguity or inconsistency that will trip up design.==**


### Modeling Out Loud

One of the best ways to refine a model is to explore with speech, trying out loud various constructs from possible model variations. Rough edges are easy to hear.

It is vital that we play around with words and phrases, harnessing our linguistic abilities to the modeling effort, just as it is vital to engage our visual/spatial reasoning by sketching diagrams

**==Play with the model as you talk about the system. Describe scenarios out loud using the elements and interactions of the model, combining concepts in ways allowed by the model. Find easier ways to say what you need to say, and then take those new ideas back down to the diagrams and code.==**

### One Team, One Language

Technical people often feel the need to "shield" the business experts from the domain model. They say:
"Too abstract for them."
"They don't understand objects."
"We have to collect requirements in their terminology."
These are just a few of the reasons I've heard for having two languages on the team. Forget them

***==If sophisticated domain experts don't understand the model, there is something wrong with the model.==***

The developers and domain experts can informally test the model by walking through scenarios, using the model objects step-by-step. Almost every discussion is an opportunity for the developers and user experts to play with the model together, deepening each other's understanding and refining concepts as they go.

![[Pasted image 20250714215430.png]]

With a *UBIQUITOUS LANGUAGE* , conversations among developers, discussions among domain experts, and expressions in the code itself are all based on the same language, derived from a shared domain model.

### Documents and Diagrams

Some people are naturally visual, and diagrams help people grasp certain kinds of information. UML diagrams are pretty good at communicating relationships between objects, and they are fair at showing interactions. But they do not convey the conceptual definitions of those objects. In a meeting, I would flesh out those meanings in speech as I sketched the diagram, or they would emerge in a dialog with other participants.

Simple, informal UML diagrams can anchor a discussion. Sketch a diagram of three to five objects central to the issue at hand, and everyone can stay focused. Everyone will share a view of the relationships between the objects and, significantly, the objects' names. The spoken discussion can be more effective with this aid. A diagram can be changed as people try different thought experiments, and the sketch will take on some of the fluidity of spoken words, a true part of the discussion. After all, UML stands for Unified Modeling Language .

The trouble comes when people feel compelled to convey the whole model or design through UML. A lot of object model diagrams are too complete and, simultaneously, leave too much out. They are too complete because people feel they have to put all the objects that they are going to code into a modeling tool. With all that detail, no one can see the forest for the trees.

The behavioral responsibilities of an object can be hinted at through operation names, and they can be implicitly demonstrated with object interaction (or sequence) diagrams, but they cannot be stated . So, this task falls to supplemental text or conversation. **==In other words, a UML diagram cannot convey two of the most important aspects of a model: the meaning of the concepts it represents, and what the objects are meant to do==**

The vital detail about the design is captured in the code . A well-written implementation should be transparent, revealing the model underlying it. (Making sure that this happens is the subject of the next chapter and much of the rest of this book.) Supplemental diagrams and documents can guide people's attention to the central points. Natural language discussion can fill in the nuances of meaning.

#### Written Design Documents

Once a document takes on a persistent form, it often loses its connection with the flow of the project. It is left behind by the evolution of the code, or by the evolution of the language of the project.

**Documents Should Complement Code and Speech**

A document shouldn't try to do what the code already does well . The code already supplies the detail. It is an exact specification of program behavior.

Other documents need to illuminate meaning, to give insight into large-scale structures, and to focus attention on core elements. Documents can clarify design intent when the programming language does not support a straightforward implementation of a concept. Written documents should complement the code and the talking.

**Documents Should Work for a Living and Stay Current**

A document must be involved in project activities . The easiest way to judge this is to observe the document's interaction with the UBIQUITOUS LANGUAGE . Is the document written in the language people speak on the project (now)? Is it written in the language embedded in the code?

By keeping documents minimal and focusing them on complementing code and conversation, documents can stay connected to the project. Let the UBIQUITOUS LANGUAGE and its evolution be your guide to choosing documents that live and get woven into the project's activity.

**Executable Bedrock**

Well-written code can be very communicative, but the message it communicates is not guaranteed to be accurate. Oh, the reality of the behavior caused by a section of code is inescapable. But a method name can be ambiguous, misleading, or out of date compared to the internals of the method. The assertions in a test are rigorous, but the story told by variable names and the organization of the code is not. Good programming style keeps this connection as direct as possible, but it is still an exercise in self-discipline.

Aligning the behavior, intent, and message of code using current standard technology requires discipline and a certain way of thinking about design (discussed at length in Part III ). To communicate effectively, the code must be based on the same language used to write the requirements—the same language that the developers speak with each other and with domain experts.

### Explanatory Models

The thrust of this book is that one model should underlie implementation, design, and team communication. Having separate models for these separate purposes poses a hazard.

**==Models can also be valuable as education aids to teach about the domain. The model that drives the design is one view of the domain, but it may aid learning to have other views, used only as educational tools, to communicate general knowledge of the domain.==**

One particular reason that other models are needed is scope. The technical model that drives the software development process must be strictly pared down to the necessary minimum to fulfill its functions. An explanatory model can include aspects of the domain that provide context that clarifies the more narrowly scoped model. Explanatory models offer the freedom to create much more communicative styles tailored to a particular topic.

There is no need for explanatory models to be object models, and it is generally best if they are not. It is actually helpful to avoid UML in these models, to avoid any false impression of correspondence with the software design. Even though the explanatory model and the model that drives design do often correspond, the similarities will seldom be exact. To avoid confusion, everyone must be conscious of the distinction

## Chapter Three. Binding Model and Implementation

Models come in many varieties and serve many roles, even those restricted to the context of a software development project. Domain-driven design calls for a model that doesn't just aid early analysis but is the very foundation of the design. This approach has some important implications for the code. What is less obvious is that domain-driven design requires a different approach to modeling

### Model-Driven Design

Tightly relating the code to an underlying model gives the code meaning and makes the model relevant

many complex projects do attempt some sort of domain model, but they don't maintain a tight connection between the model and the code. The model they develop, possibly useful as an exploratory tool at the outset, becomes increasingly irrelevant and even misleading. All the care lavished on the model provides little reassurance that the design is correct, because the two are different.

This connection can break down in many ways, but the detachment is often a conscious choice. Many design methodologies advocate an analysis model , quite distinct from the design and usually developed by different people. It is called an analysis model because it is the product of analyzing the business domain to organize its concepts without any consideration of the part it will play in a software system. An analysis model is meant as a tool for understanding only

The pure analysis model even falls short of its primary goal of understanding the domain, because crucial discoveries always emerge during the design/implementation effort. Very specific, unanticipated problems always arise. An up-front model will go into depth about some irrelevant subjects, while it overlooks some important subjects.

Whatever the cause, software that lacks a concept at the foundation of its design is, at best, a mechanism that does useful things without explaining its actions.

**==If the design, or some central part of it, does not map to the domain model, that model is of little value, and the correctness of the software is suspect. At the same time, complex mappings between models and design functions are difficult to understand and, in practice, impossible to maintain as the design changes. A deadly divide opens between analysis and design so that insight gained in each of those activities does not feed into the other==**

*MODEL-DRIVEN DESIGN* discards the dichotomy of analysis model and design to search out a single model that serves both purposes. Setting aside purely technical issues, each object in the design plays a conceptual role described in the model. This requires us to be more demanding of the chosen model, since it must fulfill two quite different objectives.
 
 **==Design a portion of the software system to reflect the domain model in a very literal way, so that mapping is obvious. Revisit the model and modify it to be implemented more naturally in software, even as you seek to make it reflect deeper insight into the domain. Demand a single model that serves both purposes well, in addition to supporting a robust *UBIQUITOUS LANGUAGE* . Draw from the model the terminology used in the design and the basic assignment of responsibilities. The code becomes an expression of the model, so a change to the code may be a change to the model. Its effect must ripple through the rest of the project's activities accordingly. To tie the implementation slavishly to a model usually requires software development tools and languages that support a modeling paradigm, such as object-oriented programming.==**

The single model reduces the chances of error, because the design is now a direct outgrowth of the carefully considered model. The design, and even the code itself, has the communicativeness of a model.

### Modeling Paradigms and Tool Support

To make a *MODEL-DRIVEN DESIGN* pay off, the correspondence must be literal, exact within bounds of human error. To make such a close correspondence of model and design possible, it is almost essential to work within a modeling paradigm supported by software tools that allow you to create direct analogs to the concepts in the model.

![[Pasted image 20250715120607.png]]

### Hands-On Modelers

software development is all design. All teams have specialized roles for members, but over separation of responsibility for analysis, modeling, design, and programming interferes with *MODEL-DRIVEN DESIGN*

**==If the people who write the code do not feel responsible for the model, or don't understand how to make the model work for an application, then the model has nothing to do with the software. If developers don't realize that changing code changes the model, then their refactoring will weaken the model rather than strengthen it. Meanwhile, when a modeler is separated from the implementation process, he or she never acquires, or quickly loses, a feel for the constraints of implementation. The basic constraint of MODEL-DRIVEN DESIGN —that the model supports an effective implementation and abstracts key domain knowledge—is half-gone, and the resulting models will be impractical. Finally, the knowledge and skills of experienced designers won't be transferred to other developers if the division of labor prevents the kind of collaboration that conveys the subtleties of coding a *MODEL-DRIVEN DESIGN*==**

The effectiveness of an overall design is very sensitive to the quality and consistency of fine-grained design and implementation decisions. With a *MODEL-DRIVEN DESIGN* , a portion of the code is an expression of the model; changing that code changes the model. Programmers are modelers, whether anyone likes it or not. So it is better to set up the project so that the programmers do good modeling work

**==Any technical person contributing to the model must spend some time touching the code, whatever primary role he or she plays on the project. Anyone responsible for changing code must learn to express a model through the code. Every developer must be involved in some level of discussion about the model and have contact with domain experts. Those who contribute in different ways must consciously engage those who touch the code in a dynamic exchange of model ideas through the *UBIQUITOUS LANGUAGE* .==**

Domain-driven design puts a model to work to solve problems for an application. Through knowledge crunching, a team distills a torrent of chaotic information into a practical model. *A MODEL-DRIVEN DESIGN* intimately connects the model and the implementation. The *UBIQUITOUS LANGUAGE* is the channel for all that information to flow between developers, domain experts, and the software.
The result is software that provides rich functionality based on a fundamental understanding of the core domain.

# Part II: The Building Blocks of a Model-Driven Design

## Chapter Four. Isolating the Domain

The part of the software that specifically solves problems from the domain usually constitutes only a small portion of the entire software system, although its importance is disproportionate to its size. To apply our best thinking, we need to be able to look at the elements of our model and see them as a system.

Software programs involve design and code to carry out many different kinds of tasks. They accept user input, carry out business logic, access databases, communicate over networks, display information to users, and so on. So the code involved in each program function can be substantial.

**==In an object-oriented program, UI , database, and other support code often gets written directly into the business objects. Additional business logic is embedded in the behavior of UI widgets and data-base scripts. This happens because it is the easiest way to make things work, in the short run.**==

==**When the domain-related code is diffused through such a large amount of other code, it becomes extremely difficult to see and to reason about. Superficial changes to the UI can actually change business logic. To change a business rule may require meticulous tracing of UI code, database code, or other program elements. Implementing coherent, model-driven objects becomes impractical. Automated testing is awkward. With all the technologies and logic involved in each activity, a program must be kept very simple or it becomes impossible to understand.==**

The value of layers is that each specializes in a particular aspect of a computer program. This specialization allows more cohesive designs of each aspect, and it makes these designs much easier to interpret. Of course, it is vital to choose layers that isolate the most important cohesive design aspects.

 **==Partition a complex program into layers. Develop a design within each layer that is cohesive and that depends only on the layers below. Follow standard architectural patterns to provide loose coupling to the layers above. Concentrate all the code related to the domain model in one layer and isolate it from the user interface, application, and infrastructure code. The domain objects, free of the responsibility of displaying themselves, storing themselves, managing application tasks, and so forth, can be focused on expressing the domain model. This allows a model to evolve to be rich enough and clear enough to capture essential business knowledge and put it to work.==**

### The Domain Layer Is Where the Model Lives

domain-driven design requires only one particular layer to exist. The domain model is a set of concepts. The "domain layer" is the manifestation of that model and all directly related design elements. The design and implementation of business logic constitute the domain layer.
In a *MODEL-DRIVEN DESIGN* , the software constructs of the domain layer mirror the model concepts. It is not practical to achieve that correspondence when the domain logic is mixed with other concerns of the program. Isolating the domain implementation is a prerequisite for domain-driven design.

### The Smart UI "Anti-Pattern"

A project needs to deliver simple functionality, dominated by data entry and display, with few business rules. Staff is not composed of advanced object modelers.

**==If an unsophisticated team with a simple project decides to try a MODEL-DRIVEN DESIGN with LAYERED ARCHITECTURE , it will face a difficult learning curve. Team members will have to master complex new technologies and stumble through the process of learning object modeling (which is challenging, even with the help of this book!). The overhead of managing infrastructure and layers makes very simple tasks take longer. Simple projects come with short time lines and modest expectations. Long before the team completes the assigned task, much less demonstrates the exciting possibilities of its approach, the project will have been canceled.**==

==**Even if the team is given more time, the team members are likely to fail to master the techniques without expert help. And in the end, if they do surmount these challenges, they will have produced a simple system. Rich capabilities were never requested.==**

**==Put all the business logic into the user interface. Chop the application into small functions and implement them as separate user interfaces, embedding the business rules into them. Use a relational database as a shared repository of the data. Use the most automated UI building and visual programming tools available.==**

**Advantages**

- Productivity is high and immediate for simple applications.
- Less capable developers can work this way with little training.
- Even deficiencies in requirements analysis can be overcome by releasing a prototype to users and then quickly changing the product to fit their requests.
- Applications are decoupled from each other, so that delivery schedules of small modules can be planned relatively accurately. Expanding the system with additional, simple behavior can be easy.
- Relational databases work well and provide integration at the data level.
- 4GL tools work well.
- When applications are handed off, maintenance programmers will be able to quickly redo portions they can't figure out, because the effects of the changes should be localized to each particular UI.

**Disadvantages**

- Integration of applications is difficult except through the database.
- There is no reuse of behavior and no abstraction of the business problem. Business rules have to be duplicated in each operation to which they apply.
- Rapid prototyping and iteration reach a natural limit because the lack of abstraction limits refactoring options.
- Complexity buries you quickly, so the growth path is strictly toward additional simple applications. There is no graceful path to richer behavior.

Remember, one of the consequences of this pattern is that you can't migrate to another design approach except by replacing entire applications. Just using a general-purpose language such as Java won't really put you in a position to later abandon the SMART UI, so if you've chosen that path, you should choose development tools geared to it. Don't bother hedging your bet. Just using a flexible language doesn't create a flexible system, but it may well produce an expensive one.

> *If the architecture isolates the domain-related code in a way that allows a cohesive domain design loosely coupled to the rest of the system, then that architecture can probably support domain-driven design*

## Chapter Five. A Model Expressed in Software

Defining objects that capture concepts of the domain seems very intuitive on the surface, but serious challenges are lurking in the shades of meaning. Certain distinctions have emerged that clarify the meaning of model elements and tie into a body of design practices for carving out specific kinds of objects.

Does an object represent something with continuity and identity—something that is tracked through different states or even across different implementations? Or is it an attribute that describes the state of something else? This is the basic distinction between an ENTITY and a VALUE OBJECT . Defining objects that clearly follow one pattern or the other makes the objects less ambiguous and lays out the path toward specific choices for robust design.

### Associations

The interaction between modeling and implementation is particularly tricky with the associations between objects.

For every traversable association in the model, there is a mechanism in the software with the same properties.
A model that shows an association between a customer and a sales representative corresponds to two things. On one hand, it abstracts a relationship developers deemed relevant between two real people. On the other hand, it corresponds to an object pointer between two Java objects, or an encapsulation of a database lookup, or some comparable implementation

There are at least three ways of making associations more tractable.
1. Imposing a traversal direction
2. Adding a qualifier, effectively reducing multiplicity
3. Eliminating nonessential associations

It is important to constrain relationships as much as possible. A bidirectional association means that both objects can be understood only together.

Constraining the traversal direction of a many-to-many association effectively reduces its implementation to one-to-many—a much easier design.

Consistently constraining associations in ways that reflect the bias of the domain not only makes those associations more communicative and simpler to implement, it also gives significance to the remaining bidirectional associations. When the bidirectionality of a relationship is a semantic characteristic of the domain, when it's needed for application functionality, the retention of both traversal directions conveys that.

### Entities (a.k.a. Reference Objects)

Many objects are not fundamentally defined by their attributes, but rather by a thread of continuity and identity.

Object modeling tends to lead us to focus on the attributes of an object, but the fundamental concept of an ENTITY is an abstract continuity threading through a life cycle and even passing through multiple forms.

**==Some objects are not defined primarily by their attributes. They represent a thread of identity that runs through time and often across distinct representations. Sometimes such an object must be matched with another object even though attributes differ. An object must be distinguished from other objects even though they might have the same attributes. Mistaken identity can lead to data corruption.==**

**==An object defined primarily by its identity is called an ENTITY . ENTITIES have special modeling and design considerations. They have life cycles that can radically change their form and content, but a thread of continuity must be maintained. Their identities must be defined so that they can be effectively tracked. Their class definitions, responsibilities, attributes, and associations should revolve around who they are, rather than the particular attributes they carry.==**

An ENTITY is anything that has continuity through a life cycle and distinctions independent of attributes that are important to the application's user. It could be a person, a city, a car, a lottery ticket, or a bank transaction.

**==When an object is distinguished by its identity, rather than its attributes, make this primary to its definition in the model. Keep the class definition simple and focused on life cycle continuity and identity. Define a means of distinguishing each object regardless of its form or history. Be alert to requirements that call for matching objects by attributes. Define an operation that is guaranteed to produce a unique result for each object, possibly by attaching a symbol that is guaranteed unique. This means of identification may come from the outside, or it may be an arbitrary identifier created by and for the system, but it must correspond to the identity distinctions in the model. The model must define what it means to be the same thing.==**

**Modeling ENTITIES**

the most basic responsibility of ENTITIES is to establish continuity so that behavior can be clear and predictable. They do this best if they are kept spare. Rather than focusing on the attributes or even the behavior, strip the ENTITY object's definition down to the most intrinsic characteristics, particularly those that identify it or are commonly used to find or match it. Add only behavior that is essential to the concept and attributes that are required by that behavior. Beyond that, look to remove behavior and attributes into other objects associated with the core ENTITY

![[Pasted image 20250718210701.png]]

**Designing the Identity Operation**

Each ENTITY must have an operational way of establishing its identity with another object—distinguishable even from another object with the same descriptive attributes. An identifying attribute must be guaranteed to be unique within the system however that system is defined—even if distributed, even when objects are archived.

### Value Objects

Many objects have no conceptual identity. These objects describe some characteristic of a thing.

the most conspicuous objects in a model are usually ENTITIES , and because it is so important to track each ENTITY 's identity, it is natural to consider assigning an identity to all domain objects. Indeed, some frameworks assign a unique ID to every object

**==Tracking the identity of ENTITIES is essential, but attaching identity to other objects can hurt system performance, add analytical work, and muddle the model by making all objects look the same.**==
==**Software design is a constant battle with complexity. We must make distinctions so that special handling is applied only where necessary.**==

==**However, if we think of this category of object as just the absence of identity, we haven't added much to our toolbox or vocabulary. In fact, these objects have characteristics of their own and their own significance to the model. These are the objects that describe things.**==

==**An object that represents a descriptive aspect of the domain with no conceptual identity is called a VALUE OBJECT . V ALUE OBJECTS are instantiated to represent elements of the design that we care about only for what they are, not who or which they are.==**

V ALUE OBJECTS are often passed as parameters in messages between objects. They are frequently transient, created for an operation and then discarded. V ALUE OBJECTS are used as attributes of ENTITIES (and other VALUES ). A person may be modeled as an ENTITY with an identity, but that person's name is a VALUE .

**==When you care only about the attributes of an element of the model, classify it as a VALUE OBJECT . Make it express the meaning of the attributes it conveys and give it related functionality. Treat the VALUE OBJECT as immutable. Don't give it any identity and avoid the design complexities necessary to maintain ENTITIES==**

![[Pasted image 20250718211024.png]]

**Designing VALUE OBJECTS**

We don't care which instance we have of a VALUE OBJECT . This lack of constraints gives us design freedom we can use to simplify the design or optimize performance. This involves making choices about copying, sharing, and immutability.

Sharing is best restricted to those cases in which it is most valuable and least troublesome:
- When saving space or object count in the database is critical
 - When communication overhead is low (such as in a centralized server)
 - When the shared object is strictly immutable

As long as a VALUE OBJECT is immutable, change management is simple—there isn't any change except full replacement. Immutable objects can be freely shared, as in the electrical outlet example. If garbage collection is reliable, deletion is just a matter of dropping all references to the object. When a VALUE OBJECT is designated immutable in the design, developers are free to make decisions about issues such as copying and sharing on a purely technical basis, secure in the knowledge that the application does not rely on particular instances of the object

Defining VALUE OBJECTS and designating them as immutable is a case of following a general rule: Avoiding unnecessary constraints in a model leaves developers free to do purely technical performance tuning. Explicitly defining the essential constraints lets developers tweak the design while keeping safe from changing meaningful behavior. Such design tweaks are often very specific to the technology in use on a particular project.

### Services

There are important domain operations that can't find a natural home in an ENTITY or VALUE OBJECT . Some of these are intrinsically activities or actions, not things, but since our modeling paradigm is objects, we try to fit them into objects anyway.

when we force an operation into an object that doesn't fit the object's definition, the object loses its conceptual clarity and becomes hard to understand or refactor. Complex operations can easily swamp a simple object, obscuring its role. And because these operations often draw together many domain objects, coordinating them and putting them into action, the added responsibility will create dependencies on all those objects, tangling concepts that could be understood independently.

**==Some concepts from the domain aren't natural to model as objects. Forcing the required domain functionality to be the responsibility of an ENTITY or VALUE either distorts the definition of a model-based object or adds meaningless artificial objects.==**

A SERVICE is an operation offered as an interface that stands alone in the model, without encapsulating state, as ENTITIES and VALUE OBJECTS do. S ERVICES are a common pattern in technical frameworks, but they can also apply in the domain layer.

SERVICES should be used judiciously and not allowed to strip the ENTITIES and VALUE OBJECTS of all their behavior. But when an operation is actually an important domain concept, a SERVICE forms a natural part of a MODEL-DRIVEN DESIGN . Declared in the model as a SERVICE, rather than as a phony object that doesn't actually represent anything, the standalone operation will not mislead anyone.
A good SERVICE has three characteristics.
1. The operation relates to a domain concept that is not a natural part of an ENTITY or VALUE OBJECT .
2. The interface is defined in terms of other elements of the domain model.
3. The operation is stateless.

**==When a significant process or transformation in the domain is not a natural responsibility of an ENTITY or VALUE OBJECT , add an operation to the model as a standalone interface declared as a SERVICE . Define the interface in terms of the language of the model and make sure the operation name is part of the UBIQUITOUS LANGUAGE . Make the SERVICE stateless.==**

### Modules

The MODULES in the domain layer should emerge as a meaningful part of the model, telling the story of the domain on a larger scale

**==Everyone uses MODULES , but few treat them as a full-fledged part of the model. Code gets broken down into all sorts of categories, from aspects of the technical architecture to developers' work assignments. Even developers who refactor a lot tend to content themselves with MODULES conceived early in the project.**==

==**It is a truism that there should be low coupling between MODULES and high cohesion within them. Explanations of coupling and cohesion tend to make them sound like technical metrics, to be judged mechanically based on the distributions of associations and interactions. Yet it isn't just code being divided into MODULES , but concepts. There is a limit to how many things a person can think about at once (hence low coupling). Incoherent fragments of ideas are as hard to understand as an undifferentiated soup of ideas (hence high cohesion).==**

Whenever two model elements are separated into different modules, the relationships between them become less direct than they were, which increases the overhead of understanding their place in the design. Low coupling between MODULES minimizes this cost, and makes it possible to analyze the contents of one MODULE with a minimum of reference to others that interact

At the same time, the elements of a good model have synergy, and well-chosen MODULES bring
together elements of the model with particularly rich conceptual relationships. This high cohesion of objects with related responsibilities allows modeling and design work to concentrate within a single MODULE , a scale of complexity a human mind can easily handle.

**==Choose MODULES that tell the story of the system and contain a cohesive set of concepts. This often yields low coupling between MODULES , but if it doesn't, look for a way to change the model to disentangle the concepts, or search for an overlooked concept that might be the basis of a MODULE that would bring the elements together in a meaningful way. Seek low coupling in the sense of concepts that can be understood and reasoned about independently of each other. Refine the model until it partitions according to highlevel domain concepts and the corresponding code is decoupled as well.**==

==**Give the MODULES names that become part of the UBIQUITOUS LANGUAGE . MODULES and their names should reflect insight into the domain.==**

## Chapter Six. The Life Cycle of a Domain Object

![[Pasted image 20250718220731.png]]

1. Maintaining integrity throughout the life cycle
2. Preventing the model from getting swamped by the complexity of managing the life cycle

### Aggregates

Minimalist design of associations helps simplify traversal and limit the explosion of relationships somewhat, but most business domains are so interconnected that we still end up tracing long, deep paths through object references. In a way, this tangle reflects the realities of the world, which seldom obliges us with sharp boundaries. It is a problem in a software design.

Say you were deleting a Person object from a database. Along with the person go a name, birth date, and job description. But what about the address? There could be other people at the same address. If you delete the address, those Person objects will have references to a deleted object. If you leave it, you accumulate junk addresses in the database. Automatic garbage collection could eliminate the junk addresses, but that technical fix, even if available in your database system, ignores a basic modeling issue.

Even when considering an isolated transaction, the web of relationships in a typical object model gives no clear limit to the potential effect of a change. It is not practical to refresh every object in the system, just in case there is some dependency.

The problem is acute in a system with concurrent access to the same objects by multiple clients. With many users consulting and updating different objects in the system, we have to prevent simultaneous changes to interdependent objects. Getting the scope wrong has serious consequences.

**==It is difficult to guarantee the consistency of changes to objects in a model with complex associations. Invariants need to be maintained that apply to closely related groups of objects, not just discrete objects. Yet cautious locking schemes cause multiple users to interfere pointlessly with each other and make a system unusable==**

Put another way, how do we know where an object made up of other objects begins and ends? In any system with persistent storage of data, there must be a scope for a transaction that changes data, and a way of maintaining the consistency of the data (that is, maintaining its invariants). Databases allow various locking schemes, and tests can be programmed. But these ad hoc solutions divert attention away from the model, and soon you are back to hacking and hoping.

Schemes have been developed for defining ownership relationships in the model. The following simple but rigorous system, distilled from those concepts, includes a set of rules for implementing transactions that modify the objects and their owners 

**==First we need an abstraction for encapsulating references within the model. An AGGREGATE is a cluster of associated objects that we treat as a unit for the purpose of data changes. Each AGGREGATE has a root and a boundary. The boundary defines what is inside the AGGREGATE . The root is a single, specific ENTITY contained in the AGGREGATE . The root is the only member of the AGGREGATE that outside objects are allowed to hold references to, although objects within the boundary may hold references to each other. ENTITIES other than the root have local identity, but that identity needs to be distinguishable only within the AGGREGATE , because no outside object can ever see it out of the context of the root ENTITY==**

![[Pasted image 20250718220935.png]]

![[Pasted image 20250718220950.png]]

To translate the conceptual **AGGREGATE** into an implementation, the following rules should be applied to all transactions, based on the provided description, formatted as markdown bullet points:

- **Root Entity Responsibility**: The root **ENTITY** has global identity and is responsible for enforcing all invariants across the **AGGREGATE**.
- **Entity Identity**: 
  - Root **ENTITIES** possess global identity, unique across the system.
  - **ENTITIES** within the **AGGREGATE** boundary have local identity, unique only within that **AGGREGATE**.
- **Reference Restrictions**:
  - External objects cannot hold references to any internal **ENTITIES** except the root **ENTITY**.
  - The root **ENTITY** may pass references to internal **ENTITIES** to external objects, but these references must be used transiently and not persisted.
  - The root **ENTITY** can pass copies of **VALUE OBJECTS** to external objects, which can be used freely since they are immutable and disconnected from the **AGGREGATE**.
- **Database Access**: Only **AGGREGATE** roots can be retrieved directly via database queries; all other internal objects must be accessed through traversal of associations from the root.
- **Cross-Aggregate References**: Objects within an **AGGREGATE** can hold references to other **AGGREGATE** roots.
- **Deletion Rule**: A delete operation must remove the entire **AGGREGATE** (all objects within its boundary) in a single operation. With garbage collection, deleting the root ensures all internal objects are collected, as no external references exist except to the root.
- **Invariant Enforcement**: When any change is committed within the **AGGREGATE** boundary, all invariants of the entire **AGGREGATE** must be satisfied.

**==Cluster the ENTITIES and VALUE OBJECTS into AGGREGATES and define boundaries around each. Choose one ENTITY to be the root of each AGGREGATE , and control all access to the objects inside the boundary through the root. Allow external objects to hold references to the root only. Transient references to internal members can be passed out for use within a single operation only. Because the root controls access, it cannot be blindsided by changes to the internals. This arrangement makes it practical to enforce all invariants for objects in the AGGREGATE and for the AGGREGATE as a whole in any state change==**

### Factories

An object should be distilled until nothing remains that does not relate to its meaning or support its role in interactions. This mid-life cycle responsibility is plenty. Problems arise from overloading a complex object with responsibility for its own creation 

**==Creation of an object can be a major operation in itself, but complex assembly operations do not fit the responsibility of the created objects. Combining such responsibilities can produce ungainly designs that are hard to understand. Making the client direct construction muddies the design of the client, breaches encapsulation of the assembled object or AGGREGATE , and overly couples the client to the implementation of the created object.==**

**==Shift the responsibility for creating instances of complex objects and AGGREGATES to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design. Provide an interface that encapsulates all complex assembly and that does not require the client to reference the concrete classes of the objects being instantiated. Create entire AGGREGATES as a piece, enforcing their invariants==**

The two basic requirements for any good FACTORY are
1. Each creation method is atomic and enforces all invariants of the created object or AGGREGATE . A FACTORY should only be able to produce an object in a consistent state. For an ENTITY, this means the creation of the entire AGGREGATE , with all invariants satisfied, but probably with optional elements still to be added. For an immutable VALUE OBJECT , this means that all attributes are initialized to their correct final state. If the interface makes it possible to request an object that can't be created correctly, then an exception should be raised or some other mechanism should be invoked that will ensure that no improper return value is possible.
2. The FACTORY should be abstracted to the type desired, rather than the concrete class(es) created. The sophisticated FACTORY patterns in Gamma et al. 1995 help with this.

### Repositories

To do anything with an object, you have to hold a reference to it. How do you get that reference? One way is to create the object, as the creation operation will return a reference to the new object. A second way is to traverse an association. You start with an object you already know and ask it for an associated object. Any object-oriented program is going to do a lot of this, and these links give object models much of their expressive power. But you have to get that first object.

**==A client needs a practical means of acquiring references to preexisting domain objects. If the infrastructure makes it easy to do so, the developers of the client may add more traversable associations, muddling the model. On the other hand, they may use queries to pull the exact data they need from the database, or to pull a few specific objects rather than navigating from AGGREGATE roots. Domain logic moves into queries and client code, and the ENTITIES and VALUE OBJECTS become mere data containers. The sheer technical complexity of applying most database access infrastructure quickly swamps the client code, which leads developers to dumb down the domain layer, which makes the model irrelevant.==**

**==A subset of persistent objects must be globally accessible through a search based on object attributes. Such access is needed for the roots of AGGREGATES that are not convenient to reach by traversal. They are usually ENTITIES , sometimes VALUE OBJECTS with complex internal structure, and sometimes enumerated VALUES . Providing access to other objects muddies important distinctions. Free database queries can actually breach the encapsulation of domain objects and AGGREGATES . Exposure of technical infrastructure and database access mechanisms complicates the client and obscures the MODEL-DRIVEN DESIGN.==**

**==For each type of object that needs global access, create an object that can provide the illusion of an in-memory collection of all objects of that type. Set up access through a well-known global interface. Provide methods to add and remove objects, which will encapsulate the actual insertion or removal of data in the data store. Provide methods that select objects based on some criteria and return fully instantiated objects or collections of objects whose attribute values meet the criteria, thereby encapsulating the actual storage and query technology. Provide REPOSITORIES only for AGGREGATE roots that actually need direct access. Keep the client focused on the model, delegating all object storage and access to the REPOSITORIES .==**


REPOSITORIES have many advantages, including the following:

- They present clients with a simple model for obtaining persistent objects and managing their life cycle.
- They decouple application and domain design from persistence technology, multiple database strategies, or even multiple data sources.
- They communicate design decisions about object access.
- They allow easy substitution of a dummy implementation, for use in testing (typically using an in-memory collection).


# Part III: Refactoring Toward Deeper Insight

### Levels of Refactoring

The refactorings that have the greatest impact on the viability of the system are those motivated by new insights into the domain or those that clarify the model's expression through the code

Executing a refactoring based on domain insight often involves a series of micro-refactorings, but the motivation is not just the state of the code. Rather, the micro-refactorings provide convenient units of change toward a more insightful model. The goal is that not only can a developer understand what the code does; he or she can also understand why it does what it does and can relate that to the ongoing communication with the domain experts.

### Deep Models

The traditional way of explaining object analysis involves identifying nouns and verbs in the requirements documents and using them as the initial objects and methods. This explanation is recognized as an oversimplification that can be useful for teaching object modeling to beginners. The truth is, though, that initial models usually are naive and superficial, based on shallow knowledge.

> *A deep model provides a lucid expression of the primary concerns of the domain experts and their most relevant knowledge while it sloughs off the superficial aspects of the domain.*

## Chapter Eight. Breakthrough

![[Pasted image 20250720133003.png]]

The returns from refactoring are not linear. Usually there is a marginal return for a small effort, and the small improvements add up. They fight entropy, and they are the frontline protection against a fossilized legacy. But some of the most important insights come abruptly and send a shock through the project.

Don't become paralyzed trying to bring about a breakthrough. The possibility usually comes after many modest refactorings. Most of the time is spent making piecemeal improvements, with model insights emerging gradually during each successive refinement

## Chapter Nine. Making Implicit Concepts Explicit

**==Many transformations of domain models and the corresponding code happen when developers recognize a concept that has been hinted at in discussion or present implicitly in the design, and they then represent it explicitly in the model with one or more objects or relationships.==**

### Digging Out Concepts

**==Listen to the language the domain experts use. Are there terms that succinctly state something complicated? Are they correcting your word choice (perhaps diplomatically)? Do the puzzled looks on their faces go away when you use a particular phrase? These are hints of a concept that might benefit the model.==**

The UBIQUITOUS LANGUAGE is made up of the vocabulary that pervades speech, documents, model diagrams, and even code. If a term is absent from the design, it is an opportunity to improve the model and design by including it.

### Specification

In all kinds of applications, Boolean test methods appear that are really parts of little rules. As long as they are simple, we handle them with testing methods, such as ``anIterator.hasNext()`` or ``anInvoice.isOverdue()`` . In an Invoice class, the code in ``isOverdue()`` is an algorithm that evaluates a rule. For example,

```java
public boolean isOverdue() {Date currentDate = new Date();return currentDate.after(dueDate);}
```

**==Business rules often do not fit the responsibility of any of the obvious ENTITIES or VALUE OBJECTS , and their variety and combinations can overwhelm the basic meaning of the domain object. But moving the rules out of the domain layer is even worse, since the domain code no longer expresses the model.**==
==**Logic programming provides the concept of separate, combinable, rule objects called "predicates," but full implementation of this concept with objects is cumbersome. It is also so general that it doesn't communicate intent as much as more specialized designs.==**

Fortunately, we don't really need to fully implement logic programming to get a large benefit. Most of our rules fall into a few special cases. We can borrow the concept of predicates and create specialized objects that evaluate to a Boolean. Those testing methods that get out of hand will neatly expand into objects of their own. They are little truth tests that can be factored out into a separate VALUE OBJECT . This new object can evaluate another object to see if the predicate is true for that object

To put it another way, the new object is a specification . A SPECIFICATION states a constraint on the state of another object, which may or may not be present. It has multiple uses, but one that conveys the most basic concept is that a SPECIFICATION can test any object to see if it satisfies the specified criteria

**==Create explicit predicate-like VALUE OBJECTS for specialized purposes. A SPECIFICATION is a predicate that determines if an object does or does not satisfy some criteria.==**

Many SPECIFICATIONS are simple, special-purpose tests, as in the delinquent invoice example. In cases where the rules are complex, the concept can be extended to allow simple specifications to be combined, just as predicates are combined with logical operators. (This technique will be discussed in the next chapter.) The fundamental pattern stays the same and provides a path from the simpler to more complex models

**Applying and Implementing SPECIFICATION**

1. To validate an object to see if it fulfills some need or is ready for some purpose
2. To select an object from a collection (as in the case of querying for overdue invoices)
3. To specify the creation of a new object to fit some need
These three uses—validation, selection, and building to order—are the same on a conceptual level. Without a pattern such as SPECIFICATION , the same rule may show up in different guises, and possibly contradictory forms. The conceptual unity can be lost. Applying the SPECIFICATION pattern allows a consistent model to be used, even when the implementation may have to diverge.

## Chapter Ten. Supple Design

Early versions of a design are usually stiff. Many never acquire any suppleness in the time frame or budget of the project. I've never seen a large program that had this quality throughout. But when complexity is holding back progress, honing the most crucial, intricate parts to a supple design makes the difference between getting sucked down into legacy maintenance and punching through the complexity ceiling.
There is no formula for designing software like this, but I have culled a set of patterns that, in my experience, tend to lend suppleness to a design when they fit. These patterns and examples should give a feel for what a supple design is like and the kind of thinking that goes into it.

![[Pasted image 20250720141915.png]]

### Intention-Revealing Interfaces

**==If a developer must consider the implementation of a component in order to use it, the value of encapsulation is lost. If someone other than the original developer must infer the purpose of an object or operation based on its implementation, that new developer may infer a purpose that the operation or class fulfills only by chance. If that was not the intent, the code may work for the moment, but the conceptual basis of the design will have been corrupted, and the two developers will be working at cross-purposes.==**

**==Name classes and operations to describe their effect and purpose, without reference to the means by which they do what they promise. This relieves the client developer of the need to understand the internals. These names should conform to the UBIQUITOUS LANGUAGE so that team members can quickly infer their meaning. Write a test for a behavior before creating it, to force your thinking into client developer mode.==**

### Side -Effect-Free Functions

**==Interactions of multiple rules or compositions of calculations become extremely difficult to predict. The developer calling an operation must understand its implementation and the implementation of all its delegations in order to anticipate the result. The usefulness of any abstraction of interfaces is limited if the developers are forced to pierce the veil. Without safely predictable abstractions, the developers must limit the combinatory explosion, placing a low ceiling on the richness of behavior that is feasible to build.**==

==**Place as much of the logic of the program as possible into functions, operations that return results with no observable side effects. Strictly segregate commands (methods that result in modifications to observable state) into very simple operations that do not return domain information. Further control side effects by moving complex logic into VALUE OBJECTS when a concept fitting the responsibility presents itself.==**

### Assertions

Separating complex computations into SIDE-EFFECT-FREE FUNCTIONS cuts the problem down to size, but there is still a residue of commands on the ENTITIES that produce side effects, and anyone using them must understand their consequences. A SSERTIONS make side effects explicit and easier to deal with.

**==When the side effects of operations are only defined implicitly by their implementation, designs with a lot of delegation become a tangle of cause and effect. The only way to understand a program is to trace execution through branching paths. The value of encapsulation is lost. The necessity of tracing concrete execution defeats abstraction.==**

**==State post-conditions of operations and invariants of classes and AGGREGATES . If ASSERTIONS cannot be coded directly in your programming language, write automated unit tests for them. Write them into documentation or diagrams where it fits the style of the project's development process.**==
==**Seek models with coherent sets of concepts, which lead a developer to infer the intended ASSERTIONS , accelerating the learning curve and reducing the risk of contradictory code.==**

Clearly stated invariants and pre- and post-conditions allow a developer to understand the consequences of using an operation or object. Theoretically, any noncontradictory set of assertions would work. But humans don't just compile predicates in their heads. They will be extrapolating and interpolating the concepts of the model, so it is important to find models that make sense to people as well as satisfying the needs of the application.

### Conceptual Contours

**==When elements of a model or design are embedded in a monolithic construct, their functionality gets duplicated. The external interface doesn't say everything a client might care about. Their meaning is hard to understand, because different concepts are mixed together.**==

==**On the other hand, breaking down classes and methods can pointlessly complicate the client, forcing client objects to understand how tiny pieces fit together. Worse, a concept can be lost completely. Half of a uranium atom is not uranium. And of course, it isn't just grain size that counts, but just where the grain runs.==**

**==Decompose design elements (operations, interfaces, classes, and AGGREGATES ) into cohesive units, taking into consideration your intuition of the important divisions in the domain. Observe the axes of change and stability through successive refactorings and look for the underlying CONCEPTUAL CONTOURS that explain these shearing patterns. Align the model with the consistent aspects of the domain that make it a viable area of knowledge in the first place.==**

The goal is a simple set of interfaces that combine logically to make sensible statements in the UBIQUITOUS LANGUAGE , and without the distraction and maintenance burden of irrelevant options. This is typically an outcome of refactoring: it's hard to produce up front. But it may never emerge from technically oriented refactoring; it emerges from refactoring toward deeper insight.
### Standalone Classes
Interdependencies make models and designs hard to understand. They also make them hard to test and maintain. And interdependencies pile up easily

**==Even within a MODULE , the difficulty of interpreting a design increases wildly as dependencies are added. This adds to mental overload, limiting the design complexity a developer can handle. Implicit concepts contribute to this load even more than explicit references.==**

**==Low coupling is fundamental to object design. When you can, go all the way. Eliminate all other concepts from the picture. Then the class will be completely self-contained and can be studied and understood alone. Every such self-contained class significantly eases the burden of understanding a MODULE .==**

### Closure of Operations

> If we take two real numbers and multiply them together, we get another real number. [The real numbers are all the rational numbers and all the irrational numbers.] Because this is always true, we say that the real numbers are "closed under the operation of multiplication": there is no way to escape the set. When you combine any two elements of the set, the result is also included in the set.

**==Most interesting objects end up doing things that can't be characterized by primitives alone.**==

==**Where it fits, define an operation whose return type is the same as the type of its argument(s). If the implementer has state that is used in the computation, then the implementer is effectively an argument of the operation, so the argument(s) and return value should be of the same type as the implementer. Such an operation is closed under the set of instances of that type. A closed operation provides a high-level interface without introducing any dependency on other concepts.==**

## Chapter Eleven. Applying Analysis Patterns

> In Analysis Patterns: Reusable Object Models , Martin Fowler defined his patterns this way:
Analysis patterns are groups of concepts that represent a common construction in business modeling. It may be relevant to only one domain or it may span many domains.

The analysis patterns Fowler presents arose from experience in the field, and so they are practical, in the right situation. Such patterns provide someone facing a challenging domain with very valuable starting points for their iterative development process. The name emphasizes their conceptual nature. Analysis patterns are not technological solutions; they are guides to help you work out a model in a particular domain

## Chapter Twelve. Relating Design Patterns to the Model

Point of view affects one's interpretation of what is and isn't a pattern. One person's pattern can be another person's primitive building block. For this book we have concentrated on patterns at a certain level of abstraction. Design patterns are not about designs such as linked lists and hash tables that can be encoded in classes and reused as is. Nor are they complex, domain-specific designs for an entire application or subsystem. The design patterns in this book are descriptions of communicating objects and classes that are customized to solve a general design problem in a particular context

## Chapter Thirteen. Refactoring Toward Deeper Insight

Refactoring toward deeper insight is a multifaceted process. It will be helpful to stop for a moment to pull together the major points. There are three things you have to focus on.
1. Live in the domain.
2. Keep looking at things a different way.
3. Maintain an unbroken dialog with domain experts.

### Initiation

Refactoring toward deeper insight can begin in many ways. It may be a response to a problem in the code—some complexity or awkwardness. Rather than apply a standard transformation of the code, the developers sense that the root of the problem is in the domain model. Perhaps a concept is missing. Maybe some relationship is wrong.

### Exploration Teams

There are a few keys to keeping this process productive.

- Self-determination . A small team can be assembled on the fly to explore a design problem. The team can operate for a few days and then disband. There is no need for long-term, elaborate organizational structures.
- Scope and sleep . Two or three short meetings spaced out over a few days should produce a design worth trying. Dragging it out doesn't help. If you get stuck, you may be taking on too much at once. Pick a smaller aspect of the design and focus on that.
 - Exercising the UBIQUITOUS LANGUAGE . Involving the other team members—particularly the subject matter expert—in the brain-storming session creates an opportunity to exercise and refine the UBIQUITOUS LANGUAGE . The end result of the effort is a refinement of that LANGUAGE which the original developer(s) will take back and formalize in code.