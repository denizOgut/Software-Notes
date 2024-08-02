# CREATING AND DESTROYING OBJECTS

##  Consider Static Factory Methods Instead Of Constructors 

Make class constructor private, and call that constructor from static named methods:

```java
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
}
```

One advantage of static factory methods is that, unlike constructors, they have names. A static factory with a well-chosen name is easier to use, and the resulting client code is easier to read.

A class can have only a single constructor with a given signature. To get around this restriction by providing two constructors whose parameter lists differ only in the order of their parameter types. This is a **really bad idea ( ambiguity )**. The user of such an API will never be able to remember which constructor is which and will end up calling the wrong one by mistake.

**Because static factory methods have names, they don't share the restriction in cases where a class seems to require multiple constructors with the same signature. Replace the constructors with static factory methods and carefully chosen names to highlight their differences.**

The `Boolean.valueOf(boolean)` method illustrates this technique: it never creates an object. It can greatly improve performance if equivalent objects are requested often, especially if they are expensive to create.

### Instance Controlled:

Ensures that only one instance of a class is created and provides a global point of access to that instance.

Instance control allows a class to guarantee that it is a singleton or noninstantiable. Also, it allows an immutable value class to make the guarantee that no two equal instances exist. `a.equals(b)` if and only if `a == b`.

### Unlike constructors, they can return an object of any subtype of their return type.

This gives you great flexibility in choosing the class of the returned object.

### The class of the returned object can vary from call to call as a function of the input parameters.

Any sub-type of the declared return type is tolerable.

### The class of the returned object need not exist when the class containing the method is written.

Such flexible static factory methods form the basis of service provider frameworks. There are three essential components in a service provider framework:

- **Service Interface**: Represents Implementation
- **Provider Registration API**: Providers use to register implementation
- **Service Access API**: Obtain an instance of API

### The Main Limitation Of Providing Only Static Factory Method Is That Classes Without Public Or Protected Constructors Can Not Be Subclassed

**Static Factory Methods Are Hard For Programmers To Find**

Common names for static factory methods:

- **from**: Type Conversion method, e.g., `Date d = Date.from(instant);`
- **of**: An aggregation method, e.g., `Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);`
- **valueOf**: A more verbose alternative to  from  and  of , e.g., `BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);`
- **instance  or  getInstance**: Returns an instance that is described by its parameters, e.g., `StackWalker luke = StackWalker.getInstance(options);`
- **create  or  newInstance**: Methods guarantee that each call returns a new instance, e.g., `Object newArray = Array.newInstance(classObject, arrayLen);`
- **getType**: Like getInstance but used if the factory method is in a different class, e.g., `FileStore fs = Files.getFileStore(path);`
- **newType**: Like newInstance but used if the factory method is in a different class, e.g., `BufferedReader br = Files.newBufferedReader(path);`
- **type**: An alternative to getType and newType, e.g., `List<Complaint> litany = Collections.list(legacyLitany);`

##  Consider A Builder When Faced With Many Constructor Parameters 

Static factories and constructors share a limitation: they do not scale well to large numbers of optional parameters. Telescoping constructor pattern and JavaBeans pattern are two approaches to handle this limitation.

Telescoping constructor pattern involves providing a constructor with only the required parameters. While it works, it becomes hard to write and read client code when there are many parameters.

JavaBeans pattern involves calling a no-args constructor to create the object and then calling setter methods to set each required and optional parameter of interest. However, this pattern makes it possible for the object to be in an inconsistent state partway through its construction, and it prevents the possibility of making a class immutable.

Instead of making the desired object directly, the Builder pattern is suggested. The client calls a constructor (or static factory) with all the required parameters and gets a  builder  object. The client then calls setter-like methods on the builder object to set each optional parameter of interest. The builder is typically a static member class of the class it builds.

### The Builder pattern simulates named optional parameters and is well-suited for class hierarchies.

Abstract classes have abstract builders, and concrete classes have concrete builders. A minor advantage of builders over constructors is that builders can have multiple varargs parameters because each parameter is specified in its own method.

The Builder pattern is quite flexible. A single builder can be used repeatedly to build multiple objects. The parameters of the builder can be tweaked between invocations of the build method to vary the objects that are created. A builder can fill in some fields automatically upon object creation.

The Builder pattern has disadvantages as well. In order to create an object, you must first create its builder. The pattern is more verbose than the telescoping constructor pattern, so it should be used only if there are enough parameters to make it worthwhile. Often, it's better to start with a builder in the first place.

The Builder pattern is a good choice when designing classes whose constructor or static factories would have more than a handful of parameters, especially if many of the parameters are optional or of identical type.

##  Enforce The Singleton Property With A Private Constructor Or An Enum Type 

Singletons typically represent either a stateless object, such as a function, or a system component that is intrinsically unique. Making a class a singleton can make it difficult to test its clients.

### Singleton with public final fields:

```java
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis() {...}

    public void leaveTheBuilding() {...}
}
```

The private constructor is called only once to initialize the public static final field `Elvis.INSTANCE`. The main advantage of the public field approach is that the API makes it clear that the class is a singleton. The second advantage is that it's simpler.

### Enum Singleton - the preferred approach:

```java
public enum Elvis {
    INSTANCE;

    public void leaveTheBuilding() {...}
}
```

This approach is similar to the public field approach but is more concise, provides the serialization machinery for free, and guarantees against multiple instantiation. A single-element enum type is often the best way to implement a singleton.

## Enforce Noninstantiability With A Private Constructor

A class that is just a grouping of static methods and static fields can be used to group related methods on primitive values or arrays (e.g., `java.lang.Math`, `java.util.Arrays`). It can also be used to group static methods, including factories for objects that implement some interface methods (e.g., `java.util.Collections`). Such classes can be used to group methods on a final class since you can't put them in a subclass. Such utility classes were not designed to be instantiated; an instance would be absurd.

Attempting to enforce noninstantiability by making a class abstract does not work. There is a simple idiom to ensure noninstantiability: include a private constructor.

```java
// Noninstantiable utility class
public class UtilityClass {
    // Suppress default constructor for noninstantiability
    private UtilityClass() {
        throw new AssertionError();
    }
    // ...
}
```

Because the explicit constructor is private, it is inaccessible outside the class. This guarantees that the class will never be instantiated under any circumstances and also prevents the class from being subclassed.

## Prefer Dependency Injection To Hardwiring Resources

Static utility classes and singletons are inappropriate for classes whose behavior is parameterized by an underlying resource. Pass the resource to the constructor when creating a new instance. A useful variant of the pattern is to pass a resource factory to the constructor. A factory is an object that can be called repeatedly to create instances of a type. Factories embody the Factory Method pattern, and the `Supplier <T>` interface, introduced in Java 8, is perfect for representing factories.

```java
Mosaic create(Supplier<? extends Tile> tileFactory) {...}
```

Do not use a singleton or static utility class to implement a class that depends on one or more underlying resources whose behavior affects that of the class. Instead, pass the resources or factories to create them into the constructor (or static factory or builder).

## Avoid Creating Unnecessary Objects

Reuse can be both faster and more stylish. An object can always be reused if it is immutable. You can often avoid creating unnecessary objects by using static factory methods in preference to constructors on immutable classes that provide both. For example, the factory method `Boolean.valueOf(String)` is preferable to the constructor `Boolean(String)` (deprecated). The constructor must create a new object each time it's called, while the factory method is never required to do so and won't in practice.

Some object creations are much more expensive than others. If you are going to need such an "expensive object" repeatedly, it may be advisable to cache it for reuse.

```java
// Performance can be greatly improved
static boolean isRomanNumeral(String s) {
    return s.matches("regular expression");
}
```

While `String.matches` is the easiest way to check if a string matches a regular expression, it is not suitable for repeated use in performance-critical situations. The problem is that it internally creates a `Pattern` instance for the regex and uses it only once, after which it becomes eligible for garbage collection.

```java
// Reusing expensive object for improved performance
public class RomanNumerals {
    private static final Pattern ROMAN = Pattern.compile("regex");

    static boolean isRomanNumeral(String s) {
        return ROMAN.matcher(s).matches();
    }
}
```

When an object is immutable, it is obvious it can be reused safely, but there are other situations where it is far less obvious, even illogical.

Autoboxing blurs but does not erase the distinction between primitive and boxed primitive types.

```java
// Hideously Slow
private static long sum() {
    Long sum = 0L; // Make primitive long sum = 0L;
    for (...)
        sum += val;
    return sum;
}
```

Prefer primitives to boxed primitives, and watch out for unintentional autoboxing. Defensive copying is a technique that involves creating a new object when you should reuse an existing one or vice versa.

```java
public class MyClass {
    private List<String> myList;

    public MyClass(List<String> list) {
        this.myList = new ArrayList<>(list); // make a defensive copy of the list
    }

    public List<String> getMyList() {
        return new ArrayList<>(myList); // return a defensive copy of the list
    }
}
```

Creating objects unnecessarily may affect style and performance.

## Eliminate Obsolete Object References

```java
public class Stack {
    // ... fields and constructor
    public Object pop() { 
        if (size == 0)
            throw new EmptyStackException();
        Object result = elements[--size]; // Memory Leak
        elements[size] = null; // eliminate obsolete reference / prevent memory leak
        return result;
    }
}
```

The objects that were popped off the stack will not be garbage collected, even if the program using the stack has no more references to them. This is because the stack maintains "obsolete references" to these objects; obsolete references are references that will never be dereferenced again.

Nulling out object references should be the exception rather than the norm. The best way to eliminate an obsolete reference is to let the variable that contained the reference fall out of scope. This occurs naturally if you define each variable in the narrowest possible scope.

Whenever a class manages its memory, the programmer should be alert for memory leaks. Whenever an element is freed, any object references contained in the element should be nulled out. Another common source of memory leaks is caches. Once you put an object reference into a cache, it's easy to forget that it is there and leave it in the cache long after it becomes irrelevant. A third common source of memory leaks is listeners and other callbacks. If you implement an API where clients register callbacks but don't deregister them explicitly, they will accumulate unless you take some action.

## Avoid Finalizers And Cleaners

Finalizers are unpredictable, often dangerous, and generally unnecessary.
Their use can cause erratic behavior, poor performance, and portability problems. Cleaners are less dangerous than finalizers, but they are still unpredictable.

In Java, the garbage collector reclaims the storage associated with an object when it becomes unreachable. Try-with-resources or try-finally blocks are used for this purpose.

One major shortcoming of finalizers and cleaners is that there is no guarantee they will be executed promptly, if at all.

**Never do anything time-critical in a finalizer or cleaner.** Never depend on a finalizer or cleaner to update persistent state. There is a severe performance penalty for using finalizers and cleaners. Finalizers have a serious security problem: they open your class up to finalizer attacks. Throwing an exception from a constructor should be sufficient to prevent an object from coming into existence; in the presence of finalizers, it is not. To protect non-final classes from finalizer attacks, write a final `finalize` method that does nothing.

**Just have your class implement `AutoCloseable` and require its clients to invoke the `close` method on each instance when it is no longer needed.**

So, what, if anything, are cleaners and finalizers good for?

1. They can act as a safety net in case the owner of a resource neglects to call its `close` method.
2. They concern objects with native peers.

## Prefer Try-With-Resources To Try-Finally

If you write a class that represents a resource that must be closed, your class should implement `AutoCloseable` too.

### Try-with-resources - the best way to close resources!

```java
static String firstLineOfFile(String path) throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader(path))) {
        return br.readLine();
    }
}
```

### Try-with-resources - on multiple resources

```java
static void copy(String src, String dst) throws IOException {
    try (InputStream in = new FileInputStream(src);
         OutputStream out = new FileOutputStream(dst)) {
        byte[] buf = new byte[BUFFER_SIZE];
        int n;
        while ((n = in.read(buf)) >= 0)
            out.write(buf, 0, n);
    }
}
```

Always use try-with-resources in preference to try-finally when working with resources that must be closed. The resulting code is shorter, clearer, and the exceptions that it generates are more useful.

# Methods Common to All Objects

Although `Object` is a concrete class, it is designed primarily for extension. All of its non-final methods (`equals`, `hashCode`, `toString`, `clone`, and `finalize`) have explicit general contracts because they are designed to be overridden.

### Obey The General Contract When Overriding Equals

