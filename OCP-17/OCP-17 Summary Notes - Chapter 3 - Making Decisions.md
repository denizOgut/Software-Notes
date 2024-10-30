
## `if` Statement

**The `if` statement, execute a particular block of code if and only if a `boolean` expression evaluates to `true` at runtime.**

```java
if(hourOfDay < 11) {
	System.out.println("Good Morning");
} else if(hourOfDay < 15) {
	System.out.println("Good Afternoon");
} else {
	System.out.println("Good Evening");
}
```

**Another common way the exam may try to lead you astray is by providing code where the `boolean` expression inside the if statement is not actually a boolean expression**

```java
int hourOfDay = 1;
if(hourOfDay) { // DOES NOT COMPILE
	...
}
```

## Pattern Matching

```java
void compareIntegers(Number number) {
	if(number instanceof Integer data) { 
		System.out.print(data.compareTo(5));
	}
}
```

**The variable data in this example is referred to as the pattern variable**. 
**The pattern variables are those that store data from the target only if the predicate returns `true` which is ``instanceof``**

**Reassigning Pattern Variables**

```java
if(number instanceof Integer data) {
	data = 10;
}
```


```java
void printIntegersGreaterThan5(Number number) {
	if(number instanceof Integer data && data.compareTo(5)>0)
		System.out.print(data);
}
```

**Notice that we’re using the pattern variable in an expression in the same line in which it is declared.**

**The type of the pattern variable must be a subtype of the variable on the left side of the expression. It also cannot be the same type. This rule does not exist for traditional `instanceof` operator expressions**


```java
Integer value = 123;
if(value instanceof Integer) {}
if(value instanceof Integer data) {} // DOES NOT COMPILE
```

**the last line does not compile because pattern matching requires that the pattern variable type Integer be a strict subtype of Integer. making `Integer` on both sides redundant and thus invalid.** 

---

**A _strict subtype_ means a type that is a direct descendant of another type in the inheritance hierarchy, excluding the type itself.**

For example:

- **`Integer` is a strict subtype of `Number` but not of `Integer` itself.**
- **Similarly, `ArrayList` is a strict subtype of `List`, but `List` is not a strict subtype of itself.**

---

## Flow Scoping

 **Flow scoping means the variable is only in scope when the compiler can definitively determine its type.**

```java
void printIntegersOrNumbersGreaterThan5(Number number) {
	if(number instanceof Integer data || data.compareTo(5)>0) // DOES NOT COMPILE
		System.out.print(data);
}
```

Since the compiler cannot guarantee that data is an instance of ``Integer``, data is not in scope, and the code does not compile. 

```java
void printIntegerTwice(Number number) {
if (number instanceof Integer data)
	System.out.print(data.intValue());
	System.out.print(data.intValue()); // DOES NOT COMPILE
}
```


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

**this code does compile! The method returns if the input does not inherit ``Integer``. This means that when the last line of the method is reached, the input must inherit ``Integer``, and therefore data stays in scope even after the if statement ends.**

**In particular, it is possible to use a pattern variable outside of the if statement, but only when the compiler can definitively determine its type.**

## `switch` Statements


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

- **The first switch statement does not compile because it is missing parentheses around the switch variable.** 
- **The second statement does not compile because it is missing braces around the switch body.**
- **The third statement does not compile because a comma `(,)` should be used to separate combined case statements, not a colon `(:)`.**
- **a switch statement is not required to contain any case statements.**

```java
switch(month) {} // Perfectly Valid !!!
```

### Selecting ``switch`` Data Types

**a switch statement has a target variable that is not evaluated until runtime.**

- **``int`` and ``Integer``**
- **``byte`` and ``Byte``**
- **``short`` and ``Short``**
- **``char`` and ``Character``**
- **``String``**
- **``enum`` values**
- **``var`` (if the type resolves to one of the preceding types)

