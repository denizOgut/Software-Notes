# Book Notes

## Honesty in small things not a small thing

In software, %80 or more of what we do is quaintly called "maintenance". You should name a variable using the same care with which you name a first-born child.

### 1. CLEAN CODE

If the discipline of requirements specification has taught us anything, it is that well-specified requirements are as formal as code and can act as executable tests of that code.

**LeBlanc's Law:** Later equals never.

#### What Is Clean Code For Some Software Engineer Gurus

- **Bjarne Stroustrup:**
  Clean code should be "elegant" and "efficient". The logic should be straightforward to make it hard for bugs to hide. Bad code tries to do too much; clean code is "focused".

- **Grady Booch:**
  Clean code is "simple" and "direct", focusing on "readability".

- **Big Dave Thomas:**
  Clean code makes it easy for other people to enhance it. Smaller is better.

- **Micheal Feathers:**
  Clean code always looks like it was written by someone who cares.

- **Ron Jeffries:**
  - Run all the tests.
  - Contains no duplication.
  - Expresses all the design ideas that are in the system.
  - Minimize the number of entities.

- **Ward Cunningham:**
  Beautiful code makes the language look like it was made for the problem.

The `@author` field of a Javadoc tells us who we are. The next time you write a line of code, remember you are an author, writing for readers who will judge your effort.

**Leave the campground cleaner than you found it.** Apply for code.

### 2. Meaningful Names

Names should reveal intent. Choosing good names takes time but saves more than it takes. The name of a variable, function, or class should answer all the big questions: "why it exists", "what it does", "how it is used".

```java
int d  // int daysOfCreation
if (x[0] == 4)  // if (cell[STATUS_VALUE] == FLAGGED) --> if (cell.isFlagged()) // Mine Swapper Game````
```

Do not refer to a grouping of accounts as an "accountList" unless it's actually a List. If the container holding the accounts is not actually a List, it may lead to false conclusions: `accounts`, `accountGroup`, `bunchOfAccounts`.

Beware of using names that vary in small ways, like `XYZControllerForEfficientHandlingOfStrings` vs. `XYZControllerForEfficientStorageOfStrings`.

Spelling similar concepts similarly is information. Using inconsistent spellings is disinformation.

If names must be different, then they should also mean something different.

Numbers-series naming is noninformative (e.g., a1, a2, .. aN).

```java
public static void copyChars(char a1[], char a2[])  // (char source[], char destination[])
```

Noise words are another meaningless distinction like "Info" and "Data" (e.g., `ProductData`, `ProductInfo`). Noise words are redundant. The word variable should never appear in a variable name (e.g., `Customer` and `CustomerObject`, which one is present: customer's payment history).

Distinguish names in such a way that the reader knows what the difference offers. If you can't pronounce it, you can't discuss it without sounding like an idiot.

Single-letter names and numeric constants have a particular problem as they are not easy to locate across a body of text (e.g., `7` vs. `MAX_CLASSES_PER_STUDENT`). Consider how much easier it will be to find `WORK_DAYS_OF_WEEK` than to find all the places where `5` was used and filter the list down to just the instances with intended meaning.

Single-letter names can ONLY be used as local variables inside short methods.

The preceding 'I', so common in today's legacy wads, is a distraction. So if either interface or implementation, choose the implementation, calling it `ShapeFactoryImp`.

Readers shouldn't have to mentally translate your names into other names they already know. This is a problem with single-letter variable names. A single-letter name is a poor choice; it's just a placeholder.

**Clarity is king.**

Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`, `Account`. A class name should not be a verb.

Methods should have verb or verb phrase names like `postPayment`, `readPage`.

When constructors are overloaded, use static factory methods with names that describe the arguments (e.g., `Complex fulcrumPoint = Complex.FromRealNumber(23.0)`). Consider enforcing their use by making the corresponding constructors private.

Choose clarity over entertainment value. Say what you mean. Mean what you say.

Pick one word for one abstract concept and stick with it. How do you remember which method name goes with which class? `fetch`, `retrieve`, and `get`.

Avoid using the same word for two purposes.

Our goal as authors is to make our code as easy as possible to understand. So use CS terms, algorithm names, pattern names, etc. It is not wise to draw every name from the problem domain. When there is no "programmer-eese" for what you are doing, use the name from the problem domain.

You can add context by using prefixes: `addrFirstName`, `addrLastName`, `addrState`. Readers'll understand that these variables are part of a larger structure -> Best way is the `Address` class.

Shorter names are generally better than longer ones, as long as they are clear. Add no more context to a name than is necessary.

The hardest thing about choosing good names is that it requires good descriptive skills and a shared cultural background.

### 3. Functions

The first rule of functions is that they should be small. The second rule of functions is that they should be smaller than that.

***FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.***

Describe the function by describing it as a brief "TO" paragraph.

**TO Paragraph:** "TO" paragraph is a type of documentation that explains the purpose of a function, what it does, and what it returns. This type of documentation is often written in a single sentence, and it is meant to provide a quick and easy-to-understand summary of the function's behavior. The goal is to make it easy for other developers to understand how a function works and how it can be used in their own code.

```java
public double calculateAverage(List<Integer> numberList) {
    //....
}
```

**TO: Calculate the average of a list of numbers and return the result.**

If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing.

Functions that do one thing cannot be reasonably divided into sections like "declarations", "initializations", and "sieve".

In order to make sure our functions are doing "one thing", we need to make sure that the statements within our function are all the same level of abstraction.

**The StepDown Rule:** We want to be able to read the program as though it were a set of "TO" paragraphs, each of which is describing the current level of abstraction and referencing subsequent "TO" paragraphs at the next level down.

**Switch Statements:** It is hard to make a small switch statement. It is also hard to make a switch statement that does one thing. The general rule for switch statements is that if they appear only once, are used to create polymorphic objects, and are hidden behind an inheritance relationship so that the rest of the system can't see them.

**Descriptive Names:** You know you are working on clean code when each routine turns out to be pretty much what you expected. The smaller and more focused a function is, the easier it is to choose a descriptive name. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment. Choosing a descriptive name will clarify the design of the module in your mind and help you to improve it. Be consistent in your names.

**Function Arguments:** The ideal number of arguments for a function is "ZERO (niladic)". Next comes "ONE (monadic)" followed closely by "TWO (dyadic)". "THREE (triadic)" arguments should be avoided where possible. "3+ (polyadic)" needs very special justification and shouldn't be used anywhere.

Arguments are hard. They take a lot of "conceptual power". Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. Output arguments are harder to understand than input arguments. We don't usually expect information to be going out through the arguments.

**Common Monadic Forms:** There are two very common reasons to pass a single argument into a function:

1. Asking a question about that argument (e.g., `boolean fileExist("MyFile")`).
2. Operating, transforming on that argument (e.g., `InputStream fileOpen("MyFile")`).

Choose names and contexts carefully.

**Flag Arguments:** Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice, proclaiming that this function does more than one thing. It does one thing if the flag is true and another if the flag is false.

**Dyadic Functions:** The parts we ignore are where bugs will hide. The two arguments have no natural ordering.

**Argument Objects:** When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own.

```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

When groups of variables are passed together, they are likely part of a concept that deserves a name of its own.

**Argument List:** If the variable arguments are all treated identically, then they are equivalent to a single argument of type List.

```java
public String format(String format, Object...args)
void monad(Integer...args)
```

**Have No Side Effects:** Side effects are lies. Your function promises to do one thing, but it also does other hidden things.

**Output Arguments:** In general, output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.

```java
public void appendFooter(s);
report.appendFooter();
```

**Command Query Separation:** Functions should either do something or answer something but not both.

**Extract Try-Catch Blocks:** Try/catch blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So it's better to extract the bodies of the try and catch blocks out into functions of their own.

**Error Handling Is One Thing:** Functions should do one thing. Error handling is one thing. This implies that if the keyword try exists in a function, it should be the very first word in the function, and that there should be nothing after the catch/finally blocks.

**Don't Repeat Yourself (DRY):** Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling it or eliminating it.

**Structured Programming:** Every function and every block within a function should have one entry and one exit. There should only be one return statement in a function, no break or continue statements in a loop, and NEVER EVER EVER "GOTO" statements. "GOTO" only makes sense in large functions, so it should be avoided.

**Functions are verbs, and classes are nouns of a domain-specific language designed by programmers. The art of programming is, and has always been, the art of language design.**

## 4. Comments

Comments are at best a necessary evil. If our programming languages were expressive enough or if we had the talent to subtly wield those languages to express our intent, we would not need comments very much. Comments are always failures; we have them because we cannot always figure out how to express ourselves without them.

The older a comment is, and the farther away it is from the code it describes, code changes and evolves, and comments can't follow them. Inaccurate comments are far worse than no comments at all. Truth can only be found in one place: the code.

Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments.

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))  
    // Better: if (employee.isEligibleForFullBenefits())