If any of the following conditions apply, do not override:

- Each instance of the class is inherently unique (e.g., `Thread`).
- There is no need for the class to provide a "logical equality" test (e.g., `java.util.regex.Pattern`).
- A superclass has already overridden `equals`, and the superclass behavior is appropriate for this class (e.g., Map Implementations or Set Implementations).
- The class is private or package-private, and you are certain that its `equals` method will never be invoked.

```java
@Override
public boolean equals(Object o) {
    throw new AssertionError(); // Method is never called.
}
```

When is it appropriate to override equals? When a class has a notion of logical equality that differs from mere object identity, and a superclass has not already overridden `equals`. This is generally for value classes.

### Value Class

A value class represents a single value, similar to a primitive type, but with additional functionality and behavior. Value classes are immutable and are often used to represent simple data types, such as integers, strings, or dates.

```java
public class Point {
    private final int x;
    private final int y;
    // Constructor... Getter / Setter
    // Equal, HashCode, ToString methods overridden...
}
```

When you override the `equals` method, you must adhere to its general contracts:

- **Reflective:** For any non-null reference value `x`, `x.equals(x)` must return true (Object must be equal to itself).
- **Symmetric:** For any non-null reference values `x` and `y`, `x.equals(y)` must return true if and only if `y.equals(x)` returns true (Any two objects must agree on whether they are equal).
- **Transitive:** For any non-null reference values `x`, `y`, `z`, if `x.equals(y)` returns true and `y.equals(z)` returns true, then `x.equals(z)` must return true (If one object is equal to a second and the second equals to third, then the first equals to third).
- **Consistent:** If two objects are equal according to the method, they must remain equal for the entire lifetime of the objects, as long as their state doesn't change.
- **Non-nullity:** All objects must be unequal to null.

If you violate it, you may well find that your program behaves erratically or crashes, and it can be very difficult to pin down the source of the failure.

For an `equals` method to be useful, all of the elements in each "equivalence class" must be interchangeable.

### Equivalence Class

An equivalence class is a set of objects that are considered equivalent under some equivalence relation. In other words, an equivalence class is a group of objects that are indistinguishable from each other with respect to a particular property or criterion.

```java
// Broken - violates symmetry!
public final class CaseInsensitiveString {
    private final String s;
    // Constructor...

    // Broken - violates symmetry
    @Override
    public boolean equals(Object o) {
        if (o instanceof CaseInsensitiveString)
            return s.equalsIgnoreCase((String) o); // One-way interoperability!
    }
}
```

Once you have violated the `equals` contract, you simply don't know how other objects will behave when confronted with your object.

```java
// Broken - violates symmetry!
@Override
public boolean equals(Object o) {
    if (!(o instanceof ColorPoint))
        return false;
    return super.equals(o) && ((ColorPoint) o).color == color;
}
```

The problem with this method is that you might get different results when comparing a point to a color point or vice versa:

```java
Point p = new Point(1, 2);
ColorPoint cp = new ColorPoint(1, 2, Color.RED);
```

The `p.equals(cp)` returns true, while `cp.equals(p)` returns false.

```java
// Broken - violates transitivity!
@Override
public boolean equals(Object o) {
    if (!(o instanceof Point))
        return false;

    // If o is a normal Point, do a color-blind comparison
    if (!(o instanceof ColorPoint))
        return o.equals(this);

    return super.equals(o) && ((ColorPoint) o).color == color;
}
```

This approach provides symmetry but at the expense of transitivity:

```java
ColorPoint cp1 = new ColorPoint(1, 2, Color.RED);
Point p2 = new Point(1, 2);
ColorPoint cp3 = new ColorPoint(1, 2, Color.BLUE);
```

Now `p1.equals(p2)` and `p2.equals(p3)` return true, while `p1.equals(p3)` returns false, a clear violation of transitivity.

There is no way to extend an instantiable class and add value components while preserving the `equals` contract. Favor composition over inheritance.

Do not write an `equals` method that depends on unreliable resources. To test its argument for equality, the `equals` method must first cast its argument to an appropriate type so its accessors can be invoked or its fields accessed. Before doing the cast, the method must use the `instanceof` operator to check that its argument is of the correct type:

```java
@Override
public boolean equals(Object o) {
    if (!(o instanceof MyType))
        return false;
    MyType mt = (MyType) o;
    //....
}
```

The `instanceof` operator is specified to return false if its first operand is null, regardless of what type appears in the second operand.

### Recipe For High-Quality Equals Method

- Use the `==` operator to check if the argument is a reference to this object. If so, return true.
- Use the `instanceof` operator to check if the argument has the correct type. If not, return false.
- Cast the argument to the correct type because this cast was preceded by an `instanceof` test, it is guaranteed to succeed.
- For each "significant" field in the class, check if that field of the argument matches the corresponding field of this object.
    - For primitive fields whose type is not `float` or `double`, use the `==` for comparisons.
    - For object reference fields, call the `equals` method recursively.
    - For `float` fields, use the static `Float.compare(float, float)` method.
    - For `double` fields, use the static `Double.compare(double, double)` method.
    - For array fields, if every element in an array field is significant, use one of the `Arrays.equals` methods.
- For some classes, field comparisons are more complex than simple equality tests. You may want to store a "canonical form" rather than a more costly non-standard comparison. This technique is most appropriate for immutable classes.

The performance of the `equals` method may be affected by the order in which fields are compared. For the best performance, you should first compare fields that are more likely to differ, less expensive to compare, or ideally both.

When you are finished writing your `equals` method, ask yourself three questions:

1. Is it symmetric?
2. Is it transitive?
3. Is it consistent?

Your `equals` method must also satisfy the other two properties (reflexivity and non-nullity), but these two usually take care of themselves.

```java
@Override
public boolean equals(Object o) {
    if (o == this)
        return true;
    if (!(o instanceof PhoneNumber))
        return false;
    PhoneNumber pn = (PhoneNumber) o;

    return pn.lineNum == lineNum && pn.prefix == prefix && pn.areaCode == areaCode;
}
```

Always override `hashCode` when you override `equals`. Don't try to be too clever, and don't substitute another type for `Object` in the `equals` declaration.

```java
public boolean equals(MyClass o) {} // Broken - Parameter must be object
```

The problem is that the method does not override `Object.equals` but overloads it instead.

Writing and testing `equals` (and `hashCode`) methods is tedious, and the resulting code is usually repetitive. An alternative is the Google Open Source AutoValue Framework. Having IDEs generate `equals` (and `hashCode`) methods is generally preferable to implementing them manually because IDEs do not make careless mistakes, and humans do.

In summary, don't override the `equals` method unless you have to. If you do override `equals`, make sure to compare all of the class's significant fields and compare them in a manner that preserves all five provisions of the `equals` contract.

## Always Override HashCode When You Override Equals

You must override `hashCode` in every class that overrides `equals`.

### HashCode Contract

The key provision that is violated when you fail to override `hashCode` is that equal objects must have equal hash codes.

```java
Map<PhoneNumber, String> m = new HashMap<>();
m.put(new PhoneNumber(707, 867, 5309), "Jenny");

// The worst possible legal hashCode implementation - never use !!!
@Override
public int hashCode() {
    return 42;
}
```

It's legal because it ensures that equal objects have the same hash code. It's atrocious because it ensures that every object has the same hash code.

A good hash function tends to produce unequal hash codes for unequal instances.

### Simple Recipe For Hash Code

1. Compute an `int` hash code `c` for the field.
2. Combine the hash code `c` computed in step 2.a into `result` as follows:

```java
result = 31 * result + c;
```

3. Return `result`.

```java
// Typical hashCode method
@Override
public int hashCode() {
    int result = hashCode;
    if (result == 0) {
        result = Short.hashCode(areaCode);
        result = 31 * result + Short.hashCode(prefix);
        result = 31 * result + Short.hashCode(lineNum);
        hashCode = result;
    }
    return result;
}
```

Do not be tempted to exclude significant fields from the hash code computation to improve performance. Do not provide a detailed specification for the value returned by `hashCode`, so clients can't reasonably depend on it; this gives you the flexibility to change.

You must override `hashCode` every time you override `equals` or your program will not run correctly. Your `hashCode` method must obey the general contract specified in `Object` and must do a reasonable job assigning unequal hash codes to unequal instances.

## Always Override ToString

The general contract for `toString` says that the returned string should be "a concise but informative representation that is easy for a person to read."

Providing a good `toString` implementation makes your class much more pleasant to use and makes systems using the class easier to debug. The `toString` method is automatically invoked when an object is passed to print functions, the string concatenation operator, or `assert`, or is printed by a debugger.

When practical, the `toString` method should return all of the interesting information contained in the object. If the object is large or if it contains state that is not conducive to string representation, `toString` should return a summary.

One important decision you'll have to make when implementing a `toString` method is whether to specify the format of the return value in the documentation. The advantage of specifying the format is that it serves as a standard, unambiguous, human-readable representation of the object. If you specify the format, it is usually a good idea to provide a matching static factory or constructor so programmers can easily translate back and forth between the object and its string representation. The disadvantage is that you are stuck with a defined format, which gives flexibility to add information.

Whether or not you decide to specify the format, you should clearly document your intentions. Provide programmatic access to the information contained in the value returned by `toString`.

It makes no sense to write a `toString` method in a static utility class. Nor write a `toString` method in most enum types. However, write a `toString` method in any abstract class whose subclasses share a common string representation. Override `Object`'s `toString` implementation in every instantiable class you write unless a superclass has already done so.

## Override Clone Judiciously (Cautious)

If a class implements `Cloneable`, `Object`'s `clone` method returns a field-by-field copy of the object; otherwise, it throws `CloneNotSupportedException`. Normally, implementing an interface says something about what a class can do for its clients. In this case, it modifies the behavior of a protected method on a superclass.

In practice, a class implementing `Cloneable` is expected to provide a properly functioning public `clone` method.

- `x.clone() != x` will be true, and the expression `x.clone().getClass() == x.getClass()` will be true, but these are not absolute requirements.
- `x.clone().equals(x)` will be true; this is not an absolute requirement.

Immutable classes should never provide a `clone` method

```java
// Clone method for class with no references to mutable state
@Override
public PhoneNumber clone() {
    try {
        return (PhoneNumber) super.clone();
    } catch (CloneNotSupportedException e) {
        throw new AssertionError(); // Can't happen
    }
}
```

In order for this method to work, the class declaration for `PhoneNumber` would have to be modified to indicate that it implements `Cloneable`.

In effect, the `clone` method functions as a constructor; you must ensure that it does no harm to the original object and that it properly establishes invariants on the clone.

The `Cloneable` architecture is incompatible with the normal use of final fields referring to mutable objects. To make a class cloneable, it may be necessary to remove final modifiers from some fields.

Public `clone` methods should omit the `throws` clause. You have two choices when designing a class for inheritance, but whichever one you choose, the class should not implement `Cloneable`.

To recap, all classes that implement `Cloneable` should override `clone` with a public method whose return type is the class itself. This method should first call `super.clone` then fix any fields that need fixing. A better approach to object copying is to provide a copy constructor or copy factory.

A better approach to object copying is to provide a copy constructor or copy factory.

```java

// Copy constructor
public Yum(Yum yum) {...}

// Copy factory
public static Yum newInstance(Yum yum) {...};

```
As a rule, copy functionality is best provided by constructors or factories. A notable exception to this rule is arrays, which are best copied with the clone method

## Consider Implementing Comparable

By implementing `Comparable`, a class indicates that its instances have a natural ordering.

If you are writing a value class with an obvious natural ordering, such as alphabetical order, numerical order, or chronological order, you should implement the `Comparable` interface:

```java
public interface Comparable<T> {
    int compareTo(T t);
}
```

Unlike the `equals` method, which imposes a global equivalence relation on all objects, `compareTo` doesn't have to work across objects of different types; when confronted with objects of different types, `compareTo` is permitted to throw `ClassCastException`.

A `compareTo` method must obey the same restrictions imposed by the `equals` contract: reflexivity, symmetry, and transitivity.

The `compareTo` method should generally return the same results as the `equals` method. If this override is obeyed, the ordering imposed by the `compareTo` method is said to be consistent with equals.

