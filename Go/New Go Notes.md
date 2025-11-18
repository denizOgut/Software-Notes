
# 1. Go Fundamentals & Setup

## 1.1 Go Environment

### GOPATH vs Go Modules

####  the GOPATH Environment Variable

The Go programming language initially delimited a scope for the location of dependencies and custom projects inside a filesystem. This was defined by the `GOPATH` environment variable. 

The `GOPATH` variable by default would point to a `/go` folder defined directly under the user home directory path (`~/` in ``unix``-based or `%HOMEPATH%` on windows-based systems).

There are three notable directories under `GOPATH`: `src`, `pkg`, and `bin`. The `src` directory holds the source code of both your projects and installed dependencies. When you execute a command such as `go get github.com/user/repo`, the Go tool fetches the module from the specified location and places it into the `src` directory under the `GOPATH`, with a path named after the resource's URL.

The `pkg` directory contains compiled package objects (.a files) that your code depends on. When a package is built, the resulting file is placed in the `pkg` directory.

The `bin` directory holds the binary executables of your applications. When you build an executable program, the resulting binary file is placed in the `bin` directory.


the default path for `GOPATH`:

```
/home/user/go/         <--- This is your GOPATH
├── bin/
├── pkg/
│   └── linux_amd64/
│       └── github.com/
│           └── someuser/
│               └── somelib.a    <--- Compiled dependency package
└── src/
    ├── github.com/
    │   └── someuser/
    │       └── somelib/         <--- Dependency's source code
    │           └── somelib.go
    └── myapp/                   <--- Your project
        └── main.go
```

The single workspace structure defined by `GOPATH` means that all your Go code and its dependencies share a single common space.

#### Modular Approach 

This is delimited by the presence of a `go.mod` file and also usually a go.sum file, generated once any operation concerning externally hosted packages is executed (like `go get <package>`).

A module is a collection of related Go packages that are versioned together as a single unit. 

A Go module is defined by a go.mod file that resides at the root of the module's directory hierarchy. This file defines the module path, which is the import path prefix for all packages within the module. It specifies the dependencies of the module, including the required versions of other modules.

Modules allow for versioning and releasing a set of packages together, and they also make dependency version information explicit and easier to manage.

**==a module is a versioned collection of packages that also handles dependency management. This allows each Go project to have its own isolated and reproducible build environment.==**

#####  Naming Conventions for Modules

**module names are used system-wide and therefore should be as specific as possible,** especially if you plan on distributing the module to other developers. The module name is specified in the `go.mod` file, which acts as the module's manifest and is located at the root of the module's directory hierarchy.

**Module Path**: The module path should be a globally unique identifier for the module. It typically takes the form of an internet domain name in reverse order, followed by the module name. For example, `github.com/littlejohnny65/example-module`.

**Module Name**: The module name is the last component of the module path. It should be short, descriptive, and adhere to Go's naming conventions. It is recommended to use lowercase letters with no underscores or ``mixedCaps``. For example, `examplemodule`.

**Versioning**: The module name itself does not include version information. The version of a module is specified separately in the `go.mod` file using a module version identifier, such as `v1.2.3`. The combination of the module path and the version identifier uniquely identifies a specific version of the module.

### go.mod & go.sum files

#### go.mod File

The `go.mod` file is Go's dependency manifest file (similar to `pom.xml` in Maven or `build.gradle` in Gradle). It defines the module's properties and tracks dependency requirements.
##### Basic Structure

```go
module github.com/username/projectname

go 1.21

require (
    github.com/gin-gonic/gin v1.9.1
    github.com/joho/godotenv v1.5.1
    github.com/lib/pq v1.10.9
)

require (
    // indirect dependencies (automatically managed)
    github.com/bytedance/sonic v1.9.1 // indirect
    github.com/chenzhuoyu/base64x v0.0.0-20221115062448-fe3a3abad311 // indirect
)

replace github.com/broken/package v1.0.0 => github.com/fork/package v1.0.1

exclude github.com/unwanted/package v1.2.3
```

##### Key Components

**Module Declaration**

```go
module github.com/username/projectname
```

- Defines the module path (import path prefix for all packages in the module)
- Should be a path that can be fetched by Go tools (typically a repository URL)

**Go Version**

```go
go 1.21
```

- Specifies the minimum Go version required
- Affects language features and standard library availability
- Not a strict enforcement, more of a recommendation

**Require Directives**

```go
require (
    github.com/gin-gonic/gin v1.9.1
    github.com/lib/pq v1.10.9
)
```

- Lists direct dependencies with their minimum versions
- Version format: `vMAJOR.MINOR.PATCH` (semantic versioning)
- `latest`: latest available version (resolved to specific version)

**Indirect Dependencies**

```go
require (
    github.com/some/package v1.0.0 // indirect
)
```

- Dependencies of your dependencies
- Automatically managed by Go tools
- Marked with `// indirect` comment

**Replace Directive**

```go
replace (
    github.com/broken/package v1.0.0 => github.com/fork/package v1.0.1
    github.com/local/package => ../local-package
    github.com/old/package => github.com/old/package v1.2.3
)
```

- Substitutes one module with another
- Useful for:
    - Using forked repositories
    - Local development (pointing to local directories)
    - Fixing broken dependencies
    - Testing with specific versions

**Exclude Directive**

````go
exclude github.com/unwanted/package v1.2.3
```
- Prevents specific module versions from being used
- Rarely used, mainly for broken releases

#### go.sum File

The `go.sum` file is a checksum database containing cryptographic hashes of module versions (similar to `package-lock.json` in npm or `Gemfile.lock` in Ruby).

##### Purpose
- **Security**: Ensures downloaded modules haven't been tampered with
- **Reproducibility**: Guarantees the same dependencies across different builds
- **Integrity**: Verifies module content integrity

##### Structure
```
github.com/gin-gonic/gin v1.9.1 h1:4idEAncQnU5cB7BeOkPtxjfCSye0AAm1R0RVIqJ+Jmg=
github.com/gin-gonic/gin v1.9.1/go.mod h1:hPrL7YrpYKXt5YId3A/Tnip5kqbEAP+KLuI3SUcPTeU=
github.com/go-playground/validator/v10 v10.14.0 h1:vgvQWe3XCz3gIeFDm/HnTIbj6UGmg/+t63MyGU2n5js=
github.com/go-playground/validator/v10 v10.14.0/go.mod h1:9iXMNT7sEkjXb0I+enO7QXmzG6QCsPWY4zveKFVRSyU=
````

Each module version has two entries:

1. **Module hash**: Hash of the module's `.zip` file
2. **go.mod hash**: Hash of the module's `go.mod` file only

Format: `<module> <version> <hash-algorithm>:<hash>`

- Hash algorithm is typically `h1:` (SHA-256)

#### go.sum File

The `go.sum` file is Go's checksum lock file that ensures dependency integrity and reproducible builds (similar to `package-lock.json` in ``npm`` or `Gemfile.lock` in Ruby).

##### Purpose

- **Security**: Verifies modules haven't been tampered with
- **Reproducibility**: Ensures everyone gets the exact same dependencies
- **Integrity**: Cryptographic proof of module contents

##### Structure

```
github.com/gin-gonic/gin v1.9.1 h1:4idEAncQnU5cB7BeOkPtxjfCSye0AAm1R0RVIqJ+Jmg=
github.com/gin-gonic/gin v1.9.1/go.mod h1:hPrL7YrpYKXt5YId3A/Tnip5kqbEAP+KLuI3SUcPTeU=
github.com/lib/pq v1.10.9 h1:YXG7RB+JIjhP29X+OtkiDnYaXQwpS4JEWq7dtCCRUEw=
github.com/lib/pq v1.10.9/go.mod h1:AlVN5x4E4T544tWzH6hKfbfQvm3HdbOxrmggDNAPY9o=
```

Each dependency has **two entries**:

1. **Module hash**: `<module> <version> h1:<hash>` - Hash of the entire module
2. **go.mod hash**: `<module> <version>/go.mod h1:<hash>` - Hash of just the go.mod file

The `h1:` prefix indicates SHA-256 hashing algorithm.

##### Key Characteristics

**Automatically Generated**

- Created and updated automatically by Go commands
- Never edit manually
- Generated when you run `go get`, `go mod tidy`, or `go build`

**Contains All Versions**

- Includes hashes for all versions ever downloaded
- Even versions no longer used (for rollback safety)
- May contain more entries than go.mod requires

##### Best Practices

1. **Always commit go.sum to version control**
    - Essential for reproducible builds
    - Team members get exact same dependencies
2. **Don't modify go.sum manually**
    - Let Go tools manage it
    - If corrupted, delete and run `go mod tidy`
3. **Review go.sum changes in PRs**
    - New entries indicate new dependencies
    - Changed hashes could indicate security issues
4. **Handle merge conflicts**


```bash
   # After resolving go.mod conflicts
   rm go.sum
   go mod tidy  # Regenerate go.sum
```


## 1.2 Go Toolchain

### go run, build

#### go run

The go run command **compiles and runs a main package comprised of the .go files specified on the command line**. The command is compiled to a temporary folder. The go build and go install examine the files in the directory to determine which .go files are included in the main package.

Usage:
```go
go run [build flags] [-exec xprog] package [arguments...]
```

#### go build

The `go build` command compiles Go source code along with dependencies into an executable. It's designed for flexibility, supporting single packages, entire projects, and cross-platform compilation. By default, it generates a binary in the current directory, named after the package's directory.

```go
go build

go build ./...

go build path/to/package
```

##### Cross-Platform Compilation

Go excels at cross-compiling binaries for diverse platforms. Specify the target OS and architecture using `GOOS` and `GOARCH`:

```go
GOOS=linux GOARCH=amd64 go build -o app-linux
```

##### Supported Platforms

To get list all supported platforms:

```go
go tool dist list
```

##### Common Targets:

- **Windows 64-bit**: `GOOS=windows GOARCH=amd64`
- **Linux ARM64**: `GOOS=linux GOARCH=arm64`
- **macOS**: `GOOS=darwin GOARCH=arm64`

### go get, mod tidy

#### go get

The `go get` command is a tool used to download dependencies along with updating the `go.mod` file.

Using this command, you can download Go packages for your project from remote repositories such as GitHub, Bitbucket or other Git-based repositories.

```go
go get [flags] [packages]

go get github.com/google/uuid

go get github.com/google/uuid gorm.io/gorm

```

#### go mod tidy

Tidy makes sure go.mod matches the source code in the module. It adds any missing modules necessary to build the current module’s packages and dependencies, and it removes unused modules that don’t provide any relevant packages. It also adds any missing entries to go.sum and removes any unnecessary ones.

It:
- Scans your app’s Go source files for package references
- Adds them to _go.mod_
- Creates _go.sum_ (if not present) and adds the packages there as well

