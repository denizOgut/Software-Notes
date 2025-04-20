
# Maven Module

A Maven module is a sub-project. The significant advantage of using this approach is that it helps reduce duplication in projects.

# Parent Pom

A Parent POM is used to define common configuration that can be inherited by one or more child POMs. The child POM inherits the configuration specified in the parent POM, including dependencies, build settings, and other configurations. Maven supports inheritance, and each `pom.xml` file has an implicit parent POM called the Super POM.

```xml
<packaging>pom</packaging>
```

The `<packaging>` element set to "pom" declares that the project will serve as a parent or an aggregator and won't produce further artifacts. It helps to reduce duplication and manage common configuration across multiple projects.

```xml
<relativePath>...</relativePath>
```

The `<relativePath>` element specifies the location of a parent POM relative to the current POM. It is used in conjunction with the `<parent>` element. This element is optional and is only needed if the parent POM is not located in the default location.

```xml
<skip>true</skip>
```

The `<skip>` element is a configuration element used to skip the execution of a particular build phase.

```xml
<exclude>
  <!-- specify artifacts to exclude from the dependency list -->
</exclude>
```

The `<exclude>` element is used to specify artifacts that should be excluded from the dependency list of a project.

## Properties

Properties in Maven define values that can be reused throughout a project. They can be used to specify information such as the version number of a library or the location of a resource. Developers can centralize the configuration of a project, making it easier to maintain.

```xml
<properties>
  <library.version>1.0.0</library.version>
</properties>

<dependencies>
  <dependency>
    <groupId>com.example</groupId>
    <artifactId>library</artifactId>
    <version>${library.version}</version>
  </dependency>
</dependencies>
```

## Profile

A profile in Maven is a set of configuration settings used to customize the build process for a specific environment or situation. Profiles can be activated by specifying their ID or a condition in the command line, in the POM file, or in a settings file

```xml
<profiles>
  <profile>
    <id>profileId</id>
    <activation>
      <activeByDefault>true</activeByDefault>
    </activation>
    <!-- Configuration specific to the profile -->
  </profile>
</profiles>
```

## Dependency Management

The `<dependencyManagement>` section is used to manage the versions of dependencies used in a project. It allows for centralized version management, dependency version control, simplified dependency declaration, and inheritance.

1. **Centralized version management**: Consolidate and centralize the management of dependency versions without adding dependencies inherited by all children.
2. **Dependency version control**: Control versions of dependencies centrally.
3. **Simplified dependency declaration**: Simplify dependency declarations in child modules.
4. **Dependency inheritance**: Inherit dependencies from the parent POM.

```xml
<dependencyManagement>
  <!-- Dependency versions are defined here -->
</dependencyManagement>
```

These features make dependency management more organized and efficient across multiple modules.

# VAR

`var` is a contextual keyword used in programming languages, particularly in the context of type inference.

- **Initialization Requirement:**
  In the case of `var` variables, initialization is mandatory. The variable type is determined by the compiler based on the type of the initial value (type inference/deduction).

- **Type Inference:**
  The type of `var` variables is determined by the compiler at compile-time based on the type of the initial value. Once assigned, the type of `var` variables remains constant during runtime.

- **Limitations:**
  - `var` variables cannot be used for method parameter variables.
  - `var` variables cannot be used for class data members.

Note: The use of `var` enhances code readability and reduces redundancy by allowing the compiler to infer the variable type based on the assigned initial value.

Example Usage:

```java
// Example in Java
var myVariable = 42; // Compiler infers the type of myVariable as int
```


# VARARGS

Varargs, kısaltma olarak kullanılan bir terimdir ve "Variable-Length Argument Lists" anlamına gelir. Bu, değişken sayıda argüman alan metotları ifade eder ve genellikle "..." (ellipsis) sembolü ile gösterilir.

- **Varargs Metotları:**
  Varargs parametresi, bir metot için bir dizi referansıdır. Bu parametre, çağrılan metoda hem dizi referansı hem de aynı türden değişken sayıda argüman geçmek için kullanılabilir.

- **Argüman Sayısı Esnekliği:**
  Varargs parametresine hiç argüman geçilmeyebilir. Bu durumda, boş bir dizi (uzunluğu sıfır olan dizi) argüman olarak geçilmiş olur.

- **Sıralama Kuralları:**
  Varargs parametresi, metodun son parametresi olmak zorundadır. Bu kural gereği bir metodun birden fazla varargs parametresine sahip olması mümkün değildir.

- **İmza Açısından Benzerlik:**
  T bir tür olmak üzere, `T...` ve `T[]` parametreleri imza açısından aynıdır.

Örnek Kullanım:

```java
public void printNumbers(String... numbers) {
    for (String number : numbers) {
        System.out.println(number);
    }
}

// Kullanım
printNumbers("One", "Two", "Three");
printNumbers(); // Hiç argüman geçilmez, boş dizi olarak işlenir.
```

Varargs, değişken sayıda argüman almak istediğiniz durumlarda kodunuzu daha esnek hale getirmenizi sağlar.

# RECURSION

In the software world, typical scenarios where recursive algorithms are encountered include:

- Traversal algorithms for directory trees
- Exploration of data structures like trees and graphs and searching within them
- Parsing algorithms
- Solving specific problems (e.g., the 8-queens problem in chess)
- Mathematical algorithms
- Certain sorting algorithms (e.g., quicksort, mergesort, heapsort)
- Optimization problems

Algorithmic problems can be categorized in terms of recursion into three groups:

1. **Algorithms Realizable Both Recursively and Iteratively:**
   These algorithms can be implemented both with recursion and without recursion (iteratively).

2. **Algorithms Realizable Only Recursively:**
   Some algorithms are naturally suited for recursive implementations and may be challenging or inefficient to implement iteratively.

3. **Algorithms Realizable Only Iteratively:**
   There are cases where recursion might not be the most suitable or practical method for implementation.

It's crucial to note that excessive recursion can lead to a "stack overflow" since method parameters and local variables are created in the stack, and too many recursive calls can exhaust the available stack space. "Stack overflow" refers to the situation where the stack runs out of space for storing information related to method calls.

**Key Notes:**
- Iterative solutions, which do not involve recursion, are referred to as "iterative solutions."
- Recursion is a complex and sometimes challenging technique, and programmers should avoid it unless necessary.
- When a method is called, not only local variables and parameter variables are stored in the stack but also additional information, depending on the system (e.g., special registers), may be stored in the stack.

Recursion is a powerful tool, but it should be used judiciously, considering both complexity and ease of debugging.

# BITWISE
## Bitwise Operators in Java

Java provides a set of bitwise operators for manipulating the bits of integer values:

#### Bitwise Operators:

- `~`: Bitwise NOT
- `<<`, `>>`, `>>>`: Bitwise left shift, right shift, unsigned right shift
- `&`: Bitwise AND
- `^`: Bitwise XOR
- `|`: Bitwise OR
- `>>=`, `<<=`, `>>>=`, `&=`, `|=`, `^=`: Bitwise compound assignment operators

These operators are arranged based on their precedence. They cannot be used with real number types and, with a few exceptions, cannot be used with the boolean type.

## Bitwise NOT (`~`)

The `~` operator performs a bitwise complement operation on the bits of the integer value. For example:

```java
var a = Console.readUInt("Enter a number:");
var b = ~a;

BitwiseUtil.writeBits(a);
BitwiseUtil.writeBits(b);
```
### Bitwise Left Shift (`<<`)

The `<<` operator shifts the bits of the first operand (integer) to the left by the number specified by the second operand. For example:

```java
var a = 0x00000001;
while (a != 0) {
    BitwiseUtil.writeBits(a);
    a <<= 1;
}
```

This code demonstrates left-shifting the bits of `a` and printing the result until all bits become zero.

### Bitwise Right Shift (`>>`, `>>>`)

The `>>` operator shifts the bits of the first operand (integer) to the right by the number specified by the second operand. The `>>>` operator does the same but fills the leftmost bits with zero, regardless of the sign. For example:

```java
var a = Console.readInt("Enter a number:");
var n = Console.readUInt("How many positions to shift to the right?");
BitwiseUtil.writeBits(a);
BitwiseUtil.writeBits(a >> n);
BitwiseUtil.writeBits(a >>> n);
```

## Writing a 32-bit Number with Specific Bit Pattern

```java
BitwiseUtil.writeBits(~0);
BitwiseUtil.writeBits(~0 >>> 1);
BitwiseUtil.writeBits(~(~0 >>> 1));
```

|A|B|AND: A & B|OR: A \| B|XOR: A ^ B|
|---|---|---|---|---|
|T|T|1|1|0|
|T|F|0|1|1|
|F|T|0|1|1|
|F|F|0|0|0|

### BitwiseUtil

```java
package org.csystem.util.bitwise;

public final class BitwiseUtil {
    private BitwiseUtil()
    {}

    public static int clearBit(int a, int k) // -> [0, 31]
    {
        return a & ~(1 << k);
    }

    public static long clearBit(long a, int k) // -> [0, 63]
    {
        return a & ~(1L << k);
    }

    public static int highestSetBit(int a)
    {
        for (int i = Integer.SIZE - 1; i >= 0; --i)
            if (isSet(a, i))
                return i;

        return -1;
    }

    public static int lowestClearBit(byte a)
    {
        for (int i = 0; i < Byte.SIZE; ++i)
            if (isClear(a, i))
                return i;

        return -1;
    }

    public static int lowestClearBit(short a)
    {
        for (int i = 0; i < Short.SIZE; ++i)
            if (isClear(a, i))
                return i;

        return -1;
    }

    public static int lowestClearBit(int a)
    {
        for (int i = 0; i < Integer.SIZE; ++i)
            if (isClear(a, i))
                return i;

        return -1;
    }

    public static int lowestClearBit(long a)
    {
        for (int i = 0; i < Long.SIZE; ++i)
            if (isClear(a, i))
                return i;

        return -1;
    }

    public static int lowestClearBit(char a)
    {
        for (int i = 0; i < Character.SIZE; ++i)
            if (isClear(a, i))
                return i;

        return -1;
    }

    public static int lowestSetBit(byte a)
    {
        for (int i = 0; i < Byte.SIZE; ++i)
            if (isSet(a, i))
                return i;

        return -1;
    }

    public static int lowestSetBit(short a)
    {
        for (int i = 0; i < Short.SIZE; ++i)
            if (isSet(a, i))
                return i;

        return -1;
    }

    public static int lowestSetBit(int a)
    {
        for (int i = 0; i < Integer.SIZE; ++i)
            if (isSet(a, i))
                return i;

        return -1;
    }

    public static int lowestSetBit(long a)
    {
        for (int i = 0; i < Long.SIZE; ++i)
            if (isSet(a, i))
                return i;

        return -1;
    }

    public static int lowestSetBit(char a)
    {
        for (int i = 0; i < Character.SIZE; ++i)
            if (isSet(a, i))
                return i;

        return -1;
    }

    public static int [] indicesOfSetBits(int a)
    {
        var indices = new int[setBitsCount(a)];
        var idx = 0;

        for (int i = 0; i < Integer.SIZE; ++i)
            if (isSet(a, i))
                indices[idx++] = i;

        return indices;
    }

    public static int [] indicesOfSetBits(long a)
    {
        var indices = new int[setBitsCount(a)];
        var idx = 0;

        for (int i = 0; i < Long.SIZE; ++i)
            if (isSet(a, i))
                indices[idx++] = i;

        return indices;
    }

    public static boolean isClear(int a, int k)
    {
        return !isSet(a, k);
    }

    public static boolean isClear(long a, int k)
    {
        return !isSet(a, k);
    }

    public static boolean isPowerOfTwo(int a)
    {
        return a != 0 && (a & (a - 1)) == 0;
    }

    public static boolean isPowerOfTwo(long a)
    {
        return a != 0 && (a & (a - 1)) == 0;
    }

    public static boolean isSet(int a, int k)
    {
        return (a & 1 << k) != 0;
    }

    public static boolean isSet(long a, int k)
    {
        return (a & 1L << k) != 0;
    }

    public static int setBitsCount(int a)
    {
        var count = 0;

        for (int i = 0; i < Integer.SIZE; ++i)
            if (isSet(a, i))
                ++count;

        return count;
    }

    public static int setBitsCount(long a)
    {
        var count = 0;

        for (int i = 0; i < Long.SIZE; ++i)
            if (isSet(a, i))
                ++count;

        return count;
    }

    public static int setBit(int a, int k) // -> [0, 31]
    {
        return a | 1 << k;
    }

    public static long setBit(long a, int k) // -> [0, 63]
    {
        return a | 1L << k;
    }

    public static int toggleBit(int a, int k) // -> [0, 31]
    {
        return a ^ 1 << k;
    }

    public static long toggleBit(long a, int k) // -> [0, 31]
    {
        return a ^ 1L << k;
    }

    public static String toBitsStr(byte a)
    {
        var bits = new char[Byte.SIZE];

        for (int k = 7; k >= 0; --k)
            bits[7 - k] = (a & 1 << k) != 0 ? '1' : '0';

        return String.valueOf(bits);
    }

    public static String toBitsStr(short a)
    {
        var bits = new char[Short.SIZE];

        for (int k = 15; k >= 0; --k)
            bits[15 - k] = (a & 1 << k) != 0 ? '1' : '0';

        return String.valueOf(bits);
    }

    public static String toBitsStr(int a)
    {
        var bits = new char[Integer.SIZE];

        for (int k = 31; k >= 0; --k)
            bits[31 - k] = isSet(a, k) ? '1' : '0';

        return String.valueOf(bits);
    }

    public static String toBitsStr(long a)
    {
        var bits = new char[Long.SIZE];

        for (int k = 63; k >= 0; --k)
            bits[63 - k] = isSet(a, k) ? '1' : '0';

        return String.valueOf(bits);
    }

    public static String toBitsStr(char c)
    {
        var bits = new char[Character.SIZE];

        for (int k = 15; k >= 0; --k)
            bits[15 - k] = (c & 1 << k) != 0 ? '1' : '0';

        return String.valueOf(bits);
    }

    public static void writeBits(byte a)
    {
        System.out.println(toBitsStr(a));
    }

    public static void writeBits(short a)
    {
        System.out.println(toBitsStr(a));
    }

    public static void writeBits(int a)
    {
        System.out.println(toBitsStr(a));
    }

    public static void writeBits(long a)
    {
        System.out.println(toBitsStr(a));
    }

    public static void writeBits(char c)
    {
        System.out.println(toBitsStr(c));
    }
}
```

# LOCAL DATE-TIME

Java 8 ile birlikte gelen yeni nesil tarih ve zaman işlemleri sınıfları, tarih, zaman ve tarih-zamanı ayrı ayrı ele alır. Bu sınıfların çoğu "immutable" (değiştirilemez) özellik taşır ve genellikle türünden nesneler oluşturmak için `of` adlı factory metotlarına sahiptir.

LocalDate ve diğer Java 8 ile eklenen tarih-zaman sınıfları, geçerlilik kontrolü yapar ve geçersiz değerler için `DateTimeException` nesnesi fırlatır. Tarih ve zamanla ilgili ölçümler için `ChronoUnit` enum sınıfı kullanılabilir.

```java
// LocalDate örneği
LocalDate currentDate = LocalDate.now();

// Belirli bir tarih oluşturma
LocalDate specificDate = LocalDate.of(2022, 12, 31);

// Belirli bir tarih üzerine ölçüm eklemek
LocalDate futureDate = specificDate.plus(Period.ofDays(7));

// Tarih arasındaki farkı ölçmek
long daysBetween = ChronoUnit.DAYS.between(currentDate, futureDate);
System.out.println("Days between: " + daysBetween);

// Tarih formatlama
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");
String formattedDate = currentDate.format(formatter);
System.out.println("Formatted Date: " + formattedDate);

// Farklı bir tarih formatı
DateTimeFormatter customFormatter = DateTimeFormatter.ofPattern("E, MMM dd yyyy");
String customFormattedDate = currentDate.format(customFormatter);
System.out.println("Custom Formatted Date: " + customFormattedDate);
```

| Pattern                              | Example                                      |
| -------------------------------------| -------------------------------------------- |
| yyyy-MM-dd (ISO)                     | “2018-07-14”                                |
| dd-MMM-yyyy                           | “14-Jul-2018”                               |
| dd/MM/yyyy                            | “14/07/2018”                                |
| E, MMM dd yyyy                        | “Sat, Jul 14 2018”                          |
| h:mm a                                | “12:08 PM”                                  |
| EEEE, MMM dd, yyyy HH:mm:ss a         | “Saturday, Jul 14, 2018 14:31:06 PM”        |
| yyyy-MM-dd'T'HH:mm:ssZ               | “2018-07-14T14:31:30+0530”                 |
| hh 'o''clock' a, zzzz                 | “12 o’clock PM, Pacific Daylight Time”     |
| K:mm a, z                             | “0:08 PM, PDT”                              |


# BIG DECIMAL

`BigDecimal` sınıfı ondalık aritmetiği işlemek üzere tasarlanmış olup yuvarlama üzerinde hassas kontrol sağlar. Son derece büyük veya küçük ondalık sayılarla çalışmak için idealdir ve yuvarlamanın nasıl yapılacağı belirlenebilir.

Temel Özellikler:
- **Değişmezlik:** `BigDecimal` değişmez bir sınıftır, yani bir kez oluşturulduktan sonra değiştirilemez. Bu değişmezlik, iş paralelliği ve öngörülebilir davranışı sağlar.

- **Yuvarlama Kontrolü:** `BigDecimal`, yuvarlama işlemleri konusunda esneklik sağlar. Yuvarlama modunu, hassasiyeti belirleyebilir ve hatta hiç yuvarlama yapmamayı seçebilirsiniz.

- **Kullanım Senaryoları:** `BigDecimal`, yuvarlama hatalarını ortadan kaldırmasının yanı sıra performans maliyeti de beraberinde getirir. Genellikle finansal ve parasal hesaplamalar gibi hassasiyetin kritik olduğu uygulamalarda tercih edilir.

Düşünülmesi Gerekenler:
- **Performans Etkisi:** `BigDecimal`'ı aşırı kullanmak, işlemleri gerçekleştirmek için gereken makine komutlarının çokluğu nedeniyle performansı olumsuz etkileyebilir. Bu nedenle, sunduğu hassasiyetin belirli bir kullanım durumu için gerekli olup olmadığını değerlendirmek önemlidir.

- **Alternatifler:** Hassasiyetin yüksek derecede kritik olmadığı uygulamalarda, `double` veya `float` gibi ilkel tipler daha performanslı ve yeterli olabilir.

Örnek Kullanım:
```java
import java.math.BigDecimal;
import java.math.RoundingMode;

public class BigDecimalOrnek {
    public static void main(String[] args) {
        BigDecimal bigDecimal1 = new BigDecimal("123.456");
        BigDecimal bigDecimal2 = new BigDecimal("789.012");

        // Toplama
        BigDecimal toplam = bigDecimal1.add(bigDecimal2);

        // 2 ondalık basamağa yuvarlama
        BigDecimal yuvarlanmisToplam = toplam.setScale(2, RoundingMode.HALF_UP);

        System.out.println("Toplam: " + toplam);
        System.out.println("Yuvarlanmış Toplam: " + yuvarlanmisToplam);
    }
}
```

**Önemli:** `BigDecimal`, hassasiyet sağlasa da kullanımı dikkatlice düşünülmelidir. İlkel tipler yerine tercih edilmeden önce hassasiyet ihtiyaçları ile performans etkisi arasındaki denge değerlendirilmelidir.

# ASSERT

```JAVA
// Örnek assert kullanımı
public class AssertExample {
    public static void main(String[] args) {
        int age = 17;

        // Yaş 18'den küçükse AssertionError fırlatılır
        assert age >= 18 : "Yaş 18'den küçük";

        System.out.println("Bu satır assert başarılı olduğunda çalışır");
    }
}
```

```java
// Akışın hiçbir zaman bu noktaya gelmeyeceğini derleyici anlar
final boolean alwaysFalse = false;
if (alwaysFalse) {
    // Bu kod asla çalıştırılmaz
    System.out.println("Bu kod asla çalışmaz");
}
```

`alwaysFalse` değişkeni final ve false olduğu için, derleyici bu if deyimini ara koda eklemez ve bu kod ürün aşamasında çalıştırılmaz. Bu tür durumlar, `assert` ifadelerinin ürün aşamasında koddan çıkartılması için kullanılabilir.

# CLASS

Java'da sınıf bildirimleri, farklı tiplerde sınıfları içerebilir. İşte bu tür sınıf bildirimleri ve kullanım amaçları:

### 1. Static Sınıflar (Nested Classes)

Bir sınıf içerisinde başka bir sınıf static olarak bildirilebilir. İçteki sınıf dıştaki sınıfın bir elemanıdır (member). İçteki sınıfın erişim belirleyicileri kullanılabilir.

```java
class A {
    static class B {
        // ...
    }
}

// Erişim: A.B
```

Static sınıflar, parçası oldukları sınıfın sadece static üyelerine, private tanımlansalar bile, ulaşabilirler.

### 2. Non-Static Sınıflar (Inner Classes)

Inner class türünden bir nesne, kapsayan sınıf türünden bir nesne kullanılarak yaratılabilir. Inner class içerisinde, kapsayan sınıfın elemanlarına doğrudan erişilebilir, hatta `private` olsa bile.

```java
class A {
    class B {
        // ...
    }
}

// Yaratma: A a = new A(); A.B b = a.new B();
```

### 3. Yerel Sınıflar (Local Classes)

Yerel sınıflar, bir metot içerisinde bildirilen sınıflardır. Kapsamları içinde bulundukları blok ile sınırlıdır. Farklı faaliyet alanları içinde aynı isimde yerel sınıf bildirimi geçerlidir.

### 4. Anonim Sınıflar (Anonymous Classes)

Anonim sınıf bildiriminin genel biçimi:

```java
new <tür>([argümanlar]) {
    <bildirimler>
}
```

Anonim sınıflar, bir türetme işlemidir ve kullanılacak sınıfın türetmeye kapalı olmaması, yani final olarak bildirilmemiş olması gerekir. Anonim sınıflar sıklıkla olayları yakalamada ve arayüzleri gerçekleştirmede kullanılırlar.

```java
Sample s1 = new Sample() {
    //...
};

Sample s2 = new Sample() {
    //...
};
```
İsimsiz sınıflar içinde bulundukları bloğun yerel değişkenlerine final ya da değeri değişmediği ****effectively final** hallerde ulaşabilirler.

Bu farklı sınıf türleri, kodunuzu daha modüler hale getirmek, sarmalamayı artırmak ve okunabilirliği kolaylaştırmak için kullanılır.

# CALLBACK

Callback, bir metotun içinde çağrılacak olan başka bir metodu belirlemek için kullanılan bir kavramdır. Yani, bir metotun ne yapacağını bilmediği, sadece hangi metodu çağırmak istediği durumları ifade eder.

#### Effectively Final

`Effectively final`, bir değişkenin sadece bir kez atanmış ve bir daha değiştirilmemiş olma durumunu ifade eder. Bu durum genellikle lambda ifadeleri ve anonim sınıflar içinde kullanılır.

#### Anonim Sınıflar ve Callback Örneği

Aşağıdaki örnekte, bir anonim sınıf kullanılarak bir nesneye ilk değer verilmiştir. Bu sentaks, nesneye ilk değer verme sentaksı değildir; bunun yerine anonim sınıf içinde non-static initializer kullanılmıştır. Dikkat edilirse, `p` referansının dinamik türü `Product` değil, `Product` sınıfından türetilmiş bir anonim sınıf türündedir.

```java
Product p = new Product() {
    {
        setName("laptop");
        setStock(100);
        setCost(BigDecimal.valueOf(7000));
        setUnitPrice(BigDecimal.valueOf(10000));
        setExpiryDate(null);
    }
};
```

#### Fonksiyonel Arayüzler (Functional Interfaces)

Bir arayüzün "bir ve yalnız bir tane" abstract metodu varsa, bu arayüze "fonksiyonel arayüz" denir. Java 8 ile birlikte eklenen lambda ifadeleri ve fonksiyonel arayüzler, callback işlevselliğini destekler. Fonksiyonel arayüzlerdeki tek metot, anonim sınıflar veya lambda ifadeleri ile implemente edilebilir.

```java
@FunctionalInterface
interface MyCallback {
    void execute();
}

public class MyClass {
    public static void main(String[] args) {
        MyCallback callback = () -> System.out.println("Callback executed");
        performOperation(callback);
    }

    public static void performOperation(MyCallback callback) {
        // Some operation
        callback.execute();
    }
}
```

# LAMBDA

Lambda ifadeleri, Java'da fonksiyonel programlamaya olanak tanıyan ve genellikle bir fonksiyonun (bir arayüzün abstract metodu) yerine geçen ifadelerdir.

#### Genel Biçimler

1. `(<değişken isim listesi>) -> ifade`
2. `(<değişken isim listesi>) -> {...}`
3. `<değişken ismi> -> ifade`
4. `<değişken ismi> -> {...}`
5. `() -> ifade`
6. `() -> {...}`
7. `(<tür değişken> listesi) -> ifade`
8. `(<tür değişken> listesi) -> {...}`

#### Lambda İfadelerinin Kullanımı

Lambda ifadeleri, bir arayüz referansına atanır. Bu arayüz, yalnızca bir tane abstract metodu içeriyorsa "fonksiyonel arayüz" olarak adlandırılır.

```java
interface MyFunction {
    int operate(int a, int b);
}

public class Sample {
    public static void doOperation(MyFunction function, int x, int y) {
        System.out.println(function.operate(x, y));
    }

    public static void main(String[] args) {
        // Lambda ifadesi kullanımı
        doOperation((a, b) -> a * b, 10, 20);
    }
}
```

#### Lambda Parametreleri ve Scoping

Lambda parametreleri, yerel değişkenler gibi davranır. Aynı faaliyet alanındaki bir yerel değişken veya parametre ile aynı isme sahip bir lambda parametresi bildirilemez. Lambda ifadeleri, statik kapsam (static scope) sahiptir ve "shadowing" yapamazlar.

#### Lambda İfadeleri ve Hedef Tipi

Lambda ifadeleri daima hedef tipiyle birlikte bir bağlamda kullanılır. Yani, lambda ifadesi hedef tipinden bir değişkene atanır, hedef tipinden bir metoda/kurucuya geçilir veya hedef tipinden dönüşe sahip bir metottan geri döndürülür.

#### Lambda İfadeleri ve Fonksiyonel Arabirimler

Lambda ifadeleri genellikle fonksiyonel arayüzlerle kullanılır. Bir fonksiyonel arayüz, yalnızca bir tane abstract metodu içeren bir arayüzdür. Örneğin:

```java
@FunctionalInterface
interface StringFunction {
    String run(String str);
}

public class Sample {
    public static void printFormatted(String str, StringFunction format) {
        String result = format.run(str);
        System.out.println(result);
    }

    public static void main(String[] args) {
        StringFunction exclaim = s -> s + "!";
        StringFunction ask = s -> s + "?";
        printFormatted("Hello", exclaim);
        printFormatted("Hello", ask);
    }
}
```

# METHOD REFERENCE

