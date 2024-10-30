## String

### Concatenating

1. **If both operands are numeric, ``+`` means numeric addition.**
2. **If either operand is a String, ``+`` means concatenation.**
3. **The expression is evaluated left to right.**

```java
System.out.println(1 + 2); // 3
System.out.println("a" + "b"); // ab
System.out.println("a" + "b" + 3); // ab3
System.out.println(1 + 2 + "c"); // 3c
System.out.println("c" + 1 + 2); // c12
System.out.println("c" + null); // cnull
```

- ``null`` is represented as a string when concatenated or printed
- **use numeric addition if two numbers are involved, use concatenation otherwise, and evaluate from left to right.**
### Methods

- **Java counts from 0 when indexed.**
- **String is immutable, or unchangeable. This means calling a method on a String will return a different String object rather than changing the value of the reference.**

```java
var name = "animals";
System.out.println(name.length()); // 7
```

 **zero counting happens only when you’re using indexes or positions within a list**. 

```java
var name = "animals";
System.out.println(name.charAt(0)); // a
System.out.println(name.charAt(6)); // s
System.out.println(name.charAt(7)); // exception
```

```java
var name = "animals";
System.out.println(name.indexOf('a')); // 0
System.out.println(name.indexOf("al")); // 4
System.out.println(name.indexOf('a', 4)); // 4
System.out.println(name.indexOf("al", 5)); // -1
```

**Unlike ``charAt()``, the ``indexOf()`` method doesn’t throw an exception if it can’t find a match, instead returning –1.**

```java
var name = "animals";
System.out.println(name.substring(3)); // mals
System.out.println(name.substring(name.indexOf('m'))); // mals
System.out.println(name.substring(3, 4)); // m
System.out.println(name.substring(3, 7)); // mals
```

**Notice  “stop at” rather than “include.”**

![[Pasted image 20240204161904.png]]

```java
System.out.println(name.substring(3, 3)); // empty string
System.out.println(name.substring(3, 2)); // exception
System.out.println(name.substring(3, 8)); // exception
```

**Since we start and end with the same index, there are no characters in between.**

**The method returns the string starting from the requested index. If an end index is requested, it stops right before that index. Otherwise, it goes to the end of the string.**

```java
var name = "animals";
System.out.println(name.toUpperCase()); // ANIMALS
System.out.println("Abc123".toLowerCase()); // abc123
```

**These methods leave alone any characters other than letters. Also, remember that strings are immutable, so the original string stays the same.**

```java
System.out.println("abc".equals("ABC")); // false
System.out.println("ABC".equals("ABC")); // true
System.out.println("abc".equalsIgnoreCase("ABC")); // true
```

- **The ``equals()`` method checks whether two ``String`` objects contain exactly the same characters in the same order.** 
- **The ``equalsIgnoreCase()`` method checks whether two ``String`` objects contain the same characters, with the exception that it ignores the characters’ case.**


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

 **The`` strip()`` and ``trim()`` methods remove whitespace from the beginning and end of a ``String``**
  **The ``strip()`` method does everything that ``trim()`` does, but it supports Unicode.**

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
    }
}
```



```java
String text = "  Line 1\n  Line 2  ";  
String indented = text.indent(2);  // Positive: Adds 2 spaces  
String normalized = text.indent(-3);  // Negative: No change in indentation  
  
System.out.println("indented:" +indented);  
System.out.println("normalized:" +normalized);
```

The`` indent()`` method 
- **Positive: Adds the same number of blank spaces to the beginning of each line.**
- **Negative: Tries to remove the specified number of whitespace characters from the beginning of the line.**
- **Zero: The indentation remains unchanged.**

``indent()`` also normalizes whitespace characters. What does normalizing whitespace mean, you ask?
- **First, a line break is added to the end of the string if not already there.**
- **Second, any line breaks are converted to the ``\n`` format. Regardless of whether your operating system uses**


**Because of ``\n`` at the end of Line 1, ``indent()`` method also applies to Line 2 and gives the output below**

```text
indented:    Line 1
    Line 2  

