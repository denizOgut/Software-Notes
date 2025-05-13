
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


```java
package buckpal.application.domain.model;

public class Account {

    private AccountId id;
    private Money baselineBalance;
    private ActivityWindow activityWindow;

    // constructors and getters omitted

    public Money calculateBalance() {
        return Money.add(
            this.baselineBalance,
            this.activityWindow.calculateBalance(this.id));
    }

    public boolean withdraw(Money money, AccountId targetAccountId) {
        if (!mayWithdraw(money)) {
            return false;
        }

        Activity withdrawal = new Activity(
            this.id,
            this.id,
            targetAccountId,
            LocalDateTime.now(),
            money);
        this.activityWindow.addActivity(withdrawal);
        return true;
    }

    private boolean mayWithdraw(Money money) {
        return Money.add(
            this.calculateBalance(),
            money.negate())
            .isPositive();
    }

    public boolean deposit(Money money, AccountId sourceAccountId) {
        Activity deposit = new Activity(
            this.id,
            sourceAccountId,
            this.id,
            LocalDateTime.now(),
            money);
        this.activityWindow.addActivity(deposit);
        return true;
    }
}
```

## A use case in a nutshell

1. ==**Take the input.**==
2. ==**Validate the business rules.**==
3. ==**Manipulate the model state.**==
4.  ==**Return the output.==**

A use case takes input from an incoming adapter. You might wonder why I didn’t call the first step Validate input. The answer is that I believe **==use case code should only be concerned with domain**== ==**logic and we shouldn’t pollute it with input validation==**

The use case is, however, responsible for validating business rules. It shares this responsibility with the domain entities

If the business rules were satisfied, the use case then manipulates the state of the model in one way or another, based on the input. Usually, it will change the state of a domain object and pass this new state to a port implemented by the persistence adapter to be persisted. If the use case drives other side effects than persistence, it invokes an appropriate adapter for each side effect

The last step is to translate the return value from the outgoing adapter into an output object, which will be returned to the calling adapter.

```java
package buckpal.application.domain.service;

@RequiredArgsConstructor
@Transactional
public class SendMoneyService implements SendMoneyUseCase {

    private final LoadAccountPort loadAccountPort;
    private final UpdateAccountStatePort updateAccountStatePort;

    @Override
    public boolean sendMoney(SendMoneyCommand command) {
        // TODO: validate business rules
        // TODO: manipulate model state
        // TODO: return output
    }
}

```

The service also sets the boundary for a database transaction, as implied by the ``@Transactional`` annotation

![[Pasted image 20250507132313.png]]


---

``UpdateAccountStatePort`` and ``LoadAccountPort``, in this example, are port interfaces implemented by a persistence adapter. If they are often used together, we could also combine them into a broader interface. We could even call that interface ``AccountRepository`` to stick with the DDD language.

---

## Validating input

The application layer should care about input validation because, well, otherwise it might get invalid input from outside the application core. This might cause damage to the state of our model.

where do we put the input validation if not in the use case class? We’ll let **==the input model take care of it==** we’ll do the validation within the constructor:

```java
package buckpal.application.port.in;

import static java.util.Objects.requireNonNull;
import static buckpal.common.Validation.requireGreaterThan;

public record SendMoneyCommand(
    AccountId sourceAccountId,
    AccountId targetAccountId,
    Money money
) {
    public SendMoneyCommand {
        requireNonNull(sourceAccountId);
        requireNonNull(targetAccountId);
        requireNonNull(money);
        requireGreaterThan(money, Money.zero());
    }
}
```

By using a **record** to implement ``SendMoneyCommand``, we make it **immutable**. So, once constructed successfully, we can be sure that the state is valid and cannot be changed to something invalid.

**==Since ``SendMoneyCommand`` is part of the use cases’ API, it’s located in the incoming port package. Thus, the validation remains in the core of the application (at the edge of the hexagon of our architecture) but does not pollute the sacred use case code.==**

```java
package buckpal.application.port.in;

import jakarta.validation.constraints.NotNull;
import buckpal.common.validation.PositiveMoney;

public record SendMoneyCommand(
    @NotNull AccountId sourceAccountId,
    @NotNull AccountId targetAccountId,
    @NotNull @PositiveMoney Money money
) {
    public SendMoneyCommand {
        this.sourceAccountId = sourceAccountId;
        this.targetAccountId = targetAccountId;
        this.money = money;
        Validator.validate(this);
    }
}
```

```java
package buckpal.application.port.in;

import jakarta.validation.ConstraintViolation;
import jakarta.validation.ConstraintViolationException;
import jakarta.validation.Validation;
import jakarta.validation.ValidatorFactory;

import java.util.Set;

public class Validator {
    private static final jakarta.validation.Validator validator =
        Validation.buildDefaultValidatorFactory().getValidator();

    /**
     * Evaluates all Bean Validation annotations on the subject.
     */
    public static <T> void validate(T subject) {
        Set<ConstraintViolation<T>> violations = validator.validate(subject);
        if (!violations.isEmpty()) {
            throw new ConstraintViolationException(violations);
        }
    }
}
```

Note that the term “command,” as used in the ``SendMoneyCommand`` class, does not match the common interpretation of the “command pattern.” In the command pattern, a command is executable, that is, it has a method called execute() that actually invokes the use case. In our case, the command is just a data transfer object that transfers the required parameters to the use case service that executes the command.

## The power of constructors

```java
SendMoneyCommand command = new SendMoneyCommandBuilder()
    .sourceAccountId(new AccountId(41L))
    .targetAccountId(new AccountId(42L))
    // Initialize other fields as needed, for example:
    .money(new Money(500L))
    .build();
```

if we use the constructor directly instead of hiding it behind a builder, each time a new field is added or an existing field is removed, we can just follow the trail of compile errors to reflect that change in the rest of the code base.

```java
ClassWithManyFields person = new ClassWithManyFields(
    "Donald",                                 // name
    LocalDate.of(1934, 6, 9),                 // date of birth
    "1234567",                                // social security number
    "Duckburg",                               // birthplace
    "Duckstreet 42",                          // street
    "Duckburg",                               // city
    "12345",                                  // zipcode
    "USA",                                    // country
    "Calisota"                                // state
);
```

**==To make the preceding code even more readable and safer to work with, we can introduce immutable value objects to replace some of the primitives we used as constructor parameters. A value object is an object whose value is its identity.==** Two value objects with the same value are considered the same. Instead of passing the street, city, zip code, country, and state separately, we could combine them into an ``Address`` value object, for example, because they belong together. We could even go a step further and create City and ``ZipCode`` value objects, for example. This would reduce the chance of confusing one String parameter with another, because the compiler would complain if we tried to pass a ``City`` into a ``ZipCode`` parameter and vice versa.

There are cases where a builder may be the better solution, though. If some parameters in ``ClassWithManyFields`` from the preceding example were optional, for example, we would have to pass null values into the constructor, which is ugly at best. A builder would allow us to define only the required parameters. But if using builders, we should make very sure that the ``build()`` method fails loudly when we forget to define a required parameter because the compiler doesn’t check that for us!


## Different input models for different use cases

A dedicated input model for each use case makes the use case much clearer and also decouples it from other use cases, preventing unwanted side effects. It comes at a cost, however, because we have to map incoming data to different input models for different use cases

## Validating business rules

**==While validating input is not part of the use case logic, validating business rules definitely is==**. Business rules are the core of the application and should be handled with appropriate care.

**==A very pragmatic distinction between the two is that validating a business rule requires access to the current state of the domain model while validating input does not.==**

The best way is to put the business rules into a domain entity as we did for the rule the source account must not be overdrawn:

```java
package buckpal.application.domain.model;

public class Account {

    // Other fields and methods omitted for brevity

    public boolean withdraw(Money money, AccountId targetAccountId) {
        if (!mayWithdraw(money)) {
            return false;
        }

        // Record the withdrawal activity
        Activity withdrawal = new Activity(
            this.id,                 // owner account
            this.id,                 // source account
            targetAccountId,         // target account
            LocalDateTime.now(),     // timestamp
            money                    // amount
        );
        this.activityWindow.addActivity(withdrawal);

        return true;
    }

    private boolean mayWithdraw(Money money) {
        return Money.add(
            this.calculateBalance(),
            money.negate()
        ).isPositive();
    }
}

```

