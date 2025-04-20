
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