normalized:Line 1
Line 2  
```

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



The ``stripIndent()`` method is useful when a ``String`` was built with concatenation rather than using a text block. **It gets rid of all incidental whitespace.**

**If the `stripIndent()` method is used and there are no leading spaces on the first line of a multiline string, no changes will occur. `stripIndent()` only removes the common indentation level from each line, and if there are no leading spaces on the first line, the text remains unchanged.**

```java
String text = "No leading spaces.\n  Indented line.\n  Another indented line.";
System.out.println(text.stripIndent());
```

```text
No leading spaces.
  Indented line.
  Another indented line.
```

Like ``indent()``, ``\r\n`` is turned into \n. However, **the ``stripIndent()`` method does not add a trailing line break if it is missing.**

| Method               | Indent change                                    | Normalizes existing line breaks | Adds line break at end if missing |
|----------------------|--------------------------------------------------|---------------------------------|------------------------------------|
| `indent(n)` where n > 0 | Adds n spaces to beginning of each line           | Yes                             | Yes                                |
| `indent(n)` where n == 0| No change                                        | Yes                             | Yes                                |
| `indent(n)` where n < 0 | Removes up to n spaces from each line             | Yes                             | Yes                                |
| `stripIndent()`       | Removes all leading incidental whitespace         | Yes                             | No                                 |
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


```java
var str = "1\\t2";
System.out.println(str); // 1\t2
System.out.println(str.translateEscapes()); // 1 2
```

- **The first line prints the literal string \t because the backslash is escaped.**
- **The second line prints an actual tab since we translated the escape.**

**The ``translateEscapes()`` method takes these literals and turns them into the equivalent escaped character.**

> The `translateEscapes` method in Java changes special codes like `\n` (new line) and `\t` (tab) within a text into the actual characters they represent, making the text easier to read by processing these escape sequences.

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


```java
public static String format(String format, Object args...)
public static String format(Locale loc, String format, Object args...)
public String formatted(Object args...)
```


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

**Mixing data types may cause exceptions at runtime.** 

**However, on the exam, there is a tendency to cram as much code as possible into a small space. You’ll see code using a technique called *method chaining.***

```java
String result = "AniMaL ".trim().toLowerCase().replace('a', 'A');
System.out.println(result);
```

**To read code that uses method chaining, start at the left and evaluate the first method. Then call the next method on the returned value of the first method. Keep going until you get to the semicolon.**

## ``StringBuilder`` Class

**because the ``String`` object is immutable, a new ``String`` object is assigned to alpha, and the ``""`` object becomes eligible for garbage collection.**

**When we chained ``String`` method calls, the result was a new ``String`` with the answer.**
**StringBuilder changes its own state and returns a reference to itself.**

```java
4: StringBuilder sb = new StringBuilder("start");
5: sb.append("+middle"); // sb = "start+middle"
6: StringBuilder same = sb.append("+end"); // "start+middle+end"
```

```java
4: StringBuilder a = new StringBuilder("abc");
5: StringBuilder b = a.append("de");
6: b = b.append("f").append("g");
7: System.out.println("a=" + a);
8: System.out.println("b=" + b);
```

both print "``abcdefg``". **There’s only one ``StringBuilder`` object here. We know that because ``new StringBuilder()`` is called only once.**

**These four methods work exactly the same as in the String class.**==

```java
var sb = new StringBuilder("animals");
String sub = sb.substring(sb.indexOf("a"), sb.indexOf("al"));
int len = sb.length();
char ch = sb.charAt(6);
System.out.println(sub + " " + len + " " + ch);
```

**The ``replace()`` method works differently for ``StringBuilder`` than it did for ``String``**

```java
public StringBuilder replace(int startIndex, int endIndex, String newString)
```

```java
var builder = new StringBuilder("pigeon dirty");
builder.replace(3, 6, "sty");
System.out.println(builder); // pigsty dirty
```

**the `replace()` method in `StringBuilder` uses start and end index positions to specify the part of the text to be replaced, whereas in `String`, it replaces all occurrences of a specified substring with another substring.**

## Equality

```java
var one = new StringBuilder();
var two = new StringBuilder();
var three = one.append("a");
System.out.println(one == two); // false
System.out.println(one == three); // true
```

**``equals()`` to check the values inside the ``String`` rather than the string reference itself.**
**If a class doesn’t have an ``equals()`` method, Java determines whether the references point to the same object, which is exactly what ``==`` does.**

**``StringBuilder`` did not implement ``equals()``. If you call ``equals()`` on two ``StringBuilder`` instances, it will check reference equality**.

```java
var name = "a";
var builder = new StringBuilder("a");
System.out.println(name == builder); // DOES NOT COMPILE
```

**The string pool, also known as the intern pool, is a location in the Java Virtual Machine (JVM) that collects all these strings.**

**The string pool contains literal values and constants that appear in your program. For example, *"name"* is a literal and therefore goes into the string pool. The ``myObject.toString()`` method returns a string but not a literal, so it does not go into the string pool.**


```java
var x = "Hello World";
var y = "Hello World";
System.out.println(x == y); // true
```

Remember that **a ``String`` is immutable and literals are pooled. The JVM created only one literal in memory. The x and y variables both point to the same location in memory**;

```java
var x = "Hello World";
var z = " Hello World".trim();
System.out.println(x == z); // false
System.out.println(x.equals(z)); // true
```

we don’t have two of the same ``String`` literal. **Although x and z happen to evaluate to the same string, one is computed at runtime. Since it isn’t the same at compile-time, a new ``String`` object is created**

```java
var singleString = "hello world";
var concat = "hello ";
concat += "world";
System.out.println(singleString == concat); // false
```

**Calling ``+=`` is just like calling a method and results in a new ``String``**

```java
var x = "Hello World"; // String Pool
var y = new String("Hello World"); // New Object @ Heap
System.out.println(x == y); // false
```

 **The ``intern()`` method will use an object in the string pool if one is present.**

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
    }
}
```

