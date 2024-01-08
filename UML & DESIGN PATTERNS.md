# UML (Unified Modeling Language)

UML (Unified Modeling Language) is a modeling language used for software and system design. It serves as a common ground for different stakeholders approaching the same system from various perspectives, such as use case, class-object diagram, and deployment diagrams.

**Modeling:** The process of creating a simplified representation or abstraction of a system or concept to understand, analyze, or communicate, particularly in the context of software development.

## Advantages of UML

1. **Improved Communication:**
   - UML provides a common language and notation for software developers, designers, and stakeholders, reducing misunderstandings and enhancing collaboration.

2. **Better Visualization:**
   - UML allows designers to create visual models of software systems, making it easier to understand and identify design flaws.

3. **Improved Design:**
   - By offering a standard way to describe software architecture, components, and interactions, UML facilitates the creation of better-designed systems, identifying potential issues early.

4. **Reusability:**
   - UML models can be reused across different projects, as they are not tied to any specific programming language or platform.

5. **Testability:**
   - UML models aid in creating test plans and cases, verifying the functionality and performance of software systems.

## Extendable Values

- **Extendable Values:**
  - Used to determine options for a property or value and make them expandable for the future. These values can define a list or options for an object or property in a model.

- **Stereotype << >>:**
  - A mechanism to extend the semantics of a modeling element beyond its standard definition. Stereotypes can create new modeling elements specific to a domain or modify properties of existing elements.

    - Example: `<<singleton>>`, `<<payment>>`

- **Constraint {}:**
  - A condition or set of conditions that must be satisfied by a modeling element. Constraints specify business rules, validation rules, or other conditions for correct system functioning.

    - Example: Specify that an attribute must be unique within a collection of objects.

- **Tagged Value:**
  - A mechanism to add additional information to a modeling element, often used to specify properties not part of standard UML elements.

    - Example: Specify the author of a class, provide a brief description of its purpose, or mention the implementation language or associated database table.


# Use Case Diagram

A use case diagram is a type of UML diagram used to model interactions between a system and its users or external systems. It provides a high-level view of the system, depicting actors (users or external systems) and the use cases (functions or processes) the system offers to these actors.

- **Boundary:** Represented by a rectangle containing use cases, it signifies the system's boundary, defining its scope.

- **Actor:** Represents a user or an external system interacting with the modeled system. Actors can be human users, software systems, hardware devices, or other entities interacting with the system.

- **Use Case:** Describes specific functionality or behavior the system provides to actors, outlining the steps taken to achieve a particular goal or task.

When determining use cases, two fundamental questions are asked:
1. What actions are performed in the system? (Use cases)
2. Who performs these actions? (Actors)

Actors are not necessarily associated with the entire system.

**Functional Requirements:** Describe what a system must accomplish to fulfill its purpose.

**Non-Functional Requirements:** Describe how the system should perform in terms of quality attributes such as performance, usability, reliability, security, and maintainability.

Expectations should be detailed and itemized during business analysis.

Relationships:
- Association between actors: Association
- Relationships between use cases: Dependency

**Narrative:** A written description of the use case providing a detailed explanation of interactions between actors and the system. It should be free from technical details.

**Assumption:** Statements about the environment or context in which the use case operates. Used to clarify uncertainties, establishing conditions under which the use case is valid.

When naming:
- Names: Represent classes.
- Verbs: Indicate functions.
- Adjectives: Denote properties.

# Business Process Model

A business process model is a visual representation of a business process illustrating the flow of tasks, data, and activities from one step to another. Workflow charts provide stakeholders with a clear view of a process, enabling the identification of inefficiencies, redundancies, and potential issues affecting productivity, quality, and customer satisfaction.

- **Activity:** A generic term for a task or work in a business process. It can be performed by humans or systems and can be broken down into smaller activities or tasks.

- **Action:** A specific type of activity representing a single step or operation within a process. It provides a granular representation of work, showing detailed interactions between participants or systems in a process.

The distinction between "activity" and "action" lies in the scope, with "activity" referring to the entire process and "action" denoting a specific action within that process.

- **Merge and Decision:** Differentiated based on entry and exit points and quantities. "Merge" has multiple inputs and a single output, while "Decision" has a single input and multiple outputs.

- **Fork:** A gateway used to split a single flow into multiple parallel flows. Represented by a horizontal bar with one incoming flow and multiple outgoing flows.

- **Join:** A gateway used to synchronize parallel flows into a single flow. Represented by a horizontal bar with multiple incoming flows and one outgoing flow.

- **Object:** Represents an entity or data object processed during an activity. These objects are used or produced by an activity within the workflow process.

- **Send/Receive:** Symbols representing communication between different elements or participants in the workflow. They illustrate information flow, such as sending a notification or receiving an approval.

- **Partition:** A graphical element used to group related activities or steps within the workflow. Represented as horizontal or vertical lines, partitions divide the diagram into sections, each indicating a different grouping of activities. Grouping activities helps highlight different phases or stages of the workflow and facilitates the identification of related activities.


# Class Diagram 

A class diagram is a UML diagram that illustrates the structure of a system by showcasing classes, attributes, methods, and relationships between these classes.

- **Attribute (Data Members or Variables):** Represents the properties or characteristics of an object.

- **Operation (Functions):** Depicts the actions that an object can perform or its behavior.

- **Package:** Denoted as `com.denizogut` within the class diagram.

- **Association:** Represents a relationship between two classes, indicating a connection or dependency. It holds references between classes.

  - **Bi-Directional Association:** Each class has a reference to the other, enabling communication in both directions.

  - **Self-Associate (Self-Reference):** An association between a class and itself, often used for a "singleton" class.

- **Cardinality:** Defines the number of instances of one class associated with instances of another class. Symbolized by "0..1," "*", or "1."

- **Qualified Association:** Adds a qualifier or condition for objects to be associated, often based on a property or attribute.

- **Aggregation:** Represents a relationship where one object is composed of one or more other objects, having a "has-a" relationship.

  - *Example:* A "Car" class aggregating "Wheel" class.

- **Composition:** A stronger form of aggregation where the contained objects cannot exist without the container object, having a "part-of" relationship.

  - *Example:* A "Car" class composing an "Engine" class.

  - *Difference:* Aggregation allows independent existence of contained objects, while composition indicates a dependency.

- **Generalization (Inheritance):** Allows a class to inherit properties, methods, and characteristics from a parent or superclass.

- **Realization (Interface):** Represents a relationship between a class and an interface, where the class agrees to implement methods specified by the interface.

- **Dependency:** A relationship where one class (client) depends on another class (supplier), signifying that changes to the supplier may affect the client.

- **Usage:** A strong relationship between two classes, indicating that one class uses the functionality of another class in a specific way.

  - *Example:* "ShoppingCart" class using the "Product" class for tracking items.

These relationships and elements in a class diagram help model and understand the structure and dependencies within a system.

# State Diagrams 

State diagrams are UML diagrams that illustrate the behavior of a system or process over time, showcasing different states and transitions based on inputs or events.

- **State:** Represents a condition or mode in which a system or process exists at a specific time, including variables, inputs, outputs, and ongoing operations. States can be transient (short-lived) or persistent (lasting until a specific condition triggers a transition).

- **State Machine:** A mathematical model capturing system behavior with states and transitions. It consists of:
  - A set of states representing distinct conditions or modes.
  - Transitions describing how the system moves between states in response to events or stimuli.
  - Transitions triggered by events or conditions, with associated actions or outputs.

- **Initial State:** The state in which the system or process starts or initializes.

- **Final State:** Represents the end or completion of the modeled system or process.

- **Multiple Final States:** A state machine may have multiple final states, each denoting a different outcome or result. Transitions leading to final states may trigger associated actions or outputs.

- **Transition:** Describes the change from one state to another based on events or conditions. It may have associated actions or outputs.

- **Output/Action:** Actions or outputs associated with transitions or final states, depicting activities performed when the system reaches a particular state.

State diagrams are widely used in software development to enhance understanding and visualization of system behavior. They are effective in modeling complex systems, hardware, and business processes.

# Sequence Diagrams 

Sequence diagrams, a type of Unified Modeling Language (UML) diagram, are used to depict the behavior of a system or component by illustrating how objects interact over time. They are especially valuable for modeling scenarios involving sequential events, like business processes, software programs, or communication protocols.

## Key Elements:

- **Lifelines:** Represent objects or components participating in the interaction. Each lifeline extends vertically to indicate their existence over time during the interaction.

- **Messages:** Symbolize interactions or communications between lifelines. Messages demonstrate the flow of information between objects or components.

- **Objects:** Instances of a class or component involved in the interaction. Objects are represented by lifelines.

- **Return Messages:** Indicate the response of an object or component to a preceding message, showcasing the order of interactions.

- **Self-Interaction:** Depicts a message sent by an object to itself, reflecting internal processes or actions within an individual object.

## Benefits:

- **Flow Visualization:** Clearly and concisely visualizes how different components or objects interact to achieve a specific task or process.

- **Message Order:** Illustrates the order in which messages are exchanged between lifelines, aiding in the understanding of the sequence of events.

- **Scenario Modeling:** Particularly useful for modeling scenarios involving a sequence of events or steps.

Sequence diagrams provide a powerful tool for system developers to comprehend and communicate the dynamic behavior of a system, enhancing the overall understanding of complex processes.

# Communication Diagrams 

Communication diagrams, a type of Unified Modeling Language (UML) diagram, are employed to elucidate the interactions among objects or components in a system or process. These diagrams provide a visual depiction of the relationships between objects, showcasing their communication and collaboration towards a specific task or goal. Communication diagrams are especially beneficial for modeling systems with numerous interacting objects or components.

## Key Components:

- **Objects:** Instances of classes or components involved in the communication. Each object represents a participant in the interaction.

- **Messages:** Symbolize the communications or interactions occurring between objects or components. Messages illustrate the flow of information or actions.

- **Links:** Represent the relationships between objects or components, depicting how they are connected or associated.

- **Roles:** Signify the various roles that an object or component may assume during the interaction, offering insights into their functions.

## Benefits:

- **Relationship Visualization:** Clearly illustrates how objects or components relate to each other and collaborate in achieving specific tasks.

- **Communication Flow:** Visual representation of the communication and interaction flow between objects, aiding in understanding the dynamic behavior of the system.

- **Scalability:** Particularly useful for modeling systems with a large number of interacting objects or components.

Communication diagrams serve as a valuable tool for system modeling, enhancing the understanding of interactions and relationships within a complex system.

# Component Diagrams 

Component diagrams, a type of Unified Modeling Language (UML) diagram, are utilized to model the components of a system and depict their relationships. Components, in this context, refer to modular, deployable, and replaceable parts of a system encapsulating behavior and data. These components can encompass software modules, hardware components, or even physical devices. Component diagrams facilitate the understanding of system components, their dependencies, and collaborative functioning to achieve specific functions or goals.

## Key Elements:

- **Component:** Represents a modular, deployable, and replaceable part of a system. It encapsulates both behavior and data.

- **Interface:** Represents a contract between a component and its environment. Specifies the operations a component provides or requires and the data exchanged.

- **Dependency:** Signifies a relationship where one component depends on another to provide a service or functionality.

- **Association:** Indicates a relationship where one component uses or has access to the services or functionality of another component.

- **Generalization:** Represents a relationship where one component is a specialized version of another component.

- **Package:** A grouping mechanism for components, interfaces, and other UML elements.

## Purpose and Benefits:

- **Identification of Components:** Clearly identifies and defines the components of a system.

- **Dependency Mapping:** Illustrates dependencies, interfaces, associations, and generalizations between components.

- **Collaboration Understanding:** Provides insights into how components collaborate and work together to fulfill system functions.

Component diagrams are valuable in system design, offering a comprehensive view of the components and their relationships, aiding in effective system architecture.

# Package Diagrams 

Package diagrams, part of the Unified Modeling Language (UML), serve to visualize and organize a system's structure into packages. Packages act as grouping mechanisms for UML elements like classes, components, and other packages. This organizational approach enhances system manageability and maintenance. Package diagrams illustrate packages and their relationships, including dependencies, associations, and generalizations.

## Key Elements:

- **Package:** Represents a grouping mechanism for UML elements, including classes, components, and other packages.

- **Dependency:** Signifies a relationship where one package depends on another to provide a service or functionality.

- **Association:** Represents a relationship where one package has access to the services or functionality of another package.

- **Package Import:** Denotes a relationship between a package and an element or another package in a different package.

## Purpose and Benefits:

- **Logical Grouping:** Organizes system elements into logical groups for enhanced clarity and understanding.

- **Dependency Mapping:** Illustrates dependencies, associations, and generalizations between packages.

- **System Management:** Facilitates easier management and maintenance of a system's components.

Package diagrams are instrumental in presenting an organized view of a system's structure, enabling effective management and comprehension.

# Deployment Diagrams

Deployment diagrams, another UML type, visualize the physical deployment of software artifacts onto the hardware infrastructure of a system. They showcase how software components distribute across nodes in a network, encompassing servers, routers, and other devices.

## Key Elements:

- **Node:** Represents a physical device or resource in the network, such as a server, router, or printer.

- **Artifact:** Represents a physical component of the software system, like a file, library, or executable.

- **Connectors:** Represent relationships between nodes and artifacts, including deployment, association, and dependency.

## Purpose and Benefits:

- **Physical Deployment Overview:** Provides an overview of how software artifacts are deployed on the hardware infrastructure.

- **Network Representation:** Illustrates the distribution of software components across nodes in a network.

- **System Architecture Understanding:** Enhances comprehension of the physical architecture of a software system.

Deployment diagrams aid in visualizing the deployment architecture of a system, offering insights into its physical structure and relationships.

---



# Software Design Principles and Patterns

• **Program to an interface, not an implementation.**
• **Favor object composition over class inheritance.**
• **Design for change.**

## Christopher Alexander's Wisdom

Christopher Alexander states, "Each pattern describes a problem which occurs over and over again in our environment and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice."

Design patterns aim to:
- Identify correct responsibilities using object-oriented principles.
- Distribute responsibilities to objects with a focus on cohesion and low coupling.
- Design objects with minimal dependencies between them.

## Essential Features of Software

Four essential features of software:
1. **Complexity:** Software is inherently more complex than other engineering products.
2. **Changeability:** Software undergoes frequent changes.
3. **Invisibility:** Software is intangible and invisible.
4. **Conformity:** Software must conform to other elements in its environment.

## Anemic Domain Model

An Anemic Domain Model (ADM) represents objects related to a domain that only carry data without exhibiting any behavior. This contradicts the essence of object-oriented design. The key is to combine data and process, fostering rich behavior in domain objects.

## SOLID Principles

### Single Responsibility Principle (SRP)
A class should have only one reason to change. Methods should be short, with few parameters and minimal decision-making. Complies with Dijkstra's "Separation of Concerns" principle.

### Open-Closed Principle (OCP)
Software entities should be open for extension but closed for modification. New requirements should be met through existing structures' extension.

### Liskov Substitution Principle (LSP)
Functions using base class pointers or references should be able to use derived class objects without knowing it. Inheritance should adhere to "generalization-specialization."

### Interface Segregation Principle (ISP)
Clients should not be forced to depend on interfaces they do not use. A refined form of SRP aiming at high cohesion of interfaces.

### Dependency Inversion Principle (DIP)
High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

## Law of Demeter
Objects should interact with each other through interfaces, knowing the least about each other as possible. Objects should not know the implementation details of other objects.

## GRASP (General Responsibility Assignment Software Patterns)

### Responsibilities
- **Knowing Responsibilities:**
  - Knowing about private encapsulated data.
  - Knowing about related objects.
  - Knowing about things it can derive or calculate.
- **Doing Responsibilities:**
  - Doing something itself, such as creating an object or doing a calculation.
  - Initiating action in other objects.
  - Controlling and coordinating activities in other objects.

---


# DESIGN PATTERNS

## Simplest and most common patterns

- Abstract Factory
- Factory Method
- Adapter
- Observer
- Composite
- Strategy
- Decorator
- Template Method

## CHAPTER 1

Designing object-oriented software is hard, and designing "reusable" object-oriented software is harder. Your design should be specific to the problem at hand but also general enough to address future problems and requirements.

Expert designers reuse solutions that have worked for them in the past. When they find a good solution, they use it again and again. Consequently, you'll find recurring patterns of classes and communicating objects in many object-oriented systems.

Design patterns make it easier to reuse successful designs and architectures. Design patterns help you choose design alternatives that make a system reusable and avoid alternatives that compromise reusability. Design patterns can even improve the documentation and maintenance of existing systems by furnishing an explicit specification of class and object interactions and their underlying intent.

### 1.1 What Is a Design Pattern

Each pattern describes a problem that occurs repeatedly in our environment and then describes the core of the solution to that problem in a way that you can use this solution a million times over without ever doing it the same way twice.

In general, a pattern has four essential elements:

1. The **pattern name** is a handle we can use to describe a design problem, its solutions, and consequences in a word or two. It lets us design at a higher level of abstraction and makes it easier to think about designs and to communicate them and their trade-offs to others.
    
2. The **problem** describes when to apply the pattern. It explains the problem and its context. Sometimes the problem will include a list of conditions that must be met before it makes sense to apply the pattern.
    
3. The **solution** describes the elements that make up the design, their relationships, responsibilities, and collaborations. The solution doesn't describe a particular concrete design or implementation because a pattern is like a template that can be applied in many different situations.
    
4. The **consequences** are the results and trade-offs of applying the pattern. They are critical for evaluating design alternatives and for understanding the costs and benefits of applying the pattern. The consequences for software often concern space and time trade-offs. Since reuse is often a factor in object-oriented design, the consequences of a pattern include its impact on a system's flexibility, extensibility, or portability.
    

The design patterns in this book are descriptions of communicating objects and classes that are customized to solve a general design problem in a particular context.

### 1.2 Design Patterns in Smalltalk MVC

The Model/View/Controller (MVC) triad of classes is used to build user interfaces.

MVC consists of three kinds of objects:

1. The model: is the application object.
2. The view: is its screen presentation.
3. The controller: defines the way the user interface reacts to user input.

MVC decouples them to increase flexibility and reuse. MVC decouples views and models by establishing a subscribe/notify protocol between them. A view must ensure that its appearance reflects the state of the model. Whenever the model's data changes, the model notifies views that depend on it. This approach lets you attach multiple views to the model to provide different presentations.

Another feature of MVC is that views can be nested. MVC also lets you change the way a view responds to user input without changing its visual presentation.

### 1.3 Describing Design Patterns

We describe design patterns using a consistent format.

1. **Pattern Name and Classification**: The pattern name conveys the essence of the pattern succinctly. The pattern's classification reflects the scheme.
    
2. **Intent**: A short statement that answers the following questions: "What does the design pattern do?"
    
3. **Also Known As**: Other well-known names for the pattern, if any.
    
4. **Motivation**: A scenario that illustrates a design problem and how the class and object structures in the pattern solve the problem.
    
5. **Applicability**: What are the situations in which the design patterns can be applied?
    
6. **Structure**: A graphical representation of the classes in the pattern.
    
7. **Participants**: The classes and/or objects participating in the design pattern and their responsibilities.
    
8. **Collaborations**: How the participants collaborate to carry out their responsibilities.
    
9. **Consequences**: How does the pattern support its objectives? What are the trade-offs and results of using the pattern?
    
10. **Implementation**: What pitfalls, hints, or techniques should you be aware of when implementing the pattern?
    
11. **Sample Code**: Code fragments that illustrate how you might implement the pattern in a programming language.
    
12. **Known Uses**: Examples of the pattern found in real systems.
    
13. **Related Patterns**: What design patterns are closely related to this one?
    

### 1.4 The Catalog Of Design Patterns

1. **Abstract Factory**: Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
    
2. **Adapter**: Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
    
3. **Bridge**: Decouple an abstraction from its implementation so that the two can vary independently.
    
4. **Builder**: Separate the construction of a complex object from its representation so that the same construction process can create different representations.
    
5. **Chain Of Responsibility**: Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request.
    
6. **Command**: Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.
    
7. **Composite**: Compose objects into tree structures to represent part-whole hierarchies.
    
8. **Decorator**: Attach additional responsibilities to an object dynamically.
    
9. **Facade**: Provide a unified interface to a set of interfaces in a subsystem.
    
10. **Factory Method**: Define an interface for creating an object but let subclasses decide which class to instantiate.
    
11. **Flyweight**: Use sharing to support large numbers of fine-grained objects efficiently.
    
12. **Interpreter**: Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.
    
13. **Iterator**: Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
    
14. **Mediator**: Define an object that encapsulates, captures, and externalizes an object's internal state so that the object can be restored to this state later.
    
15. **Memento**: Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.
    
16. **Observer**: Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
    
17. **Prototype**: Specify the kinds of objects to create using a prototypical instance and create new objects by copying this prototype.
    
18. **Proxy**: Provide a surrogate or placeholder for another object to control access to it.
    
19. **Singleton**: Ensure a class only has one instance and provide a global point of access to it.
    
20. **State**: Allow an object to alter its behavior when its internal state changes.
    
21. **Strategy**: Define a family of algorithms, encapsulate each one, and make them interchangeable.
    