```

Write certain comments for legal reasons (copyright, authorship statements). It is sometimes useful to provide basic information with a comment.

```java
// Return an instance of the Responder being tested
protected abstract Responder responderInstance();
// Better: public void responderBeingTested()
```

Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision. Sometimes it is just helpful to translate the meaning of some obscure argument or return value into something that's readable.

```java
assertTrue(a.compareTo(a) == 0);  // a == a
assertTrue(a.compareTo(b) == 1);  // a > b
```

Sometimes it is useful to warn other programmers about certain consequences.

```java
// Don't run unless you have some time to kill
public void testWithReallyBigFile();
```

TODOs are jobs that the programmer thinks should be done. A comment may be used to amplify the importance of something that may otherwise seem inconsequential.

Any comment that forces you to look in another module for the meaning of that comment has failed to communicate to you and is not worth the bits it consumes. Replace the temptation to create noise with the determination to clean your code.

**"Don't use a comment when you can use a function or a variable."** **Commenting-out code: Don't do it!** Others who see that commented-out code won't have the courage to delete it. If you must write a comment, then make sure it describes the code it appears near. Don't offer systemwide information in the context of a local comment.

Don't put historical discussions or irrelevant descriptions of details into your comments. The connection between a comment and the code it describes should be obvious. A well-chosen name for a small function that does one thing is usually better than a comment header.

## 5. Formatting

### The Purpose of Formatting

Code formatting is about communication, and communication is the professional developer's first order of business. "Your style and discipline survive even though your code does not."

Small files are usually easier to understand than large files. **"The Newspaper Metaphor":** Code should be organized and structured like a well-written newspaper article.

Each line should be separated from each other with blank lines. Each blank line is a visual cue that identifies a new and separate concept.

If openness separates concepts, then "vertical density" implies close association. So lines of code that are tightly related should appear vertically dense. Concepts that are closely related should be kept vertically close to each other; this is one of the reasons that protected variables should be avoided.

**Variable Declarations:** Variables should be declared as close to their usage as possible. Instances should be declared at the top of the class.

**Dependent Functions:** If one function calls another, they should be vertically close, and the caller should be above the callee. This gives the program a natural flow. **Conceptual Affinity:** The stronger the affinity, the less "vertical distance" should be between them. In general, we want function call dependencies to point in the downward direction, creating a nice flow down the source code module from high level to low level.

Horizontal white space is used to associate things that are strongly related and disassociate things that are more weakly related.

```java
totalChars += lineSize;
lineWidthHistogram.addLine(lineSize, lineCount);
```

Unaligned declarations and assignments point out an important deficiency. Without indentation, programs would be virtually unreadable by humans.

Every programmer has his own favorite formatting rules, but if he works in a team, then team rules.

## 6. Objects and Data Structures

**"Law of Demeter":** An object should only communicate with its immediate neighbors and should not have knowledge of the internal workings of other objects that it interacts with.

Hiding implementation is about "abstractions." Objects hide their data behind abstractions and expose functions that operate on that data. Data structures expose their data and have no meaningful functions.

**Procedural Code (using Data Structures):** Makes it easy to add new functions without changing existing data structures. OO code, on the other hand, makes it easy to add new classes without changing existing functions.

```java
// Using Data Structures
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();

// Better version
Options opts = ctx.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();