Method reference in Java is a shorthand notation that allows you to refer to methods or constructors without invoking them. It is often used as a more concise way to express lambda expressions.

## Method Reference Types

1. **Static Method Reference (static method reference)**

```java
IntBinaryOperator ibo = IntOperation::multiply; // Lambda Equivalent: (a, b) -> IntOperation.multiply(a, b);
IntPredicate iPred = NumberUtil::isPrime; // Lambda Equivalent: a -> NumberUtil.isPrime(a);
```

2. **Reference to an Instance Method of a Particular Object (non-static method reference)**

```java
IntSupplier intSupplier = random::nextInt; // Lambda Equivalent: () -> random.nextInt();
```

3. **Reference to an Instance Method of Any Object of a Particular Type (non-static method reference)**

```java
IIntRandomBoundSupplier supplier = Random::nextInt; // Lambda Equivalent: (r, b) -> r.nextInt(b);
```

4. **Constructor Reference**

```java
IIntValueFactory factory = IntValue::new; // Lambda Equivalent: a -> new IntValue(a);
IIntValueDefaultFactory defaultFactory = IntValue::new; // Lambda Equivalent: () -> new IntValue();
```

#### Using Method References

Method references provide a concise way to represent lambda expressions, especially when the lambda expression is just a call to some method. They offer a more readable and elegant syntax.

```java
// Example with method reference
List<String> names = Arrays.asList("John", "Jane", "Doe");
names.forEach(System.out::println); // Equivalent Lambda: name -> System.out.println(name);
```

#### Limitations and Considerations

- The output from the previous expression needs to match the input parameters of the referenced method signature.
- Method references work best when the lambda expression is a simple call to an existing method or constructor.

Method references enhance the readability of your code and are often preferred when working with functional interfaces in Java.

# FUNCTIONAL INTERFACE

Java'da fonksiyonel programlamayı desteklemek için bir dizi fonksiyonel arayüz bulunmaktadır. Bu arayüzler, genellikle lambda ifadeleriyle birlikte kullanılır ve farklı türde operasyonları temsil eder.

#### 1. `Function` Arayüzleri

- `Function<T, R>`: `R apply(T t)` metodu ile bir giriş değerini alır ve bir çıkış değeri üretir.
- `BiFunction<T, U, R>`: `R apply(T t, U u)` metodu ile iki giriş değerini alır ve bir çıkış değeri üretir.

#### 2. `Operator` Arayüzleri

- `UnaryOperator<T>`: `T apply(T t)` metodu ile bir giriş değeri üzerinde bir operasyon uygular ve sonucu döndürür.
- `BinaryOperator<T>`: `T apply(T t1, T t2)` metodu ile iki giriş değeri üzerinde bir operasyon uygular ve sonucu döndürür.

#### 3. `Consumer` Arayüzleri

- `Consumer<T>`: `void accept(T t)` metodu ile bir giriş değeri üzerinde işlem yapar, ancak bir çıkış değeri üretmez.
- `BiConsumer<T, U>`: `void accept(T t, U u)` metodu ile iki giriş değeri üzerinde işlem yapar, ancak bir çıkış değeri üretmez.

#### 4. `Supplier` Arayüzleri

- `Supplier<T>`: `T get()` metodu ile herhangi bir giriş almadan bir değer üretir.

#### 5. `Predicate` Arayüzleri

- `Predicate<T>`: `boolean test(T t)` metodu ile bir giriş değeri üzerinde bir koşulu değerlendirir ve boolean bir sonuç üretir.
- `BiPredicate<T, U>`: `boolean test(T t, U u)` metodu ile iki giriş değeri üzerinde bir koşulu değerlendirir ve boolean bir sonuç üretir.

#### Anahtar Notlar

- Bu arayüzlerin temel tür karşılıkları her tür ve her işlem için bulunmaz.
- Bu arayüzler temel türler için çok kullanılan ve diğerlerinin bu türlere doğrudan (implicit) dönüşümlerinin geçerli olduğu için yazılmıştır.

```java
Function<Integer, Double> squareRoot = Math::sqrt;
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;

UnaryOperator<Integer> square = x -> x * x;
BinaryOperator<Integer> multiply = (a, b) -> a * b;

Consumer<String> logger = message -> System.out.println("Log: " + message);
Supplier<Integer> randomNumber = () -> (int) (Math.random() * 100);

Predicate<Integer> isEven = num -> num % 2 == 0;
BiPredicate<Integer, Integer> isGreater = (x, y) -> x > y;
```

# OPTINAL

ava'nın null referans sorunlarına karşı çözüm olarak sunulan `Optional` sınıfı, bir değerin mevcut olup olmadığını kontrol etmek ve değeri güvenli bir şekilde işlemek için kullanılır. İşte `Optional` sınıfının kullanımına dair örnekler:

## 1. Optional Oluşturma

```java
private Optional<String> m_middleNameOpt;

public MyClass(String middleName) {
    m_middleNameOpt = Optional.ofNullable(middleName);
}
```

## 2. Optional Değer Kontrolü

```java
public String getFullName() {
    return String.format("%s%s %s", 
        m_firstName, 
        m_middleNameOpt.map(n -> " " + n).orElse(""), 
        m_lastName);
}
```

#### Optional Kullanımına Dair Notlar

- `Optional` nesnesi kendisi hiçbir zaman null olmamalıdır.
- `ofNullable` metodu, bir nesnenin null olup olmadığını kontrol eder ve null ise boş bir Optional nesnesi oluşturur.
- `map` metodu, optional içinde değer varsa bu değeri üzerinde bir işlem yapmak için kullanılır.
- `orElse` metodu, optional içinde değer varsa bu değeri alır, değer yoksa belirtilen bir varsayılan değeri döner.
- `orElseGet` metodu, optional içinde değer varsa bu değeri alır, değer yoksa bir Supplier fonksiyonundan elde edilen değeri döner. Bu sayede varsayılan değeri oluşturmak için gereksiz işlem yapılmaz.
- `isPresent` metodu, optional içinde değer olup olmadığını kontrol eder ve bir boolean sonuç döner.

# ANNOTATION

Java'da annotation'lar, kodunuzu işaretlemek ve ek bilgi sağlamak için kullanılan önemli bir mekanizmadır. İşte Java'da annotation'ların getirilebildiği bildirimler ve annotation kullanımına dair bazı temel bilgiler:

#### 1. Annotation Kullanımı

```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation {
    String message() default "";
    int value();

    boolean success() default true;
}
```

#### 2. Annotation Kullanımı Sınıflarda

```java
@MyAnnotation(message = "This is a test message", value = 20)
class Sample {
    //...
}
```

#### 3. Enum ve Eleman Dizileri İle Annotation

```java
enum ButtonType { NONE, OK, YES, NO, CANCEL, YES_NO, YES_NO_CANCEL }

@Retention(RetentionPolicy.RUNTIME)
@interface ButtonAnnotation {
    ButtonType[] value() default { ButtonType.NONE };
}

@ButtonAnnotation({ ButtonType.YES, ButtonType.CANCEL })
class LoginWindow {
    //...
}
```

#### 4. Retention Policy (Saklama Politikası)

Java'da annotation'ların kullanım süresini belirlemek için `Retention` annotation'ı kullanılır. Bu annotation, `RetentionPolicy` enum'u türünden `value` adında bir elemana sahiptir. `RetentionPolicy.RUNTIME` ile belirtilen annotation'lar, çalışma zamanında kullanılabilir.

```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyRuntimeAnnotation {
    //...
}

@Retention(RetentionPolicy.CLASS)
@interface MyClassAnnotation {
    //...
}

@Retention(RetentionPolicy.SOURCE)
@interface MySourceAnnotation {
    //...
}
```


# REFLECTION

#### Reflection (Yansıma)

Java'da reflection, derleme zamanı bilgilerin çalışma zamanında elde edilip metadata'lar ile işlem yapma faaliyetidir. Java'da çalışma zamanında her tür bir `Class` nesnesi ile eşleştirilir ve bu nesne üzerinden türle ilgili bilgilere ulaşabiliriz.

```java
// Tür ismi ve nokta operatörü kullanarak Class nesnesi elde etme
Class<String> clsString = String.class;
Class<Sample> clsSample = Sample.class;
Class<?> clsInt = int.class;
Class<?> cslDouble = double.class;
Class<int[]> clsIntArray = int[].class;

// Class.forName metodu ile Class nesnesi elde etme
Class<?> clsString = Class.forName("java.lang.String");
Class<?> clsSample = Class.forName("org.csystem.app.Sample");

// Object sınıfının getClass metodu ile Class nesnesi elde etme
var cls = obj.getClass();
```

#### Reflection ile Tür Elemanlarına Erişim

Reflection kullanarak bir türün elemanlarına erişebiliriz. `getDeclaredXXXs` metotları ile tüm elemanlara, `getXXXs` metotları ile yalnızca public elemanlara ulaşabiliriz.

```java
var clsFactory = RandomObjectArrayFactory.class;
var ctor = clsFactory.getConstructor(); // Default ctor
var factory = ctor.newInstance();
var methodCreateObject = clsFactory.getDeclaredMethod("createObject");

methodCreateObject.setAccessible(true);
var obj = methodCreateObject.invoke(factory);
methodCreateObject.setAccessible(false);
```

#### Annotation Kullanımı

Java'da annotation'lar, kodunuzu işaretlemek ve ek bilgi sağlamak için kullanılan önemli bir mekanizmadır.

```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation {
    String message() default "";
    int value();

    boolean success() default true;
}

@MyAnnotation(message = "This is a test message", value = 20)
class Sample {
    //...
}
```

#### Repeatable Annotation Kullanımı

Bir annotation'ın aynı bildirimin önüne birden fazla kez getirilebilmesi için `@Repeatable` kullanılır.

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@Repeatable(Commands.class)
@interface Command {
    String value() default "";
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface Commands {
    Command[] value();
}
```

#### Reflection ve Cons

Reflection kullanımı genellikle yavaş ve zahmetli bir işlemdir. Ayrıca, encapsulation prensiplerini bozarak private metod ve alanlara erişimi mümkün kılabilir ve bu da güvenlik riski oluşturabilir.

Bu nedenle, reflection kullanımına karar verirken dikkatli olunmalı ve alternatif çözümler değerlendirilmelidir.

# ITERABLE

```java
// Iterable arayüzünü destekleyen bir sınıfın örneği
public class Passwords implements Iterable<String> {
    private List<String> passwords;

    public Passwords(List<String> passwords) {
        this.passwords = passwords;
    }

    @Override
    public Iterator<String> iterator() {
        return passwords.iterator();
    }

    public static void main(String[] args) {
        List<String> passwordList = List.of("password1", "password2", "password3");
        Passwords passwords = new Passwords(passwordList);

        // for-each döngüsü ile dolaşma
        for (String passwd : passwords) {
            System.out.printf("%s ", passwd);
        }
    }
}
```

### Iterable ve Iterator

Collection'ın üst arayüzüdür; dolayısıyla tüm Collection nesneleri Iterable'dır. Bir sınıfın for-each döngü deyimi ile dolaşılabilmesi için `Iterable<E>` arayüzünü desteklemesi gerekir. `Iterable<T>` arayüzünün bir tane `iterator` isimli abstract metodu vardır. Bu metot `Iterator<E>` arayüz referansına geri döner.

For-each döngüsünün karşılığı şu şekildedir:

```java
{
    Iterator<String> iter = passwords.iterator();
    String passwd;

    while (iter.hasNext()) {
        passwd = iter.next();
        Console.write("%s ", passwd);
    }
}
```


# COMPARABLE & COMPARATOR

`Comparable` arayüzü, onu gerçekleştiren nesnelerin sıralanabilmesini sağlar. Comparable arayüzü ile sağlanan sıralanmaya tabi sıralanma "natural ordering" denir.

Örnek bir Comparable implementasyonu:

```java
@Override
public int compareTo(Player otherPlayer) {
    return Integer.compare(getRanking(), otherPlayer.getRanking());
}
```

Eğer sınıf `Comparable<T>` arayüzünü desteklemezse veya desteklese bile farklı bir kritere göre sıralama yapmak istenirse, sıralama kriteri `Comparator` parametreli constructor'u ile verilebilir.

```java
Comparator<Player> byRanking = Comparator.comparing(Player::getRanking);
Comparator<Player> byAge = Comparator.comparing(Player::getAge);
```

`Comparator` kullanmanın avantajları şunlardır:

- Sınıfın kaynak kodunu değiştirmek mümkün değilse veya değiştirmek istenmiyorsa
- Birden fazla karşılaştırma stratejisi tanımlanabilir
- `Comparable` kullanıldığında belirlenen doğal sıralamadan farklı bir sıralama yapılabilir.

# LIST

Liste tarzı collection sınıfları, elemanları arasında öncelik-sonralık ilişkisi olan collection sınıflarıdır.

`List<E>` arayüzünün, `Collection<E>` arayüzünden gelen metotlarının yanı sıra, önemli iki metodu daha bulunmaktadır: `indexOf` ve `get`.

- **indexOf Metodu:** Bu metot, arama işleminde `equals` metoduna bakarak eşitlik karşılaştırması yapar. Örneğin:

```java
List<String> stringList = Arrays.asList("apple", "banana", "orange");
int index = stringList.indexOf("banana"); // Equals metoduna dayalı arama
```

**get Metodu:** Bu metot, listenin belirli bir indisindeki elemanı döndürür.

```java
String element = stringList.get(1); // İndise dayalı eleman alma
```

# LINKED LIST

`LinkedList` sınıfı, hem `List<E>` hem de `Deque<E>` arayüzlerini destekler. Ayrıca, `Deque<E>` arayüzü de `Queue<E>` arayüzünden türetilmiştir. Bu nedenle, `LinkedList` sınıfı genellikle "kuyruk tarzı collection"ları temsil eder.

#### Çift Taraflı Bağlı Listeler ve LinkedList

`LinkedList`, çift taraflı bağlı listeleri temsil eder. Her eleman, hem bir önceki hem de bir sonraki elemanı bilir. Bu, liste üzerinde çeşitli işlemleri daha etkili bir şekilde gerçekleştirmeyi sağlar.

#### LinkedList ve ArrayList Karşılaştırması

`LinkedList` ve `ArrayList` arasındaki temel fark, `LinkedList`'in elemanlarının her iki tarafındaki komşu elemanları bilmesidir. Bu, özellikle listenin başında veya sonunda yapılan ekleme veya silme işlemlerini daha hızlı hale getirebilir. Ancak, rastgele erişim (indeksleme) noktasında `ArrayList` genellikle daha hızlıdır.

#### Kuyruk Tarzı Collection ve poll Metotları

`LinkedList`, kuyruk tarzı bir collection olduğundan, `Queue<E>` arayüzünü destekler ve bu arayüzdeki metotları sağlar. Bu metotlardan bazıları şunlardır:

- `poll()`: Kuyruktan bir eleman çıkar ve null değeri döndürür (liste boşsa).
- `pollFirst()`: Listenin başından bir eleman çıkar ve null değeri döndürür (liste boşsa).
- `pollLast()`: Listenin sonundan bir eleman çıkar ve null değeri döndürür (liste boşsa).

Bu metotlar, listenin boş olup olmadığını kontrol etmek için geri dönüş değerlerini kullanabilir.

```java
LinkedList<String> linkedList = new LinkedList<>();
String element = linkedList.poll();

if (element == null) {
    System.out.println("LinkedList boş.");
} else {
    System.out.println("LinkedList boş değil.");
}
```

# SET

`Set<E>` arayüzünü destekleyen sınıflar küme koleksiyon sınıflarıdır. İki temel özelliği içerirler:

1. Bir kümede tüm elemanların sırasının önemi yoktur. Sıralama, ekleme ve silme önceliği ile ilgilidir, gerçek anlamda bir sıralama değildir.
    
2. Bir kümede bir elemandan yalnızca bir tane bulunur. Yani kümede eleman tekrarı olmaz.
    

#### TreeSet Sınıfı

`TreeSet<E>` sınıfı elemanları sıralı bir şekilde tutar. Bu sıralama, elemanların doğal sıralamasına göre gerçekleşir. Doğal sıralama genellikle artan sıradır. `TreeSet` sınıfı, elemanların eşitlik karşılaştırması için `equals` metodunu kullanır.

```java
TreeSet<Integer> treeSet = new TreeSet<>(); // Doğal sıralama (artan sıra)
treeSet.add(5);
treeSet.add(3);
treeSet.add(8);
// treeSet: [3, 5, 8]
```

Eğer `TreeSet` sınıfı bir sıralama kriteri almadan oluşturulursa, elemanların tipi `Comparable<T>` arayüzünü desteklemelidir. Aksi takdirde bir exception alınır.

```java
TreeSet<String> stringSet = new TreeSet<>();
stringSet.add("apple");
stringSet.add("orange");
stringSet.add("banana");
// Exception: java.lang.ClassCastException: class java.lang.String cannot be cast to class java.lang.Comparable
```

#### Comparator ile Sıralama

`Comparator` arayüzü kullanılarak isteğe bağlı sıralamalar yapılabilir. Örneğin, elemanları ters sıralamak için:

```java
var treeSetDesc = new TreeSet<Integer>((a, b) -> b - a);
// veya
var treeSetDesc = new TreeSet<Integer>(Comparator.reverseOrder());
```

#### HashSet ve TreeSet Arasındaki Farklar

- `HashSet`: Sırasız bir küme koleksiyonudur. Dizilim garantisi vermez. Herhangi bir elemanın yerini önceden bilmek mümkün değildir.
    
- `TreeSet`: Elemanları sıralı bir şekilde tutar. Doğal sıralama veya belirtilen bir `Comparator` kullanılarak sıralama yapabilir.
    

Her iki koleksiyon sınıfı da `Set` arayüzünü implemente eder, bu nedenle her ikisi de küme özelliklerini paylaşır: tekrarlayan elemanlara izin vermez ve bir elemanın sırasının önemi yoktur.


# MAP

`Map` tarzı koleksiyon sınıfları, anahtar-değer çiftlerini içerir. Bu sınıflarda her anahtar tekildir ve bir değer ile ilişkilidir. Anahtar-değer çiftlerini saklamak için `Set` sınıfı ve bir anahtarın değerini bulmak için `Collection` sınıfı kullanılır.

#### HashMap Sınıfı

`HashMap<K, V>` sınıfı, `Map<K, V>` arayüzünü destekleyen ve sıkça kullanılan bir koleksiyon sınıfıdır. Anahtarlar ve değerler arasında eşleme sağlar. Ancak, `HashMap` sınıfında anahtarların sıralaması belirsizdir ve hashCode'a göre belirlenir.

```java
HashMap<String, Integer> hashMap = new HashMap<>();
hashMap.put("apple", 5);
hashMap.put("banana", 3);
hashMap.put("orange", 8);

int appleCount = hashMap.get("apple"); // 5
```

`put` metodu, eğer anahtar daha önce eklenmişse, eski değeri günceller; eğer anahtar daha önce eklenmemişse, yeni bir değer ekler.

```java
hashMap.put("apple", 10); // apple anahtarı zaten ekli, değeri 10 ile güncellenir.
hashMap.put("grape", 7);  // grape anahtarı eklenir.
```

`putIfAbsent` metodu, eğer anahtar daha önce eklenmemişse, değeriyle birlikte ekler.

```java
hashMap.putIfAbsent("apple", 15); // apple anahtarı zaten ekli olduğu için işlem yapmaz.
hashMap.putIfAbsent("kiwi", 4);   // kiwi anahtarı eklenir.
```

Herhangi bir `Map` sınıfında, anahtarların hangi sıra ile tutulacağı belirsizdir. Ancak, elemanlara hızlı bir şekilde erişim sağlarlar.

Map'te iki önemli collection nesnesi bulunur:

- Anahtarları tutan `Set` (Anahtar Set'i): `keySet()` metodu ile alınır.
- Değerleri tutan `Collection` (Değer Collection'ı): `values()` metodu ile alınır.

Map sınıflarında ayrıca anahtar-değer ikililerini temsil eden `Entry` sınıfını içeren bir `Set` olan `entrySet()` metodu da bulunur.

# DEQUE

Java'da `Deque<T>` arayüzü çift yönlü kuyrukları temsil eder ve normal kuyruklardan farkı, başa ve sona eleman eklemenin yaklaşık olarak sabit zamanlı olmasıdır.

Bu arayüz, `Queue<T>` arayüzünden türetilmiştir. `Deque<T>` sınıfı, iki taraftan da efektif bir biçimde büyüyebilen bir dinamik dizi sınıfını temsil eder. Bu sınıfın birçok metodu, ya O(1) ya da "amortized O(1)" karmaşıklıkta çalışır.

# STREAM

### Stream API Temel Özellikleri

- **Veri Tutmazlar:** Stream'ler, bir veri yapısı gibi verileri tutmazlar.
- **Değişiklik Yapmazlar:** Stream'ler, kaynak veri üzerinde değişiklik yapmazlar.
- **Fonksiyonel Programlamaya Uygun Tasarım:** Fonksiyonel programlamaya uygun olarak tasarlanmışlardır ve çeşitli metotları fonksiyonel arayüzlerle callback alacak biçimde tasarlanmışlardır.
- **Veri Kaynağı Olabilirler:** Bir diziyi, bir collection sınıfını veya I/O Channel'ı gibi kaynak verileri kullanarak "stream" elde edilebilir.
- **Paralel İşlem Yeteneği:** Stream API içerisinde çeşitli işlemleri paralel yapabilen "parallel stream"'ler de bulunur.
- **Zincir (Fluent) Biçiminde İşlemler:** Stream işlemleri zincir (fluent) biçiminde yapılabilecek şekilde tasarlanmıştır.

> **Not:** Stream pipleline'ı sıfır ya da daha fazla ara işlem ve en fazla bir tane terminal işlemi içerebilir.

### Stream İşlemleri

- **Terminal İşlemler (Terminal Operations):** Çağrıldıklarında tüm zinciri çalıştırır.
- **Intermediate İşlemler (Intermediate Operations):** Terminal işlemi olmadan yapılamayan işlemlerdir (lazy evaluation). Bu işlemler, stream referanslarına geri dönerler. Callback'ler, terminal işlemi çağrıldığında ark planda çalıştırılır.

### Stream Kullanımı

```java
// Arrays sınıfının stream metodu ile bir diziden stream elde edilebilir.
Arrays.stream(numbers).filter(val -> val < threshold).forEach(Console::writeLine);

// Stream arayüzlerinin of metotları ile bir diziden stream elde edilebilir.
IntStream.of(numbers).filter(val -> val < threshold).forEach(Console::writeLine);
```

### Lazy Invocation

Intermediate işlemler, tembel (lazy) olarak çalışır. Yani, terminal işlemi çağrıldığında önceden belirlenen callback'ler ile işlemler gerçekleşir.

```java
// Stream'den başka bir Stream elde etme
Stream<Integer> newStream = stream.map(val -> val * 2);

// Reduce metodu
Optional<Integer> result = stream.reduce((a, b) -> a + b);

// Stream'den List elde etme
List<Integer> list = stream.collect(Collectors.toList());

// Filtering ve Mapping
List<String> stringList = stream
    .filter(val -> val % 2 == 0)
    .map(Object::toString)
    .collect(Collectors.toList());

// GroupingBy
Map<Integer, List<Integer>> groupedBy = stream
    .collect(Collectors.groupingBy(val -> val % 2));

// Joining
String resultString = stream
    .map(Object::toString)
    .collect(Collectors.joining(", ", "[", "]"));
```

### Özel Stream İşlemleri

- `takeWhile`: Belirli bir koşulu sağladığı sürece elemanları alır.
- `dropWhile`: Belirli bir koşulu sağlamadığı sürece elemanları atar.
- `Stream.generate()`: Belirtilen boyuta ulaşana kadar çalışan bir stream elde eder.

### Collectors Sınıfı

Collectors sınıfından elde edilen listeler iki gruba ayrılır: modifiable (değiştirilebilir), unmodifiable (değiştirilemez).

### Stream API İleri Seviye Kullanımlar

- **StreamSupport Sınıfı:** Iterable arayüzünün spliterator metodunun geri dönüş değeri verilerek Stream referansı elde edilebilir.
- **Distinct Metodu:** Elde edilen stream'e ilişkin tekrarlı eleman bulunmaz.
- **SummarizingInt Metodu:** Veri kümesinin temel aritmetik işlemlerini verir.

# LOGGING

Logging is a fundamental practice in software development and system administration, serving various purposes that contribute to efficient debugging, monitoring, security, and analysis of software applications and systems.

#### **Purposes:**

1. **Troubleshooting and Debugging:**
    
    - Developers can analyze log files to understand issues and errors.
    - Logs provide valuable information about the sequence of events leading to problems and relevant data.
2. **Monitoring and Performance Analysis:**
    
    - Log data monitors the health and performance of applications or systems.
    - Administrators can identify bottlenecks, slow response times, and resource utilization through log analysis.
3. **Security and Auditing:**
    
    - Logs capture unauthorized access attempts, potential security breaches, and suspicious activities.
    - Security teams analyze logs to detect and respond to threats, ensuring compliance with regulatory requirements.
4. **Historical Records:**
    
    - Logs serve as a historical record of events within a system over time.
    - Valuable for tracking down issues, understanding system behavior, and making informed decisions.
5. **Capacity Planning:**
    
    - Log data provides insights into resource usage and demand fluctuations for capacity planning.
    - Useful for scaling systems to accommodate increased traffic or usage.

#### **Types of Logging:**

- **FATAL:**
    
    - Represents critical issues leading to application failure (Logback doesn't have this level).
    - Logs fatal errors resulting in application termination or significant system failure.
- **ERROR:**
    
    - Indicates an error has occurred, but the application can continue to function.
    - Addresses errors needing attention but not causing complete failure.
- **WARN:**
    
    - Represents potentially harmful situations that may lead to errors or unexpected behavior.
    - Events might impact functionality or performance if left unaddressed.
- **INFO:**
    
    - Provides informational messages about the application's state, progress, or major events.
    - Logs important events, milestones, or state changes in the application.
- **DEBUG:**
    
    - Used for detailed debugging information, helping developers diagnose and troubleshoot issues.
    - Debug messages are useful during development and testing.
- **TRACE:**
    
    - The most detailed logging level, providing highly granular information about application flow.
    - Similar to DEBUG, TRACE messages provide even finer details.

```java
@Service
public class MyService {
    private static final Logger logger = LoggerFactory.getLogger(MyService.class);

    public void performActions() {
        // FATAL (ERROR in Logback)
        logger.error("FATAL: Critical system failure. Application cannot continue.");

        // ERROR
        logger.error("An error occurred while processing user request.");

        // WARN
        logger.warn("Potential resource shortage: Available memory is running low.");

        // INFO
        logger.info("Application started and ready to serve requests.");

        // DEBUG
        logger.debug("Processing user request: {}", getRequestDetails());

        // TRACE
        logger.trace("Entering method calculateTotal()");
    }