22. **Template Method**: Define a skeleton of an algorithm in an operation, deferring some steps to subclasses.
    
23. **Visitor**: Represent an operation to be performed on the elements of an object structure.
    

### 1.5 Organizing the Catalog

The first criterion, called "purpose," reflects what a pattern does. Patterns can have either

- "creational (Concern the process of object creation),"
- "structural (Deal with the composition of classes or objects)," or
- "behavioral (Characterize the ways in which classes or objects interact and distribute responsibility)" purpose.

The second criterion called "scope" specifies whether the pattern applies primarily to classes or to objects.

Class patterns deal with relationships between classes and their subclasses. These relationships are established through inheritance, so they are static-fixed at compile-time.

Object patterns deal with object relationships, which can be changed at run-time and are more dynamic. The only patterns labeled "class patterns" are those that focus on class relationships.

### 1.6 How Design Patterns Solve Design Problems

#### Finding Appropriate Objects

An "object" includes both data and the procedures (methods) that operate on that data. An object performs an operation when it receives a "request" (or "message") from a "client."

The hard part about object-oriented design is decomposing a system into objects. The task is difficult because many factors come into play: encapsulation, granularity, dependency, flexibility, performance, evolution, reusability.

Strict modeling of the real world leads to a system that reflects today's realities but not necessarily tomorrow's. The abstractions that emerge during design are key to making a design flexible.

#### Determining Object Granularity

Objects can vary tremendously in size and number. They can represent everything down to the hardware or all the way up to entire applications. How do we decide what should be an object?

How detailed and specific the class is in describing the object's characteristics and behaviors.

#### Specifying Object Interface

Every operation declared by an object specifies the operation's name, the objects it takes as parameters, and the operation's return value. This is known as the operation's "signature." The set of all signatures defined by an object's operations is called the "interface" to the object // the set of methods that the object can perform.

A "type" is a name used to denote a particular interface. A type is a "subtype" of another if its interface contains the interface of its "supertype."

Objects are known only through their interfaces // the only way to interact with an object is through its interface, and the object's internal implementation details are hidden from the outside world. An object's interface says nothing about implementation.

When a request is sent to an object, the particular operation that's performed depends on both the request and the receiving object. The run-time association of a request to an object and one of its operations is known as "dynamic binding" // a way of connecting method calls to the code that implements them at runtime means that issuing a request doesn't commit you to a particular implementation until runtime. Dynamic binding lets you substitute objects that have identical interfaces for each other at runtime. This is known as "polymorphism."

Polymorphism simplifies the definitions of clients, decouples objects from each other, and lets them vary their relationships to each other at runtime.

Design patterns help you define interfaces by identifying their key elements and the kinds of data that get sent across an interface. A design pattern might also tell you what not to put in the interface.

Design patterns also specify relationships between interfaces.

#### Specifying Object Implementations

An object's implementation is defined by its class. Objects are created by "instantiating" a class. The object is said to be an "instance" of the class.

New classes can be defined in terms of existing classes using "class inheritance." When a "subclass" inherits from a "parent class," it includes the definitions of all the data and operations that the parent class defines.

An "abstract class" is one whose main purpose is to define a common interface for its subclasses. An abstract class can't be instantiated. The operations that an abstract class declares but doesn't implement are called "abstract operations."

Subclasses can refine and redefine behaviors of their parent classes. More specifically, a class may "override" an operation defined by its parent class.

A "mixin class" is a class that's intended to provide an optional interface or functionality to other classes. // is a way of adding additional functionality to a class without changing its inheritance hierarchy, which allows for greater flexibility and code reuse // typically implemented as an interface

## Class versus Interface Inheritance

An object's class defines how the object is implemented. The class defines the object's internal state and the implementation of its operations.

An object's type primarily refers to its interface—the set of requests to which it can respond. An object can have many types, and objects of different classes can have the same type.

When we say that an object is an instance of a class, we imply that the object supports the interface defined by the class.

### Programming to an Interface, not an Implementation

Class inheritance is basically a mechanism for extending an application's functionality by reusing functionality in parent classes.

Inheritance's ability to define families of objects with identical interfaces is crucial for polymorphism.

All classes derived from an abstract class will share its interface. A subclass merely adds or overrides operations and does not hide operations of the parent class. All subclasses can then respond to the requests in the interface of this abstract class, making them all subtypes of the abstract class.

Two benefits of manipulating objects solely in terms of the interface defined by abstract classes:

1. Clients remain unaware of the specific types of objects they use, as long as the objects adhere to the interface that clients expect.
2. Clients remain unaware of the classes that implement these objects.

Don't declare variables to be instances of particular concrete classes. Instead, commit only to an interface defined by an abstract class.

### Putting Reuse Mechanisms to Work

The challenge lies in applying OOP to build flexible, reusable software, and design patterns show you how.

#### Inheritance Versus Composition

The two most common techniques for reusing functionality in object-oriented systems are class inheritance and object composition. Reuse by subclassing is often referred to as "white-box reuse." The term "white-box" refers to visibility: the internals of parent classes are often visible to subclasses.

Object composition obtains new functionality by assembling or composing objects to get more complex functionality. This style of reuse is called "black-box reuse" because no internal details of objects are visible. Objects appear only as "black boxes."

Class inheritance is defined statically at compile-time and is straightforward to use. Class inheritance also makes it easier to modify the implementation being reused.

You can't change the implementations inherited from parent classes at run-time because inheritance is defined at compile-time. Parent classes often define at least part of their subclass's physical representation. Because inheritance exposes a subclass to details of its parent's implementation, it's often said that "inheritance breaks encapsulation."

Object composition is defined dynamically at run-time through objects acquiring references to other objects. Favoring object composition over class inheritance helps you keep each class encapsulated and focused on one task.

 Favor object composition over class inheritance
 It is based on the idea that it's often better to build new classes by combining existing objects rather than by extending existing classes.


Ideally, you shouldn't have to create new components to achieve reuse. You should be able to get all the functionality you need just by assembling existing components through object composition. Reuse by inheritance makes it easier to make new components that can be composed with old ones. Inheritance and object composition thus work together.

### Delegation

"Delegation" is a way of making composition as powerful for reuse as inheritance. You are giving someone else the responsibility to do the job for you. In delegation, two objects are involved in handling a request: a receiving object delegates operations to its "delegate."

The main advantage of delegation is that it makes it easy to compose behaviors at run-time and to change the way they are composed.

Delegation has a disadvantage. Dynamic highly parameterized software is harder to understand than more static software. There are also run-time inefficiencies, but human inefficiencies are more important in the long run.

Delegation is an extreme example of object composition. It shows that you can always replace inheritance with object composition as a mechanism for code reuse.

### Inheritance versus Parameterized Types

Another technique for reusing functionality is through "parameterized types," also known as "generics." This technique lets you define a type without specifying all the other types it uses.

There are important differences between these techniques. Object composition lets you change the behavior being composed at run-time, but it also requires indirection and can be less efficient. Inheritance lets you provide default implementations for operations and lets subclasses override them. Parameterized types let you change the types that a class can use. But neither parameterized type nor inheritance can change at run-time.

## Relating Run-Time and Compile-Time Structures

An object-oriented program's run-time structure often bears little resemblance to its code structure. The code structure is frozen at compile-time; it consists of classes in fixed inheritance relationships. Run-time structure consists of rapidly changing networks of communicating objects.

Code won't reveal everything about how a system will work. The system's run-time structure must be imposed more by the designer than the language.

### Designing for Change

To design the system so that it's robust to such changes, you must consider how the system might need to change over its lifetime. Redesign affects many parts of the software systems, and unanticipated changes are invariably expensive.

Design patterns help you avoid this by ensuring that a system can change in specific ways. Common causes of redesign along with the design patterns that address them:

1. **Creating an object by specifying a class explicitly:** Specifying a class name when you create an object commits you to a particular implementation instead of a particular interface.
    
2. **Dependence on specific operations:** When you specify a particular operation, you commit to one way of satisfying requests. By avoiding hard-coded requests, you make it easier to change the way a request gets satisfied both at compile-time and at run-time.
    
3. **Dependence on hardware and software platform:** Software that depends on a particular platform will be harder to port to other platforms. It's important, therefore, to design your system to limit its platform dependencies.
    
4. **Dependence on object representation or implementations:** Clients that know how an object is represented, stored, located, or implemented might need to be changed when the object changes. Hiding this information from clients keeps changes from cascading.
    
5. **Algorithmic Dependencies:** Objects that depend on an algorithm will have to change when the algorithm changes. Therefore, algorithms that are likely to change should be isolated.
    
6. **Tight coupling:** Classes that are tightly coupled are hard to reuse in isolation since they depend on each other. Loose coupling increases the probability that a class can be reused by itself and that a system can be learned, ported, modified, and extended more easily.
    
7. **Extending functionality by subclassing:** Customizing an object by subclassing often isn't easy. Every new class has a fixed implementation overhead. Defining a subclass also requires an in-depth understanding of the parent class.
    
    Object composition, in general, and delegation, in particular, provide flexible alternatives to inheritance for combining behavior. New functionality can be added to an application by composing existing objects in new ways rather than by defining new subclasses of existing classes. On the other hand, heavy use of object composition can make designs harder to understand.
    
8. **Inability to alter classes conveniently:** Sometimes you have to modify a class that can't be modified conveniently. Perhaps you need the source code and don't have it. Or maybe any change would require modifying lots of existing subclasses.
    

### Application Programs

Internal reuse, maintainability, and extension are high priorities. Reuse ensures that you don't design and implement any more than you have to.

### Toolkits

A toolkit is a set of related and reusable classes designed to provide useful, general-purpose functionality. An example of a toolkit is a set of collection classes. Toolkits don't impose a particular design on your application; they just provide functionality that can help your application do its job.

### Frameworks

A "framework" is a set of cooperating classes that make up a reusable design for a specific class of software. The framework dictates the architecture of your application. The framework captures the design decisions that are common to its application domain. Frameworks thus emphasize design reuse over code reuse.

Reuse on this level leads to an inversion of control between the application and the software. An added benefit comes when the framework is documented with design patterns it uses. People who know the patterns gain insight into the framework faster.

Patterns and frameworks differ in three major ways:

1. Design patterns are more abstract than frameworks.
2. Design patterns are smaller architectural elements than frameworks.
3. Design patterns are less specialized than frameworks.

## 1.7 How to Select a Design Pattern

- Consider how design patterns solve design problems
- Scan Intent sections
- Study how patterns interrelate
- Study patterns of like purpose
- Examine a cause of redesign
- Consider what should be variable in your design

## 1.8 How to Use a Design Pattern

1. Read the pattern once through for an overview
2. Go back and study the "Structure," "Participants," and "Collaborations"
3. Look at the "Sample Code" section to see a concrete example of the pattern in code
4. Choose names for pattern participants that are meaningful in the application context
5. Define the classes
6. Define application-specific names for operations in the pattern
7. Implement the operations to carry out the responsibilities and collaborations in the pattern

# CHAPTER 3: CREATIONAL PATTERNS

Creational patterns abstract the instantiation process. They help make a system independent of how its objects are created, composed, and represented.

There are two recurring themes in these patterns:

1. They all encapsulate knowledge about which concrete classes the system uses.
2. They hide how instances of these classes are created and put together.

Nesne yaratmada temel iki problem şunlardır:

- Nesnenin yaratılacağı yer
- Nesnenin nasıl yaratılacağı

Nesne yaratılmasıyla ilgili problemler şöyle çözülebilir:

- Nesnelerin yaratılması basitleştirilmeli,
- Nesnelerin yaratılması tekrar kullanılabilir olmalı,
- İstemcilerin, nesnelerin yaratılmasına olan bağımlılıkları asgari seviyeye indirilmeli.

## SINGLETON

### Intent

Ensure a class only has one instance and provide a global point of access to it.

### Motivation

It's important for some classes to have exactly one instance. There should be only one file system and one window manager. An accounting system will be dedicated to serving one company.

### Applicability

Use the Singleton pattern when:

- There must be exactly one instance of a class and it must be accessible to clients from a well-known access point.
- The sole instance should be extensible by subclassing, and clients should be able to use an extended instance without modifying their code.

### Structure

1. **Private constructor:** The Singleton class has a private constructor, which prevents direct instantiation of the class from outside.
2. **Private static instance variable:** The Singleton class has a private static variable that holds the instance of the Singleton class.
3. **Public static method to access the instance:** The Singleton class provides a public static method that returns the instance of the Singleton class.

### Participants

- **Singleton:**
  - Defines an instance operation that lets clients access its unique instance.
  - May be responsible for creating its own unique instances.

### Collaborations

- Clients access a Singleton instance solely through Singleton's Instance operation.

### Consequences

1. **Controlled access to the sole instance.**
2. **Reduced name space:**
   - Avoids polluting the name space with global variables that store sole instances.
3. **Permits refinement of operations and representations:**
   - Configures the application with an instance of the class at run-time.
4. **Permits a variable number of instances:**
   - Makes it easy to change to allow more than one instance of the Singleton class.
5. **More flexible than class operations.**

### Implementation

1. **Ensuring a unique instance:**
   - The Singleton pattern makes the sole instance a normal instance of a class, but that class is written so that only one instance can ever be created. A common way to do this is to hide the operation that creates the instance behind a class operation that guarantees only one instance is created.
2. **Subclassing the Singleton Class:**
   - The main issue is installing its unique instance so that clients will be able to use it. In essence, the variable that refers to the singleton instance must get initialized with an instance of the subclass.
   - A more flexible approach is "registry of Singleton."
     // registry of Singleton: a registry is a central place that maintains a map of named Singleton instances. The registry provides a global point of access to these Singleton instances, similar to the way a phone book provides a directory of phone numbers.

Singleton sınıf oluşturmanın en azından iki yolu vardır:
- Nesne yaratmayı kontrol ederek: Bu daha sıkıntılı bir çözüm ailesi sunar.
- Enumeration kullanarak: Bu daha basit ve sıkıntısı az olan çözümdür.
  // enum ile tanımlanan tek nesne serialization ve reflection ile çoğaltılamaz.

### Sample Code

```java
public class CookieJar {
    private static CookieJar jar;

    private CookieJar() {}

    public static CookieJar getInstance() {
        if (jar == null) {
            jar = new CookieJar();
        }
        return jar;
    }

    public void takeCookie() {
        // code to take a cookie
    }
}
```

```java
public enum Singleton {
    INSTANCE;

    public void doSomething() {
        // code to perform some action
    }
}
```

### Known Uses

- `java.lang.Runtime#getRuntime()`
- `java.awt.Desktop#getDesktop()`
- `java.lang.System#getSecurityManager()`

### Related Patterns

- AbstractFactory
- Builder
- Prototype

**Singleton pattern provides:**

- Tek nesnenin oluşturulmasını ve erişimini kontrol eder.
- Global değişkenlere göre daha sağlıklıdır.
- Statik metotlardan daha rahat ve genişleyebilir bir yapı sunar.

# FACTORY METHOD

## Intent

Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

## Also Known As

Virtual Constructor

## Motivation

Frameworks use abstract classes to define and maintain relationships between objects. A framework is often responsible for creating these objects as well.

The framework must instantiate classes but it only knows about abstract classes which it cannot instantiate.

The Factory Method pattern offers a solution. It encapsulates the knowledge of which Document subclass to create and moves this knowledge out of the framework.

## Applicability

Use the Factory Method pattern when:

- A class can't anticipate the class of objects it must create.
- A class wants its subclasses to specify the objects it creates.
- Classes delegate responsibility to one of several helper subclasses, and you want to localize the knowledge of which helper subclass is the delegate.

## Structure

The structure of the Factory Method pattern typically includes the following elements:

1. **Product:** This is the interface or abstract class that defines the type of objects the Factory Method will create.

2. **Concrete Product:** These are the classes that implement the Product interface or abstract class.

3. **Creator:** This is the abstract class that declares the Factory Method, which returns an object of type Product. The Creator may also provide a default implementation of the Factory Method that creates a default Concrete Product.

4. **Concrete Creator:** These are the classes that implement the Creator abstract class and override the Factory Method to return a specific Concrete Product.

## Participant

- **Product:**
  - Defines the interface of objects the factory method creates.

- **ConcreteProduct:**
  - Implements the Product interface.

- **Creator:**
  - Declares the factory method, which returns an object of type Product.
  - May also define a default implementation of the factory method that returns a default ConcreteProduct object.
  - May call the factory method to create a Product object.

- **ConcreteCreator:**

## Collaborations

- Creator relies on its subclasses to define the factory method so that it returns an instance of the appropriate ConcreteProduct.

## Consequences

Factory methods eliminate the need to bind application-specific classes into your code. The code only deals with the Product interface; therefore it can work with any user-defined ConcreteProduct classes.

A potential disadvantage of factory methods is that clients might have to subclass the Creator class just to create a particular ConcreteProduct object.

Consequences of Factory Method Patterns:

1. **Provides hooks for subclasses:**
   Creating objects inside a class with a factory method is always more flexible than creating an object directly. Factory Method gives subclasses a hook for providing an extended version of an object.

2. **Connects Parallel class hierarchies:**
   Parallel class hierarchies result when a class delegates some of its responsibilities to a separate class. Connecting parallel class hierarchies in the Factory Method pattern involves creating a separate hierarchy for creating objects with additional functionality or variations and providing a way to create objects from the main class hierarchy using the factory hierarchy.

## Implementation

Consider the following issues when applying the Factory Method pattern:

1. **Two major varieties:**
   - The case when the Creator class is an abstract class and does not provide an implementation for the factory method it declares.
   - The case when the Creator is a concrete class and provides a default implementation for the factory method.
   - The first case requires subclasses to define an implementation. In the second case, the concrete Creator uses the factory method primarily for flexibility. It's following a rule that says, "Create objects in a separate operation so that subclasses can override the way they are created." This rule ensures that designers of subclasses can change the class of objects their parent class instantiates if necessary.

2. **Parameterized Factory Methods:**
   - The pattern lets the factory method create multiple kinds of products. The factory method takes a parameter that identifies the kind of object to create. Overriding a parameterized factory method lets you easily and selectively extend or change the products that a Creator produces. You can introduce new identifiers for new kinds of products, or you can associate existing identifiers with different products.

3. **Language-specific variants and issues:**
   - Different languages lend themselves to other interesting variations and caveats.

4. **Using templates to avoid subclassing**

5. **Naming Conventions:**
   - It's good practice to use naming conventions that make it clear you're using factory methods.

## Sample Code

```java
// PaymentProcessor interface
public interface PaymentProcessor {
    void validate();
    void process();
}

// CreditCardProcessor class
public class CreditCardProcessor implements PaymentProcessor {
    // implementation for credit card validation and processing
    public void validate() { /* ... */ }
    public void process() { /* ... */ }
}

// PayPalProcessor class
public class PayPalProcessor implements PaymentProcessor {
    // implementation for PayPal validation and processing
    public void validate() { /* ... */ }
    public void process() { /* ... */ }
}

// BankTransferProcessor class
public class BankTransferProcessor implements PaymentProcessor {
    // implementation for bank transfer validation and processing
    public void validate() { /* ... */ }
    public void process() { /* ... */ }
}

// PaymentProcessorFactory class
public abstract class PaymentProcessorFactory {
    public abstract PaymentProcessor createProcessor();
}

// CreditCardProcessorFactory class
public class CreditCardProcessorFactory extends PaymentProcessorFactory {
    public PaymentProcessor createProcessor() {
        return new CreditCardProcessor();
    }
}

// PayPalProcessorFactory class
public class PayPalProcessorFactory extends PaymentProcessorFactory {
    public PaymentProcessor createProcessor() {
        return new PayPalProcessor();
    }
}

// BankTransferProcessorFactory class
public class BankTransferProcessorFactory extends PaymentProcessorFactory {
    public PaymentProcessor createProcessor() {
        return new BankTransferProcessor();
    }
}
```

## Known Uses

- `java.util.Calendar#getInstance()`
- `java.util.ResourceBundle#getBundle()`
- `java.text.NumberFormat#getInstance()`
- `java.nio.charset.Charset#forName()`
- `java.net.URLStreamHandlerFactory#createURLStreamHandler(String)` (Returns singleton object per protocol)
- `java.util.EnumSet#of()`
- `javax.xml.bind.JAXBContext#createMarshaller()`

## Related Patterns

- Abstract Factory is often implemented with factory methods.
- Factory methods usually called within Template Methods.
- Prototypes don't require subclassing Creator; however, they often require an initialize operation on the Product class. Creator uses initialize to initialize the object. Factory method doesn't require such an operation.

**Factory Method’un her zaman nesne oluşturması gerekmez.** **Nesne havuzu (object pool) gibi yapılarda Factory Method havuzdan bir nesne de geri döndürebilir.**  

**Aslolan Factory Method’un nesne yaratmayı soyutlamasıdır, sistemin diğer kısımlarından ayırmasıdır, nesnenin nasıl yaratılacağı ayrı bir konudur ve bu nesneye bağlıdır.**

# ABSTRACT FACTORY

## Overview

- Factory Method abstracts the creation of a single object, while Abstract Factory abstracts the creation of multiple related or dependent objects.
- Abstract Factory typically has multiple Factory Methods.
- Objects within a family don't need to share a common interface.