// Best version
final String outputDir = ctxt.options.scratchDir.absolutePath;
```

Objects expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behavior. Data structures expose data and have no significant behavior.

## 7. Error Handling

Error handling is important, but if it obscures logic, it's wrong. Exceptions define a scope within your program; try blocks are like transactions.

**Use Unchecked Exceptions:** The price of checked exceptions is an Open/Closed Principle violation.

Each exception you throw should provide enough context to determine the source and location of an error. Wrapping third-party APIs is a best practice.

**"Don't Return Null":** If you are tempted to return null from a method, consider throwing an exception or returning a "SPECIAL CASE OBJECT" instead.

**"Don't Pass Null":** Avoid passing null in code whenever possible. Use assertions instead.

We can write robust clean code if we see error handling as a separate concern, something that is viewable independently of our main logic.

## 8. Boundaries

Providers of third-party packages and frameworks strive for broad applicability. Users want an interface that is focused on their particular needs.

**Learning Tests:** These are controlled experiments that check our understanding of a third-party API.

There are often places in the code where our knowledge seems to drop off the edge. Good software designs accommodate change without huge investments and rework.

Code at the boundaries needs clear separation and tests that define expectations. We should avoid letting too much of our code know about third-party particulars.

## 9. Unit Tests

### Three Laws of TDD

1. **First Law:** You may not write any production code until you have first written a failing unit test.
2. **Second Law:** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
3. **Third Law:** You may not write more production code than is sufficient to pass the currently failing test.

Tests and production code are written together. When working this way, tests cover virtually all of the production code. Having dirty tests is equivalent to, if not worse than, having no tests at all. Test code is just as important as production code and must be kept as clean.

Unit tests keep code flexible, maintainable, and reusable. If you have tests, you don't fear making changes to the code. Tests enable all the "-ilities" because they enable change.

**Readability** is crucial for clean tests. A clean test is readable, clear, simple, and has density of expression. The "Build-Operate-Check" pattern emphasizes the use of automated testing and continuous integration.

```java
@Test
public void turnOnLoTempAlarmAtThreshold() throws Exception {
    hw.setTemp(WAY_TO_COLD);
    controller.tic();
    assertTrue(hw.heaterState());
    assertTrue(hw.blowerState());
    assertFalse(hw.coolerState());
    assertFalse(hw.hiTempAlarm());
    assertTrue(hw.loTempAlarmState());
}

