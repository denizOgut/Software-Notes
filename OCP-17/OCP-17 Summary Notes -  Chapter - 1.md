

## Java File 

To keep things simple for now, we follow this subset of the rules:
- **Each file can contain only one public class.**
- **`private` and ``protected`` keywords not allowed in TOP LEVEL class declaration !!!**
- **The filename must match the class name, including case, and have a .java extension.**
- **If the Java class is an entry point for the program, it must contain a valid ``main()`` method.**
- **``final`` keyword is optional in ``main()`` method**

## Packages

- **Java only looks for class names in the package.**
- **The `import` statement doesn’t bring in child packages, fields, or methods; it imports only classes directly under the package**
- **There’s one special package in the Java world called `java.lang`. This package is special in that it is automatically imported.**

 Some imports that don't work

```java
import java.nio.*; // NO GOOD -a wildcard only matches class names, not "file.Files"
import java.nio.*.*; // NO GOOD -you can only have one wildcard  and it must be at the end
import java.nio.file.Paths.*; // NO GOOD -you cannot import methods only class names
```


- **If you specifically mention the name of a class when importing in programming, it's more important than using a general import with a wildcard `(*)`. The specific import has priority.**

### Ordering Elements in a Class


| **Element**                    | **Example**               | **Required?** | **Where does it go?**                                          |
| ------------------------------ | ------------------------- | ------------- | -------------------------------------------------------------- |
| **Package declaration**        | **`package abc;`**        | **No**        | **First line in the file (excluding comments or blank lines)** |
| **Import statements**          | **`import java.util.*;`** | **No**        | **Immediately after the package (if present)**                 |
| **Top-level type declaration** | **`public class C`**      | **Yes**       | **Immediately after the import (if any)**                      |
| **Field declarations**         | **`int value;`**          | **No**        | **Any top-level element within a class**                       |
| **Method declarations**        | **`void method()`**       | **No**        | **Any top-level element within a class**                       |
## Creating Objects

***There are two key points to note about the constructor:***
- ***the name of the constructor matches the name of the class***
- ***there’s no return type***


```java
public class Chick {
	public Chick() {
		System.out.println("in constructor");
	}
	public void Chick() { } // NOT A CONSTRUCTOR
}
```

- **code blocks appear outside a method. These are called instance initializers.**
- **instance initializers cannot exist inside of a method**

```java
1: public class Bird { // Class Definition
	2: public static void main(String[] args) { // Method Declaration
		3: { System.out.println("Feathers"); } // Inner Block
	4: }
	5: { System.out.println("Snowy"); } // Instance initializer
6: }
```

### Following the Order of Initialization

| Order No. | Order of Initialization           | Description                                                                                                                                                       | Simple Example                                         |
| --------- | --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| 1         | Static Variables Initialization   | Static variables are initialized first, either at the time of declaration or in a static block.                                                                   | `static int staticVariable = 42;`                      |
| 1         | Static Initialization Blocks      | Static initialization blocks are executed in the order they appear in the class after static variable initialization.                                             | ```static { /* initialization code */ }```             |
| 2         | Instance Variables Initialization | Instance variables are initialized next, either at the time of declaration or in an instance initialization block.                                                | `int instanceVariable = 10;`                           |
| 2         | Instance Initialization Blocks    | Instance initialization blocks are executed in the order they appear in the class after instance variable initialization, just before the constructor is invoked. | ```java { /* initialization code */ }```               |
| 3         | Constructor Execution             | Finally, the constructor of the class is executed, allowing specific instance-level initialization tasks to be performed.                                         | ```java public MyClass() { /* constructor code */ }``` |

- **Fields and instance initializer blocks are run in the order in which they appear in the file.**
- **The constructor runs after all fields and instance initializer blocks have run.**

###  Understanding Data Types

- **The ``byte``, ``short``, ``int``, and ``long`` types are used for integer values without decimal** **points.**

- **Each numeric type uses twice as many bits as the smaller similar type. For example,** ``short`` uses twice as many bits as ``byte`` does.**

- **All of the numeric types are signed and reserve one of their bits to cover a negative** **range.**

- **A ``float`` requires the letter f or F following the number so Java knows it is a ``float``. Without an f or F, Java interprets a decimal value as a ``double``.**

- **``long`` requires the letter l or L following the number so Java knows it is a ``long``. Without an l or L, Java interprets a number without a decimal point as an int in most** **scenarios.**

```java
long max = 3123456789; // DOES NOT COMPILE
long max = 3123456789L; // Now Java knows it is a long
```

**You can add underscores anywhere except at the beginning of a literal, the end of a literal, right before a decimal point, or right after a decimal point.**

