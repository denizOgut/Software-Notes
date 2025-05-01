
# Maintainability

## What does maintainability even mean?

Architecture is designing this structure with a purpose. There are functional requirements that the software has to fulfil to create value for its users. Without functionality, software is worthless, because it produces no value.

There are also **quality requirements** (also called **non-functional requirements**) that the software should fulfill to be considered high quality by its users, developers, and stakeholders. One such quality requirement is maintainability.

maintainability is special. If software is maintainable, that means it’s easy to change. If it’s easy to change, it’s flexible and probably modular. It’s probably cost-effective, too, because easy changes mean cheap changes. If it’s maintainable, we can probably evolve it to be scalable, secure, reliable, and performant, should the need arise.

 **==if software is maintainable, it’s easier to evolve in any direction, functionally and non-functionally==**

## Maintainability enables functionality

**==maintainability is a key supporter of functionality.==**

![[Pasted image 20250419212957.png]]

what about those big software systems that are successful in spite of bad maintainability? Those systems usually fall into one (or both) of two categories:
• They are at the end of their life where changes to the system are few and far between
• They are backed by a financially well-off company that is willing to throw money at the problem

we need to do some design up-front (should we call it SDUF?) to bake a seed of maintainability into the software, which can make it easier to evolve the architecture to where it needs to be over time.

## Maintainability generates developer joy

if our software system is maintainable, we need less time to implement a change, so we are more productive. Also, if our software system is maintainable, we find more joy in making changes because it’s more efficient and we can take more pride in it.

![[Pasted image 20250419213532.png]]

## Maintainability supports decision-making

When building a software system, we solve problems every day. For most problems we face, there is more than one solution. We have to make decisions to choose between those solutions.

• We apply don’t repeat yourself (DRY) when we find code duplication
• We use dependency injection to make the code more testable
• We introduce a builder to make it simpler to create an object

**==Maintainability is built into many of the decisions we’re making automatically every day!==**

## Maintaining maintainability

How do we manage maintainability over time?

The answer to that question is to create and maintain an architecture that makes it easy to create maintainable code. A good architecture makes it easy to navigate the code base. In an easily navigable code base, it’s a breeze to modify existing features or add new features. The dependencies between the components of our application are clear and not tangled. **==In summary, good architecture increases maintainability:==**

![[Pasted image 20250419214336.png]]

# What’s Wrong with Layers?

Layers are a solid architecture pattern! If we get them right, we’re able to build domain logic that is independent of the web and persistence layers. We can switch out the web or persistence technologies without affecting our domain logic, if the need arises. We can also add new features without affecting existing features.

With a good layered architecture, we’re keeping our options open and are able to quickly adapt to changing requirements and external factors. **A good layered architecture is maintainable**

So, what’s wrong with layers?

**==Layers don’t provide enough guardrails to keep the architecture on track==**. We need to rely too much on human discipline and diligence to keep it maintainable.

## They promote database-driven design

By its very definition, the foundation of a conventional layered architecture is the database. The web layer depends on the domain layer, which in turn depends on the persistence layer and thus the database. Everything builds on top of the persistence layer. This is problematic for several reasons.

We’re primarily trying to model behavior, not the state, the state is an important part of any application, but the behavior is what changes the state and thus drives the business!

in a conventional layered architecture since we’re going with the natural flow of dependencies. But it makes absolutely no sense from a business point of view! **==We should build the domain logic before building anything else! We want to find out whether we have understood the business rules correctly. And only once we know we’re building the right domain logic should we move on to build a persistence and web layer around it.==**

driving force in such a database-centric architecture is the use of object-relational mapping (ORM) frameworks

![[Pasted image 20250420112642.png]]

Since a layer may access the layers below it, the domain layer is allowed to access those entities. And if it’s allowed to use them, it will use them at some point

**==This creates a strong coupling between the domain layer and the persistence layer==**. Our business services use the persistence model as their business model and have to deal not only with the domain logic but also with eager versus lazy loading, database transactions, flushing caches, and similar housekeeping tasks

