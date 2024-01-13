
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
- `java`: Executes the program
- `jar`: Packages files together
- `javadoc`: Generates documentation

The `javac` program generates instructions in a special format called bytecode that the java command can run.

Then java launches the Java Virtual Machine (JVM) before running the code The JVM knows how to run bytecode on the actual machine it is on.

think of the JVM as a special magic box on your machine that knows how to run your .class file within your particular operating system and hardware.

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

In Java programs, classes are the basic building blocks. When defining a class, you describe all the parts and characteristics of one of those building blocks.

To use most classes, you have to create objects.  An object is a runtime instance of a class in memory. An object is often referred to as an instance since it represents a single representation of the class.

All the various objects of all the different classes represent the state of your program. A reference is a variable that points to an object.

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

On lines 3–5, we define a method. A method is an operation that can be called. Again, `public` is used to signify that this method may be called from other classes

Next comes the return type—in this case, the method returns a `String`. On lines 6–8 is another method. This one has a special return type called void. The `void` keyword means that no value at all is returned.

This method requires that information be supplied to it from the calling method; this information is called a *parameter*.

The `setName()` method has one parameter named `newName`, and it is of type String. This means the caller should pass in one String parameter and expect nothing to be returned.

The method name and parameter types are called the method signature.

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
The name of the file must match the name of the public class.  The result is a file of bytecode
with the same name but with a .class filename extension.

To keep things simple
for now, we follow this subset of the rules:
- ==**Each file can contain only one public class.**==
- ==**The filename must match the class name, including case, and have a .java extension.**==
- ==**If the Java class is an entry point for the program, it must contain a valid main() method.**==

review the words in the `main()` method’s signature, one at a time. 

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

This error could mean you made a typo in the name of the class. The other cause of this error is omitting a needed `import` statement. A statement is an instruction, and import statements tell Java which packages to look in for classes. Since you didn’t tell Java where to look for Random, it has no clue.

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

There’s one special package in the Java world called `java.lang`. This package is special in that it is automatically imported.

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

you can pick one to use in the import statement and use the other’s fully qualified class name. Or you can drop both import statements and always use the fully qualified class name.

```java
public class Conflicts {
java.util.Date date;
java.sql.Date sqlDate;
}
```

---
### Creating a New Package

the default package. This is a special unnamed package that you should use only for throwaway code. You can tell the code is in the default package, because there’s no package name. In real life, always name your packages to avoid naming conflicts and to allow others to reuse your code.

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

First you declare the type that you’ll be creating (Park) and give the variable a name (p). This gives Java a place to store a reference to the object.  Then you write `new Park()` to actually create the object.

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
==**method that does compile but will not be called when you write new Chick().**== #TIP 

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
2: String first = "Theodore";
3: String last = "Moose";
4: String full = first + last;
5: }
```

Lines 2 and 3 both write to fields. Line 4 both reads and writes data. It reads the fields `first` and `last`. It then writes the field full.
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

When you’re counting instance initializers, keep in mind that they cannot exist inside of a method. Line 5 is an instance initializer, with its braces outside a method.
### Following the Order of Initialization

This is simply the order in which different methods, constructors, or blocks are called when an instance of the class is created.

| Order No. | Order of Initialization            | Description                                                                                      | Simple Example                                   |
|-----------|-------------------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------|
| 1         | Static Variables Initialization | Static variables are initialized first, either at the time of declaration or in a static block.  | `static int staticVariable = 42;`                |
| 2         | Static Initialization Blocks    | Static initialization blocks are executed in the order they appear in the class after static variable initialization. | ```java static { /* initialization code */ }``` |
| 3         | Instance Variables Initialization | Instance variables are initialized next, either at the time of declaration or in an instance initialization block. | `int instanceVariable = 10;`                     |
| 4         | Instance Initialization Blocks | Instance initialization blocks are executed in the order they appear in the class after instance variable initialization, just before the constructor is invoked. | ```java { /* initialization code */ }```        |
| 5         | Constructor Execution           | Finally, the constructor of the class is executed, allowing specific instance-level initialization tasks to be performed. | ```java public MyClass() { /* constructor code */ }``` |

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

start with the main() method because that’s where Java starts execution. On line 9, we call the constructor of Chick. Java creates a new object. First it initializes name to "Fluffy" on line 2. Next it executes the `println()` statement in the instance initializer on line 3. Once all the fields and instance initializers have run, Java returns to the constructor. Line 5 changes the value of name to "Tiny", and line 6 prints another statement.

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

Java applications contain two types of data: **primitive** types and **reference** types.
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

You can add underscores anywhere except at the beginning of a literal, the end of a literal, right before a decimal point, or right after a decimal point.

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

The greeting reference points to a new String object, "How are you?". The String object does not have a name and can be accessed only via a corresponding reference.
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

All of the numeric classes extend the Number class, which means they all come with some useful helper methods: `byteValue(), shortValue(), intValue(), longValue(), floatValue()`, and `doubleValue()`. The Boolean and Character wrapper classes include `booleanValue()` and `charValue()`, respectively. These methods return the primitive value of a wrapper instance, in the type requested.

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

You can freely adjust incidental whitespace without impacting your String content. Visualize a vertical line on the leftmost non-whitespace character in your text block – everything to the left is incidental whitespace, and everything to the right is essential whitespace. Adjusting the left side won't change your String; it's there solely for code aesthetics.

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
1. **Begin with a letter, currency symbol, or _ symbol:** Identifiers must start with a letter (a-z or A-Z), a currency symbol (e.g., $, ¥, €), or an underscore `(_)`.
    
2. **Include numbers but not start with them:** While identifiers can include numbers, they must not begin with a number.
    
3. **Single underscore _ is not allowed:** Using a single underscore by itself as an identifier is not allowed.
    
4. **Avoid Java reserved words:** Identifiers cannot have the same name as Java reserved words. Reserved words are special words in the Java language that have predefined meanings and cannot be used as identifiers.

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

Local variables do not have a default value and must be initialized before use. Furthermore, the compiler will report an error if you try to read an uninitialized value.

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

Instance and class variables do not require you to initialize them. As soon as you declare these variables, they are given a default value. The compiler doesn’t know what value to use and so wants the simplest value it can give the type: `null` for an object, `zero` for the numeric types, and `false` for a `boolean`

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

The variable tricky is an instance variable. Local variable type inference works with local variables and not instance variables. 
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

and b are method parameters. These are not local variables. Be on the lookout for var used with constructors, method parameters, or instance variables. **var is only used for local variable type inference!**

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

```java
public class VarReview {  
    
