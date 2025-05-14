# 🔍 What Is _Not_ Hexagonal Architecture? 

Hexagonal Architecture (HA), despite its simplicity, is often misunderstood or mixed up with other software design concepts. Here's a summary of **what Hexagonal Architecture is _not_**:

---
## ✅ **It is NOT:**

- **A strict recipe or detailed framework.**  
    HA doesn’t dictate folder structures, naming conventions, or specific technologies.
    
- **Clean Architecture (with capital C).**  
    Although Clean Architecture builds upon HA principles, it's a more opinionated and layered version, popularized by Robert C. Martin.
    
- **Onion Architecture.**  
    Similar in concept, but a different interpretation with its own layering and terminology.
    
- **About layers, command buses, or use case orchestration.**  
    Those are implementations or additions, not requirements of HA itself.
    
- **Domain-Driven Design (DDD).**  
    HA can support DDD, but they are independent concepts and can be used separately.
    
- **CQRS or Event Sourcing.**  
    These can coexist with HA but are not part of it.
    
- **A solution for every project.**  
    Its benefits shine in complex applications with multiple entry points but may be unnecessary in simpler contexts.
# 🎯 The Intent

>Allow an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.

The idea of Hexagonal Architecture is to put inputs and outputs at the edges of our design. Business logic should not depend on whether we expose a REST or a ``GraphQL`` API, and it should not depend on where we get data from — a database, a microservice API exposed via ``gRPC`` or REST, or just a simple CSV file.

In practice, this means that **business logic should be isolated** **from** any **infrastructure** and **framework** code and be **completely independent** of them.

# ⚖️ The Principle

> **Invert the dependencies** so that the application core (business logic) is the center of the system, and all interactions with the outside world occur through well-defined boundaries (ports).

Hexagonal Architecture is guided by the **Dependency Inversion Principle**: high-level modules (business rules) should not depend on low-level modules (infrastructure); both should depend on abstractions.

**Any real world thing that the domain interacts with is called an actor**. That could be a test case, a human user or a single-page app. There are two types of actors:

- **Driving** (primary) **actors** – they **use the domain** to achieve a goal; e.g. a test case or a human user
- **Driven** (secondary) **actors** – they **provide functionality** needed by the domain to achieve a goal

![[Pasted image 20250501152850.png]]

How they interact with our application happens will determine the way we define the contracts the application sets for them(**ports**).

##  The ports

> **Ports are interfaces defined by the application core** to describe how it communicates with the outside world — either to receive input (driving ports) or to request something (driven ports).

In Hexagonal Architecture, **ports are abstractions** that separate the business logic from external actors (like databases, UIs, APIs, etc.). They form the **application’s boundary** — everything beyond a port is considered infrastructure.

There are two main types of ports:

### ✅ Driving Ports

- Represent **entry points** into the application.
    
- Defined by the application to describe how external actors (users, UIs, tests) can invoke use cases.
    
- Example: `CreateOrderUseCase`, `TransferFunds`, etc.
    

### ✅ Driven Ports

- Represent **outgoing dependencies** the application needs to fulfill a use case.
    
- Defined as interfaces inside the application, to be implemented by infrastructure (e.g., database access, notification services, etc.).
    
- Example: `OrderRepository`, `EmailSender`, `PaymentGateway`.
    

> 🧠 Think of ports as contracts: they say what the application expects (driven) or offers (driving), without saying how it is implemented.

This abstraction allows the application to be **flexibly wired** with different implementations (called **adapters**) — like using a mock database in tests or switching from REST to messaging.

![[Pasted image 20250501154102.png]]

## Adapters

> **Adapters are the components that implement or use the ports**, enabling communication between the application core and the external world.

In Hexagonal Architecture, **adapters are the glue** between the application and its environment. They live **outside the hexagon**, and they **convert external input/output** into something the core application understands — and vice versa.

There are two main kinds of adapters, corresponding to the two types of ports:

### ✅ Driving Adapters

- **Initiate interaction** with the application by calling driving ports.
    
- Examples:
    
    - A REST controller calling a use case
        
    - A command-line script triggering a batch process
        
    - A scheduled job
        