**==The persistence code is virtually fused into the domain code and thus it’s hard to change one without the other.==** That’s the opposite of being flexible and keeping options open, which should be the goal of our architecture.

## They’re prone to shortcuts

In a conventional layered architecture, the only global rule is that from a certain layer, we can only access components in the same layer or a layer below. 

So, if we need access to a certain component in a layer above ours, we can just push the component down a layer and we’re allowed to access it. Problem solved. Doing this once may be OK. But doing it once opens the door for doing it a second time.

**==if there is an option to do something, someone will do it, especially in combination with a looming deadline. And if something has been done before, the likelihood of someone doing it again will increase drastically==**. This is a psychological effect called the **Broken Windows Theory**

![[Pasted image 20250420113539.png]]

if we want to disable shortcut mode for our architecture, layers are not the best option, at least not without enforcing some kind of additional architecture rules. And by enforcing, I don’t mean a senior developer doing code reviews, but automatically enforced rules that make the build fail when they’re broken.

## They grow hard to test
 
 A common evolution within a layered architecture is that layers are skipped. We access the persistence layer directly from the web layer since we’re only manipulating a single field of an entity, and for that, we need not bother the domain layer

![[Pasted image 20250420114100.png]]

Again, this feels OK the first couple of times, but it has two drawbacks if it happens often

First, we’re implementing domain logic in the web layer, even if it’s only manipulating a single field What if the use case expands in the future? We’re most likely going to add more domain logic to the web layer, mixing responsibilities and spreading essential domain logic across all layers.

Second, **==in the unit tests of our web layer, we not only have to manage the dependencies on the domain layer but also the dependencies on the persistence layer==**. If we’re using mocks in our tests, that means we have to create mocks for both layers. This adds complexity to the tests. And a complex test setup is the first step toward no tests at all because we don’t have time for them.

## They hide the use cases

**==Since we’re so often searching for the right place to add or change functionality, our architecture should help us to quickly navigate the code base==**. How does a layered architecture hold up in this regard?

**==in a layered architecture, it easily happens that domain logic is scattered throughout the layers.==**

layered architecture does not impose rules on the “width” of domain services. Over time, this often leads to very broad services that serve multiple use cases
![[Pasted image 20250420114837.png]]

A broad service has many dependencies on the persistence layer and many components in the web layer depend on it. This not only makes the service hard to test but also makes it hard for us to fin the code responsible for the use case we want to work on.

## They make parallel work difficult

Adding manpower to a late software project makes it later.  on a healthy scale, we can certainly expect to be faster with more people on the project. And management is right to expect that of us. To meet this expectation, our architecture must support parallel work. This is not easy. And a layered architecture doesn’t really help us here.

**==Since everything builds on top of the persistence layer, the persistence layer must be developed first. Then comes the domain layer and finally the web layer. So only one developer can work on the feature at a time!==**

Working on different use cases will cause the same service to be edited in parallel, which leads to merge conflicts and potentially regressions.

## How does this help me build maintainable software?

If done correctly, and if some additional rules are imposed on it, a layered architecture can be very maintainable and can make changing or adding to the code base a breeze. 

Without good self-discipline, it’s prone to degrading and becoming less maintainable over time. And our self discipline usually takes a hit each time a team member rotates into or out of the team, or a manager draws a new deadline around the development team.

# Inverting Dependencies

## The Single Responsibility Principle

A component should do only one thing and do it right. That’s good advice, but not the actual intent of the SRP.

Here’s the actual definition of the SRP: **==A component should have only one reason to change==**. As we see, “responsibility” should actually be translated to “reason to change” instead of “do only one thing.” Perhaps we should rename the SRP to the “Single Reason to Change Principle.”

![[Pasted image 20250430184957.png]]

The only reason to change component E is when the functionality of E must change due to some new requirement. Component A, however, might have to change when any of the other components change because it depends on them.

## The Dependency Inversion Principle

In our layered architecture, the cross-layer dependencies always point down to the next layer. When we apply the Single Responsibility Principle on a high level, we notice that the upper layers have more reasons to change than the lower layers.