    private String getRequestDetails() {
        return "Sample request details";
    }
}
```

#### **Tips and Tricks:**

- **Clear Messages**
- **Choose the Right Level**
- **Use {} Brackets:** `logger.info("User: {}", username)` // Placeholders
- **Be Concise**
- **Log Exceptions**
- **Keep Secrets Safe**
- **External Config**
- **Regular Review**
- **Context Matters**
- **Start Simple**
- **Profile-Based:** Dev - Prod
- **Monitor Logs**
- **Document Standards** (In Markdown format)

# S.O.L.I.D

#### Single Responsibility Principle (SRP):

Every class should have only one reason to change, meaning each class should have only one job or responsibility.

#### Open-Closed Principle (OCP):

Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This is often achieved through the use of inheritance.

#### Liskov Substitution Principle (LSP):

Objects of the base class should be replaceable with objects of the derived class without affecting the correctness of the program. Subtypes must be substitutable for their base types (polymorphism).

#### Interface Segregation Principle (ISP):

Clients should not be forced to implement interfaces they do not use. In other words, a class should not be required to implement interfaces it does not need.

#### Dependency Inversion Principle (DIP):

High-level modules should not depend on low-level modules; both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

# IOC - INVERSION OF CONTROL

refers to the process of relinquishing control over the creation of objects within an application, allowing a framework to take charge. In IoC, the framework decides when to call methods based on predefined bindings, thus inverting the flow of control. This is sometimes known as the Hollywood Principle - "Don't call us, we'll call you." IoC is a fundamental concept that distinguishes a framework from a library.

### Coupling vs. Dependency

**Coupling** is a general relationship among objects, whereas **dependency** is a more specific relationship where modification in one object may necessitate a modification in another. Dependency implies a direct connection between two objects, such as when one object relies on another.

### Dependency Injection (DI)

**Dependency Injection** is a practice within IoC that involves separating the creation of dependent objects and providing them from the outside. It is a technique for minimizing dependencies within a system, fostering loose coupling and enhancing maintainability. By removing the responsibility of creating service objects, DI allows client objects to be highly cohesive and loosely coupled.

#### Advantages of Dependency Injection:

1. **Loose Coupling Between Components:**
    
    - Dependencies are managed externally, reducing direct connections between components.
2. **Minimizes Code Amount:**
    
    - The amount of code in the application is minimized as the responsibility of object creation is delegated.
3. **Easy Unit Testing with Mocks:**
    
    - Unit testing becomes easier as dependencies can be replaced with mock objects.
4. **Increased System Maintainability & Module Reusability:**
    
    - System maintenance is facilitated, and modules become more reusable.
5. **Allows Concurrent or Independent Development:**
    
    - Different parts of the system can be developed concurrently or independently.
6. **Replacing Modules Has No Side Effects:**
    
    - The replacement of modules does not adversely affect other modules.

By employing Dependency Injection, systems can achieve greater flexibility, modularity, and ease of testing.


# SPRING CORE

## Spring Framework Overview

Spring is an application development framework for Java that focuses on speed, simplicity, and productivity, making it the world's most popular Java application framework. It consists of various modules and provides multiple configuration options, with a significant portion being XML-based.

### Spring vs. Spring Boot

- **Spring Framework:** Modular structure, diverse configuration options (often XML-based).
- **Spring Boot:** Built on top of the Spring Framework, designed as a single, large module, prioritizes simplicity and fast configuration using primarily Java-based configurations.

### Spring Boot Features

Spring Boot applies the "convention over configuration" concept, simplifying development. It offers starters for libraries, easing dependency management, and includes features like the actuator for observability in cloud-deployed apps.

## Inversion of Control (IoC) in Spring

Spring uses a container to implement the IoC pattern. The container manages objects, known as "beans." Beans can be added using annotations like `@Bean` or stereotype annotations (`@Component`, `@Service`, `@Controller`, `@Repository`). Spring manages objects using reflection and proxies, allowing for dependency injection.

- **IoC:** In traditional programming, the application controls object creation; with IoC, the framework/container manages it.
- **DI (Dependency Injection):** A specific implementation of IoC where the container injects dependencies at runtime.
- **AOP (Aspect-Oriented Programming):** Separates cross-cutting concerns from core business logic.

### Application Context in Spring

The Application Context is the IoC container in Spring, representing the framework's "brain." It is a sub-interface of BeanFactory and adds more enterprise-specific functionality. The ApplicationContext is used more frequently than BeanFactory and supports autowiring.

- **What Application Context Does:**
  - **Dependency Injection:** Injects dependencies into objects based on configuration.
  - **Bean Lifecycle Management:** Creates, initializes, and manages bean lifecycles.
  - **Configuration Management:** Loads and manages configuration files defining beans and relationships.

## Spring Boot and @SpringBootApplication

The `@SpringBootApplication` annotation combines `@EnableAutoConfiguration`, `@Configuration`, and `@ComponentScan`. It serves as the main entry point, invoking the `SpringApplication.run` method. Typically placed in a root package, it enables component scanning across sub-packages for beans. This annotation designates the application's entry point, equivalent to the main function.

## Bean

A **bean** is an object instantiated, assembled, and managed by a Spring IoC container (Application Context), where Spring holds instances of objects identified to be managed and distributed automatically. These are called beans. Spring collects bean instances from the application and uses them at the appropriate time.

- **What is a Bean?** Instance of Class controlled by the IoC Container (Application Context).
- **When?** When the application starts.
- **How?** XML or Annotation.
- **Where?** In Application Context.
- **By Who?** Application Context.

## BeanFactory

`BeanFactory` is the root interface for accessing the Spring IoC container, providing basic functionality to manage beans in Spring. Managing includes creating objects and injecting them to satisfy dependencies.

```java
Object getBean(String name)
T getBean(Class<T> requiredType)
T getBean(String name, Class<T> requiredType)
```

`ListableBeanFactory` finds more than one bean defined for a specific type.

## Configuration Metadata

The Spring IoC container gets instructions to instantiate, configure, and assemble beans by reading configuration metadata represented in XML or properties files, Java annotations, or Java code.

## @Component

The `@Component` annotation is a class-level annotation. It marks the Java class as a bean or component for Spring to manage. Using `@Component` across the application marks the beans as Spring's managed components.

## Creating Beans Programmatically


```java
context.registerBean("volkswo&en", Vehicle.class, volkswałenSupplier);
```

## @Bean

The `@Bean` annotation is a method-level annotation. Spring calls these methods when a new instance of the return type is required.

```java
@Bean
Engine engine() {
    return new Engine();
}
```

Note: All methods annotated with `@Bean` must be in `@Configuration` classes. For 3rd party libraries where source code is unavailable, we can control instance creation logic.

### Bean Injection Methods

- Construction Injection
- Field Injection
- Setter Injection
- `@Autowired` annotation

Field injection should be avoided because:

- It uses reflection during injection of the field which will be costly in performance
- Testing will be difficult as it will require using either reflection to set the field or starting the spring container which will make it an integration test
- The objects cannot be immutable as in the constructor injection
- The field can reference a null instance
- The class can have additional dependencies without restricting it as in the constructor injection, therefore it can violate single responsibility principle

Constructor injection should be used for mandatory dependencies whilst setter methods can be used for optional dependencies.

## @Scope

We use `@Scope` to define the scope of a `@Component` class or a `@Bean` definition.

Scope Types:

- **Singleton:** The container creates a single instance of that bean. Modifications to the object reflect in all references.
- **Prototype:** A new instance is created for each request. Better for concurrency.
- **Request:** Creates a bean instance for a single HTTP request.
- **Session:** Creates a bean instance for a single HTTP session.
- **Application:** Creates a bean instance for the lifecycle of a ServletContext.
- **WebSocket:** Creates a bean instance for a particular WebSocket session.

## @Lazy

By default, the Spring IoC container creates and initializes all singleton beans at the time of application startup. `@Lazy` delays bean initialization until requested.

## @Configuration

`@Configuration` indicates that the class has `@Bean` definition methods.

## @Qualifier

The `@Qualifier` annotation differentiates a bean among the same type of bean objects. It provides the bean ID or bean name in ambiguous situations. Note that "@Qualifier" invalidates "@Primary" if used together.

## @Autowired

The `@Autowired` annotation marks a dependency for Spring to resolve and inject. It looks for a class or interface with a property matching the `@Autowired` annotation. It is recommended for use with a single constructor.

In a class, only one constructor can be annotated with `@Autowired`. If there is only one constructor with an injectable dependency, there is no need for `@Autowired` for that constructor.

### Why @Autowired is Not Recommended

- Reduced Readability: Autowiring may obscure required dependencies.
- Increased Coupling: Autowired dependencies can lead to tight coupling between classes.
- Testing Challenges: Autowired dependencies can complicate unit testing.

> Annotating `@Bean` only registers the service (custom object) as a bean in the Spring application context. In simple words, it is just registration and nothing else. Annotating a variable with `@Autowired` injects a `BookingService` bean (i.e., object) from the Spring Application Context. The registered object with `@Bean` annotation will be injected into the variable annotated with `@Autowired`.

# Other Dependency Injection Annotations and Features

## @Inject

- **Not Spring Annotation Originally**
- Injects any Java object which is a POJO.
- No need to mark POJOs to be injected by @Inject.
- **Note:** @Autowired is Spring's own annotation. @Inject is part of a Java technology called CDI that defines a standard for dependency injection similar to Spring.

## @Named

- **Not Spring Annotation Originally**
- Performs the same functionality as @Component.
- Used to qualify beans for injection.

## @Required (Deprecated)

- Method-level annotation applied to the setter method of a bean property, making setter-injection mandatory.
- Indicates that the required bean property must be injected with a value at configuration time.
- Deprecated; legacy code may still use it.

## @Value

- Assigns default values to variables and method arguments.
- Reads Spring environment variables and system variables.
- If the same property is defined as a system property and in the properties file, the system property takes precedence.
- Provides a default value in the SpEL expression to prevent null values.
- Used for constant values.

```java
@Value("#{systemProperties['unknown'] ?: 'some default'}") // Default value expression
private String spelSomeDefault;

@Value("#{'${listOfValues}'.split(',')}") // Manipulating properties to get a List
private List<String> valuesList;
```

## @Primary

- Used to give higher preference to a bean when multiple beans of the same type exist.
- Serves the bean marked with @Primary in case of ambiguity, when a bean is not marked with @Qualifier.

# Spring Profiles

Each environment requires settings specific to them, allowing mapping beans to different profiles (e.g., dev, test, prod). Activate profiles in different environments to bootstrap only the needed beans.

## @Profile

- Maps a bean to a particular profile.
- Profile names can be prefixed with a NOT operator.

```java
@Profile({"Tomcat", "Linux", "!Windows"})
@Configuration
public class AppConfigMongodbLinux { ... }
```

## @Conditional

- Used for conditional bean registration.
- Similar to an if-else for bean registration.
- Indicates that a component is eligible for registration when specified conditions match.
- Conditions apply to @Bean methods, @Import annotations, and @ComponentScan annotations in a @Configuration class.

## @ComponentScan

- Used with @Configuration to specify packages for Spring to scan for annotated components.
- Without arguments, it scans the current package and sub-packages.
- The location of the configuration class determines the scanning starting point.

## @ConfigurationProperties

- Annotation-driven feature binding external configuration properties to Java objects.
- Simplifies loading and using configuration values from various sources.
- Encapsulates configuration values in strongly-typed Java classes.

```java
@Component
@ConfigurationProperties("myapp")
public class MyAppProperties { ... }
```

```properties
# application.properties
myapp.name=My Awesome App
myapp.maxConnections=10
```

```java
@SpringBootApplication
@EnableConfigurationProperties(MyAppProperties.class)
public class MyApplication { ... }
```

```java
@RestController
public class MyController {
    private final MyAppProperties appProperties;

    @Autowired
    public MyController(MyAppProperties appProperties) {
        this.appProperties = appProperties;
    }

    @GetMapping("/info")
    public String getAppInfo() {
        return "App Name: " + appProperties.getName() +
               ", Max Connections: " + appProperties.getMaxConnections();
    }
}
```

# Application Runner Interface

The `ApplicationRunner` interface in Spring is a functional interface with a `run()` method to be invoked at application startup. It is commonly used to perform specific tasks or actions when the application starts.

## Key Points

- **Functional Interface**: `ApplicationRunner` is a functional interface, meaning it has a single abstract method (`run()`) and can be used as a lambda expression or method reference.

- **Application Arguments**: The `run()` method has an instance of the `ApplicationArguments` class as a parameter. This class provides access to the arguments passed to the application at runtime.

- **Usage**: It can be used in two main ways—annotated with `@Component` or defined as a `@Bean`. In both cases, Spring manages the instantiation and injection of the `ApplicationRunner` instance.

- **Execution After Startup**: The `run()` method is invoked after the application has started. It guarantees that the object has been initialized before the `run` method is called.

- **Not Asynchronous**: Unlike some other Spring features, `ApplicationRunner` does not run asynchronously.

- **Outside Web Applications**: It is commonly used in applications other than web applications. In the case of web applications, there are other mechanisms, such as `@PostConstruct` or `CommandLineRunner`, that can be used.

## Property Lookup Order

Spring looks for properties at runtime in the following order:

1. **Command Line Arguments**: Properties specified through the command line.
   ```bash
   java -jar your-application.jar --property=value
```

2. **Application's Jar Folder**: An `application.properties` file within the same folder as the JAR.

```bash
/your-application.jar
/config/application.properties
```

3. **Embedded in JAR**: An `application.properties` file embedded within the JAR.

```java
/your-application.jar
    /BOOT-INF
        /classes
            /application.properties
```


# Aspect-Oriented Programming (AOP) in Spring

An aspect is a piece of code that the Spring framework executes when you call specific methods within your application. Spring AOP facilitates Aspect-Oriented Programming in Spring applications, allowing the modularization of concerns such as transaction management, logging, or security, which cut across multiple types and objects (known as crosscutting concerns).

## Key Concepts

1. **Dynamic Cross-Cutting Concerns**: AOP provides a way to dynamically add cross-cutting concerns before, after, or around the actual logic using simple pluggable configurations.

2. **Separation of Concerns**: AOP helps in separating and maintaining non-business logic-related code, such as logging, auditing, security, and transaction management.

3. **Modularity with Cross-Cutting Concerns**: AOP is a programming paradigm that increases modularity by allowing the separation of cross-cutting concerns. It adds additional behavior to existing code without modifying the code itself.

## Spring AOP Architecture

The core architecture of Spring AOP is based on _proxies_. When the application is initialized, an advised instance of a class is created as the result of a _``ProxyFactory``_ creating a proxy instance of that class with all the aspects woven into the proxy. 

In runtime, Spring analyzes the crosscutting concerns defined for the beans in _``ApplicationContext``_ and generates proxy beans (which wrap the underlying target bean) dynamically. Instead of accessing the target bean directly, callers are injected with the proxied bean.

Internally, Spring has two proxy implementations:

- **JDK dynamic proxies**: when the target object to be advised implements an interface.
- **CGLIB proxies**: when the advised target object doesn’t implement an interface. For example, it’s a concrete class.

Note that the JDK dynamic proxy supports only the proxying of interfaces.

Remember that **Spring AOP has some limitations**. Such as:

- Final classes or methods cannot be proxied since they cannot be extended.
- Also, due to the proxy implementation, Spring AOP only applies to public, non-static methods on Spring Beans.
- If there is an internal method call from one method to another within the same class, the advice will never be executed for the internal method call.

## AOP Jargons

- **Joinpoint**: is a point of execution of the program, such as executing a method or handling an exception. **In Spring AOP, a joinpoint always represents a method execution.** Joinpoints define the points in your application at which you can insert additional logic using AOP.

- **Advice**: is the code that is executed at a particular joinpoint. There are many types of advice, such as _before_, which executes before the joinpoint, and _after_, which executes after it.

- **Aspect**: is the combination of advices and pointcuts encapsulated in a class.

- **Pointcut**: is a predicate or expression that matches joinpoints.

- **Weaving**: is the process of inserting aspects into the application code at the appropriate point. AspectJ supports a weaving mechanism called _load-time weaving (LTW)_, in which it intercepts the underlying JVM class loader and provides weaving to the bytecode when it is being loaded by the class loader.

- **Target**: is the object whose execution flow is modified by an AOP process. Often you see the target object referred to as the _advised object_.

- Spring uses the AspectJ pointcut expression language by default.



## Type of Advices in Spring AOP

- **Before advice**: Advice that executes before a join point, but which does not have the ability to prevent execution flow proceeding to the join point (unless it throws an exception).

- **After returning advice**: Advice to be executed after a join point completes normally: for example, if a method returns without throwing an exception.

- **After throwing advice**: Advice to be executed if a method exits by throwing an exception.

- **After advice**: Advice to be executed regardless of the means by which a join point exits (normal or exceptional return).

- **Around advice:** Advice that surrounds a join point such as a method invocation. This is the most powerful kind of advice. Around advice can perform custom behavior before and after the method invocation. It is also responsible for choosing whether to proceed to the join point or to shortcut the advised method execution by returning its own return value or throwing an exception.

## Spring AOP Pointcut Expression

Spring AOP uses AspectJ-style expressions for defining pointcuts. The syntax involves combining various elements to precisely target specific join points.

For example, use `_execution_()` to specify the method execution join points. The basic syntax is in the pattern ‘_``execution(modifiers? return_type method_name(param_type1, param_type2, …))``_‘. Consider the following example:

```java
execution(public void com.example.service.MyService.doSomething())
```

Use wildcards to match multiple elements, similar to regular expressions. For instance, `*` matches any sequence of characters, and `..` matches any number of parameters. Consider the following example:

```java
execution(* com.example.service.*.*(..))
```

Use `_within()_` to specify join points within a certain type or package. For example, the following expression matches all methods within the ‘_``com.example.service``_‘ package.

```java
within(com.example.service.*)
```

The most typical point-cut expressions are used to match the methods by their signatures.

### Pointcut Expressions: Matching Specific Methods in a Class

|Pointcut Expression|Description|
|---|---|
|execution(* com.example.EmployeeManager.*(..))|Match all methods in the specified package and class|
|execution(* EmployeeManager.*(..))|Match all methods in the same package and specified class|
|execution(public * EmployeeManager.*(..))|Match all public methods in _EmployeeManager_|
|execution(public Employee EmployeeManager.*(..))|Match all public methods in EmployeeManager with return type _Employee_ object|
|execution(public Employee EmployeeManager.*(Employee, ..))|Match all public methods in _EmployeeManager_ with return type _Employee_ and first parameter as _Employee_|
|execution(public Employee EmployeeManager.*(Employee, Integer))|Match all public methods in _EmployeeManager_ with return type _Employee_ and the specified parameters|
### Pointcut Expressions: Matching All Methods in a Class or Package

|Pointcut Expression|Description|
|---|---|
|within(com.example.*)|Match all methods in all the classes inside package ‘_com.example.*_‘|
|within(com.example..*)|Match all methods in all the classes inside package ‘_com.howtodoinjava_‘ and the classes inside all sub-packages as well|
|within(com.example.EmployeeManagerl)|Match all methods within the specified class in the specified package|
|within(EmployeeManager)|Match all methods within the specified class in the current package|
|within(IEmployeeManager+)|Match all methods within all the implementations of the specified interface|
### Pointcut Expressions: Matching Class Name Patterns

|Pointcut Expression|Description|
|---|---|
|bean(*Manager)|Match all methods in bean whose name ends with ‘_Manager_‘|
|bean(employeeManager)|Match all methods in specified bean with name ‘_employeeManager_‘|
|bean(com.example.service.*)|Match all methods in all the beans in a specific Package|
|bean(@MyCustomAnnotation *)|Match all methods in all the beans with a specific annotation|

### Combining Pointcut Expressions

In AspectJ, pointcut expressions can be combined with the operators `&& (and)`, `|| (or)`, and `! (not)`.
The following matches all the methods in beans whose names ending with _Manager_ or _DAO_.

Use `'||'` sign to combine both expressions.

 ```java
 bean(*Manager) || bean(*DAO) 
```
## Example Codes 

### Maven

Before writing any code, you will need to import _Spring AOP dependencies_ into your project.

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.1.1</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context-support</artifactId>
    <version>6.1.1</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
    <version>6.1.1</version>
</dependency>
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjrt</artifactId>
    <version>1.9.20.1</version>
</dependency>
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.20.1</version>
</dependency>
```


In a Spring Boot application, adding dependencies is rather easier.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

### Enabling Spring AOP

We can enable Spring AOP using the **_``@EnableAspectJAutoProxy``_** annotation on a configuration.

```java
@Configuration
@EnableAspectJAutoProxy
@ComponentScan
public class AopConfig {
 
}
```

### Define an Advice using Aspect and Pointcut Expression

Each Aspect class should be annotated with **_@Aspect_** annotation. Within that class, we then specify Pointcuts and Advice. It should also be annotated with _@Component_ to be picked up by component scanning (or configured as a Spring bean in another way).

```java
@Aspect
public class EmployeeCRUDAspect {
      
    @Before("execution(* EmployeeManager.getEmployeeById(..))")     //point-cut expression
    public void logBeforeV1(JoinPoint joinPoint) {

        System.out.println("EmployeeCRUDAspect.logBeforeV1() : " + joinPoint.getSignature().getName());
    }
}
```

### Advised Methods (Jointpoints)

Write methods on which you want to execute advice and those match with point-cut expressions.

```java
@Component
public class EmployeeManager {

    public EmployeeDTO getEmployeeById(Integer employeeId) {
        System.out.println("Method getEmployeeById() called");
        return new EmployeeDTO();
    }
}
```

In the above example, `logBeforeV1()` will be executed **before** `getEmployeeById()` method because it matches the join-point expression.

### Run the Application

Run the application and watch the console.

```java
public class TestAOP
{
    @SuppressWarnings("resource")
    public static void main(String[] args) {
  
        ApplicationContext context = new ClassPathXmlApplicationContext
                  ("com/howtodoinjava/demo/aop/applicationContext.xml");
 
        EmployeeManager manager = context.getBean(EmployeeManager.class);
  
        manager.getEmployeeById(1);
    }
}
```

Program output:

```log
EmployeeCRUDAspect.logBeforeV1() : getEmployeeById
Method getEmployeeById() called
```


# SPRING WEB

Web services are structures that provide services to other systems/devices over the HTTP protocol. When you need to send your data to all devices outside your web page, the concept of Web Service comes into play. Web services enable different applications to work together, even with different languages or frameworks, by facilitating communication.

## Types of Web Services

1. **SOAP (Simple Object Access Protocol):**
   - A protocol for exchanging structured information.
   - XML is used for data transmission.
   - Applications use SOAP protocols for inter-application communication.

2. **RESTful (Representational State Transfer):**
   - Data is often transferred in JSON (JavaScript Object Notation) format.
   - Enables communication between web clients and resources.
   - Principles:
     1. Uniform Interface
     2. Stateless
     3. Layered System
     4. Cacheable
     5. Code on Demand (optional)

3. **gRPC:**
   - Open-source Remote Procedure Call (RPC) framework.
   - Advantages:
     1. Lightweight messages (up to 30% smaller than JSON).
     2. High performance (5-8 times faster than REST+JSON).
     3. Built-in code generation.
     4. More connection options with data streaming.

## Servlet

Servlet is a Java EE framework that manages the client-server architecture with the help of an Application Server (e.g., Tomcat). It utilizes HTTP protocols for communication between the application and the server.

## HTTP Requests

HTTP requests are made by a client to a named host located on a server, aiming to access a resource. HTTP request codes are status codes returned by a web server in response to a client's HTTP request.

### HTTP Status Codes

- 1xx: Informational (100-199)
- 2xx: Success (200-299)
- 3xx: Redirection (300-399)
- 4xx: Client errors (400-499)
- 5xx: Server errors (500-599)

### HTTP Methods

1. **GET:**
   - Request data from a specified resource.
   - Success: 200 (OK), Error: 404 (Not Found) or 400 (Bad Request).

2. **POST:**
   - Send data to a server to create/update a resource.
   - Success: 201 (Created), Error: 404 (Not Found), 409 (Conflict).

3. **PUT:**
   - Send data to a server to create/update a resource.
   - Success: 200 (OK) or 204 (No Content), Error: 404 (Not Found).
   - Idempotent: Multiple calls produce the same result.

4. **HEAD:**
   - Similar to GET but without the response body.

5. **DELETE:**
   - Deletes the specified resource.
   - Success: 200 (OK), Error: 404 (Not Found).

6. **PATCH:**
   - Apply partial modifications to a resource.
   - Success: 200 (OK) or 204 (No Content), Error: 404 (Not Found).

## ResponseEntity in Spring

The `ResponseEntity` class in Spring represents the entire HTTP response, including the status code, headers, and body. It's a generic type that allows specifying the response body type, HTTP status code, and headers. This class is particularly useful for creating custom HTTP responses in a Spring application.

## Returning a Custom HTTP Status Code

You can use `ResponseEntity` to return a custom HTTP status code, as shown in the following examples:

### Create User Example

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
    // Code to create user
    return new ResponseEntity<>(user, HttpStatus.CREATED);
}
```

### Get User Example

```java
@GetMapping("/users/{id}")
public ResponseEntity<User> getUser(@PathVariable int id) {
    try {
        User user = // Code to get user by id
        return new ResponseEntity<>(user, HttpStatus.OK);
    } catch (UserNotFoundException ex) {
        return new ResponseEntity<>(null, HttpStatus.NOT_FOUND);
    }
}

@ExceptionHandler(UserNotFoundException.class)
public ResponseEntity<ErrorResponse> handleUserNotFoundException(UserNotFoundException ex) {
    ErrorResponse error = new ErrorResponse("User not found", ex.getMessage());
    return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
}
```

## Spring MVC Annotations

### @Controller vs. @RestController

- `@Controller`: Used for traditional web applications generating views (HTML and static pages).
- `@RestController`: Used for building RESTful APIs that return data directly in JSON or XML format.

### DispatcherServlet

The `DispatcherServlet` is a key component of the Spring MVC framework, acting as the front controller. It handles incoming HTTP requests, manages the flow, and interacts with controllers, adapters, and view resolvers.

### @RequestMapping

The `@RequestMapping` annotation is used to map HTTP requests to handler methods in MVC and REST controllers. It can be applied at the class and/or method level. Examples:

```java
// Class-level mapping
@RequestMapping("/api/greetings")

// Method-level mapping
@GetMapping("/greeting")
public String getGreeting() {
    return "Hello, World!";
}
```

### HTTP Methods Annotations

Spring provides specialized annotations for common HTTP methods:

- `@GetMapping`: Handles HTTP GET requests.
- `@PostMapping`: Handles HTTP POST requests.
- `@PutMapping`: Handles HTTP PUT requests.
- `@DeleteMapping`: Handles HTTP DELETE requests.
- `@PatchMapping`: Handles HTTP PATCH requests.

### @RequestParam

The `@RequestParam` annotation is used to extract query parameters from the URL. Example:

```java
@GetMapping("/greet")
public String greet(@RequestParam String name) {
    return "Hello, " + name + "!";
}
```

### @RequestBody

The `@RequestBody` annotation is used to bind a method parameter to the body of the HTTP request. It automatically deserializes JSON into a Java type. Example:

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
    // Code to create user
    return new ResponseEntity<>(user, HttpStatus.CREATED);
}
```

### @PathVariable

The `@PathVariable` annotation handles template variables in the request URI mapping. It extracts data from the URI path. Example:

```java
@GetMapping("/users/{id}")
public ResponseEntity<User> getUser(@PathVariable int id) {
    try {
        User user = // Code to get user by id
        return new ResponseEntity<>(user, HttpStatus.OK);
    } catch (UserNotFoundException ex) {
        return new ResponseEntity<>(null, HttpStatus.NOT_FOUND);
    }
}
```

### Difference Between @RequestParam and @PathVariable

- `@RequestParam`: Extracts query parameters from the URL.
- `@PathVariable`: Extracts data from the URI path.

### URL vs. URI

- A URL is a specific type of URI that includes the protocol, domain, and resource path.
- A URI is a string of characters identifying a name or resource on the internet.

# SPRING DATA

# Immutability in Spring

Immutability is crucial in Spring for several reasons:

1. **Thread Safety:**
   - Immutable objects are inherently thread-safe because their state cannot be modified after creation.
   
2. **Predictability and Stability (Idempotency):**
   - Immutable objects have a fixed state, making their behavior predictable and stable. Once created, they cannot be modified accidentally or maliciously by other parts of the code.
   
3. **Simplicity and Maintainability:**
   - Immutable objects promote simplicity and ease of maintenance. Without the need to manage internal state transitions or mutation-related logic, the code becomes cleaner and more maintainable.
   
4. **Better Testing:**
   - Immutable objects are typically easier to test as their state remains constant. Unit testing becomes straightforward without complex setups or mocking.
   
5. **Caching and Optimization:**
   - Immutable objects can be safely cached since their state is guaranteed not to change. This can lead to performance optimizations by avoiding unnecessary object creation and reducing memory overhead.

# Loading Initial Data with Spring Boot

## data.sql File
Spring Boot creates an empty table but doesn't populate it. To load initial data:
- Create a file named `data.sql` that Spring will pick up to populate the database.

## schema.sql File
- If a custom schema is needed, create a `schema.sql` file.
- Spring will use this file for creating the schema.
- Use the `spring.sql.init.mode` property to customize schema creation behavior.

# Intro to JDBC (Java Database Connectivity)

- JDBC is a Java API that provides a standard abstraction for Java applications to communicate with various databases.
- Steps in JDBC:
  1. Load Driver Class
  2. Obtain a DB connection
  3. Obtain a statement using the connection object
  4. Execute the query
  5. Process the result set
  6. Close the connection

## Problems with JDBC
- Duplication of code.
- Handling checked exceptions.
- Database dependency.

# Spring JDBC

## JdbcTemplate Class

- Takes care of low-level details in JDBC.
- Handles creation and release of resources.
- Manages exceptions and provides informative messages.
- Enables performing database operations easily.

## NamedParameterJdbcTemplate Class

- Wraps JdbcTemplate.
- Allows the use of named parameters instead of traditional placeholders.
- Provides a way to specify named parameters in SQL queries.
- Improves readability and maintainability.

## RowMapper Interface

- Maps a row of a ResultSet to a domain object.
- Used to process one record of ResultSet at a time.
- Allows customization based on the row number.

## ResultSetExtractor Interface

- Processes multiple records of ResultSet at a time.
- Useful for complex joins in a query.
- Allows access to the entire ResultSet.

## BeanPropertySqlParameterSource

- Maps Java Bean properties to SQL parameters.
- Convenient for specifying SQL parameters for SimpleJdbcCall or SimpleJdbcInsert.
- Reduces manual mapping code.

ResultSetExtractor is designed to extract the entire ResultSet (possibly multiple rows), while RowMapper is fed with one row at a time.

# Spring Data JPA

**Core Objectives:** Spring Data JPA aims to simplify the Data Access Layer, reducing code complexity while providing a feature-rich set of functionalities.

## What is ORM

ORM is a technique that provides interaction with a database using OOP languages. Hereby, it provides simplicity in discrepant database operations like creating, reading, updating and deleting.

## ICrudRepository

- **Definition:**
    
    - A convenience interface providing common methods for CRUD operations on a repository of a specific type.
    - Extends the Repository interface and adds basic CRUD methods.
- **Usage:**
    
    - `public interface CrudRepository<T, ID> extends Repository<T, ID>`
    - T: Domain type (Entity/Model class)
    - ID: Type of the entity's ID (Wrapper class of @Id)

## @Repository

- **Definition:**
    - Specialization of the @Component annotation, indicating that a class is a repository.
    - Responsible for managing the data access layer, providing CRUD methods.

## @Service

- **Definition:**
    - Specialization of the @Component annotation.
    - Indicates that a class belongs to the service layer, holding business logic.

## Data Transfer Object (DTO)

- **Definition:**
    - A design pattern used to transfer data between systems or layers of an application.
    - Minimizes calls between layers, improving application performance.
    - Should not contain business logic but handles serialization and deserialization.

## MapStruct

- **Definition:**
    
    - Java annotation processor for implementing bean mapping between Java bean classes.
    - Generates mapping code at compile time, reducing manual coding effort.
- **Annotations:**
    
    - @Mapper: Indicates that the interface contains methods for mapping between Java bean classes.
    - @Mapping: Specifies how fields in a Java object map to columns in a database table.

## Object-Relational Model (ORM)

- **Definition:**
    
    - A technique bridging databases and object-oriented programming.
    - Represents database entities in application code.
- **Pros:**
    
    - DRY principle, easier maintenance.
    - Easier querying using ORM.
    - No need to change code with database changes.
- **Cons:**
    
    - Learning curve.
    - Performance can be an issue for some queries.
    - Database abstraction can lead to less efficient queries.

## Spring Data JPA

- **Definition:**
    
    - Reduces code complexity in the Data Access Layer while providing rich functionality.
    - Automatically generates queries from method names.
- **Query DSL (Domain Specific Language):**
    
    - Creates queries using a clear and concise syntax.
    - Improves readability and type safety.
    - Validates queries at application startup.
- **Query Method Syntax Examples:**
    
    - See table for various query methods based on method names.
- **Performance Considerations:**
    
    - JPA is designed for reading and querying data rather than massive write operations.
    - Overhead costs during write operations can impact performance.


## What is Hibernate

Hibernate is an ORM (Object Relational Mapping) tool that provides a framework to map OOP domain models to relational database tables in the Spring Boot application.

##  What is JPA and Spring Data JPA

JPA is a standard that persists and retrieves information from a non-volatile storage system, mapping Java objects to tables in a database.

- The entity manager API can persist, update, retrieve or remove objects from a database.
- The entity manager API can provide ORM without requiring JDBC or SQL code.
- JPA provides a query language that can retrieve objects without writing massive SQL queries

Spring Data JPA uses JPA to store data in a relational database. Hibernate is a JPA implementation.

Hibernate, Explips Link, or any other JPA provider may be used. Spring Data is not an implementation or JPA provider; it is just an abstraction to reduce the boilerplate code significantly.

> JPA is not a framework. It is a standard and concept.


##  JPA Architecture

![[Pasted image 20240212095139.png]]

![[Pasted image 20240212095202.png]]

###  How Persistence Operation works

![[Pasted image 20240212095429.png]]

Hibernate is a JPA provider, while Spring Data JPA is not a JPA provider. It is just an abstraction that can be used with Hibernate, Eclipse Link, etc.  

##  Repository Pattern

the repository pattern manages fundamental CRUD operations in a BaseRepository class.

![[Pasted image 20240212095655.png]]

The repository pattern involves creating a Generic BaseRepository interface that contains basic CRUD operations for the database. Alongside this interface, there’s a concrete BaseRepositoryImpl class that implements these operations using the EntityManager.

To perform these common operations for entities, we create abstract classes like UserRepository for the User entity. These abstract classes define custom operations relevant to the entity. Additionally, we have concrete classes like UserRepositoryImpl, which extend both the BaseRepositoryImpl and the respective abstract UserRepository.

This approach offers several benefits.

- Firstly, it encapsulates common database operations within the BaseRepository, promoting code reuse and maintainability.
- Secondly, by extending abstract classes like UserRepository, we can define entity operations while inheriting the generic CRUD functionality from the base repository.

**Generic BaseRepository**

```java
package com.beratyesbek.basicjparepositorypattern.repository.base;  
  
import com.beratyesbek.basicjparepositorypattern.model.BaseEntity;  
  
import java.util.List;  
  
public interface BaseRepository<E extends BaseEntity, I> {  
void save(E entity);  
  
void update(E entity, I id);  
  
List<E> findAll();  
  
E findById(I id);  
}
```

**Generic BaseRepositoryImpl**
```java
package com.beratyesbek.basicjparepositorypattern.repository.base;  
  
import com.beratyesbek.basicjparepositorypattern.model.BaseEntity;  
import jakarta.persistence.EntityManager;  
import jakarta.persistence.PersistenceContext;  
import org.springframework.transaction.annotation.Transactional;  
  
import java.util.List;  
  
  
public class BaseRepositoryImpl<E extends BaseEntity, I> implements BaseRepository<E, I> {  
  
@PersistenceContext  
private EntityManager entityManager;  
private final Class<E> entityClass;  
  
public BaseRepositoryImpl(Class<E> entityClass) {  
this.entityClass = entityClass;  
}  
  
@Override  
@Transactional  
public void save(E entity) {  
entityManager.persist(entity);  
}  
  
@Override  
@Transactional  
public void update(E entity, I id) {  
E result = entityManager.find((Class<E>) entity.getClass(), id);  
if (result != null) {  
entityManager.merge(result);  
}  
  
}  
  
@Override  
@Transactional  
public List<E> findAll() {  
return entityManager.createQuery("SELECT e FROM " + entityClass.getSimpleName() + " e", entityClass).getResultList();  
}  
  
@Override  
@Transactional  
public E findById(I id) {  
return entityManager.find(entityClass, id);  
}  
}
```

**UserRepository for User entity**

```java
package com.beratyesbek.basicjparepositorypattern.repository;  
  
import com.beratyesbek.basicjparepositorypattern.model.User;  
import com.beratyesbek.basicjparepositorypattern.repository.base.BaseRepository;  
  
  
public interface UserRepository extends BaseRepository<User, Integer> {  
}
```

**UserRepositoryImpl for User Entity**

```java
package com.beratyesbek.basicjparepositorypattern.repository;  
  
import com.beratyesbek.basicjparepositorypattern.model.User;  
import com.beratyesbek.basicjparepositorypattern.repository.base.BaseRepositoryImpl;  
import org.springframework.stereotype.Component;  
  
@Component  
public class UserRepositoryImpl extends BaseRepositoryImpl<User, Integer> implements UserRepository{  
  
public UserRepositoryImpl() {  
super(User.class);  
}  
}
```

##  JPA Repository Pattern

JPA entities are mapped to database tables, and each JPA repository interfaces associates with a specific JPA entity. These repositories simplify the data access layer and are defined as Java interfaces rather than classes.

```java
// Example of a Spring Data JPA repository interface
public interface MyJpaRepository extends JpaRepository<Entity, IdType> {}
```

With Spring Data JPA repositories, implementation details are abstracted away, as the framework generates the necessary code.

### JPARepository Features

- **Query DSL:** Allows the creation of queries for entities.
- **CRUD operations:** Provides standard CRUD (Create, Read, Update, Delete) methods.
- **Paging and sorting:** Supports methods for pagination and sorting of query results.
- **Helpers:** Offers various helper methods for common data access tasks.

![[Pasted image 20240212100436.png]]

each entity has its own repositories that have been extended from the JpaRepository interface in the background. The JPA repository works with EntityManager, and It works with Hibernate, which works with JDBC.

###  Hibernate Architecture

![[Pasted image 20240212100522.png]]

Hibernate has a layered architecture which helps the user perform operations without touching anything under the hood. Hibernate provides ORM for persistence service.

### **_Configuration Object_**

Usually, the Configuration Object is created once during the application lifecycle; additionally, it is the first hibernate object that is created. It represents the database and other configurations.

### **_SessionFactory Object_**

SessionFactory object is created using Configuration Object. The SessionFactory object is a heavyweight object. It is usually created when the application is initialized. Additionally, The SessionFactory is a thread-safe object and is used by other threads.

### **_Session Object_**

The session object is used to provide the database connection. It was designed as a lightweight object that is to be created each time when database interaction is required. In addition, SessionObject is not recommended to be retained for later use because it is not thread-safe.

### **_Transaction Object_**

The Transaction object is used whenever we want to perform operations on an entity, committing or rolling back changes according to the result.

### **_Query Object_**

The query object uses SQL or HQL (Hibernate Query Language) to retrieve data from the database. The query instance is obtained by calling the createQuery method that belongs to the Session object.

### **_Criteria Object_**

It usually uses dynamic queries that are obtained from Session objects.

## Hibernate Proxy

Hibernation involves two fetching-type strategies: Lazy and Eager loading. Hibernate uses Lazy loading as a default strategy, which means retrieving data until it is needed. This will enhance the performance of the application. Hibernate manages this phenomenon with Proxy Entities.

A Hibernate proxy is a way to avoid retrieving massive amounts of data until it is needed.

###  Lazy Fetch Type

 The Lazy Fetch type will enhance the application's performance if an entity contains so many relations involving massive data.
 
The lazy fetch type is managed using proxies by Hibernate. Hibernate creates a proxy for each entity. The benefit is retrieving relation data (entity) when it is called. It enhances performance. It is a valuable strategy in one-to-many, many-to-many relations if they have massive data.

Advantages:

- Much smaller initial load time than in the other approach
- Less memory consumption than in the other approach

Disadvantages:

- Delayed initialization might impact performance during unwanted moments.
- In some cases we need to handle lazily initialized objects with special care, or we might end up with an exception.

###  Eager Fetch Type

When business logic loads users from the database, JPA loads its ID, name, email, and all associated entities, such as Login History. This will come at a cost in application performance, and It consumes memory resources. Eager loading is very useful for one-to-one entity relations.

The eager fetch type retrieves data directly from the database and maps the actual entity without using any additional proxy. It might kill the performance of one-to-many or many-to-many relations. On the other hand, the eager fetch type in one-to-one relations is significantly helpful. Default is Eager in one-to-one and many-to-one.

**Advantages**:

- No delayed initialization-related performance impacts

**Disadvantages**:

- Long initial loading time
- Loading too much unnecessary data might impact performance


![[Pasted image 20240212104055.png]]

##  Hibernate Associations

Associations in programming allow us to establish relationships between different pieces of data or entities, enabling us to model and represent complex relationships in our applications. This helps in organizing and structuring data in a way that mirrors real-world connections, leading to more flexible, efficient, and maintainable code.

### One-To-One

one-to-one relation means that an entity is associated with only one entity.

![[Pasted image 20240212110014.png]]

**Product Entity**

```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
public class Product {  
  
	@Id  
	@GeneratedValue(strategy = GenerationType.IDENTITY)  
	private Integer id;  
	  
	@Column(name = "name", length = 100)  
	private String name;  
	  
	@Column(name = "quantity")  
	private Integer quantity;  
	  
	@OneToOne  
	@JoinColumn(name = "product_detail_id")  
	private ProductDetail productDetail;  
}
```

**ProductDetail Entity**

```java
	@Data  
	@Entity  
	@NoArgsConstructor  
	@AllArgsConstructor  
	public class ProductDetail {  
	
	@Id  
	@GeneratedValue(strategy = GenerationType.IDENTITY)  
	private Integer id;  
	
	@Column(name = "description", length = 1000)  
	private String description;  
	
	@Column(name = "warranty", columnDefinition = "boolean default true")  
	private Boolean warranty;  
	
	@OneToOne(mappedBy = "productDetail")  
	private Product product;  
	}
```

### Many-To-One and One-To-Many

many-to-one relation means that many entities are associated with one another entity.

![[Pasted image 20240212110442.png]]

**Product Entity**

```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
public class Product {  
  
	@Id  
	@GeneratedValue(strategy = GenerationType.IDENTITY)  
	private Integer id;  
	  
	@Column(name = "name", length = 100)  
	private String name;  
	  
	@Column(name = "quantity")  
	private Integer quantity;  
	  
	@OneToOne  
	@JoinColumn(name = "product_detail_id")  
	private ProductDetail productDetail;  
	  
	 @ManyToOne
    @JoinColumn(name = "category_id", referencedColumnName = "ID")
    private Category category;  
  
}
```

**Category Entity**

```java
@Data
@Entity
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class Category {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;

    @Column(name = "name", nullable = false, unique = true)
    private String name;


    @Column(name = "code")
    private String code;

    @OneToMany(mappedBy = "category", orphanRemoval = true, cascade = CascadeType.REMOVE)
    List<Product> products;
}
```

###  Many-To-Many

Two entities are connected in a many-to-many relationship, meaning each entity can be associated with multiple instances of the other.

![[Pasted image 20240212111956.png]]

#### FIRST OPTION, Many-To-Many

Create all entities that are connected to each other in the Hibernate App.

**Product**

```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
public class Product {  
  
	@Id  
	@GeneratedValue(strategy = GenerationType.IDENTITY)  
	private Integer id;  
	  
	@Column(name = "name", length = 100)  
	private String name;  
	  
	@Column(name = "quantity")  
	private Integer quantity;  
	  
	@OneToMany(mappedBy = "product")  
	private List<ProductTag> productTags;  
  
}
```

**Tag**

```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
public class Tag {  
  
	@Id  
	@GeneratedValue(strategy = GenerationType.IDENTITY)  
	private Integer id;  
	  
	@Column(name = "name", length = 100)  
	private String name;  
	  
	@OneToMany(mappedBy = "tag")  
	private List<ProductTag> productTags;  
}
```

**ProductTag**

```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
public class ProductTag {  
  
	@Id  
	@GeneratedValue(strategy = GenerationType.IDENTITY)  
	private Integer id;  
	  
	@ManyToOne  
	@JoinColumn(name = "product_id")  
	private Product product;  
	  
	@ManyToOne  
	@JoinColumn(name = "tag_id")  
	private Tag tag;  
}
```

#### The Second Option with an Inverse Join Column, Many-to-Many

In JPA, when we are dealing with Many-to-Many associations between entities, we often use a join table to represent the relationship. This join table typically consists of foreign keys that refer to the primary keys of the associated entities.

the **_@JoinTable_** annotation. In the **_@JoinTable_** annotation, we have two properties related to foreign keys: **_joinColumns_** and **_inverseJoinColumns_**.

**_joinColumns:_** This property defines the foreign key column in the join table that references the primary key of the owning entity. It specifies the columns in the join table that represent the current entity Product.

**_inverseJoinColumns_**: This property defines the foreign key column in the join table that references the primary key of the target entity. It specifies the columns in the join table that represent the associated entity.


**Product**
```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
public class Product {  
  
@Id  
@GeneratedValue(strategy = GenerationType.IDENTITY)  
private Integer id;  
  
@Column(name = "name", length = 100)  
private String name;  
  
@Column(name = "quantity")  
private Integer quantity;  
  
@OneToOne  
@JoinColumn(name = "product_detail_id")  
private ProductDetail productDetail;  
  
@ManyToOne  
@JoinColumn(name = "color_id")  
private Color color;  
  
@ManyToMany  
@JoinTable(  
name = "product_tag",  
joinColumns = @JoinColumn(name = "product_id", referencedColumnName = "id"),  
inverseJoinColumns = @JoinColumn(name = "tag_id", referencedColumnName = "id")  
)  
private List<Tag> tags;  
}
```

## CASCADE TYPES

Cascade types are responsible for ensuring that an entity instance relies on another entity instance. An entity depends on another entity. For instance, a Product will be pointless without Product Details. Cascade Types are used when a Product is created then Product Details must be created simultaneously, or a Product is deleted, then Product Details must be deleted simultaneously.

JPA allows the propagation of entity state changes from parents to child entities, known as cascading. The `cascade` configuration option accepts an array of `CascadeTypes`.

### Cascade Types

1. **CascadeType.PERSIST**: Save() or persist() operations cascade to related entities.
2. **CascadeType.MERGE**: Related entities are merged when the owning entity is merged.
3. **CascadeType.REFRESH**: Child entity also gets reloaded from the database whenever the parent entity is refreshed.
4. **CascadeType.REMOVE**: Propagates the remove operation from parent to child entity.
5. **CascadeType.DETACH**: Detach all child entities if a "manual detach" occurs for the parent.
6. **CascadeType.ALL**: Shorthand for all of the above cascade operations.

### CascasdeType.ALL

It admits to performing all operations on related entities. For instance, when a persistent operation is performed on a Product entity, it will affect other related entities that have been established within the Product. (Delete, Update, Create, etc.)

### CascasdeType.PERSIST

It admits to performing a persistent operation on the related entity, such as create. When a Product entity is created, Product Details will be created before the creation of the Product. Why? Because the Product entity table involves product_detail_id, clearly without Product Detail ID, Hibernate is not able to save the product. Therefore, the Product Detail must be created before the Product entity. (persist operations)

### CascasdeType.MERGE

CascadeType.MERGE specifies that when a merge operation is performed on an entity, the same operation should be applied to its associated entities as well. In other words, if an entity is merged, any changes made to its state will also be propagated to its related entities that have CascadeType.MERGE specified. This ensures consistency and coherence among related entities when changes are made at the top level. (Update operations)

### CascasdeType.REMOVE

As the name implies, it admits to performing a remove operation on the related entity. For instance, when a Product entity is deleted, the Product Details entity will be deleted simultaneously. There is another type which is specified and provided by Hibernate, which is CascadeType.DELETE. There is no discrepancy among them.

##  Orphan Removal

It is a property in relational annotations, meaning that if the parent entity has no reference, remove the child entity.

![[Pasted image 20240212123942.png]]

you have a product, and this product has images. When you want to remove the product from the database, you must remove the images connected to each other with a Foreign Key. How can you provide this in Spring Boot in a simple way? You can create an Image and Product Repository. And you can call the repositories in a service. In the service, you can remove the images that are related to this product using Product ID, and then you can remove the Product. Luckily, we have an Orphan Removal property that removes child entities if references are no longer available.

##  Hibernate Inheritance, Composite PK

Hibernate Inheritance is a method of reflecting and creating tables into OOP classes according to Table or Column.

### MappedSupperClass

***This type is used to capsulate common values in one class***. It has no Entity annotation because this is not an entity. It just involves common values for each sub-class, such as ``BaseEntity``; you might have some data that contains sub-classes; you can put them together at a parent class using a **_@MappedSuperClass_** annotation.

![[Pasted image 20240221123450.png]]

```java
import lombok.Data;  
  
import javax.persistence.*;  
import java.time.OffsetDateTime;  
  
@Data  
@MappedSuperclass  
public abstract class BaseEntity{  
  
private static final Boolean DEFAULT_DELETED = false;  
  
@Id  
@Column(name = "id")  
@GeneratedValue(strategy = GenerationType.SEQUENCE)  
protected Integer id;  
  
@Column(name = "created_at", nullable = false, updatable = false)  
protected OffsetDateTime createdAt;  
  
@Column(name = "updated_at", nullable = false)  
protected OffsetDateTime updatedAt;  
  
protected Boolean deleted = DEFAULT_DELETED;  
  
@Version  
@Column(name = "version")  
protected Long version;  
  
@PrePersist  
public void prePersist() {  
this.createdAt = OffsetDateTime.now();  
this.updatedAt = OffsetDateTime.now();  
}  
  
@PreUpdate  
public void preUpdate() {  
this.updatedAt = OffsetDateTime.now();  
}  
  
}
```

**Product Class**

```java
@Data  
@Entity  
@Builder  
@NoArgsConstructor  
@AllArgsConstructor  
public class Product extends BaseEntity {  
  
@Id  
@GeneratedValue(strategy = GenerationType.IDENTITY)  
private Integer id;  
  
private String name;  
}
```

### SINGLE TABLE

Hibernate creates one table for each entity that is signed with **_@Inheritance_** annotation and as an **_``InheritanceType.SINGLE_TABLE``_**. When the client calls the repository, hibernate maps related to the columns to the related class. This feature could be very useful in some cases. For instance, you have public and private machines, and you want to separate two machines from each other. Each machine has its own properties. In this case, the single table will be entirely useful.

![[Pasted image 20240221124553.png]]

```java
@Entity  
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)  
public abstract class Machine {  
@Id  
@GeneratedValue(strategy = GenerationType.IDENTITY)  
private Long id;  
private String name;  
}  
  
@Entity  
public class PublicMachine extends Machine {  
// other prop  
}  
  
@Entity  
public class PrivateMachine extends Machine {  
// other prop  
}
```

### Discriminator Column and Value

The discriminator is such a helpful feature for most cases in Hibernate. For instance, you have two **_accessor_type_** users, such as **_root_** and **_regular_**. You want to retrieve them from the database and separate different classes with different values.

```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)  
@DiscriminatorColumn(name = "accessor_type", discriminatorType = DiscriminatorType.STRING)  
public class MachineAccessor {  
@Id  
@GeneratedValue(strategy = GenerationType.IDENTITY)  
private Integer id;  
private String name;  
private String ipAddress;  
private String macAddress;  
}  
  
@Entity  
@DiscriminatorValue("regular_machine")  
public class RegularMachineAccessor extends MachineAccessor {  
private String ippAddress;  
private String macAddress;  
private List<String> logHistory;  
}  
  
@Data  
@Entity  
@DiscriminatorValue("root_machine")  
public class RootMachineAccessor extends MachineAccessor {  
private String rootPassword;  
private String rootUsername;  
private String rootIpAddress;  
private String rootMacAddress;  
}
```

### **JOINED TABLE**

In this strategy, each class in the hierarchy is mapped to its own table in the database. The tables are linked together through foreign key relationships to represent the inheritance relationships between the classes. The superclass table contains common properties, while the subclass tables contain properties specific to each subclass.

```java
@Entity  
@Inheritance(strategy = InheritanceType.JOINED)  
public class Payment {  
  
@Id  
@GeneratedValue(strategy = GenerationType.IDENTITY)  
private Integer id;  
private BigDecimal amount;  
private String currency;  
private String method;  
}  
  
@Entity  
public class BitcoinProvider extends Payment {  
private String bitcoinAddress;  
private String bitcoinWallet;  
private String bitcoinProviderName;  
}  
  
@Entity  
@PrimaryKeyJoinColumn(name = "paypal_id")  
public class PaypalProvider extends Payment {  
private String paypalEmail;  
private String paypalPassword;  
private String paypalProviderName;  
}
```

## **COMPOSITE PK (Composite Identifier)**

There is another way in hibernate to define a primary key, combining two columns as a primary key. This phenomenon is called Composite PK or Composite Identifier. In hibernate, Composite PK is defined using **_@EmbeddedId_** and **_@Embeddable_** annotation. This allows us to provide some benefits, such as increasing simplicity and performance; on the other hand, it comes with complexity and maintenance problems.

```sql
create table "user" (  
email varchar(255) not null,  
user_type varchar(255) not null,  
name varchar(255),  
primary key (email, user_type)  
)
```

**_UserID_**

```java
@Embeddable  
@NoArgsConstructor  
@AllArgsConstructor  
public class UserId implements Serializable {  
private String email;  
private String userType;  
}
```

**_USER_**

```java
@Data  
@Entity  
@NoArgsConstructor  
@AllArgsConstructor  
@Table(name = "users")  
public class User {  
  
@EmbeddedId  
private UserId userId;  
  
private String name;  
}
```

## Hibernate Cache