## Intent

Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

## Also Known As

Kit

## Motivation

Clients only have to commit to an interface defined by an abstract class, not a particular concrete class.

## Applicability

Use when:

- A system should be independent of how its products are created, composed, and represented.
- A system should be configured with one of multiple families of products.
- A family of related product objects is designed to be used together, and you need to enforce this constraint.
- You want to provide a class library of products, and you want to reveal just their interfaces, not their implementations.

## Structure

### Participants

- **AbstractFactory:**
  - Declares an interface for operations that create abstract product objects.

- **ConcreteFactory:**
  - Implements the operations to create concrete product objects.

- **Abstract Product:**
  - Declares an interface for a type of product object.

- **Concrete Product:**
  - Defines a product object to be created by the corresponding concrete factory.
  - Implements the AbstractProduct interface.

- **Client:**
  - Uses only interfaces declared by AbstractFactory and AbstractProduct classes.

## Collaborations

- Normally, a single instance of a ConcreteFactory class is created at runtime. This concrete factory creates product objects having a particular implementation. To create different product objects, clients should use a different concrete factory.
- AbstractFactory defers the creation of product objects to its ConcreteFactory subclass.

## Consequences

The Abstract Factory pattern has the following benefits and liabilities:

1. **It isolates concrete classes:**
   - Helps you control the classes of objects that an application creates.
   - Because a factory encapsulates the responsibility and the process of creating product objects, it isolates clients from implementation classes.
   - Product class names are isolated in the implementation of the concrete factory; they do not appear in client code.

2. **It makes exchanging product families easy:**
   - The class of a concrete factory appears only once in an application—where it's instantiated.
   - It can use different product configurations simply by changing the concrete factory.

3. **It promotes consistency among products:**
   - When product objects in a family are designed to work together, it's important that an application use objects from only one family at a time.

4. **Supporting new kinds of products is difficult:**
   - Extending abstract factories to produce new kinds of products isn't easy. That's because the AbstractFactory interface fixes the set of products that can be created.

## Implementation

1. **Factories as singletons:**
   - An application typically needs only one instance of a ConcreteFactory per product family.

2. **Creating the products:**
   - AbstractFactory only declares an interface for creating products. It's up to ConcreteProduct subclasses to actually create them.
   - The most common way is to define a factory method for each product.
   - If many product families are possible, the concrete factory can be implemented using the Prototype pattern.

3. **Defining Extensible Factories:**
   - A more flexible but less safe design is to add a parameter to operations that create objects. This parameter specifies the kind of object to be created.

## Sample Code

```java
// First, we define our abstract factory interface
interface CharacterFactory {
    public Character createCharacter(String name);
}

// Next, we define our concrete factories
class WarriorFactory implements CharacterFactory {
    public Character createCharacter(String name) {
        return new Warrior(name);
    }
}

class MageFactory implements CharacterFactory {
    public Character createCharacter(String name) {
        return new Mage(name);
    }
}

// Then, we define our abstract product interface
interface Character {
    public void useAbility();
}

// Finally, we define our concrete products
class Warrior implements Character {
    // implementation details...
}

class Mage implements Character {
    // implementation details...
}

// Now we can use our factories to create different types of characters
public class Game {
    public static void main(String[] args) {
        CharacterFactory warriorFactory = new WarriorFactory();
        CharacterFactory mageFactory = new MageFactory();

        Character warrior = warriorFactory.createCharacter("Sir Lancelot");
        Character mage = mageFactory.createCharacter("Gandalf");

        warrior.useAbility();
        mage.useAbility();
    }
}
```

---
```java
// Another example: Music playback service

// First, we define our abstract factory interface
interface MusicPlayerFactory {
    public Playback createPlayback();
}

// Next, we define our concrete factories
class StreamingMusicPlayerFactory implements MusicPlayerFactory {
    public Playback createPlayback() {
        return new StreamingPlayback();
    }
}

class DownloadingMusicPlayerFactory implements MusicPlayerFactory {
    public Playback createPlayback() {
        return new DownloadingPlayback();
    }
}

class LocalMusicPlayerFactory implements MusicPlayerFactory {
    public Playback createPlayback() {
        return new LocalPlayback();
    }
}

// Then, we define our abstract product interface
interface Playback {
    public void play();
}

// Finally, we define our concrete products
class StreamingPlayback implements Playback {
    // implementation details...
}

class DownloadingPlayback implements Playback {
    // implementation details...
}

class LocalPlayback implements Playback {
    // implementation details...
}

// Now we can use our factories to create different types of music playback
public class MusicService {
    // implementation details...
}
```



## Known Uses

- `javax.xml.parsers.DocumentBuilderFactory#newInstance()`
- `javax.xml.transform.TransformerFactory#newInstance()`
- `javax.xml.xpath.XPathFactory#newInstance()`

## Related Patterns

- Abstract factory classes are often implemented with factory methods but they can also be implemented using Prototype.
- A concrete factory is often a singleton.

**Abstract Factory provides systematic naming for object families and the objects that create them.**

# BUILDER

In this pattern, the emphasis is on the process of creating an object, not where it is created.

- The builder, in its simplest form, calls the default constructor of an object and then constructs the object with set methods, returning the created object to the client.

## Intent

Separate the construction of a complex object from its representation so that the same construction process can create different representations.

## Motivation

The Builder pattern captures relationships between objects. Each converter class is called a "builder," and the reader is called the "director." It focuses on how a converted format gets created and represented.

## Applicability

Use the Builder pattern when:

- The algorithm for creating a complex object should be independent of the parts that make up the object and how they are assembled.
- The construction process must allow different representations for the object that's constructed.

## Structure

### Participants

- **Builder:**
  - Specifies an abstract interface for creating parts of a Product object.

- **ConcreteBuilder:**
  - Constructs and assembles parts of the product by implementing the Builder interface.
  - Defines and keeps track of the representation it creates.
  - Provides an interface for retrieving the product.

- **Director:**
  - Constructs an object using the Builder interface.

- **Product:**
  - Represents the complex object under construction.
  - ConcreteBuilder builds the product's internal representation and defines the process by which it's assembled.
  - Includes classes that define the constituent parts, including interfaces for assembling the parts into the final result.

## Collaborations

- The client creates the Director object and configures it with the desired Builder object.
- Director notifies the builder whenever a part of the product should be built.
- Builder handles requests from the director and adds parts to the product.
- The client retrieves the product from the builder.

## Consequences

1. **It lets you vary a product's internal representation:**
   - The product is constructed through an abstract interface, so changing the product's internal representation only requires defining a new kind of builder.

2. **It isolates code for construction and representation:**
   - Each ConcreteBuilder contains all the code to create and assemble a particular kind of product, providing reusability for different Directors.

3. **It gives you finer control over the construction process:**
   - The Builder pattern constructs the product step by step under the director's control, offering finer control over the construction process.

## Implementation

1. **Assembly and construction interface:**
   - Builder constructs their products in a step-by-step fashion, so the Builder class interface must be general enough to allow the construction of products for all kinds of concrete builders.

2. **Why no abstract class for products?**
   - The client usually configures the director with the proper concrete builder. The client knows which concrete subclass of Builder is in use and can handle its products accordingly.

3. **Empty methods as default in Builder:**
   - Empty methods can be provided as default implementations in the Builder interface.

## Sample Code

```java
class App {
    public static void main(String[] args) {
        new AlertDialog.Builder()
                .setText("Are you sure you want to exit without saving?")
                .setButton(ButtonType.YES_NO_CANCEL)
                .setIcon(IconType.QUESTION)
                .build()
                .show();
    }
}

enum IconType {NONE, INFORMATION, QUESTION, WARNING, CRITICAL}
enum ButtonType {NONE, OK, YES_NO, YES_NO_CANCEL}

class AlertDialog {
    // implementation details...

    private AlertDialog(String title, String text, ButtonType buttonType, IconType iconType) {
        // implementation details...
    }

    public static class Builder {
        // implementation details...

        public Builder setTitle(String title) {
            // implementation details...
            return this;
        }

        public Builder setText(String text) {
            // implementation details...
            return this;
        }

        public Builder setButton(ButtonType buttonType) {
            // implementation details...
            return this;
        }

        public Builder setIcon(IconType iconType) {
            // implementation details...
            return this;
        }

        public AlertDialog build() {
            // implementation details...
            return m_dialog;
        }
    }

    public void show() {
        // implementation details...
    }
}
```

---
```java
public class NutritionFacts {
    // implementation details...

    public static class Builder {
        // implementation details...

        public Builder(int servingSize, int servings) {
            // implementation details...
        }

        public Builder calories(int val) {
            // implementation details...
            return this;
        }

        public Builder fat(int val) {
            // implementation details...
            return this;
        }

        public Builder carbohydrate(int val) {
            // implementation details...
            return this;
        }

        public Builder sodium(int val) {
            // implementation details...
            return this;
        }

        public NutritionFacts build() {
            // implementation details...
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        // implementation details...
    }

    public static void main(String[] args) {
        NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
                .calories(100).sodium(35).carbohydrate(27).build();
    }
}
```

## Known Uses

- `java.lang.StringBuilder#append()` (unsynchronized)
- `java.lang.StringBuffer#append()` (synchronized)
- `java.nio.ByteBuffer#put()`

- (also on CharBuffer, ShortBuffer, IntBuffer, LongBuffer, FloatBuffer, and DoubleBuffer)
- `javax.swing.GroupLayout.Group#addComponent()`
- All implementations of `java.lang.Appendable`
- `java.util.stream.Stream.Builder`

## Related Patterns

The primary difference is that the Builder pattern focuses on constructing a complex object step by step. It is related to:

- **Abstract Factory Pattern:** Both patterns abstract the construction of complex objects but differ in their intent. The Builder focuses on constructing a product step by step, while the Abstract Factory provides an interface for creating families of related or dependent objects without specifying their concrete classes.

**Builder pattern is about constructing step by step, while Abstract Factory pattern is about providing an interface for creating families of related or dependent objects without specifying their concrete classes.**

# PROTOTYPE

- Sometimes, objects created from a class are desired to have a few specific states.
- These different states can be obtained by copying existing objects.
- Objects are copied (cloned) from a prototype or sample object.
- The prototype is also known as the "prototypal" or "exemplar" object.

## Intent

Specify the kinds of objects to create using a prototypical instance and create new objects by copying this prototype.

## Motivation

The Prototype pattern is useful to reduce the number of classes even further. For example, separate classes for whole notes and half notes might be unnecessary.

## Applicability

Use the Prototype pattern when:

- A system should be independent of how its products are created, composed, and represented.
- The classes to instantiate are specified at run-time, for example, by dynamic overloading.
- To avoid building a class hierarchy of factories that parallels the class hierarchy of products.
- Instances of a class can have only a few different combinations of state. In such cases, it may be more convenient to install a corresponding number of prototypes and clone them rather than instantiating the class manually each time with the appropriate state.

## Participants

- **Prototype:**
  - Declares an interface for cloning itself.

- **ConcretePrototype:**
  - Implements an operation for cloning itself.

- **Client:**
  - Creates a new object by asking a prototype to clone itself.

## Collaborations

- A client asks a prototype to clone itself.

## Consequences

Prototype shares many consequences with Abstract Factory and Builder patterns. It hides concrete product classes from the client, reducing the number of names clients need to know. Additional benefits include:

1. **Adding and removing products at run-time:**
   - Prototype allows incorporating a new concrete product class into a system by registering a prototypical instance with the client.

2. **Specifying new objects by varying values:**
   - The pattern supports defining new behavior through object composition, similar to instantiating existing classes and registering the instances as prototypes.

3. **Specifying new objects by varying structure:**
   - The pattern supports building objects from parts and subparts, allowing instantiation of complex user-defined structures.

4. **Reduced subclassing:**
   - The pattern lets you clone a prototype instead of asking a factory method to make a new object, eliminating the need for a Creator class hierarchy.

5. **Configuring an application with classes dynamically.**

The main liability is that each subclass of Prototype must implement the Clone operation, which may be difficult.

## Implementation

1. **Using a prototype manager:**
   - Keep a registry of available prototypes when the number of prototypes in a system isn't fixed. Clients store and retrieve prototypes from the registry (prototype manager).

2. **Implementing the Clone operation:**
   - The hardest part is implementing the Clone operation correctly, especially with object structures containing circular references. A deep copy may be required.

3. **Initializing clones:**
   - Some prototypes might need multiple initialization parameters. Passing parameters in the Clone operation may preclude a uniform cloning interface. Beware of deep-copying Clone operations; copies may need to be deleted before reinitializing them.

## Sample Code

```java
public class Doll implements Cloneable {
  private String color;

  public Doll(String color) {
    this.color = color;
  }

  public void setColor(String color) {
    this.color = color;
  }

  public String getColor() {
    return color;
  }

  public Doll copy() throws CloneNotSupportedException {
    return (Doll) super.clone();
  }
}

Doll originalDoll = new Doll("blue");
Doll newDoll = originalDoll.copy();

originalDoll.setColor("red");
System.out.println(originalDoll.getColor()); // prints "red"
System.out.println(newDoll.getColor()); // prints "blue"
```

---
```java
public class Enemy implements Cloneable {
    // implementation details...

    public Enemy clone() throws CloneNotSupportedException {
        return (Enemy) super.clone();
    }

    // implementation details...
}

Enemy originalEnemy = new Enemy("Goblin", 100, 10);
Enemy newEnemy = originalEnemy.clone();

originalEnemy.setName("Orc");
originalEnemy.setHealth(200);
System.out.println(originalEnemy); // prints "Enemy[name=Orc, health=200, attack=10]"
System.out.println(newEnemy); // prints "Enemy[name=Goblin, health=100, attack=10]"
```
---
```java
public abstract class Report implements Cloneable {
    // implementation details...

    public Report clone() throws CloneNotSupportedException {
        return (Report) super.clone();
    }

    public abstract void generate();
}

Report originalReport = new PDFReport("Monthly Sales Report", salesData);
Report newReport = originalReport.clone();

originalReport = new ExcelReport("Monthly Sales Report", salesData);
System.out.println(originalReport.generate()); // generates an Excel report
System.out.println(newReport.generate()); // generates a PDF report
```

## Known Uses

- `java.lang.Object#clone()` (the class has to implement `java.lang.Cloneable`)

## Related Patterns

Designs that make heavy use of the Composite and Decorator patterns often benefit from Prototype as well.

# CHAPTER 3: STRUCTURAL PATTERNS

Structural patterns are concerned with how classes and objects are composed to form larger structures. Structural class patterns use inheritance to compose interfaces or implementations.

Rather than composing interfaces or implementations, structural object patterns describe ways to compose objects to realize new functionality. The added flexibility of object composition comes from the ability to change composition at "run-time," which is impossible with "static class composition."

- **Adapter:** Uyumsuz arayüzleri uyumlu kılmak.
- **Bridge:** Soyutlama ile gerçekleştirmesini birbirlerinden ayırmak.
- **Composite:** Bütün-parça ilişkisi kurgulamak.
- **Decorator:** Nesneye dinamik olarak yeni özellikler kazandırmak.
- **Facade:** Karmaşık bir alt sistemi kullanmayı kolaylaştırmak.
- **Flyweight:** Nesneleri paylaşarak, nesne sayısını azaltmak.
- **Proxy:** Bir nesneye erişimi kontrol etmek.

## Flyweight

### Intent

Use sharing to support large numbers of fine-grained objects efficiently.

### Motivation

Some applications could benefit from using objects throughout their design, but a naive implementation would be probably expensive.

The flyweight pattern describes how to share objects to allow their use at fine granularities without prohibitive cost.

A "flyweight" is a shared object that can be used in multiple contexts simultaneously. The flyweight acts as an independent object in each context — It is indistinguishable from an instance of the object that's not shared. The key concept here is the distinction between "intrinsic" and "extrinsic" state.

- The intrinsic state is the shared data that all objects can use.
- The extrinsic state is the unique data that distinguishes each object from the others.

Clients are responsible for passing extrinsic state to the flyweight when it needs it.

### Applicability

The Flyweight pattern's effectiveness depends heavily on how and where it's used.

- An application uses a large number of objects.
- Storage costs are high because of the sheer quantity of objects.
- Most objects' state can be made extrinsic.
- Many groups of objects may be replaced by relatively few shared objects once extrinsic state is removed.
- The application doesn't depend on object identity.

### Structure

#### Participants

- **Flyweight:** Declares an interface through which flyweights can receive and act on extrinsic state.
- **ConcreteFlyweight:** Implements the Flyweight interface and adds storage for intrinsic state, if any. A ConcreteFlyweight object must be shareable. Any state it stores must be intrinsic; that is, it must be independent of the ConcreteFlyweight object's context.
- **UnsharedConcreteFlyweight:** Not all Flyweight subclasses need to be shared. The Flyweight interface enables sharing; it doesn't enforce it. It's common for UnsharedConcreteFlyweight objects to have ConcreteFlyweight objects as children at some level in the flyweight object structure.
- **FlyweightFactory:** Creates and manages flyweight objects, ensures that flyweights are shared properly. When a client requests a flyweight, the FlyweightFactory object supplies an existing instance or creates one if none exists.
- **Client:** Maintains a reference to flyweight(s), computes, or stores the extrinsic state of flyweight(s).

#### Collaborations

- State that a flyweight needs to function must be characterized as either intrinsic or extrinsic.
- Intrinsic state is stored in the ConcreteFlyweight object; extrinsic state is stored or computed by Client objects.
- Clients pass this state to the flyweight when they invoke its operations.
- Clients should not instantiate ConcreteFlyweight directly. Clients must obtain ConcreteFlyweight objects exclusively from the FlyweightFactory object to ensure they are shared properly.

### Consequences

Flyweight may introduce run-time costs associated with transactions on extrinsic state, especially if it was formerly stored as intrinsic state. However, such costs are offset by space savings, which increase as more flyweights are shared.

Storage savings are a function of several factors:

- The reduction in the total number of instances that comes from sharing.
- The amount of intrinsic state per object.
- Whether extrinsic state is computed or stored.

The more flyweights are shared, the greater the storage savings. The greatest savings occur when the objects use substantial quantities of both intrinsic and extrinsic state, and the extrinsic state can be computed rather than stored.

- Flyweight kalıbı, çok nesne gereksinimi olduğunda kullanılır ve nesne sayısını azaltır.

### Implementation

1. **Removing extrinsic state:**
   The pattern's applicability is determined largely by how easy it is to identify extrinsic state and remove it from shared objects.

2. **Managing Shared Objects:**
   Because objects are shared, clients shouldn't instantiate them directly. FlyweightFactory lets clients locate a particular flyweight.

### Sample Code

```java
// Example 1: E-commerce Website

// Product class representing a product
public class Product {
  // Intrinsic state
  private String name;
  private BigDecimal price;
  private String description;
  private String manufacturer;

  public Product(String name, BigDecimal price, String description, String manufacturer) {
    this.name = name;
    this.price = price;
    this.description = description;
    this.manufacturer = manufacturer;
  }
  // ... getters and setters for product information
}

// ProductFactory class managing the creation of Product objects
public class ProductFactory {
  // Shared information (intrinsic state)
  private Map<String, Product> products = new HashMap<>();

  public Product getProduct(String name, BigDecimal price, String description, String manufacturer) {
    String key = manufacturer + name + price + description;
    if (!products.containsKey(key)) {
      products.put(key, new Product(name, price, description, manufacturer));
    }
    return products.get(key);
  }
}

// EcommerceWebsite class representing an e-commerce website
public class EcommerceWebsite {
  // Unique information (extrinsic state)
  private List<Product> products = new ArrayList<>();

  public void displayProducts(String manufacturer) {
    ProductFactory factory = new ProductFactory();
    Product product1 = factory.getProduct("Product 1", new BigDecimal("10.00"), "Description 1", manufacturer);
    products.add(product1); // Add the unique information (extrinsic state)
    Product product2 = factory.getProduct("Product 2", new BigDecimal("20.00"), "Description 2", manufacturer);
    products.add(product2); // Add the unique information (extrinsic state)
    // ... display the products on the website
  }
}
```

---
```java
// Example 2: Paint Brush Application

// Pen interface
public interface Pen {
  void setColor(String color);
  void draw(String content);
}

// Enum for brush size
public enum BrushSize {
  THIN, MEDIUM, THICK
}

// ConcreteFlyweight for ThickPen
public class ThickPen implements Pen {
  final BrushSize brushSize = BrushSize.THICK; // Intrinsic state - shareable
  private String color = null; // Extrinsic state - supplied by the client

  public void setColor(String color) {
    this.color = color;
  }

  @Override
  public void draw(String content) {
    System.out.println("Drawing THICK content in color: " + color);
  }
}

// PenFactory for creating and managing pens
public class PenFactory {
  private static final HashMap<String, Pen> pensMap = new HashMap<>();

  public static Pen getThickPen(String color) {
    String key = color + "-THICK";

    Pen pen = pensMap.get(key);

    if (pen != null) {
      return pen;
    } else {
      pen = new ThickPen();
      pen.setColor(color);
      pensMap.put(key, pen);
    }

    return pen;
  }
  // Similar methods for other pen sizes...
}

// PaintBrushClient for testing and output
public class PaintBrushClient {
  public static void main(String[] args) {
    Pen yellowThinPen1 = PenFactory.getThickPen("YELLOW"); // created a new pen
    yellowThinPen1.draw("Hello World !!");

    Pen yellowThinPen2 = PenFactory.getThickPen("YELLOW"); // pen is shared
    yellowThinPen2.draw("Hello World !!");

    Pen blueThinPen = PenFactory.getThickPen("BLUE"); // created a new pen
    blueThinPen.draw("Hello World !!");

    System.out.println(yellowThinPen1.hashCode());
    System.out.println(yellowThinPen2.hashCode());

    System.out.println(blueThinPen.hashCode());
  }
}
```