## Arrays

```java
char[] letters;
```

**Keep in mind that letters is a reference variable and not a primitive. The char type is a primitive. But char is what goes into the array and not the type of the array itself. The array itself is of type char[].**

![[Pasted image 20240206131327.png]]

**When you use this form to instantiate an array, all elements are set to the default value for that type.**

```java
int ids[], types;
```

**This time we get one variable of type int[] and one variable of type int. Java sees this line of code and thinks something like this: “They want two variables of type int. The first one is called ids[]. This one is an int[] called ids. The second one is just called types. No brackets, so it is a regular integer.”

```java
public class Names {
	String names[];
}
```

**The code never instantiated the array, so it is just a reference variable to ``null``**

```java
public class Names {
String names[] = new String[2];
}
```

Each of those two slots currently is ``null`` but has the potential to point to a ``String`` object.

```java
var birds = new String[6];
System.out.println(birds.length);
```

**The length attribute does not consider what is in the array; it only considers how many slots have been allocated.**

### Sorting

```java
String[] strings = { "10", "9", "100" };
Arrays.sort(strings);
for (String s : strings)
System.out.print(s + " "); // 10 100 9
```

**The problem is that ``String`` sorts in alphabetic order, and 1 sorts before 9. (Numbers sort before letters, and uppercase sorts before lowercase.)**

### Searching

Java also provides a convenient way to search, **but only if the array is already sorted.**

**Returns:**
**index of the search key, if it is contained in the array; otherwise,`` (-(insertion point) - 1)``. The insertion point is defined as the point at which the key would be inserted into the array**

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

**As soon as you see the array isn’t sorted, look for an answer choice about unpredictable output.**

### Comparing

- **A negative number means the first array is smaller than the second.**
- **A zero means the arrays are equal.**
-  **A positive number means the first array is larger than the second.**

how to compare arrays of different lengths:

- **If both arrays are the same length and have the same values in each spot in the same order, return zero.**
- **If all the elements are the same but the second array has extra elements at the end, return a negative number.**
- **If all the elements are the same, but the first array has extra elements at the end, return a positive number.**
- **If the first element that differs is smaller in the first array, return a negative number.**
- **If the first element that differs is larger in the first array, return a positive number.**

