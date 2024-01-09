
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

The Java Development Kit (JDK) contains the minimum software you need to do Java
development. Key commands include:

- `javac`: Converts .java source files into .class bytecode
- java: Executes the program
- jar: Packages files together
- `javadoc`: Generates documentation

The `javac` program generates instructions in a special format called bytecode that
the java command can run.

Then java launches the Java Virtual Machine (JVM) before running the code The JVM knows how to run bytecode on the actual machine it is on.

think of the JVM as a special magic box on your machine that knows how to run your
.class file within your particular operating system and hardware.

---

**Where Did the JRE Go?**

In Java 8 and earlier, you could download a Java Runtime Environment (JRE) instead of the
full JDK. The JRE was a subset of the JDK that was used for running a program but could
not compile one.

Now, people can use the full JDK when running a Java program. Alternatively,
developers can supply an executable that contains the required pieces that would
have been in the JRE.

When writing a program, there are common pieces of functionality and algorithms that
developers need. Java comes with a large suite of application programming interfaces (APIs) that you can use.

For example, there is a `StringBuilder` class to create a large `String` and a method in `Collections` to sort a list. When writing a program, it is helpful to determine what pieces of your assignment can be accomplished by existing APIs.

---

### Downloading a JDK

Every six months, Oracle releases a new version of Java. 
The rules and behavior can change with later versions of Java.
There are many JDKs available, the most popular of which, besides Oracle’s JDK, is OpenJDK.

Many versions of Java include preview features that are off by default but that you can
enable. Preview features are not on the exam.

---
**Check Your Version of Java**

```shell
javac -version
java -version
```

---


## Understanding the Class Structure

In Java programs, classes are the basic building blocks. When defining a class, you describe
all the parts and characteristics of one of those building blocks.

To use most classes, you have to create objects.  An object is a runtime instance of a class
in memory. An object is often referred to as an instance since it represents a single representation of the class.

All the various objects of all the different classes represent the state of
your program. A reference is a variable that points to an object.

### Fields and Methods

Java classes have two primary elements: **methods**, often called functions or procedures in
other languages, and **fields**, more generally known as variables.
Together these are called the members of the class.

Variables hold the state of the program, and methods operate on that
state. If the change is important to remember, a variable stores that change.

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

On line 2, we define a variable named name. We also declare the type of that variable to
be `String`.

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

On lines 3–5, we define a method. A method is an operation that can be called. Again,
`public` is used to signify that this method may be called from other classes

Next comes the return type—in this case, the method returns a `String`.
On lines 6–8 is another method. This one has a special return type called void.
The `void` keyword means that no value at all is returned.

This method requires that information be supplied to it from the calling method;
this information is called a *parameter*.

The `setName()` method has one parameter named `newName`, and it is of type String.
This means the caller should pass in one String parameter and expect nothing to be returned.

The method name and parameter types are called the method signature.

```java
public int numberVisitors(int month) {
	return 10;
}
```

The method name is `numberVisitors`. There’s one parameter named month,
which is of type `int`, which is a numeric type. the method signature is
**`numberVisitors(int).`**

### Comments

Another common part of the code is called a comment. Because comments aren’t executable
code, you can place them in many places. Comments can make your code easier to read.

There are three types of comments in Java. 
**single-line comment**:

```java
// comment until end of line
```

A single-line comment begins with two slashes. The compiler ignores anything you type
after that on the same line.

**multiple-line comment**

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


This comment is similar to a multiline comment, except it starts with `/**`.   This special
syntax tells the Javadoc tool to pay attention to the comment.
Javadoc comments have a specific structure that the Javadoc tool knows how to read.

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

The line with ferret is interesting in that it doesn’t compile. Everything from the first /* to
the first */ is part of the comment which means the compiler sees something like this:
`/* * /  */`

There is an extra `*/`. That’s not valid syntax

### Classes and Source Files

Most of the time, each Java class is defined in its own .java file. 
A top-level type is a data structure that can be defined independently within a source file.
A top-level class is often `public`, which means any code can call it. Interestingly, Java does
not require that the type be `public`

```java
1: class Animal {
2: String name;
3: }
```

You can even put two types in the same file. When you do so, **==at most one of the top-level**==
==**types in the file is allowed to be public==**

```java
1: public class Animal {
2: private String name;
3: }
4: class Animal2 {} // Bold
```

**==If you do have a public type, it needs to match the filename**. The declaration==
==public class Animal2 would not compile in a file named **`Animal.java`**.==


## Writing a main() Method

A Java program begins execution with its main() method. 
The main() method is often called an entry point into the program, because it is the starting point that the JVM looks for when it begins running a new program.

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
The name of the file must match the name of the public class.  The result is a file of bytecode
with the same name but with a .class filename extension.

To keep things simple
for now, we follow this subset of the rules:
- ==**Each file can contain only one public class.**==
- ==**The filename must match the class name, including case, and have a .java extension.**==
- ==**If the Java class is an entry point for the program, it must contain a valid main() method.**==

review the words in the main() method’s signature, one at a time. 

The keyword `public` is what’s called an access modifier. It declares this method’s level of exposure to potential callers in the program. Naturally, public means full access from anywhere in the program.

The keyword `static` binds a method to its class so it can be called by just the class name 
Java doesn’t need to create an object to call the main() method 

The keyword `void` represents the return type. A method that returns no data returns control
to the caller silently.  In general, it’s good practice to use void for methods that change an
object’s state. In that sense, the main() method changes the program state from started to finished.

Finally, the main() method’s parameter list, represented as an array of `java.lang.String` objects. can use any valid variable name along with any of these three formats:

- ==**`String[] args`**==
- ==**`String options[]`**==
- ==**`String... friends`**==

The variable name args is common because it hints that this list contains values that were read in (arguments) when the JVM started.

---
**Optional Modifiers in main() Methods** #TIP

While most modifiers, such as public and static, are required for main() methods,
there are some optional modifiers allowed.

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

The program correctly identifies the first two “words” as the arguments. Spaces are used
to separate the arguments. **==want spaces inside an argument, you need to use quotes==**

```shell
javac Zoo.java
java Zoo "San Diego" Zoo
```

what happens if you don’t pass in enough arguments?

```shell
javac Zoo.java
java Zoo Zoo
```

Reading args[0] goes fine, and Zoo is printed out. Then Java panics. There’s no second
argument! Java prints out an exception telling you it has no idea what to do with this argument at position 1.

```java
Zoo
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException:
Index 1 out of bounds for length 1
at Zoo.main(Zoo.java:4)
```

To review, the JDK contains a compiler. Java class files run on the JVM and therefore run
on any machine with Java rather than just the machine or operating system they happened
to have been compiled on.

---

**Single-File Source-Code**

```shell
java Zoo.java Bronx Zoo
```

There is a key difference here. When compiling first, you omitted the .java extension
when running java. When skipping the explicit compilation step, you include this
extension. This feature is called launching single-file source-code programs and is useful for
testing or for small programs.

---


## Understanding Package Declarations and Imports















