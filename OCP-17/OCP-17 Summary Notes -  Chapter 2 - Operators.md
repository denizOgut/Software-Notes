
## Types of Operators

Java supports three flavors of operators: 
- **unary,** 
- **binary,**  
- **ternary.**

## Operator Precedence

**Unless overridden with parentheses, Java operators follow order of operation, listed in Table 2.1, by decreasing order of operator precedence.**

![[Pasted image 20240116144727.png]]

## Unary Operators


| Operator Type       | Example     | Description                                                                                               |
| ------------------- | ----------- | --------------------------------------------------------------------------------------------------------- |
| Logical Complement  | `!a`        | Inverts a boolean’s logical value                                                                         |
| Bitwise Complement  | `~b`        | Inverts all 0s and 1s in a number                                                                         |
| Plus                | `+c`        | Indicates a number is positive (assumed positive in Java unless accompanied by a negative unary operator) |
| Negation or Minus   | `-d`        | Indicates a literal number is negative or negates an expression                                           |
| Increment           | `++e`       | Increments a value by 1                                                                                   |
| Increment (Postfix) | `f++`       | Increments a value by 1 after its current value is used                                                   |
| Decrement           | `--f`       | Decrements a value by 1                                                                                   |
| Decrement (Postfix) | `h--`       | Decrements a value by 1 after its current value is used                                                   |
| Cast                | `(String)i` | Casts a value to a specific type                                                                          |
**`bitwise complement operator (~)`**, which flips all of the 0s and 1s in a number. **It can only be applied to integer numeric types such as ``byte``, ``short``, ``char``, ``int``, and ``long``.**


```java
int value = 3; // Stored as 0011
int complement = ~value; // Stored as 1100
System.out.println(value); // 3
System.out.println(complement); // -4
```

**remember this rule: to find the bitwise complement of a number, multiply it by negative one and then subtract one.**

```java
System.out.println(-1 * value -1); // -4
System.out.println(-1 * complement -1); // 3
```

**Increment and decrement operators, `++` and `--`, respectively, can be applied to numeric variables and have a high order of precedence compared to binary operators. In other words, they are often applied first in an expression.**

| Operator Type  | Example | Description                                             |
| -------------- | ------- | ------------------------------------------------------- |
| Pre-increment  | `++w`   | Increases the value by 1 and returns the new value      |
| Pre-decrement  | `--x`   | Decreases the value by 1 and returns the new value      |
| Post-increment | `y++`   | Increases the value by 1 and returns the original value |
| Post-decrement | `z--`   | Decreases the value by 1 and returns the original value |
## Binary Arithmetic

| Operator Type  | Example | Description                                                          |
| -------------- | ------- | -------------------------------------------------------------------- |
| Addition       | `a + b` | Adds two numeric values                                              |
| Subtraction    | `c - d` | Subtracts two numeric values                                         |
| Multiplication | `e * f` | Multiplies two numeric values                                        |
| Division       | `g / h` | Divides one numeric value by another                                 |
| Modulus        | `i % j` | Returns the remainder after division of one numeric value by another |
**the difference between arithmetic division and modulus. For integer values, division results in the floor value of the nearest integer that fulfills the operation, whereas modulus is the remainder value.**

## Numeric Promotion

**each primitive numeric type has a bit-length. You don’t need to know the exact size of these types for the exam, but you should know which are bigger than others.**==

**Numeric Promotion Rules**

1. **If two values have different data types, Java will automatically promote one of the values to the larger of the two data types.**
2. **If one of the values is integral and the other is floating-point, Java will automatically promote the integral value to the floating-point value’s data type.**
3. **Smaller data types, namely, `byte`, `short`, and `char`, are first promoted to int any time they’re used with a Java binary arithmetic operator with a variable (as opposed to a value), even if neither of the operands is int.**
4. **After all promotion has occurred and the operands have the same data type, the resulting value will have the same data type as its promoted operands.**

