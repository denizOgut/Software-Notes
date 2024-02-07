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

==**Essential whitespace is the intentional indentation and formatting that directly contributes to the structure and readability of your String. Incidental whitespace, on the other hand, is extra spacing added for code readability, but it doesn't affect the actual String value.**== 

You can freely adjust incidental whitespace without impacting your String content. ==**Visualize a vertical line on the leftmost non-whitespace character in your text block – everything to the left is incidental whitespace, and everything to the right is essential whitespace.**== Adjusting the left side won't change your String; it's there solely for code aesthetics.

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

This chapter presented how to make intelligent decisions in Java.

We covered basic decision-making constructs such as if, else, and switch statements and showed how to use them to change the path of the process at runtime. We also presented newer features in the Java language, including pattern matching and switch expressions, both designed to reduce boilerplate code.

We then moved our discussion to repetition control structures, starting with while and do/while loops.

Next, we covered the extremely convenient repetition control structures: the for and for-each loops. While their syntax is more complex than the traditional while or do/while loops, they are extremely useful in everyday coding and allow you to create complex expressions in a single line of code.

We concluded this chapter by discussing advanced control options and how flow can be enhanced through nested loops coupled with break, continue, and return statements.

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

this is an example of a reference type. reference types are created using the *new* keyword. In Java, these two
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

Java combines the two String objects. Placing one String before the other String and combining them is called string *concatenation.* 
The exam creators like string concatenation because the ``+`` operator can be used in two ways within the same line of code.

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
- Finally, the last example shows how ``null`` is represented as a string when concatenated or printed, giving us ``"cnull"``.

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

For all these methods, you need to remember that a string is a sequence of characters and ==**Java counts from 0 when indexed.**==

also need to know that a ==**String is immutable, or unchangeable. This means calling a method on a String will return a different String object rather than changing the value of the reference.**==

#### Determining the Length

The method ``length()`` returns the number of characters in the String.
```java
public int length()
```

```java
var name = "animals";
System.out.println(name.length()); // 7
```

Java counts from 0? The difference is that zero counting happens only when you’re using indexes or positions 
within a list. When determining the total size or length, Java uses normal counting again.

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
 
 These methods remove blank space from the beginning and/or end of a String. The`` strip()`` and ``trim()`` methods remove whitespace from the beginning and end of a String. In terms of the exam, whitespace consists of spaces along with the \t (tab) and \n (newline) characters. Other characters, such as \r (carriage return), are also included in what gets trimmed.
The ``strip()`` method does everything that ``trim()`` does, but it supports Unicode.

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
System.out.println(text.trim().length()); // 3
System.out.println(text.strip().length()); // 3
System.out.println(text.stripLeading().length()); // 5
System.out.println(text.stripTrailing().length());// 4
```

First, remember that ``\t`` is a single character. The backslash escapes the t to represent a tab.
The second example gets rid of the leading tab, subsequent spaces, and the trailing newline. It leaves the spaces that are in the middle of the string.
The remaining examples just print the number of characters remaining

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

The ``stripIndent()`` method is useful when a String was built with concatenation rather than using a text block. ==**It gets rid of all incidental whitespace.**== This means that all non-blank lines are shifted left so the same number of whitespace characters are removed from each line and the first character that remains is not blank

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
15: + " b\n"
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

#### Translating Escapes

When we escape characters, we use a single backslash. For example, ``\t`` is a tab. If we don’t want this behavior, we add another backslash to escape the backslash, so ``\\t`` is the literal string ``\t``.
The ``translateEscapes()`` method takes these literals and turns them into the equivalent escaped character.

```java
public String translateEscapes()
```

```java
var str = "1\\t2";
System.out.println(str); // 1\t2
System.out.println(str.translateEscapes()); // 1 2
```

- The first line prints the literal string \t because the backslash is escaped.
- The second line prints an actual tab since we translated the escape.

This method can be used for escape sequences such as ``\t`` (tab), ``\n`` (new line), ``\s`` (space), ``\"`` (double quote), and ``\'`` (single quote.)

#### Checking for Empty or Blank Strings

```java
public boolean isEmpty()
public boolean isBlank()
```

```java
System.out.println(" ".isEmpty()); // false
System.out.println("".isEmpty()); // true
System.out.println(" ".isBlank()); // true
System.out.println("".isBlank()); // true
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
4: sb.insert(7, "-");
// sb = animals-5:
sb.insert(0, "-"); // sb = -animals-
6:sb.insert(4, "-"); // sb = -ani-mals-
7:System.out.println(sb);
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

The ``replace()`` method works differently for StringBuilder than it did for String

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

the method is first doing a logical delete. The replace() method allows specifying a second parameter that is past the end of the StringBuilder. That means only the first three characters remain.

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

StringBuilder did not implement equals(). If you call equals() on two StringBuilder instances, it will check reference equality. You can call ``toString()`` on StringBuilder to get a String to check for equality instead.

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

==**If the arrays are equal, ``mismatch()`` returns -1.Otherwise, it returns the first index where they differ.**==

```java
System.out.println(Arrays.mismatch(new int[] {1}, new int[] {1}));
System.out.println(Arrays.mismatch(new String[] {"a"},
new String[] {"A"}));
System.out.println(Arrays.mismatch(new int[] {1, 2}, new int[] {1}));
```

- In the first example, the arrays are the same, so the result is -1. 
- In the second example, the entries at element 0 are not equal, so the result is 0.
- In the third example, the entries at element 0 are equal, so we keep looking. The element at index 1 is not equal. Or, more specifically, one array has an element at index 1, and the other does not. Therefore, the result is 1.

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

Java counts starting with 0. Well, months are an exception. For months in the new date and time methods, Java counts starting from 1, just as we humans do.

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