This way, the business rule is easy to locate and reason about because it’s right next to the business logic that requires this rule to be honored. If it’s not feasible to validate a business rule in a domain entity, we can do it in the use case code before it starts working on the domain entities:

```java
package buckpal.application.domain.service;

@RequiredArgsConstructor
@Transactional
public class SendMoneyService implements SendMoneyUseCase {

    @Override
    public boolean sendMoney(SendMoneyCommand command) {
        requireAccountExists(command.sourceAccountId());
        requireAccountExists(command.targetAccountId());
    }
}
```

More complex business rules might require us to load the domain model from the database first and then do some checks on its state. If we have to load the domain model anyway, we should implement the business rule in the domain entities themselves, as we did with the rule the source account must not be overdrawn.

## Rich versus anemic domain model

In a rich domain model, as much of the domain logic as possible is implemented within the entities at the core of the application. The entities provide methods to change the state and only allow changes that are valid according to the business rules. This is the way we pursued the entity previously. ``Account`` Where is our use case implementation in this scenario?

In this case, our use case serves as an entry point to the domain model. A use case then only represents the intent of the user and translates it into orchestrated method calls to the domain entities, which do the actual work. Many of the business rules are located in the entities instead of the use case implementation

## Different output models for different use cases

Once the use case has done its work, what should it return to the caller? **==Similar to the input, it has benefits if the output is as specific to the use case as possible==**. The output should only include the data that is really needed for the caller to work.

But we should ask them to try to keep our use cases as specific as possible. When in doubt, return as little as possible.

Sharing the same output model between use cases also tends to tightly couple those use cases. If one of the use cases needs a new field in the output model, the other use cases have to handle this field as well, even if it’s irrelevant to them. Shared models tend to grow timorously for multiple reasons in the long run. Applying the Single Responsibility Principle and keeping models separated helps in decoupling use cases.

## What about read-only use cases?

From the viewpoint of the application core, however, this is a simple query for data. So, if it’s not considered a use case in the context of the project, we can implement it as a query to set it apart from the real use cases.
One way of doing this within our architecture style is to create a dedicated incoming port for the query and implement it in a “query service:”

```java
package buckpal.application.domain.service;

import lombok.RequiredArgsConstructor;
import java.time.LocalDateTime;

@RequiredArgsConstructor
class GetAccountBalanceService implements GetAccountBalanceUseCase {

    private final LoadAccountPort loadAccountPort;

    public Money getAccountBalance(GetAccountBalanceQuery query) {
        return loadAccountPort.loadAccount(query.accountId(), LocalDateTime.now())
                              .calculateBalance();
    }
}
```

This way, read-only queries are clearly distinguishable from modifying use cases (or “commands”) in our code base. We just have to look at the names of the input types to know which we’re dealing with. This plays nicely with concepts such as **==Command-Query Separation (CQS) and Command-Query Responsibility Segregation (CQRS).==**

## How does this help me build maintainable software?

Our architecture lets us implement the domain logic as we see fit, but if we model the input and output
of our use cases independently, we avoid unwanted side effects Yes, it’s more work than just sharing models between use cases. We have to introduce a separate model for each use case and map between this model and our entities.

But use case-specific models allow for a crisp understanding of a use case, making it easier to maintain in the long run. Also, they allow multiple developers to work on different use cases in parallel without stepping on each other’s toes. Together with tight input validation, use case-specific input and output models go a long way toward a maintainable code base.

## Implementing a Web Adapter

## Dependency Inversion

![[Pasted image 20250507142649.png]]

The web adapter is a “driving” or “incoming” adapter. It takes requests from the outside and translates them into calls to our application core, telling it what to do.

The application layer provides specific ports through which the web adapter may communicate. **==Each port is what I have called a “use case”==** in the previous chapter, and it is implemented by a domain service in the application layer.

![[Pasted image 20250507142944.png]]

So why do we add another layer of indirection between the adapter and the use cases? The reason is that **==the ports are a specification of the places where the outside world can interact with our application core. By having ports in place, we know exactly which communication with the outside world takes place==**, which is valuable information for any maintenance engineer working on your legacy code base.

Knowing the ports that drive the application also lets us build a test driver for the application.

One question remains, though, which is relevant for highly interactive applications. Imagine a server application that sends real-time data to the user’s browser via ``WebSocket``. How does the application core send this real-time data to the web adapter, which in turn sends it to the user’s browser? For this scenario, we definitely need a port because, **==without a port, the application would have to depend on an adapter implementation, breaking our efforts to keep the application free from dependencies on the outside.==**

![[Pasted image 20250507143324.png]]

## Responsibilities of a web adapter

What does a web adapter actually do? Let’s say we want to provide a REST API for our ``BuckPal`` application. Where do the responsibilities of the web adapter start and where do they end? A web adapter usually does these things:

1. ==**Maps the incoming HTTP request to objects.**==
2. ==**Performs authorization checks.**==
3. ==**Validates the input.**==
4. ==**Maps the request objects to the input model of the use case.**==
5. ==**Calls the use case.**==
6. ==**Maps the output of the use case back to HTTP.**==
7. ==**Returns the HTTP response.==**

to call a certain use case with the transformed input model. The adapter then takes the output of the use case and serializes it into an HTTP response, which is sent back to the caller. **==Anything that has to do with HTTP must not leak into the application layer. If the application core knows that we’re dealing with HTTP on the outside, we have lost the option to perform the same domain logic from other incoming adapters that do not use HTTP. In a maintainable architecture, we want to keep options open.==**

## Slicing controllers

A web adapter may certainly consist of more than one class. We should take care, however, to put these classes into the same package hierarchy to mark them as belonging together. **==We should make sure that each controller implements a slice of the web adapter that is as narrow as possible and that shares as little as possible with other controllers.==**

```java
package buckpal.adapter.in.web;

import lombok.RequiredArgsConstructor;
import org.springframework.web.bind.annotation.*;
import java.util.List;

@RestController
@RequiredArgsConstructor
class AccountController {

    private final GetAccountBalanceUseCase getAccountBalanceUseCase;
    private final ListAccountsQuery listAccountsQuery;
    private final LoadAccountQuery loadAccountQuery;
    private final SendMoneyUseCase sendMoneyUseCase;
    private final CreateAccountUseCase createAccountUseCase;

    @GetMapping("/accounts")
    public List<AccountResource> listAccounts() {
        // Implementation goes here
        return List.of(); // placeholder
    }

    @GetMapping("/accounts/{id}")
    public AccountResource getAccount(@PathVariable("id") Long accountId) {
        // Implementation goes here
        return null; // placeholder
    }

    @GetMapping("/accounts/{id}/balance")
    public Long getAccountBalance(@PathVariable("id") Long accountId) {
        // Implementation goes here
        return null; // placeholder
    }

    @PostMapping("/accounts")
    public AccountResource createAccount(@RequestBody AccountResource account) {
        // Implementation goes here
        return null; // placeholder
    }

    @PostMapping("/accounts/send/{sourceAccountId}/{targetAccountId}/{amount}")
    public void sendMoney(
        @PathVariable("sourceAccountId") Long sourceAccountId,
        @PathVariable("targetAccountId") Long targetAccountId,
        @PathVariable("amount") Long amount
    ) {
        // Implementation goes here
    }
}
```

Everything concerning the account resource is in a single class, which feels good. But let’s discuss the downsides of this approach

- **First, less code per class is a good thing.**
- The same argument is valid for test code. If the controller itself has a lot of code, there will be a lot of test code. And often, test code is even harder to grasp than production code because it tends to be more abstract.

 **==Equally important, however, is that putting all operations into a single controller class encourages the reuse of data structures ? I advocate the approach to create a separate controller, potentially in a separate package, for each operation. Also, we should name the methods and classes as close to our use cases as possible:==**

```java
package buckpal.adapter.in.web;

import lombok.RequiredArgsConstructor;
import org.springframework.web.bind.annotation.*;

@RestController
@RequiredArgsConstructor
public class SendMoneyController {

    private final SendMoneyUseCase sendMoneyUseCase;

    @PostMapping("/accounts/sendMoney/{sourceAccountId}/{targetAccountId}/{amount}")
    public void sendMoney(
        @PathVariable("sourceAccountId") Long sourceAccountId,
        @PathVariable("targetAccountId") Long targetAccountId,
        @PathVariable("amount") Long amount
    ) {
        SendMoneyCommand command = new SendMoneyCommand(
            new AccountId(sourceAccountId),
            new AccountId(targetAccountId),
            Money.of(amount)
        );
        sendMoneyUseCase.sendMoney(command);
    }
}
```