// Refactored
@Test
public void turnOnLoTempAlarmAtThreshold() throws Exception { 
    wayTooCold();
    assertEquals("HBchL", hw.getState());  // "HBchL" --> MENTAL MAPPING
}
```

Every test function in JUnit should have one and only one assert statement. The single assert rule is a good guideline. Usually, try to create a domain-specific testing language that supports it. The best practice is to minimize the number of asserts in a test.

### Five Rules of Clean Test (F.I.R.S.T)

1. **Fast:** Tests should run quickly. Slow tests discourage frequent execution.
2. **Independent:** Each test should be independent and not rely on others.
3. **Repeatable:** Tests should be repeatable in any environment.
4. **Self-Validating:** Tests should have a boolean output - pass or fail.
5. **Timely:** Unit tests should be written just before the production code that makes them pass.

Tests are as important to the health of a project as production code. Perhaps they are even more important because tests preserve and enhance the flexibility, maintainability, and reusability of the production code.

## 10. Classes

A class should begin with a list of variables, starting with public static constants, private static variables, private instance variables, and finally, public functions. If a test in the same package needs to call a function or access a variable, it should be protected or have package scope.

The first rule for classes is to keep them small, and the name of a class should describe what responsibilities it fulfills. The Single Responsibility Principle (SRP) states that classes should have one reason to change, i.e., one responsibility.

"Cohesion" is crucial; classes should have a small number of instance variables, and methods should be cohesive. High cohesion is the target, and when classes lose cohesion, they should be split. Good class design helps in reducing the risk of change.

The goal is to structure systems to reduce the risk of change. Dependency Injection (DI) is a powerful mechanism for separating construction from use, and it helps in achieving a clean and testable architecture.

## 11. Systems

Software systems should separate the startup process from the runtime logic. Dependency Injection (DI) and the Inversion of Control (IoC) pattern are effective in decoupling construction from use, making systems modular and easier to test.

Cross-cutting concerns refer to aspects affecting multiple parts of a system and cannot be cleanly separated. Aspect-oriented programming helps in isolating these concerns.

A good Domain-Specific Language (DSL) minimizes the communication gap between a domain concept and the code that implements it. Standards and DSLs help in achieving clarity and maintaining a high level of abstraction, making the intent clear at all levels.


## 12. Emergence

### Kent Beck's Four Rules of Simple Design

1. **Run all the tests:**
    
    - A design must produce a system that acts as intended.
    - A comprehensively tested system is a testable system.
    - A system that cannot be verified should not be deployed.
    - Testing classes conforming to the Single Responsibility Principle (SRP) is easier.
    - Tight coupling makes testing difficult.
    - Writing tests leads to better designs.
2. **Contains No Duplication:**
    
    - Duplication is the primary enemy of a well-designed system.
    - Reuse in the small is a principle of using small code components or functions.
    - Reuse in the small leads to more flexible, maintainable, and readable code.
3. **Expresses the Intent of the Programmer:**
    
    - Code should clearly express the intent of its author.
    - The majority of the cost in a software project is long-term maintenance.
    - Well-written unit tests act as documentation.
    - Minimize the cost of maintenance by choosing good names, keeping functions and classes small, and using standard nomenclature.
4. **Minimizes the Number of Classes and Methods:**
    
    - Keep the overall system small, but focus on keeping functions and classes small.
    - It's essential to have tests, eliminate duplication, and express yourself.
    - The goal is to keep the count of functions and classes low while maintaining clean code.
    - Focus on tests and clean code during refactoring.

Once tests are in place, code and classes can be kept clean by incrementally refactoring. The presence of tests eliminates the fear of breaking the code during cleanup. During refactoring, apply principles of good software design, such as increasing cohesion, decreasing coupling, separating concerns, modularizing system concerns, shrinking functions and classes, and choosing better names.

## 13. Concurrency

Objects represent abstraction of processing, while threads are abstractions of schedule. Writing code for a single thread is easier, but writing correct multithreaded code can be challenging, especially under stress.

### Myths and Misconceptions:

- **Concurrency always improves performance:** Only true when there is a lot of wait-time that can be shared between multiple threads or processors.
- **Design does not change when writing concurrent programs:** The decoupling of what from when affects the structure of the system.
- **Understanding concurrency issues is not important when working with a container:** It is crucial to understand concurrency issues regardless of the container.
- **Concurrency incurs some overhead:** Both in performance and writing additional code.
- **Correct concurrency is complex, even for simple problems:** Concurrency often requires a fundamental change in design strategy.

### Concurrency Defense Principles:

1. **Single Responsibility Principle (SRP):**
    
    - Concurrency-related code deserves to be separated from the rest of the code.
    - It has its own life cycle, challenges, and requires different considerations.
    
    _Corollary: Limit the Scope of Data_
    
    - Severely limit the access of any data that may be shared.
    
    _Corollary: Use Copies of Data_
    
    - Avoid sharing data; use copies when possible.
    
    _Corollary: Threads Should Be as Independent as Possible_
    
    - Design threaded code so that each thread exists in its own world, sharing no data with any other thread.
2. **Know Your Library:**
    
    - Use thread-safe collections.
    - Use the executor framework for executing unrelated tasks.
    - Use nonblocking solutions when possible.
    - Be aware of classes that are not thread-safe.
3. **Thread-Safe Collections:**
    
    - Examples include `ReentrantLock`, `Semaphore`, and `CountDownLatch`.
4. **Know Your Execution Methods:**
    
    - Understand concepts like bound resources, mutual exclusion, starvation, deadlock, and livelock.
5. **Producer-Consumer:**
    
    - Use queues as bound resources; producers wait for free space, consumers wait for items to consume.
6. **Readers-Writers:**
    
    - Balance the needs of readers and writers to satisfy correct operation and avoid starvation.
7. **Dining Philosophers:**
    
    - A classic problem demonstrating how to share limited resources among multiple entities.
8. **Beware Dependencies Between Synchronized Methods:**
    
    - Avoid using more than one method on a shared object; if necessary, use client-based or server-based locking.
9. **Keep Synchronized Sections Small:**
    
    - Locks are expensive; design code with as few critical sections as possible.
10. **Writing Correct Shut-Down Code Is Hard:**
    
    - Graceful shutdown can be challenging, expect to spend time getting it right.
11. **Testing Threaded Code:**
    
    - Treat spurious failures as potential threading issues.
    - Get nonthreaded code working before chasing threading bugs.
    - Make threaded code pluggable, tunable, and test on different platforms.
12. **Treat Spurious Failures as Candidate Threading Issues:**
    
    - Do not ignore system failures; treat them as potential threading issues.
13. **Get Your Nonthreaded Code Working First:**
    
    - Focus on non-threading bugs before tackling threading bugs.
14. **Make Your Threaded Code Pluggable:**
    
    - Design threaded code to be easily pluggable for testing in various configurations.
15. **Run on Different Platforms:**
    
    - Test threaded code on all target platforms early and frequently.
16. **Instrument Your Code to Try and Force Failures:**
    
    - Use automated or hand-coded instrumentation to simulate different scenarios and catch rare occurrences.


## 14. Successive Refinement

The code-only work is not enough to have good code. Professionals who care only about the code that works cannot be considered professional. We should ignore that we have no time to refactor one code. The code not taken care of today can become a problem for the team because no one will want to mess with it. Try not to let the code rot. It is much cheaper to create clean code than cleaning rotten code, as a move in a tangle can be an arduous task. The solution comes down to maintaining the cleanest code possible and as simple as possible without ever letting it begin to rot.

## 15. JUnit

Look to cover tests for each (not every method, but each code line). No code is immune to improvement, and each of us has a responsibility to make the code a little better than we found it. Refactoring is an iterative process full of trial and error, inevitably converging to something that we feel is worthy of a professional.

## 16. Refactoring Serial Date

Before making any kind of refactoring, it is important to have good coverage tests. After increasing or creating test coverage, you can begin to leave the clearest code and fix some bugs. Now, after leaving the code clearer, someone else can probably clean it even more.

## 17. Smell and Heuristics

### Comments

#### Inappropriate Information

It is inappropriate for a comment to hold information better held in a different kind of system. In general, metadata such as authors, last modified date, SPR number, and so on should not appear in comments. Comments should be reserved for technical notes about the code and design.

#### Obsolete Comment

A comment that has gotten old, irrelevant, and incorrect is obsolete. If you find an obsolete comment, it is best to update it or get rid of it as quickly as possible. Obsolete comments lend to migrate away from the code they once described.

#### Redundant Comment

```java
// i++; // increment i
```

Comments should say things that the code cannot say for itself.

#### Poorly Written Comment

A comment worth writing is worth writing well. Take the time to make sure it is the best comment you can write.

#### Commented-Out Code

It pollutes the modules that contain it and distracts the people who try to read it. Commented-Out is an abomination. When you see commented-out code, delete it!

### Environment

#### Build Requires More Than One Step

Building a project should be a single trivial operation. You should be able to check out the system with one simple command and then issue one other simple command to build it. A software build process should be designed to be modular and composable, with each step performing a specific task such as compiling source code, running automated tests, packaging the application, etc. The benefit of a multi-step build process is that it makes it easier to reason about the behavior of the build, to identify problems, and to improve the overall quality of the software. The idea is to encourage developers to adopt a more modular and composable approach to building software.

#### Tests Require More Than One Step

Should be able to run all the unit tests with just one command. In the best case, you can run all the tests by clicking on one button in your IDE. In the worst case, you should be able to issue a single simple command in a shell.

### Functions

#### Too Many Arguments

Functions should have a small number of arguments. No arguments are best. More than three is very questionable and should be avoided with prejudice.

#### Output Arguments

Output arguments are illogical. Readers expect arguments to be inputs, not outputs.

#### Flag Arguments

Boolean arguments loudly declare that the function does more than one thing.

#### Dead Functions

Methods that are never called should be discarded. Keeping dead code around is wasteful.

### General

#### Multiple Languages In One Source File

The ideal is for a source file to contain one, and only one, language. Realistically, we will probably have to use more than one. But we should take pains to minimize both the number and extent of extra languages in our source files.

#### Obvious Behavior Is Unimplemented

```java
// The Principle of Least Surprise: software should behave in a way that is least surprising or unexpected to the user.
// This principle applies not only to the behavior of the software itself but also to the way it is structured, designed, and documented.
```

Any function or class should implement the behaviors that another programmer could reasonably expect. When an obvious behavior is not implemented, readers and users of the code can no longer depend on their intuition about function names. They lose their trust in the original author and must fall back on reading the details of the code.

#### Incorrect Behavior At The Boundaries

Don't rely on your intuition. Look for every boundary condition and write a test for it.

#### Overridden Safeties

It is risky to override safeties. Overridden safeties can result in a variety of negative consequences, including increased security risks, unexpected behavior, and reduced system reliability. It can also make the code harder to maintain and extend, as developers may have difficulty understanding how the system works and what assumptions it makes. Developers should also resist the urge to bypass or disable safety features, even if it seems like it might be easier or more expedient to do so.

#### Duplication

DRY principle, Once and only once. Every time you see duplication in the code, it represents a missed opportunity for abstraction. Coding becomes faster and less error-prone because you have raised the abstraction level. A more subtle form is the switch/case or if/else chain that appears again and again in various modules, always testing for the same set of conditions. These should be replaced with polymorphism. Still more subtle are the modules that have similar algorithms but that don't share similar lines of code. This is still duplication and should be addressed by using the "TEMPLATE" / "STRATEGY" pattern.

#### Code At Wrong Level Of Abstraction

It is important to create abstractions that separate higher-level general concepts from lower-level detailed concepts. We want all the lower-level concepts to be in the derivatives and all the higher-level concepts to be in the base class. For example, constants, variables, or utility functions that relate only to the detailed implementation should not be present in the base class. The base class should know nothing about them. The point is that you cannot lie or fake your way out of a misplaced abstraction. Isolating abstractions is one of the hardest things that software developers do, and there is no quick fix when you get it wrong.

#### Base Classes Depending On Their Derivatives

Base classes should know nothing about their derivatives.

#### Too Much Information

Well-defined modules have very small interfaces that allow you to do a lot with a little. Poorly defined modules have wide and deep interfaces that force you to use many different gestures to get simple things done. Hide your data, hide your utility functions. Hide your constants and your temporaries. Concentrate on keeping interfaces very tight and very small. Help keep coupling low by limiting information.

#### Dead Code

Dead code is that isn't executed. The problem with dead code is that after a while it starts to smell. The older it is, the stronger and sourer the odor becomes. This is because dead code is not completely updated when designs change. It still compiles but does not follow newer conventions or rules. When you find dead code, give it a decent burial. Delete it from the system.

#### Vertical Separation

Variables and functions should be defined close to where they are used. Local variables should be declared just above their first usage and should have a small vertical scope. Private functions should be defined just below their first usage. Finding a private function should just be a matter of scanning downward from the first usage.

#### Inconsistency

If you do something a certain way, do all similar things in the same way. Be careful with the conventions you choose, and once chosen, be careful to continue to follow them.

#### Clutter

All these things are clutter and should be removed.

#### Artificial Coupling

Things that don't depend upon each other should not be artificially coupled. An artificial coupling is a coupling between two modules that serves no direct purpose. It is a result of putting a variable, constant, or function in a temporarily convenient though inappropriate location. This is lazy and careless.

#### Feature Envy

The methods of a class should be interested in the variables and functions of the class they belong to and not the variables and functions of other classes.

#### Selector Arguments

There is hardly anything more abominable than a dangling false argument at the end of a function call. Not only is the purpose of a selector argument difficult to remember, each selector argument combines many functions into one. Selector arguments are just a lazy way to avoid splitting a large function into several smaller functions.

#### Obscured Intent

We want code to be as expressive as possible. Run-on expressions, Hungarian notation, and magic numbers all obscure the author's intent.

#### Misplaced Responsibility

One of the most important decisions a software developer can make is where to put code. The principle of least surprise comes into play here. Code should be placed where a reader would naturally expect it to be.

#### Inappropriate State

You should prefer non-static methods to static methods. When in doubt, make the function non-static. If you really want to make a function static, make sure that there is no chance that you'll want it to behave polymorphically.

#### Use Explanatory Variables

Break the calculations up into intermediate values that are held in variables with meaningful names. More explanatory variables are generally better than fewer.

#### Functions Names Should Say What They Do

If you have to look at the implementation (or documentation) of the function to know what it does, then you should work to find a better name or rearrange the functionality so that it can be placed in functions with better names.

#### Understand The Algorithm

Programming is often an exploration. Before you consider yourself to be done with a function, make sure you understand how it works. You must know that the solution is correct.

#### Make Logical Dependencies Physical

If one module depends upon another, that dependency should be physical, not just logical. The dependent module should not make assumptions about the module it depends upon.

#### Prefer Polymorphism To If/Else Or Switch/Case

Most people use switch statements because it's the obvious brute force solution, not because it's the right solution for the situation. Consider polymorphism before using a switch. The cases where functions are more volatile than types are relatively rare. So every switch statement should be suspect.

##### One Switch Rule

The One Switch rule states that if there are multiple switches or flags that control the behavior of a section of code, then the code may be overly complex, difficult to understand, and harder to maintain. In contrast, having only one switch or flag makes the code simpler and easier to reason about.

#### Follow Standard Conventions

Every team should follow a coding standard based on common industry norms. This means that each team member must be mature enough to realize that it doesn't matter a whit where you put your braces, so long as you all agree on where to put them.

#### Replace Magic Numbers With Named Constants

It is a bad idea to have raw numbers in code. You should hide them behind well-named constants. The term "Magic Number" does not apply only to numbers. It applies to any token that has a value that is not self-describing.

```java
assertEquals(7777, Employee.find("John Doe").employeeNumber());