## 1.3 Package System

### Package declaration

Every Go program is made up of packages.

Programs start running in package `main`. By convention, the package name is the same as the last element of the import path. For instance, the `"math/rand"` package comprises files that begin with the statement `package rand`.

Packages in the standard library have short import paths, such as `"fmt"` and `"math/rand"`. Third-party packages, such as `"github.com/yourbasic/graph"`, typically have an import path that includes a hosting service (`github.com`) and an organization name (`yourbasic`).

References to other packages’ definitions must always be prefixed with their package names, and only the capitalized names from other packages are accessible.

```go
package main

import (
	"fmt"
	"math/rand"

	"github.com/yourbasic/graph"
)

func main() {
	n := rand.Intn(100)
	g := graph.New(n)
	fmt.Println(g)
}
```

#### Declare a package

Every Go source file starts with a package declaration, which contains only the package name.

```go
package rand
  
import "math"
  
const re = 7.69711747013104972
…
```

#### Package name conflicts

```go
package main

import (
	csprng "crypto/rand"
	prng "math/rand"

	"fmt"
)

func main() {
	n := prng.Int() // pseudorandom number
	b := make([]byte, 8)
	csprng.Read(b) // cryptographically secure pseudorandom number
	fmt.Println(n, b)
}
```

### Import statements

Package needs to be imported first to use its exported identifiers. It’s done with construct called _import declaration_:

```go
package main

import (  
    "fmt"  
    "math"  
)

func main() {  
    fmt.Println(math.Exp2(10))  // 1024  
}
```

When importing a package from the standard library you need to use the _full path to the package_ in the standard library tree, not just the name of the package. For example:

```go
import (
    "fmt"
    "math/rand"         // Not "rand"
    "net/http"          // Not "http"
    "net/http/httptest" // Not "httptest"
)
```
Once imported, the _package name_ becomes an accessor for the contents of that package. Conveniently, all the packages in the Go standard library have a package name which is the _same as the final element of their import path_.

#### Unused and missing imports

If you import a package but don't actually use it in your code, it will result in a compile-time error. For example, if you import the `os` package but don't use it you will get an error like:

`"os" imported and not used`

Similarly, you'll also get a compile-time error if a package is referenced in your code but _not_ imported. For example, if you try to use the `strconv` package without importing it you'll get an error like this:

`   undefined: strconv   `

#### Import with alias

Packages can be imported with custom aliases to avoid naming conflicts or provide shorter references.

```go
package main

import (
    "fmt"
    m "math"
)

func main() {
    fmt.Println("Cosine of 0:", m.Cos(0))
    fmt.Println("Square root of 9:", m.Sqrt(9))
}

```

#### Blank import

Blank imports execute package initialization without making its exports available. This is used for side effects like database drivers.

```go
package main

import (
    "fmt"
    _ "image/png"
)

func main() {
    fmt.Println("PNG decoder registered")
}

```

The `_ "image/png"` import registers the PNG decoder without exposing its functions. The main function demonstrates that the program runs while the import's side effect takes place.

####  Dot imports

If a period `.` appears instead of a name in an import statement, all the package’s exported identifiers can be accessed without a qualifier.

```go
package main

import (
	"fmt"
	. "math"
)

func main() {
	fmt.Println(Sin(Pi/2)*Sin(Pi/2) + Cos(Pi)/2) // 0.5
}
```

Dot imports can make programs hard to read and **generally should be avoided**.

### ``init()`` function

The **`init()` function** serves as a unique package initializer in the Go language. An `init()` function is package-scoped, and we can use it to set up our application state before entering into the `main()` function. It is invoked sequentially in a single `Goroutine`, along with other global variable initializations.

- The `init` function doesn’t take any arguments.
- The `init` function doesn’t return any results.

```go
package main
import "fmt"
func init(){
  fmt.Printf("Invoked init()\n")
}

func main() {
    fmt.Printf("Executing main()\n")
}
```

We can define multiple `init()` functions in Go. We can even have multiple `init` functions in a single file. They’ll be invoked sequentially in the order that they appear

### Package visibility (exported/unexported)

- All identifiers defined within a package are visible throughout that package.
- When importing a package you can access only its **exported** identifiers.
- An identifier is exported if it begins with a **capital letter**.

```go

package timer

import "time"

// A StopWatch is a simple clock utility.
// Its zero value is an idle clock with 0 total time.
type StopWatch struct {
	start   time.Time
	total   time.Duration
	running bool
}

// Start turns the clock on.
func (s *StopWatch) Start() {
	if !s.running {
		s.start = time.Now()
		s.running = true
	}
}
```

The `StopWatch` and its exported methods can be imported and used in a different package.

```go

package main

import "timer"

func main() {
	clock := new(timer.StopWatch)
	clock.Start()
	if clock.running { // ILLEGAL
		// …
	}
}
```

# 2. Basic Syntax & Types

## 2.1 Variables & Constants

### Variable declaration

In Go, there are two ways to declare a variable:

#### 1. With the `var` keyword:

Use the `var` keyword, followed by variable name and type:

```go
var _variablename type_ = _value_
```

 You always have to specify either `type` or `value` (or both).

#### 2. With the `:=` sign:

Use the `:=` sign, followed by the variable value:

```go
_variablename_ := _value_
```

 In this case, the type of the variable is **inferred** from the value

```go
package main  
import ("fmt")  
  
func main() {  
  var student1 string = "John" _//type is string_  
  var student2 = "Jane" _//type is inferred_  
  x := 2 _//type is inferred_  
  
  fmt.Println(student1)  
  fmt.Println(student2)  
  fmt.Println(x)  
}
```

### Zero Values

- `0` for all **integer** types,
- `0.0` for **floating point** numbers,
- `false` for **booleans**,
- `""` for **strings**,
- `nil` for **interfaces**, **slices**, **channels**, **maps**, **pointers** and **functions**.

### Multiple assignment

```go
package main  
import ("fmt")  
  
func main() {  
  var a, b, c, d int = 1, 3, 5, 7  
  
  fmt.Println(a)  
  fmt.Println(b)  
  fmt.Println(c)  
  fmt.Println(d)  
}
```

If the `type` keyword is not specified, you can declare different types of variables on the same line:

```go
package main  
import ("fmt")  
  
func main() {  
  var a, b = 6, "Hello"  
  c, d := 7, "World!"  
  
  fmt.Println(a)  
  fmt.Println(b)  
  fmt.Println(c)  
  fmt.Println(d)  
}
```

### Constants & iota

#### Constants

Constants hold a piece of data just like variables, but their value cannot change during the execution of the program. Constants are defined using the `const` keyword and can be numbers, characters, strings, or booleans. Constants cannot be declared using the `:=` syntax.

```go
const CONSTNAME type = value
const PI = 3.14
```


##### Multiple Constants Declaration

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

- Constant variables cannot be reassigned after their declaration.
- `const` values must be known at compile time. Hence, a `const` value cannot be assigned to a function call that is evaluated at runtime.

##### Typed and Untyped Constants

- Go has a very strong type system that doesn’t allow implicit conversion between any of the types.
- Even with the same numeric types, no operation is allowed without explicit conversion.
- However, untyped constants have the flexibility of temporary escape from Go’s type system.

###### Typed Constant

A `const` declared specifying the type in the declaration is a typed constant.

```go
const a int32 = 8

```

###### Untyped Constant

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

#### Iota

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

- Iota keyword can be used on each line as well. In that case, also iota will start from zero and increment on each new line.

```go
const (
	a = iota
	b = iota
	c = iota
)
```

* iota keyword can be skipped as well. In that case, also iota will start from zero and increment on each new line.
```go
const (
    a = iota
    b
    c = iota
)
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

### Scope

In Go, all identifiers are lexically scoped, meaning the scope can be determined at compile time. A variable is only accessible within the block of code where it is defined.

```go
package main    
import "fmt"  
  
// Global variable declaration   
var myVariable int = 100   
  
func main() {  
    // Local variable inside the main function   
    var localVar int = 200   
    fmt.Printf("Inside main - Global variable: %d\n", myVariable)   
    fmt.Printf("Inside main - Local variable: %d\n", localVar)   
    display()   
}  
  
func display() {  
    fmt.Printf("Inside display - Global variable: %d\n", myVariable)   
}
```

**When a local variable shares the same name as a global variable, the local variable takes precedence within its scope.**

## 2.2 Basic Data Types

| Tür ismi   | Uzunluğu (byte) | Varsayılan Değer       |
| ---------- | --------------- | ---------------------- |
| int8       | 1               | 0                      |
| uint8      | 1               | 0                      |
| int16      | 2               | 0                      |
| uint16     | 2               | 0                      |
| int32      | 4               | 0                      |
| uint32     | 4               | 0                      |
| int64      | 8               | 0                      |
| uint64     | 8               | 0                      |
| byte       | 1               | 0                      |
| rune       | 4               | 0                      |
| uint       | 4/8             | 0 (Platform Dependent) |
| int        | 4/8             | 0 (Platform Dependent) |
| float32    | 4               | 0                      |
| float64    | 8               | 0                      |
| complex64  | 8               | (0+0i)                 |
| complex128 | 16              | (0+0i)                 |
| bool       | 1               | false                  |

Golang is a statically typed programming language meaning that each variable has a type.

- Boolean types -> Represents true or false values.
    
- Numeric types -> Represents integers, floating-point numbers, and complex numbers.
    
- String types -> Represents text.
    
- **Boolean:** Represents True or False values. Uses 1 bit of memory.
    
- **Byte:** Represents an 8-bit character. Uses 1 byte of memory.
    
- **Rune:** Represents a UTF-8 character. Uses 4 bytes of memory.
    
- **Int:** Represents signed or unsigned integers. Uses 4 or 8 bytes of memory.
    
- **Uint:** Represents unsigned integers. Uses 4 or 8 bytes of memory.
    
- **Float:** Represents decimal numbers. Uses 4 or 8 bytes of memory.
    
- **Complex:** Represents complex numbers. Uses 8 or 16 bytes of memory.
    
- Numeric types are generally divided into two groups: integer/integral types, real types/floating point types
    

- Integer types are kept separately as signed and unsigned and work in two's complement format.
- Real number types use the IEEE754 format.
- complex64 type represents a complex number whose real and imaginary parts are of type float32.
- complex128 type represents a complex number whose real and imaginary parts are of type float64.
- The lengths of integer types int8, uint8, int16, uint16, int32, uint32, int64, uint64 do not change from system to system.
- The lengths of float32, float64, complex64 and complex128 types do not change from system to system.
- byte type is an alias for the uint8 type.
- rune type is an alias for the int32 type.
- int and uint types are integer types whose length can vary from system to system (4 bytes or 8 bytes).
- bool type is a type that is 1 byte long and can take one of the true or false values.


## 2.3 Functions

### Basic functions

- `func` keyword starts the declaration.
- Parameters: name + type.
- Return type after parameter list.

```go
func functionName(parameter type) returnType {
    // function body
    return value
}

