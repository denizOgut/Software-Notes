Aslında Go ile geliştirme yapmak için kullanılan en temel program `go` programıdır. go programı bir çok switch'e sahiptir.

go programının switch'lerini görmek için komut satırında yalnızca `go` yazmak yeterlidir. Go dosyaları geleneksel olarak .go uzantılı olarak yazılır. 

Bir Go dosyasını yorumlayarak çalıştırmak yani, go yorumlayıcısını çalıştırmak için go ile birlikte run switch'i kullanılabilir: 

> go run sample.go

Go ile yazılan bir kodun işletim sistemi düzeyinde ***executable*** bir dosya olarak build edilmesi (tek bir dosya için derleme denebilir) için go ile build switch'i kullanılır:

> go build sample.go 

Hello, World Programı

```go  
package main

	import "fmt"

	func main() {
		fmt.Println("Hello, World")
	} 
```

***Bildirim (declaration)***: Bir ismin derleyiciye tanıtılmasıdır. Yani derleyici bir ismin bildirimini arar.

Paket bildiriminin genel biçimi şu şekildedir:
		package paket ismi
		Örneğin:
			package main

Fonksiyon bildiriminin genel biçimi:
	func fonksiyon ismi ([parametreler]) [geri dönüş bilgisi] {
		//...
	}
	
	func foo() {
		fmt.Println("foo")
	}

Fonksiyon çağrısının genel biçimi:
	[paket ismi].fonksiyon isimi([argümanlar])
	Örneğin
		foo() 
			test.Foo()


***Anahtar Notlar***: Bir fonksiyonun isminin küçük harf başlatılması durumunda o fonksiyon başka bir paketten çağrılamaz. ->  **Private**

Başka bir paketten çağrılabilecek bir fonksiyon isminin ilk harfi büyük olmalıdır. -> **Public**

Go'da akış main fonksiyonu ile başlar. Belirli koşullar dışında main fonksiyonu bittiğinde program sonlanır. Bu anlamda main fonksiyonuna ***entry point*** de denilmektedir. 


Programlamada taşınabilirlik (portability) denilen önemli bir kavram vardır.
Bu anlamda portability genel olarak ikiye ayrılabilir: kod taşınabilirliği (code potability), program taşınabilirliği (program portability).

* kod taşınabilirliği (code potability):
	* özellikle her sistemde build edilmesi gereken diller ve teknolojiler için, her hangi bir sistem için build ederken bir değişiklik yapılmasına gerek olmaması anlamındadır.

* program taşınabilirliği (program portability):
	* Programın taşınabilirliği ise üretilen kodun bir sisteme özgü olmaması dolayısıyla bir kez üretilip her sistemde çalıştırılabilmesidir.

---

# TYPES

Golang is a statically typed programming language meaning that each variable has a type.
Bir değişkenin içerisindeki değerin hangi formatta tutulduğunu ve bellekte ne kadar uzunlukta (byte) yer ayrılacağını belirten kavramdır.

* Boolean types -> True veya false değerlerini temsil eder.
*  Numeric types -> Tam sayılar(Integer), kayan nokta sayılar(Floating) ve karmaşık sayıları(Complex) temsil eder.
- String types -> Metinleri temsil eder.
- Derived types -> Diğer veri türlerinden türetilen veri türleridir. (Array,Map,Struct...)

***Anahtar Notlar***: Go'da bazı durumlar sistemden sisteme değişiklik gösterebilmektedir. 
Örneğin int türünün uzunluğu bazı sistemlerde 4 byte iken, bazı sistemlerde 8 byte olarak ele alınmaktadır.
Bu duruma genel olarak ***implementation specified/defined/dependent*** denilmektedir.

 **Numeric Types(Sayısal Türler)**

| Tür ismi        | Uzunluğu (byte) | Varsayılan Değer    |
|-----------------|-----------------|---------------------|
| int8            | 1               | 0                   |
| uint8           | 1               | 0                   |
| int16           | 2               | 0                   |
| uint16          | 2               | 0                   |
| int32           | 4               | 0                   |
| uint32          | 4               | 0                   |
| int64           | 8               | 0                   |
| uint64          | 8               | 0                   |
| byte            | 1               | 0                   |
| rune            | 4               | 0                   |
| uint            | 4/8             | 0 (Platform Dependent) |
| int             | 4/8             | 0 (Platform Dependent) |
| float32         | 4               | 0                   |
| float64         | 8               | 0                   |
| complex64       | 8               | (0+0i)              |
| complex128      | 16              | (0+0i)              |
| bool            | 1               | false               |


* **Boolean:** True veya False değerlerini temsil eder. 1 bit bellek kullanır.
* **Byte:** 8 bitlik bir karakteri temsil eder. 1 byte bellek kullanır.
* **Rune:** UTF-8 karakterini temsil eder. 4 byte bellek kullanır.
* **Int:** İşaretli veya işaretsiz tamsayıları temsil eder. 4 veya 8 byte bellek kullanır.
* **Uint:** İşaretsiz tamsayıları temsil eder. 4 veya 8 byte bellek kullanır.
* **Float:** Ondalık sayıları temsil eder. 4 veya 8 byte bellek kullanır.
* **Complex:** Karmaşık sayıları temsil eder. 8 veya 16 byte bellek kullanır.

 * Sayısal türler (numeric types) genel olarak iki gruba ayrılır: tamsayı türleri (integer/integral types), gerçek sayı türleri (real types/floating point types)
	
- Tamsayı türleri işaretli (signed) ve işaretsiz (unsigned) olarak ayrı ayrı bulundurulmuştur ve ikiye tümleme formatında çalışırlar.

- Gerçek sayı türleri ise IEEE754 formatını kullanırlar

- complex64 türü gerçek (real) ve sanal (imaginary) kısımları float32 türünden olan karmaşık sayıyı temsil eder

- complex128 türü gerçek (real) ve sanal (imaginary) kısımları float64 türünden olan karmaşık sayıyı temsil eder

- int8, uint8, int16, uint16, int32, uint32, int64, uint64 tamsayı türlerinin uzunlukları sistemden sisteme değişiklik göstermez

- float32, float64 complex64 ve complex128 türlerinin uzunlukları sistemden sistemden sisteme değişmez.

- byte türü uint8 türünün ayrı bir ismidir (alias)

- rune türü int32 türünün ayrı bir ismidir (alias)

- int ve uint türleri sistem sisteme uzunluğu değişebilen (4 byte veya 8 byte) olan tamsayı türleridir.

- bool türü 1 byte uzunluğunda, true veya false değerlerinden birini alabilen bir türdür.

---

İfade (expression): Sabitlerden, operatörlerden ve değişkenlerden oluşan dizilimlere denir

Bir değişkene ilişkin temel kavramlar:
	***İsim (name)***: Belirli kurallara göre verilebilen karakter topluluğudur
	***Tür (type)***: Bir değişkenin içerisindeki değerin hangi formatta tutulduğunu ve bellekte ne kadar uzunlukta (byte) yer ayrılacağını belirten kavramdır
	***Faaliyet Alanı (scope)***: Değişken isminin derleyici/yorumlayıcı tarafından görülebildiği kod aralığıdır
	***Ömür (storage duration)***: Değişkenin bellekte yaratılmasıyla, yok edilmesi arasındaki zamana denir


***Nesne (object)***: Bellekte yer ayrılan terimdir.

Go'da C'den gelen iki önemli kavram vardır: Sol taraf değeri (lvalue), Sağ taraf değeri (rvalue).
	**lvalue**: Nesne gösteren ifadelere denir. Yani bellekte yer ayrılmasına yol açan ifadelerdir. Bu anlamda bir değişken de lvalue ya da lvalue expression'dır.
	**rvalue**: lvalue olmayan ifadelerdir. Bu ifadeler atama operatörünün birinci operandı olamazlar.

Bir değişkene bildirim noktasında verilen değere **initialization** denir.
	Go'da değişken bildirimleri ya var anahtar sözcüğü ile ya da doğrudan (immediate) yapılabilir.
	var değişken bildiriminin genel biçimi şu şekildedir
	var isim tür

ilkdeğer (initialization) verilmesi zorunlu değildir. var değişkenlere ilk değer verilmiyorsa tür belirtilmesi zorunludur.

***Anahtar Notlar***: Go'da bildirilmiş bir değişkenin kullanılmaması durumu error'dur

---

Aşağıdaki örnekte a değişkenine ilk değer verildiği için tür bilgisi otomatik tespit edilir (type inference/deduction)

```go
package main

import "fmt"

func main() {
	var a = 10

	fmt.Println(a)
}
```


Bir değişkene ilk kez **:=** operatörü değer verildiğinde o değişken aynı zamanda bildirilmiş olur.
Bu değişkenlere immediate değişken de denilmektedir. 
Tabi bu durumda tür bilgisi yazılmaz. Çünkü yine tür otomatik tespit edilir


```go
package main

import "fmt"

func main() {
	a := 20
	b := a

	milage, company := 80276, "Tesla"

	fmt.Println(a)
	fmt.Println(b)
}
```

farklı türdeki değişkenler ilk değer verilerek ve virgül ile ayrılarak aşağıdaki gibi bildirilebilir. Bu bildirim biçimine ***mixed variable declaration/initialization*** denir

```go
package main

import "fmt"

func main() {
	var a, b, c = 10, 3.4, 56

	fmt.Println(a)
	fmt.Println(b)
	fmt.Println(c)
}
```

### WEB NOTES
---
Single variable declaration without initial value -> var variable_name type -> var a int
Single variable declaration with initial value -> var variable_name type = value -> var a int = 8

Multiple variable declaration without initial value -> `var name1, name2,….nameN type` -> `var a, b int`
Multiple variable declaration with initial value -> `var name1, name2, …..,nameN type = value1, value2, ….. ,valueN` -> `var a, b int = 8, 9`

Declare variables of different types

```go
var (
	a int
	b int    = 8
	c string = "a"
)
```

Variable Declaration with no type or Type Inference -> `var <variable_name> = <value>` -> `var t = 123`, `var u = "circle"`
Short variable declaration -> `:=` -> both `var` keyword and type info can be omitted. -> `t := 123`, `u := "circle"` same as above

***:= operator is only available within a function. It is not allowed outside the function.***
A variable once declared using := cannot be redeclared using the := operator.
raise a compiler error  “no new variables in the left side of :=” .

:= operator can also be used to declare multiple variables in a single line.

```go
func main() {
	a, b := 1, 2
	b, c := 3, 4
	fmt.Println(a, b, c)
}
```
In case of multiple declaration, `:=` can also be used again for a particular variable if at least one of the variables on the left-hand side is new.

---

Bir fonksiyon içerisinde { ile } arasındak kalan bölgeye blok (block) denir. Bu anlamda bir fonksiyonun gövdesi de bir bloktur.
Bir fonksiyon içerisinde istenildiği kadar ayrı ve içiçe bloklar olabilir

```go
package main
func main() {
	{
		//...
		{

		}
	}

	{
		//...
	}
}
```

Bir blok içerisinde bildirilen değişkenlere **yerel değişkenler (local variables)** denir
İçiçe bloklarda aynı isimde yerel değişken bildirilebilir. Bu durumda içteki isim dıştaki ismi maskeler **(masking/shadowing)**

```go
package main
import "fmt"

func main() {
	var a int32

	fmt.Println(a)

	{
		var a = 10

		a = a + 2

		fmt.Println(a)
	}
}
```


Go'da tüm fonksiyonların dışında paket içerisinde bildirilen değişkenlere **global değişkenler (global variables)** denir.
Global değişkenler aynı dosyadaki tüm fonksiyonlar içerisinde görülebilirdir.
Global değişkenlere de default değerler otomatik olarak atanır


>A variable will be global within a package if it is declared at the top of a file outside the scope of any function or block.
 If the variable name stats with a uppercase letter then it can be accessed from outside different package other than which it is declared.
 Global variable are available throughout the lifetime of a program

```go
package main

import "fmt"

// Global variable
var name string = "Bard"

func main() {
	// Print the global variable
	fmt.Println(name)
}
```

* **ADVANTAGE**
	- Programın tümünde erişilebilirlik
	* Değerlerin tutarlılığı 

*  **DISADVANTAGE**
	- Performans kaybı
	- Değişikliklerden kaynaklanan istenmeyen sonuçlar

* **CAVEAT**
	- Global değişkenlerin kullanımını sınırlayın.
	- Global değişkenlerin değerini sadece gerekli olduğunda değiştirin.
	- Global değişkenlerin değerini değiştirmeden önce, bu değişikliğin programın diğer kısımlarını nasıl etkileyeceğini düşünün.



* **IMPORTANT POINTS**
	A unused variable will be reported as a compiler error. 
	GO compiler doesn’t allow any unused variable. This is an optimization in GO.
			
	A variable declared within an inner scope having the same name as variable declared in the outer scope will shadow the variable in the outer scope.
	
	A variable once inİtialized with a particular type, cannot be assigned a value of different type later. 
	This is applicable for short hand declaration is well.	

---

# CONSTANT

Constants hold a piece of data just like variables, but their value cannot change during the execution of the program. Constants are defined using the `const` keyword and can be numbers, characters, strings, or booleans. Constants cannot be declared using the `:=` syntax.

```go
const CONSTNAME type = value
const PI = 3.14
```


### Multiple Constants Declaration

```go
package main

import (
	"fmt"
)

const (
	A int    = 1
	B        = 3.14
	C        = "Hi!"
)

func main() {
	fmt.Println(A)
	fmt.Println(B)
	fmt.Println(C)
}

```

### WEB NOTES

---
### Important Points

- Constant variables cannot be reassigned after their declaration.
- `const` values must be known at compile time. Hence, a `const` value cannot be assigned to a function call that is evaluated at runtime.

### Typed and Untyped Constants

- Go has a very strong type system that doesn’t allow implicit conversion between any of the types.
- Even with the same numeric types, no operation is allowed without explicit conversion.
- However, untyped constants have the flexibility of temporary escape from Go’s type system.

#### Typed Constant

A `const` declared specifying the type in the declaration is a typed constant.

```go
const a int32 = 8

```

#### Untyped Constant

An untyped constant is a constant whose type has not been specified. It can be either named or unnamed.

```go
const a = 123 // unnamed
const b int = 123

```

The default type of a named or unnamed constant will become the type of a variable they are assigned to.

**Use of Untyped Constants:** The use of untyped constants is that the type of the constant will be decided depending upon the type of variable they are being assigned to.

```go
const Pi = 3.14159265358979323846264338327950288419716939937510582097494459

func main() {
    var f1 float32
    var f2 float64
    f1 = Pi
    f2 = Pi

    fmt.Printf("Type: %T Value: %v\n", Pi, Pi)
    fmt.Printf("Type: %T Value: %v\n", f1, f1)
    fmt.Printf("Type: %T Value: %v\n", f2, f2)
}

```

**Output:**
```
Type: float64 Value: 3.141592653589793
Type: float32 Value: 3.1415927
Type: float64 Value: 3.141592653589793
```

Depending upon the use case, an untyped constant can be assigned to a low precision type (float32) or a high precision type (float64).

### Naming Conventions

Naming conventions for constants are the same as naming conventions for variables.

### Global Constant

Like any other variable, a constant will be global within a package if it is declared at the top of a file outside the scope of any function.

---

# IOTA

```go
package card
import (
	"SampleGoLand/csd/util/algorithm"
	"fmt"
	"math/rand"
)

type Type int
type Value int

type Card struct {
	cardType  Type
	cardValue Value
}

const (
	Spade = iota
	Heart
	Diamond
	Club
)

const (
	Two = iota
	Three
	Four
	Five
	Six
	Seven
	Eight
	Nine
	Ten
	Knave
	Queen
	King
	Ace
)

var cardTypes = [...]string{"Spade", "Heart", "Diamond", "Club"}
var cardValues = [...]string{"Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Knave", "Queen", "King", "Ace"}

const defaultCount = 100

func NewCard(cardType Type, cardValue Value) *Card {
	return &Card{cardType, cardValue}
}

func NewDeck() []Card {
	deck := make([]Card, 52)
	i := 0

	for t := Spade; t <= Club; t++ {
		for v := Two; v <= Ace; v++ {
			deck[i] = Card{Type(t), Value(v)}
			i++
		}
	}

	return deck
}

func NewShuffledDeck() []Card {
	return NewShuffledCountDeck(defaultCount)
}

func NewShuffledCountDeck(count int) []Card {
	return ShuffleCount(NewDeck(), count)
}

func (c *Card) SetType(cardType Type) {
	if cardType < Spade || cardType > Club {
		panic("invalid card type!...")
	}

	c.cardType = cardType
}

func (c *Card) GetType() Type {
	return c.cardType
}

func (c *Card) SetValue(cardValue Value) {
	if cardValue < Two || cardValue > Ace {
		panic("invalid card value!...")
	}

	c.cardValue = cardValue
}

func (c *Card) GetValue() Value {
	return c.cardValue
}

func ShuffleCount(deck []Card, count int) []Card {
	length := len(deck)

	for i := 0; i < count; i++ {
		algorithm.Swap(&deck[rand.Intn(length)], &deck[rand.Intn(length)])
	}

	return deck
}

func Shuffle(deck []Card) []Card {
	return ShuffleCount(deck, defaultCount)
}

func (c *Card) String() string {
	return fmt.Sprintf("%s-%s", cardTypes[c.cardType], cardValues[c.cardValue])
}
```

## WEB NOTES

is an identifier which is used with constant and which can simplify constant definitions that use auto increment numbers.

The **IOTA** keyword represent integer constant starting from zero.

Auto increment constant without IOTA

```go
const (
    a = 0
    b = 1
    c = 2
)
```

Auto increment constant with IOTA

```go
const (
    a = iota
    b
    c
)
```

Both will set

```go
a=0
b=1
c=2
```

So IOTA is

- **A counter which starts with zero**
- **Increases by 1 after each line**
- **Is only used with constant**

## **More about IOTA**

* Iota keyword can be used on each line as well. In that case, also iota will start from zero and increment on each new line.

```go
const (
	a = iota
	b = iota
	c = iota
)
```

will output

```go
0
1
2
```

* iota keyword can be skipped as well. In that case, also iota will start from zero and increment on each new line.

```go
const (
    a = iota
    b
    c = iota
)
```

will output

```go
0
1
2
```

*  There will be no increment if there is a empty line or a commented line

```go
const (
	a = iota

	b
	//comment
	c
)
```

will output

```go
0
1
2
```

-  Iota value will reset and again start with zero if the const keyword is used again

```go
const (
	a = iota
	b
)
const (
	c = iota
)
```

will output

```none
0
1
0
```

- iota increment can be skipped using a blank identifier

```go
const (
	a = iota
	_
	b
	c
)
```

will output

```go
0
2
3
```

- iota expressions – iota allows expressions which can be used to set any value for the constant

```go
package main

import "fmt"

const (
	a = iota
	b = iota + 4
	c = iota * 4
)

func main() {
	fmt.Println(a)
	fmt.Println(b)
	fmt.Println(c)
}
```

will output

```go
0
5
8
```

- iota can also start from non-zero number- iota expressions can also be used to start iota from any number

```go
const (
	a = iota + 10
	b
	c
)
```

will output

```go
10
11
12
```


# **Enum in Golang**

**IOTA** provides an automated way to create a enum

```go
package main

import "fmt"

type Size uint8

const (
	small Size = iota
	medium
	large
	extraLarge
)

func main() {
	fmt.Println(small)
	fmt.Println(medium)
	fmt.Println(large)
	fmt.Println(extraLarge)
}
```

```go
fmt.Println(small)      >> outputs 0  
fmt.Println(medium)     >> outputs 1
fmt.Println(large)      >> outputs 2
fmt.Println(extraLarge) >> outputs 3
```



---


# FUNCTIONS

## Fonksiyon Bildirimi ve Tanımlaması

Fonksiyon bildirimi (function declaration), genellikle fonksiyonun isminin, parametrik yapısının ve geri dönüş değerinin (ya da değerleri) derleyiciye tanıtılmasıdır. Fonksiyon tanımlaması (function definition) ise fonksiyonun gövdesiyle beraber yazılmış halidir.

Scan, Scanf ve Scanln fonksiyonlarının parametrelerine içerisini doldurmak üzere bir nesnenin adresi geçilmelidir. Bu anlamda bir değişkenin adresini almak için ``address of (&)`` isimli tek operandlı bir operator kullanılır. Bir değişkenin adresi bu operatör kullanılarak bu fonksiyonlara geçirilir.

Geri dönüş değeri olan fonksiyonlarda `return` deyimi tek başına kullanılamaz. Geri dönüş değeri olan fonksiyonlarda akışın her noktasında `return` deyimi olmalıdır. Aksi durumda fonksiyon bildiriminde derleme zamanında hata oluşur. `return` deyimi nasıl kullanılırsa kullanılsın fonksiyonu sonlandırır.

```go
package main

import "fmt"

func main() {
    result := sum() * 2

    fmt.Println("result =", result)
}

func sum() int {
    var a, b int

    fmt.Print("İki sayı giriniz:")
    fmt.Scan(&a, &b)

    total := a + b

    return total
}
```

***Bir fonksiyonun geri dönüş değeri, geçici bir değişkene (temporary variable) yapılan bir atama işlemidir.***
Bu değişken, geçici bir değişkendir, çünkü fonksiyondan sonra bellekten silinir.

Fonksiyonların parametre değişkenleri (ya da kısa parametreleri), fonksiyon isminde parantez içerisinde bildirilen değişkenlerdir.
Fonksiyonların parametre değişkenleri de isim ve tür ile bildirilir ve virgül ile birbirinden ayrılır.
Parametre değişkenleri aynı türdense ve peşpeşe bildiriliyorsa bir kez tür ismi yazmak yeterlidir.

Fonksiyon çağrısında parametrelere aktarılan değerlere argüman (argument) denir.

```go
package main

import "fmt"

func main() {
    var a, b int
    fmt.Print("İki sayı giriniz")
    fmt.Scan(&a, &b)

    display(a, b)
    fmt.Print(a, " + ", b, " = ", sum(a, b))
}

func sum(a, b int) int {
    return a + b
}

func display(a int, b int) {
    fmt.Println("a =", a, "b =", b)
}
```

### Fonksiyonun Geri Dönüş Değeri Yoksa ve Birden Fazla Değer Dönme Durumu

Fonksiyonun geri dönüş değeri yoksa, `return` deyimi zorunlu değildir. Ancak istenirse fonksiyonu sonlandırmak için tek başına (yani ifade olmadan) kullanılabilir.

```go
package main

import "fmt"

func main() {
    var a int
    fmt.Print("Bir sayı giriniz:")
    fmt.Scan(&a)

    displayIfPositive(a)
}

func displayIfPositive(a int) {
    if a < 0 {
        return
    }

    fmt.Println(a)
}
```

### Fonksiyonun Birden Fazla Değer Dönme Durumu

Go'da bir fonksiyon birden fazla değere geri dönebilir. Bu durumda geri dönüş değeri bilgisi yerine türler parantez içerisinde virgül ile yazılabilir. `return` deyiminde ise ifadeler virgül ile ayrılır.

```go
package main

import "fmt"

func main() {
    var a, b int
    fmt.Print("İki sayı giriniz:")
    fmt.Scan(&a, &b)

    x, y := swapped(a, b)

    fmt.Println("x =", x, "y =", y)
}

func swapped(a, b int) (int, int) {
    return b, a
}
```

```go
package main

import "fmt"

func main() {
    run()
}

func run() {
    var a, b int
    fmt.Print("İki tane sayı giriniz:")
    fmt.Scan(&a, &b)

    fmt.Println(getAddSubtractMultiply(a, b))
}

func getAddSubtractMultiply(a, b int) (int, int, int) {
    return a + b, a - b, a * b
}
```

Go'da bir fonksiyonun geri dönüş değerine isim de verilebilmektedir.

```go
func sum(a, b int) (total int) {
	return a + b
}
```

>Go'da bir fonksiyon bir parametre açısından iki şekilde çağrılabilir: call by value, call by reference. Bir fonksiyona bir nesnenin adresi veriliyorsa o parametre için call by reference yapılmış olur. Aksi durumda call by value yapılmış olur.

```go
// Örnek: Call by value
func main() {
    a := 5
    modifyValue(a)
    fmt.Println("Original:", a)
}

func modifyValue(x int) {
    x = 10
    fmt.Println("Modified:", x)
}

// Örnek: Call by reference
func main() {
    a := 5
    modifyValue(&a)
    fmt.Println("Modified:", a)
}

func modifyValue(x *int) {
    *x = 10
}
```

# Printf Fonksiyonu ve Formatlanmış Yazı Gönderimi

Go'da `Printf` fonksiyonu ile `stdout`'a formatlanmış bir yazı gönderilebilir. `Printf` fonksiyonunun birinci parametresi bir yazı (string) olmalıdır. Bu parametre format parametresidir. `%` karakteri ile birlikte özel bazı karakterler yer tutucu (placeholder) anlamında kullanılır ve bunlara genel olarak format specifiers denilmektedir.

```go
package main

import "fmt"

func main() {
    name := "John"
    age := 25

    fmt.Printf("Hello, my name is %s and I'm %d years old.\n", name, age)
}
```

# Fonksiyon Adresi ve Function Type

Bir process'in makine kodları (genellikle fonksiyonlar) kod bölümünde (code section) bulunur. Bu durumda bir fonksiyon çağrısı aslında ilgili fonksiyonun kodlarının bulunduğu adrese jump işlemidir. Bu durumda fonksiyonun bir adresi vardır ve genellikle fonksiyonun ismi ile erişilebilir.

Go'da bir fonksiyonun adresini tutabilen "function type" bulunur. Fonksiyon türleri aslında bir çeşit pointer biçimindedir (function pointer).

# Fonksiyon Türü Bildirimi

```go
func ([parametre listesi]) [geri dönüş değeri bilgisi] // -> Tür bildirimi
```

Fonksiyon türlerinde parametre değişkenlerine isim verilmesi zorunlu değildir.

Bir fonksiyonun parametresi de bir fonksiyon türünden olabilir. High-order function, VIP functions vb. Bu tarz fonksiyonların parametre olarak aldıkları fonksiyonlara callable/callback denir.

```go
func ([parametre listesi]) [geri dönüş değeri bilgisi] {
    //...
}
```

# Higher-Order Functions in Go

```go
func main() {
    a := []int{1, 2, 3, 4, 5, 6, 7, 8}

    // forEach function example
    forEach(a, func(a int) { fmt.Printf("%d ", a) })
    fmt.Println()

    // sumSliceIf function examples
    fmt.Println(sumSliceIf(a, func(a int) bool { return a%2 == 0 }))  // Sum of even numbers
    fmt.Println(sumSliceIf(a, func(a int) bool { return a%2 != 0 }))  // Sum of odd numbers

    // reduceSlice function examples
    fmt.Println(reduceSlice(a, func(a, b int) int { return a + b }))  // Sum of all elements
    fmt.Println(reduceSlice(a, func(a, b int) int { return a * b }))  // Product of all elements
}

// forEach function: Iterates over each element in a slice and applies the given function
func forEach(a []int, f func(int)) {
    for _, val := range a {
        f(val)
    }
}

// sumSliceIf function: Sums the elements in a slice based on a given predicate function
func sumSliceIf(a []int, pred func(int) bool) int {
    total := 0

    for _, val := range a {
        if pred(val) {
            total += val
        }
    }

    return total
}

// reduceSlice function: Reduces the elements in a slice using a given binary function
func reduceSlice(a []int, f func(int, int) int) int {
    result := a[0]

    for _, val := range a {
        result = f(result, val)
    }

    return result
}
```

# Anonymous Functions and Function Types

## Capture in Anonymous Functions

In anonymous functions, local variables and parameters declared before them can be used. This concept is known as "capture."

```go
func main() {
    a := []int{1, 2, 3, 4, 5, 6, 7, 8}
    var val int
    fmt.Print("Input a value:")
    fmt.Scan(&val)

    // forEach function with anonymous function
    forEach(a, func(val int) { fmt.Printf("%d ", val) })
    fmt.Println()

    // reduceSlice function with anonymous function and captured variable
    fmt.Println(reduceSlice(a, func(r, value int) int { return r + value + val }))
    fmt.Printf("val = %d\n", val)
}
```

Captured variables can be modified within the anonymous function.

## Returning a Function from a Function

A function can return a function of a function type.

```go
func main() {
    a := []int{1, 2, 3, 4, 5, 6, 7, 8}
    var val int
    fmt.Print("Input a value:")
    fmt.Scan(&val)

    // forEach function with anonymous function
    forEach(a, func(val int) { fmt.Printf("%d ", val) })
    fmt.Println()

    // reduceSlice function with a function returned from another function
    fmt.Println(reduceSlice(a, getFunction(val)))
    fmt.Printf("val = %d\n", val)
}

func getFunction(val int) func(int, int) int {
    return func(a, b int) int { return a + b + val }
}

```

## Type Aliases for Function Types

Function types can be given type aliases for better readability.

```go
type IntUnaryPredicate func(int) bool
type IntBinaryOperator func(int, int) int
type IntConsumer func(int)

func main() {
    a := []int{1, 2, 3, 4, 5, 6, 7, 8}
    var val int
    fmt.Print("Input a value:")
    fmt.Scan(&val)

    // forEach function with IntConsumer type alias
    forEach(a, func(val int) { fmt.Printf("%d ", val) })
    fmt.Println()

    // reduceSlice function with IntBinaryOperator type alias
    fmt.Println(reduceSlice(a, func(r, value int) int { return r + value + val }))
    fmt.Printf("val = %d\n", val)
}

func forEach(a []int, f IntConsumer) {
    for _, val := range a {
        f(val)
    }
}

func sumSliceIf(a []int, pred IntUnaryPredicate) int {
    total := 0

    for _, val := range a {
        if pred(val) {
            total += val
        }
    }

    return total
}

func reduceSlice(a []int, f IntBinaryOperator) int {
    result := a[0]

    for _, val := range a {
        result = f(result, val)
    }

    return result
}

```

### WEB NOTES
---
# Functions in Go

A function in Go is a group of statements that perform a specific task. Functions in Go are first-order variables, meaning they can be passed around like any other variable.

## Function Naming Conventions

- A function whose name starts with a capital letter will be exported outside its package and can be called from other packages.
- A function whose name starts with lowercase letters will not be exported and is only visible within its package.

## Function Signature

The signature of a function in Go is as follows:

```go
func funcName(inputParameters) returnValues {}
```

## Calling a Function

- When calling a function from another package, the package name must be prefixed in uppercase.
- Within the same package, the function can be called directly using its name suffixed by ().

## Function Parameters

- Types for consecutive same types can be specified only once (e.g., `func sum(a, b int)`).
- A copy of all arguments is made while calling a function.

## Return Values

- A function can have one or more return values (e.g., `func sumAvg(a, b int) (int, int)`).
- Error is conventionally returned as the last argument in a function.

### Named Return Values

- Named return values don't need to be initialized in the function; they are specified in the signature.

```go
func sum(a, b int) (result int)
```

## Function Usages

- Generic Usage
- Function as Type
- Function as Values

### Function as Type

- In Go, a function is also a type.
- Two functions are of the same type if they have the same number and type of arguments and the same number and type of return values.
- Useful in higher-order functions and defining interfaces.

### Function as Value (Anonymous Functions)

- A function in Go is a first-order variable and can be used as a value.
- Also called anonymous functions because they are not named and can be assigned to variables and passed around.

```go
var max = func(a, b int) int {
    if a >= b {
        return a
    }
    return b
}

func main() {
    res := max(2, 3)
    fmt.Println(res)
}

```

### Special Usages of Function

#### Function Closures

- Anonymous functions that can access variables declared outside the function and retain values between different calls.

```go
func getModulus() func(int) int {
    count := 0
    return func(x int) int {
        count++
        fmt.Printf("modulus function called %d times\n", count)
        if x < 0 {
            x = x * -1
        }
        return x
    }
}
```

#### Higher Order Function

- Functions that either accept a function as a type or return a function.
- Can be passed around, returned from functions, and assigned to variables.

```go
func getAreaFunc() func(int, int) int {
    return func(x, y int) int {
        return x * y
    }
}

```

#### Immediately Invoked Function (IIF)

- Functions that are defined and executed at the same time.

```go
func main() {
    squareOf2 := func() int {
        return 2 * 2
    }()
    fmt.Println(squareOf2)
}

```

##### Use Cases of IIF Functions

- When you don't want to expose the logic of the function either within or outside the package (encapsulation).

#### Variadic Function

- A function that can accept a dynamic number of arguments.

```go
func add(numbers ...int)

fmt.Println(add(1, 2))
fmt.Println(add(1, 2, 3))
fmt.Println(add(1, 2, 3, 4))

```


---

# PRINTF

# Printf Function in Golang

In Golang, the `Printf` function can format and print values of various types. Here are the types it can handle:

## Basic Types:
- int
- float64
- string
- bool
- byte
- rune
- complex128
- complex64

## Composite Types:
- struct
- interface
- map
- channel
- slice

```go
package main

import "fmt"

func main() {
    // int
    i := 123
    fmt.Printf("%d\n", i)
    // float64
    f := 3.1415
    fmt.Printf("%f\n", f)
    // string
    s := "Merhaba, dünya!"
    fmt.Printf("%s\n", s)
    // bool
    b := true
    fmt.Printf("%t\n", b)
    // byte
    c := byte('a')
    fmt.Printf("%c\n", c)
    // rune
    r := rune('A')
    fmt.Printf("%c\n", r)
    // complex128
    z := complex128(1 + 2i)
    fmt.Printf("%v\n", z)
    // complex64
    w := complex64(1 + 2i)
    fmt.Printf("%v\n", w)
}
```

Output:

```
123
3.1415
Merhaba, dünya!
true
a
A
(1+2i)
(1+2i)
```

# Tips and Tricks for Printf in Golang

In Golang's `Printf` function, you can use various format specifiers to control the output format:

- `%v`: Prints the value of the variable in the default format.
- `%+v`: Prints the value of the variable in a detailed format.
- `%#v`: Prints the value of the variable in a Go source code-like format.
- `%T`: Prints the type of the variable.
- `%s`: Prints the value of the variable as a string.
- `%p`: Prints the address of the variable.

```go
package main

import "fmt"

func main() {
    // Variables to print
    i := 123
    f := 3.1415
    s := "Merhaba, dünya!"
    b := true
    c := byte('a')

    // Print variables with format specifiers
    fmt.Printf("%d\n", i) // 123
    fmt.Printf("%f\n", f) // 3.1415
    fmt.Printf("%s\n", s) // Merhaba, dünya!
    fmt.Printf("%t\n", b) // true
    fmt.Printf("%c\n", c) // a

    // Advanced formatting with additional parameters
    fmt.Printf("%.2f\n", f)  // 3.14
    fmt.Printf("%02d\n", i)  // 0123
    fmt.Printf("%-5d\n", i)  // 123

    // Advanced features with format specifiers
    fmt.Printf("%+v\n", s) // "Merhaba, dünya!"
    fmt.Printf("%#v\n", s) // "string"
    fmt.Printf("%T\n", s)  // string
}
```

In the `Printf` function, when a digit is placed between `%` and the format character (e.g., `%02d`), it represents alignment.

```go
func main() {
    var day, month, year int

    fmt.Print("Input date values:")
    fmt.Scan(&day, &month, &year)

    fmt.Printf("%02d.%02d.%04d\n", day, month, year)
}

```

For floating-point types, like `%f`, you can specify the number of decimal places to format the value.

```go
func main() {
    var val float64

    fmt.Print("Input a value:")
    fmt.Scan(&val)

    fmt.Printf("val = %.10f\n", val)
}
```

Integers can be formatted in various number systems (base/radix). For example, use `%x` or `%X` for hexadecimal, `%o` or `%O` for octal.

```go
func main() {
    var val int

    fmt.Print("Input a value:")
    fmt.Scan(&val)

    fmt.Printf("val = %d\n", val)
    fmt.Printf("val = %x\n", val)
    fmt.Printf("val = %X\n", val)
    fmt.Printf("val = %b\n", val)
    fmt.Printf("val = %o\n", val)
    fmt.Printf("val = %O\n", val)
}
```

# Printf Double Percent and Scanf in Golang

## Printf Double Percent

If you want to include a percent character in the formatted string using `Printf`, you can achieve this by using two consecutive percent characters (``%%``))

```go
package main

import "fmt"

func main() {
    var midTermRatio, finalRatio int

    fmt.Print("Input midterm and final ratios:")
    fmt.Scan(&midTermRatio, &finalRatio)

    fmt.Printf("Midterm ratio:%%%d, Final ratio:%%%d\n", midTermRatio, finalRatio)
}
```


## Scanf in Golang

In Golang's `fmt` package, there is a function called `Scanf` for formatted reading from stdin. The format characters are mostly the same as in `Printf`.

```go
func main() {
    var midTermRatio, finalRatio int

    fmt.Print("Input midterm and final ratios:")
    fmt.Scan(&midTermRatio, &finalRatio)

    fmt.Printf("Midterm ratio:%%%d, Final ratio:%%%d\n", midTermRatio, finalRatio)
}


```

---

# LITERALS

In programming, literals are values directly written in the source code. Constants are expressions that consist of literals, operators, and variables. Literals can be written directly in the code and assigned to variables or passed as parameters to functions.

Here are different types of literals in Go:

- **Integer Literals:** Represent integer values. Examples: `123`, `456`, `-789`.
- **Floating Point Literals:** Represent decimal numbers. Examples: `3.1415`, `12.3456`, `-7.8901`.
- **Complex Literals:** Represent complex numbers. Examples: `3.1415`, `12.3456`, `-7.8901`.
- **Boolean Literals:** Represent `true` or `false`.
- **Rune Literals:** Represent characters enclosed in single quotes. Examples: `'A'`, `'b'`, `'3'`.
- **String Literals:** Represent text strings. Examples: `"Hello, World!"`, `"This is a string."`, `"1234567890"`.

Constants, consisting of literals, operators, and variables, are referred to as constant expressions. A constant by itself is also a constant expression.

Numeric constants can be further classified into integer, floating-point, complex, and rune constants.

- If a number does not contain a decimal point and is within the limits, it is an integer constant. Overflow results in an error.
- If a number contains a decimal point, it is a floating-point constant.

Rune constants generally represent characters, and they are enclosed in single quotes. They actually represent the ordinal number (Unicode code point) of the character.

Some characters cannot be directly printed to the standard output. These characters are called non-printable or common escape sequence characters.

- `'\a'`: Alert/Bell
- `'\b'`: Backspace
- `'\f'`: Form Feed
- `'\n'`: Line Feed/New Line (LF)
- `'\r'`: Carriage Return (CR)
- `'\t'`: Horizontal Tab
- `'\v'`: Vertical Tab
- `'\\'`: Backslash

```go
package main

import "fmt"

func main() {
    fmt.Print("\"Hello, World\"\a\n")
    fmt.Print("'Goodbye, World'\a\n")
}
```

In Go, you can use underscores between digits of constants, which enhances readability.

```
const million = 1_000_000
const billion = 1_000_000_000
const trillion = 1_000_000_000_000
```

---

# OPERATORS

Operatörler, bir işleme yol açan ve işlem sonucunda bir değer üreten atomlardır. Bir operatör ile işleme giren ifadelere ise operand denir.

## İşlevine Göre Sınıflandırma

### Aritmetik Operatörler (Arithmetic Operators)

Sayılarla matematiksel işlemler yapar.

- `+`: Toplama
- `-`: Çıkarma
- `*`: Çarpma
- `/`: Bölme
- `%`: Mod (Kalan)

### Karşılaştırma Operatörleri (Comparison Operators)

İki değeri karşılaştırır.

- `==`: Eşitse
- `!=`: Eşit değilse
- `<`: Küçükse
- `>`: Büyükse
- `<=`: Küçük veya eşitse
- `>=`: Büyük veya eşitse

### Mantıksal Operatörler (Logical Operators)

İki değeri mantıksal olarak karşılaştırır.

- `&&`: VE (AND)
- `||`: VEYA (OR)
- `!`: DEĞİL (NOT)

### Bitsel Operatörler (Bitwise Operators)

Sayıların bitlerini manipüle eder.

- `&`: Bitwise AND
- `|`: Bitwise OR
- `^`: Bitwise XOR
- `~`: Bitwise NOT
- `<<`: Left Shift
- `>>`: Right Shift

### Özel Amaçlı Operatörler (Special Purpose Operators)

- `...`: Ellipsis (slicing, varargs)
- `&`: Adres alma (Address of)
- `*`: İçerik (Dereference)
- `new`: Yeni bir örnek oluşturma

## Operand Sayısına Göre Sınıflandırma

### Tek Operandlı (Unary)

- `++`, `--`: Bir arttırma ve bir azaltma
- `+`, `-`: İşaret değiştirme, negatif alma
- `!`: Mantıksal DEĞİL (NOT)
- `*`: İçerik (Dereference)
- `&`: Adres alma
- `^`: Bitwise NOT
- `~`: Tersleme (Negation)

### İki Operandlı (Binary)

- `==`, `!=`: Eşitlik ve eşitsizlik
- `<`, `>`: Küçüklük ve büyüklük
- `<=`, `>=`: Küçük veya eşitlik, büyük veya eşitlik
- `&&`: VE (AND)
- `||`: VEYA (OR)
- `+=`, `-=`, `*=`, `/=`, `%=`: Atama ile işlem
- `&=`, `|=`, `^=`: Bitsel atama ile işlem
- `<<`, `>>`: Left Shift ve Right Shift

### Üç Operandlı (Ternary)

- ?: Koşul operatörü (conditional operator)

## Operatörün Konumuna Göre Sınıflandırma

### Önek (Prefix)

Operatör operandın önünde gelir.

- `++`, `--`, `+`, `-`, `!`, `&`, `^`, `~`

### Araek (Infix)

Operatör operandların arasında gelir.

- `==`, `!=`, `<`, `>`, `<=`, `>=`, `&&`, `||`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`

### Sonek (Postfix)

Operatör operandın arkasında gelir.

- `++`, `--`

## Diğer Özellikler

- Atama Operatörleri: `=`, `:=`
- Atama operatörü sağdan sola önceliklidir (right associative).
- Atama operatörü bir değer üretmez.
- Atama operatörlerinin birinci operandı bir sol taraf değeri (lvalue) olmalıdır.
- Sonlandırıcı (terminator) olarak yeni satır kullanmak veya `;` kullanmak mümkündür. Ancak, `;` kullanımını genellikle programcılar tercih etmezler.
- Etkisiz ifadeler genellikle derleme zamanında bir hata oluşturur ("code has no effect").

```go
package main

import "fmt"

func main() {
    var a, b = 10, 20

    a + b // Error: code has no effect
}

```

---

# STATEMENTS

## Basit Deyimler (Simple Statements)

Basit deyimler, bir ifadenin sonuna noktalı virgül konması ve bir sonraki satıra geçilmesi ile oluşan deyimdir. Basit deyim çalıştırıldığında ilgili ifade hesaplanır.

## Bileşik Deyimler (Compound Statements)

Bileşik deyimler, bir bloğa denir. Fonksiyon gövdesi de bir bileşik deyimdir. Bileşik deyim çalıştırıldığında blok içerisindeki tüm deyimler sırasıyla çalıştırılır.

## Bildirim Deyimleri (Declaration Statements)

Bildirim deyimleri, değişken bildirimine ilişkin deyimlerdir. Bildirim deyimleri çalıştırıldığında bellekte yer ayrılır.

## Kontrol Deyimleri (Control Statements)

Kontrol deyimleri, akışın yönlendirilmesine yol açan deyimlerdir. Bu deyimler arasında `if`, `else`, `switch`, `for`, `break`, `continue` gibi yapılar bulunur.

## Boş Deyim (Empty/Null Statement)

Go'da çok kullanılmasa da `;` kendisi bir boş deyimdir. Boş deyim çalıştırıldığında hiçbir şey yapılmaz.

## IF
```go
func main() {
    var a int
    fmt.Print("Enter a number:")
    fmt.Scan(&a)

    if a%2 == 0 {
        fmt.Println("You entered an even number!")
    } else {
        fmt.Println("You entered an odd number!")
    }

    fmt.Println("Do you want to try again?")
}

```

```go
func main() {
    var a int
    fmt.Print("Enter a number:")
    fmt.Scan(&a)

    if a > 0 {
        fmt.Println("You entered a positive number")
    } else if a == 0 {
        fmt.Println("You entered zero")
    } else {
        fmt.Println("You entered a negative number")
    }

    fmt.Println("Do you want to try again?")
}

```

```go
package main

import (
    "fmt"
    "math"
)

func main() {
    runApp()
}

func runApp() {
    var a, b, c float64
    fmt.Print("Enter the coefficients:")
    fmt.Scan(&a, &b, &c)

    status, x1, x2 := findQuadraticEquationRoots(a, b, c)

    if status {
        fmt.Printf("Root 1 (x1) = %f, Root 2 (x2) = %f\n", x1, x2)
    } else {
        fmt.Println("No real roots")
    }
}

func findQuadraticEquationRoots(a, b, c float64) (bool, float64, float64) {
    delta := b*b - 4*a*c

    if delta > 0 {
        sqrtDelta := math.Sqrt(delta)
        return true, (-b + sqrtDelta) / (2 * a), (-b - sqrtDelta) / (2 * a)
    }

    if delta == 0 {
        return true, -b / (2 * a), -b / (2 * a)
    }

    return false, 0, 0
}

```

### WEB NOTES
---
In Go, you can use a short statement before the condition in an `if` statement
```go
package main

import "fmt"

func main() {
    if a := 6; a > 5 {
        fmt.Println("a is greater than 5")
    }
}

```

---

# LOOPS

### For Loop in Go

In Go, only the `for` loop statement is available. There are no classical `while` or `do-while` loops. The `for` loop in Go can be used to cover the functionality of `while` loops.

The general form of the `for` loop statement is as follows:

```go
for [bool expression] {
    //...
}

```

```go
package main

import "fmt"

func main() {
    var n int
    fmt.Print("Input a number:")
    fmt.Scan(&n)
    i := 0

    for i < n {
        fmt.Printf("%d ", i)
        i++
    }

    fmt.Println()
    fmt.Println("Tekrar yapıyor musunuz?")
}

```

In Go, the assignment operator does not specify an expression, and therefore, it does not produce a value. For this reason, the loop would be invalid if it contained an assignment operation.

#### Infinite Loop:

An infinite loop is a loop that cannot terminate due to its condition. It can be created using `for true` or `for {}`.

```go
func main() {
    for true {
        // Infinite loop
    }
}

```

To exit a loop in Go, you can use the `break` statement.

```go
func findTotal() int {
    var val int

    total := 0

    for {
        fmt.Scan(&val)

        if val == 0 {
            break
        }

        total += val
    }

    return total
}

```

The `break` statement can be used to terminate the loop it is used within. For a labeled `break` statement, a label declaration is required immediately before the loop it is used in.

```go
func main() {
    exitLoop:
    for i := 0; i < 20; i++ {
        for k := 40; k >= 0; k-- {
            fmt.Printf("(%d, %d)\n", i, k)
            if (i+k)%6 == 0 {
                break exitLoop
            }
        }
    }

    fmt.Println("Tekrar yapıyor musunuz?")
}

```

The `continue` statement is used within a `for` loop to skip the rest of the loop's code block and move to the next iteration.

```go
func reverseNumber(val int) int {
    result := 0

    for val != 0 {
        result = result*10 + val%10
        val /= 10
    }

    return result
}

```

### For Loop Structure

The general structure of the `for` loop in Go is as follows:

```go
for [1st part]; [2nd part]; [3rd part] {
    //...
}
```

- **1st part:** Executed before the loop starts, typically used for variable initialization.
- **2nd part:** The loop condition, a boolean expression that is evaluated before each iteration.
- **3rd part:** Executed after each iteration, often used for incrementing or decrementing loop counters.

```go
for i := 0; i < n; i++ {
    fmt.Printf("%d ", i)
}
```

#### Shadowing Variables:

Be cautious when using a loop variable with the same name as a variable declared outside the loop, as it will shadow the outer variable.

```go
func main() {
    var n int
    fmt.Print("Bir sayı giriniz:")
    fmt.Scan(&n)

    i := 67

    for i := 0; i < n; i++ {
        fmt.Printf("%d ", i)
    }

    fmt.Printf("\ni = %d\n", i)
}
```

### Examples of Functions Using `for` Loop:

#### 1. Factorial Calculation:

```go
func factorial(n int) int {
    result := 1

    for i := 2; i <= n; i++ {
        result *= i
    }

    return result
}
```

#### 2. Fibonacci Number Calculation:
```go
func fibonacciNumber(n int) int {
    if n <= 2 {
        return n - 1
    }

    prev1, prev2 := 1, 0
    value := prev1 + prev2

    for i := 3; i < n; i++ {
        prev2 = prev1
        prev1 = value
        value = prev1 + prev2
    }

    return value
}
```


### WEB NOTES
---

### For Loop in Go

The `for` loop in Go has the following general structure:

```go
for [init_part]; [condition_part]; [post_part] {
   //...
}
```

- The `init_part` is executed first before the first iteration.
- The `condition_part` is executed before every iteration.
- The `post_part` is executed after every iteration.

The `init_part` and `post_part` are optional. The `init_part` can be any statement with a short declaration, function call, or assignment. The `post_part` can be any statement but generally contains the increment logic. The `post_part` cannot contain initialization.

Go doesn't have a `while` keyword. Instead, it utilizes the `for` keyword, which can be implemented to behave like `while` if `init_part` and `post_part` are skipped.

```go
package main

import "fmt"

func main() {
   i := 0

   for i < 5 {
      fmt.Println(i)
      i++
   }
}
```

### For-Range Loop

The `for-range` loop is used to iterate over various collection data structures in Go, such as arrays, slices, strings, maps, and channels.

```go
for index, value := range array/slice {
   // Do something with index and value
}


for key, value := range map {
   // Do something with key and value
}


for value := range channel {
   // Do something with value
}
```

The `for-range` loop simplifies the iteration process, providing access to both the index/key and the corresponding value in the collection.

```go
package main

import "fmt"

func main() {
   numbers := []int{1, 2, 3, 4, 5}

   for index, value := range numbers {
      fmt.Printf("Index: %d, Value: %d\n", index, value)
   }
}
```

---

# SWITCH

### Switch Statement in Go

The `switch` statement in Go is divided into two categories:

1. **Expression Switch**: Performs operations based on the value of an expression.
2. **Type Switch**: Performs operations based on the type of an expression.

In Go, the `switch` statement does not have the fallthrough feature by default.

```go
package main

import "fmt"

func main() {
    var code int

    fmt.Print("Enter the area code:")
    fmt.Scan(&code)

    switch code {
    case 212, 216:
        fmt.Println("Istanbul")
    case 312:
        fmt.Println("Ankara")
    case 372:
        fmt.Println("Zonguldak")
    default:
        fmt.Println("Invalid area code!...")
    }

    fmt.Println("Do you want to repeat?")
}
```

In the above example, the `switch` statement is used to determine the city based on the area code.

### Fallthrough in Switch

Go allows the use of `fallthrough` to transfer control to the next case even if the current case matches. It needs to be the final statement within the `switch` block.

```go
package main

import "fmt"

func main() {
    var code int

    fmt.Print("Enter the area code:")
    fmt.Scan(&code)

    switch code {
    case 212:
        fmt.Print("Europe ")
        fallthrough
    case 216:
        fmt.Println("Istanbul")
    case 312:
        fmt.Println("Ankara")
    case 372:
        fmt.Println("Zonguldak")
    default:
        fmt.Println("Invalid area code!...")
    }

    fmt.Println("Do you want to repeat?")
}
```

In this example, the `fallthrough` statement is used to fall through to the next case after printing "Europe" for area code 212.

### Usage with `if` and `switch`

The usage of `if` and `switch` statements, as shown above, is preferred for enhancing readability and scoping variables.

```go
package main

import "fmt"

func main() {
    var n int

    fmt.Print("Enter two numbers:")
    fmt.Scan(&n)

    switch result := factorial(n); {
    case result > 10:
        fmt.Printf("%d! > 10\n", result)
    case result < 5:
        fmt.Printf("%d! <= 5\n", result)
    default:
        fmt.Printf("%d! is not in range\n", result)
    }

    fmt.Println("Do you want to repeat?")
}

func factorial(n int) int {
    result := 1

    for i := 2; i <= n; i++ {
        result *= i
    }

    return result
}
```

### WEB NOTES

---

Certainly! Here's the provided information about the scenarios and details of the `switch` statement and `switch` expression in Go, formatted as markdown:

### Four Possible Scenarios for `switch` Statement and `switch` Expression

#### 1. Both `switch` Statement and `switch` Expression Are Present

```go
switch statement; expression {
   //...
}

func main() {
    switch ch := "b"; ch {
    case "a":
        fmt.Println("a")
    case "b", "c":
        fmt.Println("b or c")    
    default:
        fmt.Println("No matching character")    
    }
}

```

#### Only `switch` Statement Is Present
```go
switch statement; {
    //...
}
```

#### Only `switch` Expression Is Present

```go
switch expression {
   //...
}

func main() {
    char := "a"
    switch char {
    case "a":
        fmt.Println("a")
    case "b":
        fmt.Println("b")
    default:
        fmt.Println("No matching character")
    }
}
```

#### Both `switch` Statement and `switch` Expression Are Absent
```go
switch {
  //...
}

func main() {
    age := 45
    switch {
    case age < 18:
        fmt.Println("Kid")
    case age >= 18 && age < 40:
        fmt.Println("Young")
    default:
        fmt.Println("Old")
    }
}
```

### Additional Details

- If the `switch` expression is not provided, the default type assumed by the compiler is boolean.
- The type of the `switch` expression and all of the case expressions should match; otherwise, there will be a compiler error. When the `switch` expression is not provided, the type of all case expressions needs to be a boolean too.
- The default case is optional.
- Case can have multiple expressions separated by a comma: `case expression1, expression2 ...:`
- The `case` block also allows the `fallthrough` keyword, which transfers control to the next case even though the current case might have matched. `fallthrough` needs to be the final statement within the `switch` block; otherwise, the compiler raises an error.
- `switch` statement can also be used as a type switch, where it is used to determine the type of an empty interface at runtime.

### Type Switch

```go
func printType(t interface{}) {
    switch v := t.(type) {
    case string:
        fmt.Println("Type: string")
    case int:
        fmt.Println("Type: int")
    default:
        fmt.Printf("Unknown Type %T", v)
    }
}

```

---

# TYPE CONVERSION

## Tür Dönüşümü (Type Conversion)

### Otomatik Tür Dönüşümü

Otomatik tür dönüşümü, derleyici tarafından, iki veri türünün uyumlu olması durumunda yapılır. Uyumlu veri türleri, aynı temel veri türüne sahip veya birbirleriyle ilişkili veri türleridir.

```go
var i int = 123
var f float64 = 3.1415

// i'yi f'ye dönüştürme
fmt.Println(float64(i)) // 123.0

// f'yi i'ye dönüştürme
i = int(f) // 123

```

### Manuel Tür Dönüşümü

Manuel tür dönüşümü, programcı tarafından, iki veri türünün uyumlu olmaması durumunda yapılır. Bu dönüşüm, `type()` operatörü kullanılarak yapılır.

```go
var i int = 123
var f float64 = float64(i) // 123.0

var f float64 = 3.1415
var i int = int(f) // 123
```

### İşlem Öncesi Otomatik Tür Dönüşümü

Go'da, untyped constant'lar dışında işlem öncesi otomatik tür dönüşümü yapılmaz.

```go
var a int = 10
var b = 4.5
var c float64 = a + b // error
```

### Tür Dönüştürme Operatörü

Tür dönüştürme operatörü ile genel olarak implicit olarak yapılamayan dönüşümler yapılabilir.

```go
<tür>(<ifade>)
```

Bu operatör özel amaçlı tek operandlı (unary) ve önek (prefix) durumundadır. Küçük işaretli tamsayı türünden büyük işaretli tamsayı türüne yapılan dönüşümde sayının yüksek anlamlı byte değerleri sayı pozitifse sıfır ile negatifse 1 ile beslenir.

Küçük işaretli tamsayı türünden büyük işaretsiz tamsayı türüne yapılan dönüşüm hedef işaretsiz tamsayı türünün işaretli olanına dönüştürülür ve elde edilen işaretsiz olarak yorumlanır.

### Adres Kavramı

Belleğin her bir byte'ına bir numara verilmiş olup, bellekteki nesnelerin de adresleri vardır. Adresin sayısal ve tür bileşenleri bulunur. Yazılımsal adres bilgisi iki bileşenli bir bilgidir: sayısal ve tür bileşeni.

```go
var a *int // int türden adres (pointer to int)
```

### Prosesin Adres Alanı ve Bölümleri

Prosesin adres alanı içerisinde stack, data, bss, ve heap gibi bölümler vardır. Stack, yerel ve parametre değişkenlerinin yaratıldığı ve yok edildiği alandır. Data, ilk değer verilmiş global nesnelerin yaratıldığı bölümdür. BSS, ilk değer verilmemiş global nesnelerin yaratıldığı bölümdür. Heap, dinamik bellek fonksiyonlarıyla tahsisat yapılan bölümdür.

### Nesnelerin Ömürleri

Ömür, bir nesnenin bellekte tutulduğu zaman aralığına denir. Statik ömürlü nesneler program çalışmak üzere belleğe yüklendiğinde yaratılır, program sonlanana kadar bellekte kalır. Dinamik ömürlü nesnelerin ömrü programın çalışma zamanından küçüktür.

## Bilgi

Bilgi işlem yapılamaması durumunda int32 türünden int64 türüne implicit conversion yapılamaz. Ancak untyped constant'lar için bu kural geçerli değildir.

```go
var a int = 10
var b int64 = a // error

```

Go'da untyped constant'lar dışında işlem öncesi otomatik tür dönüşümü yapılmaz.

```go
var a int = 10
var b = 4.5
var c float64 = a + b // error
```

Küçük işaretli tamsayı türünden büyük işaretli tamsayı türüne yapılan dönüşümde sayının yüksek anlamlı byte değerleri sayı pozitifse sıfır ile negatifse 1 ile beslenir.

Büyük işaretli tamsayı türünden küçük işaretli tamsayı türüne yapılan dönüşümde sayının yüksek anlamlı byte değerleri atılır, elde edilen sayı atanır. Bu durumda bilgi kaybı oluşabilir.

---
# DEFER

//...

### WEB NOTES

Defer  is used to defer the cleanup activities in a function. These cleanup activities will be performed at the end of the function.
This cleanup activities will be done in a different function called by defer.  This different function is called at the end of the surrounding function before it returns.

```go
defer {function_or_method_call}
```

Things to note about defer function

- Execution of a deferred function is delayed to the moment the surrounding function returns
- deferred function will also be executed if the enclosing function terminates abruptly. For example in case of a panic

```go
package main

import (
    "fmt"
    "log"
    "os"
)

func main() {
    err := writeToTempFile("Some text")
    if err != nil {
        log.Fatalf(err.Error())
    }
    fmt.Printf("Write to file succesful")
}

func writeToTempFile(text string) error {
    file, err := os.Open("temp.txt")
    if err != nil {
        return err
    }
    n, err := file.WriteString("Some text")
    if err != nil {
        return err
    }
    fmt.Printf("Number of bytes written: %d", n)
    file.Close()
    return nil
}
```

in the **writeToTempFile** function, we are opening a file and then trying to write some content to the file. After we have written the contents of the file we close the file. It is possible that during the write operation it might result into an error and function will return without closing the file. **Defer** function helps to avoid these kinds of problems. **Defer** function is always executed before the surrounding function returns

**Defer Version**

```go
package main

import (
    "fmt"
    "log"
    "os"
)

func main() {
    err := writeToTempFile("Some text")
    if err != nil {
        log.Fatalf(err.Error())
    }
    fmt.Printf("Write to file succesful")
}

func writeToTempFile(text string) error {
    file, err := os.Open("temp.txt")
    if err != nil {
        return err
    }
    defer file.Close()

    n, err := file.WriteString("Some text")
    if err != nil {
        return err
    }
    fmt.Printf("Number of bytes written: %d", n)
    return nil
}
```

**defer file.Close()** after opening the file. This will make sure that closing of the file is executed even if the write to the file results into an error. Defer function makes sure that the file will be closed regardless of number of return statements in the function

# **Custom Function in defer**

We can also call a custom function in **defer**

```go
package main
import "fmt"
func main() {
    defer test()
    fmt.Println("Executed in main")
}
func test() {
    fmt.Println("In Defer")
}
```

**Output**

```go
Executed in main
In Defer
```

a **defer** statement calling the custom function named **test**. As seen from the output, the **test** function is called after everything in the main is executed and before main returns

# **Inline Function in Defer**

```go
package main

import "fmt"

func main() {
    defer func() { fmt.Println("In inline defer") }()
    fmt.Println("Executed")
}
```

**Output**

```go
Executed
In inline defer
```

```go
defer func() { fmt.Println("In inline defer") }()
```

This is allowed in go. Also note that it is mandatory to add **“()”** after the function otherwise compiler will raise error

```go
expression in defer must be function call
```

# **How does defer works**

==When the the compiler encounter a defer statement in a function it pushes it onto a list. This list internally implements a stack data structure.  All the encountered defer statement in the same function are pushed onto this list. When the surrounding function returns then all the functions in the stack starting from top to bottom are executed before execution can begin in the calling function. Now same thing will happen in the calling function as well.==

Imagine a function call from **main** function to **f1** function to **f2** function

**main**->**f1**->**f2**

Below is the sequence that will be happening after f2 returns

- Defer functions in **f2** will be executed if present. Control will return to the caller which is a function **f1**.

- Defer functions in **f1** will be executed if present. Control will return to the caller which is a function **main**. Note that if there are more functions in between then the process will continue up the stack in a similar way

- After main returns the defer  function if present in main will be executed

Let’s see a program for that

```go
package main

import "fmt"

func main() {
	defer fmt.Println("Defer in main")
	fmt.Println("Stat main")
	f1()
	fmt.Println("Finish main")
}

func f1() {
	defer fmt.Println("Defer in f1")
	fmt.Println("Start f1")
	f2()
	fmt.Println("Finish f1")
}

func f2() {
	defer fmt.Println("Defer in f2")
	fmt.Println("Start f2")
	fmt.Println("Finish f2")
}
```

**Output**

```go
Stat main
Start f1
Start f2
Finish f2
Defer in f2
Finish f1
Defer in f1
Finish main
Defer in main
```

# **Evaluation of defer arguments**

defer arguments are evaluated at the time defer statement is evaluated

```go
package main

import "fmt"

func main() {
	sample := "abc"

	defer fmt.Printf("In defer sample is: %s\n", sample)
	sample = "xyz"
}
```

**Output**

```go
In defer sample is: abc
```

when the defer statement was evaluated the value of the **sample** variable was **“abc”**. In the defer function, we print the  sample variable. After the defer statement we change the value of the **sample** variable to **“xyz”**.  But the program outputs **“abc”** instead of **“xyz”** because when the defer arguments were evaluated the value of the  sample variable was **“abc”**.

# **Multiple defer functions in the same function**

 In case we have multiple defer functions within a particular function, then all the  defer functions will be executed in last in first out order

Let’s see a program for that

```go
package main
import "fmt"
func main() {
    i := 0
    i = 1
    defer fmt.Println(i)
    i = 2
    defer fmt.Println(i)
    i = 3
    defer fmt.Println(i)
}
```

**Output**

```go
3
2
1
```

# **Defer function and Named Return Values**

In case of named return value in the function, the defer function can read as well as modified those named return values. If the defer function modifies the name return value then that modified value will  be returned

```go
package main
import "fmt"
func main() {
    s := test()
    fmt.Println(s)
}
func test() (size int) {
    defer func() { size = 20 }()
    size = 30
    return
}
```

**Output**

```go
20
```

# **Defer and Methods**

**defer** statement is also applicable  for methods in a similar way it is applicable to functions. In the first example we had already seen the **Close** method which was called on the file instance. That shows that the  **defer** statement is also applicable for methods as well

# **Defer and Panic**

defer function will also be executed even if panic happens in a program.  When the panic is raised in a function then the execution of that function is stopped and any deferred function will be executed. In fact deferred function of all the function calls in the stack will also be executed until all the functions have returned .At that time the program will exit and it will print the panic message

So if a  defer function is present it then it will be executed and the control will be  returned back to the caller function which will again execute its defer function if present and the chain goes on until the program exists.

```go
package main
import "fmt"
func main() {
    defer fmt.Println("Defer in main")
    panic("Panic with Defer")
    fmt.Println("After painc in f2")
}
```

**Output**

```go
Defer in main
panic: Panic Create

goroutine 1 [running]:
main.main()
        /Users/slohia/go/src/github.com/golang-examples/articles/tutorial/panicRecover/deferWithPanic/main.go:7 +0x95
exit status 2
```



---

# POINTER

==_**Pointers in Golang are utilized to enhance performance and flexibility by avoiding unnecessary copies of data and enabling efficient data structures and function calls.**_==

In Go, the general form of a pointer declaration with `var` is as follows:

```go
var p *<type> [= expression]
```

Here, `*` indicates that it is a pointer, and `<type>` specifies the type of the address it holds.

_**p is a pointer to `<type>` object. In other words, p can hold an address of type `<type>`.**_ The `&` (address of) operator, used in the single operand and prefix position, allows obtaining the address of a variable. A pointer's default value (zero value) is nil.

When you have an address, the content (dereferencing) operator is used to access the object at that address. This operator is represented by the `*` atom. The operand of the operator must be an address.

Using this operator, changes to the object can be indirectly made.

```go
var a int = 10
var pi *int = &a

fmt.Printf("a = %d, *pi = %d\n", a, *pi)

*pi++

fmt.Printf("a = %d, *pi = %d\n", a, *pi)
```

Different types of pointers cannot be explicitly assigned to each other. However, pointers of the same type can be assigned. The `Printf` function's format character `%p` can be used to print the object's address to stdout.

```go
a := 10
b := 20
var pi = &a
var pi2 *int

pi2 = pi

fmt.Printf("a = %d, *pi = %d, *pi2 = %d, pi = %p, pi2 = %p\n", a, *pi, *pi2, pi, pi2)

*pi2--

fmt.Printf("a = %d, *pi = %d, *pi2 = %d, pi = %p, pi2 = %p\n", a, *pi, *pi2, pi, pi2)

pi = &b

fmt.Printf("a = %d, *pi = %d, *pi2 = %d, pi = %p, pi2 = %p\n", a, *pi, *pi2, pi, pi2)
```

Output:

```
a = 10, *pi = 10, *pi2 = 10, pi = 0xc000012028, pi2 = 0xc000012028
a = 9, *pi = 9, *pi2 = 9, pi = 0xc000012028, pi2 = 0xc000012028
a = 9, *pi = 20, *pi2 = 9, pi = 0xc000012040, pi2 = 0xc000012028
```

### WEB NOTES
---
### Initialization of a Pointer

#### Using the `new` Operator

```go
a := new(int)
*a = 10
fmt.Println(*a) // Output will be 10
```

#### Using the Ampersand `&` Operator

```go
a := 2
b := &a
fmt.Println(*b) // Output will be 2
```

### About `*` or Dereferencing Pointer

Dereferencing a pointer means getting the value at the address stored in the pointer. Changing the value at that pointer location reflects in the original variable.

```go
a := 2
b := &a // b = 2
fmt.Println(a)  // 2
fmt.Println(*b) // 2

*b = 3
fmt.Println(a)  // 3
fmt.Println(*b) // 3

a = 4
fmt.Println(a)  // 4
fmt.Println(*b) // 4
```

Both `a` and `*b` refer to the same variable internally. Changing the value of one reflects in the other.

### Pointer to a Pointer

```go
a := 2
b := &a
c := &b

fmt.Printf("a: %d\n", a)    // 2
fmt.Printf("b: %p\n", b)    // c000018078
fmt.Printf("c: %p\n", c)    // c00000e028

fmt.Println()
fmt.Printf("a: %d\n", a)    // 2 
fmt.Printf("*&a: %d\n", *&a) // 2
fmt.Printf("*b: %d\n", *b)   // 2
fmt.Printf("**c: %d\n", **c) // 2

fmt.Println()
fmt.Printf("&a: %d\n", &a)    // 824633819256
fmt.Printf("b: %d\n", b)      // 824633819256
fmt.Printf("&*b: %d\n", &*b)  // 824633819256
fmt.Printf("*&b: %d\n", *&b)  // 824633819256
fmt.Printf("*c: %d\n", *c)    // 824633819256

fmt.Println()
fmt.Printf("b: %d\n", &b)     // 824633778216
fmt.Printf("*c: %d\n", c)     // 824633778216
```

---

# STRUCT

### Yapılar (Structures) ve Methodlar (Methods) - Go

Go'da programcılar, built-in türler dışında kendi türlerini tanımlayabilir (user-defined types). Bu genellikle yapılar (structures) kullanılarak gerçekleştirilir. Yapılar, bilgilerin bir araya getirilmesiyle oluşan ve özellikle tek başına anlam ifade etmeyen, ancak bir araya geldiklerinde bir türü belirten nesneler için kullanılır. Aynı zamanda birer data structure'dir.

#### Yapı Tanımlama

```go
type Point struct {
    x, y int
}

type PointF struct {
    x, y float32
}
```

Yapı içerisindeki değişkenlere "yapı elemanı" (structure member/field/member variable) denir. Yapılar için birinci operandı, bir yapı nesnesi veya yapı türünden gösterici olabilir. İkinci operandı ise yapının elemanı veya yapıya eklenmiş bir fonksiyon olabilir.

#### Yapı Nesnesi Oluşturma

```go
var p Point
var pf PointF

p.x = 100
p.y = 2000
pf.x = 3.456
pf.y = -5678.89

// veya

p := Point{100, 200}
pf := PointF{3.45, 78.9}
```

Yapı nesneleri oluşturulduğunda elemanları default değerlerini alırlar.

#### Yapılar Arasında Atama (Memberwise Copy)

```go
a := Point{1, 2}
b := Point{3, 4}

a = b // Karşılıklı elemanlar kopyalanır
```

#### Yapıları Fonksiyonlara Geçirme

```go
func printPoint(p *Point) {
    fmt.Println(*p)
}

func main() {
    p := Point{100, 100}
    printPoint(&p)
}
```
#### Pointer ile Yapı Elemanlarına Erişim

```go
func setPoint(p *Point, x, y int) {
    (*p).x = x
    p.y = y // (*p).y = y
}

var p Point
setPoint(&p, 100, 100)
```

#### Yapılar Üzerinde Methodlar
```go
func (p *Point) Print() {
    fmt.Printf("x = %d, y = %d\n", p.x, p.y)
}

func (p *Point) Set(x, y int) {
    p.x = x
    p.y = y
}

func create(x, y int) *Point {
    return &Point{x, y}
}

func main() {
    p := create(100, 100)

    p.Print()
    p.Set(200, 300)
    p.Print()
}
```

Yapılara fonksiyonlar eklenerek "method" adını alır. Her ne kadar tam anlamını yansıtmasa da bu fonksiyonlara "extension functions" da denilebilmektedir. Bu methodlar, ilgili türden bir nesne ile çağrılabilir. Eğer tür bir pointer ise, bu durumda o türden bir pointer ile çağrılabilir.

### WEB NOTES
---

In Go, a struct is a named collection of data fields that can be of different types. It serves as a container for different heterogeneous data types, representing an entity.

#### Struct Definition

```go
type struct_name struct {
    field_name1 field_type1
    field_name2 field_type2
    // ...
}

type employee struct {
    name   string
    age    int
    salary int
}
```

#### Creating a Struct Variable
```go
// All fields initialized with default zero values
emp := employee{}

// Initializing values for each struct field
emp := employee{
    name:   "Sam",
    age:    31,
    salary: 2000,
}

// Initializing only some fields (others get zero values)
emp := employee{"Sam", 31, 2000}
```

#### Accessing and Setting Struct Fields
```go
emp.name = "some_new_name"
```

#### Pointer to a Struct

Two ways to create a pointer to a struct:

```go
emp := employee{name: "Sam", age: 31, salary: 2000}
empP := &emp

// OR

empP := &employee{name: "Sam", age: 31, salary: 2000}

// Using the new keyword
empP := new(employee)
```

#### Struct Field Tags (Metadata)

```go
type employee struct {
    Name   string `json:"n"`
    Age    int    `json:"a"`
    Salary int    `json:"s"`
}
```

#### Anonymous Fields in a Struct

A struct can have anonymous fields, meaning a field with no name:

```go
type employee struct {
    string  // anonymous
    age    int
    salary int
}

emp := employee{string: "Sam", age: 31, salary: 2000}
```


#### Nested Struct
```go
type employee struct {
    name    string
    age     int
    salary  int
    address address
}

type address struct {
    city    string
    country string
}
```

#### Anonymous Nested Struct Fields
```go
type employee struct {
    name   string
    age    int
    salary int
    address
}

type address struct {
    city    string
    country string
}

address := address{city: "London", country: "UK"}

emp := employee{name: "Sam", age: 31, salary: 2000, address: address}
```

#### Exported and Unexported Fields
```go
type Person struct {
    Name string   // Exported
    age  int      // Unexported
}

type company struct {
    // Unexported fields
}
```

#### Struct Equality

Two structs are equal if all their field types are comparable and all corresponding field values are equal:

```go
emp1 := employee{name: "Sam", age: 31, salary: 2000}
emp2 := employee{name: "Sam", age: 31, salary: 2000}

if emp1 == emp2 {
    fmt.Println("emp1 and emp2 are equal")
} else {
    fmt.Println("emp1 and emp2 are not equal")
}
```

#### Structs are Value Types

A struct is a value type in Go. A new copy of the struct is created when:

- A struct variable is assigned to another struct variable.
- A struct variable is passed as an argument to a function.

---

# METHOD

In Go, a method is nothing but a function with a receiver. A receiver is an instance of a specific type, such as a struct or any other custom type. Methods allow you to write object-oriented code in Go and offer benefits such as the ability to have two different methods with the same name in the same package.

#### Format of a Method

```go
func (receiver receiver_type) some_func_name(arguments) return_values
```

- A method is defined with a receiver argument.
- Methods differ from functions in terms of functionality.
- Methods can be used for chaining on the receiver, and different methods can have the same name with a different receiver.

#### Methods on Structs

Methods can be defined on any custom type, including structs. When a method is defined on a value receiver, a copy of the receiver is made, and changes made inside the method are not visible to the caller.

```go
type employee struct {
    name   string
    age    int
    salary int
}

func (e employee) details() {
    fmt.Printf("Name: %s\n", e.name)
    fmt.Printf("Age: %d\n", e.age)
}

func (e employee) getSalary() int {
    return e.salary
}

func (e employee) setNewName(newName string) {
    e.name = newName
}

func main() {
    emp := employee{name: "Sam", age: 31, salary: 2000}
    emp.details()
    emp.setNewName("John")
    fmt.Printf("Salary %d\n", emp.getSalary())
}
```

#### Method on a Pointer Receiver

Methods can also be defined on a pointer receiver. Changes made to the pointer receiver are visible to the caller.

```go
func (e *employee) setNewName(newName string) {
    e.name = newName
}

func main() {
    emp := &employee{name: "Sam", age: 31, salary: 2000}
    emp.setNewName("John")
    fmt.Printf("Name: %s\n", emp.name)
}
```

#### Calling Methods with Value or Pointer Receivers

The language allows calling a method with a pointer receiver on a non-pointer instance, and vice versa.

```go
emp.setNewName("John")
(&emp).setNewName("Mike")
```

#### When to Use Pointer Receivers

- When changes to the receiver made inside the method need to be visible to the caller.
- When the struct is large to avoid making a copy of the struct every time a method is called.

#### Other Points about Methods

- The receiver type must be defined in the same package as the method definition.
- Methods can be called in different ways, providing flexibility in using value or pointer receivers.
- Methods can be defined on anonymous nested struct fields.
- Method chaining is possible by having methods return the receiver.

#### Methods on Non-Struct Types

Methods can be defined on non-struct custom types.

```go
type myFloat float64

func (m myFloat) ceil() float64 {
    return math.Ceil(float64(m))
}

func main() {
    num := myFloat(1.4)
    fmt.Println(num.ceil())
}
```

# STRING

In Go, the `string` type is used for handling textual data. Strings in Go represent characters in UTF-8 encoding, allowing variable-length characters. Strings in Go are immutable, meaning functions that modify strings create a new string.

#### String Literals

String literals (SL) are text between two double-quote characters, and they represent a string of the `string` type.

```go
func main() {
    s1 := "ankara"
    var s2 string = "istanbul"

    fmt.Println(s1)
    fmt.Println(s2)
    fmt.Printf("City:%s\n", s1)
}
```

Escape sequences in SL have their usual meaning. For raw string literals without escape sequences, backticks (`) are used.

```go
func main() {
    path1 := "C:\\test\\names.txt"
    path2 := `C:\test\names.txt`

    fmt.Println(path1)
    fmt.Println(path2)
}
```

#### String Length

The `len` function is used to get the length of a string in bytes.

```go
func main() {
    var str string
    fmt.Print("Input a text:")
    fmt.Scan(&str)

    fmt.Printf("Length:%d\n", len(str))
}
```

#### String Concatenation and Comparison

Strings can be concatenated using the `+` operator. Strings can be compared for equality using `==` or `!=` and lexicographically using `<`, `>`, `<=`, `>=` operators.

```go
str1 := "Hello"
str2 := "World"
result := str1 + " " + str2
```

#### Using `strings.Builder`

The `strings` package includes a `Builder` type for more efficient string manipulations.

```go
var builder strings.Builder
builder.WriteString("Hello")
builder.WriteString(" World")
result := builder.String()
```

#### Case Conversion with `strings.ToUpperSpecial` and `strings.ToLowerSpecial`

These methods allow case conversion based on a specified locale.

```go
func main() {
    for {
        var str string

        fmt.Print("Input text:")
        fmt.Scan(&str)

        if str == "quit" {
            break
        }

        fmt.Println(strings.ToUpperSpecial(unicode.TurkishCase, str))
        fmt.Println(strings.ToLowerSpecial(unicode.TurkishCase, str))
    }
}
```

# STRCONV

The `strconv` package in Go provides functions for string conversions, particularly for numeric types.

#### Numeric to String Conversions:

1. **`Itoa(i int) string`**:
    - Converts an integer to its decimal string representation.
```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	i := 42
	str := strconv.Itoa(i)
	fmt.Printf("Integer to String: %s\n", str)
}

	
```

**`FormatInt(i int64, base int) string`**:

- Converts an integer to its string representation in the specified base (e.g., binary, octal, decimal, hexadecimal).

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	i := int64(42)
	str := strconv.FormatInt(i, 16) // Convert to hexadecimal
	fmt.Printf("Integer to Hexadecimal String: %s\n", str)
}
```

#### String to Numeric Conversions:

1. **`Atoi(s string) (int, error)`**:
    - Parses a string `s` and converts it to an integer. Returns an error if the string is not a valid integer.

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	str := "42"
	i, err := strconv.Atoi(str)
	if err == nil {
		fmt.Printf("String to Integer: %d\n", i)
	} else {
		fmt.Println("Error:", err)
	}
}
```

**`ParseInt(s string, base int, bitSize int) (int64, error)`**:

- Parses a string `s` representing an integer in the specified base and bit size and returns the integer value. It can handle binary, octal, decimal, and hexadecimal representations.

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	str := "2a" // Hexadecimal representation
	i, err := strconv.ParseInt(str, 16, 64)
	if err == nil {
		fmt.Printf("Hexadecimal String to Integer: %d\n", i)
	} else {
		fmt.Println("Error:", err)
	}
}
```

#### Parsing and Formatting Floating-Point Numbers:

1. **`Atof(s string) (float64, error)`**:
    - Parses a string `s` and converts it to a `float64`. Returns an error if the string is not a valid floating-point number.

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	str := "3.14"
	f, err := strconv.Atof(str)
	if err == nil {
		fmt.Printf("String to Float: %f\n", f)
	} else {
		fmt.Println("Error:", err)
	}
}
```

**`ParseFloat(s string, bitSize int) (float64, error)`**:

- Parses a string `s` representing a floating-point number with the specified bit size and returns the `float64` value.

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	str := "3.14"
	f, err := strconv.ParseFloat(str, 64)
	if err == nil {
		fmt.Printf("String to Float: %f\n", f)
	} else {
		fmt.Println("Error:", err)
	}
}
```

#### Boolean Conversion:

- **`ParseBool(str string) (bool, error)`**:
    - Parses a string that represents a boolean ("true" or "false") and returns the corresponding boolean value.

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	str := "true"
	b, err := strconv.ParseBool(str)
	if err == nil {
		fmt.Printf("String to Boolean: %t\n", b)
	} else {
		fmt.Println("Error:", err)
	}
}
```

#### Quoting and Unquoting:

1. **`Quote(s string) string`**:
    - Returns a double-quoted Go string literal representing the string `s`. Useful for escaping special characters in strings.

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	str := "Hello, Go!"
	quoted := strconv.Quote(str)
	fmt.Printf("Quoted String: %s\n", quoted)
}
```

2. **`Unquote(s string) (string, error)`**:
    - Unquotes a double-quoted string, removing the surrounding quotes and unescaping any special characters.

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	quoted := `"Hello, Go!"`
	unquoted, err := strconv.Unquote(quoted)
	if err == nil {
		fmt.Printf("Unquoted String: %s\n", unquoted)
	} else {
		fmt.Println("Error:", err)
	}
}
```

# UNICODE

The `unicode` package in Go provides functionalities for working with Unicode characters. It includes operations for testing character properties, converting characters to different cases, character classification, character representation, and working with character ranges and tables.

#### Character Properties:

- `unicode.IsDigit`, `unicode.IsLetter`, `unicode.IsUpper`, `unicode.IsLower`, and similar functions:
    - Used to test character properties such as digit, letter, uppercase, lowercase, and more.

#### Case Conversion:

- `unicode.ToUpper` and `unicode.ToLower` functions:
    - Utilized for changing the case of characters.

#### Character Classification:

- `unicode.Is` function:
    - Allows testing if a character belongs to a specific class, such as a letter, number, space, or symbol.

#### Character Representation:

- `unicode.ReplacementChar` constant:
    - Represents the Unicode replacement character (U+FFFD), used to replace invalid or ill-formed UTF-8 sequences.

#### Ranges and Tables:

- The package includes functions for working with ranges of characters and tables that map characters to specific properties.

Below is an example demonstrating the use of some functions from the `unicode` package:

```go
package main

import (
	"fmt"
	"unicode"
)

func main() {
	// Testing character properties
	char := 'A'
	fmt.Printf("Is '%c' a digit? %t\n", char, unicode.IsDigit(char))
	fmt.Printf("Is '%c' a letter? %t\n", char, unicode.IsLetter(char))

	// Case conversion
	upperChar := unicode.ToUpper(char)
	fmt.Printf("Uppercase of '%c': %c\n", char, upperChar)

	// Character classification
	fmt.Printf("Is '%c' a space? %t\n", char, unicode.IsSpace(char))

	// Character representation
	invalidChar := unicode.ReplacementChar
	fmt.Printf("Replacement character: %c\n", invalidChar)
}
```

---

# PACKAGES AND MODULES 

Go dilinde farklı dosyalardan farklı isimlerin kullanılabilmesi için genellikle paketlere isim verilir. Bu isimler, fonksiyon isimleri, tür isimleri, yapı elemanı isimleri gibi çeşitli isimler olabilir.

#### Paket İsimlendirme ve İçe Aktarma

- Farklı Go dosyalarındaki isimlerin kullanılabilmesi için genellikle paketler kullanılır.
- Paket isimleri, bir paketi kullanabilmek için import edilir.
- İstendiğinde paket ismine bir alias (takma ad) verilebilir.
- Eğer bir paket veya alias kullanılmıyorsa, Go derleyicisi hata verebilir.
- Paketler ve dosyalar arasında bir hiyerarşi vardır. Örneğin, `<üst paket>/<alt paket>` şeklinde bir bildirim kullanılabilir.

```go
import (
	"fmt"
	myutil "example.com/util" // Örnek olarak bir paketin import edilmesi
	_ "unused-package"        // Bir paketi import etmek ama ismini kullanmamak
)
```

#### Paket İçerisindeki İsimler

- Paket içindeki isimlere, eğer büyük harfle başlıyorsa, diğer paketlerden erişilebilir.
- Küçük harfle başlayan isimler, paket dışında gizlenir ve doğrudan erişilemez.
- Init fonksiyonları, bir paket import edildiğinde çağrılır. Bir paket için init fonksiyonu yazmak zorunlu değildir.

#### Paketlerin Yüklenme Sıralaması

Bir program çalıştırıldığında, paketlerin yüklenmesi şu sırayla gerçekleşir:

1. Main paket
2. İmport edilen paketler
3. Bağımlı (dependent) paketler
4. Paketler içindeki global nesnelere ilk değerler verilir
5. İmport edilen paketlerin init fonksiyonları çağrılır
6. Main paketi içindeki global nesnelere ilk değerler verilir
7. Main paketi içindeki init fonksiyonları çağrılır
8. Main fonksiyonu çağrılır

Bu sıralama, bir programın başlangıcında paketlerin yüklenme ve başlatılma sürecini belirtir.

### WEB NOTES
---

#### Packages in Go

- Every Go source file (.go file) in a Go application belongs to a package.
- All .go files in the same directory are part of the same package.
- A package's name is determined by the "Package Declaration" and not the directory's name.
- There are two types of packages:
    - Executable Package: Contains the `main` function and denotes the start of a program.
    - Utility Package: Any package other than the `main` package; it contains utility functions for use by executable packages.

#### Modules in Go

- A module is a collection of related packages with a `go.mod` file at its root.
- The `go.mod` file defines the module import path and dependency requirements.
- Modules provide:
    - Dependency management
    - Versioning using semantic versioning (semver)
    - Automatic fetching and inclusion of dependencies
    - Module awareness with metadata defined in `go.mod`
    - Compatibility specifications for the minimum required Go version
    - A "vendor" directory for local copies of dependencies
    - Improved support for replacing dependencies with different versions or alternatives

#### Before Modules

- In the pre-modules era, Go projects used the `GOPATH` environment variable.
- Developers manually organized projects within the GOPATH, and dependency management was done manually.
- Versioning was challenging, and some projects used a "vendor" directory for dependencies.
- Limited dependency metadata and challenges in fetching and updating dependencies were faced.

#### Creating a Module

- To create a module, use the command: `go mod init {module_import_path}`
- Example: `go mod init sample.com/learn`
- The `go.mod` file defines the module's import path and required Go version.
- Executable binaries are created using commands like `go install`, `go build`, or `go install .`

#### Nested Packages

- Go allows organizing code into nested packages.
- Nested packages are useful for modularity and structured code organization.
- The import path of a nested package includes both the parent and child package names.

#### Aliasing in Importing Packages

- Aliasing in import statements allows giving a different name to the imported package.
- Syntax: `import aliasName "actualPackageName"`
- Aliasing is useful for providing more relevant names or avoiding conflicts when two import paths contain the same package name.

#### Init Functions

- `init()` functions initialize global variables of a package and are executed when the package is initialized.
- Init functions are called implicitly, and a package can have multiple `init()` functions.
- Blank identifier `_` in import statements is used when a package is imported solely for its side effects, such as calling `init()` functions.

#### Types of Modules

- Modules can be executable or non-executable (utility).
- Executable modules contain the `main` package and denote the start of a program.
- Non-executable modules contain utility packages and are not self-executable.

#### Package vs. Module

- A module is a directory containing nested packages with a `go.mod` file.
- Modules provide dependency management and versioning.
- The behavior of packages within a module is similar to the pre-modules era.

#### Add a Dependency to a Project

- Dependencies can be added directly to the `go.mod` file or by using `go get`.
- After adding a dependency, run `go mod tidy` to synchronize the go.mod file with the actual dependencies used.

#### Adding a Vendor Directory

- Use `go mod vendor` to create a vendor directory with local copies of dependencies.
- This aids in reproducible builds, as dependencies do not need to be downloaded at runtime.

#### Module Import Path

- The module import path can be set based on whether the module is utility, not published, or executable.
- Executable module import paths can be any valid path, even if planning to commit to version control.

#### Importing Packages within the Same Module

- Packages within the same module can be imported using the module's import path and the directory containing the package.
- Example: `import "sample.com/learn/math"`

#### Importing Packages from Different Modules Locally

- Use the `replace` directive in the `go.mod` file to substitute an external module with a local directory during development.

#### Go Mod Command

- Various `go mod` commands are available for managing modules, such as `download`, `edit`, `tidy`, `vendor`, and others.

#### Direct vs. Indirect Dependencies in go.mod File

- The `go.mod` file records direct dependencies, and indirect dependencies may be recorded based on certain conditions.

This summarizes the key concepts of Go packages and modules, including their creation, organization, dependency management, and various related commands.

---

# ARRAY

### Diziler (Arrays) ve Kullanımı

Diziler, aynı türden elemanları içeren ve elemanlarını belirli bir sırayla saklayan veri yapılarıdır. Go'da dizilerin uzunluğu değiştirilemez ve sabit bir ifade olmalıdır. Dizi elemanları yaratıldığında varsayılan değerlerini alırlar.

```go
var a [n]int
```

Burada, `n` bir sabit ifadesi olmalıdır. Diziler, `range` ifadesi ile dolaşılabilir. Bu sayede index numarası ve o index numarasındaki dizi elemanı elde edilebilir.

```go
func main() {
    var a [10]int

    for i, val := range a {
        fmt.Printf("%d -> %d\n", i, val)
    }
}
```

Dizilerin isimleri Go'da bir adres değildir. Dizilerin uzunluğu `len` built-in fonksiyonu ile elde edilebilir.

```go
func main() {
    a := [5]int{1, 2, 3, 4, 5}
    s := [7]string{"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}

    for _, val := range a {
        fmt.Printf("%02d ", val)
    }

    fmt.Println()

    for _, dow := range s {
        fmt.Printf("%s\n", dow)
    }
}
```

Diziye ilk değer verilirken, dizi içerisi boş bırakılabilir veya `...` (ellipsis) atomu kullanılabilir. `[]` içerisinin boş bırakılması aslında bir dilim (slice) yaratmak anlamına gelir.

```go
func main() {
    a := [...]int{1, 2, 3, 4, 5}
    s := []string{"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}

    for _, val := range a {
        fmt.Printf("%02d ", val)
    }

    fmt.Println()

    for _, dow := range s {
        fmt.Printf("%s\n", dow)
    }
}
```

Boş bırakma ve ellipses kullanımı genellikle dizinin boyutunu esnek tutmak ya da mevcut elemanlarla otomatik belirlenmesini sağlamak için kullanılır.

Dizi fonksiyona geçirilirken doğrudan geçirildiğinde kopyalama işlemi yapılır. Bu durum, çok büyük diziler için maliyetli olabilir. Bu durumda, fonksiyona doğrudan geçirmek yerine bir pointer ile geçirmek veya dizi yerine dilim (slice) kullanmak daha doğru bir yaklaşım olabilir.

```go
func printDayOfWeeks(s [7]string) {
    for _, dow := range s {
        fmt.Printf("%s ", dow)
    }

    fmt.Println()
}

func main() {
    s := [7]string{"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}

    printDayOfWeeks(s)
}
```

Fonksiyon tanımında dizi parametresi belirtilirken tipi ve boyutu ifade edilmelidir. Eğer bir fonksiyon bir diziyi değiştirecekse, ya dizinin referansını ya da dilimi geçmelidir.

### WEB NOTES
---

### Diziler (Arrays) ve Kullanımı

Diziler, Go dilinde aynı türden elemanları içeren ve elemanlarını belirli bir sırayla saklayan veri yapılarıdır. Dizinin boyutu, tipin bir parçasıdır; bu nedenle farklı sayıda elemana sahip iki dizi, iki farklı türdür ve birbirine atama yapılamaz.

Dizi tanımlama örneği:

```go
sample := [size_of_array]{type}{a1, a2... an}
```

Go'da diziler değer tipindedir, yani bir dizi değişken adı bir işaretçi değildir; aslında, tüm diziyi temsil eder. Bir dizi değişkeni başka bir dizi değişkenine atanırsa veya bir işlevin argümanı olarak geçirilirse, dizi bir kopyası oluşturulur.

```go
sample1 := [2]string{"a", "b"}
fmt.Printf("Sample1 Before: %v\n", sample1)
sample2 := sample1
sample2[0] = "c"
fmt.Printf("Sample1 After assignment: %v\n", sample1)
fmt.Printf("Sample2: %v\n", sample2)
test(sample1)
fmt.Printf("Sample1 After Test Function Call: %v\n", sample1)
```

Dizilere erişim:
```go
sample := [2]string{"aa", "bb"}
fmt.Println(sample[0])
fmt.Println(sample[1])
sample[0] = "xx"
fmt.Println(sample)
// sample[3] = "yy" -> Hata: Dizi indeksi sınırların dışında
```

Farklı dizileri işlemek için iki yaygın yol şunlardır:

1. **For Döngüsü Kullanarak:**

```go
letters := [3]string{"a", "b", "c"}
fmt.Println("Using for loop")
len := len(letters)
for i := 0; i < len; i++ {
    fmt.Println(letters[i])
}
```

**For-Range Döngüsü Kullanarak:**

```go
fmt.Println("\nUsing for-range loop")
for i, letter := range letters {
    fmt.Printf("%d %s\n", i, letter)
}
```

Çok boyutlu diziler:

```go
sample := [x][y]{type}{{a11, a12 .. a1y},
                   {a21, a22 .. a2y},
                   {.. },
                   {ax1, ax2 .. axy}}
```

Burada:

- `x` satır sayısını temsil eder.
- `y` sütun sayısını temsil eder.
- `aij` i. satır ve j. sütundaki elemanı temsil eder.

```go
matrix := [2][3]int{{1, 2, 3}, {4, 5, 6}}
```
---

# SLICE

**Arrays vs. Slices:**

- **Arrays:** Fixed size, value types, stack-allocated memory.
- **Slices:** Dynamic and flexible, reference types, underlying array on the heap.

**Internal Representation of a Slice:**

```go
type SliceHeader struct {
    Pointer uintptr // Pointer to the underlying array
    Len     int     // Current length of the underlying array
    Cap     int     // Total capacity, the maximum capacity to which the underlying array can expand
}
```

- The slice header contains a pointer to the underlying array, the current length, and the total capacity.

**Advantages of Capacity:**

- Capacity allows pre-allocation during initialization, providing a performance boost when additional elements are needed.

**Creating a Slice:**

1. **Using `[]<type>{}` Format:**
	```go
s := []int
s := []int{1, 2}

	```

**Creating a Slice from Another Slice or Array:**

```go
numbers := [5]int{1, 2, 3, 4, 5}
num1 := numbers[2:4] // End index not included
```

**Using `make`:**

```go
numbers := make([]int, 3, 5) // Capacity is optional

```

**Using `new`:**

```go
numbers := new([]int)
```

- `make` is more flexible and commonly used.

**Accessing and Modifying Slice Elements:**

- Access elements using an index.
- Modify elements by assigning new values using the index.

**Iterating Through a Slice:**

- Iterate through a slice using loops, similar to arrays.

**Appending to a Slice:**

- Use the `append` function to add elements to the end of a slice:

```go
numbers := []int{1, 2}
numbers = append(numbers, 3, 4, 5) // Result: [1, 2, 3, 4, 5]
```

- `append` dynamically increases the length and capacity of the slice.
    

**Copying a Slice:**

- Use the `copy` function to copy elements from one slice to another:

```go
src := []int{1, 2, 3, 4, 5}
dst := make([]int, 5)
numberOfElementsCopied := copy(dst, src)
```

- The number of elements copied is the minimum of the lengths of `src` and `dst`.
    
**Multidimensional Slices:**

- Initialize a 2D slice using `make`:

```go
twoDSlice = make([][]int, 2)

```

Initialize inner slices individually:

```go
for i := range twoDSlice {
    twoDSlice[i] = make([]int, 3)
```

Different lengths for inner slices are possible. Unlike arrays, slices allow flexibility in inner slice lengths.

# INTERFACE


### WEB NOTES
---

## Interface in Go

- An interface in Go is a collection of method signatures representing certain behavior.
- It declares the method set, and any type implementing all methods of the interface is of that interface type.

### Example Interface Definition:

```go
type animal interface {
    breathe()
    walk()
}

```

### Implementing an Interface:

```go
type lion struct {
    age int
}

func (l lion) breathe() {
    fmt.Println("Lion breathes")
}

func (l lion) walk() {
    fmt.Println("Lion walks")
}
```

### Interface Types as Arguments to a Function:

```go
func callBreathe(a animal) {
    a.breathe()
}

func callWalk(a animal) {
    a.walk()
}
```


``
```go
func callBreathe(a animal) {
    a.breathe()
}

func callWalk(a animal) {
    a.walk()
}
```

### Why Use Interfaces:

- Helps write modular and decoupled code, reducing dependencies.
- Enables runtime polymorphism.

### Pointer Receiver While Implementing an Interface:

- A type can implement an interface with either value or pointer receivers.

```go
func (l *lion) breathe() {
    fmt.Println("Lion breathes")
}
```

### Non-Struct Custom Type Implementing an Interface:

```go
type cat string

func (c cat) breathe() {
    fmt.Println("Cat breathes")
}

func (c cat) walk() {
    fmt.Println("Cat walks")
}
```

### Type Implementing Multiple Interfaces:

```go
type mammal interface {
    feed()
}

type lion struct {
    age int
}

func (l lion) feed() {
    fmt.Println("Lion feeds young")
}
```

### Zero Value of Interface:

- Default or zero value of an interface is `nil`.

### Inner Working of Interface:

```go
var a animal
a = lion{age: 10}
fmt.Printf("Underlying Type: %T\n", a)
fmt.Printf("Underlying Value: %v\n", a)
```
### Embedding Interfaces:

```go
type human interface {
    animal
    speak()
}
```

### Embedding Interface in a Struct:

```go
type pet1 struct {
    a    animal
    name string
}

type pet2 struct {
    animal
    name string
}
```

### Access Underlying Variable of Interface:

#### Type Assertion:

```go
l, ok := a.(lion)
if ok {
    fmt.Println(l)
} else {
    fmt.Println("a is not of type lion")
}
```

#### Type Switch:

```go
switch v := a.(type) {
case lion:
    fmt.Println("Type: lion")
case dog:
    fmt.Println("Type: dog")
default:
    fmt.Printf("Unknown Type %T", v)
}
```

 ### Empty Interface:

- An empty interface has no methods, making it implementable by any type.
```go
func test(a interface{}) {
    fmt.Printf("(%v, %T)\n", a, a)
}
```

---

# ERROR 

Error işlemleri genel olarak fonksiyonların geri dönüş değeri ile yapılır. 
Burada anlatılan error çalışma zamanında oluşan hatalara (runtime error) ilişkindir.
Error işlemleri için error isimli standart bir arayüz bulunmaktadır.
Go da hata durumları için panic terimi de kullanılabilmektedir.
	
Bir fonksiyon geri dönüş değeri olarak error türüne  de geri döner.
Bu durumda fonksiyonu çağıran programcı error değeri için nil kontrolü yaparak hatalı durumu elde eder.
error arayüzünün Error isimli fonksiyonu hata mesajına ilişkin yazıya (string) geri döner.

Bir error nesnesi yaratılabilmesi için errors paketinde New fonksiyonu çağrılabilir.
Bu fonksiyon parametresi hata mesajına ilişkin yazıdır (string).
Ayrıca fmt paketi içerisinde Printf gibi formatlama işlemi de yapabilen Errorf isimli  bir fonksiyon da vardır.
Bu fonksiyon yazıyı formatladıktan sonra yazıya ilişkin error nesnesinin adresine geri döner.

Error işlemlerinde panic built-in fonksiyonu da kullanılabilir.
Bu fonksiyon ile oluşturulan bir error handle edilmezse ilgili akış (thred/goroutine) abnormal bir biçimde sonlanır.
Bu durumda o akış için kritik bazı problemler olabilmektedir.


```go

package main

import (
	"SampleGoLand/csd/cmath"
	"fmt"
	"os"
)

func main() {
	var a float64

	fmt.Print("Input a value:")
	_, err := fmt.Scan(&a)

	if err != nil {
		fmt.Printf("Read value error: %s\n", err.Error())
		os.Exit(1)
	}

	result, err := cmath.CLog(a)

	if err != nil {
		fmt.Printf("Error message: %s\n", err.Error())
	} else {
		fmt.Printf("Log(%f) = %f\n", a, result)
	}
}

```

```go
package cmath

import (
	"errors"
	"fmt"
	"math"
)

func CLog(a float64) (float64, error) {
	if a < 0 {
		return 0, errors.New("indeterminate")
	}

	if a == 0 {
		return 0, errors.New("undefined")
	}

	return math.Log(a), nil
}

func CSqrt(a float64) (float64, error) {
	if a < 0 {
		return 0, fmt.Errorf("undefined -> value: %f", a)
	}

	return math.Sqrt(a), nil
}
```

### WEB NOTES

---

In Go, error handling can be done in two primary ways:

### 1. Using Type which Implements the Error Interface

Go handles errors by explicitly returning the error as a separate value. The error interface, defined in the `builtin` package, is crucial for this purpose.

```go
type error interface {
    Error() string
}
```

Any type that implements the `Error` method is considered to implement the error interface. Checking for nil allows programmers to determine whether a function call resulted in an error.

Example:

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("non-existing.txt")
    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Println(file.Name() + " opened successfully")
    }
}
```

Custom error types can also be created:

```go
type PathError struct {
    Op   string
    Path string
    Err  error
}

func (e *PathError) Error() string {
    return e.Op + " " + e.Path + ": " + e.Err.Error()
}
```

### 2. Using Panic and Recover

Panic and recover are mechanisms for handling exceptional conditions. However, using panic is discouraged in normal error-handling scenarios.

### Advantages of Using Error as a Type

- Provides more control over error handling.
- Avoids the need for try-catch blocks, promoting cleaner code.

### Different Ways of Creating an Error

1. Using `errors.New("some_error_message")`

```go
package main

import (
    "errors"
    "fmt"
)

func main() {
    sampleErr := errors.New("error occurred")
    fmt.Println(sampleErr)
}
```

Using `fmt.Errorf("error is %s", "some_error_message")`

```go
package main

import "fmt"

func main() {
    sampleErr := fmt.Errorf("Err is: %s", "database connection issue")
    fmt.Println(sampleErr)
}
```

Creating Custom Error

```go
package main

import "fmt"

type inputError struct {
    message      string
    missingField string
}

func (i *inputError) Error() string {
    return i.message
}

func (i *inputError) getMissingField() string {
    return i.missingField
}

func main() {
    err := validate("", "")
    if err != nil {
        if err, ok := err.(*inputError); ok {
            fmt.Println(err)
            fmt.Printf("Missing Field is %s\n", err.getMissingField())
        }
    }
}

func validate(name, gender string) error {
    if name == "" {
        return &inputError{message: "Name is mandatory", missingField: "name"}
    }
    if gender == "" {
        return &inputError{message: "Gender is mandatory", missingField: "gender"}
    }
    return nil
}
```

### Ignoring Errors

The underscore (`_`) operator can be used to ignore errors returned from a function call.
```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, _ := os.Open("non-existing.txt")
    fmt.Println(file)
}
```

### Wrapping of Error

```go
e := fmt.Errorf("... %w ...", ..., err, ...)
```

The `%w` directive is used for wrapping errors.

Example:

```go
package main

import (
    "fmt"
)

type notPositive struct {
    num int
}

func (e notPositive) Error() string {
    return fmt.Sprintf("checkPositive: Given number %d is not a positive number", e.num)
}

type notEven struct {
    num int
}

func (e notEven) Error() string {
    return fmt.Sprintf("checkEven: Given number %d is not an even number", e.num)
}

func checkPositive(num int) error {
    if num < 0 {
        return notPositive{num: num}
    }
    return nil
}

func checkEven(num int) error {
    if num%2 == 1 {
        return notEven{num: num}
    }
    return nil
}

func checkPostiveAndEven(num int) error {
    if num > 100 {
        return fmt.Errorf("checkPostiveAndEven: Number %d is greater than 100", num)
    }

    err := checkPositive(num)
    if err != nil {
        return fmt.Errorf("checkPostiveAndEven: %w", err)
    }

    err = checkEven(num)
    if err != nil {
        return fmt.Errorf("checkPostiveAndEven: %w", err)
    }

    return nil
}

func main() {
    num := 3
    err := checkPostiveAndEven(num)
    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Println("Given number is positive and even")
    }
}
```

Output:

```go
checkPostiveAndEven: checkEven: Given number 3 is not an even number
```

### Unwrap an Error

The `Unwrap` function of the `errors` package can be used to unwrap an error.

```go
func Unwrap(err error) error
```

If the error wraps another error, the wrapped error will be returned; otherwise, `Unwrap` returns `nil`.

```go
package main

import (
    "errors"
    "fmt"
)

type errorOne struct{}

func (e errorOne) Error() string {
    return "Error One happened"
}

func main() {
    e1 := errorOne{}
    e2 := fmt.Errorf("E2: %w", e1)
    e3 := fmt.Errorf("E3: %w", e2)

    fmt.Println(errors.Unwrap(e3))
    fmt.Println(errors.Unwrap(e2))
    fmt.Println(errors.Unwrap(e1))
}
```

Output:

```go
E2: Error One happened
Error One happened
```

### Check If Two Errors Are Equal

Two errors are equal in Go if they refer to the same underlying type and have the same underlying value (or both are `nil`).

Example:

```go
package main
import (
    "errors"
    "fmt"
)

type errorOne struct{}

func (e errorOne) Error() string {
    return "Error One happened"
}

func main() {
    var err1 errorOne
    err2 := do()

    if err1 == err2 {
        fmt.Println("Equality Operator: Both errors are equal")
    }

    if errors.Is(err1, err2) {
        fmt.Println("Is function: Both errors are equal")
    }
}

func do() error {
    return errorOne{}
}
```

Output:

```go
Equality Operator: Both errors are equal
Is function: Both errors are equal
```

### Get the Underlying Error from an Error Represented by the Error Interface

There are two ways of getting the underlying type:

1. Using the `.(type)` assert:

```go
err := err.(type)
err, ok := err.(type)
```

Using the `As` function of the `errors` package:

```go
func As(err error, target interface{}) bool
```

```go
package main

import (
    "errors"
    "fmt"
    "os"
)

func main() {
    err := openFile("non-existing.txt")

    if e, ok := err.(*os.PathError); ok {
        fmt.Printf("Using Assert: Error e is of type path error. Path: %v\n", e.Path)
    } else {
        fmt.Println("Using Assert: Error not of type path error")
    }

    var pathError *os.PathError
    if errors.As(err, &pathError) {
        fmt.Printf("Using As function: Error e is of type path error. Path: %v\n", pathError.Path)
    }
}

func openFile(fileName string) error {
    _, err := os.Open("non-existing.txt")
    if err != nil {
        return err
    }
    return nil
}
```

Output:

```go
Using Assert: Error e is of type path error. Path: non-existing.txt
Using As function: Error e is of type path error. Path: non-existing.txt
```

---

# PANIC & RECOVER

Panic in GoLang is similar to exceptions in other languages. It is meant to handle abnormal conditions that would lead to program termination. Panic can occur in two ways:

### 1. Runtime Error Panic

A panic can occur due to a runtime error in the program, such as an out-of-bounds array access.

```go
package main

import "fmt"

func main() {
    a := []string{"a", "b"}
    print(a, 2)
}

func print(a []string, index int) {
    fmt.Println(a[index])
}
```

Output:

```go
panic: runtime error: index out of range [2] with length 2
goroutine 1 [running]:
main.checkAndPrint(...)
        main.go:12
main.main()
        /main.go:8 +0x1b
exit status 2
```

### 2. Calling the Panic Function Explicitly

The panic function can be called explicitly by the programmer in situations where the program cannot continue.

```go
package main

import "fmt"

func main() {
    a := []string{"a", "b"}
    checkAndPrint(a, 2)
}

func checkAndPrint(a []string, index int) {
    if index > (len(a) - 1) {
        panic("Out of bound access for slice")
    }
    fmt.Println(a[index])
}
```

Output:

```go
panic: Out of bound access for slice

goroutine 1 [running]:
main.checkAndPrint(0xc000104f58, 0x2, 0x2, 0x2)
        main.go:13 +0xe2
main.main()
        main.go:8 +0x7d
exit status 2
```

### Panic with Defer

When a panic is raised in a function, the execution of that function is stopped, and any deferred function will be executed. Deferred functions of all the function calls in the stack will also be executed until all the functions have returned. At that point, the program will exit, printing the panic message.

```go
package main

import "fmt"

func main() {
    defer fmt.Println("Defer in main")
    panic("Panic with Defer")
    fmt.Println("After panic in main")
}
```

Output:

```go
Defer in main
panic: Panic with Defer

goroutine 1 [running]:
main.main()
        /main.go:7 +0x95
exit status 2
```

### Recover in GoLang

The `recover` function is used to handle panics. It is deferred and should be placed in a deferred function to catch and handle panics.

```go
package main

import "fmt"

func main() {
    a := []string{"a", "b"}
    checkAndPrint(a, 2)
    fmt.Println("Exiting normally")
}

func checkAndPrint(a []string, index int) {
    defer handleOutOfBounds()
    if index > (len(a) - 1) {
        panic("Out of bound access for slice")
    }
    fmt.Println(a[index])
}

func handleOutOfBounds() {
    if r := recover(); r != nil {
        fmt.Println("Recovering from panic:", r)
    }
}
```

Output:

```go
Recovering from panic: Out of bound access for slice
Exiting normally
```

The `recover` function catches the panic, prints the panic message, and allows the program to continue.

### Panic/Recover and Goroutine

`Recover` can only recover panics happening in the same goroutine. If the panic occurs in a different goroutine, `recover` in a different goroutine won't stop the panic.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    a := []string{"a", "b"}
    checkAndPrintWithRecover(a, 2)
    time.Sleep(time.Second)
    fmt.Println("Exiting normally")
}

func checkAndPrintWithRecover(a []string, index int) {
    defer handleOutOfBounds()
    go checkAndPrint(a, 2)
}

func checkAndPrint(a []string, index int) {
    if index > (len(a) - 1) {
        panic("Out of bound access for slice")
    }
    fmt.Println(a[index])
}

func handleOutOfBounds() {
    if r := recover(); r != nil {
        fmt.Println("Recovering from panic:", r)
    }
}
```

Output:

```go
Exiting normally
panic: Out of bound access for slice

goroutine 18 [running]:
main.checkAndPrint(0xc0000a6020, 0x2, 0x2, 0x2)
        /main.go:19 +0xe2
created by main.checkAndPrintWithRecover
        /main.go:14 +0x82
exit status 2
```

### Printing Stack Trace

To print a stack trace during a panic, use the `debug.PrintStack()` function.

```go
package main

import (
    "fmt"
    "runtime/debug"
)

func main() {
    a := []string{"a", "b"}
    checkAndPrint(a, 2)
    fmt.Println("Exiting normally")
}

func checkAndPrint(a []string, index int) {
    defer handleOutOfBounds()
    if index > (len(a) - 1) {
        panic("Out of bound access for slice")
    }
    fmt.Println(a[index])
}

func handleOutOfBounds() {
    if r := recover(); r != nil {
        fmt.Println("Recovering from panic:", r)
        fmt.Println("Stack Trace:")
        debug.PrintStack()
    }
}
```

Output:

```go
Recovering from panic: Out of bound access for slice
Stack Trace:
goroutine 1 [running]:
runtime/debug.Stack(0xd, 0x0, 0x0)
        stack.go:24 +0x9d
runtime/debug.PrintStack()
        stack.go:16 +0x22
main.handleOutOfBounds()
        main.go:27 +0x10f
panic(0x10ab8c0, 0x10e8f60)
        /runtime/panic.go:967 +0x166
main.checkAndPrint(0xc000104f58, 0x2, 0x2, 0x2)
        main.go:18 +0x111
main.main()
        main.go:11 +0x81
Exiting normally
```

### Return Value of the Function when Panic is Recovered

When a panic is recovered, the return value of a panicking function will be the default value of the return types of the panicking function.

```go
package main

import "fmt"

func main() {
    a := []int{5, 6}
    val, err := checkAndGet(a, 2)
    fmt.Printf("Val: %d\n", val)
    fmt.Println("Error: ", err)
}

func checkAndGet(a []int, index int) (int, error) {
    defer handleOutOfBounds()
    if index > (len(a) - 1) {
        panic("Out of bound access for slice")
    }
    return a[index], nil
}

func handleOutOfBounds() {
    if r := recover(); r != nil {
        fmt.Println("Recovering from panic:", r)
    }
}
```

Output:

```go
Recovering from panic: Out of bound access for slice
Val: 0
Error:  <nil>
```

In this case, the return value of the function is `0` for the `int` type and `<nil>` for the `error` type.

---
# GENERICS


Generics, derleme zamanında türden bağımsız kod yazmak için düşünülmüş bir kavramdır. Bu, Compile Time Polymorphism (CTP)'nin Go dilinde belirli bir ölçüde desteklenmesini sağlar. Go'ya generic'ler 1.18 sürümü ile eklenmiştir. Generic türü temsil eden isimlere **generic type parameters** denir. Bu parametreler, değişken isimlendirme kurallarına uygun olarak herhangi bir isim olarak belirlenebilir. Generic tür parametreleri, fonksiyon çağrısında derleyici tarafından tespit edilir (*type inference/deduction*). Bu durumda fonksiyon farklı türler ile çağrıldığında adeta farklı fonksiyonmuş gibi ele alınır. Bu durumun ayrıntıları aşağıda ele alınacaktır.

Generic bir fonksiyon bildiriminin genel biçimi şu şekildedir:

```go
func <fonksiyon ismi>[<generic tür parametre isim tür listesi>]([parametre değişken listesi]) [geri dönüş değeri] {
    //...
}
```

```go
func ForEach[T any](s []T, f func(int, T)) {
    for i, val := range s {
        f(i, val)
    }
}

func ReduceSlice[T any](a []T, f func(T, T) T) T {
    result := a[0]

    for _, val := range a {
        result = f(result, val)
    }

    return result
}
```

## Underlying Type (~)
Generic tür parametreleri için kısıt verilirken belirtilen türler için `~` kullanıldığında o tür için yapılan type
definition/type alias için de kullanılabilir bir kısıt bildirilmiş olur.

Bu anlamda  `~` aslında underlying type'ı o tür olanlar için de bir kısıt olmuş olur.

```go
package main

import "fmt"

type Signed interface {
	~int | ~int8 | ~int16 | ~int32 | ~int64
}

type Unsigned interface {
	~uint | ~uint8 | ~uint16 | ~uint32 | ~uint64
}

type Integer interface {
	Signed | Unsigned
}

type MyValue int
type YourValue int8

func square[T Integer](val T) T {
	return val * val
}

func main() {
	var a int = 10
	var b int16 = 20
	var c MyValue = 45
	var d YourValue = 45

	fmt.Println(square(a))
	fmt.Println(square(b))
	fmt.Println(square(c))
	fmt.Println(square(d))
}
```

**Kısıtlar interface bildirmeden de doğrudan verilebilir**

```go
package main

import "fmt"

func square[T ~int | ~int8 | ~int16 | ~int32 | ~int64 | ~uint | ~uint8 | ~uint16 | ~uint32 | ~uint64](val T) T {
	return val * val
}

func main() {
	var a int = 10
	var b int16 = 20

	fmt.Println(square(a))
	fmt.Println(square(b))
}
```

```go
package cmath

import (
	"cmp"
	"math"
)

type Numeric interface {
	~int | ~float32 | ~rune | ~float64
}

type UnsignedInteger interface {
	~uint | ~uint8 | ~uint16 | ~uint64
}

func Sqrt[T Numeric](a T) any {
	return math.Sqrt(float64(a))
}

func SqrtUnsigned[T UnsignedInteger](a T) any {
	return math.Sqrt(float64(a))
}

func Add[T cmp.Ordered](a, b T) T {
	return a + b
}
```



### WEB NOTES
---
## Understanding The Generic Problem

Consider a scenario where you have a function that performs a specific operation on two values, let's call it `Operation()`:

```go
func Operation(a, b ???) ??? {
    // Some operation on a and b
    // ...
    return result
}

func main() {
    result := Operation(3, 4)
    fmt.Println(result) // Output: Some result based on the operation
}
```

The `Operation()` function is designed to work with specific data types. However, as your codebase grows, you find the need to perform the same operation on various types like integers, floats, strings, etc. Creating a separate function for each data type is neither practical nor maintainable.

If you attempt to use different types with the same `Operation()` function, you face challenges:


```go
result := Operation(3.14, 2.7)    // Error: mismatched types
result := Operation("Hello", "World") // Error: mismatched types
```

Using interfaces might seem like a solution, but it lacks the specificity you desire. You want `Operation()` to work with a predefined set of types, not any arbitrary type.

This is where Golang generics come in handy. They enable you to write a single generic function that can operate on a variety of types while maintaining type safety and code clarity.

```go
func Operation[T any](a, b T) T {
    // Some generic operation on a and b
    // ...
    return result
}
```

With generics, you can achieve a more versatile and concise solution to the problem of working with a specific set of types in a generic operation.

## What is a Generic Type?

In programming, a generic type is a type that can be used with multiple other types, allowing for code reusability and flexibility. It serves as a template, enabling you to write functions and data structures that work seamlessly with various data types without duplicating code.

>a _generic type_ is a type that can be used in conjunction with multiple types, and a _generic function_ is one that can work with more than one type.


## Generics Overview

To grasp the concept of generics in Go more effectively, let’s briefly compare how other programming languages, such as C++ and Java, implement generics. By understanding these implementations, we can better appreciate the unique approach that Golang brings to the table.
### Java

Java introduced generics with the release of Java 5, implementing them using type erasure. Type erasure is a technique where type information is removed at runtime, making generics a compile-time feature.

```go
public class Box<T> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

In this example, `T` is the type parameter that allows the `Box` class to work with different types of values.
## Golang Generics Syntax

In the world of Go, generics have made their grand entrance starting from version 1.18, adding a whole new level of flexibility and power to the language. Now, let’s dive into the syntax of Golang generics, exploring how they can be used with functions and types.

#### **Golang Generic Function Syntax**

To define a generic function in Go, we utilize the following syntax:

```go
func FunctionName[T Constraint](a, b T) T {
    // Function Body
}
```

In the above syntax, `FunctionName` represents the name of our **generic function**. The **square brackets** `[T Constraint]` indicate the use of a **type parameter** `T`, which can be any **type constraint**.

Inside the function parentheses `(a, b T)`, we define the **input parameters** `a` and `b` of type `T`. The return type of the function is also `T`, denoted after the parentheses. You can replace `T` with any valid identifier that fits your needs.

#### **Golang Generic Type Syntax**

Similarly, we can use generics when defining **types in Go**. The syntax for a generic type declaration is as follows:

```go
type Number[T Constraint] interface {
    Method(T) T
}

type Student[T Constraint] struct {
    Name T
}
```

In the syntax above, we showcase two types: `Number[T Constraint]` and `Student[T Constraint]`. Here, `Number` is an `interface` that specifies a method `Method` which takes a parameter of type `T` and returns a value of the same type. The `Student` `struct` type, on the other hand, has a single field `Name` of type `T`.

## Working with Golang Generics

Now that we have familiarized ourselves with the syntax of Golang generics, it’s time to dive into their practical usage. Let’s explore how we can employ Golang generics to solve a common problem.

Let’s build upon the example we discussed in the “Understanding The Problem” section. Imagine we want to create an `Add()` function that can handle both integer and float values, providing the sum as the result.

```go
func Add[T int | float64](a T, b T) T {
	return a + b
}

func main() {
	fmt.Println(Add(3, 4))       // Output: 7
	fmt.Println(Add(3.1, 4.1))   // Output: 7.199999999999999
}
```

In the above example, we define the `Add` function using generics. The function signature includes a type parameter `T`, which represents the type of the operands and the return value. We specify that `T` can be either `int` or `float64` using the **constraint** `[T int | float64]`.


## How Golang Generics Work?

Working with practical examples is fun, but understanding the underlying concepts is even more exciting. In this section, we will delve into the inner workings of Golang generics. We will dissect each component and explore how they are composed and function together.

In the previous section, we encountered terms like **type parameters** and **type constraints**. However, there are a few more concepts to grasp, such as **type argument**, **type instantiation**, **type sets**, and **type inference**. This section will provide a detailed explanation, and it’s possible that some aspects may not immediately make sense. But fear not! We will cover these topics comprehensively in upcoming sections, and you can always revisit this section for a complete understanding.

#### Go Generics Example

To better understand how Golang generics work, let’s continue with the example from the previous section:

```go
// Generic Function
func Add[T int | float64](a T, b T) T {
	return a + b
}

func main() {
	add := Add[int]    // Type instantiation
	fmt.Println(reflect.TypeOf(add)) // Output: func(int, int) int
	fmt.Println(add(1, 2))           // Output: 3
}
```

In this updated example, the `Add()` function remains the same, but the way we call the function has changed. Now, pay close attention:

When we write `Add[int]`, this part is known as **type instantiation**, where we assign a specific type as a **type argument**. It instructs the compiler to generate a concrete version of the generic function for the specified type.

the `reflect package` to check the type of the **type-instantiated function variable**.  the output, the type instantiation converts the generic function into a normal Go function. In this case, the type of `add` is `func(int, int) int`, which is then used for function calls as usual.

# Golang Interface as Type Sets

In the latest release of Go 1.18, there have been notable changes to the definition of interfaces. Post Go 1.18, Golang interfaces can now define a set of types in addition to a set of methods. These adjustments were made to support type constraints in Golang Generics. Let’s explore these changes and what is essential to comprehend for mastering Golang Generics.

## Background

The motivation behind these changes becomes evident when considering an example. Suppose we aim to create a generic comparison function. The code might initially look like this:

```go
func Compare[T any](a, b T) bool {
    return a == b      // invalid operation: a == b (incomparable types in type set)
}

func main() {
    println(Compare(1, 2))
}
```

However, notice a potential issue here. The type parameter’s constraint is bound with the `any` type, allowing the `Compare` function to accept any type as its argument. Yet, if we pass a slice, can it be compared using the `==` operator? No, because slices do not support the `==` operator. This situation highlights the need to create a set of types to be used as constraints, introducing the concept of type sets.

Type sets are essentially interfaces that contain one or more sets of types using the `|` (Union) operator.

## Example

```go
// Type Set
type Num interface {
    int | float32 | float64 | string | bool
}

func Compare[T Num](a, b T) bool {
    return a == b
}

func main() {
    println(Compare(1, 2))         // false
    println(Compare(1, 1))         // true
    println(Compare(1.1, 1.1))     // true
    println(Compare(1.1, 2.2))     // false
    println(Compare("1", "2"))     // false
}
```

In this example, we created a type set called `Num` using the `|` (Union) operator to combine multiple types. Now, our generic function works properly because we have ensured that the type set only contains types that support the `==` operator.

# The Underlying Type Element

In Go 1.18, a new operator, ~ (tilde), has been introduced, known as the underlying type operator. Let's delve into understanding this operator and its relevance in Golang generics.

## Introduction

The underlying type operator (~) plays a significant role in Golang generics. To comprehend its purpose, let's revisit an example:

```go
type Num interface {
    int | float32 | float64 | string | bool
}

func Compare[T Num](a, b T) bool {
    return a == b
}

func main() {
    type Integer int
    var a Integer = 1
    var b Integer = 2
    println(Compare(a, b))
}

```

## The Challenge

While the core logic remains the same, passing values as arguments has changed. However, an error occurs: `Integer does not satisfy Num (possibly missing ~ for int in Num)`. Why?

The type parameter of the `Compare` function is bound to the `Num` type set, allowing only explicitly defined types within the set. The error arises because `Integer` has an underlying type of `int`, and the type set expects an explicit match. Here, the underlying operator (~) becomes crucial.

## Using the Underlying Type Element

Let's enhance the example by incorporating the underlying operator:

```go
// Type Set
type Num interface {
    ~int | ~float32 | ~float64 | ~string | ~bool
}

func Compare[T Num](a, b T) bool {
    return a == b
}

func main() {
    type Integer int
    type Str string
    type Double float64

    var a Integer = 1
    var b Integer = 2

    var s1 Str = "Hello"
    var s2 Str = "Hello"

    var d1 Double = 1.1
    var d2 Double = 1.2

    println(Compare(a, b))   // false
    println(Compare(s1, s2)) // true
    println(Compare(d1, d2)) // false
}
```

By utilizing the underlying operator (~), we modified the `Num` type set to consider underlying types explicitly. This improvement allows us to pass arguments whose underlying types match those defined within the type set.

In this improved example, the `Compare` function can correctly compare values of types like `Integer`, `Str`, and `Double`. The underlying operator (~) provides flexibility in working with underlying types, enhancing the capabilities of generics in Go.

# Type Parameters in Golang Generics

In the earlier sections, we explored the concept of type parameters in Golang generics. Let’s delve deeper to enhance our understanding of this crucial aspect.

## Overview

Type parameters serve as abstract data types in generic code, allowing us to write code that can work with different types without sacrificing reusability and flexibility. Think of type parameters as placeholders to be replaced with actual types during the type instantiation of the generic code.

## Union Constraint Elements

In some cases, we may need to impose multiple constraints on the type parameters. Golang allows us to achieve this using the union `|` operator. For example, when defining generic functions or types, we can specify multiple constraints:

```go
func F[T int | float64 | string](a, b T) T {...}
```

Similarly, when working with types, we can define a type interface or a struct with multiple constraints:

```go
type Number interface {
    int | float64 | string
}

type Num[T int | float64 | string] interface{}

type Student[T int | float64 | string] struct {
    Name T
}
```

## Multiple Type Parameters

Just as a regular function can have multiple parameters, type parameters can also be defined in multiples. This allows us to work with multiple types simultaneously. For instance:

```go
func Add[T int32 | float32, S int64 | float64](a T, b S) S {
	return S(a) + b
}

func main() {
	fmt.Println(Add[int32, float64](3, 5.5))   // Output: 8.5
}
```

Here, the `Add` function takes two type parameters `T` and `S`, which can be either `int32` or `float32` for `T`, and `int64` or `float64` for `S`.

## Type Parameters Reference

A fascinating concept of type parameters in Go generics is the ability to reference any type parameter that has not been defined yet. This feature adds flexibility and enables you to create generic functions that can work with multiple types, even if they are related to each other within the same function.

```go
func PrintList[S []T, T any](list S) {
    for _, v := range list {
        println(v)
    }
}

func main() {
    PrintList([]int{1, 2, 3})
    PrintList([]string{"a", "b", "c"})
}
```

the `PrintList` function takes two type parameters: `S` and `T`. The first parameter, `S []T`, represents a slice of elements of type `T`. The second parameter, `T any`, can be any type. The dynamic referencing of type parameters allows the function to determine the type of elements in the slice based on the provided type parameter `T`.

This dynamic referencing showcases the flexibility and versatility of generics in Go, enabling the creation of generic functions that adapt to various types for a concise and reusable solution.

# Type Constraints in Golang Generics

In the previous section, we explored type parameters, but our understanding wouldn’t be complete without delving into the world of type constraints. So, let’s dive right in!

## What is a Type Constraint?

A type constraint, also known as a meta-type, is an interface that defines a set of rules regarding what type of values can be used as arguments for a specific type parameter.

To illustrate the concept of type constraints, let’s consider the following example:

```go
func Add[T int](a, b T) T {
    return a + b
}

func main() {
    println(Add(1, 2))

```


`T int` as the constraint for the type parameter. However, according to the definition , a type constraint is actually an interface. So, it can also be written as:

```go
func Add[T interface{ int }](a, b T) T {}
```

Using Union Operator:

```go
func Add[T interface{ int | float64 }](a, b T) T {}
```

But hold on! While these alternative ways of expressing constraints are technically valid, they can compromise the readability of your code. So, it’s generally recommended to stick with the first form for the sake of clarity.

## The Comparable Constraint

In the “Type Set” section, we discussed the need to define a set of types that support comparison operators when working with generics in Go. However, the good news is that the Go developers have introduced a convenient built-in type parameter constraint called “comparable”.

This constraint allows developers to utilize existing Go types that inherently support comparison operators without the need for additional type sets.

```go
func F[T comparable](a, b T) bool {
    return a == b
}

func main() {
    fmt.Println(F(1, 2))            // false
    fmt.Println(F("a", "a"))     // true
    fmt.Println(F([]int{1, 2, 3}, []int{1, 2, 3}))   // Error: []int does not satisfy comparable)
```

the generic function `F` uses the `comparable` constraint by specifying `[T comparable]` as a type parameter. This constraint ensures that the types passed to the function must support comparison operators, such as == , >,  <, etc.


# Type Argument and Type Instantiation

Now that we have a solid understanding of type parameters and type constraints, let's dive deeper into the exciting world of type arguments and instantiation. Understanding how type instantiation works is essential to prepare for the thrilling world of Golang Generics.

## What is Type Instantiation?

Type instantiation is the process of substituting type arguments for type parameters in a generic function or type. It transforms generic code into specific, non-generic code tailored to specific needs.

Let’s take a look at an example:

```go
add := Add[float64]
fmt.Println(reflect.TypeOf(add)) // Output: func Add(a, b float64) float64 {}
```

In this example, we define the “type argument” as `float64`, which replaces the “type parameter” in the generic function. As a result, the generic function becomes a non-generic function, as indicated by the output of the reflect package.

## Type Instantiation Steps

Type instantiation involves two crucial steps:

1. **Substituting Type Arguments:** Each type argument is substituted for its corresponding type parameter throughout the generic declaration. This substitution encompasses the type parameter list itself and any other types associated with it.
    
2. **Satisfying Type Constraints:** After substitution, each type argument must satisfy the constraint of the corresponding type parameter. If a type argument fails to satisfy the constraint, instantiation fails.
    

## Rules of Type Instantiation

To make things more interesting, let’s explore some rules regarding type instantiation in Golang generics:

- **Type Argument Required:** For a generic function that isn’t called, you need to provide a type argument list for successful instantiation. It’s a necessary ingredient to unlock the power of generics.
    
- **Partial Type Arguments are Allowed:** In some cases, you can provide a partial type argument list, leaving some arguments unspecified. However, any remaining “type argument” must be inferable based on the context.
    
- **Partial Type Argument List Cannot be Empty:** Remember, a partial type argument list cannot be empty. You need to include at least the first argument to initiate the process.
    
- **Right to Left Type Argument Omission:** When omitting type arguments, you have the freedom to do it from “right to left“. In other words, you can omit type arguments in reverse order, starting from the rightmost parameter.

```go
func F[T []V, S []T, V int](list T, matrix S, size V) {
    // Function body here
}

func main() {
    // Explicitly defined Type Argument for Type Instantiation 
    f := F[[]int]       // Partial Type Argument
    // Rest of the code
}
```

we’ve omitted two “type arguments” in the “right to left” order. It’s just one of the many intriguing possibilities that Golang generics offer.

# Type Inference in Golang Generics

In the previous section, we briefly touched upon the concept of type inference. Now, let’s take a deeper dive into this topic.

## What is Type Inference?

Type inference is the process of determining the correct types of type arguments when they are not explicitly provided by the user. It plays a crucial role in working with generic functions or types. Without proper type inference, the user will have to do extra work of explicitly assigning type arguments for type instantiation.

## Key Components of Type Inference

In Go, type inference involves several components that work together to deduce types in a concise manner. Let’s explore these components briefly:

- **Type Parameter List:** This list defines the unknown types as placeholders for inference. They represent the types that need to be determined based on the context.
- **Substitution Map:** The substitution map (M) keeps track of known type arguments for the type parameters. It is updated as type arguments are inferred.
- **Ordinary Function Arguments:** For function calls, typed ordinary function arguments undergo function argument type inference to determine their types based on given values.
- **Constraint Type Inference:** This step analyzes constraints on generic types to narrow down the possible types assignable to type parameters.
- **Default Type Inference:** For untyped ordinary function arguments, default types are used to infer their types during function argument type inference.

The process continues until the substitution map has a type argument for each type parameter or until an inference step fails. Failed steps or incomplete substitution maps indicate unsuccessful type inference.

## Types of Type Inference

There are two types of type inference that we’ll explore: function argument type inference and constraint type inference.

### Function Argument Type Inference

As the name suggests, function argument type inference is concerned with inferring the types of a function’s arguments. This type of inference occurs when the “type arguments” are determined based on the types of the function’s arguments.

Let’s consider an example to illustrate this:

```go
func Add[T int | float32](a, b T) T {
	return a + b
}

func main() {
	println(Add[int](1, 2)) // Explicit type argument
	println(Add(1, 2))      // Type inference (No type argument)
```

In the above code snippet, we have a generic function called Add. It takes two arguments, a and b, of type T, which can be either int or float32. In the main function, we demonstrate both explicit type argument usage and type inference. In the second println statement, type inference is used, as we don’t explicitly specify the type argument for Add.

### Constraint Type Inference

Constraint type inference, on the other hand, involves inferring type arguments based on type constraints.

```go
type Num interface {
	int | float64
}

type IdConstraint interface {
	int | ~string
}

type Student[I IdConstraint, T Num] struct {
	ID         I
	TotalMarks T
}

func IncreaseMarks[S []Student[string, T], T Num](studentList S, marksToIncrease T) S {
	for index, _ := range studentList {
		studentList[index].TotalMarks += marksToIncrease
	}

	return studentList
}

func main() {
	student := []Student[string, int]{}
	student = append(student, Student[string, int]{"1", 90})
	student = append(student, Student[string, int]{"2", 80})
	student = append(student, Student[string, int]{"3", 70})

	s := IncreaseMarks(student, 10)
	for _, v := range s {
		println(v.ID, v.TotalMarks)
	}
```

In this example, we define two constraints: Num and IdConstraint. These constraints are utilized as type parameters in the Student struct type. We also define the IncreaseMarks function, which takes a list of Student structs, the marks to increase, and returns the updated slice of students. To make this function generic, we introduce type parameters.

In the main function, we create a slice of Student structs and append data for three students. We then call IncreaseMarks(student, 10) with the student slice and the marks to increase. Finally, we print the IDs and total marks of the students in the returned slice.

In this example, we haven’t explicitly used type arguments for type instantiation. However, the type is inferred from the constraints specified in the function and the constraints of the function arguments. This is known as type constraint inference.

Output:

```
1 100
2 90
3 80
```



---
# TIME & DATE

Go'da tarih-zaman işlemleri için genel olarak time nesnesi kullanılır.

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	now := time.Now()

	fmt.Println(now)

}
```

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	now := time.Now()

	fmt.Printf("%02d/%02d/%04d %02d:%02d:%02d\n", now.Day(), now.Month(), now.Year(), now.Hour(), now.Minute(), now.Second())
}
```

Go'da tarih formatlama işlemi Format metodu ile yapılabilir. Bu metot'da formatlama için özel değerler kullanılır:

2           	-> Gün
1 		    	-> Ay
2006	    	-> Yıl
15/3	    	-> Saat (24/12)
4		    	-> Dakika
5		    	-> Saniye
Mon, Monday 	-> Haftanın günü
Jan, January 	-> Ay bilgisi

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	now := time.Now()
	str := now.Format("02/01/2006 15:04:05")
	fmt.Printf("%s\n", str)
	str = now.Format("2/1/2006 15:4:5")
	fmt.Printf("%s\n", str)
	str = now.Format("02/01/2006 03:04:05 pm")
	fmt.Printf("%s\n", str)
	str = now.Format("2 Jan 2006 Mon 03:04:05 pm")
	fmt.Printf("%s\n", str)
	str = now.Format("2 January 2006 Monday 03:04:05 pm")
	fmt.Printf("%s\n", str)
}
```

Time yapısının Month metodu ile ay ilişkin değer elde edilebilir. Ay bilgisi 1 değerinden başlar. Weekday metodu
ile ilgili tarihin haftanın hangi günün geldiği bilgisi elde edilebilir. Bu değer Pazar için sıfır, Pazartesi için 1, ..., Cumartesi için 6 değeridir.

```go
package main

import (
	"fmt"
	"time"
)

var daysOfWeekTR = [7]string{"Pazar", "Pazartesi", "Salı", "Çarşamba", "Perşembe", "Cuma", "Cumartesi"}
var monthsTR = [13]string{"", "Ocak", "Şubat", "Mart", "Nisan", "Mayıs", "Haziran",
	"Temmuz", "Ağustos", "Eylül", "Ekim", "Kasım", "Aralık"}

func main() {
	now := time.Now()
	str := now.Format(fmt.Sprintf("2 %s 2006 %s 15:04:05", monthsTR[now.Month()], daysOfWeekTR[now.Weekday()]))
	str = now.Format(fmt.Sprintf("2 %s 2006 %s 15:04:05", now.Month(), now.Weekday()))

	fmt.Printf("%s\n", str)
	fmt.Printf("%s\n", str)
}
```

Time yapısının Parse fonksiyon ile ilgili formatte bir yazı Time türüne çevrilebilr. Parse fonksiyonun geri dönüş değeri (Time, error)'dur.

```go
package main

import (
	"SampleGoLand/csd/console"
	"fmt"
	"time"
)

func main() {
	str := console.ReadString("Input birthdate(DD/MM/YYYY):")
	birthDate, err := time.Parse("02/01/2006", str)

	if err == nil {
		fmt.Println(birthDate)
	} else {
		fmt.Printf("Invalid date:%s\n", err.Error())
	}
}
```

Format ve Parse fonksiyonları için önceden tanımlanmış bazı format string'leri vardır. Bunlar resmi dokumanlara göre şu şekildedir:

```go
const (
		Layout      = "01/02 03:04:05PM '06 -0700" // The reference time, in numerical order.
		ANSIC       = "Mon Jan _2 15:04:05 2006"
		UnixDate    = "Mon Jan _2 15:04:05 MST 2006"
		RubyDate    = "Mon Jan 02 15:04:05 -0700 2006"
		RFC822      = "02 Jan 06 15:04 MST"
		RFC822Z     = "02 Jan 06 15:04 -0700" // RFC822 with numeric zone
		RFC850      = "Monday, 02-Jan-06 15:04:05 MST"
		RFC1123     = "Mon, 02 Jan 2006 15:04:05 MST"
		RFC1123Z    = "Mon, 02 Jan 2006 15:04:05 -0700" // RFC1123 with numeric zone
		RFC3339     = "2006-01-02T15:04:05Z07:00"
		RFC3339Nano = "2006-01-02T15:04:05.999999999Z07:00"
		Kitchen     = "3:04PM"
		// Handy time stamps.
		Stamp      = "Jan _2 15:04:05"
		StampMilli = "Jan _2 15:04:05.000"
		StampMicro = "Jan _2 15:04:05.000000"
		StampNano  = "Jan _2 15:04:05.000000000"
		DateTime   = "2006-01-02 15:04:05"
		DateOnly   = "2006-01-02"
		TimeOnly   = "15:04:05"
	)
```

İki tarihin karşılaştırılması için After, Before, Equal ve Compare metotları kullanılabilir. Bu metotları parametreleri
karşılaştıracak zamandır. After, Before ve Equal metotlarının geri dönüş değerleri bool türdendir. Compare metodu int türden bir değere geri döner. Bu değer d1.Compare(d2) çağrısı için
	1. negatifse <=> d1 zamanı d2 zamanından önce gelir
	2. pozitifse <=> d1 zamanı d2 zamanından sonra gelir
	3. sıfırsa <=> d1 ile d2 eşittir

```go
package app

import (
	"fmt"
	"os"
	"time"
)

func checkArgs(message string) {
	if len(os.Args) != 2 {
		fmt.Println(message)
		os.Exit(1)
	}
}

func checkError(err error, message string) {
	if err != nil {
		fmt.Println(message)
		os.Exit(1)
	}
}

func getAge(birthDate, now time.Time) float64 {
	return float64(now.Unix()-birthDate.Unix()) / float64(60*60*24*365)
}

func Run() {
	checkArgs("Geçersiz komut satırı argümanları!...")
	str := os.Args[1]
	birthDate, err := time.Parse("02/01/2006", str)
	checkError(err, "Geçersiz tarih!...")
	now := time.Now()
	now = time.Date(now.Year(), now.Month(), now.Day(), 0, 0, 0, 0, time.UTC)
	birthDay := time.Date(now.Year(), birthDate.Month(), birthDate.Day(), 0, 0, 0, 0, time.UTC)
	age := getAge(birthDate, now)

	switch status := now.Compare(birthDay); status {
	case 1:
		fmt.Printf("Geçmiş doğum gününüz kutlu olsun. Yani yaşınız:%f\n", age)
	case -1:
		fmt.Printf("Doğum gününüz şimdiden kutlu olsun. Yani yaşınız:%f\n", age)
	default:
		fmt.Printf("Doğum gününüz kutlu olsun. Yani yaşınız:%f\n", age)
	}
}
```


### WEB NOTES

**Time** or **Date** is represented in Go using **time.Time** struct. time can be also be represented as a

- **Unix Time (Also known as Epoch Time)** – It is the number of seconds elapsed since 00:00:00 UTC on 1 January 1970. This time is also known as the Unix epoch.

# **Structure**

**time.Time** object is used to represent a specific point in time. The **time.Time** struct is as below

```go
type Time struct {
    // wall and ext encode the wall time seconds, wall time nanoseconds,
    // and optional monotonic clock reading in nanoseconds.
    wall uint64
    ext  int64
    //Location to represent timeZone
    // The nil location means UTC
    loc *Location
}
```

every **time.Time** object has an associated **location** value which is used to determine the minute, hour, month, day and year corresponding to that time.

# **Create a new time**

## **Using time.Now()**

This function can be used to get the current local timestamp. The signature of the function is

```go
func Now() Time
```

## **Using time.Date()**

This function returns the time which is **yyyy-mm-dd hh:mm:ss + nsec** nanoseconds with the appropriate time zone corresponding to the given location. The signature of the function is:

```go
func Date(year int, month Month, day, hour, min, sec, nsec int, loc *Location) Time
```

# **Understanding Duration**

**duration** is the time that has elapsed between two instants of time. It is represented as **int64nanosecond** count. So duration is nothing in Go but just a number representing time in nanoseconds. So if duration value is  equal to **1000000000** then it represents **1 sec** or **1000 milliseconds** or **10000000000 nanoseconds**

duration between two time values 1 hour apart will be below value which is equal number of nanoseconds in 1 hour.

```go
1 *60*60*1000*1000*1000
```

It is represented as below in the **time** package.

```go
type Duration int64
```

Below are some common duration which are defined in **time** package

```go
const (
    Nanosecond  Duration = 1
    Microsecond          = 1000 * Nanosecond
    Millisecond          = 1000 * Microsecond
    Second               = 1000 * Millisecond
    Minute               = 60 * Second
    Hour                 = 60 * Minute
)
```

Some of the function defined on **time.Time** object that returns the **Duration** are

- **func (t Time) Sub(u Time) Duration** – It returns the duration t-u
- **func Since(t Time) Duration –** It returns the duration which has elapsed since t
- **func Until(t Time) Duration** – It returns the duration until t

# **Add or Subtract to a time**

**Time** package in golang defines two ways of adding or subtracting to a time.

- **Add** function – It is used to add/subtract a duration to time t. Since duration can be represented in hours, minutes, seconds, milliseconds, microseconds and nanoseconds, therefore Add function can be used to add/subtract hours, minutes, seconds, milliseconds, microseconds and nanoseconds from a time . Its signature is

```go
func (t Time) Add(d Duration) Time
```

- **AddDate** function – It is used to add/subtract years, months and days to time t. Its signature is

```go
func (t Time) AddDate(years int, months int, days int) Time
```

Note: Positive values are used to add to time and negative values are used to subtract.

## **Add to time**

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    t := time.Now()

    //Add 1 hours
    newT := t.Add(time.Hour * 1)
    fmt.Printf("Adding 1 hour\n: %s\n", newT)

    //Add 15 min
    newT = t.Add(time.Minute * 15)
    fmt.Printf("Adding 15 minute\n: %s\n", newT)

    //Add 10 sec
    newT = t.Add(time.Second * 10)
    fmt.Printf("Adding 10 sec\n: %s\n", newT)

    //Add 100 millisecond
    newT = t.Add(time.Millisecond * 10)
    fmt.Printf("Adding 100 millisecond\n: %s\n", newT)

    //Add 1000 microsecond
    newT = t.Add(time.Millisecond * 10)
    fmt.Printf("Adding 1000 microsecond\n: %s\n", newT)

    //Add 10000 nanosecond
    newT = t.Add(time.Nanosecond * 10000)
    fmt.Printf("Adding 1000 nanosecond\n: %s\n", newT)

    //Add 1 year 2 month 4 day
    newT = t.AddDate(1, 2, 4)
    fmt.Printf("Adding 1 year 2 month 4 day\n: %s\n", newT)
}
```

**Output:**

```go
Adding 1 hour:
 2020-02-01 02:16:35.893847 +0530 IST m=+3600.000239893

Adding 15 minute:
 2020-02-01 01:31:35.893847 +0530 IST m=+900.000239893

Adding 10 sec:
 2020-02-01 01:16:45.893847 +0530 IST m=+10.000239893

Adding 100 millisecond:
 2020-02-01 01:16:35.903847 +0530 IST m=+0.010239893

Adding 1000 microsecond:
 2020-02-01 01:16:35.903847 +0530 IST m=+0.010239893

Adding 1000 nanosecond:
 2020-02-01 01:16:35.893857 +0530 IST m=+0.000249893

Adding 1 year 2 month 4 day:
 2021-04-05 01:16:35.893847 +0530 IST
```

## **Subtract to time**

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    t := time.Now()

    //Add 1 hours
    newT := t.Add(-time.Hour * 1)
    fmt.Printf("Subtracting 1 hour:\n %s\n", newT)

    //Add 15 min
    newT = t.Add(-time.Minute * 15)
    fmt.Printf("Subtracting 15 minute:\n %s\n", newT)

    //Add 10 sec
    newT = t.Add(-time.Second * 10)
    fmt.Printf("Subtracting 10 sec:\n %s\n", newT)

    //Add 100 millisecond
    newT = t.Add(-time.Millisecond * 10)
    fmt.Printf("Subtracting 100 millisecond:\n %s\n", newT)

    //Add 1000 microsecond
    newT = t.Add(-time.Millisecond * 10)
    fmt.Printf("Subtracting 1000 microsecond:\n %s\n", newT)

    //Add 10000 nanosecond
    newT = t.Add(-time.Nanosecond * 10000)
    fmt.Printf("Subtracting 1000 nanosecond:\n %s\n", newT)

    //Add 1 year 2 month 4 day
    newT = t.AddDate(-1, -2, -4)
    fmt.Printf("Subtracting 1 year 2 month 4 day:\n %s\n", newT)
}
```

**Output:**

```go
Subtracting 1 hour:
 2020-02-01 00:18:29.772673 +0530 IST m=-3599.999784391

Subtracting 15 minute:
 2020-02-01 01:03:29.772673 +0530 IST m=-899.999784391

Subtracting 10 sec:
 2020-02-01 01:18:19.772673 +0530 IST m=-9.999784391

Subtracting 100 millisecond:
 2020-02-01 01:18:29.762673 +0530 IST m=-0.009784391

Subtracting 1000 microsecond:
 2020-02-01 01:18:29.762673 +0530 IST m=-0.009784391

Subtracting 1000 nanosecond:
 2020-02-01 01:18:29.772663 +0530 IST m=+0.000205609

Subtracting 1 year 2 month 4 day:
 2018-11-27 01:18:29.772673 +0530 IST
```

# **Time Parsing/Formatting**

Golang, instead of using codes, uses date and time format placeholders that look like date and time only. Go uses standard time, which is:

```go
Mon Jan 2 15:04:05 MST 2006  (MST is GMT-0700)
or 
01/02 03:04:05PM '06 -0700
```

  
So if you notice go uses

- 01 for day of the month ,
- 02 for the month
- 03 for hours ,
- 04 for minutes
- 05 for second
- and so on

Below placeholder table describes the exact mapping. Go takes a more pragmatic approach where you don’t need to remember or lookup for the traditional formatting codes as in other languages

|   |   |
|---|---|
|**Type**|**Placeholder**|
|Day|**2** or **02** or **_2**|
|Day of Week|**Monday** or **Mon**|
|Month|**01** or **1** or **Jan** or **January**|
|Year|**2006** or **06**|
|Hour|**03** or **3** or **15**|
|Minutes|**04** or **4**|
|Seconds|**05** or **5**|
|Milli Seconds  (ms)|**.000**        //Trailing zero will be includedor **.999**   //Trailing zero will be omitted|
|Micro Seconds (μs)|**.000000**             //Trailing zero will be includedor **.999999**        //Trailing zero will be omitted|
|Nano Seconds (ns)|**.000000000**        //Trailing zero will be includedor **.999999999** //Trailing zero will be omitted|
|am/pm|**PM** or **pm**|
|Timezone|**MST**|
|Timezone offset |**Z0700** or **Z070000** or **Z07** or **Z07:00** or **Z07:00:00**  or **-0700** or  **-070000** or **-07** or **-07:00** or **-07:00:00**|

## **Time Parse Example**

**time.Parse**. The signature of the function is

```none
func Parse(layout, value string) (Time, error)
```

**time.Parse** function takes in two arguments

- First argument is the layout consisting of time format placeholder

- Second argument is the actual formatted string representing a time.

The way you have to go about this is to make sure that the layout string (first argument ) matches the string representation (second argument) of the time you want to parse into time.Time. For parsing

- For parsing **2020-01-29**, layout string should be **06-01-02** or **2006-01-02** or something which maps correctly based on above placeholder table.

- Similarly for parsing **“2020-Jan-29 Wednesday 12:19:25”** the layout string can be **“2006-Jan-02 Monday 03:04:05”**

Below are the working Code Examples of **time.Parse().**

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    //Parse YYYY-MM-DD
    timeT, _ := time.Parse("2006-01-02", "2020-01-29")
    fmt.Println(timeT)

    //Parse YY-MM-DD
    timeT, _ = time.Parse("06-01-02", "20-01-29")
    fmt.Println(timeT)

    //Parse YYYY-#{MonthName}-DD
    timeT, _ = time.Parse("2006-Jan-02", "2020-Jan-29")
    fmt.Println(timeT)

    //Parse YYYY-#{MonthName}-DD WeekDay HH:MM:SS
    timeT, _ = time.Parse("2006-Jan-02 Monday 03:04:05", "2020-Jan-29 Wednesday 12:19:25")
    fmt.Println(timeT)

    //Parse YYYY-#{MonthName}-DD WeekDay HH:MM:SS PM Timezone TimezoneOffset
    timeT, _ = time.Parse("2006-Jan-02 Monday 03:04:05 PM MST -07:00", "2020-Jan-29 Wednesday 12:19:25 AM IST +05:30")
    fmt.Println(timeT)
}
```

**Output:**

```go
2020-01-29 00:00:00 +0000 UTC
2020-01-29 00:00:00 +0000 UTC
2020-01-29 00:00:00 +0000 UTC
2020-01-29 12:19:25 +0000 UTC
2020-01-29 00:19:25 +0530 IST
```

## **Time Formatting Example**

**time.Format** function can be used to format time to a string representation. The signature of the function is

```go
func (t Time) Format(layout string)
```

Let’s see some time format code examples

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    now := time.Now()
    
    //Format YYYY-MM-DD
    fmt.Printf("YYYY-MM-DD: %s\n", now.Format("2006-01-02"))

    //Format YY-MM-DD
    fmt.Printf("YY-MM-DD: %s\n", now.Format("06-01-02"))

    //Format YYYY-#{MonthName}-DD
    fmt.Printf("YYYY-#{MonthName}-DD: %s\n", now.Format("2006-Jan-02"))

    //Format HH:MM:SS
    fmt.Printf("HH:MM:SS: %s\n", now.Format("03:04:05"))

    //Format HH:MM:SS Millisecond
    fmt.Printf("HH:MM:SS Millisecond: %s\n", now.Format("03:04:05 .999"))

    //Format YYYY-#{MonthName}-DD WeekDay HH:MM:SS
    fmt.Printf("YYYY-#{MonthName}-DD WeekDay HH:MM:SS: %s\n", now.Format("2006-Jan-02 Monday 03:04:05"))

    //Format YYYY-#{MonthName}-DD WeekDay HH:MM:SS PM Timezone TimezoneOffset
    fmt.Printf("YYYY-#{MonthName}-DD WeekDay HH:MM:SS PM Timezone TimezoneOffset: %s\n", now.Format("2006-Jan-02 Monday 03:04:05 PM MST -07:00"))
}
```

**Output:**

```go
YYYY-MM-DD: 2020-01-25
YY-MM-DD: 20-01-25
YYYY-#{MonthName}-DD: 2020-Jan-25
HH:MM:SS: 11:14:16
HH:MM:SS Millisecond: 11:14:16 .213
YYYY-#{MonthName}-DD WeekDay HH:MM:SS: 2020-Jan-25 Saturday 11:14:16
YYYY-#{MonthName}-DD WeekDay HH:MM:SS PM Timezone TimezoneOffset: 2020-Jan-25 Saturday 11:14:16 PM IST +05:30
```

# **Time Diff**

**time** package has a method **Sub** which can be used to get the difference between two different time values. The signature of the function is

```go
func (t Time) Sub(u Time) Duration
```

```go
currentTime := time.Now()
oldTime := time.Date(2020, 1, 2, 0, 0, 0, 0, time.UTC)
diff := currentTime.Sub(oldTime)
```

# **Time Conversion**

Below code shows conversion of

- time.Time to Unix Timestamp
- Unix Timestamp to time.Time

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    tNow := time.Now()

    //time.Time to Unix Timestamp
    tUnix := tNow.Unix()
    fmt.Printf("timeUnix %d\n", tUnix)

    //Unix Timestamp to time.Time
    timeT := time.Unix(tUnix, 0)
    fmt.Printf("time.Time: %s\n", timeT)
}
```

**Output:**

```go
timeUnix 1257894000
time.Time: 2009-11-10 23:00:00 +0000 UTC
```

## **Convert time between different timezones**

The **In** function can be used to change the **location** associated with a particular **time.Time** object. Whenever the **In** function is called on any **time.Time** object (say t)  then,

- A copy of **t** is created representing the same time instant.

- t’s location is set to the location passed to In function for display purposes

- **t** is returned back

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    now := time.Now()

    loc, _ := time.LoadLocation("UTC")
    fmt.Printf("UTC Time: %s\n", now.In(loc))
   
    loc, _ = time.LoadLocation("Europe/Berlin")
    fmt.Printf("Berlin Time: %s\n", now.In(loc))

    loc, _ = time.LoadLocation("America/New_York")
    fmt.Printf("New York Time: %s\n", now.In(loc))

    loc, _ = time.LoadLocation("Asia/Dubai")
    fmt.Printf("Dubai Time: %s\n", now.In(loc))
}
```

**Output:**

```go
UTC Time: 2020-01-31 18:09:41.705858 +0000 UTC
Berlin Time: 2020-01-31 19:09:41.705858 +0100 CET
New York Time: 2020-01-31 13:09:41.705858 -0500 EST
Dubai Time: 2020-01-31 22:09:41.705858 +0400 +04
```

---

#  Goroutines

Operating systems execute processes using a technique where they are logically run for a little bit from here and a little bit from there. For example, a CPU or core can only execute the machine code of a single process at any given moment. In the case of a system with, for instance, 4 CPUs or cores, how can more than 4 applications be run simultaneously? This is where the scheduling algorithms of operating systems come into play. These algorithms operate by allowing a process to run for a specified time and then preemptively switching to another process, enabling the concurrent execution of multiple applications. This concept is generally referred to as ***preemptive***.

The maximum time a process will be executed on a CPU or core is referred to as ***quantum time.*** In other words, when it is the turn of a process in the execution flow, it is allowed to run for a maximum duration of the quantum time. The term used for the swapping of a running process with another one when it's their turn is called a ***context switch***.

During a context switch, various pieces of information related to the current execution state are stored by the operating system, such as the position in the execution flow. The area where the operating system maintains various information about a process is referred to as the ***Process Control Block (PCB).***

In this context, at the operating system level, a process can be in one of the following states at any given moment:
- **Start state:** The initial state when a program becomes a process, i.e., when it first starts execution.
- **Ready state:** The state where the process is waiting for its turn to run.
- **Waiting state:** The state in which a process is blocked and waiting until a certain event occurs.
- **Running state:** The state where the process's code is assigned to and executed on the CPU or core.
- **End state:** The state when the process completes its execution.

**Key Notes:** The concept related to the CPU or core to which a thread is assigned while in the running state is called ***affinity mask***.

A stream of execution that enters the scheduling independently for a process is referred to as a ***thread***. When a process is created, a thread called the main ***thread*** is created. In this sense, at the system level, a process has at least one thread. Programmers can create various threads within the flow to generate different streams (asynchronous). In reality, scheduling is done at the thread level rather than the process level in the operating system. The specifics of how scheduling is done are system-specific, and operating systems can employ various algorithms.

In Go, the flow of the main thread of a program is the `main` method. To create a thread or establish an asynchronous flow in Go, the `go` keyword is used. The streams created with Go are referred to as ***goroutines*** in Go terminology. Goroutines are managed not by the operating system but by the ***Go runtime.*** This allows goroutines to operate more efficiently compared to traditional operating system threads. The management of goroutine-related flows in Go is handled by the ***Go scheduler***.


The general form of the `go` keyword is as follows:

```go
go <function call>
```

When the `go` keyword is used, the function called with it runs in a separate thread. The `go` keyword does not wait for the function call to complete. Therefore, a new flow has been created with the `go` keyword, and it continues asynchronously with the other flows of the process. When the `main` function finishes, the process terminates. As a result, when the process ends, all other flows of the process also come to an end.


**Key Notes:** When a process is created, some initial operations (startup code) are performed before the `main` function is called, even before loading import packages. These initial operations are system-specific. When the `main` function finishes, some final operations are carried out, and the `os.Exit` function is invoked. This function, in turn, calls the relevant function to terminate the process.


Typically, a separate stack area is created for each thread (including goroutines). The heap and global area are shared resources.

Communication between threads can be achieved using ***channels***.


```go
package main

import (
	"fmt"
	"time"
)

func goroutineCallback1(count int) {
	for i := 0; i < count; i++ {
		fmt.Printf("goroutine1:%d\n", i)
		time.Sleep(time.Second)
	}
}

func goroutineCallback2(count int) {
	for i := 0; i < count; i++ {
		fmt.Printf("goroutine2:%d\n", i)
		time.Sleep(time.Second)
	}
}

func main() {
	go goroutineCallback1(10)
	go goroutineCallback2(10)
	time.Sleep(20 * time.Second)
}

```

In the demo example below, since the threads have different stack areas, the variable 'i' in the loop is created separately for each thread.

```go
package main

import (
	"fmt"
	"time"
)

func goroutineCallback(count int, message string) {
	for i := 0; i < count; i++ {
		fmt.Printf("%s:%d\n", message, i)
		time.Sleep(time.Second)
	}
}

func main() {
	go goroutineCallback(10, "gr1")
	go goroutineCallback(10, "gr2")
	time.Sleep(20 * time.Second)
}

```

## Web Notes

Goroutines can be thought of as a lightweight thread that has a separate independent execution and which can execute concurrently with other goroutines. It is a function or method that is executing concurrently with other goroutines. It is entirely managed by the GO runtime.

###  **Start a go routine**

Golang uses a special keyword **‘go’**  for starting a goroutine. To start one just add **go** keyword before a function or method call. That function or method will now be executed in the goroutine.  Note that it is not the function or method which determines if it is a goroutine.

- Normal Running a function

```go
statment1
start()
statement2
```

- Running a function as a goroutine

```go
statment1
go start()
statement2
```

In running a function as a goroutine for the above scenario

1. First, statement1 will be executed
2. Then function start() will be called as a goroutine which will execute asynchronously.
3. **statement2** will be executed immediately. It will not wait for **start()** function to complete. The start function will be executed concurrently as a goroutine while the rest of the program continues its execution.

when calling a function as a goroutine, call will return immediately the execution will continue from the next line while the goroutine will be executed concurrently in the background.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    go start()
    fmt.Println("Started")
    time.Sleep(1 * time.Second)
    fmt.Println("Finished")
}

func start() {
    fmt.Println("In Goroutine")
}
```

**Output**

```go
Started
In Goroutine
Finished
```

```go
go start()
```

The above line will start a goroutine which will run the **start()** function. 

###  **Main goroutine**

The **main** function in the **main** package is the main goroutine. All  goroutines are started from the main goroutine. These goroutines can then start multiple other goroutine and so on.

The main goroutine represents the main program. Once it exits then it means that the program has exited.

Goroutines don’t have parents or children. When you start a goroutine it just executes alongside all other running goroutines. Each goroutine exits only when its function returns. The only exception to that is that all goroutines exit when the main goroutine (the one that runs function **main**) exits.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    go start()
    fmt.Println("Started")
    time.Sleep(1 * time.Second)
    fmt.Println("Finished")
}

func start() {
    go start2()
    fmt.Println("In Goroutine")
}
func start2() {
    fmt.Println("In Goroutine2")
}
```

**Output**

```go
Started
In Goroutine
In Goroutine2
Finished
```

the first goroutine starts the second goroutine. The first goroutine then prints **“In Goroutine”** and then it exits. The second goroutine then starts and prints **“In Goroutine2”**. It shows that goroutines don’t have parents or children and they exist as an independent execution.

###  **Creating Multiple Goroutines**

```go
package main

import (
    "fmt"
    "time"
)

func execute(id int) {
    fmt.Printf("id: %d\n", id)
}

func main() {
    fmt.Println("Started")
    for i := 0; i < 10; i++ {
        go execute(i)
    }
    time.Sleep(time.Second * 2)
    fmt.Println("Finished")
}
```

**Output**

```go
Started
id: 4
id: 9
id: 1
id: 0
id: 8
id: 2
id: 6
id: 3
id: 7
id: 5
Finished
```

Every time you will run the program it will give different outputs since the goroutines will be run concurrently and it is not deterministic which will run first.

### **Scheduling of the goroutines**

Once the go program starts,  go runtime will launch OS threads equivalent to the number of number of logical CPUs usable by the current process.  There is one logical CPU per virtual core where virtual core means

```go
virtual_cores = x*number_of_physical_cores
```

where x=number of hardware threads per core

The **``runtime.Numcpus``** function can be used to get the the number of logical processors available to the GO program.


```go
package main
import (
    "fmt"
    "runtime"
)
func main() {
    fmt.Println(runtime.NumCPU())
}
```

The go program will launch OS threads equal to the number of logical CPUs available to it or the output of ``runtime.NumCPU()``. These threads will be managed by the OS and scheduling of these threads onto CPU cores is the responsibility of OS only. 

The go runtime has its own scheduler that will multiplex the groutines on the OS level threads in the go runtime. So essentially each goroutine is running on an OS thread that is assigned to a logical CPU

There are two queues involved for managing the goroutines and assigning it to the OS threads

## **Local run queue**

Within go runtime each of this OS thread will have one queue associated with it. It is called Local Run Queue. It contains all the goroutines that will be executed in the context of that thread. The go runtime will be doing the scheduling and context switching of the goroutines belonging to a particular LRQ to the corresponding OS level thread which owns this LRQ

## **Global Run Queue**

It contains all the goroutines that haven't been moved to any LRQ of any OS thread. The Go scheduler will assign a goroutine from this queue to the Local Run Queue of any OS thread

![[Pasted image 20240219153753.png]]

### **Golang scheduler is a Cooperative Scheduler**

Means that is non-preemptive one.  There is no time based preemption that is happening which is the case with a preemptive scheduler.  In a cooperative scheduler threads have to explicitly yield execution. There are some specific check points where goroutine can yield its execution to other goroutine.

The runtime calls the scheduler on function calls to decide weather a new goroutine needs to be scheduled . So basically when a goroutine makes any function call, in that case scheduler will be called and context switch might happen meaning a new goroutine might be scheduled . It is also possible that existing goroutine also continues execution.  The scheduler also gets the opportunity for contexts switch on below events too

1. **Functions Call**
2. **Garbage Collection**
3. **Network Calls**
4. **Channel operations**
5. **On using go keyword**
6. **Blocking on primitives such as mutex etc**

It is to mention that scheduler runs during above events but it doesn't mean that context switch will happen. It is just that the scheduler gets the opportunity. It is up to the scheduler then weather to do a context switch or not.

### **Advantages of goroutines over threads**

- Goroutines in Go start with a small 8kb size and dynamically adjust, while OS threads are over 1 MB, making goroutines highly cost-effective to allocate.
- The go runtime efficiently manages the resizing and scheduling of goroutines, allowing the launch of a large number simultaneously, surpassing the limitations of traditional threads.
- Goroutines communicate through built-in channels, ensuring safe communication without explicit locking, preventing common issues like deadlocks and race conditions seen in threaded programming.

### **Anonymous Goroutines**

Anonymous functions in golang can also be called using goroutine.

```go
go func(){
   //body
}(args..)
```

There is no difference in behavior though when calling a anonymous function using goroutine or calling a normal function using goroutine

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    go func() {
        fmt.Println("In Goroutine")
    }()

    fmt.Println("Started")
    time.Sleep(1 * time.Second)
    fmt.Println("Finished")
}
```

**Output**

```go
Started
In Goroutine
Finished
```


---
# GO-CRON 

The **`cron`** command-line utility is a job scheduler "Job scheduler") on Unix-like operating systems. Users who set up and maintain software environments use cron to schedule jobs **cron jobs**, to run periodically at fixed times, dates, or intervals. It typically automates system maintenance or administration—though its general-purpose nature makes it useful for things like downloading files from the Internet and downloading email at regular intervals.

```
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday)
# │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
# │ │ │ │ │ 
# │ │ │ │ │
# * * * * *
```

``gocron`` is a job scheduling package which lets you run Go functions at pre-determined intervals.

```shell
go get github.com/go-co-op/gocron/v2
```

```go
package main

import (
	"fmt"
	"time"

	"github.com/go-co-op/gocron/v2"
)

func main() {
	// create a scheduler
	s, err := gocron.NewScheduler()
	if err != nil {
		// handle error
	}

	// add a job to the scheduler
	j, err := s.NewJob(
		gocron.DurationJob(
			10*time.Second,
		),
		gocron.NewTask(
			func(a string, b int) {
				// do things
			},
			"hello",
			1,
		),
	)
	if err != nil {
		// handle error
	}
	// each job has a unique id
	fmt.Println(j.ID())

	// start the scheduler
	s.Start()

	// block until you are ready to shut down
	select {
	case <-time.After(time.Minute):
	}

	// when you're done, shut it down
	err = s.Shutdown()
	if err != nil {
		// handle error
	}
}
```

## Concepts

- **Job**: The job encapsulates a "task", which is made up of a go function and any function parameters. The Job then provides the scheduler with the time the job should next be scheduled to run.
- **Scheduler**: The scheduler keeps track of all the jobs and sends each job to the executor when it is ready to be run.
- **Executor**: The executor calls the job's task and manages the complexities of different job execution timing requirements

## Features

### Job Types

Jobs can be run at various intervals.

- [**Duration**](https://pkg.go.dev/github.com/go-co-op/gocron/v2#DurationJob): Jobs can be run at a fixed `time.Duration`.
- [**Random duration**](https://pkg.go.dev/github.com/go-co-op/gocron/v2#DurationRandomJob): Jobs can be run at a random `time.Duration` between a min and max.
- [**Cron**](https://pkg.go.dev/github.com/go-co-op/gocron/v2#CronJob): Jobs can be run using a crontab.
- [**Daily**](https://pkg.go.dev/github.com/go-co-op/gocron/v2#DailyJob): Jobs can be run every x days at specific times.
- [**Weekly**](https://pkg.go.dev/github.com/go-co-op/gocron/v2#WeeklyJob): Jobs can be run every x weeks on specific days of the week and at specific times.
- [**Monthly**](https://pkg.go.dev/github.com/go-co-op/gocron/v2#MonthlyJob): Jobs can be run every x months on specific days of the month and at specific times.
- [**One time**](https://pkg.go.dev/github.com/go-co-op/gocron/v2#OneTimeJob): Jobs can be run once at a specific time. These are non-recurring jobs.

**Examples**

```GO
package main

import (
	"fmt"
	"github.com/go-co-op/gocron/v2"
	"os"
	"time"
)

func printMessage(message string) {
	fmt.Println(message)
}

func runApp() {
	scheduler, err := gocron.NewScheduler()

	if err != nil {
		fmt.Printf("Problem occurred while creating scheduler:%s\n", err.Error())
		os.Exit(1)
	}

	job, err := scheduler.NewJob(gocron.DurationJob(10*time.Second), gocron.NewTask(printMessage, "Hello, World!..."))

	if err != nil {
		fmt.Printf("Problem occurred while creating job:%s\n", err.Error())
		os.Exit(1)
	}
	fmt.Printf("Job Id = %v, Job Name:%s\n", job.ID(), job.Name())
	scheduler.Start()

	console.ReadString("")

	err = scheduler.Shutdown()
	if err != nil {
		fmt.Printf("Problem occurred while shut down:%s\n", err.Error())
		os.Exit(1)
	}

}

func main() {
	runApp()
}
```

```GO
package main

import (
	"SampleGoLand/csd/console"
	"fmt"
	"github.com/go-co-op/gocron/v2"
	"os"
)

func printMessage(message string) {
	fmt.Println(message)
}

func runApp() {
	scheduler, err := gocron.NewScheduler()

	defer func() {
		err = scheduler.Shutdown()
		if err != nil {
			fmt.Printf("Problem occurred while shut down:%s\n", err.Error())
			os.Exit(1)
		}
	}()

	if err != nil {
		fmt.Printf("Problem occurred while creating scheduler:%s\n", err.Error())
		os.Exit(1)
	}

	_, err = scheduler.NewJob(gocron.DailyJob(1, gocron.NewAtTimes(gocron.NewAtTime(19, 9, 10))), gocron.NewTask(printMessage, "Hello, World!..."))

	if err != nil {
		fmt.Printf("Problem occurred while creating job:%s\n", err.Error())
		os.Exit(1)
	}
	scheduler.Start()

	console.ReadString("")
}

func main() {
	runApp()
}
```


---
# GO - SQL

## User 

**Entity**

```GO
package entity

type User struct {
	Username, Password, Name, Phone string
}

func NewUser(username, password, name, phone string) *User {
	return &User{username, password, name, phone}
}
```

**Repository**

```go
package repository

import (
	"PaymentServiceApp/data/entity"
	"database/sql"
)

const saveCmd = `insert into users (username, password, name, phone) values ($1, $2, $3, $4)`
const findAllCmd = "select * from get_all_users()"
const findByIdCmd = `select * from get_user_by_username($1)` //`select * from users where username=$1`
const countCmd = "select count(*) from users"

type UserRepository struct {
	db *sql.DB
}

func NewUserRepository(db *sql.DB) *UserRepository {
	return &UserRepository{db}
}

func (ur *UserRepository) Count() (int, error) {
	rows, err := ur.db.Query(countCmd)

	if err != nil {
		return 0, err
	}

	rows.Next()

	var count int

	err = rows.Scan(&count)

	if err != nil {
		return 0, err
	}

	return count, nil
}

func (ur *UserRepository) ExistsById(username string) (bool, error) {
	//TODO
	panic("TODO")
}

func (ur *UserRepository) FindAll() ([]entity.User, error) {
	rows, err := ur.db.Query(findAllCmd)

	if err != nil {
		return nil, err
	}

	var users []entity.User

	for rows.Next() {
		var username, password, name, phone string

		err = rows.Scan(&username, &password, &name, &phone)

		if err != nil {
			return nil, err
		}

		users = append(users, *entity.NewUser(username, password, name, phone))
	}

	return users, nil
}

func (ur *UserRepository) FindById(username string) (*entity.User, error) {
	rows, err := ur.db.Query(findByIdCmd, username)

	if err != nil {
		return nil, err
	}

	if !rows.Next() {
		return nil, nil
	}

	var password, name, phone string

	err = rows.Scan(&username, &password, &name, &phone)

	if err != nil {
		return nil, err
	}

	return entity.NewUser(username, password, name, phone), nil
}

func (ur *UserRepository) FindAllFunc(f func(*entity.User)) error {
	rows, err := ur.db.Query(findAllCmd)

	if err != nil {
		return err
	}

	for rows.Next() {
		var username, password, name, phone string

		err = rows.Scan(&username, &password, &name, &phone)

		if err != nil {
			return err
		}
		f(entity.NewUser(username, password, name, phone))
	}

	return nil
}

func (ur *UserRepository) Save(user *entity.User) (*entity.User, error) {
	_, err := ur.db.Exec(saveCmd, user.Username, user.Password, user.Name, user.Phone)

	if err != nil {
		return nil, err
	}

	return user, nil
}

///////////////////////////////////////////////////////////////////////////////////////

func (ur *UserRepository) DeleteById(id string) error {
	//TODO implement me
	panic("implement me")
}

func (ur *UserRepository) Delete(entity *entity.User) error {
	//TODO implement me
	panic("implement me")
}

func (ur *UserRepository) DeleteAll() error {
	//TODO implement me
	panic("implement me")
}

func (ur *UserRepository) DeleteAllById(ids []string) error {
	//TODO implement me
	panic("implement me")
}

func (ur *UserRepository) SaveAll(entities ...entity.User) ([]entity.User, error) {
	//TODO implement me
	panic("implement me")
}
```

## Product

**Entity**
```go
package entity

type Product struct {
	Code, Name             string
	Stock, Cost, UnitPrice float64
}

func NewProduct(code, name string, stock, cost, unitPrice float64) *Product {
	return &Product{code, name, stock, cost, unitPrice}
}
```

**Repository**

```go
package repository

import "database/sql"

type ProductRepository struct {
	db *sql.DB
}

func NewProductRepository(db *sql.DB) *ProductRepository {
	return &ProductRepository{db}
}

//...
```

## Payment 

**Entity**

```go
package entity

type Payment struct {
	Id                    int
	Username, ProductCode string
	Amount, UnitPrice     float64
}

func NewPayment(id int, username, productCode string, amount, unitPrice float64) *Payment {
	return &Payment{id, username, productCode, amount, unitPrice}
}
```

**Repository**

```go
package repository

import "database/sql"

type PaymentRepository struct {
	db *sql.DB
}

func NewPaymentRepository(db *sql.DB) *PaymentRepository {
	return &PaymentRepository{db}
}
```


## WEB NOTES

The idiomatic way to use a SQL, or SQL-like, database in Go is through the [database/sql package](http://golang.org/pkg/database/sql/). It provides a lightweight interface to a row-oriented database.

To access databases in Go, you use a `sql.DB`. You use this type to create statements and transactions, execute queries, and fetch results.

 **a `sql.DB` isn’t a database connection**.

It’s an abstraction of the interface and existence of a database, which might be as varied as a local file, accessed through a network connection, or in-memory and in-process.

`sql.DB` performs some important tasks for you behind the scenes:

- It opens and closes connections to the actual underlying database, via the driver.
- It manages a pool of connections as needed, which may be a variety of things as mentioned.

The `sql.DB` abstraction is designed to keep you from worrying about how to manage concurrent access to the underlying datastore. A connection is marked in-use when you use it to perform a task, and then returned to the available pool when it’s not in use anymore

One consequence of this is that **if you fail to release connections back to the pool, you can cause `sql.DB` to open a lot of connections**, potentially running out of resources (too many connections, too many open file handles, lack of available network ports, etc)

## Database driver

To use `database/sql` you’ll need the package itself, as well as a driver for the specific database you want to use.

generally shouldn’t use driver packages directly, although some drivers encourage you to do so. Instead, your code should only refer to types defined in `database/sql`, if possible.  

This helps avoid making your code dependent on the driver, so that you can change the underlying driver (and thus the database you’re accessing) with minimal code changes.

It also forces you to use the Go idioms instead of ad-hoc idioms that a particular driver author may have provided.

No database drivers are included in the Go standard library. But there are plenty of them implemented as a third-party,  [https://golang.org/s/sqldrivers](https://golang.org/s/sqldrivers).

```go
import (  
"database/sql"  
_ "github.com/go-sql-driver/mysql"  
)
```

loading the driver anonymously, aliasing its package qualifier to `_` so none of its exported names are visible to our code. Under the hood, the driver registers itself as being available to the `database/sql` package, but in general nothing else happens with the exception that the init function is run.

##  Accessing the database

To create a `sql.DB`, you use `sql.Open()`. This returns a `*sql.DB`:

```go
func main() {
    db, err := sql.Open("mysql",
        "user:password@tcp(127.0.0.1:3306)/hello")
    if err != nil {
        log.Fatal(err)
    }
    defer db.Close()
}

```


1. The first argument to `sql.Open` is the driver name. This is the string that the driver used to register itself with `database/sql`, and is conventionally the same as the package name to avoid confusion. For example, it’s `mysql` for [github.com/go-sql-driver/mysql](https://github.com/go-sql-driver/mysql). Some drivers do not follow the convention and use the database name, e.g. `sqlite3` for [github.com/mattn/go-sqlite3](https://github.com/mattn/go-sqlite3) and `postgres` for [github.com/lib/pq](https://github.com/lib/pq).

2. The second argument is a driver-specific syntax that tells the driver how to access the underlying datastore.

3. always check and handle errors returned from all `database/sql` operations.

4.  It is idiomatic to `defer db.Close()` if the `sql.DB` should not have a lifetime beyond the scope of the function.

Perhaps counter-intuitively, `sql.Open()` does not establish any connections to the database, nor does it validate driver connection parameters. Instead, it simply prepares the database abstraction for later use.

The first actual connection to the underlying datastore will be established lazily, when it’s needed for the first time. If you want to check right away that the database is available and accessible use `db.Ping()` to do that, and remember to check for errors:

```go
err = db.Ping()  
if err != nil {  
	// do something here  
}
```

Although it’s idiomatic to `Close()` the database when you’re finished with it, the `sql.DB` object is designed to be long-lived. Don’t `Open()` and `Close()` databases frequently.

**Instead, create one `sql.DB` object for each distinct datastore you need to access, and keep it until the program is done accessing that datastore. Pass it around as needed, or make it available somehow globally, but keep it open. And don’t `Open()` and `Close()` from a short-lived function. Instead, pass the `sql.DB` into that short-lived function as an argument.**

## Retrieving Result Sets

Go’s `database/sql` function names are significant. If a function name includes `Query`, it is designed to ask a question of the database, and will return a set of rows, even if it’s empty.

Statements that don’t return rows should not use `Query` functions; they should use `Exec()`.

**the function names in `database/sql` provide a clear indication of the expected behavior based on whether they include "Query" or not.**

### Fetching Data from the Database

```go
var (
    id   int
    name string
)

rows, err := db.Query("select id, name from users where id = ?", 1)
if err != nil {
    log.Fatal(err)
}
defer rows.Close()

for rows.Next() {
    err := rows.Scan(&id, &name)
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println(id, name)
}

err = rows.Err()
if err != nil {
    log.Fatal(err)
}
```



1.  using `db.Query()` to send the query to the database. We check the error, as usual.
2.  defer `rows.Close()`. This is very important.
3.  iterate over the rows with `rows.Next()`.
4.  read the columns in each row into variables with `rows.Scan()`.
5.  check for errors after we’re done iterating over the rows.

This is pretty much the only way to do it in Go. You can’t get a row as a map, for example. That’s because everything is strongly typed. You need to create variables of the correct type and pass pointers to them

A couple parts of this are easy to get wrong, and can have bad consequences.

- `rows.Next()` indicates whether the next row from result set is available, and will return `true` until either result set is exhausted or an error has occurred during fetching the data. For this reason always check for an error at the end of the `for rows.Next()` loop (this is done calling `rows.Err()`). If there’s an error during the loop, you need to know about it. Don’t just assume that the loop iterates until you’ve processed all the rows.

-  Second, as long as there’s an open result set (represented by `rows`), the underlying connection is busy and can’t be used for any other query until `rows.Close()` is called. That means it’s not available in the connection pool. The nice thing about `database/sql` is that it will implicitly call `rows.Close()` for you, when `rows.Next()` returns `false`, but if you exit the loop prematurely, it is your responsibility to close the rows, otherwise the connection will be left busy and unavailable to other operations, leading to a connection leak. Thus, as a rule of thumb, always `defer rows.Close()`, to avoid connection leak and running out of resources.

- `rows.Close()` is a harmless no-op if it’s already closed, so it’s OK to call it multiple times. Notice, however, that we check the error from `db.Query()` first, and only defer `rows.Close()` if there isn’t an error, in order to avoid a runtime panic (e.g. when error is returned from `db.Query()` method, the `rows` object will be `nil`).

###  How Scan() Works

When  iterate over rows and scan them into destination variables, Go performs data type conversions work for you, behind the scenes. It is based on the type of the destination variable.

For example, if a database table uses string columns to store numerical values, you can pass pointers to more appropriate Go data types, such as integers. This allows for direct conversion without unnecessary copying of bytes.

Or, you can just pass `Scan()` a pointer to an integer. Go will detect that and call `strconv.ParseInt()` for you. If there’s an error in conversion, the call to `Scan()` will return it. Your code is neater and smaller now. This is the recommended way to use `database/sql`.


#### Preparing Queries

in general, always prepare queries to be used multiple times. The result of preparing the query is a prepared statement, which can have placeholders (a.k.a. bind values) for parameters that you’ll provide when you execute the statement. This is much better than concatenating strings, for all the usual reasons (avoiding SQL injection attacks, for example).

In MySQL, the parameter placeholder is `?`, and in PostgreSQL it is `$N`, where N is a number. SQLite accepts either of these. In Oracle placeholders begin with a colon and are named, like `:param1`

```go
stmt, err := db.Prepare("select id, name from users where id = ?")
if err != nil {
	log.Fatal(err)
}
defer stmt.Close()
rows, err := stmt.Query(1)
if err != nil {
	log.Fatal(err)
}
defer rows.Close()
for rows.Next() {
	// ...
}
if err = rows.Err(); err != nil {
	log.Fatal(err)
}
```

Under the hood, `db.Query()` actually prepares, executes, and closes a prepared statement. That’s three round-trips to the database. If you’re not careful, you can triple the number of database interactions your application makes


###  Single-Row Queries

```go
var name string
err = db.QueryRow("select name from users where id = ?", 1).Scan(&name)
if err != nil {
    log.Fatal(err)
}
fmt.Println(name)
```

Errors from the query are deferred until `Scan()` is called, and then are returned from that.


##  Modifying Data and Using Transactions

### Statements that Modify Data

Use `Exec()`, preferably with a prepared statement, to accomplish an `INSERT`, `UPDATE`, `DELETE`, or another statement that doesn’t return rows

```go
stmt, err := db.Prepare("INSERT INTO users(name) VALUES(?)")
if err != nil {
	log.Fatal(err)
}
res, err := stmt.Exec("Dolly")
if err != nil {
	log.Fatal(err)
}
lastId, err := res.LastInsertId()
if err != nil {
	log.Fatal(err)
}
rowCnt, err := res.RowsAffected()
if err != nil {
	log.Fatal(err)
}
log.Printf("ID = %d, affected = %d\n", lastId, rowCnt)
```

Executing the statement produces a `sql.Result` that gives access to statement metadata: the last inserted ID and the number of rows affected.

```go
_, err := db.Exec("DELETE FROM users")  // OK
_, err := db.Query("DELETE FROM users") // BAD
```

do **not** do the same thing, and **you should never use `Query()` like this.** The `Query()` will return a `sql.Rows`, which reserves a database connection until the `sql.Rows` is closed. Since there might be unread data (e.g. more data rows), the connection can not be used.

The garbage collector will eventually close the underlying `net.Conn` for you, but this might take a long time. Moreover the database/sql package keeps tracking the connection in its pool, hoping that you release it at some point, so that the connection can be used again. This anti-pattern is therefore a good way to run out of resources

### Working with Transactions

In Go, a transaction is essentially an object that reserves a connection to the datastore. It lets you do all of the operations, but guarantees that they’ll be executed on the same connection.

begin a transaction with a call to `db.Begin()`, and close it with a `Commit()` or `Rollback()` method on the resulting `Tx` variable. Under the covers, the `Tx` gets a connection from the pool, and reserves it for use only with that transaction. The methods on the `Tx` map one-for-one to methods you can call on the database itself, such as `Query()` and so forth.

Prepared statements that are created in a transaction are bound exclusively to that transaction.

not mingle the use of transaction-related functions such as `Begin()` and `Commit()` with SQL statements such as `BEGIN` and `COMMIT` in your SQL code. Bad things might result:

- The `Tx` objects could remain open, reserving a connection from the pool and not returning it.
- The state of the database could get out of sync with the state of the Go variables representing it.
- You could believe you’re executing queries on a single connection, inside of a transaction, when in reality Go has created several connections for you invisibly and some statements aren’t part of the transaction.

While you are working inside a transaction you should be careful not to make calls to the `db` variable. Make all of your calls to the `Tx` variable that you created with `db.Begin()`. `db` is not in a transaction, only the `Tx` object is. If you make further calls to `db.Exec()` or similar, those will happen outside the scope of your transaction, on other connections.

If you need to work with multiple statements that modify connection state, you need a `Tx` even if you don’t want a transaction per se. For example:

- Creating temporary tables, which are only visible to one connection.
- Setting variables, such as MySQL’s `SET @var := somevalue` syntax.
- Changing connection options, such as character sets or timeouts.

```go
package main

import (
	"database/sql"
	"fmt"
	"log"

	_ "github.com/go-sql-driver/mysql"
)

func main() {
	// Connect to the database
	db, err := sql.Open("mysql", "user:password@tcp(127.0.0.1:3306)/exampledb")
	if err != nil {
		log.Fatal(err)
	}
	defer db.Close()

	// Begin a transaction
	tx, err := db.Begin()
	if err != nil {
		log.Fatal(err)
	}

	// Example 1: Creating a temporary table within the transaction
	_, err = tx.Exec("CREATE TEMPORARY TABLE temp_table (id INT, name VARCHAR(50))")
	if err != nil {
		// Rollback the transaction in case of an error
		tx.Rollback()
		log.Fatal(err)
	}

	// Example 2: Setting a variable within the transaction
	_, err = tx.Exec("SET @example_var := 42")
	if err != nil {
		// Rollback the transaction in case of an error
		tx.Rollback()
		log.Fatal(err)
	}

	// Example 3: Changing connection options within the transaction
	_, err = tx.Exec("SET NAMES utf8mb4")
	if err != nil {
		// Rollback the transaction in case of an error
		tx.Rollback()
		log.Fatal(err)
	}

	// Commit the transaction if all statements were successful
	err = tx.Commit()
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println("Transaction completed successfully.")
}
```

##  Prepared Statements

At the database level, a prepared statement is bound to a single database connection. The typical flow is that the client sends a SQL statement with placeholders to the server for preparation, the server responds with a statement ID, and then the client executes the statement by sending its ID and parameters.

In Go, however, connections are not exposed directly to the user of the `database/sql` package. You don’t prepare a statement on a connection. You prepare it on a `DB` or a `Tx`. And `database/sql` has some convenience behaviors such as automatic retries. For these reasons, the underlying association between prepared statements and connections, which exists at the driver level, is hidden from your code.

how it works:

1. When you prepare a statement, it’s prepared on a connection in the pool.
2. The `Stmt` object remembers which connection was used.
3. When you execute the `Stmt`, it tries to use the connection. If it’s not available because it’s closed or busy doing something else, it gets another connection from the pool _and re-prepares the statement with the database on another connection.

Because statements will be re-prepared as needed when their original connection is busy, it’s possible for high-concurrency usage of the database, which may keep a lot of connections busy, to create a large number of prepared statements. This can result in apparent leaks of statements, statements being prepared and re-prepared more often than you think, and even running into server-side limits on the number of statements.

### Avoiding Prepared Statements

A simple `db.Query(sql, param1, param2)`, for example, works by preparing the sql, then executing it with the parameters and finally closing the statement.

If you don’t want to use a prepared statement, you need to use `fmt.Sprint()` or similar to assemble the SQL, and pass this as the only argument to `db.Query()` or `db.QueryRow()`. And your driver needs to support plaintext query execution, which is added in Go 1.1 via the `Execer` and `Queryer` interfaces,

###  Prepared Statements in Transactions

Prepared statements that are created in a `Tx` are bound exclusively to it, so the earlier cautions about repreparing do not apply. When you operate on a `Tx` object, your actions map directly to the one and only one connection underlying it.

This also means that **prepared statements created inside a `Tx` can’t be used separately from it. Likewise, prepared statements created on a `DB` can’t be used within a transaction, because they will be bound to a different connection.**

To use a prepared statement prepared outside the transaction in a `Tx`, you can use `Tx.Stmt()`, which will create a new transaction-specific statement from the one prepared outside the transaction. It does this by taking an existing prepared statement, setting the connection to that of the transaction and repreparing all statements every time they are executed.

**This behavior and its implementation are undesirable**

```go
tx, err := db.Begin()
if err != nil {
	log.Fatal(err)
}
defer tx.Rollback()
stmt, err := tx.Prepare("INSERT INTO foo VALUES (?)")
if err != nil {
	log.Fatal(err)
}
defer stmt.Close() // danger!
for i := 0; i < 10; i++ {
	_, err = stmt.Exec(i)
	if err != nil {
		log.Fatal(err)
	}
}
err = tx.Commit()
if err != nil {
	log.Fatal(err)
}
// stmt.Close() runs here!
```

###  Parameter Placeholder Syntax

The syntax for placeholder parameters in prepared statements is database-specific.

 ```
MySQL               PostgreSQL            Oracle
=====               ==========            ======
WHERE col = ?       WHERE col = $1        WHERE col = :col
VALUES(?, ?, ?)     VALUES($1, $2, $3)    VALUES(:val1, :val2, :val3)
```
##  Errors

Almost all operations with `database/sql` types return an error as the last value.  Always check these errors, never ignore them.
### Errors From Iterating Resultsets

```go
for rows.Next() {
	// ...
}
if err = rows.Err(); err != nil {
	// handle the error here
}
```

The error from `rows.Err()` could be the result of a variety of errors in the `rows.Next()` loop. The loop might exit for some reason other than finishing the loop normally, so you always need to check whether the loop terminated normally or not. An abnormal termination automatically calls `rows.Close()`, although it’s harmless to call it multiple times.

### Errors From Closing Resultsets

always explicitly close a `sql.Rows` if you exit the loop prematurely. It’s auto-closed if the loop exits normally or through an error, but  might mistakenly do this:

```go
for rows.Next() {
	// ...
	break; // whoops, rows is not closed! memory leak...
}
// do the usual "if err = rows.Err()" [omitted here]...
// it's always safe to [re?]close here:
if err = rows.Close(); err != nil {
	// but what should we do if there's an error?
	log.Println(err)
}
```

The error returned by `rows.Close()` is the only exception to the general rule that it’s best to capture and check for errors in all database operations.

###  Errors From QueryRow()

```go
var name string
err = db.QueryRow("select name from users where id = ?", 1).Scan(&name)
if err != nil {
	log.Fatal(err)
}
fmt.Println(name)
```

What if there was no user with `id = 1`? Then there would be no row in the result, and `.Scan()` would not scan a value into `name`. What happens then?

Go defines a special error constant, called `sql.ErrNoRows`, which is returned from `QueryRow()` when the result is empty. This needs to be handled as a special case in most circumstances.

Errors from the query are deferred until `Scan()` is called, and then are returned from that. The above code is better written like this instead:

```go
var name string
err = db.QueryRow("select name from users where id = ?", 1).Scan(&name)
if err != nil {
	if err == sql.ErrNoRows {
		// there were no rows, but otherwise no error occurred
	} else {
		log.Fatal(err)
	}
}
fmt.Println(name)
```

There’s nothing erroneous about an empty set. The reason is that the `QueryRow()` method needs to use this special-case in order to let the caller distinguish whether `QueryRow()` in fact found a row; without it, `Scan()` wouldn’t do anything


### Identifying Specific Database Errors

```go
rows, err := db.Query("SELECT someval FROM sometable")
// err contains:
// ERROR 1045 (28000): Access denied for user 'foo'@'::1' (using password: NO)
if strings.Contains(err.Error(), "Access denied") {
	// Handle the permission-denied error
}
```

This is not the best way to do it, though. For example, the string value might vary depending on what language the server uses to send error messages. It’s much better to compare error numbers to identify what a specific error is.

The mechanism to do this varies between drivers, however, because this isn’t part of `database/sql` itself.

```go
if driverErr, ok := err.(*mysql.MySQLError); ok { // Now the error number is accessible directly
	if driverErr.Number == 1045 {
		// Handle the permission-denied error
	}
}
```

The value of the number, however, is taken from MySQL’s error message, and is therefore database specific, not driver specific.

This code is still ugly. Comparing to 1045, a magic number, is a code smell. Some driversprovide a list of error identifiers. The Postgres `pq` driver does, for example, in [error.go](https://github.com/lib/pq/blob/master/error.go).

```go
if driverErr, ok := err.(*mysql.MySQLError); ok {
	if driverErr.Number == mysqlerr.ER_ACCESS_DENIED_ERROR {
		// Handle the permission-denied error
	}
}
```


###  Handling Connection Errors

What if your connection to the database is dropped, killed, or has an error?

 don’t need to implement any logic to retry failed statements when this happens. As part of the [connection pooling](http://go-database-sql.org/connection-pool.html) in `database/sql`, handling failed connections is built-in.

If you execute a query or other statement and the underlying connection has a failure, Go will reopen a new connection (or just get another from the connection pool) and retry, up to 10 times.

There can be some unintended consequences, however. Some types of errors may be retried when other error conditions happen. This might also be driver-specific.
## NULLS

There are types for nullable booleans, strings, integers, and floats

```go
for rows.Next() {
	var s sql.NullString
	err := rows.Scan(&s)
	// check err
	if s.Valid {
	   // use s.String
	} else {
	   // NULL value
	}
}
```

Limitations of the nullable types, and reasons to avoid nullable columns in case you need more convincing:

1. There’s no `sql.NullUint64` or `sql.NullYourFavoriteType`. You’d need to define your own for this.
2. Nullability can be tricky, and not future-proof. If you think something won’t be null, but you’re wrong, your program will crash, perhaps rarely enough that you won’t catch errors before you ship them.
3. One of the nice things about Go is having a useful default zero-value for every variable. This isn’t the way nullable things work.

need to define your own types to handle NULLs, you can copy the design of `sql.NullString` to achieve that.

can’t avoid having NULL values in your database, there is another work around that most database systems support, namely `COALESCE()`

```go
rows, err := db.Query(`
	SELECT
		name,
		COALESCE(other_field, '') as otherField
	WHERE id = ?
`, 42)

for rows.Next() {
	err := rows.Scan(&name, &otherField)
	// ..
	// If `other_field` was NULL, `otherField` is now an empty string. This works with other data types as well.
}
```


##  Unknown Columns

The `Scan()` function requires you to pass exactly the right number of destination variables

If you don’t know how many columns the query will return, you can use `Columns()` to find a list of column names. You can examine the length of this list to see how many columns there are, and you can pass a slice into `Scan()` with the correct number of values.

```go
cols, err := rows.Columns()
if err != nil {
	// handle the error
} else {
	dest := []interface{}{ // Standard MySQL columns
		new(uint64), // id
		new(string), // host
		new(string), // user
		new(string), // db
		new(string), // command
		new(uint32), // time
		new(string), // state
		new(string), // info
	}
	if len(cols) == 11 {
		// Percona Server
	} else if len(cols) > 8 {
		// Handle this case
	}
	err = rows.Scan(dest...)
	// Work with the values in dest
}
```

don’t know the columns or their types, you should use `sql.RawBytes`.

```go
cols, err := rows.Columns() // Remember to check err afterwards
vals := make([]interface{}, len(cols))
for i, _ := range cols {
	vals[i] = new(sql.RawBytes)
}
for rows.Next() {
	err = rows.Scan(vals...)
	// Now you can check each element of vals for nil-ness,
	// and you can use type introspection and type assertions
	// to fetch the column into a typed variable.
}
```


##  The Connection Pool

- Connection pooling means that executing two consecutive statements on a single database might open two connections and execute them separately. It is fairly common for programmers to be confused as to why their code misbehaves. For example, `LOCK TABLES` followed by an `INSERT` can block because the `INSERT` is on a connection that does not hold the table lock.
- Connections are created when needed and there isn’t a free connection in the pool.
- By default, there’s no limit on the number of connections. If you try to do a lot of things at once, you can create an arbitrary number of connections. This can cause the database to return an error such as “too many connections.”
- In Go 1.1 or newer, you can use `db.SetMaxIdleConns(N)` to limit the number of _idle_ connections in the pool. This doesn’t limit the pool size, though.
- In Go 1.2.1 or newer, you can use `db.SetMaxOpenConns(N)` to limit the number of _total_ open connections to the database. Unfortunately, a [deadlock bug](https://groups.google.com/d/msg/golang-dev/jOTqHxI09ns/x79ajll-ab4J) ([fix](https://code.google.com/p/go/source/detail?r=8a7ac002f840)) prevents `db.SetMaxOpenConns(N)` from safely being used in 1.2.
- Connections are recycled rather fast. Setting a high number of idle connections with `db.SetMaxIdleConns(N)` can reduce this churn, and help keep connections around for reuse.
- Keeping a connection idle for a long time can cause problems (like in [this issue](https://github.com/go-sql-driver/mysql/issues/257) with MySQL on Microsoft Azure). Try `db.SetMaxIdleConns(0)` if you get connection timeouts because a connection is idle for too long.
- You can also specify the maximum amount of time a connection may be reused by setting `db.SetConnMaxLifetime(duration)` since reusing long lived connections may cause network issues. This closes the unused connections lazily i.e. closing expired connection may be deferred.

##  Surprises, Antipatterns and Limitations

###  Resource Exhaustion

- Opening and closing databases can cause exhaustion of resources.
- Failing to read all rows or use `rows.Close()` reserves connections from the pool.
- Using `Query()` for a statement that doesn’t return rows will reserve a connection from the pool.
- Failing to be aware of how [prepared statements](http://go-database-sql.org/prepared.html) work can lead to a lot of extra database activity.

###  Large uint64 Values

can’t pass big unsigned integers as parameters to statements if their high bit is set:

```go
_, err := db.Exec("INSERT INTO users(id) VALUES", math.MaxUint64) // Error
```

###  Connection State Mismatch

Some things can change connection state, and that can cause problems for two reasons:

1. Some connection state, such as whether you’re in a transaction, should be handled through the Go types instead.
2. You might be assuming that your queries run on a single connection when they don’t.

after you’ve changed the connection, it’ll return to the pool and potentially pollute the state for some other code. This is one of the reasons why you should never issue ``BEGIN`` or ``COMMIT`` statements as SQL commands directly, too.

###  Database-Specific Syntax

The `database/sql` API provides an abstraction of a row-oriented database, but specific databases and drivers can differ in behavior and/or syntax, such as [prepared statement placeholders](http://go-database-sql.org/prepared.html).

### Multiple Result Sets

The Go driver doesn’t support multiple result sets from a single query in any way, and there doesn’t seem to be any plan to do that, although there is [a feature request](https://github.com/golang/go/issues/5171) for supporting bulk operations such as bulk copy.

This means, among other things, that a stored procedure that returns multiple result sets will not work correctly.

###  Invoking Stored Procedures

Invoking stored procedures is driver-specific, but in the MySQL driver it can’t be done at present. It might seem that you’d be able to call a simple procedure that returns a single result set,

```go
err := db.QueryRow("CALL mydb.myprocedure").Scan(&result) // Error
```

In fact, this won’t work. You’ll get the following error: _Error 1312: PROCEDURE mydb.myprocedure can’t return a result set in the given context_. This is because MySQL expects the connection to be set into multi-statement mode, even for a single result, and the driver doesn’t currently do that

### Multiple Statement Support

The `database/sql` doesn’t explicitly have multiple statement support, which means that the behavior of this is backend dependent:

```go
_, err := db.Exec("DELETE FROM tbl1; DELETE FROM tbl2") // Error/unpredictable result
```

The server is allowed to interpret this however it wants, which can include returning an error, executing only the first statement, or executing both.

Similarly, there is no way to batch statements in a transaction. Each statement in a transaction must be executed serially, and the resources in the results, such as a Row or Rows, must be scanned or closed so the underlying connection is free for the next statement to use.

This differs from the usual behavior when you’re not working with a transaction. In that scenario, it is perfectly possible to execute a query, loop over the rows, and within the loop make a query to the database (which will happen on a new connection):

```go
rows, err := db.Query("select * from tbl1") // Uses connection 1
for rows.Next() {
	err = rows.Scan(&myvariable)
	// The following line will NOT use connection 1, which is already in-use
	db.Query("select * from tbl2 where id = ?", myvariable)
}
```

But transactions are bound to just one connection, so this isn’t possible with a transaction:

```go
tx, err := db.Begin()
rows, err := tx.Query("select * from tbl1") // Uses tx's connection
for rows.Next() {
	err = rows.Scan(&myvariable)
	// ERROR! tx's connection is already busy!
	tx.Query("select * from tbl2 where id = ?", myvariable)
}
```


---

# GO - ORM / GORM

### Entity Layer

```go
package entity

import (
	"gorm.io/gorm"
	"time"
)

type Flight struct {
	gorm.Model
	DepartureAirportID   int
	DestinationAirportID int
	DepartureTime        time.Time
	DestinationTime      time.Time
	Price                float64
}
```

```go
package entity

import "gorm.io/gorm"

type Airport struct {
	gorm.Model
	City               string
	DepartureFlights   []Flight `gorm:"foreignKey:DepartureAirportID"`
	DestinationFlights []Flight `gorm:"foreignKey:DestinationAirportID"`
}
```

### Repository Layer

```go
package repository

import (
	"SampleTimeServiceApp/app/data/repository/entity"
	_ "github.com/lib/pq"
	"gorm.io/gorm"
)

type AirPortRepository struct {
	db *gorm.DB
}

func NewAirPortRepository(db *gorm.DB) *AirPortRepository {
	return &AirPortRepository{db}
}

func (ar *AirPortRepository) Save(a *entity.Airport) {
	ar.db.Create(a)
}

func (ar *AirPortRepository) Count() int64 {
	var count int64

	ar.db.Count(&count)

	return count
}
```

```go
package repository

import (
	"SampleTimeServiceApp/app/data/repository/entity"
	_ "github.com/lib/pq"
	"gorm.io/gorm"
)

type FlightRepository struct {
	db *gorm.DB
}

func NewFlightRepository(db *gorm.DB) *FlightRepository {
	return &FlightRepository{db}
}

func (fr *FlightRepository) Save(f *entity.Flight) {
	fr.db.Create(f)
}
```

### Data Access Layer

```GO
package dal

import (
	"SampleTimeServiceApp/app/data/repository"
	"SampleTimeServiceApp/app/data/repository/entity"
	"gorm.io/driver/postgres"
	"gorm.io/gorm"
)

type FlightSearchHelper struct {
	ar *repository.AirPortRepository
	fr *repository.FlightRepository
}

func NewFlightSearchHelper() (*FlightSearchHelper, error) {
	const URL = "postgres://postgres:csystem1993@csd-postgresql-db.cmxkkfycsomh.us-east-1.rds.amazonaws.com:5432/gs23_flightsearchdb"
	db, err := gorm.Open(postgres.Open(URL), &gorm.Config{})
	if err != nil {
		return nil, err
	}

	err = db.AutoMigrate(&entity.Airport{})
	if err != nil {
		return nil, err
	}
	err = db.AutoMigrate(&entity.Flight{})

	if err != nil {
		return nil, err
	}

	return &FlightSearchHelper{repository.NewAirPortRepository(db), repository.NewFlightRepository(db)}, nil
}

func (h *FlightSearchHelper) CountAirPort() int64 {
	return h.ar.Count()
}

func (h *FlightSearchHelper) SaveAirPort(a *entity.Airport) {
	h.ar.Save(a)
}

func (h *FlightSearchHelper) SaveFlight(f *entity.Flight) {
	h.fr.Save(f)
}
```

### WEB NOTES

GORM, the Object Relational Mapping library for Go, streamlines the process of querying databases.

## Install

```shell
go get -u gorm.io/gorm  
go get -u gorm.io/driver/sqlite|
```

# Declaring Models

GORM simplifies database interactions by mapping Go structs to database tables.

Models are defined using normal structs. These structs can contain fields with basic Go types, pointers or aliases of these types, or even custom types, as long as they implement the [Scanner](https://pkg.go.dev/database/sql/?tab=doc#Scanner) and [Valuer](https://pkg.go.dev/database/sql/driver#Valuer) interfaces from the `database/sql` package

```go
type User struct {  
  ID           uint           // Standard field for the primary key  
  Name         string         // A regular string field  
  Email        *string        // A pointer to a string, allowing for null values  
  Age          uint8          // An unsigned 8-bit integer  
  Birthday     *time.Time     // A pointer to time.Time, can be null  
  MemberNumber sql.NullString // Uses sql.NullString to handle nullable strings  
  ActivatedAt  sql.NullTime   // Uses sql.NullTime for nullable time fields  
  CreatedAt    time.Time      // Automatically managed by GORM for creation time  
  UpdatedAt    time.Time      // Automatically managed by GORM for update time  
}
```

In this model:

- Basic data types like `uint`, `string`, and `uint8` are used directly.
- Pointers to types like `*string` and `*time.Time` indicate nullable fields.
- `sql.NullString` and `sql.NullTime` from the `database/sql` package are used for nullable fields with more control.
- `CreatedAt` and `UpdatedAt` are special fields that GORM automatically populates with the current time when a record is created or updated.

### Conventions

1. **Primary Key**: GORM uses a field named `ID` as the default primary key for each model.
    
2. **Table Names**: By default, GORM converts struct names to `snake_case` and pluralizes them for table names. For instance, a `User` struct becomes `users` in the database.
    
3. **Column Names**: GORM automatically converts struct field names to `snake_case` for column names in the database.
    
4. **Timestamp Fields**: GORM uses fields named `CreatedAt` and `UpdatedAt` to automatically track the creation and update times of records.

### `gorm.Model`

GORM provides a predefined struct named `gorm.Model`, which includes commonly used fields:

```go
// gorm.Model definition  
type Model struct {  
  ID        uint           `gorm:"primaryKey"`  
  CreatedAt time.Time  
  UpdatedAt time.Time  
  DeletedAt gorm.DeletedAt `gorm:"index"`  
}
```

- **Embedding in Your Struct**: You can embed `gorm.Model` directly in your structs to include these fields automatically. This is useful for maintaining consistency across different models and leveraging GORM’s built-in conventions
- - **Fields Included**:
    
    - `ID`: A unique identifier for each record (primary key).
    - `CreatedAt`: Automatically set to the current time when a record is created.
    - `UpdatedAt`: Automatically updated to the current time whenever a record is updated.
    - `DeletedAt`: Used for soft deletes (marking records as deleted without actually removing them from the database).

## Advanced

### Field-Level Permission

Exported fields have all permissions when doing CRUD with GORM, and GORM allows you to change the field-level permission with tag, so you can make a field to be read-only, write-only, create-only, update-only or ignored

```go
type User struct {
  Name1 string `gorm:"<-:create"`               // allow read and create
  Name2 string `gorm:"<-:update"`               // allow read and update
  Name3 string `gorm:"<-"`                      // allow read and write (create and update)
  Name4 string `gorm:"<-:false"`                // allow read, disable write permission
  Name5 string `gorm:"->"`                      // readonly (disable write permission unless it configured)
  Name6 string `gorm:"->;<-:create"`            // allow read and create
  Name7 string `gorm:"->:false;<-:create"`      // createonly (disabled read from db)
  Name8 string `gorm:"-"`                       // ignore this field when write and read with struct
  Name9 string `gorm:"-:all"`                   // ignore this field when write, read and migrate with struct
  Name10 string `gorm:"-:migration"`            // ignore this field when migrate with struct
}
```


### Embedded Struct

For anonymous fields, GORM will include its fields into its parent struct, for example:

```go
type User struct {  
  gorm.Model  
  Name string  
}  
// equals  
type User struct {  
  ID        uint           `gorm:"primaryKey"`  
  CreatedAt time.Time  
  UpdatedAt time.Time  
  DeletedAt gorm.DeletedAt `gorm:"index"`  
  Name string  
}
```

For a normal struct field, you can embed it with the tag `embedded`

```go
type Author struct {  
  Name  string  
  Email string  
}  
  
type Blog struct {  
  ID      int  
  Author  Author `gorm:"embedded;embeddedPrefix:author_"`  
  Upvotes int32  
}  
// equals  
type Blog struct {  
  ID    int64  
  Name  string  
  Email string  
  Upvotes  int32  
}
```

### Fields Tags

Tags are optional to use when declaring models, GORM supports the following tags:  
Tags are case insensitive, however `camelCase` is preferred.

|Tag Name|Description|
|---|---|
|column|column db name|
|type|column data type, prefer to use compatible general type, e.g: bool, int, uint, float, string, time, bytes, which works for all databases, and can be used with other tags together, like `not null`, `size`, `autoIncrement`… specified database data type like `varbinary(8)` also supported, when using specified database data type, it needs to be a full database data type, for example: `MEDIUMINT UNSIGNED NOT NULL AUTO_INCREMENT`|
|serializer|specifies serializer for how to serialize and deserialize data into db, e.g: `serializer:json/gob/unixtime`|
|size|specifies column data size/length, e.g: `size:256`|
|primaryKey|specifies column as primary key|
|unique|specifies column as unique|
|default|specifies column default value|
|precision|specifies column precision|
|scale|specifies column scale|
|not null|specifies column as NOT NULL|
|autoIncrement|specifies column auto incrementable|
|autoIncrementIncrement|auto increment step, controls the interval between successive column values|
|embedded|embed the field|
|embeddedPrefix|column name prefix for embedded fields|
|autoCreateTime|track current time when creating, for `int` fields, it will track unix seconds, use value `nano`/`milli` to track unix nano/milli seconds, e.g: `autoCreateTime:nano`|
|autoUpdateTime|track current time when creating/updating, for `int` fields, it will track unix seconds, use value `nano`/`milli` to track unix nano/milli seconds, e.g: `autoUpdateTime:milli`|
|index|create index with options, use same name for multiple fields creates composite indexes, refer [Indexes](https://gorm.io/docs/indexes.html) for details|
|uniqueIndex|same as `index`, but create uniqued index|
|check|creates check constraint, eg: `check:age > 13`, refer [Constraints](https://gorm.io/docs/constraints.html)|
|<-|set field’s write permission, `<-:create` create-only field, `<-:update` update-only field, `<-:false` no write permission, `<-` create and update permission|
|->|set field’s read permission, `->:false` no read permission|
|-|ignore this field, `-` no read/write permission, `-:migration` no migrate permission, `-:all` no read/write/migrate permission|
|comment|add comment for field when migration|

# Connecting to a Database

GORM officially supports the databases MySQL, PostgreSQL, SQLite, SQL Server

## MySQL

```go
import (  
  "gorm.io/driver/mysql"  
  "gorm.io/gorm"  
)  
  
func main() {  
  // refer https://github.com/go-sql-driver/mysql#dsn-data-source-name for details  
  dsn := "user:pass@tcp(127.0.0.1:3306)/dbname?charset=utf8mb4&parseTime=True&loc=Local"  
  db, err := gorm.Open(mysql.Open(dsn), &gorm.Config{})  
}
```

### Customize Driver

GORM allows to customize the MySQL driver with the `DriverName` option

```go
import (  
  _ "example.com/my_mysql_driver"  
  "gorm.io/driver/mysql"  
  "gorm.io/gorm"  
)  
  
db, err := gorm.Open(mysql.New(mysql.Config{  
  DriverName: "my_mysql_driver",  
  DSN: "gorm:gorm@tcp(localhost:9910)/gorm?charset=utf8&parseTime=True&loc=Local", // data source name, refer https://github.com/go-sql-driver/mysql#dsn-data-source-name  
}), &gorm.Config{})
```

### Existing database connection

GORM allows to initialize `*gorm.DB` with an existing database connection

```go
import (  
  "database/sql"  
  "gorm.io/driver/mysql"  
  "gorm.io/gorm"  
)  
  
sqlDB, err := sql.Open("mysql", "mydb_dsn")  
gormDB, err := gorm.Open(mysql.New(mysql.Config{  
  Conn: sqlDB,  
}), &gorm.Config{})
```

## PostgreSQL

```go
import (  
  "gorm.io/driver/postgres"  
  "gorm.io/gorm"  
)  
  
dsn := "host=localhost user=gorm password=gorm dbname=gorm port=9920 sslmode=disable TimeZone=Asia/Shanghai"  
db, err := gorm.Open(postgres.Open(dsn), &gorm.Config{})
```

### Customize Driver

GORM allows to customize the PostgreSQL driver with the `DriverName` option

```go
import (  
  _ "github.com/GoogleCloudPlatform/cloudsql-proxy/proxy/dialers/postgres"  
  "gorm.io/gorm"  
)  
  
db, err := gorm.Open(postgres.New(postgres.Config{  
  DriverName: "cloudsqlpostgres",  
  DSN: "host=project:region:instance user=postgres dbname=postgres password=password sslmode=disable",  
})
```

### Existing database connection

GORM allows to initialize `*gorm.DB` with an existing database connection

```go
import (  
  "database/sql"  
  "gorm.io/driver/postgres"  
  "gorm.io/gorm"  
)  
  
sqlDB, err := sql.Open("pgx", "mydb_dsn")  
gormDB, err := gorm.Open(postgres.New(postgres.Config{  
  Conn: sqlDB,  
}), &gorm.Config{})
```


# CRUD INTERFACE

# Create
## Create Record

```go
user := User{Name: "Jinzhu", Age: 18, Birthday: time.Now()}  
  
result := db.Create(&user) // pass pointer of data to Create  
  
user.ID             // returns inserted data's primary key  
result.Error        // returns error  
result.RowsAffected // returns inserted records count
```

can also create multiple records with `Create()`:

```go
users := []*User{  
  User{Name: "Jinzhu", Age: 18, Birthday: time.Now()},  
  User{Name: "Jackson", Age: 19, Birthday: time.Now()},  
}  
  
result := db.Create(users) // pass a slice to insert multiple row  
  
result.Error        // returns error  
result.RowsAffected // returns inserted records count
```

> **NOTE** You cannot pass a struct to ‘create’, so you should pass a pointer to the data.

## Create Record With Selected Fields

Create a record and assign a value to the fields specified.

```go
db.Select("Name", "Age", "CreatedAt").Create(&user)  
// INSERT INTO `users` (`name`,`age`,`created_at`) VALUES ("jinzhu", 18, "2020-07-04 11:05:21.775")
```

Create a record and ignore the values for fields passed to omit.

```go
db.Omit("Name", "Age", "CreatedAt").Create(&user)  
// INSERT INTO `users` (`birthday`,`updated_at`) VALUES ("2020-01-01 00:00:00.000", "2020-07-04 11:05:21.775")
```

## Batch Insert

To efficiently insert large number of records, pass a slice to the `Create` method. GORM will generate a single SQL statement to insert all the data and backfill primary key values, hook methods will be invoked too. It will begin a **transaction** when records can be split into multiple batches.

```go
var users = []User{{Name: "jinzhu1"}, {Name: "jinzhu2"}, {Name: "jinzhu3"}}  
db.Create(&users)  
  
for _, user := range users {  
  user.ID // 1,2,3  
}
```

You can specify batch size when creating with `CreateInBatches`

```go
var users = []User{{Name: "jinzhu_1"}, ...., {Name: "jinzhu_10000"}}  
  
// batch size 100  
db.CreateInBatches(users, 100)
```

> **NOTE** initialize GORM with `CreateBatchSize` option, all `INSERT` will respect this option when creating record & associations

```go
db, err := gorm.Open(sqlite.Open("gorm.db"), &gorm.Config{  
  CreateBatchSize: 1000,  
})  
  
db := db.Session(&gorm.Session{CreateBatchSize: 1000})  
  
users = [5000]User{{Name: "jinzhu", Pets: []Pet{pet1, pet2, pet3}}...}  
  
db.Create(&users)  
// INSERT INTO users xxx (5 batches)  
// INSERT INTO pets xxx (15 batches)
```

## Create Hooks

GORM allows user defined hooks to be implemented for `BeforeSave`, `BeforeCreate`, `AfterSave`, `AfterCreate`. These hook method will be called when creating a record

```go
func (u *User) BeforeCreate(tx *gorm.DB) (err error) {  
  u.UUID = uuid.New()  
  
  if u.Role == "admin" {  
    return errors.New("invalid role")  
  }  
  return  
}
```

## Create From Map

GORM supports create from `map[string]interface{}` and `[]map[string]interface{}{}`

```go
db.Model(&User{}).Create(map[string]interface{}{  
  "Name": "jinzhu", "Age": 18,  
})  
  
// batch insert from `[]map[string]interface{}{}`  
db.Model(&User{}).Create([]map[string]interface{}{  
  {"Name": "jinzhu_1", "Age": 18},  
  {"Name": "jinzhu_2", "Age": 20},  
})
```

> **NOTE** When creating from map, hooks won’t be invoked, associations won’t be saved and primary key values won’t be back filled

## Create From SQL Expression/Context Valuer

GORM allows insert data with SQL expression, there are two ways to achieve this goal, create from `map[string]interface{}` or [Customized Data Types](https://gorm.io/docs/data_types.html#gorm_valuer_interface)

```go
// Create from map  
db.Model(User{}).Create(map[string]interface{}{  
  "Name": "jinzhu",  
  "Location": clause.Expr{SQL: "ST_PointFromText(?)", Vars: []interface{}{"POINT(100 100)"}},  
})  
// INSERT INTO `users` (`name`,`location`) VALUES ("jinzhu",ST_PointFromText("POINT(100 100)"));  
  
// Create from customized data type  
type Location struct {  
  X, Y int  
}  
  
// Scan implements the sql.Scanner interface  
func (loc *Location) Scan(v interface{}) error {  
  // Scan a value into struct from database driver  
}  
  
func (loc Location) GormDataType() string {  
  return "geometry"  
}  
  
func (loc Location) GormValue(ctx context.Context, db *gorm.DB) clause.Expr {  
  return clause.Expr{  
    SQL:  "ST_PointFromText(?)",  
    Vars: []interface{}{fmt.Sprintf("POINT(%d %d)", loc.X, loc.Y)},  
  }  
}  
  
type User struct {  
  Name     string  
  Location Location  
}  
  
db.Create(&User{  
  Name:     "jinzhu",  
  Location: Location{X: 100, Y: 100},  
})  
// INSERT INTO `users` (`name`,`location`) VALUES ("jinzhu",ST_PointFromText("POINT(100 100)"))
```

## Advanced

### Create With Associations

When creating some data with associations, if its associations value is not zero-value, those associations will be upserted, and its `Hooks` methods will be invoked.

```go
type CreditCard struct {  
  gorm.Model  
  Number   string  
  UserID   uint  
}  
  
type User struct {  
  gorm.Model  
  Name       string  
  CreditCard CreditCard  
}  
  
db.Create(&User{  
  Name: "jinzhu",  
  CreditCard: CreditCard{Number: "411111111111"}  
})  
// INSERT INTO `users` ...  
// INSERT INTO `credit_cards` ...
```

### Default Values

You can define default values for fields with tag `default`

```go
type User struct {  
  ID   int64  
  Name string `gorm:"default:galeone"`  
  Age  int64  `gorm:"default:18"`  
}
```

 Then the default value _will be used_ when inserting into the database for [zero-value](https://tour.golang.org/basics/12) fields
> **NOTE** Any zero value like `0`, `''`, `false` won’t be saved into the database for those fields defined default value, you might want to use pointer type or Scanner/Valuer to avoid this, for example:

```go
type User struct {  
  gorm.Model  
  Name string  
  Age  *int           `gorm:"default:18"`  
  Active sql.NullBool `gorm:"default:true"`  
}
```

# Query

## Retrieving a single object

GORM provides `First`, `Take`, `Last` methods to retrieve a single object from the database, it adds `LIMIT 1` condition when querying the database, and it will return the error `ErrRecordNotFound` if no record is found.

```go
// Get the first record ordered by primary key  
db.First(&user)  
// SELECT * FROM users ORDER BY id LIMIT 1;  
  
// Get one record, no specified order  
db.Take(&user)  
// SELECT * FROM users LIMIT 1;  
  
// Get last record, ordered by primary key desc  
db.Last(&user)  
// SELECT * FROM users ORDER BY id DESC LIMIT 1;  
  
result := db.First(&user)  
result.RowsAffected // returns count of records found  
result.Error        // returns error or nil  
  
// check error ErrRecordNotFound  
errors.Is(result.Error, gorm.ErrRecordNotFound)
```

> If you want to avoid the `ErrRecordNotFound` error, you could use `Find` like `db.Limit(1).Find(&user)`, the `Find` method accepts both struct and slice data

> Using `Find` without a limit for single object `db.Find(&user)` will query the full table and return only the first object which is not performant and nondeterministic

The `First` and `Last` methods will find the first and last record (respectively) as ordered by primary key. They only work when a pointer to the destination struct is passed to the methods as argument or when the model is specified using `db.Model()`. Additionally, if no primary key is defined for relevant model, then the model will be ordered by the first field.

```go
var user User  
var users []User  
  
// works because destination struct is passed in  
db.First(&user)  
// SELECT * FROM `users` ORDER BY `users`.`id` LIMIT 1  
  
// works because model is specified using `db.Model()`  
result := map[string]interface{}{}  
db.Model(&User{}).First(&result)  
// SELECT * FROM `users` ORDER BY `users`.`id` LIMIT 1  
  
// doesn't work  
result := map[string]interface{}{}  
db.Table("users").First(&result)  
  
// works with Take  
result := map[string]interface{}{}  
db.Table("users").Take(&result)  
  
// no primary key defined, results will be ordered by first field (i.e., `Code`)  
type Language struct {  
  Code string  
  Name string  
}  
db.First(&Language{})  
// SELECT * FROM `languages` ORDER BY `languages`.`code` LIMIT 1
```

### Retrieving objects with primary key

Objects can be retrieved using primary key by using [Inline Conditions](https://gorm.io/docs/query.html#inline_conditions) if the primary key is a number. When working with strings, extra care needs to be taken to avoid SQL Injection

```go
db.First(&user, 10)  
// SELECT * FROM users WHERE id = 10;  
  
db.First(&user, "10")  
// SELECT * FROM users WHERE id = 10;  
  
db.Find(&users, []int{1,2,3})  
// SELECT * FROM users WHERE id IN (1,2,3);
```


If the primary key is a string (for example, like a uuid), the query will be written as follows:

```go
db.First(&user, "id = ?", "1b74413f-f3b8-409f-ac47-e8c062e3472a")  
// SELECT * FROM users WHERE id = "1b74413f-f3b8-409f-ac47-e8c062e3472a";
```

## Retrieving all objects

```go
// Get all records  
result := db.Find(&users)  
// SELECT * FROM users;  
  
result.RowsAffected // returns found records count, equals `len(users)`  
result.Error        // returns error
```

## Conditions

### String Conditions

```go
// Get first matched record  
db.Where("name = ?", "jinzhu").First(&user)  
// SELECT * FROM users WHERE name = 'jinzhu' ORDER BY id LIMIT 1;  
  
// Get all matched records  
db.Where("name <> ?", "jinzhu").Find(&users)  
// SELECT * FROM users WHERE name <> 'jinzhu';  
  
// IN  
db.Where("name IN ?", []string{"jinzhu", "jinzhu 2"}).Find(&users)  
// SELECT * FROM users WHERE name IN ('jinzhu','jinzhu 2');  
  
// LIKE  
db.Where("name LIKE ?", "%jin%").Find(&users)  
// SELECT * FROM users WHERE name LIKE '%jin%';  
  
// AND  
db.Where("name = ? AND age >= ?", "jinzhu", "22").Find(&users)  
// SELECT * FROM users WHERE name = 'jinzhu' AND age >= 22;  
  
// Time  
db.Where("updated_at > ?", lastWeek).Find(&users)  
// SELECT * FROM users WHERE updated_at > '2000-01-01 00:00:00';  
  
// BETWEEN  
db.Where("created_at BETWEEN ? AND ?", lastWeek, today).Find(&users)  
// SELECT * FROM users WHERE created_at BETWEEN '2000-01-01 00:00:00' AND '2000-01-08 00:00:00';
```

### Struct & Map Conditions

```go
// Struct  
db.Where(&User{Name: "jinzhu", Age: 20}).First(&user)  
// SELECT * FROM users WHERE name = "jinzhu" AND age = 20 ORDER BY id LIMIT 1;  
  
// Map  
db.Where(map[string]interface{}{"name": "jinzhu", "age": 20}).Find(&users)  
// SELECT * FROM users WHERE name = "jinzhu" AND age = 20;  
  
// Slice of primary keys  
db.Where([]int64{20, 21, 22}).Find(&users)  
// SELECT * FROM users WHERE id IN (20, 21, 22);
```


> **NOTE** When querying with struct, GORM will only query with non-zero fields, that means if your field’s value is `0`, `''`, `false` or other [zero values](https://tour.golang.org/basics/12), it won’t be used to build query conditions

### Specify Struct search fields

When searching with struct, you can specify which particular values from the struct to use in the query conditions by passing in the relevant field name or the dbname to `Where()`

```go
db.Where(&User{Name: "jinzhu"}, "name", "Age").Find(&users)  
// SELECT * FROM users WHERE name = "jinzhu" AND age = 0;  
  
db.Where(&User{Name: "jinzhu"}, "Age").Find(&users)  
// SELECT * FROM users WHERE age = 0;
```

### Inline Condition

Query conditions can be inlined into methods like `First` and `Find` in a similar way to `Where`.

```go
// Get by primary key if it were a non-integer type  
db.First(&user, "id = ?", "string_primary_key")  
// SELECT * FROM users WHERE id = 'string_primary_key';  
  
// Plain SQL  
db.Find(&user, "name = ?", "jinzhu")  
// SELECT * FROM users WHERE name = "jinzhu";  
  
db.Find(&users, "name <> ? AND age > ?", "jinzhu", 20)  
// SELECT * FROM users WHERE name <> "jinzhu" AND age > 20;  
  
// Struct  
db.Find(&users, User{Age: 20})  
// SELECT * FROM users WHERE age = 20;  
  
// Map  
db.Find(&users, map[string]interface{}{"age": 20})  
// SELECT * FROM users WHERE age = 20;
```
### Not Conditions

```go
db.Not("name = ?", "jinzhu").First(&user)  
// SELECT * FROM users WHERE NOT name = "jinzhu" ORDER BY id LIMIT 1;  
  
// Not In  
db.Not(map[string]interface{}{"name": []string{"jinzhu", "jinzhu 2"}}).Find(&users)  
// SELECT * FROM users WHERE name NOT IN ("jinzhu", "jinzhu 2");  
  
// Struct  
db.Not(User{Name: "jinzhu", Age: 18}).First(&user)  
// SELECT * FROM users WHERE name <> "jinzhu" AND age <> 18 ORDER BY id LIMIT 1;  
  
// Not In slice of primary keys  
db.Not([]int64{1,2,3}).First(&user)  
// SELECT * FROM users WHERE id NOT IN (1,2,3) ORDER BY id LIMIT 1;
```

### Or Conditions

```go
db.Where("role = ?", "admin").Or("role = ?", "super_admin").Find(&users)  
// SELECT * FROM users WHERE role = 'admin' OR role = 'super_admin';  
  
// Struct  
db.Where("name = 'jinzhu'").Or(User{Name: "jinzhu 2", Age: 18}).Find(&users)  
// SELECT * FROM users WHERE name = 'jinzhu' OR (name = 'jinzhu 2' AND age = 18);  
  
// Map  
db.Where("name = 'jinzhu'").Or(map[string]interface{}{"name": "jinzhu 2", "age": 18}).Find(&users)  
// SELECT * FROM users WHERE name = 'jinzhu' OR (name = 'jinzhu 2' AND age = 18);
```

## Selecting Specific Fields

`Select` allows you to specify the fields that you want to retrieve from database. Otherwise, GORM will select all fields by default.

```go
db.Select("name", "age").Find(&users)  
// SELECT name, age FROM users;  
  
db.Select([]string{"name", "age"}).Find(&users)  
// SELECT name, age FROM users;  
  
db.Table("users").Select("COALESCE(age,?)", 42).Rows()  
// SELECT COALESCE(age,'42') FROM users;
```

## Order

```go
db.Order("age desc, name").Find(&users)  
// SELECT * FROM users ORDER BY age desc, name;  
  
// Multiple orders  
db.Order("age desc").Order("name").Find(&users)  
// SELECT * FROM users ORDER BY age desc, name;  
  
db.Clauses(clause.OrderBy{  
  Expression: clause.Expr{SQL: "FIELD(id,?)", Vars: []interface{}{[]int{1, 2, 3}}, WithoutParentheses: true},  
}).Find(&User{})  
// SELECT * FROM users ORDER BY FIELD(id,1,2,3)
```

## Limit & Offset

`Limit` specify the max number of records to retrieve  
`Offset` specify the number of records to skip before starting to return the records

```go
db.Limit(3).Find(&users)  
// SELECT * FROM users LIMIT 3;  
  
// Cancel limit condition with -1  
db.Limit(10).Find(&users1).Limit(-1).Find(&users2)  
// SELECT * FROM users LIMIT 10; (users1)  
// SELECT * FROM users; (users2)  
  
db.Offset(3).Find(&users)  
// SELECT * FROM users OFFSET 3;  
  
db.Limit(10).Offset(5).Find(&users)  
// SELECT * FROM users OFFSET 5 LIMIT 10;  
  
// Cancel offset condition with -1  
db.Offset(10).Find(&users1).Offset(-1).Find(&users2)  
// SELECT * FROM users OFFSET 10; (users1)  
// SELECT * FROM users; (users2)
```

## Group By & Having

```go
type result struct {  
Date time.Time  
Total int  
}  
  
db.Model(&User{}).Select("name, sum(age) as total").Where("name LIKE ?", "group%").Group("name").First(&result)  
// SELECT name, sum(age) as total FROM `users` WHERE name LIKE "group%" GROUP BY `name` LIMIT 1  
  
  
db.Model(&User{}).Select("name, sum(age) as total").Group("name").Having("name = ?", "group").Find(&result)  
// SELECT name, sum(age) as total FROM `users` GROUP BY `name` HAVING name = "group"  
  
rows, err := db.Table("orders").Select("date(created_at) as date, sum(amount) as total").Group("date(created_at)").Rows()  
defer rows.Close()  
for rows.Next() {  
...  
}  
  
rows, err := db.Table("orders").Select("date(created_at) as date, sum(amount) as total").Group("date(created_at)").Having("sum(amount) > ?", 100).Rows()  
defer rows.Close()  
for rows.Next() {  
...  
}  
  
type Result struct {  
Date time.Time  
Total int64  
}  
db.Table("orders").Select("date(created_at) as date, sum(amount) as total").Group("date(created_at)").Having("sum(amount) > ?", 100).Scan(&results)
```

## Distinct

```go
db.Distinct("name", "age").Order("name, age desc").Find(&results)
```

## Joins

```go
type result struct {  
  Name  string  
  Email string  
}  
  
db.Model(&User{}).Select("users.name, emails.email").Joins("left join emails on emails.user_id = users.id").Scan(&result{})  
// SELECT users.name, emails.email FROM `users` left join emails on emails.user_id = users.id  
  
rows, err := db.Table("users").Select("users.name, emails.email").Joins("left join emails on emails.user_id = users.id").Rows()  
for rows.Next() {  
  ...  
}  
  
db.Table("users").Select("users.name, emails.email").Joins("left join emails on emails.user_id = users.id").Scan(&results)  
  
// multiple joins with parameter  
db.Joins("JOIN emails ON emails.user_id = users.id AND emails.email = ?", "jinzhu@example.org").Joins("JOIN credit_cards ON credit_cards.user_id = users.id").Where("credit_cards.number = ?", "411111111111").Find(&user)
```


# Update
## Save All Fields

`Save` will save all fields when performing the Updating SQL

```go
db.First(&user)  
  
user.Name = "jinzhu 2"  
user.Age = 100  
db.Save(&user)  
// UPDATE users SET name='jinzhu 2', age=100, birthday='2016-01-01', updated_at = '2013-11-17 21:34:10' WHERE id=111;
```

`Save` is a combination function. If save value does not contain primary key, it will execute `Create`, otherwise it will execute `Update` (with all fields).

## Update single column

When updating a single column with `Update`, it needs to have any conditions or it will raise error `ErrMissingWhereClause`

When using the `Model` method and its value has a primary value, the primary key will be used to build the condition

```go
// Update with conditions  
db.Model(&User{}).Where("active = ?", true).Update("name", "hello")  
// UPDATE users SET name='hello', updated_at='2013-11-17 21:34:10' WHERE active=true;  
  
// User's ID is `111`:  
db.Model(&user).Update("name", "hello")  
// UPDATE users SET name='hello', updated_at='2013-11-17 21:34:10' WHERE id=111;  
  
// Update with conditions and model value  
db.Model(&user).Where("active = ?", true).Update("name", "hello")  
// UPDATE users SET name='hello', updated_at='2013-11-17 21:34:10' WHERE id=111 AND active=true;
```

## Updates multiple columns

`Updates` supports updating with `struct` or `map[string]interface{}`, when updating with `struct` it will only update non-zero fields by default


```go
// Update attributes with `struct`, will only update non-zero fields  
db.Model(&user).Updates(User{Name: "hello", Age: 18, Active: false})  
// UPDATE users SET name='hello', age=18, updated_at = '2013-11-17 21:34:10' WHERE id = 111;  
  
// Update attributes with `map`  
db.Model(&user).Updates(map[string]interface{}{"name": "hello", "age": 18, "active": false})  
// UPDATE users SET name='hello', age=18, active=false, updated_at='2013-11-17 21:34:10' WHERE id=111;
```

## Update Hooks

GORM allows the hooks `BeforeSave`, `BeforeUpdate`, `AfterSave`, `AfterUpdate`. Those methods will be called when updating a record

```go
func (u *User) BeforeUpdate(tx *gorm.DB) (err error) {  
  if u.Role == "admin" {  
    return errors.New("admin user not allowed to update")  
  }  
  return  
}
```

## Batch Updates

If we haven’t specified a record having a primary key value with `Model`, GORM will perform a batch update

```go
// Update with struct  
db.Model(User{}).Where("role = ?", "admin").Updates(User{Name: "hello", Age: 18})  
// UPDATE users SET name='hello', age=18 WHERE role = 'admin';  
  
// Update with map  
db.Table("users").Where("id IN ?", []int{10, 11}).Updates(map[string]interface{}{"name": "hello", "age": 18})  
// UPDATE users SET name='hello', age=18 WHERE id IN (10, 11);
```
## Delete a Record

When deleting a record, the deleted value needs to have primary key or it will trigger a [Batch Delete](https://gorm.io/docs/delete.html#batch_delete)

```go
// Email's ID is `10`  
db.Delete(&email)  
// DELETE from emails where id = 10;  
  
// Delete with additional conditions  
db.Where("name = ?", "jinzhu").Delete(&email)  
// DELETE from emails where id = 10 AND name = "jinzhu";
```

## Delete with primary key

GORM allows to delete objects using primary key(s) with inline condition

```go
db.Delete(&User{}, 10)  
// DELETE FROM users WHERE id = 10;  
  
db.Delete(&User{}, "10")  
// DELETE FROM users WHERE id = 10;  
  
db.Delete(&users, []int{1,2,3})  
// DELETE FROM users WHERE id IN (1,2,3);
```

## Delete Hooks

GORM allows hooks `BeforeDelete`, `AfterDelete`, those methods will be called when deleting a record

```go
func (u *User) BeforeDelete(tx *gorm.DB) (err error) {  
  if u.Role == "admin" {  
    return errors.New("admin user not allowed to delete")  
  }  
  return  
}
```

## Batch Delete

The specified value has no primary value, GORM will perform a batch delete, it will delete all matched records

```go
db.Where("email LIKE ?", "%jinzhu%").Delete(&Email{})  
// DELETE from emails where email LIKE "%jinzhu%";  
  
db.Delete(&Email{}, "email LIKE ?", "%jinzhu%")  
// DELETE from emails where email LIKE "%jinzhu%";
```

To efficiently delete large number of records, pass a slice with primary keys to the `Delete` method.

```go
var users = []User{{ID: 1}, {ID: 2}, {ID: 3}}  
db.Delete(&users)  
// DELETE FROM users WHERE id IN (1,2,3);  
  
db.Delete(&users, "name LIKE ?", "%jinzhu%")  
// DELETE FROM users WHERE name LIKE "%jinzhu%" AND id IN (1,2,3);
```

# **Associations**

## Belongs To

A `belongs to` association sets up a one-to-one connection with another model, such that each instance of the declaring model “belongs to” one instance of the other model.

For example, if your application includes users and companies, and each user can be assigned to exactly one company, the following types represent that relationship. Notice here that, on the `User` object, there is both a `CompanyID` as well as a `Company`. By default, the `CompanyID` is implicitly used to create a foreign key relationship between the `User` and `Company` tables, and thus must be included in the `User` struct in order to fill the `Company` inner struct.

```go
// `User` belongs to `Company`, `CompanyID` is the foreign key  
type User struct {  
  gorm.Model  
  Name      string  
  CompanyID int  
  Company   Company  
}  
  
type Company struct {  
  ID   int  
  Name string  
}
```

## Override Foreign Key

To define a belongs to relationship, the foreign key must exist, the default foreign key uses the owner’s type name plus its primary field name.

For the above example, to define the `User` model that belongs to `Company`, the foreign key should be `CompanyID` by convention

GORM provides a way to customize the foreign key

```go
type User struct {  
  gorm.Model  
  Name         string  
  CompanyRefer int  
  Company      Company `gorm:"foreignKey:CompanyRefer"`  
  // use CompanyRefer as foreign key  
}  
  
type Company struct {  
  ID   int  
  Name string  
}
```

For a belongs to relationship, GORM usually uses the owner’s primary field as the foreign key’s value. When you assign a user to a company, GORM will save the company’s `ID` into the user’s `CompanyID` field. You are able to change it with tag `references`

```go
type User struct {  
  gorm.Model  
  Name      string  
  CompanyID string  
  Company   Company `gorm:"references:Code"` // use Code as references  
}  
  
type Company struct {  
  ID   int  
  Code string  
  Name string  
}
```

**NOTE** GORM usually guess the relationship as `has one` if override foreign key name already exists in owner’s type, we need to specify `references` in the `belongs to` relationship.

```go
type User struct {  
  gorm.Model  
  Name      string  
  CompanyID string  
  Company   Company `gorm:"references:CompanyID"` // use Company.CompanyID as references  
}  
  
type Company struct {  
  CompanyID   int  
  Code        string  
  Name        string  
}
```

## CRUD with Belongs To

## Eager Loading

GORM allows eager loading belongs to associations with `Preload` or `Joins`

## FOREIGN KEY Constraints

You can setup `OnUpdate`, `OnDelete` constraints with tag `constraint`, it will be created when migrating with GORM

```go
type User struct {  
  gorm.Model  
  Name      string  
  CompanyID int  
  Company   Company `gorm:"constraint:OnUpdate:CASCADE,OnDelete:SET NULL;"`  
}  
  
type Company struct {  
  ID   int  
  Name string  
}
```

## Has One

A `has one` association sets up a one-to-one connection with another model, but with somewhat different semantics (and consequences). This association indicates that each instance of a model contains or possesses one instance of another model.

For example, if your application includes users and credit cards, and each user can only have one credit card.

```go
// User has one CreditCard, UserID is the foreign key  
type User struct {  
  gorm.Model  
  CreditCard CreditCard  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number string  
  UserID uint  
}
```

```go
// Retrieve user list with eager loading credit card  
func GetAll(db *gorm.DB) ([]User, error) {  
  var users []User  
  err := db.Model(&User{}).Preload("CreditCard").Find(&users).Error  
  return users, err  
}
```

## Override Foreign Key

For a `has one` relationship, a foreign key field must also exist, the owner will save the primary key of the model belongs to it into this field. 
The field’s name is usually generated with `has one` model’s type plus its `primary key`, for the above example it is `UserID`.
When you give a credit card to the user, it will save the User’s `ID` into its `UserID` field.
If you want to use another field to save the relationship, you can change it with tag `foreignKey`

```go
type User struct {  
  gorm.Model  
  CreditCard CreditCard `gorm:"foreignKey:UserName"`  
  // use UserName as foreign key  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number   string  
  UserName string  
}
```

## Override References

By default, the owned entity will save the `has one` model’s primary key into a foreign key, you could change to save another field’s value, like using `Name`

You are able to change it with tag `references`
```go
type User struct {  
  gorm.Model  
  Name       string     `gorm:"index"`  
  CreditCard CreditCard `gorm:"foreignKey:UserName;references:name"`  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number   string  
  UserName string  
}
```

## Polymorphism Association

GORM supports polymorphism association for `has one` and `has many`, it will save owned entity’s table name into polymorphic type’s field, primary key into the polymorphic field

```go
type Cat struct {  
ID int  
Name string  
Toy Toy `gorm:"polymorphic:Owner;"`  
}  
  
type Dog struct {  
ID int  
Name string  
Toy Toy `gorm:"polymorphic:Owner;"`  
}  
  
type Toy struct {  
ID int  
Name string  
OwnerID int  
OwnerType string  
}  
  
db.Create(&Dog{Name: "dog1", Toy: Toy{Name: "toy1"}})  
// INSERT INTO `dogs` (`name`) VALUES ("dog1")  
// INSERT INTO `toys` (`name`,`owner_id`,`owner_type`) VALUES ("toy1","1","dogs")
```

## CRUD with Has One

## Self-Referential Has One

```go
type User struct {  
  gorm.Model  
  Name      string  
  ManagerID *uint  
  Manager   *User  
}
```

## FOREIGN KEY Constraints

You can setup `OnUpdate`, `OnDelete` constraints with tag `constraint`, it will be created when migrating with GORM

```go
type User struct {  
  gorm.Model  
  CreditCard CreditCard `gorm:"constraint:OnUpdate:CASCADE,OnDelete:SET NULL;"`  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number string  
  UserID uint  
}
```

## Has Many

A `has many` association sets up a one-to-many connection with another model, unlike `has one`, the owner could have zero or many instances of models

For example, if your application includes users and credit card, and each user can have many credit cards.

```go
// User has many CreditCards, UserID is the foreign key  
type User struct {  
  gorm.Model  
  CreditCards []CreditCard  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number string  
  UserID uint  
}
```

```go
// Retrieve user list with eager loading credit cards  
func GetAll(db *gorm.DB) ([]User, error) {  
    var users []User  
    err := db.Model(&User{}).Preload("CreditCards").Find(&users).Error  
    return users, err  
}
```

## Override Foreign Key

To define a `has many` relationship, a foreign key must exist. The default foreign key’s name is the owner’s type name plus the name of its primary key field
For example, to define a model that belongs to `User`, the foreign key should be `UserID`.
To use another field as foreign key, you can customize it with a `foreignKey`

```go
type User struct {  
  gorm.Model  
  CreditCards []CreditCard `gorm:"foreignKey:UserRefer"`  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number    string  
  UserRefer uint  
}
```

## Override References

GORM usually uses the owner’s primary key as the foreign key’s value, for the above example, it is the `User`‘s `ID`,
When you assign credit cards to a user, GORM will save the user’s `ID` into credit cards’ `UserID` field.
You are able to change it with tag `references`

```go
type User struct {  
  gorm.Model  
  MemberNumber string  
  CreditCards  []CreditCard `gorm:"foreignKey:UserNumber;references:MemberNumber"`  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number     string  
  UserNumber string  
}
```

## Polymorphism Association

GORM supports polymorphism association for `has one` and `has many`, it will save owned entity’s table name into polymorphic type’s field, primary key value into the polymorphic field

```go
type Dog struct {  
ID int  
Name string  
Toys []Toy `gorm:"polymorphic:Owner;"`  
}  
  
type Toy struct {  
ID int  
Name string  
OwnerID int  
OwnerType string  
}  
  
db.Create(&Dog{Name: "dog1", Toys: []Toy{{Name: "toy1"}, {Name: "toy2"}}})  
// INSERT INTO `dogs` (`name`) VALUES ("dog1")  
// INSERT INTO `toys` (`name`,`owner_id`,`owner_type`) VALUES ("toy1","1","dogs"), ("toy2","1","dogs")
```

## CRUD with Has Many

## Self-Referential Has Many

```go
type User struct {  
  gorm.Model  
  Name      string  
  ManagerID *uint  
  Team      []User `gorm:"foreignkey:ManagerID"`  
}
```

## FOREIGN KEY Constraints

You can setup `OnUpdate`, `OnDelete` constraints with tag `constraint`, it will be created when migrating with GORM

```go
type User struct {  
  gorm.Model  
  CreditCards []CreditCard `gorm:"constraint:OnUpdate:CASCADE,OnDelete:SET NULL;"`  
}  
  
type CreditCard struct {  
  gorm.Model  
  Number string  
  UserID uint  
}
```

## Many To Many

Many to Many add a join table between two models.

For example, if your application includes users and languages, and a user can speak many languages, and many users can speak a specified language.

```go
// User has and belongs to many languages, `user_languages` is the join table  
type User struct {  
  gorm.Model  
  Languages []Language `gorm:"many2many:user_languages;"`  
}  
  
type Language struct {  
  gorm.Model  
  Name string  
}
```

When using GORM `AutoMigrate` to create a table for `User`, GORM will create the join table automatically

## Back-Reference

```go
// User has and belongs to many languages, use `user_languages` as join table  
type User struct {  
  gorm.Model  
  Languages []*Language `gorm:"many2many:user_languages;"`  
}  
  
type Language struct {  
  gorm.Model  
  Name string  
  Users []*User `gorm:"many2many:user_languages;"`  
}
```

```go
// Retrieve user list with eager loading languages  
func GetAllUsers(db *gorm.DB) ([]User, error) {  
  var users []User  
  err := db.Model(&User{}).Preload("Languages").Find(&users).Error  
  return users, err  
}  
  
// Retrieve language list with eager loading users  
func GetAllLanguages(db *gorm.DB) ([]Language, error) {  
  var languages []Language  
  err := db.Model(&Language{}).Preload("Users").Find(&languages).Error  
  return languages, err  
}
```

## Override Foreign Key

For a `many2many` relationship, the join table owns the foreign key which references two models

```go
type User struct {  
gorm.Model  
Languages []Language `gorm:"many2many:user_languages;"`  
}  
  
type Language struct {  
gorm.Model  
Name string  
}  
  
// Join Table: user_languages  
// foreign key: user_id, reference: users.id  
// foreign key: language_id, reference: languages.id
```

To override them, you can use tag `foreignKey`, `references`, `joinForeignKey`, `joinReferences`, not necessary to use them together, you can just use one of them to override some foreign keys/references

```go
type User struct {  
  gorm.Model  
  Profiles []Profile `gorm:"many2many:user_profiles;foreignKey:Refer;joinForeignKey:UserReferID;References:UserRefer;joinReferences:ProfileRefer"`  
  Refer    uint      `gorm:"index:,unique"`  
}  
  
type Profile struct {  
  gorm.Model  
  Name      string  
  UserRefer uint `gorm:"index:,unique"`  
}  
  
// Which creates join table: user_profiles  
//   foreign key: user_refer_id, reference: users.refer  
//   foreign key: profile_refer, reference: profiles.user_refer
```

> **NOTE:**  
>Some databases only allow create database foreign keys that reference on a field having unique index, so you need to specify the `unique index` tag if you are creating database foreign keys when migrating

## Self-Referential Many2Many

```go
type User struct {  
gorm.Model  
Friends []*User `gorm:"many2many:user_friends"`  
}  
  
// Which creates join table: user_friends  
// foreign key: user_id, reference: users.id  
// foreign key: friend_id, reference: users.id
```

## CRUD with Many2Many

## Customize JoinTable

`JoinTable` can be a full-featured model, like having `Soft Delete`，`Hooks` supports and more fields, you can set it up with `SetupJoinTable`

> **NOTE:**  
> Customized join table’s foreign keys required to be composited primary keys or composited unique index

```go
type Person struct {  
  ID        int  
  Name      string  
  Addresses []Address `gorm:"many2many:person_addresses;"`  
}  
  
type Address struct {  
  ID   uint  
  Name string  
}  
  
type PersonAddress struct {  
  PersonID  int `gorm:"primaryKey"`  
  AddressID int `gorm:"primaryKey"`  
  CreatedAt time.Time  
  DeletedAt gorm.DeletedAt  
}  
  
func (PersonAddress) BeforeCreate(db *gorm.DB) error {  
  // ...  
}  
  
// Change model Person's field Addresses' join table to PersonAddress  
// PersonAddress must defined all required foreign keys or it will raise error  
err := db.SetupJoinTable(&Person{}, "Addresses", &PersonAddress{})
```

## FOREIGN KEY Constraints

You can setup `OnUpdate`, `OnDelete` constraints with tag `constraint`, it will be created when migrating with GORM

```go
type User struct {  
gorm.Model  
Languages []Language `gorm:"many2many:user_speaks;"`  
}  
  
type Language struct {  
Code string `gorm:"primarykey"`  
Name string  
}  
  
// CREATE TABLE `user_speaks` (`user_id` integer,`language_code` text,PRIMARY KEY (`user_id`,`language_code`),CONSTRAINT `fk_user_speaks_user` FOREIGN KEY (`user_id`) REFERENCES `users`(`id`) ON DELETE SET NULL ON UPDATE CASCADE,CONSTRAINT `fk_user_speaks_language` FOREIGN KEY (`language_code`) REFERENCES `languages`(`code`) ON DELETE SET NULL ON UPDATE CASCADE);
```

## Composite Foreign Keys

If you are using [Composite Primary Keys](https://gorm.io/docs/composite_primary_key.html) for your models, GORM will enable composite foreign keys by default

You are allowed to override the default foreign keys, to specify multiple foreign keys, just separate those keys’ name by commas

```go
type Tag struct {  
  ID     uint   `gorm:"primaryKey"`  
  Locale string `gorm:"primaryKey"`  
  Value  string  
}  
  
type Blog struct {  
  ID         uint   `gorm:"primaryKey"`  
  Locale     string `gorm:"primaryKey"`  
  Subject    string  
  Body       string  
  Tags       []Tag `gorm:"many2many:blog_tags;"`  
  LocaleTags []Tag `gorm:"many2many:locale_blog_tags;ForeignKey:id,locale;References:id"`  
  SharedTags []Tag `gorm:"many2many:shared_blog_tags;ForeignKey:id;References:id"`  
}  
  
// Join Table: blog_tags  
//   foreign key: blog_id, reference: blogs.id  
//   foreign key: blog_locale, reference: blogs.locale  
//   foreign key: tag_id, reference: tags.id  
//   foreign key: tag_locale, reference: tags.locale  
  
// Join Table: locale_blog_tags  
//   foreign key: blog_id, reference: blogs.id  
//   foreign key: blog_locale, reference: blogs.locale  
//   foreign key: tag_id, reference: tags.id  
  
// Join Table: shared_blog_tags  
//   foreign key: blog_id, reference: blogs.id  
//   foreign key: tag_id, reference: tags.id
```

# Associations

## Auto Create/Update

GORM automates the saving of associations and their references when creating or updating records, using an upsert technique that primarily updates foreign key references for existing associations.

### Auto-Saving Associations on Create

When you create a new record, GORM will automatically save its associated data. This includes inserting data into related tables and managing foreign key references.

```go
user := User{  
  Name:            "jinzhu",  
  BillingAddress:  Address{Address1: "Billing Address - Address 1"},  
  ShippingAddress: Address{Address1: "Shipping Address - Address 1"},  
  Emails:          []Email{  
    {Email: "jinzhu@example.com"},  
    {Email: "jinzhu-2@example.com"},  
  },  
  Languages:       []Language{  
    {Name: "ZH"},  
    {Name: "EN"},  
  },  
}  
  
// Creating a user along with its associated addresses, emails, and languages  
db.Create(&user)  
// BEGIN TRANSACTION;  
// INSERT INTO "addresses" (address1) VALUES ("Billing Address - Address 1"), ("Shipping Address - Address 1") ON DUPLICATE KEY DO NOTHING;  
// INSERT INTO "users" (name,billing_address_id,shipping_address_id) VALUES ("jinzhu", 1, 2);  
// INSERT INTO "emails" (user_id,email) VALUES (111, "jinzhu@example.com"), (111, "jinzhu-2@example.com") ON DUPLICATE KEY DO NOTHING;  
// INSERT INTO "languages" ("name") VALUES ('ZH'), ('EN') ON DUPLICATE KEY DO NOTHING;  
// INSERT INTO "user_languages" ("user_id","language_id") VALUES (111, 1), (111, 2) ON DUPLICATE KEY DO NOTHING;  
// COMMIT;  
  
db.Save(&user)
```
### Updating Associations with `FullSaveAssociations`

For scenarios where a full update of the associated data is required (not just the foreign key references), the `FullSaveAssociations` mode should be used.

```go
// Update a user and fully update all its associations  
db.Session(&gorm.Session{FullSaveAssociations: true}).Updates(&user)  
// SQL: Fully updates addresses, users, emails tables, including existing associated records
```

Using `FullSaveAssociations` ensures that the entire state of the model, including all its associations, is reflected in the database, maintaining data integrity and consistency throughout the application.

## Skip Auto Create/Update

GORM provides flexibility to skip automatic saving of associations during create or update operations. This can be achieved using the `Select` or `Omit` methods, which allow you to specify exactly which fields or associations should be included or excluded in the operation.

Using `Select` to Include Specific Fields

The `Select` method lets you specify which fields of the model should be saved. This means that only the selected fields will be included in the SQL operation.

```go
user := User{  
  // User and associated data  
}  
  
// Only include the 'Name' field when creating the user  
db.Select("Name").Create(&user)  
// SQL: INSERT INTO "users" (name) VALUES ("jinzhu");
```

### Using `Omit` to Exclude Fields or Associations

Conversely, `Omit` allows you to exclude certain fields or associations when saving a model.

```go
// Skip creating the 'BillingAddress' when creating the user  
db.Omit("BillingAddress").Create(&user)  
  
// Skip all associations when creating the user  
db.Omit(clause.Associations).Create(&user)
```

Using `Select` and `Omit`, you can fine-tune how GORM handles the creation or updating of your models, giving you control over the auto-save behavior of associations.

Select/Omit Association fields

In GORM, when creating or updating records, you can use the `Select` and `Omit` methods to specifically include or exclude certain fields of an associated model.

With `Select`, you can specify which fields of an associated model should be included when saving the primary model. This is particularly useful for selectively saving parts of an association.

Conversely, `Omit` lets you exclude certain fields of an associated model from being saved. This can be useful when you want to prevent specific parts of an association from being persisted.

```go
user := User{  
  Name:            "jinzhu",  
  BillingAddress:  Address{Address1: "Billing Address - Address 1", Address2: "addr2"},  
  ShippingAddress: Address{Address1: "Shipping Address - Address 1", Address2: "addr2"},  
}  
  
// Create user and his BillingAddress, ShippingAddress, including only specified fields of BillingAddress  
db.Select("BillingAddress.Address1", "BillingAddress.Address2").Create(&user)  
// SQL: Creates user and BillingAddress with only 'Address1' and 'Address2' fields  
  
// Create user and his BillingAddress, ShippingAddress, excluding specific fields of BillingAddress  
db.Omit("BillingAddress.Address2", "BillingAddress.CreatedAt").Create(&user)  
// SQL: Creates user and BillingAddress, omitting 'Address2' and 'CreatedAt' fields
```

## Delete Associations

GORM allows for the deletion of specific associated relationships (has one, has many, many2many) using the `Select` method when deleting a primary record.

```go
// Delete a user's account when deleting the user  
db.Select("Account").Delete(&user)  
  
// Delete a user's Orders and CreditCards associations when deleting the user  
db.Select("Orders", "CreditCards").Delete(&user)  
  
// Delete all of a user's has one, has many, and many2many associations  
db.Select(clause.Associations).Delete(&user)  
  
// Delete each user's account when deleting multiple users  
db.Select("Account").Delete(&users)
```

> **NOTE:**  
>It’s important to note that associations will only be deleted if the primary key of the deleting record is not zero. GORM uses these primary keys as conditions to delete the selected associations.

## Association Mode

Association Mode in GORM offers various helper methods to handle relationships between models, providing an efficient way to manage associated data.

To start Association Mode, specify the source model and the relationship’s field name. The source model must contain a primary key, and the relationship’s field name should match an existing association.

```go
var user User  
db.Model(&user).Association("Languages")  
// Check for errors  
error := db.Model(&user).Association("Languages").Error
```

### Finding Associations

Retrieve associated records with or without additional conditions.

```go
// Simple find  
db.Model(&user).Association("Languages").Find(&languages)  
  
// Find with conditions  
codes := []string{"zh-CN", "en-US", "ja-JP"}  
db.Model(&user).Where("code IN ?", codes).Association("Languages").Find(&languages)
```

### Appending Associations

Add new associations for `many to many`, `has many`, or replace the current association for `has one`, `belongs to`.

```go
// Append new languages  
db.Model(&user).Association("Languages").Append([]Language{languageZH, languageEN})  
  
db.Model(&user).Association("Languages").Append(&Language{Name: "DE"})  
  
db.Model(&user).Association("CreditCard").Append(&CreditCard{Number: "411111111111"})
```

### Replacing Associations

Replace current associations with new ones.

```go
// Replace existing languages  
db.Model(&user).Association("Languages").Replace([]Language{languageZH, languageEN})  
  
db.Model(&user).Association("Languages").Replace(Language{Name: "DE"}, languageEN)
```

### Deleting Associations

Remove the relationship between the source and arguments, only deleting the reference.

```go
// Delete specific languages  
db.Model(&user).Association("Languages").Delete([]Language{languageZH, languageEN})  
  
db.Model(&user).Association("Languages").Delete(languageZH, languageEN)
```

### Clearing Associations

Remove all references between the source and association.

```go
// Clear all languages  
db.Model(&user).Association("Languages").Clear()
```

### Counting Associations

Get the count of current associations, with or without conditions.

```go
// Count all languages  
db.Model(&user).Association("Languages").Count()  
  
// Count with conditions  
codes := []string{"zh-CN", "en-US", "ja-JP"}  
db.Model(&user).Where("code IN ?", codes).Association("Languages").Count()
```

## Association Tags

Association tags in GORM are used to specify how associations between models are handled. These tags define the relationship’s details, such as foreign keys, references, and constraints. Understanding these tags is essential for setting up and managing relationships effectively.

|Tag|Description|
|---|---|
|`foreignKey`|Specifies the column name of the current model used as a foreign key in the join table.|
|`references`|Indicates the column name in the reference table that the foreign key of the join table maps to.|
|`polymorphic`|Defines the polymorphic type, typically the model name.|
|`polymorphicValue`|Sets the polymorphic value, usually the table name, if not specified otherwise.|
|`many2many`|Names the join table used in a many-to-many relationship.|
|`joinForeignKey`|Identifies the foreign key column in the join table that maps back to the current model’s table.|
|`joinReferences`|Points to the foreign key column in the join table that links to the reference model’s table.|
|`constraint`|Specifies relational constraints like `OnUpdate`, `OnDelete` for the association.|

---

# GO -  Dependency Injection

Dependency Injection (DI) is a software design pattern that promotes decoupling of components by passing dependencies, which are usually interfaces, to the components that need them. This pattern increases testability, maintainability, and scalability of your code.

In Golang, there are several ways to implement dependency injection, from simple manual dependency injection to more complex frameworks. When choosing a framework, it's important to consider factors such as ease of use, performance, and community support.

## The Basics of Dependency Injection in Golang

Creating structs and interfaces is an essential part of implementing dependency injection in Golang. Structs are used to define objects, while interfaces are used to define the behavior of those objects.

 it's important to consider the dependencies that each object will have and how those dependencies will be injected.

To implement dependency injection, you can use constructor injection, setter injection, or method injection. Constructor injection involves passing dependencies to a struct's constructor, while setter injection involves setting dependencies using setter methods. Method injection involves passing dependencies to methods as arguments.

Dependency injection frameworks in Golang can make implementing dependency injection easier and more efficient. There are several popular dependency injection frameworks available for Golang, such as Google's Wire, Facebook's Inject, and Uber's Dig.

it's important to remember that while frameworks can make implementing dependency injection easier, they are not a silver bullet. It's still important to follow best practices for dependency injection and struct/interface design to ensure that your code remains flexible and maintainable over time.

### Creating Structs and Interfaces

it's  important to avoid using global state or package-level variables. This can make it difficult to reason about the flow of data in your code and can lead to unexpected behavior. Instead, pass dependencies explicitly to functions or use constructor injection to initialize objects with their dependencies. This practice helps to isolate the behavior of your code and makes it easier to test individual components.

Using interfaces to define dependencies is another important practice. By defining dependencies using interfaces, you can swap out an implementation without having to modify all of the code that depends on it. This makes your code more flexible and easier to maintain over time.

Finally, to ensure that your code is functioning as expected, it's important to write tests for your code. By using dependency injection to provide mock objects for testing, you can more easily isolate different parts of your code and ensure that each component is working correctly.

#### Manual Dependency Injection - Example

`Repository` has a dependency on `DB`, which is used to retrieve data. The constructor for `Repository` takes a pointer to a `Database` instance, which is used to initialize the `db` field of the struct.

```go
// db.go 
type Database struct {
    Host string
    Port int
}

func (r *Database) Get(id string) (string, error) {
    // Implements DB interface
}

// repo.go
type DB interface {
    Get(id string) (string, error)
}

type Repository struct {
    db DB
}

func NewRepository(db DB) *Repository {
    return &Repository{db: db}
}

func (r *Repository) Get(id string) (string, error) {
    return r.db.Get(id)
}

```

To use `Repository`, you would first need to create an instance of `Database`, and then pass it to the constructor of `Repository`:

```go
db := &Database{Host: "localhost", Port: 5432}
repo := NewRepository(db)
```

Now `repo` is an instance of `Repository` with the `db` field set to `db`. This allows `Repository` to use `Database` via the interface `DB` to retrieve data as needed.

You can then call the `Get` method on `repo` to retrieve data:

```go
data, err := repo.Get("123")
```

`Get` uses `r.db` to retrieve data with the given id.

#### Manual Dependency Injection - Testing

By using a mock implementation of `DB`, we can isolate the behavior of `Repository` and test it without relying on the actual implementation of `DB`.


```go
// repo_test.go
type MockDB struct {
    GetFunc func(id string) (string, error)
}

func (m *MockDB) Get(id string) (string, error) {
    return m.GetFunc(id)
}

func TestRepository_Get(t *testing.T) {
    mockDB := &MockDB{
        GetFunc: func(id string) (string, error) {
            if id != "123" {
                return "", errors.New("Not found")
            }
            return "Data", nil
        },
    }

    repo := NewRepository(mockDB)
    data, err := repo.Get("123")
    if err != nil {
        t.Errorf("unexpected error: %v", err)
    }
    if data != "Data" {
        t.Errorf("expected data to be 'Data', got '%v'", data)
    }
}

```

create a mock implementation of `DB` called `MockDB`. This mock implementation has a `GetFunc` field, which is used to simulate the behavior of `Get` in  tests. 

then create an instance of `MockDB` with a `GetFunc` that returns `"Data"` when called with `"123"`. We use this mock implementation to create an instance of `Repository`, and then call `Get` on the repository with `"123"`. We check that the result is `"Data"`, as expected.

By using a mock implementation of `DB` in our tests, we can more easily isolate and test the behavior of `Repository`, without relying on the actual implementation of `DB`.


#### Summary of manual dependency injection

Some upsides of manual dependency injection include:

- It can be easier to reason about the flow of data in your code, as dependencies are passed explicitly to functions or constructors.
    
- It can be easier to manage dependencies, especially in smaller codebases.
    
- It can be easier to test code that relies on manual dependency injection, especially if dependencies are loosely coupled with each other.
    

On the other side, manual dependency injection also has downsides:

- It can be tedious and error-prone to manually instantiate and inject dependencies throughout your codebase.
    
- It can be difficult to manage complex dependencies, especially as your codebase grows.
    
- It can be difficult to test code that relies on manual dependency injection, especially if dependencies are tightly coupled with each other.

## Dependency Injection Frameworks in Golang

There are several popular dependency injection frameworks available for Golang, each with its own set of advantages and disadvantages

#### Google's Wire

Wire is a compile-time dependency injection framework developed by Google. It uses code generation to automatically generate wire functions for your code, which can then be used to generate and wire your dependencies. Wire is known for its ease of use and is a good choice for small-to-medium-sized projects.

#### Facebook's Inject

Inject is a runtime dependency injection framework developed by Facebook. It uses reflection to automatically generate and wire your dependencies at runtime. Inject is known for its performance and is a good choice for larger, more complex projects

#### Uber's Dig

Dig is a dependency injection framework developed by Uber. It uses reflection to automatically generate and wire your dependencies, similar to Inject. Dig is known for its flexibility and is a good choice for projects that require a high degree of customization.


### Choosing the Right Framework for Your Project

#### Ease of Use

The framework should be easy to use and integrate with your existing codebase. It should also have good documentation and a helpful community.

#### Performance

The framework should not introduce significant performance overhead or cause excessive memory usage.

#### Community Support

The framework should have an active community that can provide support and contributes to its development.

#### Future Proofing

The framework should be compatible with your existing codebase and should be able to adapt to future changes.

## Google Wire

### Basics

Wire has two core concepts: providers and injectors.

#### Defining Providers

The primary mechanism in Wire is the **provider**: a function that can produce a value. These functions are ordinary Go code.

```go
package foobarbaz

type Foo struct {
    X int
}

// ProvideFoo returns a Foo.
func ProvideFoo() Foo {
    return Foo{X: 42}
}
```

Provider functions must be exported in order to be used from other packages, just like ordinary functions.

Providers can specify dependencies with parameters:

```go
package foobarbaz

// ...

type Bar struct {
    X int
}

// ProvideBar returns a Bar: a negative Foo.
func ProvideBar(foo Foo) Bar {
    return Bar{X: -foo.X}
}
```

Providers can also return errors:
```go
package foobarbaz

import (
    "context"
    "errors"
)

// ...

type Baz struct {
    X int
}

// ProvideBaz returns a value if Bar is not zero.
func ProvideBaz(ctx context.Context, bar Bar) (Baz, error) {
    if bar.X == 0 {
        return Baz{}, errors.New("cannot provide baz when bar is zero")
    }
    return Baz{X: bar.X}, nil
}
```

Providers can be grouped into **provider sets**. This is useful if several providers will frequently be used together. To add these providers to a new set called `SuperSet`, use the `wire.NewSet` function:

```go
package foobarbaz

import (
    // ...
    "github.com/google/wire"
)

// ...

var SuperSet = wire.NewSet(ProvideFoo, ProvideBar, ProvideBaz)
```

 can also add other provider sets into a provider set.
```go
package foobarbaz

import (
    // ...
    "example.com/some/other/pkg"
)

// ...

var MegaSet = wire.NewSet(SuperSet, pkg.OtherSet)
```

#### Injectors

An application wires up these providers with an **injector**: a function that calls providers in dependency order. With Wire, you write the injector's signature, then Wire generates the function's body.

An injector is declared by writing a function declaration whose body is a call to `wire.Build`. The return values don't matter as long as they are of the correct type. The values themselves will be ignored in the generated code. Let's say that the above providers were defined in a package called `example.com/foobarbaz`. The following would declare an injector to obtain a `Baz`:

```go
// +build wireinject
// The build tag makes sure the stub is not built in the final build.

package main

import (
    "context"

    "github.com/google/wire"
    "example.com/foobarbaz"
)

func initializeBaz(ctx context.Context) (foobarbaz.Baz, error) {
    wire.Build(foobarbaz.MegaSet)
    return foobarbaz.Baz{}, nil
}
```

Like providers, injectors can be parameterized on inputs (which then get sent to providers) and can return errors. Arguments to `wire.Build` are the same as `wire.NewSet`: they form a provider set. This is the provider set that gets used during code generation for that injector.

### Advanced Features

The following features all build on top of the concepts of providers and injectors.

#### Binding Interfaces

Frequently, dependency injection is used to bind a concrete implementation for an interface. Wire matches inputs to outputs via [type identity](https://golang.org/ref/spec#Type_identity), so the inclination might be to create a provider that returns an interface type. However, this would not be idiomatic, since the Go best practice is to [return concrete types](https://github.com/golang/go/wiki/CodeReviewComments#interfaces). Instead, you can declare an interface binding in a provider set:

```go
type Fooer interface {
    Foo() string
}

type MyFooer string

func (b *MyFooer) Foo() string {
    return string(*b)
}

func provideMyFooer() *MyFooer {
    b := new(MyFooer)
    *b = "Hello, World!"
    return b
}

type Bar string

func provideBar(f Fooer) string {
    // f will be a *MyFooer.
    return f.Foo()
}

var Set = wire.NewSet(
    provideMyFooer,
    wire.Bind(new(Fooer), new(*MyFooer)),
    provideBar)
```

The first argument to `wire.Bind` is a pointer to a value of the desired interface type and the second argument is a pointer to a value of the type that implements the interface. Any set that includes an interface binding must also have a provider in the same set that provides the concrete type.

#### Struct Providers

Structs can be constructed using provided types. Use the `wire.Struct` function to construct a struct type and tell the injector which field(s) should be injected. The injector will fill in each field using the provider for the field's type. For the resulting struct type `S`, `wire.Struct` provides both `S` and `*S`.

```go
type Foo int
type Bar int

func ProvideFoo() Foo {/* ... */}

func ProvideBar() Bar {/* ... */}

type FooBar struct {
    MyFoo Foo
    MyBar Bar
}

var Set = wire.NewSet(
    ProvideFoo,
    ProvideBar,
    wire.Struct(new(FooBar), "MyFoo", "MyBar"))
```

A generated injector for `FooBar` would look like this:

```go
func injectFooBar() FooBar {
    foo := ProvideFoo()
    bar := ProvideBar()
    fooBar := FooBar{
        MyFoo: foo,
        MyBar: bar,
    }
    return fooBar
}
```

The first argument to `wire.Struct` is a pointer to the desired struct type and the subsequent arguments are the names of fields to be injected. A special string `"*"` can be used as a shortcut to tell the injector to inject all fields. So `wire.Struct(new(FooBar), "*")` produces the same result as above.

#### Binding Values

Occasionally, it is useful to bind a basic value (usually `nil`) to a type. Instead of having injectors depend on a throwaway provider function, you can add a value expression to a provider set.

```go
type Foo struct {
    X int
}

func injectFoo() Foo {
    wire.Build(wire.Value(Foo{X: 42}))
    return Foo{}
}
```

The generated injector would look like this:

```go
func injectFoo() Foo {
    foo := _wireFooValue
    return foo
}

var (
    _wireFooValue = Foo{X: 42}
)
```

It's important to note that the expression will be copied to the injector's package; references to variables will be evaluated during the injector package's initialization. Wire will emit an error if the expression calls any functions or receives from any channels.

For interface values, use `InterfaceValue`:

```go
func injectReader() io.Reader {
    wire.Build(wire.InterfaceValue(new(io.Reader), os.Stdin))
    return nil
}
```

#### Use Fields of a Struct as Providers

Sometimes the providers the user wants are some fields of a struct.

```go
type Foo struct {
    S string
    N int
    F float64
}

func getS(foo Foo) string {
    // Bad! Use wire.FieldsOf instead.
    return foo.S
}

func provideFoo() Foo {
    return Foo{ S: "Hello, World!", N: 1, F: 3.14 }
}

func injectedMessage() string {
    wire.Build(
        provideFoo,
        getS)
    return ""
}
```

You can instead use `wire.FieldsOf` to use those fields directly without writing `getS`:

```go
func injectedMessage() string {
    wire.Build(
        provideFoo,
        wire.FieldsOf(new(Foo), "S"))
    return ""
}
```

The generated injector would look like this:

```go
func injectedMessage() string {
    foo := provideFoo()
    string2 := foo.S
    return string2
}
```

You can add as many field names to a `wire.FieldsOf` function as you like. For a given field type `T`, `FieldsOf` provides at least `T`; if the struct argument is a pointer to a struct, then `FieldsOf` also provides `*T`

#### Cleanup functions

If a provider creates a value that needs to be cleaned up (e.g. closing a file), then it can return a closure to clean up the resource. The injector will use this to either return an aggregated cleanup function to the caller or to clean up the resource if a provider called later in the injector's implementation returns an error.

```go
func provideFile(log Logger, path Path) (*os.File, func(), error) {
    f, err := os.Open(string(path))
    if err != nil {
        return nil, nil, err
    }
    cleanup := func() {
        if err := f.Close(); err != nil {
            log.Log(err)
        }
    }
    return f, cleanup, nil
}
```

A cleanup function is guaranteed to be called before the cleanup function of any of the provider's inputs and must have the signature `func()`.

**EXAMPLE**

```go
// wire.go
func NewDatabase() *Database {
    return &Database{Host: "localhost", Port: 5432}
}

func NewRepository(db DB) *Repository {
    return &Repository{db: db}
}

func main() {
    db, err := InitializeNewDatabase()
    if err != nil {
        panic(err)
    }

    repo, err := InitializeNewRepository(db)
    if err != nil {
        panic(err)
    }

    // Use repo
}
```

To use Wire, we first need to define a `wire.go` file that specifies the dependencies for our code.

```go
// wire.go
// +build wireinject

package main

import "github.com/google/wire"

func InitializeNewDatabase() (*Database, error) {
    wire.Build(NewDatabase)
    return &Database{}, nil
}

func InitializeNewRepository(db DB) (*Repository, error) {
    wire.Build(NewRepository)
    return &Repository{}, nil
}
```

**CSD EXAMPLE**

```GO
package main

import (
	"fmt"
)

type NameType string

type SensorInfo struct {
	Name NameType
	//...
}

type SensorEvent struct {
	Sensor *SensorInfo
	//...
}

func NewName() NameType {
	return NameType("CSD Sensor") //Bu isim herhangi bir yerden elde edilebilir
}

func NewSensorInfo(name NameType) *SensorInfo {
	return &SensorInfo{Name: name}
}

func (si *SensorInfo) GetName() NameType {
	return si.Name
}

func NewSensorEvent(si *SensorInfo) *SensorEvent {
	return &SensorEvent{Sensor: si}
}

func (e *SensorEvent) PrintName() {
	fmt.Printf("Sensor Name:%s\n", e.Sensor.GetName())
}

func main() {
	e := InitSensorEvent()
	e.PrintName()
}
```

```go
package main

import (
	"github.com/google/wire"
)

func InitSensorEvent() SensorEvent {
	wire.Build(NewName, NewSensorInfo, NewSensorEvent)
	return SensorEvent{}
}
```

## Best Practices for Dependency Injection in Golang

### Avoiding Common Pitfalls

When using a dependency injection framework, it's important to remember that the framework should not affect the structure or behavior of our code. Instead, it should make it easier to manage dependencies and ensure that our code is testable and maintainable. Therefore, the tests we write for our code that uses dependency injection frameworks should still focus on testing the behavior of individual components, rather than the framework itself.
The tests should verify that each component behaves as expected, given its dependencies, and that the interactions between different components are correct.

#### Avoid Global State

A global state can make it difficult to reason about the flow of data in your code and can lead to unexpected behavior. Instead, pass dependencies explicitly to functions or use constructor injection to initialize objects with their dependencies. This practice helps to isolate the behavior of your code and makes it easier to test individual components.

#### Use Interfaces to Define Dependencies

By defining dependencies using interfaces, you can swap out an implementation without having to modify all of the code that depends on it. This makes your code more flexible and easier to maintain over time. When defining interfaces, it's important to keep them simple and focused. Interfaces should define the behavior of an object, rather than its implementation details.

#### Write Tests for Your Code

to ensure that your code is functioning as expected, it's important to write tests for your code. By using dependency injection to provide mock objects for testing, you can more easily isolate different parts of your code and ensure that each component is working correctly. When writing tests, it's important to focus on testing the behavior of individual components, rather than the implementation details. Tests should verify that each component behaves as expected, given its dependencies, and that the interactions between different components are correct.

---
# GO - WEB PROGRAMMING

### WEB NOTES

# `NET/HTTP` PACKAGE

The `net/http` package provides a rich set of features to build web applications and services. It includes an HTTP server, an HTTP client, methods to create custom HTTP servers, and methods to build RESTful APIs. Some of the key components of the `net/http` package are: 

- **Server:** A simple and efficient HTTP server that can serve static files or dynamic content.
- **Client:** An HTTP client that can send requests and receive responses from remote servers.
- **Handler:** An interface to implement custom request handling logic.
- **Request:** A structure that represents an HTTP request received by the server or sent by the client.
- **Response:** A structure that represents an HTTP response received by the client or sent by the server.

## Creating a Simple HTTP Server

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello, world!")
	})

	http.ListenAndServe(":8080", nil)
}
```

The `http.HandleFunc` function registers a function to be called whenever a request is received on the specified path ("/" in this case). The registered function takes a `ResponseWriter` and a `*Request` as arguments. The `ResponseWriter` is an interface that allows you to send an HTTP response to the client. The `*Request` is a pointer to the Request object representing the incoming HTTP request.

The `http.ListenAndServe` function starts an HTTP server that listens on the specified address and port. The second argument is the handler that will be used to process incoming requests.

## HTTP Handlers

In Go, an HTTP handler is any type that implements the `http.Handler` interface

```go
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```

Any custom type that has a method `ServeHTTP` with the required signature can be used as an HTTP handler.

```go
package main

import (
	"fmt"
	"net/http"
)

type MyHandler struct{}

func (h *MyHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello from MyHandler!")
}

func main() {
	handler := &MyHandler{}
	http.Handle("/", handler)
	http.ListenAndServe(":8080", nil)
}
```

## Working with HTTP Requests

The `net/http` package provides a `Request` structure that contains all the information about an incoming HTTP request. Some of the key fields and methods of the `Request` structure are:

- **Method:** The HTTP method (GET, POST, PUT, DELETE, etc.) of the request.
- **URL:** The URL of the request, represented as a `*url.URL` object.
- **Header:** The HTTP headers of the request, stored as a `http.Header` map.
- **Body:** The request body, if any, represented as an `io.ReadCloser`.
- **Form:** The parsed form data from the request body or URL query string, stored as a `url.Values` map.

```go
func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Method: %s\n", r.Method)
    fmt.Fprintf(w, "URL: %s\n", r.URL)
    fmt.Fprintf(w, "Header: %v\n", r.Header)
    fmt.Fprintf(w, "Content-Type: %s\n", r.Header.Get("Content-Type"))

    // Read and close the request body
    body, _ := ioutil.ReadAll(r.Body)
    r.Body.Close()
    fmt.Fprintf(w, "Body: %s\n", body)

    // Parse and access form data
    r.ParseForm()
    fmt.Fprintf(w, "Form: %v\n", r.Form)
    fmt.Fprintf(w, "Form value 'name': %s\n", r.Form.Get("name"))
}
```

## Working with HTTP Responses

Some of the key methods of the `ResponseWriter` interface are:

- **Header():** Returns the `http.Header` map representing the response headers.
- **WriteHeader(statusCode int):** Sets the status code of the response.
- **Write([]byte):** Writes the response body.

```go
func handler(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(http.StatusOK)

    response := map[string]interface{}{
        "status":  "success",
        "message": "Hello, world!",
    }
    json.NewEncoder(w).Encode(response)
}
```

## Customizing the HTTP Client

The `net/http` package provides a default HTTP client that can be used to send requests to remote servers. However, you might want to customize the client to set a custom timeout, use a custom transport, or configure other settings. To do this, you can create an instance of the `http.Client` type and set its fields accordingly.

```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

func main() {
	client := &http.Client{
		Timeout: 5 * time.Second,
	}

	resp, err := client.Get("https://example.com")
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	defer resp.Body.Close()

	fmt.Printf("Response status: %s\n", resp.Status)
}
```

## Best Practices

Here are some best practices to follow when working with the `net/http` package:

- Always close the request body after reading it to prevent resource leaks.
- Set a custom timeout for the HTTP client to avoid hanging indefinitely when the server doesn't respond.
- Use the `http.Error` function to send error responses with a custom status code and message.
- Handle panics in your HTTP handlers using a custom middleware or the `http.RecoverHandler` function.
- Use context values to pass request-specific data between handlers or middleware.

# `ENCODING/JSON` PACKAGE

There are two key terminologies to note when working with JSON in Go:

1. **Marshalling**: the act of converting a Go data structure into valid JSON.
2. **Unmarshalling**: the act of parsing a valid JSON string into a data structure in Go.

In other languages, marshalling is often referred to as “serializing”, while unmarshalling is referred to as “deserializing”.

## Unmarshalling JSON in Go

```go
func Unmarshal(data []byte, v any) error
```

This methods accepts two arguments: the first is a `[]byte` which represents the JSON object to unmarshal, and the second is `any` which should be a pointer to the target data structure for storing the result of unmarshalling the JSON data. 

```go
func main() {
    input := `{
        "name": "John Doe",
        "age": 15,
        "hobbies": ["climbing", "cycling", "running"]
    }`

    var target map[string]any

    err := json.Unmarshal([]byte(input), &target) 
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    for k, v := range target {
        fmt.Printf("k: %s, v: %v\n", k, v)
    }
}
```

The `map[string]any` data type in Go is a generic container that can hold values of any type In this case, the JSON keys will be unmarshalled into the `string` type, and their corresponding values will be unmarshalled into the `any` type of the `map[string]any`. A `nil` map is permissible here as `Unmarshal()` will allocate a new map in such cases.

The expected output

```text
k: name, v: John Doe
k: age, v: 15
k: hobbies, v: [climbing cycling running]
```

If an invalid JSON object is provided, an error will be returned by `Unmarshal()`. A common example of an invalid JSON object is one that has a [trailing comma](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Trailing_commas)

```go
input := `
  {
    name: "John Doe",
    "age": 15,
    "hobbies": ["climbing", "cycling", "running"],
  }
`
```

Attempting to unmarshal the JSON object above would yield the following error:

 Output

```text
2023/03/23 07:24:39 Unable to marshal JSON due to invalid character '}' looking for beginning of object key string
```

While `map[string]any` can be used to unmarshal JSON, it is not the most optimal solution for several reasons:

- You lose the type safety and compile-time checks that are provided by Go's static type system. This can make it harder to catch errors and maintain code over time.
    
- It can be slower than working with typed structs or custom types that implement the `json.Unmarshaler` interface. This is because accessing fields in a map requires a dynamic lookup, whereas accessing fields in a struct is done statically at compile-time.
    
- It can make it more difficult to reason about the structure of the JSON data being unmarshalled, as the values can be of any type. This can lead to more verbose and error-prone code.

In general, it's best to use typed structs or custom types whenever possible for JSON unmarshalling in Go. These types provide better type safety, performance, and maintainability than using `map[string]any`.

### Using structs for JSON unmarshalling

When using structs for unmsarshalling JSON objects, the field names in the object are mapped to the field names in the `struct` and the values are assigned accordingly.


```go
type Dog struct {
    Breed         string
    Name          string
    FavoriteTreat string
    Age           int
}

func main() {
    input := `{
        "Breed": "Golden Retriever",
        "Age": 8,
        "Name": "Paws",
        "FavoriteTreat": "Kibble"
    }`

    var dog Dog

    err := json.Unmarshal([]byte(input), &dog)
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    fmt.Printf(
        "%s is a %d years old %s who likes %s\n",
        dog.Name,
        dog.Age,
        dog.Breed,
        dog.FavoriteTreat,
    )
}
```

```text
Paws is a 8 years old Golden Retriever who likes Kibble
```

In this example, the `json.Unmarshal()` function takes the `input` data, along with a pointer to a `Dog` struct.

```json
{
  "name": "James Peterson",
  "age": 37,
  "address": {
    "line1": "Block 78 Woodgrove Avenue 5",
    "line2": "Unit #05-111",
    "postal": "654378"
  },
  "pets": [
    {
      "name": "Lex",
      "kind": "Dog",
      "age": 4,
      "color": "Gray"
    },
    {
      "name": "Faye",
      "kind": "Cat",
      "age": 6,
      "color": "Orange"
    }
  ]
}
```

must design your target struct to include other structs as fields and allow `Unmarshal()` to handle the mapping of fields accordingly.

```go
type (
    FullPerson struct {
        Address Address
        Name    string
        Pets    []Pet
        Age     int
    }

    Pet struct {
        Name  string
        Kind  string
        Color string
        Age   int
    }

    Address struct {
        Line1  string
        Line2  string
        Postal string
    }
)

func main() {
    b, err := os.ReadFile("assets/complex.json")
    if err != nil {
        log.Fatalf("Unable to read file due to %s\n", err)
    }

    var person FullPerson

    err = json.Unmarshal(b, &person)
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    litter.Dump(person)
}
```

the output: 
```json
main.FullPerson{
  Name: "James Peterson",
  Age: 37,
  Address: examples.Address{
    Line1: "Block 78 Woodgrove Avenue 5",
    Line2: "Unit #05-111",
    Postal: "654378",
  },
  Pets: []examples.Pet{
    examples.Pet{
      Name: "Lex",
      Kind: "Dog",
      Age: 4,
      Color: "Gray",
    },
    examples.Pet{
      Name: "Faye",
      Kind: "Cat",
      Age: 6,
      Color: "Orange",
    },
  },
}
```


## Common pitfalls with JSON unmarshalling in Go

### 1. Extra fields are omitted in the target struct

If the input JSON contains additional fields that are not a part of the target struct fields, they will be discarded when unmarshalled.

```go
func main() {
    input := `{
        "Breed": "Golden Retriever",
        "Age": 8,
        "Name": "Paws",
        "FavoriteTreat": "Kibble",
        "Dislikes": "Cats"
    }`


    var dog Dog

    err := json.Unmarshal([]byte(input), &dog)
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    litter.Dump(dog)
}
```

the input JSON contains the additional field `Dislikes` but that field is not included in the target `Dog` struct. Therefore, it is discarded:

 Output

```text
main.Dog{
  Breed: "Golden Retriever",
  Age: 8,
  Name: "Paws",
  FavoriteTreat: "Kibble",
}
```

### 2. Missing fields fallback to zero values

Missing fields in the input JSON will cause the zero value of the corresponding struct field to be used instead:

```go
func main() {
    input := `{
        "Breed": "Golden Retriever",
        "Age": 8,
        "Name": "Paws"
    }`

    var dog Dog

    err := json.Unmarshal([]byte(input), &dog)
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    fmt.Printf("%s likes %s\n", dog.Name, dog.FavoriteTreat)
}
```

 Output

```text
Paws likes
```

Since the `FavoriteTreat` field is been omitted from the input JSON, it will be an empty string in the resulting struct.

### 3. Unmarshalling is case insensitive

The `Unmarshal()` method will match the field name of the input JSON to the field in the `struct` in a case insensitive manner as long as the characters and their order are the same.

examples/case_sensitivity/main.go

```go
func main() {
    input := `{
        "BreED": "Golden Retriever",
        "age": 8,
        "NaME": "Paws",
        "favoriTeTrEat": "Kibble"
    }`
    var dog Dog

    err := json.Unmarshal([]byte(input), &dog)
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    fmt.Printf(
        "%s is a %d years old %s who likes %s\n",
        dog.Name,
        dog.Age,
        dog.Breed,
        dog.FavoriteTreat,
    )
}
```

 Output

```text
Paws is a 8 years old Golden Retriever who likes Kibble
```

Notice how the `Dog` struct was populated successfully despite the casing of the fields in the input JSON.

### 4. Field names must match JSON keys exactly

When defining structs for unmarshalling JSON, it's important to ensure that the names of struct fields match the keys in the JSON data exactly. If there is a mismatch, the field will not be populated with the corresponding value from the JSON data.


```go
func main() {
    input := `{
      "Breed": "Golden Retriever",
      "Age": 8,
      "Name": "Paws",
      "favorite_treat": "Kibble"
  }`

    var dog Dog

    err := json.Unmarshal([]byte(input), &dog)
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    fmt.Printf(
        "%s is a %d years old %s who likes %s\n",
        dog.Name,
        dog.Age,
        dog.Breed,
        dog.FavoriteTreat,
    )
}
```

 Output

```text
Paws is a 8 years old Golden Retriever who likes
```

As you can see, the input JSON uses the key `favorite_treat` but the `Dog` struct declares the field as `FavoriteTreat` so the unmarshalled `struct` does not use the input JSON’s value for `favorite_treat`.

### 5. Type aliases are preserved

If there are type alias fields in your struct, their values and type alias will be preserved when unmarshalled:

examples/type_alias.go

```go
type (
    TypeAliasExample string

    TypeAliasStruct struct {
        Example TypeAliasExample
    }
)

type (
    TypeAliasExample string

    TypeAliasStruct struct {
        Example TypeAliasExample
    }
)
```

 Output

```text
main.TypeAliasStruct{
  Example: "Hello world",
}
```

## JSON Marshalling in Go

The `json.Marshal()` method does the opposite of `Unmarshal()` by converting a given data structure into a JSON. When working with the basic types in Go (strings, integers, slices, maps), it generates the corresponding JSON accordingly.

examples/basic_marshal/main.go

```go
func marshal(in any) []byte {
    out, err := json.Marshal(in)
    if err != nil {
        log.Fatalf("Unable to marshal due to %s\n", err)
    }

    return out
}

func main() {
    first := marshal(14)
    second := marshal("Hello world")
    third := marshal([]float32{1.66, 6.86, 10.1})
    fourth := marshal(map[string]int{"num": 15, "other": 17})
    fmt.Printf(
        "first: %s\nsecond: %s\nthird: %s\nfourth: %s\n",
        first,
        second,
        third,
        fourth,
    )
}
```

 Output

```text
first: 14
second: "Hello world"
third: [1.66,6.86,10.1]
fourth: {"num":15,"other":17}
```

abstracted `Marshal()` into a separate function to simplify the error handling process.
### Marshalling structs

Similar to unmarshalling JSON into structs, you can also marshal a struct into JSON.


```go
func main() {
    p := Person{
        Name:  "John Jones",
        Age:   26,
        Email: "johnjones@email.com",
        Phone: "89910119",
        Hobbies: []string{
            "Swimming",
            "Badminton",
        },
    }

    b, err := json.Marshal(p)
    if err != nil {
        log.Fatalf("Unable to marshal due to %s\n", err)
    }

    fmt.Println(string(b))
}
```

 Output

```text
{"Name":"John Jones","Age":26,"Email":"johnjones@email.com","Phone":"89910119","Hobbies":["Swimming","Badminton"]}
```

The `Marshal()` method produces a valid JSON from the given struct, including any nested JSON arrays or JSON objects.

The generated JSON is a single line without proper formatting. Although this is an ideal form when transmitting information through a network, it is not a very user friendly representation of the JSON.

If you wish to format the JSON object, you can use the `MarshalIndent()` method which performs the same function as `Marshal()` but applies some indentation to format the output.

```go
b, err := json.MarshalIndent(p, "", "  ")
```


```json
{
    "Name": "John Jones",
    "Age": 26,
    "Email": "johnjones@email.com",
    "Phone": "89910119",
    "Hobbies": [
        "Swimming",
        "Badminton"
    ]
}
```

You can configure two aspects of formatting with `MarshalIndent()`. The first is the prefix per line which appears at the start of every line. For most purposes, you would set this parameter to be an empty string. The second configures the indentation level

## Customizing JSON field names with struct tags

In Go, struct tags are annotations that can be added to the fields of a struct to provide additional information about how the fields should be treated by various tools and libraries. Struct tags are strings that are added to the end of a field declaration, enclosed in backticks.

The most common use case for struct tags is to specify how a struct should be marshalled and unmarshalled to and from JSON. By adding tags to the fields of a struct, you can control how the fields are named, which fields are ignored, and how they are encoded and decoded.

```go
type Dog struct {
    Breed         string
    Name          string
    FavoriteTreat string
    Age           int
}

var dog = Dog{
  Breed: "Golden Retriever",
  Age: 8,
  Name: "Paws",
  FavoriteTreat: "Kibble",
}
```

At the moment, the `dog` variable will be marshalled into the following JSON object where the properties correspond exactly to the struct field names:

```json
{"Breed":"Golden Retriever","Name":"Paws","FavoriteTreat":"Kibble","Age":8}
```

You can customize this output by using `json` struct tags on the `Dog` type:

```go
type Dog struct {
    Breed         string `json:"breed"`
    Name          string `json:"name"`
    FavoriteTreat string `json:"favorite_treat"`
    Age           int    `json:"age"`
}
```

```json
{"breed":"Golden Retriever","name":"Paws","favorite_treat":"Kibble","age":8}
```

It also works the same way for unmarshalling.

### Other uses of struct tags

Beyond customizing the field names, struct tags can also be used to omit empty fields or to ignore fields altogether during marshalling and unmarshalling.

To omit an empty field (one with its zero value in Go), add the `omitempty` struct tag to the existing struct tag. To ignore a field whether it is empty or not, use `json:"-"`.

```go
type User struct {
    Username string   `json:"username"`
    Password string   `json:"-"`
    Email    string   `json:"email"`
    Hobbies  []string `json:"hobbies,omitempty"`
}

func main() {
    user := User{
        Username: "admin",
        Password: "root",
        Email:    "admin@email.com",
    }

    b, err := json.MarshalIndent(user, "", "  ")
    if err != nil {
        log.Fatalf("Unable to marshal due to %s\n", err)
    }

    fmt.Println(string(b))
}
```

The above code generates the following JSON:

 Output

```json
{
  "username": "admin",
  "email": "admin@email.com"
}
```

## Converting JSON to Go

```json
{
    "country": "string",
    "display_name": "string",
    "email": "string",
    "explicit_content": {
        "filter_enabled": true,
        "filter_locked": true
    },
    "external_urls": {
        "spotify": "string"
    },
    "followers": {
        "href": "string",
        "total": 0
    },
    "href": "string",
    "id": "string",
    "images": [
        {
            "url": "https://i.scdn.co/image/ab67616d00001e02ff9ca10b55ce82ae553c8228\n",
            "height": 300,
            "width": 300
        }
    ],
    "product": "string",
    "type": "string",
    "uri": "string"
}
```

To manually map the JSON schema to a struct in Go would be a time consuming process, but this task can be eased through tools that can perform this conversion such as [JSON-to-Go](https://mholt.github.io/json-to-go/) and [JSON Typedef](https://jsontypedef.com/docs/go-codegen/).

## Validating JSON data

There are two main forms of JSON validation. The first kind is involves validating that a given JSON string is proper (i.e. not malformed). The second kind checks if the input JSON conforms to a predefined schema.

First, let's use the `json.Valid()` method to check for malformed JSON in Go:

```go
func main() {
    good := `{"name": "John Doe"}`
    bad := `{name: "John Doe"}`

    fmt.Println(json.Valid([]byte(good)))
    fmt.Println(json.Valid([]byte(bad)))
}
```

The `bad` input JSON string does not wrap the `name` key in double quotes.

 Output

```text
true
false
```

its often necessary to enforce a particular schema for the input JSON. This can be achieved using third-party validation packages such as [go-playground/validator](https://github.com/go-playground/validator). It also relies on struct tags to perform data validation.

The `validator` package provides [several struct tags](https://pkg.go.dev/github.com/go-playground/validator/v10) that can be used to validate JSON input

To implement data validation on a struct, you must use the `validate` tags shown below:


```go
type User struct {
    Username string `json:"username" validate:"required"`
    Password string `json:"password" validate:"required"`
    Email    string `json:"email"    validate:"required,email"`
    Age      int    `json:"age"      validate:"required,min=18,max=99"`
}
```

Notice that the validation rules are provided as a set of comma-separated values with some properties having a value after an `=` symbol.

Given the following invalid JSON, we should expect the validation to flag out the invalid fields:

```json
{
  "username": "johndoe",
  "email": "johndoe@emai",
  "age": -14
}
```


```go
func main() {
    input := `{
    "username": "johndoe",
    "email": "johndoe@emai",
    "age": -14
  }`

    var user User

    err := json.Unmarshal([]byte(input), &user)
    if err != nil {
        log.Fatalf("Unable to marshal JSON due to %s", err)
    }

    fmt.Printf("User before validation: %v\n", user)

    err = validator.New().Struct(user)
    if err != nil {
        log.Fatalf("Validation failed due to %v\n", err)
    }
}
```

As expected, the validator returns an error that flags the erroneous fields in the input JSON after unmarshalling:

 Output

```text
User before validation: {johndoe  johndoe@emai -14}
Validation failed due to Key: 'ValidatedUser.Password' Error:Field validation for 'Password' failed on the 'required' tag
Key: 'ValidatedUser.Email' Error:Field validation for 'Email' failed on the 'email' tag
Key: 'ValidatedUser.Age' Error:Field validation for 'Age' failed on the 'min' tag
```

Note that the prior to using the `validator` package, the JSON was successfully unmarshalled since the validation struct tags are only evaluated when explicitly called.

By altering the input JSON to abide by the validation rules set out above, we can expect the validation to pass.

```json
{
  "username": "johndoe",
  "password": "root",
  "email": "johndoe@email.com",
  "age": 18
}
```

This time, with a valid JSON input, the validation passes:

 Output

```text
User before validation: {johndoe root johndoe@email.com 18}
User after validation: {johndoe root johndoe@email.com 18}
```


## Defining custom behavior for marshalling and unmarshalling data

In Go, you can define custom behavior for marshalling data by implementing the `json.Marshaler` interface. This interface defines a single method, `MarshalJSON()` which takes no arguments and returns a byte slice and an error.

```go
type (
    CustomTime struct {
        time.Time
    }

    Baby struct {
        BirthDate CustomTime `json:"birth_date"`
        Name      string    `json:"name"`
        Gender    string    `json:"gender"`
    }
)
```

```go
func main() {
    baby := Baby{
        Name:   "johnny",
        Gender: "male",
        BirthDate: CustomTime{
            time.Date(2023, 1, 1, 12, 0, 0, 0, time.Now().Location()),
        },
    }

    b, err := json.Marshal(baby)
    if err != nil {
        log.Fatalf("Unable to marshal due to %s\n", err)
    }

    fmt.Println(string(b))
}
```

```json
{"birth_date":"2023-01-01T12:00:00+01:00","name":"johnny","gender":"male"}
```

Notice how the `birth_date` presented in the [RFC 3339 format](https://www.rfc-editor.org/rfc/rfc3339). You can now define the custom marshalling behavior that will return a different format for `CustomTime` values (such as `DD-MM-YYYY`) instead of the default RFC 3339 timestamp format.

```go
func (ct CustomTime) MarshalJSON() ([]byte, error) {
    return []byte(fmt.Sprintf(`%q`, ct.Time.Format("02-01-2006"))), nil
}
```

Now, when you marshal the `baby` variable once more, you will observe the new format for `birth_date`:

 Output

```json
{"birth_date":"01-01-2023","name":"johnny","gender":"male"}
```

Customizing the unmarshalling behavior for a type works in a similar way. You need to implement the `json.Unmarshaler` type instead:

```go
type Unmarshaler interface {
    UnmarshalJSON([]byte) error
}
```

```go
func (ct *CustomTime) UnmarshalJSON(input []byte) error {
    value := strings.Trim(string(input), `"`)

    t, err := dateparse.ParseAny(value)
    if err != nil {
        return err
    }

    ct.Time = t

    return nil
}
```

Here, the `UnmarshalJSON()` method unmarshals a JSON string in variety of formats into a `CustomTime` value as long as it is supported by the `dateparse` package. With this in place, any of the following date formats (and many others) will be unmarshalled successfully:

```json
{"name": "Mary", "gender": "F", "birth_date": "19-02-2023"}
{"name": "Mary", "gender": "F", "birth_date": "Mon 30 Sep 2022 09:09:09 PM UTC"}
{"name": "Mary", "gender": "F", "birth_date": "2022/12/31"}
```

### The difference between JSON encoding and marshalling

The `encoding/json` package also provides two other constructs for working with JSON in Go which are `json.Encoder` and `json.Decoder`. These types essentially do the same thing as `Marshal` and `Unmarshal` but they operate on streams of data instead of JSON objects that are already fully loaded in memory.

```go
func main() {
    coffeeFile, err := os.Open("assets/coffee.json")
    if err != nil {
        log.Fatalf("Unable to read file due to %s\n", err)
    }

    var coffee Dog

    decoder := json.NewDecoder(coffeeFile)

    err = decoder.Decode(&coffee)
    if err != nil {
        log.Fatalf("Unable to decode due to %s\n", err)
    }

    litter.Dump(coffee)
}
```


 Output

```text
main.Dog{
  Breed: "Toy Poodle",
  Name: "Coffee",
  FavoriteTreat: "Kibble",
  Age: 5,
}
```

One difference between `json.Decode()` and `json.Unmarshal` is that the former allows you to display an error when the input JSON contains properties that do not match any non-ignored, exported fields in the destination unlike the latter where such fields are simply ignored.

This is done through the `DisallowUnknownFields()` method on the `Decoder`:

```go
decoder := json.NewDecoder(coffeeFile)
decoder.DisallowUnknownFields()
```

Assuming the input JSON contains a property that is not present in the `Dog` struct:

```json
{
  "name": "Coffee",
  "breed": "Toy Poodle",
  "age": 5,
  "favorite_treat": "Kibble",
  "color": "brown"
}
```

 error:

```text
2023/03/23 15:29:51 Unable to decode due to json: unknown field "color"
```

The `json.Encoder` type, on the other hand, writes the JSON encoding of a Go type into a provided writable stream (`io.Writer`). It is often used to write a JSON response to a client request:


```go
func main() {
    newDog := Dog{
        Breed:         "Poodle",
        Age:           15,
        Name:          "Chloe",
        FavoriteTreat: "Dog Sticks",
    }

    mux := http.NewServeMux()
    mux.HandleFunc("/", func(w http.ResponseWriter, _ *http.Request) {
        encoder := json.NewEncoder(w)

        err := encoder.Encode(newDog)
        if err != nil {
            log.Fatalf("Unable to encode due to %s\n", err)
        }
    })

    log.Fatal(http.ListenAndServe(":3000", mux))
}
```

When you start the server and make a request to it, you will observe the following response:

```command
curl locahosst:3000
```

 Output

```json
{"breed":"Poodle","name":"Chloe","favorite_treat":"Dog Sticks","age":15}
```



---
# GO - TESTING

Go'da birim testleri için standart kütüphanede bulunan testing paketi kullanır.
Anahtar Notlar: Test işlemlerinde karşılaştığımız önemli iki terim vardır: Verification & Validation (V&V).  
Verification, yazılmış olan kodun doğru çalışmasıdır. Validation kodun doğru işi yapmasıdır.

**assert.go**

```go
package assert  
  
import "testing"  
  
func AssertEqualsFloat64(t *testing.T, errorMessage string, expected, actual float64) {  
    if expected != actual {  
       t.Error(errorMessage)  
    }}  
  
func AssertEqualsBool(t *testing.T, errorMessage string, expected, actual bool) {  
    if expected != actual {  
       t.Error(errorMessage)  
    }}  
  
func AssertTrue(t *testing.T, errorMessage string, result bool) {  
    if !result {  
       t.Error(errorMessage)  
    }}  
func AssertFalse(t *testing.T, errorMessage string, result bool) {  
    if result {  
       t.Error(errorMessage)  
    }
}
```

**clog_test.go**

```go
package cmath  
  
import (  
    "SampleGoLand/csd/cmath"  
    "SampleGoLand/test/assert"    "fmt"    "math"    "testing")  
  
func Test_CLog(t *testing.T) {  
    var input float64 = 100  
    var expected float64 = math.Log(input)  
    actual, _ := cmath.CLog(input)  
  
    assert.AssertEqualsFloat64(t, fmt.Sprintf("Test CLog FAIL:Input:%f, Expected:%f, Actual:%f\n", input, expected, actual), expected, actual)  
}  
  
func Test_CLog_Error(t *testing.T) {  
    var input float64 = -2  
  
    _, err := cmath.CLog(input)  
  
    if err == nil {  
       t.Errorf("Function must give error for the input:%f", input)  
    } else {  
       t.Logf("SUCCESS: Message:%s", err.Error())  
    }}
```

**csqrt_test.go**
```go
package cmath  
  
import (  
    "SampleGoLand/csd/cmath"  
    "SampleGoLand/test/assert"    "fmt"    "testing")  
  
func Test_CSqrt(t *testing.T) {  
    var input float64 = 100  
    var expected float64 = 10  
    actual, _ := cmath.CSqrt(input)  
  
    assert.AssertEqualsFloat64(t, fmt.Sprintf("Test Sqrt FAIL:Input:%f, Expected:%f, Actual:%f\n", input, expected, actual), expected, actual)  
}
```

**isprime_test.go**

```go
package numeric  
  
import (  
    "SampleGoLand/csd/numeric"  
    "SampleGoLand/test/assert"    "fmt"    "testing")  
  
func Test_IsPrime(t *testing.T) {  
    inputs := []struct { //Şüphesiz veriler herhangi bir kaynaktan (source) da elde edilebilir  
       val      int  
       expected bool  
    }{  
       {val: 19, expected: true},  
       {val: 2, expected: true},  
       {val: 1000003, expected: true},  
       {val: -1, expected: false},  
       {val: 1, expected: false},  
    }  
    for _, data := range inputs {  
       actual := numeric.IsPrime(data.val)  
       assert.AssertEqualsBool(t, fmt.Sprintf("Test_IsPrime FAIL: Value:%d, Expected:%t, Actual:%t", data.val, data.expected, actual), data.expected, actual)  
    }}
```

---

### WEB NOTES

Unit tests are a way to test small pieces of code, such as functions and methods. This is useful because it allows you to find bugs early. Unit tests make your testing strategies more efficient, since they are small and independent, and thus easy to maintain.

```go
package main

import "strconv"

// If the number is divisible by 3, write "Foo" otherwise, the number
func Fooer(input int) string {

    isfoo := (input % 3) == 0

    if isfoo {
        return "Foo"
    }

    return strconv.Itoa(input)
}
```

Unit tests in Go are located in the same package (that is, the same folder) as the tested function. By convention, if your function is in the file `fooer.go` file, then the unit test for that function is in the file `fooer_test.go`.

```go
package main
import "testing"
func TestFooer(t *testing.T) {
    result := Fooer(3)
    if result != "Foo" {
    t.Errorf("Result was incorrect, got: %s, want: %s.", result, "Foo")
    }
}
```

A test function in Go starts with `Test` and takes [`*testing.T`](https://pkg.go.dev/testing#T) as the only parameter. In most cases, you will name the unit test `Test[NameOfFunction]`

You can run your tests using the command line:

> go test

## **Writing Table-Driven Tests**

When writing tests, you may find yourself repeating a lot of code in order to cover all the cases required.

You could write one test function per case, but this would lead to a lot of duplication. You could also call the tested function several times in the same test function and validate the output each time, but if the test fails, it can be difficult to identify the point of failure. Instead, you can use a table-driven approach to help reduce repetition.

this involves organizing a test case as a table that contains the inputs and the desired outputs.

This comes with two benefits:

- Table tests reuse the same assertion logic, keeping your test [DRY](https://blog.jetbrains.com/dotnet/2021/02/08/make-code-more-readable-by-refactoring-with-resharper/#DRY_readability).
- Table tests make it easy to know what is covered by a test, as you can easily see what inputs have been selected. Additionally, each row can be given a unique name to help identify what’s being tested and express the intent of the test.

```go
func TestFooerTableDriven(t *testing.T) {
      // Defining the columns of the table
        var tests = []struct {
        name string
            input int
            want  string
        }{
            // the table itself
            {"9 should be Foo", 9, "Foo"},
            {"3 should be Foo", 3, "Foo"},
            {"1 is not Foo", 1, "1"},
            {"0 should be Foo", 0, "Foo"},
        }
      // The execution loop
        for _, tt := range tests {
            t.Run(tt.name, func(t *testing.T) {
                ans := Fooer(tt.input)
                if ans != tt.want {
                    t.Errorf("got %s, want %s", ans, tt.want)
                }
            })
        }
    }
```

A table-driven test starts by defining the input structure. You can see this as defining the columns of the table. Each row of the table lists a test case to execute. Once the table is defined, you write the execution loop.

The execution loop calls [`t.Run()`](https://pkg.go.dev/testing#T.Run), which defines a subtest. As a result, each row of the table defines a subtest named `[NameOfTheFuction]/[NameOfTheSubTest]`.

This way of writing tests is very popular, and considered the canonical way to write unit tests in Go.

## **The Testing Package**

The `testing` package plays a pivotal role in Go testing. It enables developers to create unit tests with different types of test functions. The `testing.T` type offers methods to control test execution, such as running tests in parallel with [`Parallel()`](https://pkg.go.dev/testing#T.Parallel), skipping tests with [`Skip()`](https://pkg.go.dev/testing#T.Skip), and calling a test teardown function with [`Cleanup()`](https://pkg.go.dev/testing#T.Cleanup).

### Errors and Logs

==It is important to mention that `t.Error*` does not stop the execution of the test. Instead, all encountered errors will be reported once the test is completed. Sometimes it makes more sense to fail the execution; in that case, you should use `t.Fatal*`==

```go
func TestFooer2(t *testing.T) {
            input := 3
            result := Fooer(3)
            t.Logf("The input was %d", input)
            if result != "Foo" {
                t.Errorf("Result was incorrect, got: %s, want: %s.", result, "Foo")
            }
            t.Fatalf("Stop the test now, we have seen enough")
            t.Error("This won't be executed")
        }
```

### Running Parallel Tests

By default, tests are run sequentially; the method [`Parallel()`](https://pkg.go.dev/testing#T.Parallel) signals that a test should be run in parallel. All tests calling this function will be executed in parallel. `go test` handles parallel tests by pausing each test that calls `t.Parallel()`, and then resuming them in parallel when all non-parallel tests have been completed.

The `GOMAXPROCS` environment defines how many tests can run in parallel at one time, and by default this number is equal to the number of CPUs.

```go
func TestFooerParallel(t *testing.T) {
        t.Run("Test 3 in Parallel", func(t *testing.T) {
            t.Parallel()
            result := Fooer(3)
            if result != "Foo" {
                t.Errorf("Result was incorrect, got: %s, want: %s.", result, "Foo")
            }
        })
        t.Run("Test 7 in Parallel", func(t *testing.T) {
            t.Parallel()
            result := Fooer(7)
            if result != "7" {
                t.Errorf("Result was incorrect, got: %s, want: %s.", result, "7")
            }
        })
    }
```

To reduce duplication, you may want to use table-driven tests when using `Parallel()`.

### Skipping Tests

Using the [`Skip()`](https://pkg.go.dev/testing#T.Skip) method allows you to separate unit tests from [integration tests](https://medium.com/@victorsteven/understanding-unit-and-integrationtesting-in-golang-ba60becb778d). Integration tests validate multiple functions and components together and are usually slower to execute, so sometimes it’s useful to execute unit tests only.

```go
func TestFooerSkiped(t *testing.T) {
        if testing.Short() {
            t.Skip("skipping test in short mode.")
        }
        result := Fooer(3)
        if result != "Foo" {
            t.Errorf("Result was incorrect, got: %s, want: %s.", result, "Foo")
        }
    }
```

This test will be executed if you run `go test -v`, but will be skipped if you run `go test -v -test.short`.

### Test Teardown and Cleanup

The [`Cleanup()`](https://pkg.go.dev/testing#T.Cleanup) method is convenient for managing test tear down.
Using the `defer` solution looks like this:

```go
func Test_With_Cleanup(t *testing.T) {

  // Some test code

  defer cleanup()

  // More test code
}
```

While this is simple enough, it comes with a few issues The main argument against the `defer` approach is that it can make test logic more complicated to set up, and can clutter the test function when many components are involved.

The `Cleanup()` function is executed at the end of each test (including subtests), and makes it clear to anyone reading the test what the intended behavior is.

```go
func Test_With_Cleanup(t *testing.T) {

  // Some test code here

    t.Cleanup(func() {
        // cleanup logic
    })

  // more test code here

}
```

[`Helper()`](https://pkg.go.dev/testing#T.Helper) method. This method exists to improve the logs when a test fails. In the logs, the line number of the helper function is ignored and only the line number of the failing test is reported, which helps figure out which test failed.

```go
func helper(t *testing.T) {
  t.Helper()
  // do something
}

func Test_With_Cleanup(t *testing.T) {

  // Some test code here

    helper(t)

  // more test code here

}
```

[`TempDir()`](https://pkg.go.dev/testing#T.TempDir) is a method that automatically creates a temporary directory for your test and deletes the folder when the test is completed, removing the need to write additional cleanup logic.

```go
func TestFooerTempDir(t *testing.T) {
    tmpDir := t.TempDir()

  // your tests
}
```

## **Writing Coverage Tests**

As tests are crucial to modern development work, it’s essential to know how much of your code is covered by tests. You can use Go’s built-in tool to generate a test report for the package you’re testing by simply adding the `-cover` flag in the test command:

```go
go test -cover
```

By default, test coverage calculates the percentage of statements covered through tests.

There are various arguments that can be passed to `go test -cover`. For example, `go test` only considers packages with test files in the coverage calculation. You can use `-​coverpkg` to include all packages in the coverage calculation:

```go
go test ./... -coverpkg=./...
```

also use go tool cover to format the report. For example, the `-html` flag will open your default browser to display a graphical report.

```go
go tool cover -html=output_filename
```

The last flag  [`-covermode`](https://go.dev/blog/cover#heat-maps) . By default, the coverage is calculated based on the statement coverage, but this can be changed to take into account how many times a statement is covered. There are several different options:

- `set`: Coverage is based on statements.
- `count`: Count is how many times a statement was run. It allows you to see which parts of code are only lightly covered.
- `atomic`: Similar to count, but for parallel tests.

Knowing which flag to use when running coverage tests is most important when running tests in your CI/CD 

## **Writing Benchmark Tests**

Benchmark tests are a way of testing your code performance. The goal of those tests is to verify the runtime and the memory usage of an algorithm by running the same function many times.

To create a benchmark test:

- Your test function needs to be in a `*_test` file.
- The name of the function must start with `Benchmark`.
- The function must accept `*testing.B` as the unique parameter.
- The test function must contain a `for` loop using `b.N` as its upper bound.

```go
func BenchmarkFooer(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Fooer(i)
    }
}
```

The target code should be run `N` times in the benchmark function, and `N` is automatically adjusted at runtime until the execution time of each iteration is statistically stable.

have to use other tools if you want to save and analyze the results in your CI/CD. [`perf/cmd`](https://golang.org/x/perf/cmd) offers packages for this purpose. [`benchstat`](https://golang.org/x/perf/cmd/benchstat) can be used to analyze the results, and [`benchsave`](https://pkg.go.dev/golang.org/x/perf/cmd/benchsave) can be used to save the result.

## **Writing Fuzz Tests**

Fuzz testing is an exciting testing technique in which random input is used to discover bugs or edge cases. Go’s fuzzing algorithm is smart because it will try to cover as many statements in your code as possible by generating many new input combinations.

To create a fuzz test:

- Your test function needs to be in a `_test` file.
- The name of the function must start with `Fuzz`.
- The test function must accept `testing.F` as the unique parameter.
- The test function must define initial values, called [seed corpus](https://go.dev/security/fuzz/#glos-seed-corpus), with the `f.Add()` method.
- The test function must define a [fuzz target](https://go.dev/security/fuzz/#glos-fuzz-target).

```go
func FuzzFooer(f *testing.F) {
    f.Add(3)
    f.Fuzz(func(t *testing.T, a int) {
        Fooer(a)
    })
}
```

The goal of the fuzz test is not to validate the output of the function, but instead to use unexpected inputs to find potential edge cases. By default, fuzzing will run indefinitely, as long as there isn’t a failure. The `-fuzztime` flag should be used in your CI/CD to specify the maximum time for which fuzzing should run. This approach to testing is particularly interesting when your code has many branches; even with table-driven tests, it can be hard to cover a large set of input, and fuzzing helps to solve this problem.

## **The Testify Package**

[Testify](https://github.com/stretchr/testify) is a testing framework providing many tools for testing Go code.

Testify can be installed with the command `go get github.com/stretchr/testify`.

Testify provides assert functions and mocks, which are similar to traditional testing frameworks, like [JUnit](https://junit.org/junit5/) for Java

```go
func TestFooerWithTestify(t *testing.T) {

    // assert equality
    assert.Equal(t, "Foo", Fooer(0), "0 is divisible by 3, should return Foo")

    // assert inequality
    assert.NotEqual(t, "Foo", Fooer(1), "1 is not divisible by 3, should not return Foo")
}
```

Testify provides two packages, `require` and `assert`. The `require` package will stop execution if there is a test failure, which helps you fail fast. `assert` lets you collect information, but accumulate the results of assertions.

```go
func TestMapWithTestify(t *testing.T) {

    // require equality
    require.Equal(t, map[int]string{1: "1", 2: "2"}, map[int]string{1: "1", 2: "3"})

    // assert equality
    assert.Equal(t, map[int]string{1: "1", 2: "2"}, map[int]string{1: "1", 2: "2"})
}
```

The output log also clearly indicates the difference between the actual output and the expected output. Compared to Go’s built-in `testing` package, the output is more readable, especially when the testing data is complicated, such as with a long map or a complicated object. The log points out exactly which line is different, which can boost your productivity.