each controller can also have its own input model. Instead of a generic model such as ``AccountResource``, we might then have a model specific to the use case such as ``CreateAccountResource`` or ``UpdateAccountResource``. Those specialized model classes may even be private to the controller’s package to prevent accidental reuse. Controllers may still share models, but using shared classes from another package makes us think about it more and perhaps we will find out that we don’t need half of the fields and will create our own, after all.

Another benefit of this slicing style is that it makes parallel work on different operations a breeze. We won’t have merge conflicts if two developers work on different operations.

## How does this help me build maintainable software?
 
 To build maintainable software, web adapters should strictly handle HTTP translation without leaking protocol details into the application layer, ensuring modularity and adaptability. Using many small, focused controller classes improves testability, clarity, and supports easier long-term maintenance.

# Implementing a Persistence Adapter

## Dependency inversion

![[Pasted image 20250507191435.png]]

Our domain services call port interfaces to access persistence functionality. These ports are implemented by a persistence adapter class that does the actual persistence work and is responsible for talking to the database.

The ports are effectively a layer of indirection between the domain services and the persistence code 

Naturally, at runtime, we still have a dependency from our application core to the persistence adapter. If we modify the code in the persistence layer and introduce a bug, for example, we may still break the functionality in the application core. However, as long as the contracts of the ports are fulfilled we’re free to do what we want in the persistence adapter without affecting the core.

## Responsibilities of a persistence adapter

1. **Takes the input.**
2. **Maps the input into database format.**
3. **Sends the input to the database.** 
4. **Maps the database output into application format.** 
5. **Returns the output.**

The persistence adapter takes input through a port interface. The input model may be a domain entity or an object dedicated to a specific database operation, as specified by the interface.

Instead of using JPA or another object-relational mapping framework, we might use any other technique to talk to the database. We might map the input model into plain SQL statements and send these statements to the database, or we might serialize incoming data into files and read them back from there.

**==The important part is that the input model to the persistence adapter lies within the application core, and not within the persistence adapter itself, so that changes in the persistence adapter don’t affect the core.==**

Next, the persistence adapter queries the database and receives the query results.

Finally, it maps the database answer into the output model expected by the port and returns it. Again, it’s important that the output model lies within the application core and not within the persistence adapter to have the dependencies point in the right direction

## Slicing port interfaces

One question that comes to mind when implementing services is how to slice the port interfaces that define the database operations available to the application core. It’s a common practice to create a single repository interface that provides all database operations for a certain entity

![[Pasted image 20250507192035.png]]

Dependencies on methods that we don’t need in our context make the code harder to understand and test.

> Depending on something that carries baggage that you don’t need can cause you troubles that you didn’t expect

The **Interface Segregation Principle** provides an answer to this problem. It states that broad interfaces should be split into specific ones so that clients only know the methods they need.

![[Pasted image 20250507192116.png]]

Each service now only depends on the methods it actually needs. What’s more, the names of the ports clearly state what they’re about. In a test, we no longer have to think about which methods to mock since most of the time, there is only one method per port.

Having very narrow ports such as these makes coding a plug-and-play experience. When working on a service, we just “plug in” the ports we need. There is no baggage to carry around.

## Slicing persistence adapters

**==There is no rule, however, that forbids us to create more than one persistence adapter, as long as all persistence ports are implemented.==**

![[Pasted image 20250507192340.png]]

This way, our persistence adapters are automatically sliced along the seams of the domain that we support with persistence functionality

**==The one persistence adapter per aggregate approach is also a good foundation to separate the persistence needs for multiple bounded contexts in the future==**

![[Pasted image 20250507192412.png]]

Each bounded context has its own persistence adapter (or potentially more than one, as described previously). The term “bounded context” implies boundaries, which means that services of the context may not access persistence adapters of the context, and vice versa. If one account billing context needs something of the other, they can call each other’s domain services, or we can introduce an application service as a coordinator between the bounded contexts

## An example with Spring Data JPA

```java
package buckpal.application.domain.model;

public class Account {

    private AccountId id;
    private Money baselineBalance;
    private ActivityWindow activityWindow;

    // Constructor
    public Account(AccountId id, Money baselineBalance, ActivityWindow activityWindow) {
        this.id = id;
        this.baselineBalance = baselineBalance;
        this.activityWindow = activityWindow;
    }

    // Static factory method: without ID
    public static Account withoutId(Money baselineBalance, ActivityWindow activityWindow) {
        return new Account(null, baselineBalance, activityWindow);
    }

    // Static factory method: with ID
    public static Account withId(AccountId accountId, Money baselineBalance, ActivityWindow activityWindow) {
        return new Account(accountId, baselineBalance, activityWindow);
    }

    // Example balance calculation method (stub)
    public Money calculateBalance() {
        // Logic to calculate balance goes here
        return baselineBalance;
    }

    // Withdraw method stub
    public boolean withdraw(Money money, AccountId targetAccountId) {
        // Logic to handle withdrawal goes here
        return true;
    }

    // Deposit method stub
    public boolean deposit(Money money, AccountId sourceAccountId) {
        // Logic to handle deposit goes here
        return true;
    }

    // Getters (optional, depending on usage)
    public AccountId getId() {
        return id;
    }

    public Money getBaselineBalance() {
        return baselineBalance;
    }

    public ActivityWindow getActivityWindow() {
        return activityWindow;
    }
}

```

```java
package buckpal.adapter.out.persistence;

import jakarta.persistence.*; // or use javax.persistence.* if on older Java
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Table(name = "account")
@Data
@AllArgsConstructor
@NoArgsConstructor
public class AccountJpaEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    // Add other fields if necessary (e.g., balance, user ID, etc.)
}
```

```java
package buckpal.adapter.out.persistence;

import jakarta.persistence.*; // or javax.persistence.* if using older versions
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.time.LocalDateTime;

@Entity
@Table(name = "activity")
@Data
@AllArgsConstructor
@NoArgsConstructor
public class ActivityJpaEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column
    private LocalDateTime timestamp;

    @Column
    private long ownerAccountId;

    @Column
    private long sourceAccountId;

    @Column
    private long targetAccountId;

    @Column
    private long amount;
}

```

```java
package buckpal.adapter.out.persistence;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

import java.time.LocalDateTime;
import java.util.List;
import java.util.Optional;

public interface ActivityRepository extends JpaRepository<ActivityJpaEntity, Long> {

    @Query("""
        select a from ActivityJpaEntity a
        where a.ownerAccountId = :ownerAccountId
        and a.timestamp >= :since
    """)
    List<ActivityJpaEntity> findByOwnerSince(
        @Param("ownerAccountId") long ownerAccountId,
        @Param("since") LocalDateTime since
    );

    @Query("""
        select sum(a.amount) from ActivityJpaEntity a
        where a.targetAccountId = :accountId
        and a.ownerAccountId = :accountId
        and a.timestamp < :until
    """)
    Optional<Long> getDepositBalanceUntil(
        @Param("accountId") long accountId,
        @Param("until") LocalDateTime until
    );

    @Query("""
        select sum(a.amount) from ActivityJpaEntity a
        where a.sourceAccountId = :accountId
        and a.ownerAccountId = :accountId
        and a.timestamp < :until
    """)
    Optional<Long> getWithdrawalBalanceUntil(
        @Param("accountId") long accountId,
        @Param("until") LocalDateTime until
    );
}
```

```java
@RequiredArgsConstructor
@Component
class AccountPersistenceAdapter implements
    LoadAccountPort,
    UpdateAccountStatePort {

    private final AccountRepository accountRepository;
    private final ActivityRepository activityRepository;
    private final AccountMapper accountMapper;

    @Override
    public Account loadAccount(
            AccountId accountId,
            LocalDateTime baselineDate) {

        AccountJpaEntity account = 
            accountRepository.findById(accountId.getValue())
                .orElseThrow(EntityNotFoundException::new);

        List<ActivityJpaEntity> activities = 
            activityRepository.findByOwnerSince(
                accountId.getValue(),
                baselineDate);

        Long withdrawalBalance = activityRepository
            .getWithdrawalBalanceUntil(
                accountId.getValue(),
                baselineDate)
            .orElse(0L);

        Long depositBalance = activityRepository
            .getDepositBalanceUntil(
                accountId.getValue(),
                baselineDate)
            .orElse(0L);

        return accountMapper.mapToDomainEntity(
            account,
            activities,
            withdrawalBalance,
            depositBalance);
    }

    @Override
    public void updateActivities(Account account) {
        for (Activity activity : account.getActivityWindow().getActivities()) {
            if (activity.getId() == null) {
                activityRepository.save(accountMapper.mapToJpaEntity(activity));
            }
        }
    }

    private Long orZero(Long value){
        return value == null ? 0L : value;
    }
}
```