**the values in each case statement must be compile-time constant values of the same data type as the switch value. This means you can use only literals, enum constants, or final constant variables of the same data type.**

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
	}
}
```

- **They also must be able to fit in the ``switch`` data type without an explicit cast.**
- **The data type for case statements must match the data type of the ``switch`` variable.**

## ``switch`` Expression

a ``switch`` statement, **capable of returning a value**.
**For this to work, all case and default branches must return a data type that is compatible with the assignment.**

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

**Notice that a semicolon is required after each ``switch`` expression.** 

```java
var result = switch(bear) { // Does not compile
	case 30 -> "Grizzly"
	default -> "Panda"
} // Each case or ``default`` expression requires a semicolon as well as the assignment itself.
```

All of the previous rules around ``switch`` data types and case values still apply

1. **All of the branches of a ``switch`` expression that do not ``throw`` an exception must return a consistent data type (if the ``switch`` expression returns a value).**
2. **If the ``switch`` expression returns a value, then every branch that isn’t an expression must ``yield`` a value.**
3. **A default branch is required unless all cases are covered or no value is returned.**

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

 **the values have to be consistent with size, but they do not all have to be the same data type**.

**``switch`` expressions, ``yield`` statements are NOT OPTIONAL if the switch statement RETURNS a value.**

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

**The last rule about ``switch`` expressions is probably the one the exam is most likely to try to trick you on: a ``switch`` expression that returns a value must handle all possible input values. when it does not return a value, it is optional.**

**there are two ways to address this:**
- **Add a ``default`` branch.**
- **If the ``switch`` expression takes an ``enum`` value, add a case branch for every possible ``enum`` value.**
- **consider including a default branch in every ``switch`` expression, even those that involve ``enum`` values.**

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

**Unlike a regular ``switch`` statement, a ``switch`` expression can be used with the assignment operator and requires a semicolon when doing so. Furthermore, semicolons are required for case expressions but cannot be used with case blocks.**

```java
var name = switch(fish) {
case 1 -> "Goldfish" // DOES NOT COMPILE (missing semicolon)
case 2 -> {yield "Trout";}; // DOES NOT COMPILE (extra semicolon)
...
} // DOES NOT COMPILE (missing semicolon)
```

## ``while`` Statement

**One thing to remember is that a ``while`` loop may terminate after its first evaluation of the ``boolean`` expression**

```java
int full = 5;
while(full < 5) {
	System.out.println("Not full!");
	full++;
}
```

## ``do/while`` Statement

**Unlike a ``while`` loop, though, a ``do/while`` loop guarantees that the statement or block will be executed at least once.**

```java
int lizard = 0;
do {
	lizard++;
} while(false);
System.out.println(lizard); // 1
```

 **The single most important thing you should be aware of when you are using any repetition control structures is to make sure they always terminate!**
## ``for`` Loops

**Each of the three sections is separated by a semicolon. In addition, the initialization and update sections may contain multiple statements, separated by commas.**

```java
int x = 0;
for(long y = 0, z = 4; x < 5 && y < 10; x++, y++) {
System.out.print(y + " "); }
System.out.print(x + " ");
```

- **First, you can declare a variable, such as x in this example, before the loop begins and use it after it completes.**
- **Second, your initialization block, boolean expression, and update statements can include extra variables that may or may not reference each other**
- **Finally, the update statement can modify multiple variables.**

**The variables in the initialization block must all be of the same type**

## ``for-each`` Loop

**The ``for-each`` loop declaration is composed of an initialization section and an object to be iterated over. The right side of the for-each loop must be one of the following:**

- **A built-in Java array**  
- **An object whose type implements`` java.lang.Iterable``**

**on each iteration, a ``for-each`` loop assigns a variable with the same type as the generic argument.**

**One facet of ``break``, ``continue``, and ``return`` that you should be aware of is that any code placed immediately after them in the same block is considered unreachable and will not compile.**

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

| Control Statement | Support Labels | Support Break | Support Continue | Support Yield |
| ----------------- | -------------- | ------------- | ---------------- | ------------- |
| while             | Yes            | Yes           | Yes              | No            |
| do/while          | Yes            | Yes           | Yes              | No            |
| for               | Yes            | Yes           | Yes              | No            |
| switch            | Yes            | Yes           | No               | Yes           |
## Summary 

**This chapter presented how to make intelligent decisions in Java.**

**We covered basic decision-making constructs such as if, else, and switch statements and showed how to use them to change the path of the process at runtime. We also presented newer features in the Java language, including pattern matching and switch expressions, both designed to reduce boilerplate code.**

**We then moved our discussion to repetition control structures, starting with while and do/while loops.**

**Next, we covered the extremely convenient repetition control structures: the for and for-each loops. While their syntax is more complex than the traditional while or do/while loops, they are extremely useful in everyday coding and allow you to create complex expressions in a single line of code.**

**We concluded this chapter by discussing advanced control options and how flow can be enhanced through nested loops coupled with break, continue, and return statements.**