```java
double notAtStart = _1000.00; // DOES NOT COMPILE
double notAtEnd = 1000.00_; // DOES NOT COMPILE
double notByDecimal = 1000_.00; // DOES NOT COMPILE
double annoyingButLegal = 1_00_0.0_0; // Ugly, but compiles
double reallyUgly = 1__________2; // Also compiles
```

###  Reference Types

- **references do not hold the value of the object they refer to. Instead, a reference “points” to an object by storing the memory address where the object is located, a concept referred to as a pointer.**
-  **A reference can be assigned to another object of the same or compatible type.**
- **A reference can be assigned to a new object using the ``new`` keyword.**

### Difference between Primitive & Reference Types

- **First, notice that all the primitive types have lowercase type names. All classes that come with Java begin with uppercase. Although not required, it is a standard practice, and you should follow this convention for classes you create as well.**

- **Next, reference types can be used to call methods, assuming the reference is not ``null``. Primitives do not have methods declared on them.**

- **Finally, reference types can be assigned `null`, which means they do not currently refer to an object. Primitive types will give you a compiler error if you attempt to assign them `null`.**

```java
int primitive = Integer.parseInt("123"); // Primitive Type - int
Integer wrapper = Integer.valueOf("123"); // Object Type - Integer
```

## Text Blocks

![[Pasted image 20240111141502.png]]

**In Java text blocks, use triple quotes `(""")` on separate lines above and below your text. Only the text between these lines becomes the Java String.**

**Essential whitespace is the intentional indentation and formatting that directly contributes to the structure and readability of your String. Incidental whitespace, on the other hand, is extra spacing added for code readability, but it doesn't affect the actual ``String`` value.** 

**the difference in the start location of the last triple quotes `(""")` and the leftmost character of the text inside the text block determines how much indentation is left inside the Java String produced by the Java text block declaration.**

**In Java text blocks (introduced in Java 13+), the opening `"""` must be followed by a newline, and the content starts from the next line. The closing `"""` can either be on a new line after the last content or aligned with the indentation level, but any whitespace before the closing delimiter is ignored.

```java
String block = """doe"""; // DOES NOT COMPILE Text blocks require a line break after the opening ``""",`` making this one invalid

String block = """
doe \
deer""";

String block = """
doe \n
deer
""";
```


| Formatting                     | Meaning in Regular String | Meaning in Text Block    |
|--------------------------------|---------------------------|--------------------------|
| `\"`                           | `"`                       | `"`                      |
| `\"""` (Invalid)               | n/a - Invalid             | n/a - Invalid            |
| `\"\"\"`                       | n/a - Invalid             | `"""`                    |
| Space (at end of line)          | Space                     | Ignored                  |
| `\s` (Two spaces)              | Two spaces                | Two spaces (preserves leading space on the line) |
| `\` (at end of line, Invalid)   | n/a - Invalid             | Omits new line on that line (Invalid in a text block) |
## Declaring Variables

There are only four rules to remember for legal identifiers:
1. ==**Begin with a letter, currency symbol, or _ symbol:**== Identifiers must start with a letter `(a-z or A-Z)`, a currency symbol `(e.g., $, ¥, €)`, or an underscore `(_)`.
    
2. ==**Include numbers but not start with them:**== While identifiers can include numbers, they must not begin with a number.
    
3. ==**Single underscore _ is not allowed:**== Using a single underscore by itself as an identifier is not allowed.
    
4. ==**Avoid Java reserved words:**== Identifiers cannot have the same name as Java reserved words. Reserved words are special words in the Java language that have predefined meanings and cannot be used as identifiers.

* The reserved words `const` and `goto` aren’t actually used in Java. They are reserved so that people coming from other programming languages don’t use them by accident

- There are other names that you can’t use. For example, **`true`**, **`false`**, and **`null`** are literal values, so they can’t be variable names. Additionally, there are contextual keywords like **`module


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

### Declaring Multiple Variables

- **You can declare many variables** **in the same declaration as long as they are all of the same type**
- **That’s the trick. Each snippet separated by a comma is a little declaration of its own**
- **In summary, for multiple variable declarations in the same line, variables must share the same type declaration**

```java
4: boolean b1, b2; // legal
5: String s1 = "1", s2; // legal
6: double d1, double d2; // not legal
7: int i1; int i2; // legal
8: int i3; i4; //not  legal
```

### Initializing Variables

- **A local variable is a variable defined within a constructor, method, or initializer block.**
- **Local variables do not have a default value and must be initialized before use.**
- **Variables passed to a constructor or method are called constructor parameters or method parameters, respectively. These parameters are like local variables that have been pre-initialized.**
- **You can tell a variable is a class variable because it has the keyword `static` before it.**
- **Instance and class variables do not require you to initialize them. As soon as you declare these variables, they are given a default value.**