However, JPA then forces us to make compromises in the domain model. For instance, JPA requires entities to have a no-args constructor. Alternatively, it might be that in the persistence layer, a “many-to-one” relationship makes sense from a performance point of view, but in the domain model, we want this relationship to be the other way around.

## What about database transactions?

A transaction should span all write operations to the database that are performed within a certain use case, ensuring that all those operations can be rolled back together if one of them fails.

**==Since the persistence adapter doesn’t know which other database operations are part of the same use case, it cannot decide when to open and close a transaction. We have to delegate this responsibility to the services that orchestrate the calls to the persistence adapter.==**

The easiest way to do this with Java and Spring is to add the annotation to the ``@Transactional`` domain service classes so that Spring will wrap all public methods with a transaction:

Using narrow port interfaces, we’re flexible to implement one port in one way and another port in another way, perhaps even with a different persistence technology, without the application noticing.

# Testing Architecture Elements

## The test pyramid

![[Pasted image 20250511144310.png]]

The basic statement of the pyramid is that we should have high coverage of fine-grained tests that are cheap to build, easy to maintain, fast-running, and stable. These are unit tests that verify that a single unit (usually a class) works as expected.

The pyramid tells us that the more expensive those tests become, the less we should aim for high coverage of these tests because, otherwise, we’ll spend too much time building tests instead of new functionality.

• **Unit tests** are the base of the pyramid. A unit test usually instantiates a single class and tests its functionality through its interface. If the class under test has non-trivial dependencies on other classes, we can replace those dependencies with mock objects that simulate the behavior of the real objects, as required by the test.

• **Integration tests** form the next layer of the pyramid. These tests instantiate a network of multiple units and verify whether this network works as expected, by sending some data into it through the interface of an entry class. In our interpretation, integration tests will cross the boundary between two layers, so the network of objects is not complete or must work against mocks at some point.

• **System tests**, finally, spin up the whole network of objects that make up our application and verify whether a certain use case works as expected through all the layers of the application.

## Testing a domain entity with unit tests

```java
@Test  
void withdrawalSucceeds() {  
    AccountId accountId = new AccountId(1L);  
    Account account = defaultAccount()  
          .withAccountId(accountId)  
          .withBaselineBalance(Money.of(555L))  
          .withActivityWindow(new ActivityWindow(  
                defaultActivity()  
                      .withTargetAccount(accountId)  
                      .withMoney(Money.of(999L)).build(),  
                defaultActivity()  
                      .withTargetAccount(accountId)  
                      .withMoney(Money.of(1L)).build()))  
          .build();  
  
    AccountId randomTargetAccount = new AccountId(99L);  
    boolean success = account.withdraw(Money.of(555L), randomTargetAccount);  
  
    assertThat(success).isTrue();  
    assertThat(account.getActivityWindow().getActivities()).hasSize(3);  
    assertThat(account.calculateBalance()).isEqualTo(Money.of(1000L));  
}
```

Unit tests such as these are our best bet to verify the business rules encoded within our domain entities. We don’t need any other type of test since domain entity behavior has little to no dependencies on other classes.

## Testing a use case with unit tests

```java
@Test  
void transactionSucceeds() {  
  
    Account sourceAccount = givenSourceAccount();  
    Account targetAccount = givenTargetAccount();  
  
    givenWithdrawalWillSucceed(sourceAccount);  
    givenDepositWillSucceed(targetAccount);  
  
    Money money = Money.of(500L);  
  
    SendMoneyCommand command = new SendMoneyCommand(  
          sourceAccount.getId().get(),  
          targetAccount.getId().get(),  
          money);  
  
    boolean success = sendMoneyService.sendMoney(command);  
  
    assertThat(success).isTrue();  
  
    AccountId sourceAccountId = sourceAccount.getId().get();  
    AccountId targetAccountId = targetAccount.getId().get();  
  
    then(accountLock).should().lockAccount(eq(sourceAccountId));  
    then(sourceAccount).should().withdraw(eq(money), eq(targetAccountId));  
    then(accountLock).should().releaseAccount(eq(sourceAccountId));  
  
    then(accountLock).should().lockAccount(eq(targetAccountId));  
    then(targetAccount).should().deposit(eq(money), eq(sourceAccountId));  
    then(accountLock).should().releaseAccount(eq(targetAccountId));  
  
    thenAccountsHaveBeenUpdated(sourceAccountId, targetAccountId);  
}

private void thenAccountsHaveBeenUpdated(AccountId... accountIds){  
    ArgumentCaptor<Account> accountCaptor = ArgumentCaptor.forClass(Account.class);  
    then(updateAccountStatePort).should(times(accountIds.length))  
          .updateActivities(accountCaptor.capture());  
  
    List<AccountId> updatedAccountIds = accountCaptor.getAllValues()  
          .stream()  
          .map(Account::getId)  
          .map(Optional::get)  
          .collect(Collectors.toList());  
  
    for(AccountId accountId : accountIds){  
       assertThat(updatedAccountIds).contains(accountId);  
    }
}

private Account givenTargetAccount(){  
    return givenAnAccountWithId(new AccountId(42L));  
}  
  
private Account givenSourceAccount(){  
    return givenAnAccountWithId(new AccountId(41L));  
}
```

Since the use case service under test is stateless, we cannot verify a certain state in the section. then Instead, the test verifies that the service has interacted with certain methods on its (mocked) dependencies. This means that the test is vulnerable to changes in the structure of the code under test and not only its behavior. This, in turn, means that there is a higher chance that the test has to be modified if the code under test is refactored.

**==While this test is still a unit test, it borders on being an integration test because we test the interaction on dependencies.==**

## Testing a web adapter with integration tests

```java
@WebMvcTest(controllers = SendMoneyController.class)  
class SendMoneyControllerTest {  
  
    @Autowired  
    private MockMvc mockMvc;  
  
    @MockBean  
    private SendMoneyUseCase sendMoneyUseCase;  
  
    @Test  
    void testSendMoney() throws Exception {  
  
       mockMvc.perform(post("/accounts/send/{sourceAccountId}/{targetAccountId}/{amount}",  
             41L, 42L, 500)  
             .header("Content-Type", "application/json"))  
             .andExpect(status().isOk());  
  
       then(sendMoneyUseCase).should()  
             .sendMoney(eq(new SendMoneyCommand(  
                   new AccountId(41L),  
                   new AccountId(42L),  
                   Money.of(500L))));  
    }  
  
}
```

We’re not actually testing via the HTTP protocol since we’re mocking that away with the ``MockMvc`` object. We trust that the framework translates everything to and from HTTP properly. There’s no need to test the framework.

**==So, why is this an integration test and not a unit test? Even though it seems that we only test a single web controller class in this test, there’s a lot more going on under the hood. With the ``@WebMvcTest`` annotation, we tell Spring to instantiate a whole network of objects that is responsible for responding to certain request paths, mapping between Java and JSON, validating HTTP input, and so on. And in this test, we verify that our web controller works as a part of this network.==**

## Testing a persistence adapter with integration tests

```java
@DataJpaTest  
@Import({AccountPersistenceAdapter.class, AccountMapper.class})  
class AccountPersistenceAdapterTest {  
  
    @Autowired  
    private AccountPersistenceAdapter adapterUnderTest;  
  
    @Autowired  
    private ActivityRepository activityRepository;  
  
    @Test  
    @Sql("AccountPersistenceAdapterTest.sql")  
    void loadsAccount() {  
       Account account = adapterUnderTest.loadAccount(new AccountId(1L), LocalDateTime.of(2018, 8, 10, 0, 0));  
  
       assertThat(account.getActivityWindow().getActivities()).hasSize(2);  
       assertThat(account.calculateBalance()).isEqualTo(Money.of(500));  
    }  
  
    @Test  
    void updatesActivities() {  
       Account account = defaultAccount()  
             .withBaselineBalance(Money.of(555L))  
             .withActivityWindow(new ActivityWindow(  
                   defaultActivity()  
                         .withId(null)  
                         .withMoney(Money.of(1L)).build()))  
             .build();  
  
       adapterUnderTest.updateActivities(account);  
  
       assertThat(activityRepository.count()).isEqualTo(1);  
  
       ActivityJpaEntity savedActivity = activityRepository.findAll().get(0);  
       assertThat(savedActivity.getAmount()).isEqualTo(1L);  
    }  
  
}
```