func add(a int, b int) int {
    return a + b
}

func sayHello() {
    fmt.Println("Hello!")
}
```

### Multiple return values

```go
func divide(a, b int) (int, int) {
    return a / b, a % b
}

q, r := divide(10, 3) // q=3, r=1
```

- Commonly used for returning a value and an error.

### Named returns

Go's return values may be named. If so, they are treated as variables defined at the top of the function.

These names should be used to document the meaning of the return values.

A `return` statement without arguments returns the named return values. This is known as a "naked" return.

Named return values are automatically initialized to zero values when the function starts

```go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	fmt.Println(split(17))
}
```

```go
func calculate(a, b int) (sum int, product int) {
    sum = a + b
    product = a * b
    return // naked return - returns named values
}

x, y := calculate(3, 4) // x=7, y=12
```

```go
func readFile(filename string) (data []byte, err error) {
    file, err := os.Open(filename)
    if err != nil {
        return // data=nil, err=<error> 
    }
    defer file.Close()
    
    data, err = io.ReadAll(file)
    return // return both
}
```

### Variadic functions

- A function that can take **zero or more arguments** of the same type.
- Syntax: `...type` as the **last parameter**.

```go
func sum(nums ...int) int {
    total := 0
    for _, n := range nums {
        total += n
    }
    return total
}

fmt.Println(sum(1, 2, 3))    // 6
fmt.Println(sum())           // 0
```

- Only **one variadic parameter**, and it must be last.
- Inside the function, it behaves like a **slice**.

```go
func greet(prefix string, names ...string) {
    for _, n := range names {
        fmt.Println(prefix, n)
    }
}

greet("Hello", "Alice", "Bob")
```

### First-class functions

In Go, functions are **first-class citizens**, meaning they can be treated like any other value - assigned to variables, passed as arguments, returned from functions, and stored in data structures.
#### 1. Assigning Functions to Variables

```go
package main

import "fmt"

func main() {
    // Assign function to a variable
    add := func(a, b int) int {
        return a + b
    }
    
    result := add(5, 3)
    fmt.Println(result) // 8
}
```

#### 2. Functions as Parameters

```go
func applyOperation(a, b int, op func(int, int) int) int {
    return op(a, b)
}

func add(x, y int) int {
    return x + y
}

func subtract(x, y int) int {
    return x - y
}

func main() {
    result1 := applyOperation(10, 5, add)      // 15
    result2 := applyOperation(10, 5, subtract) // 5
    
    // Using anonymous function
    result3 := applyOperation(10, 5, func(x, y int) int {
        return x * y
    }) // 50
    
    fmt.Println(result1, result2, result3)
}
```

#### 3. Returning Functions

```go
func makeMultiplier(factor int) func(int) int {
    return func(num int) int {
        return num * factor
    }
}

func main() {
    double := makeMultiplier(2)
    triple := makeMultiplier(3)
    
    fmt.Println(double(5))  // 10
    fmt.Println(triple(5))  // 15
}
```

### Anonymous functions

Anonymous functions are functions **without a name**. They're also called **lambda functions** or **function literals**.

#### 1. Assigning to Variables

```go
package main

import "fmt"

func main() {
    // Anonymous function assigned to a variable
    greet := func(name string) string {
        return "Hello, " + name
    }
    
    fmt.Println(greet("Alice")) // Hello, Alice
}
```

#### 2. Immediate Invocation (IIFE)

**Immediately Invoked Function Expression** - define and call at the same time:

```go
func main() {
    // Define and call immediately
    result := func(a, b int) int {
        return a + b
    }(5, 3) // Notice the (5, 3) right after function definition
    
    fmt.Println(result) // 8
}
```

```go
func main() {
    func() {
        fmt.Println("This runs immediately!")
    }() // () at the end calls it
}
```

```go
func main() {
    func(msg string) {
        fmt.Println(msg)
    }("Hello from IIFE!") // Pass argument directly
}
```

### Closures

**==a closure is a function that captures variables from its surrounding scope. This allows the function to "remember" the environment in which it was created, even when it's executed outside that environment==**

---

A **closure** is a function defined inside another function that **captures and keeps access to the outer function’s variables**, even **after the outer function has finished executing**.

- **Captures by reference**, not by value.
- Each call to the outer function gets its **own copy** of the captured variables.
- Useful for **encapsulation**, **stateful functions**, and **function factories**.

---

```go
package main

import "fmt"

func makeCounter() func() int {
    count := 0
    return func() int {
        count++
        return count
    }
}

func main() {
    counterA := makeCounter()
    fmt.Println(counterA()) // 1
    fmt.Println(counterA()) // 2
    fmt.Println(counterA()) // 3

    counterB := makeCounter()
    fmt.Println(counterB()) // 1 (new closure, new count)
    fmt.Println(counterA()) // 4 (original closure continues from 3)
}
```

- `makeCounter` creates a closure that captures `count`.
- Each `counterA()` call **remembers and updates** `count`.
- `counterB()` starts fresh because it gets a **new instance** of `count`.

#### Common Patterns

- **Function generators**: Create customized functions with internal state.
- **Callback functions**: Used in goroutines, handlers, etc.
- **Testing and mocking**: Return functions with embedded test logic.

###  Defer, panic & recover

#### Defer

- `defer` tells Go to **wait to run a function until the current function finishes**.
- You write `defer` before a function call, and Go will remember it.
- Once your current function is _**about to return**_ (either because it finished or panicked), Go runs all the deferred functions.

##### Why use `defer`?

- It's mostly used for **cleanup tasks**, like:
    - Closing a file after you're done reading/writing it.
    - Unlocking something you locked earlier.
    - Releasing a resource (like a network connection).

```go
func main() {
    fmt.Println("Start")
    defer fmt.Println("This runs last")
    fmt.Println("End")
}
```

```
Start
End
This runs last
```

##### What if you use multiple `defer` statements?

- Go runs them in **reverse order** — like a stack.
- The **last one you deferred runs first**, then the one before that, and so on.

```go
func example() {
    defer fmt.Println("first")
    defer fmt.Println("second")
}
```

```
second
first
```

##### Common Use Cases

1. `defer file.Close()` → after opening a file.
2. `defer mu.Unlock()` → after acquiring a lock.
3. `defer recover()` → inside a panic handler.

#### Panic & Recover

- **`panic`**: Immediately stops normal execution and begins **stack unwinding** (like throwing an exception).
- **`recover`**: Regains control during a panic, but only **within a `defer` function**.

Together, they allow **controlled failure handling**.

|Feature|Use When…|
|---|---|
|`panic`|- unrecoverable error (e.g., out of bounds, nil pointer) - programmer bug or critical failure|
|`recover`|- want to gracefully handle a panic and prevent the program from crashing (e.g., in servers, middleware)|

##### Panic

- **Function signature**: `panic(v interface{})`
- **Effect**:
    1. Stops function execution.
    2. Runs any `defer` statements.
    3. Propagates panic up the call stack.
    4. Crashes the program **if not recovered**.

```go
func main() {
    panic("something went wrong")
}
```

##### Recover

- **Function signature**: `recover() interface{}`
- Must be **called inside a deferred function** to catch the panic.
- If called outside `defer`, it returns `nil` and does nothing.

```go
func safe() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered from:", r)
        }
    }()
    panic("fail")
}
```

#####  Do not forget

- `panic` **executes all defers** before propagating.
- `recover` **only works inside deferred functions**.
- If no `recover` is present, panic will **crash the program**.
- Use `panic` for **bugs** or **non-recoverable errors**, **not for flow control**.
- `recover()` returns:
    - The panic value (if one exists)
    - `nil` otherwise

##### Internal Working

- Panic causes **stack unwinding**: deferred calls execute in **LIFO** order.
- Once recovered, execution resumes **after the `defer` block**.
- You can `re-panic` by calling `panic(r)` again inside the deferred function.

##### Bad practice

- **Don’t use panic/recover for regular error handling**.
- Prefer `error` values for expected failures.
- Use `panic` sparingly—only for truly exceptional cases.


# 3. Data Structures

## 3.1 Arrays & Slices

### Arrays

- Fixed-length sequence of elements of the **same type**.
- Stored **contiguously** in memory.

#### Key Properties:

- Length is part of the type: `[3]int` ≠ `[4]int`.
- Cannot be resized.
- Default zero values assigned on creation.
- Index starts at 0.
- Arrays are **value types** — copied on assignment, and independent data is created.

```go
package main

import "fmt"

func main() {

    // 1. Basic declaration with size
    var arr1 [5]int
    fmt.Println("1. var arr1 [5]int:", arr1) // [0 0 0 0 0]
    
    // 2. Declaration with initialization
    var arr2 [3]string = [3]string{"a", "b", "c"}
    fmt.Println("2. With initialization:", arr2)
    
    // 3. Short declaration with initialization
    arr3 := [4]int{1, 2, 3, 4}
    fmt.Println("3. Short declaration:", arr3)
    
    // 4. Array literal with ... (compiler counts length)
    arr4 := [...]int{10, 20, 30, 40, 50}
    fmt.Println("4. With ... (auto length):", arr4)
}
```

```go
a := [3]int{1, 2, 3}
b := a       // creates a copy
b[0] = 10    // a[0] still 1
```

### Slices

```go
type SliceHeader struct {
    Pointer uintptr // Pointer to the underlying array
    Len     int     // Current length of the underlying array
    Cap     int     // Total capacity, the maximum capacity to which the underlying array can expand
}
```

- A **dynamic, flexible view** over an array.
- Internally: a struct with:
    - Pointer to array
    - Length
    - Capacity

```go
slice := []int{1, 2, 3}
```

```go
package main

import "fmt"