Hibernate access to the database for each request. This comes at a time-consuming cost. Hibernate’s developers built a two-level caching mechanism to prevent this time-consuming process for each request. Additionally, this two-level cache mechanism steadily upturns response time performance.

### **Architecture**

![[Pasted image 20240306115520.png]]

### Hibernate Cache Level - 1

The first-level cache is automatically enabled and operates within the scope of a Session object. When an entity is fetched from the database, it is cached in the Session (Persistence Context). If the same entity is requested again within the same Session, Hibernate retrieves it from the cache instead of the database. However, once the Session is closed (typically at the end of a transaction), attempting to access an entity will result in an exception, as the Session is no longer available to retrieve the entity from the cache. Hibernate manages the first-level cache automatically, so there is no need for explicit configuration.

![[Pasted image 20240306115657.png]]

### Hibernate Cache Level - 2

In concurrent processes, it’s crucial to manage how objects are shared between sessions. Hibernate’s first-level cache, specific to each session, helps maintain data integrity by ensuring that objects are not shared inappropriately between different sessions.

The second-level cache, on the other hand, is an optional feature in Hibernate that stores the state of persistent entities, making it available across sessions. When a client requests an entity, Hibernate first checks the first-level cache within the current session. If the entity is not found there, Hibernate then checks the second-level cache. If the entity is not found in either cache, Hibernate loads it from the database, caches it in both levels and returns it to the client.

while the first-level cache is essential for session-specific object management, the second-level cache provides a shared cache mechanism for entities, improving performance by reducing the need for repeated database queries in concurrent environments.

![[Pasted image 20240306115843.png]]

**implement dependencies**

```gradle
implementation 'org.hibernate.orm:hibernate-jcache:6.2.7.Final'  
implementation('org.ehcache:ehcache:3.10.8') {  
capabilities {  
requireCapability('org.ehcache:ehcache-jakarta')  
}  
}  
implementation 'org.hibernate:hibernate-core:6.2.5.Final'
```

**Configure** **``application.properties``**

```application.properties
spring.jpa.properties.javax.cache.provider=org.ehcache.jsr107.EhcacheCachingProvider  
spring.jpa.properties.javax.cache.uri=classpath:ehcache.xml  
spring.jpa.properties.hibernate.cache.use_query_cache=true  
spring.jpa.properties.hibernate.cache.use_second_level_cache=true  
spring.jpa.properties.hibernate.cache.region.factory_class=jcache
```

create a file “**_ecache.xml_**” under the “**_src/main/resources/_**” folder

```xml
<config xmlns='http://www.ehcache.org/v3'>  
<cache alias="default-query-results-region">  
<expiry>  
<ttl unit="minutes">30</ttl>  
</expiry>  
<heap>1000</heap>  
</cache>  
  
<cache alias="default-update-timestamps-region">  
<expiry>  
<none/>  
</expiry>  
<heap>1000</heap>  
</cache>  
<cache alias="com.beratyesbek.youtubehibernate.entity.Category">  
<expiry>  
<ttl unit="minutes">100</ttl>  
</expiry>  
<heap>1000</heap>  
</cache>  
</config>
```

```java
import jakarta.persistence.*;  
import lombok.AllArgsConstructor;  
import lombok.Builder;  
import lombok.Data;  
import lombok.NoArgsConstructor;  
import org.hibernate.annotations.Cache;  
import org.hibernate.annotations.CacheConcurrencyStrategy;  
  
  
@Data  
@Entity  
@Builder  
@NoArgsConstructor  
@AllArgsConstructor  
@Cacheable  
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)  
public class Category {  
  
@Id  
@GeneratedValue(strategy = GenerationType.IDENTITY)  
private Integer id;  
  
@Column(name = "name", nullable = false, unique = true)  
private String name;  
  
@Column(name = "code")  
private String code;  
  
}
```

### Hibernate Cache Level - 3 (Query Hint)

The concept of the Query cache is straightforward: Hibernate checks if a query’s result is already cached. If the result is found in the cache, Hibernate retrieves it. If the result is not cached, Hibernate executes the query, caches the result for future use, and then returns it.

Additionally, the Query cache ensures that if the underlying data changes, any previously cached data for that query is invalidated. This ensures that clients always see the most up-to-date version of the data.

![[Pasted image 20240306120253.png]]

```java
import com.beratyesbek.youtubehibernate.entity.Category;  
import jakarta.persistence.QueryHint;  
import org.springframework.data.jpa.repository.JpaRepository;  
import org.springframework.data.jpa.repository.QueryHints;  
  
import java.util.List;  
  
public interface CategoryRepository extends JpaRepository<Category, Integer> {  
  
@QueryHints({@QueryHint(name = "org.hibernate.cacheable", value = "true")})  
List<Category> findAllByCode(String code);  
}
```

The **_QueryHints_** annotation allows this method to cache results using the Hibernate query cache. This can improve performance because results can be retrieved from the cache when the same query is called again.

The **_@QueryHints_** line ensures that the results of the method’s query are cached. Cache usage is enabled by setting the value of the property named ``org.hibernate.cacheable`` to true.

### Advantages of Caching

**Improved Performance:** Caching reduces the need to fetch data from the database, which is repeatedly slower. Instead, accesses from local memory or faster data.

**Reduced Latency:** Caching reduces the latency by fetching the data from faster sources. (Memory, Redis, etc..)

**Scalability:** Caching can help improve application scalability by reducing time-response and handling more requests without overloading.

### **Disadvantages of Caching**

**Security Concerns:** Caching sensitive data can pose security risks if it is not properly managed.

**Stale Data:** Previous versions of data, when a data is updated, cache should be updated. hard to manage (ORM has their own mechanism)

### FIRST-LEVEL CACHE vs SECOND-LEVEL CACHE


![[Pasted image 20240306121256.png]]

## Query Method Syntax Examples

| Keyword            | Sample                          | JPQL Snippet                                                    |
| ------------------ | ------------------------------- | --------------------------------------------------------------- |
| And                | findByLastnameAndFirstname      | ...where x.lastname = ?1 and x.firstname = ?2                   |
| Or                 | findByLastnameOrFirstname       | ...where x.lastname = ?1 or x.firstname = ?2                    |
| Is, Equals         | findByFirstnameEquals           | ...where x.firstname = ?1                                       |
| Between            | findByStartDateBetween          | ...where x.startDate between ?1 and ?2                          |
| LessThan           | findByAgeLessThan               | ...where x.age < ?1                                             |
| LessThanEqual      | findByAgeLessThanEqual          | ...where x.age <= ?1                                            |
| GreaterThan        | findByAgeGreaterThan            | ...where x.age > ?1                                             |
| GreaterThanEqual   | findByAgeGreaterThanEqual       | ...where x.age >= ?1                                            |
| After              | findByStartDateAfter            | ...where x.startDate > ?1                                       |
| Before             | findByStartDateBefore           | ...where x.startDate < ?1                                       |
| IsNull             | findByAgeIsNull                 | ...where x.age is null                                          |
| IsNotNull, NotNull | findByAge(Is)NotNull            | ...where x.age not null                                         |
| Like               | findByFirstnameLike             | ...where x.firstname like ?1                                    |
| NotLike            | findByFirstnameNotLike          | ...where x.firstname not like ?1                                |
| StartingWith       | findByFirstnameStartingWith     | ...where x.firstname like ?1 (parameter bound with appended %)  |
| EndingWith         | findByFirstnameEndingWith       | ...where x.firstname like ?1 (parameter bound with prepended %) |
| Containing         | findByFirstnameContaining       | ...where x.firstname like ?1 (parameter bound wrapped in %)     |
| OrderBy            | findByAgeOrderByLastnameDesc    | ...where x.age = ?1 order by x.lastname desc                    |
| Not                | findByLastnameNot               | ...where x.lastname <> ?1                                       |
| In                 | findByAgeIn(Collection ages)    | ...where x.age in ?1                                            |
| NotIn              | findByAgeNotIn(Collection ages) | ...where x.age not in ?1                                        |
| True               | findByActiveTrue()              | ...where x.active = true                                        |
| False              | findByActiveFalse()             | ...where x.active = false                                       |
| IgnoreCase         | findByFirstnameIgnoreCase       | ...where UPPER(x.firstame) = UPPER(?1)                          |

# Performance Considerations

JPA is not a great candidate for massive amounts of writes to your data store. This is because JPA was designed primarily for reading and querying data, rather than for writing data.

When you use JPA to write data to the database, it first updates the in-memory representation of the entity, and then it synchronizes the changes with the database. This process involves a number of overhead costs, such as updating the entity's state in the persistence context, generating and executing SQL statements, and flushing the changes to the database. For applications that need to perform a large number of writes, these overhead costs can become significant, leading to slower performance.

## Annotations

### @EnableJpaRepositories

Used to enable the creation of repository beans from JPA repository interfaces. It scans the package of the configuration class for JPA repository interfaces and creates implementations at runtime.

### @EntityScan

Enables the scanning of entities for a Spring-based application using Java Persistence API (JPA). It scans specified packages for JPA entities, registering them with the JPA persistence provider.

### @Entity

Defines that a class can be mapped to a table. It is a marker interface, and entity classes must have a no-arg constructor and a primary key. Attributes include:

- `name`: Specifies the name of the entity.
- `table`: Specifies the name of the database table.
- `schema`: Specifies the schema that the entity's table belongs to.
- `uniqueConstraints`: Specifies unique constraints for the entity's table.

### @Id

Marks a field as the primary key of an entity.

### @GeneratedValue

Specifies how the value of a primary key field is generated. It is applied to a primary key field and includes attributes such as:

- `strategy`: Specifies the generation strategy (AUTO, IDENTITY, SEQUENCE, TABLE).

```java
@Entity
public class Book {

    @Id
    @GeneratedValue(generator = "UUID")
    @GenericGenerator(
        name = "UUID",
        strategy = "org.hibernate.id.UUIDGenerator"
    )
    private UUID id;

    // Other fields...
}
```

### @Table

Specifies the mapping of an entity to a database table. Attributes include:

- `name`: Specifies the name of the database table.
- `schema`: Specifies the schema that the table belongs to.
- `uniqueConstraints`: Specifies unique constraints for the table.

### @Column

Specifies the mapping of a field to a column in a database table. Attributes include:

- `name`: Specifies the name of the primary key column.
- `column`: Specifies the name and characteristics of the primary key column.
- `nullable`, `updatable`, `unique`, `length`, `precision`, etc.

### @Transient

Marks a field or method as non-persistent, indicating that the field won't be persisted.

### @Transactional

Defines a block of code that should be executed as a single transaction. Helps ensure consistent and reliable execution of database operations.

### @Modifying

Used with `@Query` to execute non-SELECT queries (INSERT, UPDATE, DELETE, DDL). Example:

```java
@Modifying
@Query("delete User u where u.active = false")
int deleteDeactivatedUsers();
```

### @Enumerated

Specifies whether the enum should be persisted by name or ordinal (default). Example:

```java
@Enumerated(EnumType.STRING)
private Gender gender;
```

If persisting by enum name, the `@Enumerated` annotation can be omitted, as it defaults to ordinal persistence.

# Auditing Support By Spring Data JPA

Spring Data provides robust support for auditing, allowing transparent tracking of entity creation and modification details. To leverage this functionality, entity classes should be equipped with auditing metadata, defined using annotations or by implementing an interface.

## Key Annotations for JPA Auditing

### @CreatedDate

Marks a field to be automatically populated with the timestamp when the entity is first persisted (created). Used for auditing to track creation time.

### @CreatedBy

Marks a field to be automatically populated with the identifier or username of the user who created the entity. Commonly used for auditing to track the creator.

### @LastModifiedDate

Marks a field to be automatically updated with the timestamp of the last modification made to the entity. Updated when an existing entity is modified.

### @LastModifiedBy

Marks a field to be automatically updated with the identifier or username of the user who last modified the entity. Used for auditing to track the last modifier.

Example entity class:

```java
@Entity
@EntityListeners(AuditingEntityListener.class)
public class Book {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;
    private String author;

    @CreatedDate
    private LocalDateTime createdAt;

    @LastModifiedDate
    private LocalDateTime updatedAt;

    @CreatedBy
    private String createdBy;

    @LastModifiedBy
    private String modifiedBy;

    // Constructors, getters, setters (omitted for brevity)...
}
```

### Step 2

Date-related information will be fetched from the server by JPA. For `CreatedBy` and `UpdatedBy`, we need to inform JPA how to fetch that information by implementing the `AuditorAware` interface.

```java
@Component("auditAwareImpl")
public class AuditAwareImpl implements AuditorAware<String> {

    @Override
    public Optional<String> getCurrentAuditor() {
        return Optional.ofNullable(SecurityContextHolder.getContext().getAuthentication().getName());
    }
}
```

### Step 3

Enable JPA auditing by annotating a configuration class with the `@EnableJpaAuditing` annotation.

```java
@SpringBootApplication
@EnableJpaRepositories("com.eazybytes.eazyschool.repository")
@EntityScan("com.eazybytes.eazyschool.model")
@EnableJpaAuditing(auditorAwareRef = "auditAwareImpl")
public class EazyschoolApplication {

    public static void main(String[] args) {
        SpringApplication.run(EazyschoolApplication.class, args);
    }
}
```

# Key Points Of Cascade Types

JPA allows the propagation of entity state changes from parents to child entities, known as cascading. The `cascade` configuration option accepts an array of `CascadeTypes`.

## Cascade Types

1. **CascadeType.PERSIST**: Save() or persist() operations cascade to related entities.
2. **CascadeType.MERGE**: Related entities are merged when the owning entity is merged.
3. **CascadeType.REFRESH**: Child entity also gets reloaded from the database whenever the parent entity is refreshed.
4. **CascadeType.REMOVE**: Propagates the remove operation from parent to child entity.
5. **CascadeType.DETACH**: Detach all child entities if a "manual detach" occurs for the parent.
6. **CascadeType.ALL**: Shorthand for all of the above cascade operations.

## Best Practices

- Cascading makes sense for Parent-Child associations (where the Parent entity state transition is cascaded to its Child entities).
- Cascading from Child to Parent is not recommended.
- There is no default cascade type in JPA. By default, no operation is cascaded.



# @Query Annotation in Spring Data JPA

The `@Query` annotation is used to define a query for a repository method, supporting both JPQL and native SQL queries.

## Attributes

- **value**: Specifies the query string. It can be a JPQL query or a native SQL query.
- **nativeQuery**: Indicates whether the query is a JPQL query (`false` by default) or a native SQL query (`true`).
- **countQuery**: Specifies a count query for pagination. The repository method will return a `Page` object with both data and the total number of elements.
- **countName**: Specifies the name of the count query. The default count query is derived from the main query by replacing `SELECT` with `SELECT COUNT(*)`.

```java
@Query(value = "SELECT e FROM Employee e WHERE e.lastName = :lastName",
       countQuery = "SELECT COUNT(e) FROM Employee e WHERE e.lastName = :lastName",
       countName = "countEmployeesByLastName")
Page<Employee> findByLastName(@Param("lastName") String lastName, Pageable pageable);
```
## @Param Annotation

The `@Param` annotation is used to bind a parameter to a named query. It is typically used in conjunction with the `@Query` annotation.

```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
   @Query("SELECT e FROM Employee e WHERE e.lastName = :lastName")
   List<Employee> findByLastName(@Param("lastName") String lastName);
}
```

## @Modifying Annotation

The `@Modifying` annotation indicates that a method performs a modifying query, such as an update or delete. It is used in conjunction with the `@Query` annotation for custom update or delete queries.

```java
@Modifying
@Query("UPDATE User u SET u.firstName = :firstName WHERE u.id = :id")
int updateFirstName(@Param("firstName") String firstName, @Param("id") Long id);
```

## Query Projection

Query projection allows selecting specific fields from an entity, rather than retrieving the entire entity.

### Scalar Projection

Select a single scalar value, like a column or an aggregate function.

```java
interface EmployeeRepository extends JpaRepository<Employee, Long> {
    @Query("SELECT e.name, e.email, d.name as departmentName FROM Employee e JOIN e.department d")
    List<Tuple> findEmployeeSummary();
}
```
### Dynamic Projection

Use the JPA Tuple or the Criteria API for dynamic projections.

### Interface Projection

Define a plain Java interface with getter methods for the desired fields.

```java
interface EmployeeSummary {
    String getName();
    String getEmail();
}

interface EmployeeRepository extends JpaRepository<Employee, Long> {
    @Query("SELECT e.name, e.email FROM Employee e")
    List<EmployeeSummary> findEmployeeSummary();
}
```
These annotations and techniques enhance the flexibility and efficiency of querying with Spring Data JPA.

## Püf Nokta I
1:1 ve M:1 ilişkiler de dahil olmak üzere bütün ilişkileri LAZY tanımlayın.

## Püf Nokta II
1:M ilişkileri her zaman için çift yönlü tanımlayın, ilişkiyi sadece M:1 tarafından yönetin. 1:M ilişkileri sadece sorgularda kullanın.

## Püf Nokta III
M:N ilişkileri, aradaki "association table" için ayrı bir entity tanımlayarak iki tane çift yönlü 1:M ilişki şeklinde ele alın.

## Püf Nokta IV
Cascade'i sadece 1:M ve 1:1 ilişkilerde ve gerçekten hangi işlemlerin cascade etmesini istiyorsanız sadece onlar için kullanın.

## Püf Nokta V
Embedded/Embeddable yerine her zaman için Entity kullanın.

## Püf Nokta VI
Derin inheritance hiyerarşilerinden kaçının, mümkün olduğunca bütün hiyerarşi için "tek tablo" (SINGLE_TABLE) yönetimini tercih edin.

## Püf Nokta VII
Bileşke PK yönetiminden uzak durun. Sentetik PK kullanın.

## Püf Nokta VIII
Nümerik PK değeri ile çalışacaksanız, sentetik PK üretme yöntemlerinden SEQUENCE'i tercih edin.

## Püf Nokta IX
Entity sınıfların equals ve hashCode metotlarını implement ederken Hibernate proxy ile çalışma ihtimaline karşın attribute değerlerine her zaman getter metotlar vasıtası ile erişin.

## Püf Nokta XI
LazyInitializationException probleminin en iyi çözüm yolu "fetch join"dir.

## Püf Nokta XII
Prod ortamında detached uninitialized lazy ilişkilerle veya proxy'lerden dolayı lazy hatası almamak için hibernate.enable_lazy_load_no_trans property=TRUE yapın.

## Püf Nokta XIII
Entity düzeyinde ikincil önbellek (second level cache) kullanıyorsanız, bu entity'nin 1:1 ve M:1 ilişkili hedef entity'lerini ya LAZY yapın, yada bunları da önbellek kontrolüne dahil etmeyi unutmayın.

## Püf Nokta XIV
1:M ve M:N ilişkilerde ikincil önbellek kullanıyorsanız, ilişkinin hedef entity'sini de entity düzeyinde önbellek kontrolüne dahil etmeyi unutmayın.

## Püf Nokta XV
Sorgularda önbellek kullanırsanız ve sorgu sonucunda entity dönülüyorsa hedef entity'yi de önbellek kontrolüne dahil etmeyi unutmayın.

---

# EXCEPTION HANDLING IN SPRING

## `@ControllerAdvice`
- Used to create a global exception handler for multiple controllers.
- Centralizes exception handling across all controllers in a single class.

## `@ExceptionHandler`
- Specifies a method that will handle a specific exception thrown by a controller.
- Can be used at the class or method level to make exception handling specific to a controller or method.

## `ResponseEntityExceptionHandler`
- Provides a base class for creating global exception handlers for a Spring REST application.
- Abstract class implementing the `HandlerExceptionResolver` interface.

## `@ResponseStatus`
- Sets the HTTP status code of the response when a specific exception is thrown.
- Used in conjunction with custom exception classes.

### Example Custom Exception Class:
```java
@ResponseStatus(value = HttpStatus.NOT_FOUND, reason = "User Not found")
public class UserNotFoundException extends RuntimeException {
}
```

### Example Usage in a Method:

```java
private User findUser(int id) {
    return userList.stream()
            .filter(user -> user.getId().equals(id))
            .findFirst()
            .orElseThrow(() -> new UserNotFoundException());
}
```

## `@RestControllerAdvice`

- A specialization of `@ControllerAdvice` combined with `@ResponseBody`.
- Centralizes exception handling across all RESTful web services controllers in a single class.
- Returns a `ResponseEntity` object containing the error response.

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class CustomerNotFoundException extends RuntimeException {
    public CustomerNotFoundException(String s) {
        super(s);
    }
}

@RestControllerAdvice
public class GeneralExceptionHandler extends ResponseEntityExceptionHandler {
    // Exception handling methods go here
    
