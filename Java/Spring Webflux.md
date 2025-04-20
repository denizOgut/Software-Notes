
Spring WebFlux is a reactive web framework in the Spring ecosystem, designed to support asynchronous, non-blocking, and event-driven programming using reactive streams. It is built on **Project Reactor** and can handle large numbers of concurrent requests with less resource consumption than traditional blocking models like **Spring MVC**.

#  Key Components of Spring WebFlux

**Reactive WebClient:** Spring WebFlux provides a non-blocking WebClient that allows you to perform HTTP requests to external services asynchronously. This is especially beneficial when integrating with other reactive systems.

**Reactive Controllers:** WebFlux offers the ``@RestController`` and ``@RequestMapping`` annotations to create reactive RESTful APIs. These controllers can handle requests in a non-blocking manner, making them ideal for high-performance applications.

**Reactive Data Repositories:** Spring Data supports reactive repositories, allowing developers to interact with databases asynchronously. This ensures that database interactions do not block the application’s event loop.
# Programming models

Spring WebFlux provides a two programming models. We will be discussing each of them in the subsequent articles in details.

- **[Annotation-based Controllers](https://jstobigdata.com/spring/getting-started-with-spring-webflux/#4_annotationbased_reactive_rest_endpoint):** You can use the same annotations from the spring-web module. Both Spring MVC and WebFlux controllers support reactive (Reactor and RxJava) return types, and, as a result, it is not easy to tell them apart. One notable difference is that WebFlux also supports reactive `@RequestBody` arguments.

- **[Functional Endpoints](https://jstobigdata.com/spring/a-functional-endpoint-in-spring-webflux/)**: You can use the Lambda-based, lightweight, and functional programming model. You can think of this as a small library or a set of utilities that an application can use to route and handle requests. The big difference with annotated controllers is that the application is in charge of request handling from start to finish versus declaring intent through annotations and being called back.

# Spring WebFlux or Spring MVC

![[Pasted image 20240918115857.png]]

- **The main difference between the two frameworks** is that requests to Spring MVC use a single thread whereas Spring WebFlux is fully non-blocking e.g. if the application makes a blocking call, the thread will not wait and can be used for processing other requests.
- If you predict that your application will need to **scale with high loads, consider using WebFlux**.
- It’s a good idea to start by checking the dependencies of your project. For applications that use **blocking persistence APIs or networking APIs, WebMVC** is a sound choice.
- For smaller applications where there is **a need for transparency and control but requirements aren’t as complex, Spring WebFlux** functional web endpoints are a good option.
- The same stands for microservices, but in this case, you may also decide to **combine Spring Web MVC and Spring WebFlux controllers**.

# Spring Data R2DBC

R2DBC stands for `Reactive Relational Database Connectivity` and is intended to provide a way to work with SQL databases using a fully reactive, non-blocking API. It is based on the Reactive Streams specification and is primarily an SPI (Service Provider Interface) for database driver implementers and client library authors — meaning it is not intended to be used directly in application code.


This is not a full ORM like JPA — it does not offer features such as caching or lazy loading. But it does provide object mapping functionality and a Repository abstraction.

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-r2dbc</artifactId>
        </dependency>

        <dependency>
            <groupId>io.r2dbc</groupId>
            <artifactId>r2dbc-postgresql</artifactId>
            <scope>runtime</scope>
        </dependency>
        ...
</dependencies>
```

```properties
spring.r2dbc.url=r2dbc:postgresql://localhost/studentdb
spring.r2dbc.username=user
spring.r2dbc.password=secret
```

```java
import io.r2dbc.spi.ConnectionFactories;
import io.r2dbc.spi.ConnectionFactory;
import io.r2dbc.spi.ConnectionFactoryOptions;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import static io.r2dbc.spi.ConnectionFactoryOptions.*;

@Configuration
public class R2DBCConfig {

    @Bean
    public ConnectionFactory connectionFactory() {
        return ConnectionFactories.get(
                ConnectionFactoryOptions.builder()
                        .option(DRIVER, "postgresql")
                        .option(HOST, "localhost")
                        .option(USER, "user")
                        .option(PASSWORD, "secret")
                        .option(DATABASE, "studentdb")
                        .build());
    }

}
```

```java
public interface StudentRepository extends ReactiveCrudRepository<Student, Long> {

    public Flux<Student> findByName(String name);

}
```

Besides the `ReactiveCrudRepository`, there is also an extension called [ReactiveSortingRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/reactive/ReactiveSortingRepository.html) which provides additional methods to retrieve entities sorted.

# Reactive Crud API

### Technologies & Concepts Used:
- **Entity**: `Book`
- **DTO**: `BookDto`
- **Repository**: `ReactiveCrudRepository` for non-blocking DB operations.
- **Mapper**: Map `Book` to `BookDto` and vice-versa.
- **Service**: Business logic layer.
- **Controller**: REST controller for handling API endpoints.
- **Error Handling**: Custom error handler for 4xx errors.
- **Pagination**: Handling paginated results.
- **``WebTestClient``**: Reactive testing.
- **``RestClient``**: REST client for external communication.
  
---

## 1. **Entity Class (Book)**
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Document(collection = "books")  // For MongoDB, use @Entity for relational DB.
public class Book {
    @Id
    private String id;
    private String title;
    private String author;
    private Double price;
}
```

## 2. **DTO Class (BookDto)**
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class BookDto {
    private String id;
    private String title;
    private String author;
    private Double price;
}
```

## 3. **Mapper Class**
You can use **`MapStruct`** for automatic mapping or write custom mapping.

```java
@Component
public class BookMapper {

    public BookDto toDto(Book book) {
        return new BookDto(book.getId(), book.getTitle(), book.getAuthor(), book.getPrice());
    }

    public Book toEntity(BookDto bookDto) {
        return new Book(bookDto.getId(), bookDto.getTitle(), bookDto.getAuthor(), bookDto.getPrice());
    }
}
```

## 4. **Repository Interface**
This repository interface extends **ReactiveCrudRepository**, providing CRUD methods in a reactive manner.

```java
@Repository
public interface BookRepository extends ReactiveCrudRepository<Book, String> {
    Flux<Book> findAllBy(Pageable pageable);  // For paginated results
}
```

## 5. **Configuration Class**
Here we configure any necessary beans like `R2dbcEntityTemplate` or MongoDB support.

```java
@Configuration
public class BookConfig {
    // Example for R2DBC configuration
    @Bean
    public ConnectionFactory connectionFactory() {
        return ConnectionFactories.get("r2dbc:postgresql://localhost:5432/bookdb");
    }

    @Bean
    public R2dbcEntityTemplate r2dbcEntityTemplate(ConnectionFactory connectionFactory) {
        return new R2dbcEntityTemplate(connectionFactory);
    }
}
```

## 6. **Service Layer**
Business logic resides here. You can also handle custom business validation or transformation.

```java
@Service
public class BookService {

    private final BookRepository bookRepository;
    private final BookMapper bookMapper;

    public BookService(BookRepository bookRepository, BookMapper bookMapper) {
        this.bookRepository = bookRepository;
        this.bookMapper = bookMapper;
    }

    public Mono<BookDto> createBook(BookDto bookDto) {
        Book book = bookMapper.toEntity(bookDto);
        return bookRepository.save(book).map(bookMapper::toDto);
    }

    public Flux<BookDto> getAllBooks(Pageable pageable) {
        return bookRepository.findAllBy(pageable)
                .map(bookMapper::toDto);
    }

    public Mono<BookDto> getBookById(String id) {
        return bookRepository.findById(id)
                .map(bookMapper::toDto)
                .switchIfEmpty(Mono.error(new BookNotFoundException("Book not found")));
    }

    public Mono<Void> deleteBook(String id) {
        return bookRepository.findById(id)
                .switchIfEmpty(Mono.error(new BookNotFoundException("Book not found")))
                .flatMap(book -> bookRepository.delete(book));
    }
}
```

## 7. **Controller Layer**
This layer handles HTTP requests and responses.

```java
@RestController
@RequestMapping("/api/books")
public class BookController {

    private final BookService bookService;

    public BookController(BookService bookService) {
        this.bookService = bookService;
    }

    @PostMapping
    public Mono<ResponseEntity<BookDto>> createBook(@RequestBody BookDto bookDto) {
        return bookService.createBook(bookDto)
                .map(createdBook -> ResponseEntity.status(HttpStatus.CREATED).body(createdBook));
    }

    @GetMapping
    public Flux<BookDto> getAllBooks(@RequestParam(defaultValue = "0") int page,
                                     @RequestParam(defaultValue = "10") int size) {
        Pageable pageable = PageRequest.of(page, size);
        return bookService.getAllBooks(pageable);
    }

    @GetMapping("/{id}")
    public Mono<ResponseEntity<BookDto>> getBookById(@PathVariable String id) {
        return bookService.getBookById(id)
                .map(ResponseEntity::ok)
                .onErrorResume(BookNotFoundException.class,
                        e -> Mono.just(ResponseEntity.status(HttpStatus.NOT_FOUND).build()));
    }

    @DeleteMapping("/{id}")
    public Mono<ResponseEntity<Void>> deleteBook(@PathVariable String id) {
        return bookService.deleteBook(id)
                .then(Mono.just(ResponseEntity.noContent().build()))
                .onErrorResume(BookNotFoundException.class,
                        e -> Mono.just(ResponseEntity.status(HttpStatus.NOT_FOUND).build()));
    }
}
```

## 8. **Error Handling**
Handle 4xx errors (e.g., book not found) with custom exceptions.

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class BookNotFoundException extends RuntimeException {
    public BookNotFoundException(String message) {
        super(message);
    }
}
```

## 9. **Paginated Results**
We use Spring Data `Pageable` for handling pagination. For relational databases, you can leverage `findAllBy(Pageable pageable)` in the repository.

## 10. **WebTestClient for Testing**
`WebTestClient` is used for testing reactive APIs.

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class BookControllerTest {

    @Autowired
    private WebTestClient webTestClient;

    @Test
    void testCreateBook() {
        BookDto bookDto = new BookDto(null, "Spring WebFlux", "John Doe", 39.99);

        webTestClient.post().uri("/api/books")
                .bodyValue(bookDto)
                .exchange()
                .expectStatus().isCreated()
                .expectBody(BookDto.class)
                .value(response -> assertNotNull(response.getId()));
    }

    @Test
    void testGetBookById() {
        String bookId = "book-123";

        webTestClient.get().uri("/api/books/{id}", bookId)
                .exchange()
                .expectStatus().isOk()
                .expectBody(BookDto.class)
                .value(response -> assertEquals(bookId, response.getId()));
    }
}
```

## 11. **Using RestClient (for external communication)**
If the service needs to communicate with another API, you can use **WebClient** (Spring’s non-blocking client).

```java
@Service
public class ExternalApiService {

    private final WebClient webClient;

    public ExternalApiService(WebClient.Builder webClientBuilder) {
        this.webClient = webClientBuilder.baseUrl("https://external-api.com").build();
    }

    public Mono<ExternalBookDto> getExternalBook(String bookId) {
        return webClient.get()
                .uri("/books/{id}", bookId)
                .retrieve()
                .bodyToMono(ExternalBookDto.class);
    }
}
```

### Conclusion:
This example demonstrates a **reactive CRUD API** with entity, DTO, repository, mapper, service, controller layers, and how to handle common features like error handling, pagination, and testing. By leveraging **Mono**, **Flux**, and reactive programming concepts in **Spring WebFlux**, the API is scalable and highly performant for concurrent requests.


# WebFilter Chain

Spring WebFlux supports two types of filters: `**WebFilters**` and `**HandlerFilterFunction**`_,_ which will handle web requests from HTTP clients.

## 1. WebFilter

WebFilter defines a contract for intercepting and processing web requests in a chained manner.

> A _WebFilter_ acts on a global level and applicable on annotation based WebFlux Controllers and the Functional Web framework style Routing Functions.

The `WebFilter` interface looks like the following.

```java
public interface WebFilter {  
  
   Mono<Void> filter(ServerWebExchange exchange, WebFilterChain chain);  
  
}
```

- The `filter` method accepts a `ServerWebExchange` where you can interact with the web request and raise cross-cutting concerns as you expected in the response.
- The `WebFilterChain` defines a chain of filters that are invoked in sequence. At the end of the chain, it invokes the actual controller or routing function.

### **WebFilter transforming Response**

Let us implement a `WebFilter` to add a new header to the response.

```java
@Component  
public class TranformResponseHeaderWebFilter implements WebFilter {  
   
    @Override  
    public Mono<Void> filter(ServerWebExchange exchange, WebFilterChain chain) {  
        exchange.getResponse().getHeaders().add("user-group", "ADMIN");  
        return chain.filter(exchange);  
    }  
}
```

## WebFilter transforming Request

Let us implement a `WebFilter` to add a new header to the request.

```java
@Component  
public class TranformRequestHeaderWebFilter implements WebFilter {  
   
    @Override  
    public Mono<Void> filter(ServerWebExchange exchange, WebFilterChain chain) {  
        exchange.getRequest().mutate().header("user-group", "USER");  
        return chain.filter(exchange);  
    }

}
```

Why can’t we directly transform the request headers map, unlike response headers?

> **It’s because the request headers map is read-only:**

## 2. ``HandlerFilterFunction``

In functional-style routing, a router function intercepts a request and invokes the desired handler function. Functional routing allows us to plugin zero or more `**HandlerFilterFunction**` instances, which can be applied before the `**HandlerFunction**`.

> **The WebFlux Filters of type `HandlerFilterFunctions` can be applied only to endpoints written in functional style.**

The `HandlerFilterFunction` interface looks like the following:

```JAVA
public interface HandlerFilterFunction<T extends ServerResponse, R extends ServerResponse> {  
  
   Mono<R> filter(ServerRequest request, HandlerFunction<T> next);  
  
  //other default & static methods  
}
```

- The `filter` method accepts a `ServerRequest` where you can interact with the web request and raise cross-cutting concerns as you expected in the response.
- The `HandlerFunction` represents the next entity in the chain and can be invoked to proceed to this entity or not invoked to block the chain.

## ``HandlerFilterFunction`` transforming Request

Let us implement a `HandlerFilterFunction` to add a new header to the request.

```java
public static HandlerFilterFunction<ServerResponse, ServerResponse> TransformRequestHeader() {  
    return (request, next) -> {  
        final ServerRequest serverRequest = ServerRequest.from(request)  
           .header("user-group", "FUNCTION-USER")  
           .build();  
        return next.handle(serverRequest);  
    };  
}
```


# Functional Endpoints

**functional endpoints** (also called **functional routing**) provide an alternative to the traditional **annotated controller-based approach** (`@RestController`). Instead of using annotations, you define the routing and handlers for each endpoint using functional constructs.

Functional endpoints offer a more **declarative and lightweight** approach, allowing greater control over the request and response flow. This approach can be more suitable for reactive programming because it aligns with functional and reactive paradigms.

![[Pasted image 20240918155751.png]]

An Http request initiated by a client app arrives at the Server (Netty/Undertow etc.). This request is forwarded to the **``RouterFunction``** to assign an appropriate **``HandlerFunction``** to serve the Http request. The ``RouterFunction`` is similar to `@RequestMapping` and the ``HandlerFunction`` is similar to the body of `@RequestMapping` method in the annotation-driven programming model.

## **Basic Components of Functional Endpoints**:

### a) **``RouterFunction``**:

- Defines the routing configuration. It maps incoming HTTP requests to appropriate handlers based on request details (e.g., URI, HTTP method).

### b) **``HandlerFunction``**:

- The function that handles the request and produces a response. It takes a `ServerRequest` as input and returns a `Mono<ServerResponse>`.

```java
@Component
public class UserHandler {

    private final UserService userService;

    public UserHandler(UserService userService) {
        this.userService = userService;
    }

    public Mono<ServerResponse> getUserById(ServerRequest request) {
        String userId = request.pathVariable("id");
        Mono<User> userMono = userService.getUserById(userId);

        return userMono
            .flatMap(user -> ServerResponse.ok().bodyValue(user))
            .switchIfEmpty(ServerResponse.notFound().build());
    }

    public Mono<ServerResponse> createUser(ServerRequest request) {
        Mono<User> userMono = request.bodyToMono(User.class);
        return userMono
            .flatMap(userService::createUser)
            .flatMap(user -> ServerResponse.ok().bodyValue(user));
    }
}
```

```java
@Configuration
public class UserRouter {

    @Bean
    public RouterFunction<ServerResponse> route(UserHandler handler) {
        return RouterFunctions.route()
            .GET("/users/{id}", handler::getUserById)
            .POST("/users", handler::createUser)
            .build();
    }
}
```

## **How It Works**:

- **Request Handling**: When a client makes a request (e.g., `GET /users/123`), Spring WebFlux matches it against the routes defined in the `RouterFunction`. If a match is found, the corresponding handler is invoked.
- **Reactive Flow**: Handlers return `Mono<ServerResponse>` or `Flux<ServerResponse>`, making it naturally reactive.
- **Custom Logic**: You can include custom logic (e.g., validation, filtering) directly in the handler or in custom middleware.

 **Handler Class:**

```java
@Component
public class ProductHandler {

    private final ProductService productService;

    public ProductHandler(ProductService productService) {
        this.productService = productService;
    }

    public Mono<ServerResponse> getAllProducts(ServerRequest request) {
        int page = Integer.parseInt(request.queryParam("page").orElse("0"));
        int size = Integer.parseInt(request.queryParam("size").orElse("10"));

        Flux<Product> products = productService.getAllProducts(page, size);
        return ServerResponse.ok().body(products, Product.class);
    }

    public Mono<ServerResponse> getProductById(ServerRequest request) {
        String productId = request.pathVariable("id");
        Mono<Product> product = productService.getProductById(productId);

        return product
            .flatMap(prod -> ServerResponse.ok().bodyValue(prod))
            .switchIfEmpty(ServerResponse.notFound().build());
    }

    public Mono<ServerResponse> createProduct(ServerRequest request) {
        Mono<Product> productMono = request.bodyToMono(Product.class);

        return productMono
            .flatMap(productService::createProduct)
            .flatMap(prod -> ServerResponse.status(HttpStatus.CREATED).bodyValue(prod))
            .onErrorResume(e -> ServerResponse.badRequest().bodyValue("Invalid product data"));
    }

    public Mono<ServerResponse> deleteProduct(ServerRequest request) {
        String productId = request.pathVariable("id");
        return productService.deleteProduct(productId)
            .then(ServerResponse.noContent().build())
            .onErrorResume(e -> ServerResponse.status(HttpStatus.INTERNAL_SERVER_ERROR).bodyValue("Failed to delete product"));
    }
}
```

**Router Class:**

```java
@Configuration
public class ProductRouter {

    @Bean
    public RouterFunction<ServerResponse> productRoutes(ProductHandler handler) {
        return RouterFunctions.route()
            .GET("/products", handler::getAllProducts)
            .GET("/products/{id}", handler::getProductById)
            .POST("/products", handler::createProduct)
            .DELETE("/products/{id}", handler::deleteProduct)
            .build();
    }
}
```

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class ProductHandlerTest {

    @Autowired
    private WebTestClient webTestClient;

    @Test
    void testGetProductById() {
        webTestClient.get().uri("/products/{id}", "123")
            .exchange()
            .expectStatus().isOk()
            .expectBody(Product.class)
            .value(product -> assertEquals("123", product.getId()));
    }

    @Test
    void testCreateProduct() {
        Product newProduct = new Product("456", "New Product", 29.99);

        webTestClient.post().uri("/products")
            .bodyValue(newProduct)
            .exchange()
            .expectStatus().isCreated()
            .expectBody(Product.class)
            .value(product -> assertEquals("New Product", product.getName()));
    }
}
```

- Functional endpoints in Spring WebFlux provide a flexible, declarative approach to defining API routes.
- `RouterFunction` maps routes to handler functions, and `HandlerFunction` processes the requests.
- You have full control over request processing with **Mono** and **Flux**, making it ideal for reactive programming.

# WebClient in Spring WebFlux

**`WebClient`** is a non-blocking, reactive HTTP client provided by Spring WebFlux. It is designed to handle asynchronous and reactive operations, making it suitable for high-performance applications that require non-blocking I/O operations.

## 1. **Non-Blocking Concurrent Requests**

**Non-blocking** means that operations can proceed without waiting for others to complete. This is crucial for high concurrency and efficiency in applications, especially when dealing with I/O-bound tasks like HTTP requests.

**Concurrent Requests** are handled efficiently using a non-blocking approach:

- **Asynchronous Processing**: WebClient issues requests asynchronously. When a request is made, it returns immediately with a `Mono` or `Flux`, which represents a future result. The application can continue processing other tasks while waiting for the response.
- **Event Loop**: WebClient relies on an event loop (or reactor) to handle multiple requests concurrently. Instead of blocking a thread while waiting for I/O operations, the event loop processes other tasks and handles responses when they are ready.

## 2. **How the Event Loop Works**

![[Pasted image 20240918161911.png]]

The **event loop** is a core concept in non-blocking I/O operations. It efficiently manages multiple I/O operations using a single or a few threads. Here's a simplified flow:

1. **Request Submission**: When a request is submitted, it is registered with the event loop.
2. **Non-Blocking I/O**: Instead of waiting for the I/O operation to complete, the thread returns to handle other tasks.
3. **Event Handling**: Once the I/O operation is complete (e.g., an HTTP response is received), the event loop triggers the appropriate callback or continuation.
4. **Response Handling**: The response is processed, and any associated callbacks are executed.

## 3. **URI Variables**

**URI variables** are placeholders in the URL that are replaced with actual values when making a request. WebClient allows you to specify these variables dynamically.

Example:
```java
String userId = "123";
webClient.get()
    .uri(uriBuilder -> uriBuilder.path("/users/{id}").build(userId))
    .retrieve()
    .bodyToMono(User.class)
    .subscribe(user -> System.out.println(user.getName()));
```

In this example, `{id}` is a URI variable that gets replaced with `userId` (`123`).

## 4. **Streaming GET**

**Streaming GET** requests involve processing large responses or data streams without loading the entire response into memory.

Example:
```java
webClient.get()
    .uri("/large-data-stream")
    .retrieve()
    .bodyToFlux(DataChunk.class)
    .subscribe(chunk -> {
        // Process each chunk of data
    });
```

Here, `bodyToFlux` is used to stream data chunks as they arrive.

## 5. **POST Requests**

For **POST** requests, you send data to the server, typically in the request body.

Example:
```java
User newUser = new User("John", "Doe");
webClient.post()
    .uri("/users")
    .bodyValue(newUser)
    .retrieve()
    .bodyToMono(User.class)
    .subscribe(user -> System.out.println("Created user: " + user.getName()));
```

## 6. **Body Publisher vs Body Value**

- **`bodyValue`**: This is used for simple cases where you send a single value (like an object) in the request body.

  ```java
  webClient.post()
      .uri("/users")
      .bodyValue(newUser)
      .retrieve()
      .bodyToMono(User.class);
  ```

- **`bodyPublisher`**: This is more flexible and allows you to send a stream of data or provide a custom publisher. This is useful for large datasets or complex streaming operations.

  ```java
  webClient.post()
      .uri("/upload")
      .body(BodyPublishers.fromFile(Paths.get("large-file.txt")))
      .retrieve()
      .bodyToMono(Void.class);
  ```

## 7. **Retrieve vs Exchange**

- **`retrieve()`**: A more straightforward method for making requests and handling responses. It is typically used for common use cases where you are only interested in the response body or status code.

  ```java
  webClient.get()
      .uri("/users")
      .retrieve()
      .bodyToMono(User.class);
  ```

- **`exchange()`**: Provides more control over the entire response, including status code, headers, and body. It is useful when you need to handle responses or errors more comprehensively.

  ```java
  webClient.get()
      .uri("/users")
      .exchange()
      .flatMap(response -> {
          if (response.statusCode().is2xxSuccessful()) {
              return response.bodyToMono(User.class);
          } else {
              return Mono.error(new RuntimeException("Failed request"));
          }
      });
  ```

## Summary

- **Non-Blocking Concurrent Requests**: WebClient uses a non-blocking approach to handle concurrent HTTP requests efficiently.
- **Event Loop**: Manages multiple I/O operations with minimal threads by using callbacks to handle responses asynchronously.
- **URI Variables**: Dynamically substitute placeholders in URLs.
- **Streaming GET**: Handles large data or continuous data streams without loading everything into memory.
- **POST Requests**: Sends data to the server in the request body.
- **Body Publisher vs Body Value**: `bodyValue` is for simple data, while `bodyPublisher` handles more complex streaming or custom publishers.
- **Retrieve vs Exchange**: `retrieve()` is simpler for common scenarios, whereas `exchange()` provides detailed control over the response.

Using WebClient in a reactive, non-blocking manner helps to build scalable and efficient applications that handle many concurrent operations with minimal resources.

XXX
# Server-Sent Events (SSE)

**Server-Sent Events (SSE)** is a standard for server-to-client streaming of updates over HTTP. It allows servers to push real-time data updates to the client through a single, long-lived connection. Unlike WebSockets, SSE is one-way (from server to client) and is built on top of the HTTP/1.1 protocol.

## 1. **How SSE Works**

- The client (typically a browser or a front-end service) establishes an HTTP connection to the server.
- The server keeps the connection open and continuously pushes updates as events.
- The client receives these events and processes them in real time.
  
SSE is commonly used for real-time data applications like stock tickers, social media updates, notifications, and dashboards.

## 2. **How to Use SSE in Spring WebFlux**

Spring WebFlux provides first-class support for SSE, and you can easily implement it in a reactive, non-blocking manner.

### Key Concepts:
- **Media Type**: The server uses the `text/event-stream` content type to communicate that the data stream is an SSE.
- **Event Streaming**: The server pushes a stream of data in the form of events.
- **Auto-Reconnect**: The browser automatically reconnects to the server if the connection is lost, which is a built-in feature of SSE.

## 3. **Basic Server-Sent Events Example**

### a) **Controller for SSE**

In Spring WebFlux, you can create a controller that pushes data to clients using a `Flux`. The controller should return a `Flux<ServerSentEvent<?>>` to continuously stream the data.

```java
@RestController
public class SSEController {

    @GetMapping(value = "/sse/stream", produces = MediaType.TEXT_EVENT_STREAM_VALUE)
    public Flux<ServerSentEvent<String>> streamEvents() {
        return Flux.interval(Duration.ofSeconds(1))
            .map(sequence -> ServerSentEvent.<String>builder()
                .id(String.valueOf(sequence))
                .event("periodic-event")
                .data("Event #" + sequence)
                .build());
    }
}
```

In this example:
- The `@GetMapping` endpoint is used to stream events.
- `Flux.interval(Duration.ofSeconds(1))` generates a stream of events every second.
- The `ServerSentEvent` object is used to wrap the data and send it to the client.

### b) **Client-Side JavaScript to Receive SSE**

On the client side (e.g., in the browser), you can listen for SSE updates using JavaScript:

```javascript
const eventSource = new EventSource('/sse/stream');

eventSource.onmessage = function(event) {
  console.log('New message: ', event.data);
};

eventSource.onerror = function(error) {
  console.error('Error occurred:', error);
};
```

- `EventSource` opens a persistent connection to the SSE endpoint (`/sse/stream`).
- `onmessage` receives the data whenever a new event is pushed from the server.

## 4. **Advanced SSE with Spring WebFlux**

### a) **SSE for Real-Time Notifications**

You can use SSE to send real-time notifications to clients. For example, if you are running a notification service, you could push updates to users in real time.

```java
@RestController
public class NotificationController {

    private final NotificationService notificationService;

    @GetMapping(value = "/notifications/stream", produces = MediaType.TEXT_EVENT_STREAM_VALUE)
    public Flux<ServerSentEvent<Notification>> streamNotifications() {
        return notificationService.getNotificationsStream()
            .map(notification -> ServerSentEvent.builder(notification)
                .event("notification")
                .build());
    }
}
```

In this case:
- `NotificationService` provides a stream of `Notification` objects (e.g., from a `Flux`).
- Each notification is wrapped in a `ServerSentEvent` and streamed to the client as soon as it becomes available.

### b) **Handling Errors and Reconnection in SSE**

SSE automatically handles reconnection attempts if the connection drops, but you may want to manage custom error handling on the server side.

```java
@GetMapping(value = "/sse/errors", produces = MediaType.TEXT_EVENT_STREAM_VALUE)
public Flux<ServerSentEvent<String>> streamWithErrorHandling() {
    return Flux.interval(Duration.ofSeconds(1))
        .map(sequence -> {
            if (sequence == 10) {
                throw new RuntimeException("Error occurred at event #" + sequence);
            }
            return ServerSentEvent.builder("Event #" + sequence).build();
        })
        .onErrorResume(e -> Flux.just(ServerSentEvent.builder("Error: " + e.getMessage()).build()));
}
```

- **`onErrorResume`**: Handles the error by sending an error event to the client and continuing the stream.
- The client can receive error messages, but the server doesn't break the entire stream.

## 5. **SSE vs. WebSockets**

| Feature            | **SSE (Server-Sent Events)**                  | **WebSockets**                                      |
|--------------------|-----------------------------------------------|----------------------------------------------------|
| **Direction**       | One-way: Server to client                     | Full-duplex (two-way communication)                |
| **Protocol**        | Built on top of HTTP/1.1                      | Separate protocol (ws:// or wss://)                |
| **Connection**      | Long-lived, event-based                       | Long-lived, full-duplex                            |
| **Reconnection**    | Automatically reconnects                      | Manual reconnection required                       |
| **Complexity**      | Simpler to implement                          | More complex, requires explicit handling of both sides |
| **Use Cases**       | Streaming notifications, live updates         | Chat applications, real-time collaborative apps    |

## 6. **Best Practices for SSE**

- **Connection Keep-Alive**: Make sure the server sends periodic keep-alive messages to ensure that the connection stays open, especially in cases where the stream may be idle for a while.
  
  Example:
  ```java
  return Flux.interval(Duration.ofSeconds(5))
      .map(sequence -> ServerSentEvent.builder("keep-alive").build());
  ```

- **Retry Strategy**: While SSE has a built-in retry mechanism, you can control the retry interval using the `retry` field in the `ServerSentEvent`.

  ```java
  return ServerSentEvent.<String>builder()
      .data("message")
      .id("1")
      .event("custom-event")
      .retry(Duration.ofSeconds(5).toMillis())
      .build();
  ```

- **Use Cases**: SSE is ideal for use cases where the client needs to receive real-time data updates from the server, such as:
  - Stock prices
  - Social media feeds
  - Notifications
  - Real-time monitoring dashboards

## 7. **Streaming Events with WebClient**

If you need to stream SSE from a client using WebClient in Spring WebFlux:

```java
WebClient webClient = WebClient.create();

Flux<ServerSentEvent<String>> eventStream = webClient.get()
    .uri("/sse/stream")
    .accept(MediaType.TEXT_EVENT_STREAM)
    .retrieve()
    .bodyToFlux(new ParameterizedTypeReference<ServerSentEvent<String>>() {});

eventStream.subscribe(event -> System.out.println("Received event: " + event.data()));
```

- This example demonstrates how to consume SSE from a WebClient and subscribe to the stream of events.

## 8. **Summary**

- **Server-Sent Events (SSE)** allows the server to push real-time updates to the client over a long-lived HTTP connection.
- SSE is simpler than WebSockets and provides automatic reconnection, making it ideal for one-way data streaming like notifications, social media updates, or stock prices.
- Spring WebFlux provides built-in support for SSE through the `ServerSentEvent` class, making it easy to stream events reactively with `Flux`.
- Error handling, reconnection, and client-side integration are straightforward and handled with minimal setup.
- SSE works well in use cases where only server-to-client communication is required, while WebSockets are more suitable for full-duplex communication.