### Known Uses

- `java.lang.Integer#valueOf(int)` (also on Boolean, Byte, Character, Short, Long, and BigDecimal)

### Related Patterns

It's often best to implement State and Strategy objects as flyweights.

# Adapter Pattern

### Intent

Convert the interface of a class into another interface. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

### Also Known As

Wrapper

### Motivation

Sometimes a toolkit class that's designed for reuse isn't reusable only because its interface doesn't match the domain-specific interface an application requires. Often the adapter is responsible for functionality the adapted class doesn't provide.

### Applicability

- You want to use an existing class, and its interface does not match the one you need.
- You want to create a reusable class that cooperates with unrelated or unforeseen classes, that is, classes that don't necessarily have compatible interfaces.
- (Object adapter only) You need to use several existing subclasses, but it's impractical to adapt their interface by subclassing every one. An object adapter can adapt the interface of its parent class.

### Structure

#### Participants

- **Target:** Defines the domain-specific interface that Client uses.
- **Client:** Collaborates with objects conforming to the Target interface.
- **Adaptee:** Defines an existing interface that needs adapting.
- **Adapter:** Adapts the interface of Adaptee to the Target interface.

#### Collaborations

Clients call operations on an Adapter instance. In turn, the adapter calls Adaptee operations that carry out the request.

### Consequences

Class and object adapters have different trade-offs.

A class adapter:
- Adapts Adaptee to Target by committing to a concrete Adaptee class. As a consequence, a class adapter won't work when we want to adapt a class and all its subclasses.
- Lets Adapter override some of Adaptee's behavior, since Adapter is a subclass of Adaptee.
- Introduces only one object, and no additional pointer indirection is needed to get to the Adaptee.

An object adapter:
- Lets a single Adapter work with many Adaptees, that is, the Adaptee itself and all of its subclasses. The Adapter can also add functionality to all Adaptees at once.
- Makes it harder to override Adaptee behavior. It will require subclassing Adaptee and making Adapter refer to the subclass rather than the Adaptee itself.

Other issues to consider when using the Adapter pattern:

1. **How much adapting does Adapter do?**
   Adapters vary in the amount of work they do to adapt Adaptee to the Target interface. The amount of work Adapter does depends on how similar the Target interface is to Adaptee.

2. **Pluggable Adapters**
   A class is more reusable when you minimize the assumptions other classes must make to use it. Interface adaptation lets us incorporate our class into existing systems that might accept a pluggable adapter.

3. **Using two-way adapters to provide transparency**
   A potential problem with adapters is that they aren't transparent to all clients. An adapted object no longer conforms to the Adaptee interface, so it can't be used as-is wherever an Adaptee object can. A "two-way adapter" can provide such transparency. Specifically, they're useful when two different clients need to view an object differently.

- Adaptor, uyumsuz nesnenin wrapperı olmuştur.
- Adaptor'ün ne kadar iş yaptığı, uyumsuzluğun miktarıyla ilgilidir.
- Karmaşıklıktan kaçınmak için olması gereken her adaptör nesnesinin tek bir uyumsuz arayüzü uyumlu hale getirmesidir.

### Implementation

1. **Implementing class adapters in Java**
   Adapter would inherit publicly from Target and privately from Adaptee. Thus, Adapter would be a subtype of Target but not of Adaptee.

2. **Pluggable adapters**
   The first step, common to all three of the implementations discussed here, is to find a "narrow" interface for Adaptee, that is, the smallest subset of operations that let us do the adaptation. A narrow interface consisting of only a couple of operations is easier to adapt than an interface with dozens of operations. The narrow interface leads to three implementation approaches:
   - (a) Using abstract operations
   - (b) Using delegate objects
   - (c) Parameterized adapters

### Sample Code

```java
// Example 1: Payment Processing System Integration

// PaymentProcessor interface
public interface CreditCardPaymentProcessor {
    void processCreditCardPayment(String cardNumber, double amount);
}

// Third-party PaymentGateway class
public class PaymentGateway {
    public void processPayment(String gatewayName, String cardNumber, double amount) {
        System.out.println("Processing " + gatewayName + " payment of $" + amount + " with card number " + cardNumber);
    }
}

// Adapter for PaymentGateway
public class PaymentGatewayAdapter implements CreditCardPaymentProcessor {
    private PaymentGateway paymentGateway;
    private String gatewayName;

    public PaymentGatewayAdapter(PaymentGateway paymentGateway, String gatewayName) {
        this.paymentGateway = paymentGateway;
        this.gatewayName = gatewayName;
    }

    public void processCreditCardPayment(String cardNumber, double amount) {
        paymentGateway.processPayment(gatewayName, cardNumber, amount);
    }
}

// Usage
PaymentGatewayAdapter paymentGatewayAdapter = new PaymentGatewayAdapter(new PaymentGateway(), "Stripe");
paymentGatewayAdapter.processCreditCardPayment("1234567890123456", 99.99);
```

---

```java
// Example 2: Weather Service Integration

// WeatherData interface
public interface WeatherData {
    String getLocation();
    double getTemperature();
    double getHumidity();
}

// Third-party WeatherService class
public class WeatherService {
    public String getWeatherData() {
        return "New York,75,60";
    }
}

// Adapter for WeatherService
public class WeatherDataAdapter implements WeatherData {
    private WeatherService weatherService;

    public WeatherDataAdapter(WeatherService weatherService) {
        this.weatherService = weatherService;
    }

    public String getLocation() {
        String weatherData = weatherService.getWeatherData();
        String[] parts = weatherData.split(",");
        return parts[0];
    }

    public double getTemperature() {
        String weatherData = weatherService.getWeatherData();
        String[] parts = weatherData.split(",");
        return Double.parseDouble(parts[1]);
    }

    public double getHumidity() {
        String weatherData = weatherService.getWeatherData();
        String[] parts = weatherData.split(",");
        return Double.parseDouble(parts[2]);
    }
}

// Usage
WeatherDataAdapter weatherDataAdapter = new WeatherDataAdapter(new WeatherService());
System.out.println("Location: " + weatherDataAdapter.getLocation());
System.out.println("Temperature: " + weatherDataAdapter.getTemperature());
System.out.println("Humidity: " + weatherDataAdapter.getHumidity());
```

### Known Uses

- `java.util.Arrays#asList()`
- `java.util.Collections#list()`
- `java.util.Collections#enumeration()`
- `java.io.InputStreamReader(InputStream)` (returns a Reader)
- `java.io.OutputStreamWriter(OutputStream)` (returns a Writer)
- `javax.xml.bind.annotation.adapters.XmlAdapter#marshal()` and `#unmarshal()`

### Related Patterns

- Bridge has a structure similar to an object adapter, but Bridge has a different implementation. "An adapter is meant to change the interface of an existing object."
- Decorator enhances another object without changing its interface. "Decorator supports recursive composition."
- Proxy defines a representative or surrogate for another object and does not change the interface.

# Composite Pattern

### Intent

Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

### Motivation

The user can group components to form larger components, which, in turn, can be grouped to form still larger components. But there's a problem with this approach: Code that uses these classes must treat primitive and container objects differently, even if most of the time the user treats them identically. Having to distinguish these objects makes the application more complex. The Composite pattern describes how to use recursive composition so that clients don't have to make this distinction. The key to the Composite pattern is an abstract class that represents both primitives and their containers.

### Applicability

Use Composite pattern when:
- You want to represent part-whole hierarchies of objects.
- You want clients to be able to ignore the difference between compositions of objects and individual objects. Clients will treat all objects in the composite structure uniformly.

### Structure

#### Participants

- **Component:**
  - Declares the interface for objects in the composition.
  - Implements default behavior for the interface common to all classes, as appropriate.
  - Declares an interface for accessing and managing its child components.
  - (Optional) Defines an interface for accessing a component's parent in the recursive structure and implements it if that's appropriate.

- **Leaf:**
  - Represents leaf objects in the composition. A leaf has no children.
  - Defines behavior for primitive objects in the composition.

- **Composite:**
  - Defines behavior for components having children.
  - Stores child components.
  - Implements child-related operations in the Composite interface.

- **Client:**
  - Manipulates objects in the composition through the Component interface.

#### Collaborations

Clients use the Component class interface to interact with objects in the composite structure. If the recipient is a Leaf, then the request is handled directly. If the recipient is a Composite, then it usually forwards requests to its child components, possibly performing additional operations before and/or after forwarding.

### Consequences

- Defines a class hierarchy consisting of primitive objects and composite objects. Primitive objects can be composed into more complex objects, which in turn can be composed and so on recursively.
- Makes the client simple. Clients can treat composite structures and individual objects uniformly. Clients normally don't know whether they're dealing with a leaf or a composite component.
- Makes it easier to add new kinds of components. Newly defined Composite or Leaf subclasses work automatically with existing structures and client code.
- Can make your design overly general. The disadvantage of making it easy to add new components is that it makes it harder to restrict the components of a composite.

### Implementation

1. **Explicit parent references:**
   Maintaining references from child components to their parent can simplify the traversal and management of a composite structure. The parent reference simplifies moving up the structure and deleting a component. With parent references, it's essential to maintain the invariant that all children of a composite have, as their parent, the composite that, in turn, has them as children.

2. **Sharing components:**
   When a component can have no more than one parent, sharing components becomes difficult. A possible solution is for children to store multiple parents. But that can lead to ambiguities as a request propagates up the structure. It works in cases where children can avoid sending parent requests by externalizing some or all of their state.

3. **Maximizing the Component Interface:**
   One of the goals of the Composite pattern is to make clients unaware of specific Leaf or Composite classes they're using. To attain this goal, the Component class should define as many common operations for Composite and Leaf classes as possible. This goal will sometimes conflict with the principle of class hierarchy design that says a class should only define operations that are meaningful to its subclass. Sometimes a little creativity shows how an operation that would appear to make sense only for Composites can be implemented for all Components by moving it to the Component class.

4. **Declaring the child management operations:**
   Although the Composite class implements the Add and Remove operations for managing children, an important issue in the Composite pattern is which classes declare these operations in the Composite class hierarchy. The decision involves a trade-off between safety and transparency. Transparency over safety.

5. **Should Component implement a list of Components?:**
   This is worthwhile only if there are relatively few children in the structure.

6. **Child ordering:**
   When child ordering is an issue, you must design child access and management interfaces carefully to manage the sequence of children.

7. **Caching to improve performance:**

8. **Who should delete components:**
   In languages without garbage collectors, it's best to make a Composite responsible for deleting its children when it's destroyed.

9. **What's the best data structure for storing components:**

### Sample Code

```java
// Example 1: Drawing Shapes

public interface Shape {
    void draw(String fillColor);
}

public class Triangle implements Shape {
    @Override
    public void draw(String fillColor) {
        System.out.println("Drawing Triangle with color " + fillColor);
    }
}

public class Circle implements Shape {
    @Override
    public void draw(String fillColor) {
        System.out.println("Drawing Circle with color " + fillColor);
    }
}

public class Drawing implements Shape {
    // Collection of Shapes
    private List<Shape> shapes = new ArrayList<>();

    @Override
    public void draw(String fillColor) {
        for (Shape sh : shapes) {
            sh.draw(fillColor);
        }
    }

    // Adding shape to drawing
    public void add(Shape s) {
        this.shapes.add(s);
    }

    // Removing shape from drawing
    public void remove(Shape s) {
        shapes.remove(s);
    }

    // Removing all the shapes
    public void clear() {
        System.out.println("Clearing all the shapes from drawing");
        this.shapes.clear();
    }
}

// Usage
public static void main(String[] args) {
    Shape tri = new Triangle();
    Shape tri1 = new Triangle();
    Shape cir = new Circle();

    Drawing drawing = new Drawing();
    drawing.add(tri1);
    drawing.add(tri1);
    drawing.add(cir);

    drawing.draw("Red");

    drawing.clear();

    drawing.add(tri);
    drawing.add(cir);
    drawing.draw("Green");
}
```

---
```java
// Example 2: Product Bundles in an Online Store

public interface Product {
    double getPrice();
}

public class SimpleProduct implements Product {
    private String name;
    private double price;

    public SimpleProduct(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public double getPrice() {
        return price;
    }
}

public class CompositeProduct implements Product {
    private String name;
    private List<Product> products = new ArrayList<>();

    public CompositeProduct(String name) {
        this.name = name;
    }

    public void addProduct(Product product) {
        products.add(product);
    }

    public double getPrice() {
        double total = 0;
        for (Product product : products) {
            total += product.getPrice();
        }
        return total;
    }
}

// Usage
public static void main(String[] args) {
    SimpleProduct backpack = new SimpleProduct("Backpack", 50.0);
    SimpleProduct notebook = new SimpleProduct("Notebook", 5.0);
    SimpleProduct pen = new SimpleProduct("Pen", 1.0);

    CompositeProduct backToSchoolBundle = new CompositeProduct("Back to School Bundle");
    backToSchoolBundle.addProduct(backpack);
    backToSchoolBundle.addProduct(notebook);
    backToSchoolBundle.addProduct(pen);

    System.out.println("The Back to School bundle costs $" + backToSchoolBundle.getPrice());
}
```
### Known Uses

- `java.awt.Container#add(Component)` (practically all over Swing thus)
- `javax.faces.component.UIComponent#getChildren()` (practically all over JSF UI thus)

### Related Patterns

- Often component-parent link is used for a Chain of Responsibility.
- Decorator is often used with Composite.
- Flyweight lets you share components, but they can no longer refer to their parents.
- Iterator can be used to traverse composites.
- Visitor localizes operations and behavior that would otherwise be distributed across Composite and Leaf classes.

# Facade Pattern

### Intent

Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

### Motivation

Structuring a system into subsystems helps reduce complexity. A common design goal is to minimize communication and dependencies between subsystems.

### Applicability

- Provide a simple interface to a complex subsystem. Subsystems often get more complex as they evolve. Most patterns, when applied, result in more and smaller classes. This makes the subsystem more reusable and easier to customize, but it also becomes harder to use for clients that don't need to customize it.

- There are many dependencies between clients and the implementation classes of an abstraction. Introduce a facade to decouple the subsystem from clients and other subsystems.

- You want to layer your subsystems. Use a facade to define an entry point to each subsystem level.

### Participants

- **Facade:**
  - Knows which subsystem classes are responsible for a request.
  - Delegates client requests to appropriate subsystem objects.

- **Subsystem classes:**
  - Implement subsystem functionality.
  - Handle work assigned by the Facade object.
  - Have no knowledge of the facade; that is, they keep no references to it.

### Collaborations

- Clients communicate with the subsystem by sending requests to Facade, which forwards them to the appropriate subsystem object(s).
- Clients that use the facade don't have to access its subsystem objects directly.

### Consequences

1. It shields clients from subsystem components, thereby reducing the number of objects that clients deal with and making the subsystem easier to use.

2. It promotes weak coupling between the subsystem and its clients. A facade can also simplify porting systems to other platforms because it's less likely that building one subsystem requires building all objects.

3. It doesn't prevent applications from using subsystem classes if they need to. This way, you can choose between ease of use and generality.

### Implementation

1. **Reducing client-subsystem coupling:**
   The coupling between clients and the subsystem can be reduced even further by making Facade an abstract class with concrete subclasses for different implementations of a subsystem.

2. **Public versus private subsystem classes:**

### Sample Code

```java
public class ComplexClassA {
    public void methodA() {
        // do something complicated
    }
}

public class ComplexClassB {
    public void methodB() {
        // do something complicated
    }
}

public class ComplexClassC {
    public void methodC() {
        // do something complicated
    }
}

public class Facade {
    private ComplexClassA complexClassA;
    private ComplexClassB complexClassB;
    private ComplexClassC complexClassC;

    public Facade() {
        complexClassA = new ComplexClassA();
        complexClassB = new ComplexClassB();
        complexClassC = new ComplexClassC();
    }

    public void doSomething() {
        complexClassA.methodA();
        complexClassB.methodB();
        complexClassC.methodC();
    }
}

public class MyProgram {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.doSomething();
    }
}
```

---
```java
// Example 2: E-commerce Website

public class VendorA {
    public void fetchProductInfo(String productId) {
        // fetch product info from Vendor A's API
    }

    public void placeOrder(String productId, int quantity) {
        // place order on Vendor A's API
    }

    public void handlePayment(String orderId, double amount) {
        // handle payment on Vendor A's API
    }
}

public class VendorB {
    public void getProductInfo(String id) {
        // fetch product info from Vendor B's API
    }

    public void createOrder(String id, int quantity) {
        // place order on Vendor B's API
    }

    public void processPayment(String orderId, double amount) {
        // handle payment on Vendor B's API
    }
}

// Creating Facade Class

public class VendorAPIFacade {
    private VendorA vendorA;
    private VendorB vendorB;

    public VendorAPIFacade() {
        vendorA = new VendorA();
        vendorB = new VendorB();
    }

    public void getProductInfo(String productId) {
        vendorA.fetchProductInfo(productId);
        vendorB.getProductInfo(productId);
    }

    public void placeOrder(String productId, int quantity) {
        vendorA.placeOrder(productId, quantity);
        vendorB.createOrder(productId, quantity);
    }

    public void handlePayment(String orderId, double amount) {
        vendorA.handlePayment(orderId, amount);
        vendorB.processPayment(orderId, amount);
    }
}

// Test

public class MyEcommerceWebsite {
    public static void main(String[] args) {
        VendorAPIFacade vendorAPIFacade = new VendorAPIFacade();

        // fetch product info from all vendors
        vendorAPIFacade.getProductInfo("product123");

        // place order on all vendors
        vendorAPIFacade.placeOrder("product456", 2);

        // handle payment on all vendors
        vendorAPIFacade.handlePayment("order789", 50.0);
    }
}
```

### Known Uses

- `javax.faces.context.FacesContext`, it internally uses, among others, the abstract/interface types `LifeCycle`, `ViewHandler`, `NavigationHandler` and many more without that the end-user has to worry about it (which are, however, overrideable by injection).
- `javax.faces.context.ExternalContext`, which internally uses `ServletContext`, `HttpSession`, `HttpServletRequest`, `HttpServletResponse`, etc.

### Related Patterns

- Abstract Factory can be used with Facade to provide an interface for creating subsystem objects in a subsystem-independent way.
- Mediator is similar to Facade in that it abstracts functionality of existing classes.
- Usually, only one Facade object is required. Thus Facade objects are often Singletons.

# Proxy Pattern

### Intent

Provide a surrogate or placeholder for another object to control access to it.

### Motivation

One reason for controlling access to an object is to defer the full cost of its creation and initialization until we actually need to use it. Constraints would suggest creating each expensive object on demand. The solution is to use another object, a "proxy," that acts as a stand-in for the real object. The proxy acts just like the object and takes care of instantiating it when it's required.

### Applicability

Proxy is applicable whenever there is a need for a more versatile or sophisticated reference to an object than a simple pointer.

1. A "remote proxy" provides a local representative for an object in a different address space.

2. A "virtual proxy" creates expensive objects on demand.

3. A "protection proxy" controls access to the original object.

4. A "smart reference" is a replacement for a bare pointer that performs additional actions when an object is accessed.

### Participants

- **Proxy:**
  - Maintains a reference that lets the proxy access the real subject.
  - Provides an interface identical to Subjects so that a proxy can be substituted for the real subject.
  - Controls access to the real subject and may be responsible for creating and deleting it.
    - "Remote proxies" are responsible for encoding a request and its arguments and for sending the encoded request to the real subject in a different address space.
    - "Virtual proxies" may cache additional information about the real subject so that they can postpone accessing it.
    - "Protection proxies" check that the caller has the access permissions required to perform a request.
  
- **Subject:**
  - Defines the common interface for RealSubject and Proxy so that a Proxy can be used anywhere a RealSubject is expected.
  
- **RealSubject:**
  - Defines the real object that the proxy represents.

### Collaborations

- Proxy forwards requests to RealSubject when appropriate, depending on the kind of proxy.

### Consequences

The proxy pattern introduces a level of indirection when accessing an object.

1. A remote proxy can hide the fact that an object resides in a different address space.

2. A virtual proxy can perform optimizations such as creating an object on demand.

3. Both protection proxies and smart references allow additional housekeeping tasks when an object is accessed.

There is another optimization that the Proxy pattern can hide from the client. It's called "copy-on-write," and it's related to creation on demand. Copying a large and complicated object can be an expensive operation.

### Implementation

Here are some general rules for implementing the Proxy pattern:

1. Define an interface that represents the original object and the proxy object. This interface should include all of the methods that the client needs to interact with the object.