### ✅ Driven Adapters

- **Provide implementations** for driven ports (the application’s outgoing dependencies).
    
- Examples:
    
    - A database repository implementing `UserRepository`
        
    - An SMTP service sending emails
        
    - An HTTP client calling an external API
        

> Adapters are **replaceable** — you can swap a web UI for a CLI, or a SQL DB for a NoSQL one, without touching your core business logic.

#### ✨ Why Adapters Matter

- They **keep infrastructure details** out of your domain model.
    
- They **enable testability** — e.g., you can inject a fake adapter for testing.
    
- They **support flexibility** — you can add new technologies or integration mechanisms without changing your core application.
    

![[Pasted image 20250501154704.png]]

# Project Structure

Here is the **combined project structure and explanation** based on your two provided screenshots — this is a full representation of a **Hexagonal Architecture** project (specifically, the ``BuckPal`` example commonly used to illustrate clean hexagonal design in Java with Spring Boot).

---
![[Pasted image 20250501160113.png]]

--- 


```
📦 src
 └── 📁 main
     └── 📁 java
         └── 📁 io.reflectoring.buckpal
             ├── 📁 adapter
             │   ├── 📁 in.web
             │   │   └── 📄 SendMoneyController
             │   └── 📁 out.persistence
             │       ├── 📄 AccountJpaEntity
             │       ├── 📄 AccountMapper
             │       ├── 📄 AccountPersistenceAdapter
             │       ├── 📄 ActivityJpaEntity
             │       ├── 📄 ActivityRepository
             │       ├── 📄 NoOpAccountLock
             │       └── 📄 SpringDataAccountRepository

             ├── 📁 application
             │   ├── 📁 domain
             │   │   ├── 📁 model
             │   │   │   ├── 📄 Account
             │   │   │   ├── 📄 Activity
             │   │   │   ├── 📄 ActivityWindow
             │   │   │   └── 📄 Money
             │   │   └── 📁 service
             │   │       ├── 📄 GetAccountBalanceService
             │   │       ├── 📄 MoneyTransferProperties
             │   │       ├── 📄 SendMoneyService
             │   │       └── ⚡ ThresholdExceededException
             │   └── 📁 port
             │       ├── 📁 in
             │       │   ├── 📄 GetAccountBalanceUseCase
             │       │   ├── 🟣 PositiveMoney (Annotation)
             │       │   ├── 📄 PositiveMoneyValidator
             │       │   ├── 🟡 SendMoneyCommand (DTO/Request)
             │       │   └── 📄 SendMoneyUseCase
             │       └── 📁 out
             │           ├── 📄 AccountLock
             │           ├── 📄 LoadAccountPort
             │           └── 📄 UpdateAccountStatePort

             ├── 📁 common
             │   └── 📁 validation
             │       └── 📄 Validation
             │
             ├── 📄 BuckPalApplication                # Main Spring Boot app
             ├── 📄 BuckPalConfiguration              # App config
             ├── 📄 BuckPalConfigurationProperties    # Externalized settings

             ├── 🟣 PersistenceAdapter (Custom annotation)
             ├── 📄 UseCase (Annotation)
             └── 🟣 WebAdapter (Custom annotation)

 📦 test
 📂 resources
```

---

### 💡 Hexagonal Breakdown

|Component|Role|
|---|---|
|`adapter.in.web`|📥 Driving Adapter (e.g., controllers calling use cases)|
|`adapter.out.persistence`|📤 Driven Adapters (e.g., JPA Repositories)|
|`port.in`|✅ Use Case interfaces (e.g., `SendMoneyUseCase`)|
|`port.out`|✅ External interface contracts (e.g., `LoadAccountPort`)|
|`domain.model`|🧠 Entities and value objects (e.g., `Account`, `Money`)|
|`domain.service`|🧠 Application or domain services (e.g., `SendMoneyService`)|
|`common.validation`|✅ Cross-cutting concerns (e.g., custom validation)|
|`BuckPalApplication`|🏁 Entry point (Spring Boot main class)|

---

### 📐 Design Highlights