Thus, due to the domain layer’s dependency on the persistence layer, each change in the persistence layer potentially requires a change in the domain layer. But the domain code is the most important code in our application! We don’t want to have to change it when something changes in the persistence code!

The **Dependency Inversion Principle (DIP)** provides the answer.
In contrast to the SRP, the DIP means what the name suggests:
We can turn around (invert) the direction of any dependency within our code base

![[Pasted image 20250430185135.png]]

## Clean Architecture

the domain code must not have any outward-facing dependencies. Instead, **==with the help of the DIP, all dependencies point toward the domain code==**

![[Pasted image 20250430185451.png]]

**==The main rule in such an architecture is the “Dependency Rule,” which states that all dependencies between those layers must point inward.==** 

The core of the architecture contains the domain entities, which are accessed by the surrounding use cases. The use cases are what we have called services earlier, but are more fine-grained to have a single responsibility (i.e., a single reason to change), thus avoiding the problem of broad services

Since the domain code knows nothing about which persistence or UI framework is used, it cannot contain any code specific to those frameworks and will concentrate on the business rules.

Clean Architecture comes at a cost. Since the domain layer is completely decoupled from the outer layers such as the persistence and UI layers, we have to maintain a model of our application’s entities in each of the layers

In Clean and Hexagonal Architectures, the domain layer is decoupled from outer layers like persistence. ORMs, such as JPA, require metadata and specific constraints (e.g., default constructors) that don’t belong in domain models. To maintain separation, the persistence layer maps domain entities to its own representations. This extra mapping preserves a clean domain model, free from framework-specific dependencies. Hexagonal Architecture makes these abstract principles more concrete by clearly defining boundaries and interactions.

## Hexagonal Architecture

![[Pasted image 20250430190044.png]]

all dependencies point toward the center. To clearly call out a central attribute of Hexagonal Architecture, the application core (the hexagon) defines and owns the interface to the outside (the ports). The adapters then work with this interface. This is the Dependency Inversion Principle applied at the architecture level. Due to its central concepts, this architecture style is also known as a Ports and Adapters architecture.

**==The business logic is implemented in the use case classes and entities. The use case classes are narrow domain services, implementing just a single use case.==** We can choose to combine multiple use cases to a broader domain service, of course, but ideally, we do this only when the use cases are often used together, to increase maintainability.

**==An application service is a service that coordinates calls to use cases (domain services)==**

![[Pasted image 20250430190612.png]]

Here, the application services translate between the input and output ports and the domain services, shielding the domain services from the outside world, and potentially coordinating between the domain services.

## How does this help me build maintainable software?

The domain code is free to be modeled as best fits the business problems, while the persistence and UI code are free to be modeled as best fits the persistence and UI problems.

# Organizing Code

Wouldn’t it be nice to recognize the architecture just by looking at the code? Classes in one package import classes from other packages that should not be imported

## Organizing By Layer

![[Pasted image 20250501112108.png]]

we have already applied the Dependency Inversion Principle here, only allowing dependencies toward the domain code in the package. We did this by domain introducing the interface in the package and implementing it in ``AccountRepository`` domain the package. persistence

- First, we have no package boundary between functional slices or features of our application. If we add a feature for managing users, we’ll add a to the package; ``UserController`` web a ``UserService``, ``UserRepository``, and to the package; and a User domain to the package. Without further structure, this ``UserRepositoryImpl`` persistence might quickly become a mess of classes, leading to unwanted side effects between supposedly unrelated features of the application.

- Second, we can’t see which use cases our application provides. Can you tell what use cases the or classes implement? If we’re looking for a ``AccountService`` ``AccountController`` certain feature, we have to guess which service implements it and then search for the responsible method within that service.

- Finally, we can’t see our target architecture within the package structure. We can guess that we have followed the Hexagonal Architecture style and then browse the classes in the web and packages to find the web and persistence adapters. But we can’t see at a persistence glance which functionality is called by the web adapter and which functionality the persistence adapter provides to the domain layer. The incoming and outgoing ports are hidden in the code.

## Organizing by feature

![[Pasted image 20250501112527.png]]

In essence, we have put all the code related to accounts into the high-level package, account. we can enforce
package boundaries between the features by using package-private visibility for the classes that should not be accessed from the outside.