An important aspect of these tests is that we’re not mocking away the database. The tests actually hit the database. Had we mocked the database away, the tests would still cover the same lines of code, producing the same high coverage of lines of code. However, despite this high coverage, the tests would still have a rather high chance of failing in a setup with a real database, due to errors in SQL statements or unexpected mapping errors between database tables and Java objects.

persistence adapter tests should run against the real database. Libraries such as ``Testcontainers`` are a great help in this regard, spinning up a Docker container with a database on demand

## Testing main paths with system tests

A system test starts up the whole application and runs requests against its API, verifying that all our layers work in concert. Hexagonal Architecture is all about creating a well-defined boundary between our application and the outside world. Doing so makes our application boundaries very testable by design.

![[Pasted image 20250511145702.png]]

however, that, instead of writing “application tests” that mock away the input and output adapters, we should aim to write “system tests” that cover the whole path from a real input adapter to a real output adapter. These tests uncover many subtle bugs that we wouldn’t catch if we mocked away the input and output adapters. These bugs include mapping errors between the layers, or simply wrong expectations between the application and the outside systems it’s talking to.

There are valid reasons to test against mock adapters instead of real adapters, of course. If our application runs in multiple profiles, for example, and each profile uses a different (real) input or output adapter implemented against the same input and output ports, we might want to have tests that isolate errors in the application from errors in the adapters. Application tests that cover only our hexagon are exactly the tool we want, then. However, for a standard web application with a database, where the input and output adapters are rather static, we probably want to focus on system tests instead.

```java
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)  
class SendMoneySystemTest {  
  
    @Autowired  
    private TestRestTemplate restTemplate;  
  
    @Autowired  
    private LoadAccountPort loadAccountPort;  
  
    @Test  
    @Sql("SendMoneySystemTest.sql")  
    void sendMoney() {  
  
       Money initialSourceBalance = sourceAccount().calculateBalance();  
       Money initialTargetBalance = targetAccount().calculateBalance();  
  
       ResponseEntity response = whenSendMoney(  
             sourceAccountId(),  
             targetAccountId(),  
             transferredAmount());  
  
       then(response.getStatusCode())  
             .isEqualTo(HttpStatus.OK);  
  
       then(sourceAccount().calculateBalance())  
             .isEqualTo(initialSourceBalance.minus(transferredAmount()));  
  
       then(targetAccount().calculateBalance())  
             .isEqualTo(initialTargetBalance.plus(transferredAmount()));  
  
    }  
  
    private Account sourceAccount() {  
       return loadAccount(sourceAccountId());  
    }  
  
    private Account targetAccount() {  
       return loadAccount(targetAccountId());  
    }  
  
    private Account loadAccount(AccountId accountId) {  
       return loadAccountPort.loadAccount(  
             accountId,  
             LocalDateTime.now());  
    }  
  
  
    private ResponseEntity whenSendMoney(  
          AccountId sourceAccountId,  
          AccountId targetAccountId,  
          Money amount) {  
       HttpHeaders headers = new HttpHeaders();  
       headers.add("Content-Type", "application/json");  
       HttpEntity<Void> request = new HttpEntity<>(null, headers);  
  
       return restTemplate.exchange(  
             "/accounts/send/{sourceAccountId}/{targetAccountId}/{amount}",  
             HttpMethod.POST,  
             request,  
             Object.class,  
             sourceAccountId.getValue(),  
             targetAccountId.getValue(),  
             amount.getAmount());  
    }  
  
    private Money transferredAmount() {  
       return Money.of(500L);  
    }  
  
    private Money balanceOf(AccountId accountId) {  
       Account account = loadAccountPort.loadAccount(accountId, LocalDateTime.now());  
       return account.calculateBalance();  
    }  
  
    private AccountId sourceAccountId() {  
       return new AccountId(1L);  
    }  
  
    private AccountId targetAccountId() {  
       return new AccountId(2L);  
    }  
  
}
```

While a domain-specific language such as this is a good idea in any type of test, it’s even more important in system tests. System tests simulate the real users of the application much better than unit or integration tests can, so we can use them to verify the application from the viewpoint of the user. This is much easier with a suitable vocabulary at hand. This vocabulary also enables domain experts, who are best suited to embody a user of the application and probably aren’t programmers, to reason about the tests and give feedback.

System tests play out their strength best if they combine multiple use cases to create scenarios. Each scenario represents a certain path a user might typically take through the application. If the most important scenarios are covered by passing system tests, we can assume that we haven’t broken them with our latest modifications and are ready to ship.

## How much testing is enough?

Line coverage is a bad metric to measure test success. Any goal other than 100% is completely meaningless because important parts of the code base might not be covered at all.6 And even at 100%, we still can’t be sure that every bug has been squashed.

I suggest measuring test success by how comfortable we feel shipping the software. If we trust the tests enough to ship after having executed them, we’re good. The more often we ship, the more trust we have in our tests.

helps, however, to start with a strategy that defines the tests we should create. One such strategy for our Hexagonal Architecture is this:

**==• While implementing a domain entity, cover it with a unit test.**==
==**• While implementing a use case service, cover it with a unit test.**==
==**• While implementing an adapter, cover it with an integration test.**==
==**• Cover the most important paths a user can take through the application with a system test.==**

Note the phrase while implementing – when tests are done during the development of a feature and
not after, they become a development tool and no longer feel like a chore.

# Mapping between Boundaries

## The “No Mapping” strategy

![[Pasted image 20250511153024.png]]

Since all layers use the same model, we don’t need to implement mapping between them. But what are the consequences of this design?

The web and persistence layers may have special requirements for their models. If our web layer exposes its model via REST, for instance, the model classes might need some annotations that define how to serialize certain fields into JSON. The same is true for the persistence layer if we’re using an object-relational mapping (ORM) framework, which might require some annotations that define the database mapping. The framework might also require the class to follow a certain contract.

This violates the Single Responsibility Principle since the class has to be changed for reasons related to Account the web, application, and persistence layers. Aside from the technical requirements, each layer might require certain custom fields on the Account class. This might lead to a fragmented domain model with certain fields only relevant in one layer.

**==As long as all layers need exactly the same information in exactly the same structure, a “no mapping” strategy is a perfectly valid option.==**

even though we have decided on a certain mapping strategy in the past, we can change it later.

## The “Two-Way” mapping strategy

Each layer has its own model, which may have a structure that is completely different from the domain model. 

The web layer maps the web model into the input model that is expected by the incoming ports. It also maps domain objects returned by the incoming ports back into the web model.

The persistence layer is responsible for a similar mapping between the domain model, which is used by the outgoing ports, and the persistence model. Both layers map in two directions, hence the name “Two-Way” mapping.

With each layer having its own model, it can modify its own model without affecting the other layers

This mapping strategy also leads to a clean domain model that is not dirtied by web or persistence concerns. It does not contain JSON or ORM mapping annotations. The Single Responsibility Principle is satisfied.

Another bonus of “Two-Way” mapping is that, after the “No Mapping” strategy, it’s conceptually the simplest mapping strategy. The mapping responsibilities are clear: the outer layers/adapters map into the model of the inner layers and back. The inner layers only know their own model and can concentrate on the domain logic instead of mapping.

As with every mapping strategy, the “Two-Way” mapping also has its drawbacks. First of all, it usually ends up in a lot of boilerplate code.

Another potential drawback is that the incoming and outgoing ports use domain objects as input parameters and return values. The adapters map these into their own model, but this still creates more coupling between the layers than if we introduce a dedicated “transport model” as in the “full” mapping strategy

## The “Full” mapping strategy

![[Pasted image 20250511153403.png]]

This mapping strategy introduces a separate input and output model per operation. Instead of using the domain model to communicate across layer boundaries, we use a model specific to each operation

Naturally, mapping from one layer into many different commands requires even more mapping code than mapping between a single web model and a domain model. This mapping, however, is significantly easier to implement and maintain than a mapping that has to handle the needs of many use cases instead of only one.