- **Driving Adapters** (input): UI, API controllers call `port.in` (use cases).
    
- **Application Core**: Contains the domain logic and use case contracts.
    
- **Driven Adapters** (output): Implement `port.out` to handle persistence, messaging, etc.
    
- **Isolation**: Business logic is free from frameworks or infrastructure dependencies.
    
- **Annotations** like `@WebAdapter`, `@PersistenceAdapter`, and `@UseCase` help mark roles clearly (optional but helpful for code clarity or DI configuration).
    

---

```
📦 banking-application
 ├── 📁 account-management
 │   ├── 📁 src/main/java/com/bankapp/account
 │   │   ├── 📁 adapter
 │   │   │   ├── 📁 in
 │   │   │   │   ├── 📁 web
 │   │   │   │   │   ├── 📄 AccountController
 │   │   │   │   │   ├── 📄 AccountCreationRequest
 │   │   │   │   │   ├── 📄 AccountResponse
 │   │   │   │   │   └── 📄 AccountExceptionHandler
 │   │   │   │   └── 📁 batch
 │   │   │   │       └── 📄 AccountImportJob
 │   │   │   └── 📁 out
 │   │   │       ├── 📁 persistence
 │   │   │       │   ├── 📄 AccountEntity
 │   │   │       │   ├── 📄 AccountMapper
 │   │   │       │   ├── 📄 AccountPersistenceAdapter
 │   │   │       │   └── 📄 SpringDataAccountRepository
 │   │   │       └── 📁 notification
 │   │   │           └── 📄 AccountNotificationAdapter
 │   │   ├── 📁 application
 │   │   │   ├── 📁 domain
 │   │   │   │   ├── 📁 model
 │   │   │   │   │   ├── 📄 Account
 │   │   │   │   │   ├── 📄 AccountId
 │   │   │   │   │   ├── 📄 AccountStatus
 │   │   │   │   │   └── 📄 AccountType
 │   │   │   │   └── 📁 service
 │   │   │   │       ├── 📄 AccountService
 │   │   │   │       └── 📄 AccountStatusCalculator
 │   │   │   └── 📁 port
 │   │   │       ├── 📁 in
 │   │   │       │   ├── 📄 CreateAccountUseCase
 │   │   │       │   ├── 📄 GetAccountDetailsUseCase
 │   │   │       │   ├── 📄 CloseAccountUseCase
 │   │   │       │   └── 📄 CreateAccountCommand
 │   │   │       └── 📁 out
 │   │   │           ├── 📄 LoadAccountPort
 │   │   │           ├── 📄 SaveAccountPort
 │   │   │           └── 📄 SendAccountNotificationPort
 │   │   └── 📁 config
 │   │       └── 📄 AccountModuleConfiguration
 │   └── 📁 build.gradle
 │
 ├── 📁 transaction-processing
 │   ├── 📁 src/main/java/com/bankapp/transaction
 │   │   ├── 📁 adapter
 │   │   │   ├── 📁 in
 │   │   │   │   ├── 📁 web
 │   │   │   │   │   ├── 📄 TransactionController
 │   │   │   │   │   ├── 📄 TransferRequest
 │   │   │   │   │   └── 📄 TransactionResponse
 │   │   │   │   └── 📁 messaging
 │   │   │   │       └── 📄 PaymentMessageListener
 │   │   │   └── 📁 out
 │   │   │       ├── 📁 persistence
 │   │   │       │   ├── 📄 TransactionEntity
 │   │   │       │   ├── 📄 TransactionMapper
 │   │   │       │   ├── 📄 TransactionPersistenceAdapter
 │   │   │       │   └── 📄 SpringDataTransactionRepository
 │   │   │       ├── 📁 accountclient
 │   │   │       │   └── 📄 AccountServiceAdapter
 │   │   │       └── 📁 messaging
 │   │   │           └── 📄 TransactionEventPublisher
 │   │   ├── 📁 application
 │   │   │   ├── 📁 domain
 │   │   │   │   ├── 📁 model
 │   │   │   │   │   ├── 📄 Transaction
 │   │   │   │   │   ├── 📄 TransactionId
 │   │   │   │   │   ├── 📄 TransactionType
 │   │   │   │   │   └── 📄 Money
 │   │   │   │   └── 📁 service
 │   │   │   │       ├── 📄 MoneyTransferService
 │   │   │   │       ├── 📄 TransactionValidationService
 │   │   │   │       └── 📄 TransactionLimitsService
 │   │   │   └── 📁 port
 │   │   │       ├── 📁 in
 │   │   │       │   ├── 📄 SendMoneyUseCase
 │   │   │       │   ├── 📄 GetTransactionHistoryUseCase
 │   │   │       │   └── 📄 SendMoneyCommand
 │   │   │       └── 📁 out
 │   │   │           ├── 📄 LoadTransactionPort
 │   │   │           ├── 📄 SaveTransactionPort
 │   │   │           ├── 📄 LoadAccountDetailsPort
 │   │   │           └── 📄 PublishTransactionEventPort
 │   │   └── 📁 config
 │   │       └── 📄 TransactionModuleConfiguration
 │   └── 📁 build.gradle
 │
 ├── 📁 customer-service
 │   ├── 📁 src/main/java/com/bankapp/customer
 │   │   ├── 📁 adapter
 │   │   │   ├── 📁 in
 │   │   │   │   ├── 📁 web
 │   │   │   │   │   ├── 📄 CustomerController
 │   │   │   │   │   └── 📄 CustomerProfileResponse
 │   │   │   │   └── 📁 graphql
 │   │   │   │       └── 📄 CustomerGraphQLResolver
 │   │   │   └── 📁 out
 │   │   │       ├── 📁 persistence
 │   │   │       │   ├── 📄 CustomerEntity
 │   │   │       │   ├── 📄 CustomerMapper
 │   │   │       │   └── 📄 CustomerPersistenceAdapter
 │   │   │       └── 📁 kyc
 │   │   │           └── 📄 KycServiceAdapter
 │   │   ├── 📁 application
 │   │   │   ├── 📁 domain
 │   │   │   │   ├── 📁 model
 │   │   │   │   │   ├── 📄 Customer
 │   │   │   │   │   ├── 📄 CustomerId
 │   │   │   │   │   └── 📄 CustomerProfile
 │   │   │   │   └── 📁 service
 │   │   │   │       ├── 📄 CustomerService
 │   │   │   │       └── 📄 CustomerVerificationService
 │   │   │   └── 📁 port
 │   │   │       ├── 📁 in
 │   │   │       │   ├── 📄 RegisterCustomerUseCase
 │   │   │       │   ├── 📄 GetCustomerProfileUseCase
 │   │   │       │   └── 📄 UpdateCustomerCommand
 │   │   │       └── 📁 out
 │   │   │           ├── 📄 LoadCustomerPort
 │   │   │           ├── 📄 SaveCustomerPort
 │   │   │           └── 📄 VerifyCustomerIdentityPort
 │   │   └── 📁 config
 │   │       └── 📄 CustomerModuleConfiguration
 │   └── 📁 build.gradle
 │
 ├── 📁 security
 │   ├── 📁 src/main/java/com/bankapp/security
 │   │   ├── 📁 adapter
 │   │   │   ├── 📁 in
 │   │   │   │   └── 📁 web
 │   │   │   │       ├── 📄 AuthController
 │   │   │   │       └── 📄 LoginRequest
 │   │   │   └── 📁 out
 │   │   │       ├── 📁 persistence
 │   │   │       │   ├── 📄 UserEntity
 │   │   │       │   └── 📄 UserPersistenceAdapter
 │   │   │       └── 📁 jwt
 │   │   │           └── 📄 JwtTokenProvider
 │   │   ├── 📁 application
 │   │   │   ├── 📁 domain
 │   │   │   │   ├── 📁 model
 │   │   │   │   │   ├── 📄 User
 │   │   │   │   │   ├── 📄 Role
 │   │   │   │   │   └── 📄 Permission
 │   │   │   │   └── 📁 service
 │   │   │   │       └── 📄 AuthenticationService
 │   │   │   └── 📁 port
 │   │   │       ├── 📁 in
 │   │   │       │   ├── 📄 AuthenticateUserUseCase
 │   │   │       │   └── 📄 LoginCommand
 │   │   │       └── 📁 out
 │   │   │           ├── 📄 LoadUserPort
 │   │   │           └── 📄 GenerateTokenPort
 │   │   └── 📁 config
 │   │       ├── 📄 SecurityConfiguration
 │   │       └── 📄 WebSecurityConfig
 │   └── 📁 build.gradle
 │
 ├── 📁 common
 │   ├── 📁 src/main/java/com/bankapp/common
 │   │   ├── 📁 validation
 │   │   │   └── 📄 ValidationUtils
 │   │   ├── 📁 annotation
 │   │   │   ├── 📄 UseCase
 │   │   │   ├── 📄 WebAdapter
 │   │   │   └── 📄 PersistenceAdapter
 │   │   ├── 📁 domain
 │   │   │   ├── 📄 Money
 │   │   │   ├── 📄 Email
 │   │   │   └── 📄 PhoneNumber
 │   │   ├── 📁 exception
 │   │   │   ├── 📄 BusinessException
 │   │   │   └── 📄 ResourceNotFoundException
 │   │   └── 📁 util
 │   │       └── 📄 DateUtils
 │   └── 📁 build.gradle
 │
 ├── 📁 api
 │   ├── 📁 src/main/java/com/bankapp/api
 │   │   ├── 📁 rest
 │   │   │   ├── 📄 ApiErrorResponse
 │   │   │   └── 📄 ApiConstants
 │   │   └── 📁 dto
 │   │       ├── 📄 AccountDto
 │   │       ├── 📄 CustomerDto
 │   │       └── 📄 TransactionDto
 │   └── 📁 build.gradle
 │
 ├── 📁 infrastructure
 │   ├── 📁 src/main/java/com/bankapp/infrastructure
 │   │   ├── 📁 config
 │   │   │   ├── 📄 DatabaseConfig
 │   │   │   └── 📄 MessageBrokerConfig
 │   │   ├── 📁 monitoring
 │   │   │   ├── 📄 MetricsConfig
 │   │   │   └── 📄 LoggingAspect
 │   │   └── 📁 cache
 │   │       └── 📄 CacheConfig
 │   └── 📁 build.gradle
 │
 ├── 📁 app
 │   ├── 📁 src/main/java/com/bankapp
 │   │   ├── 📄 BankingApplication
 │   │   └── 📄 ApplicationConfig
 │   ├── 📁 src/main/resources
 │   │   ├── 📄 application.yml
 │   │   ├── 📄 application-dev.yml
 │   │   └── 📄 application-prod.yml
 │   └── 📁 build.gradle
 │
 ├── 📁 build.gradle
 ├── 📁 settings.gradle
 └── 📁 docker-compose.yml
```