The package boundaries, combined with package-private visibility, enable us to avoid unwanted dependencies between features also renamed to narrow its responsibility ``AccountService`` ``SendMoneyService`` (we actually could have done that in the package-by-layer approach, too). We can now see that the code implements the Send money use case just by looking at the class name. Making the application’s functionality visible in the code is what Robert Martin calls a “Screaming Architecture” because it screams its intention at us

We have no package names to identify our adapters, and we still don’t see the incoming and outgoing ports. What’s more, even though we have inverted the dependencies between the domain code and persistence code so that only knows about ``SendMoneyService`` the interface and not its implementation, we cannot use package-private ``AccountRepository`` visibility to protect the domain code from accidental dependencies on the persistence code

## An architecturally expressive package structure

In a Hexagonal Architecture, we have entities, use cases, **input** and **output ports**, and input and output (or “**driving**” and “**driven**”) adapters as our main architectural elements

![[Pasted image 20250501113315.png]]

the highest level, we have the and packages. ``adapter`` ``application``, The package contains the incoming adapters that call the application’s incoming ports and adapter the outgoing adapters that provide implementations for the application’s outgoing ports.
 
 Moving the adapters’ code to their own packages has the benefit that we can very easily replace one adapter with another implementation, should the need arise. Imagine we have started implementing a persistence adapter against a simple key-value database because we thought we knew the required access patterns, but those patterns have changed, and we would be better off with an SQL database now. We simply implement all relevant outgoing ports in a new adapter package and then remove the old package.

The ``application`` package contains the “hexagon,” as in, our application code. This code consists application of our domain model, which lives in the package, and the port interfaces, which live in the  ``port`` package. 

Why are the ports inside the **application** package and not next to it? The ports are our way to application apply the **Dependency Inversion Principle**. The application defines these ports to communicate with the outside world. Putting the **port** package inside the **application** package expresses that the  application owns the ports.

Th ``domain`` package contains our domain entities and domain services that implement the input domain ports and coordinate between the domain entities. Finally, there is ``common`` a package, which contains some code that is shared across the rest of the common code base

This package structure is a powerful element in the fight against the so-called **architecture/code gap or model/code gap**. These terms describe the fact that in most software development projects, the architecture is only an abstract concept that cannot be directly mapped to the code. With time, if the package structure (among other things) does not reflect the architecture, the code will usually deviate more and more from the target architecture.

Also, this expressive package structure promotes active thinking about the architecture. We have to actively decide which package our code to put into

Within the ``application`` package, however, some classes indeed have to be public. The ports must application be public because they must be accessible to the adapters by design. The domain model must be public to be accessible to the services and, potentially, to the adapters. The services don’t need to be public because they can be hidden behind the incoming port interfaces.

There is no perfection. But with an expressive package structure, we can at least reduce the gap between code and architecture.

## The role of dependency injection

==an essential requirement of such an architecture is that the **application layer** does not have dependencies on the incoming and outgoing adapters,==

For incoming adapters, such as our web adapter, this is easy since the control flow points in the same direction as the dependency between the adapter and the domain code. The adapter simply calls the service within the application layer. In order to clearly bring out the entry points to our application, we’ll want to hide the actual services behind port interfaces.

For outgoing adapters, such as our persistence adapter, we have to make use of the **Dependency Inversion Principle** to turn the dependency against the direction of the control flow

![[Pasted image 20250501115841.png]]

But who provides the application with the actual objects that implement the port interfaces? We don’t want to instantiate the ports manually within the application layer because we don’t want to introduce a dependency on an adapter.

This is where **dependency injection** comes into play. We introduce a neutral component that has a dependency on all layers. This component is responsible for instantiating most of the classes that make up our architecture.

## How does this help me build maintainable software?

looked at a package structure for a Hexagonal Architecture that takes the actual code structure as close to the target architecture as possible. Finding an element of the architecture in the code is now a matter of navigating down the package structure along the names of certain boxes in an architecture diagram, helping with communication, development, and maintenance.

# Implementing a Use Case