 // Review of var Rules  
  
// 1- A var is used as a local variable in a constructor, method, or initializer block.   
// 2- A var cannot be used in constructor parameters, method parameters, instance variables, or class variables.    
// 3- A var is always initialized on the same line (or statement) where it is declared.    
// 4- The value of a var can change, but the type cannot.    
// 5- A var cannot be initialized with a null value without a type.    
// 6- A var is not permitted in a multiple-variable declaration.    
// 7- A var is a reserved type name but not a reserved word,    
// meaning it can be used as an identifier except as a class, interface, or enum name.  
  
}  
  
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

---## Destroying Objects

Java provides a garbage collector to automatically look for objects that aren’t needed anymore.  All Java objects are stored in your program memory’s heap. The heap, which is also referred to as the free store, represents a large pool of unused memory allocated to your Java application. If your program keeps instantiating objects and leaving them on the heap, eventually it will run out of memory and crash. garbage collection solves this problem.

### Understanding Garbage Collection

Garbage collection refers to the process of automatically freeing memory on the heap by deleting objects that are no longer reachable in your program. 

As a developer, the most interesting part of garbage collection is determining when the memory belonging to an object can be reclaimed. In Java and other languages, ==**eligible for garbage collection refers to an object’s state of no longer being accessible in a program and therefore able to be garbage collected.**==

Think of garbage-collection eligibility like shipping a package. You can take an item, seal it in a labeled box, and put it in your mailbox. This is analogous to making an item eligible for garbage collection. When the mail carrier comes by to pick it up, though, is not in your control 

Java includes a built-in method to help support garbage collection where you can suggest that garbage collection run.

```java
System.gc();
```

Java is free to ignore you. This method is not guaranteed to do anything.

### Tracing Eligibility

How does the JVM know when an object is eligible for garbage collection? The JVM waits patiently and monitors each object until it determines that the code no longer needs that memory. An object will remain on the heap until it is no longer reachable. An object is no longer reachable when one of two situations occurs:

-  ==**The object no longer has any references pointing to it.**==
-  ==**All references to the object have gone out of scope.**==

---
**Objects vs. References**

Do not confuse a reference with the object that it refers to; they are two different entities.

The reference is a variable that has a name and can be used to access the contents of an object. A reference can be assigned to another reference, passed to a method, or returned from a method. All references are the same size, no matter what their type is.

An object sits on the heap and does not have a name. Therefore, you have no way to access an object except through a reference. Objects come in all different shapes and sizes and consume varying amounts of memory. An object cannot be assigned to another object, and an object cannot be passed to a method or returned from a method. ==**It is the object that gets garbage collected, not its reference.**==

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

## Summary #Summary 

==**Java begins program execution with a `main()` method. The most common signature for this method run from the command line is `public static void main(String[] args)`. Arguments are passed in after the class name, as in java `NameOfClass` `firstArgument`. Arguments are indexed starting with 0.**==

==**Java code is organized into folders called packages. To reference classes in other packages, you use an `import` statement. A wildcard ending an import statement means you want to import all classes in that package. It does not include packages that are inside that one. The package` java.lang` is special in that it does not need to be imported.**==

==**For some class elements, order matters within the file. The package statement comes first if present. Then come the import statements if present. Then comes the class declaration. Fields and methods are allowed to be in any order within the class.**==

==**Primitive types are the basic building blocks of Java types. They are assembled into reference types. Reference types can have methods and be assigned a null value. Numeric literals are allowed to contain underscores (_) as long as they do not start or end the literal and are not next to a decimal point `(.)`. Wrapper classes are reference types, and there is one for each primitive. Text blocks allow creating a String on multiple lines using `"""`.**==

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