2. Create a class that implements the interface and acts as the real object. This class should contain the actual implementation of the object's behavior.

3. Create a class that also implements the interface and acts as a proxy for the real object. This class should have a reference to the real object and control access to it. It can add additional functionality before or after the real object's behavior is executed.

4. Modify the client code to use the proxy object instead of the real object.

### Sample Code

```java
// Example 1: Pizza Ordering

public interface Pizza {
    void orderPizza();
}

public class PizzaProxy implements Pizza {
    private Pizza realPizza;

    public PizzaProxy() {
        this.realPizza = new RealPizza();
    }

    public void orderPizza() {
        System.out.println("Taking pizza order...");
        realPizza.orderPizza();
        System.out.println("Pizza is on its way!");
    }
}

public class RealPizza implements Pizza {
    public void orderPizza() {
        System.out.println("Ordering pizza...");
    }
}

public class Main {
    public static void main(String[] args) {
        Pizza pizza = new PizzaProxy();
        pizza.orderPizza();
    }
}
```

--- 
```java
// Example 2: Image Loading

public interface Image {
    void display();
}

public class RealImage implements Image {
    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk(fileName);
    }

    private void loadFromDisk(String fileName) {
        System.out.println("Loading " + fileName);
    }

    public void display() {
        System.out.println("Displaying " + fileName);
    }
}

public class ProxyImage implements Image {
    private RealImage realImage;
    private String fileName;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    public void display() {
        if (realImage == null) {
            realImage = new RealImage(fileName);
        }
        realImage.display();
    }
}

// Test

public class Main {
    public static void main(String[] args) {
        Image image1 = new ProxyImage("image1.png");
        Image image2 = new ProxyImage("image2.png");
        
        // Loading image1 from disk
        image1.display(); 
        // Displaying image1 from cache
        image1.display();
        
        // Loading image2 from disk
        image2.display();
        // Displaying image2 from cache
        image2.display();
    }
}
```
---
```java
// Example 3: Article Caching

public interface Article {
    String getId();
    String getTitle();
    String getContent();
}

public class RealArticle implements Article {
    private String id;
    private String title;
    private String content;

    public RealArticle(String id) {
        this.id = id;
        // Simulate slow database access
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // Retrieve article data from the database using the given id
        this.title = "Title of article " + id;
        this.content = "Content of article " + id;
    }

    public String getId() {
        return id;
    }

    public String getTitle() {
        return title;
    }

    public String getContent() {
        return content;
    }
}

public class ProxyArticle implements Article {
    private static final int CACHE_SIZE = 10;
    private static Map<String, Article> cache = new LinkedHashMap<String, Article>() {
        @Override
        protected boolean removeEldestEntry(Map.Entry<String, Article> eldest) {
            return size() > CACHE_SIZE;
        }
    };

    private String id;

    public ProxyArticle(String id) {
        this.id = id;
    }

    public String getId() {
        return id;
    }

    public String getTitle() {
        Article article = cache.get(id);
        if (article != null) {
            return article.getTitle();
        } else {
            article = new RealArticle(id);
            cache.put(id, article);
            return article.getTitle();
        }
    }

    public String getContent() {
        Article article = cache.get(id);
        if (article != null) {
            return article.getContent();
        } else {
            article = new RealArticle(id);
            cache.put(id, article);
            return article.getContent();
        }
    }
}

// Test

public class Main {
    public static void main(String[] args) {
        Article article1 = new ProxyArticle("article1");
        Article article2 = new ProxyArticle("article2");
        
        // Accessing article1
        System.out.println(article1.getTitle());
        System.out.println(article1.getContent());
        
        // Accessing article2
        System.out.println(article2.getTitle());
        System.out.println(article2.getContent());
    }
}
```

### Known Uses

- `java.lang.reflect.Proxy`
- `java.rmi.*`
- `javax.ejb.EJB`
- `javax.inject.Inject`
- `javax.persistence.PersistenceContext`

### Related Patterns

- **Adapter:** Provides a different interface to the object it adapts. In contrast, a proxy provides the same interface as its subject. However, a proxy used for access protection might refuse to perform an operation that the subject will perform.
    
- **Decorator:** Can have similar implementations as proxies, decorators have different purposes. Proxy controls access to an object, while decorators add responsibilities to the object.

# Decorator Pattern

### Intent

Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

### Also Known As

Wrapper

### Motivation

Sometimes we want to add responsibilities to individual objects, not to an entire class. One way to add responsibilities is with inheritance, but this is inflexible because the choice of the field is made statically. A more flexible approach is to enclose the component in another object that adds the field. The enclosing object is called a "decorator." The decorator conforms to the interface of the component it decorates so that its presence is transparent to the component's clients. The decorator forwards requests to the component and may perform additional actions before or after forwarding.

### Applicability

- To add responsibilities to individual objects dynamically and transparently, i.e., without affecting other objects.
- For responsibilities that can be withdrawn.
- When extension by subclassing is impractical. Sometimes a large number of independent extensions are possible and would produce an explosion of subclasses to support every combination.

### Structure

### Participants

- **Component:**
  - Defines the interface for objects that can have responsibilities added to them dynamically.

- **ConcreteComponent:**
  - Defines an object to which additional responsibilities can be attached.

- **Decorator:**
  - Maintains a reference to a Component object and defines an interface that conforms to Component's interface.

- **ConcreteDecorator:**
  - Adds responsibilities to the component.

### Collaborations

- Decorator forwards requests to its Component object. It may optionally perform additional operations before and after forwarding requests.

### Consequences

1. **More flexibility than a static interface:**
   - With decorators, responsibilities can be added and removed at runtime simply by attaching and detaching them. Decorators also make it easy to add a property twice. Inheriting from a class twice is error-prone at best.

2. **Avoids feature-laden classes high up in the hierarchy:**
   - Instead of trying to support all foreseeable features in a complex, customizable class, you can define a simple class and add functionality incrementally with Decorator objects. Functionality can be composed from simple pieces. As a result, an application needn't pay for features it doesn't use.

3. **A decorator and its component aren't identical:**
   - A decorator acts as a transparent enclosure. But from an object identity point of view, a decorated component is not identical to the component itself.

4. **List of little objects:**
   - A design that uses Decorator often results in systems composed of lots of little objects that all look alike. The objects differ only in the way they are interconnected, not in their class or in the value of their variables. Although these systems are easy to customize by those who understand them, they can be hard to learn and debug.

### Implementation

1. **Interface conformance:**
   - A decorator object's interface must conform to the interface of the component it decorates. ConcreteDecorator classes must, therefore, inherit from a common class.

2. **Omitting the abstract Decorator class:**
   - There's no need to define an abstract Decorator class when you only need to add one responsibility.

3. **Keeping Component classes lightweight:**
   - To ensure a conforming interface, components and decorators must descend from a common Component class. It's important to keep this common class lightweight, focusing on defining an interface, not on storing data.

4. **Changing the skin of an object versus changing its guts:**
   - We can think of a decorator as a skin over an object that changes its behavior. An alternative is to change the object's guts, which is the Strategy pattern. Strategies are a better choice in situations where the Component class is intrinsically heavyweight, making the Decorator pattern too costly to apply. Since the Decorator pattern only changes a component from the outside, the component doesn't have to know anything about its decorators; that is, the decorators are transparent to the component.

### Sample Code

```java
// Example 1: Ice Cream Decoration

// Interface
public interface Icecream {
    String makeIcecream();
}

// Base Component
public class SimpleIcecream implements Icecream {
    @Override
    public String makeIcecream() {
        return "Base Icecream";
    }
}

// Decorator
abstract class IcecreamDecorator implements Icecream {
    protected Icecream specialIcecream;

    public IcecreamDecorator(Icecream specialIcecream) {
        this.specialIcecream = specialIcecream;
    }

    public String makeIcecream() {
        return specialIcecream.makeIcecream();
    }
}

// Concrete Decorators
public class NuttyDecorator extends IcecreamDecorator {
    public NuttyDecorator(Icecream specialIcecream) {
        super(specialIcecream);
    }

    public String makeIcecream() {
        return specialIcecream.makeIcecream() + " + crunchy nuts";
    }
}

public class HoneyDecorator extends IcecreamDecorator {
    public HoneyDecorator(Icecream specialIcecream) {
        super(specialIcecream);
    }

    public String makeIcecream() {
        return specialIcecream.makeIcecream() + " + sweet honey";
    }
}

// Test
public class TestDecorator {
    public static void main(String args[]) {
        Icecream icecream = new HoneyDecorator(new NuttyDecorator(new SimpleIcecream()));
        System.out.println(icecream.makeIcecream());
    }
}
```

---
```java
// Example 2: Social Media Post Decoration

// Component
public interface Post {
    void create();
    void publish();
}

// Concrete Component
public class BasicPost implements Post {
    private String text;

    public BasicPost(String text) {
        this.text = text;
    }

    public void create() {
        System.out.println("Creating a basic post with text: " + text);
    }

    public void publish() {
        System.out.println("Publishing a basic post with text: " + text);
    }
}

// Decorator
abstract class PostDecorator implements Post {
    protected Post decoratedPost;

    public PostDecorator(Post decoratedPost) {
        this.decoratedPost = decoratedPost;
    }

    public void create() {
        decoratedPost.create();
    }

    public void publish() {
        decoratedPost.publish();
    }
}

// Concrete Decorators
public class PhotoPost extends PostDecorator {
    private String photoUrl;

    public PhotoPost(Post decoratedPost, String photoUrl) {
        super(decoratedPost);
        this.photoUrl = photoUrl;
    }

    public void publish() {
        System.out.println("Adding photo with url: " + photoUrl + " to post.");
        decoratedPost.publish();
    }
}

public class VideoPost extends PostDecorator {
    private String videoUrl;

    public VideoPost(Post decoratedPost, String videoUrl) {
        super(decoratedPost);
        this.videoUrl = videoUrl;
    }

    public void publish() {
        System.out.println("Adding video with url: " + videoUrl + " to post.");
        decoratedPost.publish();
    }
}

public class AudioPost extends PostDecorator {
    private String audioUrl;

    public AudioPost(Post decoratedPost, String audioUrl) {
        super(decoratedPost);
        this.audioUrl = audioUrl;
    }

    public void publish() {
        System.out.println("Adding audio with url: " + audioUrl + " to post.");
        decoratedPost.publish();
    }
}

// Test and Output
public class TestDecorator {
    public static void main(String[] args) {
        // Create a basic post
        Post post = new BasicPost("Hello world!");

        // Decorate the post with a photo
        post = new PhotoPost(post, "https://example.com/myphoto.jpg");

        // Decorate the post with a video
        post = new VideoPost(post, "https://example.com/myvideo.mp4");

        // Decorate the post with audio
        post = new AudioPost(post, "https://example.com/mysong.mp3");

        // Publish the fully decorated post
        post.publish();
    }
}
```
---
### Known Uses

- All subclasses of `java.io.InputStream`, `OutputStream`, `Reader`, and `Writer` have a constructor taking an instance of the same type.
- `java.util.Collections`, the `checkedXXX()`, `synchronizedXXX()`, and `unmodifiableXXX()` methods.
- `javax.servlet.http.HttpServletRequestWrapper` and `HttpServletResponseWrapper`
- `javax.swing.JScrollPane`

### Related Patterns

- **Adapter:**
    
    - A decorator is different from an adapter in that a decorator only changes an object's responsibilities, not its interface.
- **Composite:**
    
    - A decorator can be viewed as a degenerate composite with only one component. However, a decorator adds additional responsibilities (not for object aggregation).
- **Strategy:**
    
    - A decorator lets you change the skin of an object; a strategy lets you change the guts.

# Bridge Pattern

### Intent

Decouple an abstraction from its implementation so that the two can vary independently.

### Also Known As

Handle/Body

### Motivation

When an abstraction can have one of several possible implementations, the usual way to accommodate them is to use inheritance. However, this approach isn't always flexible enough. Inheritance binds an implementation to the abstraction permanently, making it difficult to modify, extend, and reuse abstractions and implementations independently. It's inconvenient to extend the class abstraction to cover different kinds of subclasses or new platforms, making client code platform-dependent. The Bridge pattern addresses these problems by putting the Window abstraction and its implementation in separate class hierarchies, letting them vary independently.

### Applicability

- You want to avoid a permanent binding between an abstraction and its implementation. This might be the case when the implementation must be selected or switched at run-time.
- Both the abstraction and their implementations should be extensible by subclassing.
- Changes in the implementation of an abstraction should have no impact on clients; their code should not have to be recompiled.
- You want the implementation of an abstraction completely hidden from clients.
- You want to share an implementation among multiple objects, and this fact should be hidden from the client.

### Structure

### Participants

- **Abstraction:**
  - Defines the abstraction's interface.
  - Maintains a reference to an object of type implementor.

- **Refined Abstraction:**
  - Extends the interface defined by Abstraction.

- **Implementor:**
  - Defines the interface for implementation classes.
  - Typically, the implementor interface provides only primitive operations, and Abstraction defines higher-level operations based on the primitives.

- **Concrete Implementor:**
  - Implements the Implementor interface and defines its concrete implementation.

### Collaborations

1. **Decoupling interface and implementation:**
   - The implementation of an abstraction can be configured at run-time, and it's even possible for an object to change its implementation at run-time. Changing an implementation class doesn't require recompiling the Abstraction class and its clients.

2. **Improved extensibility:**

3. **Hiding implementation details from clients:**

### Implementation

1. **Only one Implementor:**
   - In situations where there is only one implementation, creating an abstract Implementor class isn't necessary. This is a degenerate case of the Bridge pattern.

2. **Creating the right Implementor object:**
   - Decide which Implementor class to instantiate when there's more than one. If Abstraction knows about all ConcreteImplementor classes, it can instantiate one of them in its constructor. Another approach is to choose a default implementation initially and change it later according to usage.

3. **Sharing implementors:**
   - The Body stores a reference count that the Handle class increments and decrements.

4. **Using multiple inheritance:**
   - You can use multiple inheritance to combine an interface with its implementation. But because this approach relies on static inheritance, it binds an implementation permanently to its interface. Therefore, you can't implement a true Bridge with multiple inheritances.

### Sample Code

```java
// Example 1: Media Player

// Define the interface that represents the Abstraction.
public interface MediaPlayer {
   void play();
}

// Create a Concrete Abstraction class that implements the Abstraction interface.
public class AudioPlayer implements MediaPlayer {
   private MediaDecoder mediaDecoder;

   public AudioPlayer(MediaDecoder mediaDecoder) {
      this.mediaDecoder = mediaDecoder;
   }

   @Override
   public void play() {
      mediaDecoder.decode("audio");
   }
}

public class VideoPlayer implements MediaPlayer {
   private MediaDecoder mediaDecoder;

   public VideoPlayer(MediaDecoder mediaDecoder) {
      this.mediaDecoder = mediaDecoder;
   }

   @Override
   public void play() {
      mediaDecoder.decode("video");
   }
}

// Define the interface that represents the Implementation.
public interface MediaDecoder {
   void decode(String type);
}

// Create Concrete Implementation classes that implement the Implementation interface.
public class AudioDecoder implements MediaDecoder {
   @Override
   public void decode(String type) {
      System.out.println("Decoding audio " + type + " file...");
   }
}

public class VideoDecoder implements MediaDecoder {
   @Override
   public void decode(String type) {
      System.out.println("Decoding video " + type + " file...");
   }
}

// Create an instance of the Concrete Abstraction class and pass it an instance of the Concrete Implementation class.
MediaPlayer audioPlayer = new AudioPlayer(new AudioDecoder());
MediaPlayer videoPlayer = new VideoPlayer(new VideoDecoder());

audioPlayer.play();
videoPlayer.play();
// OUTPUT
// Decoding audio file...
// Decoding video file...
```

---

```java
// Example 2: Message Sender

// Define the interface that represents the Abstraction.
public interface MessageSender {
    void send(String message);
}

// Create a Concrete Abstraction class that implements the Abstraction interface.
public class UserMessageSender implements MessageSender {
    private MessageFormatter messageFormatter;
    private MessageChannel messageChannel;

    public UserMessageSender(MessageFormatter messageFormatter, MessageChannel messageChannel) {
        this.messageFormatter = messageFormatter;
        this.messageChannel = messageChannel;
    }

    @Override
    public void send(String message) {
        String formattedMessage = messageFormatter.format(message);
        messageChannel.sendMessage(formattedMessage);
    }
}

// Define the interface that represents the Implementation.
public interface MessageFormatter {
    String format(String message);
}

// Create Concrete Implementation classes that implement the Implementation interface.
public class TextMessageFormatter implements MessageFormatter {
    @Override
    public String format(String message) {
        return "Text message: " + message;
    }
}

public class HTMLMessageFormatter implements MessageFormatter {
    @Override
    public String format(String message) {
        return "<html><body><p>" + message + "</p></body></html>";
    }
}

// Define another interface that represents the Implementation.
public interface MessageChannel {
    void sendMessage(String message);
}

// Create Concrete Implementation classes that implement the Implementation interface.
public class EmailMessageChannel implements MessageChannel {
    @Override
    public void sendMessage(String message) {
        System.out.println("Sending email message: " + message);
    }
}

public class SMSMessageChannel implements MessageChannel {
    @Override
    public void sendMessage(String message) {
        System.out.println("Sending SMS message: " + message);
    }
}

public class PushNotificationChannel implements MessageChannel {
    @Override
    public void sendMessage(String message) {
        System.out.println("Sending push notification: " + message);
    }
}

// Create an instance of the Concrete Abstraction class and pass it instances of the Concrete Implementation classes.
MessageSender userMessageSender = new UserMessageSender(new TextMessageFormatter(), new EmailMessageChannel());
userMessageSender.send("Hello, world!");
```

### Known Uses

- `new LinkedHashMap(LinkedHashSet<K>, List<V>)`, which returns an unmodifiable linked map that doesn't clone the items but uses them. The `java.util.Collections#newSetFromMap()` and `singletonXXX()` methods, however, come close.

### Related Patterns

- An Abstract Factory can create and configure a particular Bridge.
- The Adapter pattern is geared toward making unrelated classes work together.

# Chapter 5: Behavioral Patterns

Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects. These patterns characterize complex control flow that's difficult to follow at run-time. Behavioral class patterns use inheritance to distribute behavior between classes.

## Strategy Pattern

### Intent

Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

### Also Known As

- Policy

### Motivation

- Multiple algorithms in one place can lead to problems.
- Many if-else statements may be required.
- Unnecessary and accidental dependencies may arise between algorithms.

Hard-wiring all such algorithms into the classes that require them isn't desirable for several reasons:
- Clients that need the algorithm get more complex if they include the algorithm code.
- Different algorithms will be appropriate at different times.
- It's difficult to add new algorithms and vary existing ones when the algorithm is an integral part of a client.

We can avoid these problems by defining classes that encapsulate different algorithms.

### Applicability

- Many related classes differ only in their behavior. Strategies provide a way to configure a class with one of many behaviors.
- You need different variants of an algorithm.
- An algorithm uses data that clients shouldn't know about.
- A class defines many behaviors, and these appear as multiple conditional statements in operations.

### Structure

#### Participants

- **Strategy:**
  - Declares an interface common to all supported algorithms.
  - Context uses this interface to call the algorithm defined by a ConcreteStrategy.

- **Concrete Strategy:**
  - Implements the algorithm using the Strategy interface.

- **Context:**
  - Is configured with a ConcreteStrategy object.
  - Maintains a reference to a Strategy object.
  - May define an interface that lets Strategy access its data.

#### Collaborations

- Strategy and Context interact to implement the chosen algorithm. A context may pass all data required by the algorithm to the strategy when the algorithm is called. Alternatively, the context can pass itself as an argument to Strategy operations.
- A context forwards requests from its clients to its strategy.

#### Consequences

1. **Families of related algorithms:**
   Hierarchies of Strategy classes define a family of algorithms or behaviors for the context to reuse. Inheritance can help factor out common functionality of the algorithms.

2. **An alternative to subclassing:**
   Encapsulating the algorithm in separate Strategy classes lets you vary the algorithm independently of its context, making it easier to switch, understand, and extend.

3. **Strategies eliminate conditional statements:**
   Encapsulating the behavior in separate Strategy classes eliminates conditional statements.

4. **A choice of implementations:**
   Strategies can provide different implementations of the same behavior. The client can choose among strategies with different time and space trade-offs.

5. **Clients must be aware of different Strategies:**
   The pattern has a potential drawback in that a client must understand how Strategies differ before it can select the appropriate one. Therefore, you should use the Strategy pattern only when the variation in behavior is relevant to clients.

6. **Communication between Strategy and Context:**
   The strategy interface is shared by all ConcreteStrategy classes, whether the algorithms they implement are trivial or complex. That means there will be times when the context creates and initializes parameters that never get used.

7. **Increased number of objects:**

### Implementation

1. **Defining Strategy and Context interfaces:**
   The Strategy and Context interfaces must give a ConcreteStrategy efficient access to any data it needs from a context and vice versa. One approach is to have the Context pass data in parameters to Strategy operations—in other words, take the data to the strategy. Another technique has a context pass itself as an argument, and the strategy requests data from the context explicitly.

2. **Strategies as template parameters:**