```java
double x = 39.21;
float y = 2.1;
var z = x + y;
```

 **the second line does not compile! Floating-point literals are assumed to be double unless post-fixed with an f, as in 2.1f.**

## Assigning Values

**Java will automatically promote from smaller to larger data types, on arithmetic operators, but it will throw a compiler exception if it detects that you are trying to convert from larger to smaller data types without casting.**

| Operator   | Example       | Description                                                 |
| ---------- | ------------- | ----------------------------------------------------------- |
| Assignment | `int a = 50;` | Assigns the value on the right to the variable on the left. |
 **Casting is optional and unnecessary when converting to a larger or widening data type, but it is required when converting to a smaller or narrowing data type.**

```java
int fur = (int)5;
int hair = (short) 2;
String type = (String) "Bird";
short tail = (short)(4 + 10);
long feathers = 10(long); // DOES NOT COMPILE
```

```java
float egg = 2.0 / 9; // DOES NOT COMPILE
int tadpole = (int)5 * 2L; // DOES NOT COMPILE
short frog = 3 -2.0; // DOES NOT COMPILE
```

**Put simply, casting a numeric value may change the data type, while casting an object only changes the reference to the object, not the object itself.**

**Remember, casting primitives is required any time you are going from a larger numerical data type to a smaller numerical data type, or converting from a floating-point number to an integral value.**

```java
long reptile = (long)192301398193810323; // DOES NOT COMPILE
```

**This still does not compile because the value is first interpreted as an int by the compiler and is out of range.** The following fixes this code without requiring casting:

```java
long reptile = 192301398193810323L;
```

## Casting Values vs. Variables

**the compiler doesn’t require casting when working with literal values that fit into the data type.**

## Compound Assignment Operators

| Operator                  | Example    | Description                                                                                                |
| ------------------------- | ---------- | ---------------------------------------------------------------------------------------------------------- |
| Addition assignment       | `a += 5`   | Adds the value on the right to the variable on the left and assigns the sum to the variable.               |
| Subtraction assignment    | `b -= 0.2` | Subtracts the value on the right from the variable on the left and assigns the difference to the variable. |
| Multiplication assignment | `c *= 100` | Multiplies the value on the right with the variable on the left and assigns the product to the variable.   |
| Division assignment       | `d /= 4`   | Divides the variable on the left by the value on the right and assigns the quotient to the variable.       |

**Compound operators are useful for more than just shorthand—they can also save you from having to explicitly cast a value.

```java
long goat = 10;
int sheep = 5;
sheep = sheep * goat; // DOES NOT COMPILE
```

```java
long goat = 10;
int sheep = 5;
sheep *= goat;
```

## Return Value of Assignment Operators

**the result of an assignment is an expression in and of itself equal to the value of the assignment.**

```java
boolean healthy = false;
if(healthy = true) 
System.out.print("Good!");
```

 **it’s actually assigning healthy a value of true. The result of the assignment is the value of the assignment, which is true**

## Comparing Values

| Operator   | Example | Apply to Primitives                                     | Apply to Objects                                      |
|------------|---------|---------------------------------------------------------|--------------------------------------------------------|
| Equality   | a == 10 | Returns true if the two values represent the same value | Returns true if the two values reference the same object |
| Inequality | b != 3.14 | Returns true if the two values represent different values | Returns true if the two values do not reference the same object |

**The equality operator can be applied to numeric values, `boolean` values, and objects (including `String` and `null`). When applying the equality operator, you cannot mix these types.**

**Pay close attention to the data types when you see an equality operator on the exam.**

```java
boolean bear = false;
boolean polar = (bear = true);
System.out.println(polar); // true
```

**For object comparison, the equality operator is applied to the references to the objects, not the objects they point to. Two references are equal if and only if they point to the same object or both point to ``null``.**

## Relational Operators