assertEquals(
    HOURLY_EMPLOYEE_ID,
    Employee.find(HOURLY_EMPLOYEE_NAME).employeeNumber()
);
```

#### Be Precise

When you make a decision in your code, make sure you make it precisely. Know why you have made it and how you will deal with any exceptions. Ambiguities and imprecision in code are either a result of disagreements or laziness.

#### Structure Over Convention

Enforce design decisions with structure over convention. Naming conventions are good, but they are inferior to structures that force compliance.

#### Encapsulate Conditionals

Boolean logic is hard enough to understand without having to see it in the context of an if or while statement. Extract functions that explain the intent of the conditional.

```java
if (shouldBeDeleted(timer)) > if (timer.hasExpired() && !timer.isRecurrent())
```

#### Avoid Negative Conditionals

Negatives are just a bit harder to understand than positives. So when possible, conditionals should be expressed as positives.

```java
if (buffer.shouldCompact()) > if (!buffer.shouldNotCompact())
```

#### Functions Should Do One Thing

Functions of this kind do more than one thing and should be converted into many smaller functions, each of which does one thing.

#### Hidden Temporal Couplings

Temporal couplings are often necessary, but you should not hide the coupling. Structure the arguments of functions such that the order in which they should be called is obvious.

#### Don't Be Arbitrary

Have a reason for the way you structure your code, and make sure that reason is communicated by the structure of the code.

#### Encapsulate Boundary Conditions

Boundary conditions are hard to keep track of. Put the processing for them in one place. Don't let them leak all over the code.

```java
if (level + 1 < tags.length) {
    parts = new Parse(body, tags, level + 1, offset + endTag);
    body = null;
}
```


```java
int nextLevel = level + 1;
if (nextLevel < tags.length) {
    parts = new Parse(body, tags, nextLevel, offset + endTag);
    body = null;
}
```

#### Functions Should Descend Only One Level Of Abstraction

The statements within a function should all be written at the same level of abstraction, which should be one level below the operation described by the name of the function. Separating levels of abstraction is one of the most important functions of refactoring, and it's one of the hardest to do well.

#### Keep Configurable Data At High Level

If you have a constant such as default or configuration value that is known and expected at a high level of abstraction, do not bury it in a low-level function.

#### Avoid Transitive Navigation

We don't want a single module to know much about its collaborators. More specifically, if "A" collaborates with "B," and "B" collaborates with "C," we don't want modules that use "A" to know about "C". The Law Of Demeter applies here.

## Java

- **Avoid Long Import Lists By Using Wildcards**
    
    - If you use two or more classes from a package, import the whole package with `import package.*`.
    - Long lists of imports are daunting to the reader.
- **Don't Inherit Constants**
    
    - Don't use inheritance as a way to cheat the scoping rules of the language. Use a static import instead.
- **Constants Versus Enums**
    
    - Avoid using public static final ints; use enums instead.

## Names

- **Choose Descriptive Names**
    
    - Names should be descriptive. Names in software are 90 percent of what makes software readable.
- **Choose Names At The Appropriate Level Of Abstraction**
    
    - Pick names that reflect the level of abstraction of the class or function you are working in.
- **Use Standard Nomenclature Where Possible**
    
    - Names are easier to understand if they are based on existing conventions or usage.
- **Unambiguous Names**
    
    - Choose names that make the workings of a function or variable unambiguous.
- **Use Long Names For Long Scopes**
    
    - The length of a name should be related to the length of the scope; for big scopes, use longer names.
- **Avoid Encodings**
    
    - Names should not be encoded with type or scope information.
- **Names Should Describe Side-Effects**
    
    - Names should describe everything that a function, variable, or class is or does.

## Tests

- **Insufficient Tests**
    
    - A test suite should test everything that could possibly break.
    - The tests are insufficient so long as there are conditions that have not been explored by the tests or calculations that have not been validated.
- **Use Coverage Tool**
    
    - Coverage tools report gaps in your testing strategy.
- **Don't Skip Trivial Tests**
    
- **An Ignored Test Is A Question About An Ambiguity**
    
    - An ignored test is a question about an ambiguity; resolve ambiguities in requirements.
- **Test Boundary Conditions**
    
    - Take special care to test boundary conditions.
- **Exhaustively Test Near Bugs**
    
    - When you find a bug in a function, do exhaustive testing of that function.
- **Patterns Of Failure Are Revealing**
    
    - Diagnose problems by finding patterns in the way the test cases fail.
- **Test Coverage Patterns Can Be Revealing**
    
- **Tests Should Be Fast**
    
    - A slow test is a test that won't get run. Ensure tests are fast to encourage regular execution.


---

# SLIDES NOTES

- Kodlama (programlama) aslen karmaşık ve zordur ve aslolan geliştirmek değil değiştirmektir (bakım), dolayısıyla değişebilen kod geliştirmek daha da zordur.

  Temiz Kod (Clean Code), rahat anlaşılır ve kolay değişebilir koddur. / Temiz kod, odaklıdır dolayısıyla da kısadır ve bağımlılıkları azdır.



  	• Clean/Dirty Code, bir teknoloji problemi değildir.
  	• Clean/Dirty Code, bir ahlak ve bilgi problemidir.
  	• Clean/Dirty Code, işini iyi yapmakla ilgilidir.

Eğer bir kod parçası rahat anlaşılır, hızlıca değiştirilebilir, varsa hatası kolayca bulunup düzeltilebilir değilse ne kadar performanslı ya da güvenli olduğunun pek önemi olmayabilir.

Temiz Kod, temelde dört özelliğe sahiptir:

- **Basit:** Bir şeyi ilk defa yaparken muhtemelen karmaşık yaparız. "KISS": Keep it simple, stupid - keep it simple and short! Kodun basitleştirilmesine "iyileştirme (refactoring)" denir.
    
    - Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away.
    - Basit kod en temelde doğru soyutlama seviyesinde olan koddur. Rahat anlaşılır, kısadır.
- **Odaklı:** Anlaşılır kodun en temel içerik özelliği, odaklı olmasıdır. "Odaklı kod, bir yerde birden fazla şeyi bir araya getirmez."
    
    - Tek hedefli: "Single-responsibility principle", "High-cohesion", "Low-coupling"
    - Tekrarsız: Tasarımla ve sonrasında gerektiğinde refactoring ile elde edilir. "Don’t Repeat Yourself, DRY" Copy-paste kullanmayın, cut-paste kullanın!
- **Doğru:** Bir kodun kendi başına doğruluğu ancak "birim testiyle (unit test)" sınanabilir. Bir kodun çevresindeki diğer kod parçalarıyla birlikte doğru çalıştığı ise ancak "entegrasyon testiyle" sağlanabilir.
    
- **Tam:** "Exception Handling", "Defensive Programming"
    
    - Olması gerekeni yapması,
    - Olmaması gerekene karşı önlem alması, engellemesi,
    - Olabilecek olanı da öngörmesi.

Anlaşılır kodun iki şartı vardır:

- Şekil şartı, standart olması,
    
- İçerik şartı, odaklı olmasıdır. -> bir yerde sadece ve sadece bir şeyi yapar ama tam yapar.
    
- Mimariye Uyum: Belirlenen mimariye uygun geliştirilir,
    
- İsim: Anlaşılır isimler içerir,
    
- Şekil: Ferahtır, mekanı etkin kullanır dolayısıyla rahat okunur,
    
- İsim, Şekil ve Dilin Kullanımı: Tutarlıdır yani şaşırtmaz, beklenildiği gibidir, aşina olunandır
    
- Dokümantasyon: Gerektiği kadar, anlaşılmaya yardım edecek şekilde dokümante edilmiştir.
    

## Mimari:

- Mimari, üst düzey tasarımdır.
- Mimari, bileşenleri, en temel özelliklerini ve aralarındaki ilişkileri betimler.
- Mimari tasarım, projenin en soyut ama en katma değerli kalıbı/şablonu ve yol göstericisidir. // • Anlaşılıklık, mimari tasarımla başlar.

Projelerde standarttan ilk sapma genelde mimariye uyumda yaşanır.

## İsimlendirme

- Öncelikle, İngilizce isimler kullanılmalıdır.
    
- Anlaşılır isimlendirmenin en temel engeli kısaltmadır.
    
- Zihinsel kodlamalardan kaçının, açıkça anlaşılır olun. -> private int nofInst; private int nofInst; -> anlamsız
    
- Çok bilindik, evrenselleşmiş değil ise kısaltmalardan kaçının
    
- Kısa, bulmaca gibi isimler yerine uzun, okuması zaman alan ama anlamlı isimler verin. -> File file / File fileToReadFromClientToConfigureServer / Product pr / Product productToBeDeleted
    
- İş mantığı karmaşıklaştıkça ayırt edici isimler daha önemli hale geliyor
    
- İsimleriniz olabildiğince soyut ve kapsayıcı olsun -> int km -> int distance -> int distanceToGo / int remainingDistance
    
- Ne yaptığınızı bilmiyorsanız iyi isim veremezsiniz!
    
- Aynı kelimeleri kullanan değişik isimler oluştururken dikkatli olun. -> StudentRegistration / RegistrationStudent
    
- Aynı kavramlara, işlere farklı yerlerde farklı isimler vermeyin İsimlendirmede tüm sistemde, analist, PM, tester, developer, iş birimleri vs. tüm çalışanlarla tutarlı bir dil kurun. "• Domain-Driven Design"
    

**TEMEL KURALLAR**

- İngilizce isim.
- Kısaltma yok: Anlamlı olacak kadar uzun isimler!
- Şaşırtmaca yok, standart var: Herkes aynı isimleri aynı anlamda ve aynı şekilde kullanıyor.

## Dökümantasyon:

Anlaşılır kodun son şartı, gerektiği kadar dokümante edilmiş (commented - documented) olmasıdır. "Anlaşılır kod için iyi isimlendirme ve odaklı olmaktan kaynaklanan kısalık yeterli değilse", kod açıklanmalıdır. Kodu açıklamak, kod dokümantasyonu (code documentation) ile olur.

* Eğer bir kodun anlaşılması için dokümantasyona ihtiyaç duyuluyorsa, bunun çözümü öncelikle dokümantasyon değildir.
*  Koda yazılan her yorumun bir özür olduğu söylenir:

- Kod içi dokümantasyon, ihtiyaca bağlı olarak kısa “//“ ya da “/* */“ notları halinde yapılabilir.
    
- API dokümantasyonu, kodun arayüzünün dokümantasyonudur.
    
- API dokümantasyonu çok daha önemli ve stratejiktir.
    
- Debugger kullanmaya harcanan vakti API dokümantasyonuna harcamak çok daha faydalıdır.
    
- Kod içi dokümantasyon, açık olanı, görüneni değil, iyi isimlendirmeye rağmen görünmeyeni, açık olmayanı açıklamalıdır.


## Yazılım Doğası

Yazılımın asli "(essential)" olan dört özelliği:

- _**Karmaşıklık (Complexity):**_ Yazılım diğer mühendislik ürünlerinden daha karmaşıktır.
- _**Değişebilirlik (Changeability):**_ Yazılım çok sık değişir.
- _**Görünmezlik (Invisibility):**_ Yazılım görülemez.
- _**Uyumlu Olma (Conformity):**_ Yazılım uyumludur, sahnedeki diğer oyunculara uyar.

### Karmaşıklık (Complexity)

Karmaşıklık soyuttur, zihinseldir ve görünmez; bu yüzden fiziksel kısıtları yoktur. Yazılımın yaşam döngüsünde en kolay olanı, yazılımı kodlamaktır, çünkü en fazla görünür olan kısım kodlamadır. Yazılımların bileşenleri birbirlerinden farklıdır ve yazılımların büyümesi yeni ve orijinal bileşenlerin eklenmesiyle gerçekleşir.

### Birliktelik (Cohesion)

Birliktelik, bir bileşenin alt parçalarının ne kadar bir arada olduğunun bir ölçüsüdür. "Birliktelik," tek bir amaca veya sorumluluğa odaklanmadır ("single responsibility").

- **High Cohesion:** Bileşenin alt elemanları birbirine yakın ve belirli bir amacı başarmak için bir araya gelir, karmaşıklığı düşüktür, bakım maliyetleri düşüktür ve tekrar kullanıma daha yatkındırlar.
- **Low Cohesion:** Bileşenin alt elemanları birbirine gevşek bağlıdır ve tek bir amaç için bir araya gelmezler.

**Cohesion Types: Worst To Better**

1. **Gelişigüzel "(Coincidental)":** Bir araya getirilmiş ilgisiz yapılar.
2. **Mantıksal "(Logical)":** Ortak bir koşul veya karar tarafından ilişkilendirilen yapılar.
3. **Zamansal "(Temporal)":** Zaman tarafından ilişkilendirilen yapılar.
4. **Prosedürel "(Procedural)":** İşlemlere dayalı yapılar.
5. **İletişimsel "(Communicational/Informational)":** Veri üzerinde çalışan yapılar.
6. **Ardışıl "(Sequential)":** Sıralı çalışan yapılar.
7. **Fonksiyonel "(Functional)":** Tek bir amaç için bir araya getirilmiş yapılar.

### Nesne Kategorizasyonu

- **Boundary:** Sistemin aktörleriyle olan iletişimini yöneten nesneler.
- **Control:** İş süreçlerini yöneten ve ilgili kuralları bilen nesneler.
- **Entity:** İş alanı (business domain) nesneleri.

B-C-E nesneleri arasındaki bağımlılıklar temelde dıştan içe doğrudur. Aynı roldeki nesneler birbirlerini kullanabilirler.

### Bağımlılık (Coupling)

Bağımlılık, bir modülün kendi başına ifade edilebilirliğinin veya diğerleriyle ne kadar ilgili olduğunun ölçüsüdür. Farklı modül veya bileşenler arasındaki bağlılık derecesidir.

**Coupling Types: Worst To Better**

1. **İçerik "(Content)":** İç yapıya bağımlılık.
2. **Ortak "(Common)":** Ortak modüle veya bileşene bağımlılık.
3. **Dışsal "(External)":** Dış bir bileşenin formatına veya arayüzüne bağımlılık.
4. **Kontrol "(Control)":** Akış kontrolüne bağımlılık.
5. **Veri-yapısı bağımlılığı "(Stamp (Data-Structured) Coupling)":** Karmaşık veri yapılarına bağımlılık.
6. **Veri bağımlılığı "(Data Coupling)":** Basit veriye bağımlılık.
7. **Mesaj "(Message)":** Nesne arayüzü bilgisi dışında bağımlılık.

## Birliktelik ve Bağımlılık "Cohesion and Coupling"

İşleri yapan bileşenlerin yüksek birliktelikli ve düşük bağımlılıklı olması için işlerin uygun bir şekilde alt parçalara bölünmesi gerekir. Koordinasyon, bir bağımlılıktır ve açık ve olabilecek en az seviyede olmalıdır. Yüksek birliktelikli ve düşük bağımlılıklı işler, rahat anlaşılır, hızlı geliştirilir, kolay test edilir ve aktarılır.

Sonsuz birliktelik mümkün olamazken, sıfır bağımlılık da mümkün değildir.

## Değişim

Değişim, yazılımın doğasının bir parçasıdır. Bakım, büyük oranda yazılımı değiştirmektir. Yazılımda değişimin temel sebebi, yeni ihtiyaçlardır. Birlikteliği yüksek, bağımlılığı düşük olan yapılar daha rahat değişir.

- **Design for Change:** Sık değişecek kısımların kolay değişecek şekilde tasarlanması stratejisidir. Yazılımda değişen ile sabit kalanı ayırt etmek fiziksel mühendislik ürünlerindeki kadar öngörülebilir değildir.
    
- **Aslolan veri sağlamak değil, davranış sağlamaktır.** Veri anlamdan yoksundur; veriyi anlamlı hale getiren bağlamdır. Bağlam ise davranış tarafından belirlenir. Nesnelerin varlık sebebi sorumluluklarıdır. Veri, davranış için vardır.

## **SOLID İlkeleri:**

1. **Tek Sorumluluk Prensibi (Single Responsibility Principle - SRP):**
    
    - Bir sınıfın değişmesi için sadece bir neden olmalıdır.
    - Bir sınıfın sorumlulukları birbirinden ayrılmalıdır.
    - Paket, sınıf, metod, blok ve cümle gibi farklı soyutlama seviyeleri için ele alınmalıdır.
2. **Açık-Kapalı Prensibi (Open-Closed Principle - OCP):**
    
    - Yazılım birimleri genişletilmeye açık, değişime kapalı olmalıdır.
    - Yeni özellikler eklemek, mevcut kodu değiştirmeyi gerektirmemelidir.
3. **Liskov Yerine Koyma Prensibi (Liskov Substitution Principle - LSP):**
    
    - Alt sınıflar, üst sınıfların yerine kullanılabilir olmalıdır.
    - İstemci, üst sınıfları kullandığında alt sınıfların davranışlarını bilmemelidir.
4. **Arayüz Ayrımı Prensibi (Interface Segregation Principle - ISP):**
    
    - İstemciler, kullanmadıkları arayüzlerden etkilenmemelidir.
    - Büyük arayüzler, istemcileri sıkıntıya sokmamak için küçük arayüzlere bölünmelidir.
5. **Bağımlılıkların Tersine Çevrilmesi Prensibi (Dependency Inversion Principle - DIP):**
    
    - Yüksek seviyeli modüller, düşük seviyeli modüllere bağımlı olmamalıdır.
    - Her ikisi de soyutlamalara bağımlı olmalıdır.

**Diğer Prensip:**

- **Granularity Prensibi:**
    - Sistemdeki farklı bileşenlerin (sınıf, metod, paket, vs.) uygun seviyede ayrıntılı olması gerektiğini ifade eder.

**Ekstra Kavramlar:**

- **Cümle (Statement):**
    
    - Bir metodun ya da bloğun parçası olarak bir işin tek bir adımını gerçekleştirmelidir.
    - Karmaşık ifadeler alt parçalara ayrılmalı ve tekrar kullanılabilir olmalıdır.
- **Metot (Method):**
    
    - Metotlar tek bir işi yerine getirmelidir.
    - "İşçi/atomik metotlar" ve "Yöneten/yönetsel/koordinatif metotlar" olarak iki tür metot vardır.
- **Sınıf (Class):**
    
    - Bir sınıf sadece tek bir sorumluluğa odaklanmalıdır.
    - Atomik işçi metotlar ile yöneten metotlar farklı sınıflarda olmalıdır.
- **Tam Yazılım:**
    
    - Yazılım, olması gerekenleri yaparken olmaması gerekenleri önlemeli ve olabilecek durumları öngörmelidir.
- **Savunmacı Programlama:**
    
    - Yazılımın güvenirliğini sağlamak için yapılan tekniklerdir.
    - Assertion ifadeleri ve istisna işleme bu kapsamda değerlendirilebilir.
- **En Az Bilgi Prensibi:**
    
    - Nesneler, birbirlerinin gerçekleştirme detaylarını bilmemeli, sadece arayüzleri üzerinden iletişim kurmalıdır.
- **Law of Demeter:**
    
    - Her birim sadece ve sadece “arkadaşlarıyla” iletişim kurmalı, “yabancılarla” iletişim kurmamalıdır.
- **Assertations:**
    
    - Kodun beklenen şekilde çalışıp çalışmadığını kontrol etmek için kullanılır.
    - Geliştirme sırasında açılıp, canlı ortamda kapatılabilir.
- **Exception Handling:**
    
    - Yazılımın çalışması sırasında oluşabilecek anormal durumları yönetmek için kullanılır.
    - Sıra dışı durumları önceden düşünüp tedbir almak önemlidir.