3. **Making Strategy objects optional:**
   The context class may be simplified if it's meaningful not to have a Strategy object. The Context checks to see if it has a Strategy object before accessing it. If there is one, then Context uses it normally. If there isn't a strategy, then Context carries out default behavior.

### Sample Code

```java
// Define the interface that represents the Strategy.
public interface ShippingStrategy {
    double calculate(double weight);
}

// Implement different shipping strategies.
public class StandardShipping implements ShippingStrategy {
    public double calculate(double weight) {
        return weight * 0.5; // $0.50 per pound
    }
}

public class ExpeditedShipping implements ShippingStrategy {
    public double calculate(double weight) {
        return weight * 1.5; // $1.50 per pound
    }
}

public class FreeShipping implements ShippingStrategy {
    public double calculate(double weight) {
        return 0.0; // free shipping
    }
}

// Create a ShippingCalculator class that takes a ShippingStrategy as a parameter.
public class ShippingCalculator {
    private ShippingStrategy strategy;

    public ShippingCalculator(ShippingStrategy strategy) {
        this.strategy = strategy;
    }

    public double calculateShippingCost(double weight) {
        return strategy.calculate(weight);
    }
}

// Use the ShippingCalculator class to calculate the shipping cost using different shipping strategies.
ShippingCalculator calculator = new ShippingCalculator(new StandardShipping());
double cost = calculator.calculateShippingCost(10.0); // $5.00

calculator = new ShippingCalculator(new ExpeditedShipping());
cost = calculator.calculateShippingCost(10.0); // $15.00

calculator = new ShippingCalculator(new FreeShipping());
cost = calculator.calculateShippingCost(10.0); // $0.00
```

---

```java
// Building an e-commerce website with different pricing strategies for products.

// Define the interface that specifies the calculatePrice method.
public interface PricingStrategy {
    double calculatePrice(Product product);
}

// Implement different pricing strategies.
public class DefaultPricingStrategy implements PricingStrategy {
    public double calculatePrice(Product product) {
        return product.getBasePrice();
    }
}

public class DiscountPricingStrategy implements PricingStrategy {
    public double calculatePrice(Product product) {
        return product.getBasePrice() * 0.8; // 20% discount
    }
}

public class PremiumPricingStrategy implements PricingStrategy {
    public double calculatePrice(Product product) {
        return product.getBasePrice() * 1.2; // 20% premium
    }
}

// Create a Product class that contains the product's data.
public class Product {
    private String name;
    private double basePrice;

    public Product(String name, double basePrice) {
        this.name = name;
        this.basePrice = basePrice;
    }

    public double calculatePrice(PricingContext pricingContext) {
        return pricingContext.calculatePrice(this);
    }
    // getters and setters
}

// Create a class that contains a PricingStrategy instance and provides a unified interface for calculating prices.
public class PricingContext {
    private PricingStrategy pricingStrategy;

    public PricingContext(PricingStrategy pricingStrategy) {
        this.pricingStrategy = pricingStrategy;
    }

    public double calculatePrice(Product product) {
        return pricingStrategy.calculatePrice(product);
    }
}

// Test and Output
PricingContext defaultContext = new PricingContext(new DefaultPricingStrategy());
PricingContext discountContext = new PricingContext(new DiscountPricingStrategy());
PricingContext premiumContext = new PricingContext(new PremiumPricingStrategy());

Product book = new Product("Book", 10.0);
Product laptop = new Product("Laptop", 500.0);
Product shirt = new Product("Shirt", 20.0);

double bookPrice = book.calculatePrice(defaultContext); // $10.0
double laptopPrice = laptop.calculatePrice(discountContext); // $400.0 (20% discount)
double shirtPrice = shirt.calculatePrice(premiumContext); // $24.0 (20% premium)
```

### Known Uses

- `java.util.Comparator#compare()`, executed by, among others, `Collections#sort()`.
- `javax.servlet.http.HttpServlet`, the `service()` and all `doXXX()` methods take `HttpServletRequest` and `HttpServletResponse`, and the implementor has to process them.
- `javax.servlet.Filter#doFilter()`.

### Related Pattern

Flyweight: Strategy objects often make good flyweights.


# Command Pattern

## Intent

Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

### Also Known As

Action, Transaction

## Motivation

- Bilmediğiniz birine gerçekte ne olduğunu bilmediğiniz bir işi, çok genel bir emirle, “yap” diye söylüyorsunuz ve o ne yapacağını bildiği için yapması gerekeni yapıyor.
  
- Buradaki “yap” emri çok genel bir emirdir, herhangi özel bir hareketi değil, sadece yapanın yapmasını bildiği şeyi temsil eder.
  
- Command kalıbı, Strateji’nin daha genel hali olarak, sadece isteği alan nesnenin değil metodun da saklandığı çözüm olarak görülebilir.

  Sometimes, it's necessary to issue requests to an object without knowing anything about the operation being requested or the receiver of the request. The Command pattern makes requests of unspecified application objects by turning the request itself into an object. This object can be stored and passed around like other objects. The key to this pattern is an abstract Command class which declares an interface for executing operations.

## Applicability

- Parameterize objects by an action to perform. You can express such parameterization in a procedural language with a "callback" function. Commands are an object-oriented replacement for callbacks.
  
- Specify, queue, and execute requests at different times.
  
- Support undo. The command's Execute operation can store state for reversing its effects in the command itself. Executed commands are stored in a history list.
  
- Support logging changes so that they can be reapplied in case of a system crash. By augmenting the Command interface with load and store operations, you can keep a persistent log of changes.
  
- Structure a system around high-level operations built on primitive operations.

## Structure

### Participants

- **Command:**
  Declares an interface for executing an operation.
  
- **ConcreteCommand:**
  Defines a binding between a Receiver object and an action. Implements Execute by invoking the corresponding operation(s) on Receiver.
  
- **Client:**
  Creates a ConcreteCommand object and sets its receiver.
  
- **Invoker:**
  Asks the command to carry out the request.
  
- **Receiver:**
  Knows how to perform the operations associated with carrying out a request. Any class may serve as a Receiver.

### Collaborations

- The client creates a ConcreteCommand object and specifies its receiver.
  
- An Invoker issues a request by calling Execute on the command.
  
- The ConcreteCommand object invokes operations on its receiver to carry out the request.

### Consequences

1. Command decouples the object that invokes the operation from the one that knows how to perform it.
  
2. Commands are first-class objects. They can be manipulated and extended like any other objects.
  
3. You can assemble commands into a composite command.
  
4. It's easy to add new commands because you don't have to change existing classes.

## Implementation

1. **How intelligent should a command be?**
   A command can have a wide range of abilities.
  
2. **Supporting undo and redo**
   Commands can support undo and redo capabilities if they provide a way to reverse their execution. A ConcreteCommand class might need to store additional state to do so. This state can include:
   - The Receiver object, which actually carries out operations in response to the request.
   - The arguments to the operation performed on the receiver.
   - Any original values in the receiver that can change as a result of handling the request. To support one level of undo, an application needs to store only the command that was executed last. For multiple-level undo and redo, the application needs a "history list" of commands that have been executed.
  
3. **Avoiding error accumulation in the undo process**
   Errors can accumulate as commands are executed, unexecuted, reexecuted repeatedly, so it may be necessary to store more information in the command to ensure that objects are restored to their original state.

## Sample Code

```java
// Step 1: Define the command interface
public interface Command {
    void execute();
}

// Step 2: Define the receiver class
public class Receiver {
    public void doSomething() {
        System.out.println("Doing something...");
    }
}

// Step 3: Implement the concrete command classes
public class ConcreteCommand1 implements Command {
    private final Receiver receiver;

    public ConcreteCommand1(Receiver receiver) {
        this.receiver = receiver;
    }

    public void execute() {
        receiver.doSomething();
    }
}

public class ConcreteCommand2 implements Command {
    private final Receiver receiver;

    public ConcreteCommand2(Receiver receiver) {
        this.receiver = receiver;
    }

    public void execute() {
        System.out.println("Doing something else...");
        receiver.doSomething();
    }
}

// Step 4: Use the commands
public class Client {
    public static void main(String[] args) {
        Receiver receiver = new Receiver();
        Command command1 = new ConcreteCommand1(receiver);
        Command command2 = new ConcreteCommand2(receiver);

        command1.execute();
        command2.execute();
    }
}
```

Test & Output:

```java
Doing something...
Doing something else...
Doing something...
```

### Example with Undo and Redo

A text editor application that supports multiple document types. Each document type has its own set of operations (e.g., open, save, cut, copy, paste, spell check). We want to design the text editor in a way that allows us to add new document types and operations easily, without affecting the existing codebase. We also want to be able to undo and redo the user's actions.

```java
// Create a Command interface
public interface Command {
    void execute();
    void undo();
}

// Create command classes for each operation
public class OpenDocumentCommand implements Command {
    private Document document;

    public OpenDocumentCommand(Document document) {
        this.document = document;
    }

    public void execute() {
        document.open();
    }

    public void undo() {
        document.close();
    }
}

public class SaveDocumentCommand implements Command {
    private Document document;

    public SaveDocumentCommand(Document document) {
        this.document = document;
    }

    public void execute() {
        document.save();
    }

    public void undo() {
        // Not possible to undo a save operation
    }
}

public class CutCommand implements Command {
    private Document document;

    public CutCommand(Document document) {
        this.document = document;
    }

    public void execute() {
        document.cut();
    }

    public void undo() {
        document.undoCut();
    }
}

// ... (Similar implementations for other commands)

// Create an Invoker class
public class ToolbarButton {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void click() {
        command.execute();
    }

    public void undo() {
        command.undo();
    }
}

// Add support for undo and redo
public static void main(String[] args) {
    Document document = new RichTextDocument();
    ToolbarButton openButton = new ToolbarButton();
    ToolbarButton saveButton = new ToolbarButton();
    ToolbarButton cutButton = new ToolbarButton();
    ToolbarButton copyButton = a ToolbarButton();
    // ... (Create buttons for other operations)

    // Set the commands for each button
    openButton.setCommand(new OpenDocumentCommand(document));
    saveButton.setCommand(new SaveDocumentCommand(document));
    cutButton.setCommand(new CutCommand(document));
    copyButton.setCommand(new CopyCommand(document));
    // ... (Set commands for other buttons)

    // Perform actions
    openButton.click();
    cutButton.click();
    copyButton.click();
    // ... (Perform other actions)

    // Undo the last two actions
    undoButton.click();
    undoButton.click();

    // Redo the last undone action
    redoButton.click();
}
```

Output:

```java
Opening rich text document...
Cutting text...
Copying text...
Undoing spell check...
Undoing paste...
Redoing paste...
```

## Known Uses

- All implementations of `java.lang.Runnable`
    
- All implementations of `javax.swing.Action`
    

## Related Patterns

- A composite can be used to implement MacroCommands.
    
- A memento can keep state the command requires to undo its effect.
    
- A command that must be copied before being placed on the history list acts as a Prototype.


# Iterator Pattern

## Intent

Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

### Also Known As

Cursor

## Motivation

The key idea in this pattern is to take the responsibility for access and traversal out of the list object and put it into an "iterator" object. An iterator object is responsible for keeping track of the current element; that is, it knows which elements have been traversed already. Separating the traversal mechanism from the List object lets us define iterators for different traversal policies without enumerating them in the List interface.

## Applicability

- To access an aggregate object's contents without exposing its internal representation.

- To support multiple traversals of aggregate objects.

- To provide a uniform interface for traversing different aggregate structures.

## Structure

### Participants

- **Iterator:**
  Defines an interface for accessing and traversing elements.

- **ConcreteIterator:**
  Implements the Iterator interface. Keeps track of the current position in the traversal of the aggregate.

- **Aggregate:**
  Defines an interface for creating an Iterator object.

- **ConcreteAggregate:**
  Implements the Iterator creation interface to return an instance of the proper ConcreteIterator.

### Collaborations

- A ConcreteIterator keeps track of the current object in the aggregate and can compute the succeeding object in the traversal.

### Consequences

1. **It supports operations in the traversal of an aggregate.**

2. **Iterators simplify the Aggregate interface.**

3. **More than one traversal can be pending on an aggregate.**
   An iterator keeps track of its traversal state. Therefore, you can have more than one traversal in progress at once.

## Implementation

1. **Who controls iteration?**
   A fundamental issue is deciding which party controls the iteration: the iterator or the client that uses the iterator.
   - When the client controls iteration -> External iterator.
   - When the iterator controls iteration -> Internal iterator.
   External iterators are more flexible than internal iterators. Internal iterators are easier to use because they define the iteration logic for you.

2. **Who defines the traversal algorithm?**
   The aggregate might define the traversal algorithm and use the iterator to store just the state of the iteration (cursor).

3. **How robust is the iterator?**
   It can be dangerous to modify an aggregate while you're traversing it. A sample solution is to copy the aggregate and traverse the copy, but that's too expensive to do in general.

4. **Additional Iterator operations**
   The minimal interface to Iterator consists of the operations First, Next, IsDone, and CurrentItem.

5. **Using polymorphic iterators**
   Polymorphic iterators have their cost. They require the iterator object to be allocated dynamically by a factory method. Hence, they should be used only when there's a need for polymorphism. Polymorphic iterators have another drawback: the client is responsible for deleting them.

6. **Iterators may have privileged access**

7. **Iterators for composites**

8. **Null iterators**
   A "Nulliterator" is a degenerate iterator that's helpful for handling boundary conditions. The isDone operation always evaluates to true.

## Sample Code

```java
public class MyIterable implements Iterable<String> {
    private ArrayList<String> list = new ArrayList<>();

    public void add(String str) {
        list.add(str);
    }

    @Override
    public Iterator<String> iterator() {
        return list.iterator();
    }

    public static void main(String[] args) {
        MyIterable myIterable = new MyIterable();
        myIterable.add("Hello");
        myIterable.add("World");

        for (String str : myIterable) {
            System.out.println(str);
        }
    }
}
```

## Known Uses

- All implementations of `java.util.Iterator` (thus among others also `java.util.Scanner!`).
    
- All implementations of `java.util.Enumeration`
    

## Related Patterns

- Composite: Iterators are often applied to recursive structures such as Composites.

# Template Method Pattern

## Intent

Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm structure.

### Motivation

The template method pattern provides a way to define a skeletal structure for a group of classes, allowing for code reuse, flexibility, and easier maintenance. It strikes a balance between providing a common structure and allowing subclasses to customize certain parts of the algorithm to suit their specific needs. A template method defines an algorithm in terms of abstract operations that subclasses override to provide concrete behavior.

## Applicability

- To implement the invariant parts of an algorithm once and leave it up to subclasses to implement the behavior that can vary.

- When common behavior among subclasses should be factored and localized in a common class to avoid code duplication. This is a good example of "refactoring to generalize."

- To control subclasses' extensions. You can define a template method that calls "hook operations" at specific points, thereby permitting extensions only at those points.

## Participants

- **AbstractClass:**
  Defines abstract "primitive operations" that concrete subclasses define to implement steps of an algorithm. Implements a template method defining the skeleton of an algorithm.

- **ConcreteClass:**
  Implements the primitive operations to carry subclass-specific steps of the algorithm.

## Collaborations

- ConcreteClass relies on AbstractClass to implement the invariant steps of the algorithm.

## Consequences

- Template Methods are a fundamental technique for code reuse.

- Template Methods lead to an inverted control structure that's sometimes referred to as "the Hollywood principle" — that is, "Don't call us, we'll call you."

- Template methods call the following kinds of operations:
  - Concrete operations.
  - Concrete AbstractClass operations.
  - Primitive operations.
  - Factory methods.
  - "Hook operations" — an optional method that is declared in the base class but does not have a default implementation.

## Implementation

1. **Minimizing primitive operations:**
   An important goal in designing template methods is to minimize the number of primitive operations that a subclass must override to flesh out the algorithm.

2. **Naming conventions:**
   You can identify the operations that should be overridden by adding a prefix to their names.

## Sample Code

```java
// Create an abstract base class for the character
public abstract class Character {

    public final void move() {
        // Step 1: Get the current position
        int currentPosition = getCurrentPosition();

        // Step 2: Calculate the new position
        int newPosition = calculateNewPosition(currentPosition);

        // Step 3: Move to the new position
        moveTo(newPosition);
    }

    protected abstract int getCurrentPosition();

    protected abstract int calculateNewPosition(int currentPosition);

    protected abstract void moveTo(int newPosition);
}

// Create a subclass for each type of character
public class PlayerCharacter extends Character {
    private int currentPosition = 0;

    @Override
    protected int getCurrentPosition() {
        return currentPosition;
    }

    @Override
    protected int calculateNewPosition(int currentPosition) {
        return currentPosition + 1;
    }

    @Override
    protected void moveTo(int newPosition) {
        System.out.println("Moving player character to position " + newPosition);
        currentPosition = newPosition;
    }
}

// Use the template method to move the character
public static void main(String[] args) {
    PlayerCharacter player = new PlayerCharacter();
    player.move();
    player.move();
    player.move();
}
```

### Output

```java
Moving player character to position 1
Moving player character to position 2
Moving player character to position 3
```

---

```java
// Create a base class called Authenticator for a web application
public abstract class Authenticator {

    public final User authenticate(String username, String password) {
        validateInput(username, password);
        User user = findUserByUsername(username);
        verifyPassword(user, password);
        checkAuthorization(user);
        return user;
    }

    protected abstract User findUserByUsername(String username);

    protected abstract void verifyPassword(User user, String password);

    protected void checkAuthorization(User user) {
        // Default implementation for checking user authorization based on roles
        // This can be overridden by concrete authenticators if necessary
    }

    private void validateInput(String username, String password) {
        // Input validation for username and password
    }
}

// Concrete classes
public class LdapAuthenticator extends Authenticator {
    // Implementation for finding user in LDAP directory and more
}

public class OAuthAuthenticator extends Authenticator {
    // Implementation for finding user in OAuth provider and more
}

// Test & Output
public static void main(String[] args) {
    Authenticator ldapAuthenticator = new LdapAuthenticator();
    User ldapUser = ldapAuthenticator.authenticate("jdoe", "password");
    System.out.println("LDAP authenticated user: " + ldapUser);

    Authenticator oauthAuthenticator = new OAuthAuthenticator();
    User oauthUser = oauthAuthenticator.authenticate("jdoe", null);
    System.out.println("OAuth authenticated user: " + oauthUser);
}
```

## Known Uses

- All non-abstract methods of `java.io.InputStream`, `java.io.OutputStream`, `java.io.Reader`, and `java.io.Writer`.
    
- All non-abstract methods of `java.util.AbstractList`, `java.util.AbstractSet`, and `java.util.AbstractMap`.
    
- `javax.servlet.http.HttpServlet`: All the doXXX() methods by default send a HTTP 405 "Method Not Allowed" error to the response. You're free to implement none or any of them.
    

## Related Patterns

- Factory methods are often called by template methods.
    
- Strategy: Template methods use inheritance to vary part of an algorithm. Strategy uses delegation to vary the entire algorithm.

# Observer Pattern

## Intent

Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

### Also Known As

Dependents, Publish-Subscribe

## Motivation

A common side effect of partitioning a system into a collection of cooperating classes is the need to maintain consistency between related objects. You don't want to achieve consistency by making the classes tightly coupled because that reduces their reusability.

The key objects in this pattern are "subject" and "observer." A subject may have any number of dependent observers. All observers are notified whenever the subject undergoes a change in state. In response, each observer will query the subject to synchronize the state with the subject's state.

This kind of interaction is also known as "publish-subscribe." The subject is the publisher of notifications. It sends out these notifications without having to know who its observers are. Any number of observers can subscribe to receive notifications.

## Applicability

- When abstraction has two aspects, one dependent on the other.

- When a change to one object requires changing others, and you don't know how many objects need to be changed.

- When an object should be able to notify other objects without making assumptions about who these objects are. In other words, you don't want these objects tightly coupled.

## Structure

### Participants

- **Subject:**
  Knows its observers. Any number of observer objects may observe a subject. Provides an interface for attaching and detaching Observer objects.

- **Observer:**
  Defines an updating interface for objects that should be notified of changes in a subject.

- **ConcreteSubject:**
  Stores the state of interest to ConcreteObserver objects. Sends a notification to its observers when its state changes.

- **ConcreteObserver:**
  Maintains a reference to a ConcreteSubject object. Stores state that should stay consistent with the subject's. Implements the Observer updating interface to keep its state consistent with the subject's.

### Collaborations

- ConcreteSubject notifies its observers whenever a change occurs that could make its observers' state inconsistent with its own.

- After being informed of a change in the concrete subject, a ConcreteObserver object may require the subject for information.

## Consequences

1. **Abstract coupling between Subject and Observer:**
   All a subject knows is that it has a list of observers, each conforming to the simple interface of the abstract Observer class. Because Subject and Observer aren't tightly coupled, they can belong to different layers of abstraction in a system.

2. **Support for broadcast communication:**
   Unlike an ordinary request, the notification that a subject sends needn't specify its receiver. The subject doesn't care how many interested objects exist; its only responsibility is to notify observers. This gives you the freedom to add and remove observers at any time.

