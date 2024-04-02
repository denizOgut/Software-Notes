# Introduction

## Reviewing Question Types

**Questions with Extra Information** 
  Provided Imagine the question includes a statement that `XMLParseException` is a checked exception. It’s fine if you don’t know what an `XMLParseException` is or what XML is, for that matter. (If you are wondering, it is a format for data.) This question is a gift. You know the question is about exception handling.

**Questions with Embedded Questions**
  To answer some questions on the exam, you may have to answer two or three sub-questions. For example, the question may contain two blank lines and ask you to choose the two answers that fill in each blank. In some cases, the two answer choices are not related, which means you’re really answering multiple questions, not just one! These questions are among the most difficult and time-consuming on the exam because they contain multiple, often independent, questions to answer.

**Questions with Unfamiliar APIs**
  If you see a class or method that wasn’t covered in this book, assume that it works as you would expect. Assume that the part of the code using that API is correct, and look very hard for other errors.

**Questions That Are Really Out of Scope**
  When introducing new questions, Oracle includes them as unscored questions at first. This allows the exam creators to see how real exam takers do without impacting your score. You will still receive the number of questions the exam lists. However, a few of them may not count. These unscored questions may contain out-of- scope material or even errors. They will not be marked as unscored, so you still have to do your best to answer them. Follow the previous advice to assume that anything you haven’t seen before is correct. That will cover you if the question is being counted!


## How This Book Is Organized

The chapters are organized as follows:
- **Chapter 1: Building Blocks** 
	   describes the basics of Java, such as how to run a program. It covers variables such as primitives, object data types, and scoping variables. It also discusses garbage collection.
	   
- **Chapter 2: Operators** 
	 explains operations with variables. It also talks about casting and the precedence of operators.
	 
-  **Chapter 3: Making Decisions** 
	 covers core logical constructs such as decision statements, pattern matching, and loops.
	 
- **Chapter 4: Core APIs** 
	 works with String, StringBuilder, arrays, and dates.
	 
- **Chapter 5: Methods** 
	explains how to design and write methods. It also introduces access modifiers, which are used throughout the book.
	
- **Chapter 6: Class Design** 
	covers class structure, constructors, inheritance, and initialization. It also teaches you how to create abstract classes and overload methods.
	
- **Chapter 7: Beyond Classes** 
	introduces many top-level types (other than classes), including interfaces, enums, sealed classes, records, and nested classes. It also covers polymorphism.
	
- **Chapter 8: Lambdas and Functional Interfaces** 
	shows how to use lambdas, method references, and built-in functional interfaces.
	
- **Chapter 9: Collections and Generics** 
	demonstrates method references, generics with wildcards, and Collections. The Collections portion covers many common interfaces, classes, and methods that are useful for the exam and in everyday software development.
	
- **Chapter 10: Streams** 
	explains stream pipelines in detail. It also covers the Optional class. If you want to become skilled at creating streams, read this chapter more than once!
	
 - **Chapter 11: Exceptions and Localization** 
	 demonstrates the different types of exception classes and how to apply them to build more resilient programs. It concludes with localization and formatting, which allow your program to gracefully support multiple countries or languages.
	 
- **Chapter 12: Modules** 
	details the benefits of the new module feature. It shows how to compile and run module programs from the command line. Additionally, it describes services and how to migrate an application to a modular infrastructure.
	
-  **Chapter 13: Concurrency** 
	introduces the concept of thread life cycle and thread-safety. It teaches you how to build multithreaded programs using the Concurrency API and parallel streams.

- **Chapter 14: I/O** 
	introduces you to managing files and directories using the I/O and NIO.2 APIs. It covers a number of I/O stream classes, teaches you how to serialize data, and shows how to interact with a user. Additionally, it includes techniques for using streams to traverse and search the file system.
	
- **Chapter 15: JDBC** 
	provides the basics of working with databases in Java, including working with stored procedures and transactions.

At the end of each chapter
 - **Summary** 
	This section reviews the most important topics that were covered in the chapter and serves as a good review.

- **Exam Essentials** 
	This section summarizes highlights that were covered in the chapter.

- **Review Questions** 
	Each chapter concludes with at least 20 review questions. You should answer these questions and check your answers against the ones provided in the Appendix. If you can’t answer at least 80 percent of these questions correctly, go back and review the chapter,

## Identifying Your Weakest Link

The review questions in each chapter are designed to help you home in on those features of the Java language where you may be weak and that are required knowledge for the exam.
For each chapter, you should note which questions you got wrong, understand why you got
them wrong, and study those areas even more. After you’ve reread the chapter and written
lots of code, you can do the review questions again

## Using the Provided Writing Material

After first checking whether the code compiles, it is time to understand what the program
does! One of the most useful applications of writing material is tracking the state of primitive
and reference variables. For example, let’s say you encountered the following code snippet on a question about garbage collection:

```java
Object o = new Turtle();
Mammal m = new Monkey();
Animal a = new Rabbit();
o = m;
```

In a situation like this, it can be helpful to draw a diagram of the current state of the variable
references. As each reference variable changes which object it points to, you erase or
cross out the arrow between them and draw a new one to a different object.
Using the writing material to track state is also useful for complex questions that involve
a loop, especially questions with embedded loops

## Understanding the Question

the number-one question we recommend that you answer before attempting to solve the question is this:

==***Does the code compile?***==

> If all of the answers to a question are printed values, aka there is no Does not compile option, consider that question a gift. It means every line does compile, and you may be able to use information from this question to answer other questions! #TIP

## Applying the Process of Elimination

Although you might not immediately know the correct answer to a question, if you can
reduce the question from five answers to three, your odds of guessing the correct answer are markedly improved.

In some cases, you may be able to eliminate answer choices without even reading the
question. If you come across such questions on the exam, consider it a gift.

1. Which line, when inserted independently at line m1, allows the code to compile?
-Code Omitted -

```java
A. public abstract final int swim();
B. public abstract void swim();
C. public abstract swim();
D. public abstract void swim() {}
E. public void swim() {}
```

B & E

## Skipping Difficult Questions

The exam software includes an option to “mark” a question and review all marked questions
at the end of the exam. If you are pressed for time, answer a question as best you can
and then mark it to come back to later.

All questions are weighted equally, so spending 10 minutes answering five questions correctly is a lot better use of your time than spending 10 minutes on a single question.

## Being Suspicious of Strong Words

Many questions on the exam include answer choices with descriptive sentences rather than
lines of code. When you see such questions, be wary of any answer choice that includes
strong words such as “**must**,” “**all**,” or “**cannot**.”

If you think about the complexities of programming languages, it is rare for a rule to have no exceptions or special cases. Therefore, ==if you are stuck between two answers and one of them uses “must” while the other uses “can” or “may,” you are better off picking the one with the weaker word since it is a more ambiguous statement.==

## Choosing the Best Answer

If you’re nearly out of time or you just can’t decide on an answer, select a random option and move on. If you’ve been able to eliminate even one answer choice, then your guess is better than blind luck.


|Chapter|Exam Objectives|
|---|---|
|1, 2, 4|Handling date, time, text, numeric, and boolean values. Use primitives and wrapper classes, including Math API, parentheses, type promotion, and casting to evaluate arithmetic and boolean expressions.|
|4|Manipulate text, including text blocks, using String and StringBuilder classes.|
|4|Manipulate date, time, duration, period, instant, and time-zone objects using Date-Time API.|
|3|Controlling Program Flow. Create program flow control constructs including if/else, switch statements and expressions, loops, and break and continue statements.|
|1, 7|Utilizing Java Object-Oriented Approach. Declare and instantiate Java objects, including nested class objects, and explain the object life-cycle, including creation, reassigning references, and garbage collection.|
|5, 6, 7|Create classes and records, and define and use instance and static fields and methods, constructors, and instance and static initializers. Implement overloading, including var-arg methods.|
|1, 6, 7, 8|Understand variable scopes, use local variable type inference, apply encapsulation, and make objects immutable.|
|3, 6, 7|Implement polymorphism and differentiate object type versus reference type. Perform type casting, identify object types using the instanceof operator and pattern matching.|
|7, 8|Create and use interfaces, identify functional interfaces, and utilize private, static, and default interface methods.|
|7|Create and use enumerations with fields, methods, and constructors.|
|11|Handling Exceptions. Handle exceptions using try/catch/finally, try-with-resources, and multi-catch blocks, including custom exceptions.|
|4, 9|Working with Arrays and Collections. Create Java arrays, List, Set, Map, and Deque collections, and add, remove, update, retrieve, and sort their elements.|
|10|Working with Streams and Lambda expressions. Use Java object and primitive Streams, including lambda expressions implementing functional interfaces, to supply, filter, map, consume, and sort data. Perform decomposition, concatenation and reduction, and grouping and partitioning on sequential and parallel streams.|
|12|Packaging and deploying Java code and use the Java Platform Module System. Define modules and their dependencies, expose module content including for reflection. Define services, producers, and consumers. Compile Java code, produce modular and non-modular jars, runtime images, and implement migration using unnamed and automatic modules.|
|13|Managing concurrent code execution. Create worker threads using Runnable and Callable, manage the thread lifecycle, including automations provided by different Executor services and concurrent API. Develop thread-safe code, using different locking mechanisms and concurrent API. Process Java collections concurrently, including the use of parallel streams.|
|14|Using Java I/O API. Read and write console and file data using I/O Streams. Serialize and de-serialize Java objects. Create, traverse, read, and write Path objects and their properties using java.nio.file API.|
|15|Accessing databases using JDBC. Create connections, create and execute basic, prepared and callable statements, process query results and control transactions using JDBC API.|
|11|Implementing Localization. Implement localization using locales, resource bundles, parse and format messages, dates, times, and numbers including currency and percentage values.|

## Assessment Test

1. What is the result of executing the following code snippet?

```java
41: final int score1 = 8, score2 = 3;
42: char myScore = 7;
43: var goal = switch (myScore) {
44: default -> { if (10 > score1) yield "unknown"; }
45: case score1 -> "great";
46: case 2, 4, 6 -> "good";
47: case score2, 0 -> { "bad"; }
48: };
49: System.out.println(goal);
```

- [ ] A. unknown
- [ ] B. great
- [ ] C. good
- [ ] D. bad
- [ ] E. unknowngreatgoodbad
- [ ] F. Exactly one line needs to be changed for the code to compile.
- [x] G. Exactly two lines need to be changed for the code to compile.
- [ ] H. None of the above

**The question does not compile because line 44 and line 47 do not always return a value**
**in the case block, which is required when a switch expression is used in an assignment**
**operation.** 
**Line 44 is missing a yield statement when the if statement evaluates to false,**
**while line 47 is missing a yield statement entirely.**

---

2. What is the output of the following code snippet?

```java
int moon = 9, star = 2 + 2 * 3;
float sun = star > 10 ? 1 : 3;
double jupiter = (sun + moon) - 1.0f;
int mars = --moon <= 8 ? 2 : 3;
System.out.println(sun + ", " + jupiter + ", " + mars);

```

- [ ] A. 1, 11, 2
- [x] B. 3.0, 11.0, 2
- [ ] C. 1.0, 11.0, 3
- [ ] D. 3.0, 13.0, 3
- [ ] E. 3.0f, 12, 2
- [ ] F. The code does not compile because one of the assignments requires an explicit numeric
- [ ] cast.

**The multiplication operator (*) has a higher order of precedence than the addition operator (+), so it gets evaluated first. Since star is not greater than 10, sun is assigned a value of 3, which is**
**promoted to 3.0f as part of the assignment. The value of jupiter is (3.0f + 9) -1.0, which is 11.0f.**

**This value is implicitly promoted to double when it is assigned. In the last assignment, moon is decremented from 9 to 8, with the value of the expression returned as 8. Since 8 less than or equal to 8 is true, mars is set to a value of 2. The final output is 3.0, 11.0, 2,**

**Note that while Java outputs the decimal for both float and double values, it does not output the f for float values**

---

3. Which changes, when made independently, guarantee the following code snippet prints 100 at
runtime? (Choose all that apply.)

```java
List<Integer> data = new ArrayList<>();
IntStream.range(0, 100)
         .parallel()
         .forEach(s -> data.add(s));
System.out.println(data.size());
```

- [ ] A. Change data to an instance variable and mark it volatile.
- [x] B. Remove parallel() in the stream operation.
- [x] C. Change forEach() to forEachOrdered() in the stream operation.
- [ ] D. Change parallel() to serial() in the stream operation.
- [x] E. Wrap the lambda body with a synchronized block.
- [ ] F. The code snippet will always print 100 as is.

My Answer : A, E

**The code may print 100 without any changes, but since the data class is not thread-safe,**
**this behavior is not guaranteed. For this reason, option F is incorrect. Option A is also**
**incorrect, as volatile does not guarantee thread-safety.**

**Options B and C are correct, as they both cause the stream to apply the add() operation in a synchronized manner. Option D is incorrect, as serial() is not a stream method. Option E is correct. Synchronization will cause each thread to wait so that the List is modified one element at a time**

---

4. What is the output of this code?
```java
20: Predicate<String> empty = String::isEmpty;
21: Predicate<String> notEmpty = empty.negate();
22:
23: var result = Stream.generate(() -> "")
24:               .filter(notEmpty)
25:               .collect(Collectors.groupingBy(k -> k))
26:               .entrySet()
27:               .stream()
28:               .map(Entry::getValue)
29:               .flatMap(Collection::stream)
30:               .collect(Collectors.partitioningBy(notEmpty));
31: System.out.println(result);
```

- [ ] A. It outputs {}.
- [ ] B. It outputs {false=[], true=[]}.
- [ ] C. The code does not compile.
- [x] D. The code does not terminate.

My Answer: A

**the source is an infinite stream. The filter operation will check each element in turn to see whether any are not empty. While nothing passes the filter, the code does not terminate.**

---

5. What is the result of the following program?

```java
1: public class MathFunctions {
2:     public static void addToInt(int x, int amountToAdd) {
3:         x = x + amountToAdd;
4:     }
5:     public static void main(String[] args) {
6:         var a = 15;
7:         var b = 10;
8:         MathFunctions.addToInt(a, b);
9:        System.out.println(a);
		}
	 }
```

- [ ] A. 10
- [x] B. 15
- [ ] C. 25
- [ ] D. Compiler error on line 3
- [ ] E. Compiler error on line 8
- [ ] F. None of the above

**The value of a cannot be changed by the `addToInt()` method, no matter what the method does, because only a copy of the variable is passed into the parameter x. Therefore, a does not change, and the output on line 9 is 15 which is option B.**

---


6. Suppose that we have the following property files and code. What values are printed on lines
8 and 9, respectively?
**Penguin.properties**
name=Billy
age=1
**Penguin_de.properties**
name=Chilly
age=4
**Penguin_en.properties**
name=Willy

```java
5: Locale fr = new Locale("fr");
6: Locale.setDefault(new Locale("en", "US"));
7: var b = ResourceBundle.getBundle("Penguin", fr);
8: System.out.println(b.getString("name"));
9: System.out.println(b.getString("age"));
```

- [ ] A. Billy and 1
- [ ] B. Billy and null
- [x] C. Willy and 1
- [ ] D. Willy and null
- [ ] E. Chilly and null
- [ ] F. The code does not compile.

My Answer: F

**Since there is no match for French, the default locale is used. Line 8 finds a matching**
**key in the Penguin_en.properties file. Line 9 does not find a match in the**
**Penguin_en.properties file; therefore, it has to look higher up in the hierarchy to**
**Penguin.properties. This makes option C the answer**

---

7. What is guaranteed to be printed by the following code? (Choose all that apply.)

``` java
int[] array = {6, 9, 8}; System.out.println("B" + Arrays.binarySearch(array, 9)); System.out.println("C" + Arrays.compare(array, new int[]{6, 9, 8})); System.out.println("M" + Arrays.mismatch(array, new int[]{6, 9, 8}));
```

- [ ] A. B1
- [ ] B. B2
- [ ] C. C-1
- [x] D. C0
- [x] E. M-1
- [ ] F. M0
- [ ] G. The code does not compile.

My Answer: A

**The array is allowed to use an anonymous initializer because it is in the same line as**
**the declaration. The results of the binary search are undefined since the array is not sorted.**
**Since the question asks about guaranteed output, options A and B are incorrect.**

**Option D is correct because the compare() method returns 0 when the arrays are the same**
**length and have the same elements. Option E is correct because the mismatch() method**
**returns a -1 when the arrays are equivalent.**

---

8. Which functional interfaces complete the following code, presuming variable r exists?
(Choose all that apply.)
```java
6: x =  r.negate();
7: y = () -> System.out.println();
8: z = (a, b) -> a - b;
```


- [ ] `A. BinaryPredicate<Integer, Integer>`
- [ ] `B. Comparable<Integer>`
- [x] `C. Comparator<Integer>`
- [ ] `D. Consumer<Integer>`
- [x] `E. Predicate<Integer>`
- [x] `F. Runnable`
- [ ] `G. Runnable<Integer>`

My Answer: C, D

**note that option A is incorrect because the interface should be BiPredicate**
**and not BinaryPredicate. Line 6 requires you to know that negate() is a convenience**
**method on Predicate. This makes option E correct. Line 7 takes zero parameters and**
**doesn’t return anything, making it a Runnable. Remember that Runnable doesn’t use**
**generics. This makes option F correct. Finally, line 8 takes two parameters and returns an**
**int. Option C is correct. Comparable is there to mislead you since it takes only one parameter**
**in its single abstract method**

---

9. Suppose you have a module named com.vet. Where could you place the following
module-info.
java file to create a valid module?

```java
public module com.vet {
	exports com.vet;
}
```

- [ ] A. At the same level as the com folder
- [ ] B. At the same level as the vet folder
- [ ] C. Inside the vet folder
- [x] D. None of the above

My Answer: A

**If this were a valid module-info. java file, it would need to be placed at the root directory of the module, which is option A. However, a module is not allowed to use the public access modifier.**

---

10. What is the output of the following program? (Choose all that apply.)

```java
1: interface HasTail { private int getTailLength(); }
2: abstract class Puma implements HasTail {
3: String getTailLength() { return "4"; }
4: }
5: public class Cougar implements HasTail {
6: public static void main(String[] args) {
7: var puma = new Puma() {};

8: System.out.println(puma.getTailLength());
9: }
10: public int getTailLength(int length) { return 2; }
11: }
```

- [ ] A. 2
- [ ] B. 4
- [x] C. The code will not compile because of line 1.
- [ ] D. The code will not compile because of line 3.
- [ ] E. The code will not compile because of line 5.
- [ ] F. The code will not compile because of line 7.
- [ ] G. The code will not compile because of line 10.
- [ ] H. The output cannot be determined from the code provided.

My Answer: D, E

**The getTailLength() method in the interface is private; therefore, it must include**
**a body. For this reason, line 1 is the only line that does not compile and option C is correct.**
**Line 3 uses a different return type for the method, but since it is private in the interface, it**
**is not considered an override. Note that line 7 defines an anonymous class using the abstract**  **Puma parent class**



---

11. Which lines in Tadpole.java give a compiler error? (Choose all that apply.)

```java
// Frog.java
1: package animal;
2: public class Frog {
3: protected void ribbit() { }
4: void jump() { }
5: }
// Tadpole.java
1: package other;
2: import animal.*;
3: public class Tadpole extends Frog {
4: public static void main(String[] args) {
5: Tadpole t = new Tadpole();
6: t.ribbit();
7: t.jump();
8: Frog f = new Tadpole();
9: f.ribbit();
10: f.jump();
11: } }
```

- [ ] A. Line 5
- [ ] B. Line 6
- [x] C. Line 7
- [ ] D. Line 8
- [x] E. Line 9
- [x] F. Line 10
- [ ] G. All of the lines compile.

My Answer: G

**The jump() method has package access, which means it can be accessed only**
**from the same package. Tadpole is not in the same package as Frog, causing lines 7**
**and 10 to trigger compiler errors**

**The ribbit() method has protected access, which means it can only be accessed from a subclass reference or in the same package. Line 6 is fine because Tadpole is a subclass. Line 9 does not compile and our final answer is option E because the variable reference is to a Frog, which doesn’t grant access to the protected method**

---

12. Which of the following can fill in the blanks in order to make this code compile?
"_________"a  ="_________" .getConnection( url, userName, password);
"___________" b = a.prepareStatement(sql);
"________" c = b.executeQuery();
if (c.next()) System.out.println(c.getString(1));

- [x] `A. Connection, Driver, PreparedStatement, ResultSet`
- [ ] `B. Connection, DriverManager, PreparedStatement, ResultSet`
- [ ] `C. Connection, DataSource, PreparedStatement, ResultSet`
- [ ] `D. Driver, Connection, PreparedStatement, ResultSet`
- [ ] `E. DriverManager, Connection, PreparedStatement, ResultSet`
- [ ] `F. DataSource, Connection, PreparedStatement, ResultSet`

My Answer: B

**DataSource isn’t on the exam, so any question containing one is wrong. The key variables**
**used in running a query are Connection, PreparedStatement, and ResultSet.**
**A Connection is obtained through a DriverManager, making option B correct**

---

13. Which of the following statements can fill in the blank to make the code compile successfully?
(Choose all that apply.)

```java
Set<? extends RuntimeException> mySet = new ??? ();
```

- [ ] `A. HashSet<? extends RuntimeException>`
- [ ] `B. HashSet<Exception>`
- [x] `C. TreeSet<RuntimeException>`
- [x] `D. TreeSet<NullPointerException>`
- [ ] `E. None of the above`

My Answer: A, C

**The mySet declaration defines an upper bound of type RuntimeException.**
**This means that classes may specify RuntimeException or any subclass of**
**RuntimeException as the type parameter**

**Option A is incorrect because the wildcard cannot occur on the right side of the assignment**

---

14. Assume that birds.dat exists, is accessible, and contains data for a Bird object. What is
the result of executing the following code? (Choose all that apply.)

```java
1: import java.io.*;
2: public class Bird {
3: private String name;
4: private transient Integer age;
5:
6: // Getters/setters omitted
7:
8: public static void main(String[] args) {
9: try(var is = new ObjectInputStream(
10: new BufferedInputStream(
11: new FileInputStream("birds.dat")))) {
12: Bird b = is.readObject();
13: System.out.println(b.age);
14: } } }
```

- [ ] A. It compiles and prints 0 at runtime.
- [ ] B. It compiles and prints null at runtime.
- [ ] C. It compiles and prints a number at runtime.
- [x] D. The code will not compile because of lines 9–11.
- [x] E. The code will not compile because of line 12.
- [ ] F. It compiles but throws an exception at runtime.

My Answer: A, B

**Line 10 includes an unhandled checked `IOException`, while line 11 includes an**
**unhandled checked `FileNotFoundException`, making option D correct. Line 12 does not**
**compile because `is.readObject()` must be cast to a Bird object to be assigned to b. It**
**also does not compile because it includes two unhandled checked exceptions, `IOException`**
**and `ClassNotFoundException`, making option E correct. If a cast operation were added**
**on line 12 and the main() method were updated on line 8 to declare the various checked**

**exceptions, the code would compile but throw an exception at runtime since Bird does not**
**implement Serializable. Finally, if the class did implement Serializable, the program**
**would print null at runtime, as that is the default value for the transient field age.**

---

15. Which of the following are valid instance members of a class? (Choose all that apply.)
- [ ] `A. var var = 3;`
- [ ] `B. Var case = new Var();`
- [x] `C. void var() {}`
- [ ] `D. int Var() { var _ = 7; return _;}`
- [ ] `E. String new = "var";`
- [ ] `F. var var() { return null; }`

My Answer:  B, F

**Option A is incorrect because var is only allowed as a type for local variables, not instance**
**members. Options B and E are incorrect because new and case are reserved words**
**and cannot be used as identifiers. Option C is correct, as var can be used as a method name.**
**Option D is incorrect because a single underscore (_) cannot be used as an identifier. Finally,**
**option F is incorrect because var cannot be specified as the return type of a method**

---

16. Which is true if the table is empty before this code is run? (Choose all that apply.) 

```java
var sql = "INSERT INTO people VALUES(?, ?, ?)";
conn.setAutoCommit(false);
try (var ps = conn.prepareStatement(sql,
ResultSet.TYPE_SCROLL_SENSITIVE,
ResultSet.CONCUR_UPDATABLE)) {
ps.setInt(1, 1);
ps.setString(2, "Joslyn");
ps.setString(3, "NY");
ps.executeUpdate();
Savepoint sp = conn.setSavepoint();
ps.setInt(1, 2);
ps.setString(2, "Kara");
ps.executeUpdate();
conn. ??? ;
}
```

- [x] A. If the blank line contains rollback(), there are no rows in the table.
- [ ] B. If the blank line contains rollback(), there is one row in the table.
- [ ] C. If the blank line contains rollback(sp), there are no rows in the table.
- [x] D. If the blank line contains rollback(sp), there is one row in the table.
- [ ] E. The code does not compile.
- [ ] F. The code throws an exception because the second update does not set all the parameters.

My Answer:  B

**JDBC will use the existing parameter**
**set if you don’t replace it. This means Kara’s row will be set to use NY as the third parameter.**
**Rolling back to a savepoint throws out any changes made since. This leaves Joslyn and**
**eliminates Kara, making option D correct. Rolling back without a savepoint brings us back**
**to the beginning of the transaction, which is option A**

---

17. Which is true if the contents of path1 start with the text Howdy? (Choose two.)

```java
System.out.println(Files.mismatch(path1,path2));
```

- [ ] A. If path2 doesn’t exist, the code prints -1.
- [ ] B. If path2 doesn’t exist, the code prints 0.
- [x] C. If path2 doesn’t exist, the code throws an exception.
- [x] D. If the contents of path2 start with Hello, the code prints -1.
- [ ] E. If the contents of path2 start with Hello, the code prints 0.
- [ ] F. If the contents of path2 start with Hello, the code prints 1.

My Answer: C, D

**Option C is correct as mismatch() throws an exception if the files do not exist unless**
**they both refer to the same file. Additionally, option F is correct because the first index that**
**differs is returned, which is the second character. Since Java uses zero-based**
**indexes, this is 1.**

---

18. Which of the following types can be inserted into the blank to allow the program to compile successfully? (Choose all that apply.)

```java
1: import java.util.*;
2: final class Amphibian {}
3: abstract class Tadpole extends Amphibian {}
4: public class FindAllTadpoles {
5: public static void main(String... args) {
6: var tadpoles = new ArrayList<Tadpole>();
7: for (var amphibian : tadpoles) {
8:  ??? tadpole = amphibian;
9: } } }
```

- [ ] `A. List<Tadpole>`
- [ ] `B. Boolean`
- [ ] `C. Amphibian`
- [ ] `D. Tadpole`
- [ ] `E. Object`
- [x] `F. None of the above`

**The Amphibian class is marked final, which means line 3 triggers a compiler error and**
**option F is correct.**

---

19. What is the result of compiling and executing the following program?

```java
1: public class FeedingSchedule {
2: public static void main(String[] args) {
3: var x = 5;
4: var j = 0;

5: OUTER: for (var i = 0; i < 3;)
6: INNER: do {
7: i++;
8: x++;
9: if (x> 10) break INNER;
10: x += 4;
11: j++;
12: } while (j <= 2);
13: System.out.println(x);
14: } }
```

- [ ] A. 10
- [ ] B. 11
- [x] C. 12
- [ ] D. 17
- [ ] E. The code will not compile because of line 5.
- [ ] F. The code will not compile because of line 6.

My Answer: 11

**On the first iteration of the outer loop, i is 0, so the loop continues.**
- **On the first iteration of the inner loop, i is updated to 1 and x to 6. The if statement**
**branch is not executed, and x is increased to 10 and j to 1.**
- **On the second iteration of the inner loop (since j = 1 and 1 <= 2), i is updated to 2**
**and x to 11. At this point, the if branch will evaluate to true for the remainder of**
**the program run, which causes the flow to break out of the inner loop each time it**
**is reached.**
- **On the second iteration of the outer loop (since i = 2), i is updated to 3 and x to 12. As**
**before, the inner loop is broken since x is still greater than 10.**
- **On the third iteration of the outer loop, the outer loop is broken, as i is already not less**
**than 3. The most recent value of x, 12, is output, so the answer is option C.**

---

20. When printed, which String gives the same value as this text block?

```java
var pooh = """
"Oh, bother." -Pooh
""".indent(1);
System.out.print(pooh);
```

- [ ] `A. "\n\"Oh, bother.\" -Pooh\ n"`
- [ ] `B. "\n \"Oh, bother.\" -Pooh\ n"`
- [x] `C. " \"Oh, bother.\" -Pooh\ n"`
- [ ] `D. "\n\"Oh, bother.\" -Pooh"`
- [ ] `E. "\n \"Oh, bother.\" -Pooh"`
- [ ] `F. " \"Oh, bother.\" -Pooh"`
- [ ] `G. None of the above`

My Answer: G

**First, note that the text block has the closing """ on a separate line, which means there**
**is a new line at the end and rules out options D, E, and F. Additionally, text blocks don’t**
**start with a new line, ruling out options A and B**

---

21. A(n) ???  module always contains a module-info. java file, while a(n) ??? module always exports all its packages to other modules.

- [ ] A. automatic, named
- [ ] B. automatic, unnamed
- [x] C. named, automatic
- [ ] D. named, unnamed
- [ ] E. unnamed, automatic
- [ ] F. unnamed, named
- [ ] G. None of the above

**Only named modules are required to have a module-info. java file, ruling out options**
**A, B, E, and F. Unnamed modules are not readable by any other types of modules, ruling**
**out option D. Automatic modules always export all packages to other modules, making the**
**answer option C.**

---

22. What is the result of the following code?
```java
22: var treeMap = new TreeMap<Character, Integer>();
23: treeMap.put('k', 1);
24: treeMap.put('k', 2);
25: treeMap.put('m', 3);
26: treeMap.put('M', 4);
27: treeMap.replaceAll((k, v) -> v + v);
28: treeMap.keySet()
29: .forEach(k ->
System.out.print(treeMap.get(k)));
```


- [ ] A. 268
- [ ] B. 468
- [ ] C. 2468
- [ ] D. 826
- [x] E. 846
- [ ] F. 8246
- [ ] G. None of the above

My Answer: G

**When the same key is put into a Map, it overrides the original value. This means that line**
**23 could be omitted and the code would be the same, and there are only three key/value**
**pairs in the map. TreeMap sorts its keys, making the order M followed by k followed by m.**
**Remember that natural sort ordering has uppercase before lowercase. The replaceAll()**
**method runs against each element in the map, doubling the value**

---

23. Which of the following lines can fill in the blank to print true? (Choose all that apply.)

```java
10: public static void main(String[] args) {
11: System.out.println(test( ??? ));
12: }
13: private static boolean test(Function<Integer, Boolean> b) {
14: return b.apply(5);
15: }
```

- [ ] `A. i::equals(5)`
- [ ] `B. i -> {i == 5;}`
- [x] `C. (i) -> i == 5`
- [ ] `D. (int i) -> i == 5`
- [ ] `E. (int i) -> {return i == 5;}`
- [x] `F. (i) -> {return i == 5;}`

**A looks like a method reference. However, it doesn’t call a valid method, nor**
**can method references take parameters. The Predicate interface takes a single parameter**
**and returns a boolean. Lambda expressions with one parameter are allowed to omit**
**the parentheses around the parameter list, making option C correct.**

**The return statement**
**is optional when a single statement is in the body, making option F correct. Option**
**B is incorrect because a return statement must be used if braces are included around the**
**body. Options D and E are incorrect because the type is Integer in the predicate and int**
**in the lambda. Autoboxing works for collections, not inferring predicates. If these two were**
**changed to Integer, they would be correct.**

---

24. How many times is the word true printed?

```java
var s1 = "Java";
var s2 = "Java";
var s3 = s1.indent(1).strip();
var s4 = s3.intern();
var sb1 = new StringBuilder();
sb1.append("Ja").append("va");


System.out.println(s1 == s2);
System.out.println(s1.equals(s2));
System.out.println(s1 == s3);
System.out.println(s1 == s4);
System.out.println(sb1.toString() == s1);
System.out.println(sb1.toString().equals(s1));
```

- [ ] A. Once
- [ ] B. Twice
- [ ] C. Three times
- [x] D. Four times
- [ ] E. Five times
- [ ] F. The code does not compile.

My Answer: B

**String literals are used from the string pool. This means that s1 and s2 refer to the**
**same object and are equal. Therefore, the first two print statements print true. While the**
**indent() and strip() methods create new String objects and the third statement prints**
**false, the intern() method reverts the String to the one from the string pool. Therefore,**
**the fourth print statement prints true. The fifth print statement prints false because**
**toString() uses a method to compute the value, and it is not from the string pool. The**
**final print statement again prints true because equals() looks at the values of String**
**objects**

---

25. What is the output of the following program?

```java
1: class Deer {
2: public Deer() {System.out.print("Deer");}
3: public Deer(int age) {System.out.print("DeerAge");}
4: protected boolean hasHorns() { return false; }
5: }
6: public class Reindeer extends Deer {
7: public Reindeer(int age) {System.out.print("Reindeer");}
8: public boolean hasHorns() { return true; }
9: public static void main(String[] args) {
10: Deer deer = new Reindeer(5);
11: System.out.println("," + deer.hasHorns());
12: } }
```

- [ ] A. ReindeerDeer,false
- [ ] B. DeerAgeReindeer,true
- [x] C. DeerReindeer,true
- [ ] D. DeerReindeer,false
- [ ] E. ReindeerDeer,true
- [ ] F. DeerAgeReindeer,false
- [ ] G. The code will not compile because of line 4.
- [ ] H. The code will not compile because of line 12.

My Answer: B

**The Reindeer object is instantiated using the constructor that takes an int value. Since**
**there is no explicit call to the parent constructor, the compiler inserts super() as the first**
**line of the constructor on line 7. The parent constructor is called, and Deer is printed on line**
2. **The flow returns to the constructor on line 7, with Reindeer being printed. Next, the**
**hasHorns() method is called. The reference type is Deer, and the underlying object type**
**is Reindeer. Since Reindeer correctly overrides the hasHorns() method, the version in**
**Reindeer is called, with line 11 printing ,true. Therefore, option C is correct**

---

26. Which of the following are true? (Choose all that apply.)

```java
private static void magic(Stream<Integer> s) {
Optional o = s
.filter(x ->
x < 5)
.limit(3)
.max((x, y) ->
x-y);
System.out.println(o.get());
}
```

- [ ] `A. magic(Stream.empty()); runs infinitely.`
- [x] `B. magic(Stream.empty()); throws an exception.`
- [ ] `C. magic(Stream.iterate(1, x -> x++)); runs infinitely.`
- [ ] `D. magic(Stream.iterate(1, x -> x++)); throws an exception.`
- [ ] `E. magic(Stream.of(5, 10)); runs infinitely.`
- [x] `F. magic(Stream.of(5, 10)); throws an exception.`
- [ ] `G. The method does not compile.`

My Answer: D, F

**Calling get() on an empty Optional causes an exception to be thrown, making**
**option B correct. Option F is also correct because filter() makes the Optional empty**
**before it calls get(). Option C is incorrect because the infinite stream is made finite by the**
**intermediate limit() operation. Options A and E are incorrect because the source streams**
**are not infinite.**

---

27. Assuming the following declarations are top-level types declared in the same file, which successfully compile? (Choose all that apply.)

```java
record Music() {
final int score = 10;
}
record Song(String lyrics) {
Song {
this.lyrics = lyrics + "Hello World";
}
}
sealed class Dance {}
record March() {
@Override String toString() { return null; }
}
class Ballet extends Dance {}
```

- [ ] A. Music
- [ ] B. Song
- [x] C. Dance
- [ ] D. March
- [ ] E. Ballet
- [ ] F. None of them compile.

**Music does not compile because records cannot include instance variables not listed in**
**the declaration of the record, as it could break immutability. Song does not compile because**
**a compact constructor cannot set an instance variable. The record would compile if this**
**were removed from the compact constructor, as compact constructors can modify input**
**parameters. March does not compile because it is an invalid override; it reduces the visibility**
**of the toString() method from public to package access. Ballet does not compile**
**because the subclass of a sealed class must be marked final, sealed, or non-sealed.**
**Since the only one that compiles is Dance, option C is the answer.**

---

28. Which of the following expressions compile without error? (Choose all that apply.)

- [ ] `A. int monday = 3 + 2.0;`
- [x] `B. double tuesday = 5_6L;`
- [ ] `C. boolean wednesday = 1 > 2 ? !true;`
- [x] `D. short thursday = (short)Integer.MAX_VALUE;`
- [ ] `E. long friday = 8.0L;`
- [ ] `F. var saturday = 2_.0;`
- [ ] `G. None of the above`

My Answer: E, F

**Option A does not compile, as the expression 3 + 2.0 is evaluated as a double,**
**and a double requires an explicit cast to be assigned to an int. Option B compiles without**
**issue, as a long value can be implicitly cast to a double. Option C does not compile**
**because the ternary operator (? :) is missing a colon (:), followed by a second expression.**
**Option D is correct. Even though the int value is larger than a short, it is explicitly cast to**
**a short, which means the value will wrap around to fit in a short. Option E is incorrect,**
**as you cannot use a decimal (.) with the long (L) postfix. Finally, option F is incorrect, as an**
**underscore cannot be used next to a decimal point.**

---

29. What is the result of executing the following application?

```java
final var cb = new CyclicBarrier(3,
() ->
System.out.println("Clean!")); // u1
ExecutorService service = Executors.newSingleThreadExecutor();
try {
IntStream.generate(() ->
1)
.limit(12)
.parallel()
.forEach(i ->
service.submit(() ->
cb.await())); // u2
} finally { service.shutdown(); }
```

- [ ] A. It outputs Clean! at least once.
- [ ] B. It outputs Clean! exactly four times.
- [ ] C. The code will not compile because of line u1.
- [ ] D. The code will not compile because of line u2.
- [ ] E. It compiles but throws an exception at runtime.
- [x] F. It compiles but waits forever at runtime.

**The code compiles without issue. The key to understanding this code is to notice that our**
**thread executor contains only one thread, but our CyclicBarrier limit is 3. Even though**
**12 tasks are all successfully submitted to the service, the first task will block forever on the**
**call to await(). Since the barrier is never reached, nothing is printed, and the program**
**hangs, making option F correct.**

---

30.  Which statement about the following method is true?

```java
5: public static void main(String... unused) {
6: System.out.print("a");
7: try (StringBuilder reader = new StringBuilder()) {
8: System.out.print("b");
9: throw new IllegalArgumentException();
10: } catch (Exception e || RuntimeException e) {
11: System.out.print("c");
12: throw new FileNotFoundException();
13: } finally {
14: System.out.print("d");
15: } }
```

- [ ] A. It compiles and prints abc.
- [ ] B. It compiles and prints abd.
- [ ] C. It compiles and prints abcd.
- [ ] D. One line contains a compiler error.
- [ ] E. Two lines contain a compiler error.
- [x] F. Three lines contain a compiler error.
- [ ] G. It compiles but prints an exception at runtime.

My Answer: C

**Line 5 does not compile as the FileNotFoundException thrown on line 12 is not handled**
**or declared by the method. Line 7 does not compile because StringBuilder does not**
**implement AutoCloseable and is therefore not compatible with a try-with- resource**
**statement. Finally, line 10 does not compile as RuntimeException is a subclass of Exception**
**in the multi-catch block, making it redundant. Since this method contains three compiler**
**errors, option F is the correct answer.**

---

# Chapter 1 - Building Blocks #Chapter

## Learning about the Environment

### Major Components of Java

The Java Development Kit (JDK) contains the minimum software you need to do Java development. Key commands include:

- `javac`: Converts .java source files into .class bytecode
- `java`: Executes the program
- `jar`: Packages files together
- `javadoc`: Generates documentation

The `javac` program generates instructions in a special format called bytecode that the java command can run.
Then java launches the Java Virtual Machine (JVM) before running the code The JVM knows how to run bytecode on the actual machine it is on.
think of the JVM as a special magic box on your machine that knows how to run your .class file within your particular operating system and hardware.

---

**Where Did the JRE Go?**

In Java 8 and earlier, you could download a Java Runtime Environment (JRE) instead of the full JDK. The JRE was a subset of the JDK that was used for running a program but could not compile one.

Now, people can use the full JDK when running a Java program. Alternatively, developers can supply an executable that contains the required pieces that would have been in the JRE.

When writing a program, there are common pieces of functionality and algorithms that developers need. Java comes with a large suite of application programming interfaces (APIs) that you can use.

For example, there is a `StringBuilder` class to create a large `String` and a method in `Collections` to sort a list. When writing a program, it is helpful to determine what pieces of your assignment can be accomplished by existing APIs.

---

### Downloading a JDK

Every six months, Oracle releases a new version of Java.  The rules and behavior can change with later versions of Java. There are many JDKs available, the most popular of which, besides Oracle’s JDK, is OpenJDK.

Many versions of Java include preview features that are off by default but that you can enable. Preview features are not on the exam.

---
**Check Your Version of Java**

```shell
javac -version
java -version
```

---


## Understanding the Class Structure

In Java programs, classes are the basic building blocks. When defining a class, you describe all the parts and characteristics of one of those building blocks.

To use most classes, you have to create objects.  ==**An object is a runtime instance of a class in memory.**== An object is often referred to as an instance since it represents a single representation of the class.

All the various objects of all the different classes represent the state of your program. ==**A reference is a variable that points to an object.**==
### Fields and Methods

Java classes have ==**two primary elements**==: ==**methods**==, often called functions or procedures in other languages, and ==**fields**==, more generally known as variables. Together these are called the members of the class.

Variables hold the state of the program, and methods operate on that state. If the change is important to remember, a variable stores that change.

The simplest Java class you can write looks like this:

```java
1: public class Animal {
2: }
```

Line 1 includes the `public` keyword, which allows other classes to use it. The `class` keyword indicates you’re defining a class. Animal gives the name of the class.

```java
1: public class Animal {
2: String name;
3: }
```

On line 2, we define a variable named name. We also declare the type of that variable to be `String`.

```java
1: public class Animal {
2: String name;
3: public String getName() {
4: return name;
5: }
6: public void setName(String newName) {
7: name = newName;
8: }
9: }
```

The `setName()` method has one parameter named `newName`, and it is of type String. This means the caller should pass in one `String` parameter and expect nothing to be returned.

==**The method name and parameter types are called the method signature.**==

```java
public int numberVisitors(int month) {
	return 10;
}
```

The method name is `numberVisitors`. There’s one parameter named month, which is of type `int`, which is a numeric type. the method signature is **`numberVisitors(int).`**

---

```java
// Most of the time, each Java class is defined in its own .java file.  
// A top-level class is often public, which means any code can call it.  
// If you do have a public type, it needs to match the filename.  
  
/*public */ class AnimalV2 { // ONLY AnimalV2 class can be public in this source file.  
    private String name;  
}  
  
// You can even put two types in the same file.  
// When you do so, at most one of the toplevel types in the file is allowed to be public.  
class Animal2 {  
}  
  
// public class Animal3{} // Compile Error
```

---

### Comments

Another common part of the code is called a comment. Because comments aren’t executable code, you can place them in many places. Comments can make your code easier to read.

There are three types of comments in Java.  **single-line comment**:

```java
// comment until end of line
```

A single-line comment begins with two slashes. The compiler ignores anything you type after that on the same line. **multiple-line comment**

```java
/* Multiple
* line comment
*/
```

A multiple-line comment includes anything starting from the symbol /* until the symbol  * /.
**Javadoc comment**

```go
/**
* Javadoc multiple-line
comment
* @author Jeanne and Scott
*/
```

This comment is similar to a multiline comment, except it starts with `/**`.   This special syntax tells the Javadoc tool to pay attention to the comment. Javadoc comments have a specific structure that the Javadoc tool knows how to read.

```java
/*
* // anteater
*/
// bear
// // cat
// /* dog */
/* elephant */
/*
* /* ferret */
*/
```

The line with ferret is interesting in that it doesn’t compile. Everything from the first /* to the first */ is part of the comment which means the compiler sees something like this:  `/* * /  */` There is an extra `*/`. That’s not valid syntax
### Classes and Source Files

Most of the time, each Java class is defined in its own .java file.  A top-level type is a data structure that can be defined independently within a source file. A top-level class is often `public`, which means any code can call it. Interestingly, Java does not require that the type be `public`

```java
1: class Animal {
2: String name;
3: }
```

You can even put two types in the same file. When you do so, ==**at most one of the top-level types in the file is allowed to be public**==

```java
1: public class Animal {
2: private String name;
3: }
4: class Animal2 {} // Bold
```

==**If you do have a public type, it needs to match the filename**. The declaration public class Animal2 would not compile in a file named **`Animal.java`**.==

## Writing a `main()` Method

A Java program begins execution with its `main()` method.  The `main()` method is often called an entry point into the program, because it is the starting point that the JVM looks for when it begins running a new program.
### Creating a main() Method

```java
1: public class Zoo {
2: public static void main(String[] args) { // Bold
3: System.out.println("Hello World");
4: }
5: }
```

To compile and execute this code, type it into a file called Zoo.java and execute the following:

```shell
javac Zoo.java
java Zoo
```

To compile Java code with the `javac` command, the file must have the extension .java
The name of the file must match the name of the public class.  The result is a file of bytecode with the same name but with a .class filename extension.

To keep things simple for now, we follow this subset of the rules:
- ==**Each file can contain only one public class.**==
- ==**The filename must match the class name, including case, and have a .java extension.**==
- ==**If the Java class is an entry point for the program, it must contain a valid main() method.**==

review the words in the `main()` method’s signature, one at a time. 

- ==**The keyword `public` is what’s called an access modifier. It declares this method’s level of exposure to potential callers in the program. Naturally, public means full access from anywhere in the program.**==

- ==**The keyword `static` binds a method to its class so it can be called by just the class name  Java doesn’t need to create an object to call the main() method**== 

- ==**The keyword `void` represents the return type. A method that returns no data returns control to the caller silently.  In general, it’s good practice to use `void` for methods that change an object’s state. In that sense, the `main()` method changes the program state from started to finished.**==

- ==**Finally, the `main()` method’s parameter list, represented as an array of `java.lang.String` objects. can use any valid variable name along with any of these three formats:**==

- ==**`String[] args`**==
- ==**`String options[]`**==
- ==**`String... friends`**==

The variable name args is common because it hints that this list contains values that were read in (arguments) when the JVM started.

---
**Optional Modifiers in main() Methods** #TIP

While most modifiers, such as public and static, are required for main() methods, there are some optional modifiers allowed.

```java
public final static void main(final String[] args) {}
```

both **final** modifiers are optional, and the main() method is a valid entry point with or without them.

---
### Passing Parameters to a Java Program

```java
public class Zoo {
public static void main(String[] args) {
System.out.println(args[0]);
System.out.println(args[1]);
}
}
```

The code args[0] accesses the first element of the array.
To run:
```bash
javac Zoo.java
java Zoo Bronx Zoo
```

The output: 

```
Bronx
Zoo
```

The program correctly identifies the first two “words” as the arguments. Spaces are used to separate the arguments. **==want spaces inside an argument, you need to use quotes==**

```shell
javac Zoo.java
java Zoo "San Diego" Zoo
```

what happens if you don’t pass in enough arguments?

```shell
javac Zoo.java
java Zoo Zoo
```

Reading args[0] goes fine, and Zoo is printed out. Then Java panics. There’s no second argument! Java prints out an exception telling you it has no idea what to do with this argument at position 1.

```java
Zoo
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException:
Index 1 out of bounds for length 1
at Zoo.main(Zoo.java:4)
```

To review, the JDK contains a compiler. Java class files run on the JVM and therefore run on any machine with Java rather than just the machine or operating system they happened to have been compiled on.

---

**Single-File Source-Code**

```shell
java Zoo.java Bronx Zoo
```

There is a key difference here. When compiling first, you omitted the .java extension when running java. When skipping the explicit compilation step, you include this extension. This feature is called launching single-file source-code programs and is useful for testing or for small programs.

---
## Understanding Package Declarations and Imports


Java comes with thousands of built-in classes, and there are countless more from developers. With all those classes, Java needs a way to organize them. It handles this in a way similar to a file cabinet.

Java puts classes in packages. These are logical groupings for classes. Java needs you to tell it which packages to look in to find code.

```java
public class NumberPicker {
public static void main(String[] args) {
Random r = new Random(); // DOES NOT COMPILE
System.out.println(r.nextInt(10));
}
}
```

the output: 

```java
error: cannot find symbol
```

This error could mean you made a typo in the name of the class. The other cause of this error is omitting a needed `import` statement. A statement is an instruction, and import statements tell Java which packages to look in for classes. Since you didn’t tell Java where to look for `Random`, it has no clue.

```java
import java.util.Random; // import tells us where to find Random
public class NumberPicker {
public static void main(String[] args) {
Random r = new Random();
System.out.println(r.nextInt(10)); // a number 0-9
}
}
```

### Packages
Java classes are grouped into packages. The `import` statement tells the compiler which package to look in to find a class.

==**Java only looks for class names in the package.**== Package names are hierarchical. The rule for package names is that they are mostly letters or numbers separated by periods `(.)`. Technically, you’re allowed a couple of other characters between the periods` (.)`.

### Wildcards

Classes in the same package are often imported together. You can use a shortcut to import all the classes in a package.

```java
import java.util.*; // imports java.util.Random among other things
public class NumberPicker {
public static void main(String[] args) {
Random r = new Random();
System.out.println(r.nextInt(10));
}
}
```

The `*` is a wildcard that matches all classes in the package.  Every class in the` java.util` package
is available to this program when Java compiles it. ==**The `import` statement doesn’t bring in child packages, fields, or methods; it imports only classes directly under the package**==

Example to use the class `AtomicInteger`

```java
import java.util.*;
import java.util.concurrent.*;
import java.util.concurrent.atomic.*;
```

Only the last import allows the class to be recognized because child packages are not included with the first two.

Might think that including so many classes slows down your program execution, but it doesn’t. The compiler figures out what’s actually needed.

- Listing the classes used makes the code easier to read
- Using the wildcard can shorten the import list.

### Redundant Imports

==**There’s one special package in the Java world called `java.lang`. This package is special in that it is automatically imported.**==

```java
1: import java.lang.System;
2: import java.lang.*;
3: import java.util.Random;
4: import java.util.*;
5: public class NumberPicker {
6: public static void main(String[] args) {
7: Random r = new Random();
8: System.out.println(r.nextInt(10));
9: }
10: }
```

How many of the imports do you think are redundant?  The answer is that three of the imports are redundant. Lines 1 and 2 are redundant because everything in `java.lang` is automatically imported. Line 4 is also redundant in this example because Random is already imported from `java.util.Random`

Another case of redundancy involves importing a class that is in the same package as the class importing it. Java automatically looks in the current package for other classes.

```java
public class InputImports {
public void read(Files files) {
Paths.get("name");
}
}
```

Which import statements do you think would work to get this code to compile?

There are two possible answers. The shorter one is to use a wildcard to import both at the same time.

```java
import java.nio.file.*;
```

The other answer is to import both classes explicitly.

```java
import java.nio.file.Files;
import java.nio.file.Paths;
```

Some imports that don't work

```java
import java.nio.*; // NO GOOD -a wildcard only matches
// class names, not "file.Files"
import java.nio.*.*; // NO GOOD -you can only have one wildcard
// and it must be at the end
import java.nio.file.Paths.*; // NO GOOD -you cannot import methods
// only class names
```

### Naming Conflicts

One of the reasons for using packages is so that class names don’t have to be unique across all of Java. This means you’ll sometimes want to import a class that can be found in multiple places. A common example of this is the Date class. Java provides implementations of `java.util.Date` and `java.sql.Date`. What import statement can we use if we want the `java.util.Date` version?

```java
public class Conflicts {
Date date;
// some more code
}
```

write either  `import java.util.*;` or  `import java.util.Date;`

The tricky cases come about when other imports are present. 

```java
import java.util.*;
import java.sql.*; // causes Date declaration to not compile
```

When the class name is found in multiple packages, Java gives you a compiler error.

```java
import java.util.Date;
import java.sql.*;
```

now it works! If you explicitly import a class name, it takes precedence over any wildcards present. 

 **==If you specifically mention the name of a class when importing in programming, it's more important than using a general import with a wildcard `(*)`. The specific import has priority.==**

What does Java do with “ties” for precedence? 

```java
import java.util.Date;
import java.sql.Date;
```

Java is smart enough to detect that this code is no good. As a programmer, you’ve claimed to explicitly want the default to be both the `java.util.Date` and` java.sql.Date` implementations. Because there can’t be two defaults, the compiler tells you the imports are **ambiguous**.

---
**If You Really Need to Use Two Classes with the Same Name**

you can pick one to use in the import statement and use the other’s fully qualified class name. Or you can drop both import statements and ==**always use the fully qualified class name.**==

```java
public class Conflicts {
java.util.Date date;
java.sql.Date sqlDate;
}
```

---
### Creating a New Package

**The default package**. This is a special unnamed package that you should use only for throwaway code. You can tell the code is in the default package, because there’s no package name. In real life, always name your packages to avoid naming conflicts and to allow others to reuse your code.

```java
package packageb;
import packagea.ClassA; // Bold
public class ClassB {
public static void main(String[] args) {
ClassA a; // Bold
System.out.println("Got it");
}
}
```

When you run a Java program, Java knows where to look for those package names.
### Compiling and Running Code with Packages 

| Step | Windows                  | Mac/Linux                 |
|------|--------------------------|---------------------------|
| 1.   | Create first class.      | Create first class.       |
|      | `C:\temp\packagea\`      | `/tmp/packagea/`          |
|      | `ClassA.java`            | `ClassA.java`             |
|      | `/tmp/packagea/ClassA.java`|                           |
| 2.   | Create second class.     | Create second class.      |
|      | `C:\temp\packageb\`      | `/tmp/packageb/`          |
|      | `ClassB.java`            | `ClassB.java`             |
|      | `/tmp/packageb/ClassB.java`|                           |
| 3.   | Go to directory.         | Go to directory.          |
|      | `cd C:\temp`             | `cd /tmp`                 |

To compile, type the following command:
```shell
javac packagea/ClassA.java packageb/ClassB.java
```

---
**Compiling with Wildcards**
```shell
javac packagea/*.java packageb/*.java
```

However, you cannot use a wildcard to include subdirectories. If you were to write `javac *.java`, the code in the packages would not be picked up.

---

can run it by typing the following command:

```shell
java packageb.ClassB
```

we typed `ClassB` rather than `ClassB.class`. As discussed earlier, you don’t pass the extension when running  a program.

![[Pasted image 20240109140348.png]]
### Compiling to Another Directory

By default, the javac command places the compiled classes in the same directory as the
source code. It also provides an option to place the class files into a different directory. The
`-d` option specifies this target directory.


---
**Note**
Java options are case sensitive. This means you cannot pass -D instead of -d.

---

```shell
javac -d classes packagea/ClassA.java packageb/ClassB.java
```

Where to create the file classes`/packagea/ClassA.class.` The package structure is preserved under the requested target directory.

![[Pasted image 20240109140649.png]]

To run the program, you specify the classpath so Java knows where to find the classes.
There are three options you can use. All three of these do the same thing:

- **`java -cp classes packageb.ClassB`** 
- **`java -classpath classes packageb.ClassB`**
- **`java -- class- path classes packageb.ClassB`**

Notice that the last one requires two dashes (-- ), while the first two require one dash (-).

### Compiling with JAR Files

A Java archive (JAR) file is like a ZIP file of mainly Java class files.  On Windows, you type the following:

```shell
java -cp ".;C:\temp\someOtherLocation;c:\temp\myJar.jar" myPackage.MyClass
```

when you’re compiling, you can use a wildcard `(*)` to match all the JARs in a directory.

```java
java -cp "C:\temp\directoryWithJars\*" myPackage.MyClass
```

This command will add to the classpath all the JARs that are in `directoryWithJars`. It won’t include any JARs in the classpath that are in a subdirectory of `directoryWithJars`.

### Creating a JAR File

use the jar command. The simplest commands create a jar containing the files in the current directory. You can use the short or long form for each option.

```shell
jar -cvf myNewFile.jar .
jar --create--verbose--filemyNewFile.jar .
```

Alternatively, you can specify a directory instead of using the current directory.

```java
jar -cvf myNewFile.jar -C dir .
```

| Option     | Description                                   |
|------------|-----------------------------------------------|
| `-c`       | `--create`                                    |
|            | Creates a new JAR file                         |
| `-v`       | `--verbose`                                   |
|            | Prints details when working with JAR files    |
| `-f`       | `<fileName>`                                  |
|            | JAR filename                                  |
| `-C`       | `<directory>`                                 |
|            | Directory containing files to be used to create the JAR |

### Ordering Elements in a Class

Comments can go anywhere in the code.

| **Element**                  | **Example**                | **Required?** | **Where does it go?**                                |
|--------------------------|------------------------|-----------|--------------------------------------------------|
| **Package declaration**      | **`package abc;`**         | **No**        | **First line in the file (excluding comments or blank lines)** |
| **Import statements**        | **`import java.util.*;`**  | **No**        | **Immediately after the package (if present)**        |
| **Top-level type declaration**| **`public class C`**       | **Yes**       | **Immediately after the import (if any)**            |
| **Field declarations**       | **`int value;`**           | **No**        | **Any top-level element within a class**              |
| **Method declarations**      | **`void method()`**        | **No**        | **Any top-level element within a class**              |
**A Few Example**

**Good**

```java
package structure; // package must be first non-comment
import java.util.*; // import must come after package
public class Meerkat { // then comes the class
double weight; // fields and methods can go in either order
public double getWeight() {
return weight; }
double height; // another field -they don't need to be together
}
```

```java
/* header */
package structure;
// class Meerkat
public class Meerkat { }
```

**Bad**
```java
import java.util.*;
package structure; // DOES NOT COMPILE
String name; // DOES NOT COMPILE
public class Meerkat { } // DOES NOT COMPILE
```

There are two problems here. One is that the package and import statements are reversed. Although both are optional, package must come before `import` if present.
The other issue is that a field attempts a declaration outside a class. This is not allowed. Fields and methods must be within a class.
## Creating Objects

an object is an instance of a class
### Calling Constructors

To create an instance of a class, all you have to do is write new before the class name and add parentheses after it.

```java
Park p = new Park();
```

First you declare the type that you’ll be creating (`Park`) and give the variable a name (`p`). This gives Java a place to store a reference to the object.  Then you write `new Park()` to actually create the object.

`Park()` looks like a method since it is followed by parentheses. It’s called a **constructor**, which is a special type of method that creates a new object.

```java
public class Chick {
public Chick() { // Chick Bold
System.out.println("in constructor");
}
}
```

==***There are two key points to note about the constructor:***==
- ==***the name of the constructor matches the name of the class***==
- ==***there’s no return type***==

```java
public class Chick {
public void Chick() { } // NOT A CONSTRUCTOR
}
```

==**When you see a method name beginning with a capital letter and having a return type,**==
==**pay special attention to it. It is not a constructor since there’s a return type. It’s a regular**==
==**method that does compile but will not be called when you write new `Chick()`.**== #TIP 

The purpose of a constructor is to initialize fields,  Another way to initialize fields is to do so directly on the line on which they’re declared.

```java
public class Chicken {
int numEggs = 12; // initialize on line
String name;
public Chicken() {
name = "Duke"; // initialize in constructor
}
}
```

For most classes, the compiler will supply a “do nothing” default constructor for you.
### Reading and Writing Member Fields

It’s possible to read and write instance variables directly from the caller.

```java
public class Swan {
int numberEggs; // instance variable
public static void main(String[] args) {
Swan mother = new Swan();
mother.numberEggs = 1; // set variable
System.out.println(mother.numberEggs); // read variable
}
}
```

can even read values of already initialized fields on a line initializing a new field:

```java
1: public class Name {
2: String first = "Theodore"; // Write
3: String last = "Moose"; // Write
4: String full = first + last; // Read
5: }
```
### Executing Instance Initializer Blocks

The code between the braces (sometimes called “inside the braces”) is called a code block. Anywhere you see braces is a code block.

Sometimes code blocks are inside a method. These are run when the method is called.
Other times, ==**code blocks appear outside a method. These are called instance initializers.**==

```java
1: public class Bird { // Class Definition
2: public static void main(String[] args) { // Method Declaration
3: { System.out.println("Feathers"); } // Inner Block
4: }
5: { System.out.println("Snowy"); } // Instance initializer
6: }
```

There are four code blocks in this example: a class definition, a method declaration, an inner block, and an instance initializer.

When you’re counting ==**instance initializers cannot exist inside of a method**==. Line 5 is an instance initializer, with its braces outside a method.
### Following the Order of Initialization

This is simply the order in which different methods, constructors, or blocks are called when an instance of the class is created.

| Order No. | Order of Initialization            | Description                                                                                      | Simple Example                                   |
|-----------|-------------------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------|
| 1         | Static Variables Initialization | Static variables are initialized first, either at the time of declaration or in a static block.  | `static int staticVariable = 42;`                |
| 1         | Static Initialization Blocks    | Static initialization blocks are executed in the order they appear in the class after static variable initialization. | ```static { /* initialization code */ }``` |
| 2         | Instance Variables Initialization | Instance variables are initialized next, either at the time of declaration or in an instance initialization block. | `int instanceVariable = 10;`                     |
| 2         | Instance Initialization Blocks | Instance initialization blocks are executed in the order they appear in the class after instance variable initialization, just before the constructor is invoked. | ```java { /* initialization code */ }```        |
| 3         | Constructor Execution           | Finally, the constructor of the class is executed, allowing specific instance-level initialization tasks to be performed. | ```java public MyClass() { /* constructor code */ }``` |

- ==**Fields and instance initializer blocks are run in the order in which they appear in the file.**==
- ==**The constructor runs after all fields and instance initializer blocks have run.**==

```java
1: public class Chick {
2: private String name = "Fluffy";
3: { System.out.println("setting field"); }
4: public Chick() {
5: name = "Tiny";
6: System.out.println("setting constructor");
7: }
8: public static void main(String[] args) {
9: Chick chick = new Chick();
10: System.out.println(chick.name); } }
```

the output: 

```java
Running this example prints this:
setting field
setting constructor
Tiny
```

start with the `main()` method because that’s where Java starts execution. On line 9, we call the constructor of Chick. Java creates a new object. First it initializes name to "Fluffy" on line 2. Next it executes the `println()` statement in the instance initializer on line 3. Once all the fields and instance initializers have run, Java returns to the constructor. Line 5 changes the value of name to "Tiny", and line 6 prints another statement.

Order matters for the fields and blocks of code. You can’t refer to a variable before it has been defined:

```java
{ System.out.println(name); } // DOES NOT COMPILE
private String name = "Fluffy";
```

**Example**
```java
public class Egg {
public Egg() {
number = 5;
}
public static void main(String[] args) {
Egg egg = new Egg();
System.out.println(egg.number);
}
private int number = 3;
{ number = 4; } }
```

Fields and blocks are run first in order, setting number to 3 and then 4. Then the constructor runs, setting number to 5.
## Understanding Data Types

Java applications contain two types of data: **==primitive==** types and **==reference==** types.
### Using Primitive Types

Java has eight built-in data types, referred to as the Java primitive types. These eight data types represent the building blocks for Java objects, because all Java objects are just a complex collection of these primitive data types.  A primitive is not an object in Java, nor does it represent an object. A primitive is just a single value in memory, such as a number or character.
### The Primitive Types

| Keyword  | Type                      | Min Value                   | Max Value                   | Default Value               | Example    |
|----------|---------------------------|-----------------------------|-----------------------------|-----------------------------|------------|
| boolean  | true or false              | n/a                         | n/a                         | false                       | true       |
| byte     | 8-bit integral value       | -128                        | 127                         | 0                           | 123        |
| short    | 16-bit integral value      | -32,768                     | 32,767                      | 0                           | 123        |
| int      | 32-bit integral value      | -2,147,483,648              | 2,147,483,647               | 0                           | 123        |
| long     | 64-bit integral value      | -9,223,372,036,854,775,808  | 9,223,372,036,854,775,807   | 0L                          | 123L       |
| float    | 32-bit floating-point value| n/a                         | n/a                         | 0.0f                        | 123.45f    |
| double   | 64-bit floating-point value| n/a                         | n/a                         | 0.0                         | 123.456   |
| char     | 16-bit Unicode value       | 0                           | 65,535                      | '\u0000'                    | 'a'        |

some key points:

- ==**The byte, short, int, and long types are used for integer values without decimal** **points.**==

- ==**Each numeric type uses twice as many bits as the smaller similar type. For example,** **short uses twice as many bits as byte does.**==

- ==**All of the numeric types are signed and reserve one of their bits to cover a negative** **range.**==

- ==**A float requires the letter f or F following the number so Java knows it is a float.** **Without an f or F, Java interprets a decimal value as a double.**==

- ==**long requires the letter l or L following the number so Java knows it is a long.**==
==**Without an l or L, Java interprets a number without a decimal point as an int in most** **scenarios.**==

---
**Signed and Unsigned: short and char**

For the exam, you should be aware that short and char are closely related, as both are stored as integral types with the same 16-bit length. ==**The primary difference is that short is signed, which means it splits its range across the positive and negative integers. Alternatively, char is unsigned, which means its range is strictly positive, including 0.**==

Often, short and char values can be cast to one another because the underlying data size is the same.

---
### Writing Literals

When a number is present in the code, it is called a literal. By default, Java assumes you are defining an int value with a numeric literal.

In the following example, the number listed is bigger than what fits in an int.

```java
long max = 3123456789; // DOES NOT COMPILE
```

Java complains the number is out of range. And it is—for an int. However, we don’t have an int. The solution is to add the character `L` to the number:

```java
long max = 3123456789L; // Now Java knows it is a long
```

Another way to specify numbers is to change the `base.`  Java allows you to specify digits in several other formats:

- ==**Octal (digits 0–7), which uses the number 0 as a prefix—for example, 017.**==
-  ==**Hexadecimal (digits 0–9 and letters A–F/a–f), which uses 0x or 0X as a prefix—for example, 0xFF, 0xff, 0XFf. Hexadecimal is case insensitive, so all of these examples mean the same value.**==
-  ==**Binary (digits 0–1), which uses the number 0 followed by b or B as a prefix—for example, 0b10, 0B10.**==

### Literals and the Underscore Character

you can have underscores in numbers to make them easier to read:

```java
int million1 = 1000000;
int million2 = 1_000_000;
```

==**You can add underscores anywhere except at the beginning of a literal, the end of a literal, right before a decimal point, or right after a decimal point.**==

```java
double notAtStart = _1000.00; // DOES NOT COMPILE
double notAtEnd = 1000.00_; // DOES NOT COMPILE
double notByDecimal = 1000_.00; // DOES NOT COMPILE
double annoyingButLegal = 1_00_0.0_0; // Ugly, but compiles
double reallyUgly = 1__________2; // Also compiles
```

### Using Reference Types

**A reference type refers to an object (an instance of a class). Unlike primitive types that hold their values in the memory where the variable is allocated, references do not hold the value of the object they refer to. Instead, a reference “points” to an object by storing the memory address where the object is located, a concept referred to as a pointer.**

```java
String greeting;
```

The greeting variable is a reference that can only point to a String object. A value assigned to a reference in one of two ways:

- ==**A reference can be assigned to another object of the same or compatible type.**==
- ==**A reference can be assigned to a new object using the new keyword.**==

```java
greeting = new String("How are you?");
```

The greeting reference points to a new String object, *"How are you?"*. The String object does not have a name and can be accessed only via a corresponding reference.
### Distinguishing between Primitives and Reference Types

There are a few important differences between primitives and reference types.

- ==**First, notice that all the primitive types have lowercase type names. All classes that come with Java begin with uppercase. Although not required, it is a standard practice, and you should follow this convention for classes you create as well.**==

- ==**Next, reference types can be used to call methods, assuming the reference is not null. Primitives do not have methods declared on them.**==

  ```java
  String reference = "hello";
  int len = reference.length();
  int bad = len.length(); // DOES NOT COMPILE
```

Primitives do not have methods.

- ==**Finally, reference types can be assigned `null`, which means they do not currently refer to an object. Primitive types will give you a compiler error if you attempt to assign them `null`.**==

```java
int value = null; // DOES NOT COMPILE
String name = null;
```

### Creating Wrapper Classes

Each primitive type has a wrapper class, which is an object type that corresponds to the primitive.

| Primitive Type | Wrapper Class | Inherits Number? | Example of Creating |
|-----------------|---------------|-------------------|----------------------|
| boolean         | Boolean       | No                | `Boolean.valueOf(true)` |
| byte            | Byte          | Yes               | `Byte.valueOf((byte) 1)` |
| short           | Short         | Yes               | `Short.valueOf((short) 1)` |
| int             | Integer       | Yes               | `Integer.valueOf(1)` |
| long            | Long          | Yes               | `Long.valueOf(1)` |
| float           | Float         | Yes               | `Float.valueOf((float) 1.0)` |
| double          | Double        | Yes               | `Double.valueOf(1.0)` |
| char            | Character     | No                | `Character.valueOf('c')` |

There is also a `valueOf()` variant that converts a String into the wrapper class.

```java
int primitive = Integer.parseInt("123");
Integer wrapper = Integer.valueOf("123");
```

All of the numeric classes extend the Number class, which means they all come with some useful helper methods: `byteValue(), shortValue(), intValue(), longValue(), floatValue()`, and `doubleValue()`. The Boolean and Character wrapper classes include `booleanValue()` and `charValue()`, respectively. ==**These methods return the primitive value of a wrapper instance**==, in the type requested.

```java
Double apple = Double.valueOf("200.99");
System.out.println(apple.byteValue()); // -56
System.out.println(apple.intValue()); // 200
System.out.println(apple.doubleValue()); // 200.99
```

These helper methods do their best to convert values but can result in a loss of precision. 

### Defining Text Blocks

What if we want to have a String with something more complicated?

```java
"Java Study Guide"
by Scott & Jeanne
```

Building this as a String requires two things The syntax `\"` lets you say you want a " rather than to end the String, and `\n` says you want a new line. Both of these are called escape characters because the backslash provides a special meaning

```java
String eyeTest = "\"Java Study Guide\"\n by Scott & Jeanne";
```

While this does work, it is hard to read. Luckily, Java has text blocks, also known as multiline strings.

![[Pasted image 20240111141502.png]]

A text block starts and ends with three double quotes `(""")`, and the contents don’t need to be escaped. This is much easier to read.

==**In Java text blocks, use triple quotes `(""")` on separate lines above and below your text. Only the text between these lines becomes the Java String.**==

==**Essential whitespace is the intentional indentation and formatting that directly contributes to the structure and readability of your String. Incidental whitespace, on the other hand, is extra spacing added for code readability, but it doesn't affect the actual String value.**== 

```java
String textblock = """
                   This is a text inside a
                   text block.
                   You can use "quotes" in here
                   without escaping them.
                   """;
```

You can freely adjust incidental whitespace without impacting your String content. ==**Visualize a vertical line on the leftmost non-whitespace character in your text block – everything to the left is incidental whitespace, and everything to the right is essential whitespace.**== Adjusting the left side won't change your String; it's there solely for code aesthetics.

==**the difference in the start location of the last triple quotes `(""")` and the leftmost character of the text inside the text block determines how much indentation is left inside the Java String produced by the Java text block declaration.**==

```java
14: String pyramid = """
15: *
16: * *
17: * * *
18: """;
19: System.out.print(pyramid);
```

The closing `"""` on line 18 are the leftmost characters, so the line is drawn at the leftmost position

| Formatting                     | Meaning in Regular String | Meaning in Text Block    |
|--------------------------------|---------------------------|--------------------------|
| `\"`                           | `"`                       | `"`                      |
| `\"""` (Invalid)               | n/a - Invalid             | n/a - Invalid            |
| `\"\"\"`                       | n/a - Invalid             | `"""`                    |
| Space (at end of line)          | Space                     | Ignored                  |
| `\s` (Two spaces)              | Two spaces                | Two spaces (preserves leading space on the line) |
| `\` (at end of line, Invalid)   | n/a - Invalid             | Omits new line on that line (Invalid in a text block) |

**Examples**

```java
String block = """doe"""; // DOES NOT COMPILE
```

Text blocks require a line break after the opening """, making this one invalid

```java
String block = """
doe \
deer""";
```

How many lines ?  Just one. The output is doe deer since the \ tells Java not to add a new line before deer.

```java
String block = """
doe \n
deer
""";
```

This time we have four lines. Since the text block has the closing `"""` on a separate line,
we have three lines for the lines in the text block plus the explicit `\n`.

1. "doe " (ends with a space)
2. "deer" (no newline character here)
3. "" (empty line due to the closing `"""`)

---
```java
public static void main(String[] args) {  
  
  
    // Since Java 15, text blocks are available as a standard feature.  
    // A text block starts and ends with three double quotes ("""), and the contents don’t need to be escaped.  
    String textBlocks1 = """  
            Hello TextBlocks            """;  
  
    System.out.println("----textBlock1----");  
    System.out.println(textBlocks1);  
  
    String textBlocks2 = """  
                line1            """;  
  
    System.out.println("----textBlock2----");  
    System.out.println(textBlocks2);  
  
  
    String textBlocks3 = """  
                        line1            """;  
    System.out.println("----textBlock3----");  
    System.out.println(textBlocks3);  
  
  
    String textBlocks4 = """  
            line1                                """;  
  
    System.out.println("----textBlock4----");  
    System.out.println(textBlocks4);  
  
    String textBlocks5 = """  
                line1            line2                """;  
  
    System.out.println("----textBlock5----");  
    System.out.println(textBlocks5);  
  
    String textBlocks6 = """  
                line1            line2         """;  
  
    System.out.println("----textBlock6----");  
    System.out.println(textBlocks6);  
  
    String textBlocks7 = """  
                line1            line2               line3                        line4      """;  
  
    System.out.println("----textBlock7----");  
    System.out.println(textBlocks7);  
  
    String textBlocks8 = """  
                "line1"            "line2"                "line3"                    "line4"         """;  
  
    System.out.println("----textBlock8----");  
    System.out.println(textBlocks8);  
  
    String textBlocks9 = """  
                \"line1\"            \"line2\"                \"line3\"                    \"line4\"                """;  
  
    System.out.println("----textBlock9----");  
    System.out.println(textBlocks9);  
  
}
```

**the output**

```java
----textBlock1----
Hello TextBlocks

----textBlock2----
    line1

----textBlock3----
            line1

----textBlock4----
line1

----textBlock5----
    line1
line2

----textBlock6----
       line1
   line2

----textBlock7----
    line1
line2
   line3
            line4
----textBlock8----
       "line1"
   "line2"
       "line3"
           "line4"

----textBlock9----
    "line1"
"line2"
    "line3"
        "line4"
```

```java
public class DefiningTextBlockFormatting {  
  
    public static void main(String[] args) {  
  
        String textBlock1 = """  
                    \"sample"                """;  
  
        System.out.println(textBlock1);  
  
        String textBlock2 = """  
                    \"""line1"                """;  
  
        System.out.println(textBlock2);  
  
        String textBlock3 = """  
                    \"\"\"line1"                """;  
  
        System.out.println(textBlock3);  
  
  
        String textBlock4 = """  
                    \\\\\\line1"                """;  
  
        System.out.println(textBlock4);  
  
        String textBlock5 = """  
                \s\s\sline1                """;  
  
        System.out.println(textBlock5);  
  
        String textBlock6 = """  
                line1 \                    line1-part2 \                  line1-part3                """;  
  
        System.out.println(textBlock6);  
  
    }  
}

```

**the output**

```java
"sample"

    """line1"

    """line1"

    \\\line1"

   line1

line1     line1-part2   line1-part3
```

---
## Declaring Variables

A variable is a name for a piece of memory that stores data. When you declare a variable, you need to state the variable type along with giving it a name. Giving a variable a value is called initializing a variable. To initialize a variable, you just type the variable name followed by an equal sign, followed by the desired value

```java
String zooName = "The Best Zoo";
```

## Identifying Identifiers

An identifier is the name of a variable, method, class, interface, or package.

There are only four rules to remember for legal identifiers:
1. ==**Begin with a letter, currency symbol, or _ symbol:**== Identifiers must start with a letter `(a-z or A-Z)`, a currency symbol `(e.g., $, ¥, €)`, or an underscore `(_)`.
    
2. ==**Include numbers but not start with them:**== While identifiers can include numbers, they must not begin with a number.
    
3. ==**Single underscore _ is not allowed:**== Using a single underscore by itself as an identifier is not allowed.
    
4. ==**Avoid Java reserved words:**== Identifiers cannot have the same name as Java reserved words. Reserved words are special words in the Java language that have predefined meanings and cannot be used as identifiers.

| Reserved Words | Explanation                                       |
|-----------------|---------------------------------------------------|
| **`abstract`**      | Used to declare abstract classes or methods.      |
| **`assert`**        | Used for assertion checking in debugging.         |
| **`boolean`**       | Represents a data type with two values: true or false. |
| **`break`**         | Exits from the loop or switch statement.           |
| **`byte`**          | Represents a data type with values from -128 to 127. |
| **`case`**          | Used in switch statements to define different cases. |
| **`catch`**         | Catches exceptions in try-catch blocks.            |
| **`char`**          | Represents a data type for a single character.     |
| **`class`**         | Declares a class.                                 |
| **`const*`**        | Not used. (Reserved for future use.)              |
| **`continue`**      | Skips the rest of the loop and starts the next iteration. |
| **`default`**       | Used in switch statements as a default case.       |
| **`do`**            | Starts a do-while loop.                           |
| **`double`**        | Represents a data type for double-precision floating-point numbers. |
| **`else`**          | Defines the else clause in if statements.         |
| **`enum`**          | Declares an enumeration (a list of named values). |
| **`extends`**       | Indicates a class is derived from another class.  |
| **`final`**         | Prevents a class from being subclassed or a method from being overridden. |
| **`finally`**       | Defines a block of code to be executed after try-catch blocks. |
| **`float`**         | Represents a data type for single-precision floating-point numbers. |
| **`for`**           | Starts a for loop.                                |
| **`goto*`**         | Not used. (Reserved for future use.)              |
| **`if`**            | Makes a decision in conditional statements.       |
| **`implements`**    | Indicates a class implements an interface.        |
| **`import`**        | Imports a package or a specific class.            |
| **`instanceof`**    | Checks if an object is an instance of a particular class or interface. |
| **`int`**           | Represents a data type for integer numbers.       |
| **`interface`**     | Declares an interface.                            |
| **`long`**          | Represents a data type for long integers.         |
| **`native`**        | Specifies a method is implemented in a language other than Java. |
| **`new`**           | Creates an instance of a class.                   |
| **`package`**       | Declares a package.                               |
| **`private`**       | Restricts access to members within the same class. |
| **`protected`**     | Allows access to members within the same class and its subclasses. |
| **`public`**        | Provides unrestricted access to a class or method. |
| **`return`**        | Exits a method and optionally returns a value.   |
| **`short`**         | Represents a data type for short integers.        |
| **`static`**        | Declares a static method or field.                |
| **`strictfp`**      | Enforces strict floating-point precision.         |
| **`super`**         | Refers to the superclass.                          |
| **`switch`**        | Provides multi-way decision-making based on a value. |
| **`synchronized`**  | Coordinates access to objects by multiple threads. |
| **`this`**          | Refers to the current object.                     |
| **`throw`**         | Throws an exception manually.                     |
| **`throws`**        | Indicates a method may throw specific exceptions. |
| **`transient`**     | Specifies a field should not be serialized.      |
| **`try`**           | Encloses a block of code in which exceptions may occur. |
| **`void`**          | Specifies that a method does not return a value.  |
| **`volatile`**      | Indicates that a variable may be changed by multiple threads. |
| **`while`**         | Starts a while loop.                              |
* The reserved words `const` and `goto` aren’t actually used in Java. They are reserved so that people coming from other programming languages don’t use them by accident

- There are other names that you can’t use. For example, **`true`**, **`false`**, and **`null`** are literal values, so they can’t be variable names. Additionally, there are contextual keywords like **`module`**

**LEGAL**

```java
long okidentifier;
float $OK2Identifier;
boolean _alsoOK1d3ntifi3r;
char __SStillOkbutKnotsonice$;

int _a;  
int $c;  
int ______2_w;  
int _$;  
int this_is_a_very_detailed_name_for_an_identifier;

int ¥Ⅻ₤$ώ   = 100;  
// https://www.rapidtables.com/code/text/unicode-characters.html
```

**NOT LEGAL**

```java
int 3DPointClass; // identifiers cannot begin with a number
byte hollywood@vine; // @ is not a letter, digit, $ or _
String *$coffee; // * is not a letter, digit, $ or _
double public; // public is a reserved word
short _; // a single underscore is not allowed

int :b;  
int -d;  
int e#;  
int .f;  
int 7g;
```

## Declaring Multiple Variables

can also declare and initialize multiple variables in the same statement.

```java
void sandFence() {
String s1, s2;
String s3 = "yes", s4 = "no";
}
```

Four String variables were declared: s1, s2, s3, and s4. ==**You can declare many variables**== ==**in the same declaration as long as they are all of the same type**==

```java
void paintFence() {
int i1, i2, i3 = 0;
}
```

three variables were declared: i1, i2, and i3. However, only one of those values was initialized: i3. The other two remain declared but not yet initialized.  ==**That’s the trick. Each snippet separated by a comma is a little declaration of its own**==. The initialization of i3 only applies to i3. It doesn’t have anything to do with i1 or i2 despite being in the same statement.

```java
int num, String value; // DOES NOT COMPILE
```

```java
4: boolean b1, b2;
5: String s1 = "1", s2;
6: double d1, double d2;
7: int i1; int i2;
8: int i3; i4;
```

- **Legal Declarations:**
    
    - Lines 4 and 5 are legal. Line 4 declares two boolean variables, and Line 5 declares a String variable (`s1`) and another uninitialized String variable (`s2`).
- **Legal, but Uncommon:**

    - Line 7 is legal. It declares two int variables (`i1` and `i2`) in separate statements on the same line, separated by a semicolon.
- **Illegal Declarations:**
    
    - Line 6 is not legal. Java doesn't allow the declaration of two different types in the same statement, even if the types are the same (e.g., `double d1, double d2`).
    - Line 8 is not legal. It contains an oddly placed semicolon. To analyze, consider separating the code into individual lines and checking for valid declarations.

==**In summary, for multiple variable declarations in the same line, variables must share the same type declaration**==, and oddly placed semicolons can affect the legality of the code.

## Initializing Variables

Before you can use a variable, it needs a value.
### Creating Local Variables

==**A local variable is a variable defined within a constructor, method, or initializer block.**==
### Final Local Variables

The `final` keyword can be applied to local variables and is equivalent to declaring constants in other languages

```java
5: final int y = 10;
6: int x = 20;
7: y = x + 10; // DOES NOT COMPILE
```

The final modifier can also be applied to local variable references.

```java
5: final int[] favoriteNumbers = new int[10];
6: favoriteNumbers[0] = 10;
7: favoriteNumbers[1] = 20;
8: favoriteNumbers = null; // DOES NOT COMPILE
```

The compiler error isn’t until line 8, when we try to change the value of the reference `favoriteNumbers`.

---
```java
void sampleKeywordsForLocalVariables() {  
  
     private int secret = 10; // DOES NOT COMPILE  
     public int number = 100; // DOES NOT COMPILE  
     static int size = 20 ; // DOES NOT COMPILE  
     abstract int age = 25; // DOES NOT COMPILE  
     volatile int counter = 10; // DOES NOT COMPILE  
     transient int life = 50;  
  
    final int valid = 200;  
  
}
```

---
### Uninitialized Local Variables

==**Local variables do not have a default value and must be initialized before use.**== Furthermore, the compiler will report an error if you try to read an uninitialized value.

```java
4: public int notValid() {
5: int y = 10;
6: int x;
7: int reply = x + y; // DOES NOT COMPILE
8: return reply;
9: }
```

The compiler is smart enough to recognize variables that have been initialized after their declaration but before they are used.

```java
public int valid() {
int y = 10;
int x; // x is declared here
x = 3; // x is initialized here
int z; // z is declared here but never initialized or used
int reply = x + y;
return reply;
}
```

The compiler is also smart enough to recognize initializations that are more complex.

```java
public void findAnswer(boolean check) {
int answer;
int otherAnswer;
int onlyOneBranch;
if (check) {
onlyOneBranch = 1;
answer = 1;
} else {
answer = 2;
}
System.out.println(answer);
System.out.println(onlyOneBranch); // DOES NOT COMPILE
}
```

The `answer` variable is initialized in both branches of the if statement, so the compiler is perfectly happy. It knows that regardless of whether check is true or false, the value answer will be set to something before it is used. The `otherAnswer` variable is not initialized but never used, and the compiler is equally as happy. ==**The compiler is only concerned if you try to use uninitialized local variables; it doesn’t mind the ones you never use.**==

---
**On the exam, be wary of any local variable that is declared but not initialized in a single line. This is a common place on the exam that could result in a “Does not compile” answer. Be sure to check to make sure it’s initialized before it’s used on the exam.** #TIP 

---
### Passing Constructor and Method Parameters

Variables passed to a constructor or method are called constructor parameters or method
parameters, respectively. These parameters are like local variables that have been pre-initialized.

```java
public void findAnswer(boolean check) {} // check Bold
```

```java
public void checkAnswer() {
boolean value;
findAnswer(value); // DOES NOT COMPILE
}
```

The call to `findAnswer()` does not compile because it tries to use a variable that is not initialized.
### Defining Instance and Class Variables

Variables that are not local variables are defined either as instance variables or as class variables.

- An instance variable, often called a field, is a value defined within a specific instance of an object. Let’s say we have a `Person` class with an instance variable name of type `String`.
	Each instance of the class would have its own value for name, such as *Elysia* or *Sarah*.
	==**Two instances could have the same value for name, but changing the value for one does not modify the other.**==

- A class variable is one that is defined on the class level and shared among all instances of the class. It can even be publicly accessible to classes outside the class and doesn’t require an instance to use. ==**You can tell a variable is a class variable because it has the keyword `static` before it.**==

==**Instance and class variables do not require you to initialize them. As soon as you declare these variables, they are given a default value.**== The compiler doesn’t know what value to use and so wants the simplest value it can give the type: `null` for an object, `zero` for the numeric types, and `false` for a `boolean`

![[Pasted image 20240114005317.png]]
### Inferring the Type with `var`

have the option of using the keyword var instead of the type when declaring local variables under certain conditions

```java
public class Zoo {
public void whatTypeAmI() {
var name = "Hello";
var size = 7;
}
}
```

The formal name of this feature is ==**local variable type inference**==  You can only use this feature for
local variables. The exam may try to trick you with code like this:

```java
public class VarKeyword {
var tricky = "Hello"; // DOES NOT COMPILE
}
```

The variable `tricky` is an instance variable. Local variable type inference works with local variables and not instance variables. 
### Type Inference of var

When you type `var`, you are instructing the compiler to determine the type for you The compiler looks at the code on the line of the declaration and uses it to infer the type.

```java
7: public void reassignment() {
8: var number = 7;
9: number = 4;
10: number = "five"; // DOES NOT COMPILE
11: }
```

---
**In Java, var is still a specific type defined at compile time. It does not change type at runtime.** #TIP

---
### Examples with var

```java
3: public void doesThisCompile(boolean check) {
4: var question;
5: question = 1;
6: var answer;
7: if (check) {
8: answer = 2;
9: } else {
10: answer = 3;
11: }
12: System.out.println(answer);
13: }
```

The code does not compile. ==**for local variable type inference, the compiler looks only at the line with the declaration.**==  the initial value used to determine the type needs to be part of the same statement.

```java
var y;   // Compilation error: cannot infer type for local variable y
y = 10;  // Type inference requires an initializer on the same line

```


```java
4: public void twoTypes() {
5: int a, var b = 3; // DOES NOT COMPILE
6: var n = null; // DOES NOT COMPILE
7: }
```

Line 5 wouldn’t work even if you replaced var with a real type. All the types declared on a single line must be the same type and share the same declaration.

Line 6 is a single line. The compiler is being asked to infer the type of `null`. This could be any reference type. The only choice the compiler could make is `Object`. However  the designers of Java decided it would be better not to allow var for `null` than to have to guess at intent.

```java
4: public void twoTypes() {
5: var a = 2, var b = 3; // DOES NOT COMPILE
6: int x, int v = 3; // DOES NOT COMPILE 
7: var a = 2; var b = 3; // DOES  COMPILE
8: }
```


---

**While a `var` cannot be initialized with a null value without a type, it can be reassigned a null value after it is declared, provided that the underlying data type is a reference type.**  #TIP 

---

```java
public int addition(var a, var b) { // DOES NOT COMPILE
return a + b;
}
```

a and b are method parameters. These are not local variables. Be on the lookout for var used with constructors, method parameters, or instance variables. **var is only used for local variable type inference!**

==**one last rule  should be aware of:  `var` is not a reserved word and allowed to be used as an identifier. It is considered a reserved type name.  A reserved type name means it cannot be used to define a type, such as a class, interface, or enum.**==

```java
package var;
public class Var {
public void var() {
var var = "var";
}
public void Var() {
Var var = new Var();
}
}
```

this code does compile. 

---
**Var Review**

1. ==**A `var` is used as a local variable in a constructor, method, or initializer block.**==   
 2. ==**A `var` cannot be used in constructor parameters, method parameters, instance variables, or class variables.**==   
 3. ==**A `var` is always initialized on the same line (or statement) where it is declared.**==    
 4. ==**The value of a `var` can change, but the type cannot.**==    
 5. ==**A `var` cannot be initialized with a null value without a type.**==    
 6. ==**A `var` is not permitted in a multiple-variable declaration.**==    
 7.  ==**A `var` is a reserved type name but not a reserved word, meaning it can be used as an identifier except as a class, interface, or enum name.**== 

```java

  
// A var is used as a local variable in a constructor, method, or initializer block.  
class Example {  
  
    public Example() {  
        var number = 10;  
    }  
  
    private void method() {  
        var name = "username";  
    }  
  
    {  
        var initialized = true;  
    }  
}  
  
// A var cannot be used in constructor parameters, method parameters, instance variables, or class variables.  
class Example2 {  
  
     private void notValid(var notAllowedHere) {} // DOES NOT COMPILE  
     public Example2(var notAllowedHere) {} // DOES NOT COMPILE  
     private var instanceVariableAsVarNotAllowed; // DOES NOT COMPILE  
     private static var staticVariableAsVarNotAllowed; // DOES NOT COMPILE  
}  
  
// A var is always initialized on the same line (or statement) where it is declared.  
class Example3 {  
  
    void method() {  
        var number = 10;  
  
        var sum  
                = 20;  
  
         var notValid; notValid =20; // DOES NOT COMPILE  
         var notValid2;  
    }  
}  
  
// The value of a var can change, but the type cannot.  
  
class Example4 {  
  
    void method() {  
        var number = 10;  
        number = 20;  
        number = 30;  
  
        final var sum = 100;  
        sum = 150; // DOES NOT COMPILE, final variable  
  
        var today = LocalDate.now();  
  
         today = LocalTime.now(); // DOES NOT COMPILE  
  
        var str = new StringBuilder("example content");  
         str = "another content"; // DOES NOT COMPILE  
    }  
}  
  
// A var cannot be initialized with a null value without a type.  
  
class Example5 {  
  
    void method() {  
  
        var object = null; // DOES NOT COMPILE  
  
        var content = (String) null;  
  
        var invalid = (null)String; // DOES NOT COMPILE  
        var size = 10;  
         size = null; // DOES NOT COMPILE  
  
        var age = (Integer) 50;  
        age = null;  
  
        var name = "username";  
        name = null;  
    }  
}  
  
// A var is not permitted in a multiple-variable declaration.  
class Example6 {  
  
    void method() {  
  
         var number = 100, size = 200; // DOES NOT COMPILE  
        int number2 = 100, size2 = 200;  
  
         var number3 = 100, var size3 = 200; // DOES NOT COMPILE  
         int number4 = 100, int number4 = 200; // DOES NOT COMPILE  
    }  
}  
  
// 7- A var is a reserved type name but not a reserved word,  
// meaning it can be used as an identifier except as a class, interface, or enum name.  
  
// 'var' is a restricted identifier and cannot be used for type declarations  
  
class var { // DOES NOT COMPILE  
  
    public var() {}  
  
    private void var() {}  
}  
  
 interface var {} // DOES NOT COMPILE  
  
 enum var {} // DOES NOT COMPILE
```

---
## Managing Variable Scope

```java
public void eat(int piecesOfCheese) {
int bitesOfCheese = 1;
}
```

There are two variables with local scope. The `bitesOfCheese` variable is declared inside the method. The `piecesOfCheese` variable is a method parameter. Neither variable can be used outside of where it is defined.
### Limiting Scope

==**Local variables can never have a scope larger than the method they are defined in.**== However, they can have a smaller scope.

```java
3: public void eatIfHungry(boolean hungry) {
4: if (hungry) {
5: int bitesOfCheese = 1;
6: } // bitesOfCheese goes out of scope here
7: System.out.println(bitesOfCheese); // DOES NOT COMPILE
8: }
```

When you see a set of braces `({})` in the code, it means you have entered a new block of code. Each block of code has its own scope. When there are multiple blocks, you match them from the inside out.

Remember that blocks can contain other blocks. These smaller contained blocks can reference variables defined in the larger scoped blocks, but not vice versa.

```java
16: public void eatIfHungry(boolean hungry) {
17: if (hungry) {
18: int bitesOfCheese = 1;
19: {
20: var teenyBit = true;
21: System.out.println(bitesOfCheese);
22: }
23: }
24: System.out.println(teenyBit); // DOES NOT COMPILE
25: }
```

The variable defined on line 18 is in scope until the block ends on line 23. Using it in the smaller block from lines 19 to 22 is fine. The variable defined on line 20 goes out of scope on line 22. Using it on line 24 is not allowed.

### Tracing Scope

which line each of the five local variables goes into and out of scope:

```java
11: public void eatMore(boolean hungry, int amountOfFood) { // Method
12: int roomInBelly = 5;
13: if (hungry) { // if
14: var timeToEat = true;
15: while (amountOfFood > 0) { // while
16: int amountEaten = 2;
17: roomInBelly = roomInBelly -amountEaten;
18: amountOfFood = amountOfFood -amountEaten;
19: } // while
20: } // if
21: System.out.println(amountOfFood);
22: } // Method
```

This method does compile. The first step in figuring out the scope is to identify the blocks of code. In this case, there are three blocks. You can tell this because there are three sets of braces.

| Block Type | First Line in Block | Last Line in Block |
|------------|----------------------|---------------------|
| `while`    | 15                   | 19                  |
| `if`       | 13                   | 20                  |
| Method     | 11                   | 22                  |

`hungry` and `amountOfFood` are method parameters, so they are available for the entire method. This means their scope is lines 11 to 22. The variable `roomInBelly` goes into scope on line 12 because that is where it is declared. It stays in scope for the rest of the method and goes out of scope on line 22. The variable `timeToEat` goes into scope on line 14 where it is declared. It goes out of scope on line 20 where the if block ends. Finally, the variable `amountEaten` goes into scope on line 16 where it is declared. It goes out of scope on line 19 where the while block ends.

==**Identifying blocks and variable scope needs to be second nature for the exam.**==
### Applying Scope to Classes

- ==**the rule for instance variables is easier: they are available as soon as they are defined and last for the entire lifetime of the object itself.**==

- ==**The rule for class, aka `static`, variables is even easier: they go into scope when declared like the other variable types. However, they stay in scope for the entire life of the program.**==

```java
1: public class Mouse {
2: final static int MAX_LENGTH = 5; // End of the program - scope: 2 - 10
3: int length; // End of the object - scope: 3 - 10
4: public void grow(int inches) { // scope: 4 - 9
5: if (length < MAX_LENGTH) {
6: int newSize = length + inches; // scope: 6 - 8
7: length = newSize;
8: }
9: }
10: }
```
### Reviewing Scope

- ==**Local variables: In scope from declaration to the end of the block**==
- ==**Method parameters: In scope for the duration of the method**==
- ==**Instance variables: In scope from declaration until the object is eligible for garbage collection**==
- ==**Class variables: In scope from declaration until the program ends**==

---
```java
public class ReviewingScope {  
  
    private String instanceVariable = "best object value";  
  
    private static String classVariable = "cool class";  
  
    private void method(int methodParameter) {  
  
        int localVariableX = 100;  
  
        var localVariableY = 200;  
  
        if (methodParameter > 10) {  
            int localVariableInTheIfBlock = 30;  
            System.out.println(localVariableInTheIfBlock);  
            System.out.println(localVariableX);  
            System.out.println(localVariableY);  
            System.out.println(methodParameter);  
            System.out.println(instanceVariable);  
            System.out.println(classVariable);  
        } else {  
            int localVariableInTheElseBlock = 50;  
            System.out.println(localVariableX);  
            System.out.println(localVariableY);  
            //System.out.println(localVariableInTheIfBlock); //DOES NOT COMPILE  
            System.out.println(methodParameter);  
            System.out.println(instanceVariable);  
            System.out.println(ReviewingScope.classVariable);  
        }  
  
        // System.out.println(localVariableInTheIfBlock); //DOES NOT COMPILE  
  
        System.out.println(instanceVariable);  
        System.out.println(classVariable);  
    }
```

---
## Destroying Objects

Java provides a garbage collector to automatically look for objects that aren’t needed anymore.  All Java objects are stored in your program memory’s heap. The heap, which is also referred to as the free store, represents a large pool of unused memory allocated to your Java application. If your program keeps instantiating objects and leaving them on the heap, eventually it will run out of memory and crash. garbage collection solves this problem.

### Understanding Garbage Collection

Garbage collection refers to the process of automatically freeing memory on the heap by deleting objects that are no longer reachable in your program. 

As a developer, the most interesting part of garbage collection is determining when the memory belonging to an object can be reclaimed. In Java and other languages, ==**eligible for garbage collection refers to an object’s state of no longer being accessible in a program and therefore able to be garbage collected.**==

Think of garbage-collection eligibility like shipping a package. You can take an item, seal it in a labeled box, and put it in your mailbox. This is analogous to making an item eligible for garbage collection. When the mail carrier comes by to pick it up, though, is not in your control 

Java includes a built-in method to help support garbage collection where you can suggest that garbage collection run.

```java
System.gc();
```

Java is free to ignore you. ==**This method is not guaranteed to do anything**==.

### Tracing Eligibility

How does the JVM know when an object is eligible for garbage collection? The JVM waits patiently and monitors each object until it determines that the code no longer needs that memory. An object will remain on the heap until it is no longer reachable. An object is no longer reachable when one of two situations occurs:

-  ==**The object no longer has any references pointing to it.**==
-  ==**All references to the object have gone out of scope.**==

---
**Objects vs. References**

Do not confuse a reference with the object that it refers to; they are two different entities.

- The reference is a variable that has a name and can be used to access the contents of an object. A reference can be assigned to another reference, passed to a method, or returned from a method. All references are the same size, no matter what their type is.

- An object sits on the heap and does not have a name. Therefore, you have no way to access an object except through a reference. Objects come in all different shapes and sizes and consume varying amounts of memory. An object cannot be assigned to another object, and an object cannot be passed to a method or returned from a method. ==**It is the object that gets garbage collected, not its reference.**==

			![[Pasted image 20240112123949.png]]

---

```java
1: public class Scope {
2: public static void main(String[] args) {
3: String one, two;
4: one = new String("a");
5: two = new String("b");
6: one = two;
7: String three = one;
8: one = null;
9: } }
```

- Line 3: Declares two String variables, `one` and `two`.
- Lines 4-5: Creates two String objects ("a" and "b") on the heap and assigns them to `one` and `two`.
- Line 6: Makes `one` point to the same object as `two`.
- Line 7: Declares a new variable `three` and makes it point to the same object as `one`.
- Line 8: Sets `one` to `null`.
- Garbage Collection Eligibility:
    - Object with "a" becomes eligible for garbage collection on line 6 when the only arrow pointing to it is replaced.
    - Object with "b" remains eligible until the end of the method (line 9) since `three` is still referencing it.


---
**Code Formatting on the Exam** #TIP 

Not all questions will include package declarations and imports. Don’t worry about missing package statements or imports unless you are asked about them. The following are common cases where you don’t need to check the imports:

- ==**Code that begins with a class name**==
-  ==**Code that begins with a method declaration**==
- ==**Code that begins with a code snippet that would normally be inside a class or method**==
- ==**Code that has line numbers that don’t begin with 1**==
 
 You’ll see code that doesn’t have a method. When this happens, assume any necessary plumbing code like the main() method and class definition were written correctly. You’re just being asked if the part of the code you’re shown compiles when dropped into valid surrounding code. Finally, remember that extra whitespace doesn’t matter in Java syntax. The exam may use varying amounts of whitespace to trick you.

---

## Summary #OCP_Summary 

==**Java begins program execution with a `main()` method. The most common signature for this method run from the command line is `public static void main(String[] args)`. Arguments are passed in after the class name, as in java `NameOfClass` `firstArgument`. Arguments are indexed starting with 0.**==

==**Java code is organized into folders called packages. To reference classes in other packages, you use an `import` statement. A wildcard ending an import statement means you want to import all classes in that package. It does not include packages that are inside that one. The package` java.lang` is special in that it does not need to be imported.**==

==**For some class elements, order matters within the file. The package statement comes first if present. Then come the import statements if present. Then comes the class declaration. Fields and methods are allowed to be in any order within the class.**==

==**Primitive types are the basic building blocks of Java types. They are assembled into reference types. Reference types can have methods and be assigned a null value. Numeric literals are allowed to contain underscores `(_)` as long as they do not start or end the literal and are not next to a decimal point `(.)`. Wrapper classes are reference types, and there is one for each primitive. Text blocks allow creating a String on multiple lines using `"""`.**==

==**Declaring a variable involves stating the data type and giving the variable a name. Variables that represent fields in a class are automatically initialized to their corresponding 0, `null`, or `false` values during object instantiation. Local variables must be specifically initialized before they can be used. Identifiers may contain letters, numbers, currency symbols, or _. Identifiers may not begin with numbers. Local variable declarations may use the var keyword instead of the actual type. When using var, the type is set once at compile time and does not change.**==

==**Scope refers to that portion of code where a variable can be accessed. There are three kinds of variables in Java, depending on their scope: instance variables, class variables, and local variables. Instance variables are the non-static fields of your class. Class variables are the static fields within a class. Local variables are declared within a constructor, method, or initializer block.**==

==**Constructors create Java objects. A constructor is a method matching the class name and omitting the return type. When an object is instantiated, fields and blocks of code are initialized first. Then the constructor is run. Finally, garbage collection is responsible for removing objects from memory when they can never be used again. An object becomes eligible for garbage collection when there are no more references to it or its references have all gone out of scope.**==


## Exam Essentials #Essential

**Be able to write code using a main() method**. A `main()` method is usually written as `public static void main(String[] args)`. Arguments are referenced starting with `args[0]`. Accessing an argument that wasn’t passed in will cause the code to throw an exception.

**Understand the effect of using packages and imports**. Packages contain Java classes. Classes can be imported by class name or wildcard. Wildcards do not look at subdirectories. In the event of a conflict, class name imports take precedence. Package and import statements are optional. If they are present, they both go before the class declaration in that order.

**Be able to recognize a constructor.** A constructor has the same name as the class. It looks like a method without a return type.

**Be able to identify legal and illegal declarations and initialization**. Multiple variables can be declared and initialized in the same statement when they share a type. Local variables require an explicit initialization; others use the default value for that type. Identifiers may contain letters, numbers, currency symbols, or _, although they may not begin with numbers. Also, you cannot define an identifier that is just a single underscore character _. Numeric literals may contain underscores between two digits, such as 1_000, but not in other places, such as _100_.0_.

**Understand how to create text blocks.**  A text block begins with `"""` on the first line. On the next line begins the content. The last line ends with `""".` If `"""` is on its own line, a trailing line break is included.

**Be able to use `var` correctly.** A var is `var` for a local variable. A `var` is initialized on the same line where it is declared, and while it can change value, it cannot change type. A `var` cannot be initialized with a `null` value without a type, nor can it be used in multiple variable declarations.

**Be able to determine where variables go into and out of scope.** All variables go into scope when they are declared. Local variables go out of scope when the block they are declared in ends. Instance variables go out of scope when the object is eligible for garbage collection. Class variables remain in scope as long as the program is running.

**Know how to identify when an object is eligible for garbage collection.** Draw a diagram to keep track of references and objects as you trace the code. When no arrows point to a box (object), it is eligible for garbage collection.

## Review Questions

1. Which of the following are legal entry point methods that can be run from the command line? (Choose all that apply.)
A.  ``private static void main(String[] args)``
B.  ``public static final main(String[] args)``
C.  ``public void main(String[] args)``
D.  ``public static final void main(String[] args)``
E.  ``public static void main(String[] args)``
F.  ``public static main(String[] args)``

**My Answer: D, E
Correct Answer: D,E**

**D, E. Option E is the canonical main() method signature. You need to memorize it. Option D is an alternate form with the redundant final.**

---

Which answer options represent the order in which the following statements can be assembled into a program that will compile successfully? (Choose all that apply.)
```java
X: class Rabbit {}
Y: import java.util.*;
Z: package animals;
```
A.  X, Y, Z
B.  Y, Z, X
C.  Z, Y, X
D.  Y, X
E.  Z, X
F.  X, Z
G. None of the above

**My Answer: C,D  
Correct Answer: C,D,E**

**The package and import statements are both optional. If both are present, the order must be package, then import, and then class.**

---

3. Which of the following are true? (Choose all that apply.)
```java
public class Bunny {
public static void main(String[] x) {
Bunny bun = new Bunny();
} }
```

A.  Bunny is a class.
B.  bun is a class.
C.  main is a class.
D.  Bunny is a reference to an object.
E.  bun is a reference to an object.
F.  main is a reference to an object.
G.  The main() method doesn’t run because the parameter name is incorrect.

**My Answer: A,E  
Correct Answer: A,E**

**Bunny is a class, which can be seen from the declaration: public class Bunny. The variable bun is a reference to an object. The method main() is the standard entry point to a program.**

---

4. Which of the following are valid Java identifiers? (Choose all that apply.)
A.  `_`
B. ` _helloWorld$`
C.  `true`
D.  `java.lang`
E.  Public
F.  1980_s
G.  _Q2_

**My Answer: B,E,G 
Correct Answer: B,E,G**

---

5. Which statements about the following program are correct? (Choose all that apply.)

```java
2: public class Bear {
3: private Bear pandaBear;
4: private void roar(Bear b) {
5: System.out.println("Roar!");
6: pandaBear = b;
7: }
8: public static void main(String[] args) {
9: Bear brownBear = new Bear();
10: Bear polarBear = new Bear();
11: brownBear.roar(polarBear);
12: polarBear = null;
13: brownBear = null;
14: System.gc(); } }
```

A.  The object created on line 9 is eligible for garbage collection after line 13.
B.  The object created on line 9 is eligible for garbage collection after line 14.
C.  The object created on line 10 is eligible for garbage collection after line 12.
D.  The object created on line 10 is eligible for garbage collection after line 13.
E.  Garbage collection is guaranteed to run.
F.  Garbage collection might or might not run.
G.  The code does not compile.

**My Answer: A,D,F  
Correct Answer: A,D,F**

**Garbage collection is never guaranteed to run, making option F correct and option E incorrect. Next, the class compiles and runs without issue, so option G is incorrect. The Bear object created on line 9 is accessible until line 13 via the brownBear reference variable, which is option A. The Bear object created on line 10 is accessible via both the polarBear reference and the `brownBear.pandaBear` reference. After line 12, the object is still accessible via `brownBear.pandaBear.` After line 13, though, it is no longer accessible since `brownBear` is no longer accessible, which makes option D the final answer.**

---

6. Assuming the following class compiles, how many variables defined in the class or method are in scope on the line marked on line 14?
```java
1: public class Camel {
2: { int hairs = 3_000_0; }
3: long water, air=2;
4: boolean twoHumps = true;
5: public void spit(float distance) {
6: var path = "";
7: { double teeth = 32 + distance++; }
8: while(water > 0) {
9: int age = twoHumps ? 1 : 2;
10: short i=-1;
11: for(i=0; i<10; i++) {
12: var Private = 2;
13: }
14: // SCOPE
15: }
16: }
17: }
```

A. 2
B. 3
C. 4
D. 5
E. 6
F. 7
G. None of the above

**My Answer: D  
Correct Answer: F**

**To solve this problem, you need to trace the braces {} and see when variables go in and out of scope. The variables on lines 2 and 7 are only in scope for a single line block. The variable on line 12 is only in scope for the for loop. None of these are in scope on line 14.  By contrast, the three instance variables on lines 3 and 4 are available in all instance methods. Additionally, the variables on lines 6, 9, and 10 are available since the method and while loop are still in scope.**

---

7. Which are true about this code? (Choose all that apply.)

```JAVA
public class KitchenSink {
private int numForks;
public static void main(String[] args) {
int numKnives;
System.out.print("""
"# forks = " + numForks +
" # knives = " + numKnives +
# cups = 0""");
}
}
```

A. The output includes: # forks = 0.
B.  The output includes: # knives = 0.
C.  The output includes: # cups = 0.
D.  The output includes a blank line.
E.  The output includes one or more lines that begin with whitespace.
F.  The code does not compile.

**My Answer: F 
Correct Answer: C, E**

**The first thing to recognize is that this is a text block and the code inside the `"""` is just text. Options A and B are incorrect because the `numForks` and `numKnives` variables are not used. This is convenient since `numKnives` is not initialized and would not compile if it were referenced. Option C is correct as it is matching text. Option D is incorrect because the text block does not have a trailing blank line. Finally, option E is also an answer since " # knives is indented.**

---

8. Which of the following code snippets about `var` compile without issue when used in a method? (Choose all that apply.)

```java
A. var spring = null;
B. var fall = "leaves";
C. var evening = 2; evening = null;
D. var night = Integer.valueOf(3);
E. var day = 1/0;
F. var winter = 12, cold;
G. var fall = 2, autumn = 2;
H. var morning = ""; morning = null;
```

**My Answer: B,C,D,H  
Correct Answer: B,D,E,H**

**`var` cannot be initialized with a null value without a type, but it can be assigned a null value later if the underlying type is not a primitive. var cannot be used in a multiple-variable assignment.**

---

9. Which of the following are correct? (Choose all that apply.)
A.  An instance variable of type float defaults to 0.
B.  An instance variable of type char defaults to null.
C.  A local variable of type double defaults to 0.0.
D.  A local variable of type int defaults to null.
E.  A class variable of type String defaults to null.
F.  A class variable of type String defaults to the empty string "".
G.  None of the above.

**My Answer: B,F  
Correct Answer: E**

==**local variables don’t have default values.  primitives do not default to null.  reference types in class variables default to null.**==

---

10. Which of the following expressions, when inserted independently into the blank line, allow the code to compile? (Choose all that apply.)

```java
public void printMagicData() {
var magic = ???;
System.out.println(magic);
}
```

A.  3_1
B.  1_329_.0
C.  3_13.0_
D.  5_291._2
E.  2_234.0_0
F.  9___6
G.  _1_3_5_0

**My Answer: A,E,F  / Correct Answer: A,E,F**

---

11. Given the following two class files, what is the maximum number of imports that can be removed and have the code still compile?

```java
// Water.java
package aquarium;
public class Water { }

// Tank.java
package aquarium;
import java.lang.*;
import java.lang.System;
import aquarium.Water;
import aquarium.*;
public class Tank {
public void print(Water water) {
System.out.println(water); } }
```

A. 0
B. 1
C. 2
D. 3
E. 4
F. Does not compile

**My Answer: E  
Correct Answer: E**

**The first two imports can be removed because `java.lang` is automatically imported. The**
**following two imports can be removed because Tank and Water are in the same package,**

---

12. Which statements about the following class are correct? (Choose all that apply.)

```JAVA
1: public class ClownFish {
2: int gills = 0, double weight=2;
3: { int fins = gills; }
4: void print(int length = 3) {
5: System.out.println(gills);
6: System.out.println(weight);
7: System.out.println(fins);
8: System.out.println(length);
9: } }
```

A.  Line 2 generates a compiler error.
B.  Line 3 generates a compiler error.
C.  Line 4 generates a compiler error.
D.  Line 7 generates a compiler error.
E.  The code prints 0.
F.  The code prints 2.0.
G.  The code prints 2.
H.  The code prints 3.

**My Answer: A 
Correct Answer: A,C,D**

**Line 2 does not compile as only one type should be specified, making option A correct.  Line 4 does not compile because Java does not support setting default method parameter values, making option C correct. Finally, line 7 does not compile because fins is in scope and accessible only inside the instance initializer on line 3, making option D correct.**

---

13. Given the following classes, which of the following snippets can independently be inserted in place of INSERT IMPORTS HERE and have the code compile? (Choose all that apply.)

```java
package aquarium;
public class Water {
boolean salty = false;
}
package aquarium.jellies;
public class Water {
boolean salty = true;
}
package employee;
INSERT IMPORTS HERE
public class WaterFiller {
Water water;
}
```

A. import aquarium.*;
B. import `aquarium.Water`;
   import `aquarium.jellies.*`;
C. import aquarium.*;
   import `aquarium.jellies.Water`;
D. import aquarium.*;
   import `aquarium.jellies.*`;
E. import `aquarium.Water`;
   import `aquarium.jellies.Water`;
F. None of these imports can make the code compile.

**My Answer: A,B,C  
Correct Answer: A,B,C**

---

14. Which of the following statements about the code snippet are true? (Choose all that apply.)
```java
3: short numPets = 5L;
4: int numGrains = 2.0;
5: String name = "Scruffy";
6: int d = numPets.length();
7: int e = numGrains.length;
8: int f = name.length();
```

A. Line 3 generates a compiler error.
B. Line 4 generates a compiler error.
C. Line 5 generates a compiler error.
D. Line 6 generates a compiler error.
E. Line 7 generates a compiler error.
F. Line 8 generates a compiler error.

**My Answer: A,B,D,E 
Correct Answer: A,B,D,E**

**Line 3 does not compile because the L suffix makes the literal value a long, which cannot be stored inside a short directly, making option A correct. Line 4 does not compile because int is an integral type, but 2.0 is a double literal value, making option B correct. both primitives, and you can call methods only on reference types, not primitive values, making options D and E correct**

---

15. Which of the following statements about garbage collection are correct? (Choose all that apply.)

A. Calling `System.gc()` is guaranteed to free up memory by destroying objects eligible for garbage collection.
B. Garbage collection runs on a set schedule.
C. Garbage collection allows the JVM to reclaim memory for other objects.
D. Garbage collection runs when your program has used up half the available memory.
E. An object may be eligible for garbage collection but never removed from the heap.
F. An object is eligible for garbage collection once no references to it are accessible in the program.
G. Marking a variable final means its associated object will never be garbage collected.

**My Answer: C,F  
Correct Answer: C,E,F**

**In Java, there are no guarantees about when garbage collection will run. The JVM is free to ignore calls to `System.gc()`. the purpose of garbage collection is to reclaim used memory. Option E is also correct that an object may never be garbage collected, such as if the program ends  before garbage collection runs.** 

---

16. Which are true about this code? (Choose all that apply.)
```java
var blocky = """
squirrel \s
pigeon \
termite""";
System.out.print(blocky);
```

A. It outputs two lines.
B. It outputs three lines.
C. It outputs four lines.
D. There is one line with trailing whitespace.
E. There are two lines with trailing whitespace.
F. If we indented each line five characters, it would change the output.

**My Answer: B,D 
Correct Answer: A,D**

**here are two lines. One starts with squirrel, and the other starts with pigeon. Remember that a backslash means to skip the line break. Option D is also correct as \s means to keep whitespace. In a text block, incidental indentation is ignored**

---

17. What lines are printed by the following program? (Choose all that apply.)

```java
1: public class WaterBottle {
2: private String brand;
3: private boolean empty;
4: public static float code;
5: public static void main(String[] args) {
6: WaterBottle wb = new WaterBottle();
7: System.out.println("Empty = " + wb.empty);
8: System.out.println("Brand = " + wb.brand);
9: System.out.println("Code = " + code);
10: } }
```

A. Line 8 generates a compiler error.
B. Line 9 generates a compiler error.
C. Empty =
D. Empty = false
E. Brand =
F. Brand = null
G. Code = 0.0
H. Code = 0f

**My Answer: D,E,G 
Correct Answer: D,F,G**

**The code compiles and runs without issue, so options A and B are incorrect. A boolean field initializes to false, making option D correct with Empty = false being printed. Object references initialize to null, not the empty String, so option F is correct with Brand = null being printed.  Finally, the default value of floating-point numbers is 0.0. Although float values can be declared with an f suffix, they are not printed with an f suffix. For these reasons, option G is correct and Code = 0.0 is printed.**

---

18. Which of the following statements about var are true? (Choose all that apply.)

A. A var can be used as a constructor parameter.
B. The type of a var is known at compile time.
C. A var cannot be used as an instance variable.
D. A var can be used in a multiple variable assignment statement.
E. The value of a var cannot change at runtime.
F. The type of a var cannot change at runtime.
G. The word var is a reserved word in Java.

**My Answer: B,C,F 
Correct Answer: B,C,F**

---

19. Which are true about the following code? (Choose all that apply.)

```java
var num1 = Long.parseLong("100");
var num2 = Long.valueOf("100");
System.out.println(Long.max(num1, num2));
```

A. The output is 100.
B. The output is 200.
C. The code does not compile.
D. num1 is a primitive.
E. num2 is a primitive.

**My Answer: A  
Correct Answer: A,D**

==**The first is a long primitive and the second is a Long reference object,**==

---

20. Which statements about the following class are correct? (Choose all that apply.)

```java
1: public class PoliceBox {
2: String color;
3: long age;
4: public void PoliceBox() {
5: color = "blue";
6: age = 1200;
7: }
8: public static void main(String []time) {
9: var p = new PoliceBox();
10: var q = new PoliceBox();
11: p.color = "green";
12: p.age = 1400;
13: p = q;
14: System.out.println("Q1="+q.color);
15: System.out.println("Q2="+q.age);
16: System.out.println("P1="+p.color);
17: System.out.println("P2="+p.age);
18: } }
```

A. It prints Q1=blue.
B. It prints Q2=1200.
C. It prints P1=null.
D. It prints P2=1400.
E. Line 4 does not compile.
F. Line 12 does not compile.
G. Line 13 does not compile.
H. None of the above.

**My Answer: F,G  
Correct Answer: C**

**The key thing to notice is that line 4 does not define a constructor, but instead a method named `PoliceBox()`, since it has a return type of void. This method is never executed during the program run, and color and age are assigned the default values null and 0L, respectively. Lines 11 and 12 change the values for an object associated with p, but then, on line 13, the p variable is changed to point to the object associated with q, which still has the default values. For this reason, the program prints Q1=null, Q2=0, P1=null, and P2=0,**

---

21. What is the output of executing the following class?

```java
1: public class Salmon {
2: int count;
3: { System.out.print(count+"-");
}
4: { count++; }
5: public Salmon() {
6: count = 4;
7: System.out.print(2+"-");
8: }
9: public static void main(String[] args) {
10: System.out.print(7+"-");
11: var s = new Salmon();
12: System.out.print(s.count+"-");
} }
```

A. 7-0-2-1- 
B. 7-0-1- 
C. 0-7-2-1- 
D. 7-0-2-4- 
E. 0-7-1- 
F. The class does not compile because of line 3. 
G. The class does not compile because of line 4. 
H. None of the above.

**My Answer: D  
Correct Answer: D**

---

22. Given the following class, which of the following lines of code can independently replace INSERT CODE HERE to make the code compile? (Choose all that apply.)

```java
public class Price {
public void admission() {
INSERT CODE HERE
System.out.print(amount);
} }
```

A. int Amount = 0b11;
B. int amount = 9L;
C. int amount = 0xE;
D. int amount = 1_2.0;
E. double amount = 1_0_.0;
F. int amount = 0b101;
G. double amount = 9_2.1_2;
H. double amount = 1_2_.0_0;

**My Answer: A,C,F,G  
Correct Answer: C,F,G**

--- 

23. Which statements about the following class are true? (Choose all that apply.)

```java
1: public class River {
2: int Depth = 1;
3: float temp = 50.0;
4: public void flow() {
5: for (int i = 0; i < 1; i++) {
6: int depth = 2;
7: depth++;
8: temp--
;
9: }
10: System.out.println(depth);
11: System.out.println(temp); }
12: public static void main(String... s) {
13: new River().flow();
14: } }
```

A. Line 3 generates a compiler error.
B. Line 6 generates a compiler error.
C. Line 7 generates a compiler error.
D. Line 10 generates a compiler error.
E. The program prints 3 on line 10.
F. The program prints 4 on line 10.
G. The program prints 50.0 on line 11.
H. The program prints 49.0 on line 11.

**My Answer: A  
Correct Answer: A,D**

**The first compiler error is on line 3. The variable temp is declared as a float, but the assigned value is 50.0, which is a double without the F/f postfix. Since a double doesn’t fit inside a float, line 3 does not compile. Next, depth is declared inside the for loop and only has scope inside this loop. Therefore, reading the value on line 10 triggers a compiler error.**

---

# Chapter 2 - Operators #Chapter

## Understanding Java Operators

A Java operator is a special symbol that can be applied to a set of variables, values, or literals—referred to as operands—and that returns a result. The term operand, refers to the value or variable the operator is being applied to.

![[Pasted image 20240116141817.png]]

### Types of Operators

==**Java supports three flavors of operators: unary, binary, and ternary.**== These types of operators
can be applied to one, two, or three operands, respectively. 

Java operators are not necessarily evaluated from left-to-right order.

```java
int cookies = 4;
double reward = 3 + 2 * --cookies;
System.out.print("Zoo animal receives: "+reward+" reward points");
```

In this example, first decrement `cookies` to 3, then multiply the resulting value by 2, and finally add 3. The value then is automatically promoted from 9 to 9.0 and assigned to `reward`. The final values of `reward` and `cookies` are 9.0 and 3, respectively, with the following printed:

```java
Zoo animal receives: 9.0 reward points
```

### Operator Precedence

In mathematics, certain operators can override other operators and be evaluated first. ==**Determining which operators are evaluated in what order is referred to as operator precedence.**== In this manner, Java more closely follows the rules for mathematics.

```java
var perimeter = 2 * height + 2 * length;
// how the compiler evaluates this statement:
var perimeter = ((2 * height) + (2 * length));
```

The multiplication operator `(*)` has a higher precedence than the addition operator `(+)`, The assignment
operator `(=)` has the lowest order of precedence, so the assignment to the `perimeter` variable is performed last.

==**Unless overridden with parentheses, Java operators follow order of operation, listed in Table 2.1, by decreasing order of operator precedence.**== If two operators have the same level of precedence, then Java guarantees left-to-right evaluation for most operators other than the ones marked in the table.

![[Pasted image 20240116144727.png]]

## Applying Unary Operators

By definition, a unary operator is one that requires exactly one operand, or variable, to function. they often perform simple tasks, such as increasing a numeric variable by one or negating a `boolean` value.

| Operator Type         | Example      | Description                                           |
|------------------------|--------------|-------------------------------------------------------|
| Logical Complement     | `!a`         | Inverts a boolean’s logical value                     |
| Bitwise Complement     | `~b`         | Inverts all 0s and 1s in a number                     |
| Plus                   | `+c`         | Indicates a number is positive (assumed positive in Java unless accompanied by a negative unary operator) |
| Negation or Minus      | `-d`         | Indicates a literal number is negative or negates an expression |
| Increment              | `++e`        | Increments a value by 1                               |
| Increment (Postfix)    | `f++`        | Increments a value by 1 after its current value is used |
| Decrement              | `--f`        | Decrements a value by 1                               |
| Decrement (Postfix)    | `h--`        | Decrements a value by 1 after its current value is used |
| Cast                   | `(String)i`  | Casts a value to a specific type                      |
## Complement and Negation Operators

The logical complement operator `(!)` flips the value of a `boolean` expression. For example, if the value is true, it will be converted to false, and vice versa.

```java
boolean isAnimalAsleep = false;
System.out.print(isAnimalAsleep); // false
isAnimalAsleep = !isAnimalAsleep;
System.out.print(isAnimalAsleep); // true
```

For the exam, you also need to know about the **`bitwise complement operator (~)`**, which flips all of the 0s and 1s in a number. ==**It can only be applied to integer numeric types such as byte, short, char, int, and long.**==

```java
int value = 3; // Stored as 0011
int complement = ~value; // Stored as 1100
System.out.println(value); // 3
System.out.println(complement); // -4
```

==**remember this rule: to find the bitwise complement of a number, multiply it by negative one and then subtract one.**==

```java
System.out.println(-1 * value -1); // -4
System.out.println(-1 * complement -1); // 3
```

the negation operator `(-)` reverses the sign of a numeric expression

```java
double zooTemperature = 1.21;
System.out.println(zooTemperature); // 1.21
zooTemperature = -zooTemperature;
System.out.println(zooTemperature); // -1.21
zooTemperature = -(-zooTemperature);
System.out.println(zooTemperature); // -1.21
```

Notice that in the last example we used parentheses, `()`, for the negation operator, `-`, to apply the negation twice. If we had instead written `--` , then it would have been interpreted as the decrement operator and printed -2.21.

Based on the description, it might be obvious that some operators require the variable or expression they’re  acting on to be of a specific type. For example, you cannot apply a negation operator `(-)` to a boolean expression, nor can you apply a logical complement operator `(!)` to a numeric expression.

```java
int pelican = !5; // DOES NOT COMPILE
boolean penguin = -true; // DOES NOT COMPILE
boolean peacock = !0; // DOES NOT COMPILE
```

---
 **Keep an eye out for questions on the exam that use numeric values (such as 0 or 1) with `boolean` expressions. Unlike in some other programming languages, in Java, 1 and `true` are not related in any way, just as 0 and `false` are not related.** #TIP 

---

### Increment and Decrement Operators

==**Increment and decrement operators, `++` and `--`, respectively, can be applied to numeric variables and have a high order of precedence compared to binary operators. In other words, they are often applied first in an expression.**==

Increment and decrement operators require special care because the order in which they are attached to their associated variable can make a difference in how an expression is processed.

| Operator Type      | Example | Description                                               |
|---------------------|---------|-----------------------------------------------------------|
| Pre-increment       | `++w`   | Increases the value by 1 and returns the new value        |
| Pre-decrement       | `--x`   | Decreases the value by 1 and returns the new value        |
| Post-increment      | `y++`   | Increases the value by 1 and returns the original value  |
| Post-decrement      | `z--`   | Decreases the value by 1 and returns the original value  |
```java
int parkAttendance = 0;
System.out.println(parkAttendance); // 0
System.out.println(++parkAttendance); // 1
System.out.println(parkAttendance); // 1
System.out.println(parkAttendance--); // 1
System.out.println(parkAttendance); // 0
```

## Working with Binary Arithmetic Operators

operators that take two operands, called binary operators. Binary operators are by far the most common operators in the Java language.  Binary operators are often combined in complex expressions with other binary operators; therefore, operator precedence is very important in evaluating expressions containing binary operators.

| Operator Type | Example  | Description                                              |
|---------------|----------|----------------------------------------------------------|
| Addition      | `a + b`  | Adds two numeric values                                  |
| Subtraction   | `c - d`  | Subtracts two numeric values                              |
| Multiplication| `e * f`  | Multiplies two numeric values                              |
| Division      | `g / h`  | Divides one numeric value by another                      |
| Modulus       | `i % j`  | Returns the remainder after division of one numeric value by another |

Arithmetic operators also include the unary operators, ++ and --

```java
int price = 2 * 5 + 3 * 4 -8; // First, you evaluate the 2 * 5 and 3 * 4, which reduces the expression to this:
int price = 10 + 12 -8;
```

---

**All of the arithmetic operators may be applied to any Java primitives, with the exception of `boolean`.**

---

### Adding Parentheses

*Unless overridden with parentheses* prior to presenting Table 2.1 on operator precedence. That’s because you can change the order of operation explicitly by wrapping parentheses around the sections you want evaluated first.

**Changing the Order of Operation**

```java
int price = 2 * ((5 + 3) * 4 -8);
int price = 2 * (8 * 4 -8);
int price = 2 * (32 -8);
int price = 2 * 24;
```

---
**When you encounter code in your professional career in which you are not sure about the order of operation, feel free to add optional parentheses. While often not required, they can improve readability, especially as you’ll see with ternary operators.**  #TIP 

---

**Verifying Parentheses Syntax**

When working with parentheses, you need to make sure they are always valid and balanced.

```java
long pigeon = 1 + ((3 * 5) / 3; // DOES NOT COMPILE
int blueJay = (9 + 2) + 3) / (2 * 4; // DOES NOT COMPILE
```

When reading from left to right, a new right parenthesis must match a previous left parenthesis. Likewise, all left parentheses must be closed by right parentheses before the end of the expression.

```java
short robin = 3 + [(4 * 2) + 4]; // DOES NOT COMPILE
```

This example does not compile because Java, unlike some other programming languages, does not allow brackets, [], to be used in place of parentheses.

### Division and Modulus Operators

The modulus operator, sometimes called the remainder operator, is simply the remainder when two numbers are divided.

```java
System.out.println(9 / 3); // 3
System.out.println(9 % 3); // 0

System.out.println(10 / 3); // 3
System.out.println(10 % 3); // 1

System.out.println(11 / 3); // 3
System.out.println(11 % 3); // 2

System.out.println(12 / 3); // 4
System.out.println(12 % 3); // 0
```

Be sure to understand ==**the difference between arithmetic division and modulus. For integer values, division results in the floor value of the nearest integer that fulfills the operation, whereas modulus is the remainder value.**==

---

**The modulus operation is not limited to positive integer values in Java; it may also be applied to negative integers and floating-point numbers. For example, if the divisor is 5, then the modulus value of a negative number is between -4 and 0.**

---

### Numeric Promotion

==**each primitive numeric type has a bit-length. You don’t need to know the exact size of these types for the exam, but you should know which are bigger than others.**==

==**Numeric Promotion Rules**==

1. ==**If two values have different data types, Java will automatically promote one of the values to the larger of the two data types.**==
2. ==**If one of the values is integral and the other is floating-point, Java will automatically promote the integral value to the floating-point value’s data type.**==
3. ==**Smaller data types, namely, `byte`, `short`, and `char`, are first promoted to int any time they’re used with a Java binary arithmetic operator with a variable (as opposed to a value), even if neither of the operands is int.**==
4. ==**After all promotion has occurred and the operands have the same data type, the resulting value will have the same data type as its promoted operands.**==

The last two rules are the ones most people have trouble with and the ones likely to trip you up on the exam. For the third rule, note that unary operators are excluded from this rule. For example, applying ++ to a short value results in a short value.

**Examples**

- What is the data type of x * y?
```java
int x = 1;
long y = 33;
var z = x * y;
```

In this case, we follow the first rule. Since one of the values is `int` and the other is `long`, and `long` is larger than `int`, the `int` value x is first promoted to a`long`long. The result z is then a `long` value.

- What is the data type of x + y?
```java
double x = 39.21;
float y = 2.1;
var z = x + y;
```

This is actually a trick question, as ==**the second line does not compile! Floating-point literals are assumed to be double unless postfixed with an f, as in 2.1f.**== If the value of y was set properly to 2.1f, then the promotion would be similar to the previous example, with both operands being promoted to a `double`, and the result z would be a `double` value.

- What is the data type of x * y?
```java
short x = 10;
short y = 3;
var z = x * y;
```

On the last line, we must apply the third rule: that x and y will both be promoted to `int` before the binary multiplication operation, resulting in an output of type `int`. If you were to try to assign the value to a `short` variable z without casting, then the code would not compile. 

- What is the data type of w * x / y?
```java
short w = 14;
float x = 13;
double y = 30;
var z = w * x / y;
```

In this case, must apply all of the rules. First, w will automatically be promoted to `int` solely because it is a `short` and is being used in an arithmetic binary operation. The promoted w value will then be automatically promoted to a `float` so that it can be multiplied with x. The result of w * x will then be automatically promoted to a `double` so that it can be divided by y, resulting in a `double` value. 

When working with arithmetic operators in Java, you should always be aware of the data type of variables, intermediate values, and resulting values. You should apply operator precedence and parentheses and work outward, promoting data types along the way.

## Assigning Values

### Assignment Operator

An assignment operator is a binary operator that modifies, or assigns, the variable on the left side of the operator with the result of the value on the right side of the equation.  Unlike most other Java operators, the assignment operator is evaluated from right to left.

The simplest assignment operator is the `=` assignment

```java
int herd = 1;
```

==**Java will automatically promote from smaller to larger data types, on arithmetic operators, but it will throw a compiler exception if it detects that you are trying to convert from larger to smaller data types without casting.**==

| Operator     | Example         | Description                                      |
|--------------|-----------------|--------------------------------------------------|
| Assignment   | `int a = 50;`    | Assigns the value on the right to the variable on the left. |

### Casting Values

Casting is a unary operation where one data type is explicitly interpreted as another data type. ==**Casting is optional and unnecessary when converting to a larger or widening data type, but it is required when converting to a smaller or narrowing data type.**== Without casting, the compiler will generate an error when trying to put a larger data type inside a smaller one.

Casting is performed by placing the data type, enclosed in parentheses, to the left of the value you want to cast.

```java
int fur = (int)5;
int hair = (short) 2;
String type = (String) "Bird";
short tail = (short)(4 + 10);
long feathers = 10(long); // DOES NOT COMPILE
```

Spaces between the cast and the value are optional.  it is common for the right side to also be in parentheses. Since casting is a unary operation, it would only be applied to the 4 if we didn’t enclose 4 + 10 in parentheses.

On the one hand, it is convenient that the compiler automatically casts smaller data types to larger ones. On the other hand, it makes for great exam questions when they do the opposite to see whether you are paying attention

```java
float egg = 2.0 / 9; // DOES NOT COMPILE
int tadpole = (int)5 * 2L; // DOES NOT COMPILE
short frog = 3 -2.0; // DOES NOT COMPILE
```

All of these examples involve putting a larger value into a smaller data type. casting can also be applied to objects and references. In those cases, though, no conversion is performed. ==**Put simply, casting a numeric value may change the data type, while casting an object only changes the reference to the object, not the object itself.**==

**Reviewing Primitive Assignments**

```java
int fish = 1.0; // DOES NOT COMPILE
short bird = 1921222; // DOES NOT COMPILE
int mammal = 9f; // DOES NOT COMPILE
long reptile = 192_301_398_193_810_323; // DOES NOT COMPILE
```

The first statement does not compile because you are trying to assign a double 1.0 to an integer value.
The second statement does not compile because the literal value 1921222 is outside the range of short, and the compiler detects this. The third statement does not compile because the f added to the end of the number instructs the compiler to treat the number as a floating-point value, but the assignment is to an int. Finally the last statement does not compile because Java interprets the literal as an int and notices that the value is larger than int allows. The literal would need a postfix L or l to be considered a long.

**Applying Casting**

==**Remember, casting primitives is required any time you are going from a larger numerical data type to a smaller numerical data type, or converting from a floating-point number to an integral value.**==

```java
int fish = (int)1.0;
short bird = (short)1921222; // Stored as 20678
int mammal = (int)9f;
```

```java
long reptile = (long)192301398193810323; // DOES NOT COMPILE
```

**This still does not compile because the value is first interpreted as an int by the compiler and is out of range.** The following fixes this code without requiring casting:

```java
long reptile = 192301398193810323L;
```

---
**Overflow and Underflow** 

The second value, 1,921,222, is too large to be stored as a short, so numeric overflow occurs, and it becomes 20,678. **Overflow is when a number is so large that it will no longer fit within the data type, so the system “wraps around” to the lowest negative value and counts up from there, similar to how modulus arithmetic works.  There’s also an analogous underflow, when the number is too low to fit in the data type, such as storing -200 in a byte field.**

```java
System.out.print(2147483647+1); // -2147483648
```

Since 2147483647 is the maximum int value, adding any strictly positive value to it will cause it to wrap to the smallest negative number.

---

**Numeric Promotion Example**

```java
short mouse = 10;
short hamster = 3;
short capybara = mouse * hamster; // DOES NOT COMPILE
```

short values are automatically promoted to int when applying any arithmetic operator, with the resulting value being of type int. Trying to assign a short variable with an int value results in a compiler error, as Java thinks you are trying to implicitly convert from a larger data type to a smaller one.  can be fix by casting

```java
short mouse = 10;
short hamster = 3;
short capybara = (short)(mouse * hamster);
```
 
 By casting a larger value into a smaller data type, you instruct the compiler to ignore its default behavior. In other words, you are telling the compiler that you have taken additional steps to prevent overflow or underflow. It is also possible that in your particular application and scenario, overflow or underflow would result in acceptable values.

Last but not least, casting can appear anywhere in an expression, not just on the assignment.

```java
short mouse = 10;
short hamster = 3;
short capybara = (short)mouse * hamster; // DOES NOT COMPILE
```

casting was a unary operation. That means the cast in the last line is applied to mouse, and mouse alone. After the cast is complete, both operands are promoted to int since they are used with the binary multiplication operator `(*)`, making the result an int and causing a compiler error.

```java
short capybara = 1 + (short)(mouse * hamster); // DOES NOT COMPILE
```

casting is performed successfully, but the resulting value is automatically promoted to int because it is used with the binary arithmetic operator `(+)`.

### Casting Values vs. Variables

==**the compiler doesn’t require casting when working with literal values that fit into the data type.**==

```java
byte hat = 1;
byte gloves = 7 * 10;
short scarf = 5;
short boots = 2 + 1;
```

```java
short boots = 2 + hat; // DOES NOT COMPILE
byte gloves = 7 * 100; // DOES NOT COMPILE
```

The first statement does not compile because hat is a variable, not a value, and both operands are automatically promoted to int. When working with values, the compiler had enough information to determine the writer’s intent. When working with variables, though, there is ambiguity about how to proceed, so the compiler reports an error.

The second expression does not compile because 700 triggers an overflow for byte, which has a maximum value of 127.

### Compound Assignment Operators

| Operator               | Example      | Description                                                                      |
|------------------------|--------------|----------------------------------------------------------------------------------|
| Addition assignment    | `a += 5`      | Adds the value on the right to the variable on the left and assigns the sum to the variable.  |
| Subtraction assignment | `b -= 0.2`    | Subtracts the value on the right from the variable on the left and assigns the difference to the variable. |
| Multiplication assignment | `c *= 100` | Multiplies the value on the right with the variable on the left and assigns the product to the variable. |
| Division assignment    | `d /= 4`      | Divides the variable on the left by the value on the right and assigns the quotient to the variable. |
Compound operators are really just glorified forms of the simple assignment operator, with a built-in arithmetic or logical operation that applies the left and right sides of the statement and stores the resulting value in the variable on the left side of the statement. 

```java
int camel = 2, giraffe = 3;
camel = camel * giraffe; // Simple assignment operator
camel *= giraffe; // Compound assignment operator
```

The left side of the compound operator can be applied only to a variable that is already defined and cannot be used to declare a new variable.
==**Compound operators are useful for more than just shorthand—they can also save you from having to explicitly cast a value.**==

```java
long goat = 10;
int sheep = 5;
sheep = sheep * goat; // DOES NOT COMPILE
```

We are trying to assign a long value to an int variable. This last line could be fixed with an explicit cast to (int), but there’s a better way using the compound assignment operator:

```java
long goat = 10;
int sheep = 5;
sheep *= goat;
```

The compound operator will first cast sheep to a long, apply the multiplication of two long values, and then cast the result to an int. Unlike the previous example, in which the compiler reported an error, the compiler will automatically cast the resulting value to the data type of the value on the left side of the compound operator.

### Return Value of Assignment Operators

One final thing to know about assignment operators is that ==**the result of an assignment is an expression in and of itself equal to the value of the assignment.**==

```java
long wolf = 5;
long coyote = (wolf=3);
System.out.println(wolf); // 3
System.out.println(coyote); // 3
```

The key here is that `(wolf=3)` does two things. First, it sets the value of the variable wolf to be 3. Second, it returns a value of the assignment, which is also 3.

```java
boolean healthy = false;
if(healthy = true)
System.out.print("Good!");
```

While this may look like a test if healthy is true, it’s actually assigning healthy a value of true. The result of the assignment is the value of the assignment, which is true, resulting in this snippet printing Good!

## Comparing Values

The last set of binary operators revolves around comparing values. They can be used to check if two values are the same, check if one numeric value is less than or greater than another, and perform Boolean arithmetic.

## Equality Operators

Determining equality in Java can be a nontrivial endeavor as there’s a semantic difference between “two objects are the same” and “two objects are equivalent.” It is further complicated by the fact that for numeric and boolean primitives, there is no such distinction.

The equals operator `(==)` and not equals operator `(!=)` compare two operands and return a boolean value determining whether the expressions or values are equal or not equal, respectively.

| Operator   | Example | Apply to Primitives                                     | Apply to Objects                                      |
|------------|---------|---------------------------------------------------------|--------------------------------------------------------|
| Equality   | a == 10 | Returns true if the two values represent the same value | Returns true if the two values reference the same object |
| Inequality | b != 3.14 | Returns true if the two values represent different values | Returns true if the two values do not reference the same object |
==**The equality operator can be applied to numeric values, `boolean` values, and objects (including `String` and `null`). When applying the equality operator, you cannot mix these types.**==

```java
boolean monkey = true == 3; // DOES NOT COMPILE
boolean ape = false != "Grape"; // DOES NOT COMPILE
boolean gorilla = 10.2 == "Koko"; // DOES NOT COMPILE
```

==**Pay close attention to the data types when you see an equality operator on the exam.**==

```java
boolean bear = false;
boolean polar = (bear = true);
System.out.println(polar); // true
```

In this example, though, the expression is assigning the value of `true` to `bear`, and on assignment operators, the assignment itself has the value of the assignment. Therefore, polar is also assigned a value of `true`, and the output is `true`.

==**For object comparison, the equality operator is applied to the references to the objects, not the objects they point to. Two references are equal if and only if they point to the same object or both point to null.**==

```java
var monday = new File("schedule.txt");
var tuesday = new File("schedule.txt");
var wednesday = tuesday;
System.out.println(monday == tuesday); // false
System.out.println(tuesday == wednesday); // true
```

Even though all of the variables point to the same file information, only two references, `tuesday` and `wednesday`, are equal in terms of `==` since they point to the same object.

==**In some languages, comparing null with any other value is always false, although this is not the case in Java.**==

```java
System.out.print(null == null); // true
```

### Relational Operators

compare two expressions and return a `boolean` value. 

| Operator          | Example             | Description                                                |
|-------------------|---------------------|------------------------------------------------------------|
| Less than         | `a < 5`             | Returns true if the value on the left is strictly less than the value on the right |
| Less than or equal to | `b <= 6`         | Returns true if the value on the left is less than or equal to the value on the right |
| Greater than      | `c > 9`             | Returns true if the value on the left is strictly greater than the value on the right |
| Greater than or equal to | `3 >= d`      | Returns true if the value on the left is greater than or equal to the value on the right |
| Type comparison   | `e instanceof String` | Returns true if the reference on the left side is an instance of the type on the right side (class, interface, record, enum, annotation) |

**Numeric Comparison Operators**

The first four relational operators in Table 2.8 apply only to numeric values. ==**If the two numeric operands are not of the same data type, the smaller one is promoted**==

```java
int gibbonNumFeet = 2, wolfNumFeet = 4, ostrichNumFeet = 2;
System.out.println(gibbonNumFeet < wolfNumFeet); // true
System.out.println(gibbonNumFeet <= wolfNumFeet); // true
System.out.println(gibbonNumFeet >= ostrichNumFeet); // true
System.out.println(gibbonNumFeet > ostrichNumFeet); // false
```

**`instanceof` Operator**

It is useful for determining whether an arbitrary object is a member of a particular class or interface at runtime.
For now, all you need to know is objects can be passed around using a variety of references. For example, all classes inherit from `java.lang.Object`. This means that any instance can be assigned to an Object reference.

```java
Integer zooTime = Integer.valueOf(9);
Number num = zooTime;
Object obj = zooTime;
```

In this example, only one object is created in memory, but there are three different references to it because `Integer` inherits both `Number` and `Object`. This means that you can call instanceof on any of these references with three different data types, and it will return true for each of them.

```java
public void openZoo(Number time) {}
```

Now, want the function to add O'clock to the end of output if the value is a whole number type, such as an Integer; otherwise, it just prints the value.

```java
public void openZoo(Number time) {
if (time instanceof Integer)
System.out.print((Integer)time + " O'clock");
else
System.out.print(time);
}
```

It is common to use casting with instanceof when working with objects that can be various different types, since casting gives you access to fields available only in the more specific classes. **It is considered a good coding practice to use the instanceof operator prior to casting from one object to a narrower type.**

**Invalid instanceof**

One area the exam might try to trip you up on is using `instanceof` with incompatible types. For example, `Number` cannot possibly hold a String value, so the following causes a compilation error:

```java
public void openZoo(Number time) {
if(time instanceof String) // DOES NOT COMPILE
System.out.print(time);
}
```

**null and the instanceof operator**
==**calling instanceof on the null literal or a null reference always returns false.**==

```java
System.out.print(null instanceof Object); // false
Object noObjectHere = null;
System.out.print(noObjectHere instanceof String); // false
```

### Logical Operators

The logical operators, `(&)`, `(|)`, and `(^)`, may be applied to both numeric and boolean data types;  ==**When they’re applied to boolean data types, they’re referred to as logical operators. Alternatively, when they’re applied to numeric data types, they’re referred to as bitwise operators**==, as they perform bitwise comparisons of the bits that compose the number. 

| Operator              | Example     | Description                                                    |
|-----------------------|-------------|----------------------------------------------------------------|
| Logical AND           | `a & b`     | Value is true only if both values are true.                    |
| Logical inclusive OR  | `c \| d`    | Value is true if at least one of the values is true.           |
| Logical exclusive OR  | `e ^ f`     | Value is true only if one value is true and the other is false.|
![[Pasted image 20240118220950.png]]


- ==**AND is only true if both operands are true.**==
- ==**Inclusive OR is only false if both operands are false.**==
- ==**Exclusive OR is only true if the operands are different.**==

```java
boolean resting = eyesClosed | breathingSlowly;
boolean asleep = eyesClosed & breathingSlowly;
boolean awake = eyesClosed ^ breathingSlowly;
System.out.println(resting); // true
System.out.println(asleep); // true
System.out.println(awake); // false
```

### Conditional Operators

| Operator          | Example    | Description                                                                      |
|-------------------|------------|----------------------------------------------------------------------------------|
| Conditional AND   | `a && b`   | Value is true only if both values are true. If the left side is false, then the right side will not be evaluated. |
| Conditional OR    | `c \|\| d` | Value is true if at least one of the values is true. If the left side is true, then the right side will not be evaluated. |
The conditional operators, often called short-circuit operators, are nearly identical to the logical operators, `&` and `|`, ==**except that the right side of the expression may never be evaluated if the final result can be determined by the left side of the expression.**==

```java
int hour = 10;
boolean zooOpen = true || (hour < 4);
System.out.println(zooOpen); // true
```

Since we know the left side is true, there’s no need to evaluate the right side, since no value of hour will ever make this code print `false`. In other words, hour could have been -10 or 892; the output would have been the same.

### Avoiding a `NullPointerException`

A more common example of where conditional operators are used is checking for `null` objects before performing an operation.

```java
if(duck!=null & duck.getAge()<5) { // Could throw a NullPointerException
// Do something
}
```
 
 The issue is that the logical `AND (&)` operator evaluates both sides of the expression. We could add a second if statement, but this could get unwieldy if we have a lot of variables to check. An easy-to- read solution is to use the conditional `AND` operator `(&&)`:

```java
if(duck!=null && duck.getAge()<5) {
// Do something
}
```

### Checking for Unperformed Side Effects

==**Be wary of short-circuit behavior on the exam, as questions are known to alter a variable on the right side of the expression that may never be reached. This is referred to as an unperformed side effect.**==

```java
int rabbit = 6;
boolean bunny = (rabbit >= 6) || (++rabbit <= 7);
System.out.println(rabbit);
```

Because `rabbit >= 6` is `true`, the increment operator on the right side of the expression is never evaluated, so the output is 6.

## Making Decisions with the Ternary Operator

It is notable in that it is the only operator that takes three operands.
```java
booleanExpression ? expression1 : expression2
```

==**The first operand must be a boolean expression, and the second and third operands can be any expression that returns a value.** ==The ternary operation is really a condensed form of a combined if and else statement that returns a value.

```java
for an owl:
int owl = 5;
int food;
if(owl < 2) {
food = 3;
} else {
food = 4;
}
System.out.println(food); // 4
```

```java
int owl = 5;
int food = owl < 2 ? 3 : 4;
System.out.println(food); // 4
```

These two code snippets are equivalent. Note that it is often helpful for readability to add parentheses around the expressions in ternary operations, although doing so is certainly not required.

```java
int food1 = owl < 4 ? owl > 2 ? 3 : 4 : 5;
int food2 = (owl < 4 ? ((owl > 2) ? 3 : 4) : 5);
```

For the exam, you should know that there is no requirement that second and third expressions in ternary operations have the same data types, although it does come into play when combined with the assignment operator.

```java
int stripes = 7;
System.out.print((stripes > 5) ? 21 : "Zebra");
int animal = (stripes < 9) ? 3 : "Horse"; // DOES NOT COMPILE
```

Both expressions evaluate similar `boolean` values and return an `int` and a `String`, although only the first one will compile. `System.out.print()` does not care that the expressions are completely different types, because it can convert both to Object values and call `toString()` on them. On the other hand, the compiler does know that "Horse" is of the wrong data type and cannot be assigned to an int; therefore, it does not allow the code to be compiled.

---
**Ternary Expression and Unperformed Side Effects** #TIP 

ternary expression can contain an unperformed side effect, as only one of the expressions on the right side will be evaluated at runtime.

```java
int sheep = 1;
int zzz = 1;
int sleep = zzz<10 ? sheep++ : zzz++;
System.out.print(sheep + "," + zzz); // 2,1
```

Notice that since the left-hand `boolean` expression was true, only sheep was incremented.

```java
int sheep = 1;
int zzz = 1;
int sleep = sheep>=10 ? sheep++ : zzz++;
System.out.print(sheep + "," + zzz); // 1,2
```

Now that the left-hand boolean expression evaluates to false, only `zzz` is incremented.

---

## Summary  #OCP_Summary 

==**This chapter provides a comprehensive overview of Java operators, encompassing unary, binary, and ternary operators. Familiarity with these operators is crucial, and if any are not yet well-understood, a thorough study is recommended. A solid grasp of how to utilize the various Java operators covered in this chapter, coupled with an understanding of operator precedence and the impact of parentheses on expression interpretation, is essential.**==

==**During the exam, seemingly unrelated questions may actually test knowledge of specific operators, potentially causing compilation failures. Always scrutinize numeric operators, verifying that appropriate data types are used and match where necessary. Since operators are pervasive in exam code samples, a strong comprehension of this chapter enhances preparedness for the OCP**==

## Exam Essentials #Essential 

**Be able to recognize which operators are associated with which data types.**  This chapter covered a wide variety of operator symbols. Go back and review them several times so that you are familiar with them throughout the rest of the book.

**Be able to recognize which operators are associated with which data types.** Some operators may be applied only to numeric primitives, some only to boolean values, and some only to objects. It is important that you notice when an operator and operand(s) are mismatched, as this issue is likely to come up in a couple of exam questions.

**Understand when casting is required or numeric promotion occurs.** Whenever you mix operands of two different data types, the compiler needs to decide how to handle the resulting data type. ==**When you’re converting from a smaller to a larger data type, numeric promotion is automatically applied. When you’re converting from a larger to a smaller data type casting is required.**==

**Understand Java operator precedence.** Most Java operators you’ll work with are binary, but the number of expressions is often greater than two. Therefore, you must understand the order in which Java will evaluate each operator symbol.

**Be able to write code that uses parentheses to override operator precedence.** can use parentheses in your code to manually change the order of precedence.

## Review Questions

1. Which of the following Java operators can be used with boolean variables? (Choose all that apply.)
A. ==
B. +
C. --
D. !
E. %
F. ~
G. Cast with (boolean)

**My Answer:  A,D,G**
**Correct Answer: A,D,G**

**Option F is a bitwise complement operator and can only be applied to integer values. Finally,**
**option G is correct, as you can cast a boolean variable since boolean is a type.**

---

2. What data type (or types) will allow the following code snippet to compile? (Choose all that apply.)

```java
byte apples = 5;
short oranges = 10;
_____ bananas = apples + oranges;
```

A. int
B. long
C. boolean
D. double
E. short
F. byte

**My Answer : A**
**Correct Answer: A,B,D**

**The expression apples + oranges is automatically promoted to int, so int and data types that can be promoted automatically from int will work. Options A, B, and D are such data types.** 

---

3. What change, when applied independently, would allow the following code snippet to compile? (Choose all that apply.)

```java
3: long ear = 10;
4: int hearing = 2 * ear;
```

A. No change; it compiles as is.
B. Cast ear on line 4 to int.
C. Change the data type of ear on line 3 to short.
D. Cast 2 * ear on line 4 to int.
E. Change the data type of hearing on line 4 to short.
F. Change the data type of hearing on line 4 to long.

**My Answer : B,C,D,F**
**Correct Answer: B,C,D,F**

---

4. What is the output of the following code snippet?

```java
3: boolean canine = true, wolf = true;
4: int teeth = 20;
5: canine = (teeth != 10) ^ (wolf=false);
6: System.out.println(canine+", "+teeth+", "+wolf);
```

A. true, 20, true
B. true, 20, false
C. false, 10, true
D. false, 20, false
E. The code will not compile because of line 5.
F. None of the above.

**My Answer : D**
**Correct Answer: B**

---

5. Which of the following operators are ranked in increasing or the same order of precedence? Assume the + operator is binary addition, not the unary form. (Choose all that apply.)

`A. +, *, %, --`
`B.`
`++, (int), *`
`C. =, ==, !`
`D. (short), =, !, *`
`E. *, /, %, +, ==`
`F. !, ||, &`
`G. ^, +, =, +=`

**My Answer : A,C**
**Correct Answer: A,C**



---

6. What is the output of the following program?

```java
1: public class CandyCounter {
2: static long addCandy(double fruit, float vegetables) {
3: return (int)fruit+vegetables;
4: }
5:
6: public static void main(String[] args) {
7: System.out.print(addCandy(1.4, 2.4f) + ", ");
8: System.out.print(addCandy(1.9, (float)4) + ", ");
9: System.out.print(addCandy((long)(int)(short)2, (float)4)); } }
```
A. 4, 6, 6.0
B. 3, 5, 6
C. 3, 6, 6
D. 4, 5, 6
E. The code does not compile because of line 9.
F. None of the above.

**My Answer : F**
**Correct Answer: F**

**The code does not compile because line 3 contains a compilation error. The cast (int) is applied to fruit, not the expression `fruit+vegetables`. Since the cast operator has a higher operator precedence than the addition operator, it is applied to fruit, but the expression is promoted to a float, due to vegetables being float. The result cannot be returned as long in the `addCandy()` method without a cast. For this reason, option F is correct. If parentheses were added around `fruit+vegetables`, then the output would be 3, 5, 6, and option B would be correct. Remember that ==casting floating-point numbers to integral values results in truncation, not rounding.==**

---

7. What is the output of the following code snippet?

```java
int ph = 7, vis = 2;
boolean clear = vis > 1 & (vis < 9 || ph < 2);
boolean safe = (vis > 2) && (ph++ > 1);
boolean tasty = 7 <= -- ph;
System.out.println(clear + "-" + safe + "-" + tasty);
```

A. true-true-true
B. true-true-false
C. true-false-true
D. true-false-false
E. false-true-true
F. false-true-false
G. false-false-true
H. false-false-false

**My Answer : H**
**Correct Answer: D**

---

8. What is the output of the following code snippet?

```java
4: int pig = (short)4;
5: pig = pig++;
6: long goat = (int)2;
7: goat -= 1.0;
8: System.out.print(pig + " -" + goat);
```

A. 4 -1
B. 4 -2
C. 5 -1
D. 5 -2
E. The code does not compile due to line 7.
F. None of the above.

**My Answer : E**
**Correct Answer: A**

**Line 7 does not produce a compilation error since ==the compound operator applies casting automatically==.**

---

9. What are the unique outputs of the following code snippet? (Choose all that apply.)

```java
int a = 2, b = 4, c = 2;
System.out.println(a > 2 ? -- c: b++);
System.out.println(b = (a!=c ? a : b++));
System.out.println(a > b ? b < c ? b : 2 : 1);
```

A. 1
B. 2
C. 3
D. 4
E. 5
F. 6
G. The code does not compile.

**My Answer : A**
**Correct Answer: A,D,E**

---

10. What are the unique outputs of the following code snippet? (Choose all that apply.)

```java
short height = 1, weight = 3;
short zebra = (byte) weight * (byte) height;
double ox = 1 + height * 2 + weight;
long giraffe = 1 + 9 % height + 1;
System.out.println(zebra);
System.out.println(ox);
System.out.println(giraffe);
```

A. 1
B. 2
C. 3
D. 4
E. 5
F. 6
G. The code does not compile.

**My Answer : G**
**Correct Answer: G**
 
 **The code does not compile due to an error on the second line. Even though both height and weight are cast to byte, the multiplication operator automatically promotes them to int, resulting in an attempt to store an int in a short variable**

---

11. What is the output of the following code?

```java
11: int sample1 = (2 * 4) % 3;
12: int sample2 = 3 * 2 % 3;
13: int sample3 = 5 * (1 % 2);
14: System.out.println(sample1 + ", " + sample2 + ", " + sample3);
```

A. 0, 0, 5
B. 1, 2, 10
C. 2, 1, 5
D. 2, 0, 5
E. 3, 1, 10
F. 3, 2, 6
G. The code does not compile.

**My Answer : D**
**Correct Answer: D**

---

12. The _________ operator increases a value and returns the original value, while the _______ operator decreases a value and returns the new value.
A. post-increment, post-increment
B. pre-decrement, post-decrement
C. post-increment, post-decrement
D. post-increment, pre-decrement
E. pre-increment, pre-decrement
F. pre-increment, post-decrement

**My Answer : C**
**Correct Answer: D**

---

13. What is the output of the following code snippet?

```java
boolean sunny = true, raining = false, sunday = true;
boolean goingToTheStore = sunny & raining ^ sunday;
boolean goingToTheZoo = sunday && !raining;
boolean stayingHome = !(goingToTheStore && goingToTheZoo);
System.out.println(goingToTheStore + "-" + goingToTheZoo + "-" +stayingHome);
```

A. true-false-false
B. false-true-false
C. true-true-true
D. false-true-true
E. false-false-false
F. true-true-false
G. None of the above

**My Answer : F**
**Correct Answer: F**

---

14. Which of the following statements are correct? (Choose all that apply.)

A. The return value of an assignment operation expression can be void.
B. The inequality operator (!=) can be used to compare objects.
C. The equality operator (`==`) can be used to compare a boolean value with a numeric
value.
D. During runtime, the & and | operators may cause only the left side of the expression to
be evaluated.
E. The return value of an assignment operation expression is the value of the newly
assigned variable.
F. In Java, 0 and false may be used interchangeably.
G. The logical complement operator (!) cannot be used to flip numeric values.

**My Answer : B,E,G**
**Correct Answer: B,E,G**

---

15. Which operators take three operands or values? (Choose all that apply.)

A. =
B. &&
C. *=
D. ? :
E. &
F. ++
G. /

**My Answer : D**
**Correct Answer: D**

---

16. How many lines of the following code contain compiler errors?

```java
int note = 1 * 2 + (long)3;
short melody = (byte)(double)(note *= 2);
double song = melody;
float symphony = (float)((song == 1_000f) ? song * 2L : song);
```

A. 0
B. 1
C. 2
D. 3
E. 4

**My Answer : C**
**Correct Answer: B**

**The first line contains a compilation error. The value 3 is cast to long. The 1 * 2 value is evaluated as int but promoted to long when added to the 3. Trying to store a long value in an int variable triggers a compiler error. The other lines do not contain any compilation errors, as they store smaller values in larger or same-size data types**

---

17. Given the following code snippet, what are the values of the variables after it is executed? (Choose all that apply.)

```java
int ticketsTaken = 1;
int ticketsSold = 3;
ticketsSold += 1 + ticketsTaken++;
ticketsTaken *= 2;
ticketsSold += (long)1;
```

A. ticketsSold is 8.
B. ticketsTaken is 2.
C. ticketsSold is 6.
D. ticketsTaken is 6.
E. ticketsSold is 7.
F. ticketsTaken is 4.
G. The code does not compile.

**My Answer : G**
**Correct Answer: C,F**

**Note the last line does not trigger a compilation error as the compound operator automatically casts the right-hand operand.**

---

18. Which of the following can be used to change the order of operation in an expression? (Choose all that apply.)
A. [ ]
B. < >
C. ( )
D. \ /
E. { }
F. " "

**My Answer : C**
**Correct Answer: C**

---

19. What is the result of executing the following code snippet? (Choose all that apply.)

```JAVA
3: int start = 7;
4: int end = 4;
5: end += ++start;
6: start = (byte)(Byte.MAX_VALUE + 1);
```

A. start is 0.
B. start is -128.
C. start is 127.
D. end is 8.
E. end is 11.
F. end is 12.
G. The code does not compile.
H. The code compiles but throws an exception at runtime.

**My Answer : B,F**
**Correct Answer: B,F**

---

20. Which of the following statements about unary operators are true? (Choose all that apply.)
A. Unary operators are always executed before any surrounding numeric binary or ternary operators.
B. The -operator can be used to flip a boolean value.
C. The pre-increment operator (++) returns the value of the variable before the increment is applied.
D. The post-decrement operator (-- )returns the value of the variable before the decrement is applied.
E. The ! operator cannot be used on numeric values.
F. None of the above

**My Answer : A,D,E**
**Correct Answer: A,D,E**

---

21.  What is the result of executing the following code snippet?
```java
int myFavoriteNumber = 8;
int bird = ~myFavoriteNumber;
int plane = -myFavoriteNumber;
var superman = bird == plane ? 5 : 10;
System.out.println(bird + "," + plane + "," + --superman);
```

A. -7,-
8,9
B. -7,-
8,10
C. -8,-
8,4
D. -8,-
8,5
E. -9,-
8,9
F. -9,-
8,10
G. None of the above

**My Answer : E**
**Correct Answer: E**

---

# Chapter 3 - Making Decisions #Chapter

## Creating Decision-Making Statements

### Statements and Blocks

a Java statement is a complete unit of execution in Java, terminated with a semicolon `(;)`. 
*Control flow* statements break up the flow of execution by using decision-making, looping, and branching, allowing the application to selectively execute particular segments of code.

a block of code in Java is a group of zero or more statements between balanced braces `({})` and can be used anywhere a single statement is allowed.

```java
// Single statement
patrons++;

// Statement inside a block
{
patrons++;
}
```

A statement or block often serves as the target of a decision-making statement.

```java
// Single statement
if(ticketsTaken > 1)
patrons++;
// Statement inside a block
if(ticketsTaken > 1)
{
patrons++;
}
```

the target of a decision-making statement can be a single statement or block of statements.

---
**While both of the previous examples are equivalent, stylistically using blocks is often preferred, even if the block has only one statement. The second form has the advantage that you can quickly insert new lines of code into the block, without modifying the surrounding structure.**

---

### The `if` Statement

==**The `if` statement, execute a particular block of code if and only if a `boolean` expression evaluates to `true` at runtime.**==

```java
if(hourOfDay < 11)
	System.out.println("Good Morning");

if(hourOfDay < 11) {
	System.out.println("Good Morning");
morningGreetingCount++;
}
```

---
**Watch Indentation and Braces**  #TIP
**One area where the exam writers will try to trip you up is if statements without braces `({})`. For example, take a look at this slightly modified form of our example:**

```java
if(hourOfDay < 11)
	System.out.println("Good Morning");
morningGreetingCount++;
```
 
 **Based on the indentation, you might be inclined to think the variable `morningGreetingCount` is only going to be incremented if `hourOfDay` is less than 11, but that’s not what this code does. It will execute the print statement only if the condition is met, but it will always execute the increment operation.** 

**in Java, unlike some other programming languages, tabs are just whitespace and are not evaluated as part of the execution. When you see a control flow statement in a question, be sure to trace the open and close braces of the block, ignoring any indentation you may come across.**

---

### The `else` Statement

```java
if(hourOfDay < 11) {
	System.out.println("Good Morning");
}
if(hourOfDay >= 11) {
	System.out.println("Good Afternoon");
}
```

**redundant**

```java
if(hourOfDay < 11) {
	System.out.println("Good Morning");
} else System.out.println("Good Afternoon");
```

code is truly branching between one of the two possible options, with the `boolean` evaluation happening only once. The `else` operator takes a statement or block of statements, in the same manner as the `if` statement. Similarly, we can append additional if statements to an else block to arrive at a more refined

```java
if(hourOfDay < 11) {
	System.out.println("Good Morning");
} else if(hourOfDay < 15) {
	System.out.println("Good Afternoon");
} else {
	System.out.println("Good Evening");
}
```

---
**Verifying That the if Statement Evaluates to a Boolean Expression**

**Another common way the exam may try to lead you astray is by providing code where the `boolean` expression inside the if statement is not actually a boolean expression**

```java
int hourOfDay = 1;
if(hourOfDay) { // DOES NOT COMPILE
...
}
```

---

### Shortening Code with Pattern Matching

Pattern matching is reduce the boilerplate in your code.  A lot of the newer enhancements to the Java language focus on reducing boilerplate code.

```java
void compareIntegers(Number number) {
	if(number instanceof Integer) {
		Integer data = (Integer)number;
		System.out.print(data.compareTo(5));
	}
}
```

The cast is needed since the `compareTo()` method is defined on Integer, but not on Number. 

```java
void compareIntegers(Number number) {
	if(number instanceof Integer data) { 
		System.out.print(data.compareTo(5));
	}
}
```

==**The variable data in this example is referred to as the pattern variable**==. Notice that this code also avoids any potential `ClassCastException` because the cast operation is executed only if the implicit instanceof operator returns true.

==**The pattern variables are those that store data from the target only if the predicate returns `true` which is `instanceof`**==

---

**Reassigning Pattern Variables**

**While possible, it is a bad practice to reassign a pattern variable since doing so can lead to ambiguity about what is and is not in scope.**

```java
if(number instanceof Integer data) {
	data = 10;
}
```

**The reassignment can be prevented with a `final` modifier, but it is better not to reassign the variable at all.**

```java
if(number instanceof final Integer data) {
	data = 10; // DOES NOT COMPILE
}
```

---

#### Pattern Variables and Expressions

```java
void printIntegersGreaterThan5(Number number) {
	if(number instanceof Integer data && data.compareTo(5)>0)
	System.out.print(data);
}
```

We can apply a number of filters, or patterns, so that the if statement is executed only in specific circumstances. ==**Notice that we’re using the pattern variable in an expression in the same line in which it is declared.**==

#### Subtypes

==**The type of the pattern variable must be a subtype of the variable on the left side of the expression. It also cannot be the same type. This rule does not exist for traditional `instanceof` operator expressions**==, though

```java
Integer value = 123;
if(value instanceof Integer) {}
if(value instanceof Integer data) {} // DOES NOT COMPILE
```

While the second line compiles, ==**the last line does not compile because pattern matching requires that the pattern variable type Integer be a strict subtype of Integer.**==


---
**Limitations of Subtype Enforcement**

The compiler has some limitations on enforcing pattern matching types when we mix classes and interfaces. For example, given the non-final class Number and interface List, this does compile even though they are unrelated:

```java
Number value = 123;
if(value instanceof List) {}
if(value instanceof List data) {}
```

```java
private static void patternMatchingMethodSample(Animal animal) {  
	if (animal instanceof Bird obj) {  
		System.out.println("Bird object!");  
	} else if (animal instanceof Dog obj) {  
		System.out.println("Dog object!");  
	} else if (animal instanceof Cat obj) {  
		System.out.println("Cat object!");  
	}//else if (animal instanceof Animal obj) { } // DOES NOT COMPILE  
	else if (animal instanceof Walkable obj) {  
		System.out.println("Walkable obj");  
	}    }}  
  
interface Flyable {  
  
}  
  
interface Walkable {  
}  
  
class Bird extends Animal implements Flyable {  
  
}  
  
class Chicken extends Bird implements Walkable {  
}  
  
final class Cat extends Animal {  
}  
  
class Dog extends Animal {  
}  
  
class Animal {  
}  
  
class Horse extends Animal implements Walkable {  
}
```

---

#### Flow Scoping

The compiler applies flow scoping when working with pattern matching. ==**Flow scoping means the variable is only in scope when the compiler can definitively determine its type.**== 

Flow scoping is unlike any other type of scoping in that it is not strictly hierarchical like instance, class, or local scoping. It is determined by the compiler based on the branching and flow of the program.

```java
void printIntegersOrNumbersGreaterThan5(Number number) {
	if(number instanceof Integer data || data.compareTo(5)>0) // DOES NOT COMPILE
		System.out.print(data);
}
```

If the input does not inherit Integer, the data variable is undefined. Since the compiler cannot guarantee that data is an instance of Integer, data is not in scope, and the code does not compile. 

```java
void printIntegerTwice(Number number) {
if (number instanceof Integer data)
	System.out.print(data.intValue());
	System.out.print(data.intValue()); // DOES NOT COMPILE
}
```

Since the input might not have inherited Integer, data is no longer in scope after the if statement.

```java
void printOnlyIntegers(Number number) {
if (!(number instanceof Integer data))
	return;
System.out.print(data.intValue());
}
```

this code does compile! The method returns if the input does not inherit Integer. This means that when the last line of the method is reached, the input must inherit Integer, and therefore data stays in scope even after the if statement ends.

---
**Flow Scoping and else Branches**

**Another way to think about it is to rewrite the logic to something equivalent that uses an `else` statement:**

```java
void printOnlyIntegers(Number number) {
	if (!(number instanceof Integer data))
		return;
	else
		System.out.print(data.intValue());
	}
```

**go one step further and reverse the if and else branches by inverting the boolean expression:**

```java
void printOnlyIntegers(Number number) {
	if (number instanceof Integer data)
		System.out.print(data.intValue());
	else
		return;
	}
```

**new code is equivalent to our original and better demonstrates how the compiler was able to determine that data was in scope only when number is an Integer.**

```java
public static boolean bigEnoughRect(Shape s) {
    if (!(s instanceof Rectangle r)) {
        // This block checks whether the object "s" is of type "Rectangle".
        // If not, it enters this block.
        
        // Inside this block, it is not possible to use the pattern variable "r"
        // because the pattern matching expression (s instanceof Rectangle) is false,
        // and the "r" pattern variable is only valid in the matching case.
        
        return false; // Return false if the object is not of type "Rectangle".
    }

    // If the above condition is true, we reach this point.
    // This means that the object "s" is of type "Rectangle" and the pattern variable "r" is valid from this point onward.

    // Now, we can use the "r" pattern variable because at this point, the expression "s instanceof Rectangle" is true.
    // The "r" pattern variable represents the "s" object, which is now of type "Rectangle".

    return r.length() > 5;
}
```

```java
public static boolean bigEnoughRect(Shape s) {
        if (s instanceof Rectangle r) {
            r = (Rectangle) s; // Assign value inside the if block
        } else {
	        return false;
        }
        // You can use r here.
        return r.length() > 5; 
    }
```

---

==**In particular, it is possible to use a pattern variable outside of the if statement, but only when the compiler can definitively determine its type.**==
## Applying `switch` Statements

```java
public void printDayOfWeek(int day) {
if(day == 0)
System.out.print("Sunday");
else if(day == 1)
System.out.print("Monday");
else if(day == 2)
System.out.print("Tuesday");
else if(day == 3)
System.out.print("Wednesday");
...
}
```

code that is long, difficult to read, and often not fun to maintain

###  The `switch` Statement 

A switch statement is a complex decision-making structure in which a single value is evaluated and flow is redirected to the first matching branch, known as a case statement. If no such case statement is found that matches the value, an optional default statement will be called. If no such default option is available, the entire switch statement will be skipped.

![[Pasted image 20240126183854.png]]

**Because `switch` statements can be longer than most decision-making statements, the exam may present invalid `switch` syntax to see whether you are paying attention.**

---
**Combining case Values**

**Starting with Java 14, case values can now be combined:**

```java
switch(animal) {
case 1,2: System.out.print("Lion");
case 3: System.out.print("Tiger");
}
```

---

```java
int month = 5;
switch month { // DOES NOT COMPILE
case 1: System.out.print("January");
}

switch(month) // DOES NOT COMPILE
case 1: System.out.print("January");

switch(month) {
case 1: 2: System.out.print("January"); // DOES NOT COMPILE
}
```

- **==The first switch statement does not compile because it is missing parentheses around the switch variable.==** 
- **==The second statement does not compile because it is missing braces around the switch body.==**
- **==The third statement does not compile because a comma `(,)` should be used to separate combined case statements, not a colon `(:)`.==**
- ==**a switch statement is not required to contain any case statements.**==

```java
switch(month) {} // Perfectly Valid !!!
```

```java
public void printDayOfWeek(int day) {
switch(day) {
case 0:
System.out.print("Sunday");
break;
case 1:
System.out.print("Monday");
break;
case 2:
System.out.print("Tuesday");
break;
case 3:
System.out.print("Wednesday");
break;
case 4:
System.out.print("Thursday");
break;
case 5:
System.out.print("Friday");
break;
case 6:
System.out.print("Saturday");
break;
default:
System.out.print("Invalid value");
break;
} }
```

### Exiting with `break` Statements

`break` statement terminates the ``switch`` statement and returns flow control to the enclosing process. Put simply, it ends the ``switch`` statement immediately.

The ``break`` statements are optional, but without them the code will execute every branch following a matching case statement, including any default statements it finds. Without ``break`` statements in each branch, the order of case and default statements is now extremely important.

```java
switch(month) {
case 1, 2, 3: System.out.print("Winter");
case 4, 5, 6: System.out.print("Spring");
default: System.out.print("Unknown");
case 7, 8, 9: System.out.print("Summer");
case 10, 11, 12: System.out.print("Fall");
} }
```

the output: 
```text
WinterSpringUnknownSummerFall
```

---
**The exam creators are fond of ``switch`` examples that are missing ``break`` statements! When evaluating ``switch`` statements on the exam, always consider that multiple branches may be visited in a single execution.** #TIP 

---

### Selecting ``switch`` Data Types

a switch statement has a target variable that is not evaluated until runtime. The type of this target can include select primitive data types (``int, byte, short, char``) and their associated wrapper classes (``Integer, Byte, Short, Character``)
The following all data types supported by switch statements

- ==**``int`` and ``Integer``**==
- ==**``byte`` and ``Byte``**==
- ==**``short`` and ``Short``**==
- ==**``char`` and ``Character``**==
- ==**``String``**==
- ==**``enum`` values**==
- ==**``var`` (if the type resolves to one of the preceding types)**==

---
**``boolean``, ``long``, ``float``, and ``double`` are excluded from switch statements, as are their associated ``Boolean``, ``Long``, ``Float``, and ``Double`` classes. The reasons are varied, such as boolean having too small a range of values and floating-point numbers having quite a wide range of values. For the exam, though, you just need to know that they are not permitted in switch statements.**

---

### Determining Acceptable Case Values

Not just any variable or value can be used in a case statement. First, ==**the values in each case statement must be compile-time constant values of the same data type as the switch value. This means you can use only literals, enum constants, or final constant variables of the same data type.**== By final constant, we mean that the variable must be marked with the final modifier and initialized with a literal value in the same expression in which it is declared.

```java
final int getCookies() { return 4; }
void feedAnimals() {
final int bananas = 1;
int apples = 2;
int numberOfAnimals = 3;
final int cookies = getCookies();
switch(numberOfAnimals) {
case bananas:
case apples: // DOES NOT COMPILE
case getCookies(): // DOES NOT COMPILE
case cookies : // DOES NOT COMPILE
case 3 * 5 :
} }
```

- The ``bananas`` variable is marked ``final``, and its value is known at compile-time, so it is valid. 
- The `apples` variable is not marked ``final``, even though its value is known, so it is not permitted.
- The next two case statements, with values ``getCookies()`` and cookies, do not compile because methods are not evaluated until runtime, so they cannot be used as the value of a case statement, even if one of the values is stored in a final variable
- The last case statement, with value ``3 * 5``, does compile, as expressions are allowed as case values, provided the value can be resolved at compile-time.
- ==**They also must be able to fit in the ``switch`` data type without an explicit cast.**==
- ==**The data type for case statements must match the data type of the switch variable.**==

### The ``switch`` Expression

A ``switch`` expression is a much more compact form of a ``switch`` statement, ==**capable of returning a value**==.
Because a switch expression is a compact form, there’s a lot going on. For starters, we can now assign the result of a switch expression to a variable result. ==**For this to work, all case and default branches must return a data type that is compatible with the assignment.**== The ``switch`` expression supports two types of branches: an expression and a block. Each has different syntactical rules on how it must be created.

![[Pasted image 20240126193026.png]]

Like a traditional ``switch`` statement, a ``switch`` expression supports zero or many case branches and an optional default branch. Both also support the new feature that allows case values to be combined with a single case statement using commas. Unlike a traditional ``switch`` statement, though, ``switch`` expressions have special rules around when the default branch is required.

---

**that ``->`` is the arrow operator. While the arrow operator is commonly used in lambda expressions, when it is used in a switch expression, the case branches are not lambdas.**

---

```java
public void printDayOfWeek(int day) {
var result = switch(day) {
case 0 -> "Sunday";
case 1 -> "Monday";
case 2 -> "Tuesday";
case 3 -> "Wednesday";
case 4 -> "Thursday";
case 5 -> "Friday";
case 6 -> "Saturday";
default -> "Invalid value";
};
System.out.print(result);
}
```

==**Notice that a semicolon is required after each switch expression.**== 

```java
var result = switch(bear) {
case 30 -> "Grizzly"
default -> "Panda"
}
```
**Does not compile**

Each case or default expression requires a semicolon as well as the assignment itself.

```java
var result = switch(bear) {
case 30 -> "Grizzly";
default -> "Panda";
};
```

case statements can take multiple values, separated by commas.

```java
public void printSeason(int month) {
switch(month) {
case 1, 2, 3 -> System.out.print("Winter");
case 4, 5, 6 -> System.out.print("Spring");
case 7, 8, 9 -> System.out.print("Summer");
case 10, 11, 12 -> System.out.print("Fall");
} }
```

---

**Most of the time, a ``switch`` expression returns a value, although ``printSeason()`` demonstrates one in which the return type is ``void``. Since the type is ``void``, it can’t be assigned to a variable. On the exam, you are more likely to see a ``switch`` expression that returns a value, but you should be aware that it is possible.**

---

All of the previous rules around ``switch`` data types and case values still apply, although we have some new rules.

1. ==**All of the branches of a ``switch`` expression that do not ``throw`` an exception must return a consistent data type (if the ``switch`` expression returns a value).**==
2. ==**If the ``switch`` expression returns a value, then every branch that isn’t an expression must ``yield`` a value.**==
3. ==**A default branch is required unless all cases are covered or no value is returned.**==

#### Returning Consistent Data Types

You can’t return incompatible or random data types.
```java
int measurement = 10;
int size = switch(measurement) {
case 5 -> 1;
case 10 -> (short)2;
default -> 5;
case 20 -> "3"; // DOES NOT COMPILE
case 40 -> 4L; // DOES NOT COMPILE
case 50 -> null; // DOES NOT COMPILE
};
```

Notice that the second case expression returns a ``short``, but that can be implicitly cast to an ``int``. In this manner, ==**the values have to be consistent with size, but they do not all have to be the same data type**.==

#### Applying a case Block

A ``switch`` expression supports both an expression and a block in the case and default branches. Like a regular block, a case block is one that is surrounded by braces ``({})``. It also includes a ``yield`` statement if the switch expression returns a value.

```java
int fish = 5;
int length = 12;
var name = switch(fish) {
case 1 -> "Goldfish";
case 2 -> {yield "Trout";}
case 3 -> {
if(length > 10) yield "Blobfish";
else yield "Green";
}
default -> "Swordfish";
};
```

The ``yield`` keyword is equivalent to a return statement within a ``switch`` expression and is used to avoid ambiguity about whether you meant to exit the block or method around the switch expression.

==**``switch`` expressions, ``yield`` statements are NOT OPTIONAL if the switch statement RETURNS a value.**==

```java
10: int fish = 5;
11: int length = 12;
12: var name = switch(fish) {
13: case 1 -> "Goldfish";
14: case 2 -> {} // DOES NOT COMPILE
15: case 3 -> {
16: if(length > 10) yield "Blobfish";
17: } // DOES NOT COMPILE
18: default -> "Swordfish";
19: };
```

- Line 14 does not compile because it does not return a value using ``yield``.
- Line 17 also does not compile. While the code returns a value for length greater than 10, it does not return a value if length is less than or equal to 10.

It does not matter that length is set to be 12; all branches must ``yield`` a value within the case block.

---
**Watch Semicolons in switch Expressions**
**Unlike a regular ``switch`` statement, a ``switch`` expression can be used with the assignment operator and requires a semicolon when doing so. Furthermore, semicolons are required for case expressions but cannot be used with case blocks.**

```java
var name = switch(fish) {
case 1 -> "Goldfish" // DOES NOT COMPILE (missing semicolon)
case 2 -> {yield "Trout";}; // DOES NOT COMPILE (extra semicolon)
...
} // DOES NOT COMPILE (missing semicolon)
```

---

#### Covering All Possible Values

The last rule about ``switch`` expressions is probably the one the exam is most likely to try to trick you on: a ``switch`` expression that returns a value must handle all possible input values. when it does not return a value, it is optional.

```java
String type = switch(canis) { // DOES NOT COMPILE
case 1 -> "dog";
case 2 -> "wolf";
case 3 -> "coyote";
};
```

There’s no case branch to cover 5 (or 4, -1, 0, etc.), so should the ``switch`` expression return ``null``, the empty string, undefined, or some other value? When adding ``switch`` expressions to the Java language, the authors decided this behavior would be unsupported. Every switch expression must handle all possible values of the ``switch`` variable.

==**there are two ways to address this:**==
- ==**Add a default branch.**==
- ==**If the ``switch`` expression takes an ``enum`` value, add a case branch for every possible ``enum`` value.**==

In practice, the first solution is the one most often used. For enums, the second solution works well when the number of enum values is relatively small.

```java
enum Season {WINTER, SPRING, SUMMER, FALL}
String getWeather(Season value) {
return switch(value) {
case WINTER -> "Cold";
case SPRING -> "Rainy";
case SUMMER -> "Hot";
case FALL -> "Warm";
};
}
```

Since all possible permutations of ``Season`` are covered, a default branch is not required in this ``switch`` expression.

---
**What happens if you use an ``enum`` with three values and later someone adds a fourth value? Any ``switch`` expressions that use the enum without a default branch will suddenly fail to compile. If this was done frequently, you might have a lot of code to fix! For this reason, consider including a default branch in every ``switch`` expression, even those that involve ``enum`` values.** #TIP 

---
## Writing `while` Loops

A loop is a repetitive control structure that can execute a statement of code multiple times in succession. By using variables that can be assigned new values, each repetition of the statement may be different.

```java
int counter = 0;
while (counter < 10) {
double price = counter * 10;
System.out.println(price);
counter++;
}
```

### The ``while`` Statement

The simplest repetitive control structure in Java is the ``while`` statement, Like all repetition control structures, it has a termination condition, implemented as a ``boolean`` expression, that will continue as long as the expression evaluates to ``true``.

a ``while`` loop is similar to an ``if`` statement in that it is composed of a boolean expression and a statement, or a block of statements. During execution, the boolean expression is evaluated before each iteration of the loop and exits if the evaluation returns false.

```java
int roomInBelly = 5;
public void eatCheese(int bitesOfCheese) {
while (bitesOfCheese > 0 && roomInBelly > 0) {
bitesOfCheese--;
roomInBelly--;
}
System.out.println(bitesOfCheese+" pieces of cheese left");
}
```

==**One thing to remember is that a while loop may terminate after its first evaluation of the ``boolean`` expression**==

```java
int full = 5;
while(full < 5) {
System.out.println("Not full!");
full++;
}
```

On the first iteration of the loop, the condition is reached, and the loop exits. imply put, the body of the loop may not execute at all or may execute many times.

### The ``do/while`` Statement

==**Unlike a ``while`` loop, though, a ``do/while`` loop guarantees that the statement or block will be executed at least once.**==

```java
int lizard = 0;
do {
lizard++;
} while(false);
System.out.println(lizard); // 1
```

Java will execute the statement block first and then check the loop condition. Even though the loop exits right away, the statement block is still executed once, and the program prints 1.

### Infinite Loops
 
 ==**The single most important thing you should be aware of when you are using any repetition control structures is to make sure they always terminate!**== Failure to terminate a loop can lead to numerous problems in practice, including overflow exceptions, memory leaks, slow performance, and even bad data.

```java
int pen = 2;
int pigs = 5;
while(pen < 10)
pigs++;
```

The result is that the loop will never end, creating what is commonly referred to as an infinite loop. An infinite loop is a loop whose termination condition is never reached during runtime.  

Anytime you write a loop, you should examine it to determine whether the termination condition is always eventually met under some condition. make sure the loop condition, or the variables the condition is dependent on, are changing between executions. Then, ensure that the termination condition will be eventually reached in all circumstances.

## Constructing ``for`` Loops

A basic ``for`` loop has the same conditional boolean expression and statement, or block of statements, as the ``while`` loops, as well as two new sections: an ***initialization block*** and an ***update statement.***

==**Each of the three sections is separated by a semicolon. In addition, the initialization and update sections may contain multiple statements, separated by commas.**==

Variables declared in the initialization block of a for loop have limited scope and are accessible only within the for loop. Be wary of any exam questions in which a variable is declared within the initialization block of a for loop and then read outside the loop.

```java
for(int i=0; i < 10; i++)
System.out.println("Value is: "+i);
System.out.println(i); // DOES NOT COMPILE
```

Alternatively, variables declared before the ``for`` loop and assigned a value in the initialization block may be used outside the ``for`` loop because their scope precedes the creation of the for loop.

```java
int i;
for(i=0; i < 10; i++)
System.out.println("Value is: "+i);
System.out.println(i);
```

```java
for(int i = 0; i < 5; i++) {
System.out.print(i + " ");
}
```
 
 The local variable ``i`` is initialized first to 0. The variable ``i`` is only in scope for the duration of the loop and is not available outside the loop once the loop has completed. Like a while loop, the boolean condition is evaluated on every iteration of the loop before the loop executes. Since it returns true, the loop executes and outputs 0 followed by a space. Next, the loop executes the update section, which in this case increases the value of ``i`` to 1. The loop then evaluates the boolean expression a second time, and the process repeats multiple times, printing the following:

```text
0 1 2 3 4
```

#### Printing Elements in Reverse

```java
for (var counter = 4; counter >= 0; counter--)
{
	System.out.print(counter + " ");
}
```

---

**For the exam, you are going to have to know how to read forward and backward ``for`` loops. When you see a ``for`` loop on the exam, pay close attention to the loop variable and operations if the decrement operator, ``--`` , is used. While incrementing from 0 in a ``for`` loop is often straightforward, decrementing tends to be less intuitive. In fact, if you do see a for loop with a decrement operator on the exam, you should assume they are trying to test your knowledge of loop operations.** 

---

#### Working with ``for`` Loops

**1. Creating an Infinite Loop**

```java
for( ; ; )
	System.out.println("Hello World");
```

it will in fact compile and run without issue. It is actually an infinite loop that will print the same statement repeatedly.

**2. Adding Multiple Terms to the for Statement**

```java
int x = 0;
for(long y = 0, z = 4; x < 5 && y < 10; x++, y++) {
System.out.print(y + " "); }
System.out.print(x + " ");
```

This code demonstrates three variations of the for loop

- ==**First, you can declare a variable, such as x in this example, before the loop begins and use it after it completes.**==
- ==**Second, your initialization block, boolean expression, and update statements can include extra variables that may or may not reference each other**==
- ==**Finally, the update statement can modify multiple variables.**==

**3. Redeclaring a Variable in the Initialization Block**

```java
int x = 0;
for(int x = 4; x < 5; x++) // DOES NOT COMPILE
System.out.print(x + " ");
```

It does not compile because of the initialization block. The difference is that x is repeated in the initialization block after already being declared before the loop, resulting in the compiler stopping because of a duplicate variable declaration. 

**4. Using Incompatible Data Types in the Initialization Block**

```java
int x = 0;
for(long y = 0, int z = 4; x < 5; x++) // DOES NOT COMPILE
	System.out.print(y + " ");
```

The variables in the initialization block must all be of the same type. In the multiple-terms example, y and z were both long, so the code compiled without issue; but in this example, they have different types, so the code will not compile.

**5. Using Loop Variables Outside the Loop**

```java
for(long y = 0, x = 4; x < 5 && y < 10; x++, y++)
System.out.print(y + " ");
System.out.print(x); // DOES NOT COMPILE
```

If you notice, x is defined in the initialization block of the loop and then used after the loop terminates. Since x was only scoped for the loop, using it outside the loop will cause a compiler error.

### The ``for-each`` Loop

The ``for-each`` loop is a specialized structure designed to iterate over arrays and various Collections Framework classes

==**The ``for-each`` loop declaration is composed of an initialization section and an object to be iterated over. The right side of the for-each loop must be one of the following:**==

- ==**A built-in Java array**==  
- ==**An object whose type implements`` java.lang.Iterable``**==

For the exam, you should know that this does not include all of the Collections Framework classes or interfaces, but only those that implement or extend that Collection interface. For example, Map is not supported in a for-each loop, although Map does include methods that return Collection instances.

The left side of the ``for-each`` loop must include a declaration for an instance of a variable whose type is compatible with the type of the array or collection on the right side of the statement. On each iteration of the loop, the named variable on the left side of the statement is assigned a new value from the array or collection on the right side of the statement.

```java
public void printNames(String[] names) {
	for(int counter=0; counter<names.length; counter++)
		System.out.println(names[counter]);
}

public void printNames(String[] names) {
	for(var name : names)
		System.out.println(name);
}
```

Like using a ``for`` loop in place of a ``while`` loop, ``for-each`` loops are meant to reduce boilerplate code, making code easier to read/write, and freeing you to focus on the parts of your code that really matter.

==**on each iteration, a ``for-each`` loop assigns a variable with the same type as the generic argument.**==

```java
String birds = "Jay";
for(String bird : birds) // DOES NOT COMPILE
	System.out.print(bird + " ");

String[] sloths = new String[3];
for(int sloth : sloths) // DOES NOT COMPILE
	System.out.print(sloth + " ");
```

- The first ``for-each`` loop does not compile because ``String`` cannot be used on the right side of the statement.
- The second example does not compile because the loop type on the left side of the statement is ``int`` and doesn’t match the expected type of ``String``.

## Controlling Flow with Branching

### Nested Loops

A nested loop is a loop that contains another loop, including ``while``, ``do/while``, ``for``, and ``for-each`` loops.

```java
int[][] myComplexArray = {{5,2,1,3},{3,9,8,9},{5,7,12,7}};
for(int[] mySimpleArray : myComplexArray) {
for(int i=0; i<mySimpleArray.length; i++) {
System.out.print(mySimpleArray[i]+"\t");
}
System.out.println();
}
```

```text
5 2 1 3
3 9 8 9
5 7 12 7
```

Nested loops can include ``while`` and ``do/while``

```java
int hungryHippopotamus = 8;
while(hungryHippopotamus>0) {
do {
hungryHippopotamus -=2;
} while (hungryHippopotamus>5);
hungryHippopotamus--;
System.out.print(hungryHippopotamus+", ");
}
```

The first time this loop executes, the inner loop repeats until the value of ``hungryHippopotamus`` is 4. The value will then be decremented to 3, and that will be the output at the end of the first iteration of the outer loop.

On the second iteration of the outer loop, the inner do/while will be executed once, even though ``hungryHippopotamus`` is already not greater than 5. As you may recall, do/while statements always execute the body at least once. This will reduce the value to 1, which will be further lowered by the decrement operator in the outer loop to 0. Once the value reaches 0, the outer loop will terminate.

```text
3, 0,
```

### Adding Optional Labels

A label is an optional pointer to the head of a statement that allows the application flow to jump to it or break from it. It is a single identifier that is followed by a colon ``(:)``.

```java
int[][] myComplexArray = {{5,2,1,3},{3,9,8,9},{5,7,12,7}};
OUTER_LOOP: for(int[] mySimpleArray : myComplexArray) {
INNER_LOOP: for(int i=0; i<mySimpleArray.length; i++) {
System.out.print(mySimpleArray[i]+"\t");
}
System.out.println();
}
```

Labels follow the same rules for formatting as identifiers. For readability, they are commonly expressed using uppercase letters in snake_case with underscores between words. When dealing with only one loop, labels do not add any value, they are extremely useful in nested structures.

### The ``break`` Statement

``break`` statement transfers the flow of control out to the enclosing statement. The same holds true for a ``break`` statement that appears inside of a ``while``, ``do/while``, or for loop, as it will end the loop early

the ``break`` statement can take an optional label parameter. Without a label parameter, the ``break`` statement will terminate the nearest inner loop it is currently in the process of executing. The optional label parameter allows us to break out of a higher-level outer loop.

```java
public class FindInMatrix {
    public static void main(String[] args) {
        int[][] list = {{1, 13}, {5, 2}, {2, 2}};
        int searchValue = 2;
        int positionX = -1;
        int positionY = -1;

        PARENT_LOOP:
        for (int i = 0; i < list.length; i++) {
            for (int j = 0; j < list[i].length; j++) {
                if (list[i][j] == searchValue) {
                    positionX = i;
                    positionY = j;
                    break PARENT_LOOP;
                }
            }
        }

        if (positionX == -1 || positionY == -1) {
            System.out.println("Value " + searchValue + " not found");
        } else {
            System.out.println("Value " + searchValue + " found at: " +
                    "(" + positionX + "," + positionY + ")");
        }
    }
}

```

```text
Value 2 found at: (1,1)
```

the statement ``break PARENT_LOOP``. This statement will break out of the entire loop structure as soon as the first matching value is found.

```java
if(list[i][j]==searchValue) {
	positionX = i;
	positionY = j;
	break;
}
```

Instead of exiting when the first matching value is found, the program would now only exit the inner loop when the condition was met. In other words, the structure would find the first matching value of the last inner loop to contain the value

```text
Value 2 found at: (2,0)
```

```java
if(list[i][j]==searchValue) {
	positionX = i;
	positionY = j;
}
```

the code would search for the last value in the entire structure that had the matching value.

```text
Value 2 found at: (2,1)
```

### The ``continue`` Statement

the ``continue`` statement, a statement that causes flow to finish the execution of the ==**current loop iteration**==

==**While the ``break`` statement transfers control to the enclosing statement, the ``continue`` statement transfers control to the boolean expression that determines if the loop should continue.**== In other words, it ends the current iteration of the loop. Also, like the ``break`` statement, the ``continue`` statement is applied to the nearest inner loop under execution, using optional label statements to override this behavior.

```java
1: public class CleaningSchedule {
2:     public static void main(String[] args) {
3:         CLEANING: for(char stables = 'a'; stables<='d'; stables++) {
4:             for(int leopard = 1; leopard<4; leopard++) {
5:                 if(stables=='b' || leopard==2) {
6:                     continue CLEANING;
7:                 }
8:                 System.out.println("Cleaning: "+stables+","+leopard);
9:             }
10:         }
11:     }
12: }

```

```text
Cleaning: a,1
Cleaning: c,1
Cleaning: d,1
```

remove the ``CLEANING`` label in the ``continue`` statement so that control is returned to the inner loop instead of the outer. Line 6 becomes the following:

```java
6: continue;
```

This corresponds to the zookeeper cleaning all leopards except those labeled 2 or in stable b. The output is then the following:

```text
Cleaning: a,1
Cleaning: a,3
Cleaning: c,1
Cleaning: c,3
Cleaning: d,1
Cleaning: d,3
```

### The ``return`` Statement

creating methods and using ``return`` statements can be used as an alternative to using labels and ``break`` statements.

```java
public class FindInMatrixUsingReturn {
    private static int[] searchForValue(int[][] list, int v) {
        for (int i = 0; i < list.length; i++) {
            for (int j = 0; j < list[i].length; j++) {
                if (list[i][j] == v) {
                    return new int[]{i, j};
                }
            }
        }
        return null;
    }

    public static void main(String[] args) {
        int[][] list = {{1, 13}, {5, 2}, {2, 2}};
        int searchValue = 2;
        int[] results = searchForValue(list, searchValue);

        if (results == null) {
            System.out.println("Value " + searchValue + " not found");
        } else {
            System.out.println("Value " + searchValue + " found at: " +
                    "(" + results[0] + "," + results[1] + ")");
        }
    }
}
```

the code without labels and break statements a lot easier to read and debug. Also, making the search logic an independent function makes the code more reusable and the calling main() method a lot easier to read.

Just remember that return statements can be used to exit loops quickly and can lead to more readable code in practice, especially when used with nested loops.

### Unreachable Code

==**One facet of ``break``, ``continue``, and ``return`` that you should be aware of is that any code placed immediately after them in the same block is considered unreachable and will not compile.**==

```java
int checkDate = 0;
while(checkDate<10) {
checkDate++;
if(checkDate>100) {
break;
checkDate++; // DOES NOT COMPILE
}
}
```

the compiler notices that you have statements immediately following the ``break`` and will fail to compile with “unreachable code” as the reason. The same is true for ``continue`` and ``return`` statements

```java
int minute = 1;
WATCH: while (minute > 2) {
    if (minute++ > 2) {
        continue WATCH;
         System.out.print(minute); // DOES NOT COMPILE
    }
}

int hour = 2;
switch (hour) {
    case 1:
        return; 
         hour++; // DOES NOT COMPILE
    case 2:
}
```

One thing to remember is that it does not matter if the loop or decision structure actually visits the line of code. For example, the loop could execute zero or infinite times at runtime. Regardless of execution, the compiler will report an error if it finds any code it deems unreachable, in this case any statements immediately following a break, continue, or return statement.

### Reviewing Branching

| Control Statement | Support Labels | Support Break | Support Continue | Support Yield |
|-------------------|----------------|---------------|-------------------|---------------|
| while             | Yes            | Yes           | Yes               | No            |
| do/while          | Yes            | Yes           | Yes               | No            |
| for               | Yes            | Yes           | Yes               | No            |
| switch            | Yes            | Yes           | No                | Yes           |

---

**Some of the most time-consuming questions you may see on the exam could involve nested loops with lots of branching. Unless you spot an obvious compiler error, we recommend skipping these questions and coming back to them at the end. Remember, all questions on the exam are weighted evenly!** #TIP 

---

## Summary #OCP_Summary 

**==This chapter presented how to make intelligent decisions in Java.**==

==**We covered basic decision-making constructs such as if, else, and switch statements and showed how to use them to change the path of the process at runtime. We also presented newer features in the Java language, including pattern matching and switch expressions, both designed to reduce boilerplate code.**==

==**We then moved our discussion to repetition control structures, starting with while and do/while loops.**==

==**Next, we covered the extremely convenient repetition control structures: the for and for-each loops. While their syntax is more complex than the traditional while or do/while loops, they are extremely useful in everyday coding and allow you to create complex expressions in a single line of code.**==

==**We concluded this chapter by discussing advanced control options and how flow can be enhanced through nested loops coupled with break, continue, and return statements.==**

## Exam Essentials #Essential 

- **Understand if and else decision control statements**. The if and else statements come up frequently throughout the exam in questions unrelated to decision control, so make sure you fully understand these basic building blocks of Java.

- **Apply pattern matching and flow scoping**. Pattern matching can be used to reduce boilerplate code involving an if statement, instanceof operator, and cast operation using a pattern variable. It can also include a pattern or filter after the pattern variable declaration. Pattern matching uses flow scoping in which the pattern variable is in scope as long as the compiler can definitively determine its type.

- **Understand switch statements and their proper usage**. You should be able to spot a poorly formed ``switch`` statement on the exam. The switch value and data type should be compatible with the case statements, and the values for the case statements must evaluate to compile-time constants. Finally, at runtime, a ``switch`` statement branches to the first matching ``case``, or ``default`` if there is no match, or exits entirely if there is no match and no default branch. The process then ``continues`` into any proceeding case or default statements until a break or return statement is reached.

- **Use switch expressions correctly**. Discern the differences between ``switch`` expressions and ``switch`` statements. Understand how to write switch expressions correctly, including proper use of semicolons, writing ``case`` expressions and blocks that ``yield`` a consistent value, and making sure all possible values of the switch variable are handled by the switch expression.

- **Write while loops**. Know the syntactical structure of all ``while`` and ``do/while`` loops. In particular, know when to use one versus the other.

- **Be able to use for loops**. You should be familiar with ``for`` and ``for-each`` loops and know how to write and evaluate them. Each loop has its own special properties and structures. You should know how to use for-each loops to iterate over lists and arrays.

- **Understand how break, continue, and return can change flow control**. Know how to change the flow control within a statement by applying a break, continue, or return statement. Also know which control statements can accept break statements and which can accept continue statements. Finally, you should understand how these statements work inside embedded loops or switch statements.


## Review Questions

1. Which of the following data types can be used in a switch expression? (Choose all that apply.)
A. enum
B. int
C. Byte
D. long
E. String
F. char
G. var
H. double

**My Answer: A,B,C,E,F,G**
**Correct Answer: A,B,C,E,F,G**


---

2. What is the output of the following code snippet? (Choose all that apply.)

```java
3: int temperature = 4;
4: long humidity = -temperature + temperature * 3;
5: if (temperature>=4)
6: if (humidity < 6) System.out.println("Too Low");
7: else System.out.println("Just Right");
8: else System.out.println("Too High");
```

A. Too Low
B. Just Right
C. Too High
D. A NullPointerException is thrown at runtime.
E. The code will not compile because of line 7.
F. The code will not compile because of line 8.

**My Answer: E,F**
**Correct Answer: B**

**The code compiles and runs without issue, Even though two consecutive else statements on lines 7 and 8 look a little odd, they are associated with separate if statements on lines 5 and 6, respectively**

---

3. Which of the following data types are permitted on the right side of a for-each expression? (Choose all that apply.)
A. Double``[][]``
B. Object
C. Map
D. List
E. String
F. char[]
G. Exception
H. Set

**My Answer: A,D,F,H**
**Correct Answer: A,D,F,H**

---

4. What is the output of calling ``printReptile(6)``?

```JAVA
void printReptile(int category) {
var type = switch(category) {
case 1,2 -> "Snake";
case 3,4 -> "Lizard";
case 5,6 -> "Turtle";
case 7,8 -> "Alligator";
};
System.out.print(type);
}
```

A. Snake
B. Lizard
C. Turtle
D. Alligator
E. TurtleAlligator
F. None of the above

**My Answer: C**
**Correct Answer: F**

**The code does not compile because the switch expression requires all possible case values to be handled, making option F correct. If a valid default statement was added, then the code would compile**

---

5. What is the output of the following code snippet?

```java
List<Integer> myFavoriteNumbers = new ArrayList<>();
myFavoriteNumbers.add(10);
myFavoriteNumbers.add(14);
for (var a : myFavoriteNumbers) {
System.out.print(a + ", ");
break;
}
for (int b : myFavoriteNumbers) {
continue;
System.out.print(b + ", ");
}
for (Object c : myFavoriteNumbers)
System.out.print(c + ", ");
```

A. It compiles and runs without issue but does not produce any output.
B. 10, 14,
C. 10, 10, 14,
D. 10, 10, 14, 10, 14,
E. Exactly one line of code does not compile.
F. Exactly two lines of code do not compile.
G. Three or more lines of code do not compile.
H. The code contains an infinite loop and does not terminate.

**My Answer: C**
**Correct Answer: E**

**The second for-each loop contains a continue followed by a print() statement. Because the continue is not conditional and always included as part of the body of the for-each loop, the print() statement is not reachable**

---

6. Which statements about decision structures are true? (Choose all that apply.)

A. A for-each loop can be executed on any Collections Framework object.
B. The body of a while loop is guaranteed to be executed at least once.
C. The conditional expression of a for loop is evaluated before the first execution of the loop body.
D. A switch expression that takes a String and assigns the result to a variable requires a default branch.
E. The body of a do/while loop is guaranteed to be executed at least once.
F. An if statement can have multiple corresponding else statements.

**My Answer: C,D,E**
**Correct Answer: C,D,E**

---

7. Assuming weather is a well-formed nonempty array, which code snippet, when inserted independently into the blank in the following code, prints all of the elements of ``weather``?

```java
private void print(int[] weather) {
for(???) {
System.out.println(weather[i]);
}
}
```

```
`A. int i=weather.length; i>0; i--
B. int i=0; i<=weather.length-1; ++i
C. var w : weather
D. int i=weather.length-1; i>=0; i--
E. int i=0, int j=3; i<weather.length; ++i
F. int i=0; ++i<10 && i<weather.length;
G. None of the above`
```

**My Answer: C,D,**
**Correct Answer: B,D**

---

8. What is the output of calling ``printType(11)``?

```java
31: void printType(Object o) {
32: if(o instanceof Integer bat) {
33: System.out.print("int");
34: } else if(o instanceof Integer bat && bat < 10) {
35: System.out.print("small int");
36: } else if(o instanceof Long bat || bat <= 20) {
37: System.out.print("long");
38: } default {
39: System.out.print("unknown");
40: }
41: }
```

A. int
B. small int
C. long
D. unknown
E. Nothing is printed.
F. The code contains one line that does not compile.
G. The code contains two lines that do not compile.
H. None of the above

**My Answer: G,**
**Correct Answer: G**

---

9. Which statements, when inserted independently into the following blank, will cause the code to print 2 at runtime? (Choose all that apply.)

```java
int count = 0;
BUNNY: for(int row = 1; row <=3; row++)
RABBIT: for(int col = 0; col <3 ; col++) {
if((col + row) % 2 == 0);
???
count++;
}
System.out.println(count);
```

A. break BUNNY
B. break RABBIT
C. continue BUNNY
D. continue RABBIT
E. break
F. continue
G. None of the above, as the code contains a compiler error.

**My Answer: B,E**
**Correct Answer: B,C,E**

**The code contains a nested loop and a conditional expression that is executed if the sum of col + row is an even number; otherwise, count is incremented**

---

10. Given the following method, how many lines contain compilation errors? (Choose all that apply.)

```JAVA
10: private DayOfWeek getWeekDay(int day, final int thursday) {
11: int otherDay = day;
12: int Sunday = 0;
13: switch(otherDay) {
14: default:
15: case 1: continue;
16: case thursday: return DayOfWeek.THURSDAY;
17: case 2,10: break;
18: case Sunday: return DayOfWeek.SUNDAY;
19: case DayOfWeek.MONDAY: return DayOfWeek.MONDAY;
20: }
21: return DayOfWeek.FRIDAY;
22: }
```

A. None, the code compiles without issue.
B. 1
C. 2
D. 3
E. 4
F. 5
G. 6
H. The code compiles but may produce an error at runtime.

**My Answer: H**
**Correct Answer: E**

**Line 15 does not compile, as continue cannot be used inside a switch statement like this.**
**Line 16 is not a compile-time constant since any int value can be passed as a parameter. Marking it final does not change this, so it doesn’t compile.**
**Line 18 does not compile because Sunday is not marked as final. Being effectively final is insufficient.**
**line 19 does not compile because DayOfWeek.MONDAY is not an int value. While switch statements do support enum values, each case statement must have the same data type as the switch variable otherDay, which is int**


---

11. What is the output of calling ``printLocation(Animal.MAMMAL)``?

```java
10: class Zoo {
11: enum Animal {BIRD, FISH, MAMMAL}
12: void printLocation(Animal a) {
13: long type = switch(a) {
14: case BIRD -> 1;
15: case FISH -> 2;
16: case MAMMAL -> 3;
17: default -> 4;
18: };
19: System.out.print(type);
20: } }
```

A. 3
B. 4
C. 34
D. The code does not compile because of line 13.
E. The code does not compile because of line 17.
F. None of the above

**My Answer: A**
**Correct Answer: A**

---

12. What is the result of the following code snippet?

```java
3: int sing = 8, squawk = 2, notes = 0;
4: while(sing > squawk) {
5: sing--;
6: squawk += 2;
7: notes += sing + squawk;
8: }
9: System.out.println(notes);
```

A. 11
B. 13
C. 23
D. 33
E. 50
F. The code will not compile because of line 7.

**My Answer: C**
**Correct Answer: C**

---

13. What is the output of the following code snippet?

```java
2: boolean keepGoing = true;
3: int result = 15, meters = 10;
4: do {
5: meters--
;
6: if(meters==8) keepGoing = false;
7: result -=
2;
8: } while keepGoing;
9: System.out.println(result);
```

A. 7
B. 9
C. 10
D. 11
E. 15
F. The code will not compile because of line 6.
G. The code does not compile for a different reason.

**My Answer: G**
**Correct Answer: G**

---

14. Which statements about the following code snippet are correct? (Choose all that apply.)

```java
for(var penguin : new int[2])
System.out.println(penguin);
var ostrich = new Character[3];
for(var emu : ostrich)
System.out.println(emu);
List<Integer> parrots = new ArrayList<Integer>();
for(var macaw : parrots)
System.out.println(macaw);
```

A. The data type of penguin is Integer.
B. The data type of penguin is int.
C. The data type of emu is undefined.
D. The data type of emu is Character.
E. The data type of macaw is List.
F. The data type of macaw is Integer.
G. None of the above, as the code does not compile.

**My Answer: B,D,F**
**Correct Answer: B,D,F**

---

15. What is the result of the following code snippet?

```java
final char a = 'A', e = 'E';
char grade = 'B';
switch (grade) {
default:
case a:
case 'B': 'C': System.out.print("great ");
case 'D': System.out.print("good "); break;
case e:
case 'F': System.out.print("not good ");
```

A. great
B. great good
C. good
D. not good
E. The code does not compile because the data type of one or more case statements does not match the data type of the switch variable.
F. None of the above

**My Answer: F**
**Correct Answer: F**

---

16. Given the following array, which code snippets print the elements in reverse order from how they are declared? (Choose all that apply.)

```java
char[] wolf = {'W', 'e', 'b', 'b', 'y'};
A.
int q = wolf.length;
for( ; ; ) {
System.out.print(wolf[--q]);
if(q==0) break;
}

B.
for(int m=wolf.length-1;
m>=0; --m)
System.out.print(wolf[m]);

C.
for(int z=0; z<wolf.length; z++)
System.out.print(wolf[wolf.length-z]);
D.

int x = wolf.length-1;
for(int j=0; x>=0 && j==0; x--)
System.out.print(wolf[x]);

E.
final int r = wolf.length;
for(int w = r-1;r>-1; w = r-1)
System.out.print(wolf[w]);

F.
for(int i=wolf.length; i>0; --i)
System.out.print(wolf[i]);

G. None of the above
```

**My Answer: A,D**
**Correct Answer: A,B,D**


---

17. What distinct numbers are printed when the following method is executed? (Choose all that apply.)

```java
private void countAttendees() {
int participants = 4, animals = 2, performers = -1;
while((participants = participants+1) < 10) {}
do {} while (animals++ <= 1);
for( ; performers<2; performers+=2) {}
System.out.println(participants);
System.out.println(animals);
System.out.println(performers);
}
```

A. 6
B. 3
C. 4
D. 5
E. 10
F. 9
G. The code does not compile.
H. None of the above

**My Answer: B,E**
**Correct Answer: B,E**

---

18. Which statements about pattern matching and flow scoping are correct? (Choose all that apply.)

A. Pattern matching with an if statement is implemented using the instance operator.
B. Pattern matching with an if statement is implemented using the instanceon operator.
C. Pattern matching with an if statement is implemented using the instanceof operator.
D. The pattern variable cannot be accessed after the if statement in which it is declared.
E. Flow scoping means a pattern variable is only accessible if the compiler can discern its type.
F. Pattern matching can be used to declare a variable with an else statement.

**My Answer: C,E**
**Correct Answer: C,E**

---

19. What is the output of the following code snippet?

```java
2: double iguana = 0;
3: do {
4: int snake = 1;
5: System.out.print(snake++ + " ");
6: iguana--
;
7: } while (snake <= 5);
8: System.out.println(iguana);
```

A. 1 2 3 4 -4.0
B. 1 2 3 4 -5.0
C. 1 2 3 4 5 -4.0
D. 0 1 2 3 4 5 -5.0
E. The code does not compile.
F. The code compiles but produces an infinite loop at runtime.
G. None of the above

**My Answer: E**
**Correct Answer: F**

**The variable snake is declared within the body of the do/while statement, so it is out of scope on line 7.**

---

20. Which statements, when inserted into the following blanks, allow the code to compile and run without entering an infinite loop? (Choose all that apply.)

```java
4: int height = 1;
5: L1: while(height++ <10) {
6: long humidity = 12;
7: L2: do {
8: if(humidity--% 12 == 0) ; ???
9: int temperature = 30;
10: L3: for( ; ; ) {
11: temperature++;
12: if(temperature>50) ; ???
13: }
14: } while (humidity > 4);
15: }
```

A. break L2 on line 8; continue L2 on line 12
B. continue on line 8; continue on line 12
C. break L3 on line 8; break L1 on line 12
D. continue L2 on line 8; continue L3 on line 12
E. continue L2 on line 8; continue L2 on line 12
F. None of the above, as the code contains a compiler error

**My Answer: B,E**
**Correct Answer: A,E**

**The most important thing to notice when reading this code is that the innermost loop is an infinite loop. Therefore, you are looking for solutions that skip the innermost loop entirely or that exit that loop.**

---

21. A minimum of how many lines need to be corrected before the following method will compile?
```java
21: void findZookeeper(Long id) {
22: System.out.print(switch(id) {
23: case 10 -> {"Jane"}
24: case 20 -> {yield "Lisa";};
25: case 30 -> "Kelly";
26: case 30 -> "Sarah";
27: default -> "Unassigned";
28: });
29: }
```

A. Zero
B. One
C. Two
D. Three
E. Four
F. Five

**My Answer: D**
**Correct Answer: E**

**Line 22 does not compile because Long is not a compatible type for a switch statement or expression. Line 23 does not compile because it is missing a semicolon after "Jane" and a yield statement. Line 24 does not compile because it contains an extra semicolon at the end. Finally, lines 25 and 26 do not compile because they use the same case value**

---

22. What is the output of the following code snippet? (Choose all that apply.)

```java
2: var tailFeathers = 3;
3: final var one = 1;
4: switch (tailFeathers) {
5: case one: System.out.print(3 + " ");
6: default: case 3: System.out.print(5 + " ");
7: }
8: while (tailFeathers > 1) {
9: System.out.print(--tailFeathers + " "); }
```

A. 3
B. 5 1
C. 5 2
D. 3 5 1
E. 5 2 1
F. The code will not compile because of lines 3–5.
G. The code will not compile because of line 6.

**My Answer: G**
**Correct Answer: E**

**The code compiles without issue var is supported in both switch and while loops, provided the compiler determines that the type is compatible with these statements. In addition, the variable one is allowed in a case statement because it is a final local variable, making it a compile-time constant.**

---

23. What is the output of the following code snippet?

```JAVA
15: int penguin = 50, turtle = 75;
16: boolean older = penguin >= turtle;
17: if (older = true) System.out.println("Success");
18: else System.out.println("Failure");
19: else if(penguin != 50) System.out.println("Other");
```

A. Success
B. Failure
C. Other
D. The code will not compile because of line 17.
E. The code compiles but throws an exception at runtime.
F. None of the above

**My Answer: D**
**Correct Answer: F**

**Line 19 starts with an else statement, but there is no preceding if statement that it matches. For this reason, line 19 does not compile, making option F the correct answer** 

---

24. Which of the following are possible data types for friends that would allow the code to compile? (Choose all that apply.)

```java
for(var friend in friends) {
	System.out.println(friend);
}
```

A. Set
B. Map
C. String
D. int[]
E. Collection
F. StringBuilder
G. None of the above

**My Answer: A,D,E**
**Correct Answer: G**

**The statement is not a valid for-each loop (or a traditional for loop) since it uses a nonexistent in keyword**

---

25. What is the output of the following code snippet?
```java
6: String instrument = "violin";
7: final String CELLO = "cello";
8: String viola = "viola";
9: int p = -1;
10: switch(instrument) {
11: case "bass" : break;
12: case CELLO : p++;
13: default: p++;
14: case "VIOLIN": p++;
15: case "viola" : ++p; break;
16: }
17: System.out.print(p);
```

A. -1
B. 0
C. 1
D. 2
E. 3
F. The code does not compile.

**My Answer: F**
**Correct Answer: D**

**The code compiles without issue, so option F is incorrect. The viola variable created on line 8 is never used and can be ignored. If it had been used as the case value on line 15, it would have caused a compilation error since it is not marked final. Since "violin" and "VIOLIN" are not an exact match, the default branch of the switch statement is executed at runtime. This execution path increments p a total of three times, bringing the final value of p to 2 and making option D the correct answer.**

---

26. What is the output of the following code snippet? (Choose all that apply.)

```java
9: int w = 0, r = 1;
10: String name = "";
11: while(w < 2) {
12: name += "A";
13: do {
14: name += "B";
15: if(name.length()>0) name += "C";
16: else break;
17: } while (r <=1);
18: r++; w++; }
19: System.out.println(name);
```

A. ABC
B. ABCABC
C. ABCABCABC
D. Line 15 contains a compilation error.
E. Line 18 contains a compilation error.
F. The code compiles but never terminates at runtime.
G. The code compiles but throws a NullPointerException at runtime.

**My Answer: B**
**Correct Answer: F**

**The code snippet does not contain any compilation errors, There is a problem with this code snippet, though. While it may seem complicated, the key is to notice that the variable r is updated outside of the do/while loop. This is allowed from a compilation standpoint, since it is defined before the loop, but it means the innermost loop never breaks the termination condition r <= 1. At runtime, this will produce an infinite loop the first time the innermost loop is entered**

---

27. What is printed by the following code snippet?

```java
23: byte amphibian = 1;
24: String name = "Frog";
25: String color = switch(amphibian) {
26: case 1 -> { yield "Red"; }
27: case 2 -> { if(name.equals("Frog")) yield "Green"; }
28: case 3 -> { yield "Purple"; }
29: default -> throw new RuntimeException();
30: };
31: System.out.print(color);
```

A. Red
B. Green
C. Purple
D. RedPurple
E. An exception is thrown at runtime.
F. The code does not compile.

**My Answer: F**
**Correct Answer: F**

---

28. What is the output of calling ``getFish("goldie")``?

```JAVA
40: void getFish(Object fish) {
41: if (!(fish instanceof String guppy))
42: System.out.print("Eat!");
43: else if (!(fish instanceof String guppy)) {
44: throw new RuntimeException();
45: }
46: System.out.print("Swim!");
47: }
```

A. Eat!
B. Swim!
C. Eat! followed by an exception.
D. Eat!Swim!
E. An exception is printed.
F. None of the above

**My Answer: F**
**Correct Answer: F**

**Based on flow scoping, guppy is in scope after lines 41–42 if the type is not a String. In this case, line 43 declares a variable guppy that is a duplicate of the previously defined local variable defined on line 41. For this reason, the code does not compile, and option F is correct.**

---

29. What is the result of the following code?

```java
1: public class PrintIntegers {
2: public static void main(String[] args) {
3: int y = -2;
4: do System.out.print(++y + " ");
5: while(y <= 5);
6: } }
```

A. -2 -1 0 1 2 3 4 5
B. -2 -1 0 1 2 3 4
C. -1 0 1 2 3 4 5 6
D. -1 0 1 2 3 4 5
E. The code will not compile because of line 5.
F. The code contains an infinite loop and does not terminate.

**My Answer: A**
**Correct Answer: C**

---

# Chapter 4 - Core APIs #Chapter

## Creating and Manipulating Strings

A string is basically a sequence of characters;

```JAVA
String name = "Fluffy";
```

this is an example of a reference type. reference types are created using the ***new*** keyword. In Java, these two
snippets both create a ``String``:

```JAVA
String name = "Fluffy";
String name = new String("Fluffy");
```

Both give you a reference variable named name pointing to the String object *Fluffy*. String class is special and doesn’t need to be instantiated with ``new``.  Further, text blocks are another way of creating a String. To review, this text block is the same as the previous variables:

```java
String name = """
Fluffy""";
```

Since a ``String`` is a sequence of characters, it implements the interface ``CharSequence``. This interface is a general way of representing several classes, including ``String`` and ``StringBuilder`` . 
### Concatenating

Java combines the two String objects. Placing one String before the other String and combining them is called string *concatenation.* The exam creators like string concatenation because the ``+`` operator can be used in two ways within the same line of code.

1. ==**If both operands are numeric, ``+`` means numeric addition.**==
2. ==**If either operand is a String, ``+`` means concatenation.**==
3. ==**The expression is evaluated left to right.**==

```java
System.out.println(1 + 2); // 3
System.out.println("a" + "b"); // ab
System.out.println("a" + "b" + 3); // ab3
System.out.println(1 + 2 + "c"); // 3c
System.out.println("c" + 1 + 2); // c12
System.out.println("c" + null); // cnull
```

- The first example uses the first rule. Both operands are numbers, so we use normal addition.
- The second example is simple string concatenation, described in the second rule.
- The third example combines the second and third rules. Since we start on the left, Java
	figures out what "a" + "b" evaluates to. Then Java looks at the remaining expression of "ab" + 3. The second rule tells us to concatenate since one of the operands is a ``String``.
- In the fourth example, start with the third rule, which tells us to consider 1 + 2. Both operands are numeric, so the first rule tells us the answer is 3. Then we have 3 + "c", which uses the second rule to give us "3c". 
- The fifth example shows the importance of the third rule. First we have "c" + 1, which uses the second rule to give us "c1". Then we have "c1" + 2, which uses the second rule again to give us "c12".
- Finally, the last example shows how **==``null`` is represented as a string when concatenated or printed==**, giving us ``"cnull"``.

```java
int three = 3;
String four = "4";
System.out.println(1 + 2 + three + four); // 64 type String
```

just take it slow, remember the three rules, and be sure to check the variable types. 
There is one more thing to know about concatenation, s += "2" means the same thing as s = s + "2".

```java
	4: var s = "1"; // s currently holds "1"
	5: s += "2"; // s currently holds "12"
	6: s += 3; // s currently holds "123"
	7: System.out.println(s); // 123
```

==**use numeric addition if two numbers are involved, use concatenation otherwise, and evaluate from left to right.**==
### Important String Methods

For all these methods, you need to remember that a string is a sequence of characters and ==**Java counts from 0 when indexed.**== also need to know that a ==**String is immutable, or unchangeable. This means calling a method on a String will return a different String object rather than changing the value of the reference.**==
#### Determining the Length

The method ``length()`` returns the number of characters in the String.
```java
public int length()
```

```java
var name = "animals";
System.out.println(name.length()); // 7
```

Java counts from 0? The difference is that **==zero counting happens only when you’re using indexes or positions**== 
==**within a list==**. When determining the total size or length, Java uses normal counting again.
#### Getting a Single Character

The method ``charAt()`` lets you query the string to find out what character is at a specific index.
```java
public char charAt(int index)
```

```java
var name = "animals";
System.out.println(name.charAt(0)); // a
System.out.println(name.charAt(6)); // s
System.out.println(name.charAt(7)); // exception
```
#### Finding an Index

The method ``indexOf()`` looks at the characters in the string and finds the first index that matches the desired value. The ``indexOf`` method can work with an individual character or a whole String as input. It can also start from a requested position. char can be passed to an int parameter type.

```java
public int indexOf(int ch)
public int indexOf(int ch, int fromIndex)
public int indexOf(String str)
public int indexOf(String str, int fromIndex)
```

```java
var name = "animals";
System.out.println(name.indexOf('a')); // 0
System.out.println(name.indexOf("al")); // 4
System.out.println(name.indexOf('a', 4)); // 4
System.out.println(name.indexOf("al", 5)); // -1
```

==**Unlike ``charAt()``, the ``indexOf()`` method doesn’t throw an exception if it can’t find a match, instead returning –1.**== Because indexes start with 0, the caller knows that –1 couldn’t be a valid index.
#### Getting a Substring

The method ``substring()`` also looks for characters in a string. It returns parts of the string. The first parameter is the index to start with for the returned string. As usual, this is a zero-based index. There is an optional second parameter, which is the end index you want to stop at.

==**Notice  “stop at” rather than “include.”**== This means the ``endIndex`` parameter is allowed to be one past the end of the sequence if you want to stop at the end of the sequence. That would be redundant, though, since you could omit the second parameter entirely in that case

```java
public String substring(int beginIndex)
public String substring(int beginIndex, int endIndex)
```

![[Pasted image 20240204161904.png]]

```java
var name = "animals";
System.out.println(name.substring(3)); // mals
System.out.println(name.substring(name.indexOf('m'))); // mals
System.out.println(name.substring(3, 4)); // m
System.out.println(name.substring(3, 7)); // mals
```

The ``substring()`` method is the trickiest String method on the exam. The second example calls ``indexOf()`` to get the index rather than hard-coding it. This is a common practice when coding because you may not know the index in advance.

```java
System.out.println(name.substring(3, 3)); // empty string
System.out.println(name.substring(3, 2)); // exception
System.out.println(name.substring(3, 8)); // exception
```

The first example in this set prints an empty string. The request is for the characters starting with index 3 until we get to index 3. ==**Since we start and end with the same index, there are no characters in between.**==

==**The method returns the string starting from the requested index. If an end index is requested, it stops right before that index. Otherwise, it goes to the end of the string.**==
#### Adjusting Case

```java
public String toLowerCase()
public String toUpperCase()
```

```java
var name = "animals";
System.out.println(name.toUpperCase()); // ANIMALS
System.out.println("Abc123".toLowerCase()); // abc123
```

==**These methods leave alone any characters other than letters. Also, remember that strings are immutable, so the original string stays the same.**==
#### Checking for Equality

- ==**The ``equals()`` method checks whether two String objects contain exactly the same characters in the same order.**== 
- ==**The ``equalsIgnoreCase()`` method checks whether two String objects contain the same characters, with the exception that it ignores the characters’ case.**==

```java
public boolean equals(Object obj)
public boolean equalsIgnoreCase(String str)
```

``equals()`` takes an Object rather than a String. This is because the method is the same for all objects. If you pass in something that isn’t a String, it will just return false. By contrast, the ``equalsIgnoreCase()`` method only applies to String objects, so it can take the more specific type as the parameter.

```java
System.out.println("abc".equals("ABC")); // false
System.out.println("ABC".equals("ABC")); // true
System.out.println("abc".equalsIgnoreCase("ABC")); // true
```

---
**Overriding`` toString()``, ``equals(Object)``, and ``hashCode()``**

- **``toString()``: The ``toString()`` method is called when you try to print an object or concatenate the object with a String. It is commonly overridden with a version that prints a unique description of the instance using its instance fields.**
- **``equals(Object)``: The ``equals(Object)`` method is used to compare objects, with the default implementation just using the == operator. You should override the ``equals(Object)`` method any time you want to conveniently compare elements for equality, especially if this requires checking numerous fields.**
- **``hashCode()``: Any time you override ``equals(Object)``, you must override ``hashCode()`` to be consistent. This means that for any two objects, ``if a.equals(b)`` is true, then ``a.hashCode() == b.hashCode()`` must also be true. If they are not consistent, this could lead to invalid data and side effects in hash-based collections such as ``HashMap`` and ``HashSet``.**

---
#### Searching for Substrings

The ``startsWith()`` and ``endsWith()`` methods look at whether the provided value matches part of the String. The ``contains()`` method isn’t as particular; it looks for matches anywhere in the String.

```java
public boolean startsWith(String prefix)
public boolean endsWith(String suffix)
public boolean contains(CharSequence charSeq)
```

```java
System.out.println("abc".startsWith("a")); // true
System.out.println("abc".startsWith("A")); // false

System.out.println("abc".endsWith("c")); // true
System.out.println("abc".endsWith("a")); // false

System.out.println("abc".contains("b")); // true
System.out.println("abc".contains("B")); // false
```
#### Replacing Values

The ``replace()`` method does a simple search and replace on the string. There’s a version that takes char parameters as well as a version that takes ``CharSequence`` parameters.

```java
public String replace(char oldChar, char newChar)
public String replace(CharSequence target, CharSequence replacement)
```

```java
System.out.println("abcabc".replace('a', 'A')); // AbcAbc
System.out.println("abcabc".replace("a", "A")); // AbcAbc
```
#### Removing Whitespace
 
 These methods remove blank space from the beginning and/or end of a String. ==**The`` strip()`` and ``trim()`` methods remove whitespace from the beginning and end of a String**==. In terms of the exam, whitespace consists of spaces along with the ``\t (tab)`` and ``\n (newline)`` characters. Other characters, such as ``\r (carriage return)``, are also included in what gets trimmed. **==The ``strip()`` method does everything that ``trim()`` does, but it supports Unicode.==**

Additionally, the ``stripLeading()`` method removes whitespace from the beginning of the String and leaves it at the end. The ``stripTrailing()`` method does the opposite. It removes whitespace from the end of the String and leaves it at the beginning.

```java
public String strip()
public String stripLeading()
public String stripTrailing()
public String trim()
```

```java
System.out.println("abc".strip()); // abc
System.out.println("\t a b c\n".strip()); // a b c

String text = " abc\t ";
System.out.println(text.length()); // 6
System.out.println(text.trim().length()); // 3
System.out.println(text.strip().length()); // 3
System.out.println(text.stripLeading().length()); // 5
System.out.println(text.stripTrailing().length());// 4
```

First, remember that ``\t`` is a single character. The backslash escapes the t to represent a tab.
The second example gets rid of the leading tab, subsequent spaces, and the trailing newline. It leaves the spaces that are in the middle of the string. The remaining examples just print the number of characters remaining

```java
public class RemovingWhitespace {  
  
    public static void main(String[] args) {  
  
        stripWhiteSpace();  
  
        trimWhiteSpace();  
  
        stripTabCharacter();  
  
        trimTabCharacter();  
  
        stripSpecialCharacters();  
  
        trimSpecialCharacters();  
  
        trimUnicodeContent();  
  
        stripUnicodeContent();  
    }  
    private static void stripWhiteSpace() {  
        System.out.println("##### stripWhiteSpace #####");  
        System.out.println("abc".strip());  //abc  
        System.out.println(" abc ".strip()); //abc  
        System.out.println(" abc ".strip().length()); //3  
    }  
  
    private static void trimWhiteSpace() {  
        System.out.println("##### trimWhiteSpace #####");  
        System.out.println("abc".trim());  //abc  
        System.out.println(" abc ".trim()); //abc  
        System.out.println(" abc ".trim().length()); //3  
    }  
  
    private static void stripTabCharacter() {  
        System.out.println("##### stripTabCharacter #####");  
        String text = " abc\t ";  
        System.out.println(text.strip()); //abc  
        System.out.println(text.strip().length()); //3  
        System.out.println(text.stripLeading().length()); //5  
        System.out.println(text.stripTrailing().length()); //4  
    }  
  
  
    private static void trimTabCharacter() {  
        System.out.println("##### trimTabCharacter #####");  
        String text = " abc\t ";  
        System.out.println(text.trim()); //abc  
        System.out.println(text.trim().length()); //3  
    }  
  
  
    private static void stripSpecialCharacters() {  
        System.out.println("##### stripSpecialCharacters #####");  
        String contentWithTab = "\t   a b c\n \r";  
        System.out.println(contentWithTab);  
        System.out.println(contentWithTab.length()); //12  
  
        System.out.println(contentWithTab.strip()); // a b c  
        System.out.println(contentWithTab.strip().length());   //5  
    }  
  
    private static void trimSpecialCharacters() {  
        System.out.println("##### trimSpecialCharacters #####");  
        String contentWithTab = "\t   a b c\n \r";  
        System.out.println(contentWithTab);  
        System.out.println(contentWithTab.length()); //12  
  
        System.out.println(contentWithTab.trim()); //a b c  
        System.out.println(contentWithTab.trim().length());   //5  
    }  
  
    private static void trimUnicodeContent() {  
        System.out.println("##### trimUnicodeContent #####");  
        String content = "\u2000abc\u2000";  
        System.out.println(content);  
        System.out.println(content.trim()); // DOES NOT SUPPORT Unicode  
    }  
  
    private static void stripUnicodeContent() {  
        System.out.println("##### stripUnicodeContent #####");  
        char ch = '\u2000';  
        String content = "\u2000abc\u2000";  
        System.out.println(content);  
        System.out.println(content.strip());  
    }}
```

#### Working with Indentation

```java
public String indent(int numberSpaces)
public String stripIndent()
```

The`` indent()`` method 
- ==**Positive: Adds the same number of blank spaces to the beginning of each line.**==
- ==**Negative: Tries to remove the specified number of whitespace characters from the beginning of the line.**==
- ==**Zero: The indentation remains unchanged.**==
---

**If you call ``indent()`` with a negative number and try to remove more whitespace characters than are present at the beginning of the line, Java will remove all that it can find.**

---
``indent()`` also normalizes whitespace characters. What does normalizing whitespace mean, you ask?
- ==**First, a line break is added to the end of the string if not already there.**==
- ==**Second, any line breaks are converted to the ``\n`` format. Regardless of whether your operating system uses**==

```java
String text = "  Line 1\n  Line 2  ";  
String indented = text.indent(2);  // Positive: Adds 2 spaces  
String normalized = text.indent(-3);  // Negative: No change in indentation  
  
System.out.println("indented:" +indented);  
System.out.println("normalized:" +normalized);
```
**Because of ``\n`` at the end of Line 1, ``indent()`` method also applies to Line 2 and gives the output below**

```text
indented:    Line 1
    Line 2  

normalized:Line 1
Line 2  
```

The ``stripIndent()`` method is useful when a String was built with concatenation rather than using a text block. ==**It gets rid of all incidental whitespace.**== This means that all non-blank lines are shifted left so the same number of whitespace characters are removed from each line and the first character that remains is not blank

```java
public static void main(String args[]) {
	String example = """
		This is an example
		demonstrating the usage
		of stripIndent().
		""";
	System.out.println(example.stripIndent());
}
```

```text
This is an example
demonstrating the usage
of stripIndent().
```

==**If the `stripIndent()` method is used and there are no leading spaces on the first line of a multiline string, no changes will occur. `stripIndent()` only removes the common indentation level from each line, and if there are no leading spaces on the first line, the text remains unchanged.**==

```java
String text = "No leading spaces.\n  Indented line.\n  Another indented line.";
System.out.println(text.stripIndent());
```

```text
No leading spaces.
  Indented line.
  Another indented line.
```

Like ``indent()``, ``\r\n`` is turned into \n. However, ==**the ``stripIndent()`` method does not add a trailing line break if it is missing.**==

| Method               | Indent change                                    | Normalizes existing line breaks | Adds line break at end if missing |
|----------------------|--------------------------------------------------|---------------------------------|------------------------------------|
| `indent(n)` where n > 0 | Adds n spaces to beginning of each line           | Yes                             | Yes                                |
| `indent(n)` where n == 0| No change                                        | Yes                             | Yes                                |
| `indent(n)` where n < 0 | Removes up to n spaces from each line             | Yes                             | Yes                                |
| `stripIndent()`       | Removes all leading incidental whitespace         | Yes                             | No                                 |

```java
10: var block = """
11: a
12: b
13: c""";
14: var concat = " a\n"
15: + "  b\n"
16: + " c";
17: System.out.println(block.length()); // 6
18: System.out.println(concat.length()); // 9
19: System.out.println(block.indent(1).length()); // 10
20: System.out.println(concat.indent(-1).length()); // 7
21: System.out.println(concat.indent(-4).length()); // 6
22: System.out.println(concat.stripIndent().length()); // 6
```

- Lines 10–16 create similar strings using a text block and a regular String, respectively. We say “similar” because concat has a whitespace character at the beginning of each line while block does not.
- Line 17 counts the six characters in block, which are the three letters, the blank space before b, and the \n after a and b.
- Line 18 counts the nine characters in concat, which are the three letters, one blank space before a, two blank spaces before b, one blank space before c, and the \n after a and b.
- line 19, we ask Java to add a single blank space to each of the three lines in block. However, the output says we added 4 characters rather than 3 since the length went from 6 to 10 This mysterious additional character is thanks to the line termination normalization. ==**Since the text block doesn’t have a line break at the end, indent() adds one!**==
- line 20, we remove one whitespace character from each of the three lines of concat. This gives a length of seven.
- line 21, we ask Java to remove four whitespace characters from the same three lines. Since there are not four whitespace characters, Java does its best. The single space is removed before a and c. Both spaces are removed before b. The length of six should make sense here; we removed one more character here than on line 20.
- line 22 uses the ``stripIndent()`` method. All of the lines have at least one whitespace character. Since they do not all have two whitespace characters, the method only gets rid of one character per line. Since no new line is added by ``stripIndent()``, the length is six, which is three less than the original nine.

```java
public class WorkingWithIndentation {  
  
    public static void main(String[] args) {  
  
        indentTextBlock();  
  
        indentTextBlock2();  
  
        indentTextBlock3();  
  
        indentTextBlock4();  
  
        indentConcat();  
  
        indentConcat2();  
  
        stripIndent();  
  
        stripIndent2();  
  
    }  
    private static void indentTextBlock() {  
  
        System.out.println("##### indentTextBlock #####");  
  
        var block = """   
                a  
                 b                c""";  
  
        for (char c : block.toCharArray()) {  
            System.out.print(String.format("\\u%04x", (int) c) + " | ");  
        }        System.out.println();  
  
        System.out.println(block);  
        System.out.println(block.length()); // 6  
  
        System.out.println(block.indent(1));  
        System.out.println(block.indent(1).length()); // 10  
  
        // We ask Java to add a single blank space to each of the three lines in block. 
        // However, the output says we added 4 characters rather than 3 since the length went from 6 to 10.
	   // This mysterious additional character is thanks to the line termination normalization.
	   // Since the text block doesn’t have a line break at the end, indent() adds one!    
	}  
  
    private static void indentTextBlock2() {  
  
        System.out.println("##### indentTextBlock2 #####");  
  
        var block = """   
                a  
                 b                c                """;  
  
        for (char c : block.toCharArray()) {  
            System.out.print(String.format("\\u%04x", (int) c) + " | ");  
        }        System.out.println();  
  
        System.out.println(block);  
        System.out.println(block.length()); // 7  
  
        System.out.println(block.indent(1));  
        System.out.println(block.indent(1).length()); // 10  
  
        // We have line break! The indent does not add it at the end.    }  
  
    private static void indentTextBlock3() {  
  
        System.out.println("##### indentTextBlock3 #####");  
  
        var block = """   
                a\n  
                 b\n  
                c\n  
                """;  
  
        for (char c : block.toCharArray()) {  
            System.out.print(String.format("\\u%04x", (int) c) + " | ");  
        }        System.out.println();  
  
        System.out.println(block);  
        System.out.println(block.length()); // 10  
  
        System.out.println(block.indent(1));  
        System.out.println(block.indent(1).length()); // 16  
  
        // We have line break! The indent does not add it at the end.    
	}  
  
    private static void indentTextBlock4() {  
  
        System.out.println("##### indentTextBlock4 #####");  
  
        var block = """   
                a  
                   b                c""";  
  
        System.out.println(block);  
        System.out.println(block.length()); // 8  
        System.out.println(block.indent(-1));  
        System.out.println(block.indent(-1).length()); // 8  
  
    }  
  
    private static void indentConcat() {  
  
        System.out.println("##### indentConcat #####");  
  
        var concat = " a\n"  
                   + "  b\n"  
                   + " c";  
  
        System.out.println(concat.length());    //9  
        System.out.println(concat.indent(-1).length()); // 7  
  
        // We remove one whitespace character from each of the three lines of concat.
        // This gives a length of seven. We started with nine, got rid of three characters,
        // and added a trailing normalized new line.  
  
        System.out.println(concat.indent(-4));  
        System.out.println(concat.indent(-4).length()); // 6  
  
        // we ask Java to remove four whitespace characters from the same three lines.
        // Since there are not four whitespace characters, Java does its best.
        // The single space is removed before a and c.
        // Both spaces are removed before b. The length of six should make sense here; we removed one more character here    
	}  
  
    private static void indentConcat2() {  
  
        System.out.println("##### indentConcat2 #####");  
  
        var concat = " a\n"  
                   + "  b\n"  
                   + " c\n";  
  
        System.out.println(concat.length());    //10  
        System.out.println(concat.indent(-1).length()); // 7  
  
        // We remove one whitespace character from each of the three lines of concat.       
		// This gives a length of seven. We started with nine, got rid of three characters,   
		// and NOT added a trailing normalized new line.  
  
        System.out.println(concat.indent(-4).length()); // 6  
  
        // we ask Java to remove four whitespace characters from the same three lines.        // Since there are not four whitespace characters, Java does its best.        // The concat ends with \n !    
	}  
  
  
    private static void stripIndent() {  
  
        System.out.println("##### stripIndent #####");  
  
        var concat = " a\n"  
                   + "  b\n"  
                   + " c";  
  
        System.out.println(concat.length()); // 9  
  
        System.out.println(concat.stripIndent());  
        System.out.println(concat.stripIndent().length()); // 6  
  
  
        // All of the lines have at least one whitespace character.        
        // Since they do not all have two whitespace characters,        
        // the method only gets rid of one character per line.       
		// Since no new line is added by stripIndent(), the length is six, which is three less than the original nine.    
	}  
  
    private static void stripIndent2() {  
  
        System.out.println("##### stripIndent2 #####");  
  
        var concat = "a\n"  
                   + "  b\n"  
                   + " c";  
  
        System.out.println(concat.length()); //8  
  
        System.out.println(concat);  
        System.out.println(concat.stripIndent());  
        System.out.println(concat.stripIndent().length()); // 8  
  
    }  
}
```
#### Translating Escapes

When we escape characters, we use a single backslash. For example, ``\t`` is a tab. If we don’t want this behavior, we add another backslash to escape the backslash, so ``\\t`` is the literal string ``\t``.
==**The ``translateEscapes()`` method takes these literals and turns them into the equivalent escaped character.**==

```java
public String translateEscapes()
```

```java
var str = "1\\t2";
System.out.println(str); // 1\t2
System.out.println(str.translateEscapes()); // 1 2
```

- ==**The first line prints the literal string \t because the backslash is escaped.**==
- ==**The second line prints an actual tab since we translated the escape.**==

This method can be used for escape sequences such as ``\t`` (tab), ``\n`` (new line), ``\s`` (space), ``\"`` (double quote), and ``\'`` (single quote.)

```java
public class TranslatingEscapes {  
  
    public static void main(String[] args) {  
  
        System.out.println("---------");  
  
        System.out.println("1\t2");  
        System.out.println("1\"2");  
        System.out.println("1\n2");  
        System.out.println("1\s2");  
  
        System.out.println("---------");  
  
        var str = "1\\t2";  
        System.out.println(str); // 1\t2  
        System.out.println(str.translateEscapes()); // 1 2  
  
        System.out.println("---------");  
  
        var str2 = "1\\n2";  
        System.out.println(str2); // 1\n2  
        System.out.println(str2.translateEscapes()); // 1 new line 2  
  
        System.out.println("---------");  
  
        var str3 = "1\\s2";  
        System.out.println(str3); // 1\s2  
        System.out.println(str3.translateEscapes()); // 1 2  
  
        System.out.println("---------");  
  
        var str4 = "1\\\"2";  
        System.out.println(str4); // 1\"2  
        System.out.println(str4.translateEscapes()); // 1"2  
  
        System.out.println("---------");  
  
        var str5 = "1\\\'2";  
        System.out.println(str5); // 1\'2  
        System.out.println(str5.translateEscapes()); // 1'2  
    }  
}
```

#### Checking for Empty or Blank Strings

```java
public boolean isEmpty()
public boolean isBlank()
```

```java
public static void main(String[] args) {  
  
    System.out.println(" ".isEmpty()); // false  
    System.out.println("".isEmpty()); // true  
    System.out.println(" ".isBlank()); // true  
    System.out.println("         ".isBlank()); // true  
    System.out.println("         ".isEmpty()); // false  
    System.out.println("".isBlank()); // true  
}
```

- The first line prints ``false`` because the ``String`` is not empty; it has a blank space in it.
- The second line prints ``true`` because this time, there are no characters in the ``String``.
- The final two lines print true because there are no characters other than whitespace present.
#### Formatting Values

Two of the methods take the format string as a parameter, and the other uses an instance for that value. One method takes a ``Locale``

The method parameters are used to construct a formatted String in a single method call, rather than via a lot of format and concatenation operations. They return a reference to the instance they are called on so that operations can be chained together.

```java
public static String format(String format, Object args...)
public static String format(Locale loc, String format, Object args...)
public String formatted(Object args...)
```

```java
var name = "Kate";
var orderId = 5;
// All print: Hello Kate, order 5 is ready
System.out.println("Hello "+name+", order "+orderId+" is ready");
System.out.println(String.format("Hello %s, order %d is ready",
name, orderId));
System.out.println("Hello %s, order %d is ready"
.formatted(name, orderId));
```

In the ``format()`` and ``formatted()`` operations, the parameters are inserted and formatted via symbols in the order that they are provided in the ``vararg``.

| Symbol | Description                                      |
|--------|--------------------------------------------------|
| `%s`   | Applies to any type, commonly String values      |
| `%d`   | Applies to integer values like int and long      |
| `%f`   | Applies to floating-point values like float and double |
| `%n`   | Inserts a line break using the system-dependent line separator |
```java
var name = "James";
var score = 90.25;
var total = 100;
System.out.println("%s:%n Score: %f out of %d"
.formatted(name, score, total));
```

```text
James:
Score: 90.250000 out of 100
```

==**Mixing data types may cause exceptions at runtime.**== 
### Method Chaining

It is common to call multiple methods as shown here:
```java
var start = "AniMaL ";
var trimmed = start.trim(); // "AniMaL"
var lowercase = trimmed.toLowerCase(); // "animal"
var result = lowercase.replace('a', 'A'); // "AnimAl"
System.out.println(result);
```

Each time one is called, the returned value is put in a new variable. There are four String values along the way, and ``AnimAl`` is output.
==**However, on the exam, there is a tendency to cram as much code as possible into a small space. You’ll see code using a technique called *method chaining.***==

```java
String result = "AniMaL ".trim().toLowerCase().replace('a', 'A');
System.out.println(result);
```

==**To read code that uses method chaining, start at the left and evaluate the first method. Then call the next method on the returned value of the first method. Keep going until you get to the semicolon.**==

```java
public static void main(String[] args) {  
    String a = "abc";  
    String b = a.toUpperCase();  
    b = b.replace("B", "2").replace('C', '3');  
    System.out.println("a=" + a); // a=abc  
    System.out.println("b=" + b); // b=A23  
}
```
## Using the ``StringBuilder`` Class

```java
10: String alpha = "";
11: for(char current = 'a'; current <= 'z'; current++)
12: alpha += current;
13: System.out.println(alpha);
```

==**because the ``String`` object is immutable, a new String object is assigned to alpha, and the ``""`` object becomes eligible for garbage collection.**==

The sequence of events continues, and after 26 iterations through the loop, a total of 27 objects are instantiated, most of which are immediately eligible for garbage collection. 

The ``StringBuilder`` class creates a ``String`` without storing all those interim ``String`` values. Unlike the ``String`` class, ``StringBuilder`` is not immutable.

```java
15: StringBuilder alpha = new StringBuilder();
16: for(char current = 'a'; current <= 'z'; current++)
17: alpha.append(current);
18: System.out.println(alpha);
```

This code reuses the same `StringBuilder` without creating an interim String each time.
### Mutability and Chaining

The exam will likely try to trick you with respect to String and StringBuilder being mutable.
Chaining makes this even more interesting. **==When we chained String method calls, the result was a new String with the answer.==** Chaining StringBuilder methods doesn’t work this way. Instead, the **==StringBuilder changes its own state and returns a reference to itself.==**

```java
4: StringBuilder sb = new StringBuilder("start");
5: sb.append("+middle"); // sb = "start+middle"
6: StringBuilder same = sb.append("+end"); // "start+middle+end"
```

Line 5 adds text to the end of sb. It also returns a reference to sb, which is ignored. Line 6 also adds text to the end of sb and returns a reference to sb. This time the reference is stored in same. This means sb and same point to the same object and would print out the same value.

```java
4: StringBuilder a = new StringBuilder("abc");
5: StringBuilder b = a.append("de");
6: b = b.append("f").append("g");
7: System.out.println("a=" + a);
8: System.out.println("b=" + b);
```

both print "abcdefg". ==**There’s only one ``StringBuilder`` object here. We know that because new StringBuilder() is called only once.**==
### Creating a ``StringBuilder``

```java
StringBuilder sb1 = new StringBuilder();
StringBuilder sb2 = new StringBuilder("animal");
StringBuilder sb3 = new StringBuilder(10);
```

The final example tells Java that we have some idea of how big the eventual value will be and would like the ``StringBuilder`` to reserve a certain capacity, or number of slots, for characters.
### Important ``StringBuilder`` Methods

#### Using Common Methods

==**These four methods work exactly the same as in the String class.**==

```java
var sb = new StringBuilder("animals");
String sub = sb.substring(sb.indexOf("a"), sb.indexOf("al"));
int len = sb.length();
char ch = sb.charAt(6);
System.out.println(sub + " " + len + " " + ch);
```

**Notice that substring() returns a String rather than a StringBuilder. That is why sb is not changed.**
#### Appending Values

The ``append()`` method is by far the most frequently used method in StringBuilder. it adds the parameter to the StringBuilder and returns a reference to the current StringBuilder.

```java
public StringBuilder append(String str)
```

```java
var sb = new StringBuilder().append(1).append('c');
sb.append("-").
append(true);
System.out.println(sb); // 1c-true
```

can just call ``append()`` without having to convert your parameter to a String first.`
#### Inserting Data

The ``insert()`` method adds characters to the StringBuilder at the requested index and returns a reference to the current ``StringBuilder``

```java
public StringBuilder insert(int offset, String str)
```

```java
3: var sb = new StringBuilder("animals");
4: sb.insert(7, "-"); // sb = animals-
5: sb.insert(0, "-"); // sb = -animals-
6: sb.insert(4, "-"); // sb = -ani-mals-
7: System.out.println(sb);
```
#### Deleting Contents

The ``delete()`` method is the opposite of the ``insert()`` method.  It removes characters from the sequence and returns a reference to the current StringBuilder. The ``deleteCharAt(``) method is convenient when you want to delete only one character.

```java
public StringBuilder delete(int startIndex, int endIndex)
public StringBuilder deleteCharAt(int index)
```

```java
var sb = new StringBuilder("abcdef");
sb.delete(1, 3); // sb = adef
sb.deleteCharAt(5); // exception
```

The ``delete()`` method is more flexible than some others when it comes to array indexes. If you specify a second parameter that is past the end of the StringBuilder, Java will just assume you meant the end.
#### Replacing Portions

**==The ``replace()`` method works differently for StringBuilder than it did for String==**

```java
public StringBuilder replace(int startIndex, int endIndex, String newString)
```

```java
var builder = new StringBuilder("pigeon dirty");
builder.replace(3, 6, "sty");
System.out.println(builder); // pigsty dirty
```

First, Java deletes the characters starting with index 3 and ending right before index 6. This gives us pig dirty. Then Java inserts the value "sty" in that position. In this example, the number of characters removed and inserted are the same. However, there is no reason they have to be.

```java
var builder = new StringBuilder("pigeon dirty");
builder.replace(3, 100, "");
System.out.println(builder);
```

the method is first doing a logical delete. The ``replace()`` method allows specifying a second parameter that is past the end of the StringBuilder. That means only the first three characters remain.
#### Reversing

The ``reverse()`` method does just what it sounds like: it reverses the characters in the sequences and returns a reference to the current ``StringBuilder``.

```java
public StringBuilder reverse()
```

```java
var sb = new StringBuilder("ABC");
sb.reverse();
System.out.println(sb);
```


----

**Working with `toString()`**

The ``Object`` class contains a ``toString()`` method that many classes provide custom implementations of. The ``StringBuilder`` class is one of these.

```java
var sb = new StringBuilder("ABC");
String s = sb.toString();
```

**Often ``StringBuilder`` is used internally for performance purposes, but the end result needs to be a String.**

---
## Understanding Equality

### Comparing ``equals()`` and ``==``

```java
var one = new StringBuilder();
var two = new StringBuilder();
var three = one.append("a");
System.out.println(one == two); // false
System.out.println(one == three); // true
```

The one and two variables are both completely separate ``StringBuilder`` objects, giving us two objects. Therefore, the first print statement gives us ``false``.  The three variable is more interesting. Remember how ``StringBuilder`` methods like to return the current reference for chaining? This means one and three both point to the same object, and the second print statement gives us ``true``.

``equals()`` uses logical equality rather than object equality for String objects:

```java
var x = "Hello World";
var z = " Hello World".trim();
System.out.println(x.equals(z)); // true
```

==**``equals()`` to check the values inside the String rather than the string reference itself.**==
==**If a class doesn’t have an ``equals()`` method, Java determines whether the references point to the same object, which is exactly what ``==`` does.**==

**==StringBuilder did not implement equals(). If you call equals() on two StringBuilder instances, it will check reference equality==**. You can call ``toString()`` on StringBuilder to get a String to check for equality instead.

the exam might try to trick you with a question like this.

```java
var name = "a";
var builder = new StringBuilder("a");
System.out.println(name == builder); // DOES NOT COMPILE
```

``==`` is checking for object reference equality. The compiler is smart enough to know that two references can’t possibly point to the same object when they are completely different types.
### The String Pool

Since strings are everywhere in Java, they use up a lot of memory. Java realizes that many strings repeat in the program and solves this issue by reusing common ones. ==**The string pool, also known as the intern pool, is a location in the Java Virtual Machine (JVM) that collects all these strings.**==

==**The string pool contains literal values and constants that appear in your program. For example, *"name"* is a literal and therefore goes into the string pool. The ``myObject.toString()`` method returns a string but not a literal, so it does not go into the string pool.**==


```java
var x = "Hello World";
var y = "Hello World";
System.out.println(x == y); // true
```

Remember that ==**a String is immutable and literals are pooled. The JVM created only one literal in memory. The x and y variables both point to the same location in memory**==; therefore, the statement outputs true

```java
var x = "Hello World";
var z = " Hello World".trim();
System.out.println(x == z); // false
System.out.println(x.equals(z)); // true
```

we don’t have two of the same String literal. ==**Although x and z happen to evaluate to the same string, one is computed at runtime. Since it isn’t the same at compile-time, a new String object is created**==

```java
var singleString = "hello world";
var concat = "hello ";
concat += "world";
System.out.println(singleString == concat); // false
```

==**Calling ``+=`` is just like calling a method and results in a new String**==

```java
var x = "Hello World"; // String Pool
var y = new String("Hello World"); // New Object @ Heap
System.out.println(x == y); // false
```

 ==**The ``intern()`` method will use an object in the string pool if one is present.**==

```java
public String intern()
```

```java
var name = "Hello World";
var name2 = new String("Hello World").intern();
System.out.println(name == name2); // true
```


```java
15: var first = "rat" + 1;
16: var second = "r" + "a" + "t" + "1";
17: var third = "r" + "a" + "t" + new String("1");
18: System.out.println(first == second); // true
19: System.out.println(first == second.intern()); // true
20: System.out.println(first == third); // false
21: System.out.println(first == third.intern()); // false 
```

- On line 15, we have a compile-time constant that automatically gets placed in the string pool as "rat1".
- On line 16, we have a more complicated expression that is also a compile-time constant. Therefore, first and second share the same string pool reference. This makes lines 18 and 19 print true.
- On line 17, we have a String constructor. This means we no longer have a compile-time constant, and third does not point to a reference in the string pool. Therefore, line 20 prints false.
- On line 21, the intern() call looks in the string pool. Java notices that first points to the same String and prints true.

```java
public class StringPoolFinal {  
  
    public static void main(String[] args) {  
  
  
        finalStrings();  // true
        finalStringsV2(); // false
        checkEquality();  // true
    }  
    private static void finalStrings() {  
        String fullMsg = "hello world";  
  
        final String msg1 = "hello";  
        final String msg2 = " world";  
  
        String msg3 = msg1 + msg2;  
  
        System.out.println(fullMsg == msg3);  
    }  
    private static void finalStringsV2() {  
        String fullMsg = "hello world";  
  
        final String msg1 = helloMessage();  
        final String msg2 = worldMessage();  
  
        String msg3 = msg1 + msg2;  
  
        System.out.println(fullMsg == msg3);  
    }  
    private static String helloMessage() {  
        return "hello";  
    }  
    private static String worldMessage() {  
        return " world";  
    }  
  
    private static void checkEquality() {  
  
        String fullMsg = "hello world";  
  
        String msg1 = "hello";  
        String msg2 = " world";  
  
        String msg3 = msg1 + msg2;  
  
        System.out.println(fullMsg.equals(msg3));  
    }}
```

## Understanding Arrays 

An array is an area of memory on the heap with space for a designated number of elements.
an array can be of any other Java type.

```java
char[] letters;
```

==**Keep in mind that letters is a reference variable and not a primitive. The char type is a primitive. But char is what goes into the array and not the type of the array itself. The array itself is of type char[].**==

An array is an ordered list. It can contain duplicates.
### Creating an Array of Primitives

The most common way to create an array

![[Pasted image 20240206131327.png]]


==**When you use this form to instantiate an array, all elements are set to the default value for that type.**==

Another way to create an array is to specify all the elements it should start out with:

```java
int[] moreNumbers = new int[] {42, 55, 99};
```

Java recognizes that this expression is redundant. Since you are specifying the type of the array on the left side of the equals sign, Java already knows the type. And since you are specifying the initial values, it already knows the size. As a shortcut, Java lets you write this:

```java
int[] moreNumbers = {42, 55, 99};
```

This approach is called an ***anonymous array***.

```java
int[] numAnimals;
int [] numAnimals2;
int []numAnimals3;
int numAnimals4[];
int numAnimals5 [];
```


---

**Multiple “*Arrays*” in Declarations**

```java
int[] ids, types;
```

**two variables of type int[]. This seems logical enough. After all, int a, b; created two int variables**

```java
int ids[], types;
```

**This time we get one variable of type int[] and one variable of type int. Java sees this line of code and thinks something like this: “They want two variables of type int. The first one is called ids[]. This one is an int[] called ids. The second one is just called types. No brackets, so it is a regular integer.”**

---
### Creating an Array with Reference Variables

You can choose any Java type to be the type of the array. This includes classes you create yourself.

```java
String[] bugs = { "cricket", "beetle", "ladybug" };
String[] alias = bugs;
System.out.println(bugs.equals(alias)); // true
System.out.println(bugs.toString()); // [Ljava.lang.String;@160bc7c0
```

We can call ``equals()`` because an array is an object. It returns true because of reference equality. The ``equals()`` method on arrays does not look at the elements of the array.

what do you think this array points to?

```java
public class Names {
	String names[];
}
```

==**The code never instantiated the array, so it is just a reference variable to null**==

```java
public class Names {
String names[] = new String[2];
}
```

Each of those two slots currently is null but has the potential to point to a String object.

```java
3: String[] strings = { "stringValue" };
4: Object[] objects = strings;
5: String[] againStrings = (String[]) objects;
6: againStrings[0] = new StringBuilder(); // DOES NOT COMPILE
7: objects[0] = new StringBuilder(); // Careful!
```
 
 Line 7 is where this gets interesting. From the point of view of the compiler, this is just fine. A ``StringBuilder`` object can clearly go in an ``Object[]``. The problem is that we don’t actually have an ``Object[]``. We have a ``String[]`` referred to from an ``Object[]`` variable. At runtime, the code throws an ``ArrayStoreException``.
### Using an Array

```java
4: String[] mammals = {"monkey", "chimp", "donkey"};
5: System.out.println(mammals.length); // 3
6: System.out.println(mammals[0]); // monkey
7: System.out.println(mammals[1]); // chimp
8: System.out.println(mammals[2]); // donkey
```

Note that there are no parentheses after length since it is not a method.

```java
4: String[] mammals = {"monkey", "chimp", "donkey"};
5: System.out.println(mammals.length()); // DOES NOT COMPILE
```


```java
var birds = new String[6];
System.out.println(birds.length);
```

Even though all six elements of the array are null, there are still six of them. ==**The length attribute does not consider what is in the array; it only considers how many slots have been allocated.**==

```java
5: var numbers = new int[10];
6: for (int i = 0; i < numbers.length; i++)
7: numbers[i] = i + 5;
```

The exam will test whether you are being observant by trying to access elements that are not in the array.
why each of these throws an `ArrayIndexOutOfBoundsException` for our array of size 10?

```java
numbers[10] = 3;
numbers[numbers.length] = 5;
for (int i = 0; i <= numbers.length; i++)
numbers[i] = i + 5;
```

- The first one is trying to see whether you know that indexes start with 0. Since we have 10 elements in our array, this means only numbers[0] through numbers[9] are valid.
- The second example assumes you are clever enough to know that 10 is invalid and disguises it by using the length field. However, the length is always one more than the maximum valid index.
- Finally, the for loop incorrectly uses <= instead of <, which is also a way of referring to that tenth element.
### Sorting

Java makes it easy to sort an array by providing a sort method—or rather, a bunch of sort methods.
```java
import java.util.*; // import whole package including Arrays
import java.util.Arrays; // import just Arrays

Arrays.sort()
```

Remember that if you are shown a code snippet, you can assume the necessary imports are there.

```java
int[] numbers = { 6, 9, 1 };
Arrays.sort(numbers);
for (int i = 0; i < numbers.length; i++)
System.out.print(numbers[i] + " "); // 1 6 9
```

```java
String[] strings = { "10", "9", "100" };
Arrays.sort(strings);
for (String s : strings)
System.out.print(s + " "); // 10 100 9
```

==**The problem is that String sorts in alphabetic order, and 1 sorts before 9. (Numbers sort before letters, and uppercase sorts before lowercase.)**==
### Searching
Java also provides a convenient way to search, ==**but only if the array is already sorted.**==

==**Returns:**==
==**index of the search key, if it is contained in the array; otherwise,`` (-(insertion point) - 1)``. The insertion point is defined as the point at which the key would be inserted into the array**==

| Scenario                          | Result                                                                       |
| --------------------------------- | ---------------------------------------------------------------------------- |
| Target element found in sorted array | Index of match                                                               |
| Target element not found in sorted array | Negative value showing one smaller than the negative of the index, where a match needs to be inserted to preserve sorted order  |
| Unsorted array                    | A surprise; this result is undefined                                       |

```java
3: int[] numbers = {2,4,6,8};
4: System.out.println(Arrays.binarySearch(numbers, 2)); // 0
5: System.out.println(Arrays.binarySearch(numbers, 4)); // 1
6: System.out.println(Arrays.binarySearch(numbers, 1)); // -1
7: System.out.println(Arrays.binarySearch(numbers, 3)); // -2
8: System.out.println(Arrays.binarySearch(numbers, 9)); // -5
   System.out.println(Arrays.binarySearch(numbers, 30)); // -5
	
	int[] numbersNotSorted = new int[]{3, 2, 1};  
	System.out.println(Arrays.binarySearch(numbersNotSorted, 2));  
	System.out.println(Arrays.binarySearch(numbersNotSorted, 3));  
  
	// The array isn’t sorted. This means the output will not be defined.
```

- line 3 is a sorted array
- Line 4 searches for the index of 2. The answer is index 0.
- Line 5 searches for the index of 4, which is 1.
- Line 6 searches for the index of 1. Although 1 isn’t in the list, the search can determine that it should be inserted at element 0 to preserve the sorted order. Since 0 already means something for array indexes, Java needs to subtract 1 to give us the answer of –1.
- Line 7 is similar. Although 3 isn’t in the list, it would need to be inserted at element 1 to preserve the sorted order. We negate and subtract 1 for consistency, getting –1 –1, also known as –2.
- line 8 wants to tell us that 9 should be inserted at index 4. We again negate and subtract 1, getting –4 –1, also known as –5.

```java
5: int[] numbers = new int[] {3,2,1};
6: System.out.println(Arrays.binarySearch(numbers, 2));
7: System.out.println(Arrays.binarySearch(numbers, 3));
```

Note that on line 5, the array isn’t sorted. This means the output will not be defined. ==**As soon as you see the array isn’t sorted, look for an answer choice about unpredictable output.**==
### Comparing

Java also provides methods to compare two arrays to determine which is ***“smaller.”***
#### Using ``compare()``
There are a bunch of rules you need to know before calling ``compare()``.

- ==**A negative number means the first array is smaller than the second.**==
- ==**A zero means the arrays are equal.**==
-  ==**A positive number means the first array is larger than the second.**==

```java
System.out.println(Arrays.compare(new int[] {1}, new int[] {2})); // -1 Negative
```

how to compare arrays of different lengths:

- ==**If both arrays are the same length and have the same values in each spot in the same order, return zero.**==
- ==**If all the elements are the same but the second array has extra elements at the end, return a negative number.**==
- ==**If all the elements are the same, but the first array has extra elements at the end, return a positive number.**==
- ==**If the first element that differs is smaller in the first array, return a negative number.**==
- ==**If the first element that differs is larger in the first array, return a positive number.**==

What does smaller means? 

-  ==**null is smaller than any other value.**==
- ==**For numbers, normal numeric order applies.**==
- ==**For strings, one is smaller if it is a prefix of another.**==
- ==**For strings/characters, numbers are smaller than letters.**==
- ==**For strings/characters, uppercase is smaller than lowercase.**==

==**For strings/characters: null -> numbers -> uppercase -> lowercase**==

```java
public static void main(String[] args) {  
  
    System.out.println(Arrays.compare(new int[]{1}, new int[]{1})); // 0  
    System.out.println(Arrays.compare(new int[]{1}, new int[]{2})); // negative  
    System.out.println(Arrays.compare(new int[]{1, 2}, new int[]{1})); // positive  
    System.out.println(Arrays.compare(new int[]{1, 2}, new int[]{2})); // negative  
    System.out.println(Arrays.compare(new int[]{1, 2, 5, 3, 20}, new int[]{3})); // negative  
  
    System.out.println();  
    System.out.println(Arrays.compare(new int[]{1, 2}, new int[]{1, 2})); // zero  
    System.out.println(Arrays.compare(new int[]{1, 2, -1}, new int[]{1, 2})); // positive  
    System.out.println(Arrays.compare(new int[]{1, 2}, new int[]{1, 2, -1})); // negative  
  
    System.out.println();  
    System.out.println(Arrays.compare(new String[]{"a"}, new String[]{"aa"})); // negative  
    System.out.println(Arrays.compare(new String[]{"a"}, new String[]{"A"})); // positive  
  
    //Uppercase is smaller than lowercase    System.out.println(Arrays.compare(new String[]{"a"}, new String[]{"Z"})); // positive  
  
    System.out.println(Arrays.compare(new String[]{"a"}, new String[]{null})); // positive  
  
    // null is smaller than a letter.  
    // System.out.println(Arrays.compare(new int[]{1}, new String[]{"a"})); // DOES NOT COMPILE}
```

| First array                | Second array               | Result           | Reason                                       |
|----------------------------|----------------------------|------------------|----------------------------------------------|
| `new int[] {1, 2}`          | `new int[] {1}`            | Positive number  | The first element is the same, but the first array is longer.   |
| `new int[] {1, 2}`          | `new int[] {1, 2}`         | Zero             | Exact match                                  |
| `new String[] {"a"}`        | `new String[] {"aa"}`      | Negative number  | The first element is a substring of the second.                |
| `new String[] {"a"}`        | `new String[] {"A"}`       | Positive number  | Uppercase is smaller than lowercase.                        |
| `new String[] {"a"}`        | `new String[] {null}`      | Positive number  | null is smaller than a letter.                              |
==**When comparing two arrays, they must be the same array type.**== 

```java
System.out.println(Arrays.compare(
new int[] {1}, new String[] {"a"})); // DOES NOT COMPILE
```

### Using ``mismatch()``

==**If the arrays are equal, ``mismatch()`` returns -1. Otherwise, it returns the first index where they differ.**==

```java
System.out.println(Arrays.mismatch(new int[] {1}, new int[] {1})); // -1
System.out.println(Arrays.mismatch(new String[] {"a"}, new String[] {"A"})); // 0
System.out.println(Arrays.mismatch(new int[] {1, 2}, new int[] {1})); // 1
```

- In the first example, the arrays are the same, so the result is -1. 
- In the second example, the entries at element 0 are not equal, so the result is 0.
- In the third example, the entries at element 0 are equal, so we keep looking. The element at index 1 is not equal. Or, more specifically, one array has an element at index 1, and the other does not. Therefore, the result is 1.

```java
public static void main(String[] args) {  
    System.out.println(Arrays.mismatch(new int[]{1}, new int[]{1}));  // -1  
    System.out.println(Arrays.mismatch(new String[]{"a"}, new String[]{"A"})); //0  
    System.out.println(Arrays.mismatch(new int[]{1, 2}, new int[]{1})); //1  
    System.out.println(Arrays.mismatch(new int[]{1, 2, -1}, new int[]{1, 2, -1, 5})); //3  
}
```

| Method     | When arrays contain the same data | When arrays are different        |
|------------|------------------------------------|-----------------------------------|
| equals()   | true                               | false                             |
| compare()  | 0                                  | Positive or negative number      |
| mismatch() | -1                                 | Zero or positive index           |
### Using Methods with ``Varargs``

```java
public static void main(String[] args)
public static void main(String args[])
public static void main(String... args) // varargs
```

you can use a variable defined using ``varargs`` as if it were a normal array.
### Working with Multidimensional Arrays

#### Creating a Multidimensional Array

Multiple array separators are all it takes to declare arrays with multiple dimensions.

```java
int[][] vars1; // 2D array
int vars2 [][]; // 2D array
int[] vars3[]; // 2D array
int[] vars4 [], space [][]; // a 2D AND a 3D array
```

- The third example also declares a 2D array.
- The final example declares two arrays on the same line. Adding up the brackets, we see that the vars4 is a 2D array and space is a 3D array.

You can specify the size of your multidimensional array in the declaration if you like:

```java
String [][] rectangle = new String[3][2];
```

You can think of the addressable range as [0][0] through ``[2][1]``, but don’t think of it as a structure of addresses like ``[0,0]`` or ``[2,1]``.

```java
rectangle[0][1] = "set";
```

This array is sparsely populated because it has a lot of null values.

```java
int[][] differentSizes = {{1, 4}, {3}, {9,8,7}};
```

Another way to create an asymmetric array is to initialize just an array’s first dimension and define the size of each array component in a separate statement:

```java
int [][] args = new int[4][];
args[0] = new int[5];
args[1] = new int[3];
```

This technique reveals what you really get with Java: arrays of arrays that, properly managed, offer a multidimensional effect.
#### Using a Multidimensional Array

The most common operation on a multidimensional array is to loop through it.

```java
var twoD = new int[3][2];
for(int i = 0; i < twoD.length; i++) {
for(int j = 0; j < twoD[i].length; j++)
System.out.print(twoD[i][j] + " "); // print element
System.out.println(); // time for a new row
}
```

two loops here. The first uses index i and goes through the first subarray for twoD. The second uses a different loop variable, j. It is important that these be different variable names so the loops don’t get mixed up. The inner loop looks at how many elements are in the second-level array. The inner loop prints the element and leaves a space for readability. When the inner loop completes, the outer loop goes to a new line and repeats the process for the next element.

```java
for(int[] inner : twoD) {
for(int num : inner)
System.out.print(num + " ");
System.out.println();
}
```

## Calculating with Math APIs

Pay special attention to return types in math questions. They are an excellent opportunity for trickery!
### Finding the Minimum and Maximum

The ``min()`` and ``max()`` methods compare two values and return one of them. 

```java
public static double min(double a, double b)
public static float min(float a, float b)
public static int min(int a, int b)
public static long min(long a, long b)
```

```java
int first = Math.max(3, 7); // 7
int second = Math.min(7, -9); // -9
```
### Rounding Numbers

The ``round()`` method gets rid of the decimal portion of the value, choosing the next higher
number if appropriate. ==**If the fractional part is .5 or higher, we round up.**==

```java
public static long round(double num)
public static int round(float num)
```

```java
long low = Math.round(123.45); // 123
long high = Math.round(123.50); // 124
int fromFloat = Math.round(123.45f); // 123
```

### Determining the Ceiling and Floor

The ``ceil()`` method takes a double value. If it is a whole number, it returns the same value. If it has any fractional value, it rounds up to the next whole number. By contrast, the ``floor()`` method discards any values after the decimal.

```java
public static double ceil(double num)
public static double floor(double num)
```

```java
double c = Math.ceil(3.14); // 4.0
double f = Math.floor(3.14); // 3.0
```

### Calculating Exponents

The ``pow()`` method handles exponents.
```java
public static double pow(double number, double exponent)
```

```java
double squared = Math.pow(5, 2); // 25.0
```

### Generating Random Numbers

The ``random()`` method ==**returns a value greater than or equal to 0 and less than 1**==

```java
public static double random()
```

```java
double num = Math.random();
```

## Working with Dates and Times

### Creating Dates and Times

When working with dates and times, the first thing to do is to decide how much information you need. The exam gives you four choices:

- ==**`LocalDate` Contains just a date—no time and no time zone.**== 
- ==**``LocalTime`` Contains just a time—no date and no time zone**==. 
- ==**``LocalDateTime`` Contains both a date and time but no time zone**.== 
- ==**``ZonedDateTime`` Contains a date, time, and time zone.**== 

```java
System.out.println(LocalDate.now());
System.out.println(LocalTime.now());
System.out.println(LocalDateTime.now());
System.out.println(ZonedDateTime.now());
```

```text
2021–10–25
09:13:07.768
2021–10–25T09:13:07.768
2021–10–25T09:13:07.769–05:00[America/New_York]
```

==**The key is the type of information in the output. The output uses ``T`` to separate the date and time when converting ``LocalDateTime`` to a ``String``. Finally, the fourth adds the time zone offset and time zone.**==

---

**The time zone offset can be listed in different ways: +02:00, GMT+2, and UTC+2 all mean the same thing. You might see any of them on the exam.**

---

Both of these examples create the same date:

```java
var date1 = LocalDate.of(2022, Month.JANUARY, 20);
var date2 = LocalDate.of(2022, 1, 20);
```

```java
public static LocalDate of(int year, int month, int dayOfMonth)
public static LocalDate of(int year, Month month, int dayOfMonth)
```

---

**Java counts starting with 0. Well, months are an exception. For months in the new date and time methods, Java counts starting from 1, just as we humans do.**

---

When creating a time, you can choose how detailed you want to be. You can specify just the hour and minute, or you can include the number of seconds. You can even include nanoseconds if you want to be very precise.

```java
var time1 = LocalTime.of(6, 15); // hour and minute
var time2 = LocalTime.of(6, 15, 30); // + seconds
var time3 = LocalTime.of(6, 15, 30, 200); // + nanoseconds
```

```java
public static LocalTime of(int hour, int minute)
public static LocalTime of(int hour, int minute, int second)
public static LocalTime of(int hour, int minute, int second, int nanos)
```

You can combine dates and times into one object:

```java
var dateTime1 = LocalDateTime.of(2022, Month.JANUARY, 20, 6, 15, 30);
var dateTime2 = LocalDateTime.of(date1, time1);
```

The following method signatures use integer values:

```java
public static LocalDateTime of(int year, int month, int dayOfMonth, int hour, int minute)
public static LocalDateTime of(int year, int month, int dayOfMonth, int hour, int minute, int second)
public static LocalDateTime of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanos)
```

Others take a Month reference:

```java
public static LocalDateTime of(int year, Month month, int dayOfMonth, int hour, int minute)
public static LocalDateTime of(int year, Month month, int dayOfMonth, int hour, int minute, int second)
public static LocalDateTime of(int year, Month month, int dayOfMonth, int hour, int minute, int second, int nanos)
```

Finally, one takes an existing ``LocalDate`` and ``LocalTime``:

```java
public static LocalDateTime of(LocalDate date, LocalTime time)
```

In order to create a ``ZonedDateTime``, we first need to get the desired time zone.

```java
var zone = ZoneId.of("US/Eastern");
var zoned1 = ZonedDateTime.of(2022, 1, 20, 6, 15, 30, 200, zone);
var zoned2 = ZonedDateTime.of(date1, time1, zone);
var zoned3 = ZonedDateTime.of(dateTime1, zone);
```

A better approach is to pass a ``LocalDate`` object and a ``LocalTime`` object, or a ``LocalDateTime`` object. Instead of Integers

```java
public static ZonedDateTime of(int year, int month,
int dayOfMonth, int hour, int minute, int second, int nanos, ZoneId zone)
public static ZonedDateTime of(LocalDate date, LocalTime time, ZoneId zone)
public static ZonedDateTime of(LocalDateTime dateTime, ZoneId zone)
```

==**The date and time classes have private constructors along with static methods that return instances.**==

```java
var d = new LocalDate(); // DOES NOT COMPILE
```

==**You are not allowed to construct a date or time object directly**==. Another trick is what happens when you pass invalid numbers to ``of()``,

```java
var d = LocalDate.of(2022, Month.JANUARY, 32) // DateTimeException
java.time.DateTimeException: Invalid value for DayOfMonth (valid values 1-28/ 31): 32
```
### Manipulating Dates and Times

==**The date and time classes are immutable**==. Remember to assign the results of these methods to a reference variable so they are not lost.

```java
12: var date = LocalDate.of(2022, Month.JANUARY, 20);
13: System.out.println(date); // 2022–01–20
14: date = date.plusDays(2);
15: System.out.println(date); // 2022–01–22
16: date = date.plusWeeks(1);
17: System.out.println(date); // 2022–01–29
18: date = date.plusMonths(1);
19: System.out.println(date); // 2022–02–28
20: date = date.plusYears(5);
21: System.out.println(date); // 2027–02–28
```

There are also nice, easy methods to go backward in time.

```java
22: var date = LocalDate.of(2024, Month.JANUARY, 20);
23: var time = LocalTime.of(5, 15);
24: var dateTime = LocalDateTime.of(date, time);
25: System.out.println(dateTime); // 2024–01–20T05:15
26: dateTime = dateTime.minusDays(1);
27: System.out.println(dateTime); // 2024–01–19T05:15
28: dateTime = dateTime.minusHours(10);
29: System.out.println(dateTime); // 2024–01–18T19:15
30: dateTime = dateTime.minusSeconds(30);
31: System.out.println(dateTime); // 2024–01–18T19:14:30
```

Java is smart enough to hide the seconds and nanoseconds when we aren’t using them.
It is common for date and time methods to be chained.

```java
var date = LocalDate.of(2024, Month.JANUARY, 20);
var time = LocalTime.of(5, 15);
var dateTime = LocalDateTime.of(date, time).minusDays(1).minusHours(10).minusSeconds(30);
```

There are two ways that the exam creators can try to trick you.

```java
var date = LocalDate.of(2024, Month.JANUARY, 20);
date.plusDays(10);
System.out.println(date);
```

Adding 10 days was useless because the program ignored the result. ==**Whenever you see immutable types, pay attention to make sure that the return value of a method call isn’t ignored.**==

```java
var date = LocalDate.of(2024, Month.JANUARY, 20);
date = date.plusMinutes(1); // DOES NOT COMPILE
```

**==``LocalDate`` does not contain time. This means that you cannot add minutes to it==**. This can be tricky in a chained sequence of addition/subtraction operations

```java
public static void main(String[] args) {  
  
    var date = LocalDate.of(2022, Month.JANUARY, 20);  
    System.out.println(date); //2022-01-20  
  
    date = date.plusDays(2); // 2022-01-22  
    System.out.println(date);  
  
    date = date.plusWeeks(1); //2022-01-29  
    System.out.println(date);  
  
    date = date.plusMonths(1); //2022-02-28  
    System.out.println(date);  
  
    // Java is smart enough to realize that February 29, 2022 does not exist, and it gives us February 28, 2022, instead.  
  
    date = date.plusYears(5); // 2027-02-28  
    System.out.println(date);  
  
    // date = date.plusMinutes(1); // DOES NOT COMPILE  
}
```

| Method            | Can call on LocalDate? | Can call on LocalTime? | Can call on LocalDateTime or ZonedDateTime? |
|-------------------|------------------------|------------------------|----------------------------------------------|
| plusYears()       | Yes                    | No                     | Yes                                          |
| minusYears()      | Yes                    | No                     | Yes                                          |
| plusMonths()      | Yes                    | No                     | Yes                                          |
| minusMonths()     | Yes                    | No                     | Yes                                          |
| plusWeeks()       | Yes                    | No                     | Yes                                          |
| minusWeeks()      | Yes                    | No                     | Yes                                          |
| plusDays()        | Yes                    | No                     | Yes                                          |
| minusDays()       | Yes                    | No                     | Yes                                          |
| plusHours()       | No                     | Yes                    | Yes                                          |
| minusHours()      | No                     | Yes                    | Yes                                          |
| plusMinutes()     | No                     | Yes                    | Yes                                          |
| minusMinutes()    | No                     | Yes                    | Yes                                          |
| plusSeconds()     | No                     | Yes                    | Yes                                          |
| minusSeconds()    | No                     | Yes                    | Yes                                          |
| plusNanos()       | No                     | Yes                    | Yes                                          |
| minusNanos()      | No                     | Yes                    | Yes                                          |
### Working with Periods

```java
public static void main(String[] args) {
var start = LocalDate.of(2022, Month.JANUARY, 1);
var end = LocalDate.of(2022, Month.MARCH, 30);
performAnimalEnrichment(start, end);
}
private static void performAnimalEnrichment(LocalDate start, LocalDate end) {
var upTo = start;
while (upTo.isBefore(end)) { // check if still before end
System.out.println("give new toy: " + upTo);
upTo = upTo.plusMonths(1); // add a month
} }
```

This code works fine. It adds a month to the date until it hits the end date. The problem is that this method can’t be reused.
Java has a ``Period`` class that we can pass in. This code does the same thing as the previous example:

```java
public static void main(String[] args) {
    var start = LocalDate.of(2022, Month.JANUARY, 1);
    var end = LocalDate.of(2022, Month.MARCH, 30);
    var period = Period.ofMonths(1); // create a period
    performAnimalEnrichment(start, end, period);
}

private static void performAnimalEnrichment(LocalDate start, LocalDate end, Period period) {
    // uses the generic period
    var upTo = start;
    while (upTo.isBefore(end)) {
        System.out.println("give new toy: " + upTo);
        upTo = upTo.plus(period); // adds the period
    }
}

```

The method can add an arbitrary period of time that is passed in. This allows us to reuse the same method for different periods of time

```java
var annually = Period.ofYears(1); // every 1 year
var quarterly = Period.ofMonths(3); // every 3 months
var everyThreeWeeks = Period.ofWeeks(3); // every 3 weeks
var everyOtherDay = Period.ofDays(2); // every 2 days
var everyYearAndAWeek = Period.of(1, 0, 7); // every year and 7 days
```

There’s one catch. ==**You cannot chain methods when creating a ``Period``.**== The following code looks like it is equivalent to the ``everyYearAndAWeek`` example, but it’s not. **==Only the last method is used because the ``Period.of ``methods are static methods.==**

```java
var wrong = Period.ofYears(1).ofWeeks(1); // every week
```

```java
var wrong = Period.ofYears(1);
wrong = Period.ofWeeks(1);
```

==**The ``of()`` method takes only years, months, and days**==. The ability to use another factory method to pass weeks is merely a convenience. As you might imagine, the actual period is stored in terms of years, months, and days. When you print out the value, Java displays any non-zero parts using the format

![[Pasted image 20240207145939.png]]

```java
System.out.println(Period.ofMonths(3)); // P3M.
```

Java omits any measures that are zero. The last thing to know about Period is what objects it can be used with.

```java
3: var date = LocalDate.of(2022, 1, 20);
4: var time = LocalTime.of(6, 15);
5: var dateTime = LocalDateTime.of(date, time);
6: var period = Period.ofMonths(1);
7: System.out.println(date.plus(period)); // 2022–02–20
8: System.out.println(dateTime.plus(period)); // 2022–02–20T06:15
9: System.out.println(time.plus(period)); // Exception
```

Line 9 attempts to add a month to an object that has only a time. This won’t work. Java throws an ``UnsupportedTemporalTypeException`` and complains that we attempted to use an ``Unsupported unit: Months``

==**You have to pay attention to the type of date and time objects every place you see them.**==

```java
var annually = Period.ofYears(1); // every 1 year  
var quarterly = Period.ofMonths(3); // every 3 months  
var everyThreeWeeks = Period.ofWeeks(3); // every 3 weeks  
var everyOtherDay = Period.ofDays(2); // every 2 days  
var everyYearAndAWeek = Period.of(1, 0, 7); // every year and 7 days  
  
System.out.println(annually); // P1Y  
System.out.println(quarterly);  // P3M  
System.out.println(everyThreeWeeks); // P21D  
System.out.println(everyOtherDay);  // P2D  
System.out.println(everyYearAndAWeek); // P1Y7D  
  
// There’s one catch. You cannot chain methods when creating a Period.  
var wrong = Period.ofYears(1).ofWeeks(1); // every week  
System.out.println(wrong); // P7D  
  
// This tricky code is really like writing the following:  
// var wrong = Period.ofYears(1);  
// wrong = Period.ofWeeks(1);
```

### Working with Durations

``Period`` is a day or more of time. There is also ``Duration``, which is intended for smaller units of time. For ``Duration``, you can specify the number of days, hours, minutes, seconds, or nanoseconds. And yes, you could pass 365 days to make a year, but you really shouldn’t—that’s what Period is for.

**==``Duration`` works roughly the same way as ``Period``, except it is used with objects that have time.==** ``Duration`` is output beginning with ``PT``, which you can think of as a period of time. A ``Duration`` is stored in hours, minutes, and seconds.

```java
var daily = Duration.ofDays(1); // PT24H
var hourly = Duration.ofHours(1); // PT1H
var everyMinute = Duration.ofMinutes(1); // PT1M
var everyTenSeconds = Duration.ofSeconds(10); // PT10S
var everyMilli = Duration.ofMillis(1); // PT0.001S
var everyNano = Duration.ofNanos(1); // PT0.000000001S
```

**==``Duration`` doesn’t have a factory method that takes multiple units like ``Period`` does==**. If you want something to happen every hour and a half, you specify 90 minutes.

``Duration`` includes another more generic factory method. It takes a number and a ``TemporalUnit``. The idea is, say, something like “5 seconds.” However, ``TemporalUnit`` is an interface. At the moment, there is only one implementation named ``ChronoUnit``.

```java
var daily = Duration.of(1, ChronoUnit.DAYS);
var hourly = Duration.of(1, ChronoUnit.HOURS);
var everyMinute = Duration.of(1, ChronoUnit.MINUTES);
var everyTenSeconds = Duration.of(10, ChronoUnit.SECONDS);
var everyMilli = Duration.of(1, ChronoUnit.MILLIS);
var everyNano = Duration.of(1, ChronoUnit.NANOS);
```

---

**``ChronoUnit`` for Differences**

**``ChronoUnit`` is a great way to determine how far apart two Temporal values are. Temporal includes ``LocalDate``, ``LocalTime``, and so on. ``ChronoUnit`` is in the java. ``time.temporal`` package.**

```java
var one = LocalTime.of(5, 15);
var two = LocalTime.of(6, 30);
var date = LocalDate.of(2016, 1, 20);
System.out.println(ChronoUnit.HOURS.between(one, two)); // 1
System.out.println(ChronoUnit.MINUTES.between(one, two)); // 75
System.out.println(ChronoUnit.MINUTES.between(one, date)); // DateTimeExce
```

**The last reminds us that Java will throw an exception if we mix up what can be done on date vs. time objects.**
**Alternatively, you can truncate any object with a time element.**

```java
LocalTime time = LocalTime.of(3,12,45);
System.out.println(time); // 03:12:45
LocalTime truncated = time.truncatedTo(ChronoUnit.MINUTES);
System.out.println(truncated); // 03:12
```

**This example zeroes out any fields smaller than minutes. In our case, it gets rid of the seconds.**

---

Using a ``Duration`` works the same way as using a Period. 

```java
7: var date = LocalDate.of(2022, 1, 20);
8: var time = LocalTime.of(6, 15);
9: var dateTime = LocalDateTime.of(date, time);
10: var duration = Duration.ofHours(6);
11: System.out.println(dateTime.plus(duration)); // 2022–01–20T12:15
12: System.out.println(time.plus(duration)); // 12:15
13: System.out.println(
14: date.plus(duration)); // UnsupportedTemporalTypeException
```

==**Line 13 fails because we cannot add hours to an object that does not contain a time.**==

```java
7: var date = LocalDate.of(2022, 1, 20);
8: var time = LocalTime.of(6, 15);
9: var dateTime = LocalDateTime.of(date, time);
10: var duration = Duration.ofHours(23);
11: System.out.println(dateTime.plus(duration)); // 2022–01–21T05:15
12: System.out.println(time.plus(duration)); // 05:15
13: System.out.println(
14: date.plus(duration)); // UnsupportedTemporalTypeException
```
### Period vs. Duration

Remember that ``Period`` and ``Duration`` are not equivalent.

```java
var date = LocalDate.of(2022, 5, 25);
var period = Period.ofDays(1);
var days = Duration.ofDays(1);
System.out.println(date.plus(period)); // 2022–05–26
System.out.println(date.plus(days)); // Unsupported unit: Seconds
```

Since we are working with a ``LocalDate``, we are required to use ``Period``. ``Duration`` has time units in it, even if we don’t see them, and they are meant only for objects with time.

|               | Can use with Period? | Can use with Duration? |
|---------------|----------------------|------------------------|
| LocalDate     | Yes                  | No                     |
| LocalDateTime | Yes                  | Yes                    |
| LocalTime     | No                   | Yes                    |
| ZonedDateTime | Yes                  | Yes                    |
### Working with Instants

The ``Instant`` class represents a specific moment in time in the GMT time zone.

```java
var now = Instant.now();
// do something time consuming
var later = Instant.now();
var duration = Duration.between(now, later);
System.out.println(duration.toMillis()); // Returns number milliseconds
```

If you have a ``ZonedDateTime``, you can turn it into an ``Instant``:

```java
var date = LocalDate.of(2022, 5, 25);
var time = LocalTime.of(11, 55, 00);
var zone = ZoneId.of("US/Eastern");
var zonedDateTime = ZonedDateTime.of(date, time, zone);
var instant = zonedDateTime.toInstant(); // 2022–05–25T15:55:00Z
System.out.println(zonedDateTime); // 2022–05–25T11:55–04:00[US/Eastern]
System.out.println(instant); // 202–05–25T15:55:00Z
```

The last two lines represent the same moment in time. The ``ZonedDateTime`` includes a time zone. The ``Instant`` gets rid of the time zone and turns it into an Instant of time in GMT.

```java
public static void main(String[] args) throws InterruptedException {  
  
    var date = LocalDate.of(2022, 5, 25);  
    var time = LocalTime.of(11, 55, 00);  
    var zone = ZoneId.of("US/Eastern");  
    var zonedDateTime = ZonedDateTime.of(date, time, zone);  
    var instant = zonedDateTime.toInstant(); // 2022–05–25T15:55:00Z  
    System.out.println("zonedDateTime : " + zonedDateTime); // 2022–05–25T11:55–04:00[US/Eastern]  
    System.out.println("instant : " + instant); // 202–05–25T15:55:00Z  
  
  
    ZonedDateTime istanbulZonedDateTime = ZonedDateTime.of(LocalDate.now(), LocalTime.now(), ZoneId.of("Europe/Istanbul"));  
  
    System.out.println("istanbulZonedDateTime : " + istanbulZonedDateTime);  
    System.out.println("instant : " + istanbulZonedDateTime.toInstant());  
    System.out.println("truncatedTo : " + (instant.truncatedTo(ChronoUnit.HOURS)));  
  
    Instant parsed = Instant.parse("2000-06-01T10:15:20.00Z");  
    System.out.println("parsed: " + parsed);  
}
```

### Accounting for Daylight Saving Time

Some countries observe daylight saving time. This is where the clocks are adjusted by an hour twice a year to make better use of the sunlight. You only have to work with U.S. daylight saving time on the exam, and that’s what we describe here.

The question will let you know if a date/time mentioned falls on a weekend when the clocks are scheduled to be changed. If it is not mentioned in a question, you can assume that it is a normal weekend. The act of moving the clock forward or back occurs at 2:00 a.m., which falls very early Sunday morning.

For example, on March 13, 2022, we move our clocks forward an hour and jump from 2:00 a.m. to 3:00 a.m. This means that there is no 2:30 a.m. that day. If we wanted to know the time an hour later than 1:30, it would be 3:30.

```java
var date = LocalDate.of(2022, Month.MARCH, 13);
var time = LocalTime.of(1, 30);
var zone = ZoneId.of("US/Eastern");
var dateTime = ZonedDateTime.of(date, time, zone);
System.out.println(dateTime); // 2022–03-13T01:30-05: 00[US/Eastern]
System.out.println(dateTime.getHour()); // 1
System.out.println(dateTime.getOffset()); // -05:00
dateTime = dateTime.plusHours(1);
System.out.println(dateTime); // 2022–03-13T03:30-04:00[US/Eastern]
System.out.println(dateTime.getHour()); // 3
System.out.println(dateTime.getOffset()); // -04:00
```

Notice that two things change in this example. The time jumps from 1:30 to 3:30. The UTC offset also changes. Remember when we calculated GMT time by subtracting the time zone from the time? You can see that we went from 6:30 GMT (1:30 minus –5:00) to 7:30 GMT (3:30 minus –4:00). This shows that the time really did change by one hour from GMT’s point of view.

```java
var date = LocalDate.of(2022, Month.NOVEMBER, 6);
var time = LocalTime.of(1, 30);
var zone = ZoneId.of("US/Eastern");
var dateTime = ZonedDateTime.of(date, time, zone);
System.out.println(dateTime); // 2022-11-06T01:30-04:00[US/Eastern]
dateTime = dateTime.plusHours(1);
System.out.println(dateTime); // 2022-11-06T01:30-05:00[US/Eastern]
dateTime = dateTime.plusHours(1);
System.out.println(dateTime); // 2022-11-06T02:30-05:00[US/Eastern]
```

went from 5:30 GMT to 6:30 GMT, to 7:30 GMT. Finally, trying to create a time that doesn’t exist just rolls forward:

```java
var date = LocalDate.of(2022, Month.MARCH, 13);
var time = LocalTime.of(2, 30);
var zone = ZoneId.of("US/Eastern");
var dateTime = ZonedDateTime.of(date, time, zone);
System.out.println(dateTime); // 2022–03–13T03:30–04:00[US/Eastern]
```

Java is smart enough to know that there is no 2:30 a.m. that night and switches over to the appropriate GMT offset.

```java
public static void main(String[] args) {  
  
    /*  
    Similarly, in November, an hour after the initial 1:30 a.m. is also 1:30 a.m. because at 2:00 a.m.    we repeat the hour. This time, try to calculate the GMT time yourself for all three times to confirm that    we really do move only one hour at a time.     */  
    var date = LocalDate.of(2022, Month.NOVEMBER, 6);  
    var time = LocalTime.of(1, 30);  
    var zone = ZoneId.of("US/Eastern");  
    var dateTime = ZonedDateTime.of(date, time, zone);  
    System.out.println(dateTime); // 2022-11-06T01:30-04:00[US/Eastern]  
  
    dateTime = dateTime.plusHours(1);  
    System.out.println(dateTime); // 2022-11-06T01:30-05:00[US/Eastern]  
    dateTime = dateTime.plusHours(1);  
    System.out.println(dateTime); // 2022-11-06T02:30-05:00[US/Eastern]  
}
```

```java
public class DayLightSpringExample {  
  
    public static void main(String[] args) {  
  
        /*  
        For example, on March 13, 2022, we move our clocks forward an hour and jump from 2:00 a.m. to 3:00 a.m.        This means that there is no 2:30 a.m. that day.         If we wanted to know the time an hour later than 1:30, it would be 3:30.         */  
        System.out.println("---------- US/Eastern 2022 ----------");  
  
        var date1 = LocalDate.of(2022, Month.MARCH, 10);  
        var date2 = LocalDate.of(2022, Month.MARCH, 13);  
        var date3 = LocalDate.of(2022, Month.MARCH, 20);  
  
        printDaylightSavingTime(date1, ZoneId.of("US/Eastern"));  
        printDaylightSavingTime(date2, ZoneId.of("US/Eastern"));  
        printDaylightSavingTime(date3, ZoneId.of("US/Eastern"));  
  
        // Notice that two things change in this example. The time jumps from 1:30 to 3:30. The UTC offset also changes.  
  
        System.out.println("---------- US/Eastern 2023 ----------");  
  
        var date4 = LocalDate.of(2023, Month.MARCH, 10);  
        var date5 = LocalDate.of(2023, Month.MARCH, 12);  
        var date6 = LocalDate.of(2023, Month.MARCH, 20);  
  
        printDaylightSavingTime(date4, ZoneId.of("US/Eastern"));  
        printDaylightSavingTime(date5, ZoneId.of("US/Eastern"));  
        printDaylightSavingTime(date6, ZoneId.of("US/Eastern"));  
  
        System.out.println("---------- Europe/Berlin 2023 ----------");  
  
        var date7 = LocalDate.of(2023, Month.MARCH, 12);  
        var date8 = LocalDate.of(2023, Month.MARCH, 26);  
        var date9 = LocalDate.of(2023, Month.MARCH, 28);  
  
        printDaylightSavingTime(date7, ZoneId.of("Europe/Berlin"));  
        printDaylightSavingTime(date8, ZoneId.of("Europe/Berlin"));  
        printDaylightSavingTime(date9, ZoneId.of("Europe/Berlin"));  
  
        System.out.println("---------- Europe/London 2023 ----------");  
  
        var date10 = LocalDate.of(2023, Month.MARCH, 12);  
        var date11 = LocalDate.of(2023, Month.MARCH, 26);  
        var date12 = LocalDate.of(2023, Month.MARCH, 28);  
  
        // UK change time 1.00AM  
        // US and Europe/Berlin 2.00AM        printDaylightSavingTimeForUK(date10, ZoneId.of("Europe/London"));  
        printDaylightSavingTimeForUK(date11, ZoneId.of("Europe/London"));  
        printDaylightSavingTimeForUK(date12, ZoneId.of("Europe/London"));  
  
    }  
  
    private static void printDaylightSavingTime(LocalDate date, ZoneId zone) {  
  
        System.out.println("##############");  
  
        var time = LocalTime.of(1, 30);  
        var dateTime = ZonedDateTime.of(date, time, zone);  
        System.out.println("dateTime : " + dateTime);  
        System.out.println("hour : " + dateTime.getHour() + " , offset : " + dateTime.getOffset());  
  
        dateTime = dateTime.plusHours(1);  
        System.out.println("dateTime : " + dateTime);  
        System.out.println("hour : " + dateTime.getHour() + " , offset : " + dateTime.getOffset());  
    }  
  
    private static void printDaylightSavingTimeForUK(LocalDate date, ZoneId zone) {  
  
        System.out.println("##############");  
  
        var time = LocalTime.of(00, 30);  
        var dateTime = ZonedDateTime.of(date, time, zone);  
        System.out.println("dateTime : " + dateTime);  
        System.out.println("hour : " + dateTime.getHour() + " , offset : " + dateTime.getOffset());  
  
        dateTime = dateTime.plusHours(1);  
        System.out.println("dateTime : " + dateTime);  
        System.out.println("hour : " + dateTime.getHour() + " , offset : " + dateTime.getOffset());  
    }  
}
```
## Summary #OCP_Summary 

- ==**a ``String`` is an immutable sequence of characters. Calling the constructor explicitly is optional. The concatenation operator ``(+)`` creates a new ``String`` with the content of the first ``String`` followed by the content of the second ``String``. If either operand involved in the + expression is a ``String``, concatenation is used; otherwise, addition is used. String literals are stored in the string pool. The ``String`` class has many methods. By contrast, a ``StringBuilder`` is a mutable sequence of characters. Most of the methods return a reference to the current object to allow method chaining. The ``StringBuilder`` class has many methods.**==

- ==**Calling ``==`` on ``String`` objects will check whether they point to the same object in the pool. Calling ``==`` on ``StringBuilder`` references will check whether they are pointing to the same ``StringBuilder`` object. Calling ``equals()`` on ``String`` objects will check whether the sequence of characters is the same. Calling ``equals()`` on ``StringBuilder`` objects will check whether they are pointing to the same object rather than looking at the values inside.**==

- ==**An array is a fixed-size area of memory on the heap that has space for primitives or pointers to objects. You specify the size when creating it. For example, int[] a = new int[6];. Indexes begin with 0, and elements are referred to using a [0]. The ``Arrays.sort()`` method sorts an array. ``Arrays.binarySearch()`` searches a sorted array and returns the index of a match. If no match is found, it negates the position where the element would need to be inserted and subtracts 1. ``Arrays.compare()`` and ``Arrays.mismatch()`` check whether two arrays are equivalent. Methods that are passed ``varargs (...)`` can be used as if a normal array was passed in. In a multidimensional array, the second-level arrays and beyond can be different sizes.**==

- ==**The Math class provides a number of static methods for performing mathematical operations. For example, you can get minimums or maximums. You can round or even generate random numbers. Some methods work on any numeric primitive, and others only work on double.**==

- ==**A ``LocalDate`` contains just a date, a ``LocalTime`` contains just a time, and a ``LocalDateTime`` contains both a date and a time. All three have private constructors and are created using ``LocalDate.now()`` or ``LocalDate.of()`` (or the equivalents for that class). Dates and times can be manipulated using plusXXX or minusXXX methods. The ``Period`` class represents a number of days, months, or years to add to or subtract from a ``LocalDate`` or ``LocalDateTime``. The date and time classes are all immutable, which means the return value must be used.**==


## Exam Essentials #Essential

- **Be able to determine the output of code using String**. : Know the rules for concatenating with String and how to use common String methods. Know that a String is immutable. Pay special attention to the fact that indexes are zero-based and that the ``substring()`` method gets the string up until right before the index of the second parameter.

- **Be able to determine the output of code using StringBuilder.**: Know that a StringBuilder is mutable and how to use common StringBuilder methods. Know that ``substring()`` does not change the value of a StringBuilder, whereas ``append(), delete(), and insert()`` do change it. Also note that most StringBuilder methods return a reference to the current instance of StringBuilder.

- **Understand the difference between == and equals().**: ``==`` checks object equality. ``equals()`` depends on the implementation of the object it is being called on. For the String class, ``equals()`` checks the characters inside of it.

- **Be able to determine the output of code using arrays.**: Know how to declare and instantiate one-dimensional and multidimensional arrays. Be able to access each element and know when an index is out of bounds. Recognize correct and incorrect output when searching and sorting.

- **Identify the return types of Math methods**. Depending on the primitive passed in, the Math methods may return different primitive results.

- **Recognize invalid uses of dates and times.**: ``LocalDate`` does not contain time fields, and ``LocalTime`` does not contain date fields. Watch for operations being performed on the wrong time. Also watch for adding or subtracting time and ignoring the result. Be comfortable with date math, including time zones and daylight saving time.

## Review Questions

1. What is output by the following code? (Choose all that apply.)

```java
1: public class Fish {
2: public static void main(String[] args) {
3: int numFish = 4;
4: String fishType = "tuna";
5: String anotherFish = numFish + 1;
6: System.out.println(anotherFish + " " + fishType);
7: System.out.println(numFish + " " + 1);
8: } }
```

A. 4 1
B. 5
C. 5 tuna
D. 5tuna
E. 51tuna
F. The code does not compile.

**My Answer: F
Correct Answer: F**

**``numFish`` is an int, and 1 is an int. Therefore, we use numeric addition and get 5. The problem is that we can’t store an int in a String variable.**

---

2. Which of these array declarations are not legal? (Choose all that apply.)

A. ``int[][] scores = new int[5][];``
B. ``Object[][][] cubbies = new Object[3][0][5];``
C. ``String beans[] = new beans[6];``
D. ``java.util.Date[] dates[] = new java.util.Date[2][];``
E. ``int[][] types = new int[];``
F. ``int[][] java = new int[][];``

**My Answer: C,E,F**
**Correct Answer: C,E,F**

**Option C uses the variable name as if it were a type, which is clearly illegal. Options E and F don’t specify any size. Although it is legal to leave out the size for later dimensions of a multidimensional array, the first one is required**

---

3. Note that March 13, 2022 is the weekend when we spring forward, and November 6, 2022 is when we fall back for daylight saving time. Which of the following can fill in the blank without the code throwing an exception? (Choose all that apply.)

```java
var zone = ZoneId.of("US/Eastern");
var date = ;
var time = LocalTime.of(2, 15);
var z = ZonedDateTime.of(date, time, zone);
```

`A. LocalDate.of(2022, 3, 13)`
`B. LocalDate.of(2022, 3, 40)`
`C. LocalDate.of(2022, 11, 6)`
`D. LocalDate.of(2022, 11, 7)`
`E. LocalDate.of(2023, 2, 29)`
`F. LocalDate.of(2022, MonthEnum.MARCH, 13);`

**My Answer: A,C,F**
**Correct Answer: A,C,D**

**Option B throws an exception because there is no March 40.** 
**Option E also throws an exception because 2023 isn’t a leap year and therefore has no February 29.** 
**Option F doesn’t compile because the enum should be named Month, rather than MonthEnum.**

---

4. Which of the following are output by this code? (Choose all that apply.)

```java
3: var s = "Hello";
4: var t = new String(s);
5: if ("Hello".equals(s)) System.out.println("one");
6: if (t == s) System.out.println("two");
7: if (t.intern() == s) System.out.println("three");
8: if ("Hello" == s) System.out.println("four");
9: if ("Hello".intern() == t) System.out.println("five");
```

A. one
B. two
C. three
D. four
E. five
F. The code does not compile.
G. None of the above

**My Answer: A,C,D**
**Correct Answer: A,C,D**


---

5. What is the result of the following code?

```java
7: var sb = new StringBuilder();
8: sb.append("aaa").insert(1, "bb").insert(4, "ccc");
9: System.out.println(sb);
```

A. abbaaccc
B. abbaccca
C. bbaaaccc
D. bbaaccca
E. An empty line
F. The code does not compile.

**My Answer: B**
**Correct Answer: B**

**After the call to ``append()``, sb contains "aaa". That result is passed to the first ``insert()`` call, which inserts at index 1. At this point, sb contains abbaa. That result is passed to the final insert(), which inserts at index 4, resulting in abbaccca.**

---

6. How many of these lines contain a compiler error? (Choose all that apply.)

```java
23: double one = Math.pow(1, 2);
24: int two = Math.round(1.0);
25: float three = Math.random();
26: var doubles = new double[] {one, two, three};
```

A. 0
B. 1
C. 2
D. 3
E. 4

**My Answer: B**
**Correct Answer: C**

**Remember to watch return types on math operations. ==One of the tricks is line 24. The ``round()`` method returns an int when called with a float. However, we are calling it with a double, so it returns a long. The other trick is line 25. The ``random()`` method returns a double.**==

---

7.  Which of these statements is true of the two values? (Choose all that apply.)
	2022–08–28T05:00 GMT-04:00
	2022–08–28T09:00 GMT-06:00
A. The first date/time is earlier.
B. The second date/time is earlier.
C. Both date/times are the same.
D. The date/times are two hours apart.
E. The date/times are six hours apart.
F. The date/times are 10 hours apart.

**My Answer: A,E**
**Correct Answer: A,E**

**When dealing with time zones, it is best to convert to GMT first by subtracting the time zone. Remember that subtracting a negative is like adding. The first date/time is 9:00 GMT, and the second is 15:00 GMT. Therefore, the first one is earlier by six hours.**

---

8. Which of the following return 5 when run independently? (Choose all that apply.)
```java
var string = "12345";
var builder = new StringBuilder("12345");
```

`A. builder.charAt(4)`
`B. builder.replace(2, 4, "6").charAt(3)`
`C. builder.replace(2, 5, "6").charAt(2)`
`D. string.charAt(5)`
`E. string.length`
`F. string.replace("123", "1").charAt(2)`
G. None of the above

**My Answer: A,D,E**
**Correct Answer: A,B,F**

**Remember that indexes are zero-based, which means index 4 corresponds to 5, and option A is correct.**
**For option B, the replace() method starts the replacement at index 2 and ends before index 4. This means two characters are replaced, and ``charAt(3)`` is called on the intermediate value of 1265. The character at index 3 is 5, making option B correct. Option C is similar, making the intermediate value 126 and returning 6.**

---

9. Which of the following are true about arrays? (Choose all that apply.)
A. The first element is index 0.
B. The first element is index 1.
C. Arrays are fixed size.
D. Arrays are immutable.
E. Calling ``equals()`` on two different arrays containing the same primitive values always
returns true.
F. Calling ``equals()`` on two different arrays containing the same primitive values always
returns false.
G. Calling ``equals()`` on two different arrays containing the same primitive values can return
true or false.

**My Answer: A,C,G**
**Correct Answer: A,C,F**

**An array does not override equals(), so it uses object equality. Since two different objects are not equal, option F is correct, and options E and G are incorrect.**

---

10. How many of these lines contain a compiler error? (Choose all that apply.)
```JAVA
23: int one = Math.min(5, 3);
24: long two = Math.round(5.5);
25: double three = Math.floor(6.6);
26: var doubles = new double[] {one, two, three};
```

A. 0
B. 1
C. 2
D. 3
E. 4

**My Answer: B**
**Correct Answer: A**

**All of these lines compile. The ``min()`` and ``floor()`` methods return the same type passed in: int and double, respectively. The ``round()`` method returns a long when called with a double. Option A is correct since the code compiles.**

---

11. What is the output of the following code?

```java
var date = LocalDate.of(2022, 4, 3);
date.plusDays(2);
date.plusHours(3);
System.out.println(date.getYear() + " " + date.getMonth()
+ " " + date.getDayOfMonth());
```

A. 2022 MARCH 4
B. 2022 MARCH 6
C. 2022 APRIL 3
D. 2022 APRIL 5
E. The code does not compile.
F. A runtime exception is thrown.

**My Answer: E**
**Correct Answer: E**

**A ``LocalDate`` does not have a time element. Therefore, there is no method to add hours**

---

12. What is output by the following code? (Choose all that apply.)
```java
var numbers = "012345678".indent(1);
numbers = numbers.stripLeading();
System.out.println(numbers.substring(1, 3));
System.out.println(numbers.substring(7, 7));
System.out.print(numbers.substring(7));
```

A. 12
B. 123
C. 7
D. 78
E. A blank line
F. The code does not compile.
G. An exception is thrown.

**My Answer: A**
**Correct Answer: A,D,E**

**First, notice that the ``indent()`` call adds a blank space to the beginning of numbers, and ``stripLeading()`` immediately removes it. Therefore, these methods cancel each other out and have no effect. The ``substring()`` method has two forms. The first takes the index to start with and the index to stop immediately before. The second takes just the index to start with and goes to the end of the String.**


---

13. What is the result of the following code?

```java
public class Lion {
public void roar(String roar1, StringBuilder roar2) {
roar1.concat("!!!");
roar2.append("!!!");
}
public static void main(String[] args) {
var roar1 = "roar";
var roar2 = new StringBuilder("roar");
new Lion().roar(roar1, roar2);
System.out.println(roar1 + " " + roar2);
} }
```

A. roar roar
B. roar roar!!!
C. roar!!! roar
D. roar!!! roar!!!
E. An exception is thrown.
F. The code does not compile.

**My Answer: B**
**Correct Answer: B**

**A String is immutable. Calling ``concat()`` returns a new String but does not change the original. A StringBuilder is mutable. Calling ``append()`` adds characters to the existing character sequence along with returning a reference to the same object**

---

14. Given the following, which can correctly fill in the blank? (Choose all that apply.)
```java
var date = LocalDate.now();
var time = LocalTime.now();
var dateTime = LocalDateTime.now();
var zoneId = ZoneId.systemDefault();
var zonedDateTime = ZonedDateTime.of(dateTime, zoneId);
Instant instant = ;
```

`A. Instant.now()`
`B. new Instant()`
`C. date.toInstant()`
`D. dateTime.toInstant()`
`E. time.toInstant()`
`F. zonedDateTime.toInstant()`

**My Answer: A,C,F**
**Correct Answer: A,F**

**Options C, D, and E are incorrect because the source object does not represent a point in time. Without a time zone, Java doesn’t know what moment in time to use for the Instant.**

---

15. What is the output of the following? (Choose all that apply.)

```java
var arr = new String[] { "PIG", "pig", "123"};
Arrays.sort(arr);
System.out.println(Arrays.toString(arr));
System.out.println(Arrays.binarySearch(arr, "Pippa"));
```

A. [pig, PIG, 123]
B. [PIG, pig, 123]
C. [123, PIG, pig]
D. [123, pig, PIG]
E. -3
F. -2
G. The results of ``binarySearch()`` are undefined in this example.

**My Answer: C,F**
**Correct Answer: C,E**

**The ``binarySearch()`` method looks at where a value would be inserted, which is before the second element for Pippa.**

---

16. What is included in the output of the following code? (Choose all that apply.)

```JAVA
var base = "ewe\nsheep\\t";
int length = base.length();
int indent = base.indent(2).length();
int translate = base.translateEscapes().length();

var formatted = "%s %s %s".formatted(length, indent, translate);
System.out.format(formatted);
```

A. 10
B. 11
C. 12
D. 13
E. 14
F. 15
G. 16

**My Answer: B,D**
**Correct Answer: A,B,G**

**There are 11 characters in base because there are two escape characters. The \n counts as one character representing a new line, and the \\ counts as one character representing a backslash. This makes option B one of the answers. The ``indent()`` method adds two characters to the beginning of each of the two lines of base. This gives us four additional characters. However, the method also normalizes by adding a new line to the end if**
**it is missing. The extra character means we add five characters to the existing 11, which is option G. Finally, the ``translateEscapes()`` method turns any text escape characters into actual escape characters, making \\t into \t. This gets rid of one character, leaving us with 10 characters matching option A.**

---

17. Which of these statements are true? (Choose all that apply.)

```JAVA
var letters = new StringBuilder("abcdefg");
```

A. ``letters.substring(1, 2)`` returns a single-character String.
B. ``letters.substring(2, 2)`` returns a single-character String.
C. ``letters.substring(6, 5)`` returns a single-character String.
D. ``letters.substring(6, 6)`` returns a single-character String.
E. ``letters.substring(1, 2)`` throws an exception.
F. ``letters.substring(2, 2)`` throws an exception.
G. ``letters.substring(6, 5)`` throws an exception.
H. ``letters.substring(6, 6)`` throws an exception.

**My Answer: A,G**
**Correct Answer: A,G**

---

18. What is the result of the following code? (Choose all that apply.)

```JAVA
13: String s1 = """
14: purr""";
15: String s2 = "";
16:
17: s1.toUpperCase();
18: s1.trim();
19: s1.substring(1, 3);
20: s1 += "two";
21:
22: s2 += 2;
23: s2 += 'c';
24: s2 += false;
25:
26: if ( s2 == "2cfalse") System.out.println("==");
27: if ( s2.equals("2cfalse")) System.out.println("equals");
28: System.out.println(s1.length());
```

A. 2
B. 4
C. 7
D. 10
E. ==
F. equals
G. An exception is thrown.
H. The code does not compile.

**My Answer: C,F**
**Correct Answer: C,F**

the text block on lines 13 and 14 is equivalent to a regular String. Since there is no line break at
the end, this is four characters. Then, you have to know that String objects are immutable, which means the results of lines 17–19 are ignored. Finally, on line 20, something happens. We concatenate three new characters to s1 and now have a String of length 7, making option C correct. The if statement on line 26 returns false because the two String objects are not the same in memory. One comes directly from the string pool, and the other comes from building using String operations.

---

19. Which of the following fill in the blank to print a positive integer? (Choose all that apply.)

```java
String[] s1 = { "Camel", "Peacock", "Llama"};
String[] s2 = { "Camel", "Llama", "Peacock"};
String[] s3 = { "Camel"};
String[] s4 = { "Camel", null};
System.out.println(Arrays. );
```

`A. compare(s1, s2)`
`B. mismatch(s1, s2)`
`C. compare(s3, s4)`
`D. mismatch (s3, s4)`
`E. compare(s4, s4)`
`F. mismatch (s4, s4)`

**My Answer: A,B,D**
**Correct Answer: A,B,D**

---

20. Note that March 13, 2022 is the weekend that clocks spring ahead for daylight saving time.
What is the output of the following? (Choose all that apply.)

```java
var date = LocalDate.of(2022, Month.MARCH, 13);
var time = LocalTime.of(1, 30);
var zone = ZoneId.of("US/Eastern");
var dateTime1 = ZonedDateTime.of(date, time, zone);
var dateTime2 = dateTime1.plus(1, ChronoUnit.HOURS);
long diff = ChronoUnit.HOURS.between(dateTime1, dateTime2);
int hour = dateTime2.getHour();
boolean offset = dateTime1.getOffset() == dateTime2.getOffset();
System.out.println("diff = " + diff);
System.out.println("hour = " + hour);
System.out.println("offset = " + offset);
```

A. diff = 1
B. diff = 2
C. hour = 2
D. hour = 3
E. offset = true
F. The code does not compile.
G. A runtime exception is thrown.

**My Answer: E**
**Correct Answer: A,D**

The dateTime1 object has a time of 1:30 per initialization. The dateTime2 object is an hour later. However, there is no 2:30 when springing ahead, setting the time to 3:30. Option A is correct because it is an hour later. Option D is also correct because the hour of the new time is 3. Option E is not correct because we have changed the time zone offset due to daylight saving time.

---

21. Which of the following can fill in the blank to print avaJ? (Choose all that apply.)

```JAVA
3: var puzzle = new StringBuilder("Java");
4: puzzle. ;
5: System.out.println(puzzle);
```

`A. reverse()`
`B. append("vaJ$").substring(0, 4)`
`C. append("vaJ$").delete(0, 3).deleteCharAt(puzzle.length() -1)`
`D. append("vaJ$").delete(0, 3).deleteCharAt(puzzle.length())`
E. None of the above

**My Answer: A,C**
**Correct Answer: A,C**

---

22. What is the output of the following code?

```java
var date = LocalDate.of(2022, Month.APRIL, 30);
date.plusDays(2);
date.plusYears(3);
System.out.println(date.getYear() + " " + date.getMonth() + " " + date.getDayOfMonth());
```

A. 2022 APRIL 30
B. 2022 MAY 2
C. 2025 APRIL 2
D. 2025 APRIL 30
E. 2025 MAY 2
F. The code does not compile.
G. A runtime exception is thrown.

**My Answer: A**
**Correct Answer: A**

**A. The date starts out as April 30, 2022. Since dates are immutable and the plus methods’ return values are ignored, the result is unchanged**

---


# Chapter 5 - Methods #Chapter

## Designing Methods

![[Pasted image 20240315184800.png]]

This is called a ***method declaration***, which specifies all the information needed to call the method.
**==Two of the parts—the method name and parameter list—are called the method signature==**. The method signature provides instructions for how callers can reference this method. The method signature does not include

|Element|Value|Required?|
|---|---|---|
|Access modifier|public|No|
|Optional specifier|final|No|
|Return type|void|Yes|
|Method name|nap|Yes|
|Parameter list|(int minutes)|Yes, but can be empty|
|Parentheses|Yes|Yes|
|Method signature|nap(int minutes)|Yes|
|Exception list|throws InterruptedException|No|
|Method body|{<br>// take a nap<br>}|Yes, except for abstract methods|
```java
nap(10);
```

### Access Modifiers

An access modifier determines what classes a method can be accessed from. Think of it like a security guard. Java offers four choices of access modifier:

- ==**private** The ``private`` modifier means the method can be called only from within the same class.==

- ==**Package Access** With package access, the method can be called only from a class in the same package.==

- ==**protected** The ``protected`` modifier means the method can be called only from a class in the same package or a subclass.==

- ==**public** The ``public`` modifier means the method can be called from anywhere.==

The exam creators like to trick you by putting method elements in the wrong order or using incorrect values.

```java
public class ParkTrip {
	public void skip1() {}
	default void skip2() {} // DOES NOT COMPILE
	void public skip3() {} // DOES NOT COMPILE
	void skip4() {}
}
```

### Optional Specifiers

Unlike with access modifiers, you can have multiple specifiers in the same method. When this happens, you can specify them in any order. And since these specifiers are optional, you are allowed to not have any of them at all. This means you can have zero or more specifiers in a method declaration.

|Modifier|Description|Chapter covered|
|---|---|---|
|static|Indicates the method is a member of the shared class object|Chapter 5|
|abstract|Used in an abstract class or interface when the method body is excluded|Chapter 6|
|final|Specifies that the method may not be overridden in a subclass|Chapter 6|
|default|Used in an interface to provide a default implementation of a method for classes that implement the interface|Chapter 7|
|synchronized|Used with multithreaded code|Chapter 13|
|native|Used when interacting with code written in another language, such as C++|Out of scope|
|strictfp|Used for making floating-point calculations portable|Out of scope|

While access modifiers and optional specifiers can appear in any order, **==they must all appear before the return type.==**

---

**==Access modifiers and optional specifiers can be listed in any order, but once the return type is specified, the rest of the parts of the method are written in a specific order: name, parameter list, exception list, body.==** #TIP 

---

```JAVA
public class Exercise {
	public void bike1() {}
	public final void bike2() {}
	public static final void bike3() {}
	public final static void bike4() {}
	public modifier void bike5() {} // DOES NOT COMPILE
	public void final bike6() {} // DOES NOT COMPILE
	final public void bike7() {}
}
```

- The ``bike5()`` method doesn’t compile because modifier is not a valid optional specifier.
- The ``bike6()`` method doesn’t compile because the optional specifier is after the return type.
- The ``bike7()`` method does compile. Java allows the optional specifiers to appear before the access modifier.
### Return Type

The next item in a method declaration is the return type. It must appear after any access modifiers or optional specifiers and before the method name. The return type might be an actual Java type such as ``String`` or int. If there is no return type, the ``void`` keyword is used.

---

**a method must have a return type. If no value is returned, the ``void`` keyword must be used. You cannot omit the return type.**

---

When checking return types, you also have to look inside the method body. Methods with a return type other than ``void`` are required to have a return statement inside the method body. This return statement must include the primitive or object to be returned.

```java
public void swim(int distance) {
	if(distance <= 0) {
	// Exit early, nothing to do!
	return;
}
	System.out.print("Fish is swimming " + distance + " meters");
}
```

```java
public class Hike {
	public void hike1() {}
	public void hike2() { return; }
	public String hike3() { return ""; }
	public String hike4() {} // DOES NOT COMPILE
	public hike5() {} // DOES NOT COMPILE
	public String int hike6() { } // DOES NOT COMPILE
	String hike7(int a) { // DOES NOT COMPILE
		if (1 < 2) return "orange";
	}
}
```

- The ``hike4()`` method doesn’t compile because the return statement is missing
- The ``hike5()`` method doesn’t compile because the return type is missing.
- The ``hike6()`` method doesn’t compile because it attempts to use two return types.
- The ``hike7()`` method is a little tricky. There is a return statement, but it doesn’t always get run.

```java
String hike8(int a) {
	if (1 < 2) return "orange";
		return "apple"; // COMPILER WARNING
}
```

The code compiles, although the compiler will produce a warning about *unreachable code (or dead code)*. This means the compiler was smart enough to realize you wrote code that cannot possibly be reached. 

**==When returning a value, it needs to be assignable to the return type.==**

```java
public class Measurement {
	int getHeight1() {
		int temp = 9;
		return temp;
	}
	int getHeight2() {
		int temp = 9L; // DOES NOT COMPILE
		return temp;
	}
	int getHeight3() {
		long temp = 9L;
		return temp; // DOES NOT COMPILE
	}
}
```

- The ``getHeight2()`` method doesn’t compile because you can’t assign a long to an int.
- The method ``getHeight3()`` method doesn’t compile because you can’t return a long value as an int.
### Method Name

an identifier may only contain letters, numbers, currency symbols, or _ . Also, the first character is not allowed to be a number, and reserved words are not allowed. Finally, the single underscore character is not allowed.

```java
public class BeachTrip {
	public void jog1() {}
	public void 2jog() {} // DOES NOT COMPILE
	public jog3 void() {} // DOES NOT COMPILE
	public void Jog_$() {}
	public _() {} // DOES NOT COMPILE
	public void() {} // DOES NOT COMPILE
}
```

- The ``2jog()`` method doesn’t compile because identifiers are not allowed to begin with numbers.
- The ``jog3()`` method doesn’t compile because the method name is before the return type.
- The ``_`` method is not allowed since it consists of a single underscore
- The final line of code doesn’t compile because the method name is missing.
### Parameter List

Although the parameter list is required, it doesn’t have to contain any parameters. This means you can just have an empty pair of parentheses after the method name

```java
public class Sleep {
	void nap() {}
}
```

```java
public class PhysicalEducation {
	public void run1() {}
	public void run2 {} // DOES NOT COMPILE
	public void run3(int a) {}
	public void run4(int a; int b) {} // DOES NOT COMPILE
	public void run5(int a, int b) {}
}
```

- The ``run2()`` method doesn’t compile because it is missing the parentheses around the parameter list.
-  The ``run4()`` method doesn’t compile because the parameters are separated by a semicolon rather than a comma.
### Method Signature

**==A method signature, composed of the method name and parameter list==** . It’s important to note that the names of the parameters in the method signature are not used as part of a method signature. It’s important to note that the names of the parameters in the method signature are not used as part of a method signature. **==The parameter list is about the types of parameters and their order==.**

```java
public class Trip {
	public void visitZoo(String name, int waitTime) {}
	public void visitZoo(String attraction, int rainFall) {} // DOES NOT COMPILE
}
```

Despite having different parameter names, these two methods have the same signature and cannot be declared within the same class. Changing the order of parameter types does allow the method to compile

```java
public class Trip {
	public void visitZoo(String name, int waitTime) {}
	public void visitZoo(int rainFall, String attraction) {}
}
```

### Exception List

In Java, code can indicate that something went wrong by throwing an exception. it is optional and where in the method declaration it goes if present.

```java
public class ZooMonorail {
	public void zeroExceptions() {}
	public void oneException() throws IllegalArgumentException {}
	public void twoExceptions() throws IllegalArgumentException, InterruptedException {}
}
```

### Method Body

A method body is simply a code block. It has braces that contain zero or more Java statements.

```JAVA
public class Bird {
	public void fly1() {}
	public void fly2() // DOES NOT COMPILE
	public void fly3(int a) { int name = 5; }
}
```

- The ``fly2()`` method doesn’t compile because it is missing the braces around the empty method body.
**==Methods are required to have a body unless they are declared ``abstract``.==**
## Declaring Local and Instance Variables

local variables are those defined with a method or block, while instance variables are those that are defined as a member of a class.

```java
public class Lion {
	int hunger = 4;
	public int feedZooAnimals() {
		int snack = 10; // Local variable
		if(snack > 4) {
			long dinnerTime = snack++;
			hunger--;
		}
		return snack;
	}
}
```

In the ``Lion`` class, ``snack`` and ``dinnertime`` are local variables only accessible within their respective code blocks, while ``hunger`` is an instance variable and created in every object of the Lion class.
all local variable references are destroyed after the block is executed, but the objects they point to may still be accessible.

### Local Variable Modifiers

**==There’s only one modifier that can be applied to a local variable: ``final``==**.

```java
public void zooAnimalCheckup(boolean isWeekend) {
	final int rest;
	if(isWeekend) rest = 5; else rest = 20;
	System.out.print(rest);
	final var giraffe = new Animal();
	final int[] friends = new int[5];
	rest = 10; // DOES NOT COMPILE
	giraffe = new Animal(); // DOES NOT COMPILE
	friends = null; // DOES NOT COMPILE
}
```

when a ``final`` variable is declared. The rule is only that it must be assigned a value before it can be used.

```java
public void zooAnimalCheckup(boolean isWeekend) {
	final int rest;
	if(isWeekend) rest = 5;
		System.out.print(rest); // DOES NOT COMPILE
}
```

Since the compiler does not allow the use of local variables that may not have been assigned a value, the code does not compile. The ``final`` attribute only refers to the variable reference; the contents can be freely modified (assuming the object isn’t immutable).

```java
public void zooAnimalCheckup() {
	final int rest = 5;
	final Animal giraffe = new Animal();
	final int[] friends = new int[5];
	giraffe.setName("George");
	friends[2] = 2;
}
```

The ``rest`` variable is a primitive, so it’s just a value that can’t be modified. On the other hand, the contents of the ``giraffe`` and ``friends`` variables can be freely modified, provided the variables aren’t reassigned. 

---

**marking a local variable ``final`` is often a good practice. For example, you may have a complex method in which a variable is referenced dozens of times. It would be really bad if someone came in and reassigned the variable in the middle of the method. Using the ``final`` attribute is like sending a message to other developers to leave the variable alone!**

---

### Effectively Final Variables

An *effectively final* local variable is one that is not modified after it is assigned. This means that the value of a variable doesn’t change after it is set, regardless of whether it is explicitly marked as ``final``. If you aren’t sure whether a local variable is effectively final, just add the final keyword. If the code still compiles, the variable is effectively final.

---
The Effectively Final variable is a local variable that follows the following properties:
- ==**Not defined as ``final``**==
- ==**Assigned to ONLY once.**==
---

```java
11: public String zooFriends() {
12: String name = "Harry the Hippo";
13: var size = 10;
14: boolean wet;
15: if(size > 100) size++;
16: name.substring(0);
17: wet = true;
18: return name;
19: }
```

a quick test of effectively final is to just add final to the variable declaration and see if it still compiles.
In this example, name and wet are effectively final and can be updated with the final modifier, but not size. The name variable is assigned a value on line 12 and not reassigned. Line 16 creates a value that is never used. The size variable is not effectively final because it could be incremented on line 15.
### Instance Variable Modifiers

Like methods, instance variables can use access modifiers, such as ``private``, ``package``, ``protected``, and ``public``.
Instance variables can also use optional specifiers

|Modifier|Description|Chapter Covered|
|---|---|---|
|final|Specifies that the instance variable must be initialized with each instance of the class exactly once|Chapter 5|
|volatile|Instructs the JVM that the value in this variable may be modified by other threads|Chapter 13|
|transient|Used to indicate that an instance variable should not be serialized with the class|Out of scope|
If an instance variable is marked ``final``, then it must be assigned a value when it is declared or when the object is instantiated. Like a local final variable, it cannot be assigned a value more than once

```java
public class PolarBear {
	final int age = 10;
	final int fishEaten;
	final String name;
	{ fishEaten = 10; }
	public PolarBear() {
		name = "Robert";
	}
}
```

The ``age`` variable is given a value when it is declared, while the ``fishEaten`` variable is assigned a value in an instance initializer. The name variable is given a value in the no-argument constructor.

---

==**The compiler does not apply a default value to ``final`` variables, though. A ``final`` instance or ``final static`` variable must receive a value when it is declared or as part of initialization.**==

---

```java
public class PolarBear2 {  

    final int age;  
    final int fishEaten;  
    final String name;  
  
    public PolarBear2() {  
        this(1, 5);  
    }  
  
    public PolarBear2(int age, int fishEaten) {  
        this.age = age;  
        this.fishEaten = fishEaten;  
        name = "default";  
    }  
  
    public PolarBear2(int age, int fishEaten, String name) {  
        this.age = age;  
        this.fishEaten = fishEaten;  
        this.name = name;  
    }
```

## Working with Varargs

### Creating Methods with Varargs

**Rules for Creating a Method with a Varargs Parameter**

1. ==**A method can have at most one varargs parameter.**==
2. ==**If a method contains a varargs parameter, it must be the last parameter in the list.**==

```java
public class VisitAttractions {
	public void walk1(int... steps) {}
	public void walk2(int start, int... steps) {}
	public void walk3(int... steps, int start) {} // DOES NOT COMPILE
	public void walk4(int... start, int... steps) {} // DOES NOT COMPILE
	public void walk5(int start, ...int steps) {} // DOES NOT COMPILE
}
```

### Calling Methods with Varargs

When calling a method with a varargs parameter, you have a choice. You can pass in an array, or you can list the elements of the array and let Java create it for you.

```java
// Pass an array
int[] data = new int[] {1, 2, 3};
walk1(data);
// Pass a list of values
walk1(1,2,3);
```

Regardless of which one you use to call the method, the method will receive an array containing the elements.

```java
public void walk1(int... steps) {
	int[] step2 = steps; // Not necessary, but shows steps is of type int[]
	System.out.print(step2.length);
}
```

can even omit the varargs values in the method call, and Java will create an array of length zero for you.

```java
walk1();
```
###  Accessing Elements of a Vararg

Accessing a varargs parameter is just like accessing an array. It uses array indexing.

```java
16: public static void run(int... steps) {
17: System.out.print(steps[1]);
18: }
19: public static void main(String[] args) {
20: run(11, 77); // 77
21: }
```
### Using Varargs with Other Method Parameters

```java
1: public class DogWalker {
2: public static void walkDog(int start, int... steps) {
3: System.out.println(steps.length);
4: }
5: public static void main(String[] args) {
6: walkDog(1); // 0
7: walkDog(1, 2); // 1
8: walkDog(1, 2, 3); // 2
9: walkDog(1, new int[] {4, 5}); // 2
10: } }
```

Java will create an empty array if no parameters are passed for a vararg. However, it is still possible to pass ``null`` explicitly

```java
walkDog(1, null); // Triggers NullPointerException in walkDog()
```

Since ``null`` isn’t an int, Java treats it as an array reference that happens to be ``null``. It just passes on the ``null`` array object to ``walkDog()``. Then the ``walkDog()`` method throws an exception because it tries to determine the length of ``null``.
## Applying Access Modifiers

- ==**``private``: Only accessible within the same class.**==
- ==**Package access: ``private`` plus other members of the same package. Sometimes referred to as package-private or default access.**==
- ==**``protected``: Package access plus access within subclasses.**==
- ==**``public``: ``protected`` plus classes in the other packages.==**
### Private Access

Only code in the same class can call ``private`` methods or access ``private`` fields.

```java
1: package pond.duck;
2: public class FatherDuck {
3: private String noise = "quack";
4: private void quack() {
5: System.out.print(noise); // private access is ok
6: }
7: }
```

``FatherDuck`` declares a ``private`` method ``quack()`` and uses ``private`` instance variable ``noise`` on line 5.

```java
1: package pond.duck;
2: public class BadDuckling {
3: public void makeNoise() {
4: var duck = new FatherDuck();
5: duck.quack(); // DOES NOT COMPILE
6: System.out.print(duck.noise); // DOES NOT COMPILE
7: }
8: }
```

``BadDuckling`` is trying to access an instance variable and a method it has no business touching. accessing ``private`` members of other classes is not allowed, and you need to use a different type of access.

---

**In the previous example, ``FatherDuck`` and ``BadDuckling`` are in separate files, but what if they were declared in the same file? Even then, the code would still not compile as Java prevents access outside the class.**

---
### Package Access

When there is no access modifier, Java assumes package access.

```java
package pond.duck;
public class MotherDuck {
	String noise = "quack";
	void quack() {
		System.out.print(noise); // package access is ok
	}
}
```

The big difference is that ``MotherDuck`` lets other classes in the same package access members, whereas ``FatherDuck`` doesn’t (due to being private). 

```java
package pond.duck;
public class GoodDuckling {
	public void makeNoise() {
		var duck = new MotherDuck();
		duck.quack(); // package access is ok
		System.out.print(duck.noise); // package access is ok
	}
}
```

all the classes covered so far are in the same package, ``pond.duck``. This allows package access to work.

```java
package pond.swan;
import pond.duck.MotherDuck; // import another package
public class BadCygnet {
	public void makeNoise() {
		var duck = new MotherDuck();
		duck.quack(); // DOES NOT COMPILE
		System.out.print(duck.noise); // DOES NOT COMPILE
	}
}
```

``MotherDuck`` only allows lessons to other ducks by restricting access to the ``pond.duck`` package. ``BadCygnet`` is in the ``pond.swan`` package, and the code doesn’t compile.
### Protected Access

Protected access allows everything that package access does, and more. The ``protected`` access modifier adds the ability to access members of a parent class. 

```java
public class Fish {}
public class ClownFish extends Fish {}
```

the “child” ``ClownFish`` class is a subclass of the “parent” ``Fish`` class, using the ``extends`` keyword to connect them

**==By extending a class, the subclass gains access to all ``protected`` and ``public`` members of the parent class, as if they were declared in the subclass. If the two classes are in the same package, then the subclass also gains access to all package members.==**

```java
package pond.shore;
public class Bird {
	protected String text = "floating";
	protected void floatInWater() {
		System.out.print(text); // protected access is ok
	}
}
```

```java
package pond.goose; // Different package than Bird
import pond.shore.Bird;
public class Gosling extends Bird { // Gosling is a subclass of Bird
	public void swim() {
		floatInWater(); // protected access is ok
	System.out.print(text); // protected access is ok
	}
	public static void main(String[] args) {
		new Gosling().swim();
	}
}
```

This is a simple subclass. It extends the ``Bird`` class. Extending means creating a subclass that has access to any protected or public members of the parent class

Remember that protected also gives us access to everything that package access does. This means a class in the same package as ``Bird`` can access its protected members.

```java
package pond.shore; // Same package as Bird
public class BirdWatcher {
	public void watchBird() {
		Bird bird = new Bird();
		bird.floatInWater(); // protected access is ok
		System.out.print(bird.text); // protected access is ok
	}
}
```

Since ``Bird`` and ``BirdWatcher`` are in the same package, ``BirdWatcher`` can access package members of the bird variable. **==The definition of protected allows access to subclasses and classes in the same package.==**

```java
package pond.inland; // Different package than Bird
import pond.shore.Bird;
public class BirdWatcherFromAfar { // Not a subclass of Bird
	public void watchBird() {
		Bird bird = new Bird();
		bird.floatInWater(); // DOES NOT COMPILE
		System.out.print(bird.text); // DOES NOT COMPILE
	}
}
```

``BirdWatcherFromAfar`` is not in the same package as ``Bird``, and it doesn’t inherit from ``Bird``. This means it is not allowed to access protected members of ``Bird``. Subclasses and classes in the same package are the only ones allowed to access protected members.

```java
1: package pond.swan; // Different package than Bird
2: import pond.shore.Bird;
3: public class Swan extends Bird { // Swan is a subclass of Bird
	4: public void swim() {
		5: floatInWater(); // protected access is ok
		6: System.out.print(text); // protected access is ok
	7: }
	8: public void helpOtherSwanSwim() {
		9: Swan other = new Swan();
		10: other.floatInWater(); // subclass access to superclass
		11: System.out.print(other.text); // subclass access to superclass
	12: }
	13: public void helpOtherBirdSwim() {
		14: Bird other = new Bird();
		15: other.floatInWater(); // DOES NOT COMPILE
		16: System.out.print(other.text); // DOES NOT COMPILE
	17: }
18: }
```

``Swan`` is not in the same package as ``Bird`` but does extend it—which implies it has access to the protected members of Bird since it is a subclass. And it does. Lines 5 and 6 refer to protected members via inheriting them.

Lines 10 and 11 also successfully use protected members of ``Bird``. This is allowed because these lines refer to a ``Swan`` object. ``Swan`` inherits from ``Bird``, so this is okay. It is sort of a two-phase check. The ``Swan`` class is allowed to use protected members of ``Bird``, and we are referring to a ``Swan`` object. Granted, it is a ``Swan`` object created on line 9 rather than an inherited one, but it is still a ``Swan`` object.

Lines 15 and 16 do not compile a ``Bird`` reference is used rather than inheritance. It is created on line 14. ``Bird`` is in a different package, and this code isn’t inheriting from ``Bird``, so it doesn’t get to use protected members. the variable reference isn’t a ``Swan``. The code just happens to be in the ``Swan`` class.

Looking at it a different way, the protected rules apply under two scenarios:

- ==**A member is used without referring to a variable. This is the case on lines 5 and 6. In this case, we are taking advantage of inheritance, and protected access is allowed.**==

- ==**A member is used through a variable. This is the case on lines 10, 11, 15, and 16. In this case, the rules for the reference type of the variable are what matter. If it is a subclass, protected access is allowed. This works for references to the same class or a subclass.==**

---

**==In Java, when a class extends another class, it inherits access to its protected members, allowing it to use them directly. When accessing these members through an object of the subclass, it's considered accessing them via inheritance, which is permitted. However, if you try to access protected members through a reference to the superclass, it won't compile because it's not considered inheritance and thus doesn't have access to those members.==** #TIP 

---

```JAVA
package pond.goose;
import pond.shore.Bird;
public class Goose extends Bird {
	public void helpGooseSwim() {
		Goose other = new Goose();
		other.floatInWater();
		System.out.print(other.text);
	}
	public void helpOtherGooseSwim() {
		Bird other = new Goose();
		other.floatInWater(); // DOES NOT COMPILE
		System.out.print(other.text); // DOES NOT COMPILE
	}
}
```

The second method is a problem. Although the object happens to be a ``Goose``, it is stored in a ``Bird`` reference. We are not allowed to refer to members of the ``Bird`` class since we are not in the same package and the reference type of other is not a subclass of ``Goose``.

```java
package pond.duck;
import pond.goose.Goose;
public class GooseWatcher {
	public void watch() {
		Goose goose = new Goose();
		goose.floatInWater(); // DOES NOT COMPILE
		// This code doesn’t compile because we are not in the goose object.
	}
}
```

This code doesn’t compile because we are not in the goose object. The ``floatInWater()`` method is declared in ``Bird``. ``GooseWatcher`` is not in the same package as ``Bird``, nor does it extend ``Bird``. ``Goose`` extends ``Bird``. That only lets ``Goose`` refer to ``floatInWater()``, not callers of ``Goose``.

---

**==the `GooseWatcher` class attempts to call the `floatInWater()` method on a `Goose` object, but it doesn't compile because `GooseWatcher` doesn't inherit from `Bird` nor is it in the same package as `Bird`. While `Goose` extends `Bird`, this only allows instances of `Goose` to access `floatInWater()`, not instances of `GooseWatcher`. Essentially, access to `floatInWater()` is restricted to instances of `Goose` or its subclasses due to the protected access level, and `GooseWatcher` isn't in that inheritance hierarchy.==**

---
### Public Access

``public`` means anyone can access the member from anywhere.

```java
package pond.duck;
public class DuckTeacher {
	public String name = "helpful";
	public void swim() {
		System.out.print(name); // public access is ok
	}
}
```

```java
package pond.goose;
import pond.duck.DuckTeacher;
public class LostDuckling {
	public void swim() {
		var teacher = new DuckTeacher();
		teacher.swim(); // allowed
		System.out.print("Thanks" + teacher.name); // allowed
	}
}
```

### Reviewing Access Modifiers

A method in `` ______`` can access a ``______`` member.

|                                           | private | package | protected | public |
| ----------------------------------------- | ------- | ------- | --------- | ------ |
| the same class                            | Yes     | Yes     | Yes       | Yes    |
| another class in the same package         | No      | Yes     | Yes       | Yes    |
| a subclass in a different package         | No      | No      | Yes       | Yes    |
| an unrelated class in a different package | No      | No      | No        | Yes    |
## Accessing ``static`` Data

When the ``static`` keyword is applied to a variable, method, or class, it belongs to the class rather than a specific instance of the class.
### Designing ``static`` Methods and Variables

Methods and variables declared static don’t require an instance of the class. They are shared among all users of the class.

```java
public class Penguin {
	String name;
	static String nameOfTallestPenguin;
}
```

**==think of a ``static`` variable as being a member of the single class object that exists independently of any instances of that class.==**

```java
public static void main(String[] unused) {
	var p1 = new Penguin();
	p1.name = "Lilly";
	p1.nameOfTallestPenguin = "Lilly";
	var p2 = new Penguin();
	p2.name = "Willy";
	p2.nameOfTallestPenguin = "Willy";
	
	System.out.println(p1.name); // Lilly
	System.out.println(p1.nameOfTallestPenguin); // Willy
	System.out.println(p2.name); // Willy
	System.out.println(p2.nameOfTallestPenguin); // Willy
}
```


```java
public class Koala {
	public static int count = 0; // static variable
	public static void main(String[] args) { // static method
		System.out.print(count);
	}
}
```

``static`` methods have two main purposes:

- For utility or helper methods that don’t require any object state. Since there is no need to access instance variables, having static methods eliminates the need for the caller to instantiate an object just to call the method.

-  For state that is shared by all instances of a class, like a counter. All instances must share the same state. Methods that merely use that state should be static as well.
### Accessing a ``static`` Variable or Method

```java
public class Snake {
	public static long hiss = 2;
}
```

just put the class name before the method or variable, and you are done.

```java
System.out.println(Snake.hiss);
```

**==There is one rule that is trickier. You can use an instance of the object to call a ``static`` method. The compiler checks for the type of the reference and uses that instead of the object==**

```java
5: Snake s = new Snake();
6: System.out.println(s.hiss); // s is a Snake
7: s = null;
8: System.out.println(s.hiss); // s is still a Snake
```

Java doesn’t care that ``s`` happens to be ``null``. Since we are looking for a ``static`` variable, it doesn’t matter.

---

==**Remember to look at the reference type for a variable when you see a ``static`` method or variable. The exam creators will try to trick you into thinking a ``NullPointerException`` is thrown because the variable happens to be ``null``. Don’t be fooled!**== #TIP 

---

```java
Snake.hiss = 4;
Snake snake1 = new Snake();
Snake snake2 = new Snake();
snake1.hiss = 6;
snake2.hiss = 5;
System.out.println(Snake.hiss); // 5 
```
### Class vs. Instance Membership

**==A ``static`` member cannot call an instance member without referencing an instance of the class.==**

```java
public class MantaRay {
	private String name = "Sammy";
	public static void first() { }
	public static void second() { }
	public void third() { System.out.print(name); }
	public static void main(String args[]) {
		first();
		second();
		third(); // DOES NOT COMPILE
	}
}
```

The compiler will give you an error about making a ``static`` reference to an instance method. If we fix this by adding ``static`` to ``third()``, we create a new problem.

```java
public static void third() { System.out.print(name); } // DOES NOT COMPILE
```

All this does is move the problem. Now, ``third()`` is referring to an instance variable name. There are two ways we could fix this. 

1. Add static to the name variable as well

```java
public class MantaRay {
	private static String name = "Sammy";
	...
	public static void third() { System.out.print(name); }
	...
}
```

2. call ``third()`` as an instance method and not use ``static`` for the method or the variable. 

```java
public class MantaRay {
	private String name = "Sammy";
	...
	public void third() { System.out.print(name); }
	public static void main(String args[]) {
		...
		var ray = new MantaRay();
		ray.third();
	}
}
```

**==A ``static`` method or instance method can call a ``static`` method because ``static`` methods don’t require an object to use.==** **==Only an instance method can call another instance method on the same class without using a reference variable==**, because instance methods do require an object. Similar logic applies for instance and ``static`` variables.

```java
public class Giraffe {
	public void eat(Giraffe g) {}
	public void drink() {};
	public static void allGiraffeGoHome(Giraffe g) {}
	public static void allGiraffeComeOut() {}
}
```

| Method                 | Calling                 | Legal |
| ---------------------- | ----------------------- | ----- |
| ``allGiraffeGoHome()`` | ``allGiraffeComeOut()`` | Yes   |
| ``allGiraffeGoHome()`` | ``drink()``             | No    |
| ``allGiraffeGoHome()`` | ``g.eat()``             | Yes   |
| ``eat()``              | ``allGiraffeComeOut()`` | Yes   |
| ``eat()``              | ``drink()``             | Yes   |
| ``eat()``              | ``g.eat()``             | Yes   |

```java
1: public class Gorilla {
	2: public static int count;
	3: public static void addGorilla() { count++; }
	4: public void babyGorilla() { count++; }
	5: public void announceBabies() {
		6: addGorilla();
		7: babyGorilla();
	8: }
	9: public static void announceBabiesToEveryone() {
		10: addGorilla();
		11: babyGorilla(); // DOES NOT COMPILE
	12: }
	13: public int total;
	14: public static double average
	15: = total / count; // DOES NOT COMPILE
16: }
```

- Lines 3 and 4 are fine because both ``static`` and instance methods can refer to a ``static`` variable.
- Lines 5–8 are fine because an instance method can call a ``static`` method.
- **==Line 11 doesn’t compile because a ``static`` method cannot call an instance method==**.
- **==Line 15 doesn’t compile because a ``static`` variable is trying to use an instance variable==**.
### ``static`` Variable Modifiers

``static`` variables can be declared with the same modifiers as instance variables, such as ``final``, ``transient``, and ``volatile``. While some ``static`` variables are meant to change as the program runs, like our count example, others are meant to never change. This type of ``static`` variable is known as a constant. It uses the ``final`` modifier to ensure the variable never changes.

Constants use the modifier ``static final`` and a different naming convention than other variables. They use all uppercase letters with underscores between “words.”

```java
public class ZooPen {
	private static final int NUM_BUCKETS = 45;
	public static void main(String[] args) {
		NUM_BUCKETS = 5; // DOES NOT COMPILE
	}
}
```

The compiler will make sure that you do not accidentally try to update a ``final`` variable.

```java
import java.util.*;
public class ZooInventoryManager {
	private static final String[] treats = new String[10];
	public static void main(String[] args) {
		treats[0] = "popcorn";
	}
}
```

It actually does compile since ``treats`` is a reference variable. **==We are allowed to modify the referenced object or array’s contents==**. All the compiler can do is check that we don’t try to reassign ``treats`` to point to a different object.

**==The rules for ``static final`` variables are similar to instance ``final`` variables, except they do not use ``static`` constructors (there is no such thing!) and use ``static`` initializers instead of instance initializers.==**

```java
public class Panda {
	final static String name = "Ronda";
	static final int bamboo;
	static final double height; // DOES NOT COMPILE
	static { bamboo = 5;}
}
```

- The ``name`` variable is assigned a value when it is declared
- The ``bamboo`` variable is assigned a value in a static initializer.
- The ``height`` variable is not assigned a value anywhere in the class definition, so that line does not compile.

### ``static`` Initializers

Static initializers add the ``static`` keyword to specify that they should be run when the class is first loaded.

```java
static {
	NUM_SECONDS_PER_MINUTE = 60;
	NUM_MINUTES_PER_HOUR = 60;
}
static {
	NUM_SECONDS_PER_HOUR = NUM_SECONDS_PER_MINUTE * NUM_MINUTES_PER_HOUR;
}
```

**==All ``static`` initializers run when the class is first used, in the order they are defined==**. The statements in them run and assign any ``static`` variables as needed. The final variables aren’t allowed to be reassigned(Assumed). **==The key here is that the ``static`` initializer is the first assignment. And since it occurs up front, it is okay==**.

```java
14: private static int one;
15: private static final int two;
16: private static final int three = 3;
17: private static final int four; // DOES NOT COMPILE
	private int five;
	private static final int eight;

18: static {
		19: one = 1;
		20: two = 2;
		21: three = 3; // DOES NOT COMPILE
		22: two = 4; // DOES NOT COMPILE
		five = 5; // DOES NOT COMPILE - instance variable!
		static int seven = 7; // DOES NOT COMPILE - local variable
		eight = 8;
23: }

	static {  
	     eight = 8; // DOES NOT COMPILE  
	}
```

- Line 14 declares a ``static`` variable that is not ``final``. It can be assigned as many times as we like
- Line 15 declares a ``final`` variable without initializing it. This means we can initialize it exactly once in a static block.
- Line 22 doesn’t compile because this is the second attempt.
- Line 16 declares a ``final`` variable and initializes it at the same time. We are not allowed to assign it again, so line 21 doesn’t compile.
- Line 17 declares **==a ``static final`` variable that never gets initialized==**. The compiler gives a compiler error because it knows that **==the ``static`` blocks are the only place the variable could possibly be initialized==**.

### ``static`` Imports

```java
import java.util.ArrayList;
import java.util.*;
```

```java
import java.util.List;
import java.util.Arrays;
public class Imports {
	public static void main(String[] args) {
		List<String> list = Arrays.asList("one", "two");
	}
}
```

**==Regular imports are for importing classes, while ``static`` imports are for importing static members of classes like variables and methods.==** Just like regular imports, you can use a wildcard or import a specific member.

```java
import java.util.List;
import static java.util.Arrays.asList; // static import
public class ZooParking {
	public static void main(String[] args) {
		List<String> list = asList("one", "two"); // No Arrays. prefix
	}
}
```

**==An interesting case is what would happen if we created an ``asList`` method in our ``ZooParking`` class. Java would give it preference over the imported one, and the method we coded would be used.==**

```java
1: import static java.util.Arrays; // DOES NOT COMPILE
2: import static java.util.Arrays.asList;
3: static import java.util.Arrays.*; // DOES NOT COMPILE
4: public class BadZooParking {
	5: public static void main(String[] args) {
		6: Arrays.asList("one"); // DOES NOT COMPILE
	7: }
8: }
```

- Line 1 tries to use a ``static`` import to import a class.
- Line 3 tries to see whether you are paying attention to the order of keywords.
- Line 6 is sneaky. The ``asList`` method is imported on line 2. However, the ``Arrays`` class is not imported anywhere. This makes it okay to write ``asList("one")`` but not ``Arrays.asList("one")``.

**==The compiler will complain if you try to explicitly do a ``static`` import of two methods with the same name or two ``static`` variables with the same name.==**

```java
import static zoo.A.TYPE;
import static zoo.B.TYPE; // DOES NOT COMPILE
```

```java
import static java.lang.Integer.MAX_VALUE;  
import static java.lang.Long.MAX_VALUE;  // DOES NOT COMPILE
// Field 'MAX_VALUE' is already defined in a single static import  
// Reference to 'MAX_VALUE' is ambiguous, both 'Integer.MAX_VALUE' and 'Long.MAX_VALUE'  
public class StaticImportSameName {  
  
    public static void main(String[] args) {  
  
        System.out.println(MAX_VALUE);  
  
    }
```

## Passing Data among Methods

**==Java is a *pass-by-value* language. This means that a copy of the variable is made and the method receives that copy. Assignments made in the method do not affect the caller==**

```java
2: public static void main(String[] args) {
	3: int num = 4;
	4: newNumber(num);
	5: System.out.print(num); // 4
6: }
7: public static void newNumber(int num) {
	8: num = 8;
9: }
```

The name could be anything. The exam will often use the same name to try to confuse you. The variable on line 3 never changes because no assignments are made to it.
### Passing Objects

```java
public class Dog {
	public static void main(String[] args) {
		String name = "Webby";
		speak(name);
		System.out.print(name); // Webby
	}
	public static void speak(String name) {
		name = "Georgette";
	}
}
```

Just as in the primitive example, the variable assignment is only to the method parameter and doesn’t affect the caller.

```java
public class Dog {
	public static void main(String[] args) {
		var name = new StringBuilder("Webby");
		speak(name);
		System.out.print(name); // WebbyGeorgette
	}
	public static void speak(StringBuilder s) {
		s = null;  
		s = new StringBuilder("reassign");
		s.append("Georgette");
	}
}
```

In this case, ``speak()`` calls a method on the parameter. It doesn’t reassign s to a different object. The variable ``s`` is a copy of the variable name. Both point to the same ``StringBuilder``, which means that changes made to the ``StringBuilder`` are available to both references.

![[Pasted image 20240316191549.png]]

---

**Pass-by-Value vs. Pass-by-Reference**
**the ``swap()`` method does not change the original values. It only changes a and b within the method.**

```java
public static void main(String[] args) {
	int original1 = 1;
	int original2 = 2;
	swap(original1, original2);
	System.out.println(original1); // 1
	System.out.println(original2); // 2
}
public static void swap(int a, int b) {
	int temp = a;
	a = b;
	b = temp;
}
```

---
### Returning Objects

A copy is made of the primitive or reference and returned from the method. Most of the time, this returned value is used.

```java
1: public class ZooTickets {
	2: public static void main(String[] args) {
		3: int tickets = 2; // tickets = 2
		4: String guests = "abc"; // guests = abc
		5: addTickets(tickets); // tickets = 2
		6: guests = addGuests(guests); // guests = abcd
		7: System.out.println(tickets + guests); // 2abcd
	8: }
	9: public static int addTickets(int tickets) {
		10: tickets++;
		11: return tickets;
	12: }
	13: public static String addGuests(String guests) {
		14: guests += "d";
		15: return guests;
	16: }
17: }
```

When you see such questions on the exam, write down the values of each variable.

- Lines 3 and 4 are straightforward assignments. 
- Line 5 calls a method.
- Line 10 increments the method parameter to 3 but leaves the ``tickets`` variable in the ``main()`` method as 2
- line 11 returns the value, the caller ignores it.
- The method call on line 6 doesn’t ignore the result, so ``guests`` becomes "abcd"
### Autoboxing and Unboxing Variables

Java supports some helpful features around passing primitive and wrapper data types, such as ``int`` and ``Integer``.

```java
5: int quack = 5;
6: Integer quackquack = Integer.valueOf(quack); // Convert int to Integer
7: int quackquackquack = quackquack.intValue(); // Convert Integer to int
```

Useful, but a bit verbose. Luckily, Java has handlers built into the Java language that automatically convert between primitives and wrapper classes and back again. 
- ==**Autoboxing is the process of converting a primitive into its equivalent wrapper class,**==  
- ==**Unboxing is the process of converting a wrapper class into its equivalent primitive==**

```java
5: int quack = 5;
6: Integer quackquack = Integer.valueOf(quack); // Convert int to Integer
7: int quackquackquack = quackquack.intValue(); // Convert Integer to int
```

Autoboxing applies to all primitives and their associated wrapper types, such as the following:

```java
Short tail = 8; // Autoboxing
Character p = Character.valueOf('p');
char paw = p; // Unboxing
Boolean nose = true; // Autoboxing
Integer e = Integer.valueOf(9);
long ears = e; // Unboxing, then implicit casting
```

In the last line, ``e`` is unboxed to an ``int`` value. Since an ``int`` value can be stored in a ``long`` variable via implicit casting, the compiler allows the assignment.

---
**==Limits of Autoboxing and Numeric Promotion==**

**==While Java will implicitly cast a smaller primitive to a larger type, as well as autobox, it will not do both at the same time.==**

```java
Long badGorilla = 8; // DOES NOT COMPILE
```

**==Java will automatically cast or autobox the ``int`` value to ``long`` or ``Integer``, respectively. Neither of these types can be assigned to a ``Long`` reference variable, though, so the code does not compile==**

---

What do you think happens if you try to unbox a ``null``?

```java
10: Character elephant = null;
11: char badElephant = elephant; // NullPointerException
```

Since calling any method on ``null`` gives a ``NullPointerException``, that is just what we get. Be careful when you see ``null`` in relation to autoboxing and unboxing.

```java
public class Chimpanzee {
	public void climb(long t) {}
	public void swing(Integer u) {}
	public void jump(int v) {}
	public static void main(String[] args) {
		var c = new Chimpanzee();
		c.climb(123);
		c.swing(123);
		c.jump(123L); // DOES NOT COMPILE
	}
}
```

- ``climb()`` compiles because the ``int`` value can be implicitly cast to a ``long``.
- ``swing()`` also is permitted, because the int value is autoboxed to an ``Integer``.
- ``jump()`` results in a compiler error because a ``long`` must be explicitly cast to an ``int``. In other words, Java will not automatically convert to a narrower type.

```java
public class Gorilla {
	public void rest(Long x) {
		System.out.print("long");
	}
	public static void main(String[] args) {
		var g = new Gorilla();
		g.rest(8); // DOES NOT COMPILE
	}
}
```

Java will cast or autobox the value automatically, but not both at the same time.
## Overloading Methods

==***Method overloading* occurs when methods in the same class have the same name but different method signatures, which means they use different parameter lists.**== Overloading also allows different numbers of parameters. **==Everything other than the method name can vary for overloading methods==**. This means
there can be different access modifiers, optional specifiers (like static), return types, and exception lists.

```java
public class Falcon {
	public void fly(int numMiles) {}
	public void fly(short numFeet) {}
	public boolean fly() { return false; }
	void fly(int numMiles, short numFeet) {}
	public void fly(short numFeet, int numMiles) throws Exception {}
}
```

**==the return type, access modifier, and exception list are irrelevant to overloading. Only the method name and parameter list matter.==**

```java
public class Eagle {
	public void fly(int numMiles) {}
	public int fly(int numMiles) { return 1; } // DOES NOT COMPILE
}
```

This method doesn’t compile because it differs from the original only by return type. The method signatures are the same, so they are duplicate methods as far as Java is concerned.

```java
public class Hawk {
	public void fly(int numMiles) {}
	public static void fly(int numMiles) {} // DOES NOT COMPILE
	public void fly(int numKilometers) {} // DOES NOT COMPILE
}
```

Calling overloaded methods is easy. You just write code, and Java calls the right one.

```java
public class Dove {
	public void fly(int numMiles) {
		System.out.println("int");
	}
	public void fly(short numFeet) {
		System.out.println("short");
	}
}
```

The call ``fly((short) 1)`` prints ``short``. It looks for matching types and calls the appropriate method.
### Reference Types

**==the rule about Java picking the most specific version of a method that it can==**

```java
public class Pelican {
	public void fly(String s) {
		System.out.print("string");
	}
	public void fly(Object o) {
		System.out.print("object");
	}
	public static void main(String[] args) {
		var p = new Pelican();
		p.fly("test"); // String
		System.out.print("-");
		p.fly(56); // Object
	}
}
```

- The first call passes a String and finds a direct match.
- The second call looks for an int parameter list. When it doesn’t find one, it autoboxes to ``Integer``. Since it still doesn’t find a match, it goes to the ``Object`` one.

```java
import java.time.*;
import java.util.*;
public class Parrot {
	public static void print(List<Integer> i) {
		System.out.print("I");
	}
	public static void print(CharSequence c) {
		System.out.print("C");
	}
	public static void print(Object o) {
		System.out.print("O");
	}
	public static void main(String[] args){
		print("abc"); // C
		print(Arrays.asList(3)); // I
		print(LocalDate.of(2019, Month.JULY, 4)); // O
	}
}
```

The code is due for a promotion!

- The first call to ``print()`` passes a ``String``.
- ``Arrays.asList()`` can be used to create ``asList<Integer>`` object
- The final call to print() passes a ``LocalDate``. That means the ``Object`` method signature is used.

### Primitives

Primitives work in a way that’s similar to reference variables. Java tries to find the most specific matching overloaded method.

```java
public class Ostrich {
	public void fly(int i) {
		System.out.print("int");
	}
	public void fly(long l) {
		System.out.print("long");
	}
	public static void main(String[] args) {
		var p = new Ostrich();
		p.fly(123); // int
		System.out.print("-");
		p.fly(123L); // long
	}
}
```

- The first call passes an int and sees an exact match.
- The second call passes a long and also sees an exact match
Java has no problem calling a larger primitive. However, it will not do so unless a better match is not found.

```java
public class Ambiguous {  
  
    private static void fly(int a, long b) {  
        System.out.println("int , long");  
    }  
  
    private static void fly(long a, int b) {  
        System.out.println("long , int");  
    }  
  
    public static void main(String[] args) {  
  
        fly(1, 2); // DOES NOT COMPILE Ambiguous method call!  
        fly(1L, 2);  
        fly(1, 2L);  
    }  
}
```
### Autoboxing

```java
public class Kiwi {
	public void fly(int numMiles) {}
	public void fly(Integer numMiles) {}
}
```

These method overloads are valid. Java tries to use the most specific parameter list it can find. This is true for autoboxing as well as other matching types we talk about in this section. This means calling ``fly(3)`` will call the first method. **==When the primitive ``int`` version isn’t present, Java will autobox. However, when the primitive ``int`` version is provided, there is no reason for Java to do the extra work of autoboxing.==**

### Arrays

```java
public static void walk(int[] ints) {}
public static void walk(Integer[] integers) {}
```

this code does not autobox:

### Varargs

Which method do you think is called if we pass an ``int[]``?

```java
public class Toucan {
	public void fly(int[] lengths) {}
	public void fly(int... lengths) {} // DOES NOT COMPILE
}
```

Java treats ``varargs`` as if they were an array. This means the method signature is the same for both methods. Since we are not allowed to overload methods with the same parameter list, this code doesn’t compile. Even though the code doesn’t look the same, it compiles to the same parameter list

```java
fly(new int[] { 1, 2, 3 }); // Allowed to call either fly() method
```

you can only call the ``varargs`` version with stand-alone parameters:

```java
fly(1, 2, 3); // Allowed to call only the fly() method using varargs
```

### Putting It All Together

**==Java calls the most specific method it can. When some of the types interact, the Java rules focus on backward compatibility. A long time ago, autoboxing and varargs didn’t exist. Since old code still needs to work, this means autoboxing and varargs come last when Java looks at overloaded methods.==**

The order that Java uses to choose the right overloaded method

| Rule                  | Method Signature                     |
| --------------------- | ------------------------------------ |
| Exact match by type   | `String glide(int i, int j)`         |
| Larger primitive type | `String glide(long i, long j)`       |
| Autoboxed type        | `String glide(Integer i, Integer j)` |
| Varargs               | `String glide(int... nums)`          |
```java
public class Glider {
	public static String glide(String s) {
		return "1";
	}
	public static String glide(String... s) {
		return "2";
	}
	public static String glide(Object o) {
		return "3";
	}
	public static String glide(String s, String t) {
		return "4";
	}
	public static void main(String[] args) {
		System.out.print(glide("a")); // 1
		System.out.print(glide("a", "b")); // 4
		System.out.print(glide("a", "b", "c")); // 2
	}
}
```

- The first call matches the signature taking a single ``String`` because that is the most specific match.
- The second call matches the signature taking two ``String`` parameters since that is an exact match.

## Summary #OCP_Summary 

**==The access modifiers are ``private``, package (omitted), ``protected``, and ``public``. The optional specifier for methods  ``static``. For this chapter.**==

==**the method return type, which is ``void`` if there is no return value. The method name and parameter list are provided next, which compose the unique method signature. The method name uses standard Java identifier rules, while the parameter list is composed of zero or more types with names. An optional list of exceptions may also be added following the parameter list. Finally, a block defines the method body (which is omitted for ``abstract`` methods).**==

==**Using the ``private`` keyword means the code is only available from within the same class. Package access means the code is available only from within the same package. Using the ``protected`` keyword means the code is available from the same package or subclasses. Using the ``public`` keyword means the code is available from anywhere.**==

==**Both ``static`` methods and ``static`` variables are shared by all instances of the class. When referenced from outside the class, they are called using the class name—for example, ``Pigeon.fly()``. Instance members are allowed to call ``static`` members, but ``static`` members are not allowed to call instance members. In addition, ``static`` imports are used to import ``static`` members.**==

==**the ``final`` modifier and showed how it can be applied to local, instance, and ``static`` variables. Remember, a local variable is effectively final if it is not modified after it is assigned. One quick test for this is to add the ``final`` modifier and see if the code still compiles.**==

==**Java uses pass-by- value, which means that calls to methods create a copy of the parameters. Assigning new values to those parameters in the method doesn’t affect the caller’s variables. Calling methods on objects that are method parameters changes the state of those objects and is reflected in the caller. Java supports autoboxing and unboxing of primitives and wrappers automatically within a method and through method calls.**==

==**Overloaded methods are methods with the same name but a different parameter list. Java calls the most specific method it can find. Exact matches are preferred, followed by wider primitives. After that comes autoboxing and finally ``varargs``.==**

## Exam Essentials #Essential 

**Be able to identify correct and incorrect method declarations.** Be able to view a method signature and know if it is correct, contains invalid or conflicting elements, or contains elements in the wrong order.

**Identify when a method or field is accessible**. Recognize when a method or field is accessible when the access modifier is: ``private``, package (omitted), ``protected``, or ``public``.

**Understand how to declare and use final variables**. Local, instance, and ``static`` variables may be declared final. Be able to understand how to declare them and how they can (or cannot) be used.

**Recognize valid and invalid uses of static imports**  ``Static`` imports import ``static`` members. They are written as import static, not static import. Make sure they are importing ``static`` methods or variables rather than class names.

**Apply autoboxing and unboxing**. The process of automatically converting from a primitive value to a wrapper class is called autoboxing, while the reciprocal process is called unboxing. Watch for a ``NullPointerException`` when performing unboxing.

**State the output of code involving methods**. Identify when to call ``static`` rather than instance methods based on whether the class name or object comes before the method. **==Recognize that instance methods can call ``static`` methods and that static methods need an instance of the object in order to call an instance method==**.

**Recognize the correct overloaded method**. Exact matches are used first, followed by wider primitives, followed by autoboxing, followed by varargs. Assigning new values to method parameters does not change the caller, but calling methods on them does.

## Review Questions

1. Which statements about the final modifier are correct? (Choose all that apply.)

A. Instance and static variables can be marked final.
B. A variable is effectively final only if it is marked final.
C. An object that is marked final cannot be modified.
D. Local variables cannot be declared with type var and the final modifier.
E. A primitive that is marked final cannot be modified.

**My Answer:  A,E**
**Correct Answer: A,E**

**A, E. Instance and static variables can be marked final, making option A correct. Effectively final means a local variable is not marked final but whose value does not change after it is set, making option B incorrect. Option C is incorrect, as final refers only to the reference to an object, not its contents. Option D is incorrect, as var and final can be used together. Finally, option E is correct: once a primitive is marked final, it cannot be modified.**

---

2. Which of the following can fill in the blank in this code to make it compile? (Choose all that apply.)

```JAVA
public class Ant {
	??? void method() {}
}
```

A. default
B. final
C. private
D. Public
E. String
F. zzz:

**My Answer:  B,C**
**Correct Answer: B,C**

**The keyword void is a return type. Only the access modifier or optional specifiers are allowed before the return type. Option C is correct, creating a method with private access. Option B is also correct, creating a method with package access and the optional specifier final. Since package access does not use a modifier, we get to jump right to final.**

---

3. Which of the following methods compile? (Choose all that apply.)

`A. final static void rain() {}`
`B. public final int void snow() {}`
`C. private void int hail() {}`
`D. static final void sleet() {}`
`E. void final ice() {}`
`F. void public slush() {}`

**My Answer:  A,D**
**Correct Answer: A,D**

**Options A and D are correct because the optional specifiers are allowed in any order. Options B and C are incorrect because they each have two return types. Options E and F are incorrect because the return type is before the optional specifier and access modifier, respectively.**

---

4. Which of the following can fill in the blank and allow the code to compile? (Choose all that apply.)
```java
final ??? song = 6;
```

A. int
B. Integer
C. long
D. Long
E. double
F. Double

**My Answer:  A,B,C,E**
**Correct Answer: A,B,C,E**

**The value 6 can be implicitly promoted to any of the primitive types, making options A, C, and E correct. It can also be autoboxed to Integer, making option B correct. ==It cannot be both promoted and autoboxed, making options D and F incorrect==.**

---

5. Which of the following methods compile? (Choose all that apply.)

`A. public void january() { return; }`
`B. public int february() { return null;}`
`C. public void march() {}`
`D. public int april() { return 9;}`
`E. public int may() { return 9.0;}`
`F. public int june() { return;}`

**My Answer:  A,C,D**
**Correct Answer: A,C,D**

**Options A and C are correct because a void method is optionally allowed to have a return statement as long as it doesn’t try to return a value. Option B does not compile because null requires a reference object as the return type. Since int is primitive, it is not a reference object. Option D is correct because it returns an int value. Option E does not compile because it tries to return a double when the return type is int. Since a double cannot be assigned to an int, it cannot be returned as one either. Option F does not compile because no value is actually returned.**

---

6. Which of the following methods compile? (Choose all that apply.)

`A. public void violin(int... nums) {}`
`B. public void viola(String values, int... nums) {}`
`C. public void cello(int... nums, String values) {}`
`D. public void bass(String... values, int... nums) {}`
`E. public void flute(String[] values, ...int nums) {}`
`F. public void oboe(String[] values, int[] nums) {}`

**My Answer:  A,B,F**
**Correct Answer: A,B,F**

**Options A and B are correct because the single varargs parameter is the last parameter declared. Option F is correct because it doesn’t use any varargs parameters. Option C is incorrect because the varargs parameter is not last. Option D is incorrect because two varargs parameters are not allowed in the same method. Option E is incorrect because the ``...`` for a varargs must be after the type, not before it.**

---

7. Given the following method, which of the method calls return 2? (Choose all that apply.)

```JAVA
public int juggle(boolean b, boolean... b2) {
	return b2.length;
}
```

`A. juggle();`
`B. juggle(true);`
`C. juggle(true, true);`
`D. juggle(true, true, true);`
`E. juggle(true, {true, true});`
`F. juggle(true, new boolean[2]);`

**My Answer:  D,F**
**Correct Answer: D,F**

Option D passes the initial parameter plus two more to turn into a varargs array of size 2. Option F passes the initial parameter plus an array of size 2. Option A does not compile because it does not pass the initial parameter. Option E does not compile because it does not declare an array properly. It should be ``new boolean[] {true, true}``. Option B creates a varargs array of size 0, and option C creates a varargs array of size 1.

---

8. Which of the following statements is correct?

A. Package access is more lenient than protected access.
B. A public class that has private fields and package methods is not visible to classes outside the package.
C. You can use access modifiers so only some of the classes in a package see a particular package class.
D. You can use access modifiers to allow access to all methods and not any instance variables.
E. You can use access modifiers to restrict access to all classes that begin with the word Test.

**My Answer:  D**
**Correct Answer: D**

**Option D is correct. A common practice is to set all fields to be private and all methods to be public. Option A is incorrect because protected access allows everything that package access allows and additionally allows subclasses access. Option B is incorrect because the class is public. This means that other classes can see the class. However, they cannot call any of the methods or read any of the fields. It is essentially a useless class. Option C is incorrect because package access applies to the whole package. Option E is incorrect because Java has no such wildcard access capability.**

---

9. Given the following class definitions, which lines in the main() method generate a compiler error? (Choose all that apply.)

```JAVA
// Classroom.java
package my.school;
public class Classroom {
private int roomNumber;
protected static String teacherName;
static int globalKey = 54321;
public static int floor = 3;
Classroom(int r, String t) {
roomNumber = r;
teacherName = t; } }

// School.java
1: package my.city;
2: import my.school.*;
3: public class School {
4: public static void main(String[] args) {
5: System.out.println(Classroom.globalKey);
6: Classroom room = new Classroom(101, "Mrs. Anderson");
7: System.out.println(room.roomNumber);
8: System.out.println(Classroom.floor);
9: System.out.println(Classroom.teacherName); } }
```

**My Answer:  C,D**
**Correct Answer: B,C,D,F**

**The two classes are in different packages, which means private access and package access will not compile. This causes compiler errors on lines 5, 6, and 7, making options B, C, and D correct answers. Additionally, protected access will not compile since School does not inherit from Classroom. This causes the compiler error on line 9, making option F a correct answer as well.**

---

10. What is the output of executing the Chimp program?

```JAVA
// Rope.java
1: package rope;
2: public class Rope {
3: public static int LENGTH = 5;
4: static {
5: LENGTH = 10;
6: }
7: public static void swing() {
8: System.out.print("swing ");
9: } }
// Chimp.java
1: import rope.*;
2: import static rope.Rope.*;
3: public class Chimp {
4: public static void main(String[] args) {
5: Rope.swing();
6: new Rope().swing();
7: System.out.println(LENGTH);
8: } }
```

A. swing swing 5
B. swing swing 10
C. Compiler error on line 2 of Chimp
D. Compiler error on line 5 of Chimp
E. Compiler error on line 6 of Chimp
F. Compiler error on line 7 of Chimp

**My Answer:  B**
**Correct Answer: B**

**Rope runs line 3, setting LENGTH to 5, and then immediately after that runs the static initializer, which sets it to 10. Line 5 in the Chimp class calls the static method normally and prints swing and a space. Line 6 also calls the static method. Java allows calling a static method through an instance variable, although it is not recommended. Line 7 uses the static import on line 2 to reference LENGTH.**

---

11. Which statements are true of the following code? (Choose all that apply.)

```JAVA
1: public class Rope {
2: public static void swing() {
3: System.out.print("swing");
4: }
5: public void climb() {
6: System.out.println("climb");
7: }
8: public static void play() {
9: swing();
10: climb();
11: }
12: public static void main(String[] args) {
13: Rope rope = new Rope();
14: rope.play();
15: Rope rope2 = null;
16: System.out.print("-");
17: rope2.play();
18: } }
```

A. The code compiles as is.
B. There is exactly one compiler error in the code.
C. There are exactly two compiler errors in the code.
D. If the line(s) with compiler errors are removed, the output is swing-climb.
E. If the line(s) with compiler errors are removed, the output is swing-swing.
F. If the line(s) with compile errors are removed, the code throws a NullPointerException.

**My Answer:  C,F**
**Correct Answer: B,E**

**Line 10 does not compile because static methods are not allowed to call instance methods. Even though we are calling play() as if it were an instance method and an instance exists, Java knows play() is really a static method and treats it as such. Since this is the only line that does not compile, option B is correct. If line 10 is removed, the code prints swing-swing, making ==option E correct. It does not throw a NullPointerException on line 17 because play() is a static method. Java looks at the type of the reference for rope2 and translates the call to Rope.play().==**

---

12. How many variables in the following method are effectively final?

```JAVA
10: public void feed() {
11: int monkey = 0;
12: if(monkey > 0) {
13: var giraffe = monkey++;
14: String name;
15: name = "geoffrey";
16: }
17: String name = "milly";
18: var food = 10;
19: while(monkey <= 10) {
20: food = 0;
21: }
22: name = null;
23: }
```

A. 1
B. 2
C. 3
D. 4
E. 5
F. None of the above. The code does not compile.

**My Answer:  B**
**Correct Answer: B**

**The test for effectively final is if the final modifier can be added to the local variable and the code still compiles.**

---

13. What is the output of the following code?

```JAVA
// RopeSwing.java
import rope.*;
import static rope.Rope.*;
public class RopeSwing {
private static Rope rope1 = new Rope();
private static Rope rope2 = new Rope();
{
System.out.println(rope1.length);
}
public static void main(String[] args) {
rope1.length = 2;
rope2.length = 8;
System.out.println(rope1.length);
}
}
// Rope.java
package rope;
public class Rope {
public static int length = 0;
}
```

A. 02
B. 08
C. 2
D. 8
E. The code does not compile.
F. An exception is thrown.

**My Answer:  E**
**Correct Answer: D**
 
 **There are two details to notice in this code. First, ==note that RopeSwing has an instance initializer and not a static initializer. Since RopeSwing is never constructed, the instance initializer does not run==. The other detail is that length is static. Changes from any object update this common static variable. The code prints 8, making option D correct.**

---

14. How many lines in the following code have compiler errors?

```JAVA
1: public class RopeSwing {
2: private static final String leftRope;
3: private static final String rightRope;
4: private static final String bench;
5: private static final String name = "name";
6: static {
7: leftRope = "left";
8: rightRope = "right";
9: }
10: static {
11: name = "name";
12: rightRope = "right";
13: }
14: public static void main(String[] args) {
15: bench = "bench";
16: }
17: }
```

A. 0
B. 1
C. 2
D. 3
E. 4
F. 5

**My Answer:  D**
**Correct Answer: E**

**If a variable is static final, it must be set exactly once, and it must be in the declaration line or in a static initialization block. Line 4 doesn’t compile because bench is not set in either of these locations. Line 15 doesn’t compile because final variables are not allowed to be set after that point. Line 11 doesn’t compile because name is set twice: once in the declaration and again in the static block. Line 12 doesn’t compile because rightRope is set twice as well. Both are in static initialization**

---

15. Which of the following can replace line 2 to make this code compile? (Choose all that apply.)

```JAVA
1: import java.util.*;
2: // INSERT CODE HERE
3: public class Imports {
4: public void method(ArrayList<String> list) {
5: sort(list);
6: }
7: }
```

`A. import static java.util.Collections;`
`B. import static java.util.Collections.*;`
`C. import static java.util.Collections.sort(ArrayList<String>);`
`D. static import java.util.Collections;`
`E. static import java.util.Collections.*;`
`F. static import java.util.Collections.sort(ArrayList<String>);``

**My Answer:  B**
**Correct Answer: B**

**The two valid ways to do this are import static ``java.util.Collections.``*; and import static ``java.util.Collections.sort``;. Option A is incorrect because you can do a static import only on static members. Classes such as Collections require a regular import. Option C is nonsense as method parameters have no business in an import. Options D, E, and F try to trick you into reversing the syntax of import static.**

---

16. What is the result of the following statements?
```java
1: public class Test {
2: public void print(byte x) {
3: System.out.print("byte-");
4: }
5: public void print(int x) {
6: System.out.print("int-");
7: }
8: public void print(float x) {
9: System.out.print("float-");
10: }
11: public void print(Object x) {
12: System.out.print("Object-");
13: }
14: public static void main(String[] args) {
15: Test t = new Test();
16: short s = 123;
17: t.print(s);
18: t.print(true);
19: t.print(6.789);
20: }
21: }
```

A. byte-float-Object-
B. int-float-Object-
C. byte-Object-float-
D. int-Object-float-
E. int-Object-Object-
F. byte-Object-Object-

**My Answer: E**
**Correct Answer: E**

**The argument on line 17 is a short. It can be promoted to an int, so print() on line 5 is invoked. The argument on line 18 is a boolean. It can be autoboxed to a Boolean, so print() on line 11 is invoked. The argument on line 19 is a double. It can be autoboxed to a Double, so print() on line 11 is invoked. Therefore, the output is int-Object-Object-** 

---

17. What is the result of the following program?

```JAVA
1: public class Squares {
2: public static long square(int x) {
3: var y = x * (long) x;
4: x = -1;
5: return y;
6: }
7: public static void main(String[] args) {
8: var value = 9;
9: var result = square(value);
10: System.out.println(value);
11: } }
```

A. -1
B. 9
C. 81
D. Compiler error on line 9
E. Compiler error on a different line

**My Answer: B**
**Correct Answer: B**

**Since Java is pass-by- value and the variable on line 8 never gets reassigned, it stays as 9.**

---

18. Which of the following are output by the following code? (Choose all that apply.)

```JAVA
public class StringBuilders {
public static StringBuilder work(StringBuilder a,
StringBuilder b) {
a = new StringBuilder("a");
b.append("b");
return a;
}
public static void main(String[] args) {
var s1 = new StringBuilder("s1");
var s2 = new StringBuilder("s2");
var s3 = work(s1, s2);
System.out.println("s1 = " + s1);
System.out.println("s2 = " + s2);
System.out.println("s3 = " + s3);
}
}
```

A. s1 = a
B. s1 = s1
C. s2 = s2
D. s2 = s2b
E. s3 = a
F. The code does not compile.

**My Answer: A,D,E**
**Correct Answer: B,D,E**

**Since Java is pass-by-value, assigning a new object to a does not change the caller. Calling append() does affect the caller because both the method parameter and the caller have a reference to the same object. Finally, returning a value does pass the reference to the caller for assignment to s3.**

---

19. Which of the following will compile when independently inserted in the following code? (Choose all that apply.)

```java
1: public class Order3 {
2: final String value1 = "red";
3: static String value2 = "blue";
4: String value3 = "yellow";
5: {
6: // CODE SNIPPET 1
7: }
8: static {
9: // CODE SNIPPET 2
10: } }
```

A. Insert at line 6: value1 = "green";
B. Insert at line 6: value2 = "purple";
C. Insert at line 6: value3 = "orange";
D. Insert at line 9: value1 = "magenta";
E. Insert at line 9: value2 = "cyan";
F. Insert at line 9: value3 = "turquoise";

**My Answer: B,C,E**
**Correct Answer: B,C,E**

**The variable value1 is a final instance variable. It can be set only once: in the variable declaration, an instance initializer, or a constructor. Option A does not compile because the final variable was already set in the declaration. The variable value2 is a static variable. Both instance and static initializers are able to access static variables, making options B and E correct. The variable value3 is an instance variable. Options D and F do not compile because a static initializer does not have access to instance variables.**

---

 20. Which of the following are true about the following code? (Choose all that apply.)

```JAVA
public class Run {
static void execute() {
System.out.print("1-");
}
static void execute(int num) {
System.out.print("2-");
}
static void execute(Integer num) {
System.out.print("3-");
}
static void execute(Object num) {
System.out.print("4-");
}
static void execute(int... nums) {
System.out.print("5-");
}
public static void main(String[] args) {
Run.execute(100);
Run.execute(100L);
}
}
```

A. The code prints out 2-4-.
B. The code prints out 3-4-.
C. The code prints out 4-2-.
D. The code prints out 4-4-.
E. The code prints 3-4- if you remove the method static void execute(int num).
F. The code prints 4-4- if you remove the method static void execute(int num).

**My Answer: A,E**
**Correct Answer: A,E**

**The 100 parameter is an int and so calls the matching int method, making option A correct. When this method is removed, Java looks for the next most specific constructor. Java prefers autoboxing to varargs, so it chooses the Integer constructor. The 100L parameter is a long. Since it can’t be converted into a smaller type, it is autoboxed into a Long, and then the method for Object is called,**

---

21. Which method signatures are valid overloads of the following method signature? (Choose all that apply.)

```JAVA
public void moo(int m, int... n)
```

A. public void moo(int a, int... b)
B. public int moo(char ch)
C. public void moooo(int... z)
D. private void moo(int... x)
E. public void moooo(int y)
F. public void moo(int... c, int d)
G. public void moo(int... i, int j...)

**My Answer: B,D**
**Correct Answer: B,D**

**Option A is incorrect because it has the same parameter list of types and therefore the same signature as the original method. Options B and D are valid method overloads because the types of parameters in the list change. When overloading methods, the return type and access modifiers do not need to be the same. Options C and E are incorrect because the method name is different. Options F and G do not compile. There can be at most one varargs parameter, and it must be the last element in the parameter list.**

---

# Chapter 6 - Class Design #Chapter

At its core, proper Java class design is about code reusability, increased functionality, and standardization
## Understanding Inheritance

When creating a new class in Java, you can define the class as inheriting from an existing class. Inheritance is the process by which a subclass automatically includes certain members of the class, including primitives, objects, or methods, defined in the parent class.

### Declaring a Subclass

![[Pasted image 20240322192526.png]]

indicate a class is a subclass by declaring it with the ``extends`` keyword. We don’t need to declare anything in the superclass other than making sure it is not marked ``final``.

One key aspect of inheritance is that it is transitive. Given three classes ``[X, Y, Z]``, if ``X`` extends ``Y``, and ``Y`` extends ``Z``, then ``X`` is considered a subclass or descendant of ``Z``. Likewise, ``Z`` is a superclass or ancestor of ``X``. We sometimes use the term direct subclass or descendant to indicate the class directly extends the parent class. For example, ``X`` is a direct descendant only of class ``Y``, not ``Z``.

**==When one class inherits from a parent class, all ``public`` and ``protected`` members are automatically available as part of the child class. If the two classes are in the same package, then package members are available to the child class. Last but not least, ``private`` members are restricted to the class they are defined in and are never available via inheritance.==**

```java
public class BigCat {
	protected double size;
}
public class Jaguar extends BigCat {
	public Jaguar() {
		size = 10.2;
	}
	public void printDetails() {
		System.out.print(size);
	}
}

public class Spider {
	public void printDetails() {
		System.out.println(size); // DOES NOT COMPILE
	}
}
```

``Jaguar`` is a subclass or child of ``BigCat``, making ``BigCat`` a superclass or parent of ``Jaguar``. In the ``Jaguar`` class, size is accessible because it is marked ``protected``. Via inheritance, the ``Jaguar`` subclass can read or write size as if it were its own member. Contrast this with the ``Spider`` class, which has no access to size since it is not inherited
### Class Modifiers

| Modifier   | Description                                                          |
| ---------- | -------------------------------------------------------------------- |
| final      | The class may not be extended.                                       |
| abstract   | The class is abstract, may contain abstract methods, and requires a  |
|            | concrete subclass to instantiate.                                    |
| sealed     | The class may only be extended by a specific list of classes.        |
| non-sealed | A subclass of a sealed class permits potentially unnamed subclasses. |
| static     | Used for static nested classes defined within a class.               |
**==The ``final`` modifier prevents a class from being extended any further.==**

```java
public final class Rhinoceros extends Mammal { }
public class Clara extends Rhinoceros { } // DOES NOT COMPILE
```

### Single vs. Multiple Inheritance

Java supports single inheritance, by which a class may inherit from only one direct parent class. Java also supports **==multiple levels of inheritance==**, by which one class may extend another class, which in turn extends another class. You can have any number of levels of inheritance, allowing each descendant to gain access to its ancestor’s members.

By design, Java doesn’t support multiple inheritance in the language because multiple inheritance can lead to complex, often difficult-to-maintain data models. Java does allow one exception to the single inheritance rule, which a class may implement multiple interfaces.

![[Pasted image 20240322193445.png]]

Part of what makes multiple inheritance complicated is determining which parent to inherit values from in case of a conflict. For example, if you have an object or method defined in all of the parents, which one does the child inherit? There is no natural ordering for parents in this example, which is why Java avoids these issues by disallowing multiple inheritance altogether.
### Inheriting Object

In Java, all classes inherit from a single class: ``java.lang.Object``, or ``Object`` for short. Furthermore, Object is the only class that doesn’t have a parent class. The following two are equivalent:

```java
public class Zoo { }
public class Zoo extends java.lang.Object { }
```

**==The key is that when Java sees you define a class that doesn’t extend another class, the compiler automatically adds the syntax extends ``java.lang.Object`` to the class definition.==** The result is that every class gains access to any accessible methods in the Object class. For example, the ``toString()`` and ``equals()`` methods are available in Object; therefore, they are accessible in all classes. Without being overridden in a subclass, though, they may not be particularly useful.

On the other hand, when you define a new class that extends an existing class, Java does not automatically extend the Object class. Since all classes inherit from Object, extending an existing class means the child already inherits from Object by definition.

						![[Pasted image 20240322194238.png]]


Primitive types such as ``int`` and ``boolean`` do not inherit from Object, since they are not classes. Through autoboxing they can be assigned or passed as an instance of an associated wrapper class, which does inherit ``Object``.

## Creating Classes

### Extending a Class

```java
// Animal.java
public class Animal {
	private int age;
	protected String name;
	public int getAge() {
		return age;
	}
	public void setAge(int newAge) {
		age = newAge;
	}
}
// Lion.java
public class Lion extends Animal {
	protected void setProperties(int age, String n) {
		setAge(age);
		name = n;
	}
	public void roar() {
		System.out.print(name + ", age " + getAge() + ", says: Roar!");
	}
	public static void main(String[] args) {
		var lion = new Lion();
		lion.setProperties(3, "kion");
		lion.roar(); // kion, age 3, says: Roar!
	}
}
```

- The ``age`` variable exists in the parent ``Animal`` class and is not directly accessible in the ``Lion`` child class. It is indirectly accessible via the ``setAge()`` method.
- The ``name`` variable is ``protected``, so it is inherited in the ``Lion`` class and directly accessible.
- create the ``Lion`` instance in the ``main()`` method and use ``setProperties()`` to set instance variables.
- Finally, call the ``roar()`` method,

The instance variable ``age`` is marked ``private`` and is not directly accessible from the subclass ``Lion``. Therefore, the following would not compile:

```java
public class Lion extends Animal {
	public void roar() {
		System.out.print("Lions age: " + age); // DOES NOT COMPILE
	}
}
```

**==Remember when working with subclasses that ``private`` members are never inherited, and package members are only inherited if the two classes are in the same package.==**
### Applying Class Access Modifiers

Like variables and methods, you can apply access modifiers to classes. **==A top-level class is one not defined inside**== ==**another class. Also a .java file can have at most one top-level class.==** While you can only have one top-level
class, you can have as many classes (in any order) with package access as you want

```java
// Bear.java
class Bird {}
class Bear {}
class Fish {}
```

Trying to declare a top-level class with ``protected`` or ``private`` class will lead to a compiler error,

```java
// ClownFish.java
protected class ClownFish{} // DOES NOT COMPILE
// BlueTang.java
private class BlueTang {} // DOES NOT COMPILE
```

### Accessing the ``this`` Reference

What happens when a method parameter has the same name as an existing instance variable ?

```java
public class Flamingo {
	private String color = null;
	public void setColor(String color) {
		color = color;
	}
	public static void main(String... unused) {
		var f = new Flamingo();
		f.setColor("PINK");
		System.out.print(f.color); // null
	}
}
```

Java uses the most granular scope, so when it sees ``color = color``, it thinks you are assigning the method parameter value to itself (not the instance variable). The assignment completes successfully within the method, but the value of the instance variable ``color`` is never modified and is ``null`` when printed in the ``main()`` method.

The fix **==when you have a local variable with the same name as an instance variable is to use the ``this`` reference or keyword. The this reference refers to the current instance of the class==** and can be used to access any member of the class, including inherited members. It can be used in any instance method, constructor, or instance initializer block. **==It cannot be used when there is no implicit instance of the class, such as in a static method or static initializer block.==**

```java
public void setColor(String color) {
	this.color = color; // Sets the instance variable with method parameter
}
```

In many cases, the ``this`` reference is optional. If Java encounters a variable or method it cannot find, it will check the class hierarchy to see if it is available.

```java
1: public class Duck {
	2: private String color;
	3: private int height;
	4: private int length;
5:
	6: public void setData(int length, int theHeight) {
		7: length = this.length; // Backwards --no good!
		8: height = theHeight; // Fine, because a different name
		9: this.color = "white"; // Fine, but this. reference not necessary
	10: }
11:
	12: public static void main(String[] args) {
		13: Duck b = new Duck();
		14: b.setData(1,2);
		15: System.out.print(b.length + " " + b.height + " " + b.color); // 0 2 white
	16: } }
```

- Line 7 is incorrect, and you should watch for it on the exam. The instance variable ``length`` starts out with a 0 value. That 0 is assigned to the method parameter ``length``. The instance variable stays at 0.
-  Line 8 is more straightforward. The parameter ``theHeight`` and instance variable ``height`` have different names. **==Since there is no naming collision, this is not required.==**
- line 9 shows that a variable assignment is allowed to use the this reference even when there is no duplication of variable names.
### Calling the ``super`` Reference

In Java, a variable or method can be defined in both a parent class and a child class. This means the object instance actually holds two copies of the same variable with the same underlying name. When this happens, how do we reference the version in the parent class instead of the current class?

```java
// Reptile.java
1: public class Reptile {
	2: protected int speed = 10;
3: }

// Crocodile.java
1: public class Crocodile extends Reptile {
	2: protected int speed = 20;
	3: public int getSpeed() {
		4: return speed;
	5: }
	
	6: public static void main(String[] data) {
		7: var croc = new Crocodile();
		8: System.out.println(croc.getSpeed()); // 20
	9: } 
}
```

**==One of the most important things to remember about this code is that an instance of ``Crocodile`` stores two separate values for ``speed``: one at the ``Reptile`` level and one at the ``Crocodile`` level==**. On line 4, Java first checks to see if there is a local variable or method parameter named ``speed``. Since there is not, it then checks ``this.speed;`` and since it exists, the program prints 20.

Within the ``Crocodile`` class, we can access the parent value of ``speed``, instead, by using the ``super`` reference or keyword. **==The ``super`` reference is similar to the this reference, except that it excludes any members found in the current class. In other words, the member must be accessible via inheritance.==**

```java
3: public int getSpeed() {
	4: return super.speed; // Causes the program to now print 10
5: }
```

```java
1: class Insect {
	2: protected int numberOfLegs = 4;
	3: String label = "buggy";
4: }
5:
6: public class Beetle extends Insect {
	7: protected int numberOfLegs = 6;
	8: short age = 3;
	9: public void printData() {
		10: System.out.println(this.label);
		11: System.out.println(super.label);
		12: System.out.println(this.age);
		13: System.out.println(super.age);
		14: System.out.println(numberOfLegs);
	15: }
	16: public static void main(String []n) {
		17: new Beetle().printData();
	18: }
19: }
```

this program code would not compile!

- Since ``label`` is defined in the parent class, it is accessible via both ``this`` and ``super`` references. For this reason, lines 10 and 11 compile and would both print buggy if the class compiled.
- the variable ``age`` is defined only in the current class, making it accessible via ``this`` but not ``super``. For this reason, line 12 compiles (and would print 3), but line 13 does not. **==while ``this`` includes current and inherited members, ``super`` only includes inherited members.==**
- Even though both ``numberOfLegs`` variables are accessible in ``Beetle``, **==Java checks outward, starting with the narrowest scope.==** For this reason, the value of ``numberOfLegs`` in the ``Beetle`` class is used, and 6 is printed.


**==Since ``this`` includes inherited members, you often only use ``super`` when you have a naming conflict via inheritance.==** For example, you have a method or variable defined in the current class that matches a method or variable in a parent class. This commonly comes up in method overriding and variable hiding
## Declaring Constructors

a constructor is a special method that matches the name of the class and has no return type. It is called when a new instance of the class is created.
### Creating a Constructor

```java
public class Bunny {
	public Bunny() {
		System.out.print("hop");
	}
}
```

The name of the constructor, ``Bunny``, matches the name of the class, ``Bunny``, and there is no return type, not even ``void``. That makes this a constructor.

```java
public class Bunny {
	public bunny() {} // DOES NOT COMPILE
	public void Bunny() {}
}
```

The first one doesn’t match the class name because Java is case-sensitive. Since it doesn’t match, Java knows it can’t be a constructor and is supposed to be a regular method. However, it is missing the return type and doesn’t compile. The second method is a perfectly good method but is not a constructor because it has a return type. **==Like method parameters, constructor parameters can be any valid class, array, or primitive type, including generics, but may not include ``var``==**. For example, the following does not compile:

```java
public class Bonobo {
	public Bonobo(var food) { // DOES NOT COMPILE
	}
}
```

**==A class can have multiple constructors, as long as each constructor has a unique constructor signature==**. In this case, that means ==**the constructor parameters must be distinct**==. Like methods with the same name but different signatures, declaring multiple constructors with different signatures is referred to as constructor overloading.

```java
public class Turtle {
	private String name;
	public Turtle() {
		name = "John Doe";
	}
	public Turtle(int age) {}
	public Turtle(long age) {}
	public Turtle(String newName, String... favoriteFoods) {
		name = newName;
	}
}
```

Constructors are used when creating a new object. This process is called instantiation because it creates a new instance of the class. A constructor is called when we write new followed by the name of the class we want to instantiate.

```java
new Turtle(15)
```

When Java sees the new keyword, it allocates memory for the new object. It then looks for a constructor with a matching signature and calls it.

### The Default Constructor

Every class in Java has a constructor, whether you code one or not. If you don’t include any constructors in the class, Java will create one for you without any parameters. This Java-created constructor is called the default constructor and is added any time a class is declared without any constructors.

```java
public class Rabbit {
	public static void main(String[] args) {
		new Rabbit(); // Calls the default constructor
	}
}
```

The previous class is equivalent to the following, in which the default constructor is provided and therefore not inserted by the compiler:

```java
public class Rabbit {
	public Rabbit() {}
	public static void main(String[] args) {
		new Rabbit(); // Calls the user-defined constructor
	}
}
```

This happens during the compile step. **==For the exam, one of the most important rules you need to know is that the compiler only inserts the default constructor when no constructors are defined.==**

```java
public class Rabbit1 {} // Valid No Args Ctor

public class Rabbit2 {
	public Rabbit2() {}
}
public class Rabbit3 {
	public Rabbit3(boolean b) {}
}
public class Rabbit4 {
	private Rabbit4() {}
}
```

```java
1: public class RabbitsMultiply {
	2: public static void main(String[] args) {
		3: var r1 = new Rabbit1();
		4: var r2 = new Rabbit2();
		5: var r3 = new Rabbit3(true);
		6: var r4 = new Rabbit4(); // DOES NOT COMPILE
	7: } }
```

Line 6 does not compile. ``Rabbit4`` made the constructor ``private`` so that other classes could not call it.

---

**Having only private constructors in a class tells the compiler not to provide a default no-argument constructor. It also prevents other classes from instantiating the class**

---
###  Calling Overloaded Constructors with ``this()``

Since a class can contain multiple overloaded constructors, these constructors can actually call one another.

```java
public class Hamster {
	private String color;
	private int weight;
	public Hamster(int weight, String color) { // First constructor
		this.weight = weight;
		this.color = color;
	}
	public Hamster(int weight) { // Second constructor
		this.weight = weight;
		color = "brown";
	}
}
```

One of the constructors takes a single ``int`` parameter. The other takes an ``int`` and a ``String``. These parameter lists are different, so the constructors are successfully overloaded. There is a bit of duplication, as ``this.weight`` is assigned the same way in both constructors. What we really want is for the first constructor to call the second constructor with two parameters.

```java
public Hamster(int weight) { // Second constructor
	Hamster(weight, "brown"); // DOES NOT COMPILE
}
```

This will not work. Constructors can be called only by writing new before the name of the constructor. They are not like normal methods that you can just call

```java
public Hamster(int weight) { // Second constructor
	new Hamster(weight, "brown"); // Compiles, but creates an extra object
}
```

This attempt does compile. When this constructor is called, it creates a new object with the default ``weight`` and ``color``. It then constructs a different object with the desired ``weight`` and ``color``.

Java provides a solution: ``this()`` When ``this()`` is used with parentheses, Java calls another constructor on the same instance of the class.

```java
public Hamster(int weight) { // Second constructor
	this(weight, "brown");
}
```

Now Java calls the constructor that takes two parameters, with ``weight`` and ``color`` set as expected.

---
**``this`` vs. ``this()``** #TIP 

**Despite using the same keyword, ``this`` and ``this()`` are very different. ==The first, this, refers to an instance of the class, while the second, this(), refers to a constructor call within the class==.**

---

**==Calling ``this()`` has one special rule you need to know. If you choose to call it, the`` this()`` call must be the first statement in the constructor. The side effect of this is that there can be only one call to ``this()`` in any constructor.==**

```java
3: public Hamster(int weight) {
4: System.out.println("chew");
5: // Set weight and default color
6: this(weight, "brown"); // DOES NOT COMPILE
7: }
```

There’s one last rule for overloaded constructors

```java
public class Gopher {
	public Gopher(int dugHoles) {
		this(5); // DOES NOT COMPILE
	}
}
```

**==The compiler is capable of detecting that this constructor is calling itself infinitely. This is often referred to as a cycle and is similar to the infinite loops Since the code can never terminate, the compiler stops and reports this as an error.==**

```java
public class Gopher {
	public Gopher() {
		this(5); // DOES NOT COMPILE
	}
	public Gopher(int dugHoles) {
		this(); // DOES NOT COMPILE
	}
}
```

the constructors call each other, and the process continues infinitely. Since the compiler can detect this, it reports an error.

- ==**A class can contain many overloaded constructors, provided the signature for each is distinct.**==
- ==**The compiler inserts a default no-argument constructor if no constructors are declared.**==
- ==**If a constructor calls ``this()``, then it must be the first line of the constructor.**==
- ==**Java does not allow cyclic constructor calls.==**

### Calling Parent Constructors with ``super()``

**==The first statement of every constructor is a call to a parent constructor using ``super()`` or another constructor in the class using ``this()``.==**

```java
public class Animal {
	private int age;
	public Animal(int age) {
		super(); // Refers to constructor in java.lang.Object
		this.age = age;
	}
}
	public class Zebra extends Animal {
		public Zebra(int age) {
		super(age); // Refers to constructor in Animal
	}
	public Zebra() {
		this(4); // Refers to constructor in Zebra with int argument
	}
}
```

---
**``super`` vs. ``super()``** #TIP

**Like ``this`` and ``this()``, ``super`` and ``super()`` are unrelated in Java. ==The first, ``super``, is used to reference members of the parent class, while the second, ``super()``, calls a parent constructor.**==

---
**==Like calling ``this()``, calling ``super()`` can only be used as the first statement of the constructor.==**

```java
public class Zoo {
	public Zoo() {
		System.out.println("Zoo created");
		super(); // DOES NOT COMPILE
	}
}
public class Zoo {
	public Zoo() {
		super();
		System.out.println("Zoo created");
		super(); // DOES NOT COMPILE
	}
}
```

If the parent class has more than one constructor, the child class may use any valid parent constructor in its definition

```java
public class Animal {
	private int age;
	private String name;
	public Animal(int age, String name) {
		super();
		this.age = age;
		this.name = name;
	}
	public Animal(int age) {
		super();
		this.age = age;
		this.name = null;
	}
}
public class Gorilla extends Animal {
	public Gorilla(int age) {
		super(age,"Gorilla"); // Calls the first Animal constructor
	}
	public Gorilla() {
		super(5); // Calls the second Animal constructor
	}
}
```

notice that the child constructors are not required to call matching parent constructors. Any valid parent constructor is acceptable as long as the appropriate input parameters to the parent constructor are provided.

### Understanding Compiler Enhancements

the Java compiler automatically inserts a call to the no-argument constructor ``super()`` if you do not explicitly call ``this()`` or ``super()`` as the first line of a constructor.

```java
public class Donkey {}

public class Donkey {
	public Donkey() {}
}

public class Donkey {
	public Donkey() {
		super();
	}
}
```

### Default Constructor Tips and Tricks

What happens if we define a subclass with no constructors, or a subclass with a constructor that doesn’t include a ``super()`` reference?

```java
public class Mammal {
	public Mammal(int age) {}
}
public class Seal extends Mammal {} // DOES NOT COMPILE
public class Elephant extends Mammal {
	public Elephant() {} // DOES NOT COMPILE
}
```

The answer is that neither subclass compiles. Since ``Mammal`` defines a constructor, the compiler does not insert a no-argument constructor. The compiler will insert a default no-argument constructor into ``Seal``, though, but it will be a simple implementation that just calls a nonexistent parent default constructor.

```java
public class Seal extends Mammal {
	public Seal() {
		super(); // DOES NOT COMPILE
	}
}
```

Likewise, ``Elephant`` will not compile for similar reasons. The compiler doesn’t see a call to ``super()`` or ``this()`` as the first line of the constructor so it inserts a call to a nonexistent no-argument ``super()`` automatically.

```java
public class Elephant extends Mammal {
	public Elephant() {
		super(); // DOES NOT COMPILE
	}
}
```

the compiler will not help, and you must create at least one constructor in your child class that explicitly calls a parent constructor via the ``super()`` command.

```java
public class Seal extends Mammal {
	public Seal() {
		super(6); // Explicit call to parent constructor
	}
}
public class Elephant extends Mammal {
	public Elephant() {
		super(4); // Explicit call to parent constructor
	}
}
```

Subclasses may include no-argument constructors even if their parent classes do not

---
**``super()`` Always Refers to the Most Direct Parent**
**A class may have multiple ancestors via inheritance. For constructors, though, ``super()`` always refers to the most direct parent.**

---

- ==**The first line of every constructor is a call to a parent constructor using ``super()`` or an overloaded constructor using ``this()``.**==
- ==**If the constructor does not contain a ``this()`` or ``super()`` reference, then the compiler automatically inserts super() with no arguments as the first line of the constructor.**==
- ==**If a constructor calls ``super()``, then it must be the first line of the constructor.==**

## Initializing Objects

Order of initialization refers to how members of a class are assigned values. They can be given default values, like 0 for an ``int``, or require explicit values, such as for ``final`` variables.
### Initializing Classes

First, we initialize the class, which involves invoking all ``static`` members in the class hierarchy, starting with the highest superclass and working downward. This is sometimes referred to as loading the class. The Java Virtual Machine (JVM) controls when the class is initialized, although you can assume the class is loaded before it is used. The class may be initialized when the program first starts, when a ``static`` member of the class is referenced, or shortly before an instance of the class is created.

**==One of the most important rules with class initialization is that it happens at most once for each class.==**

**Initialize Class X**

1. ==**If there is a superclass ``Y`` of ``X``, then initialize class ``Y`` first.**==
2. ==**Process all ``static`` variable declarations in the order in which they appear in the class.**==
3. ==**Process all ``static`` initializers in the order in which they appear in the class.==**

```java
public class Animal {
	static { System.out.print("A"); }
}
public class Hippo extends Animal {
	public static void main(String[] grass) {
		System.out.print("C");
		new Hippo();
		new Hippo();
		new Hippo();
	}
	static { System.out.print("B"); }
}
```

It prints ``ABC`` exactly once. Since the ``main()`` method is inside the ``Hippo`` class, the class will be initialized first, starting with the superclass and printing AB. Afterward, the ``main()`` method is executed, printing C. Even though the ``main()`` method creates three instances, the class is loaded only once.

### Initializing ``final`` Fields

**==A default value is only applied to a non-final field==**

``final static`` variables must be explicitly assigned a value exactly once. Fields marked ``final`` follow similar rules. They can be assigned values in the line in which they are declared or in an instance initializer.

```java
public class MouseHouse {
	private final int volume;
	private final String name = "The Mouse House"; // Declaration assignment
	{
		volume = 10; // Instance initializer assignment
	}
}
```
 
 Unlike ``static`` class members, though, ``final`` instance fields can also be set in a constructor. The constructor is part of the initialization process, so it is allowed to assign ``final`` instance variables. **==one important rule: by the time the constructor completes, all ``final`` instance variables must be assigned a value exactly once.==**

```java
public class MouseHouse {
	private final int volume;
	private final String name;
	public MouseHouse() {
		this.name = "Empty House"; // Constructor assignment
	}
	{
		volume = 10; // Instance initializer assignment
	}
}
```

Unlike local ``final`` variables, which are not required to have a value unless they are actually used, ``final`` instance variables must be assigned a value. If they are not assigned a value when they are declared or in an instance initializer, then they must be assigned a value in the constructor declaration. Failure to do so will result in a compiler error

```java
public class MouseHouse {
	private final int volume;
	private final String type;
	{
		this.volume = 10;
	}
	public MouseHouse(String type) {
		this.type = type;
	}
	public MouseHouse() { // DOES NOT COMPILE
		this.volume = 2; // DOES NOT COMPILE
	}
}
```

**==In terms of assigning values, each constructor is reviewed individually==**, which is why the second constructor does not compile. First, the constructor fails to set a value for the type variable. The compiler detects that a value is never set for type and reports an error on the line where the constructor is declared. Second, the constructor sets a value for the volume variable, even though it was already assigned a value by the instance initializer.

---

**On the exam, be wary of any instance variables marked ``final``. Make sure they are assigned a value in the line where they are declared, in an instance initializer, or in a constructor. They should be assigned a value only once, and failure to assign a value is considered a compiler error in the constructor.**

---

What about ``final`` instance variables when a constructor calls another constructor in the same class? In that case, you have to follow the flow carefully, making sure every ``final`` instance variable is assigned a value exactly once.

```java
public MouseHouse() {
	this(null);
}
```

can assign a ``null`` value to ``final`` instance variables as long as they are explicitly set.

### Initializing Instances

First, start at the lowest-level constructor where the ``new`` keyword is used. Remember, the first line of every constructor is a call to ``this()`` or ``super()``, and if omitted, the compiler will automatically insert a call to the parent no-argument constructor ``super()``. Then, progress upward and note the order of constructors. Finally, initialize each class starting with the superclass, processing each instance initializer and constructor in the reverse order in which it was called.

**Initialize Instance of X**

1. ==**Initialize class ``X`` if it has not been previously initialized.**==
2. ==**If there is a superclass ``Y`` of ``X``, then initialize the instance of ``Y`` first.**==
3. ==**Process all instance variable declarations in the order in which they appear in the class.**==
4. ==**Process all instance initializers in the order in which they appear in the class.**==
5. ==**Initialize the constructor, including any overloaded constructors referenced with ``this()``==**

```java
1: public class ZooTickets {
2: private String name = "BestZoo";
3: { System.out.print(name + "-");}
4: private static int COUNT = 0;
5: static { System.out.print(COUNT + "-");}
6: static { COUNT += 10; System.out.print(COUNT + "-");}
7:
8: public ZooTickets() {
	9: System.out.print("z-");
10: }
11:
12: public static void main(String... patrons) {
	13: new ZooTickets();
	// 0-10-BestZoo-z-
14: } }
```

- First, have to initialize the class. Since there is no superclass declared, which means the superclass is ``Object`` we can start with the ``static`` components of ``ZooTickets`` In this case, lines 4, 5, and 6 are executed, printing 0-and 10-
- Next, we initialize the instance created on line 13. Again, since no superclass is declared, we start with the instance components. Lines 2 and 3 are executed, which prints BestZoo- 
- Finally, we run the constructor on lines 8–10, which outputs z-.

```java
class Primate {
    public Primate() {
        System.out.print("Primate-");
    }
}

class Ape extends Primate {
    public Ape(int fur) {
        System.out.print("Ape1-");
    }

    public Ape() {
        System.out.print("Ape2-");
    }
}

public class Chimpanzee extends Ape {
    public Chimpanzee() {
        super(2);
        System.out.print("Chimpanzee-");
    }

    public static void main(String[] args) {
        new Chimpanzee(); // Primate-Ape1-Chimpanzee-
    }
}
```

The compiler inserts the ``super()`` command as the first statement of both the ``Primate`` and ``Ape`` constructors. The code will execute with the parent constructors called first

Notice that only one of the two ``Ape()`` constructors is called. You need to start with the call to ``new Chimpanzee()`` to determine which constructors will be executed. Remember, constructors are executed from the bottom up, but since the first line of every constructor is a call to another constructor, **==the flow ends up with the parent constructor executed before the child constructor.==**

```java
1: public class Cuttlefish {
	2: private String name = "swimmy";
	3: { System.out.println(name); }
	4: private static int COUNT = 0;
	5: static { System.out.println(COUNT); }
	6: { COUNT++; System.out.println(COUNT); }
	7:
	8: public Cuttlefish() {
		9: System.out.println("Constructor");
	10: }
	11:
	12: public static void main(String[] args) {
			13: System.out.println("Ready");
			14: new Cuttlefish();
15: } }
```

```text
0
Ready
swimmy
1
Constructor
```

- No superclass is declared, so we can skip any steps that relate to inheritance.
- first process the ``static`` variables and ``static`` initializers—lines 4 and 5, with line 5 printing 0.
- the ``main()`` method can run, which prints Ready.
- create an instance declared on line 14
- Lines 2, 3, and 6 are processed, with line 3 printing swimmy and line 6 printing 1.
- Finally, the constructor is run on lines 8–10, which prints Constructor.

```java
1: class GiraffeFamily {
	2: static { System.out.print("A"); }
	3: { System.out.print("B"); }
	4:
	5: public GiraffeFamily(String name) {
		6: this(1);
		7: System.out.print("C");
	8: }
	9:
	10: public GiraffeFamily() {
		11: System.out.print("D");
	12: }
	13:
	14: public GiraffeFamily(int stripes) {
		15: System.out.print("E");
	16: }
17: }
18: public class Okapi extends GiraffeFamily {
	19: static { System.out.print("F"); }
	20:
	21: public Okapi(int stripes) {
		22: super("sugar");
		23: System.out.print("G");
	24: }
	25: { System.out.print("H"); }
	26:
	27: public static void main(String[] grass) {
		28: new Okapi(1);
		29: System.out.println();
		30: new Okapi(2);
	31: }
32: }
```

```text
AFBECHG
BECHG
```

- Start with initializing the ``Okapi`` class. Since it has a superclass ``GiraffeFamily``, initialize it first, printing A on line 2.
- Next, initialize the ``Okapi`` class, printing F on line 19.
- After the classes are initialized, execute the ``main()`` method on line 27. The first line of the ``main()`` method creates a new ``Okapi`` object, triggering the instance initialization process. Per the first rule, the superclass instance of ``GiraffeFamily`` is initialized first. Per our third rule, the instance initializer in the superclass ``GiraffeFamily`` is called, and B is printed on line 3.
- Per the fourth rule, we initialize the constructors. In this case, this involves calling the constructor on line 5, which in turn calls the overloaded constructor on line 14. The result is that EC is printed, as the constructor bodies are unwound in the reverse order that they were called.
- The process then continues with the initialization of the ``Okapi`` instance itself. Per the third and fourth rules, H is printed on line 25, and G is printed on line 23, respectively
- Line 29 then inserts a line break in the output.
- Finally, line 30 initializes a new ``Okapi`` object. The order and initialization are the same as line 28, sans the class initialization, so BECHG is printed again. Notice that D is never printed, as only two of the three constructors in the superclass ``GiraffeFamily`` are called.

This example is tricky for a few reasons. There are multiple overloaded constructors, lots of initializers, and a complex constructor pathway to keep track of. Luckily, questions like this are uncommon on the exam. If you see one, just write down what is going on as you read the code.

- ==**A class is initialized at most once by the JVM before it is referenced or used.**==
- ==**All ``static final`` variables must be assigned a value exactly once, either when they are declared or in a ``static`` initializer.**==
- ==**All ``final`` fields must be assigned a value exactly once, either when they are declared, in an instance initializer, or in a constructor.**==
- ==**Non-final static and instance variables defined without a value are assigned a default value based on their type.**==
- ==**Order of initialization is as follows: variable declarations, then initializers, and finally constructors.==**
## Inheriting Members

Inheriting a class not only grants access to inherited methods in the parent class but also sets the stage for collisions between methods defined in both the parent class and the subclass
### Overriding a Method

In Java, overriding a method occurs when a subclass declares a new implementation for an inherited method with the same signature and compatible return type.

When you override a method, you may still reference the parent version of the method using the ``super`` keyword. In this manner, the keywords ``this`` and ``super`` allow you to select between the current and parent versions of a method, respectively

```java
public class Marsupial {
	public double getAverageWeight() {
		return 50;
	}
}
public class Kangaroo extends Marsupial {
	public double getAverageWeight() {
	return super.getAverageWeight()+20;
}
public static void main(String[] args) {
	System.out.println(new Marsupial().getAverageWeight()); // 50.0
	System.out.println(new Kangaroo().getAverageWeight()); // 70.0
	}
}
```

the ``Kangaroo`` class overrides the ``getAverageWeight()`` method but in the process calls the parent version using the ``super`` reference.

---

**Method Overriding Infinite Calls**

```java
public double getAverageWeight() {
	return getAverageWeight()+20; // StackOverflowError
}
```

In this example, the compiler would not call the parent ``Marsupial`` method; it would call the current ``Kangaroo`` method. The application will attempt to call itself infinitely and produce a ``StackOverflowError`` at runtime.

---

To override a method, you must follow a number of rules. The compiler performs the following checks when you override a method:

1. ==**The method in the child class must have the same signature as the method in the parent class.**==
2. ==**The method in the child class must be at least as accessible as the method in the parent class.**==
3. ==**The method in the child class may not declare a checked exception that is new or broader than the class of any exception declared in the parent class method.**==
4. ==**If the method returns a value, it must be the same or a subtype of the method in the parent class, known as covariant return types.==**
#### Rule #1: Method Signatures

If two methods have the same name but different signatures, the methods are overloaded, not overridden. Overloaded methods are considered independent and do not share the same polymorphic properties as overridden methods.
#### Rule #2: Access Modifiers

```java
public class Camel {
	public int getNumberOfHumps() {
	return 1;
	} }
	public class BactrianCamel extends Camel {
	private int getNumberOfHumps() { // DOES NOT COMPILE
	return 2;
} }
```

**==Java avoids these types of ambiguity problems by limiting overriding a method to access modifiers that are as accessible or more accessible than the version in the inherited method.==**
#### Rule #3: Checked Exceptions

Overriding a method cannot declare new checked exceptions or checked exceptions broader than the inherited method. In other words, you could end up with an object that is more restrictive than the reference type it is assigned to, resulting in a checked exception that is not handled or declared.

```java
public class Reptile {
	protected void sleep() throws IOException {}
	protected void hide() {}
	protected void exitShell() throws FileNotFoundException {}
}
public class GalapagosTortoise extends Reptile {
	public void sleep() throws FileNotFoundException {}
	public void hide() throws FileNotFoundException {} // DOES NOT COMPILE
	public void exitShell() throws IOException {} // DOES NOT COMPILE
}
```

These overridden methods use the more accessible ``public`` modifier, which is allowed per our second rule for overridden methods. 

The overridden`` hide()`` method does not compile because it declares a new checked exception not present in the parent declaration. The overridden ``exitShell()`` also does not compile, since ``IOException`` is a broader checked exception than ``FileNotFoundException``
#### Rule #4: Covariant Return Types

```java
public class Rhino {
	protected CharSequence getName() {
		return "rhino";
	}
	protected String getColor() {
		return "grey, black, or white";
	} 
}
public class JavanRhino extends Rhino {
	public String getName() {
		return "javan rhino";
	}
	public CharSequence getColor() { // DOES NOT COMPILE
		return "grey";
	} 
}
```

- ``String`` implements the ``CharSequence`` interface, making ``String`` a subtype of ``CharSequence``. Therefore, the return type of ``getName()`` in ``JavanRhino`` is covariant with the return type of ``getName()`` in ``Rhino``.
- the overridden ``getColor()`` method does not compile because ``CharSequence`` is not a subtype of ``String``. To put it another way, all ``String`` values are ``CharSequence`` values, but not all ``CharSequence`` values are ``String`` values. For instance, a ``StringBuilder`` is a ``CharSequence`` but not a ``String``.

---

**==A simple test for covariance is the following: given an inherited return type A and an overriding return type B, can you assign an instance of B to a reference variable for A without a cast? If so, then they are covariant. This rule applies to primitive types and object types alike. If one of the return types is ``void``, then they both must be ``void``, as nothing is covariant with void except itself==**

---
### Redeclaring ``private`` Methods

**==In Java, you can’t override ``private`` methods since they are not inherited.==** Just because a child class doesn’t have access to the parent method doesn’t mean the child class can’t define its own version of the method. It just means, strictly speaking, that the new method is not an overridden version of the parent class’s method.

Java permits you to redeclare a new method in the child class with the same or modified signature as the method in the parent class. This method in the child class is a separate and independent method, unrelated to the parent version’s method, so none of the rules for overriding methods is invoked.

```java
public class Beetle {
private String getSize() {
return "Undefined";
} }

public class RhinocerosBeetle extends Beetle {
private int getSize() {
return 5;
} }
```

What if ``getSize()`` method was declared ``public`` in ``Beetle``? In this case, the method in ``RhinocerosBeetle`` would be an invalid override. The access modifier in ``RhinocerosBeetle`` is more restrictive, and the return types are not covariant.

### Hiding Static Methods

**==A ``static`` method cannot be overridden because class objects do not inherit from each other in the same way as instance objects. On the other hand, they can be hidden. A hidden method occurs when a child class defines a static method with the same name and signature as an inherited ``static`` method defined in a parent class==**. Method hiding is similar to but not exactly the same as method overriding. The previous four rules for overriding a method must be followed when a method is hidden. In addition, a new fifth rule is added for hiding a method:

5. **==The method defined in the child class must be marked as ``static`` if it is marked as ``static`` in a parent class.==**

Put simply, it is method hiding if the two methods are marked ``static`` and method overriding if they are not marked ``static``. If one is marked ``static`` and the other is not, the class will not compile.

```java
public class Bear {
public static void eat() {
System.out.println("Bear is eating");
} }
public class Panda extends Bear {
public static void eat() {
System.out.println("Panda is chewing");
}
public static void main(String[] args) {
eat();
} }
```

- The ``eat()`` method in the ``Panda`` class hides the ``eat()`` method in the ``Bear`` class, printing "Panda is chewing" at runtime. Because they are both marked as ``static``, this is not considered an overridden method. If you remove the ``eat()`` declaration in the ``Panda`` class, then the program prints "Bear is eating" instead.

```java
public class Bear {
    public static void sneeze() {
        System.out.println("Bear is sneezing");
    }

    public void hibernate() {
        System.out.println("Bear is hibernating");
    }

    public static void laugh() {
        System.out.println("Bear is laughing");
    }
}

public class SunBear extends Bear {
    public void sneeze() { // DOES NOT COMPILE
        System.out.println("Sun Bear sneezes quietly");
    }

    public static void hibernate() { // DOES NOT COMPILE
        System.out.println("Sun Bear is going to sleep");
    }

    protected static void laugh() { // DOES NOT COMPILE
        System.out.println("Sun Bear is laughing");
    }
}
```

- ``sneeze()`` is marked ``static`` in the parent class but not in the child class. The compiler detects that you’re trying to override using an instance method. However, ``sneeze()`` is a ``static`` method that should be hidden, causing the compiler to generate an error
- The second method, ``hibernate()``, does not compile for the opposite reason. The method is marked ``static`` in the child class but not in the parent class.
- Finally, the ``laugh()`` method does not compile. Even though both versions of the method are marked ``static``, the version in ``SunBear`` has a more restrictive access modifier than the one it inherits, and it breaks the second rule for overriding methods

### Hiding Variables

Java doesn’t allow variables to be overridden. Variables can be hidden, though. **==A hidden variable occurs when a child class defines a variable with the same name as an inherited variable defined in the parent class==**
As when hiding a ``static`` method, you can’t override a variable; you can only hide it.

```java
class Carnivore {
	protected boolean hasFur = false;
}
public class Meerkat extends Carnivore {
	protected boolean hasFur = true;
	public static void main(String[] args) {
		Meerkat m = new Meerkat();
		Carnivore c = m;
		System.out.println(m.hasFur); // true
		System.out.println(c.hasFur); // false
	}
}
```

Both of these classes define a ``hasFur`` variable, but with different values. Even though only one object is created by the ``main()`` method, both variables exist independently of each other. The output changes depending on the reference variable used.

### Writing ``final`` Methods

**==final methods cannot be overridden. By marking a method ``final``, you forbid a child class from replacing this method==**. This rule is in place both when you override a method and when you hide a method.

```java
public class Bird {
	public final boolean hasFeathers() {
		return true;
	}
	public final static void flyAway() {}
}
public class Penguin extends Bird {
	public final boolean hasFeathers() { // DOES NOT COMPILE
		return false;
	}
	public final static void flyAway() {} // DOES NOT COMPILE
}
```

This rule applies only to inherited methods. For example, if the two methods were marked ``private`` in the parent ``Bird`` class, then the ``Penguin`` class, as defined, would compile.
## Creating Abstract Classes

### Introducing Abstract Classes

**==An abstract class is a class declared with the ``abstract`` modifier that cannot be instantiated directly and may contain abstract methods.==**

```java
public abstract class Canine {}
public class Wolf extends Canine {}
public class Fox extends Canine {}
public class Coyote extends Canine {}
```

An abstract class can contain abstract methods. An abstract method is a method declared with the ``abstract`` modifier that does not define a body. Put another way, an abstract method forces subclasses to override the method. By declaring a method abstract, we can guarantee that some version will be available on an instance without having to specify what that version is in the abstract parent class.

```java
public abstract class Canine {
public abstract String getSound();
public void bark() { System.out.println(getSound()); }
}
public class Wolf extends Canine {
public String getSound() {
return "Wooooooof!";
} }
public class Fox extends Canine {
public String getSound() {
return "Squeak!";
} }
public class Coyote extends Canine {
public String getSound() {
return "Roar!";
} }
```

```java
public static void main(String[] p) {
	Canine w = new Fox();
	w.bark(); // Squeak!
}
```

there are some rules you need to be aware of:

-  ==**Only instance methods can be marked ``abstract`` within a class, not variables, constructors, or ``static`` methods.**==
-  ==**An abstract method can only be declared in an abstract class.**==
-  ==**A non-abstract class that extends an abstract class must implement all inherited abstract methods.**==
-  ==**Overriding an abstract method follows the existing rules for overriding methods==**

```java
public class FennecFox extends Canine {
	public int getSound() {
	return 10;
} }
public class ArcticFox extends Canine {}
public class Direwolf extends Canine {
	public abstract rest();
	public String getSound() {
	return "Roof!";
} }

public class Jackal extends Canine {
	public abstract String name;
	public String getSound() {
	return "Laugh";
} }
```

- the ``FennecFox`` class does not compile because it is an invalid method override. The return types are not covariant
- The ``ArcticFox`` class does not compile because it does not override the abstract ``getSound()`` method.
- The ``Direwolf`` class does not compile because it is not abstract but declares an abstract method ``rest()``.
- the ``Jackal`` class does not compile because variables cannot be marked abstract.

```java
abstract class Alligator {
	public static void main(String... food) {
		var a = new Alligator(); // DOES NOT COMPILE
	}
}
```

An abstract class can be initialized, but only as part of the instantiation of a non-abstract subclass.

### Declaring Abstract Methods

**==An abstract method is always declared without a body. It also includes a semicolon (;) after the method declaration.==** An abstract class can include all of the same members as a non-abstract class, including variables, ``static`` and instance methods, constructors, etc. n abstract class is not required to include any abstract methods.

```java
public abstract class Llama {
	public void chew() {}
}
```

**==For the exam, keep an eye out for abstract methods declared outside abstract classes==**

```java
public class Egret { // DOES NOT COMPILE
	public abstract void peck();
}
```

Like the ``final`` modifier, the ``abstract`` modifier can be placed before or after the access modifier in class and method declarations

```java
abstract public class Tiger {
	abstract public int claw();
}
```

The ``abstract`` modifier cannot be placed after the class keyword in a class declaration or after the return type in a method declaration

```java
public class abstract Bear { // DOES NOT COMPILE
	public int abstract howl(); // DOES NOT COMPILE
}
```

### Creating a Concrete Class

A concrete class is a non-abstract class. **==The first concrete subclass that extends an abstract class is required to implement all inherited abstract methods==**. When you see a concrete class extending an abstract class on the exam, check to make sure that it implements all of the required abstract methods.

```java
public abstract class Animal {
	public abstract String getName();
}
public class Walrus extends Animal {} // DOES NOT COMPILE
```

An abstract class can extend a non-abstract class and vice versa. Anytime a concrete class is extending an abstract class, it must implement all of the methods that are inherited as abstract.

```java
public abstract class Mammal {
	abstract void showHorn();
	abstract void eatLeaf();
}
public abstract class Rhino extends Mammal {
	void showHorn() {} // Inherited from Mammal Because no abstract keyword start of the method
}
public class BlackRhino extends Rhino {
	void eatLeaf() {} // Inherited from Mammal
}
```

- the ``BlackRhino`` class is the first concrete subclass, while the ``Mammal`` and ``Rhino`` classes are abstract.
- The ``BlackRhino`` class inherits the`` eatLeaf()`` method as abstract and is therefore required to provide an implementation, which it does.
- ``showHorn()`` method. Since the parent class, ``Rhino``, provides an implementation of ``showHorn()``, the method is inherited in the ``BlackRhino`` as a non-abstract method. For this reason, the ``BlackRhino`` class is permitted but not required to override the ``showHorn()`` method.

```java
public class Rhino extends Mammal { // DOES NOT COMPILE
	void showHorn() {}
}
```

By changing ``Rhino`` to a concrete class, it becomes the first non-abstract class to extend the abstract ``Mammal`` class. Therefore, it must provide an implementation of both the ``showHorn()`` and ``eatLeaf()`` methods. Since it only provides one of these methods, the modified Rhino declaration does not compile.

```java
public abstract class Animal {
	abstract String getName();
}
public abstract class BigCat extends Animal {
	protected abstract void roar();
}

public class Lion extends BigCat {
	public String getName() {
		return "Lion";
	}
	public void roar() {
		System.out.println("The Lion lets out a loud ROAR!");
	}
}
```

- ``BigCat`` extends ``Animal`` but is marked as abstract; therefore, it is not required to provide an implementation for the ``getName()`` method
- The class ``Lion`` is not marked as ``abstract``, and as the first concrete subclass, it must implement all of the inherited abstract methods not defined in a parent class
###  Creating Constructors in Abstract Classes

Even though abstract classes cannot be instantiated, they are still initialized through constructors by their subclasses.

```java
abstract class Mammal {
	abstract CharSequence chew();
	public Mammal() {
		System.out.println(chew()); // Does this line compile?
	}
}
```

```java
public class Platypus extends Mammal {
	String chew() { return "yummy!"; }
	public static void main(String[] args) {
		new Platypus();
	}
}
```

For the exam, remember that abstract classes are initialized with constructors in the same way as non-abstract classes. For example, if an abstract class does not provide a constructor, the compiler will automatically insert a default no-argument constructor.

**==The primary difference between a constructor in an abstract class and a non-abstract class is that a constructor in an abstract class can be called only when it is being initialized by a non-abstract subclass==**

### Spotting Invalid Declarations

```java
public abstract class Turtle {
	public abstract long eat() // DOES NOT COMPILE
	public abstract void swim() {}; // DOES NOT COMPILE
	public abstract int getAge() { // DOES NOT COMPILE
	return 10;
	}
	public abstract void sleep; // DOES NOT COMPILE
	public void goInShell(); // DOES NOT COMPILE
}
```

- The first method, ``eat()``, does not compile because it is marked abstract but does not end with a semicolon (;).
- The next two methods, ``swim()`` and ``getAge()``, do not compile because they are marked abstract, but they provide an implementation block enclosed in braces ``({})``.
- The next method, ``sleep``, does not compile because it is missing parentheses, (), for method arguments.
- The last method, ``goInShell()``, does not compile because it is not marked ``abstract`` and therefore must provide a body enclosed in braces.

#### ``abstract`` and ``final`` Modifiers

If you mark something ``abstract``, you intend for someone else to extend or implement it. But if you mark something ``final``, you are preventing anyone from extending or implementing it. These concepts are in direct conflict with each other. Due to this incompatibility, **==Java does not permit a class or method to be marked both**==
==**``abstract`` and ``final``==**

```java
public abstract final class Tortoise { // DOES NOT COMPILE
	public abstract final void walk(); // DOES NOT COMPILE
}
```

#### ``abstract`` and ``private`` Modifiers

**==A method cannot be marked as both ``abstract`` and ``private``.==** the compiler will complain

```java
public abstract class Whale {
	private abstract void sing(); // DOES NOT COMPILE
}
public class HumpbackWhale extends Whale {
	private void sing() {
		System.out.println("Humpback whale is singing");
	} 
}
```

---

**While it is not possible to declare a method ``abstract`` and ``private``, ==it is possible (albeit redundant) to declare a method ``final`` and ``private``.**==

---

```java
public abstract class Whale {
	protected abstract void sing();
}
public class HumpbackWhale extends Whale {
	private void sing() { // DOES NOT COMPILE
		System.out.println("Humpback whale is singing");
	}
}
```

the code will still not compile, but for a completely different reason. the subclass cannot reduce the visibility of the parent method, ``sing()``.
#### ``abstract`` and ``static`` Modifiers

a ``static`` method can only be hidden, not overridden. It is defined as belonging to the class, not an instance of the class. **==If a ``static`` method cannot be overridden, then it follows that it also cannot be marked ``abstract`` since it can never be implemented.==**

```java
abstract class Hippopotamus {
	abstract static void swim(); // DOES NOT COMPILE
}
```

## Creating Immutable Objects

The immutable objects pattern is an object-oriented design pattern in which an object cannot be modified after it is created. Immutable objects are helpful when writing secure code because you don’t have to worry about the values changing. They also simplify code when dealing with concurrency since immutable objects can be easily shared between multiple threads.
### Declaring an Immutable Class

1. ==**Mark the class as ``final`` or make all of the constructors ``private``.**==
2. ==**Mark all the instance variables ``private`` and ``final``.**==
3. ==**Don’t define any setter methods.**==
4. ==**Don’t allow referenced mutable objects to be modified.==**

```java
import java.util.*;
public final class Animal { // Not an immutable object declaration
private final ArrayList<String> favoriteFoods;
public Animal() {
this.favoriteFoods = new ArrayList<String>();
this.favoriteFoods.add("Apples");
}
public List<String> getFavoriteFoods() {
return favoriteFoods;
} }
```

```java
var zebra = new Animal();
System.out.println(zebra.getFavoriteFoods()); // [Apples]
zebra.getFavoriteFoods().clear();
zebra.getFavoriteFoods().add("Chocolate Chip Cookies");
System.out.println(zebra.getFavoriteFoods()); // [Chocolate Chip Cookies]
```

```java
import java.util.*;
public final class Animal { // An immutable object declaration
private final List<String> favoriteFoods;
public Animal() {
this.favoriteFoods = new ArrayList<String>();
this.favoriteFoods.add("Apples");
}
public int getFavoriteFoodsCount() {
return favoriteFoods.size();
}
public String getFavoriteFoodsItem(int index) {
return favoriteFoods.get(index);
} }
```

---
**Copy on Read Accessor Methods**

**Besides delegating access to any ``private`` mutable objects, another approach is to make a copy of the mutable object any time it is requested.**

```java
public ArrayList<String> getFavoriteFoods() {
	return new ArrayList<String>(this.favoriteFoods);
}
```

**Of course, changes in the copy won’t be reflected in the original, but at least the original is**
**protected from external changes.**

---
### Performing a Defensive Copy

```java
import java.util.*;
public final class Animal { // Not an immutable object declaration
private final ArrayList<String> favoriteFoods;
public Animal(ArrayList<String> favoriteFoods) {
if (favoriteFoods == null || favoriteFoods.size() == 0)
throw new RuntimeException("favoriteFoods is required");
this.favoriteFoods = favoriteFoods;
}
public int getFavoriteFoodsCount() {
return favoriteFoods.size();
}
public String getFavoriteFoodsItem(int index) {
return favoriteFoods.get(index);
} }
```

```java
var favorites = new ArrayList<String>();
favorites.add("Apples");
var zebra = new Animal(favorites); // Caller still has access to favorites
System.out.println(zebra.getFavoriteFoodsItem(0)); // [Apples]
favorites.clear();
favorites.add("Chocolate Chip Cookies");
System.out.println(zebra.getFavoriteFoodsItem(0)); // [Chocolate Chip Cookies]
```

The solution is to make a copy of the list object containing the same elements.

```java
public Animal(List<String> favoriteFoods) {
	if (favoriteFoods == null || favoriteFoods.size() == 0)
	throw new RuntimeException("favoriteFoods is required");
	this.favoriteFoods = new ArrayList<String>(favoriteFoods);
}
```

The copy operation is called a defensive copy because the copy is being made in case other code does something unexpected. It’s the same idea as defensive driving: prevent a problem before it exists.

## Summary #OCP_Summary 

**==Java classes follow a single-inheritance pattern in which every class has exactly one direct parent class, with all classes eventually inheriting from ``java.lang.Object``. Inheriting a class gives you access to all of the ``public`` and ``protected`` members of the class. It also gives you access to package members of the class if the classes are in the same package. All instance methods, constructors, and instance initializers have access to two special reference variables: ``this`` and ``super``. Both ``this`` and ``super`` provide access to all inherited members, with only this providing access to all members in the current class declaration**==

==**Constructors are special methods that use the class name and do not have a return type. They are used to instantiate new objects. Declaring constructors requires following a number of important rules. If no constructor is provided, the compiler will automatically insert a default no-argument constructor in the class. The first line of every constructor is a call to an overloaded constructor, ``this()``, or a parent constructor, ``super()``; otherwise, the compiler will insert a call to super() as the first line of the constructor. In some cases, such as if the parent class does not define a no-argument constructor, this can lead to compilation errors. Pay close attention on the exam to any class that defines a constructor with arguments and doesn’t define a no-argument constructor.**==

==**Classes are initialized in a predetermined order: superclass initialization; ``static`` variables and ``static`` initializers in the order that they appear; instance variables and instance initializers in the order they appear; and finally, the constructor. All final instance variables must be assigned a value exactly once.**==

==**A method is overloaded if it has the same name but a different signature as another accessible method. A method is overridden if it has the same signature as an inherited method, with access modifiers, exceptions, and a return type that are compatible. A static method is hidden if it has the same signature as an inherited ``static`` method. Finally, a method is redeclared if it has the same name and possibly the same signature as an uninherited method.**==

==**abstract classes, which are just like regular classes except that they cannot be instantiated and may contain abstract methods. An abstract class can extend a non-abstract class and vice versa. Abstract classes can be used to define a framework that other developers write subclasses against. An abstract method is one that does not include a body when it is declared. An abstract method can only be placed inside an abstract class or interface. Next, an abstract method can be overridden with another abstract declaration or a concrete implementation, provided the rules for overriding methods are followed. The first concrete class must implement all of the inherited abstract methods, whether they are inherited from an abstract class or an interface.**==

==**immutable objects in Java. Although there are a number of different techniques to do so, we included the most common one you should know for the exam. Immutable objects are extremely useful in practice, especially in multi-threaded applications, since they do not change.==**

## Exam Essentials #Essential 

 **Be able to write code that extends other classes**. A Java class that extends another class inherits all of its ``public`` and ``protected`` methods and variables. If the class is in the same package, it also inherits all package members of the class. **==Classes that are marked final ``cannot`` be extended==**. Finally, all classes in Java extend ``java.lang.Object`` either directly or from a superclass.

**Be able to distinguish and use ``this``, ``this()``, ``super``, and ``super()``**. To access a current or inherited member of a class, the ``this`` reference can be used. To access an inherited member, the ``super`` reference can be used. The ``super`` reference is often used to reduce ambiguity, such as when a class reuses the name of an inherited method or variable. The calls to ``this()`` and ``super()`` are used to access constructors in the same class and parent class, respectively.


**Evaluate code involving constructors**. The first line of every constructor is a call to another constructor within the class using ``this()`` or a call to a constructor of the parent class using the ``super()`` call. The compiler will insert a call to ``super()`` if no constructor call is declared. If the parent class doesn’t contain a no-argument constructor, an explicit call to the parent constructor must be provided. Be able to recognize when the default constructor is provided. Remember that the order of initialization is to initialize all classes in the class hierarchy, starting with the superclass. Then the instances are initialized, again starting with the superclass. All final variables must be assigned a value exactly once by the time the constructor is finished.

**Understand the rules for method overriding**. Java allows methods to be overridden, or replaced, by a subclass if certain rules are followed: **==a method must have the same signature, be at least as accessible as the parent method, must not declare any new or broader exceptions, and must use covariant return types==**. **==Methods marked ``final`` may not be overridden or hidden.==**

**Recognize the difference between method overriding and method overloading.** Both method overloading and overriding involve creating a new method with the same name as an existing method. When the method signature is the same, it is referred to as method overriding and must follow a specific set of override rules to compile. When the method signature is different, with the method taking different inputs, it is referred to as method overloading, and none of the override rules are required. Method overriding is important to polymorphism because it replaces all calls to the method, even those made in a superclass.

**Understand the rules for hiding methods and variables**. When a ``static`` method is overridden in a subclass, it is referred to as method hiding. Likewise, variable hiding is when an inherited variable name is reused in a subclass. In both situations, the original method or variable still exists and is accessible depending on where it is accessed and the reference type used. For method hiding, the use of ``static`` in the method declaration must be the same between the parent and child class. Finally, variable and method hiding should generally be avoided since it leads to confusing and difficult-to- follow code.

**Be able to write code that creates and extends abstract classes**. In Java, classes and methods can be declared as ``abstract``. An ``abstract`` class cannot be instantiated. An instance of an ``abstract`` class can be obtained only through a concrete subclass. Abstract classes can include any number of ``abstract`` and non-abstract methods, including zero. Abstract methods follow all the method override rules and may be defined only within ``abstract`` classes. **==The first concrete subclass of an abstract class must implement all the inherited methods. Abstract classes and methods may not be marked as ``final``==**.

**Create immutable objects.** An immutable object is one that cannot be modified after it is declared. An immutable class is commonly implemented with a private constructor, no setter methods, and no ability to modify mutable objects contained within the class.

## Review Questions

1. Which code can be inserted to have the code print 2?

```java
public class BirdSeed {
private int numberBags;
boolean call;
public BirdSeed() {
// LINE 1
call = false;
// LINE 2
}
public BirdSeed(int numberBags) {
this.numberBags = numberBags;
}
public static void main(String[] args) {
var seed = new BirdSeed();
System.out.print(seed.numberBags);
} }
```

A. Replace line 1 with BirdSeed(2);.
B. Replace line 2 with BirdSeed(2);.
C. Replace line 1 with new BirdSeed(2);.
D. Replace line 2 with new BirdSeed(2);.
E. Replace line 1 with this(2);.
F. Replace line 2 with this(2);.
G. The code prints 2 without any changes.

**My Answer: E**
**Correct Answer: E**

**A and B will not compile because constructors cannot be called without new. Options C and D will compile but will create a new object rather than setting the fields in this one. The result is the program will print 0, not 2, at runtime. Calling an overloaded constructor, using this(), or a parent constructor, using super(), is only allowed on the first line of the constructor, making option E correct and option F incorrect.**

---

2. Which modifier pairs can be used together in a method declaration? (Choose all that apply.)
A. static and final
B. private and static
C. static and abstract
D. private and abstract
E. abstract and final
F. private and final

**My Answer: A,F**
**Correct Answer: A,B,F**

**The final modifier can be used with private and static, making options A and F correct. Marking a private method final is redundant but allowed. A private method may also be marked static, making option B correct.**

---

3. Which of the following statements about methods are true? (Choose all that apply.)

A. Overloaded methods must have the same signature.
B. Overridden methods must have the same signature.
C. Hidden methods must have the same signature.
D. Overloaded methods must have the same return type.
E. Overridden methods must have the same return type.
F. Hidden methods must have the same return type.

**My Answer: B,C**
**Correct Answer: B,C**

**Overloaded methods have the same method name but a different signature (the method parameters differ), making option A incorrect. Overridden instance methods and hidden static methods must have the same signature (the name and method parameters must match), making options B and C correct. ==Overloaded methods can have different return types, while overridden and hidden methods can have covariant return types==.**

---

4. What is the output of the following program?

```java
1: class Mammal {
2: private void sneeze() {}
3: public Mammal(int age) {
4: System.out.print("Mammal");
5: } }
6: public class Platypus extends Mammal {
7: int sneeze() { return 1; }
8: public Platypus() {
9: System.out.print("Platypus");
10: }
11: public static void main(String[] args) {
12: new Mammal(5);
13: } }
```

A. Platypus
B. Mammal
C. PlatypusMammal
D. MammalPlatypus
E. The code will compile if line 7 is changed.
F. The code will compile if line 9 is changed.

**My Answer: B**
**Correct Answer: F**

**The code will not compile as is, because the parent class Mammal does not define a no-argument constructor. For this reason, the first line of a Platypus constructor should be an explicit call to super(int), making option F the correct answer**

---

5. Which of the following complete the constructor so that this code prints out 50? (Choose all that apply.)

```java
class Speedster {
	int numSpots;
}
public class Cheetah extends Speedster {
	int numSpots;
	public Cheetah(int numSpots) {
	// INSERT CODE HERE
}

	public static void main(String[] args) {
		Speedster s = new Cheetah(50);
		System.out.print(s.numSpots);
	}
}
```

A. numSpots = numSpots;
B. numSpots = this.numSpots;
C. this.numSpots = numSpots;
D. numSpots = super.numSpots;
E. super.numSpots = numSpots;
F. The code does not compile regardless of the code inserted into the constructor.
G. None of the above

**My Answer: C,E**
**Correct Answer: E**

**An instance variable with the same name as an inherited instance variable is hidden, not overridden. This means that both variables exist, and the one that is used depends on the location and reference type. Because the main() method uses a reference type of Speedster to access the numSpots variable, the variable in the Speedster class, not the Cheetah class, must be set to 50. Option E is the only correct answer, as it assigns the instance variable numSpots in the Speedster class a value of 50. The numSpots variable in the Speedster class is then correctly referenced in the main() method, printing 50 at runtime.**

---

6. Which of the following declare immutable classes? (Choose all that apply.)

```java
public final class Moose {
	private final int antlers;
}
public class Caribou {
	private int antlers = 10;
}
public class Reindeer {
	private final int antlers = 5;
}
public final class Elk {}
	public final class Deer {
	private final Object o = new Object();
}
```

A. Moose
B. Caribou
C. Reindeer
D. Elk
E. Deer
F. None of the above

**My Answer: A,D**
**Correct Answer: D,E**

**The Moose class doesn’t compile, as the final variable antlers is not initialized  when it is declared, in an instance initializer, or in a constructor. Caribou and Reindeer are not immutable because they are not marked final, which means a subclass could extend them and add mutable fields. Elk and Deer are both immutable classes since they are marked final and only include private final members, making options D and E correct.**

---

7. What is the output of the following code?

```java
1: class Arthropod {
2: protected void printName(long input) {
3: System.out.print("Arthropod");
4: }
5: void printName(int input) {
6: System.out.print("Spooky");
7: } }
8: public class Spider extends Arthropod {
9: protected void printName(int input) {
10: System.out.print("Spider");
11: }
12: public static void main(String[] args) {
13: Arthropod a = new Spider();
14: a.printName((short)4);
15: a.printName(4);
16: a.printName(5L);
17: } }
```

A. SpiderSpiderArthropod
B. SpiderSpiderSpider
C. SpiderSpookyArthropod
D. SpookySpiderArthropod
E. The code will not compile because of line 5.
F. The code will not compile because of line 9.
G. None of the above

**My Answer: A**
**Correct Answer: A**

**The code compiles and runs without issue, so options E and F are incorrect. The Arthropod class defines two overloaded versions of the printName() method. The printName() method that takes an int value on line 5 is correctly overridden in theSpider class on line 9. Remember, an overridden method can have a broader access modifier, and protected access is broader than package access. Because of polymorphism, the overridden method replaces the method on all calls, even if an Arthropod reference variable is used, as is done in the main() method. For these reasons, the overridden method is called on lines 14 and 15, printing Spider twice. Note that the short value is automatically cast to the larger type of int, which then uses the overridden method. Line 16 calls the overloaded method in the Arthropod class, as the long value 5L does not match the overridden method, resulting in Arthropod being printed. Therefore, option A is the correct answer.**

---

8. What is the result of the following code?

```java
1: abstract class Bird {
2: private final void fly() { System.out.println("Bird"); }
3: protected Bird() { System.out.print("Wow-");}
4: }
5: public class Pelican extends Bird {
6: public Pelican() { System.out.print("Oh-");}
7: protected void fly() { System.out.println("Pelican"); }
8: public static void main(String[] args) {
9: var chirp = new Pelican();
10: chirp.fly();
11: } }
```

A. Oh-Bird
B. Oh-Pelican
C. Wow-Oh-Bird
D. Wow-Oh-Pelican
E. The code contains a compilation error.
F. None of the above

**My Answer: D**
**Correct Answer: D**

**The question is making sure you know that superclass constructors are called in the same manner in abstract classes as they are in non-abstract classes. Line 9 calls the constructor on line 6. The compiler automatically inserts super() as the first line of the constructor defined on line 6. The program then calls the constructor on line 3 and prints Wow-.Control then returns to line 6, and Oh-is printed. Finally, the method call on line 10 uses the version of fly() in the Pelican class, since it is marked private and the reference type of var is resolved as Pelican. The final output is Wow-Oh- Pelican, making option D the correct answer**

---
9. Which of the following statements about overridden methods are true? (Choose all that apply.)

A. An overridden method must contain method parameters that are the same or covariant with the method parameters in the inherited method.
B. An overridden method may declare a new exception, provided it is not checked.
C. An overridden method must be more accessible than the method in the parent class.
D. An overridden method may declare a broader checked exception than the method in the parent class.
E. If an inherited method returns void, then the overridden version of the method must return void.
F. None of the above

**My Answer: B,E**
**Correct Answer: C,E**

**An overridden method must not declare any new checked exceptions or a checked exception that is broader than the inherited method. For this reason, option B is correct Option C is incorrect because an overridden method may have the same access modifier as the version in the parent class. Finally, overridden methods must have covariant return types, and only void is covariant with void, making option E correct.**

---
10. Which of the following pairs, when inserted into the blanks, allow the code to compile? (Choose all that apply.)

```java
1: public class Howler {
2: public Howler(long shadow) {
3: ???;
4: }
5: private Howler(int moon) {
6: super();
7: }
8: }
9: class Wolf extends Howler {
10: protected Wolf(String stars) {
11: super(2L);
12: }
13: public Wolf() {
14: ???;
15: }
16: }
```

A. this(3) at line 3, this("") at line 14
B. this() at line 3, super(1) at line 14
C. this((short)1) at line 3, this(null) at line 14
D. super() at line 3, super() at line 14
E. this(2L) at line 3, super((short)2) at line 14
F. this(5) at line 3, super(null) at line 14
G. Remove lines 3 and 14.

**My Answer: A,C**
**Correct Answer: A,C**

**Option A is correct, as this(3) calls the constructor declared on line 5, while this("") calls the constructor declared on line 10. Option B does not compile, as inserting this() at line 3 results in a compiler error, since there is no matching constructor. Option C is correct, as short can be implicitly cast to int, resulting in this((short)1) calling the constructor declared on line 5. In addition, this(null) calls the String constructor declared on line 10.** 

---

11. What is the result of the following?

```java
1: public class PolarBear {
2: StringBuilder value = new StringBuilder("t");
3: { value.append("a"); }
4: { value.append("c"); }
5: private PolarBear() {
6: value.append("b");
7: }
8: public PolarBear(String s) {
9: this();
10: value.append(s);
11: }
12: public PolarBear(CharSequence p) {
13: value.append(p);
14: }
15: public static void main(String[] args) {
16: Object bear = new PolarBear();
17: bear = new PolarBear("f");
18: System.out.println(((PolarBear)bear).value);
19: } }
```

A. tacb
B. tacf
C. tacbf
D. tcafb
E. taftacb
F. The code does not compile.
G. An exception is thrown.

**My Answer: F**
**Correct Answer: C**

**Line 16 initializes a PolarBear instance and assigns it to the bear reference. The variable declaration and instance initializers are run first, setting value to tac. The constructor declared on line 5 is called, resulting in value being set to tacb. Remember, a static main() method can access private constructors declared in the same class. Line 17 creates another PolarBear instance, replacing the bear reference declared on line 16. First, value is initialized to tac as before. Line 17 calls the constructor declared on line 8, since String is the narrowest match of a String literal. This constructor then calls the overloaded constructor declared on line 5, resulting in value being updated to tacb. Control returns to the previous constructor, with line 10 updating value to tacbf, and making option C the correct answer.**

---

12. How many lines of the following program contain a compilation error?

```java
1: public class Rodent {
2: public Rodent(Integer x) {}
3: protected static Integer chew() throws Exception {
4: System.out.println("Rodent is chewing");
5: return 1;
6: }
7: }
8: class Beaver extends Rodent {
9: public Number chew() throws RuntimeException {
10: System.out.println("Beaver is chewing on wood");
11: return 2;
12: } }
```

A. None
B. 1
C. 2
D. 3
E. 4
F. 5

**My Answer: B**
**Correct Answer: C**

**The first compilation error is on line 8. Since Rodent declares at least one constructor and it is not a no-argument constructor, Beaver must declare a constructor with an explicit call to a super() constructor. Line 9 contains two compilation errors. First, the return types are not covariant since Number is a supertype, not a subtype, of Integer. Second, the inherited method is static, but the overridden method is not, making this an invalid override**

---

13. Which of these classes compile and will include a default constructor created by the compiler? (Choose all that apply.)

```java
A.
public class Bird {}
B.
public class Bird {
public bird() {}
}
C.
public class Bird {
public bird(String name) {}
}
D.
public class Bird {
public Bird() {}
}
E.
public class Bird {
Bird(String name) {}
}
F.
public class Bird {
private Bird(int age) {}
}
G.
public class Bird {
public Bird bird() { return null; }
}
```

**My Answer: A,G**
**Correct Answer: A,G**

---

14.  Which of the following statements about inheritance are correct? (Choose all that apply.)

A. A class can directly extend any number of classes.
B. A class can implement any number of interfaces.
C. All variables inherit java.lang.Object.
D. If class A is extended by B, then B is a superclass of A.
E. If class C implements interface D, then C is a subtype of D.
F. Multiple inheritance is the property of a class to have multiple direct superclasses.

**My Answer: B,E,F**
**Correct Answer: B,E,F**

**A class that implements an interface is a subtype of that interface, making option E correct.**

---

15. Which statements about the following program are correct? (Choose all that apply.)

```java
1: abstract class Nocturnal {
2: boolean isBlind();
3: }
4: public class Owl extends Nocturnal {
5: public boolean isBlind() { return false; }
6: public static void main(String[] args) {
7: var nocturnal = (Nocturnal)new Owl();
8: System.out.println(nocturnal.isBlind());
9: } }
```

A. It compiles and prints true.
B. It compiles and prints false.
C. The code will not compile because of line 2.
D. The code will not compile because of line 5.
E. The code will not compile because of line 7.
F. The code will not compile because of line 8.
G. None of the above

**My Answer: C**
**Correct Answer: C**

**The code does not compile because the isBlind() method in Nocturnal is not marked abstract and does not contain a method body. The rest of the lines compile without issue, making option C the only correct answer**

---

16. What is the result of the following?

```java
1: class Arachnid {
2: static StringBuilder sb = new StringBuilder();
3: { sb.append("c"); }
4: static
5: { sb.append("u"); }
6: { sb.append("r"); }
7: }
8: public class Scorpion extends Arachnid {
9: static
10: { sb.append("q"); }
11: { sb.append("m"); }
12: public static void main(String[] args) {
13: System.out.print(Scorpion.sb + " ");
14: System.out.print(Scorpion.sb + " ");
15: new Arachnid();
16: new Scorpion();
17: System.out.print(Scorpion.sb);
18: } }
```

A. qu qu qumrcrc
B. u u ucrcrm
C. uq uq uqmcrcr
D. uq uq uqcrcrm
E. qu qu qumcrcr
F. qu qu qucrcrm
G. The code does not compile.

**My Answer: D**
**Correct Answer: D**

**==Based on order of initialization, the static components are initialized first, starting with the Arachnid class, since it is the parent of the Scorpion class, which initializes the StringBuilder to u. The static initializer in Scorpion then updates sb to contain uq==, which is printed twice by lines 13 and 14 along with spaces separating the values. Next, an instance of Arachnid is initialized on line 15. There are two instance initializers in Arachnid, and they run in order, appending cr to the  StringBuilder, resulting in a value of uqcr. An instance of Scorpion is then initialized on line 16. The instance initializers in the superclass Arachnid run first, appending cr again and updating the value of sb to uqcrcr. Finally, the instance initializer in Scorpion runs and appends m.**

---

17. Which of the following are true? (Choose all that apply.)
A. this() can be called from anywhere in a constructor.
B. this() can be called from anywhere in an instance method.
C. this.variableName can be called from any instance method in the class.
D. this.variableName can be called from any static method in the class.
E. You can call the default constructor written by the compiler using this().
F. You can access a private constructor with the main() method in the same class.

**My Answer: C,F**
**Correct Answer: C,F**

---

18. Which statements about the following classes are correct? (Choose all that apply.)

```java
1: public class Mammal {
2: private void eat() {}
3: protected static void drink() {}
4: public Integer dance(String p) { return null; }
5: }
6: class Primate extends Mammal {
7: public void eat(String p) {}
8: }
9: class Monkey extends Primate {
10: public static void drink() throws RuntimeException {}
11: public Number dance(CharSequence p) { return null; }
12: public int eat(String p) {}
13: }
```

A. The eat() method in Mammal is correctly overridden on line 7.
B. The eat() method in Mammal is correctly overloaded on line 7.
C. The drink() method in Mammal is correctly overridden on line 10.
D. The drink() method in Mammal is correctly hidden on line 10.
E. The dance() method in Mammal is correctly overridden on line 11.
F. The dance() method in Mammal is correctly overloaded on line 11.
G. The eat() method in Primate is correctly hidden on line 12.
H. The eat() method in Primate is correctly overloaded on line 12.

**My Answer: H**
**Correct Answer: E,F**

**The eat() method is private in the Mammal class. Since it is not inherited in the Primate class, it is neither overridden nor overloaded, making options A and B incorrect. The drink() method in Mammal is correctly hidden in the Monkey class, as the signature is the same and both are static, making option D correct and option C incorrect. The version in the Monkey class throws a new exception, but it is unchecked; therefore, it is allowed. The dance() method in Mammal is correctly overloaded in the Monkey class because the signaturesare not the same, making option E incorrect and option F correct.**

---

19. What is the output of the following code?

```java
1: class Reptile {
2: {System.out.print("A");}
3: public Reptile(int hatch) {}
4: void layEggs() {
5: System.out.print("Reptile");
6: } }
7: public class Lizard extends Reptile {
8: static {System.out.print("B");}
9: public Lizard(int hatch) {}
10: public final void layEggs() {
11: System.out.print("Lizard");
12: }
13: public static void main(String[] args) {
14: var reptile = new Lizard(1);
15: reptile.layEggs();
16: } }
```

A. AALizard
B. BALizard
C. BLizardA
D. ALizard
E. The code will not compile because of line 3.
F. None of the above

**My Answer: F**
**Correct Answer: F**

**The Reptile class defines a constructor, but it is not a no-argument constructor. Therefore, the Lizard constructor must explicitly call super(), passing in an int value. For this reason, line 9 does not compile, and option F is the correct answer.**

---

20. Which statement about the following program is correct?

```java
1: class Bird {
2: int feathers = 0;
3: Bird(int x) { this.feathers = x; }
4: Bird fly() {
5: return new Bird(1);
6: } }
7: class Parrot extends Bird {
8: protected Parrot(int y) { super(y); }
9: protected Parrot fly() {
10: return new Parrot(2);
11: } }
12: public class Macaw extends Parrot {
13: public Macaw(int z) { super(z); }
14: public Macaw fly() {
15: return new Macaw(3);
16: }
17: public static void main(String... sing) {
18: Bird p = new Macaw(4);
19: System.out.print(((Parrot)p.fly()).feathers);
20: } }
```

A. One line contains a compiler error.
B. Two lines contain compiler errors.
C. Three lines contain compiler errors.
D. The code compiles but throws a ClassCastException at runtime.
E. The program compiles and prints 3.
F. The program compiles and prints 0.

**My Answer: E**
**Correct Answer: E**

**The fly() method is correctly overridden in each subclass since the signature is the same, the access modifier is less restrictive, and the return types are covariant. For covariance, Macaw is a subtype of Parrot, which is a subtype of Bird, so overridden return types are valid. Likewise, the constructors are all implemented properly, with explicit calls to the parent constructors as needed. Line 19 calls the overridden version of fly() defined in the Macaw class, as overriding replaces the method regardless of the reference type. This results in feathers being assigned a value of 3. The Macaw object is then cast to Parrot, which is allowed because Macaw inherits Parrot. The feathers variable is visible since it is defined in the Bird class, and line 19 prints 3,**

---

21. Which of the following are properties of immutable classes? (Choose all that apply.)

A. The class can contain setter methods, provided they are marked final.
B. The class must not be able to be extended outside the class declaration.
C. The class may not contain any instance variables.
D. The class must be marked static.
E. The class may not contain any static variables.
F. The class may only contain private constructors.
G. The data for mutable instance variables may be read, provided they cannot be modified by the caller.

**My Answer: B,G**
**Correct Answer: B,G**

---

22. What does the following program print?
```java
1: class Person {
	2: static String name;
	3: void setName(String q) { name = q; } }
4: public class Child extends Person {
	5: static String name;
	6: void setName(String w) { name = w; }
	7: public static void main(String[] p) {
		8: final Child m = new Child();
		9: final Person t = m;
		10: m.name = "Elysia";
		11: t.name = "Sophia";
		12: m.setName("Webby");
		13: t.setName("Olivia");
		14: System.out.println(m.name + " " + t.name);
15: } }
```

A. Elysia Sophia
B. Webby Olivia
C. Olivia Olivia
D. Olivia Sophia
E. The code does not compile.
F. None of the above

**My Answer: D**
**Correct Answer: D**

**The Child class overrides the setName() method and hides the static name variable defined in the inherited Person class. Since variables are only hidden, not overridden, there are two distinct name variables accessible, depending on the location and reference type. Line 8 creates a Child instance, which is implicitly cast to a Person reference type on line 9. Line 10 uses the Child reference type, updating Child.name to Elysia. Line 11 uses the Person referencetype, updating Person.name to Sophia. Lines 12 and 13 both call the overridden setName() instance method declared on line 6. This sets Child.name to Webby on line 12 and then to Olivia on line 13. The final values of Child.name and Person.name are Olivia and Sophia, respectively, making option D the correct answer.**

---

23. What is the output of the following program?

```java
1: class Canine {
2: public Canine(boolean t) { logger.append("a"); }
3: public Canine() { logger.append("q"); }
4:
5: private StringBuilder logger = new StringBuilder();
6: protected void print(String v) { logger.append(v); }
7: protected String view() { return logger.toString(); }
8: }
9:
10: class Fox extends Canine {
11: public Fox(long x) { print("p"); }
12: public Fox(String name) {
13: this(2);
14: print("z");
15: }
16: }
17:
18: public class Fennec extends Fox {
19: public Fennec(int e) {
20: super("tails");
21: print("j");
22: }
23: public Fennec(short f) {
24: super("eevee");
25: print("m");
26: }
27:
28: public static void main(String... unused) {
29: System.out.println(new Fennec(1).view());
30: } }
```

A. qpz
B. qpzj
C. jzpa
D. apj
E. apjm
F. The code does not compile.
G. None of the above

**My Answer: F**
**Correct Answer: B**

**The constructors are called from the child class upward, but since each line of a constructor is a call to another constructor, via this() or super(), they are ultimately executed in a top-down manner. On line 29, the main() method calls the Fennec() constructor declared on line 19. Remember, integer literals in Java are considered int by default. This constructor calls the Fox() constructor defined on line 12, which in turn calls the overloaded Fox() constructor declared on line11. Since the constructor on line 11 does not explicitly call a parent constructor, the compiler inserts a call to the no-argument super() constructor, which exists on line 3 of the Canine class. Line 3 is then executed, adding q to the output, and the compiler chain is unwound. Line 11 then executes, adding p, followed by line 14, adding z. Finally, line 21 is executed, and j is added, resulting in a final value for logger of qpzj, and making option B correct. For the exam, remember to follow constructors from the lowest level upward to determine the correct pathway, but then execute them from the top down using the established order.**

---

24. What is printed by the following program?

```java
1: class Antelope {
2: public Antelope(int p) {
3: System.out.print("4");
4: }
5: { System.out.print("2"); }
6: static { System.out.print("1"); }
7: }
8: public class Gazelle extends Antelope {
9: public Gazelle(int p) {
10: super(6);
11: System.out.print("3");
12: }
13: public static void main(String hopping[]) {
14: new Gazelle(0);
15: }
16: static { System.out.print("8"); }
17: { System.out.print("9"); }
18: }
```

A. 182640
B. 182943
C. 182493
D. 421389
E. The code does not compile.
F. The output cannot be determined until runtime.

**My Answer: C**
**Correct Answer: C**

**First, the class is initialized, starting with the superclass Antelope and then the subclass Gazelle. This involves invoking the static variable declarations and static initializers. The program first prints 1, followed by 8. Then we follow the constructor pathway from the object created on line 14 upward, initializing each class instance using a top-down approach. Within each class, the instance initializers are run, followed by the referenced constructors. The Antelope instance is initialized, printing 24, followed by the Gazelle instance, printing 93. The final output is 182493**

---

 25. Which of the following are true about a concrete class? (Choose all that apply.)
A. A concrete class can be declared as abstract.
B. A concrete class must implement all inherited abstract methods.
C. A concrete class can be marked as final.
D. A concrete class must be immutable.
E. A concrete method that implements an abstract method must match the method declaration of the abstract method exactly.

**My Answer: B,C**
**Correct Answer: B,C**

---

26. What is the output of the following code?

```java
4: public abstract class Whale {
5: public abstract void dive();
6: public static void main(String[] args) {
7: Whale whale = new Orca();
8: whale.dive(3);
9: }
10: }
11: class Orca extends Whale {
12: static public int MAX = 3;
13: public void dive() {
14: System.out.println("Orca diving");
15: }
16: public void dive(int... depth) {
17: System.out.println("Orca diving deeper "+MAX);
18: } }
```

A. Orca diving
B. Orca diving deeper 3
C. The code will not compile because of line 4.
D. The code will not compile because of line 8.
E. The code will not compile because of line 11.
F. The code will not compile because of line 12.
G. The code will not compile because of line 17.
H. None of the above

**My Answer: D**
**Correct Answer: D**

**The classes are structured correctly, but the body of the main() method contains a compiler error. The Orca object is implicitly cast to a Whale reference on line 7. This is permitted because Orca is a subclass of Whale. By performing the cast, the whale reference on line 8 does not have access to the dive(int... depth) method. For this reason, line 8 does not compile, making option D correct.**

---

# Chapter 7 - Beyond Classes #Chapter

Java file may have at most one ``public`` top-level type, and it must match the name of the file. This applies to classes, enums, records, and so on. a top-level type can only be declared with ``public`` or package access.
## Implementing Interfaces

a class may implement any number of interfaces. An interface is an abstract data type that declares a list of abstract methods that any class implementing the interface must provide.

### Declaring and Using an Interface

In Java, an interface is defined with the ``interface`` keyword, analogous to the ``class`` keyword used when defining a class

![[Pasted image 20240330165738.png]]

**==Interface variables are referred to as constants because they are assumed to be ``public``, ``static``, and ``final``.==** They are initialized with a constant value when they are declared. Since they are ``public`` and ``static``, they can be used outside the interface declaration without requiring an instance of the interface

**==One aspect of an interface declaration that differs from an abstract class is that it contains implicit modifiers==**. An implicit modifier is a modifier that the compiler automatically inserts into the code. For example, an interface is always considered to be abstract, even if it is not marked so.

```java
public abstract interface WalksOnTwoLegs {}
```

The ``abstract`` modifier in this example is optional for interfaces, with the compiler inserting it if it is not provided.

```java
public class Biped {
	public static void main(String[] args) {
		var e = new WalksOnTwoLegs(); // DOES NOT COMPILE
	}
}
public final interface WalksOnEightLegs {} // DOES NOT COMPILE
```

- The first example doesn’t compile, as ``WalksOnTwoLegs`` is an interface and cannot be instantiated.
- The second example, ``WalksOnEightLegs``, doesn’t compile because **==interfaces cannot be marked as ``final``==** for the same reason that abstract classes cannot be marked as final. 

```java
public interface Climb {
	Number getSpeed(int age);
}
```

![[Pasted image 20240330170530.png]]

The ``FieldMouse`` class declares that it implements the ``Climb`` interface and includes an overridden version of ``getSpeed()`` inherited from the ``Climb`` interface. The method signature of ``getSpeed()`` matches exactly, and the return type is covariant, since a ``Float`` can be implicitly cast to a ``Number``. The access modifier of the interface method is implicitly ``public`` in Climb, although the concrete class ``FieldMouse`` must explicitly declare it.

**==If any of the interfaces define abstract methods, then the concrete class is required to override them.==**

### Extending an Interface

Like a class, an interface can extend another interface using the ``extends`` keyword.

```java
public interface Nocturnal {}
public interface HasBigEyes extends Nocturnal {}
```

Unlike a class, which can extend only one class, an interface can extend multiple interfaces.

```java
public interface Nocturnal {
	public int hunt();
}
public interface CanFly {
	public void flap();
}
public interface HasBigEyes extends Nocturnal, CanFly {}
	public class Owl implements HasBigEyes {
	public int hunt() { return 5; }
	public void flap() { System.out.println("Flap!"); }
}
```

Extending two interfaces is permitted because interfaces are not initialized as part of a class hierarchy. Unlike abstract classes, they do not contain constructors and are not part of instance initialization. Interfaces simply define a set of rules and methods that a class implementing them must follow.

### Inheriting an Interface

Like an abstract class, when a concrete class inherits an interface, all of the inherited abstract methods must be implemented.

```java
public interface HasTail {
	public int getTailLength();
}
public interface HasWhiskers {
	public int getNumberOfWhiskers();
}

public abstract class HarborSeal implements HasTail, HasWhiskers {}
public class CommonSeal extends HarborSeal {} // DOES NOT COMPILE
```

- The ``HarborSeal`` class compiles because it is abstract and not required to implement any of the abstract methods it inherits
- The concrete ``CommonSeal`` class, though, must override all inherited abstract methods.

#### Mixing Class and Interface Keywords

**==Although a class can implement an interface, a class cannot extend an interface. Likewise, while an interface can extend another interface, an interface cannot implement another interface.==**

```java
public interface CanRun {}
public class Cheetah extends CanRun {} // DOES NOT COMPILE
public class Hyena {}
public interface HasFur extends Hyena {} // DOES NOT COMPILE
```

#### Inheriting Duplicate Abstract Methods

Java supports inheriting two abstract methods that have compatible method declarations.

```java
public interface Herbivore { public void eatPlants(); }
public interface Omnivore { public void eatPlants(); }
public class Bear implements Herbivore, Omnivore {
public void eatPlants() {
	System.out.println("Eating plants");
} }
```

By compatible, we mean a method can be written that properly overrides both inherited methods:

```java
public interface Herbivore { public void eatPlants(); }
public interface Omnivore { public int eatPlants(); }
public class Tiger implements Herbivore, Omnivore { // DOES NOT COMPILE
	...
}
```

### Inserting Implicit Modifiers

**==an implicit modifier is one that the compiler will automatically insert.==**

-  ==**Interfaces are implicitly ``abstract``.**==
-  ==**Interface variables are implicitly ``public``, ``static``, and ``final``.**==
-  ==**Interface methods without a body are implicitly ``abstract``.**==
-  ==**Interface methods without the ``private`` modifier are implicitly ``public``.==**

The following two interface definitions are equivalent, as the compiler will convert them both to the second declaration:

```java
public interface Soar {
	int MAX_HEIGHT = 10;
	final static boolean UNDERWATER = true;
	void fly(int speed);
	abstract void takeoff();
	public abstract double dive();
}

public abstract interface Soar {
	public static final int MAX_HEIGHT = 10;
	public final static boolean UNDERWATER = true;
	public abstract void fly(int speed);
	public abstract void takeoff();
	public abstract double dive();
}
```

#### Conflicting Modifiers

What happens if a developer marks a method or variable with a modifier that conflicts with an implicit modifier?

```java
public interface Dance {
	private int count = 4; // DOES NOT COMPILE
	protected void step(); // DOES NOT COMPILE
}
```

Neither of these interface member declarations compiles, as the compiler will apply the ``public`` modifier to both, resulting in a conflict.

#### Differences between Interfaces and Abstract Classes

**==Even though abstract classes and interfaces are both considered abstract types, only interfaces make use of implicit modifiers.==**

```java
abstract class Husky { // abstract required in class declaration
	abstract void play(); // abstract required in method declaration
}
interface Poodle { // abstract optional in interface declaration
	void play(); // abstract optional in method declaration
}
```

```java
public class Webby extends Husky {
	void play() {} // OK -play() is declared with package access in Husky
}
public class Georgette implements Poodle {
	void play() {} // DOES NOT COMPILE -play() is public in Poodle
}
```

Even though the two method implementations are identical, the method in the ``Georgette`` class reduces the access modifier on the method from ``public`` to package access.

### Declaring Concrete Interface Methods

![[Pasted image 20240330172909.png]]

--- 
What About ``protected`` or Package Interface Members?

**Alongside ``public`` methods, interfaces now support ``private`` methods. ==They do not support protected access, though, as a class cannot extend an interface. They also do not support package access, although more likely for syntax reasons and backward compatibility==. Since interface methods without an access modifier have been considered implicitly public, changing this behavior to package access would break many existing programs!**

---

#### Writing a ``default`` Interface Method

A default method is a method defined in an interface with the ``default`` keyword and includes a method body. It may be optionally overridden by a class implementing the interface.

One use of ``default`` methods is for backward compatibility. You can add a new ``default`` method to an interface without the need to modify all of the existing classes that implement the interface. The older classes will just use the default implementation of the method defined in the interface

```java
public interface IsColdBlooded {
	boolean hasScales();
	default double getTemperature() {
		return 10.0;
	} 
}
```

```java
public class Snake implements IsColdBlooded {
	public boolean hasScales() { // Required override
		return true;
	}
	public double getTemperature() { // Optional override
		return 12;
	}
}

```

---

**the ``default`` interface method modifier is not the same as the ``default`` label used in a switch statement or expression. Likewise, even though package access is sometimes referred to as default access, that feature is implemented by omitting an access modifier.**

---

**Default Interface Method Definition Rules**
1. ==**A ``default`` method may be declared only within an interface.**==
2. ==**A ``default`` method must be marked with the ``default`` keyword and include a method body.**==
3. ==**A ``default`` method is implicitly public.**==
4. ==**A ``default`` method cannot be marked ``abstract``, ``final``, or ``static``.**==
5. ==**A ``default`` method may be overridden by a class that implements the interface.**==
6. ==**If a class inherits two or more ``default`` methods with the same method signature, then the**==
==**class must override the method.==**

```java
public interface Carnivore {
	public default void eatMeat(); // DOES NOT COMPILE
	public int getRequiredFoodAmount() { // DOES NOT COMPILE
		return 13;
} }
```

Unlike ``abstract`` methods, though, ``default`` interface methods cannot be marked abstract since they provide a body. They also cannot be marked as ``final``, because they are designed so that they can be overridden in classes implementing the interface, just like ``abstract`` methods. Finally, they cannot be marked ``static`` since they are associated with the instance of the class implementing the interface.

##### Inheriting Duplicate ``default`` Methods

```java
public interface Walk {
	public default int getSpeed() { return 5; }
}
public interface Run {
	public default int getSpeed() { return 10; }
}
public class Cat implements Walk, Run {} // DOES NOT COMPILE
```

If the class implementing the interfaces overrides the duplicate default method, the code will compile without issue. By overriding the conflicting method, the ambiguity about which version of the method to call has been removed.

```java
public class Cat implements Walk, Run {
	public int getSpeed() { return 1; }
}
```

##### Calling a Hidden ``default`` Method

what if the ``Cat`` class wanted to access the version of ``getSpeed()`` in ``Walk`` or ``Run``? Is it still accessible?

```java
public class Cat implements Walk, Run {
	public int getSpeed() {
		return 1;
	}
	public int getWalkSpeed() {
		return Walk.super.getSpeed();
	}
}
```

we **==use the ``super`` keyword to show that we are following instance inheritance, not class inheritance==**. Note that calling ``Walk.getSpeed()`` or ``Walk.this.getSpeed()`` would not have worked.

#### Declaring ``static`` Interface Methods

**Static Interface Method Definition Rules**
1. ==**A ``static`` method must be marked with the ``static`` keyword and include a method body.**==
2. ==**A ``static`` method without an access modifier is implicitly ``public``.**==
3. ==**A ``static`` method cannot be marked ``abstract`` or ``final``.**==
4. ==**A ``static`` method is not inherited and cannot be accessed in a class implementing the interface without a reference to the interface name.**==

 can use the ``private`` access modifier with ``static`` methods.

```java
public interface Hop {
	static int getJumpHeight() {
		return 8;
	} 
}
```

Since the method is defined without an access modifier, the compiler will automatically insert the ``public`` access modifier. The method ``getJumpHeight()`` works just like a ``static`` method as defined in a class. In other words, it can be accessed without an instance of a class.

```java
public class Skip {
	public int skip() {
		return Hop.getJumpHeight();
	}
}
```

```java
public class Bunny implements Hop {
	public void printDetails() {
		System.out.println(getJumpHeight()); // DOES NOT COMPILE
	} 
}
```

Without an explicit reference to the name of the interface, the code will not compile, even though ``Bunny`` implements ``Hop``.

```java
public class Bunny implements Hop {
	public void printDetails() {
		System.out.println(Hop.getJumpHeight());
	} 
}
```

**==Java “solved” the multiple inheritance problem of ``static`` interface methods by not allowing them to be inherited!==**
#### Reusing Code with ``private`` Interface Methods

The last two types of concrete methods that can be added to interfaces are ``private`` and ``private`` ``static`` interface methods. **==Because both types of methods are ``private``, they can only be used in the interface declaration in which they are declared==**. For this reason, they were added primarily to reduce code duplication.

```java
public interface Schedule {
	default void wakeUp() { checkTime(7); }
	private void haveBreakfast() { checkTime(9); }
	static void workOut() { checkTime(18); }
	private static void checkTime(int hour) {
		if (hour> 17) {
			System.out.println("You're late!");
		} else {
			System.out.println("You have "+(17-hour)+" hours left " + "to make the appointment");
		} 
	} 
}
```

The difference between a ``non-static private`` method and a ``static`` one is analogous to the difference between an instance and static method declared within a class. In particular, it’s all about what methods each can be called from.

**Private Interface Method Definition Rules**
1. ==**A ``private`` interface method must be marked with the private modifier and include a method body.**==
2. ==**A ``private`` ``static`` interface method may be called by any method within the interface definition.**==
3. ==**A ``private`` interface method may only be called by ``default`` and other ``private non-static`` methods within the interface definition.**==

#### Calling Abstract Methods

``default`` and ``private non-static`` methods can access ``abstract`` methods declared in the interface. This is the primary reason we associate these methods with instance membership. When they are invoked, there is an instance of the interface.

```java
public interface ZooRenovation {
	public String projectName();
	abstract String status();
	default void printStatus() {
		System.out.print("The " + projectName() + " project " + status());
	} 
}
```

both ``projectName()`` and ``status()`` have the same modifiers (``abstract`` and ``public`` are implicit) and can be called by the default method ``printStatus()``.

### Reviewing Interface Members

![[Pasted image 20240330182307.png]]

quick tips for the exam:
-  ==**Treat ``abstract``, ``default``, and ``non-static private`` methods as belonging to an instance of the interface.**==
-  ==**Treat ``static`` methods and variables as belonging to the interface class object.**==
-  ==**All private interface method types are only accessible within the interface declaration.==**

```java
public interface ZooTrainTour {
	abstract int getTrainName();
	private static void ride() {}
	default void playHorn() { getTrainName(); ride(); }
	public static void slowDown() { playHorn(); }
	static void speedUp() { ride(); }
}
```

The ``slowDown()`` method does not compile. is ``static``, though, and cannot call a ``default`` or ``private`` method, such as ``playHorn()``, without an explicit reference object
## Working with Enums

An enumeration, or enum for short, is like a fixed set of constants. Using an enum is much better than using a bunch of constants because it provides type-safe checking. With enums, it is impossible to create an invalid enum value without introducing a compiler error.

**==Enumerations show up whenever you have a set of items whose types are known at compile time==**. Common examples include the compass directions, the months of the year, the planets in the solar system, and the cards in a deck
### Creating Simple Enums

![[Pasted image 20240330185501.png]]

an enum that only contains a list of values as a simple enum. **==When working with simple enums, the semicolon at the end of the list is optional.==**

---

**Enum values are considered constants and are commonly written using snake case. For example, an enum declaring a list of ice cream flavors might include values like VANILLA, ROCKY_ROAD, INT_CHOCOLATE_CHIP, and so on.**

---

```java
var s = Season.SUMMER;
System.out.println(Season.SUMMER); // SUMMER
System.out.println(s == Season.SUMMER); // true
```

enums print the name of the enum when ``toString()`` is called. They can be compared using ``==`` because they are like ``static final`` constants. In other words, you can use ``equals()`` or ``==`` to compare enums, since **==each enum value is initialized only once in the Java Virtual Machine (JVM).**== ==**One thing that you can’t do is extend an enum.==**

```java
public enum ExtendedSeason extends Season {} // DOES NOT COMPILE
```

The values in an enum are fixed. You cannot add more by extending the enum.
#### Calling the ``values()``, ``name()``, and ``ordinal()`` Methods

An enum provides a ``values()`` method to get an array of all of the values.

```java
for(var season: Season.values()) {
	System.out.println(season.name() + " " + season.ordinal());
}
```

The output shows that each enum value has a corresponding int value, and the values are listed in the order in which they are declared:

```text
WINTER 0
SPRING 1
SUMMER 2
FALL 3
```

You can’t compare an ``int`` and an enum value directly anyway since an enum is a type, like a Java class, and not a primitive ``int``.

```java
if ( Season.SUMMER == 2) {} // DOES NOT COMPILE
```

#### Calling the ``valueOf()`` Method

Another useful feature is retrieving an enum value from a ``String`` using the ``valueOf()`` method. **==The ``String`` passed in must match the enum value exactly, though.==**

```java
Season s = Season.valueOf("SUMMER"); // SUMMER
Season t = Season.valueOf("summer"); // IllegalArgumentException
```

**==Each enum value is created once when the enum is first loaded. Once the enum has been loaded, it retrieves the single enum value with the matching name==**.

### Using Enums in ``switch`` Statements

```java
Season summer = Season.SUMMER;
switch(summer) {
	case WINTER:
		System.out.print("Get out the sled!");
		break;
	case SUMMER:
		System.out.print("Time for the pool!");
		break;
	default:
		System.out.print("Is it summer yet?");
}
```

**==Java treats the enum type as implicit==**. In fact, if you were to type case ``Season.WINTER``, it would not compile.

```java
Season summer = Season.SUMMER;
var message = switch(summer) {
	case Season.WINTER -> "Get out the sled!"; // DOES NOT COMPILE
	case 0 -> "Time for the pool!"; // DOES NOT COMPILE
	default -> "Is it summer yet?";
};
System.out.print(message);
```

- The first case statement does not compile because ``Season`` is used in the case value. If we changed ``Season.FALL`` to just ``FALL``, then the line would compile.
- can’t compare enums with ``int`` values
### Adding Constructors, Fields, and Methods

```java
1: public enum Season {
	2: WINTER("Low"), SPRING("Medium"), SUMMER("High"), FALL("Medium");
	3: private final String expectedVisitors;
	4: private Season(String expectedVisitors) {
		5: this.expectedVisitors = expectedVisitors;
	6: }
	7: public void printExpectedVisitors() {
		8: System.out.println(expectedVisitors);
	9: } 
}
```

- On line 2, the list of enum values ends with a semicolon ``(;)``. While this is optional when our enum is composed solely of a list of values, it is required if there is anything in the enum besides the values.
- Lines 3–9 are regular Java code.

---

**Although it is possible to create an enum with instance variables that can be modified, it is a very poor practice to do so since they are shared within the JVM. When designing an enum, the values should be immutable.**

---

**==All enum constructors are implicitly ``private``, with the modifier being optional. In fact, an enum constructor will not compile if it contains a ``public`` or ``protected`` modifier.==**

the parentheses on line 2? Those are constructor calls, but without the new keyword normally used for objects. The first time we ask for any of the enum values, Java constructs all of the enum values. After that, Java just returns the already constructed enum values.

```java
public enum OnlyOne {
	ONCE(true);
	private OnlyOne(boolean b) {
		System.out.print("constructing,");
	}
}

public class PrintTheOne {
	public static void main(String[] args) {
		System.out.print("begin,");
		OnlyOne firstCall = OnlyOne.ONCE; // Prints constructing,
		OnlyOne secondCall = OnlyOne.ONCE; // Doesn't print anything
		System.out.print("end");
	} // begin,constructing,end
}
```

If the ``OnlyOne`` enum was used earlier in the program, and therefore initialized sooner, then the line that declares the ``firstCall`` variable would not print anything.

```java
Season.SUMMER.printExpectedVisitors();
```

to define different methods for each enum.

```java
public enum Season {
	WINTER {
		public String getHours() { return "10am-3pm";}
	},
	SPRING {
		public String getHours() { return "9am-5pm";}
	},
	SUMMER {
		public String getHours() { return "9am-7pm";}
	},
	FALL {
		public String getHours() { return "9am-5pm";}
	};
	public abstract String getHours();
}
```

The enum itself has an ``abstract`` method. This means that each and every enum value is required to implement this method. If we forget to implement the method for one of the values, we get a compiler error:

But what if we don’t want each and every enum value to have a method? We can create an implementation for all values and override it only for the special cases.

```java
public enum Season {
	WINTER {
		public String getHours() { return "10am-3pm";}
	},
	SUMMER {
		public String getHours() { return "9am-7pm";}
	},
	SPRING, FALL;
		public String getHours() { return "9am-5pm";}
}
```

---

```java
public enum Operation {
    PLUS("+") {
        public double apply(double x, double y) { return x + y; }
    },
    MINUS("-") {
        public double apply(double x, double y) { return x - y; }
    },
    TIMES("*") {
        public double apply(double x, double y) { return x * y; }
    },
    DIVIDE("/") {
        public double apply(double x, double y) { return x / y; }
    };

    private final String symbol;

    Operation(String symbol) {
        this.symbol = symbol;
    }

    @Override public String toString() { return symbol; }

    public abstract double apply(double x, double y);
}
```

---

An enum can even implement an interface, as this just requires overriding the ``abstract`` methods:

```java
public interface Weather { int getAverageTemperature(); }
public enum Season implements Weather {
	WINTER, SPRING, SUMMER, FALL;
	public int getAverageTemperature() { return 30; }
}
```

---

**==the list of values came first. This was not an accident. Whether the enum is simple or complex, the list of values always comes first.==**

---

## Sealing Classes

A sealed class is a class that restricts which other classes may **==directly==** extend it

### Declaring a Sealed Class

A sealed class declares a list of classes that can extend it, while the subclasses declare that they extend the sealed class.

![[Pasted image 20240330230403.png]]

**Sealed Class Keywords**
- ==**sealed: Indicates that a class or interface may only be extended/implemented by named classes or interfaces**==
- ==**permits: Used with the sealed keyword to list the classes and interfaces allowed**==
- ==**non-sealed: Applied to a class or interface that extends a sealed class, indicating that it can be extended by unspecified classes**==

```java
public class sealed Frog permits GlassFrog {} // DOES NOT COMPILE
public final class GlassFrog extends Frog {}
public abstract sealed class Wolf permits Timber {}
public final class Timber extends Wolf {}
public final class MyWolf extends Wolf {} // DOES NOT COMPILE
```

- The first example does not compile because the ``class`` and ``sealed`` modifiers are in the wrong order.
- The second example does not compile because ``MyWolf`` isn’t listed in the declaration of ``Wolf``.

---

**Sealed classes are commonly declared with the abstract modifier, although this is certainly not required**

---

Declaring a sealed class with the ``sealed`` modifier is the easy part. Most of the time, if you see a question on the exam about sealed classes, they are testing your knowledge of whether the subclass ``extends`` the ``sealed`` class properly

### Compiling Sealed Classes

```java
// Penguin.java
package zoo;
public sealed class Penguin permits Emperor {} // Emperor must declared already
```

**==a sealed class needs to be declared (and compiled) in the same package as its direct subclasses==**. But what about the subclasses themselves? They must each extend the sealed class

```java
// Penguin.java
package zoo;
public sealed class Penguin permits Emperor {} // DOES NOT COMPILE

// Emperor.java
package zoo;
public final class Emperor {} // Does Not Extends Penguin Class
```

### Specifying the Subclass Modifier

**==Every class that directly extends a sealed class must specify exactly one of the following three modifiers: ``final``, ``sealed``, or ``non-sealed``.==**

#### A ``final`` Subclass

```java
public sealed class Antelope permits Gazelle {}
public final class Gazelle extends Antelope {}
public class George extends Gazelle {} // DOES NOT COMPILE
```

#### A ``sealed`` Subclass

```java
public sealed class Mammal permits Equine {}
public sealed class Equine extends Mammal permits Zebra {}
public final class Zebra extends Equine {}
```

The ``sealed`` modifier applied to the subclass ``Equine`` means the same kind of rules that we applied to the parent class ``Mammal`` must be present. Namely, ``Equine`` defines its own list of permitted subclasses.

Despite allowing indirect subclasses not named in ``Mammal``, the list of classes that can inherit ``Mammal`` is still fixed. If you have a reference to a ``Mammal`` object, it must be a ``Mammal``, ``Equine``, or ``Zebra``.

#### A ``non-sealed`` Subclass

The ``non-sealed`` modifier is used to open a sealed parent class to potentially unknown subclasses.

```java
public sealed class Wolf permits Timber {}
public non-sealed class Timber extends Wolf {}
public class MyWolf extends Timber {}
public class MyFurryWolf extends MyWolf {}
```

### Omitting the ``permits`` Clause

```java
// Snake.java
public sealed class Snake permits Cobra {}
final class Cobra extends Snake {}
```

In this case, the ``permits`` clause is optional and can be omitted. The ``extends`` keyword is still required in the subclass, though:

```java
// Snake.java
public sealed class Snake {}
final class Cobra extends Snake {}
```

If these classes were in separate files, this code would not compile! This rule also applies to sealed classes with nested subclasses.

```java
// Snake.java
public sealed class Snake {
final class Cobra extends Snake {}
}
```

---
**Referencing Nested Subclasses**

**While it makes the code easier to read if you omit the ``permits`` clause for nested subclasses, you are welcome to name them. However, the syntax might be different than you expect.**

```java
public sealed class Snake permits Cobra { // DOES NOT COMPILE
	final class Cobra extends Snake {}
}
```

**This code does not compile because ``Cobra`` requires a reference to the ``Snake`` namespace. The following fixes this issue:**

```java
public sealed class Snake permits Snake.Cobra {
	final class Cobra extends Snake {}
}
```

**When all of your subclasses are nested, we strongly recommend omitting the ``permits`` class.**

---

![[Pasted image 20240330231930.png]]

### Sealing Interfaces

Besides classes, interfaces can also be sealed. The idea is analogous to classes, and many of the same rules apply. For example, the ``sealed`` interface must appear in the same package or named module as the classes or interfaces that directly extend or implement it. **==One distinct feature of a ``sealed`` interface is that the ``permits`` list can apply to a class that implements the interface or an interface that extends the interface==**.

```java
// Sealed interface
public sealed interface Swims permits Duck, Swan, Floats {}
// Classes permitted to implement sealed interface
public final class Duck implements Swims {}
public final class Swan implements Swims {}
// Interface permitted to extend sealed interface
public non-sealed interface Floats extends Swims {}
```

**==Interfaces are implicitly ``abstract`` and cannot be marked ``final``. For this reason, interfaces that ``extend`` a ``sealed`` interface can only be marked ``sealed`` or ``non-sealed``. They cannot be marked ``final``.==**

### Reviewing Sealed Class Rules

**Sealed Class Rules**
- ==**Sealed classes are declared with the ``sealed`` and ``permits`` modifiers.**==
- ==**Sealed classes must be declared in the same package or named module as their direct subclasses.**==
- ==**Direct subclasses of ``sealed`` classes must be marked ``final``, ``sealed``, or ``non-sealed``.**==
- ==**The permits clause is optional if the ``sealed`` class and its direct subclasses are declared within the same file or the subclasses are nested within the ``sealed`` class.**==
- ==**Interfaces can be ``sealed`` to limit the classes that implement them or the interfaces that extend them.**==

## Encapsulating Data with Records

### Understanding Encapsulation

A *POJO*, which stands for Plain Old Java Object, is a class used to model and pass data around, often with few or no complex methods

```java
public class Crane {
	int numberEggs;
	String name;
	public Crane(int numberEggs, String name) {
		this.numberEggs = numberEggs;
		this.name = name;
	}
}
```

```java
public class Poacher {
	public void badActor() {
		var mother = new Crane(5, "Cathy");
		mother.numberEggs = -100;
	}
}
```

*Encapsulation* is a way to protect class members by restricting access to them. In Java, it is commonly implemented by declaring all instance variables ``private``. Callers are required to use methods to retrieve or modify instance variables. Encapsulation is about protecting a class from unexpected use. It also allows us to modify the methods and behavior of the class later without someone already having direct access to an instance variable within the class.

```java
1: public final class Crane {
	2: private final int numberEggs;
	3: private final String name;
	4: public Crane(int numberEggs, String name) {
		5: if (numberEggs >= 0) this.numberEggs = numberEggs; // guard condition
		6: else throw new IllegalArgumentException();
		7: this.name = name;
	8: }
	9: public int getNumberEggs() { // getter
		10: return numberEggs;
	11: }
	12: public String getName() { // getter
		13: return name;
	14: }
15: }
```


- the instance variables are now ``private`` on lines 2 and 3. This means only code within the class can read or write their values.
- added a method on lines 9–11 to read the value, which is called an accessor method or a getter.
- marked the class and its instance variables ``final``, and we don’t have any mutator methods, or setters, to modify the value of the instance variables. That’s because we want our class to be immutable in addition to being well encapsulated.
### Applying Records

![[Pasted image 20240330233434.png]]

A record is a special type of data-oriented class in which the compiler inserts boilerplate code for you
As a bonus, the compiler inserts useful implementations of the ``Object`` methods ``equals()``, ``hashCode()``, and ``toString()``. 
Creating an instance of a ``Crane`` and printing some fields is easy:

```java
var mommy = new Crane(4, "Cammy");
System.out.println(mommy.numberEggs()); // 4
System.out.println(mommy.name()); // Cammy
```

Behind the scenes, it **==creates a constructor for you with the parameters in the same order in which they appear in the record declaration==**. Omitting or changing the type order will lead to compiler errors:

```java
var mommy1 = new Crane("Cammy", 4); // DOES NOT COMPILE
var mommy2 = new Crane("Cammy"); // DOES NOT COMPILE
```

For each field, it also creates an accessor as the field name, plus a set of parentheses. Unlike traditional *POJOs* or *JavaBeans*, the methods don’t have the prefix ``get`` or ``is``.

**Members Automatically Added to Records**
- ==**Constructor: A constructor with the parameters in the same order as the record declaration**==
- ==**Accessor method: One accessor for each field**==
- ==**``equals()``: A method to compare two elements that returns ``true`` if each field is equal in terms of ``equals()``**==
- ==**``hashCode()``: A consistent ``hashCode()`` method using all of the fields**==
- ==**``toString()``: A ``toString()`` implementation that prints each field of the record in a convenient, easy-to- read format**==

```java
var father = new Crane(0, "Craig");
System.out.println(father); // Crane[numberEggs=0, name=Craig]
var copy = new Crane(0, "Craig");
System.out.println(copy); // Crane[numberEggs=0, name=Craig]
System.out.println(father.equals(copy)); // true
System.out.println(father.hashCode() + ", " + copy.hashCode()); // 1007, 1007
```

it is legal to have a record without any fields. It is simply declared with the ``record`` keyword and parentheses:

```java
public record Crane() {}
```

### Understanding Record Immutability

records don’t have setters. Every field is inherently ``final`` and cannot be modified after it has been written in the constructor. In order to “modify” a record, you have to make a new object and copy all of the data you want to preserve.

```java
var cousin = new Crane(3, "Jenny");
var friend = new Crane(cousin.numberEggs(), "Janeice");
```

Just as interfaces are implicitly ``abstract``, **==records are also implicitly ``final``. The ``final`` modifier is optional but assumed.==**

```java
public final record Crane(int numberEggs, String name) {}
```

**==Like enums, that means you can’t extend or inherit a record.==**

```java
public record BlueCrane() extends Crane {} // DOES NOT COMPILE
```

**==Also like enums, a record can implement a regular or sealed interface, provided it implements all of the abstract methods.==**

```java
public interface Bird {}
public record Crane(int numberEggs, String name) implements Bird {}
```

### Declaring Constructors

What if you need to declare a record with some guards ? 
#### The Long Constructor

can just declare the constructor the compiler normally inserts automatically, which we refer to as the long constructor.

```java
public record Crane(int numberEggs, String name) {
	public Crane(int numberEggs, String name) {
		if (numberEggs < 0) throw new IllegalArgumentException();
		this.numberEggs = numberEggs;
		this.name = name;
	}
}
```

**==The compiler will not insert a constructor if you define one with the same list of parameters in the same order. Since each field is ``final``, the constructor must set every field.==**

```java
public record Crane(int numberEggs, String name) {
	public Crane(int numberEggs, String name) {} // DOES NOT COMPILE
}
```

While being able to declare a constructor is a nice feature of records, it’s also problematic. If we have 20 fields, we’ll need to declare assignments for every one, introducing the boilerplate we sought to remove.

#### Compact Constructors

A *compact constructor* is a special type of constructor used for records to process validation and transformations succinctly. It takes no parameters and implicitly sets all fields.

![[Pasted image 20240330234703.png]]

we can check the values we want, and we don’t have to list all the constructor parameters and trivial assignments. Java will execute the full constructor after the compact constructor. also remember that a compact constructor is declared without parentheses, as the exam might try to trick you on this. we can even transform constructor parameters as we discuss more in the next section.
##### Transforming Parameters

Compact constructors give you the opportunity to apply transformations to any of the input values.

```java
public record Crane(int numberEggs, String name) {
	public Crane {
		if (name == null || name.length() < 1)
			throw new IllegalArgumentException();
		name = name.substring(0,1).toUpperCase() + name.substring(1).toLowerCase();
	}
}
```

**==While compact constructors can modify the constructor parameters, they cannot modify the fields of the record.==**

```java
public record Crane(int numberEggs, String name) {
	public Crane {
		this.numberEggs = 10; // DOES NOT COMPILE
	}
}
```

#### Overloaded Constructors

can also create overloaded constructors that take a completely different list of parameters. They are more closely related to the long-form constructor and don’t use any of the syntactical features of compact constructors.

```java
public record Crane(int numberEggs, String name) {
	public Crane(String firstName, String lastName) {
		this(0, firstName + " " + lastName);
	}
}
```

**==The first line of an overloaded constructor must be an explicit call to another constructor via ``this()``. If there are no other constructors, the long constructor must be called.==**
Also, unlike compact constructors, you can only transform the data on the first line. After the first line, all of the fields will already be assigned, and the object is immutable.

```java
public record Crane(int numberEggs, String name) {
	public Crane(int numberEggs, String firstName, String lastName) {
		this(numberEggs + 1, firstName + " " + lastName);
		numberEggs = 10; // NO EFFECT (applies to parameter, not instance field)
		this.numberEggs = 20; // DOES NOT COMPILE
	}
}
```

also can’t declare two record constructors that call each other infinitely or as a cycle.

```java
public record Crane(int numberEggs, String name) {
	public Crane(String name) {
		this(1); // DOES NOT COMPILE
	}
	public Crane(int numberEggs) {
		this(""); // DOES NOT COMPILE
	}
}
```
### Customizing Records

Records actually support many of the same features as a class.

be familiar with for the exam:
- Overloaded and compact constructors
- Instance methods including overriding any provided methods (accessors, ``equals()``, ``hashCode()``, ``toString()``)
- Nested classes, interfaces, annotations, enum, and records

```java
public record Crane(int numberEggs, String name) {
	@Override public int numberEggs() { return 10; }
	@Override public String toString() { return name; }
}
```

While you can add methods, ``static`` fields, and other data types, **==you cannot add instance fields outside the record declaration, even if they are ``private``==**. Doing so defeats the purpose of using a record and could break immutability!

```java
public record Crane(int numberEggs, String name) {
	private static int type = 10;
	public int size; // DOES NOT COMPILE
	private boolean friendly; // DOES NOT COMPILE
}
```

Records also do not support instance initializers. **==All initialization for the fields of a record must happen in a constructor.==**
 
## Creating Nested Classes

A nested class is a class that is defined within another class. A nested class can come in one of four flavors.

-  ==**Inner class: A non-static type defined at the member level of a class**==
-  ==**Static nested class: A static type defined at the member level of a class**==
-  ==**Local class: A class defined within a method body**==
-  ==**Anonymous class: A special case of a local class that does not have a name==**

There are many benefits of using nested classes. They can define helper classes and restrict them to the containing class, thereby improving encapsulation. They can make it easy to create a class that will be used in only one place. They can even make the code cleaner and easier to read.

### Declaring an Inner Class

**==An inner class, also called a member inner class, is a non-static type defined at the member level of a class (the same level as the methods, instance variables, and constructors)==**. Because they are not top-level types, ==**they can use any of the four access levels**==, not just public and package access.

Inner classes have the following properties:
-  Can be declared ``public``, ``protected``, package, or ``private``
-  Can extend a class and implement interfaces
-  Can be marked ``abstract`` or ``final``
-  Can access members of the outer class, including ``private`` members

the inner class can access variables in the outer class without doing anything special

```java
1: public class Home {
	2: private String greeting = "Hi"; // Outer class instance variable
	3:
	4: protected class Room { // Inner class declaration
		5: public int repeat = 3;
		6: public void enter() {
			7: for (int i = 0; i < repeat; i++) greet(greeting);
		8: }
		9: private static void greet(String message) {
			10: System.out.println(message);
		11: }
	12: }
	13:
	14: public void enterRoom() { // Instance method in outer class
	15: var room = new Room(); // Create the inner class instance
	16: room.enter();
	17: }
	18: public static void main(String[] args) {
	19: var home = new Home(); // Create the outer class instance
	20: home.enterRoom();
	21: } 
}
```

- An inner class declaration looks just like a stand-alone class declaration except that it happens to be located inside another class. Line 7 shows that the inner class just refers to greeting as if it were available in the ``Room`` class. Even though the variable is private, it is accessed within that same class.
- **==Since an inner class is not ``static``, it has to be called using an instance of the outer class==**. That means you have to create two objects. Line 19 creates the outer ``Home`` object, while line 15 creates the inner ``Room`` object. It’s important to notice that line 15 doesn’t require an explicit instance of ``Home`` because it is an instance method within ``Home``. This works because ``enterRoom()`` is an instance method within the ``Home`` class. Both ``Room`` and ``enterRoom()`` are members of ``Home``.

---
**Nested Classes Can Now Have ``static`` Member**

**With the introduction of records in Java 16, the existing rule that prevented an inner class from having any ``static`` members (other than static constants) was removed. ==All four types of nested classes can now define ``static`` variables and methods!**==**

---
#### Instantiating an Instance of an Inner Class

```java
20: public static void main(String[] args) {
	21: var home = new Home();
	22: Room room = home.new Room(); // Create the inner class instance
	23: room.enter();
24: }
```

We need an instance of ``Home`` to create a ``Room``. We can’t just call new ``Room()`` inside the ``static main()`` method, because Java won’t know which instance of ``Home`` it is associated with. Java solves this by calling new as if it were a method on the room variable. We can shorten lines 21–23 to a single line:

```java
21: new Home().new Room().enter(); // Sorry, it looks ugly to us too!
```

#### Referencing Members of an Inner Class

Inner classes can have the same variable names as outer classes, making scope a little tricky. There is a special way of calling this to say which variable you want to access. Here is how to nest multiple classes and access
a variable with the same name in each:

```java
1: public class A {
	2: private int x = 10;
	3: class B {
		4: private int x = 20;
		5: class C {
			6: private int x = 30;
			7: public void allTheX() {
				8: System.out.println(x); // 30
				9: System.out.println(this.x); // 30
				10: System.out.println(B.this.x); // 20
				11: System.out.println(A.this.x); // 10
			12: } 
		} 
	}
	13: public static void main(String[] args) {
		14: A a = new A();
		15: A.B b = a.new B();
		16: A.B.C c = b.new C();
		17: c.allTheX();
	18: }
}
```

- Line 14 instantiates the outermost one.
- Line 15 uses the awkward syntax to instantiate ``a B.`` Notice that the type is ``A.B.``
- On line 16, we instantiate a ``C``. This time, the ``A.B.C`` type is necessary to specify. ``C`` is too deep for Java to know where to look. 
- Then line 17 calls a method on the instance variable ``c``.
- Line 10 uses ``this`` in a special way. We still want an instance variable. But this time, we want the one on the ``B`` class, which is the variable on line 4. 
- Line 11 does the same thing for class ``A``, getting the variable from line 2.

---
**Inner Classes Require an Instance**

```java
public class Fox {
	private class Den {}
	public void goHome() {
		new Den();
	}
	public static void visitFriend() {
		new Den(); // DOES NOT COMPILE
	}
}
	
public class Squirrel {
	public void visitFox() {
		new Den(); // DOES NOT COMPILE
	}
}
```

**The first constructor call compiles because ``goHome()`` is an instance method, and therefore the call is associated with the this instance. The second call does not compile because it is called inside a static method. You can still call the constructor, but you have to explicitly give it a reference to a ``Fox`` instance.**

**The last constructor call does not compile for two reasons. Even though it is an instance method, it is not an instance method inside the ``Fox`` class. Adding a ``Fox`` reference would not fix the problem entirely, though. ``Den`` is ``private`` and not accessible in the ``Squirrel`` class.**

---

### Creating a ``static`` Nested Class
 
 A static nested class is a static type defined at the member level. **==Unlike an inner class, a static nested class can be instantiated without an instance of the enclosing class. The trade-off, though, is that it can’t access instance variables or methods declared in the outer class==**.

In other words, it is like a top-level class except for the following:
-  ==**The nesting creates a namespace because the enclosing class name must be used to refer to it.**==
-  ==**It can additionally be marked ``private`` or ``protected``.**==
-  ==**The enclosing class can refer to the fields and methods of the ``static`` nested class.==**

```java
1: public class Park {
	2: static class Ride {
		3: private int price = 6;
	4: }
	5: public static void main(String[] args) {
		6: var ride = new Ride();
		7: System.out.println(ride.price);
	8: } 
}
```

Since the class is ``static``, you do not need an instance of ``Park`` to use it.

### Writing a Local Class

**==A local class is a nested class defined within a method. Like local variables, a local class declaration does not exist until the method is invoked, and it goes out of scope when the method returns.==** This means you can create instances only from within the method. Those instances can still be returned from the method.

---

**Local classes are not limited to being declared only inside methods. For example, they can be declared inside constructors and initializers.**

---


Local classes have the following properties:
-  ==**They do not have an access modifier.**==
-  ==**They can be declared ``final`` or ``abstract``.**==
-  ==**They have access to all fields and methods of the enclosing class (when defined in an instance method).**==
-  ==**They can access ``final`` and effectively final local variables.==**

```java
1: public class PrintNumbers {
	2: private int length = 5;
	3: public void calculate() {
		4: final int width = 20;
		5: class Calculator {
		6: public void multiply() {
			7: System.out.print(length * width);
		8: }
	9: }
		10: var calculator = new Calculator();
		11: calculator.multiply();
	12: }
	13: public static void main(String[] args) {
		14: var printer = new PrintNumbers();
		15: printer.calculate(); // 100
	16: }
17: }
```

- Lines 5–9 are the local class. That class’s scope ends on line 12, where the method ends.
- Line 7 refers to an instance variable and a final local variable, so both variable references are allowed from within the local class.

```java
public void processData() {
	final int length = 5;
	int width = 10;
	int height = 2;
	class VolumeCalculator {
		public int multiply() {
			return length * width * height; // DOES NOT COMPILE
		}
	}
	width = 2;
}
```

The ``length`` and ``height`` variables are ``final`` and effectively final, respectively, so neither causes a compilation issue. On the other hand, the ``width`` variable is reassigned during the method, so it cannot be effectively final. For this reason, the local class declaration does not compile.

---

**Why Can Local Classes Only Access ``final`` or Effectively Final Variables?**

==**the compiler generates a separate ``.class`` file for each inner class. A separate class has no way to refer to a local variable. However, if the local variable is ``final`` or effectively final, Java can handle it by passing a copy of the value or reference variable to the constructor of the local class==. If it weren’t ``final`` or effectively final, these tricks wouldn’t work because the value could change after the copy was made.**

---

### Defining an Anonymous Class

An anonymous class is a specialized form of a local class that does not have a name. **==It is declared and instantiated all in one statement using the ``new`` keyword, a type name with parentheses, and a set of braces ``{}``. Anonymous classes must extend an existing class or implement an existing interface.==** They are useful when you have a short implementation that will not be used anywhere else.

```java
1: public class ZooGiftShop {
	2: abstract class SaleTodayOnly {
		3: abstract int dollarsOff();
	4: }
	5: public int admission(int basePrice) {
		6: SaleTodayOnly sale = new SaleTodayOnly() {
			7: int dollarsOff() { return 3; }
	8: }; // Don't forget the semicolon!
	9: return basePrice - sale.dollarsOff();
	10: }
}
```

- Lines 2–4 define an ``abstract`` class. 
- Lines 6–8 define the anonymous class anonymous class does not have a name. The code says to instantiate a new ``SaleTodayOnly`` object. ``SaleTodayOnly`` is abstract. This is okay because we provide the class body right there—anonymously.
- Pay special attention to the semicolon on line 8. We are declaring a local variable on these lines. Local variable declarations are required to end with semicolons, just like other Java statements—even if they are long and happen to contain an anonymous class.

```java
1: public class ZooGiftShop {
	2: interface SaleTodayOnly {
		3: int dollarsOff();
	4: }
	5: public int admission(int basePrice) {
		6: SaleTodayOnly sale = new SaleTodayOnly() {
			7: public int dollarsOff() { return 3; }
		8: };
		9: return basePrice - sale.dollarsOff();
	10: } 
}
```

- Lines 2–4 declare an interface instead of an ``abstract`` class. 
- Line 7 is public instead of using default access since interfaces require ``public`` methods. The anonymous class is the same whether you implement an interface or extend a class! Java figures out which one you want automatically.


**==what if we want to both implement an interface and extend a class? You can’t do so with an anonymous class unless the class to extend is ``java.lang.Object``. The ``Object`` class doesn’t count in the rule==**. Remember that an anonymous class is just an unnamed local class. You can write a local class and give it a name if you have this problem. Then you can extend a class and implement as many interfaces as you like. If your code is this complex, a local class probably isn’t the most readable option anyway. 

You can even define anonymous classes outside a method body. The following may look like we are instantiating an interface as an instance variable, but the ``{}`` after the interface name indicates that this is an anonymous class implementing the interface:

```java
public class Gorilla {
	interface Climb {}
	Climb climbing = new Climb() {};
}
```

### Reviewing Nested Classes

![[Pasted image 20240331170453.png]]

![[Pasted image 20240331170503.png]]

## Understanding Polymorphism

the property of an object to take on many different forms. To put this more precisely, a Java object may be accessed using:

- ==**A reference with the same type as the object**==
- ==**A reference that is a superclass of the object**==
- ==**A reference that defines an interface the object implements or inherits==**

**==Furthermore, a cast is not required if the object is being reassigned to a supertype or interface of the object==.**

```java
public class Primate {
    public boolean hasHair() {
        return true;
    }
}

public interface HasTail {
    public abstract boolean isTailStriped();
}

public class Lemur extends Primate implements HasTail {
    public boolean isTailStriped() {
        return false;
    }

    public int age = 10;

    public static void main(String[] args) {
        Lemur lemur = new Lemur();
        System.out.println(lemur.age); // 10
        HasTail hasTail = lemur;
        System.out.println(hasTail.isTailStriped()); // false
        Primate primate = lemur;
        System.out.println(primate.hasHair()); // true
    }
}
```

**==The most important thing to note about this example is that only one object, ``Lemur``, is created==**. Polymorphism enables an instance of ``Lemur`` to be reassigned or passed to a method using one of its supertypes, such as Primate or ``HasTail``.

Once the object has been assigned to a new reference type, only the methods and variables available to that reference type are callable on the object without an explicit cast.

```java
HasTail hasTail = new Lemur();
System.out.println(hasTail.age); // DOES NOT COMPILE
Primate primate = new Lemur();
System.out.println(primate.isTailStriped()); // DOES NOT COMPILE
```

- the reference ``hasTail`` has direct access only to methods defined with the ``HasTail`` interface; therefore, it doesn’t know that the variable age is part of the object.
- Likewise, the reference primate has access only to methods defined in the ``Primate`` class, and it doesn’t have direct access to the ``isTailStriped()`` method.
### Object vs. Reference

In Java, all objects are accessed by reference, so as a developer you never have direct access to the object itself. Conceptually, though, you should consider the object as the entity that exists in memory, allocated by the Java Runtime Environment. Regardless of the type of the reference you have for the object in memory, the object itself doesn’t change.

Since all objects inherit ``java.lang.Object``, they can all be reassigned to`` java.lang.Object``,

```java
Lemur lemur = new Lemur();
Object lemurAsObject = lemur;
```

Even though the ``Lemur`` object has been assigned to a reference with a different type, the object itself has not changed and still exists as a ``Lemur`` object in memory. What has changed, then, is our ability to access methods within the ``Lemur`` class with the ``lemurAsObject`` reference. Without an explicit cast back to ``Lemur``, we no longer have access to the ``Lemur`` properties of the object.
summarize this principle with the following two rules:
1. ==**The type of the object determines which properties exist within the object in memory.**==
2. ==**The type of the reference to the object determines which methods and variables are accessible to the Java program.**==


![[Pasted image 20240331192333.png]]

**==the same object exists in memory regardless of which reference is pointing to it. Depending on the type of the reference, we may only have access to certain methods.==**

---

**Using Interface References**

**When working with a group of objects that implement a common interface, it is considered a good coding practice to use an interface as the reference type. This is especially common with collections**

```java
public void sortAndPrintZooAnimals(List<String> animals) {
	Collections.sort(animals);
	for(String a : animals) System.out.println(a);
}
```

**At no point is this class interested in what the actual underlying object for ``animals`` is. It might be an ``ArrayList`` or another type. The point is, our code works on any of these types because we used the interface reference type rather than a class type.**

---
### Casting Objects

```java
Lemur lemur = new Lemur();
Primate primate = lemur; // Implicit Cast to supertype
Lemur lemur2 = (Lemur)primate; // Explicit Cast to subtype
Lemur lemur3 = primate; // DOES NOT COMPILE (missing cast)
```

- first create a ``Lemur`` object and implicitly cast it to a ``Primate`` reference. Since ``Lemur`` is a subtype of ``Primate``, this can be done without a cast operator.
- then cast it back to a ``Lemur`` object using an explicit cast, gaining access to all of the methods and fields in the ``Lemur`` class.
- The last line does not compile because an explicit cast is required. Even though the object is stored in memory as a ``Lemur`` object, we need an explicit cast to assign it to ``Lemur``.

Casting objects is similar to casting primitives. 
- **==When casting objects, you do not need a cast operator if casting to an inherited supertype. This is referred to as an implicit cast and applies to classes or interfaces the object inherits.==**
- **==Alternatively, to access a subtype of the current reference, you need to perform an explicit cast with a compatible type. If the underlying object is not compatible with the type, then a ``ClassCastException`` will be thrown at runtime.==**

When reviewing a question on the exam that involves casting and polymorphism, be sure to remember what the instance of the object actually is. Then, focus on whether the compiler will allow the object to be referenced with or without explicit casts.

1. ==**Casting a reference from a subtype to a supertype doesn’t require an explicit cast.**==
2. ==**Casting a reference from a supertype to a subtype requires an explicit cast.**==
3. ==**At runtime, an invalid cast of a reference to an incompatible type results in a ``ClassCastException`` being thrown.**==
4. ==**The compiler disallows casts to unrelated types.==**

#### Disallowed Casts

The exam may try to trick you with a cast that the compiler knows is not permitted (aka impossible). 

```java
public class Bird {}

public class Fish {
	public static void main(String[] args) {
		Fish fish = new Fish();
		Bird bird = (Bird)fish; // DOES NOT COMPILE
	}
}
```

the classes ``Fish`` and ``Bird`` are not related through any class hierarchy that the compiler is aware of; therefore, the code will not compile. While they both extend Object implicitly, they are considered unrelated types since one cannot be a subtype of the other.

#### Casting Interfaces

While the compiler can enforce rules about casting to unrelated types for classes, it cannot always do the same for interfaces. instances support multiple inheritance, which limits what the compiler can reason about them. While a given class may not implement an interface, it’s possible that some subclass may implement the interface. When holding a reference to a particular class, the compiler doesn’t know which specific subtype it is holding.

```java
1: interface Canine {}
2: interface Dog {}
3: class Wolf implements Canine {}
4:
5: public class BadCasts {
	6: public static void main(String[] args) {
		7: Wolf wolfy = new Wolf();
		8: Dog badWolf = (Dog)wolfy;
	9: } 
}
```

- a ``Wolf`` object is created and then assigned to a ``Wolf`` reference type on line 7. With interfaces, the compiler has limited ability to enforce many rules because even though a reference type may not implement an interface, one of its subclasses could. 
- Therefore, it allows the invalid cast to the ``Dog`` reference type on line 8, even though ``Dog`` and ``Wolf`` are not related. even though the code compiles, it still throws a ``ClassCastException`` at runtime.

**==the compiler can enforce one rule around interface casting. The compiler does not allow a cast from an interface reference to an object reference if the object type cannot possibly implement the interface, such as if the class is marked ``final``==**

if the ``Wolf`` interface is marked final on line 3, then line 8 no longer compiles. The compiler recognizes that there are no possible subclasses of ``Wolf`` capable of implementing the ``Dog`` interface.
###  The ``instanceof`` Operator

The ``instanceof`` operator can be used to check whether an object belongs to a particular class or interface and to prevent a ``ClassCastException`` at runtime.

```java
1: class Rodent {}
2:
3: public class Capybara extends Rodent {
	4: public static void main(String[] args) {
		5: Rodent rodent = new Rodent();
		6: var capybara = (Capybara)rodent; // ClassCastException
	7: }
8: }
```

```java
6: if(rodent instanceof Capybara c) {
	7: // Do stuff
8: }
```

Now the code snippet doesn’t throw an exception at runtime and performs the cast only if the ``instanceof`` operator is successful. **==Just as the compiler does not allow casting an object to unrelated types, it also does not allow ``instanceof`` to be used with unrelated types==**

```java
public class Bird {}
public class Fish {
	public static void main(String[] args) {
		Fish fish = new Fish();
		if (fish instanceof Bird b) { // DOES NOT COMPILE
			// Do stuff
		}
	}
}
```

### Polymorphism and Method Overriding

In Java, polymorphism states that when you override a method, you replace all calls to it, even those defined in the parent class.

```java
class Penguin {
	public int getHeight() { return 3; }
	public void printInfo() {
		System.out.print(this.getHeight());
	}
}
public class EmperorPenguin extends Penguin {
	public int getHeight() { return 8; }
	public static void main(String []fish) {
		new EmperorPenguin().printInfo(); // 8
	}
}
```

- In this example, the object being operated on in memory is an ``EmperorPenguin``.
- The ``getHeight()`` method is overridden in the subclass, meaning all calls to it are replaced at runtime. Despite ``printInfo()`` being defined in the ``Penguin`` class, calling ``getHeight()`` on the object calls the method associated with the precise object in memory, not the current reference type where it is called.
- Even using the ``this`` reference, which is optional in this example, does not call the parent version because the method has been replaced.

***==Polymorphism’s ability to replace methods at runtime via overriding is one of the most important properties of Java.==***

can choose to limit polymorphic behavior by marking methods ``final``, which prevents them from being overridden by a subclass

---

**Calling the Parent Version of an Overridden Method**

**can use the ``super`` reference to access it.**

```java
class Penguin {
	public int getHeight() { return 3; }
	public void printInfo() {
		System.out.print(super.getHeight()); // DOES NOT COMPILE
	}
}
```

**``super`` refers to the superclass of ``Penguin``; in this case, ``Object``. The solution is to override ``printInfo()`` in the child ``EmperorPenguin`` class and use super there.**

```java
public class EmperorPenguin extends Penguin {
	public int getHeight() { return 8; }
	public void printInfo() {
		System.out.print(super.getHeight());
	}
	public static void main(String []fish) {
		new EmperorPenguin().printInfo(); // 3
	}
}
```

---

#### Overriding vs. Hiding Members

While method overriding replaces the method everywhere it is called, ``static`` method and variable hiding do not. hiding members is not a form of polymorphism since the methods and variables maintain their individual properties. Unlike method overriding, hiding members is very sensitive to the reference type and location where the member is being used.

```java
class Penguin {
	public static int getHeight() { return 3; }
	public void printInfo() {
		System.out.println(this.getHeight());
	}
}
public class CrestedPenguin extends Penguin {
	public static int getHeight() { return 8; }
	public static void main(String... fish) {
		new CrestedPenguin().printInfo(); //3 
	}
}
```

The ``getHeight()`` method is static and is therefore hidden, not overridden. The result is that calling ``getHeight()`` in ``CrestedPenguin`` returns a different value than calling it in ``Penguin``, even if the underlying object is the same 

while you are permitted to use an instance reference to access a ``static`` variable or method, doing so is often discouraged. The compiler will warn you when you access ``static`` members in a non-static way. In this case, the ``this`` reference had no impact on the program output. Besides the location, the reference type can also determine the value you get when you are working with hidden members

```java
class Marsupial {
    protected int age = 2;

    public static boolean isBiped() {
        return false;
    }
}

public class Kangaroo extends Marsupial {
    protected int age = 6;

    public static boolean isBiped() {
        return true;
    }

    public static void main(String[] args) {
        Kangaroo joey = new Kangaroo();
        Marsupial moey = joey;
        System.out.println(joey.isBiped()); // true
        System.out.println(moey.isBiped()); // false
        System.out.println(joey.age); // 6 
        System.out.println(moey.age); // 2
    }
}
```

only one object (of type ``Kangaroo``) is created and stored in memory! Since ``static`` methods can only be hidden, not overridden, Java uses the reference type to determine which version of ``isBiped()`` should be called, resulting in ``joey.isBiped()`` printing true and ``moey.isBiped()`` printing false.
Likewise, the ``age`` variable is hidden, not overridden, so the reference type is used to determine which value to output. This results in`` joey.age`` returning 6 and ``moey.age`` returning 2.
## Summary #OCP_Summary 

**==with interfaces and described how they can support multiple inheritance. Remember, interfaces and their members can include a number of implicit modifiers inserted by the compiler automatically. We then covered all six types of interface members you need to know for the exam: ``abstract`` methods, ``static`` constants, default methods, ``static`` methods, ``private`` methods, and ``private static`` methods.**==

==**enums, which are compile-time constant properties. Simple enums are composed of a list of values, while complex enums can include constructors, methods, and fields. Enums can also be used in ``switch`` statements and expressions. When an enum method is marked ``abstract``, each enum value must provide an implementation.**==

==**sealed classes and how they allow classes to function like enumerated types in which only certain subclasses are permitted. For the exam, it’s important to remember that the subclasses of a sealed class must be marked ``final``, ``sealed``, or ``non-sealed``. If the subclasses of the sealed class are defined in the same file, then the permits clause may be omitted in the sealed class declaration. Finally, sealed interfaces may be used to limit which classes can implement an interface, which interfaces may extend an interface, or both.**==

==**Records are another new feature available in Java. Records are a compact way of declaring an immutable and encapsulated POJO in which the compiler adds a lot of the boilerplate code for you. Remember, encapsulation is the practice of preventing external callers from accessing the internal components of an object. Records include automatic creation of the accessor methods, a long constructor, and useful implementations of ``equals()``, ``hashCode()``, and ``toString()``. Records can include overloaded and compact constructors to support data validation and transformation. Records do not permit instance variables, since this could break immutability, but they do allow methods, static members, and nested types**==

==**An inner class requires an instance of the outer class to use, while a static nested class does not. A local class is commonly defined within a method or block. Local classes can only access local variables that are ``final`` and effectively final. Anonymous classes are a special type of local class that does not have a name. Anonymous classes are required to extend exactly one class or implement one interface. Inner, local, and anonymous classes can access private members of the class in which they are defined, provided the latter two are used inside an instance method.**==

==**polymorphism, which is central to the Java language, and showed how objects can be accessed in a variety of forms. Make sure you understand when casts are needed for accessing objects, and be able to spot the difference between compile-time and runtime cast problems.==**

## Exam Essentials #Essential 

**Be able to write code that creates, extends, and implements interfaces**. Interfaces are specialized abstract types that focus on abstract methods and constant variables. An interface may extend any number of interfaces and, in doing so, inherits their abstract methods. An interface cannot extend a class, nor can a class extend an interface. A class may implement any number of interfaces.

==**Know which interface methods an interface method can reference**. Non-static ``private``, default, and ``abstract`` interface methods are associated with an instance of an interface. Non-static private and default interface methods may reference any method within the interface declaration. Alternatively, ``static`` interface methods are associated with class membership and can only reference other ``static`` members. Finally, ``private`` methods can only be referenced within the interface declaration.==

**Be able to create and use enum types**. An enum is a data structure that defines a list of values. If the enum does not contain any other elements, the semicolon (;) after the values is optional. An enum can be used in ``switch`` statements and contain instance variables, constructors, and methods. Enum constructors are implicitly ``private``. Enums can include methods, both as members or within individual enum values. If the enum declares an abstract method, each enum value must implement it.

**Be able to recognize when sealed classes are being correctly used**. A sealed class is one that defines a list of permitted subclasses that extend it. Be able to use the correct modifier ``(final``, ``sealed``, or ``non-sealed``) with sealed classes. Understand when the permits clause may be excluded.

**Identify properly encapsulated classes**. Instance variables in encapsulated classes are private. All code that retrieves the value or updates it uses methods. Encapsulated classes may include accessor (getter) or mutator (setter) methods, although this is not required.

**Understand records and know which members the compiler is adding automatically**. Records are encapsulated and immutable types in which the compiler inserts a long constructor, accessor methods, and useful implementations of ``equals()``, ``hashCode()``, and ``toString()``. Each of these elements may be overridden. Be able to recognize **==compact constructors and know that they are used only for validation and transformation of constructor parameters, not for accessing fields==**. Recognize that when a record is declared with an instance member, it does not compile.

**Be able to declare and use nested classes**. There are four types of nested types: inner classes, static classes, local classes, and anonymous classes. Instantiating an inner class requires an instance of the outer class. On the other hand, static nested classes can be created without a reference to the outer class. Local and anonymous classes cannot be declared with an access modifier. **==Anonymous classes are limited to extending a single class or implementing one interface==**.

**Understand polymorphism**. An object may take on a variety of forms, referred to as polymorphism. **==The object is viewed as existing in memory in one concrete form but is accessible in many forms through reference variables. Changing the reference type of an object may grant access to new members, but the members always exist in memory.==**

## Review Questions

1. Which of the following are valid record declarations? (Choose all that apply.)

```java
public record Iguana(int age) {
private static final int age = 10; }
public final record Gecko() {}
public abstract record Chameleon() {
private static String name; }
public record BeardedDragon(boolean fun) {
@Override public boolean fun() { return false; } }
public record Newt(long size) {
@Override public boolean equals(Object obj) { return false; }
public void setSize(long size) {
this.size = size;
} }
```

A. Iguana
B. Gecko
C. Chameleon
D. BeardedDragon
E. Newt
F. None of the above

**My Answer: A, B
Correct Answer: B,D**

**Iguana does not compile, as it declares a static field with the same name as an instance field. ==Records are implicitly final and cannot be marked abstract==, which is why Gecko compiles and Chameleon does not**

---

2. Which of the following statements can be inserted in the blank line so that the code will compile
successfully? (Choose all that apply.)

```java
interface CanHop {}
public class Frog implements CanHop {
	public static void main(String[] args) {
	    ???	frog = new TurtleFrog();
	}
}
class BrazilianHornedFrog extends Frog {}
class TurtleFrog extends Frog {}
```

A. Frog
B. TurtleFrog
C. BrazilianHornedFrog
D. CanHop
E. var
F. Long
G. None of the above; the code contains a compilation error.

**My Answer: A,B,D,E**
**Correct Answer: A,B,D,E**

**The blank can be filled with any class or interface that is a supertype of TurtleFrog. Option A is the direct superclass of TurtleFrog, and option B is the same class, so both are correct. TurtleFrog inherits the CanHop interface, so option D is correct. Option E is also correct, as var is permitted when the type is known.**

---

3. What is the result of the following program?

```java
public class Favorites {
enum Flavors {
VANILLA, CHOCOLATE, STRAWBERRY
static final Flavors DEFAULT = STRAWBERRY;
}
public static void main(String[] args) {
for(final var e : Flavors.values())
System.out.print(e.ordinal()+" ");
}
}
```

A. 0 1 2
B. 1 2 3
C. Exactly one line of code does not compile.
D. More than one line of code does not compile.
E. The code compiles but produces an exception at runtime.
F. None of the above

**My Answer: C**
**Correct Answer: C**

**When an enum contains only a list of values, the semicolon (;) after the list is optional. When an enum contains any other members, such as a constructor or variable, the semicolon is required. Since the enum list does not end with a semicolon, the code does not compile, making option C the correct answer**

---

4. What is the output of the following program?

```java
public sealed class ArmoredAnimal permits Armadillo {
public ArmoredAnimal(int size) {}
@Override public String toString() { return "Strong"; }
public static void main(String[] a) {
var c = new Armadillo(10, null);
System.out.println(c);
}
}
class Armadillo extends ArmoredAnimal {
@Override public String toString() { return "Cute"; }
public Armadillo(int size, String name) {
super(size);
}
}
```

A. Strong
B. Cute
C. The program does not compile.
D. The code compiles but produces an exception at runtime.
E. None of the above

**My Answer: C**
**Correct Answer: C**

**A class extending a sealed class must be marked final, sealed, or non-sealed. Since Armadillo is missing a modifier, the code does not compile**

---

5.  Which statements about the following program are correct? (Choose all that apply.)

```java
1: interface HasExoskeleton {
2: double size = 2.0f;
3: abstract int getNumberOfSections();
4: }
5: abstract class Insect implements HasExoskeleton {
6: abstract int getNumberOfLegs();
7: }
8: public class Beetle extends Insect {
9: int getNumberOfLegs() { return 6; }
10: int getNumberOfSections(int count) { return 1; }
11: }
```

A. It compiles without issue.
B. The code will produce a ClassCastException if called at runtime.
C. The code will not compile because of line 2.
D. The code will not compile because of line 5.
E. The code will not compile because of line 8.
F. The code will not compile because of line 10.

**My Answer: F**
**Correct Answer: E**

**The concrete class Beetle extends Insect and inherits two abstract methods, getNumberOfSections() and getNumberOfLegs(). The Beetle class includes an overloaded version of getNumberOfSections() that takes an int value. The method declaration is valid, making option F incorrect, although it does not satisfy the abstract method requirement inherited from HasExoskeleton. For this reason, only one of the two abstract methods is properly overridden. The Beetle class therefore does not compile, and option E is correct.**

---

6. Which statements about the following program are correct? (Choose all that apply.)

```JAVA
1: public abstract interface Herbivore {
2: int amount = 10;
3: public void eatGrass();
4: public abstract int chew() { return 13; }
5: }
6:
7: abstract class IsAPlant extends Herbivore {
8: Object eatGrass(int season) { return null; }
9: }
```

A. It compiles and runs without issue.
B. The code will not compile because of line 1.
C. The code will not compile because of line 2.
D. The code will not compile because of line 4.
E. The code will not compile because of line 7.
F. The code will not compile because line 8 contains an invalid method override.

**My Answer: D,E**
**Correct Answer: D,E**

**Line 4 does not compile, since an abstract method cannot include a body. Line 7 also does not compile because the wrong keyword is used. A class implements an interface; it does not extend it.**

---

7. What is the output of the following program?

```JAVA
1: interface Aquatic {
2: int getNumOfGills(int p);
3: }
4: public class ClownFish implements Aquatic {
5: String getNumOfGills() { return "14"; }
6: int getNumOfGills(int input) { return 15; }
7: public static void main(String[] args) {
8: System.out.println(new ClownFish().getNumOfGills(-1));
9: } }
```

A. 14
B. 15
C. The code will not compile because of line 4.
D. The code will not compile because of line 5.
E. The code will not compile because of line 6.
F. None of the above

**My Answer: B**
**Correct Answer: E**

**The inherited interface method getNumOfGills(int) is implicitly public; therefore, it must be declared public in any concrete class that implements the interface. Since the method uses the package (default) modifier in the ClownFish class, line 6 does not compile, making option E the correct answer.**

---

8. When inserted in order, which modifiers can fill in the blank to create a properly encapsulated class? (Choose all that apply.)

```java
public class Rabbits {
?? int numRabbits = 0;
?? void multiply() {
numRabbits *= 6;
}
?? int getNumberOfRabbits() {
return numRabbits;
}
}
```

A. private, public, and public
B. private, protected, and private
C. private, private, and protected
D. public, public, and public
E. The class cannot be properly encapsulated since multiply() does not begin with set.
F. None of the above

**My Answer: A**
**Correct Answer: A,B,C**

**Instance variables must include the private access modifier, making option D incorrect. While it is common for methods to be public, this is not required.**

---

9. Which of the following statements can be inserted in the blank so that the code will compile successfully? (Choose all that apply.)

```JAVA
abstract class Snake {}
class Cobra extends Snake {}
class GardenSnake extends Cobra {}
public class SnakeHandler {
private Snake snakey;
public void setSnake(Snake mySnake) { this.snakey = mySnake; }
public static void main(String[] args) {
new SnakeHandler().setSnake( );
}
}
```

A. new Cobra()
B. new Snake()
C. new Object()
D. new String("Snake")
E. new GardenSnake()
F. null
G. None of the above. The class does not compile, regardless of the value inserted in the
blank.

**My Answer: C,F**
**Correct Answer: A,E,F**

**The setSnake() method requires an instance of Snake. Cobra is a direct subclass, while GardenSnake is an indirect subclass. For these reasons, options A and E are correct. Option B is incorrect because Snake is abstract and requires a concrete subclass for instantiation. Option C is incorrect because Object is a supertype of Snake, not a subtype. Option D is incorrect as String is an unrelated class and does not inherit Snake. Finally, a null value can always be passed as an object value, regardless of type, so option F is also correct.**

---

10. What types can be inserted in the blanks on the lines marked X and Z that allow the code to compile? (Choose all that apply.)

```java
interface Walk { private static List move() { return null; } }
interface Run extends Walk { public ArrayList move(); }
class Leopard implements Walk {
public ??? move() { // X
return null;
}
}
class Panther implements Run {
public ??? move() { // Z
return null;
}
}
```

A. Integer on the line marked X
B. ArrayList on the line marked X
C. List on the line marked X
D. List on the line marked Z
E. ArrayList on the line marked Z
F. None of the above, since the Run interface does not compile
G. The code does not compile for a different reason.

**My Answer: G**
**Correct Answer: A,B,C,E**

**Walk declares a private method that is not inherited in any of its subtypes. For this reason, any valid class is supported on line X, making options A, B, and C correct. Line Z is more restrictive, with only ArrayList or subtypes of ArrayList supported, making option E correct**

---

11. What is the result of the following code? (Choose all that apply.)

```java
1: public class Movie {
2: private int butter = 5;
3: private Movie() {}
4: protected class Popcorn {
5: private Popcorn() {}
6: public static int butter = 10;
7: public void startMovie() {
8: System.out.println(butter);
9: }
10: }
11: public static void main(String[] args) {
12: var movie = new Movie();
13: Movie.Popcorn in = new Movie().new Popcorn();
14: in.startMovie();
15: } }
```

A. The output is 5.
B. The output is 10.
C. Line 6 generates a compiler error.
D. Line 12 generates a compiler error.
E. Line 13 generates a compiler error.
F. The code compiles but produces an exception at runtime.

**My Answer: B**
**Correct Answer: E**

**Starting with Java 16, inner classes can contain static variables, so the code compiles. Remember that ==private constructors can be used by any methods within the outer class==. The butter reference on line 8 refers to the inner class variable defined on line 6, with the output being 10 at runtime, and making option B correct**

---

12. Which of the following are true about encapsulation? (Choose all that apply.)

A. It allows getters.
B. It allows setters.
C. It requires specific naming conventions.
D. It requires public instance variables.
E. It requires private instance variables.

**My Answer: A,B,E**
**Correct Answer: A,B,E**



---

13. What is the result of the following program?

```JAVA
	public class Weather {
	enum Seasons {
		WINTER, SPRING, SUMMER, FALL
	}
	public static void main(String[] args) {
		Seasons v = null;
		switch (v) {
		case Seasons.SPRING -> System.out.print("s");
		case Seasons.WINTER -> System.out.print("w");
		case Seasons.SUMMER -> System.out.print("m");
		default -> System.out.println("missing data"); }
	}
}
```

A. s
B. w
C. m
D. missing data
E. Exactly one line of code does not compile.
F. More than one line of code does not compile.
G. The code compiles but produces an exception at runtime.

**My Answer: F**
**Correct Answer: F**

**When using an enum in a switch expression, the case statement must be made up of the enum values only. If the enum name is used in the case statement value, then the code does not compile.** 

---

14. Which statements about sealed classes are correct? (Choose all that apply.)

A. A sealed interface restricts which subinterfaces may extend it.
B. A sealed class cannot be indirectly extended by a class that is not listed in its permits clause.
C. A sealed class can be extended by an abstract class.
D. A sealed class can be extended by a subclass that uses the non-sealed modifier.
E. A sealed interface restricts which subclasses may implement it.
F. A sealed class cannot contain any nested subclasses.
G. None of the above

**My Answer: C,D**
**Correct Answer: A,C,E**

**A sealed interface restricts which interfaces may extend it, or which classes may implement it, making options A and E correct. Option C is correct. While a sealed class is commonly extended by a subclass**
**marked final, it can also be extended by a sealed or non-sealed subclass marked abstract**

---

15. Which lines, when entered independently into the blank, allow the code to print Not scared at runtime? (Choose all that apply.)

```JAVA
public class Ghost {
public static void boo() {
System.out.println("Not scared");
}
protected final class Spirit {
public void boo() {
System.out.println("Booo!!!");
}
}
public static void main(String... haunt) {
var g = new Ghost().new Spirit() {};
???;
}
}
```

A. g.boo()
B. g.super.boo()
C. new Ghost().boo()
D. g.Ghost.boo()
E. new Spirit().boo()
F. Ghost.boo()
G. None of the above

**My Answer: B,C,D,F**
**Correct Answer: G**

**Trick question—the code does not compile! For this reason, option G is correct. The Spirit class is marked final, so it cannot be extended. The main() method uses an anonymous class that inherits from Spirit, which is not allowed**

---

16. The following code appears in a file named Ostrich.java. What is the result of compiling the source file?

```java
1: public class Ostrich {
2: private int count;
3: static class OstrichWrangler {
4: public int stampede() {
5: return count;
6: } } }
```

A. The code compiles successfully, and one bytecode file is generated: Ostrich.class.
B. The code compiles successfully, and two bytecode files are generated: Ostrich.class and OstrichWrangler.class.
C. The code compiles successfully, and two bytecode files are generated: Ostrich.class and Ostrich$OstrichWrangler.class.
D. A compiler error occurs on line 3.
E. A compiler error occurs on line 5.

**My Answer: E**
**Correct Answer: E**

**The OstrichWrangler class is a static nested class; therefore, it cannot access the instance member count. For this reason, line 5 does not compile, and option E is correct.**

---

17.  Which lines of the following interface declarations do not compile? (Choose all that apply.)

```java
1: public interface Omnivore {
2: int amount = 10;
3: static boolean gather = true;
4: static void eatGrass() {}
5: int findMore() { return 2; }
6: default float rest() { return 2; }
7: protected int chew() { return 13; }
8: private static void eatLeaves() {}
9: }
```

A. All of the lines compile without issue.
B. Line 2
C. Line 3
D. Line 4
E. Line 5
F. Line 6
G. Line 7
H. Line 8

**My Answer: E,G**
**Correct Answer: E,G**

**Lines 2 and 3 compile with interface variables implicitly public, static, and final. Line 4 also compiles, as static methods are implicitly public. Line 5 does not compile, making option E correct. Non-static interface methods with a body must be explicitly marked private or default. Line 6 compiles, with the public modifier being added by the compiler. Line 7 does not compile, as interfaces do not have protected members, making option G correct. Finally, line 8 compiles without issue.**

---

18. What is printed by the following program?

```java
public class Deer {
enum Food {APPLES, BERRIES, GRASS}
protected class Diet {
private Food getFavorite() {
return Food.BERRIES;
}
}
public static void main(String[] seasons) {
System.out.print(switch(new Diet().getFavorite()) {
case APPLES -> "a";
case BERRIES -> "b";
default -> "c";
});
} }
```

A. a
B. b
C. c
D. The code declaration of the Diet class does not compile.
E. The main() method does not compile.
F. The code compiles but produces an exception at runtime.
G. None of the above

**My Answer: B**
**Correct Answer: E**

**Diet is an inner class, which requires an instance of Deer to instantiate. Since the main() method is static, there is no such instance. Therefore, the main() method does not compile, and option E is correct**

---

19. Which of the following are printed by the Bear program? (Choose all that apply.)

```JAVA
public class Bear {
enum FOOD {
BERRIES, INSECTS {
public boolean isHealthy() { return true; }},
FISH, ROOTS, COOKIES, HONEY;
public abstract boolean isHealthy();
}
public static void main(String[] args) {
System.out.print(FOOD.INSECTS);
System.out.print(FOOD.INSECTS.ordinal());
System.out.print(FOOD.INSECTS.isHealthy());
System.out.print(FOOD.COOKIES.isHealthy());
}
}
```

A. insects
B. INSECTS
C. 0
D. 1
E. false
F. true
G. The code does not compile.

**My Answer: G**
**Correct Answer: G**



---

20. Which statements about polymorphism and method inheritance are correct? (Choose all that apply.)
A. Given an arbitrary instance of a class, it cannot be determined until runtime which overridden method will be executed in a parent class.
B. It cannot be determined until runtime which hidden method will be executed in a parent class.
C. Marking a method static prevents it from being overridden or hidden.
D. Marking a method final prevents it from being overridden or hidden.
E. The reference type of the variable determines which overridden method will be called at runtime.
F. The reference type of the variable determines which hidden method will be called at runtime.

**My Answer: A,D,F**
**Correct Answer: A,D,F**

**Polymorphism is the property of an object to take on many forms. Part of polymorphism is that methods are replaced through overriding wherever they are called, regardless of whether they’re in a parent or child class. For this reason, option A is correct, and option E is incorrect. With hidden static methods, Java relies on the location and reference type to determine which method is called, making option B incorrect and option F correct. Finally, making a method final, not static, prevents it from being overridden, making option D correct and option C incorrect.**

---

21. Given the following record declaration, which lines of code can fill in the blank and allow the code to compile? (Choose all that apply.)

```java
public record RabbitFood(int size, String brand, LocalDate expires) {
public static int MAX_STORAGE = 100;
public RabbitFood() {
???;
}
}
```

A. size = MAX_STORAGE
B. this.size = 10
C. if(expires.isAfter(LocalDate.now())) throw new
RuntimeException()
D. if(brand== null) super.brand = "Unknown"
E. throw new RuntimeException()
F. None of the above

**My Answer: A,C,F**
**Correct Answer: F**

**==The record defines an overloaded constructor using parentheses, not a compact one. For this reason, the first line must be a call to another constructor, such as this(500, "Acme", LocalDate.now())==. For this reason, the code does not compile and option F is correct**

---

22. Which of the following can be inserted in the rest() method? (Choose all that apply.)

```JAVA
public class Lion {
class Cub {}
static class Den {}
static void rest() {
???;
} }
```

A. Cub a = Lion.new Cub()
B. Lion.Cub b = new Lion().Cub()
C. Lion.Cub c = new Lion().new Cub()
D. var d = new Den()
E. var e = Lion.new Cub()
F. Lion.Den f = Lion.new Den()
G. Lion.Den g = new Lion.Den()
H. var h = new Cub()

**My Answer: C,D,H**
**Correct Answer: C,D,G**

**Option C correctly creates an instance of an inner class Cub using an instance of the outer class Lion. Options A, B, E, and H use incorrect syntax for creating an instance of the Cub class. Options D and G correctly create an instance of the static nested Den class, which does not require an instance of Lion, while option F uses invalid syntax.**

---

23. Given the following program, what can be inserted into the blank line that would allow it to print Swim! at runtime?

```java
interface Swim {
default void perform() { System.out.print("Swim!"); }
}
interface Dance {
default void perform() { System.out.print("Dance!"); }
}
public class Penguin implements Swim, Dance {
public void perform() { System.out.print("Smile!"); }
private void doShow() {
;
}
public static void main(String[] eggs) {
new Penguin().doShow();
}
}
```

A. super.perform()
B. Swim.perform()
C. super.Swim.perform()
D. Swim.super.perform()
E. The code does not compile regardless of what is inserted into the blank.
F. The code compiles, but due to polymorphism, it is not possible to produce the requested
output without creating a new object.

**My Answer: D**
**Correct Answer: D**

**if a class or interface inherits two interfaces containing default methods with the same signature, it must override the method with its own implementation. The Penguin class does this correctly, so option E is incorrect. The way to access an inherited default method is by using the syntax Swim.super.perform(), making option D correct**

---

24. Which lines of the following interface do not compile? (Choose all that apply.)

```JAVA
1: public interface BigCat {
2: abstract String getName();
3: static int hunt() { getName(); return 5; }
4: default void climb() { rest(); }
5: private void roar() { getName(); climb(); hunt(); }
6: private static boolean sneak() { roar(); return true; }
7: private int rest() { return 2; };
8: }
```

A. Line 2
B. Line 3
C. Line 4
D. Line 5
E. Line 6
F. Line 7
G. None of the above

**My Answer: B,E**
**Correct Answer: B,E**

**Line 3 does not compile because the static method hunt() cannot access an abstract instance method getName(), making option B correct. Line 6 does not compile because the private static method sneak() cannot access the private instance method roar(), making option E correct. The rest of the lines compile without issue.**

---

25. What does the following program print?

```java
1: public class Zebra {
2: private int x = 24;
3: public int hunt() {
4: String message = "x is ";
5: abstract class Stripes {
6: private int x = 0;
7: public void print() {
8: System.out.print(message + Zebra.this.x);
9: }
10: }
11: var s = new Stripes() {};
12: s.print();
13: return x;
14: }
15: public static void main(String[] args) {
16: new Zebra().hunt();
17: } }
```

A. x is 0
B. x is 24
C. Line 6 generates a compiler error.
D. Line 8 generates a compiler error.
E. Line 11 generates a compiler error.
F. None of the above

**My Answer: A**
**Correct Answer: B**

**Zebra.this.x is the correct way to refer to x in the Zebra class. Line 5 defines an abstract local class within a method, while line 11 defines a concrete anonymous class that extends the Stripes class. The code compiles without issue and prints x is 24 at runtime, making option B the correct answer.**

---

26.   Which statements about the following enum are true? (Choose all that apply.)

```JAVA
1: public enum Animals {
2: MAMMAL(true), INVERTEBRATE(Boolean.FALSE), BIRD(false),
3: REPTILE(false), AMPHIBIAN(false), FISH(false) {
4: public int swim() { return 4; }
5: }
6: final boolean hasHair;
7: public Animals(boolean hasHair) {
8: this.hasHair = hasHair;
9: }
10: public boolean hasHair() { return hasHair; }
11: public int swim() { return 0; }
12: }
```

A. Compiler error on line 2
B. Compiler error on line 3
C. Compiler error on line 7
D. Compiler error on line 8
E. Compiler error on line 10
F. Compiler error on another line
G. The code compiles successfully.

**My Answer: C,F**
**Correct Answer: C,F**

**Enums are required to have a semicolon (;) after the list of values if there is anything else in the enum. Don’t worry; you won’t be expected to track down missing semicolons on the whole exam—only on enum questions. For this reason, line 5 should have a semicolon after it since it is the end of the list of enums, making option F correct. Enum constructors are implicitly private, making option C correct as well. The rest of the enum compiles without issue.**

---

27. Assuming a record is defined with at least one field, which components does the compiler always insert, each of which may be overridden or redeclared? (Choose all that apply.)
A. A no-argument constructor
B. An accessor method for each field
C. The toString() method
D. The equals() method
E. A mutator method for each field
F. A sort method for each field
G. The hashCode() method

**My Answer: B,C,D,G**
**Correct Answer: B,C,D,G**


---

28. Which of the following classes and interfaces do not compile? (Choose all that apply.)

```java
public abstract class Camel { void travel(); }
public interface EatsGrass { private abstract int chew(); }
public abstract class Elephant {
abstract private class SleepsAlot {
abstract int sleep();
} }
public class Eagle { abstract soar(); }
public interface Spider { default void crawl() {} }
```

A. Camel
B. EatsGrass
C. Elephant
D. Eagle
E. Spider
F. None of the classes or interfaces compile.

**My Answer: B,D,E**
**Correct Answer: A,B,D**

**Camel does not compile because the travel() method does not declare a body, nor is it marked abstract, making option A correct. EatsGrass also does not compile because an interface method cannot be marked both private and abstract, making option B correct. Finally, Eagle does not compile because it declares an abstract method soar() in a concrete class, making option D correct. The other classes compile without issue.**

---

29. How many lines of the following program contain a compilation error?

```JAVA
1: class Primate {
2: protected int age = 2;
3: { age = 1; }
4: public Primate() {
5: this().age = 3;
6: }
7: }
8: public class Orangutan {
9: protected int age = 4;
10: { age = 5; }
11: public Orangutan() {
12: this().age = 6;
13: }
14: public static void main(String[] bananas) {
15: final Primate x = (Primate)new Orangutan();
16: System.out.println(x.age);
17: }
18: }
```

A. None, and the program prints 1 at runtime.
B. None, and the program prints 3 at runtime.
C. None, but it causes a ClassCastException at runtime.
D. 1
E. 2
F. 3
G. 4

**My Answer: F**
**Correct Answer: F**

**The code does not compile, so options A through C are incorrect. Both lines 5 and 12 do not compile, as this() is used instead of this. Remember, this() refers to calling a constructor, whereas this is a reference to the current instance. Next, the compiler does not allow casting to an unrelated class type. Since Orangutan is not a subclass of Primate, the cast on line 15 is invalid, and the code does not compile. Due to these three lines containing compilation errors, option F is the correct answer.**

---

30. Assuming the following classes are declared as top-level types in the same file, which classes contain compiler errors? (Choose all that apply.)

```JAVA
sealed class Bird {
public final class Flamingo extends Bird {}
}
sealed class Monkey {}
class EmperorTamarin extends Monkey {}
non-sealed class Mandrill extends Monkey {}
sealed class Friendly extends Mandrill permits Silly {}
final class Silly {}
```

A. Bird
B. Monkey
C. EmperorTamarin
D. Mandrill
E. Friendly
F. Silly
G. All of the classes compile without issue.

**My Answer: G**
**Correct Answer: C,E**
 
 **Bird and its nested Flamingo subclass compile without issue. The permits clause is optional if the subclass is nested or declared in the same file. For this reason, Monkey and its subclass Mandrill also compile without issue. ==EmperorTamarin does not compile, as it is missing a non-sealed, sealed, or final modifier, making option C correct==. ==Friendly also does not compile, since it lists a subclass Silly that does not extend it, making option E correct==. While the permits clause is optional, the extends clause is not. Silly compiles just fine. Even though it does not extend Friendly, the compiler error is in the sealed class.**

---


# Chapter 8 - Lambdas and Functional Interfaces #Chapter

## Writing Simple Lambdas

Functional programming is a way of writing code more declaratively. You specify what you want to do rather than dealing with the state of objects. You focus more on expressions than loops.

Functional programming uses lambda expressions to write code. A lambda expression is a block of code that gets passed around. a lambda expression as an unnamed method existing inside an anonymous class. **==It has parameters and a body just like full-fledged methods do, but it doesn’t have a name like a real method.==**

### Looking at a Lambda Example

```java
public record Animal(String species, boolean canHop, boolean canSwim) { }

public interface CheckTrait {
	boolean test(Animal a);
}

public class CheckIfHopper implements CheckTrait {
	public boolean test(Animal a) {
		return a.canHop();
	}
}
```

This is part of the problem that lambdas solve

```java
1: import java.util.*;
2: public class TraditionalSearch {
	3: public static void main(String[] args) {
		4:
		5: // list of animals
		6: var animals = new ArrayList<Animal>();
		7: animals.add(new Animal("fish", false, true));
		8: animals.add(new Animal("kangaroo", true, false));
		9: animals.add(new Animal("rabbit", true, false));
		10: animals.add(new Animal("turtle", false, true));
		11:
		12: // pass class that does check
		13: print(animals, new CheckIfHopper());
	14: }
	15: private static void print(List<Animal> animals, CheckTrait checker) {
		16: for (Animal animal : animals) {
		17:
		18: // General check
			19: if (checker.test(animal))
				20: System.out.print(animal + " ");
			21: }
			22: System.out.println();
	23: }
24: }
```

What happens if we want to print the ``Animals`` that swim? Sigh. We need to write another class, ``CheckIfSwims``. Granted, it is only a few lines, but it is a whole new file.

```java
13: print(animals, a -> a.canHop());
```

We only have to add one line of code—no need for an extra class to do something simple. Here’s that other line:

```java
13: print(animals, a -> a.canSwim());
// ...
13: print(animals, a -> !a.canSwim());
```

The point is that it is really easy to write code that uses lambdas once you get the basics in place. **==This code uses a concept called deferred execution. Deferred execution means that code is specified now but will run later.==**

### Learning Lambda Syntax

One of the simplest lambda expressions is

```java
a -> a.canHop()
```

**==Lambdas work with interfaces that have exactly one abstract method.==**
**==Java relies on *context* when figuring out what lambda expressions mean. Context refers to where and how the lambda is interpreted.==**

```java
print(animals, a -> a.canHop());
```

The ``print()`` method expects a ``CheckTrait`` as the second parameter:

```java
private static void print(List<Animal> animals, CheckTrait checker) { ... }
```

Since we are passing a lambda instead, Java tries to map our lambda to the abstract method declaration in the ``CheckTrait`` interface:

```java
boolean test(Animal a);
```

Since that interface’s method takes an ``Animal``, the lambda parameter has to be an ``Animal``. And since that interface’s method returns a ``boolean``, we know the lambda returns a ``boolean``.

```java
a -> a.canHop()
(Animal a) -> { return a.canHop(); } // Identical !
```

The first example, shown in Figure 8.1, has three parts:

![[Pasted image 20240402190013.png]]

-  ==**A single parameter specified with the name a**==
-  ==**The arrow operator (->) to separate the parameter and body**==
-  ==**A body that calls a single method and returns the result of that method==**


The second example shows the most verbose form of a lambda that returns a ``boolean`` in Figure 8.2

![[Pasted image 20240402190127.png]]

-  ==**A single parameter specified with the name a and stating that the type is ``Animal``**==
-  ==**The arrow operator (->) to separate the parameter and body**==
-  ==**A body that has one or more lines of code, including a semicolon and a ``return`` statement==**

**==The parentheses around the lambda parameters can be omitted only if there is a single parameter and its type is not explicitly stated. We can omit braces when we have only a single statement. Java allows you to omit a ``return`` statement and semicolon ``(;)`` when no braces are used.==** This special shortcut doesn’t work when you have two or more statements.

The syntax in Figure 8.1 and Figure 8.2 can be mixed and matched.

```java
a -> { return a.canHop(); }
(Animal a) -> a.canHop()
```

---

**fun fact: s -> {} is a valid lambda. If there is no code on the right side of the expression, you don’t need the semicolon or return statement.** #TIP 

---

![[Pasted image 20240402191012.png]]

The final two rows take two parameters and ignore one of them—there isn’t a rule that says you must use all defined parameters.

![[Pasted image 20240402191042.png]]

Remember that the parentheses are optional only when there is one parameter and it doesn’t have a type declared.

---

**Assigning Lambdas to ``var``**

```java
var invalid = (Animal a) -> a.canHop(); // DOES NOT COMPILE
```

**Java inferring information about the lambda from the context? Well, ``var`` assumes the type based on the context as well. There’s not enough context here! ==Neither the lambda nor ``var`` have enough information to determine what type of functional interface should be used==.**

----
## Coding Functional Interfaces

**==A functional interface is an interface that contains a single abstract method.==**
###  Defining a Functional Interface

```java
@FunctionalInterface
public interface Sprint {
	public void sprint(int speed);
}
public class Tiger implements Sprint {
	public void sprint(int speed) {
		System.out.println("Animal is sprinting fast! " + speed);
	}
}
```

the ``Sprint`` interface is a functional interface because it contains exactly one abstract method, and the ``Tiger`` class is a valid class that implements the interface.

---
**The ``@FunctionalInterface`` Annotation**

**The ``@FunctionalInterface`` annotation tells the compiler that you intend for the code to be a functional interface. If the interface does not follow the rules for a functional interface, the compiler will give you an error**

```java
@FunctionalInterface
public interface Dance { // DOES NOT COMPILE
	void move();
	void rest();
}
```

**Java includes ``@FunctionalInterface`` on some, but not all, functional interfaces. This annotation means the authors of the interface promise it will be safe to use in a lambda in the future. However, just because you don’t see the annotation doesn’t mean it’s not a functional interface. Remember that having exactly one abstract method is what makes it a functional interface, not the annotation.**

---

```java
public interface Dash extends Sprint {}
public interface Skip extends Sprint {
	void skip();
}
public interface Sleep {
	private void snore() {}
	default int getZzz() { return 1; }
}
public interface Climb {
	void reach();
	default void fall() {}
	static int getBackUp() { return 100; }
	private static boolean checkHeight() { return true; }
}
```

- The ``Dash`` interface is a functional interface because it extends the ``Sprint`` interface and inherits the single abstract method ``sprint()``.
- The ``Skip`` interface is not a valid functional interface because it has two abstract methods: the inherited ``sprint()`` method and the declared ``skip()`` method.
- The ``Sleep`` interface is also not a valid functional interface. Neither ``snore()`` nor ``getZzz()`` meets the criteria of a single abstract method. **==Even though default methods function like abstract methods, in that they can be overridden in a class implementing the interface, they are insufficient for satisfying the single abstract method requirement.==**
- the ``Climb`` interface is a functional interface. Despite defining a slew of methods, it contains only one abstract method: ``reach()``.

### Adding Object Methods

All classes inherit certain methods from ``Object``.

-  `public String toString()`
-  `public boolean equals(Object)`
-  `public int hashCode()`

**==there is one exception to the single abstract method rule that you should be familiar with. If a functional interface includes an ``abstract`` method with the same signature as a ``public`` method found in ``Object``, those methods do not count toward the single abstract method test.==** The motivation behind this rule is that any class that implements the interface will inherit from ``Object``, as all classes do, and therefore always implement these methods.

---

**Since Java assumes all classes ``extend`` from ``Object``, you also cannot declare an interface method that is incompatible with Object. For example, declaring an abstract method ``int toString()`` in an interface would not compile since Object’s version of the method returns a ``String``.**

---

```java
public interface Soar {
	abstract String toString(); // Not functional interface
}
```

Since ``toString()`` is a public method implemented in ``Object``, it does not count toward the single abstract method test

```java
public interface Dive {
	String toString();
	public boolean equals(Object o);
	public abstract int hashCode();
	public void dive(); // Functional Interface
}
```

The ``dive()`` method is the single ``abstract`` method, while the others are not counted since they are ``public`` methods defined in the ``Object`` class.

Be wary of examples that resemble methods in the ``Object`` class but are not actually defined in the ``Object`` class

```java
public interface Hibernate {
	String toString();
	public boolean equals(Hibernate o);
	public abstract int hashCode();
	public void rest();
}
```

Despite looking a lot like our ``Dive`` interface, the ``Hibernate`` interface uses ``equals(Hibernate)`` instead of ``equals(Object)``. Because this does not match the method signature of the ``equals(Object)`` method defined in the ``Object`` class, this interface is counted as containing two abstract methods: ``equals(Hibernate)`` and ``rest()``

## Using Method References

Method references are another way to make the code easier to read, such as simply mentioning the name of the method.

```java
public interface LearnToSpeak {
	void speak(String sound);
}

	public class DuckHelper {
	public static void teacher(String name, LearnToSpeak trainer) {
		// Exercise patience (omitted)
		trainer.speak(name);
	}
}

public class Duckling {
	public static void makeSound(String sound) {
		LearnToSpeak learner = s -> System.out.println(s);
		DuckHelper.teacher(sound, learner);
	}
}
```

There’s a bit of redundancy, though. The lambda declares one parameter named ``s``. However, it does nothing other than pass that parameter to another method. A method reference lets us remove that redundancy and instead write this:

```java
LearnToSpeak learner = System.out::println;
```

The ``::`` operator tells Java to call the ``println()`` method later

**==A method reference and a lambda behave the same way at runtime==**. You can pretend the compiler turns your method references into lambdas for you. There are four formats for method references:

-  ==**static methods**==
-  ==**Instance methods on a particular object**==
-  ==**Instance methods on a parameter to be determined at runtime**==
-  ==**Constructors==**

### Calling ``static`` Methods

```java
interface Converter {
	long round(double num);
}
```

can implement this interface with the ``round()`` method in ``Math``. Here we assign a method reference and a lambda to this functional interface:

```java
14: Converter methodRef = Math::round;
15: Converter lambda = x -> Math.round(x);
16:
17: System.out.println(methodRef.round(100.1)); // 100
```

On line 14, we reference a method with one parameter, and Java knows that it’s like a lambda with one parameter. Additionally, Java knows to pass that parameter to the method. With both lambdas and method references, Java infers information from the *context*. Java looks for a method that matches that description. If it can’t find it or finds multiple matches, then the compiler will report an error. The latter is sometimes called an ambiguous type error.

### Calling Instance Methods on a Particular Object

```java
interface StringStart {
	boolean beginningCheck(String prefix);
}

18: var str = "Zoo";
19: StringStart methodRef = str::startsWith;
20: StringStart lambda = s -> str.startsWith(s);
21:
22: System.out.println(methodRef.beginningCheck("A")); // false
```

Line 19 shows that we want to call ``str.startsWith()`` and pass a single parameter to be supplied at runtime.
**==A method reference doesn’t have to take any parameters.==**

```java
interface StringChecker {
boolean check();
}

18: var str = "";
19: StringChecker methodRef = str::isEmpty;
20: StringChecker lambda = () -> str.isEmpty();
21:
22: System.out.print(methodRef.check()); // true
```

Since the method on ``String`` is an instance method, we call the method reference on an instance of the ``String`` class. While all method references can be turned into lambdas, the opposite is not always true.

```java
var str = "";
StringChecker lambda = () -> str.startsWith("Zoo");

StringChecker methodReference = str::startsWith; // DOES NOT COMPILE
StringChecker methodReference = str::startsWith("Zoo"); // DOES NOT COMPILE
```

### Calling Instance Methods on a Parameter

```java
interface StringParameterChecker {
	boolean check(String text);
}

23: StringParameterChecker methodRef = String::isEmpty;
24: StringParameterChecker lambda = s -> s.isEmpty();
25:
26: System.out.println(methodRef.check("Zoo")); // false
```

Line 23 says the method that we want to call is declared in ``String``. It looks like a ``static`` method, but it isn’t. Instead, Java knows that ``isEmpty()`` is an instance method that does not take any parameters. Java uses the parameter supplied at runtime as the instance on which the method is called.

can even combine the two types of instance method references.

```java
interface StringTwoParameterChecker {
	boolean check(String text, String prefix);
}
```

Pay attention to the parameter order when reading the implementation:

```java
26: StringTwoParameterChecker methodRef = String::startsWith;
27: StringTwoParameterChecker lambda = (s, p) -> s.startsWith(p);
28:
29: System.out.println(methodRef.check("Zoo", "A")); // false
```

Since the functional interface takes two parameters, Java has to figure out what they represent. The first one will always be the instance of the object for instance methods. Any others are to be method parameters.

line 26 may look like a ``static`` method, but it is really a method reference declaring that the instance of the object will be specified later. Line 27 shows some of the power of a method reference.

### Calling Constructors

A constructor reference is a special type of method reference that uses ``new`` instead of a method and instantiates an object.

```java
interface EmptyStringCreator {
	String create();
}

30: EmptyStringCreator methodRef = String::new;
31: EmptyStringCreator lambda = () -> new String();
32:
33: var myString = methodRef.create();
34: System.out.println(myString.equals("Snake")); // false
```

```java
interface StringCopier {
	String copy(String value);
}
```

In the implementation, notice that line 32 in the following example has the same method reference as line 30 in the previous example:

```java
32: StringCopier methodRef = String::new;
33: StringCopier lambda = x -> new String(x);
34:
35: var myString = methodRef.copy("Zebra");
36: System.out.println(myString.equals("Zebra")); // true
```

This means you can’t always determine which method can be called by looking at the method reference. **==Instead, you have to look at the context to see what parameters are used and if there is a return type.==**

### Reviewing Method References

![[Pasted image 20240402200041.png]]

## Working with Built-in Functional Interfaces