--- 

# Hexagonal Architecture Skeleton Pattern

## Key Repeating Patterns

Below is the essential skeleton structure that repeats across all modules in a hexagonal architecture. This pattern forms the foundation of each bounded context in the application.

```
📦 [module-name]
 └── 📁 src/main/java/com/example/[module]
     ├── 📁 adapter
     │   ├── 📁 in
     │   │   ├── 📁 web
     │   │   │   ├── 📄 [Entity]Controller
     │   │   │   ├── 📄 [Action]Request
     │   │   │   ├── 📄 [Entity]Response
     │   │   │   └── 📄 [Entity]ExceptionHandler
     │   │   └── 📁 [other-in-adapter] (messaging, batch, etc.)
     │   │       └── 📄 [Entity][AdapterType]
     │   └── 📁 out
     │       ├── 📁 persistence
     │       │   ├── 📄 [Entity]Entity
     │       │   ├── 📄 [Entity]Mapper
     │       │   ├── 📄 [Entity]PersistenceAdapter
     │       │   └── 📄 SpringData[Entity]Repository
     │       └── 📁 [other-out-adapter] (clients, messaging, etc.)
     │           └── 📄 [Entity][OutAdapter]
     ├── 📁 application
     │   ├── 📁 domain
     │   │   ├── 📁 model
     │   │   │   ├── 📄 [Entity]
     │   │   │   ├── 📄 [Entity]Id
     │   │   │   └── 📄 [Other value objects]
     │   │   └── 📁 service
     │   │       ├── 📄 [Entity]Service
     │   │       └── 📄 [Specific domain service]
     │   └── 📁 port
     │       ├── 📁 in
     │       │   ├── 📄 [Action][Entity]UseCase
     │       │   └── 📄 [Action][Entity]Command
     │       └── 📁 out
     │           ├── 📄 Load[Entity]Port
     │           └── 📄 Save[Entity]Port
     └── 📁 config
         └── 📄 [Module]Configuration
```