3. **Unexpected Updates:**
   Because observers have no knowledge of each other's presence, they can be blind to the ultimate cost of changing the subject. Without additional protocol to help observers discover what changed, they may be forced to work hard to deduce the changes.

## Implementation

1. **Mapping subjects to their observers:**
   The simplest way for a subject to keep track of the observers it should notify is to store references to them explicitly in the subject.

2. **Observing more than one subject:**

3. **Who triggers the update?**
   The subject and its observers rely on the notification mechanism to stay consistent.
   
   - (a): Have state-setting operations on Subject call Notify after they change the subject's state. The advantage is that clients don't have to remember to call Notify on the subject. The disadvantage is that several consecutive operations will cause several consecutive updates which may be inefficient.
   
   - (b): Make clients responsible for calling Notify at the right time. The advantage is that clients can wait to trigger the update until after a series of state changes has been made, thereby avoiding needless updates. The disadvantage is that clients have an added responsibility to trigger the update, making errors more likely since clients can forget to call Notify.

4. **Dangling reference to deleted subjects:**
   Deleting a subject should not produce dangling references in its observers. One way to avoid dangling references is to make the subject notify its observers as it is deleted so that they can reset their reference to it.

5. **Making sure Subject state is self-consistent before notification:**
   Because observers query the subject for its current state in the course of updating their own state.

6. **Avoiding observer-specific update protocols:**
   At one extreme, which we call the "push model," the subject sends observers detailed information about the change whether they want it or not. At the other extreme is the "pull model," where the subject sends nothing but the most minimal notification, and observers ask for details explicitly thereafter. The pull model emphasizes the subject's ignorance of its observers, whereas the push model assumes subjects know something about their observers.

7. **Specifying modifications of interest explicitly:**

8. **Encapsulating complex update semantics:**
   When the dependency relationship between subjects and observers is particularly complex, an object that maintains these relationships might be required. Its purpose is to minimize the work required to make observers reflect a change in their subject.

   - **ChangeManager Responsibilities:**
     - (a) It maps a subject to its observers and provides an interface to maintain this mapping.
     - (b) It defines a particular update strategy.
     - (c) It updates all dependent observers at the request of a subject.

9. **Combining the Subject and Observer classes:**

## Sample Code

```java
// Step 1: Define the Subject interface
public interface Subject {
    public void addObserver(Observer observer);
    public void removeObserver(Observer observer);
    public void notifyObservers();
}

// Step 2: Define the Observer interface
public interface Observer {
    public void update();
}

// Step 3: Implement the Subject class
public class WeatherStation implements Subject {
    private List<Observer> observers;
    private double temperature;

    public WeatherStation() {
        observers = new ArrayList<>();
    }

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }

    public void setTemperature(double temperature) {
        this.temperature = temperature;
        notifyObservers();
    }

    public double getTemperature() {
        return temperature;
    }
}

// Step 4: Implement the Observer class
public class PhoneDisplay implements Observer {
    private double temperature;

    public void update() {
        display();
    }

    public void display() {
        System.out.println("Phone Display: " + temperature + " degrees");
    }
}

// Step 5: Register the Observer with the Subject
public class Main {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();
        PhoneDisplay phoneDisplay = new PhoneDisplay();

        weatherStation.addObserver(phoneDisplay);

        weatherStation.setTemperature(75.0);
    }
}
```

### Output

```java
Phone Display: 75.0 degrees
```

---
```java
// Additional Sample Code

/*
A weather station that measures temperature, humidity, and pressure. We want to be able to notify different types of display devices when the weather conditions change. 
For example, we might want to display the weather on a web page, on a mobile app, or on a smartwatch.
*/

// Step 1: Define the Subject interface
public interface WeatherDataSubject {
    public void registerObserver(WeatherDataObserver observer);
    public void removeObserver(WeatherDataObserver observer);
    public void notifyObservers();
}

// Step 2: Define the Observer interface 
// update() method that will be called by the Subject when its state changes.
public interface WeatherDataObserver {
    public void update(double temperature, double humidity, double pressure);
}

// Step 3: Implement the Subject class
// WeatherData class that will keep track of the current temperature, humidity, and pressure, and notify its Observers when any of these values change.
public class WeatherData implements WeatherDataSubject {
    private List<WeatherDataObserver> observers;
    private double temperature;
    private double humidity;
    private double pressure;

    public WeatherData() {
        observers = new ArrayList<>();
    }

    public void registerObserver(WeatherDataObserver observer) {
        observers.add(observer);
    }

    public void removeObserver(WeatherDataObserver observer) {
        observers.remove(observer);
    }

    public void notifyObservers() {
        for (WeatherDataObserver observer : observers) {
            observer.update(temperature, humidity, pressure);
        }
    }

    public void setMeasurements(double temperature, double humidity, double pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        notifyObservers();
    }

    public double getTemperature() {
        return temperature;
    }

    public double getHumidity() {
        return humidity;
    }

    public double getPressure() {
        return pressure;
    }
}

// Step 4: Implement the Observer classes
public class CurrentConditionsDisplay implements WeatherDataObserver {
    private double temperature;
    private double humidity;
    private double pressure;

    public void update(double temperature, double humidity, double pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        display();
    }

    public void display() {
        System.out.println("Current conditions: " + temperature + "F degrees, " + humidity + "% humidity, " + pressure + " pressure");
    }
}

public class MobileAppDisplay implements WeatherDataObserver {
    private double temperature;

    public void update(double temperature, double humidity, double pressure) {
        this.temperature = temperature;
        display();
    }

    public void display() {
        System.out.println("Current temperature: " + temperature + "F degrees");
    }
}

// Step 5: Test the Observer pattern
public class WeatherStation {
    public static void main(String[] args) {
        WeatherData weatherData = new WeatherData();

        CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay();
        MobileAppDisplay mobileDisplay = new MobileAppDisplay();

        weatherData.registerObserver(currentDisplay);
        weatherData.registerObserver(mobileDisplay);

        weatherData.setMeasurements(25.0, 70.0, 1013.25);
    }
}
```

### Output

```java
Current conditions: Temperature 25.0°C, Humidity 70.0%, Pressure 1013.25hPa
Mobile App Display: Temperature 25.0°C
```

## Known Uses

- `java.util.Observer/java.util.Observable` (rarely used in the real world, though)
- All implementations of `java.util.EventListener` (practically all over Swing thus)
- `javax.servlet.http.HttpSessionBindingListener`
- `javax.servlet.http.HttpSessionAttributeListener`
- `javax.faces.event.PhaseListener`

## Related Patterns

- **Mediator:** By encapsulating complex update semantics, the ChangeManager acts as a mediator between subjects and observers.
    
- **Singleton:** The ChangeManager may use the Singleton pattern to make it unique and globally accessible. Same as above, please.

# Memento Pattern

## Intent

Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.

### Also Known As

Token

## Motivation

Sometimes it's necessary to record the internal state of an object. This is required when implementing checkpoints and undo mechanisms that let users back out of tentative operations or recover from errors. You must save state information somewhere so that you can restore objects to their previous state.

A "memento" is an object that stores a snapshot of the internal state of another object, the memento's "originator."

## Applicability

- A snapshot of an object's state must be saved so that it can be restored to that state later.
- A direct interface to obtaining the state would expose implementation details and break the object's encapsulation.

## Structure

### Participants

- **Memento:**
    
    - Stores internal state of the Originator object.
    - May store as much or as little of the originator's internal state as necessary at its originator's discretion.
    - Protects against access by objects other than the originator.
- **Originator:**
    
    - Creates a memento containing a snapshot of its current internal state.
    - Uses memento to restore its internal state.
- **Caretaker:**
    
    - Is responsible for the memento's safekeeping.
    - Never operates on or examines the contents of a memento.

### Collaborations

- A caretaker requests a memento from an originator, holds it for a time, and passes it back to the originator.
- Sometimes the caretaker won't pass the memento back to the originator because the originator might never need to revert to an earlier state.
- Mementos are passive. Only the originator that created a memento will assign or retrieve its state.

## Consequences

1. **Passing encapsulation boundaries:** The pattern shields other objects from potentially complex Originator internals, thereby preserving encapsulation boundaries.
    
2. **It simplifies Originator:** Originator keeps the versions of internal state that clients have requested. That puts all the storage management burden on Originator.
    
3. **Using mementos might be expensive:** Mementos might incur considerable overhead if the Originator must copy large amounts of information to store in the memento or if clients create and return mementos to the originator often enough.
    
4. **Defining narrow and wide interfaces:**
    
5. **Hidden costs in caring for mementos:** A caretaker is responsible for deleting the mementos it cares for. However, the caretaker has no idea how much state is in the memento.
    

## Implementation

1. **Language support:** Mementos have two interfaces; a wide one for originators and a narrow one for other objects. Ideally, the implementation language will support two levels of static protection.
    
2. **Storing incremental changes:**
    

## Sample Code

```java
// A TextEditor class that allows users to write and edit text. We want to implement an "undo" feature that allows users to revert back to the previous state of the text.

// Step 1: Create the TextEditor class:

public class TextEditor {
    private String text;

    public TextEditor() {
        this.text = "";
    }

    public void write(String content) {
        this.text += content;
        System.out.println("Text written: " + this.text);
    }

    public void undo() {
        // TODO: Implement the undo functionality
    }
}

// Step 2: Create the TextEditorMemento class to represent the state of the TextEditor:

public class TextEditorMemento {
    private String savedText;

    public TextEditorMemento(String text) {
        this.savedText = text;
    }

    public String getSavedText() {
        return savedText;
    }
}

// Step 3: Update the TextEditor class to support saving and restoring state using the TextEditorMemento:

public class TextEditor {
    private String text;

    public TextEditor() {
        this.text = "";
    }

    public void write(String content) {
        this.text += content;
        System.out.println("Text written: " + this.text);
    }

    public TextEditorMemento save() {
        return new TextEditorMemento(this.text);
    }

    public void restore(TextEditorMemento memento) {
        this.text = memento.getSavedText();
        System.out.println("Text restored: " + this.text);
    }

    public void undo() {
        // TODO: Implement the undo functionality
    }
}

// Step 4: Implement the undo functionality in the TextEditor class using a caretaker object:

public class TextEditor {
    private String text;
    private Stack<TextEditorMemento> undoStack;

    public TextEditor() {
        this.text = "";
        this.undoStack = new Stack<>();
    }

    public void write(String content) {
        this.text += content;
        System.out.println("Text written: " + this.text);
    }

    public TextEditorMemento save() {
        TextEditorMemento memento = new TextEditorMemento(this.text);
        undoStack.push(memento);
        return memento;
    }

    public void restore(TextEditorMemento memento) {
        this.text = memento.getSavedText();
        System.out.println("Text restored: " + this.text);
    }

    public void undo() {
        if (!undoStack.isEmpty()) {
            TextEditorMemento memento = undoStack.pop();
            this.text = memento.getSavedText();
            System.out.println("Undo completed. Text restored: " + this.text);
        } else {
            System.out.println("Nothing to undo.");
        }
    }
}

// Step 5: Test the TextEditor class by writing some text and performing undo operations:

public class Main {
    public static void main(String[] args) {
        TextEditor editor = new TextEditor();

        editor.write("Hello, ");
        TextEditorMemento memento1 = editor.save();

        editor.write("world!");
        TextEditorMemento memento2 = editor.save();

        editor.undo(); // Undo "world!"
        editor.undo(); // Undo "Hello, "
        editor.undo(); // Nothing to undo.
    }
}
```

### Output

```java
Text written: Hello,
Text written: Hello, world!
Undo completed. Text restored: Hello,
Undo completed. Text restored: 
Nothing to undo.
```

---
```java
// A BankAccount class that has a balance and allows transfers to be made to other accounts. We want to implement an "undo" feature that allows users to revert back to the previous state of the account.

// Step 1: Create the BankAccount class:

public class BankAccount {
    private int balance;
    private Stack<Memento> undoStack;

    public BankAccount(int initialBalance) {
        this.balance = initialBalance;
        this.undoStack = new Stack<>();
    }

    public void transfer(int amount, BankAccount recipient) {
        if (this.balance >= amount) {
            this.balance -= amount;
            recipient.deposit(amount);
            System.out.println("$" + amount + " transferred from Account #" + this.hashCode() + " to Account #" + recipient.hashCode() + ".");
            this.saveState();
        } else {
            System.out.println("Insufficient funds.");
        }
    }

    public void deposit(int amount) {
        this.balance += amount;
        System.out.println("$" + amount + " deposited into Account #" + this.hashCode() + ".");
        this.saveState();
    }

    public void undo() {
        if (!undoStack.isEmpty()) {
            Memento memento = undoStack.pop();
            this.balance = memento.getSavedBalance();
            System.out.println("Undo completed. Account #" + this.hashCode() + " balance restored to $" + this.balance + ".");
        } else {
            System.out.println("Nothing to undo.");
        }
    }

    private void saveState() {
        undoStack.push(new Memento(this.balance));
    }
}

// Step 2: Create the Memento class to represent the state of the BankAccount:

public class Memento {
    private int savedBalance;

    public Memento(int balance) {
        this.savedBalance = balance;
    }

    public int getSavedBalance() {
        return savedBalance;
    }
}

// Step 3: Test the BankAccount class by creating two accounts and performing transfers and undo operations:

public class Main {
    public static void main(String[] args) {
        BankAccount account1 = new BankAccount(100);
        BankAccount account2 = new BankAccount(0);

        account1.transfer(50, account2);
        account1.transfer(75, account2);
        account1.deposit(25);

        account1.undo(); // Undo deposit
        account1.undo(); // Undo transfer
        account1.undo(); // Nothing to undo
    }
}
```

### Output

```java
$50 transferred from Account #.... to Account #....
$75 transferred from Account #.... to Account #....
$25 deposited into Account #....
Undo completed. Account #.... balance restored to $100.
Undo completed. Account #.... balance restored to $175.
Nothing to undo.
```

## Known Uses

- `java.util.Date` (the setter methods do that; Date is internally represented by a long value)
- All implementations of `java.io.Serializable`
- All implementations of `javax.faces.component.StateHolder`

## Related Patterns

- Commands can use mementos to maintain state for undoable operations.
- Mementos can be used for iteration as described earlier same as above.

# Mediator Pattern

## Intent

Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

## Motivation

Object-oriented design encourages the distribution of behavior among objects. In the worst case, every object ends up knowing about every other.

A mediator is responsible for controlling and coordinating the interactions of a group of objects. The mediator serves as an intermediary that keeps objects in the group from referring to each other explicitly. The objects only know the mediator, thereby reducing the number of interconnections.

## Applicability

- A set of objects communicate in well-defined but complex ways. The resulting interdependencies are unstructured and difficult to understand.
- Reusing an object is difficult because it refers to and communicates with many other objects.
- A behavior that's distributed between several classes should be customizable without a lot of subclassing.

## Structure

### Participants

- **Mediator:**
    
    - Defines an interface for communicating with Colleague objects.
- **ConcreteMediator:**
    
    - Implements cooperative behavior by coordinating Colleague objects.
    - Knows and maintains its colleagues.
- **Colleague classes:**
    
    - Each Colleague class knows its Mediator object.
    - Each colleague communicates with its mediator whenever it would have otherwise communicated with another colleague.

### Collaborations

- Colleagues send and receive requests from a Mediator object. The mediator implements the cooperative behavior by routing requests between the appropriate colleague(s).

## Consequences

1. **It limits subclassing:** A mediator localizes behavior that otherwise would be distributed among several objects.
    
2. **It decouples colleagues:** A mediator promotes loose coupling between colleagues.
    
3. **It simplifies object protocols:** A mediator replaces many-to-many interactions with one-to-many interactions between the mediator and its colleagues.
    
4. **It abstracts how objects cooperate.**
    
5. **It centralizes control:** The Mediator pattern trades complexity of interaction for complexity in the mediator.
    

## Implementation

1. **Omitting the abstract Mediator class:** The abstract coupling that the Mediator class provides lets colleagues work with different Mediator subclasses, and vice versa.
    
2. **Colleague-Mediator communication:** Colleagues have to communicate with their mediator when an event of interest occurs.
    

## Sample Code

```java
// A chat application where users can send messages to each other through a mediator.

// First, let's define the mediator interface. In our case, it will be the ChatMediator interface:

public interface ChatMediator {
    void sendMessage(String message, User user);
    void addUser(User user);
}

// Create the User class, which represents an individual user in the chat application:

public class User {
    private String name;
    private ChatMediator mediator;

    public User(String name, ChatMediator mediator) {
        this.name = name;
        this.mediator = mediator;
    }

    public void sendMessage(String message) {
        mediator.sendMessage(message, this);
    }

    public void receiveMessage(String message) {
        System.out.println(name + " received a message: " + message);
    }
}

// Implement the ChatRoom class, which acts as the mediator and manages the communication between users:

public class ChatRoom implements ChatMediator {
    private List<User> users;

    public ChatRoom() {
        this.users = new ArrayList<>();
    }

    @Override
    public void sendMessage(String message, User user) {
        for (User u : users) {
            if (u != user) {
                u.receiveMessage(message);
            }
        }
    }

    @Override
    public void addUser(User user) {
        users.add(user);
    }
}

// Test & Output

public class Main {
    public static void main(String[] args) {
        ChatMediator chatRoom = new ChatRoom();

        User user1 = new User("Alice", chatRoom);
        User user2 = new User("Bob", chatRoom);
        User user3 = new User("Charlie", chatRoom);

        chatRoom.addUser(user1);
        chatRoom.addUser(user2);
        chatRoom.addUser(user3);

        user1.sendMessage("Hello everyone!");
        user2.sendMessage("Hi Alice!");
    }
}

// Output

// Bob received a message: Hello everyone!
// Charlie received a message: Hello everyone!
// Alice received a message: Hi Alice!
// Charlie received a message: Hi Alice!
```

---

```java
// Define the mediator interface:

public interface SmartHomeMediator {
    void turnOn(Device device);
    void turnOff(Device device);
    void notify(Device device, String message);
}

// The SmartHomeMediator interface defines the operations that can be performed within the smart home system, such as turning devices on and off, and sending notifications.

public interface Device {
    void turnOn();
    void turnOff();
    void receiveNotification(String message);
}

public class SmartHomeMediatorImpl implements SmartHomeMediator {
    private List<Device> devices;

    public SmartHomeMediatorImpl() {
        this.devices = new ArrayList<>();
    }

    @Override
    public void turnOn(Device device) {
        device.turnOn();
    }

    @Override
    public void turnOff(Device device) {
        device.turnOff();
    }

    @Override
    public void notify(Device device, String message) {
        for (Device dev : devices) {
            if (dev != device) {
                dev.receiveNotification(message);
            }
        }
    }

    public void addDevice(Device device) {
        devices.add(device);
    }
}

// Implement device classes:

public class Light implements Device {
    private SmartHomeMediator mediator;

    public Light(SmartHomeMediator mediator) {
        this.mediator = mediator;
    }

    @Override
    public void turnOn() {
        System.out.println("Light turned on");
        mediator.turnOn(this);
    }

    @Override
    public void turnOff() {
        System.out.println("Light turned off");
        mediator.turnOff(this);
    }

    @Override
    public void receiveNotification(String message) {
        System.out.println("Light received notification: " + message);
    }
}

public class Thermostat implements Device {
    private SmartHomeMediator mediator;
    private int temperature;

    public Thermostat(SmartHomeMediator mediator) {
        this.mediator = mediator;
    }

    @Override
    public void turnOn() {
        System.out.println("Thermostat turned on");
        mediator.turnOn(this);
    }

    @Override
    public void turnOff() {
        System.out.println("Thermostat turned off");
        mediator.turnOff(this);
    }

    @Override
    public void receiveNotification(String message) {
        System.out.println("Thermostat received notification: " + message);
    }

    public void setTemperature(int temperature) {
        this.temperature = temperature;
        System.out.println("Thermostat temperature set to: " + temperature);
    }

    public int getTemperature() {
        return temperature;
    }
}

// Usage

public class Main {
    public static void main(String[] args) {
        SmartHomeMediator mediator = new SmartHomeMediatorImpl();

        Light kitchenLight = new Light(mediator);
        Light livingRoomLight = new Light(mediator);
        Thermostat thermostat = new Thermostat(mediator);

        mediator.addDevice(kitchenLight);
        mediator.addDevice(livingRoomLight);
        mediator.addDevice(thermostat);

        kitchenLight.turnOn();
        livingRoomLight.turnOff();
        thermostat.setTemperature(25);

        thermostat.notify("Someone is at the door!");

        livingRoomLight.turnOn();
    }
}
```

## Known Uses

- `java.util.Timer` (all `scheduleXXX()` methods)
- `java.util.concurrent.Executor#execute()`
- `java.util.concurrent.ExecutorService` (the `invokeXXX()` and `submit()` methods)
- `java.util.concurrent.ScheduledExecutorService` (all `scheduleXXX()` methods)
- `java.lang.reflect.Method#invoke()`

## Related Patterns

- Facade: differs from Mediator in that it abstracts a subsystem of objects to provide a more convenient interface.
- Colleagues can communicate with the mediator using the Observer pattern.


# Chain of Responsibility Pattern

## Intent

Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

## Motivation