func main() {
  
    // 8. Slice declaration (nil slice)
    var slice1 []int
    fmt.Println("8. var slice1 []int:", slice1, "len:", len(slice1)) // [] len: 0
    
    // 9. Slice literal
    slice2 := []int{1, 2, 3, 4, 5}
    fmt.Println("9. Slice literal:", slice2)
    
    // 10. Using make() - most common for dynamic slices
    slice3 := make([]int, 5) // length 5, capacity 5
    fmt.Println("10. make([]int, 5):", slice3) // [0 0 0 0 0]
    
    // 11. make() with length and capacity
    slice4 := make([]int, 3, 10) // length 3, capacity 10
    fmt.Println("11. make([]int, 3, 10):", slice4, "cap:", cap(slice4))
    
    // 12. Empty slice literal (not nil, but empty)
    slice5 := []int{}
    fmt.Println("12. Empty slice []int{}:", slice5, "len:", len(slice5))
    
    // 13. Slice from array
    arr8 := [5]int{1, 2, 3, 4, 5}
    slice6 := arr8[1:4] // indices 1, 2, 3
    fmt.Println("13. Slice from array:", slice6) // [2 3 4]
    
    // 14. Slice from slice
    slice7 := []int{10, 20, 30, 40, 50}
    slice8 := slice7[2:] // from index 2 to end
    fmt.Println("14. Slice from slice:", slice8) // [30 40 50]
    
    // 15. Full slice expression
    slice9 := slice7[:3] // from start to index 3 (exclusive)
    fmt.Println("15. Slice [:3]:", slice9) // [10 20 30]
    
    // 16. Copy of entire slice
    slice10 := slice7[:]
    fmt.Println("16. Copy slice [:]:", slice10)
    
    // 17. Using append (creates slice if needed)
    var slice11 []int
    slice11 = append(slice11, 1, 2, 3)
    fmt.Println("17. Using append:", slice11)
    
    // 18. Append another slice
    slice12 := []int{1, 2}
    slice13 := []int{3, 4, 5}
    slice12 = append(slice12, slice13...)
    fmt.Println("18. Append slice:", slice12) // [1 2 3 4 5]
    
    // 19. Multi-dimensional array
    matrix1 := [3][3]int{
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9},
    }
    fmt.Println("19. 2D array:", matrix1)
    
    // 20. Multi-dimensional slice
    matrix2 := [][]int{
        {1, 2, 3},
        {4, 5},
        {6, 7, 8, 9},
    }
    fmt.Println("20. 2D slice:", matrix2)
    
    // 21. Make 2D slice manually
    rows, cols := 3, 4
    matrix3 := make([][]int, rows)
    for i := range matrix3 {
        matrix3[i] = make([]int, cols)
    }
    fmt.Println("21. 2D with make:", matrix3)
    
    // 22. Slice with specific indices
    slice14 := []int{0: 10, 5: 50, 10: 100}
    fmt.Println("22. Slice specific indices:", slice14)
    
    // 23. Array of structs
    type Person struct {
        Name string
        Age  int
    }
    people := [2]Person{
        {"Alice", 25},
        {"Bob", 30},
    }
    fmt.Println("23. Array of structs:", people)
    
    // 24. Slice of structs
    peopleSlice := []Person{
        {Name: "Charlie", Age: 35},
        {Name: "Diana", Age: 28},
    }
    fmt.Println("24. Slice of structs:", peopleSlice)
    
    // 25. Using new() - returns pointer to array
    arr9 := new([5]int)
    fmt.Println("25. new([5]int):", arr9, "value:", *arr9)
    
    // ============================================
    // KEY DIFFERENCES
    // ============================================
    fmt.Println("\n=== KEY DIFFERENCES ===")
    
    // Array: fixed size, value type
    arrayExample := [3]int{1, 2, 3}
    fmt.Printf("Array type: %T, size: %d\n", arrayExample, len(arrayExample))
    
    // Slice: dynamic size, reference type
    sliceExample := []int{1, 2, 3}
    fmt.Printf("Slice type: %T, len: %d, cap: %d\n", 
        sliceExample, len(sliceExample), cap(sliceExample))
}
```

### **Key Properties**:

- **Variable length**
- Backed by an array
- Pass by value (but refers to same underlying array)

```go
func change(s []int) {
    s[0] = 99 // changes underlying array
}

func main() {
    a := []int{1, 2, 3}
    b := a         // copy of slice struct
    b[1] = 77      // affects 'a' too
    change(a)      // also affects 'a'
    fmt.Println(a) // [99 77 3]
}
```

```go
var a []int       // nil slice
b := []int{}      // empty but non-nil
```

- `nil` slice: `len=0`, `cap=0`, `pointer=nil`
- Empty slice: `len=0`, `cap=0`, `pointer≠nil`

### For Loops

```go
for i, v := range slice {
    // use i and v
}
```

### ``make()`` vs ``new()``

#### ``make()``

the `make()` function is used for initializing slices, maps, and channels – data structures that **==require runtime initialization==**. Unlike `new()`, `make()` returns an initialized (non-zeroed) value of a specified type

```go
package main

import "fmt"

func main() {
    // Using make() to create a slice with a specified length and capacity
    s := make([]int, 10, 15)

    // Initializing the elements
    for i := 0; i < 10; i++ {
        s[i] = i + 1
    }

    fmt.Println(s)
}
```

#### ``new()``

The `new()` function in Go is a built-in function that allocates memory for a new zeroed value of a specified type and returns a pointer to it. It is primarily used for initializing and obtaining a pointer to a newly allocated zeroed value of a given type

```go
package main

import "fmt"

type Person struct {
    Name     string
    Age      int
    Gender     string
}

func main() {
    // Using new() to allocate memory for a Person struct
    p := new(Person)

    // Initializing the fields
    p.Name = "John Doe"
    p.Age = 30
    p.Gender = "Male"

    fmt.Println(p)
}
```

When dealing with value types like structs, you can use `new()` to allocate memory for a new zeroed value. This is suitable for scenarios where you want a pointer to an initialized structure.

```go
p := new(Person)
```

### ``append()``, ``copy()``

#### ``append()``

The function appends any number of elements to the end of a slice
- if there is enough capacity, the underlying array is reused;
- if not, a new underlying array is allocated and the data is copied over.

Append **returns the updated slice**. Therefore you need to store the result of an append, often in the variable holding the slice itself:

```go
a := []int{1, 2}
a = append(a, 3, 4) // a == [1 2 3 4]
```

You can **concatenate two slices** using the three dots notation: 

```go
a := []int{1, 2}
b := []int{11, 22}
a = append(a, b...) // a == [1 2 11 22]
```

#### ``copy()``

copies elements into a destination slice `dst` from a source slice `src`.

```go
func copy(dst, src []Type) int
```

It returns the number of elements copied, which will be the **minimum** of `len(dst)` and `len(src)`. The result does not depend on whether the arguments overlap.

As a **special case**, it’s legal to copy bytes from a string to a slice of bytes.

```go
copy(dst []byte, src string) int
```

```go
var s = make([]int, 3)
n := copy(s, []int{0, 1, 2, 3}) // n == 3, s == []int{0, 1, 2}
```

```go
s := []int{0, 1, 2}
n := copy(s, s[1:]) // n == 2, s == []int{1, 2, 2}
```

```go
var b = make([]byte, 5)
copy(b, "Hello, world!") // b == []byte("Hello")
```

### Memory implications

Arrays in Go are **value types** - when you assign or pass them, the **entire array is copied**.

```go
func main() {
    arr1 := [1000000]int{1, 2, 3} // 1 million integers!
    
    arr2 := arr1 // ENTIRE array copied! (8MB of data copied)
    arr2[0] = 999
    
    fmt.Println(arr1[0]) // 1 (original unchanged)
    fmt.Println(arr2[0]) // 999
}
```

**Memory impact:**

- Each array copy takes memory equal to: `size × element_size`
- Large arrays = expensive copies
- Passing to functions copies entire array

Slices are **reference types** - they point to an underlying array. Copying a slice only copies the slice **header** (24 bytes), not the data.

```go
func main() {
    slice1 := make([]int, 1000000) // 1 million integers
    
    slice2 := slice1 // Only 24 bytes copied! (the header)
    slice2[0] = 999  // Modifies underlying array
    
    fmt.Println(slice1[0]) // 999 (both point to same array!)
    fmt.Println(slice2[0]) // 999
}
```

Multiple slices can share the same backing array:

````go
func main() {
    original := []int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
    
    slice1 := original[2:5] // [2, 3, 4]
    slice2 := original[4:7] // [4, 5, 6]
    
    // They share the same backing array!
    slice1[2] = 999 // Changes index 4 of original
    
    fmt.Println(original) // [0 1 2 3 999 5 6 7 8 9]
    fmt.Println(slice1)   // [2 3 999]
    fmt.Println(slice2)   // [999 5 6] - ALSO changed!
}
```

**Visual representation:**
```
original: [0][1][2][3][4][5][6][7][8][9]
                  ↑---------↑
                  slice1: len=3
                      ↑---------↑
                      slice2: len=3
````

When you `append()` beyond capacity, Go allocates a **new, larger array**:

```go
func main() {
    slice1 := make([]int, 3, 5) // len=3, cap=5
    fmt.Printf("Address: %p, len=%d, cap=%d\n", slice1, len(slice1), cap(slice1))
    // Address: 0xc000018030, len=3, cap=5
    
    slice1 = append(slice1, 4) // Still room
    fmt.Printf("Address: %p, len=%d, cap=%d\n", slice1, len(slice1), cap(slice1))
    // Address: 0xc000018030, len=4, cap=5 (same address)
    
    slice1 = append(slice1, 5) // Still room
    fmt.Printf("Address: %p, len=%d, cap=%d\n", slice1, len(slice1), cap(slice1))
    // Address: 0xc000018030, len=5, cap=5 (same address)
    
    slice1 = append(slice1, 6) // EXCEEDS capacity!
    fmt.Printf("Address: %p, len=%d, cap=%d\n", slice1, len(slice1), cap(slice1))
    // Address: 0xc000018050, len=6, cap=10 (NEW address, NEW array!)
}
```

|Aspect|Array|Slice|
|---|---|---|
|**Memory**|Stack (if small)|Header on stack, data on heap|
|**Copying**|Entire data copied|Only 24-byte header copied|
|**Size**|Fixed at compile time|Dynamic|
|**Passing to func**|Expensive (full copy)|Cheap (24 bytes)|
|**Memory leak risk**|No|Yes (if retaining large backing array)|

## 3.2 Maps

### Map creation & initialization

Maps are created with the built-in make function, just as for slices. The type for a map is specified using the map keyword, followed by the key type in square brackets, followed by the value type. The final argument to the make function specifies the initial capacity of the map

```go
map[KeyType]ValueType
```

```go
var m map[string]int                // nil map of string-int pairs

m1 := make(map[string]float64)      // Empty map of string-float64 pairs
m2 := make(map[string]float64, 100) // Preallocate room for 100 entries

m3 := map[string]float64{           // Map literal
    "e":  2.71828,
    "pi": 3.1416,
}
fmt.Println(len(m3))                // Size of map: 2
```

### CRUD operations

```go
m := make(map[string]float64)

m["pi"] = 3.14             // Add a new key-value pair
m["pi"] = 3.1416           // Update value
fmt.Println(m)             // Print map: "map[pi:3.1416]"

v := m["pi"]               // Get value: v == 3.1416
v = m["pie"]               // Not found: v == 0 (zero value)