No single mapping strategy needs to be a global rule across all layers

## The “One-Way” mapping strategy

![[Pasted image 20250511153445.png]]

In this strategy, the models in all layers implement the same interface, which encapsulates the state of the domain model by providing getter methods on the relevant attributes.

The domain model itself can implement a rich behavior, which we can access from our services within the application layer. If we want to pass a domain object to the outer layers, we can do so without mapping since the domain object implements the state interface expected by the incoming and outgoing ports.

The mapping responsibility is clear: if a layer receives an object from another layer, we map it into something the layer can work with. Thus, each layer only maps one way, making this a “One-Way” mapping strategy.

This strategy plays out its strength best if the models across the layers are similar. For read-only operations, for instance, the web layer then might not need to map into its own model at all since the state interface provides all the information it needs.

## When to use which mapping strategy?

Since each mapping strategy has different advantages and disadvantages, we should resist the urge to define a single strategy as a hard-and-fast global rule for the whole code base. This goes against our instincts, as it feels untidy to mix patterns within the same code base. But knowingly choosing a pattern that is not the best pattern for a certain job, just to serve our sense of tidiness, is irresponsible, plain and simple.

Also, as software evolves over time, the strategy that was the best for the job yesterday might not still be the best for the job today. Instead of starting with a fixed mapping strategy and keeping it over time – no matter what – we might start with a simple strategy that allows us to quickly evolve the code and later move to a more complex one that helps us to better decouple the layers.

Guidelines for these situations might look like this:
==**• If we’re working on a modifying use case, the “Full” mapping strategy is the first choice between the web and application layer, in order to decouple the use cases from one another. This gives us clear per-use-case validation rules and we don’t have to deal with fields we don’t need in a certain use case.**==

==**• If we’re working on a modifying use case, the “No Mapping” strategy is the first choice between the application and persistence layer in order to be able to quickly evolve the code without mapping overhead. As soon as we have to deal with persistence issues in the application layer, however, we move to a “Two-Way” mapping strategy to keep persistence issues in the persistence layer.**==

==**• If we’re working on a query, the “No Mapping” strategy is the first choice between the web and application layer and between the application and persistence layer in order to be able to quickly evolve the code without mapping overhead. As soon as we have to deal with web or persistence issues in the application layer, however, we move to a “Two-Way” mapping strategy between the web and application layer or the application layer and persistence layer, respectively**==

## How does this help me build maintainable software?

With narrow ports in place for each use case, we can choose different mapping strategies for different use cases, and even evolve them over time without affecting other use cases, thus selecting the best strategy for a certain situation at a certain time.

# Assembling the Application

## Why even care about assembly?

Why aren’t we just instantiating the use cases and adapters when and where we need them? Because we want to keep the code dependencies pointed in the right direction. Remember: all dependencies should point inward, toward the domain code of our application, so that the domain code doesn’t have to change when something in the outer layers changes.

So, who’s responsible for creating our object instances? And how do we do it without violating the **Dependency Rule**?

The answer is that there must be a configuration component that is neutral to our architecture and that has a dependency to all classes in order to instantiate them

![[Pasted image 20250512180445.png]]

The configuration component is responsible for assembling a working application from the parts we provided. It must do the following:
**==• Create web adapter instances.**==
==**• Ensure that HTTP requests are actually routed to the web adapters.**==
==**• Create use case instances.**==
==**• Provide web adapters with use case instances.**==
==**• Create persistence adapter instances.**==
==**• Provide use cases with persistence adapter instances.**==
==**• Ensure that the persistence adapters can actually access the database.==**

These are a lot of responsibilities (read: reasons to change). Aren’t we violating the **Single Responsibility Principle** here? Yes, we are, but if we want to keep the rest of the application clean, we need an outside component that takes care of the wiring. And this component has to know all the moving parts to assemble them into a working application.

## Assembling via plain code

```java
package buckpal.configuration;

class Application {

    public static void main(String[] args) {
        AccountRepository accountRepository = new AccountRepository();
        ActivityRepository activityRepository = new ActivityRepository();
        AccountPersistenceAdapter accountPersistenceAdapter =
            new AccountPersistenceAdapter(accountRepository, activityRepository);

        SendMoneyUseCase sendMoneyUseCase =
            new SendMoneyUseService(
                accountPersistenceAdapter,  // LoadAccountPort
                accountPersistenceAdapter); // UpdateAccountStatePort

        SendMoneyController sendMoneyController =
            new SendMoneyController(sendMoneyUseCase);

        startProcessingWebRequests(sendMoneyController);
    }
}
```

This plain code approach is the most basic way of assembling an application. It has some drawbacks, however:

**==• First of all, the preceding code is for an application that has only a single web controller, use case, and persistence adapter. Imagine how much code like this we would have to produce to bootstrap a full-blown enterprise application!**==

==**• Second, since we’re instantiating all classes ourselves from outside of their packages, those classes all need to be public. This means, for example, that the Java compiler doesn’t prevent a use case from directly accessing a persistence adapter since it’s public. It would be nice if we could avoid unwanted dependencies like this by using package-private visibility==**

## Assembling via Spring’s classpath scanning

With classpath scanning, Spring goes through all classes that are available in a certain slice of the classpath and searches for classes that are annotated with the ``@Component`` annotation. The framework then creates an object from each of these classes. The classes should have a constructor that takes all required fields as an argument, like our ``AccountPersistenceAdapter``

```java
@Component
@RequiredArgsConstructor
class AccountPersistenceAdapter implements 
    LoadAccountPort,
    UpdateAccountStatePort {

    private final AccountRepository accountRepository;
    private final ActivityRepository activityRepository;
    private final AccountMapper accountMapper;

    @Override
    public Account loadAccount(AccountId accountId, LocalDateTime baselineDate) {
        ...
    }

    @Override
    public void updateActivities(Account account) {
        ...
    }
}
```


Spring will find this constructor and search for `@Component`-annotated classes of the required argument types and instantiate them in a similar manner to add them to the application context. Once all required objects are available, it will finally call the constructor of `AccountPersistenceAdapter` and add the resulting object to the application context as well. Classpath scanning is a very convenient way of assembling an application. We only have to sprinkle some `@Component` annotations across the code base and provide the right constructors. We can also create our own stereotype annotation for Spring to pick up. We could, for example, create a `@PersistenceAdapter` annotation.

```java
@Target({ElementType.TYPE})  
@Retention(RetentionPolicy.RUNTIME)  
@Documented  
@Component  
public @interface PersistenceAdapter {  
  
  /**  
   * The value may indicate a suggestion for a logical component name,   * to be turned into a Spring bean in case of an autodetected component.   * @return the suggested component name, if any (or empty String otherwise)  
   */  @AliasFor(annotation = Component.class)  
  String value() default "";  
  
}
```

We could now use ``@PersistenceAdapter`` instead of ``@Component`` to mark our persistence adapter classes as parts of our application. With this annotation, we have made our architecture more evident to people reading the code.

**==The classpath scanning approach has its drawbacks, however. First, it’s invasive in that it requires us to add a framework-specific annotation to our classes==**. If you’re a Clean Architecture hardliner, you’d say that this is forbidden as it binds our code to a specific framework.

Another potential drawback of the classpath scanning approach is that magic things might happen. And by magic, I mean the bad kind of magic causing inexplicable effects that might take days to figure out if you’re not a Spring expert. Magic happens because classpath scanning is a very blunt weapon to use for application assembly. We simply point Spring at the parent package of our application and tell it to go looking for `@Component`-annotated classes within this package.

Do you know every single class that exists within your application by heart? Probably not. There are bound to be some classes that we don’t actually want to have in the application context. Perhaps this class even manipulates the application context in evil ways, causing errors that are hard to track.

## Assembling via Spring’s Java Config

In this approach, we create configuration classes, each responsible for constructing a set of beans that are to be added to the application context.

```java
@Configuration
@EnableJpaRepositories
class PersistenceAdapterConfiguration {

    @Bean
    AccountPersistenceAdapter accountPersistenceAdapter(
        AccountRepository accountRepository,
        ActivityRepository activityRepository,
        AccountMapper accountMapper){
        return new AccountPersistenceAdapter(
            accountRepository,
            activityRepository,
            accountMapper);
    }

    @Bean
    AccountMapper accountMapper(){
        return new AccountMapper();
    }
}
```