Writing a `compareTo` method is similar to writing an `equals` method, but there are a few key differences. You don't need to type-check or cast its argument. If the argument is of the wrong type, the invocation won't even compile. If the argument is `null`, the invocation should throw a `NullPointerException`.

In a `compareTo` method, fields are compared for order rather than equality.

```java
// Use of the relational operators < and > in compareTo method is verbose and error-prone and no longer recommended
public int compareTo(PhoneNumber pn) {
    int result = Short.compare(areaCode, pn.areaCode);
    if (result == 0) {
        result = Short.compare(prefix, pn.prefix);
        if (result == 0)
            result = Short.compare(lineNum, pn.lineNum);
    }

    return result;
}
```

In summary, whenever you implement a value class that has a sensible ordering, you should have the class implement the `Comparable` interface so that its instances can be easily sorted, searched, and used in comparison-based collections. When comparing field values in the implementations of the `compareTo` methods, avoid the use of the `<` and `>` operators. Instead, use the static `compare` methods in the boxed primitive classes or the comparator construction methods in the `Comparator` interface.

## Conclusion

- When overriding the `equals` method, adhere to its general contracts.
- Always override `hashCode` when you override `equals`.
- Always override `toString`.
- Override `clone` judiciously and consider providing copy constructors or copy factories.
- Consider implementing `Comparable` for classes with a natural ordering.

# Classes and Interfaces

## Minimize The Accessibility Of Classes And Members

The single most important factor that distinguishes a well-designed component from a poorly designed one is the degree to which the component hides its internal data and other implementation details from other components. A well-designed component hides all its implementation details, cleanly separating its API from its implementation. This concept, known as "information hiding" or "encapsulation," is a fundamental tenet of software design.

**Information hiding is important for many reasons:**

- Allowing code to be developed, tested, optimized, used, understood, and modified in isolation. This speeds up system development because components can be developed in parallel.
- Easing the burden of maintenance because components can be understood more quickly.
- Enabling effective performance tuning.
- Increasing software reuse because components aren't tightly coupled.
- Decreasing the risk in building large systems because individual components may prove successful even if the system does not.

### Make each class or member as inaccessible as possible:

- Use the lowest possible access level consistent with the proper functioning of the software you are writing.

For top-level (non-nested) classes and interfaces, there are only two possible access levels: package-private (default) and public.

- By making it package-private, you make it part of the implementation rather than the exported API. You can modify, replace, or eliminate it in a subsequent release without fear of harming existing clients.
- If you make it public, you are obligated to support it forever to maintain compatibility.

If a package-private top-level class or interface is used by only one class, consider making the top-level class a private static nested class of the sole class that uses it. This reduces its accessibility from all the classes in its package to the one class that uses it.

Access levels in Java:

- **private:** Accessible only from the top-level class where it is declared.
- **package-private:** Accessible from any class in the package where it's declared.
- **protected:** Accessible from subclasses of the class where it is declared.
- **public:** Accessible from anywhere.

After carefully designing your class's public API, your reflex should be to make all other members private.

For members of public classes, a huge increase in accessibility occurs when the access level goes from package-private to protected. A protected member is part of the class-exported API and must be supported forever.

There is a key rule:

- **"If a method overrides a superclass method, it cannot have a more restrictive access level in the subclass than in the superclass."**
    - This is necessary to ensure that an instance of the subclass is usable anywhere that an instance of the superclass is usable (Liskov substitution).

A special case of this rule is that if a class implements an interface, all of the class methods that are in the interface must be declared public in the class.

### Instances fields of public classes should rarely be public:

- Classes with public mutable fields are not generally thread-safe.

It is wrong for a class to have a public static final array field or an accessor that returns such a field:

```java
// Potential security hole!
public static final Thing[] VALUES = {...};
```

There are two ways to fix the problem. You can make the public array private and add a public immutable list:

```java
private static final Thing[] VALUES = {...};
public static final List<Thing> VALUES = Collections.unmodifiableList(Arrays.asList(PRIVATE_VALUES));
```

Or you can make the array private and add a public method that returns a copy of a private array:

```java
private static final Thing[] VALUES = {...};
public static final Thing[] values() {
    return PRIVATE_VALUES.clone();
}
```

A module is a grouping of packages, like a package is a grouping of classes. Using the module system allows you to share classes among packages within a module without making them visible to the entire world.

Unlike the four main access levels, the two module-based levels are largely advisory ("advice"). You should reduce the accessibility of program elements as much as possible (within reason).

With the exception of public static final fields, which serve as constants, public classes should have no public fields. Ensure that objects referenced by public static final fields are immutable.

## In Public Classes, Use Accessor Methods, Not Public Fields

Degenerate classes like this should not be public:

```java
class Point {
    public double x;
    public double y;
}
```

Such classes should always be replaced by classes with private fields and public accessor methods ("getters") and, for mutable classes, mutators ("setters"):

```java
public double getX() {return x;}
public double getY() {return y;}

public void setX(double x) {this.x = x;}
public void setY(double y) {this.y = y;}
```

If a class is accessible outside its package, provide accessor methods.

If a class is package-private nested class, there is nothing inherently wrong with exposing its data fields.

Several classes in the Java Platform libraries violate the advice that public classes should not expose fields directly. While it's never a good idea for a public class to expose fields directly, it is less harmful if the fields are immutable.

In summary, public classes should never expose mutable fields. It is, however, sometimes desirable for package-private or private nested classes to expose fields, whether mutable or immutable.

## Minimize Mutability

An immutable class is simply a class whose instances cannot be modified. All of the information contained in each instance is fixed for the lifetime of the object. There are many good reasons for immutability:

- Easier to design, implement, and use than mutable classes.
- Less prone to error and more secure.

**5 Rules to make a class immutable:**

1. **Don't provide methods that modify the object's state (known as mutators).**
2. **Ensure that the class can't be extended:**
    - This prevents careless or malicious subclasses from compromising the immutable behavior of the class by behaving as if the object's state has changed.
    - Make the class `final`.
3. **Make all fields final:**
    - This clearly expresses your intent in a manner that is enforced by the system.
4. **Make all fields private:**
    - This prevents clients from obtaining access to mutable objects referred to by fields and modifying these objects directly.
5. **Ensure exclusive access to any mutable components:**
    - Make defensive copies.

In Java, defensive copies can be created by implementing the `Cloneable` interface and overriding the `clone` method of a class. Alternatively, defensive copies can be created by creating a new object and copying the state of the original object into it using getters and setters.

Immutable objects are simple; an immutable object can be in exactly one state, the state in which it was created. Immutable objects are inherently thread-safe; they require no synchronization. Immutable objects can be shared freely.

A disadvantage of immutable classes is that they require a separate object for each distinct value. Creating these objects can be costly, especially if they are large. The performance problem is magnified if you perform a multistep operation that generates a new object at every step, eventually discarding all objects except the final result.

To mitigate this, provide multistep operations as primitives, and internally, the immutable class can use a "companion class" to speed up multistep operations. The `StringBuilder` is an example of the "companion class" approach.

A more flexible alternative is to make the class final, make all of its constructors final, and add public static factories in place of the public constructors:

```java
// Immutable class with static factories instead of constructors
public class Complex {
    private final double re;
    private final double im;

    private Complex(double re, double im) {
        this.re = re;
        this.im = im;
    }

    public static Complex valueOf(double re, double im) {
        return new Complex(re, im);
    }
}
```

This approach is often the best alternative, as it is the most flexible, allowing the use of multiple package-private implementation classes to expose different aspects of the immutable class to its clients that reside outside its package.

Resist the urge to write a setter for every getter. Classes should be immutable unless there's a very good reason to make them mutable. If a class cannot be made immutable, limit its mutability as much as possible.

Declare every field private final unless there's a good reason to do otherwise. Constructors should create fully initialized objects with all of their invariants established.

## Favor Composition Over Inheritance

It is safe to use inheritance within a package, where the subclass and the superclass implementations are under the control of the same programmers. Unlike method invocation, inheritance violates encapsulation; a subclass depends on the implementation details of its superclass for its proper function. A subclass must evolve tandem with its superclass unless the superclass's authors have designed and documented it specifically for the purpose of being extended.

A better approach is to use composition (having an instance of another class within the class) instead of inheritance. This design is called composition because the existing class becomes a component of the new one.

Each instance method in the new class invokes the corresponding method on the contained instance of the existing class and returns the results. This is known as "forwarding," and the methods in the new class are known as "forwarding methods."

For example, consider the following:

```java
// Wrapper class - uses composition in place of inheritance
public class InstrumentedSet<E> extends ForwardingSet<E> {
    // ...
}

// Reusable forwarding class
public class ForwardingSet<E> implements Set<E> {
    private final Set<E> s;
}
```

The disadvantages of wrapper classes are few. One caveat is that wrapper classes are not suited for use in callback frameworks because a wrapped object doesn't know of its wrapper; it passes a reference to itself (`this`), and callbacks elude the wrapper. This is known as the SELF problem.

In summary, inheritance is powerful, but it is problematic because it violates encapsulation. It is appropriate only when a genuine subtype relationship exists between the subclass and the superclass. Even then, inheritance may lead to fragility if the subclass is in a different package from the superclass and the superclass is not designed for inheritance. To avoid this fragility, use composition and forwarding instead of inheritance.

## Design And Document For Inheritance Or Else Prohibit It

For a class to be designed and documented for inheritance, it must document its self-use if it contains overridable methods (nonfinal and either public or protected). By overridable, it means that a method can be overridden by a subclass. More generally, a class must document any circumstances under which it might invoke an overridable method.

To allow programmers to write efficient subclasses without undue pain, a class may have to provide hooks into its internal workings in the form of judiciously chosen protected methods. The only way to test a class designed for inheritance is to write subclasses. You must test your class by writing subclasses before you release it.

There are a few more restrictions that a class must obey to allow inheritance. Constructors must not invoke overridable methods, either directly or indirectly. The `Cloneable` and `Serializable` interfaces present special difficulties when designing for inheritance.

You should be aware that because the `clone` and `readObject` methods behave a lot like constructors, a similar restriction applies: neither `clone` nor `readObject` may invoke an overridable method, directly or indirectly.

In summary, you must document all of its self-use patterns, and once you have documented them, you must commit to them for the life of the class.

## Prefer Interfaces To Abstract Classes