_, found := m["pi"]        // found == true
_, found = m["pie"]        // found == false

if x, found := m["pi"]; found {
	fmt.Println(x)
}                           // Prints "3.1416"

delete(m, "pi")             // Delete a key-value pair
fmt.Println(m)              // Print map: "map[]"
```

- When you index a map you get two return values; the second one (which is optional) is a boolean that indicates if the key exists.
- If the key doesn’t exist, the first value will be the default zero value

### Checking existence

To check if a key exists in a map, use the two value assignment syntax.  The first value return is the existing value and the second value is a boolean type. The boolean type will return true if the key exists, or false otherwise.

```go
package main
 
import (
   "fmt"
)
 
func main() {
   users := map[string]int{
       "John":  21,
       "David": 43,
       "Paul":  54,
   }
 
   value, exist := users["John"]
 
   if exist {
       fmt.Printf("Found %d %v \n", value, exist)
   } else {
       fmt.Printf("Not found %d %v ", value, exist)
   }
}

```

## 3.3 Structs

a struct is a named collection of data fields that can be of different types. It serves as a container for different heterogeneous data types, representing an entity.

### Struct definition

```go
type struct_name struct {
    field_name1 field_type1
    field_name2 field_type2
    // ...
}

type Person struct { Name string Age int }

```

```go
// Value struct (named fields)
p := Person{Name: "Alice", Age: 30}
fmt.Println(p.Name)    // Acces

//Value struct (positional fields)
p := Person{"Bob", 25} 
fmt.Println(p.Name)

//Zero value with var
var p Person
fmt.Println(p.Name) // prints ""
fmt.Println(p.Age) // prints 0

//Pointer using address-of (&)
p := &Person{Name: "Dana", Age: 40}
fmt.Println(p.Name)    // Go auto-dereferences
fmt.Println((*p).Name) // Manual dereference

//Pointer using new()
p := new(Person)
p.Name = "Eve"
fmt.Println(p.Name)     // Auto-dereference
fmt.Println((*p).Name)  // Manual dereference

// Inside slices/arrays
people := []Person{{Name: "Frank", Age: 33}}
fmt.Println(people[0].Name)


```

|Creation Method|Type|Access Syntax|
|---|---|---|
|`Person{...}`|Value|`p.Name`|
|`var p Person`|Value|`p.Name`|
|`&Person{...}`|Pointer|`p.Name` or `(*p).Name`|
|`new(Person)`|Pointer|`p.Name` or `(*p).Name`|
|In slices/arrays|Value|`slice[i].Name`|

|Struct Type|Access Syntax|Notes|
|---|---|---|
|Value|`p.Name`|Direct field access|
|Pointer|`p.Name`|Auto-dereferenced|
|Pointer|`(*p).Name`|Manual dereference (optional)|

### Embedded Structs

Struct embedding in Go is a form of composition where one struct is included within another. Unlike traditional inheritance found in other programming languages, Go's embedding promotes the fields and methods of the embedded struct to the containing struct. This means that the outer struct can directly access the embedded struct's fields and methods as if they were its own.

```go
type Address struct {
    City    string
    Country string
}

type Person struct {
    Name    string
    Age     int
    Addr    Address  // Regular field with name "Addr"
}

func main() {
    p := Person{
        Name: "Alice",
        Age:  25,
        Addr: Address{City: "Istanbul", Country: "Turkey"},
    }
    
    fmt.Println(p.Addr.City) // Must use: p.Addr.City
}
```

```go
type Address struct {
    City    string
    Country string
}

type Person struct {
    Name    string
    Age     int
    Address // Embedded! No field name
}

func main() {
    p := Person{
        Name: "Alice",
        Age:  25,
        Address: Address{City: "Istanbul", Country: "Turkey"},
    }
    
    // Can access directly!
    fmt.Println(p.City)    // Direct access
    fmt.Println(p.Country) // Direct access
    
    // OR still use full path
    fmt.Println(p.Address.City) // Also works
}
```

With embedding, fields from the embedded struct become **accessible directly**:

**Use embedding when:**

- You want to "add" functionality from one struct to another
- Similar to inheritance in OOP (but it's composition!)
- You want direct access to fields/methods
- Building "has-a" relationships

### Anonymous Structs

**Anonymous struct** = a struct **without a type name**, defined on the spot.

```go

// Pattern:
variable := struct {
    field1 type1
    field2 type2
}{
    field1: value1,
    field2: value2,
}

func main() {
    // Define and use directly - no type name!
    p := struct {
        Name string
        Age  int
    }{
        Name: "Alice",
        Age:  25,
    }
    
    fmt.Println(p) // {Alice 25}
}
```

```go
func TestSomething(t *testing.T) {
    tests := []struct {
        input    int
        expected int
    }{
        {input: 2, expected: 4},
        {input: 3, expected: 9},
        {input: 4, expected: 16},
    }
    
    for _, test := range tests {
        result := square(test.input)
        if result != test.expected {
            t.Errorf("Expected %d, got %d", test.expected, result)
        }
    }
}

func square(n int) int {
    return n * n
}
```

```go
func TestAdd(t *testing.T) {
    testCases := []struct {
        name     string
        a        int
        b        int
        expected int
    }{
        {name: "positive numbers", a: 2, b: 3, expected: 5},
        {name: "negative numbers", a: -2, b: -3, expected: -5},
        {name: "mixed", a: 2, b: -3, expected: -1},
        {name: "zeros", a: 0, b: 0, expected: 0},
    }
    
    for _, tc := range testCases {
        t.Run(tc.name, func(t *testing.T) {
            result := add(tc.a, tc.b)
            if result != tc.expected {
                t.Errorf("add(%d, %d) = %d; want %d", 
                    tc.a, tc.b, result, tc.expected)
            }
        })
    }
}
```

==**Important:** Anonymous structs **cannot have methods**!==

### Struct tags (JSON, DB, validation)

tags allow developers to attach metadata to struct fields. These tags can drive features and behaviors in various libraries and tools which access the tags via reflection.

Go tags are attached to struct fields. The common convention is to structure your tags as key value pairs. A field may have more than one tag, and the value of a tag is a string.

```go
type Example struct {
	Field1 int    `tag1:"value1" tag2:"value2"`
    Field2 string `tag1:"value3,value4"`
}
```

#### JSON Tags

```go
type User struct {
    ID        int    `json:"id"`
    Name      string `json:"name"`
    Email     string `json:"email"`
    Password  string `json:"-"`              // Never in JSON
    Age       int    `json:"age,omitempty"`  // Omit if zero value
    IsActive  bool   `json:"is_active"`
}

func main() {
    user := User{ID: 1, Name: "Alice", Email: "alice@example.com"}
    
    data, _ := json.Marshal(user)
    fmt.Println(string(data))
    // {"id":1,"name":"Alice","email":"alice@example.com","is_active":false}
}
```

####  Database Tags

Used by ORMs (GORM, sqlx, etc.):

```go
type User struct {
    ID        int       `db:"id" gorm:"primaryKey"`
    Username  string    `db:"username" gorm:"unique;not null"`
    Email     string    `db:"email" gorm:"type:varchar(100);unique"`
    CreatedAt time.Time `db:"created_at" gorm:"autoCreateTime"`
    UpdatedAt time.Time `db:"updated_at" gorm:"autoUpdateTime"`
}
```

####  Validation Tags

Used by validation libraries (go-playground/validator):

```go
import "github.com/go-playground/validator/v10"

type User struct {
    Name     string `validate:"required,min=3,max=50"`
    Email    string `validate:"required,email"`
    Age      int    `validate:"required,gte=18,lte=100"`
    Password string `validate:"required,min=8"`
    Website  string `validate:"omitempty,url"`
}

func main() {
    validate := validator.New()
    
    user := User{
        Name:     "Al",  // Too short!
        Email:    "invalid-email",
        Age:      15,    // Too young!
        Password: "123", // Too short!
    }
    
    err := validate.Struct(user)
    if err != nil {
        fmt.Println(err)
    }
}
```

**Multiple Tags**

```go
type Product struct {
    ID          int     `json:"id" db:"id" gorm:"primaryKey"`
    Name        string  `json:"name" db:"name" validate:"required,min=3"`
    Price       float64 `json:"price" db:"price" validate:"required,gt=0"`
    Description string  `json:"description,omitempty" db:"description" validate:"max=500"`
    InStock     bool    `json:"in_stock" db:"in_stock"`
}
```

**Reading Tags**

```go
import "reflect"

type User struct {
    Name string `json:"username" validate:"required"`
}

func main() {
    t := reflect.TypeOf(User{})
    field, _ := t.FieldByName("Name")
    
    jsonTag := field.Tag.Get("json")      // "username"
    validateTag := field.Tag.Get("validate") // "required"
    
    fmt.Println(jsonTag, validateTag)
}
```

### Methods (value vs pointer receivers)

 a method is nothing but a function with a receiver. A receiver is an instance of a specific type, such as a struct or any other custom type.

```go
func (receiver receiver_type) some_func_name(arguments) return_values
```

- A method is defined with a receiver argument.
- Methods differ from functions in terms of functionality.
- Methods can be used for chaining on the receiver, and different methods can have the same name with a different receiver.

```go
type Rectangle struct {
    Width  float64
    Height float64
}

// Method attached to Rectangle
func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

func main() {
    rect := Rectangle{Width: 10, Height: 5}
    fmt.Println(rect.Area()) // 50
}
```

####  Value Receiver vs Pointer Receiver

#####  Value Receiver

Gets a **copy** of the struct - **cannot modify** original:

```go
type Counter struct {
    Count int
}

// Value receiver (c Counter)
func (c Counter) Increment() {
    c.Count++ // Modifies the COPY, not original!
}

func main() {
    counter := Counter{Count: 0}
    counter.Increment()
    fmt.Println(counter.Count) // 0 (unchanged!)
}
```

#####  Pointer Receiver

Gets a **reference** to the struct - **can modify** original:

```go
type Counter struct {
    Count int
}

// Pointer receiver (c *Counter)
func (c *Counter) Increment() {
    c.Count++ // Modifies the ORIGINAL!
}