we’re still using classpath scanning, but we only pick up our configuration classes instead of every single bean, which reduces the chance of evil magic happening.

this approach does not force us to sprinkle ``@Component`` annotations all over our code base, like the classpath scanning approach does. So, we can keep our application layer clean without any dependency on the Spring framework (or any other framework, for that matter).

**==There is a catch with this solution, however. If the configuration class is not within the same package as the classes of the beans it creates (the persistence adapter classes in this case), those classes must be public. To restrict visibility, we can use packages as module boundaries and create a dedicated configuration class within each package. This way, we cannot use sub-packages==**

## How does this help me build maintainable software?

By creating a dedicated configuration component responsible for assembling our application, we can liberate our application code from this responsibility (read: “reason for change” – remember the “S” in “SOLID”?). We’re rewarded with highly cohesive modules that we can start up in isolation from each other and that we can easily move around within our code base. As usual, this comes at the price of spending some extra time to maintain this configuration component.

# Taking Shortcuts Consciously

## Why shortcuts are like broken windows

**Broken Windows Theory**

Applied to working with code, this means the following:

**==• When working on a low-quality code base, the threshold to add more low-quality code is low.**==
==**• When working on a code base with a lot of coding violations, the threshold to add another coding violation is low.**==
==**• When working on a code base with a lot of shortcuts, the threshold to add another shortcut is low.==**

## The responsibility of starting clean

We should take great care to document such consciously added shortcuts, for example, in the form of Architecture Decision Records (ADRs), as proposed by Michael Nygard in his blog. We owe that to our future selves and our successors. If every member of the team is aware of this documentation, it will even reduce the Broken Windows effect because the team will know that the shortcuts have been taken consciously and for good reason.

## Sharing models between use cases

Different use cases should have different **input** and output **models**, meaning that the types of the input parameters and the types of the return values should be different

![[Pasted image 20250512185629.png]]

The effect of sharing in this case is that and are ``SendMoneyUseCase`` and ``RevokeActivityUseCase`` coupled to each other.

Sharing input and output models between use cases is valid if the use cases are functionally coupled, that is, if they share a certain requirement. In this case, we actually want both use cases to be affected if we change a certain detail. If both use cases should be able to evolve separately from each other, however, this is a shortcut. In this case, we should separate the use cases from the start, even if it means duplicating input and output classes if they look the same at the start. So, when building multiple use cases around a similar concept, it’s worthwhile to regularly ask the question of whether the use cases should evolve separately from each other. As soon as the answer becomes “yes,” it’s time to separate the input and output models

## Using domain entities as the input or output model

![[Pasted image 20250512190000.png]]

**==As soon as a use case is not simply about updating a couple of fields in the database, but instead implements more complex domain logic (potentially delegating part of the domain logic to a rich domain entity), we should use a dedicated input and output model for the use case interface, because we don’t want changes in the use case to propagate to the domain entity.==**

What makes this shortcut dangerous is the fact that many use cases start their lives as a simple create or update use case only to become beasts of complex domain logic over time. This is especially true in an agile environment where we start with a minimum viable product and add complexity as we move forward. So, if we used a domain entity as the input model at the start, we must find the point in time to replace it with a dedicated input model that is independent of the domain entity.

## Skipping incoming ports

![[Pasted image 20250512190500.png]]

The incoming ports, however, define the entry points into our application core. Once we remove them, we must know more about the internals of our application to find out which service method we can call to implement a certain use case. By maintaining dedicated incoming ports, we can identify the entry points to the application at a glance. This makes it especially easy for new developers to get their bearings in the code base.

Another reason to keep the incoming ports is that they allow us to easily enforce architecture. With the enforcement options we can make certain that incoming adapters only call incoming ports and not application services. This makes every entry point into the application layer a very conscious decision. We can no longer accidentally call a service method that was not meant to be called from an incoming adapter.

## Skipping services

Aside from the incoming ports, for certain use cases, we might want to skip the service layer as a whole,

![[Pasted image 20250512190626.png]]

It is very tempting to do this for simple CRUD use cases since in this case a service usually only forwards a create, update, or delete request to the persistence adapter, without adding any domain logic. Instead of forwarding, we can let the persistence adapter implement the use case directly.

This, however, requires a shared model between the incoming adapter and the outgoing adapter, which is the ``Account`` domain entity in this case, so it usually means that we’re using the domain model as the input model, as described previously.

In the end, to prevent boilerplate pass-through services, we might choose to skip the services for simple CRUD use cases after all. Then, however, the team should develop clear guidelines to introduce a service as soon as the use case is expected to do more than just create, update, or delete an entity.

## How does this help me build maintainable software?

Even though shortcuts may be acceptable at times, we want to make the decision to take a shortcut consciously. That means that we should define one “right” way of doing things and enforce this way, so that we can deviate from that way if there are good reasons to do so.

# Enforcing Architecture Boundaries

software project, however, architecture tends to erode over time. Boundaries between layers weaken, code becomes harder to test, and we generally need more and more time to implement new features.

## Boundaries and dependencies

![[Pasted image 20250513091344.png]]

The innermost layer contains domain entities and domain services. The application layer around it may access those entities and services to implement a use case, usually through an application service. Adapters access those services through incoming ports or are being accessed by those services through outgoing ports. Finally, the configuration layer contains factories that create adapter and service objects and provides them to a dependency injection mechanism.

According to the Dependency Rule, dependencies that cross such a layer boundary must always point inward.

## Visibility modifiers

So, why is the package-private modifier such an important modifier? **==Because it allows us to use Java packages to group classes into cohesive “modules.” Classes within such a module can access each other, but cannot be accessed from outside of the package.==** We can then choose to make specific classes public to act as entry points to the module. This reduces the risk of accidentally violating the Dependency Rule by introducing a dependency that points in the wrong direction.

![[Pasted image 20250513091606.png]]

We can make the classes in the persistence package package-private (marked with o in the tree above) because they don’t need to be accessed by the outside world. The ``persistence`` adapter is accessed through the output ports it implements. For the same reason, we can make the ``SendMoneyService`` class package-private.

The rest of the classes in the example have to be public (marked with +) as defined by our architecture: the ``domain`` package needs to be accessible by the other layers and the application layer needs to be accessible by the ``web`` and ``persistence`` adapters.

Once a package reaches a certain number of classes, however, it grows confusing to have so many classes in the same package. In this case, I like to create sub-packages to make the code easier to find (and, I admit, to satisfy my sense of aesthetics). This is where the package-private modifier fails to deliver, since Java treats sub-packages as different packages and we cannot access a package-private member of a sub-package. So, members in sub-packages must be public, exposing them to the outside world and thus making our architecture vulnerable to illegal dependencies.

## Post-compile fitness function

One way is to introduce a **fitness function** – a function that takes our architecture as input and determines its fitness in regard to a specific aspect. In our case, fitness is defined as the Dependency Rule is not violated.

A tool that supports this kind of architectural fitness function for Java is ``ArchUnit``. Among other things, ``ArchUnit`` provides an API to check whether dependencies point in the expected direction. If it finds a violation, it will throw an exception. It’s best run from within a test based on a unit testing framework such as JUnit, making the test fail in case of a dependency violation.

```java
@Test  
void domainModelDoesNotDependOnOutside() {  
    noClasses()  
          .that()  
          .resideInAPackage("io.reflectoring.buckpal.application.domain.model..")  
          .should()  
          .dependOnClassesThat()  
          .resideOutsideOfPackages(  
                "io.reflectoring.buckpal.application.domain.model..",  
                "lombok..",  
                "java.."  
          )  
          .check(new ClassFileImporter()  
                .importPackages("io.reflectoring.buckpal.."));  
}
```

![[Pasted image 20250513092039.png]]

The problem with the preceding rule is that if we use some library code in the domain model, we have to add an exception to this rule for every dependency we introduce With a little work, we can even create a kind of **domain-specific language (DSL)** on top of the ``ArchUnit`` API that allows us to specify all relevant packages within our Hexagonal Architecture and then automatically check whether all dependencies between those packages point in the right direction:

```java
@Test  
void validateRegistrationContextArchitecture() {  
    HexagonalArchitecture.basePackage("io.reflectoring.buckpal")  
  
          .withDomainLayer("application.domain")  
  
          .withAdaptersLayer("adapter")  
          .incoming("in.web")  
          .outgoing("out.persistence")  
          .and()  
  
          .withApplicationLayer("application")  
          .incomingPorts("port.in")  
          .outgoingPorts("port.out")  
          .and()  
  
          .withConfiguration("configuration")  
          .check(new ClassFileImporter()  
                .importPackages("io.reflectoring.buckpal.."));  
}
```

## Build artifacts

A main feature of build tools is dependency resolution. To transform a certain code base into a build artifact, a build tool first checks whether all the artifacts the code base depends on are available. If not, it tries to load them from an artifact repository

 **Advantages of Using Build Modules to Demarcate Architecture Boundaries**

Using build modules instead of simple packages provides several important benefits:

- **Avoidance of Circular Dependencies**
    
    - Build tools prevent circular dependencies, which can lead to endless loops and violate the Single Responsibility Principle.
        
    - Java allows circular dependencies between packages, but build tools like Maven or Gradle enforce stricter separation.
        
- **Support for Isolated Code Changes**
    
    - Build modules enable isolated development and testing.
        
    - If modules like adapters and the application layer are separated, errors in one do not block testing in the other.
        
    - This separation allows better development flow in IDEs and during build processes, and even supports placing modules in separate repositories for team autonomy.
        
- **Explicit Dependency Management**
    
    - Inter-module dependencies must be explicitly declared in build scripts.
        
    - This encourages developers to carefully consider the necessity and validity of new dependencies, reducing accidental tight coupling.

## How does this help me build maintainable software?

When producing new code or refactoring existing code, we should keep the package structure in mind and use package-private visibility when possible, to avoid dependencies to classes that should not be accessed from outside the package.

# Managing Multiple Bounded Contexts

The term “bounded context” tells us that there should be boundaries between the different domains. If we don’t have boundaries between different domains, there are no restrictions on dependencies between classes in these domains. Eventually, dependencies will grow between the domains, coupling them together. This coupling means that the domains can no longer evolve in isolation, but can only evolve together.

The whole reason to separate code into different domains is so that these domains can evolve in isolation.

Managing bounded contexts, that is, keeping the boundaries between them clear, is one of the main challenges of software engineering. Many of the pains developers associate with so-called “legacy software stem from unclear boundaries. And it turns out that software doesn’t need long to become “legacy.”

## One hexagon per bounded context?

When working with Hexagonal Architecture and multiple bounded contexts, our reflex is to create a separate “hexagon” for each bounded context

![[Pasted image 20250513105154.png]]

Each bounded context lives in its own hexagon, providing input ports to interact with it and using output ports to interact with the outside world.

If we use the architecture elements that Hexagonal Architecture provides us with, we add an output port to the first bounded context and an input port to the second bounded context. Then, we create an adapter that implements the output port, does any necessary mapping, and calls the input port of the second bounded context.

on paper this looks like a very clean solution
![[Pasted image 20250513105249.png]]

For each dependency, we would have to implement one adapter with at least one associated input and output port. **==Each adapter would have to map from one domain model to another. This quickly becomes a chore to develop and maintain. If it’s a chore and requires more effort than it brings value, the team will take shortcuts to avoid it, resulting in an architecture that looks like a Hexagonal Architecture at first glance but doesn’t have the benefits it promises.==**

The takeaway here is that Hexagonal Architecture doesn’t provide a scalable solution for managing multiple bounded contexts in the same application. And it doesn’t have to.

## Decoupled bounded contexts

we learned that the ports and adapters should encapsulate the whole application, not each bounded context separately.

In a simple case, we might have bounded contexts that don’t communicate with each other. The provide completely separate paths through the code.

![[Pasted image 20250513105554.png]]

Each bounded context exposes its own use cases via one or more dedicated input ports. The web adapter knows all input ports and thus can call the functionality of all bounded contexts.

Instead of having dedicated input ports for each of our bounded contexts, we could also implement one “broad” input port through which the web adapter routes requests to multiple bounded contexts. In this case, the boundaries between the contexts would be hidden from the outside of our hexagon.

Furthermore, each bounded context defines its own output port to the database so that it can store and retrieve its data independently of any other bounded context.

Each bounded context should have its own persistence. If bounded contexts share output ports to store and retrieve data, they will quickly become strongly coupled because they both depend on the same data model.

## Appropriately coupled bounded contexts

If all coupling could be avoided, software architecture would be a lot easier. In real-world applications, a bounded context very likely needs the help of another bounded context to do its work.


In a system with multiple bounded contexts, such as one for **transaction management** and another for **user management**, it's important to avoid tight coupling. For instance, the transaction context may need to know which user initiated a transaction for logging or validation, but it doesn't need the entire user object—just the user ID may suffice. To maintain loose coupling, one strategy is to use **domain events**. When a user’s status changes in the user management context (e.g., gets blocked), a domain event is emitted, and other contexts like transaction management can listen and update their own local data accordingly. Alternatively, an **application service** can act as an orchestrator, querying the user status from the user management context before invoking the transaction logic. Both approaches allow for collaboration between bounded contexts without introducing tight dependencies.

![[Pasted image 20250513110020.png]]

We have introduced an application service as the orchestrator above our bounded contexts. The input ports are now implemented by this service instead of by the bounded contexts themselves. The application service may call output ports to get the required information from other systems and then calls one or more domain services provided by the bounded contexts. In addition to orchestrating the calls to the bounded contexts, the application service also acts as a transaction boundary so that we can call multiple domain services in the same database transaction,

The domain services within the bounded contexts each still use their own database output ports to keep the data model between the bounded contexts separated. We may decide that this separation is not necessary and use a single database output port instead (but we should be aware that sharing a data model leads to very tight coupling).

## How does this help me build maintainable software?

Hexagonal Architecture is all about managing a boundary between an application and the outside world. The boundary is made up of certain input ports provided by the application and certain output ports expected by the application.

Hexagonal Architecture does not help us to manage finer-grained boundaries within our application. Inside our “hexagon,” we can do whatever we want.

# A Component-Based Approach to Software Architecture

how can we create a software architecture that can cope with such an agile environment? If everything can change at any time, should we even bother with architecture?

This architecture enhances maintainability because the application can mostly evolve independently of the outside world. **==As long as the ports don’t change, we can evolve anything within the application to react to changes in the agile environment==**

## Modularity through components

One of the drivers of maintainability is modularity. Modularity allows us to conquer the complexity of a software system by dividing it into simpler modules

> This modularity had lots of advantages. It meant that each component could be built to focus on one part of the problem and would need to compromise less in its design. It allowed different groups – in this case, completely different companies – to work on each module largely independently of the others. As long as the different groups agreed on how the modules would interface with each other, they could work to solve the problems of their module without constraint.”

I prefer the term “component” to describe a group of classes that were thoughtfully engineered to implement certain functionality that can be composed together with other groups of classes to build a complex system

**==a component is a set of classes that has a dedicated namespace and a clearly defined API. If another component needs this component’s functionality, it can call it via its API, but it may not reach into its internals.==** A component may be made up of smaller components. By default, these sub-components live inside the internals of the parent component, so that they are not accessible from the outside. They can, however, contribute to the parent component’s API if they implement functionality that should be accessible from the outside.

![[Pasted image 20250513165452.png]]

It can be summarized in four simple rules:
1. ==**A component has a dedicated namespace to be addressable.**==
2. ==**A component has a dedicated API and internals.**==
3. ==**A component’s API may be called from the outside, but its internals may not.**==
4. ==**A component may contain sub-components as part of its internals.==**

## Enforcing component boundaries

We need to enforce the conventions of the component architecture.

The nice thing about the component architecture is that we can apply a relatively simple fitness function to make sure that no accidental dependencies have crept into our component architecture:

No classes that are outside of an “internal” package should access a class inside of that “internal” package

```kotlin
private fun assertPackageIsNotAccessedFromOutside(internalPackage: String) {
        noClasses()
            .that()
            .resideOutsideOfPackage(packageMatcher(internalPackage))
            .should()
            .dependOnClassesThat()
            .resideInAPackage(packageMatcher(internalPackage))
            .check(analyzedClasses)
    }
```

We can still introduce unwanted dependencies by just not following our convention for internal packages, of course. And the rule still allows a loophole: if we put classes directly into the “internal” package of a top-level component, the classes of any sub-components may access it. So, we might want to introduce another rule that disallows any classes directly in the “internal” package of a top-level component.