The idea of this pattern is to decouple senders and receivers by giving multiple objects a chance to handle a request. The request gets passed along a chain of objects until one of them handles it.

The first object in the chain receives the request and either handles it or forwards it to the next candidate on the chain, which does likewise. The object that made the request has no explicit knowledge of who will handle it (implicit receiver).

The client that issued the request has no direct reference to the object that ultimately fulfills it.

To forward the request along the chain and to ensure receivers remain implicit, each object on the chain shares a common interface for handling requests and for accessing its "successor" on the chain.

## Applicability

- More than one object may handle a request, and the handler isn't known a priori.
- You want to issue a request to one of several objects without specifying the receiver explicitly.
- The set of objects that can handle a request should be specified dynamically.

## Structure

### Participants

- **Handler:**
    
    - Defines an interface for handling requests.
    - (Optional) Implements the successor link.
- **ConcreteHandler:**
    
    - Handles the requests it is responsible for.
    - Can access its successor.
    - If the ConcreteHandler can handle the request, it does so; otherwise, it forwards the request to its successor.
- **Client:**
    
    - Initiates the request to a ConcreteHandler object on the chain.

### Collaborations

- When a client issues a request, the request propagates along the chain until a ConcreteHandler object takes responsibility for handling it.

## Consequences

1. **Reduced coupling:** The pattern frees an object from knowing which other object handles a request. Both the receiver and the sender have no explicit knowledge of each other, and an object in the chain doesn't have to know about the chain's structure.
    
2. **Added flexibility in assigning responsibilities to objects:** You can add or change responsibilities for handling a request by adding to or otherwise changing the chain at run-time.
    
3. **Receipt isn't guaranteed:** Since a request has no explicit receiver, there's no guarantee it will be handled. The request can fall off the end of the chain without ever being handled.
    

## Implementation

1. **Implementing the successor chain:**
    
    - (a) Define new links.
    - (b) Use existing links. Using existing links works well when the links support the chain you need. It saves you from defining links explicitly and saves space.
2. **Connecting successors:** If there are no preexisting references for defining a chain, then you'll have to introduce them yourself.
    
3. **Representing requests:** Different options are available for representing requests. In the simplest form, the request is a hard-coded operation invocation. An alternative is to use a single handler function that takes a request code as a parameter.
    

## Sample Code

```java
// A series of processors, each responsible for handling a specific type of request. If a processor can't handle a request, it passes it to the next processor in line.

// First, let's define an interface called RequestHandler that all processors will implement:

public interface RequestHandler {
    void setNextHandler(RequestHandler handler);
    void handleRequest(Request request);
}

// Create a concrete implementation of the RequestHandler interface called ConcreteHandler. Each ConcreteHandler will have a specific type it can handle, and if it can't handle the request, it will pass it to the next handler:

public class ConcreteHandler implements RequestHandler {
    private String handlerType;
    private RequestHandler nextHandler;

    public ConcreteHandler(String handlerType) {
        this.handlerType = handlerType;
    }

    public void setNextHandler(RequestHandler handler) {
        this.nextHandler = handler;
    }

    public void handleRequest(Request request) {
        if (request.getType().equals(handlerType)) {
            // Handle the request
            System.out.println("Handling request with handler: " + handlerType);
        } else if (nextHandler != null) {
            // Pass the request to the next handler
            nextHandler.handleRequest(request);
        } else {
            // Reached the end of the chain without handling the request
            System.out.println("Cannot handle the request.");
        }
    }
}

// Create a class called Request to represent a request that will be processed by the chain:

public class Request {
    private String type;

    public Request(String type) {
        this.type = type;
    }

    public String getType() {
        return type;
    }
}

// Test

public class Main {
    public static void main(String[] args) {
        // Create the handlers
        RequestHandler handler1 = new ConcreteHandler("Handler 1");
        RequestHandler handler2 = new ConcreteHandler("Handler 2");
        RequestHandler handler3 = new ConcreteHandler("Handler 3");

        // Set up the chain
        handler1.setNextHandler(handler2);
        handler2.setNextHandler(handler3);

        // Create a request
        Request request = new Request("Handler 2");

        // Handle the request
        handler1.handleRequest(request);
    }
}
```

---

```java
// Consider a customer support ticketing system where tickets are assigned to different support teams based on their categories.

// Interface and Ticket Class:

public interface SupportHandler {
    void setNextHandler(SupportHandler handler);
    void handleTicket(Ticket ticket);
}

public class Ticket {
    private String category;
    private String description;

    // Constructor, getters, and setters
}

// Concrete Support Handlers:

public class SalesSupportHandler implements SupportHandler {
    private String supportedCategory;
    private SupportHandler nextHandler;

    public SalesSupportHandler(String supportedCategory) {
        this.supportedCategory = supportedCategory;
    }

    public void setNextHandler(SupportHandler handler) {
        this.nextHandler = handler;
    }

    public void handleTicket(Ticket ticket) {
        if (ticket.getCategory().equalsIgnoreCase(supportedCategory)) {
            System.out.println("Sales support team is handling the ticket: " + ticket.getDescription());
        } else if (nextHandler != null) {
            nextHandler.handleTicket(ticket);
        } else {
            System.out.println("No support team available for the ticket category: " + ticket.getCategory());
        }
    }
}

public class TechnicalSupportHandler implements SupportHandler {
    private String supportedCategory;
    private SupportHandler nextHandler;

    public TechnicalSupportHandler(String supportedCategory) {
        this.supportedCategory = supportedCategory;
    }

    public void setNextHandler(SupportHandler handler) {
        this.nextHandler = handler;
    }

    public void handleTicket(Ticket ticket) {
        if (ticket.getCategory().equalsIgnoreCase(supportedCategory)) {
            System.out.println("Technical support team is handling the ticket: " + ticket.getDescription());
        } else if (nextHandler != null) {
            nextHandler.handleTicket(ticket);
        } else {
            System.out.println("No support team available for the ticket category: " + ticket.getCategory());
        }
    }
}

public class GeneralSupportHandler implements SupportHandler {
    private SupportHandler nextHandler;

    public void setNextHandler(SupportHandler handler) {
        this.nextHandler = handler;
    }

    public void handleTicket(Ticket ticket) {
        System.out.println("General support team is handling the ticket: " + ticket.getDescription());
    }
}

// Factory Method for setting the Chain
public class SupportHandlerFactory {
    public static SupportHandler createSupportChain() {
        SupportHandler salesSupport = new SalesSupportHandler("Sales");
        SupportHandler technicalSupport = new TechnicalSupportHandler("Technical");
        SupportHandler generalSupport = new GeneralSupportHandler();

        salesSupport.setNextHandler(technicalSupport);
        technicalSupport.setNextHandler(generalSupport);

        return salesSupport;
    }
}

public class Main {
    public static void main(String[] args) {
        SupportHandler supportHandler = SupportHandlerFactory.createSupportChain();

        // Create a ticket
        Ticket ticket = new Ticket("Technical", "I'm facing an issue with my computer.");

        // Handle the ticket
        supportHandler.handleTicket(ticket);
    }
}
```

## Known Uses

- `java.util.logging.Logger#log()`
- `javax.servlet.Filter#doFilter()`

## Related Patterns

Chain of Responsibility is often applied in conjunction with Composite, same as above.

# Visitor Pattern

## Intent

Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

## Motivation

With the Visitor pattern, you define two class hierarchies: one for the elements being operated on and one for the visitors that define operations on the elements. You create a new operation by adding a new subclass to the visitor class hierarchy. As long as the grammar that the compiler accepts doesn't change, we can add new functionality simply by defining new `NodeVisitor` subclasses.

## Applicability

- An object structure contains many classes of objects with differing interfaces, and you want to perform operations on these objects that depend on their concrete classes.
- Many distinct and unrelated operations need to be performed on objects in an object structure, and you want to avoid "polluting" their classes with these operations. Visitor lets you keep related operations together by defining them in one class.
- The classes defining the object structure rarely change, but you often want to define new operations over the structure.

## Structure

### Participants

- **Visitor:**
    
    - Declares a `visit` operation for each class of `ConcreteElement` in the object structure.
    - The operation's name and signature identify the class that sends the `visit` request to the visitor. That lets the visitor determine the concrete class of the element being visited. Then the visitor can access the element directly through its particular interface.
- **ConcreteVisitor:**
    
    - Implements each operation declared by `Visitor`.
    - Each operation implements a fragment of the algorithm defined for the corresponding class of object in the structure.
    - `ConcreteVisitor` provides the context for the algorithm and stores its local state.
- **Element:**
    
    - Defines an `Accept` operation that takes a visitor as an argument.
- **ConcreteElement:**
    
    - Implements an `Accept` operation that takes a visitor as an argument.
- **ObjectStructure:**
    
    - Can enumerate its elements.
    - May provide a high-level interface to allow the visitor to visit its elements.
    - May either be a composite.

### Collaborations

- A client that uses the Visitor pattern must create a `ConcreteVisitor` object and then traverse the object structure, visiting each element with the visitor.
- When an element is visited, it calls the `Visitor` operation that corresponds to its class. The element supplies itself as an argument to this operation to let the visitor access its state if necessary.

## Consequences

1. **Visitor makes adding new operations easy:** You can define a new operation over an object structure simply by adding a new visitor. In contrast, if you spread functionality over many classes, then you must change each class to define a new operation.
    
2. **A visitor gathers related operations and separates unrelated ones:** Related behavior is localized in a visitor. Any algorithm-specific data structures can be hidden in the visitor.
    
3. **Adding new `ConcreteElement` is hard:** Each new `ConcreteElement` gives rise to a new abstract operation on `Visitor` and a corresponding implementation in every `ConcreteVisitor` class.
    
4. **Visiting across class hierarchies:** An iterator can visit the objects in a structure as it traverses them by calling their operations. But an iterator can't work across object structures with different types of elements.
    
5. **Accumulating state:** Visitors can accumulate state as they visit each element in the objects in a structure. Without a visitor, this state would be passed as extra arguments to the operations that perform the traversal or they might appear as global variables.
    
6. **Breaking encapsulation:** As a result, the pattern often forces you to provide public operations that access an element's internal state, which may compromise its encapsulation.
    

## Implementation

1. **Double dispatch:** The Visitor pattern lets you add operations to classes without changing them. Visitor achieves this by using a technique called "double-dispatch." This is the key to the Visitor pattern: The operation that gets executed depends on both the type of the Visitor and the type of Element it visits.
    
2. **Who is responsible for traversing the object structure?** A visitor must visit each element of the object structure. The question is how was it get there? We can put traversal in any of three places:
    
    - in object structure
    - in the visitor
    - in a separate iterator Often, the object structure is responsible for iteration. A collection will simply iterate over its elements, calling the `Accept` operation on each.

## Sample Code

```java
// Have a hierarchy of geometric shapes: Circle, Square, and Triangle. We want to calculate the area of each shape using the Visitor pattern.

// Shape.java
public interface Shape {
    void accept(ShapeVisitor visitor);
}

// Circle.java
public class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }

    @Override
    public void accept(ShapeVisitor visitor) {
        visitor.visitCircle(this);
    }
}

// Square.java
public class Square implements Shape {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    public double getSide() {
        return side;
    }

    @Override
    public void accept(ShapeVisitor visitor) {
        visitor.visitSquare(this);
    }
}

// Triangle.java
public class Triangle implements Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    public double getBase() {
        return base;
    }

    public double getHeight() {
        return height;
    }

    @Override
    public void accept(ShapeVisitor visitor) {
        visitor.visitTriangle(this);
    }
}

// ShapeVisitor.java
public interface ShapeVisitor {
    void visitCircle(Circle circle);
    void visitSquare(Square square);
    void visitTriangle(Triangle triangle);
}

// CalculateAreaVisitor.java
public class CalculateAreaVisitor implements ShapeVisitor {
    private double totalArea;

    public CalculateAreaVisitor() {
        totalArea = 0.0;
    }

    public double getTotalArea() {
        return totalArea;
    }

    @Override
    public void visitCircle(Circle circle) {
        double area = Math.PI * circle.getRadius() * circle.getRadius();
        totalArea += area;
    }

    @Override
    public void visitSquare(Square square) {
        double area = square.getSide() * square.getSide();
        totalArea += area;
    }

    @Override
    public void visitTriangle(Triangle triangle) {
        double area = 0.5 * triangle.getBase() * triangle.getHeight();
        totalArea += area;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        // Create some shapes
        Shape circle = new Circle(5.0);
        Shape square = new Square(4.0);
        Shape triangle = new Triangle(3.0, 6.0);

        // Create the visitor
        CalculateAreaVisitor areaVisitor = new CalculateAreaVisitor();

        // Apply the visitor to each shape
        circle.accept(areaVisitor);
        square.accept(areaVisitor);
        triangle.accept(areaVisitor);

        // Get the total area calculated by the visitor
        double totalArea = areaVisitor.getTotalArea();

        // Print the total area
        System.out.println("Total area: " + totalArea);
    }
}
```

---

```java
/* 
   Have a company with different types of employees, such as full-time employees, part-time employees, and contractors. 
   Each type of employee has a different way of calculating their pay, and we want to calculate the total payroll for the company using the Visitor pattern.
*/

// Employee.java
public abstract class Employee {
    protected String name;
    protected int id;

    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }

    public abstract void accept(PayrollVisitor visitor);

    public abstract double calculatePay();
}

// FullTimeEmployee.java
public class FullTimeEmployee extends Employee {
    private double salary;

    public FullTimeEmployee(String name, int id, double salary) {
        super(name, id);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    @Override
    public void accept(PayrollVisitor visitor) {
        visitor.visit(this);
    }

    @Override
    public double calculatePay() {
        return salary;
    }
}

// PartTimeEmployee.java
public class PartTimeEmployee extends Employee {
    private double hourlyRate;
    private int hoursWorked;

    public PartTimeEmployee(String name, int id, double hourlyRate, int hoursWorked) {
        super(name, id);
        this.hourlyRate = hourlyRate;
        this.hoursWorked = hoursWorked;
    }

    public double getHourlyRate() {
        return hourlyRate;
    }

    public int getHoursWorked() {
        return hoursWorked;
    }

    @Override
    public void accept(PayrollVisitor visitor) {
        visitor.visit(this);
    }

    @Override
    public double calculatePay() {
        return hourlyRate * hoursWorked;
    }
}

// Contractor.java
public class Contractor extends Employee {
    private double rate;
    private int hoursWorked;

    public Contractor(String name, int id, double rate, int hoursWorked) {
        super(name, id);
        this.rate = rate;
        this.hoursWorked = hoursWorked;
    }

    public double getRate() {
        return rate;
    }

    public int getHoursWorked() {
        return hoursWorked;
    }

    @Override
    public void accept(PayrollVisitor visitor) {
        visitor.visit(this);
    }

    @Override
    public double calculatePay() {
        return rate * hoursWorked;
    }
}

// PayrollVisitor.java
public interface PayrollVisitor {
    void visit(FullTimeEmployee employee);
    void visit(PartTimeEmployee employee);
    void visit(Contractor contractor);
}

// PayrollCalculator.java
public class PayrollCalculator implements PayrollVisitor {
    private double totalPayroll;

    public PayrollCalculator() {
        totalPayroll = 0.0;
    }

    public double getTotalPayroll() {
        return totalPayroll;
    }

    @Override
    public void visit(FullTimeEmployee employee) {
        totalPayroll += employee.calculatePay();
    }

    @Override
    public void visit(PartTimeEmployee employee) {
        totalPayroll += employee.calculatePay();
    }

    @Override
    public void visit(Contractor contractor) {
        totalPayroll += contractor.calculatePay();
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        // Create employees
        Employee fullTimeEmployee = new FullTimeEmployee("John Doe", 1, 5000.0);
        Employee partTimeEmployee = new PartTimeEmployee("Jane Smith", 2, 15.0, 40);
        Employee contractor = new Contractor("Mike Johnson", 3, 25.0, 20);

        // Create the payroll calculator
        PayrollCalculator payrollCalculator = new PayrollCalculator();

        // Apply the calculator to each employee
        fullTimeEmployee.accept(payrollCalculator);
        partTimeEmployee.accept(payrollCalculator);
        contractor.accept(payrollCalculator);

        // Get the total payroll calculated by the calculator
        double totalPayroll = payrollCalculator.getTotalPayroll();

        // Print the total payroll
        System.out.println("Total payroll: $" + totalPayroll);
    }
}
```

## Known Uses

- `javax.lang.model.element.AnnotationValue` and `AnnotationValueVisitor`
- `javax.lang.model.element.Element` and `ElementVisitor`
- `javax.lang.model.type.TypeMirror` and `TypeVisitor`
- `java.nio.file.FileVisitor` and `SimpleFileVisitor`
- `javax.faces.component.visit.VisitContext` and `VisitCallback`

## Related Pattern

- **Composite:** Visitor can be used to apply an operation over an object structure defined by the Composite pattern.
    
- **Interpreter:** Visitor may be applied to do the interpretation, same as above.

# State Pattern

## Intent

Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

## Also Known As

Objects for States.

## Motivation

The main purpose of the State design pattern is to allow objects to change their behavior based on the current state. The state information is determined at runtime and can be changed at runtime, which allows behavior to be modified dynamically, making it seem as if the object has changed classes.

## Applicability

- An object's behavior depends on its state, and it must change its behavior at runtime depending on that state.
- Operations have large multipart conditional statements that depend on the object's state. The State pattern puts each branch of the conditional in a separate class, allowing the object's state to vary independently from other objects.

## Structure

### Participants

- **Context:**
    
    - Defines the interface of interest to clients.
    - Maintains an instance of a `ConcreteState` subclass that defines the current state.
- **State:**
    
    - Defines an interface for encapsulating the behavior associated with a particular state of the `Context`.
- **ConcreteState subclass:**
    
    - Each subclass implements behavior associated with a state of the `Context`.

### Collaborations

- The `Context` delegates state-specific requests to the current `ConcreteState` object.
- A `Context` may pass itself as an argument to the `State` object handling the request.
- `Context` is the primary interface for clients. Clients can configure a context with `State` objects. Once a context is configured, its clients don't have to deal with the `State` object directly.
- Either `Context` or the `ConcreteState` subclasses can decide which state succeeds another and under what circumstances.

## Consequences

1. **It localizes state-specific behavior and partitions for different states:** The State pattern puts all behavior associated with a particular state into one object. New states and transitions can be added easily by defining new subclasses. Encapsulating each state transition and action in a class elevates the idea of an execution state to full object status.
    
2. **It makes state transitions explicit:** State transitions are represented by different state classes, making them explicit and localized.
    
3. **State can be shared:** States can be shared if they don't maintain any internal state. This can lead to more efficient use of resources.
    

## Implementation

1. **Who defines the state transitions?** The criteria for state transitions can be implemented either entirely in the `Context` or in the `ConcreteState` subclasses. It is generally more flexible and appropriate to let the `ConcreteState` subclasses decide the state transitions.
    
2. **A table-based alternative:** For each state, a table maps every possible input to a succeeding state. This approach converts conditional code into a table lookup. While regular, it can be less efficient, and the transition criteria may become less explicit.
    
3. **Creating and destroying State objects:** Consider whether to create `State` objects only when needed and destroy them afterward or create them ahead of time and never destroy them. The choice depends on the frequency of state changes.
    
4. **Using a dynamic interface:** Sometimes, the `State` interface can be made dynamic, allowing the `Context` to pass itself as an argument to `State` methods. This can be useful when state-specific behavior needs information from the `Context`.

## Sample Code

```java
// Step 1: Define the State interface
interface State {
    void turnOn();
    void turnOff();
}

// Step 2: Implement the concrete states
class OnState implements State {
    @Override
    public void turnOn() {
        System.out.println("The light bulb is already on.");
    }

    @Override
    public void turnOff() {
        System.out.println("Turning off the light bulb.");
        // Transition to the OffState
        LightBulb.setState(new OffState());
    }
}

class OffState implements State {
    @Override
    public void turnOn() {
        System.out.println("Turning on the light bulb.");
        // Transition to the OnState
        LightBulb.setState(new OnState());
    }

    @Override
    public void turnOff() {
        System.out.println("The light bulb is already off.");
    }
}

// Step 3: Create the context class that maintains the state
class LightBulb {
    private static State currentState;

    public LightBulb() {
        // Initial state is off
        currentState = new OffState();
    }

    public static void setState(State state) {
        currentState = state;
    }

    public void turnOn() {
        currentState.turnOn();
    }

    public void turnOff() {
        currentState.turnOff();
    }
}

// Step 4: Use the LightBulb class
public class Main {
    public static void main(String[] args) {
        LightBulb bulb = new LightBulb();

        bulb.turnOn();  // Turns on the light bulb
        bulb.turnOn();  // Prints "The light bulb is already on."
        bulb.turnOff(); // Turns off the light bulb
        bulb.turnOff(); // Prints "The light bulb is already off."
        bulb.turnOn();  // Turns on the light bulb again
    }
}
```

## Known Uses

- `javax.faces.lifecycle.LifeCycle#execute()` (controlled by FacesServlet, the behavior is dependent on the current phase (state) of JSF lifecycle).

## Related Patterns

The Flyweight pattern explains when and how State objects can be shared. State objects are often Singletons.