What does smaller means? 

-  **``null`` is smaller than any other value.**
- **For numbers, normal numeric order applies.**
- **For strings, one is smaller if it is a prefix of another.**
- **For strings/characters, numbers are smaller than letters.**
- **For strings/characters, uppercase is smaller than lowercase.**

**For strings/characters: ``null`` -> numbers -> uppercase -> lowercase**

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
**When comparing two arrays, they must be the same array type.** 

**If the arrays are equal, ``mismatch()`` returns -1. Otherwise, it returns the first index where they differ.**

```java
System.out.println(Arrays.mismatch(new int[] {1}, new int[] {1})); // -1
System.out.println(Arrays.mismatch(new String[] {"a"}, new String[] {"A"})); // 0
System.out.println(Arrays.mismatch(new int[] {1, 2}, new int[] {1})); // 1
```

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
### ``Varargs``

```java
public static void main(String[] args)
public static void main(String args[])
public static void main(String... args) // varargs
```
### Multidimensional Arrays

```java
int[][] vars1; // 2D array
int vars2 [][]; // 2D array
int[] vars3[]; // 2D array
int[] vars4 [], space [][]; // a 2D AND a 3D array

String [][] rectangle = new String[3][2];
rectangle[0][1] = "set";

int [][] args = new int[4][];
args[0] = new int[5];
args[1] = new int[3];
```

## Math API

**If the fractional part is .5 or higher, we round up.**

```java
public static long round(double num)
public static int round(float num)
```

```java
long low = Math.round(123.45); // 123
long high = Math.round(123.50); // 124
int fromFloat = Math.round(123.45f); // 123
```

The ``random()`` method **returns a value greater than or equal to 0 and less than 1**

```java
double num = Math.random(); // 347802527183783
```

## Date & Time

- **`LocalDate` Contains just a date—no time and no time zone.** 
- **``LocalTime`` Contains just a time—no date and no time zone**. 
- **``LocalDateTime`` Contains both a date and time but no time zone**. 
- **``ZonedDateTime`` Contains a date, time, and time zone.** 

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

**The key is the type of information in the output. The output uses ``T`` to separate the date and time when converting ``LocalDateTime`` to a ``String``. Finally, the fourth adds the time zone offset and time zone.**

**The date and time classes have ``private`` constructors along with ``static`` methods that return instances.**

```java
var d = new LocalDate(); // DOES NOT COMPILE
```

**You are not allowed to construct a date or time object directly**.
**The date and time classes are immutable**

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

There are two ways that the exam creators can try to trick you.

```java
var date = LocalDate.of(2024, Month.JANUARY, 20);
date.plusDays(10);
System.out.println(date);
```

Adding 10 days was useless because the program ignored the result. **Whenever you see immutable types, pay attention to make sure that the return value of a method call isn’t ignored.**

```java
var date = LocalDate.of(2024, Month.JANUARY, 20);
date = date.plusMinutes(1); // DOES NOT COMPILE
```

**``LocalDate`` does not contain time. This means that you cannot add minutes to it**. 

### Periods

```java
var annually = Period.ofYears(1); // every 1 year
var quarterly = Period.ofMonths(3); // every 3 months
var everyThreeWeeks = Period.ofWeeks(3); // every 3 weeks
var everyOtherDay = Period.ofDays(2); // every 2 days
var everyYearAndAWeek = Period.of(1, 0, 7); // every year and 7 days
```

There’s one catch. **You cannot chain methods when creating a ``Period``.** 

**Only the last method is used because the ``Period.of ``methods are static methods.**

```java
var wrong = Period.ofYears(1).ofWeeks(1); // every week
```

```java
var wrong = Period.ofYears(1);
wrong = Period.ofWeeks(1);
```

**The ``of()`` method takes only years, months, and days**. 

![[Pasted image 20240207145939.png]]

**You have to pay attention to the type of date and time objects every place you see them.**

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

### Duration

**``Duration`` works roughly the same way as ``Period``, except it is used with objects that have time.**