## ``var`` Keyword

- **In Java, ``var`` is still a specific type defined at compile time. It does not change type at runtime.** 
- **for local variable type inference, the compiler looks only at the line with the declaration.**==

```java
4: public void twoTypes() {
	5: int a, var b = 3; // DOES NOT COMPILE
	6: var n = null; // DOES NOT COMPILE
	int c = 2,  d = 3; // COMPILE
7: }
```

```java
4: public void twoTypes() {
	5: var a = 2, var b = 3; // DOES NOT COMPILE
	6: int x, int v = 3; // DOES NOT COMPILE 
	7: var a = 2; int b = 3; // COMPILE
8: }
```

**one last rule  should be aware of:  `var` is not a reserved word and allowed to be used as an identifier. It is considered a reserved type name.  A reserved type name means it cannot be used to define a type, such as a ``class``, ``interface``, or ``enum``.**

1. **A `var` is used as a local variable in a constructor, method, or initializer block.**   
 2. **A `var` cannot be used in constructor parameters, method parameters, instance variables, or class variables.**   
 3. **A `var` is always initialized on the same line (or statement) where it is declared.**    
 4. **The value of a `var` can change, but the type cannot.**    
 5. **A `var` cannot be initialized with a ``null`` value without a type.**    
 6. **A `var` is not permitted in a multiple-variable declaration.**    
 7.  **A `var` is a reserved type name but not a reserved word, meaning it can be used as an identifier except as a class, interface, or enum name.** 

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

## Scope

- **Local variables: In scope from declaration to the end of the block**
- **Method parameters: In scope for the duration of the method**
- **Instance variables: In scope from declaration until the object is eligible for garbage collection**
- **Class variables: In scope from declaration until the program ends**

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

## Garbage Collector

-  **eligible for garbage collection refers to an object’s state of no longer being accessible in a program and therefore able to be garbage collected.**
```java
System.gc();
```

Java is free to ignore you. ==**==This method is not guaranteed to do anything**.

**Eligibility**

-  **The object no longer has any references pointing to it.**
-  **All references to the object have gone out of scope.**

- **It is the object that gets garbage collected, not its reference.**

## Summary #OCP_Summary 

**Java begins program execution with a `main()` method. The most common signature for this method run from the command line is `public static void main(String[] args)`. Arguments are passed in after the class name, as in java `NameOfClass` `firstArgument`. Arguments are indexed starting with 0.**

**Java code is organized into folders called packages. To reference classes in other packages, you use an `import` statement. A wildcard ending an import statement means you want to import all classes in that package. It does not include packages that are inside that one. The package` java.lang` is special in that it does not need to be imported.**

**For some class elements, order matters within the file. The package statement comes first if present. Then come the import statements if present. Then comes the class declaration. Fields and methods are allowed to be in any order within the class.**

**Primitive types are the basic building blocks of Java types. They are assembled into reference types. Reference types can have methods and be assigned a ``null`` value. Numeric literals are allowed to contain underscores `(_)` as long as they do not start or end the literal and are not next to a decimal point `(.)`. Wrapper classes are reference types, and there is one for each primitive. Text blocks allow creating a ``String`` on multiple lines using `"""`.**

**Declaring a variable involves stating the data type and giving the variable a name. Variables that represent fields in a class are automatically initialized to their corresponding 0, `null`, or `false` values during object instantiation. Local variables must be specifically initialized before they can be used. Identifiers may contain letters, numbers, currency symbols, or _. Identifiers may not begin with numbers. Local variable declarations may use the ``var`` keyword instead of the actual type. When using var, the type is set once at compile time and does not change.**

**Scope refers to that portion of code where a variable can be accessed. There are three kinds of variables in Java, depending on their scope: instance variables, class variables, and local variables. Instance variables are the non-static fields of your class. Class variables are the static fields within a class. Local variables are declared within a constructor, method, or initializer block.**

**Constructors create Java objects. A constructor is a method matching the class name and omitting the return type. When an object is instantiated, fields and blocks of code are initialized first. Then the constructor is run. Finally, garbage collection is responsible for removing objects from memory when they can never be used again. An object becomes eligible for garbage collection when there are no more references to it or its references have all gone out of scope.**

## Exam Essentials

**==In the event of a conflict, class name imports take precedence==**. **==Package and import statements are optional. If they are present, they both go before the class declaration in that order.==**

**==Understand how to create text blocks.  A text block begins with `"""` on the first line. On the next line begins the content. The last line ends with `""".` If `"""` is on its own line, a trailing line break is included.==**