func main() {
    counter := Counter{Count: 0}
    counter.Increment()
    fmt.Println(counter.Count) // 1 (modified!)
}
```


#### When to Use Pointer Receivers

- When changes to the receiver made inside the method need to be visible to the caller.
- When the struct is large to avoid making a copy of the struct every time a method is called.

#### Key Points

|Aspect|Value Receiver|Pointer Receiver|
|---|---|---|
|Syntax|`func (t Type)`|`func (t *Type)`|
|Modifies original?|❌ No|✅ Yes|
|Gets|Copy|Reference|
|Use when|Read-only, small|Modify, large|
|Memory|Copies data|Just pointer|

**Rule of thumb:** If you need to modify OR struct is large, use pointer (`*`). Otherwise, value is fine. 

# 4. Object-Oriented Go

## 4.1 Interfaces

- A type that specifies **a set of method signatures**.
- It lets different types be used **interchangeably**, if they implement those methods.

### Implicit implementation

- **Implicit implementation**: A type **automatically implements** an interface if it has all the methods.
- **No keyword like `implements` or `extends`** is needed.

In Go, a type **implements an interface implicitly**, not explicitly.

That means:

- A struct **doesn’t have to implement all interface methods** _unless_ you are **assigning the struct to a variable of that interface type**.

```go
type InterfaceName interface {
    Method1()
    Method2() string
}
```

```go
type Speaker interface {
    Speak() string
}

type Dog struct{}

func (d Dog) Speak() string {
    return "Woof"
}
```

In Go, **a type must implement _all_ methods of an interface** to satisfy it.

There is **no partial implementation**—unlike some languages, Go does **not support abstract base classes or partial interfaces**.
### Empty interface

- **Definition**: An interface with **no methods**.
- **All types implement it** (because it requires nothing).
- **Used for**:
    - Generic data containers (pre-generics)
    - Accepting any type in a function
    - Decoding unknown JSON structure


```go
func PrintAny(val interface{}) {
	fmt.Println(val)
}
```

### Type Assertions

**What:** Extract the concrete value from an interface.

**Why:** When you have `interface{}` or any interface, you need to access the actual underlying type.

 **Basic Syntax (Unsafe)**

```go
var x interface{} = 10
v := x.(int) // v == 10

// If wrong type → PANIC!
v := x.(string) // PANIC: interface conversion: interface {} is int, not string
```

 **Safe Version (Comma-OK Idiom)** 

```go
var x interface{} = 10

// Returns (value, bool)
v, ok := x.(int)
if ok {
    fmt.Println("It's an int:", v) // v == 10
} else {
    fmt.Println("Not an int")
}

// Or check in one line
if v, ok := x.(string); ok {
    fmt.Println("It's a string:", v)
}
```
### Type Switch

**What:** Handle multiple possible types in a clean way.

**Why:** Cleaner than multiple `if/else` type assertions.

 **Basic Syntax**

```go
func printType(val interface{}) {
    switch v := val.(type) {
    case int:
        fmt.Println("int:", v)
    case string:
        fmt.Println("string:", v)
    case bool:
        fmt.Println("bool:", v)
    default:
        fmt.Printf("unknown type: %T\n", v)
    }
}
```

 **Multiple Types per Case**

```go
func describe(val interface{}) {
    switch v := val.(type) {
    case int, int64, int32:
        fmt.Println("Some kind of int:", v)
    case string:
        fmt.Println("String length:", len(v))
    case []int:
        fmt.Println("Int slice length:", len(v))
    case nil:
        fmt.Println("It's nil!")
    default:
        fmt.Printf("Unknown: %T\n", v)
    }
}
```


 **Type Assertion vs Type Switch**

|Feature|Type Assertion|Type Switch|
|---|---|---|
|**Use case**|Check 1-2 types|Check multiple types|
|**Syntax**|`val.(Type)`|`val.(type)`|
|**Safety**|Use comma-ok|Built-in safety|
|**When**|Know expected type|Multiple possibilities|

## 4.2 Generics

### Type parameters

> **Type parameters** = writing functions/structs that work with **any type**, not just one specific type.

**Old Problematic**

```go
// For integers
func MaxInt(a, b int) int {
    if a > b {
        return a
    }
    return b
}

// For floats
func MaxFloat(a, b float64) float64 {
    if a > b {
        return a
    }
    return b
}

// For strings
func MaxString(a, b string) string {
    if a > b {
        return a
    }
    return b
}
```

**New Solution**

```go
// [T comparable] = type parameter
func Max[T comparable](a, b T) T {
    if a > b {
        return a
    }
    return b
}

func main() {
    fmt.Println(Max(10, 20))       // 20 (int)
    fmt.Println(Max(3.14, 2.71))   // 3.14 (float64)
    fmt.Println(Max("apple", "banana")) // "banana" (string)
}
```

```go
func FunctionName[T TypeConstraint](param T) T {
    // function body
}
```

- `[T TypeConstraint]` = type parameter declaration
- `T` = the type parameter (like a variable for types)
- `TypeConstraint` = what types T can be

###  Type Constraints

> **Type constraints** = rules that define what types are allowed for a type parameter.

#### Built-in Constraints

##### 1. `any` - No restrictions

```go
func Print[T any](val T) {
    fmt.Println(val)
}

// Works with ANY type
Print(42)
Print("hello")
Print([]int{1, 2, 3})
Print(struct{}{})
```

##### 2. `comparable` - Can use `==` and `!=`

```go
func Equal[T comparable](a, b T) bool {
    return a == b
}

Equal(10, 10)           // true
Equal("hi", "bye")      // false
Equal(3.14, 3.14)       // true
// Equal([]int{}, []int{}) // ERROR: slices not comparable
```

#### Custom Constraints 

##### Union Types (Type Sets)

Use `|` to allow specific types:

```go
// Only int OR float64
type Number interface {
    int | float64
}

func Add[T Number](a, b T) T {
    return a + b
}

Add(10, 20)      // ✅ Works (int)
Add(3.14, 2.86)  // ✅ Works (float64)
// Add("a", "b") // ❌ ERROR: string not allowed
```

```go
type Integer interface {
    int | int8 | int16 | int32 | int64
}

func Sum[T Integer](numbers []T) T {
    var total T
    for _, n := range numbers {
        total += n
    }
    return total
}
```

##### Approximation Constraint (~)


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

 the `Compare` function can correctly compare values of types like `Integer`, `Str`, and `Double`. The underlying operator (~) provides flexibility in working with underlying types, enhancing the capabilities of generics in Go.

# 5. Pointers & Memory

## 5.1 Pointers

==_**Pointers in Golang are utilized to enhance performance and flexibility by avoiding unnecessary copies of data and enabling efficient data structures and function calls.**_==

### Pointer basics

```go
var p *<type> [= expression]
```

- A pointer stores the **memory address** of a variable.
- Syntax: `var ptr *int` means `ptr` is a pointer to an `int`.
- You use `&` to get the address, and to dereference (access the value at the address).

```go
var x int = 10
var p *int = &x   // p stores the address of x
fmt.Println(*p)   // dereference: prints 10
*p = 20           // updates x to 20
```

**About `*` or Dereferencing Pointer**

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

**Pointer to a Pointer**

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

### Pointer receivers vs value receivers

```go
// Value receiver - gets a COPY
func (t Type) Method() {}

// Pointer receiver - gets a REFERENCE
func (t *Type) Method() {}
```

**Key Difference**

```go
type Counter struct {
    Count int
}

// Value receiver - CANNOT modify original
func (c Counter) IncrementValue() {
    c.Count++ // Modifies the COPY only
}

// Pointer receiver - CAN modify original
func (c *Counter) IncrementPointer() {
    c.Count++ // Modifies the ORIGINAL
}

func main() {
    counter := Counter{Count: 0}
    
    counter.IncrementValue()   // Count still 0
    fmt.Println(counter.Count) // 0
    
    counter.IncrementPointer() // Count changed!
    fmt.Println(counter.Count) // 1
}
```

 **Quick Decision**

|Need to modify?|Struct size|Use|
|---|---|---|
|Yes|Any|`*Type`|
|No|Large|`*Type`|
|No|Small|`Type`|

**Rule of thumb:** When in doubt, use `*Type`

###  Nil pointers

"points to nothing
```go
var p *int        // p is nil (points to nothing)
fmt.Println(p)    // <nil>
fmt.Println(p == nil) // true
```

```go
var p *int
fmt.Println(*p) // PANIC: invalid memory address or nil pointer dereference
```

```go
var p *int

// Always check for nil before dereferencing
if p != nil {
    fmt.Println(*p) // Safe
} else {
    fmt.Println("Pointer is nil")
}
```


###  Common Use-Cases

- Mutating function parameters.
- Efficient passing of large structs.
- Shared state between functions.
- Managing optional values (`nil` as a signal).
- Dependency injection in applications.

# 6. Error Handling

## 6.1 Error Patterns

- In Go, errors are **values**.
- Represented using the built-in `error` **interface**:

```go
type error interface {
    Error() string
}
```

Any type implementing the Error() string method becomes an  error  .

### Creating an Error

 **Using `errors.New`**

```go
import "errors"

err := errors.New("something went wrong")

```

 **Using `fmt.Errorf` (for formatted errors)**

```go
import "fmt"

err := fmt.Errorf("error code %d: %s", 404, "not found")

```

### Returning Errors From Functions

```go
func divide(a, b int) (int, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}
```

```go
result, err := divide(10, 0)
if err != nil {
    fmt.Println("Error:", err)
} else {
    fmt.Println("Result:", result)
}
```

### Custom error types

```go
type MyError struct {
    Code int
    Msg  string
}

func (e MyError) Error() string {
    return fmt.Sprintf("Code %d: %s", e.Code, e.Msg)
}
```

### Error wrapping (Go 1.13+)

Add context to errors:

```go
import "fmt"

err := someFunc()
if err != nil {
    return fmt.Errorf("operation failed: %w", err)
}
```

- `%w` wraps the original error for later unwrapping.

### ``errors.Is()`` & ``errors.As()``

#### `Is()` function

The standard library offers `errors.Is()` to traverse wrapped errors. It walks the error tree and returns `true` if any error in the chain matches the **target error value**:

```go
err := fileChecker("not_here.txt")  
if errors.Is(err, os.ErrNotExist) {  
    fmt.Println("That file doesn't exist")  
}
```

> Use `errors.Is` _when you care about_ **_a specific error instance or value_** _(e.g., sentinel errors)._

#### `As()` function

While `errors.Is` checks values, `errors.As` finds the **first error of a specific type** in the error tree.

```go
var myErr MyErr  
if errors.As(err, &myErr) {  
	fmt.Println("Got custom error with codes:", myErr.Codes)  
}
```

You must pass a **pointer** to a variable of the desired type. If a match is found, `errors.As()` assigns the matching error into that pointer.

> _Use_ `errors.As` _when you're trying to extract a_ **_specific error type_** _from a wrapped chain._


# 7. Standard Library Essentials 

## 7.1 I/O & Files

### io Package Interfaces

The `io` package defines fundamental interfaces for I/O operations that are implemented throughout Go's standard library:

```go
import "io"

// Core interfaces
type Reader interface {
    Read([]byte) (n int, err error)
}

type Writer interface {
    Write([]byte) (n int, err error)
}

type Closer interface {
    Close() error
}