Existing classes can easily be retrofitted to implement a new interface. All you have to do is add the required methods (if they don't yet exist) and add an `implements` clause to the class declaration.

Interfaces are ideal for defining mixins. A mixin is a type that a class can implement in addition to its "primary type" to declare that it provides some optional behavior (e.g., `Comparable`).

Abstract classes can't be used to define mixins for the same reason that they can't be retrofitted onto existing classes: a class cannot have more than one parent, and there is no reasonable place in the class hierarchy to insert a mixin.

Interfaces allow for the construction of nonhierarchical type frameworks. For example:

```java
public interface Singer {
    AudioClip sing(Song s);
}

public interface Songwriter {
    Song compose(int chartPosition);
}
```

In real life, some singers are also songwriters. It is perfectly permissible for a single class to implement both `Singer` and `Songwriter`. In fact, we can define a third interface that extends both `Singer` and `Songwriter` and adds new methods that are appropriate to the combination:

```java
public interface SingerSongWriter extends Singer, Songwriter {
    AudioClip strum();
    void actSensitive();
}
```

Interfaces enable safe, powerful functionality enhancements. Combine the advantages of interfaces and abstract classes by providing an abstract skeletal implementation class to go with an interface. This design is known as the "skeletal implementation" and is a design pattern in Java that provides a partial implementation of an interface or abstract class, leaving certain methods to be implemented by concrete subclasses. It is often used to reduce code duplication and provide a consistent implementation across multiple subclasses.

The interface defines the type, perhaps providing some default methods, while the skeletal implementation class implements the remaining non-primitive interface methods. Stop the primitive interface methods, known as the "Template Method Pattern."

If a class cannot be made to extend the skeletal implementation, the class can always implement the interface directly. Good documentation is absolutely essential in a skeletal implementation.

To summarize, an interface provides a mechanism for defining a contract, allowing multiple classes to implement the same set of methods without the constraints of a single inheritance hierarchy. This flexibility enables diverse types to exhibit common behavior through shared interfaces.

Interfaces are particularly valuable for:

1. **Defining Contracts:** Interfaces define a set of methods that a class must implement, establishing a contract for the behavior of classes that implement them.
    
2. **Enabling Multiple Inheritance:** Unlike classes, which support single inheritance, a class can implement multiple interfaces. This allows for the creation of rich and diverse types.
    
3. **Promoting Code Reusability:** Interfaces allow unrelated classes to share common functionality through a shared interface. This promotes code reuse and modularity.
    
4. **Facilitating Polymorphism:** Interfaces play a crucial role in achieving polymorphism, allowing objects of different classes to be treated as objects of a common interface.
    
5. **Defining Mixins:** Interfaces can be used to define mixins, allowing classes to provide optional behavior by implementing additional interfaces.
    

When to Use Interfaces:

- **To Define a Contract:** Use interfaces when you want to define a contract that multiple classes can implement. This is particularly useful when you want to provide a common set of methods without enforcing a specific implementation.
    
- **For Multiple Inheritance:** Use interfaces when you need a class to inherit behavior from multiple sources. Unlike classes, which support single inheritance, interfaces enable a class to implement multiple interfaces.
    
- **To Enable Polymorphism:** Use interfaces when you want to achieve polymorphism, allowing objects of different classes to be treated as objects of a common interface.
    
- **For Code Reusability:** Use interfaces when you want to promote code reuse by allowing unrelated classes to share common functionality through a shared interface.
    

It's worth noting that Java 8 introduced the concept of default methods in interfaces, providing a way to add new methods to interfaces without breaking backward compatibility. Default methods have default implementations and can be overridden by classes that implement the interface.

In summary, interfaces are a powerful tool in Java for defining contracts, enabling multiple inheritance, promoting code reusability, and facilitating polymorphism. They play a crucial role in creating flexible and modular code structures. When designing classes, prefer interfaces over abstract classes to achieve greater flexibility and encourage code reuse.


## Don't Use Raw Types

A class or interface whose declaration has one or more type parameters is a generic class or interface. `List<E>`=> "List Of E".

Each generic type defines a raw type, which is the name of the generic type used without any accompanying type parameters. For example, the raw type corresponding to `List<E>` is `List`. Raw types behave as if all of the generic type information were erased from the type declaration.

```java
// Raw collection type - don't do this!
private final Collection stamps = ...;

// Erroneous insertion of coin into stamp collection
stamps.add(new Coin(...)); // Emits "unchecked call" warning
```

You don't get an error until you try to retrieve the coin from the stamp collection.

```java
// Parameterized collection type - typesafe
private final Collection<Stamp> stamps = ...;
```

From this declaration, the compiler knows that `stamps` should contain only `Stamp` instances and guarantees it to be true, assuming your entire codebase compiles without emitting any warnings. When `stamp` is declared with a parameterized type declaration, the erroneous insertion generates a compile-time error message that tells you exactly what is wrong.

If you use raw types, you lose all the safety and expressiveness benefits of generics.

"Migration Compatibility": Applications that were built using an older version of a library or system should be able to run without modification or with minimal modification on the newer version of the library or system.

You lose type safety if you use a raw type such as `List`, but not if you use a parameterized type such as `List<Object>`.

```java
// Use of raw type for an unknown element type - don't do this!
static int numElementsInCommon(Set s1, Set s2) {...}
```

If you want to use a generic type but you don't know or care what the actual type parameter is, you can use an "unbounded wildcard type `<?>`."

```java
// Use of unbounded wildcard type - typesafe and flexible
static int numElementsInCommon(Set<?> s1, Set<?> s2) {...}
```

A wildcard type is safe, and the raw type isn't. You can put any element into a collection with a raw type, easily corrupting the collection's type invariants. You can't put any element (other than null) into a `Collection<?>`.

You must use raw types in class literals. `List.class`, `String[].class`, and `int.class` are all legal, but `List<String>.class` is not. Because generic type information is erased at runtime, it is illegal to use the `instanceof` operator on parameterized types other than unbounded wildcard types.

```java
// Legitimate use of raw type - instanceof operator
if (o instanceof Set) {  // Raw type
    Set<?> s = (Set<?>) o; // Wildcard type
}
```

In summary, using raw types can lead to exceptions at runtime, so don't use them. They are provided only for compatibility and interoperability with legacy code.

| **Term**                | **Example**                        |
| ----------------------- | ---------------------------------- |
| Parameterized type      | `List<String>`                     |
| Actual type parameter   | `String`                           |
| Generic type            | `List<E>`                          |
| Formal type parameter   | `E`                                |
| Unbounded wildcard type | `List<?>`                          |
| Raw type                | `List`                             |
| Bounded type parameter  | `<E extends Number>`               |
| Recursive type bound    | `<T extends Comparable<T>>`        |
| Bounded wildcard type   | `List<? extends Number>`           |
| Generic method          | `static <E> List<E> asList(E[] a)` |
| Type token              | `String.class`                     |

## Eliminate Unchecked Warnings

When you get warnings that require some thought, persevere! Eliminate every unchecked warning that you can. If you eliminate all warnings, you are assured that your code is typesafe.

If you can't eliminate a warning, but you can prove that the code that provoked the warning is typesafe, then (and only then) suppress the warning with an `@SuppressWarnings("unchecked")` annotation. If you suppress warnings without first proving that the code is typesafe, you are giving yourself a false sense of security.

If, however, you ignore unchecked warnings that you know to be safe (instead of suppressing them), you won't notice when a new warning crops up that represents a real problem. Always use the `SuppressWarnings` annotation on the smallest scope possible.

It is illegal to put a `SuppressWarnings` annotation on the return statement because it isn't a declaration. You might be tempted to put the annotation on the entire method, but don't. Instead, declare a local variable to hold the return value and annotate its declaration.

Every time you use a `@SuppressWarnings("unchecked")` annotation, add a comment saying why it is safe to do so. It will decrease the odds that someone will modify the code so as to make the computation unsafe.

In summary, unchecked warnings are important. Don't ignore them. Every unchecked warning represents the potential for a `ClassCastException` at runtime.

## Prefer Lists To Arrays

Arrays differ from generic types in two important ways. First, arrays are covariant; generics are invariant.

`Covariant`: A subclass can be used in place of its superclass, and the same holds true for covariant types in generics.

`Invariant`: The type relationship between two different instantiations of a generic type is fixed and cannot be changed.

```java
// Fails at runtime!
Object[] objectArray = new Long[1];
objectArray[0] = "I don't fit in"; // Throws ArrayStoreException

// Won't compile!
List<Object> ol = new ArrayList<Long>(); // Incompatible types
ol.add("I don't fit in");
```

With an array, you find out that you've made a mistake at runtime; with a list, you find out at compile time.

The second major difference between arrays and generics is that arrays are reified; generics are implemented by erasure. This means that arrays know and enforce their element type at runtime, while generics enforce their type constraints only at compile time and discard their element type information at runtime.

Because of these fundamental differences, arrays and generics do not mix well.

Why is it illegal to create a generic array? Because it isn't typesafe.

```java
// Why generic array creation is illegal - won't compile!
List<String>[] stringLists = new List<String>[1]; // (1)
List<Integer> intList = List.of(42); // (2)
Object[] objects = stringLists; // (3)
objects[0] = intList; // (4)
String s = stringLists[0].get(0); // (5)
```

When you get a generic array creation error or an unchecked cast warning on a cast to an array type, the best solution is often to use the collection type `List<E>` in preference to the array type `E[]`. You might sacrifice some conciseness or performance, but in exchange, you get better type safety and interoperability.

In summary, arrays and generics have very different type rules. Arrays are covariant and reified; generics are invariant and erased. As a consequence, arrays provide runtime type safety but not compile-time type safety, vice versa for generics.

## Favor Generic Types

```java
// Object-based collection - a prime candidate for generics
public class Stack {
    private Object[] elements;
    //....

    public Stack() {
        elements = new Object[DEFAULT_INITIAL_CAPACITY];
    }

    public void push(Object e) {
        //...
    }

    public Object pop() {
        //...
        Object result = elements[--size];
    }
}
```

The first step in generifying a class is to add one or more type parameters to its declaration. In this case, there is one type parameter, representing the element type of the stack.

The next step is to replace all the uses of the type `Object` with the appropriate type parameter and then try to compile the resulting program.

```java
// Object-based collection - a prime candidate for generics
public class Stack<E> {
    private E[] elements;
    //....

    public Stack() {
        elements = new E[DEFAULT_INITIAL_CAPACITY];
    }

    public void push(E e) {
        //...
    }

    public E pop() {
        //...
        E result = elements[--size];
    }
}
```

The only elements stored in the array are those passed to the `push` method, which are of type `E`, so the unchecked cast can do no harm. Once you've proved that an unchecked cast is safe, suppress the warning in as narrow a scope as possible.

The second way to eliminate the generic array creation error in `Stack` is to change the type of the field `elements` from `E[]`.

The first is more readable:

- The array is declared to be of type `E[]`, clearly indicating that it contains only `E` instances.
- It is also more concise; in a typical generic class, the array appears at many points in the code; the first technique requires only a single cast.
- The first technique is preferable and more commonly used in practice.
- It does, however, cause heap pollution.

```java
// Achieving runtime type safety with a dynamic cast
public <T> void putFavorite(Class<T> type, T instance) {
    favorites.put(type, type.cast(instance));
}
```

In summary, generic types are safer and easier to use than types that require casts in client code. When you design new types, make sure that they can be used without such casts. Only this makes types generic.

## Favor Generic Methods

```java
// Uses raw types - unacceptable! (Item 26)
public static Set union(Set s1, Set s2) {
    Set result = new HashSet(s1);
    result.addAll(s2);
    return result;
}

// Generic method
public static <E> Set<E> union(Set<E> s1, Set<E> s2) {
    Set<E> result = new HashSet<>(s1);
    result.addAll(s2);
    return result;
}
```

A limitation of the `union` method is that types of all three sets have to be exactly the same. You can make the method more flexible by using `<?>`.

```java
// Generic singleton factory pattern
private static UnaryOperator<Object> IDENTITY_FN = (t) -> t;

@SuppressWarnings("unchecked")
public static <T> UnaryOperator<T> identityFunction() {
    return (UnaryOperator<T>) IDENTITY_FN;
}
```

In summary, generic methods, like generic types, are safer and easier to use than methods requiring their clients to put explicit casts on input parameters and return values. Like types, you should make sure that your methods can be used without casts, which often means making them generic. And like types, you should generify existing methods whose use requires casts.

## Use Bounded Wildcards To Increase API Flexibility

```java
// pushAll method without wildcard type - deficient!
public void pushAll(Iterable<E> src) {
    for (E e : src)
        push(e);
}

// Wildcard type for a parameter that serves as an E producer
public void pushAll(Iterable<? extends E> src) {
    for (E e : src)
        push(e);
}


// popAll method without wildcard type - deficient!
public void popAll(Collection<E> dst) {
    while (!isEmpty())
        dst.add(pop());
}

// Wildcard type for a parameter that serves as an E consumer
public void popAll(Collection<? super E> dst) {
    while (!isEmpty())
        dst.add(pop());
}
```

For maximum flexibility, use wildcard types on input parameters that represent producers or consumers. PECS stands for producer-extends, consumer-super. PECS is a guideline for using bounded wildcards in Java generics to ensure type safety when dealing with collections. It helps to remember that when you want to retrieve elements from a collection, use `extends`, and when you want to add elements to a collection, use `super`.

Properly used, wildcard types are nearly invisible to the users of a class. They cause methods to accept the parameters they should accept and reject those they should reject. If the user of a class has to think about wildcard types, there is probably something wrong with its API.

If a type parameter appears only once in a method declaration, replace it with a wildcard.

In summary, using wildcard types in your APIs, while tricky, makes the APIs far more flexible. If you write a library that will be widely used, the proper use of wildcard types should be considered mandatory. Remember the basic rule "PECS".

## Combine Generic And Varargs Judiciously

The purpose of varargs is to allow clients to pass a variable number of arguments to a method, but it is a leaky abstraction.

Heap pollution occurs when a variable of a parameterized type refers to an object that is not of that type. It can cause the compiler's automatically generated casts to fail, violating the fundamental guarantee of the generic type system.

It is unsafe to store a value in a generic varargs array parameter.

The `SafeVarargs` annotation constitutes a promise by the author of a method that it is typesafe.

```java
// Safe method with a generic varargs parameter
@SafeVarargs
static <T> List<T> flatten(List<? extends T>... lists) {
    List<T> result = new ArrayList<>();
    for (List<? extends T> list : lists)
        result.addAll(list);
    return result;
}
```

Use `@SafeVarargs` on every method with a varargs parameter of a generic or parameterized type. A generic varargs method is safe if:

  
a. **It Doesn't Store Anything in the Varargs Parameter Array:**

```java
// Safe method with a generic varargs parameter
@SafeVarargs
static <T> List<T> flatten(List<? extends T>... lists) {
    List<T> result = new ArrayList<>();
    for (List<? extends T> list : lists)
        result.addAll(list);
    return result;
}
```

In the example above, the method `flatten` does not store anything in the `lists` array. It only iterates over the arrays and extracts elements without modifying the arrays themselves. This ensures that there is no heap pollution.

b. **It Doesn't Make the Array (or a Clone) Visible to Untrusted Code:**

```java
// Safe method with a generic varargs parameter
@SafeVarargs
static <T> List<T> flatten(List<? extends T>... lists) {
    List<T> result = new ArrayList<>();
    for (List<? extends T> list : lists)
        result.addAll(list);
    return result;
}
```

The `flatten` method in this example does not leak the `lists` array or any clone of it to untrusted code. The method creates a new `ArrayList` and populates it with elements from the input lists, but it doesn't expose the internal representation of the array to external code.

Remember that while `@SafeVarargs` provides a degree of safety, it doesn't eliminate all potential pitfalls. It's crucial to design varargs methods carefully, ensuring that they adhere to the outlined principles.

In summary, when using generic varargs, employ the `@SafeVarargs` annotation on methods to indicate that they are safe and follow the guidelines mentioned above to prevent heap pollution and maintain type safety.

## Consider Typesafe Heterogeneous Containers

A heterogeneous container is a container that can hold elements of different types. While Java's arrays are homogeneous (they must have a single element type), generics provide a way to create typesafe heterogeneous containers.

```java
// Typesafe heterogeneous container pattern
public class Favorites {
    private Map<Class<?>, Object> favorites = new HashMap<>();

    public <T> void putFavorite(Class<T> type, T instance) {
        favorites.put(Objects.requireNonNull(type), type.cast(instance));
    }

    public <T> T getFavorite(Class<T> type) {
        return type.cast(favorites.get(type));
    }
}
```

In this example, the `Favorites` class uses a `Map` with `Class` objects as keys and objects of type `Object` as values. The `putFavorite` method allows you to associate a class token with an instance, and the `getFavorite` method retrieves the instance based on the class token.

This pattern ensures type safety at compile time. When you retrieve an instance using `getFavorite`, the compiler knows the exact type based on the class token, and you don't need to cast the result.

Usage example:

```java
Favorites favorites = new Favorites();
favorites.putFavorite(String.class, "Java");
favorites.putFavorite(Integer.class, 42);

String favoriteString = favorites.getFavorite(String.class);
Integer favoriteInteger = favorites.getFavorite(Integer.class);
```

This approach eliminates the need for explicit casting and provides a typesafe way to work with a container that can hold elements of different types.

In summary, when you need a container that can hold elements of different types, prefer using the typesafe heterogeneous container pattern to ensure compile-time type safety.

# ENUMS

## Use Enums Instead Of Int Constants

An enumerated type is a type whose legal values consist of a fixed set of constants. Before enum types were added to the language, a common pattern for representing enumerated types was to declare a group of named int constants, one for each member of the types.

This technique, known as the "int enum pattern," has many shortcomings. It provides nothing in the way of type safety and little in the way of expressive power. The compiler won't complain if you pass an apple to a method that expects an orange, compare apples to oranges with the == operator, or worse.

Programs that use int enums are brittle. Because int enums are constant variables, their int values are compiled into the clients that use them. If the value associated with an int enum is changed, its clients must be recompiled. If not, the clients will still run, but their behavior will be incorrect.

You may encounter a variant of this pattern in which String constants are used in place of int constants, known as the "String enum pattern." If such a hard-coded string constant contains a typographical error, it will escape detection at compile time and result in bugs at runtime.

```java
public enum Apple {FUJI, PIPPIN, GRANNY_SMITH}
public enum Orange {NAVEL, TEMPLE, BLOOD}
```

The basic idea behind Java's enum type is simple: they are classes that export one instance for each enumeration constant via a public static final field. Enum types are effectively final, by virtue of having no accessible constructors. Enum types are instance-controlled. They are a generalization of singletons, which are essentially single-element enums. Enums provide compile-time safety.

Enum types with identically named constants coexist peacefully because each type has its own namespace. Enum types let you add arbitrary methods and fields and implement arbitrary interfaces. They provide high-quality implementations of all the Object methods. They implement Comparable and Serializable, and their serialized form is designed to withstand most changes to enum type.

An enum type can start life as a simple collection of enum constants and evolve over time into a full-featured abstraction.

```java
// Enum type with data and behavior
public enum Planet {
    MERCURY(3.302e+23, 2.439e6),
    VENUS(4.869e+24, 6.052e6),
    EARTH(5.975e+24, 6.378e6),
    // ... other planets ...
    NEPTUNE(1.024e+26, 2.477e7);

    private final double mass; // In kilograms
    private final double radius; // In meters

    // Universal gravitational constant in m^3 / kg s^2
    private static final double G = 6.67300E-11;

    // Constructor
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }

    public double mass() { return mass; }
    public double radius() { return radius; }
    // ... other methods ...
}
```

To associate data with enum constants, declare instance fields and write a constructor that takes the data and stores it in the fields. Enums are, by their nature, immutable, so all fields should be final. Fields can be public, but it is better to make them private and provide public accessors.

What happens when you remove an element from an enum type? The answer is that any client program that doesn't refer to the removed element will continue to work fine. If an enum is generally useful, it should be a top-level class; if its use is tied to a specific top-level class, it should be a member class of that top-level class.

```java
// Enum type that switches on its own value - questionable
public enum Operation {
    PLUS, MINUS, TIMES, DIVIDE;

    // Do the arithmetic operation represented by this constant
    public double apply(double x, double y) {
        switch(this) {
            case PLUS: return x + y;
            case MINUS: return x - y;
            case TIMES: return x * y;
            case DIVIDE: return x / y;
        }
        throw new AssertionError("Unknown op: " + this);
    }
}
```

Luckily, there is a better way to associate different behavior with each enum constant: declare an abstract apply method in the enum type, and override it with a concrete method for each constant in a constant-specific class body. Such methods are known as constant-specific method implementations.

```java
// Enum type with constant-specific method implementations
public enum Operation {
    PLUS {
        public double apply(double x, double y) { return x + y; }
    },
    MINUS {
        public double apply(double x, double y) { return x - y; }
    },
    TIMES {
        public double apply(double x, double y) { return x * y; }
    },
    DIVIDE {
        public double apply(double x, double y) { return x / y; }
    };
}
```

Constant-specific method implementations can be combined with constant-specific data.

```java
// Enum type with constant-specific class bodies and data
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

Enum types have an automatically generated valueOf(String) method that translates a constant's name into the constant itself.

```java
// The strategy enum pattern
enum PayrollDay {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY(PayType.WEEKEND), SUNDAY(PayType.WEEKEND);

    private final PayType payType;

    PayrollDay(PayType payType) {
        this.payType = payType;
    }

    PayrollDay() {
        this(PayType.WEEKDAY); // Default
    }

    int pay(int minutesWorked, int payRate) {
        return payType.pay(minutesWorked, payRate);
    }

    // The strategy enum type
    private enum PayType {
        WEEKDAY {
            int overtimePay(int minsWorked, int payRate) {
                return minsWorked <= MINS_PER_SHIFT ? 0 :
                       (minsWorked - MINS_PER_SHIFT) * payRate / 2;
            }
        },
        WEEKEND {
            int overtimePay(int minsWorked, int payRate) {
                return minsWorked * payRate / 2;
            }
        };

        abstract int overtimePay(int mins, int payRate);

        private static final int MINS_PER_SHIFT = 8 * 60;

        int pay(int minsWorked, int payRate) {
            int basePay = minsWorked * payRate;
            return basePay + overtimePay(minsWorked, payRate);
        }
    }
}
```

The strategy enum pattern is a design pattern used in object-oriented programming. It involves using an enumeration (enum) to define a set of related algorithms or strategies and then using the enum values to select which strategy to use at runtime.

If switch statements on enums are not a good choice for implementing constant-specific behavior on enums, what are they good for? Switches on enums are good for augmenting enum types with constant-specific behavior.

A minor performance disadvantage of enums is that there is a space and time cost to load and initialize enum types, but it is unlikely to be noticeable in practice.

Use enums any time you need a set of constants whose members are known at compile time. It is not necessary that the set of constants in an enum type stay fixed for all time. Enums are more readable, safer, and more powerful. Consider the strategy enum pattern if some, but not all, enum constants share common behaviors.

## Use Instance Fields Instead Of Ordinals

All enums have an ordinal method, which returns the numerical position of each enum constant in this type.

```java
// Abuse of ordinal to derive an associated value - DON'T DO THIS
public enum Ensemble {
    SOLO, DUET, TRIO, QUARTET, QUINTET,
    SEXTET, SEPTET, OCTET, NONET, DECTET;

    public int numberOfMusicians() {
        return ordinal() + 1;
    }
}
```

While this enum works, it is a maintenance nightmare. If the constants are reordered, the numberOfMusicians method will break. Never derive a value associated with an enum from its ordinal; store it in an instance field instead.

```java
public enum Ensemble {
    SOLO(1), DUET(2), TRIO(3), QUARTET(4), QUINTET(5), SEXTET(6), SEPTET(7),
    OCTET(8), DOUBLE_QUARTET(8), NONET(9), DECTET(10), TRIPLE_QUARTET(12);

    private final int numberOfMusicians;

    Ensemble(int size) {
        this.numberOfMusicians = size;
    }

    public int numberOfMusicians() {
        return numberOfMusicians;
    }
}
```

## Use EnumSet Instead Of Bit Fields

Bit fields have all the disadvantages of int enum constants and more. It is even harder to interpret a bit field than a simple int enum constant when it is printed as a number. There is no easy way to iterate over all the elements represented by a bit field. Finally, you're writing the API and choose a type for the bit field accordingly.

A better alternative exists. The EnumSet class efficiently represents sets of values drawn from a single enum type. This class implements the Set interface, providing all the richness, type safety, and interoperability you get with any other Set implementation.

```java
// EnumSet - a modern replacement for bit fields
public class Text {
    public enum Style { BOLD, ITALIC, UNDERLINE, STRIKETHROUGH }

    // Any Set could be passed in, but EnumSet is clearly best
    public void applyStyles(Set<Style> styles) { ... }
}
```

```java
text.applyStyles(EnumSet.of(Style.BOLD, Style.ITALIC));
```


In summary, just because an enumerated type will be used in sets, there is no reason to represent it with bit fields. The only real disadvantage of EnumSet is that it is not, as of Java 9, possible to create an immutable EnumSet.

## Use EnumMap Instead Of Ordinal Indexing

When you access an array that is indexed by an enum's ordinal, it is your responsibility to use the correct int value; ints do not provide the type safety of enums. It is rarely appropriate to use ordinals to index into arrays: use EnumMap instead. If the relationship you are representing is multidimensional, use EnumMap <..., EnumMap<...>>.

## Emulate Extensible Enums With Interfaces

For the most part, extensibility of enums turns out to be a bad idea. It is confusing that elements of an extension type are instances of the base type and not vice versa. Finally, extensibility would complicate many aspects of the design and implementation, such as "Operation Codes (opcodes)," which is an enumerated type whose elements represent operations on some machinery.

Sometimes it is desirable to let the users of an API provide their own operations, effectively extending the set of operations provided by the API.

```java
public interface Operation {
    double apply(double x, double y);
}

public enum BasicOperation implements Operation {
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

    BasicOperation(String symbol) {
        this.symbol = symbol;
    }
}
```

In summary, while you cannot write an extensible enum type, you can emulate it by writing an interface to accompany a basic enum type that implements the interface.

# ANNOTATION

## Prefer Annotations To Naming Patterns

Typographical errors in naming patterns can lead to silent failures. Additionally, naming patterns lack the ability to ensure they are used only on appropriate program elements. Another disadvantage is their inability to associate parameter values with program elements.

Annotations provide an elegant solution to these problems. Consider defining an annotation type to designate simple tests that are run automatically and fail if they throw an exception:

```java
import java.lang.annotation.*;

/**
 * Indicates that the annotated method is a test method.
 * Use only on parameterless static methods.
 */
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Test {
}
```

Here, `Retention` and `Target` annotations are known as meta-annotations. This annotation is called a marker annotation because it has no parameters but simply "marks" the annotated element.

```java
// Program containing marker annotations
public class Sample {
    @Test
    public static void m1() { } // Test should pass

    public static void m2() { }

    @Test
    public static void m3() { // Test should fail
        throw new RuntimeException("Boom");
    }

    public static void m4() { }

    @Test
    public void m5() { } // INVALID USE: nonstatic method

    public static void m6() { }

    @Test
    public static void m7() { // Test should fail
        throw new RuntimeException("Crash");
    }

    public static void m8() { }
}
```

Annotations don't change the semantics of the annotated code but enable it for special treatment by tools.

As of Java 8, you can use the `@Repeatable` meta-annotation to indicate that the annotation may be applied repeatedly to a single element, providing a cleaner way to do multivalued annotations.

In summary, there is no reason to use naming patterns when annotations can be used instead. All programmers should use the predefined annotation types that Java provides.

## Consistently Use The Override Annotation

The `@Override` annotation can only be used on method declarations, indicating that the method declaration overrides a declaration in a supertype. Consistently using this annotation helps protect against a large class of bugs.

```java
@Override
public void someMethod() {
    // method implementation
}
```

If you are writing a class that is not labeled abstract and you believe that it overrides an abstract method in its superclass, you need not bother putting the `@Override` annotation on that method.

However, it is good practice to use `@Override` on concrete implementations of interface methods to ensure that the signature is correct.

In abstract classes or interfaces, it is worth annotating all methods that you believe to override superclass or superinterface methods, whether concrete or abstract.

In summary, the compiler can protect against many errors if you use the `@Override` annotation on every method declaration that you believe to override a supertype declaration.

## Use Marker Interface To Define Types

A marker interface is an interface that contains no method declarations but merely designates (or "marks") a class that implements the interface as having some property. An example is the `Serializable` interface.

Marker interfaces have two advantages:

1. Marker interfaces define a type that is implemented by instances of the marked class; marker annotations do not.
    
2. Marker interfaces can be targeted more precisely than marker annotations.
    

The chief advantage of marker annotations over marker interfaces is that they are part of the larger annotation facility.

When to use a marker annotation or a marker interface depends on the context. Use an annotation if the marker applies to any program element other than a class or interface. If the marker applies only to classes and interfaces, consider whether you might want to write methods that accept only objects with this marking. If so, use a marker interface.

If you're convinced that you'll never want to write a method accepting only objects with the marking, use a marker annotation.

In summary, both marker interfaces and marker annotations have their uses. If you want to define a type without new methods, a marker interface is suitable. If marking applies to program elements other than classes and interfaces or fits into a framework using annotations, a marker annotation is the correct choice. If you create a marker annotation with `ElementType.TYPE`, consider if a marker interface might be more appropriate.

# LAMBDA

## Prefer Lambdas To Anonymous Classes

In Java 8, the introduction of lambda expressions formalized the idea that interfaces with a single abstract method are special, known as functional interfaces. Lambdas provide a concise way to create instances of these interfaces, replacing the need for anonymous classes.

Replace an anonymous class with a lambda expression:

```java
// Anonymous Class Instance As a Function Object - Obsolete!
Collections.sort(words, new Comparator<String>() {
    public int compare(String s1, String s2) {
        return Integer.compare(s1.length(), s2.length());
    }
});

// Lambda Expression As Function Object (Replace Anonymous Class)
Collections.sort(words, (s1, s2) -> Integer.compare(s1.length(), s2.length()));
```

The compiler deduces types from context using a process known as "type inference." It's generally recommended to omit the types of lambda parameters unless their presence makes the program clearer.

Lambdas make it easy to implement constant-specific behavior, replacing anonymous classes:

```java
// Enum with function object fields & constant-specific behavior
public enum Operation {
    PLUS("+", (x, y) -> x + y),
    MINUS("-", (x, y) -> x - y),
    TIMES("*", (x, y) -> x * y),
    DIVIDE("/", (x, y) -> x / y);

    private final String symbol;
    private final DoubleBinaryOperator op;

    Operation(String symbol, DoubleBinaryOperator op) {
        this.symbol = symbol;
        this.op = op;
    }

    @Override
    public String toString() {
        return symbol;
    }

    public double apply(double x, double y) {
        return op.applyAsDouble(x, y);
    }
}
```

While lambdas lack names and documentation, it's advised to keep them concise—ideally, one line, with three lines being a reasonable maximum. If a lambda becomes long or difficult to read, consider simplifying or refactoring.

There are a few things that can be done with anonymous classes but not with lambdas, such as creating instances of interfaces with multiple abstract methods or obtaining a reference to itself.

In summary, prefer lambdas over anonymous classes unless you need to create instances of types that aren't functional interfaces.

## Prefer Method References To Lambdas

Method references provide a concise way to express lambdas, resulting in shorter and clearer code. Consider using method references, especially when the method has multiple parameters, as they eliminate boilerplate code.

Example:

```java
map.merge(key, 1, (count, incr) -> count + incr);

map.merge(key, 1, Integer::sum);
```

Method references are usually preferable for brevity and clarity. However, if a lambda is more succinct, especially when the method is in the same class, it might be a reasonable choice.

```java
service.execute(GoshThisClassNameIsHumongous::action);

service.execute(() -> action());
```

Choose method references when they are shorter and clearer, and stick with lambdas where they are more appropriate.

# Favor The Use Of Standard Functional Interfaces

In modern Java programming, it is often more practical to use standard functional interfaces provided in `java.util.function` than creating custom ones. For instance, static factory methods or constructors that accept a function object as a parameter can achieve the same effect without introducing unnecessary functional interfaces.

Example:

```java
protected boolean removeEldestEntry(Map.Entry<K,V> eldest) {
    return size() > 199;
}

// Unnecessary functional interface; use a standard one instead.
@FunctionalInterface
interface EldestEntryRemovalFunction<K,V> {
    boolean remove(Map<K,V> map, Map.Entry<K,V> eldest);
}
```

If a standard functional interface fulfills the requirements, it is generally preferable over creating a purpose-built functional interface. Annotate your functional interfaces with `@FunctionalInterface` for clarity.

For performance reasons, avoid using boxed primitives instead of primitive functional interfaces, especially for bulk operations. Consider writing a purpose-built functional interface only when it shares characteristics with `Comparator` or requires a specific contract, name, or custom default methods.

In summary, prefer standard functional interfaces from `java.util.function` unless there are compelling reasons to create a custom functional interface. Always annotate your functional interfaces with `@FunctionalInterface` for clarity.

# STREAM

## Use Streams Judiciously

The Streams API in Java provides abstractions for working with sequences of data elements. Streams can represent finite or infinite sequences and are processed through a stream pipeline, which consists of a source stream, zero or more intermediate operations, and one terminal operation. Stream pipelines are evaluated lazily, meaning that computation doesn't start until the terminal operation is invoked.

While the Streams API is powerful, overusing it can make programs hard to read and maintain. The API is designed to be fluent, allowing method calls in a pipeline to be chained into a single expression. However, careful naming of lambda parameters is crucial for readability.

```java
public class Anagrams {
    public static void main(String[] args) throws IOException {
        Path dictionary = Paths.get(args[0]);
        int minGroupSize = Integer.parseInt(args[1]);
        try (Stream<String> words = Files.lines(dictionary)) {
            words.collect(groupingBy(word -> alphabetize(word)))
                 .values()
                 .stream()
                 .filter(group -> group.size() >= minGroupSize)
                 .forEach(g -> System.out.println(g.size() + ": " + g));
        }
    }
    // alphabetize method is the same as in the original version
}
```

When using streams, explicit types are essential for readability. Additionally, using helper methods becomes even more important in stream pipelines than in iterative code. Streams are powerful but should be used judiciously. If unsure whether streams or iteration are better suited for a task, try both and choose the one that works better.

## Prefer Side-Effect-Free Functions In Streams

The Streams paradigm encourages structuring computations as sequences of transformations, with each stage as close as possible to a pure function. Avoid side effects in streams, as they can lead to unpredictable behavior.

```java
// Don't do this!
Map<String, Long> freq = new HashMap<>();
try (Stream<String> words = new Scanner(file).tokens()) {
    words.forEach(word -> {
        freq.merge(word.toLowerCase(), 1L, Long::sum);
    });
}

// Proper use of streams to initialize a frequency table
Map<String, Long> freq;
try (Stream<String> words = new Scanner(file).tokens()) {
    freq = words.collect(groupingBy(String::toLowerCase, counting()));
}
```

The `forEach` operation in streams should be used only to report the result, not to perform the computation. Statically importing all members of `Collectors` can make stream pipelines more readable. Important collector factories include `toList`, `toSet`, `toMap`, `groupingBy`, and `joining`.

## Prefer Collection To Stream As A Return Type

When writing a method that returns a sequence of elements, consider returning a `Collection` or an appropriate subtype. Accommodate both users who want to process the elements as a stream and those who prefer iteration.

```java
// Won't compile, due to limitations on Java's type inference
for (ProcessHandle ph : ProcessHandle.allProcesses()::iterator) {
    // Process the process
}

// Better workaround using an adapter method
for (ProcessHandle p : iterableOf(ProcessHandle.allProcesses())) {
    // Process the process
}
```

Use adapter methods to convert between streams and iterables. A `Collection` is generally the best return type for a public sequence-returning method. Do not store a large sequence in memory just to return it as a collection.

## Use Caution When Making Streams Parallel

Parallelizing a stream can improve performance, but it's not always beneficial. Avoid parallelizing stream pipelines indiscriminately. Some data structures and operations benefit more from parallelism, such as ArrayList, HashMap, HashSet, ConcurrentHashMap instances, arrays, int ranges, and long ranges.

**Not only can parallelizing a stream lead to poor performance, including liveness failures; it can lead to incorrect results and unpredictable behavior.**

The best terminal operations for parallelism are reductions, and short-circuiting operations like `anyMatch`, `allMatch`, and `noneMatch` are also amenable to parallelism. However, inappropriate parallelization can lead to performance disasters and incorrect results. Experiment carefully, ensuring correctness and performance gains before parallelizing stream pipelines in production code.

# METHODS

## Check Parameters For Validity

When writing methods and constructors, it's essential to validate the parameters to ensure they meet the specified restrictions. Document these restrictions and enforce them with explicit checks at the beginning of the method. The `Objects.requireNonNull` method introduced in Java 7 is a flexible and convenient way to handle null checks.

```java
// Inline use of Java's null-checking facility
this.strategy = Objects.requireNonNull(strategy, "strategy");
```

Validate parameters even if they are not immediately used by the method but are stored for later use. Always think about the restrictions on method parameters, document them, and enforce them with checks.

## Make Defensive Copies When Needed

When dealing with mutable components in a class, especially when accepting them as parameters or returning them, it's crucial to make defensive copies. This ensures that the internal state of an object is not inadvertently modified from outside.

```java
public Period(Date start, Date end) {
    this.start = new Date(start.getTime());
    this.end = new Date(end.getTime());
    if (this.start.compareTo(this.end) > 0)
        throw new IllegalArgumentException(this.start + " after " + this.end);
}
```

In summary, defensive copying is necessary for maintaining immutability and protecting the internal state of a class.

## Design Method Signatures Carefully

When designing method signatures, choose names carefully, following standard naming conventions. Avoid overloading methods excessively, and each method should "pull its weight." Long parameter lists, especially with identically typed parameters, should be shortened using various techniques.

Prefer interfaces over classes for parameter types, and use enums for parameters where appropriate. Consider the Builder pattern or helper classes for methods with long parameter lists.

```java
public enum TemperatureScale { FAHRENHEIT, CELSIUS }
```

In summary, design method signatures thoughtfully, favoring clarity and simplicity, and avoid excessive overloading.

## Use Overloading Judiciously

Overloading methods can lead to confusion, especially when the choice of which overloading to invoke is made at compile time. Avoid overloading methods with the same number of parameters, especially when the same set of parameters can be passed to different overloadings with the addition of casts.

A safe policy is to avoid exporting two overloadings with the same number of parameters. If in doubt, use different method names instead of overloading.

## Use Varargs Judiciously

Varargs methods are valuable for defining methods with a variable number of arguments. They are especially useful in methods like `printf` and reflection.

```java
static int sum(int... args) {
    int sum = 0;
    for (int arg : args)
        sum += arg;
    return sum;
}
```

In summary, use varargs judiciously, especially when defining methods with a variable number of arguments.

## Return Empty Collections Or Arrays, Not Nulls

Instead of returning null, prefer to return empty collections or arrays. Returning null introduces the risk of null pointer exceptions and can complicate client code with additional null checks.

In summary, never return null in place of an empty array or collection; it is better to return an empty container.

## Return Optionals Judiciously

The `Optional<T>` type introduced in Java 8 provides a way to represent optional values and is useful for methods that may not be able to return a result. Use `Optional<T>` as a return type when a method might not return a value, and clients need to consider this possibility.

```java
String lastWordInLexicon = max(words).orElse("No words...");
```

Return an optional that contains a boxed primitive type only when necessary, as it incurs additional boxing costs. Never use optionals as map values, and rarely store optionals in instance fields.

In summary, use optionals judiciously, primarily for methods that may not be able to return a value.

## Write Doc Comments For All Exposed API Elements

Proper documentation is essential for making your API usable. Precede every exported class, interface, constructor, method, and field declaration with a doc comment. Ensure doc comments are readable in both the source code and the generated documentation.

Document the contract between a method and its client, and avoid duplicate summary descriptions for members or constructors in a class. For generics, enums, and annotations, document type parameters, constants, and members, respectively.

In summary, documentation comments are crucial for API usability, and adopting a consistent style is imperative for clarity and understanding. Always read the generated documentation for your API.

# GENERAL PROGRAMMING

## Minimize The Scope Of Local Variables

Minimizing the scope of local variables enhances code readability, maintainability, and reduces the likelihood of errors. Declare variables where they are first used and provide initializers to nearly every local variable declaration.

If a variable is initialized to an expression that can throw a checked exception, it must be initialized inside a try block. If the value needs to be used outside the try block, declare it before the try block, but it cannot yet be "sensibly initialized."

Utilize the for loop, both in its traditional and for-each forms, to limit the scope of loop variables to the exact region where they're needed. Prefer for loops over while loops and keep methods small and focused to further minimize variable scope.

## Prefer For-Each Loops To Traditional For Loops

For-each loops provide advantages in terms of clarity, flexibility, and bug prevention without any performance penalty. However, there are situations where for-each loops are not suitable, such as destructive filtering, transforming, and parallel iteration.

In summary, for-each loops are preferable in most cases, offering compelling advantages over traditional for loops.

## Know And Use Libraries

Utilizing standard libraries offers several advantages, including leveraging the expertise of library authors, avoiding ad hoc solutions, performance improvements over time, gaining functionality, and placing code in the mainstream.

Every programmer should be familiar with the basics of `java.lang`, `java.util`, and `java.io` and their subpackages. Keep abreast of library additions with every major release.

To summarize, avoid reinventing solutions, use standard libraries, and stay informed about library updates.

## Avoid Float And Double If Exact Answers Are Required

Float and double types are designed for scientific and engineering calculations and are ill-suited for monetary calculations. For precise calculations, use `BigDecimal`, `int`, or `long`.

In summary, avoid using float or double for calculations that require an exact answer and opt for `BigDecimal` when precision is essential.

## Prefer Primitive Types To Boxed Primitives

Primitives are simpler, more time-efficient, and space-efficient than boxed primitives. Beware of pitfalls when using boxed primitives, such as identity distinction, the presence of a nonfunctional value (`null`), and performance issues.

Use boxed primitives as elements, keys, and values in collections or when required as type parameters in parameterized types and methods.

In summary, prefer primitive types for simplicity and efficiency, and be cautious when using boxed primitives.

## Avoid Strings Where Other Types Are More Appropriate

Strings are poor substitutes for other value types, such as enum types, aggregate types, or capabilities. Use appropriate value types when available, and avoid representing objects as strings when better data types exist.

To summarize, choose the most suitable data type rather than resorting to strings for representing objects.

## Beware The Performance Of String Concatenation

String concatenation using the `+` operator can lead to quadratic time complexity. Use `StringBuilder` for efficient string concatenation, especially when combining multiple strings in a loop.

In summary, be cautious with string concatenation and prefer `StringBuilder` for better performance.

## Refer To Objects By Their Interfaces

Prefer using interfaces as types for parameters, return values, variables, and fields when appropriate interface types exist. This enhances flexibility, allowing easy substitution of implementations.

Only refer to an object's class when creating it with a constructor. If no appropriate interface exists, use the last specific class in the hierarchy providing the required functionality.

In summary, use interfaces as types for flexibility and adaptability.

## Prefer Interfaces To Reflection

Reflection provides powerful access to class members but comes with drawbacks, including loss of compile-time type checking, verbose code, and performance issues. Limit reflective access and create instances reflectively while accessing them normally via interfaces or superclasses.

Reflection is useful in managing dependencies on classes, methods, or fields that may be absent at runtime, especially when dealing with multiple versions of packages.

In summary, use reflection judiciously for specific system programming tasks and be aware of its disadvantages.

## Use Native Methods Judiciously

The Java Native Interface (JNI) allows calling native methods written in languages like C or C++. However, using native methods for improved performance is rarely advisable. If necessary, use as little native code as possible and thoroughly test it.

In summary, think twice before using native methods, and if used, keep native code minimal and well-tested.

## Optimize Judiciously

Optimizing prematurely can harm software development, resulting in code that is neither fast nor correct. Focus on writing good programs, consider the performance consequences of design decisions, and measure performance before and after optimizations.

Strive to avoid design decisions that limit performance, such as making public types mutable or using inheritance inappropriately. Do not warp an API for performance; instead, measure the performance impact of design decisions.

In summary, prioritize writing good programs over prematurely optimizing, and always measure performance.

## Adhere To Generally Accepted Naming Conventions

Internalize standard naming conventions to enhance code readability and consistency. Follow typographical and grammatical conventions to create code that is straightforward and adheres to established practices.

To summarize, adopt generally accepted naming conventions, and use them consistently to improve code clarity and maintainability.

# EXCEPTION

## Use Exceptions Only For Exceptional Conditions

Exceptions are, as their name implies, to be used only for exceptional conditions; they should never be used for ordinary control flow.

A well-designed API must not force its clients to use exceptions for ordinary control flow.

## Use Checked Exceptions For Recoverable Conditions And Runtime Exceptions For Programming Errors

Use checked exceptions for conditions from which the caller can reasonably be expected to recover. By throwing a checked exception, you force the caller to handle the exception in a catch or to propagate it outward.

The user can disregard the mandate by catching the exception and ignoring it, but this is usually a bad idea. If a program throws an unchecked exception or an error, it is generally the case that recovery is impossible, and continued execution would do more harm than good. If a program does not catch such a throwable, it will cause the current thread to halt with an appropriate error message.

Use runtime exceptions to indicate programming errors. The great majority of runtime exceptions indicate "precondition violations."

All of the unchecked throwables you implement should subclass `RuntimeException`.

To summarize, throw checked exceptions for recoverable conditions and unchecked exceptions for programming errors. When in doubt, throw unchecked exceptions.

## Avoid Unnecessary Use Of Checked Exceptions

Unlike return codes and unchecked exceptions, they force programmers to deal with problems, enhancing reliability.

The easiest way to eliminate a checked exception is to return an `Optional` of the desired result type. Instead of throwing a checked exception, the method simply returns an empty optional.

In summary, when used sparingly, checked exceptions can increase the reliability of programs; when overused, they make APIs painful to use.

## Favor The Use Of Standard Exceptions

An attribute that distinguishes expert programmers from less experienced ones is that experts strive for and usually achieve a high degree of code reuse.

Reusing standard exceptions has several benefits. It makes your API easier to learn and use because it matches the established conventions that programmers are already familiar with. A second benefit is that programs using your API are easier to read because they aren't cluttered with unfamiliar exceptions. Last (and least), fewer exception classes mean a smaller memory footprint and less time spent loading classes.

Do not reuse `Exception`, `RuntimeException`, `Throwable`, or `Error` directly.

Throw `IllegalStateException` if no argument values would have worked; otherwise, throw `IllegalArgumentException`.

## Throw Exceptions Appropriate To The Abstraction

Higher layers should catch lower-level exceptions and, in their place, throw exceptions that can be explained in terms of the higher-level abstraction.

A special form of exception translation called exception chaining is called for in cases where the lower-level exception might be helpful to someone debugging the problem that caused the higher-level exception.

While exception translation is superior to mindless propagation of exceptions from lower layers, it should not be overused.

In summary, if it isn’t feasible to prevent or to handle exceptions from lower layers, use exception translation, unless the lower-level method happens to guarantee that all of its exceptions are appropriate to the higher level. Chaining provides the best of both worlds: it allows you to throw an appropriate higher-level exception while capturing the underlying cause for failure analysis.

## Document All Exceptions Thrown By Each Method

Always declare checked exceptions individually and document precisely the conditions under which each one is thrown.

Use the Javadoc `@throws` tag to document each exception that a method can throw, but do not use the `throws` keyword on unchecked exceptions. It is important that programmers using your API are aware of which exceptions are checked and which are unchecked because the programmers’ responsibilities differ in these two cases.

If an exception is thrown by many methods in a class for the same reason, you can document the exception in the class’s documentation comment.

In summary, document every exception that can be thrown by each method that you write. This documentation should take the form of `@throws` tags in doc comments. If you fail to document the exceptions that your methods can throw, it will be difficult or impossible for others to make effective use of your classes and interfaces.

## Include Failure-Capture Information In Detail Messages

It is critically important that the exception’s `toString` method return as much information as possible concerning the cause of the failure. In other words, the detail message of an exception should capture the failure for subsequent analysis.

To capture a failure, the detail message of an exception should contain the values of all parameters and fields that contributed to the exception.

Because stack traces may be seen by many people in the process of diagnosing and fixing software issues, do not include passwords, encryption keys, and the like in detail messages.

The detail message of an exception should not be confused with a user-level error message, which must be intelligible to end users. The detail message is primarily for the benefit of programmers or site reliability engineers when analyzing a failure. Therefore, information content is far more important than readability. User-level error messages are often localized, whereas exception detail messages rarely are.

One way to ensure that exceptions contain adequate failure-capture information in their detail messages is to require this information in their constructors instead of a string detail message.

## Strive For Atomicity

Generally speaking, a failed method invocation should leave the object in the state that it was in prior to the invocation (failure atomic).

There are several ways to achieve this effect:

- The simplest is to design immutable objects.
- For methods that operate on mutable objects, the most common way to achieve failure atomicity is to check parameters for validity before performing the operation.

```java
public Object pop() {
    if (size == 0)
        throw new EmptyStackException();
    Object result = elements[--size];
    elements[size] = null; // Eliminate obsolete reference
    return result;
}
```

- A last and far less common approach to achieving failure atomicity is to write recovery code that intercepts a failure that occurs in the midst of an operation and causes the object to roll back its state to the point before the operation began.

In summary, as a rule, any generated exception that is part of a method’s specification should leave the object in the same state it was in prior to the method invocation.

## Don't Ignore Exceptions

```java
// Empty catch block ignores exception - Highly suspect!
try {
    // ...
} catch (SomeException e) {
}
```

An empty catch block defeats the purpose of exceptions.

If you choose to ignore an exception, the catch block should contain a comment explaining why it is appropriate to do so, and the variable should be named `ignored`.

# CONCURRENCY

## Threads allow multiple activities to proceed concurrently

### Synchronize Access To Shared Mutable Data

The `synchronized` keyword ensures that only a single thread can execute a method or block at one time. An object is created in a consistent state and locked by the methods that access it.

These methods observe the state and optionally cause a state transition, transforming the object from one consistent state to another.

Not only does synchronization ensure that each thread entering a synchronized method or block sees the effects of all previous modifications that were guarded by the same lock. Reading or writing a variable is atomic unless the variable is of type long or double.

Synchronization is required for reliable communication between threads as well as for mutual exclusion.

Do not use `Thread.stop`. A recommended way to stop one thread from another is to have the first thread poll a boolean field that is initially false but can be set to true by the second thread to indicate that the first thread is to stop itself.

Synchronization is not guaranteed to work unless both read and write operations are synchronized.

The best way to avoid the problems is not to share mutable data. Confine mutable data to a single thread. It is acceptable for one thread to modify a data object for a while and then to share it with other threads, synchronizing only the act of sharing the object reference.

"Effectively mutable": an object or variable that is technically immutable but can still appear to be mutable in certain contexts. For example, consider a String object in Java. Once created, a String object cannot be changed. However, you can create a new String object by concatenating two existing String objects.

In summary, when multiple threads share mutable data, each thread that reads or writes the data must perform synchronization.

### Avoid Excessive Synchronization

To avoid liveness and safety failures, never cede control to the client within a synchronized method or block. Inside a synchronized region, do not invoke a method that is designed to be overridden or one provided by a client in the form of a function object.

As a rule, you should do as little work as possible inside synchronized regions.

In summary, to avoid deadlock and data corruption, never call an alien method from within a synchronized region. More generally, keep the amount of work within synchronized regions to a minimum. In the multicore era, it is more important than ever not to oversynchronize. Synchronize your class internally only if there is a good reason to do so, and document your decision clearly.

### Prefer Executors, Tasks, And Streams To Threads

`java.util.concurrent` contains an Executor Framework, flexible interface-based task execution facility.

```java
ExecutorService exec = Executors.newSingleThreadExecutor();

exec.execute(runnable);

exec.shutdown();
```

If you want more than one thread to process requests from the queue, simply call a different static factory that creates a different kind of executor service called a "thread pool." Can be used the `ThreadPoolExecutor` class directly.

For a small program or a lightly loaded server, `Executors.newCachedThreadPool` is generally a good choice because it demands no configuration and generally does the right thing.

In a heavily loaded production server, you are much better off using `Executors.newFixedThreadPool`, which gives you a pool with a fixed number of threads or using the `ThreadPoolExecutor` class directly.

The key abstraction is the unit of work which is the "task." There are two kinds of tasks: `Runnable` and `Callable`.

## Prefer Concurrency Utilities To Wait And Notify

Given the difficulty of using `wait` and `notify` correctly, you should use the higher-level concurrency utilities instead.

The higher-level utilities in `java.util.concurrent` fall into 3 categories:

1. "Executor Framework"
2. "Concurrent Collections"
3. "Synchronizers"

The concurrent collections are high-performance concurrent implementations of standard collection interfaces such as `List`, `Queue`, and `Map`.

It is impossible to exclude concurrent activity from a concurrent collection; locking it will only slow the program.

Use `ConcurrentHashMap` in preference to `Collections.synchronizedMap`.

For interval timing, always use `System.nanoTime` rather than `System.currentTimeMillis`.

The standard idiom for using the `wait` method:

```java
synchronized(obj) {
    while (<condition does not hold>)
        obj.wait(); // Releases lock and reacquires on wakeup
}
```

Always use the wait loop idiom to invoke the `wait` method; never invoke it outside of a loop.

There are several reasons a thread might wake up when the condition does not hold:

1. Another thread could have obtained the lock and changed the guarded state between the time a thread invoked `notify` and the waiting thread woke up.
2. Another thread could have invoked `notify` accidentally or maliciously when the condition did not hold.
3. The notifying thread could be overly "generous" in waking waiting threads.
4. The waiting thread could (rarely) wake up in the absence of a `notify`.

"It is sometimes said that you should always use `notifyAll()`". You may wake some other threads, too, but this won't affect the correctness of your program. These threads will check the condition for which they are waiting and, finding it false, will continue waiting.

There is seldom, if ever, a reason to use `wait` and `notify`.

If you maintain code that uses `wait` and `notify`, make sure that it always invokes `wait` from within a while loop using the standard idiom. The `notifyAll` method should generally be used in preference to `notify`.

## Document Thread Safety

The presence of the `synchronized` modifier in a method declaration is an implementation detail, not a part of its API.

To enable safe concurrent use, a class must clearly document what level of thread safety it supports. The following list summarizes levels of thread safety:

1. "Immutable": Instances of this class appear constant.
2. "Unconditionally Thread-Safe": Instances of this class are mutable, but the class has sufficient internal synchronization that its instances can be used concurrently without the need for any external synchronization.
3. "Conditionally Thread-Safe": Like Unconditionally Thread-Safe, except that some methods require external synchronization that its instances can be used concurrently without the need for any external synchronization.
4. "Not Thread-Safe": Instances of this class are mutable. To use them concurrently, clients must surround each method invocation with external synchronization of the client's choosing.
5. "Thread-Hostile": Unsafe for concurrent use even if every method invocation is surrounded by external synchronization. Usually results from modifying static data without synchronization.

These categories correspond roughly to the thread safety annotations in "Java Concurrency in Practice," which are Immutable, ThreadSafe, and NotThreadSafe.

The "Private lock object idiom" thwarts a denial-of-service attack:

```java
private final Object lock = new Object();

public void foo() {
    synchronized(lock) {
        // ...
    }
}
```

Because the private lock object is inaccessible outside the class, it is impossible for clients to interfere with the object’s synchronization. The `lock` field is declared final. This prevents you from inadvertently changing its contents, which could result in catastrophic unsynchronized access.

Lock fields should always be declared final.

The private lock object idiom can be used only on unconditionally thread-safe classes. Conditionally thread-safe classes can’t use this idiom because they must document which lock their clients are to acquire when performing certain method invocation sequences.

The private lock object idiom is particularly well-suited to classes designed for inheritance.

To summarize, every class should clearly document its thread safety properties with a carefully worded prose description or a thread safety annotation. If you write an unconditionally thread-safe class, consider using a private lock object in place of synchronized methods.

## Use Lazy Initialization Judiciously

Lazy initialization is the act of delaying the initialization of a field until its value is needed.

As is the case for most optimizations, the best advice for lazy initialization is "don’t do it unless you need to."

If a field is accessed only on a fraction of the instances of a class and it is costly to initialize the field, then lazy initialization may be worthwhile.

Under most circumstances, normal initialization is preferable to lazy initialization.

If you use lazy initialization to break an initialization circularity, use a synchronized accessor.

If you need to use lazy initialization for performance on a static field, use the lazy initialization holder class idiom.

If you need to use lazy initialization for performance on an instance field, use the double-check idiom.

All of the initialization techniques discussed in this item apply to primitive fields as well as object reference fields.

In summary, you should initialize most fields normally, not lazily.

## Don’t Depend On The Thread Scheduler

Any program that relies on the thread scheduler for correctness or performance is likely to be nonportable.

The best way to write a robust, responsive, portable program is to ensure that the average number of runnable threads is not significantly greater than the number of processors.

The main technique for keeping the number of runnable threads low is to have each thread do some useful work and then wait for more.

Threads should not run if they aren’t doing useful work.

Resist the temptation to “fix” the program by putting in calls to `Thread.yield`.

`Thread.yield` has no testable semantics.

Thread priorities are among the least portable features of Java.

# SERIALIZATION

## Prefer Alternatives To Java Serialization

A fundamental problem with serialization is that its attack surface is too big to protect and constantly growing. The attack surface includes classes in the Java platform libraries, in third-party libraries, and the application itself.

The serializable types in the Java libraries and in commonly used third-party libraries are examined for methods invoked during deserialization that perform potentially dangerous activities, known as "gadgets."

The best way to avoid serialization exploits is never to deserialize anything. There is no reason to use Java serialization in any new system you write.

The leading cross-platform structured data representations are "JSON" and "Protocol Buffers." The most significant differences between JSON and protobuf are that JSON is text-based and human-readable, whereas protobuf is binary and substantially more efficient. JSON is exclusively a data representation, whereas protobuf offers schemas(types) to document and enforce appropriate usage.

Never deserialize untrusted data. Prefer whitelisting to blacklisting.

In summary, serialization is dangerous and should be avoided. If you are designing a system from scratch, use a cross-platform structured data representation.

## Implement Serializable With Great Caution

A major cost of implementing Serializable is that it decreases the flexibility to change a class's implementation once it has been released. It also increases the likelihood of bugs and security holes, as well as the testing burden associated with releasing a new version of a class.

Implementing Serializable is not a decision to be undertaken lightly. Classes designed for inheritance should rarely implement Serializable, and interfaces should rarely extend it. Inner classes should not implement Serializable.

## Consider Using A Custom Serialized Form

Do not accept the default serialized form without first considering whether it is appropriate. The default serialized form is likely to be appropriate if an object's physical representation is identical to its logical content.

Even if you decide that the default serialized form is appropriate, you often must provide a `readObject` method to ensure invariants and security.

Using the default serialized form when an object's physical representation differs substantially from its logical data content has four disadvantages:

1. It permanently ties the exported API to the current internal representation.
2. It can consume excessive space.
3. It can consume excessive time.
4. It can cause stack overflows.

Before deciding to make a field nontransient, convince yourself that its value is part of the logical state of the object. You must impose any synchronization on object serialization that you would impose on any other method that reads the entire state of the object.

Regardless of what serialized form you choose, declare an explicit serial version UID in every serializable class you write.

```java
private static final long serialVersionUID = randomLongValue;
```



Do not change the serial version UID unless you want to break compatibility with all existing serialized instances of a class.

To summarize, if you have decided that a class should be serializable, think hard about what the serialized form should be.

## Write ReadObject Methods Defensively

The `readObject` method is effectively another public constructor, demanding all the same care as any other constructor. Just as a constructor must check its arguments for validity, the `readObject` method must perform validity checking.

When an object is deserialized, it is critical to defensively copy any field containing an object reference that a client must not possess.

Defensive copying is not possible for final fields.

To summarize, anytime you write a `readObject` method, adopt the mindset that you are writing a public constructor that must produce a valid instance regardless of what byte stream it is given. Here are the guidelines for writing a `readObject` method:

- For classes with object reference fields that must remain private, defensively copy each object in such a field. Mutable components of immutable classes fall into this category.
- Check any invariants and throw an `InvalidObjectException` if a check fails. The checks should follow any defensive copying.
- If an entire object graph must be validated after it is deserialized, use the `ObjectInputValidation` interface (not discussed in this book).
- Do not invoke any overridable methods in the class, directly or indirectly.

## For Instance Control, Prefer Enum Types To ReadResolve

If you depend on `readResolve` for instance control, all instance fields with object reference types must be declared transient.

If a singleton contains a nontransient object reference field, the contents of this field will be deserialized before the singleton’s `readResolve` method is run.

```java
// Enum singleton - the preferred approach
public enum Elvis {
    INSTANCE;
    private String[] favoriteSongs = { "Hound Dog", "Heartbreak Hotel" };
    public void printFavorites() {
        System.out.println(Arrays.toString(favoriteSongs));
    }
}
```

The accessibility of `readResolve` is significant.

To summarize, use enum types to enforce instance control invariants wherever possible. If this is not possible and you need a class to be both serializable and instance-controlled, you must provide a `readResolve` method and ensure that all of the class’s instance fields are either primitive or transient.

## Consider Serialization Proxies Instead Of Serialized Instances

The serialization proxy pattern is reasonably straightforward. First, design a private static nested class that concisely represents the logical state of an instance of the enclosing class. This nested class is known as the serialization proxy of the enclosing class. It should have a single constructor, whose parameter type is the enclosing class.

This constructor merely copies the data from its argument:

```java
public class SerializationProxy implements Serializable {
    private final int value;

    SerializationProxy(MyClass myClass) {
        this.value = myClass.value;
    }
}
```

By design, the default serialized form of the serialization proxy is the perfect serialized form of the enclosing class. Both the enclosing class and its serialization proxy must be declared to implement Serializable.

In summary, consider the serialization proxy pattern whenever you find yourself having to write a `readObject` or `writeObject` method on a class that is not extendable by its clients.