    @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex,
                                                                  HttpHeaders headers,
                                                                  HttpStatus status,
                                                                  WebRequest request) {
        // Custom handling for MethodArgumentNotValidException
        return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
    }
    
    @ExceptionHandler(CustomerNotFoundException.class)
    public ResponseEntity<?> handle(CustomerNotFoundException exception) {
        return new ResponseEntity<>(exception.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

## VALIDATION

# Bean Validation API Annotations

## Nullability Checks:
- `@Null`: Value must be null.
- `@NotNull`: Value must not be null.

## String Checks:
- `@Pattern`: Value must match the specified RegEx pattern.
- `@NotEmpty`: Value must not be null or empty.
- `@NotBlank`: Value must not be null, empty, or whitespace.

## Email Validation:
- `@Email`: Value must be a valid email format.

## Boolean Checks:
- `@AssertTrue`: Value must be true.
- `@AssertFalse`: Value must be false.

## Numeric Range Checks:
- `@Min`: Value must be greater than or equal to the specified minimum.
- `@Max`: Value must be less than or equal to the specified maximum.
- `@Negative`: Value must be negative.
- `@NegativeOrZero`: Value must be negative or zero.
- `@Positive`: Value must be positive.
- `@PositiveOrZero`: Value must be positive or zero.

## Collection/Array Size Checks:
- `@Size`: Size of the collection or array must be within the specified range.

## Date/Time Validation:
- `@Past`: Date must be in the past.
- `@PastOrPresent`: Date must be in the past or present.
- `@Future`: Date must be in the future.
- `@FutureOrPresent`: Date must be in 


### Example:

```java
@Data
@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    @NotNull
    @Size(min = 2, message = "Must be not null")
    private String nameSurname;

    @Max(value = 99999)
    @Positive
    private int studentNumber;

    @NotBlank(message = "Must be not blank")
    private String schoolName;

    @Email(message = "Email should be valid")
    private String email;

    @Min(value = 18, message = "Cannot be younger than 18 years old.")
    private int age;

    @Pattern(regexp = "[0-9\\s]{12}")
    private String phone;
}

@Valid
@RestController
public class UserController {
    public void createUser(@Valid User user) {
        // Handle the user creation
    }
}

@Validated
@RestController
public class UserController {
    public void createUser(@Validated(CreateUser.class) User user) {
        // Handle the user creation
    }
}
```

## Spring MVC Custom Validation

### Step 1: Create a Validation Annotation

```java
@Target({ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = CustomValidator.class)
public @interface CustomValidation {
    String message() default "Invalid value";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}
```

### Step 2: Implement the Custom Validator

```java
public class CustomValidator implements ConstraintValidator<CustomValidation, String> {
    @Override
    public void initialize(CustomValidation constraintAnnotation) {
        // Initialization if needed
    }

    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        // Add your custom validation logic here
        // Return true if valid, false otherwise
    }
}
```

### Step 3: Apply the Custom Annotation

```java
public class User {
    @CustomValidation
    private String username;
    
    // Other fields, getters, and setters
}
```

### Step 4: Enable Validation in Spring Configuration

```java
@Configuration
@EnableWebMvc
public class WebMvcConfig implements WebMvcConfigurer {
    // Configuration details here
}
```

### RestTemplate Configuration

```java
@Configuration
public class RestTemplateConfig {

    // Creates a prototype-scoped RestTemplate bean
    @Bean
    @Scope("prototype")
    public RestTemplate createRestTemplate() {
        return new RestTemplate();
    }

    // Configures a RestTemplate bean with specific timeout settings
    @Bean
    public RestTemplate restTemplate(RestTemplateBuilder builder) {
        return builder
                .setConnectTimeout(Duration.ofMillis(3000))
                .setReadTimeout(Duration.ofMillis(3000))
                .build();
    }
}
```

### RestTemplate Usage

```java
@RestController
public class CharacterController {

    @Autowired
    private RestTemplate restTemplate;

    @Autowired
    private HttpHeaders httpHeaders;

    private static final String CHARACTER_API = "https://api.example.com/characters";

    @GetMapping("/characters")
    public Character getAllCharacters() {
        httpHeaders.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
        HttpEntity<String> entity = new HttpEntity<>(httpHeaders);

        // Executes a GET request and returns a ResponseEntity with Character as the response body
        ResponseEntity<Character> response = restTemplate.exchange(CHARACTER_API, HttpMethod.GET, entity, Character.class);

        return response.getBody();
    }
}
```

### Scheduled Tasks Configuration

```java
@Configuration
@EnableScheduling
public class SchedulingConfig {

    // Executes the task every 5 seconds with a fixed delay after the completion of the previous execution
    @Scheduled(fixedDelay = 5000)
    public void scheduledTaskWithFixedDelay() {
        // Task logic
    }

    // Executes the task every 10 seconds at a fixed rate
    @Scheduled(fixedRate = 10000)
    public void scheduledTaskWithFixedRate() {
        // Task logic
    }

    // Executes the task every day at 2:00 AM based on a cron expression
    @Scheduled(cron = "0 0 2 * * ?")
    public void scheduledTaskWithCronExpression() {
        // Task logic
    }

    // Executes the task every hour using a cron macro
    @Scheduled(cron = "@hourly")
    public void scheduledTaskWithCronMacro() {
        // Task logic
    }
}
```

In the RestTemplate configuration, I've separated the creation of a prototype-scoped RestTemplate bean and the configuration of RestTemplate with timeout settings into a dedicated configuration class.

In the RestTemplate usage example, I've demonstrated how to inject the RestTemplate bean into a controller and use it to perform a GET request to a RESTful API endpoint.

In the scheduled tasks configuration, I've shown how to configure scheduled tasks using `@Scheduled` annotation with different parameters for fixed delay, fixed rate, and cron expressions. Each scheduled task has its corresponding method with task logic.

---

# TEST

### Test Strategies in Software Development

Software testing involves various strategies to ensure the reliability and correctness of code. Different levels of testing serve distinct purposes in the development process.

#### 1. **Unit Testing**

- **Definition:** Testing individual units or components of a software independently.
- **Approaches:**
    - **No Unit Testing:** Not recommended but might occur due to time constraints or project pressures.
    - **Strict Unit Testing:** Comprehensive testing of almost every method, regardless of complexity.
    - **Selective Unit Testing:** Prioritizing unit tests based on complexity and criticality.

```java
@Test
public void testMyMethod() {
    // Test code goes here
}
```

#### **Integration Testing**

- **Definition:** Testing the interaction between different components or systems.
- **Approach:**
    - **After Integration:** Testing modules after they are integrated.
    - **Big Bang Integration:** Combining all modules simultaneously.
    - **Continuous Integration:** Regularly integrating and testing components.

#### 3. **Module Testing**

- **Definition:** Testing individual modules or independent units of code.
- **Approach:**
    - **Comprehensive Module Testing:** Testing all modules thoroughly.
    - **Selective Module Testing:** Prioritizing critical modules.

#### 4. **Best Practices for Unit Testing**

- **Separation of Source Code and Test Classes:** Keep test classes separate from the main source code for independent development, execution, and maintenance.
    
- **Package Naming Convention:** Match the package of the test class with the package of the source class it tests.
    
- **Test Case Naming Convention:** Follow clear and consistent guidelines for naming test cases.
    
- **Use Descriptive Names:** Use names that clearly explain what the test is testing.
    
- **Camel Case Naming:** Apply camel case naming conventions for readability.
    
- **Use Prefix/Suffix for Test Type:** Indicate the test type with a prefix or suffix.
    
- **Numbering System:** Use a numbering system for multiple test cases related to the same functionality.
    
- **Describe in Given-When-Then Format:** Use the given_when_then format to describe the purpose of a unit test.

```java
@Test
public void givenRadius_whenCalculateArea_thenReturnArea() {
    //...
}
```

- **Expected vs Actual:** Clearly distinguish between expected and actual results in assertions.
    
- **Prefer Simple Test Cases:** Write simple, focused test cases rather than complex ones.
    
- **Appropriate Assertions:** Use proper assertions relevant to the test case.
    
- **Specific Unit Tests:** Create separate test cases for specific scenarios instead of adding multiple assertions to a single test.
    
- **Test Production Scenarios:** Write tests considering real-world scenarios to ensure relatability.
    
- **Mock External Services:** Mock external services to focus on the logic and execution of the code.
    
- **Avoid Code Redundancy:** Create helper functions to avoid redundant code in test cases.
    
- **Annotations:** Leverage annotations to prepare the system for tests.
    
- **80% Test Coverage:** Aim for 80% code coverage by unit tests.
    
- **TDD Approach:** Embrace Test-Driven Development for creating test cases before and during implementation.
    
- **Automation:** Automate test suite execution to catch regressions and ensure rapid feedback.


### Spring Testing Annotations and Libraries

#### 1. **`@SpringBootTest`**

- **Purpose:** Loads the entire Spring application context for integration testing.
- **Usage:** Bootstrap the entire container for comprehensive testing.
- **Example:**

```java
@SpringBootTest
public class MyIntegrationTest {
    // Test methods
}
```

#### 2. **`@TestPropertySource`**

- **Purpose:** Loads specific properties for testing.
- **Usage:** Define property sources with higher precedence than other sources.
- **Example:**

```java
@TestPropertySource(locations = "/other-location.properties",
    properties = "baeldung.testpropertysource.one=other-property-value")
```

#### 3. **`@Sql`**

- **Purpose:** Specifies SQL scripts to be executed before or after a test method or class.
- **Usage:** Set up the database for controlled environment testing.
- **Example:**

```java
@Sql({"/employees_schema.sql", "/import_employees.sql"})
public class SpringBootInitialLoadIntegrationTest {
    // Test methods
}
```

#### 4. **`@BeforeEach`**

- **Purpose:** JUnit 5 annotation executed before each test method.
- **Usage:** Set up common code before running each test.
- **Example:**

```java
@BeforeEach
public void setUp() {
    // Common setup code
}
```

#### 5. **`@DataJpaTest`**

- **Purpose:** Lightweight testing context for JPA components.
- **Usage:** Focus on testing the persistence layer.
- **Example:**

```java
@DataJpaTest
public class MyDataJpaTest {
    // Test methods
}
```

#### 6. **Mockito and BDDMockito**

- **Purpose:** Create mock objects for isolating dependencies.
- **Usage:** Define expectations and behaviors for mock objects.
- **Example:**

```java
when(mockDependency.someMethod()).thenReturn("Mocked result");

given(mockDependency.someMethod()).willReturn("Mocked result");
```

#### 7. **`@MockBean`**

- **Purpose:** Create a mock object of a bean in the Spring application context.
- **Usage:** Mock specific beans in integration tests.
- **Example:**

```java
@MockBean
private MyDependency mockDependency;
```

#### 8. **`@ExtendWith`**

- **Purpose:** JUnit 5 annotation to add extra features or behaviors to tests.
- **Usage:** Include custom or built-in extensions.
- **Example:**

```java
@ExtendWith(MockitoExtension.class)
public class MyTest {
    // Test methods
}
```

#### 9. **`@Mock`**

- **Purpose:** Mockito annotation to create a mock object.
- **Usage:** Mark a field as a mock for more readable tests.
- **Example:**

```java
@Mock
private MyDependency mockDependency;
```

#### 10. **`@InjectMocks`**

- **Purpose:** Inject mock objects into the fields of the class under test.
- **Usage:** Automatically populate dependencies with mock objects.
- **Example:**

```java
@InjectMocks
private MyUnit myUnit;
```

#### 11. **`@WebMvcTest`**

- **Purpose:** Create a slice of the Spring context focusing on the web layer.
- **Usage:** Test Spring MVC controllers and related components.
- **Example:**

```java
@WebMvcTest(MyController.class)
public class MyControllerTest {
    // Test methods
}
```

#### 12. **`MockMvc`**

- **Purpose:** Simulate HTTP requests and responses for Spring MVC controller testing.
- **Usage:** Test controller logic in isolation without deploying the entire application.
- **Example:**

```java
MockMvc mockMvc = MockMvcBuilders.standaloneSetup(myController).build();
```

#### 13. **`Mockito.when`**

- **Purpose:** Specify the behavior of a mock object using Mockito.
- **Usage:** Define expected behaviors for mock objects.
- **Example:**

```java
Mockito.when(mockDependency.someMethod()).thenReturn("Mocked result");
```

#### 14. **`TestContainers` and `@DynamicPropertySource`**

- **Purpose:** Manage lightweight, disposable containers for integration testing.
- **Usage:** Run application dependencies in isolated environments.
- **Example:**

```java
@DynamicPropertySource
public static void dynamicPropertySource(DynamicPropertyRegistry registry){
    registry.add("spring.datasource.url", MY_SQL_CONTAINER::getJdbcUrl);
    registry.add("spring.datasource.username", MY_SQL_CONTAINER::getUsername);
    registry.add("spring.datasource.password", MY_SQL_CONTAINER::getPassword);
}
```


# Persistence(Repository) Layer Test

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;
import java.util.Optional;

import static org.assertj.core.api.Assertions.assertThat;

@DataJpaTest
@Transactional
public class EmployeeRespositoryTests {

    @Autowired
    private EmployeeRepository employeeRepository;

    private Employee employee;

    @BeforeEach
    public void setup() {
        employee = Employee.builder()
                .firstName("Ramesh")
                .lastName("Ramesh")
                .email("ramesh@gmail,com")
                .build();
    }

    @Test
    public void saveEmployee_shouldReturnSavedEmployee() {
        Employee savedEmployee = employeeRepository.save(employee);
        assertThat(savedEmployee).isNotNull();
        assertThat(savedEmployee.getId()).isGreaterThan(0);
    }

    @Test
    @DisplayName("Get all employees operation")
    public void givenEmployeesList_whenFindAll_thenEmployeesList() {
        Employee employee1 = Employee.builder()
                .firstName("John")
                .lastName("Cena")
                .email("cena@gmail,com")
                .build();

        employeeRepository.save(employee);
        employeeRepository.save(employee1);

        List<Employee> employeeList = employeeRepository.findAll();

        assertThat(employeeList).isNotNull();
        assertThat(employeeList.size()).isEqualTo(2);
    }

    @Test
    @DisplayName("Get employee by id operation")
    public void givenEmployeeObject_whenFindById_thenReturnEmployeeObject() {
        employeeRepository.save(employee);
        Employee employeeDB = employeeRepository.findById(employee.getId()).get();
        assertThat(employeeDB).isNotNull();
    }

    @Test
    @DisplayName("Get employee by email operation")
    public void givenEmployeeEmail_whenFindByEmail_thenReturnEmployeeObject() {
        employeeRepository.save(employee);
        Employee employeeDB = employeeRepository.findByEmail(employee.getEmail()).get();
        assertThat(employeeDB).isNotNull();
    }

    @Test
    @DisplayName("Update employee operation")
    public void givenEmployeeObject_whenUpdateEmployee_thenReturnUpdatedEmployee() {
        employeeRepository.save(employee);
        Employee savedEmployee = employeeRepository.findById(employee.getId()).get();
        savedEmployee.setEmail("ram@gmail.com");
        savedEmployee.setFirstName("Ram");
        Employee updatedEmployee = employeeRepository.save(savedEmployee);
        assertThat(updatedEmployee.getEmail()).isEqualTo("ram@gmail.com");
        assertThat(updatedEmployee.getFirstName()).isEqualTo("Ram");
    }

    @Test
    @DisplayName("Delete employee operation")
    public void givenEmployeeObject_whenDelete_thenRemoveEmployee() {
        employeeRepository.save(employee);
        employeeRepository.deleteById(employee.getId());
        Optional<Employee> employeeOptional = employeeRepository.findById(employee.getId());
        assertThat(employeeOptional).isEmpty();
    }

    // Additional Tests for Custom Queries

    @Test
    @DisplayName("Custom query using JPQL with index")
    public void givenFirstNameAndLastName_whenFindByJPQL_thenReturnEmployeeObject() {
        employeeRepository.save(employee);
        String firstName = "Ramesh";
        String lastName = "Fadatare";
        Employee savedEmployee = employeeRepository.findByJPQL(firstName, lastName);
        assertThat(savedEmployee).isNotNull();
    }

    @Test
    @DisplayName("Custom query using JPQL with Named params")
    public void givenFirstNameAndLastName_whenFindByJPQLNamedParams_thenReturnEmployeeObject() {
        employeeRepository.save(employee);
        String firstName = "Ramesh";
        String lastName = "Fadatare";
        Employee savedEmployee = employeeRepository.findByJPQLNamedParams(firstName, lastName);
        assertThat(savedEmployee).isNotNull();
    }

    @Test
    @DisplayName("Custom query using native SQL with index")
    public void givenFirstNameAndLastName_whenFindByNativeSQL_thenReturnEmployeeObject() {
        employeeRepository.save(employee);
        Employee savedEmployee = employeeRepository.findByNativeSQL(employee.getFirstName(), employee.getLastName());
        assertThat(savedEmployee).isNotNull();
    }

    @Test
    @DisplayName("Custom query using native SQL with named params")
    public void givenFirstNameAndLastName_whenFindByNativeSQLNamedParams_thenReturnEmployeeObject() {
        employeeRepository.save(employee);
        Employee savedEmployee = employeeRepository.findByNativeSQLNamed(employee.getFirstName(), employee.getLastName());
        assertThat(savedEmployee).isNotNull();
    }
}
```

# Buisness(Service) Layer Test

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import java.util.Collections;
import java.util.List;
import java.util.Optional;

import static org.assertj.core.api.Assertions.assertThat;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.BDDMockito.given;
import static org.mockito.BDDMockito.willDoNothing;
import static org.mockito.Mockito.never;
import static org.mockito.Mockito.times;
import static org.mockito.Mockito.verify;

@ExtendWith(MockitoExtension.class)
public class EmployeeServiceTests {

    @Mock
    private EmployeeRepository employeeRepository;

    @InjectMocks
    private EmployeeServiceImpl employeeService;

    private Employee employee;

    @BeforeEach
    public void setup() {
        employee = Employee.builder()
                .id(1L)
                .firstName("Ramesh")
                .lastName("Fadatare")
                .email("ramesh@gmail.com")
                .build();
    }

    @Test
    @DisplayName("Save Employee method should return Employee object")
    public void givenEmployeeObject_whenSaveEmployee_thenReturnEmployeeObject() {
        given(employeeRepository.findByEmail(employee.getEmail())).willReturn(Optional.empty());
        given(employeeRepository.save(employee)).willReturn(employee);

        Employee savedEmployee = employeeService.saveEmployee(employee);

        assertThat(savedEmployee).isNotNull();
    }

    @Test
    @DisplayName("Save Employee method should throw ResourceNotFoundException for existing email")
    public void givenExistingEmail_whenSaveEmployee_thenThrowsException() {
        given(employeeRepository.findByEmail(employee.getEmail())).willReturn(Optional.of(employee));

        org.junit.jupiter.api.Assertions.assertThrows(ResourceNotFoundException.class, () -> {
            employeeService.saveEmployee(employee);
        });

        verify(employeeRepository, never()).save(any(Employee.class));
    }

    @Test
    @DisplayName("Get all Employees method should return Employees List")
    public void givenEmployeesList_whenGetAllEmployees_thenReturnEmployeesList() {
        Employee employee1 = Employee.builder()
                .id(2L)
                .firstName("Tony")
                .lastName("Stark")
                .email("tony@gmail.com")
                .build();

        given(employeeRepository.findAll()).willReturn(List.of(employee, employee1));

        List<Employee> employeeList = employeeService.getAllEmployees();

        assertThat(employeeList).isNotNull();
        assertThat(employeeList.size()).isEqualTo(2);
    }

    @Test
    @DisplayName("Get all Employees method should return an empty Employees List")
    public void givenEmptyEmployeesList_whenGetAllEmployees_thenReturnEmptyEmployeesList() {
        given(employeeRepository.findAll()).willReturn(Collections.emptyList());

        List<Employee> employeeList = employeeService.getAllEmployees();

        assertThat(employeeList).isEmpty();
        assertThat(employeeList.size()).isEqualTo(0);
    }

    @Test
    @DisplayName("Get Employee by Id method should return Employee Object")
    public void givenEmployeeId_whenGetEmployeeById_thenReturnEmployeeObject() {
        given(employeeRepository.findById(1L)).willReturn(Optional.of(employee));

        Employee savedEmployee = employeeService.getEmployeeById(employee.getId()).get();

        assertThat(savedEmployee).isNotNull();
    }

    @Test
    @DisplayName("Update Employee method should return Updated Employee")
    public void givenEmployeeObject_whenUpdateEmployee_thenReturnUpdatedEmployee() {
        given(employeeRepository.save(employee)).willReturn(employee);
        employee.setEmail("ram@gmail.com");
        employee.setFirstName("Ram");

        Employee updatedEmployee = employeeService.updateEmployee(employee);

        assertThat(updatedEmployee.getEmail()).isEqualTo("ram@gmail.com");
        assertThat(updatedEmployee.getFirstName()).isEqualTo("Ram");
    }

    @Test
    @DisplayName("Delete Employee method should do nothing")
    public void givenEmployeeId_whenDeleteEmployee_thenNothing() {
        long employeeId = 1L;

        willDoNothing().given(employeeRepository).deleteById(employeeId);

        employeeService.deleteEmployee(employeeId);

        verify(employeeRepository, times(1)).deleteById(employeeId);
    }
}
```


# Controller (View) Layer Test

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.ResultActions;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import static org.hamcrest.Matchers.is;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.BDDMockito.given;
import static org.mockito.BDDMockito.willAnswer;
import static org.mockito.Mockito.doNothing;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@WebMvcTest(EmployeeController.class)
public class EmployeeControllerTests {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private EmployeeService employeeService;

    @Autowired
    private ObjectMapper objectMapper;

    private Employee employee;

    @BeforeEach
    public void setup() {
        employee = Employee.builder()
                .firstName("Ramesh")
                .lastName("Fadatare")
                .email("ramesh@gmail.com")
                .build();
    }

    @Test
    public void givenEmployeeObject_whenCreateEmployee_thenReturnSavedEmployee() throws Exception {
        given(employeeService.saveEmployee(any(Employee.class)))
                .willAnswer((invocation) -> invocation.getArgument(0));

        ResultActions response = mockMvc.perform(post("/api/employees")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(employee)));

        response.andDo(print())
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.firstName", is(employee.getFirstName())))
                .andExpect(jsonPath("$.lastName", is(employee.getLastName())))
                .andExpect(jsonPath("$.email", is(employee.getEmail())));
    }

    @Test
    public void givenListOfEmployees_whenGetAllEmployees_thenReturnEmployeesList() throws Exception {
        List<Employee> listOfEmployees = new ArrayList<>();
        listOfEmployees.add(Employee.builder().firstName("Ramesh").lastName("Fadatare").email("ramesh@gmail.com").build());
        listOfEmployees.add(Employee.builder().firstName("Tony").lastName("Stark").email("tony@gmail.com").build());
        given(employeeService.getAllEmployees()).willReturn(listOfEmployees);

        ResultActions response = mockMvc.perform(get("/api/employees"));

        response.andExpect(status().isOk())
                .andDo(print())
                .andExpect(jsonPath("$.size()", is(listOfEmployees.size())));
    }

    @Test
    public void givenEmployeeId_whenGetEmployeeById_thenReturnEmployeeObject() throws Exception {
        long employeeId = 1L;
        given(employeeService.getEmployeeById(employeeId)).willReturn(Optional.of(employee));

        ResultActions response = mockMvc.perform(get("/api/employees/{id}", employeeId));

        response.andExpect(status().isOk())
                .andDo(print())
                .andExpect(jsonPath("$.firstName", is(employee.getFirstName())))
                .andExpect(jsonPath("$.lastName", is(employee.getLastName())))
                .andExpect(jsonPath("$.email", is(employee.getEmail())));
    }

    @Test
    public void givenInvalidEmployeeId_whenGetEmployeeById_thenReturnEmpty() throws Exception {
        long employeeId = 1L;
        given(employeeService.getEmployeeById(employeeId)).willReturn(Optional.empty());

        ResultActions response = mockMvc.perform(get("/api/employees/{id}", employeeId));

        response.andExpect(status().isNotFound())
                .andDo(print());
    }

    @Test
    public void givenUpdatedEmployee_whenUpdateEmployee_thenReturnUpdateEmployeeObject() throws Exception {
        long employeeId = 1L;
        Employee savedEmployee = Employee.builder()
                .firstName("Ramesh")
                .lastName("Fadatare")
                .email("ramesh@gmail.com")
                .build();

        Employee updatedEmployee = Employee.builder()
                .firstName("Ram")
                .lastName("Jadhav")
                .email("ram@gmail.com")
                .build();
        given(employeeService.getEmployeeById(employeeId)).willReturn(Optional.of(savedEmployee));
        given(employeeService.updateEmployee(any(Employee.class)))
                .willAnswer((invocation) -> invocation.getArgument(0));

        ResultActions response = mockMvc.perform(put("/api/employees/{id}", employeeId)
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(updatedEmployee)));

        response.andExpect(status().isOk())
                .andDo(print())
                .andExpect(jsonPath("$.firstName", is(updatedEmployee.getFirstName())))
                .andExpect(jsonPath("$.lastName", is(updatedEmployee.getLastName())))
                .andExpect(jsonPath("$.email", is(updatedEmployee.getEmail())));
    }

    @Test
    public void givenUpdatedEmployee_whenUpdateEmployee_thenReturn404() throws Exception {
        long employeeId = 1L;
        given(employeeService.getEmployeeById(employeeId)).willReturn(Optional.empty());
        given(employeeService.updateEmployee(any(Employee.class)))
                .willAnswer((invocation) -> invocation.getArgument(0));

        ResultActions response = mockMvc.perform(put("/api/employees/{id}", employeeId)
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(employee)));

        response.andExpect(status().isNotFound())
                .andDo(print());
    }

    @Test
    public void givenEmployeeId_whenDeleteEmployee_thenReturn200() throws Exception {
        long employeeId = 1L;
        doNothing().when(employeeService).deleteEmployee(employeeId);

        ResultActions response = mockMvc.perform(delete("/api/employees/{id}", employeeId));

        response.andExpect(status().isOk())
                .andDo(print());
    }
}
```


---

# SPRING SECURITY
## Spring Security Internal Flow

At the core of Spring Security is a chain of filters that intercept HTTP requests and perform security-related operations. These filters handle tasks such as checking for authentication, validating access rights, and handling security exceptions. Each filter plays a specific role in the overall security flow.

### Authentication

Authentication is the process of verifying the identity of a user. It typically involves providing credentials (e.g., username and password) to prove that the user is who they claim to be. Spring Security supports various authentication mechanisms, including form-based login, HTTP basic authentication, and OAuth.

### Authentication Manager

The Authentication Manager is responsible for coordinating the authentication process. It receives the authentication request from the filter chain and delegates the authentication task to one or more configured Authentication Providers.

### Authentication Provider

The Authentication Provider is responsible for validating user credentials and performing authentication. It contains the core logic for validating user details during authentication.

### UserDetails Manager/Service

The UserDetails Manager/Service is an interface in Spring Security that defines operations for managing user details. It facilitates CRUD operations on user details stored in a database or storage system.

### Password Encoder

The Password Encoder is responsible for securely encoding/hashing and verifying passwords.

### Security Context

The Security Context represents the current security state of the application. It stores information about the currently authenticated user and their granted authorities. Once the request has been authenticated, the Authentication will usually be stored in a thread-local SecurityContext managed by the SecurityContextHolder.

## Sequence Flow - Default Behavior

1. User tries to access a secure page for the first time.
2. Behind the scenes, filters identify that the user is not logged in and redirect the user to the login page.
3. User enters credentials, and the request is intercepted by filters.
4. Filters extract the username and password, forming an object of `UsernamePasswordAuthenticationToken`.
5. `ProviderManager` identifies available Authentication Providers and invokes `DaoAuthenticationProvider` in the default behavior.
6. `DaoAuthenticationProvider` loads user details from `InMemoryUserDetailsManager` and validates the user's credentials.
7. Authentication details are returned to `ProviderManager`.
8. `ProviderManager` checks if authentication is successful and returns details to the filters.
9. The Authentication object is stored in the SecurityContext for future use, and the response is returned to the end user.

## Default Security Configuration

```java
@Bean
@Order(SecurityProperties.BASIC_AUTH_ORDER)
SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
    http.authorizeHttpRequests((requests) -> requests.anyRequest().authenticated());
    http.formLogin(withDefaults());
    http.httpBasic(withDefaults());
    return http.build();
}
```

`@Order` is used to specify the execution order of multiple security filter chains in your application. `SecurityProperties.BASIC_AUTH_ORDER` indicates the order of the basic authentication filter chain.


## Custom Security Configuration

```java
@Bean
SecurityFilterChain customSecurityFilterChain(HttpSecurity http) throws Exception {
    http.authorizeHttpRequests((requests) -> requests
            .requestMatchers("/myAccount", "/myBalance", "/myLoans", "/myCards").authenticated()
            .requestMatchers("/notices", "/contact").permitAll())
            .formLogin(Customizer.withDefaults())
            .httpBasic(Customizer.withDefaults());
    return http.build();
}
```

The `SecurityFilterChain` is used to define the order and configuration of security filters within a Spring Security application.

## Deny All Security Configuration

```java
@Bean
SecurityFilterChain denyAllSecurityFilterChain(HttpSecurity http) throws Exception {
    http.authorizeHttpRequests(requests -> requests.anyRequest().denyAll())
        .formLogin(Customizer.withDefaults())
        .httpBasic(Customizer.withDefaults());
    return http.build();
}
```

## Permit All Security Configuration

```java
@Bean
SecurityFilterChain permitAllSecurityFilterChain(HttpSecurity http) throws Exception {
    http.authorizeHttpRequests(requests -> requests.anyRequest().permitAll())
        .formLogin(Customizer.withDefaults())
        .httpBasic(Customizer.withDefaults());
    return http.build();
}
```

The default fallback filter chain in a Spring Boot application has a request matcher `/**`, meaning it will apply to all requests. The default filter chain has a predefined `@Order` of `SecurityProperties.BASIC_AUTH_ORDER`. You can define the ordering of multiple filter chains using `@Order` (e.g., `@Order(SecurityProperties.BASIC_AUTH_ORDER - 10)`).

## User Configuration - InMemoryUserDetailsManager

`InMemoryUserDetailsManager` is a built-in implementation of the `UserDetailsService` interface in Spring Security. It provides an in-memory user store where user details such as username, password, and authorities are stored during the runtime of an application.

**Purpose:**
The purpose of `InMemoryUserDetailsManager` is to provide a simple and convenient way to store and manage user details within the application's memory. It is primarily used for development and testing purposes, where a lightweight user store is required without the need for persistent storage such as a database.

### Approach 1
```java
@Bean
public InMemoryUserDetailsManager userDetailsService() {
    UserDetails admin = User.withDefaultPasswordEncoder()
            .username("admin")
            .password("12345")
            .authorities("admin")
            .build();
    UserDetails user = User.withDefaultPasswordEncoder()
            .username("user")
            .password("12345")
            .authorities("read")
            .build();
    return new InMemoryUserDetailsManager(admin, user);
}
```

### Approach 2

```java
@Bean
public InMemoryUserDetailsManager userDetailsService() {
    UserDetails admin = User.withUsername("admin")
        .password("12345")
        .authorities("admin")
        .build();
    UserDetails user = User.withUsername("user")
        .password("12345")
        .authorities("read")
        .build();
    return new InMemoryUserDetailsManager(admin, user);
}

@Bean
public PasswordEncoder passwordEncoder() {
    return NoOpPasswordEncoder.getInstance();
}
```
## UserDetails Interface

The `UserDetails` interface provides core user information. It stores user information, which is later encapsulated into Authentication objects. This allows non-security related user information (such as email addresses, telephone numbers, etc.) to be stored in a convenient location.

**Purpose:** The purpose of the `UserDetails` interface is to provide a standardized way of representing user-specific details within the Spring Security framework. It serves as the principal object during the authentication process, carrying essential information about the user required for authentication and authorization decisions.

## UserDetailsService Interface

`UserDetailsService` is a core component of Spring Security used to retrieve user-specific data when authenticating a user. It provides a contract for implementing classes to load user details, including username, password, and authorities, based on the user's unique identifier (usually the username).

**Purpose:** The purpose of the `UserDetailsService` interface is to provide a way to retrieve user details during the authentication process. It abstracts the process of loading user-specific data from different data sources such as databases, LDAP directories, or in-memory stores.

The interface requires only one read-only method:

```java
UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
```

## UserDetailsManager Interface

`UserDetailsManager` is an extension of the `UserDetailsService` interface, providing the ability to create new users and update existing ones.

**Purpose:** The purpose of the `UserDetailsManager` interface is to extend the functionality of the `UserDetailsService` interface by adding methods for managing user accounts. It provides a standardized way to create, update, and delete user accounts, as well as retrieve user details for authentication and authorization purposes.

### Implementation Classes

- `JdbcUserDetailsManager`: Stores user details in a relational database using JDBC.
- `InMemoryUserDetailsManager`: Stores user details in memory.
- `LdapUserDetailsManager`: Stores user details in an LDAP directory.

**Example with JdbcUserDetailsManager:**

```java
@Bean
public UserDetailsService userDetailsService(DataSource dataSource) {
    return new JdbcUserDetailsManager(dataSource);
}
```

**Example with Custom UserDetailsService:**

```java
@Service
public class EazyBankUserDetails implements UserDetailsService {

    @Autowired
    private CustomerRepository customerRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        // Custom logic to load user details from a custom data source
    }
}
```

## UserDetails & Authentication Relation Between Them

Authentication is the return type in all scenarios where we are trying to determine if the authentication is successful or not, such as inside the `AuthenticationProvider` and `AuthenticationManager`.

UserDetails is the return type in all scenarios where we try to load the user info from the storage systems, such as inside the `UserDetailsService` and `UserDetailsManager`.

## Password Management

### Different Ways Of Password Management

1. **Encoding:**
   - Defined as the process of converting data from one form to another, with no secret involved.
   - Completely reversible.
   - Not suitable for securing data.
   - Examples: ASCII, BASE64, UNICODE.

2. **Encryption:**
   - The process of transforming data to guarantee confidentiality.
   - Requires a secret (key) for encryption and decryption.
   - Reversible with the correct key, making it secure as long as the key is confidential.

3. **Hashing:**
   - Involves converting data to a hash value using a hashing function.
   - Non-reversible; original data cannot be determined from the hash value.
   - Useful for verifying data integrity without exposing the original data.

### Password Encoder

The `PasswordEncoder` is a service interface in the Spring Security framework, used for encoding and verifying passwords or other sensitive information.

**Purpose:**
The primary purpose of the `PasswordEncoder` interface is to securely encode passwords and other sensitive information. It ensures that user passwords are not stored in plain text but rather transformed into a secure format that is difficult to reverse or decipher. This helps protect user accounts from unauthorized access in case of a data breach or unauthorized access to the password storage.

**Different Implementations of PasswordEncoder inside Spring Security:**
1. **NoOpPasswordEncoder:** Not recommended for production apps; considered deprecated and insecure as it stores passwords in plain text.
2. **BCryptPasswordEncoder:** Uses the bcrypt hashing algorithm, designed to be computationally expensive and resistant to brute-force attacks.
3. **StandardPasswordEncoder:** Not recommended for production apps; uses a deprecated algorithm (SHA-256) to encode passwords.
4. **SCryptPasswordEncoder:** Uses the scrypt hashing algorithm, which is memory-hard and computationally expensive; useful for scenarios where memory consumption is a concern.
5. **Pbkdf2PasswordEncoder:** Uses the PBKDF2 algorithm to encode passwords; allows customization of parameters such as the number of iterations and key length.
6. **Argon2PasswordEncoder:** Uses the Argon2 hashing algorithm, designed to be memory-hard and resistant to various attacks, including GPU-based attacks; recommended for new applications where maximum security is required.

### Example Usage in a Spring Boot Controller

```java
@RestController
public class LoginController {

    @Autowired
    private CustomerRepository customerRepository;

    @Autowired
    private PasswordEncoder passwordEncoder;

    @PostMapping("/register")
    public ResponseEntity<String> registerUser(@RequestBody Customer customer) {
        Customer savedCustomer = null;
        ResponseEntity response = null;
        try {
            String hashPwd = passwordEncoder.encode(customer.getPwd());
            customer.setPwd(hashPwd);
            savedCustomer = customerRepository.save(customer);
            if (savedCustomer.getId() > 0) {
                response = ResponseEntity
                        .status(HttpStatus.CREATED)
                        .body("Given user details are successfully registered");
            }
        } catch (Exception ex) {
            response = ResponseEntity
                    .status(HttpStatus.INTERNAL_SERVER_ERROR)
                    .body("An exception occurred due to " + ex.getMessage());
        }
        return response;
    }
}
```

This example demonstrates the usage of `PasswordEncoder` in a Spring Boot controller for registering users. The user's password is securely hashed before being stored in the database.

## Authentication Provider

The `AuthenticationProvider` in Spring Security is responsible for the authentication logic. While the default implementation delegates finding the user in the system to a `UserDetailsService` implementation and uses a `PasswordEncoder` for password validation, custom authentication requirements can be implemented by creating a custom `AuthenticationProvider`.

**Purpose:**
The primary purpose of the `AuthenticationProvider` interface is to perform the authentication process and verify the user's credentials. It takes in a `Token` with the user's credentials and determines if the provided credentials are valid for authentication. It then builds an `Authentication` object containing the user's authorities or roles for authorization purposes.

### Authentication Tokens

1. **UsernamePasswordAuthenticationToken:**
   - Used for username/password-based authentication.
   - Represents the user's credentials (username and password) provided during the authentication process.
   - Commonly used for authentication in Spring Security.

2. **RememberMeAuthenticationToken:**
   - Used when the user chooses the "remember me" functionality during authentication.
   - Indicates that the user is authenticated based on a previously remembered session or token.
   - Provides automatic login for returning users.

3. **PreAuthenticatedAuthenticationToken:**
   - Used for pre-authenticated scenarios, where the user is already authenticated by an external system or mechanism before reaching the Spring Security layer.

4. **AnonymousAuthenticationToken:**
   - Represents an anonymous user.
   - Used when there is no actual user authentication, but Spring Security requires an authenticated principal object for authorization purposes.
   - Allows the application to distinguish between authenticated and anonymous users.

It's important to note that Spring Security provides flexibility to create custom authentication tokens by extending the `AbstractAuthenticationToken` class. This allows developers to accommodate specific authentication requirements and integrate with various authentication mechanisms or protocols.

### Example Implementation of AuthenticationProvider

```java
@Component
public class EazyBankUsernamePwdAuthenticationProvider implements AuthenticationProvider {

    @Autowired
    private CustomerRepository customerRepository;

    @Autowired
    private PasswordEncoder passwordEncoder;

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {
        String username = authentication.getName();
        String pwd = authentication.getCredentials().toString();
        List<Customer> customer = customerRepository.findByEmail(username);
        if (customer.size() > 0) {
            if (passwordEncoder.matches(pwd, customer.get(0).getPwd())) {
                List<GrantedAuthority> authorities = new ArrayList<>();
                authorities.add(new SimpleGrantedAuthority(customer.get(0).getRole()));
                return new UsernamePasswordAuthenticationToken(username, pwd, authorities);
            } else {
                throw new BadCredentialsException("Invalid password!");
            }
        } else {
            throw new BadCredentialsException("No user registered with this details!");
        }
    }

    @Override
    public boolean supports(Class<?> authentication) {
        return (UsernamePasswordAuthenticationToken.class.isAssignableFrom(authentication));
    }
}
```

## CORS (Cross-Origin-Resource-Sharing) and CSRF (Cross-Site Request Forgery)

### CORS

**CORS (Cross-Origin Resource Sharing)** is a protocol that enables scripts running on a browser client to interact with resources from a different origin. Browsers, by default, block requests from different origins to prevent data communication between them. CORS is not a security issue but a default protection mechanism provided by browsers.

- **How it works:**
  When a web page makes a cross-origin request (e.g., AJAX request), the browser sends a pre-flight request to the server to check if the request is allowed. The server responds with CORS headers that indicate whether the request is permitted.

- **Solutions To Handle CORS:**
  - **Using `@CrossOrigin` Annotation (Class & Method Annotation):**
    - `origins`: Specify a list of allowed origins.
    - `allowedHeaders`: Specify headers accepted when the browser makes the request.
    - `exposedHeaders`: List of headers set in the actual response header.
    - `allowCredentials`: Set `Access-Control-Allow-Credentials` header to true when credentials are required.
    - `maxAge`: Set the maximum age for preflight responses.

  - **Using Spring Security:**
    ```java
    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        http.securityContext((context) -> context.requireExplicitSave(false))
            .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.ALWAYS))
            .cors(corsCustomizer -> corsCustomizer.configurationSource(new CorsConfigurationSource() {
                @Override
                public CorsConfiguration getCorsConfiguration(HttpServletRequest request) {
                    CorsConfiguration config = new CorsConfiguration();
                    config.setAllowedOrigins(Collections.singletonList("http://localhost:4200"));
                    config.setAllowedMethods(Collections.singletonList("*"));
                    config.setAllowCredentials(true);
                    config.setAllowedHeaders(Collections.singletonList("*"));
                    config.setMaxAge(3600L);
                    return config;
                }
            }))
            .and()
            .authorizeHttpRequests((requests)->requests
                .requestMatchers("/myAccount", "/myBalance", "/myLoans", "/myCards", "/user").authenticated()
                .requestMatchers("/notices", "/contact", "/register").permitAll())
            .formLogin(Customizer.withDefaults())
            .httpBasic(Customizer.withDefaults());
        return http.build();
    }
    ```

### CSRF

**CSRF (Cross-Site Request Forgery)** is an attack where a victim is tricked into unknowingly performing unwanted actions on a website where they are authenticated. It occurs when a malicious website sends a request to another website on behalf of the victim using the victim's authenticated session.

- **Solutions To Handle CSRF:**
  - To defeat a CSRF attack, applications use a **CSRF token**. It is a secure random token unique per user session.
  - By default, Spring Security blocks all HTTP POST, PUT, DELETE, PATCH operations with an error of 403 if no CSRF solution is implemented.
  - **Disable CSRF protection:**
    ```java
    http.csrf().disable();
    ```

  - **Configure CSRF with Token:**
    ```java
    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        CsrfTokenRequestAttributeHandler requestHandler = new CsrfTokenRequestAttributeHandler();
        requestHandler.setCsrfRequestAttributeName("_csrf");

        http.securityContext((context) -> context.requireExplicitSave(false))
            .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.ALWAYS))
            .cors(corsCustomizer -> corsCustomizer.configurationSource(new CorsConfigurationSource() {
                @Override
                public CorsConfiguration getCorsConfiguration(HttpServletRequest request) {
                    // CORS Configuration...
                }
            }))
            .csrf((csrf) -> csrf
                .csrfTokenRequestHandler(requestHandler)
                .ignoringRequestMatchers("/contact", "/register")
                .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse()))
            .addFilterAfter(new CsrfCookieFilter(), BasicAuthenticationFilter.class)
            .authorizeHttpRequests((requests)->requests
                .requestMatchers("/myAccount", "/myBalance", "/myLoans", "/myCards", "/user").authenticated()
                .requestMatchers("/notices", "/contact", "/register").permitAll())
            .formLogin(Customizer.withDefaults())
            .httpBasic(Customizer.withDefaults());
        return http.build();
    }
    ```

    ```java
    public class CsrfCookieFilter extends OncePerRequestFilter {
        @Override
        protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
                throws ServletException, IOException {
            // CsrfCookieFilter implementation...
        }
    }
    ```

# AUTHENTICATION & AUTHORIZATION

## AUTHENTICATION

In authentication, the identity of users is checked to provide access to the system.
Authentication (AuthN) is done before authorization.
It usually requires user login details.
If authentication fails, a 401 error response is typically received.
For example, as a bank customer/employee, we need to prove our identity to perform actions in the app.

## AUTHORIZATION

In authorization, a person's or user's authorities are checked for accessing resources.
Authorization (AuthZ) always happens after authentication.
It requires user privileges or roles.
If authorization fails, a 403 error response is usually received.
Once logged into the application, roles and authorities will decide what kind of actions a user can perform.

## HOW AUTHORITIES ARE STORED

Authorities/Roles information in Spring Security is stored inside `GrantedAuthority`.
The `SimpleGrantedAuthority` is the default implementation class of the `GrantedAuthority` interface in the Spring Security framework.

### GrantedAuthority

- Represents a granted authority or permission assigned to a user.
- Core concept for authorization in Spring Security.
- Declares a single method: `String getAuthority()`, which returns the authority as a string.
- Used for role-based access control (RBAC) systems and fine-grained access control.
- Default implementation: `SimpleGrantedAuthority`.

The authorities' information is stored within the `UserDetails` implementation as a collection of `GrantedAuthority` objects. During the authentication process, this information is retrieved from the `UserDetails` object and set within the `Authentication` object, which carries the user's authentication status, credentials, and authorities for authorization checks during the user's session.

## CONFIGURING AUTHORITIES INSIDE SPRING SECURITY

In Spring Security, authorities requirements can be configured using the following ways:

### `hasAuthority()`

Accepts a single authority for configuring an endpoint, and the user will be validated against the mentioned authority.

### `hasAnyAuthority()`

Accepts multiple authorities for configuring an endpoint, and the user will be validated against any of the mentioned authorities.

### `access()`

Using Spring Expression Language (SpEL), it provides unlimited possibilities for configuring authorities with operators like OR, AND inside the `access()` method.

Example Configuration:

```java
@Bean
SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
    // ... (other configurations)
    .authorizeHttpRequests((requests) -> requests
        .requestMatchers("/myAccount").hasAuthority("VIEWACCOUNT")
        .requestMatchers("/myBalance").hasAnyAuthority("VIEWACCOUNT", "VIEWBALANCE")
        .requestMatchers("/myLoans").hasAuthority("VIEWLOANS")
        .requestMatchers("/myCards").hasAuthority("VIEWCARDS")
        .requestMatchers("/user").authenticated()
        .requestMatchers("/notices", "/contact", "/register").permitAll())
    // ... (other configurations)
    .formLogin(Customizer.withDefaults())
    .httpBasic(Customizer.withDefaults());
    return http.build();
}
```

Additionally, an authentication provider method is provided to handle authentication logic and retrieve authorities from the database.

## AUTHORITY vs ROLE

- **AUTHORITY**
    
    - Individual privilege or action.
    - Fine-grained access control (e.g., VIEWACCOUNT, VIEWCARDS).
- **ROLE**
    
    - Group of privileges/actions.
    - Coarse-grained access control (e.g., ROLE_ADMIN, ROLE_USER).

The names of authorities/roles are arbitrary and can be customized. Roles are also represented using the same contract (`GrantedAuthority` in Spring Security). When defining a role, its name should start with the `ROLE_` prefix to specify the difference between a role and an authority.

### Configuring Roles

#### `hasRole()`

Accepts a single role name for configuring an endpoint, and the user will be validated against the mentioned role.

#### `hasAnyRole()`

Accepts multiple roles for configuring an endpoint, and the user will be validated against any of the mentioned roles.

Example Configuration:

```java
@Bean
SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
    // ... (other configurations)
    .authorizeHttpRequests((requests) -> requests
        .requestMatchers("/myAccount").hasRole("USER")
        .requestMatchers("/myBalance").hasAnyRole("USER", "ADMIN")
        .requestMatchers("/myLoans").hasRole("USER")
        .requestMatchers("/myCards").hasRole("USER")
        .requestMatchers("/user").authenticated()
        .requestMatchers("/notices", "/contact", "/register").permitAll())
    // ... (other configurations)
    .formLogin(Customizer.withDefaults())
    .httpBasic(Customizer.withDefaults());
    return http.build();
}
```

# FILTERS IN SPRING SECURITY

Many situations require performing housekeeping activities during the authentication and authorization flow. Examples include input validation, tracing, auditing, logging of details like IP addresses, encryption, decryption, and multi-factor authentication using OTP. These requirements can be addressed using HTTP Filters inside Spring Security.

## Built-in Filters

Some built-in filters of the Spring Security framework include:
- `UsernamePasswordAuthenticationFilter`
- `BasicAuthenticationFilter`
- `DefaultLoginPageGeneratingFilter`

A filter is a component that receives requests, processes its logic, and hands it over to the next filter in the chain. Spring Security is based on a chain of servlet filters, each with a specific responsibility. Custom filters can be added based on the need.

### `@EnableWebSecurity`

- **Configuration Enablement:**
  The primary purpose is to enable the configuration of web security in a Spring Boot application.
  
- **Auto-configuration:**
  Triggers the auto-configuration mechanism provided by Spring Security, applying default security configurations.
  
- **Customization and Configuration:**
  Allows customization and configuration of various aspects of web security by extending `WebSecurityConfigurerAdapter` or implementing `WebSecurityConfigurer` and overriding its methods.
  
- **Method Order:**
  The order of execution is significant when multiple configuration classes are present. Use the `@Order` annotation to control the order.

## Security Filter Chain

- `BasicUserApprovalFilter`
- `SecurityContextPersistenceFilter`
- `LogoutFilter`
- `UsernamePasswordAuthenticationFilter`
- `BasicAuthenticationFilter`
- `RequestCacheAwareFilter`
- `SecurityContextHolderAwareRequestFilter`
- `RememberMeAuthenticationFilter`
- `ForgotPasswordAuthenticationFilter`
- `AnonymousAuthenticationFilter`
- `SessionManagementFilter`
- `OAuth2ExceptionHandlerFilter`
- `VerificationCodeFilter`
- `OAuth2AuthorizationFilter`
- `OAuth2ProtectedResourceFilter`
- `FilterSecurityInterceptor`

## Implementing Custom Filters

Custom filters can be created by implementing the `Filter` interface from the `jakarta.servlet` package and overriding the `doFilter()` method. Three parameters are accepted: `ServletRequest`, `ServletResponse`, and `FilterChain`.

### Methods to Configure a Custom Filter

- `addFilterBefore(filter, class)`: Adds a filter before the specified filter class.
- `addFilterAfter(filter, class)`: Adds a filter after the specified filter class.
- `addFilterAt(filter, class)`: Adds a filter at the location of the specified filter class.

### Example Filters

```java
public class CsrfCookieFilter extends OncePerRequestFilter {
    // ... (implementation)
}

public class AuthoritiesLoggingAfterFilter implements Filter {
    // ... (implementation)
}

public class AuthoritiesLoggingAtFilter implements Filter {
    // ... (implementation)
}

public class RequestValidationBeforeFilter implements Filter {
    // ... (implementation)
}

```


### Configuration Example

```java
@Configuration
public class ProjectSecurityConfig {

    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        // ... (other configurations)
        .addFilterAfter(new CsrfCookieFilter(), BasicAuthenticationFilter.class)
        .addFilterBefore(new RequestValidationBeforeFilter(), BasicAuthenticationFilter.class)
        .addFilterAt(new AuthoritiesLoggingAtFilter(), BasicAuthenticationFilter.class)
        .addFilterAfter(new AuthoritiesLoggingAfterFilter(), BasicAuthenticationFilter.class)
        // ... (other configurations)
    }
    //...
}
```

## Other Important Filters

### `GenericFilterBean`

- An abstract class filter bean that allows using initialization parameters and configurations defined in deployment descriptors.
- Provides a way to create custom filters for intercepting and modifying incoming requests and outgoing responses.

### `OncePerRequestFilter`

- Ensures a filter is executed only once per request, designed for scenarios where single execution is required.
- Useful for implementing filters that require single execution per request, ensuring efficient processing in the filter chain.

# ROLE OF TOKENS

A Token can be a plain string of a universally unique identifier (UUID) or a JSON Web Token (JWT) generated during user authentication. On each request to a restricted resource, the client sends the access token in the query string or Authorization header. The server validates the token, and if valid, returns the secure resource to the client.

## Advantages Of Tokens

1. **Security:**
   Tokens avoid sharing credentials for every request, reducing the security risk of sending credentials over the network frequently.

2. **Dynamic Invalidation:**
   Tokens can be invalidated during suspicious activities without invalidating the user credentials.

3. **Limited Lifespan:**
   Tokens can have a short lifespan, providing an added layer of security.

4. **User Information:**
   Tokens can store user-related information such as roles and authorities.

5. **Reusability:**
   Tokens allow for reuse across separate servers, platforms, and domains, simplifying user authentication.

6. **Stateless and Scalable:**
   Tokens eliminate the need for session state, making the system stateless and easier to scale. Load balancers can distribute users to any server.

## JWT TOKENS

JSON Web Token (JWT) is a widely used token format for web requests, providing special features and advantages. JWT tokens can be utilized for both authorization/authentication and information exchange.

A JWT token consists of three parts, each separated by a period (`.`):

1. **Header:**
   - JSON object encoded as Base64Url.
   - Contains information about the token's type (typ) and the signing algorithm (alg).

2. **Payload:**
   - JSON object encoded as Base64Url.
   - Contains claims or statements about the user or entity, such as ID, name, roles, and permissions.

3. **Signature (Optional):**
   - Used to verify the integrity and authenticity of the token.
   - Created by combining the encoded header, encoded payload, and a secret key using the specified algorithm.

### Example Filters for JWT Tokens

#### JWTTokenGeneratorFilter

```java
public class JWTTokenGeneratorFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        // Implementation...
    }

    @Override
    protected boolean shouldNotFilter(HttpServletRequest request) {
        return !request.getServletPath().equals("/user");
    }
}
```

#### JWTTokenValidatorFilter

```java
public class JWTTokenValidatorFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        // Implementation...
    }

    @Override
    protected boolean shouldNotFilter(HttpServletRequest request) {
        return request.getServletPath().equals("/user");
    }
}
```

#### Security Configuration

```java
@Configuration
public class ProjectSecurityConfig {
    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        // ... (other configurations)
        .addFilterAfter(new JWTTokenGeneratorFilter(), BasicAuthenticationFilter.class)
        .addFilterBefore(new JWTTokenValidatorFilter(), BasicAuthenticationFilter.class)
        // ... (other configurations)
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

It's important to note that the payload is not encrypted, and while anyone can decode the Base64Url-encoded header and payload, modifying the payload or generating a valid signature without the secret key is not possible, ensuring the integrity and security of the token.

# Method Level Security

Method level security allows you to apply authorization rules at any layer of an application, such as the service layer or repository layer. It can be enabled using the annotation `@EnableMethodSecurity` on the configuration class.

You can control access to specific methods based on the roles or permissions of the authenticated user. Method-level security provides an additional layer of protection beyond URL-based security. It is also applicable in non-web applications where there are no endpoints.

Method level security offers the following approaches to apply authorization rules and execute your business logic:

- **Invocation Authorization**: Validates if someone can invoke a method based on their roles/authorities.
- **Filtering Authorization**: Validates what a method can receive through its parameters and what the invoker can receive back from the method post-business logic execution.

Spring Security uses aspects from the AOP module with interceptors between method invocations to apply the configured authorization rules.

The following properties enable specific Spring Security annotations:
- `prePostEnabled`: Enables Spring Security `@PreAuthorize` & `@PostAuthorize` annotations.
- `securedEnabled`: Enables `@Secured` annotation.
- `jsr250Enabled`: Enables `@RolesAllowed` annotation.

```java
@SpringBootApplication
@EnableMethodSecurity(prePostEnabled = true, securedEnabled = true, jsr250Enabled = true)
public class EazyBankBackendApplication {
    public static void main(String[] args) {
        SpringApplication.run(EazyBankBackendApplication.class, args);
    }
}
```

## `@Secured`

The `@Secured` annotation is used to restrict method access based on specific roles. Apply this annotation to a method and specify one or more roles that are allowed to invoke the method. For example, `@Secured("ROLE_ADMIN")` ensures that only users with the "ROLE_ADMIN" role can access the annotated method.

```java
@Secured("ROLE_ADMIN")
public void adminOperation() {
    // Perform admin-specific operation
}
```

This annotation is useful when specific roles are allowed to perform certain administrative operations within your application, providing a straightforward way to enforce role-based access control at the method level.

## `@PreAuthorize`

The `@PreAuthorize` annotation allows you to define an expression that will be evaluated before invoking a method. The expression can use SpEL (Spring Expression Language) to check conditions based on roles, permissions, method parameters, or other attributes. For example, `@PreAuthorize("hasRole('ROLE_USER')")` restricts access to the method to users with the "ROLE_USER" role.

```java
@PreAuthorize("hasRole('ROLE_USER')")
public void userOperation() {
    // Perform user-specific operation
}
```

This annotation is beneficial when you want to control access to a method based on more complex conditions, allowing dynamic authorization decisions based on runtime data.

## `@PostAuthorize`

The `@PostAuthorize` annotation is similar to `@PreAuthorize` but is evaluated after invoking the method. It can be used to further refine access control based on the method's return value. For example, `@PostAuthorize("returnObject.owner == principal.username")` ensures that the returned object's owner matches the authenticated user's username.

```java
@PostAuthorize("returnObject.owner == principal.username")
public Object getOwnedObject() {
    // Retrieve the object
    return ownedObject;
}
```

This annotation is useful when additional authorization checks are needed after invoking a method, providing a way to validate the result of a method against certain conditions.

## `@RolesAllowed`

The `@RolesAllowed` annotation, part of the Java EE standard, can be used in Spring Security. It specifies the roles that are allowed to invoke a method using the value attribute. For example, `@RolesAllowed("ROLE_ADMIN")` restricts access to the method to users with the "ROLE_ADMIN" role.

```java
@RolesAllowed("ROLE_ADMIN")
public void adminOperation() {
    // Perform admin-specific operation
}
```

This annotation is commonly used to apply role-based access control to a method, providing a simple way to restrict method access to specific roles without the need for complex expressions or custom logic.

Both `@Secured` and `@RolesAllowed` annotations serve a similar purpose of restricting access to resources or operations based on roles. However, `@Secured` is more flexible and powerful as it supports expressions and is provided by the Spring Security framework. On the other hand, `@RolesAllowed` is a simpler option that is part of the Java EE standard, making it suitable for Java EE-compliant environments without the need for additional dependencies.

# OAuth2 & OpenID

## Problem That OAuth2 Solves

1. **Third-Party Authorization:**
   OAuth2 enables users to grant permission to third-party applications to access their protected resources on their behalf without sharing their credentials (e.g., username and password) with those applications. This allows users to control the level of access granted to each application.

2. **User Experience:**
   With OAuth2, users can seamlessly authenticate and authorize themselves with an application using their existing credentials from an Identity Provider (IDP) such as Google, Facebook, or GitHub. This eliminates the need for users to create new accounts and remember separate credentials for each application.

3. **Fine-Grained Access Control:**
   OAuth2 provides a framework for defining scopes and permissions associated with protected resources. This allows resource owners (users) to specify the level of access (read, write, etc.) that a client application can have to their resources.

4. **Secure Access Tokens:**
   OAuth2 introduces the concept of access tokens, which are used by client applications to access protected resources on behalf of the user. These tokens are short-lived and can be scoped to limit the access rights of client applications. Access tokens are typically sent over secure channels (e.g., HTTPS) and can be revoked if needed, providing enhanced security compared to long-lived credentials.

5. **Interoperability and Standardization:**
   OAuth2 provides a standardized protocol for authorization and access delegation, ensuring compatibility and interoperability across different platforms, services, and frameworks. This allows developers to integrate their applications with various OAuth2 providers and leverage their existing authentication infrastructure.

## OAuth Introduction

OAuth stands for Open Authorization. It's a free and open protocol, built on IETF standards and licenses from the Open Web Foundation.

OAuth 2.0 is a security standard where you give one application permission to access your data in another application. The steps to grant permission, or consent, are often referred to as authorization or even delegated authorization. You authorize one application to access your data or use features in another application on your behalf, without giving them your password.

In many ways, you can think of the OAuth token as an "access card" at any office/hotel. These tokens provide limited access to someone without handing over full control in the form of the master key.

The OAuth framework specifies several grant types for different use cases, as well as a framework for creating new grant types.

- Authorization Code
- PKCE
- Client Credentials
- Device Code
- Refresh Token
- Implicit Flow (Legacy)
- Password Grant (Legacy)

## Terminology

1. **Resource Owner:**
   The end user. // The end user owns the resources

2. **Client**
   The website we want to reach

3. **Authorization Server**
   The server which knows about the resource owner
   In other words, the resource owner should have an account on this server

4. **Resource Server**
   The server where the APIs services that the client wants to consume are hosted.

5. **Scopes**
   The granular permissions the Client wants, such as access to data or to perform a certain action

### Properties File

```properties
spring.security.oauth2.client.registration.github.client-id=8cf67ab304dc500092e3
spring.security.oauth2.client.registration.github.client-secret=6e6f91851c864684af2f91eaa08fb5041162768e
```

### Config

```java
@Configuration
public class SpringSecOAUTH2GitHubConfig {
    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        http.authorizeHttpRequests((requests) -> requests.anyRequest().authenticated())
            .oauth2Login(Customizer.withDefaults());
        return http.build();
    }
}
```

## OpenID Connect

OpenID is an open standard and decentralized authentication protocol that allows users to authenticate themselves on different websites and applications using a single set of credentials. It provides a way for users to log in to multiple websites without having to create separate accounts for each site.

OpenID Connect is a protocol that sits on top of the OAuth 2.0 framework. While OAuth 2.0 provides authorization via an access token containing scopes, OpenID Connect provides authentication by introducing a new ID token that contains a new set of information and claims specifically for identity. With the ID token, OpenID Connect brings standards around sharing identity details among applications.

The OpenID Connect flow looks the same as OAuth. The only differences are, in the initial request, a specific scope of openid is used, and in the final exchange, the client receives both an Access Token and an ID Token.

The key benefits of OpenID include:

1. **Single Sign-On (SSO):** With OpenID, users can log in to multiple websites using their OpenID credentials. They don't need to remember and manage multiple usernames and passwords for each site, simplifying the authentication process.
    
2. **User Control and Privacy:** OpenID allows users to choose the identity provider they trust and control the information shared with relying parties (websites or applications). Users can manage their personal data and choose the level of information they want to share.
    
3. **Simplified Account Management:** OpenID eliminates the need for users to create and manage multiple accounts across different websites. It reduces the burden of remembering multiple usernames and passwords and reduces the administrative overhead of managing user accounts for websites.
    
4. **Seamless Integration:** OpenID is widely supported by major platforms and service providers, making it easier to integrate authentication functionality into applications. Websites can easily implement OpenID authentication to allow users to log in using their existing OpenID credentials.
    
5. **Secure Authentication:** OpenID provides a secure authentication mechanism using industry-standard encryption and token-based authentication. It helps protect user credentials and prevents password-related security issues, such as password reuse or weak passwords.
    
    Why is OpenID Connect important? Identity is the key to any application. At the core of modern authorization is OAuth 2.0, but OAuth 2.0 lacks an authentication component. Implementing OpenID Connect on top of OAuth 2.0 completes an IAM (Identity & Access Management) strategy. As more and more applications need to connect with each other and more identities are being populated on the internet, the demand to be able to share these identities is also increased. With OpenID Connect, applications can share identities easily and standard way.
    

### Configuration

```java
@Configuration
public class ProjectSecurityConfig {
    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        CsrfTokenRequestAttributeHandler requestHandler = new CsrfTokenRequestAttributeHandler();
        requestHandler.setCsrfRequestAttributeName("_csrf");
        JwtAuthenticationConverter jwtAuthenticationConverter = new JwtAuthenticationConverter();
        jwtAuthenticationConverter.setJwtGrantedAuthoritiesConverter(new KeycloakRoleConverter());

        http.sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .cors(corsCustomizer -> corsCustomizer.configurationSource(new CorsConfigurationSource() {
                @Override
                public CorsConfiguration getCorsConfiguration(HttpServletRequest request) {
                    CorsConfiguration config = new CorsConfiguration();
                    config.setAllowedOrigins(Collections.singletonList("http://localhost:4200"));
                    config.setAllowedMethods(Collections.singletonList("*"));
                    config.setAllowCredentials(true);
                    config.setAllowedHeaders(Collections.singletonList("*"));
                    config.setExposedHeaders(Arrays.asList("Authorization"));
                    config.setMaxAge(3600L);
                    return config;
                }
            }))
            .csrf((csrf) -> csrf.csrfTokenRequestHandler(requestHandler).ignoringRequestMatchers("/contact", "/register")
                .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse()))
            .addFilterAfter(new CsrfCookieFilter(), BasicAuthenticationFilter.class)
            .authorizeHttpRequests((requests) -> requests
                .requestMatchers("/myAccount").hasRole("USER")
                .requestMatchers("/myBalance").hasAnyRole("USER", "ADMIN")
                .requestMatchers("/myLoans").authenticated()
                .requestMatchers("/myCards").hasRole("USER")
                .requestMatchers("/user").authenticated()
                .requestMatchers("/notices", "/contact", "/register").permitAll())
            .oauth2ResourceServer(oauth2ResourceServerCustomizer ->
                oauth2ResourceServerCustomizer.jwt(jwtCustomizer -> jwtCustomizer.jwtAuthenticationConverter(jwtAuthenticationConverter)));
        return http.build();
    }
}

public class KeycloakRoleConverter implements Converter<Jwt, Collection<GrantedAuthority>> {
    @Override
    public Collection<GrantedAuthority> convert(Jwt jwt) {
        Map<String, Object> realmAccess = (Map<String, Object>) jwt.getClaims().get("realm_access");

        if (realmAccess == null || realmAccess.isEmpty()) {
            return new ArrayList<>();
        }

        Collection<GrantedAuthority> returnValue = ((List<String>) realmAccess.get("roles"))
            .stream().map(roleName -> "ROLE_" + roleName)
            .map(SimpleGrantedAuthority::new)
            .collect(Collectors.toList());

        return returnValue;
    }
}

public class CsrfCookieFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
        throws ServletException, IOException {
        CsrfToken csrfToken = (CsrfToken) request.getAttribute(CsrfToken.class.getName());
        if (null != csrfToken.getHeaderName()) {
            response.setHeader(csrfToken.getHeaderName(), csrfToken.getToken());
        }
        filterChain.doFilter(request, response);
    }
}
```

---

# ACTUATOR

# Spring Boot Actuator

Spring Boot Actuator is a set of production-ready features and tools that can be added to your Spring Boot application to help monitor, manage, and interact with the application in a production environment.

By default, Actuator doesn't expose many of the endpoints since they have sensitive information. We can expose them using the below property,

```properties
management.endpoints.web.exposure.include=*
```

  
markdownCopy code

`# Spring Boot Actuator  Spring Boot Actuator is a set of production-ready features and tools that can be added to your Spring Boot application to help monitor, manage, and interact with the application in a production environment.  By default, Actuator doesn't expose many of the endpoints since they have sensitive information. We can expose them using the below property,  ```properties management.endpoints.web.exposure.include=*`

Once the Actuator dependency is added to the project, we can navigate to "[http://localhost:8080/actuator](http://localhost:8080/actuator)" to check the list of APIs exposed by it.

## Some of the Most Important and Commonly Used Endpoints Provided by Spring Boot Actuator

### Health

Provides information about the health of your application and its components.

- **Path:** /actuator/health

### Metrics

Exposes various application-related metrics.

- **Path:** /actuator/metrics

### Info

Displays information about your application, such as its name, version, and description.

- **Path:** /actuator/info

### Environment

Shows properties and configuration of the application's environment.

- **Path:** /actuator/env

### Loggers

Allows you to view and modify logging levels for different loggers.

- **Path:** /actuator/loggers

### Thread Dump

Provides a snapshot of the current threads in the application.

- **Path:** /actuator/threaddump

### Heap Dump

Generates and allows you to download a heap dump of the application for memory analysis.

- **Path:** /actuator/heapdump

### Shutdown

Gracefully shuts down the application.

- **Path:** /actuator/shutdown

### Custom Endpoints

You can create your own custom endpoints to expose specific information or functionality.

- **Path:** Customizable, e.g., /actuator/custom

### Tracing

Allows you to trace the flow of requests through your application.

- **Path:** /actuator/httptrace


# CLOUD - MICROSERVICE

# Monolith - SOA - Microservice

## Monolith

A software application built as a single, self-contained unit where all the components are tightly integrated and share the same codebase, database, and resources.

### Pros

- Simpler development and deployment for smaller teams and applications
- Fewer cross-cutting concerns
- Better performance due to no network latency

### Cons

- Difficult to adopt new technologies
- Limited agility
- Single code base and difficult to maintain
- Not fault-tolerant
- Tiny update and feature development always needs a full deployment

## SOA (Service-Oriented Architecture)

An architectural style where software is designed as a collection of services that are loosely coupled, communicate through standardized interfaces, and can be independently deployed and scaled.

### Pros

- Reusability of services
- Better maintainability
- Higher reliability
- Parallel development

### Cons

- Complex management
- High investment costs
- Extra overload

## Microservice

Small, independent services that can be combined flexibly to create different software systems.

### Pros

- Easy to develop, test, and deploy
- Increased agility
- Ability to scale horizontally
- Parallel development

### Cons

- Complexity
- Infrastructure overhead
- Security concerns

## What Is and Is Not Microservice

An architectural style that structures an application as a collection of small, loosely coupled, and independently deployable services. Each service focuses on a specific business capability and can be developed, deployed, and scaled independently.

### Characteristics of Microservice

1. Single Responsibility: Each microservice handles a specific business capability or domain.
2. Independence: Microservices can be developed, deployed, and scaled independently of other services.
3. Decentralized Data Management: Each microservice manages its own database or data store.
4. Communication: Services communicate with each other using lightweight protocols, such as REST or messaging queues.
5. Resilience: Failures in one microservice do not bring down the entire application.
6. Scalability: Each service can be scaled individually to handle varying workloads.

### What Is Not Microservice

1. Teknolojik bağımsızlığı olmayan projeler Microservice değildir!
2. Birden fazla domain'in iş yükünü barındıran makro projeler Microservice değildir!
3. Tek başına bağımsız deployment yapılamayan projeler Microservice değildir!
4. Bir projede yapılan değişiklikten direk olarak etkilenen - build olamayan - projeler Microservice değildir!
5. Bir iş akışına ait bir sürecin tek başına ölçeklenemediği projeler Microservice değildir!
6. İş kuralı, akışı ya da domain yerine, iş parçacıklarının oluşturduğu projeler Microservice değildir!
7. Küçük Ölçekli Projeler, Sınırlı Ekip Kaynakları, Teknoloji Yeterliliği Olmayan Ekipler, Hızlı Teslimat Gereksinimleri
8. Başka projelere bağımlılık oluşturan projeler Microservice değildir!

### Microservice Terminology

- **API**: An Application Programming Interface
- **RestAPI**: Restful API: Representational State Transfer
- **DevOps**: Is a software development methodology that emphasizes collaboration, communication, and automation between software developers and IT operations teams to improve the speed, quality, and reliability of software delivery.
- **Cloud Computing**: Refers to the on-demand delivery of computing resources, such as servers, storage, databases, and applications, over the internet, providing scalability, flexibility, and cost-efficiency to organizations without the need for extensive on-premises infrastructure.
- **CAP Theorem**: States that in a distributed computer system, it is impossible to simultaneously achieve Consistency, Availability, and Partition tolerance.
- **Resilience**: Refers to the ability of a system or an organization to withstand and adapt to disruptions, failures, or unexpected events, while maintaining an acceptable level of functionality and performance.
- **Scalability**: Refers to the capability of a system or application to handle increased workloads or growth in users, data, or processing demands while maintaining or improving performance and responsiveness.
- **CI/CD (Continuous Integration/Continuous Deployment)**: Continuous Integration is a development practice where developers frequently merge their code changes into a shared repository, which is then automatically built and tested, enabling early detection of integration issues. Continuous Deployment is an extension of continuous integration, where code changes that pass automated testing are automatically deployed to production environments, ensuring a rapid and automated release process.
- **Fault Isolation**: Refers to the ability of a system or network to contain or localize the impact of a fault or failure, preventing it from affecting other components or services.
- **Service-Oriented Architecture (SOA)**: Is an architectural style that structures an application as a collection of loosely coupled, reusable, and interoperable services that communicate with each other over a network.


# 12 Factor App

The 12 Factor App is a methodology for building software-as-a-service (SaaS) applications, emphasizing best practices such as declarative configuration, scalability, and independence of individual components.

## Codebase

Each microservice should have a single codebase, managed in source control. The code base can have multiple instances of deployment environments such as development, testing, staging, production, and more but is not shared with any other microservice.

## Dependencies

Dependencies refer to external libraries, modules, or packages that the application relies on to function properly. These dependencies are declared explicitly and managed separately from the codebase, ensuring consistent and reproducible deployment environments.

## Configuration

Store environment-specific configuration independently from your code. Never add embedded configurations to your source code; instead, maintain your configuration completely separated from your deployable microservice. If we keep the configuration packaged within the microservice, we'll need to redeploy each of the hundred instances to make the change.

## Backing Services

Backing Services are external resources or systems that the application depends on, such as databases, message queues, or third-party APIs. Backing services are treated as attached resources that can be accessed via a well-defined interface, enabling the application to be easily connected to different environments and swapped with different implementations. Backing Services best practice indicates that a microservices deploy should be able to swap between local connections to third party without any changes to the application code.

## Build-Release-Run

Keep your build, release, and run stages of deploying your application completely separated. We should be able to build microservices that are independent of the environment in which they are running.

## Process

Processes refer to the execution of the application code. The application is divided into multiple stateless and self-contained processes that can be independently started, stopped, and scaled. Each process adheres to the principles of concurrency, isolation, and share-nothing architecture, allowing for easy scaling, fault tolerance, and efficient utilization of computing resources.

## Port Binding

Port binding refers to the practice of explicitly declaring and adhering to a specified port for the application to listen on. The application is self-contained and does not rely on a specific web server or container to handle incoming network requests. By binding to a specific port, the application can be easily deployed and scaled without conflicts, ensuring consistency across different execution environments.

## Concurrency

Concurrency refers to the ability of an application to handle multiple simultaneous requests or tasks efficiently. The application is designed to be stateless and capable of scaling horizontally by adding more instances or processes to handle increased demand. By embracing concurrency, the application can effectively utilize available computing resources and provide a responsive and scalable experience for users. Services scale out across a large number of small identical processes (copies) as opposed to scaling-up a single large instance on the most powerful machine available. Vertical scaling (Scale up) refers to increase the hardware infrastructure (CPU, RAM). Horizontal scaling (Scale out) refers to adding more instances of the application. When you need to scale, launch more microservice instances and scale out and not up.

## Disposability

Disposability refers to the ability of an application to start up quickly, shut down gracefully, and easily scale in response to demand. It emphasizes the principle of treating application processes as stateless and replaceable units that can be started or stopped at any time without significant impact. By embracing disposability, applications can recover quickly from failures, adapt to varying workloads, and promote easy deployment and scaling in modern cloud environments.

## Dev/Prod Parity

Keep environments across the application lifecycle as similar as possible, avoiding costly shortcuts. Here, the adoption of containers can greatly contribute by promoting the same execution environment. As soon as a code is committed, it should be tested and then promoted as quickly as possible from development all the way to production. This guideline is essential if we want to avoid deployment errors. Having similar development and production environments allows us to control all the possible scenarios we might have while deploying and executing our application.

## Logs

Logs refer to the aggregated and structured output of the application's internal activities, errors, and events. The application writes logs to the standard output stream (stdout) or a dedicated log stream, allowing them to be easily captured and managed by a log management system. By treating logs as event streams, the application gains visibility into its behavior, facilitates troubleshooting and debugging, and enables effective monitoring and analysis of application performance and health. The microservice should never be concerned about the mechanisms of how this happens; they only need to focus on writing the log entries into the stdout.

## Admin Processes

Admin Processes refer to tasks or actions that are executed as one-off or periodic operations to manage the application or perform administrative tasks. These processes are separate from the regular application processes and are designed to be run independently and in isolation. Tasks should never be ad hoc and instead should be done via scripts that are managed and maintained through a source code repository. These scripts should be repeatable and non-changing across each environment they're run against.


# MicroService Communication

## Synchronous Communication

1. The client sends a request and waits for a response from the service.
2. The protocol (HTTP/HTTPS) is synchronous, and the client code can only continue its task when it receives the HTTP server response.
3. Examples: RestTemplate, WebClient, and Spring Cloud OpenFeign library.

## Asynchronous Communication

1. The client sends a request and does not wait for a response from the service.
2. The client continues executing its task without waiting for the response from the service.
3. Examples: RabbitMQ or Apache Kafka.

## Microservices Communication Using RestTemplate

Microservice communication can be achieved using RestTemplate in Java Spring, which is a synchronous HTTP client that simplifies making HTTP requests to other services.

```java
@Configuration
public class AppConfig {
    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

Use RestTemplate for Communication:

```java
@RestController
public class ExampleController {
    private final RestTemplate restTemplate;

    public ExampleController(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    @GetMapping("/example")
    public String makeRequestToAnotherMicroservice() {
        String url = "http://another-microservice/api/data";
        ResponseEntity<String> response = restTemplate.getForEntity(url, String.class);
        return response.getBody();
    }
}
```

In the example above, when the "/example" endpoint is called, RestTemplate sends an HTTP GET request to "[http://another-microservice/api/data](http://another-microservice/api/data)" and retrieves the response.

## Microservices Communication Using WebClient

WebClient is a non-blocking, reactive HTTP client introduced in Spring WebFlux.

```java
@Configuration
public class AppConfig {
    @Bean
    public WebClient webClient() {
        return WebClient.create();
    }
}
```

Use WebClient to Make Requests:

```java
@RestController
public class ExampleController {
    private final WebClient webClient;

    public ExampleController(WebClient webClient) {
        this.webClient = webClient;
    }

    @GetMapping("/example")
    public Mono<String> makeRequestToAnotherMicroservice() {
        String url = "http://another-microservice/api/data";
        return webClient.get()
                .uri(url)
                .retrieve()
                .bodyToMono(String.class);
    }
}
```

When the "/example" endpoint is called, WebClient sends an HTTP GET request to "[http://another-microservice/api/data](http://another-microservice/api/data)" and retrieves the response as a `Mono<String>`, which represents a reactive stream of the response body.

## Microservices Communication Using Spring Cloud OpenFeign

Microservice communication can also be facilitated using Spring Cloud OpenFeign, a declarative HTTP client that simplifies the integration and communication between microservices in a Java Spring application.

### Pre Configuration

- **Enable Feign Client:** `spring.cloud.openfeign.enabled=true` or `@EnableFeignClients`
- **Specify Base Package for Scanning Feign Clients:** `spring.cloud.openfeign.scan.base-packages=com.example.feignclients`
- **Enable Service Discovery (optional):** `spring.cloud.discovery.client.simple.instances.another-microservice[0].uri=http://localhost:8081`
- **Specify Request and Connection Timeouts (optional):** `feign.client.config.default.connectTimeout=5000` or `feign.client.config.default.readTimeout=5000`

Add the following dependency:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

Enable Feign Client:

```java
@SpringBootApplication
@EnableFeignClients
public class YourApplication {
    public static void main(String[] args) {
        SpringApplication.run(YourApplication.class, args);
    }
}
```

Create a Feign Client Interface:

```java
@FeignClient(name = "another-microservice")
public interface AnotherMicroserviceClient {
    @GetMapping("/api/data")
    String getData();
}
```

Use the Feign Client:

```java
@RestController
public class ExampleController {
    private final AnotherMicroserviceClient client;

    public ExampleController(AnotherMicroserviceClient client) {
        this.client = client;
    }

    @GetMapping("/example")
    public String makeRequestToAnotherMicroservice() {
        return client.getData();
    }
}
```

# Service Registry and Discovery - Spring Cloud Eureka Server

## Service Registry

A **Service Registry** is a centralized component that keeps track of available services in a distributed system by registering service instances and their network locations (IP address, port, etc.), enabling service discovery.

## Service Discovery

**Service Discovery** is the process by which client applications locate and dynamically discover available service instances from the service registry, enabling efficient communication and interaction between services in a distributed environment.

## Spring Cloud Eureka Server

**Spring Cloud Eureka Server** is a component of the Spring Cloud ecosystem that provides a service registry and discovery server implementation based on Netflix Eureka.

### Enable Eureka Server:

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

### Configure Eureka Server:

```properties
spring.application.name=eureka-server
server.port=8761

eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

- `register-with-eureka`: By setting this property to false, the Eureka Server does not register itself with the service registry. In other words, it won't treat itself as a discoverable service.
    
- `fetch-registry`: With this property set to false, the Eureka Server does not attempt to fetch the registry information from other Eureka servers. It means the Eureka Server does not participate in the registry synchronization process with other Eureka instances.
    

### Register Microservices:

To register microservices with the Eureka Server, include the `spring-cloud-starter-netflix-eureka-client` dependency in your microservice projects and configure the following properties:

```properties
spring.application.name=my-microservice
eureka.client.service-url.default-zone=http://localhost:8761/eureka
```

# API GATEWAY

**API Gateway** provides a unified interface for a set of microservices so that clients don't need to know about all the details of microservices internals. It centralizes cross-cutting concerns like security, monitoring, rate limiting, etc.

API Gateway is a pattern used in microservices architecture that acts as an entry point for client requests and provides a centralized point for handling and routing API requests to the appropriate downstream services.

```xml
<!-- For Spring Cloud Gateway -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

### Configure Routing:

**Manual:**

```properties
spring.cloud.gateway.routes[0].id=my-route
spring.cloud.gateway.routes[0].uri=http://localhost:8081
spring.cloud.gateway.routes[0].predicates[0]=Path=/api/**
```

**Auto:**

```properties
spring.cloud.gateway.discovery.locator.enabled=true
spring.cloud.gateway.discovery.locator.lowerCaseServiceId=true
logging.level.org.springframework.cloud.gateway.handler.RoutePredicateHandlerMapping=DEBUG
```

The route is configured to match any request path starting with "/api/".

### Create and Run Gateway Application:

```java
@SpringBootApplication
public class GatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(GatewayApplication.class, args);
    }
}
```

# Spring Cloud Config Server

**Spring Cloud Config Server** is a component of the Spring Cloud framework that enables centralized management and distribution of configuration properties for microservices.

Add Dependencies:

```xml
<!-- For Spring Cloud Config Server -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

### Enable Config Server:

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

### Configure Git Repository:

Configure the location of your Git repository that contains the configuration files.

```properties
spring.cloud.config.server.git.uri=<git-repo-uri>
spring.cloud.config.server.git.username=<git-username>
spring.cloud.config.server.git.password=<git-password>

spring.cloud.config.server.git.clone-on-start=true
spring.cloud.config.server.git.default-label=main

spring.application.name=my-microservice
spring.cloud.config.uri=http://localhost:8888
```

### Client Side

```java
<!-- For Spring Cloud Config Client -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

### Configure Application Properties:

```properties
spring.application.name=MY-SERVICE
spring.config.import=optional:configserver:http://localhost:8888
# Other fields will be fetched from the Git repo file

@RefreshScope
```
`@RefreshScope` is an annotation provided by Spring Cloud that, when used with Spring Cloud Config Server, enables dynamic refreshing of beans at runtime when configuration properties change.

```java
@Component
@RefreshScope
public class MyConfigurableBean {
    @Value("${my.property}")
    private String myProperty;

    public String getMyProperty() {
        return myProperty;
    }
}

@RestController
public class MyController {
    @Autowired
    private MyConfigurableBean myConfigurableBean;

    @GetMapping("/property")
    public String getProperty() {
        return myConfigurableBean.getMyProperty();
    }
}
```

# Spring Cloud Bus

**Spring Cloud Bus** provides a messaging infrastructure that enables efficient and centralized communication between microservices in a distributed system. It simplifies the process of triggering configuration refreshes across multiple microservices, promoting easier management and coordination of configuration changes.

It is a lightweight messaging framework provided by Spring Cloud that facilitates communication and event-driven messaging between microservices in a distributed system.

### Add Dependencies:

```xml
<!-- For Spring Cloud Bus -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```

### Configure Message Broker:

Spring Cloud Bus relies on a message broker for communication between microservices. You can choose a message broker such as RabbitMQ or Apache Kafka. Set up the message broker and ensure it is running.

### Configure Bus Endpoint:

```properties
spring.cloud.bus.enabled=true
spring.cloud.bus.refresh.enabled=true
spring.cloud.bus.env.enabled=true
spring.rabbitmq.host=<rabbitmq-host>
spring.rabbitmq.port=<rabbitmq-port>
spring.rabbitmq.username=<rabbitmq-username>
spring.rabbitmq.password=<rabbitmq-password>
```

# Spring Cloud Sleuth and Zipkin

**Distributed Tracing** is a technique used in distributed systems to track and monitor the flow of requests as they traverse multiple microservices. It aims to solve the problem of understanding and diagnosing complex interactions between services by providing visibility into the entire request lifecycle.

**Spring Cloud Sleuth** provides distributed tracing capabilities in a Spring Cloud application. It integrates with tracing systems to generate and propagate trace IDs across services, enabling comprehensive tracing and analysis of request flows.

### Add Dependencies:

```xml
<!-- For Spring Cloud Sleuth -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
```

### Configure Tracing System:

Choose a distributed tracing system like Zipkin or Jaeger and set it up in your environment.

### Configure Sleuth:

```properties
spring.zipkin.baseUrl=<zipkin-server-url>
```

### Zipkin

**Zipkin** is a distributed tracing system that helps you monitor and analyze request flows in a microservices architecture. By instrumenting your services and sending trace data to a central Zipkin server, you gain insights into latency, dependencies, and overall system behavior.

### Set up Zipkin Server:

#### Add Dependencies:

```xml
<!-- For Zipkin Client -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
```

#### Configure Zipkin:

```properties
spring.zipkin.baseUrl=<zipkin-server-url>
```

# Resilience4j

Resilience4j is a lightweight and flexible fault tolerance library for Java applications. It provides various resilience patterns such as Circuit Breaker, Retry, Rate Limiter, and Bulkhead to make your application more resilient to failures and to improve its overall stability.

### Add Dependency:

```xml
<!-- For Resilience4j -->
<dependency>
    <groupId>io.github.resilience4j</groupId>
    <artifactId>resilience4j-spring-boot2</artifactId>
    <version>1.7.1</version>
</dependency>
```

### Configure Resilience4j:

#### Circuit Breaker:

``` yaml
resilience4j.circuitbreaker:
  instances:
    myProjectAllRemoteCallsCB:
      registerHealthIndicator: true
      slidingWindowSize: 10
      slidingWindowType: COUNT_BASED
      permittedNumberOfCallsInHalfOpenState: 4
      minimumNumberOfCalls: 10
      waitDurationInOpenState: 5s
      slowCallRateThreshold: 50
      slowCallDurationThreshold: 10
      failureRateThreshold: 50

```

#### Retry Pattern:

```properties
resilience4j.retry.configs.default.registerHealthIndicator= true
resilience4j.retry.instances.retryForCustomerDetails.maxRetryAttempts=3
resilience4j.retry.instances.retryForCustomerDetails.waitDuration=2000
```

### Code Implementation:

Use `@CircuitBreaker` annotation followed by the name of the circuit breaker and `fallbackMethod`. The `fallbackMethod` is used to return a default response when the state is HALF_OPEN or OPEN.

```java
@CircuitBreaker(name = "myProjectAllRemoteCallsCB", fallbackMethod = "getAPIFallBack")
public String getFromRemoteAPI(String searchVal) throws Exception {
    // Implementation...
}

public String getAPIFallBack(String topicPage, Exception e) {
    log.error("getAPIFallBack::{}", e);
    return "";
}
```

Make sure the method annotated with `@CircuitBreaker` should not be in the same class as the caller.