| Operator          | Example             | Description                                                |
|-------------------|---------------------|------------------------------------------------------------|
| Less than         | `a < 5`             | Returns true if the value on the left is strictly less than the value on the right |
| Less than or equal to | `b <= 6`         | Returns true if the value on the left is less than or equal to the value on the right |
| Greater than      | `c > 9`             | Returns true if the value on the left is strictly greater than the value on the right |
| Greater than or equal to | `3 >= d`      | Returns true if the value on the left is greater than or equal to the value on the right |
| Type comparison   | `e instanceof String` | Returns true if the reference on the left side is an instance of the type on the right side (class, interface, record, enum, annotation) |

**If the two numeric operands are not of the same data type, the smaller one is promoted**

## **`instanceof` Operator**

 **It is considered a good coding practice to use the instanceof operator prior to casting from one object to a narrower type.**

```java
public void openZoo(Number time) {
if (time instanceof Integer)
System.out.print((Integer)time + " O'clock");
else
System.out.print(time);
}
```

**using `instanceof` with incompatible types does not compile**
**calling instanceof on the null literal or a null reference always returns false.**

## Logical Operators

 **When they’re applied to boolean data types, they’re referred to as logical operators. Alternatively, when they’re applied to numeric data types, they’re referred to as bitwise operators**

| Operator             | Example  | Description                                                     |
| -------------------- | -------- | --------------------------------------------------------------- |
| Logical AND          | `a & b`  | Value is true only if both values are true.                     |
| Logical inclusive OR | `c \| d` | Value is true if at least one of the values is true.            |
| Logical exclusive OR | `e ^ f`  | Value is true only if one value is true and the other is false. |
![[Pasted image 20240118220950.png]]


- **AND is only true if both operands are true.**
- **Inclusive OR is only false if both operands are false.**
- **Exclusive OR is only true if the operands are different.**

```java
boolean resting = eyesClosed | breathingSlowly;
boolean asleep = eyesClosed & breathingSlowly;
boolean awake = eyesClosed ^ breathingSlowly;
System.out.println(resting); // true
System.out.println(asleep); // true
System.out.println(awake); // false
```

## Conditional Operators

| Operator        | Example    | Description                                                                                                               |
| --------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------- |
| Conditional AND | `a && b`   | Value is true only if both values are true. If the left side is false, then the right side will not be evaluated.         |
| Conditional OR  | `c \|\| d` | Value is true if at least one of the values is true. If the left side is true, then the right side will not be evaluated. |
-  **except that the right side of the expression may never be evaluated if the final result can be determined by the left side of the expression.**
- **Be wary of short-circuit behavior on the exam, as questions are known to alter a variable on the right side of the expression that may never be reached. This is referred to as an unperformed side effect.**

```java
int rabbit = 6;
boolean bunny = (rabbit >= 6) || (++rabbit <= 7);
System.out.println(rabbit); // 6 
```

## Ternary Operator

**The first operand must be a boolean expression, and the second and third operands can be any expression that returns a value.** 

```java
int food1 = owl < 4 ? owl > 2 ? 3 : 4 : 5;
int food2 = (owl < 4 ? ((owl > 2) ? 3 : 4) : 5);
```

## Summary 

**This chapter provides a comprehensive overview of Java operators, encompassing unary, binary, and ternary operators. Familiarity with these operators is crucial, and if any are not yet well-understood, a thorough study is recommended. A solid grasp of how to utilize the various Java operators covered in this chapter, coupled with an understanding of operator precedence and the impact of parentheses on expression interpretation, is essential.**

**During the exam, seemingly unrelated questions may actually test knowledge of specific operators, potentially causing compilation failures. Always scrutinize numeric operators, verifying that appropriate data types are used and match where necessary. Since operators are pervasive in exam code samples, a strong comprehension of this chapter enhances preparedness for the OCP**

## Exam Essentials

==**When you’re converting from a smaller to a larger data type, numeric promotion is automatically applied. When you’re converting from a larger to a smaller data type casting is required.**==