```java
var daily = Duration.ofDays(1); // PT24H
var hourly = Duration.ofHours(1); // PT1H
var everyMinute = Duration.ofMinutes(1); // PT1M
var everyTenSeconds = Duration.ofSeconds(10); // PT10S
var everyMilli = Duration.ofMillis(1); // PT0.001S
var everyNano = Duration.ofNanos(1); // PT0.000000001S
```

**``Duration`` doesn’t have a factory method that takes multiple units like ``Period`` does**.
**``Duration`` includes another more generic factory method. It takes a number and a ``TemporalUnit``**
``TemporalUnit`` is an interface. At the moment, there is only one implementation named ``ChronoUnit``.
```java
var daily = Duration.of(1, ChronoUnit.DAYS);
var hourly = Duration.of(1, ChronoUnit.HOURS);
var everyMinute = Duration.of(1, ChronoUnit.MINUTES);
var everyTenSeconds = Duration.of(10, ChronoUnit.SECONDS);
var everyMilli = Duration.of(1, ChronoUnit.MILLIS);
var everyNano = Duration.of(1, ChronoUnit.NANOS);
```

### Period vs. Duration

|               | Can use with Period? | Can use with Duration? |
|---------------|----------------------|------------------------|
| LocalDate     | Yes                  | No                     |
| LocalDateTime | Yes                  | Yes                    |
| LocalTime     | No                   | Yes                    |
| ZonedDateTime | Yes                  | Yes                    |
### Instants

The ``Instant`` class represents a specific moment in time in the GMT time zone.

## Summary

- **a ``String`` is an immutable sequence of characters. Calling the constructor explicitly is optional. The concatenation operator ``(+)`` creates a new ``String`` with the content of the first ``String`` followed by the content of the second ``String``. If either operand involved in the + expression is a ``String``, concatenation is used; otherwise, addition is used. String literals are stored in the string pool. The ``String`` class has many methods. By contrast, a ``StringBuilder`` is a mutable sequence of characters. Most of the methods return a reference to the current object to allow method chaining. The ``StringBuilder`` class has many methods.**

- **Calling ``==`` on ``String`` objects will check whether they point to the same object in the pool. Calling ``==`` on ``StringBuilder`` references will check whether they are pointing to the same ``StringBuilder`` object. Calling ``equals()`` on ``String`` objects will check whether the sequence of characters is the same. Calling ``equals()`` on ``StringBuilder`` objects will check whether they are pointing to the same object rather than looking at the values inside.**

- **An array is a fixed-size area of memory on the heap that has space for primitives or pointers to objects. You specify the size when creating it. For example, int[] a = new int[6];. Indexes begin with 0, and elements are referred to using a [0]. The ``Arrays.sort()`` method sorts an array. ``Arrays.binarySearch()`` searches a sorted array and returns the index of a match. If no match is found, it negates the position where the element would need to be inserted and subtracts 1. ``Arrays.compare()`` and ``Arrays.mismatch()`` check whether two arrays are equivalent. Methods that are passed ``varargs (...)`` can be used as if a normal array was passed in. In a multidimensional array, the second-level arrays and beyond can be different sizes.**

- **The Math class provides a number of static methods for performing mathematical operations. For example, you can get minimums or maximums. You can round or even generate random numbers. Some methods work on any numeric primitive, and others only work on double.**

- **A ``LocalDate`` contains just a date, a ``LocalTime`` contains just a time, and a ``LocalDateTime`` contains both a date and a time. All three have private constructors and are created using ``LocalDate.now()`` or ``LocalDate.of()`` (or the equivalents for that class). Dates and times can be manipulated using plusXXX or minusXXX methods. The ``Period`` class represents a number of days, months, or years to add to or subtract from a ``LocalDate`` or ``LocalDateTime``. The date and time classes are all immutable, which means the return value must be used.**

## Essentials

-  Pay special attention to the fact that indexes are zero-based and that the ``substring()`` method gets the string up until right before the index of the second parameter.
- ``==`` checks object equality. ``equals()`` depends on the implementation of the object it is being called on. For the String class, ``equals()`` checks the characters inside of it.
- 