// Combined interfaces
type ReadWriter interface { Reader; Writer }
type ReadCloser interface { Reader; Closer }
type WriteCloser interface { Writer; Closer }
type ReadWriteCloser interface { Reader; Writer; Closer }

// Common io functions
data, err := io.ReadAll(reader)              // Read everything into []byte
n, err := io.Copy(dst, src)                  // Copy from reader to writer
n, err := io.CopyN(dst, src, 1024)          // Copy exactly N bytes
n, err := io.WriteString(w, "hello")        // Write string to writer

// Useful utilities
reader := io.LimitReader(r, 1024)            // Limit reading to N bytes
reader = io.TeeReader(r, w)                  // Read from r, write to w simultaneously
writer := io.MultiWriter(w1, w2, w3)         // Write to multiple writers at once
```

### bufio for Buffered I/O

Buffered I/O significantly improves performance by reducing system calls:

```go
import "bufio"

// Buffered reading
file, err := os.Open("data.txt")
if err != nil {
    return err
}
defer file.Close()

// Create buffered reader (default 4KB buffer)
reader := bufio.NewReader(file)
// Or with custom size
reader = bufio.NewReaderSize(file, 16*1024)  // 16KB buffer

// Read line by line
for {
    line, err := reader.ReadString('\n')     // Read until delimiter
    if err == io.EOF {
        break
    }
    if err != nil {
        return err
    }
    fmt.Print(line)
}

// Alternative: ReadBytes
bytes, err := reader.ReadBytes('\n')         // Returns []byte instead of string

// Peek without consuming
peeked, err := reader.Peek(10)              // Look ahead 10 bytes

// Scanner for convenient iteration
scanner := bufio.NewScanner(file)
scanner.Split(bufio.ScanLines)              // Default, can also use ScanWords, ScanBytes
for scanner.Scan() {
    line := scanner.Text()                   // or scanner.Bytes()
    fmt.Println(line)
}
if err := scanner.Err(); err != nil {
    return err
}

// Buffered writing
outFile, _ := os.Create("output.txt")
defer outFile.Close()

writer := bufio.NewWriter(outFile)
writer.WriteString("Hello, ")
writer.WriteString("World!\n")
writer.Flush()  // IMPORTANT: Always flush buffered writers!

// Or use defer to ensure flush
defer writer.Flush()
```

### os Package for File Operations

The `os` package provides platform-independent file and directory operations:

```go
import "os"

// Opening files
file, err := os.Open("file.txt")            // Read-only
file, err = os.Create("new.txt")            // Create/truncate for writing
file, err = os.OpenFile("data.txt",         // Full control
    os.O_RDWR|os.O_CREATE|os.O_APPEND, 
    644)  // Unix permissions
defer file.Close()

// File flags for OpenFile
// os.O_RDONLY, os.O_WRONLY, os.O_RDWR    - Access modes
// os.O_CREATE                              - Create if doesn't exist
// os.O_EXCL                                - Fail if exists (with O_CREATE)
// os.O_APPEND                              - Append mode
// os.O_TRUNC                               - Truncate when opening
// os.O_SYNC                                - Synchronous I/O

// Reading entire file (simple but loads all in memory)
data, err := os.ReadFile("config.json")     // Returns []byte

// Writing entire file
err = os.WriteFile("output.txt", []byte("data"), 0644)

// File operations
info, err := file.Stat()                    // Get FileInfo
size := info.Size()                         // File size in bytes
modTime := info.ModTime()                   // Last modification time
isDir := info.IsDir()                       // Is directory?

// Seeking in files
newPos, err := file.Seek(0, io.SeekStart)   // Beginning
newPos, err = file.Seek(0, io.SeekEnd)      // End
newPos, err = file.Seek(-10, io.SeekCurrent) // Current position - 10

// File system operations
err = os.Rename("old.txt", "new.txt")       // Rename/move
err = os.Remove("file.txt")                 // Delete file
err = os.RemoveAll("directory")             // Delete directory recursively

// Directory operations
err = os.Mkdir("newdir", 0755)              // Create directory
err = os.MkdirAll("path/to/dir", 0755)      // Create with parents

// List directory contents
entries, err := os.ReadDir(".")             // Returns []DirEntry
for _, entry := range entries {
    info, _ := entry.Info()
    fmt.Printf("%s %d bytes\n", entry.Name(), info.Size())
}

// Working directory
cwd, err := os.Getwd()                      // Get current directory
err = os.Chdir("/new/path")                 // Change directory

// Environment variables
value := os.Getenv("HOME")
os.Setenv("MY_VAR", "value")
os.Unsetenv("MY_VAR")
allEnv := os.Environ()                      // All env vars as []string

// Temporary files and directories
tmpFile, err := os.CreateTemp("", "prefix-*.txt")
defer os.Remove(tmpFile.Name())             // Clean up
tmpDir, err := os.MkdirTemp("", "prefix-")
defer os.RemoveAll(tmpDir)
```

### filepath Package for Path Manipulation

Platform-independent path operations:

```go
import "path/filepath"

// Join paths correctly for OS
path := filepath.Join("dir", "subdir", "file.txt")  // dir/subdir/file.txt (Unix)
                                                     // dir\subdir\file.txt (Windows)

// Split path components
dir := filepath.Dir("/path/to/file.txt")            // "/path/to"
base := filepath.Base("/path/to/file.txt")          // "file.txt"
ext := filepath.Ext("file.txt")                     // ".txt"
dir, file := filepath.Split("/path/to/file.txt")    // "/path/to/", "file.txt"

// Clean paths
cleaned := filepath.Clean("./a/b/../c/")            // "a/c"

// Absolute paths
abs, err := filepath.Abs("relative/path")           // Convert to absolute
isAbs := filepath.IsAbs("/path")                    // Check if absolute

// Relative paths
rel, err := filepath.Rel("/a/b", "/a/b/c/d")       // "c/d"

// Pattern matching (globbing)
matches, err := filepath.Glob("*.go")               // All .go files
matches, err = filepath.Glob("**/*.go")             // Recursive (if supported)

// Walk directory tree
err = filepath.Walk(".", func(path string, info os.FileInfo, err error) error {
    if err != nil {
        return err  // Handle access errors
    }
    if info.IsDir() {
        if info.Name() == ".git" {
            return filepath.SkipDir  // Skip this directory
        }
        return nil
    }
    // Process file
    fmt.Println(path, info.Size())
    return nil
})

// More efficient WalkDir (Go 1.16+)
filepath.WalkDir(".", func(path string, d fs.DirEntry, err error) error {
    if err != nil {
        return err
    }
    if !d.IsDir() && filepath.Ext(path) == ".go" {
        fmt.Println(path)
    }
    return nil
})

// Match patterns
matched, err := filepath.Match("*.go", "main.go")  // true
```

### Real-World Examples

#### Safe File Writing with Atomic Replace

```go
// Write to temp file first, then rename (atomic on most systems)
func SafeWriteFile(filename string, data []byte) error {
    tempFile := filename + ".tmp"
    
    // Write to temporary file
    if err := os.WriteFile(tempFile, data, 0644); err != nil {
        return err
    }
    
    // Atomic rename
    return os.Rename(tempFile, filename)
}
```

#### Configuration File Reader with Multiple Locations

```go
func LoadConfig() ([]byte, error) {
    // Try multiple locations in order
    locations := []string{
        "./config.json",
        filepath.Join(os.Getenv("HOME"), ".myapp", "config.json"),
        "/etc/myapp/config.json",
    }
    
    for _, path := range locations {
        if data, err := os.ReadFile(path); err == nil {
            return data, nil
        }
    }
    
    return nil, fmt.Errorf("config not found")
}
```

#### Efficient Large File Processing

```go
func ProcessLargeFile(filename string) error {
    file, err := os.Open(filename)
    if err != nil {
        return err
    }
    defer file.Close()
    
    scanner := bufio.NewScanner(file)
    // Set max token size if needed (default 64KB)
    buf := make([]byte, 0, 64*1024)
    scanner.Buffer(buf, 1024*1024)  // Max 1MB per line
    
    lineNum := 0
    for scanner.Scan() {
        lineNum++
        line := scanner.Text()
        
        // Process line
        if err := processLine(line); err != nil {
            return fmt.Errorf("line %d: %w", lineNum, err)
        }
    }
    
    return scanner.Err()
}
```

#### Copy File with Progress

```go
func CopyFileWithProgress(src, dst string) error {
    sourceFile, err := os.Open(src)
    if err != nil {
        return err
    }
    defer sourceFile.Close()
    
    // Get file size for progress
    sourceInfo, err := sourceFile.Stat()
    if err != nil {
        return err
    }
    
    destFile, err := os.Create(dst)
    if err != nil {
        return err
    }
    defer destFile.Close()
    
    // Create progress reader
    progressReader := &ProgressReader{
        Reader: sourceFile,
        Total:  sourceInfo.Size(),
    }
    
    _, err = io.Copy(destFile, progressReader)
    return err
}

type ProgressReader struct {
    io.Reader
    Total   int64
    Current int64
}

func (pr *ProgressReader) Read(p []byte) (int, error) {
    n, err := pr.Reader.Read(p)
    pr.Current += int64(n)
    
    // Print progress
    percentage := float64(pr.Current) / float64(pr.Total) * 100
    fmt.Printf("\rProgress: %.2f%%", percentage)
    
    return n, err
}
```

#### Directory Watcher Pattern

```go
func WatchDirectory(dir string, action func(string)) error {
    initialFiles := make(map[string]time.Time)
    
    // Get initial state
    err := filepath.Walk(dir, func(path string, info os.FileInfo, err error) error {
        if err == nil && !info.IsDir() {
            initialFiles[path] = info.ModTime()
        }
        return nil
    })
    if err != nil {
        return err
    }
    
    // Poll for changes
    ticker := time.NewTicker(1 * time.Second)
    defer ticker.Stop()
    
    for range ticker.C {
        filepath.Walk(dir, func(path string, info os.FileInfo, err error) error {
            if err != nil || info.IsDir() {
                return nil
            }
            
            if oldTime, exists := initialFiles[path]; !exists || oldTime != info.ModTime() {
                action(path)
                initialFiles[path] = info.ModTime()
            }
            return nil
        })
    }
    
    return nil
}
```

### Best Practices

1. **Always handle errors properly**

```go
// Don't ignore errors
data, _ := os.ReadFile("file.txt")  // BAD

// Do this instead
data, err := os.ReadFile("file.txt")
if err != nil {
    return fmt.Errorf("reading file: %w", err)
}
```

2. **Use defer for cleanup**

```go
file, err := os.Open("file.txt")
if err != nil {
    return err
}
defer file.Close()  // Guaranteed to run
```

3. **Buffer I/O for performance**

```go
// Slow: many system calls
file.Write([]byte("a"))
file.Write([]byte("b"))