## Standard Components By Layer

### 1. Adapter Layer

#### Inbound Adapters (`adapter.in.*`)

**Purpose**: Convert external requests into application use case calls

|Component|Purpose|Example|
|---|---|---|
|*Controller|Handle HTTP requests|`AccountController`|
|*Request|Request DTO/payload|`CreateAccountRequest`|
|*Response|Response DTO|`AccountResponse`|
|*Listener|Message consumers|`PaymentMessageListener`|

#### Outbound Adapters (`adapter.out.*`)

**Purpose**: Implement outbound ports to external systems

|Component|Purpose|Example|
|---|---|---|
|*Entity|JPA/ORM entity|`AccountEntity`|
|*Mapper|Map domain <-> persistence|`AccountMapper`|
|*PersistenceAdapter|Implement repository port|`AccountPersistenceAdapter`|
|SpringData*Repository|Spring Data repository|`SpringDataAccountRepository`|
|*Client/*Adapter|External service clients|`PaymentGatewayAdapter`|

### 2. Application Layer

#### Domain Model (`application.domain.model`)

**Purpose**: Core business entities and logic

|Component|Purpose|Example|
|---|---|---|
|[Entity]|Domain entity|`Account`|
|[Entity]Id|Entity identifier|`AccountId`|
|[Value Objects]|Domain value objects|`Money`, `Email`|

#### Domain Services (`application.domain.service`)

**Purpose**: Core business operations

|Component|Purpose|Example|
|---|---|---|
|[Entity]Service|Primary domain logic|`AccountService`|
|[Specific]Service|Specialized domain logic|`InterestCalculationService`|

#### Inbound Ports (`application.port.in`)

**Purpose**: Define application entry points

|Component|Purpose|Example|
|---|---|---|
|[Action][Entity]UseCase|Use case interface|`CreateAccountUseCase`|
|[Action][Entity]Command|Command/parameter object|`CreateAccountCommand`|

#### Outbound Ports (`application.port.out`)

**Purpose**: Define external dependencies

|Component|Purpose|Example|
|---|---|---|
|Load[Entity]Port|Read data interface|`LoadAccountPort`|
|Save[Entity]Port|Write data interface|`SaveAccountPort`|
|[Action][Entity]Port|Other external operations|`NotifyCustomerPort`|

### 3. Configuration (`config`)

**Purpose**: Module-specific configuration

|Component|Purpose|Example|
|---|---|---|
|[Module]Configuration|Spring configuration|`AccountModuleConfiguration`|

## Common Cross-Module Classes

These components are typically shared across modules in a separate `common` module:

```
📦 common
 └── 📁 src/main/java/com/example/common
     ├── 📁 annotation
     │   ├── 📄 UseCase
     │   ├── 📄 WebAdapter
     │   └── 📄 PersistenceAdapter
     ├── 📁 domain
     │   └── 📄 [Shared value objects]
     ├── 📁 exception
     │   ├── 📄 BusinessException
     │   └── 📄 ResourceNotFoundException
     └── 📁 validation
         └── 📄 ValidationUtils
```

## Implementation Notes

1. **Dependency Flow**: All dependencies point inward (toward domain)
2. **Domain Purity**: Domain module has no external dependencies
3. **Interface Segregation**: Ports are specific to use cases
4. **Adapter Isolation**: Adapters only depend on ports, not other adapters
5. **Port Naming**: Ports are named after business capabilities, not technical details

