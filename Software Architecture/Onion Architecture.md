
This architecture is not appropriate for small websites.  It is appropriate for long-lived business applications as well as applications with complex behavior.  It emphasizes the use of interfaces for behavior contracts, and it forces the externalization of infrastructure.

The Onion Architecture , it builds on the Ports & Adapters Architecture by adhering to the idea of placing the domain in the center of the application, externalizing the delivery mechanisms (UI) and infrastructure used by the system (ORM, Search engines, 3rd party APIs, …). But it goes further and adds internal layers to it.

went from the Layered Architecture, with usually 4 layers (Presentation, Application, Domain, Persistence), to the Ports & Adapters Architecture which only implicitly mentions two concentric layers:

1. An external layer representing the delivery mechanisms and infrastructure;
2. An internal layer representing the business logic.

Both Ports & Adapters and Onion Architecture share the idea of isolating the application core from the infrastructure concerns by writing adapter code so that the infrastructure code does not leak into the application core. This makes it easier to replace both the tools and the delivery mechanisms used by the application, providing some protection against technology, tooling and vendor lockdown.

The Onion Architecture (2008) builds on concepts from Domain-Driven Design and Ports & Adapters Architecture, emphasizing multiple layers within business logic. It enforces a clear rule of dependency: **==outer layers depend on inner layers, but inner layers are unaware of outer ones==**, promoting a clean separation of concerns and maintainability.

> **==The fundamental rule is that all code can depend on layers more central, but code cannot depend on layers further out from the core.  In other words, all coupling is toward the center.==**

![[Pasted image 20250504135824.png]]


In Onion Architecture, the **Domain Model** is at the very center, representing the core business logic and being only coupled to itself. Surrounding it is the **application core**, which may include layers such as **repository interfaces** for data access. These interfaces remain in the core, while their implementations, often involving databases, reside in the **outer layers** like Infrastructure, UI, and Tests. These outer layers are more volatile and are intentionally isolated from the core. **All dependencies flow inward** — outer layers depend on inner ones, never the reverse — following the **Dependency Inversion Principle (DIP)** to ensure a clean, maintainable architecture.


In Onion Architecture, the **database is not at the center**—it is treated as an **external service**. This contrasts with traditional “database application” thinking. **==Instead of being central, the database is accessed through infrastructure code that implements interfaces defined in the application core. The application doesn’t depend directly on the database, file system, or other external resources. This decoupling reduces maintenance costs over time by isolating volatile components and protecting the core business logic from external changes.==**


==Infrastructure is any code that is a **commodity and does not give your application a competitive advantage**==.  This code is most likely to change frequently as the application goes through years of maintenance.

==The big difference is that any outer layer can directly call any inner layer. With traditionally layered architecture, a layer can only call the layer directly beneath it.  **This is one of the key points that makes Onion Architecture different from traditional layered architecture**.==  Infrastructure is pushed out to the edges where no business logic code couples to it.  The code that interacts with the database will implement interfaces in the application core.  The application core is coupled to those interfaces but not the actual data access code.  In this way, we can change code in any outer layer without affecting the application core.

![[Pasted image 20250504141844.png]]


Onion Architecture would look like when represented as a traditionally layered architecture. **==The big difference is that Data Access is a top layer along with UI, I/O, etc. Another key difference is that the layers above can use any layer beneath them, not just the layer immediately beneath. Also, business logic is coupled to the object model but not to infrastructure.==**

**Key tenets of Onion Architecture:**

- _The application is built around an independent object model_
- _Inner layers define interfaces.  Outer layers implement interfaces_
- _Direction of coupling is toward the center_
- _All application core code can be compiled and run separate from infrastructure_