// Fast: buffered writes
writer := bufio.NewWriter(file)
writer.WriteString("a")
writer.WriteString("b")
writer.Flush()
```

4. **Check for specific errors**

```go
if errors.Is(err, os.ErrNotExist) {
    // File doesn't exist
}
if errors.Is(err, os.ErrPermission) {
    // Permission denied
}
```

5. **Use io.Reader/Writer interfaces**

```go
// Good: accepts any reader
func ProcessData(r io.Reader) error { ... }

// Limited: only works with files
func ProcessData(f *os.File) error { ... }
```

**Key Points:**

- io.Reader/Writer are the foundation of Go's I/O
- Always close files and flush buffered writers
- Use bufio for line-by-line reading or when doing many small reads/writes
- filepath package handles OS-specific path separators automatically
- os.ReadFile/WriteFile for simple cases, streaming for large files
- Error wrapping with %w preserves error chain for errors.Is()

## 7.2 String Manipulation

### strings Package

The `strings` package provides essential functions for string manipulation:

```go
import "strings"

// Basic operations
s := "Hello, World!"
strings.Contains(s, "World")        // true
strings.HasPrefix(s, "Hello")       // true
strings.HasSuffix(s, "!")           // true
strings.Index(s, "World")           // 7
strings.Count(s, "l")               // 3

// Transformation
strings.ToUpper(s)                  // "HELLO, WORLD!"
strings.ToLower(s)                  // "hello, world!"
strings.TrimSpace("  hello  ")      // "hello"
strings.Trim("!!hello!!", "!")      // "hello"
strings.Replace(s, "World", "Go", 1) // "Hello, Go!"
strings.ReplaceAll(s, "l", "L")     // "HeLLo, WorLd!"

// Splitting and joining
parts := strings.Split("a-b-c", "-")     // []string{"a", "b", "c"}
strings.Join(parts, ":")                  // "a:b:c"
strings.Fields("  a   b  c  ")           // []string{"a", "b", "c"}

// Builder for efficient concatenation
var builder strings.Builder
builder.WriteString("Hello")
builder.WriteString(" ")
builder.WriteString("World")
result := builder.String()  // "Hello World"
```

### strconv Package

The `strconv` package handles conversions between strings and other types:

```go
import "strconv"

// String to number
i, err := strconv.Atoi("123")           // int: 123
f, err := strconv.ParseFloat("3.14", 64) // float64: 3.14
b, err := strconv.ParseBool("true")      // bool: true
n, err := strconv.ParseInt("42", 10, 64) // int64: 42 (base 10)

// Number to string
s1 := strconv.Itoa(123)                  // "123"
s2 := strconv.FormatFloat(3.14, 'f', 2, 64) // "3.14"
s3 := strconv.FormatBool(true)           // "true"
s4 := strconv.FormatInt(42, 10)          // "42" (base 10)

// Quote operations
quoted := strconv.Quote("Hello\nWorld")   // "\"Hello\\nWorld\""
unquoted, err := strconv.Unquote(`"test"`) // "test"
```

### regexp Package

Regular expressions for pattern matching:

```go
import "regexp"

// Compile patterns
re := regexp.MustCompile(`\d+`)  // panics on error
re2, err := regexp.Compile(`[a-z]+`)  // returns error

// Matching
matched := re.MatchString("abc123")  // true
found := re.FindString("abc123def")  // "123"
allFound := re.FindAllString("a1b2c3", -1) // ["1", "2", "3"]

// Replacing
result := re.ReplaceAllString("a1b2c3", "X")  // "aXbXcX"
result2 := re.ReplaceAllStringFunc("a1b2c3", func(s string) string {
    n, _ := strconv.Atoi(s)
    return strconv.Itoa(n * 2)
})  // "a2b4c6"

// Submatches (groups)
re3 := regexp.MustCompile(`(\w+)@(\w+\.\w+)`)
matches := re3.FindStringSubmatch("john@example.com")
// ["john@example.com", "john", "example.com"]
```

### Text Templates

The `text/template` package for dynamic text generation:

```go
import (
    "text/template"
    "bytes"
)

// Define template
const tmplText = `
Name: {{.Name}}
Age: {{.Age}}
{{if .IsActive}}Status: Active{{else}}Status: Inactive{{end}}
Skills:
{{range .Skills}}- {{.}}
{{end}}`

// Parse and execute
type Person struct {
    Name     string
    Age      int
    IsActive bool
    Skills   []string
}

tmpl, err := template.New("person").Parse(tmplText)
if err != nil {
    panic(err)
}

person := Person{
    Name:     "Alice",
    Age:      30,
    IsActive: true,
    Skills:   []string{"Go", "Python", "Docker"},
}

var buf bytes.Buffer
err = tmpl.Execute(&buf, person)
result := buf.String()

// Template functions
funcMap := template.FuncMap{
    "upper": strings.ToUpper,
    "add": func(a, b int) int { return a + b },
}

tmpl2 := template.Must(template.New("test").Funcs(funcMap).Parse(
    `{{upper .Name}} is {{add .Age 5}} in 5 years`,
))
```

**Key Points:**

- Use `strings.Builder` for efficient string concatenation
- Always handle errors from `strconv` conversions
- `regexp.MustCompile` for compile-time patterns, `Compile` for runtime
- Templates support conditionals, loops, and custom functions

## 7.3 Time & Date

### ``time.Time`` & ``time.Duration``

The `time` package handles dates, times, and durations with nanosecond precision:

```go
import "time"

// Current time
now := time.Now()                    // Local time
utcNow := time.Now().UTC()          // UTC time

// Create specific time
t := time.Date(2025, time.August, 15, 14, 30, 0, 0, time.UTC)
// year, month, day, hour, min, sec, nanosec, location

// Extract components
year := t.Year()                     // 2025
month := t.Month()                   // time.August
day := t.Day()                       // 15
weekday := t.Weekday()              // time.Friday

// Duration type (int64 nanoseconds)
duration := 2*time.Hour + 30*time.Minute
future := now.Add(duration)         // Add duration to time
past := now.Add(-24 * time.Hour)    // Subtract duration

// Calculate difference
diff := future.Sub(now)             // Returns time.Duration
hoursSince := time.Since(past)      // Convenience for time.Now().Sub(past)
hoursUntil := time.Until(future)    // Convenience for future.Sub(time.Now())

// Comparisons
if t.Before(now) {                  // Also: After(), Equal()
    fmt.Println("t is in the past")
}
```

### Timers & Tickers

Control time-based execution:

```go
// Timer - fires once after delay
timer := time.NewTimer(5 * time.Second)
<-timer.C  // Blocks until timer fires
timer.Stop()  // Cancel if needed

// AfterFunc - execute function after delay
time.AfterFunc(2*time.Second, func() {
    fmt.Println("Executed after 2 seconds")
})

// Ticker - fires repeatedly  
ticker := time.NewTicker(1 * time.Second)
go func() {
    for t := range ticker.C {
        fmt.Println("Tick at", t)
    }
}()
time.Sleep(5 * time.Second)
ticker.Stop()  // Important: always stop when done!

// Simple timeout pattern
select {
case result := <-ch:
    fmt.Println("Got result:", result)
case <-time.After(3 * time.Second):  // Creates timer internally
    fmt.Println("Timeout!")
}
```

### Time Zones

Working with different locations:

```go
// Load location
loc, err := time.LoadLocation("America/New_York")
if err != nil {
    panic(err)
}

// Create time in specific zone
nyTime := time.Date(2025, 8, 15, 14, 30, 0, 0, loc)

// Convert between zones
utcTime := nyTime.UTC()                    // Convert to UTC
localTime := nyTime.Local()                // Convert to system local
tokyoLoc, _ := time.LoadLocation("Asia/Tokyo")
tokyoTime := nyTime.In(tokyoLoc)          // Convert to any zone

// Fixed zone (when you know offset)
ist := time.FixedZone("IST", 5*3600+1800)  // +05:30
indianTime := now.In(ist)

// Unix timestamps (always UTC)
unix := now.Unix()                         // Seconds since epoch
unixNano := now.UnixNano()                // Nanoseconds since epoch
fromUnix := time.Unix(unix, 0)            // Reconstruct from Unix time
```

### Parsing & Formatting

Go uses a unique reference time for formatting: `Mon Jan 2 15:04:05 MST 2006`

```go
// Formatting (Time to String)
t := time.Now()
fmt.Println(t.Format("2006-01-02"))              // "2025-08-15"
fmt.Println(t.Format("15:04:05"))                // "14:30:00"
fmt.Println(t.Format("Jan 2, 2006 3:04 PM"))     // "Aug 15, 2025 2:30 PM"
fmt.Println(t.Format(time.RFC3339))              // ISO 8601 format

// Common predefined formats
time.RFC3339     // "2006-01-02T15:04:05Z07:00"
time.Kitchen     // "3:04PM"
time.Stamp       // "Jan _2 15:04:05"

// Parsing (String to Time)
str := "2025-08-15 14:30:00"
parsed, err := time.Parse("2006-01-02 15:04:05", str)  // Assumes UTC!

// ParseInLocation - specify timezone
loc, _ := time.LoadLocation("Asia/Kolkata")
localParsed, err := time.ParseInLocation(
    "2006-01-02 15:04:05", 
    str, 
    loc,  // Uses this location instead of UTC
)

// Important format components to remember!
// 2006 → Year       01 → Month         02 → Day
// 15 → Hour(24h)    03 → Hour(12h)     04 → Minute
// 05 → Second       PM → AM/PM         Mon → Weekday
// Jan → Month name  MST → Timezone     -0700 → Offset
```

### Practical Examples

```go
// Calculate age
birthdate := time.Date(1990, 5, 15, 0, 0, 0, 0, time.UTC)
age := int(time.Since(birthdate).Hours() / 24 / 365.25)

// Start of day
now := time.Now()
startOfDay := time.Date(now.Year(), now.Month(), now.Day(), 
                        0, 0, 0, 0, now.Location())

// Truncate to hour (rounds down)
truncated := now.Truncate(time.Hour)  // 14:30:45 → 14:00:00

// Round to nearest hour  
rounded := now.Round(time.Hour)       // 14:30:45 → 15:00:00

// Measure execution time
start := time.Now()
// ... some operation ...
elapsed := time.Since(start)
fmt.Printf("Operation took %v\n", elapsed)
```

**Key Points:**

- Always use `ParseInLocation` when time zone matters - `Parse` assumes UTC!
- The format string MUST use the reference time `2006-01-02 15:04:05`
- Store times in UTC in databases, convert to local only for display
- Remember to `Stop()` tickers to prevent goroutine leaks
- `time.Duration` max is ~290 years (int64 nanoseconds limit)

