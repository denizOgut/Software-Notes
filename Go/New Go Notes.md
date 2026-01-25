
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

## 7.4 Encoding

### JSON Marshaling/Unmarshaling

JSON is the most common data interchange format in Go:

```go
import "encoding/json"

// Basic struct for JSON
type Person struct {
    Name     string    `json:"name"`
    Age      int       `json:"age"`
    Email    string    `json:"email,omitempty"`    // Omit if empty
    Password string    `json:"-"`                   // Never include
    IsActive bool      `json:"is_active"`
    Tags     []string  `json:"tags"`
    Metadata map[string]interface{} `json:"metadata"`
}

// Marshaling (Go to JSON)
person := Person{
    Name:     "Alice",
    Age:      30,
    Email:    "alice@example.com",
    Password: "secret",  // Won't be included in JSON
    IsActive: true,
    Tags:     []string{"developer", "golang"},
    Metadata: map[string]interface{}{
        "level": "senior",
        "years": 5,
    },
}

// Marshal to bytes
data, err := json.Marshal(person)
if err != nil {
    return err
}
// Output: {"name":"Alice","age":30,"email":"alice@example.com","is_active":true,...}

// Marshal with indentation (pretty print)
prettyData, err := json.MarshalIndent(person, "", "  ")

// Unmarshaling (JSON to Go)
jsonStr := `{"name":"Bob","age":25,"is_active":false,"tags":["junior"]}`
var p Person
err = json.Unmarshal([]byte(jsonStr), &p)
if err != nil {
    return err
}

// Partial unmarshaling with json.RawMessage
type Message struct {
    Type string          `json:"type"`
    Data json.RawMessage `json:"data"`  // Delay parsing
}

msg := `{"type":"user","data":{"id":1,"name":"Alice"}}`
var m Message
json.Unmarshal([]byte(msg), &m)

// Parse Data based on Type
switch m.Type {
case "user":
    var user User
    json.Unmarshal(m.Data, &user)
case "product":
    var product Product
    json.Unmarshal(m.Data, &product)
}

// Working with unknown structure
var result map[string]interface{}
json.Unmarshal([]byte(jsonStr), &result)
name := result["name"].(string)  // Type assertion needed

// Or use interface{} for completely dynamic JSON
var anything interface{}
json.Unmarshal([]byte(jsonStr), &anything)

// Streaming JSON (for large files or HTTP responses)
decoder := json.NewDecoder(reader)  // io.Reader
encoder := json.NewEncoder(writer)  // io.Writer

// Read JSON stream
var person Person
err = decoder.Decode(&person)

// Write JSON stream
err = encoder.Encode(person)

// Handle multiple JSON objects in stream
for {
    var p Person
    if err := decoder.Decode(&p); err == io.EOF {
        break
    } else if err != nil {
        return err
    }
    // Process person
}
```

### XML Handling

Similar to JSON but with more control over structure:

```go
import "encoding/xml"

type Book struct {
    XMLName xml.Name `xml:"book"`
    ID      string   `xml:"id,attr"`        // XML attribute
    Title   string   `xml:"title"`
    Author  Author   `xml:"author"`
    Pages   int      `xml:"pages"`
    Inner   string   `xml:",innerxml"`      // Raw inner XML
    Comment string   `xml:",comment"`       // XML comment
}

type Author struct {
    Name  string `xml:"name"`
    Email string `xml:"email,omitempty"`
}

// Marshal to XML
book := Book{
    ID:    "123",
    Title: "Go Programming",
    Author: Author{
        Name:  "John Doe",
        Email: "john@example.com",
    },
    Pages: 300,
}

xmlData, err := xml.Marshal(book)
// Add XML header
xmlWithHeader := xml.Header + string(xmlData)

// Pretty printed XML
prettyXML, err := xml.MarshalIndent(book, "", "  ")

// Unmarshal XML
xmlStr := `
<book id="123">
    <title>Go Programming</title>
    <author>
        <name>John Doe</name>
    </author>
    <pages>300</pages>
</book>`

var b Book
err = xml.Unmarshal([]byte(xmlStr), &b)

// Streaming XML parsing
decoder := xml.NewDecoder(reader)
for {
    token, err := decoder.Token()
    if err == io.EOF {
        break
    }
    if err != nil {
        return err
    }
    
    switch se := token.(type) {
    case xml.StartElement:
        if se.Name.Local == "book" {
            var book Book
            decoder.DecodeElement(&book, &se)
            // Process book
        }
    }
}
```

### Base64 Encoding

Encode binary data as text:

```go
import "encoding/base64"

// Standard encoding
data := []byte("Hello, World!")
encoded := base64.StdEncoding.EncodeToString(data)
// Output: "SGVsbG8sIFdvcmxkIQ=="

decoded, err := base64.StdEncoding.DecodeString(encoded)
// Output: "Hello, World!"

// URL-safe encoding (no padding =, uses - and _ instead of + and /)
urlEncoded := base64.URLEncoding.EncodeToString(data)

// Raw encoding (no padding)
rawEncoded := base64.RawStdEncoding.EncodeToString(data)

// Encoding to writer
encoder := base64.NewEncoder(base64.StdEncoding, writer)
encoder.Write(data)
encoder.Close()  // Important: flushes remaining bytes

// Decoding from reader
decoder := base64.NewDecoder(base64.StdEncoding, reader)
io.Copy(writer, decoder)

// Custom encoding alphabet
customEncoding := base64.NewEncoding("ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-_")
```

### Custom Marshalers

Implement custom JSON/XML serialization:

```go
import (
    "encoding/json"
    "time"
    "fmt"
)

// Custom time format
type CustomTime struct {
    time.Time
}

// Implement json.Marshaler
func (ct CustomTime) MarshalJSON() ([]byte, error) {
    stamp := fmt.Sprintf("\"%s\"", ct.Format("2006-01-02"))
    return []byte(stamp), nil
}

// Implement json.Unmarshaler
func (ct *CustomTime) UnmarshalJSON(data []byte) error {
    // Remove quotes
    str := string(data)
    str = str[1 : len(str)-1]
    
    t, err := time.Parse("2006-01-02", str)
    if err != nil {
        return err
    }
    ct.Time = t
    return nil
}

// Custom type that validates during unmarshal
type Email string

func (e *Email) UnmarshalJSON(data []byte) error {
    var s string
    if err := json.Unmarshal(data, &s); err != nil {
        return err
    }
    
    // Validate email format
    if !strings.Contains(s, "@") {
        return fmt.Errorf("invalid email format")
    }
    
    *e = Email(s)
    return nil
}

// Enum with custom marshaling
type Status int

const (
    StatusPending Status = iota
    StatusActive
    StatusInactive
)

func (s Status) MarshalJSON() ([]byte, error) {
    statusNames := []string{"pending", "active", "inactive"}
    if s < 0 || int(s) >= len(statusNames) {
        return nil, fmt.Errorf("invalid status")
    }
    return json.Marshal(statusNames[s])
}

func (s *Status) UnmarshalJSON(data []byte) error {
    var str string
    if err := json.Unmarshal(data, &str); err != nil {
        return err
    }
    
    statusMap := map[string]Status{
        "pending":  StatusPending,
        "active":   StatusActive,
        "inactive": StatusInactive,
    }
    
    if val, ok := statusMap[str]; ok {
        *s = val
        return nil
    }
    return fmt.Errorf("invalid status: %s", str)
}

// Example usage
type User struct {
    Email     Email      `json:"email"`
    Status    Status     `json:"status"`
    CreatedAt CustomTime `json:"created_at"`
}
```

## 7.5 HTTP

### net/http Client & Server

Go's `net/http` package provides production-ready HTTP client and server:

```go
import (
    "net/http"
    "io"
    "bytes"
    "encoding/json"
    "time"
)

// Simple HTTP server
func main() {
    // Basic handler function
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hello, %s!", r.URL.Path[1:])
    })
    
    // Handler with different methods
    http.HandleFunc("/api/users", func(w http.ResponseWriter, r *http.Request) {
        switch r.Method {
        case http.MethodGet:
            handleGetUsers(w, r)
        case http.MethodPost:
            handleCreateUser(w, r)
        default:
            w.WriteHeader(http.StatusMethodNotAllowed)
        }
    })
    
    // Serve static files
    fs := http.FileServer(http.Dir("./static"))
    http.Handle("/static/", http.StripPrefix("/static/", fs))
    
    // Start server
    fmt.Println("Server starting on :8080")
    if err := http.ListenAndServe(":8080", nil); err != nil {
        log.Fatal(err)
    }
}

// HTTP Client
func makeRequests() {
    // Simple GET request
    resp, err := http.Get("https://api.example.com/data")
    if err != nil {
        return err
    }
    defer resp.Body.Close()
    
    body, err := io.ReadAll(resp.Body)
    if err != nil {
        return err
    }
    
    // Check status
    if resp.StatusCode != http.StatusOK {
        return fmt.Errorf("bad status: %s", resp.Status)
    }
    
    // POST with JSON
    user := User{Name: "Alice", Age: 30}
    jsonData, _ := json.Marshal(user)
    
    resp, err = http.Post(
        "https://api.example.com/users",
        "application/json",
        bytes.NewBuffer(jsonData),
    )
    defer resp.Body.Close()
    
    // Custom client with timeout
    client := &http.Client{
        Timeout: 10 * time.Second,
        Transport: &http.Transport{
            MaxIdleConns:        100,
            MaxIdleConnsPerHost: 10,
            IdleConnTimeout:     90 * time.Second,
        },
    }
    
    // Build custom request
    req, err := http.NewRequest("PUT", "https://api.example.com/user/123", bytes.NewBuffer(jsonData))
    if err != nil {
        return err
    }
    
    // Add headers
    req.Header.Set("Content-Type", "application/json")
    req.Header.Set("Authorization", "Bearer token123")
    req.Header.Add("X-Custom-Header", "value")
    
    // Send request
    resp, err = client.Do(req)
    if err != nil {
        return err
    }
    defer resp.Body.Close()
    
    // Parse JSON response
    var result map[string]interface{}
    decoder := json.NewDecoder(resp.Body)
    err = decoder.Decode(&result)
}
```

### Handlers & Middleware

Structure HTTP applications with handlers and middleware:

```go
// Custom Handler type
type APIHandler struct {
    DB     *sql.DB
    Cache  *Cache
    Logger *log.Logger
}

// Implement http.Handler interface
func (h *APIHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    // Handle request
    h.Logger.Printf("Request: %s %s", r.Method, r.URL.Path)
}

// Middleware pattern
func loggingMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        start := time.Now()
        
        // Wrap ResponseWriter to capture status
        wrapped := &responseWriter{w, http.StatusOK}
        
        // Call next handler
        next.ServeHTTP(wrapped, r)
        
        // Log after
        log.Printf("%s %s %d %v", r.Method, r.URL.Path, wrapped.status, time.Since(start))
    })
}

type responseWriter struct {
    http.ResponseWriter
    status int
}

func (rw *responseWriter) WriteHeader(code int) {
    rw.status = code
    rw.ResponseWriter.WriteHeader(code)
}

// Authentication middleware
func authMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        token := r.Header.Get("Authorization")
        if token == "" {
            http.Error(w, "Unauthorized", http.StatusUnauthorized)
            return
        }
        
        // Validate token
        if !validateToken(token) {
            http.Error(w, "Invalid token", http.StatusUnauthorized)
            return
        }
        
        next.ServeHTTP(w, r)
    })
}

// CORS middleware
func corsMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        w.Header().Set("Access-Control-Allow-Origin", "*")
        w.Header().Set("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS")
        w.Header().Set("Access-Control-Allow-Headers", "Content-Type, Authorization")
        
        if r.Method == "OPTIONS" {
            w.WriteHeader(http.StatusOK)
            return
        }
        
        next.ServeHTTP(w, r)
    })
}

// Rate limiting middleware
type RateLimiter struct {
    visitors map[string]*rate.Limiter
    mu       sync.RWMutex
    rate     rate.Limit
    burst    int
}

func (rl *RateLimiter) getVisitor(ip string) *rate.Limiter {
    rl.mu.Lock()
    defer rl.mu.Unlock()
    
    if limiter, exists := rl.visitors[ip]; exists {
        return limiter
    }
    
    limiter := rate.NewLimiter(rl.rate, rl.burst)
    rl.visitors[ip] = limiter
    return limiter
}

func (rl *RateLimiter) rateLimitMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        ip := r.RemoteAddr
        limiter := rl.getVisitor(ip)
        
        if !limiter.Allow() {
            http.Error(w, "Too Many Requests", http.StatusTooManyRequests)
            return
        }
        
        next.ServeHTTP(w, r)
    })
}

// Chain middlewares
func chainMiddleware(h http.Handler, middlewares ...func(http.Handler) http.Handler) http.Handler {
    for i := len(middlewares) - 1; i >= 0; i-- {
        h = middlewares[i](h)
    }
    return h
}

// Usage
func setupRoutes() {
    handler := http.HandlerFunc(handleAPI)
    
    // Apply middleware chain
    finalHandler := chainMiddleware(
        handler,
        loggingMiddleware,
        corsMiddleware,
        authMiddleware,
    )
    
    http.Handle("/api/", finalHandler)
}
```

### Context in HTTP

Use context for request-scoped values and cancellation:

```go
import "context"

// Pass values through context
type contextKey string

const (
    userIDKey contextKey = "userID"
    requestIDKey contextKey = "requestID"
)

func authMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        // Validate and extract user ID
        userID := validateTokenAndGetUserID(r.Header.Get("Authorization"))
        
        // Add to context
        ctx := context.WithValue(r.Context(), userIDKey, userID)
        
        // Pass updated request
        next.ServeHTTP(w, r.WithContext(ctx))
    })
}

func handleUserData(w http.ResponseWriter, r *http.Request) {
    // Retrieve from context
    userID, ok := r.Context().Value(userIDKey).(string)
    if !ok {
        http.Error(w, "User not found in context", http.StatusInternalServerError)
        return
    }
    
    // Use userID
    data := getUserData(userID)
    json.NewEncoder(w).Encode(data)
}

// Request timeout with context
func handleWithTimeout(w http.ResponseWriter, r *http.Request) {
    // Create context with timeout
    ctx, cancel := context.WithTimeout(r.Context(), 5*time.Second)
    defer cancel()
    
    // Make database query with context
    result := make(chan *Data, 1)
    go func() {
        data, err := slowDatabaseQuery(ctx)
        if err != nil {
            return
        }
        result <- data
    }()
    
    select {
    case data := <-result:
        json.NewEncoder(w).Encode(data)
    case <-ctx.Done():
        http.Error(w, "Request timeout", http.StatusRequestTimeout)
    }
}

// Graceful shutdown
func startServer() {
    srv := &http.Server{
        Addr:         ":8080",
        Handler:      router,
        ReadTimeout:  15 * time.Second,
        WriteTimeout: 15 * time.Second,
        IdleTimeout:  60 * time.Second,
    }
    
    // Start server in goroutine
    go func() {
        if err := srv.ListenAndServe(); err != nil && err != http.ErrServerClosed {
            log.Fatalf("listen: %s\n", err)
        }
    }()
    
    // Wait for interrupt signal
    quit := make(chan os.Signal, 1)
    signal.Notify(quit, os.Interrupt, syscall.SIGTERM)
    <-quit
    
    log.Println("Shutting down server...")
    
    // Graceful shutdown with timeout
    ctx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
    defer cancel()
    
    if err := srv.Shutdown(ctx); err != nil {
        log.Fatal("Server forced to shutdown:", err)
    }
    
    log.Println("Server exited")
}
```

### REST API Basics

Building RESTful APIs with proper structure:

```go
// API response structure
type APIResponse struct {
    Success bool        `json:"success"`
    Data    interface{} `json:"data,omitempty"`
    Error   string      `json:"error,omitempty"`
    Meta    *Meta       `json:"meta,omitempty"`
}

type Meta struct {
    Page       int `json:"page"`
    PerPage    int `json:"per_page"`
    Total      int `json:"total"`
    TotalPages int `json:"total_pages"`
}

// RESTful user service
type UserService struct {
    db *sql.DB
}

// GET /api/users
func (s *UserService) ListUsers(w http.ResponseWriter, r *http.Request) {
    // Parse query parameters
    page, _ := strconv.Atoi(r.URL.Query().Get("page"))
    if page < 1 {
        page = 1
    }
    perPage, _ := strconv.Atoi(r.URL.Query().Get("per_page"))
    if perPage < 1 {
        perPage = 20
    }
    
    // Get users from database
    users, total, err := s.getUsers(page, perPage)
    if err != nil {
        respondWithError(w, http.StatusInternalServerError, "Database error")
        return
    }
    
    // Send response
    respondWithJSON(w, http.StatusOK, APIResponse{
        Success: true,
        Data:    users,
        Meta: &Meta{
            Page:       page,
            PerPage:    perPage,
            Total:      total,
            TotalPages: (total + perPage - 1) / perPage,
        },
    })
}

// GET /api/users/:id
func (s *UserService) GetUser(w http.ResponseWriter, r *http.Request) {
    // Extract ID from path (using gorilla/mux or similar)
    vars := mux.Vars(r)
    id, err := strconv.Atoi(vars["id"])
    if err != nil {
        respondWithError(w, http.StatusBadRequest, "Invalid user ID")
        return
    }
    
    user, err := s.getUserByID(id)
    if err == sql.ErrNoRows {
        respondWithError(w, http.StatusNotFound, "User not found")
        return
    }
    if err != nil {
        respondWithError(w, http.StatusInternalServerError, "Database error")
        return
    }
    
    respondWithJSON(w, http.StatusOK, APIResponse{
        Success: true,
        Data:    user,
    })
}

// POST /api/users
func (s *UserService) CreateUser(w http.ResponseWriter, r *http.Request) {
    var user User
    
    // Parse request body
    if err := json.NewDecoder(r.Body).Decode(&user); err != nil {
        respondWithError(w, http.StatusBadRequest, "Invalid request payload")
        return
    }
    defer r.Body.Close()
    
    // Validate
    if err := user.Validate(); err != nil {
        respondWithError(w, http.StatusBadRequest, err.Error())
        return
    }
    
    // Create user
    if err := s.createUser(&user); err != nil {
        respondWithError(w, http.StatusInternalServerError, "Failed to create user")
        return
    }
    
    respondWithJSON(w, http.StatusCreated, APIResponse{
        Success: true,
        Data:    user,
    })
}

// PUT /api/users/:id
func (s *UserService) UpdateUser(w http.ResponseWriter, r *http.Request) {
    vars := mux.Vars(r)
    id, _ := strconv.Atoi(vars["id"])
    
    var updates map[string]interface{}
    if err := json.NewDecoder(r.Body).Decode(&updates); err != nil {
        respondWithError(w, http.StatusBadRequest, "Invalid request payload")
        return
    }
    
    user, err := s.updateUser(id, updates)
    if err != nil {
        respondWithError(w, http.StatusInternalServerError, "Failed to update user")
        return
    }
    
    respondWithJSON(w, http.StatusOK, APIResponse{
        Success: true,
        Data:    user,
    })
}

// DELETE /api/users/:id
func (s *UserService) DeleteUser(w http.ResponseWriter, r *http.Request) {
    vars := mux.Vars(r)
    id, _ := strconv.Atoi(vars["id"])
    
    if err := s.deleteUser(id); err != nil {
        respondWithError(w, http.StatusInternalServerError, "Failed to delete user")
        return
    }
    
    respondWithJSON(w, http.StatusNoContent, nil)
}

// Helper functions
func respondWithJSON(w http.ResponseWriter, code int, payload interface{}) {
    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(code)
    
    if payload != nil {
        json.NewEncoder(w).Encode(payload)
    }
}

func respondWithError(w http.ResponseWriter, code int, message string) {
    respondWithJSON(w, code, APIResponse{
        Success: false,
        Error:   message,
    })
}

// Request validation
type CreateUserRequest struct {
    Name     string `json:"name" validate:"required,min=2,max=100"`
    Email    string `json:"email" validate:"required,email"`
    Password string `json:"password" validate:"required,min=8"`
}

func (r *CreateUserRequest) Validate() error {
    if r.Name == "" {
        return fmt.Errorf("name is required")
    }
    if !strings.Contains(r.Email, "@") {
        return fmt.Errorf("invalid email format")
    }
    if len(r.Password) < 8 {
        return fmt.Errorf("password must be at least 8 characters")
    }
    return nil
}
```

### Real-World HTTP Patterns

#### API Client with Retry Logic

```go
type APIClient struct {
    BaseURL    string
    HTTPClient *http.Client
    APIKey     string
    MaxRetries int
}

func NewAPIClient(baseURL, apiKey string) *APIClient {
    return &APIClient{
        BaseURL: baseURL,
        APIKey:  apiKey,
        HTTPClient: &http.Client{
            Timeout: 30 * time.Second,
        },
        MaxRetries: 3,
    }
}

func (c *APIClient) doRequestWithRetry(req *http.Request) (*http.Response, error) {
    var resp *http.Response
    var err error
    
    for i := 0; i <= c.MaxRetries; i++ {
        resp, err = c.HTTPClient.Do(req)
        
        // Success or non-retryable error
        if err == nil && resp.StatusCode < 500 {
            return resp, nil
        }
        
        // Don't retry on last attempt
        if i == c.MaxRetries {
            break
        }
        
        // Exponential backoff
        waitTime := time.Duration(math.Pow(2, float64(i))) * time.Second
        time.Sleep(waitTime)
        
        // Close failed response body
        if resp != nil {
            resp.Body.Close()
        }
    }
    
    return resp, fmt.Errorf("max retries exceeded: %w", err)
}

func (c *APIClient) Get(endpoint string, result interface{}) error {
    req, err := http.NewRequest("GET", c.BaseURL+endpoint, nil)
    if err != nil {
        return err
    }
    
    req.Header.Set("Authorization", "Bearer "+c.APIKey)
    req.Header.Set("Accept", "application/json")
    
    resp, err := c.doRequestWithRetry(req)
    if err != nil {
        return err
    }
    defer resp.Body.Close()
    
    if resp.StatusCode != http.StatusOK {
        body, _ := io.ReadAll(resp.Body)
        return fmt.Errorf("API error: %s", string(body))
    }
    
    return json.NewDecoder(resp.Body).Decode(result)
}
```

#### WebSocket Handler

```go
import "github.com/gorilla/websocket"

var upgrader = websocket.Upgrader{
    CheckOrigin: func(r *http.Request) bool {
        return true // Configure appropriately for production
    },
}

func handleWebSocket(w http.ResponseWriter, r *http.Request) {
    conn, err := upgrader.Upgrade(w, r, nil)
    if err != nil {
        log.Printf("WebSocket upgrade failed: %v", err)
        return
    }
    defer conn.Close()
    
    // Send ping periodically
    ticker := time.NewTicker(30 * time.Second)
    defer ticker.Stop()
    
    go func() {
        for range ticker.C {
            if err := conn.WriteMessage(websocket.PingMessage, nil); err != nil {
                return
            }
        }
    }()
    
    // Read messages
    for {
        messageType, message, err := conn.ReadMessage()
        if err != nil {
            if websocket.IsUnexpectedCloseError(err, websocket.CloseGoingAway, websocket.CloseAbnormalClosure) {
                log.Printf("WebSocket error: %v", err)
            }
            break
        }
        
        // Echo message back
        if err := conn.WriteMessage(messageType, message); err != nil {
            log.Printf("Write error: %v", err)
            break
        }
    }
}
```

### Best Practices

1. **Always set timeouts**

```go
client := &http.Client{
    Timeout: 30 * time.Second,
}

server := &http.Server{
    ReadTimeout:  15 * time.Second,
    WriteTimeout: 15 * time.Second,
    IdleTimeout:  60 * time.Second,
}
```

2. **Handle errors properly**

```go
resp, err := http.Get(url)
if err != nil {
    return fmt.Errorf("request failed: %w", err)
}
defer resp.Body.Close()

if resp.StatusCode != http.StatusOK {
    body, _ := io.ReadAll(resp.Body)
    return fmt.Errorf("bad status %d: %s", resp.StatusCode, body)
}
```

3. **Use context for cancellation**

```go
ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
defer cancel()

req = req.WithContext(ctx)
```

4. **Validate input**

```go
// Limit request body size
r.Body = http.MaxBytesReader(w, r.Body, 1<<20) // 1MB

// Set content type
w.Header().Set("Content-Type", "application/json")
```

5. **Use structured logging**

```go
log.Printf("method=%s path=%s status=%d duration=%v", 
    r.Method, r.URL.Path, status, duration)
```

**Key Points:**

- JSON struct tags control marshaling: `omitempty`, `-`, field renaming
- Custom marshalers for complex types or validation
- Always close response bodies to prevent resource leaks
- Use middleware for cross-cutting concerns (auth, logging, CORS)
- Context carries request-scoped values and deadlines
- Set appropriate timeouts at both client and server level
- Use streaming (Decoder/Encoder) for large JSON/XML
- Implement proper retry logic with exponential backoff for resilient clients

# 8. Concurrency

## 8.1 Goroutines

### Goroutine Basics

Goroutines are lightweight threads managed by the Go runtime. They're the foundation of Go's concurrency model:

```go
import (
    "fmt"
    "runtime"
    "time"
)

// Basic goroutine creation
func main() {
    // Direct function call
    go sayHello("World")
    
    // Anonymous function
    go func(msg string) {
        fmt.Println("Anonymous:", msg)
    }("Goroutine")
    
    // Closure capturing variables
    message := "Captured"
    go func() {
        fmt.Println(message)  // Captures message from outer scope
    }()
    
    time.Sleep(time.Second)  // Wait for goroutines to finish
}

func sayHello(name string) {
    fmt.Println("Hello", name)
}

// Goroutine memory footprint
func checkGoroutineSize() {
    var m runtime.MemStats
    runtime.ReadMemStats(&m)
    fmt.Printf("Goroutines: %d\n", runtime.NumGoroutine())
    fmt.Printf("Memory per goroutine: ~%d KB\n", m.Sys/uint64(runtime.NumGoroutine())/1024)
    // Typical goroutine stack starts at ~2KB (vs OS thread ~1-8MB)
}
```

**Goroutine Characteristics:**

- Initial stack size: ~2KB (dynamically grows/shrinks as needed, max 1GB)
- OS Thread stack: ~1-8MB (fixed size)
- Creation time: ~1-2 microseconds
- Context switch: ~200 nanoseconds (vs ~1-2 microseconds for OS threads)
- No thread ID exposed (by design - prevents thread-local storage abuse)

### Goroutine Lifecycle

**Goroutine States:**

1. **Runnable** - Ready to run, waiting in run queue
2. **Running** - Currently executing on an OS thread (M)
3. **Blocked** - Waiting for I/O, channel operation, mutex lock, etc.
4. **Dead** - Finished execution, waiting for GC

```go
// Demonstrating goroutine states
func lifecycleExample() {
    // Goroutine starts in Runnable state
    done := make(chan bool)
    
    go func() {
        // Now Running
        fmt.Println("Goroutine running")
        
        // Will become Blocked on channel receive
        <-done  // Blocked state
        
        fmt.Println("Goroutine resuming")
        // Returns to Running, then Dead after function exits
    }()
    
    time.Sleep(100 * time.Millisecond)
    done <- true  // Unblocks the goroutine
}

// Monitor goroutine lifecycle
func monitorGoroutines() {
    for i := 0; i < 3; i++ {
        fmt.Printf("Active goroutines: %d\n", runtime.NumGoroutine())
        
        // Get goroutine stack traces
        buf := make([]byte, 1<<16)
        stackLen := runtime.Stack(buf, true)
        fmt.Printf("Stack trace:\n%s\n", buf[:stackLen])
        
        time.Sleep(time.Second)
    }
}
```

### Go Runtime Scheduler (GMP Model)

The Go scheduler uses an M:N threading model, multiplexing M goroutines onto N OS threads:

**Components:**

- **G** (Goroutine): Lightweight thread of execution
- **M** (Machine): OS thread that executes goroutines
- **P** (Processor): Logical processor with local run queue

```go
// Scheduler interaction
func schedulerExample() {
    // Set maximum number of CPUs that can execute simultaneously
    runtime.GOMAXPROCS(4)  // Default is runtime.NumCPU()
    
    // Get current configuration
    fmt.Printf("NumCPU: %d\n", runtime.NumCPU())
    fmt.Printf("GOMAXPROCS: %d\n", runtime.GOMAXPROCS(0))
    
    // Force scheduler to run pending goroutines
    runtime.Gosched()  // Yields processor, allowing other goroutines to run
    
    // Pin goroutine to current OS thread
    runtime.LockOSThread()
    defer runtime.UnlockOSThread()
    // Useful for: CGO calls, thread-local storage, GUI libraries
}

// Work stealing demonstration
func workStealing() {
    numWorkers := runtime.GOMAXPROCS(0)
    var wg sync.WaitGroup
    
    // Create CPU-intensive work
    for i := 0; i < numWorkers*10; i++ {
        wg.Add(1)
        go func(id int) {
            defer wg.Done()
            
            // Simulate CPU-intensive work
            sum := 0
            for j := 0; j < 1000000; j++ {
                sum += j
            }
            
            fmt.Printf("Worker %d on P%d\n", id, runtime.GOMAXPROCS(0))
        }(i)
    }
    
    wg.Wait()
}
```

**Scheduler Mechanics:**

- Each P has a local run queue (256 goroutines max)
- Global run queue for overflow
- Work stealing: Idle P steals goroutines from other P's queues
- Preemption: Goroutines preempted after ~10ms (since Go 1.14)
- Network poller integration for async I/O


**Best Practices (Non-Channel Related):**

1. **Always know how a goroutine will terminate**
    
    - Use context for cancellation
    - Avoid infinite loops without exit conditions
    - Monitor goroutine counts in production
2. **Limit concurrent goroutines**
    
    - Use worker pools for bounded concurrency
    - Prevents resource exhaustion
    - Better performance for CPU-bound tasks
3. **Handle panics in goroutines**
    
    - Panics don't propagate to parent
    - Always use defer recover() in long-running goroutines
    - Log and monitor goroutine failures
4. **Profile and monitor**
    
    - Use ``pprof`` to identify leaks
    - Monitor ``runtime.NumGoroutine()`` in production
    - Set up alerts for abnormal goroutine counts
5. **Consider goroutine lifecycle**
    
    - Implement graceful shutdown
    - Drain work before terminating
    - Use ``sync.WaitGroup`` or similar for coordination

**Key Metrics to Monitor:**

- `runtime.NumGoroutine()` - Current goroutine count
- `runtime.NumCPU()` - Available CPU cores
- `runtime.GOMAXPROCS(0)` - Configured parallelism
- Memory usage per goroutine
- Goroutine creation/destruction rate

## 8.2 Channels

Channels are Go's primary mechanism for communication between goroutines, implementing the CSP (Communicating Sequential Processes) model. They provide synchronized communication without explicit locks.

==**Core Philosophy:** "Don't communicate by sharing memory; share memory by communicating"==

### Unbuffered vs Buffered Channels

**Unbuffered Channels (Synchronous)**

Unbuffered channels have no capacity to hold values. A send operation blocks until another goroutine receives the value, creating a synchronization point between goroutines.

```go
// Unbuffered channel creation
ch := make(chan int)        // Zero capacity
ch := make(chan int, 0)     // Explicitly zero capacity

// Synchronous handoff example
func unbufferedExample() {
    ch := make(chan int)
    
    // Sender blocks until receiver is ready
    go func() {
        fmt.Println("Sender: About to send")
        ch <- 42  // BLOCKS until someone receives
        fmt.Println("Sender: Sent successfully")
    }()
    
    time.Sleep(2 * time.Second)
    fmt.Println("Receiver: About to receive")
    value := <-ch  // Unblocks sender
    fmt.Println("Receiver: Got", value)
}

// Unbuffered as synchronization primitive
func synchronizationPoint() {
    done := make(chan struct{})
    
    go func() {
        fmt.Println("Working...")
        time.Sleep(time.Second)
        done <- struct{}{}  // Signal completion
    }()
    
    <-done  // Wait for completion
    fmt.Println("Work complete")
}
```

**Characteristics of Unbuffered Channels:**

- **Capacity:** 0
- **Send blocks:** Until a receiver is ready
- **Receive blocks:** Until a sender is ready
- **Synchronization:** Guarantees goroutine rendezvous
- **Memory:** Minimal overhead (no buffer allocation)
- **Use cases:** Signaling, synchronization, ensuring handoff

**Buffered Channels (Asynchronous)**

Buffered channels have capacity to hold values, allowing senders to proceed without waiting for receivers (until buffer is full).

```go
// Buffered channel creation
ch := make(chan int, 3)     // Buffer size of 3

// Asynchronous communication
func bufferedExample() {
    ch := make(chan string, 2)
    
    // Send without blocking (buffer not full)
    ch <- "first"   // Doesn't block
    ch <- "second"  // Doesn't block
    
    fmt.Println("Sent two values without blocking")
    
    ch <- "third"   // Would block - buffer full
    
    // Receive values
    fmt.Println(<-ch)  // "first"
    fmt.Println(<-ch)  // "second"
}

// Buffer as work queue
func workQueue() {
    tasks := make(chan Task, 100)  // Buffer up to 100 tasks
    
    // Producer can add tasks without waiting
    for i := 0; i < 50; i++ {
        tasks <- Task{ID: i}  // Non-blocking while buffer has space
    }
    
    // Workers process asynchronously
    for i := 0; i < 5; i++ {
        go worker(tasks)
    }
}

// Check buffer status
func bufferStatus() {
    ch := make(chan int, 5)
    
    ch <- 1
    ch <- 2
    
    fmt.Printf("Length: %d\n", len(ch))  // 2 (current items)
    fmt.Printf("Capacity: %d\n", cap(ch)) // 5 (max items)
    
    // Check if send would block
    select {
    case ch <- 3:
        fmt.Println("Sent without blocking")
    default:
        fmt.Println("Buffer full, would block")
    }
}
```

**Characteristics of Buffered Channels:**

- **Capacity:** 1 to max(int)
- **Send blocks:** Only when buffer is full
- **Receive blocks:** Only when buffer is empty
- **Synchronization:** Decouples sender and receiver
- **Memory:** Allocates buffer array
- **Use cases:** Work queues, rate limiting, batching

**Performance Comparison:**

```go
// Benchmark unbuffered vs buffered
func benchmarkChannels() {
    const n = 1000000
    
    // Unbuffered - full synchronization overhead
    unbuffered := make(chan int)
    go func() {
        for i := 0; i < n; i++ {
            unbuffered <- i
        }
    }()
    
    // Buffered - reduced synchronization
    buffered := make(chan int, 1000)
    go func() {
        for i := 0; i < n; i++ {
            buffered <- i  // Less blocking
        }
    }()
}
```

**Choosing Buffer Size:**

- **0 (unbuffered):** Maximum synchronization, guaranteed handoff
- **1:** Allows sender to proceed immediately for one value
- **N:** Smooths out production/consumption rate differences
- **Unlimited (using intermediary goroutine):** Dangerous, can cause memory issues

### Channel Directions

Channel directions restrict how a channel can be used, providing compile-time safety and clear API contracts.

```go
// Bidirectional channel (default)
var ch chan int           // Can send and receive

// Send-only channel
var sendOnly chan<- int    // Can only send

// Receive-only channel  
var recvOnly <-chan int    // Can only receive

// Direction conversion (implicit)
func directions() {
    ch := make(chan int)    // Bidirectional
    
    var send chan<- int = ch  // Convert to send-only
    var recv <-chan int = ch  // Convert to receive-only
    
    // send = recv  // Compile error: incompatible types
}

// API design with directions
func producer(out chan<- int) {
    for i := 0; i < 10; i++ {
        out <- i
        // value := <-out  // Compile error: receive from send-only channel
    }
    close(out)  // Sender should close
}

func consumer(in <-chan int) {
    for value := range in {
        fmt.Println(value)
        // in <- 42  // Compile error: send to receive-only channel
    }
}

func pipeline() {
    ch := make(chan int)
    go producer(ch)  // Implicitly converted to send-only
    consumer(ch)     // Implicitly converted to receive-only
}

// Return channels with specific direction
func makeReadOnly() <-chan int {
    ch := make(chan int)
    go func() {
        defer close(ch)
        for i := 0; i < 5; i++ {
            ch <- i
        }
    }()
    return ch  // Caller can only receive
}

// Multiple return channels pattern
type Processor struct {
    input  chan<- Data      // Send-only for users
    output <-chan Result    // Receive-only for users
    errors <-chan error     // Receive-only for users
}

func NewProcessor() *Processor {
    in := make(chan Data)
    out := make(chan Result)
    errs := make(chan error)
    
    // Internal processing with full access
    go func() {
        for data := range in {
            result, err := process(data)
            if err != nil {
                errs <- err
                continue
            }
            out <- result
        }
        close(out)
        close(errs)
    }()
    
    return &Processor{
        input:  in,   // Exposed as send-only
        output: out,  // Exposed as receive-only
        errors: errs, // Exposed as receive-only
    }
}
```

**Channel Direction Rules:**

- Bidirectional can be assigned to directional
- Directional cannot be assigned to opposite direction
- Directional cannot be converted back to bidirectional
- Only the sender should close a channel
- Closing receive-only channel is a compile error

### Channel Closing

Closing a channel signals that no more values will be sent. It's a broadcast mechanism that affects all receivers.

```go
// Basic closing
func closeBasics() {
    ch := make(chan int, 3)
    ch <- 1
    ch <- 2
    close(ch)
    
    // Can still receive after close
    fmt.Println(<-ch)  // 1
    fmt.Println(<-ch)  // 2
    fmt.Println(<-ch)  // 0 (zero value)
    
    // Check if channel is closed
    value, ok := <-ch
    if !ok {
        fmt.Println("Channel is closed")
    }
}

// Range automatically handles closing
func rangeOverClosed() {
    ch := make(chan int)
    
    go func() {
        for i := 0; i < 5; i++ {
            ch <- i
        }
        close(ch)  // Required for range to terminate
    }()
    
    // Range exits when channel is closed
    for value := range ch {
        fmt.Println(value)
    }
}

// Broadcasting with close
func broadcastClose() {
    stop := make(chan struct{})
    
    // Multiple goroutines waiting
    for i := 0; i < 5; i++ {
        go func(id int) {
            <-stop  // All will unblock when closed
            fmt.Printf("Worker %d stopping\n", id)
        }(i)
    }
    
    time.Sleep(time.Second)
    close(stop)  // Broadcast to all workers
}

// Safe closing pattern
type SafeChannel struct {
    ch   chan int
    once sync.Once
}

func (sc *SafeChannel) Close() {
    sc.once.Do(func() {
        close(sc.ch)  // Guarantees single close
    })
}

// Who should close pattern
func ownershipPattern() {
    // Creator/owner closes
    dataCh := make(chan Data)
    
    // Producer owns and closes
    go func() {
        defer close(dataCh)  // Always close when done
        for _, data := range getData() {
            dataCh <- data
        }
    }()
    
    // Consumer just receives
    for data := range dataCh {
        process(data)
    }
}

// Check if closed without receiving
func isClosedNonBlocking(ch <-chan int) bool {
    select {
    case <-ch:
        return true  // Either got value or closed
    default:
        return false // Not closed, would block
    }
}
```

**Channel Closing Axioms:**

1. **Sending to closed channel:** Panics
2. **Receiving from closed channel:** Returns immediately with zero value
3. **Closing closed channel:** Panics
4. **Closing receive-only channel:** Compile error
5. **Closing nil channel:** Panics

**Closed Channel Behavior Table:**

|Operation|Closed Channel|Buffered & Closed|
|---|---|---|
|Send|Panic|Panic|
|Receive|(zero value, false)|Drain buffer then (zero, false)|
|Close|Panic|Panic|
|len()|0|Number of elements remaining|
|cap()|Original capacity|Original capacity|

### nil Channels Behavior

nil channels have special blocking behavior that can be useful in certain patterns:

```go
// nil channel operations
func nilChannelBehavior() {
    var ch chan int  // nil by default
    
    // All operations block forever
    // ch <- 42        // Blocks forever
    // <-ch            // Blocks forever
    // close(ch)       // Panic: close of nil channel
    
    // Useful in select statements
    select {
    case <-ch:  // Never selected (blocks forever)
    case <-time.After(time.Second):
        fmt.Println("Timeout")
    }
}

// Disable case in select
func dynamicSelect() {
    ch1 := make(chan int)
    ch2 := make(chan int)
    
    var activeCh chan int
    enable := true
    
    for {
        // Conditionally enable channel
        if enable {
            activeCh = ch1
        } else {
            activeCh = nil  // Disable this case
        }
        
        select {
        case val := <-activeCh:  // Skipped if nil
            fmt.Println("Got:", val)
        case val := <-ch2:
            fmt.Println("Ch2:", val)
        case <-time.After(time.Second):
            enable = !enable  // Toggle
        }
    }
}

// Merge channels with nil
func mergeChannels(ch1, ch2 <-chan int) <-chan int {
    out := make(chan int)
    
    go func() {
        defer close(out)
        
        for ch1 != nil || ch2 != nil {
            select {
            case val, ok := <-ch1:
                if !ok {
                    ch1 = nil  // Disable this case
                    continue
                }
                out <- val
                
            case val, ok := <-ch2:
                if !ok {
                    ch2 = nil  // Disable this case
                    continue
                }
                out <- val
            }
        }
    }()
    
    return out
}

// nil channel in struct initialization
type Worker struct {
    tasks   chan Task
    results chan Result
}

func (w *Worker) Start() {
    if w.tasks == nil {
        w.tasks = make(chan Task, 10)  // Lazy initialization
    }
    if w.results == nil {
        w.results = make(chan Result, 10)
    }
    
    go w.process()
}
```

**nil Channel Rules:**

- **Send to nil:** Blocks forever (no panic)
- **Receive from nil:** Blocks forever (no panic)
- **Close nil:** Panics
- **len(nil):** Returns 0
- **cap(nil):** Returns 0

### Channel Internals and Performance

**Channel Internal Structure:**

- Lock-free circular buffer for buffered channels
- Waiting goroutine queues (sendq and recvq)
- Mutex for synchronization
- Atomic operations for fast path

```go
// Channel performance considerations
func performancePatterns() {
    // Batch sending for better performance
    ch := make(chan []int, 10)
    
    // Instead of sending individual items
    // Send batches
    batch := make([]int, 0, 100)
    for i := 0; i < 1000; i++ {
        batch = append(batch, i)
        if len(batch) == 100 {
            ch <- batch
            batch = make([]int, 0, 100)
        }
    }
    
    // Reuse channels when possible
    pool := &sync.Pool{
        New: func() interface{} {
            return make(chan int, 100)
        },
    }
    
    ch := pool.Get().(chan int)
    defer pool.Put(ch)
}

// Channel select performance
func selectPerformance() {
    // Random selection for fairness
    ch1 := make(chan int, 1)
    ch2 := make(chan int, 1)
    ch1 <- 1
    ch2 <- 2
    
    // Go randomly selects when multiple ready
    select {
    case <-ch1:
        fmt.Println("Selected ch1")
    case <-ch2:
        fmt.Println("Selected ch2")
    }
}
```

### Advanced Channel Patterns

```go
// Try-send pattern
func trySend(ch chan<- int, value int) bool {
    select {
    case ch <- value:
        return true
    default:
        return false  // Would block
    }
}

// Try-receive pattern
func tryReceive(ch <-chan int) (int, bool) {
    select {
    case value := <-ch:
        return value, true
    default:
        return 0, false  // Would block
    }
}

// Timeout pattern
func withTimeout(ch <-chan int, timeout time.Duration) (int, error) {
    select {
    case value := <-ch:
        return value, nil
    case <-time.After(timeout):
        return 0, fmt.Errorf("timeout after %v", timeout)
    }
}

// Fan-in with proper closure handling
func fanIn(channels ...<-chan int) <-chan int {
    out := make(chan int)
    var wg sync.WaitGroup
    
    for _, ch := range channels {
        wg.Add(1)
        go func(c <-chan int) {
            defer wg.Done()
            for val := range c {
                out <- val
            }
        }(ch)
    }
    
    go func() {
        wg.Wait()
        close(out)
    }()
    
    return out
}

// Debounce pattern
func debounce(input <-chan int, duration time.Duration) <-chan int {
    out := make(chan int)
    
    go func() {
        defer close(out)
        
        var lastValue int
        timer := time.NewTimer(duration)
        timer.Stop()
        
        for {
            select {
            case value, ok := <-input:
                if !ok {
                    return
                }
                lastValue = value
                timer.Reset(duration)
                
            case <-timer.C:
                out <- lastValue
            }
        }
    }()
    
    return out
}
```

**Channel Best Practices:**

1. **Ownership:** The goroutine that creates a channel should close it
2. **Direction:** Use directional channels in function parameters
3. **Buffering:** Start unbuffered, add buffering for performance
4. **nil channels:** Use to disable select cases dynamically
5. **Close once:** Use sync.Once if multiple goroutines might close
6. **Don't close from receiver:** Only sender should close
7. **Check if closed:** Use comma-ok idiom when needed
8. **Range for unknown count:** Use range when count is unknown

**When to Use Channels:**

- **Communication:** Between goroutines
- **Synchronization:** Coordinating goroutine execution
- **Distribution:** Fan-out/fan-in patterns
- **Cancellation:** Broadcasting stop signals

**When NOT to Use Channels:**

- Simple data protection (use mutex)
- High-frequency, low-latency operations (use atomic)
- When shared memory is cleaner and simpler

**Common Channel Gotchas:**

- Forgetting to close channels (goroutine leaks with range)
- Sending on closed channel (panic)
- Not checking if channel is closed
- Deadlock from circular dependencies
- Unbuffered channels in same goroutine
- nil channel operations without checking

## 8.3 Select Statement

The select statement is Go's powerful control structure for multiplexing channel operations. It allows a goroutine to wait on multiple channel operations simultaneously, proceeding with whichever operation becomes ready first.

**Core Concept:** Select is to channels what switch is to values - it chooses between multiple communication operations.

### Multiplexing

Select enables concurrent channel operations, choosing non-deterministically when multiple cases are ready.

```go
// Basic select multiplexing
func basicSelect() {
    ch1 := make(chan string)
    ch2 := make(chan string)
    
    go func() {
        time.Sleep(1 * time.Second)
        ch1 <- "from ch1"
    }()
    
    go func() {
        time.Sleep(2 * time.Second)
        ch2 <- "from ch2"
    }()
    
    // Select waits for first available
    select {
    case msg1 := <-ch1:
        fmt.Println("Received:", msg1)
    case msg2 := <-ch2:
        fmt.Println("Received:", msg2)
    }
}

// Multiple receives from same channel
func multipleReceives() {
    ch := make(chan int, 3)
    ch <- 1
    ch <- 2
    ch <- 3
    
    for i := 0; i < 3; i++ {
        select {
        case val := <-ch:
            fmt.Println("Got:", val)
        case <-time.After(time.Second):
            fmt.Println("Timeout")
        }
    }
}

// Multiplexing different types
func mixedTypeSelect() {
    intCh := make(chan int)
    stringCh := make(chan string)
    boolCh := make(chan bool)
    
    go func() { intCh <- 42 }()
    go func() { stringCh <- "hello" }()
    go func() { boolCh <- true }()
    
    for i := 0; i < 3; i++ {
        select {
        case v := <-intCh:
            fmt.Printf("Int: %d\n", v)
        case v := <-stringCh:
            fmt.Printf("String: %s\n", v)
        case v := <-boolCh:
            fmt.Printf("Bool: %v\n", v)
        }
    }
}

// Fair multiplexing with multiple ready channels
func fairnessDemo() {
    ch1 := make(chan int, 100)
    ch2 := make(chan int, 100)
    
    // Fill both channels
    for i := 0; i < 100; i++ {
        ch1 <- i
        ch2 <- i * 100
    }
    
    count1, count2 := 0, 0
    
    // Select randomly chooses when multiple ready
    for i := 0; i < 200; i++ {
        select {
        case <-ch1:
            count1++
        case <-ch2:
            count2++
        }
    }
    
    fmt.Printf("Ch1: %d, Ch2: %d\n", count1, count2)
    // Results will be approximately 50/50 due to random selection
}

// Priority select pattern (not built-in)
func prioritySelect(high, low <-chan int) int {
    // Try high priority first
    select {
    case val := <-high:
        return val
    default:
        // High not ready, try both
        select {
        case val := <-high:
            return val
        case val := <-low:
            return val
        }
    }
}

// Bi-directional multiplexing
func bidirectionalSelect() {
    send := make(chan int, 1)
    recv := make(chan int, 1)
    recv <- 42
    
    value := 100
    
    select {
    case send <- value:  // Try to send
        fmt.Println("Sent:", value)
    case val := <-recv:  // Try to receive
        fmt.Println("Received:", val)
    }
}
```

**Select Execution Rules:**

1. All channel expressions are evaluated once
2. If multiple cases are ready, one is chosen randomly
3. If no cases are ready and no default, select blocks
4. Empty select `select {}` blocks forever

```go
// Channel expression evaluation
func evaluationOrder() {
    // All expressions evaluated before selection
    select {
    case ch1 <- getValue():  // getValue() called even if not selected
    case val := <-ch2:
        process(val)
    case ch3 <- compute():   // compute() also called
    }
}

// Empty select use case
func blockForever() {
    go doWork()
    
    select {}  // Block main goroutine forever
    // Common in programs that should run indefinitely
}

// Select with nil channels
func nilChannelSelect() {
    var ch1 chan int  // nil
    ch2 := make(chan int)
    
    go func() { ch2 <- 42 }()
    
    select {
    case <-ch1:  // Never selected (nil blocks forever)
        fmt.Println("Ch1")
    case val := <-ch2:
        fmt.Println("Ch2:", val)  // This will be selected
    }
}
```

### Non-blocking Operations

Select with default case enables non-blocking channel operations, crucial for responsive concurrent systems.

```go
// Non-blocking send
func nonBlockingSend(ch chan<- int, value int) bool {
    select {
    case ch <- value:
        return true
    default:
        // Channel full or unbuffered with no receiver
        return false
    }
}

// Non-blocking receive
func nonBlockingReceive(ch <-chan int) (int, bool) {
    select {
    case value := <-ch:
        return value, true
    default:
        // Channel empty or unbuffered with no sender
        return 0, false
    }
}

// Non-blocking multi-receive
func drainChannel(ch <-chan int) []int {
    var values []int
    
    for {
        select {
        case val := <-ch:
            values = append(values, val)
        default:
            return values  // No more values available
        }
    }
}

// Work stealing with non-blocking
type WorkStealer struct {
    own    chan Task
    others []chan Task
}

func (ws *WorkStealer) getTask() Task {
    // Try own queue first
    select {
    case task := <-ws.own:
        return task
    default:
        // Try to steal from others
        for _, other := range ws.others {
            select {
            case task := <-other:
                return task
            default:
                continue
            }
        }
        return nil  // No work available
    }
}

// Non-blocking state check
func checkState(stateCh <-chan State) State {
    select {
    case state := <-stateCh:
        // Got new state
        return state
    default:
        // Use cached or default state
        return currentState
    }
}

// Polling pattern
func pollWithBackoff(ch <-chan Event) {
    backoff := 10 * time.Millisecond
    maxBackoff := 1 * time.Second
    
    for {
        select {
        case event := <-ch:
            handleEvent(event)
            backoff = 10 * time.Millisecond  // Reset backoff
            
        default:
            // No event, back off
            time.Sleep(backoff)
            backoff *= 2
            if backoff > maxBackoff {
                backoff = maxBackoff
            }
        }
    }
}
```

### Default Case

The default case executes immediately if no other cases are ready, preventing blocking and enabling various patterns.

```go
// Default case basics
func defaultBasics() {
    ch := make(chan int)
    
    select {
    case val := <-ch:
        fmt.Println("Received:", val)
    default:
        fmt.Println("No value available")
    }
}

// Busy polling (anti-pattern)
func busyPolling() {
    ch := make(chan int)
    
    // BAD: Consumes 100% CPU
    for {
        select {
        case val := <-ch:
            process(val)
        default:
            // Spinning without delay
        }
    }
}

// Proper polling with default
func properPolling() {
    ch := make(chan int)
    ticker := time.NewTicker(100 * time.Millisecond)
    defer ticker.Stop()
    
    for {
        select {
        case val := <-ch:
            process(val)
        case <-ticker.C:
            // Check periodically
            select {
            case val := <-ch:
                process(val)
            default:
                // Nothing to process
            }
        }
    }
}

// Default with state machine
func stateMachine() {
    state := "idle"
    eventCh := make(chan Event)
    
    for {
        select {
        case event := <-eventCh:
            state = processEvent(state, event)
            
        default:
            // Perform state-specific background work
            switch state {
            case "idle":
                // Do idle tasks
            case "processing":
                // Continue processing
                if done := continueProcessing(); done {
                    state = "idle"
                }
            case "error":
                // Try recovery
                if recovered := tryRecover(); recovered {
                    state = "idle"
                }
            }
            
            time.Sleep(10 * time.Millisecond)
        }
    }
}

// Conditional channel operations
func conditionalOps() {
    sendCh := make(chan int, 1)
    recvCh := make(chan int, 1)
    
    shouldSend := true
    shouldReceive := false
    value := 42
    
    for {
        select {
        case sendCh <- value:
            if !shouldSend {
                panic("Shouldn't have sent")
            }
            shouldSend = false
            
        case val := <-recvCh:
            if !shouldReceive {
                panic("Shouldn't have received")
            }
            fmt.Println("Received:", val)
            
        default:
            // Neither operation ready or allowed
            if shouldSend {
                fmt.Println("Send would block")
            }
            if shouldReceive {
                fmt.Println("Receive would block")
            }
            time.Sleep(100 * time.Millisecond)
        }
    }
}

// Resource pool with non-blocking acquire
type ResourcePool struct {
    resources chan Resource
}

func (p *ResourcePool) TryAcquire() (Resource, bool) {
    select {
    case r := <-p.resources:
        return r, true
    default:
        return nil, false  // Pool empty
    }
}

func (p *ResourcePool) AcquireWithTimeout(timeout time.Duration) (Resource, error) {
    select {
    case r := <-p.resources:
        return r, nil
    case <-time.After(timeout):
        return nil, fmt.Errorf("timeout acquiring resource")
    default:
        // Try to create new resource if pool empty
        if r := p.createNew(); r != nil {
            return r, nil
        }
        // Fall back to waiting
        select {
        case r := <-p.resources:
            return r, nil
        case <-time.After(timeout):
            return nil, fmt.Errorf("timeout acquiring resource")
        }
    }
}
```

### Timeouts

Timeouts prevent indefinite blocking and implement deadline-based operations.

```go
// Basic timeout pattern
func basicTimeout() {
    ch := make(chan Result)
    
    go func() {
        time.Sleep(2 * time.Second)
        ch <- computeResult()
    }()
    
    select {
    case result := <-ch:
        fmt.Println("Got result:", result)
    case <-time.After(1 * time.Second):
        fmt.Println("Operation timed out")
    }
}

// Configurable timeout
func withTimeout(ch <-chan int, timeout time.Duration) (int, error) {
    select {
    case val := <-ch:
        return val, nil
    case <-time.After(timeout):
        return 0, fmt.Errorf("timeout after %v", timeout)
    }
}

// Multiple timeouts
func multipleTimeouts() {
    shortTimeout := 1 * time.Second
    longTimeout := 5 * time.Second
    
    ch := make(chan string)
    
    select {
    case msg := <-ch:
        fmt.Println("Received:", msg)
    case <-time.After(shortTimeout):
        fmt.Println("Short timeout reached, trying fallback...")
        
        // Nested select for extended timeout
        select {
        case msg := <-ch:
            fmt.Println("Received after retry:", msg)
        case <-time.After(longTimeout - shortTimeout):
            fmt.Println("Final timeout")
        }
    }
}

// Timeout with cleanup
func timeoutWithCleanup() {
    type Result struct {
        value int
        err   error
    }
    
    resultCh := make(chan Result, 1)
    
    // Start operation
    cancel := make(chan struct{})
    go func() {
        select {
        case resultCh <- doExpensiveOperation():
            // Success
        case <-cancel:
            // Cancelled, cleanup
            cleanup()
        }
    }()
    
    // Wait with timeout
    select {
    case result := <-resultCh:
        if result.err != nil {
            return result.err
        }
        process(result.value)
    case <-time.After(5 * time.Second):
        close(cancel)  // Signal cancellation
        return fmt.Errorf("operation timeout")
    }
}

// Reusable timer for efficiency
func efficientTimeout() {
    timer := time.NewTimer(0)
    timer.Stop()  // Stop immediately
    
    ch := make(chan int)
    
    for {
        timer.Reset(1 * time.Second)
        
        select {
        case val := <-ch:
            if !timer.Stop() {
                <-timer.C  // Drain channel if fired
            }
            process(val)
            
        case <-timer.C:
            fmt.Println("Timeout")
        }
    }
}

// Progressive timeout (exponential backoff)
func progressiveTimeout() {
    ch := make(chan Result)
    timeout := 100 * time.Millisecond
    maxTimeout := 10 * time.Second
    
    for attempt := 0; attempt < 5; attempt++ {
        select {
        case result := <-ch:
            handleResult(result)
            return
            
        case <-time.After(timeout):
            fmt.Printf("Attempt %d timed out after %v\n", attempt+1, timeout)
            
            // Exponential backoff
            timeout *= 2
            if timeout > maxTimeout {
                timeout = maxTimeout
            }
            
            // Maybe retry the operation
            go retryOperation(ch)
        }
    }
    
    fmt.Println("All attempts failed")
}

// Deadline pattern
func withDeadline(deadline time.Time) error {
    ch := make(chan Result)
    
    go doWork(ch)
    
    timeout := time.Until(deadline)
    if timeout <= 0 {
        return fmt.Errorf("deadline already passed")
    }
    
    select {
    case result := <-ch:
        return processResult(result)
    case <-time.After(timeout):
        return fmt.Errorf("deadline exceeded")
    }
}

// Heartbeat/keepalive pattern
func heartbeatMonitor(heartbeat <-chan struct{}) {
    timeout := 5 * time.Second
    
    for {
        select {
        case <-heartbeat:
            fmt.Println("Heartbeat received")
            // Reset monitoring
            
        case <-time.After(timeout):
            fmt.Println("Heartbeat timeout - service may be down")
            alertOps()
            return
        }
    }
}
```

### Advanced Select Patterns

```go
// Dynamic case selection
func dynamicSelect(channels []chan int) {
    cases := make([]reflect.SelectCase, len(channels))
    
    for i, ch := range channels {
        cases[i] = reflect.SelectCase{
            Dir:  reflect.SelectRecv,
            Chan: reflect.ValueOf(ch),
        }
    }
    
    // Add timeout case
    cases = append(cases, reflect.SelectCase{
        Dir:  reflect.SelectRecv,
        Chan: reflect.ValueOf(time.After(time.Second)),
    })
    
    chosen, value, ok := reflect.Select(cases)
    if chosen < len(channels) {
        if ok {
            fmt.Printf("Received %v from channel %d\n", value.Int(), chosen)
        }
    } else {
        fmt.Println("Timeout")
    }
}

// Round-robin selection
type RoundRobin struct {
    channels []<-chan int
    current  int
}

func (rr *RoundRobin) Next() (int, bool) {
    start := rr.current
    
    for {
        select {
        case val := <-rr.channels[rr.current]:
            rr.current = (rr.current + 1) % len(rr.channels)
            return val, true
        default:
            rr.current = (rr.current + 1) % len(rr.channels)
            
            if rr.current == start {
                return 0, false  // All channels empty
            }
        }
    }
}

// Weighted selection
type WeightedChannel struct {
    ch     <-chan int
    weight int
}

func weightedSelect(channels []WeightedChannel) int {
    for {
        // Build cases based on weights
        for _, wc := range channels {
            for i := 0; i < wc.weight; i++ {
                select {
                case val := <-wc.ch:
                    return val
                default:
                    // Try next
                }
            }
        }
        
        time.Sleep(10 * time.Millisecond)
    }
}

// Context-aware select
func contextSelect(ctx context.Context, ch <-chan int) (int, error) {
    select {
    case val := <-ch:
        return val, nil
    case <-ctx.Done():
        return 0, ctx.Err()
    }
}

// Batch collection with timeout
func collectBatch(input <-chan int, maxSize int, maxWait time.Duration) []int {
    batch := make([]int, 0, maxSize)
    timer := time.NewTimer(maxWait)
    defer timer.Stop()
    
    for {
        select {
        case val := <-input:
            batch = append(batch, val)
            if len(batch) >= maxSize {
                return batch
            }
            
        case <-timer.C:
            if len(batch) > 0 {
                return batch
            }
            timer.Reset(maxWait)
        }
    }
}

// Debounced select
func debounce(input <-chan Event, delay time.Duration) <-chan Event {
    output := make(chan Event)
    
    go func() {
        defer close(output)
        
        var timer *time.Timer
        var latestEvent Event
        
        for {
            select {
            case event, ok := <-input:
                if !ok {
                    return
                }
                
                latestEvent = event
                
                if timer != nil {
                    timer.Stop()
                }
                timer = time.AfterFunc(delay, func() {
                    output <- latestEvent
                })
                
            case <-time.After(delay * 2):
                // Safety timeout
            }
        }
    }()
    
    return output
}

// Rate-limited select
func rateLimitedSelect(input <-chan Request, rateLimit time.Duration) {
    ticker := time.NewTicker(rateLimit)
    defer ticker.Stop()
    
    for {
        select {
        case req := <-input:
            // Wait for next tick
            <-ticker.C
            process(req)
            
        case <-time.After(10 * time.Second):
            fmt.Println("No requests for 10 seconds")
        }
    }
}
```

### Select Performance and Optimization

```go
// Benchmark select vs direct receive
func benchmarkSelect() {
    ch := make(chan int, 1000)
    
    // Fill channel
    for i := 0; i < 1000; i++ {
        ch <- i
    }
    
    // Direct receive - fastest
    start := time.Now()
    for i := 0; i < 1000; i++ {
        <-ch
    }
    directTime := time.Since(start)
    
    // Select with single case - slightly slower
    for i := 0; i < 1000; i++ {
        ch <- i
    }
    
    start = time.Now()
    for i := 0; i < 1000; i++ {
        select {
        case <-ch:
        }
    }
    selectTime := time.Since(start)
    
    fmt.Printf("Direct: %v, Select: %v\n", directTime, selectTime)
}

// Optimize select in hot paths
func optimizedSelect(primary, secondary <-chan int) {
    // Fast path for primary channel
    for {
        // Try primary without select first
        select {
        case val := <-primary:
            process(val)
            continue
        default:
        }
        
        // Fallback to full select
        select {
        case val := <-primary:
            process(val)
        case val := <-secondary:
            process(val)
        case <-time.After(time.Second):
            return
        }
    }
}
```

**Select Statement Guarantees:**

1. **Fairness:** Random selection when multiple ready
2. **Atomicity:** Only one case executes
3. **Evaluation:** All channel expressions evaluated once
4. **Blocking:** Without default, blocks until a case is ready

**Select Anti-patterns:**

- Busy waiting with empty default case
- Creating timer channels in loop (use ``Timer.Reset``)
- Forgetting to handle channel closure
- Not draining ``timer.C`` after Stop()
- Too many cases (consider ``reflect.Select``)

**Select Best Practices:**

1. **Use default for non-blocking:** But avoid busy loops
2. **Reuse timers:** Don't create new timers in loops
3. **Handle nil channels:** Use to disable cases
4. **Check channel closure:** Use comma-ok idiom
5. **Prefer simple selects:** Complex selects are hard to debug
6. **Context for cancellation:** Integrate ``context.Done()``
7. **Document randomness:** Make random selection behavior clear

**Common Select Patterns Summary:**

- **Timeout:** Prevent indefinite waiting
- **Non-blocking:** Try operation without waiting
- **Multiplex:** Handle multiple channels
- **Priority:** Implement channel priorities
- **Cancellation:** Stop operations cleanly
- **Rate limiting:** Control operation frequency
- **Debouncing:** Reduce event frequency
- **Batching:** Collect multiple items

**Performance Considerations:**

- Single-case select has ~5% overhead vs direct operation
- Default case adds minimal overhead
- Many cases can impact performance (consider alternatives)
- ``reflect.Select`` for dynamic cases has significant overhead
- Timer channel creation is expensive (pool or reuse)

XXX

## 8.4 Synchronization Primitives

The sync package provides low-level synchronization primitives for coordinating access to shared memory. These are the building blocks for safe concurrent programming when channels aren't the best fit.

**Core Philosophy:** These primitives are for low-level synchronization. Prefer channels for high-level coordination between goroutines.

### ``sync.WaitGroup``

``WaitGroup`` waits for a collection of goroutines to finish executing. It's a counter-based synchronization primitive.

```go
import "sync"

// Basic WaitGroup usage
func basicWaitGroup() {
    var wg sync.WaitGroup
    
    for i := 0; i < 5; i++ {
        wg.Add(1)  // Increment counter before starting goroutine
        
        go func(id int) {
            defer wg.Done()  // Decrement counter when done
            
            fmt.Printf("Worker %d starting\n", id)
            time.Sleep(time.Second)
            fmt.Printf("Worker %d done\n", id)
        }(i)
    }
    
    wg.Wait()  // Block until counter reaches zero
    fmt.Println("All workers completed")
}

// WaitGroup with error handling
func waitGroupWithErrors() error {
    var wg sync.WaitGroup
    errCh := make(chan error, 5)  // Buffered to prevent blocking
    
    for i := 0; i < 5; i++ {
        wg.Add(1)
        
        go func(id int) {
            defer wg.Done()
            
            if err := doWork(id); err != nil {
                errCh <- err
            }
        }(i)
    }
    
    wg.Wait()
    close(errCh)  // Close after all goroutines done
    
    // Collect any errors
    for err := range errCh {
        if err != nil {
            return err  // Return first error
        }
    }
    
    return nil
}

// Reusable WaitGroup pattern
type Worker struct {
    wg sync.WaitGroup
}

func (w *Worker) Run(tasks []Task) {
    w.wg.Add(len(tasks))
    
    for _, task := range tasks {
        go w.process(task)
    }
    
    w.wg.Wait()
}

func (w *Worker) process(task Task) {
    defer w.wg.Done()
    task.Execute()
}

// Dynamic WaitGroup - adding tasks during execution
func dynamicWaitGroup() {
    var wg sync.WaitGroup
    taskCh := make(chan int)
    
    // Producer
    go func() {
        for i := 0; i < 10; i++ {
            taskCh <- i
            wg.Add(1)  // Add before sending
        }
        close(taskCh)
    }()
    
    // Consumers
    for i := 0; i < 3; i++ {
        go func(workerID int) {
            for task := range taskCh {
                processTask(workerID, task)
                wg.Done()
            }
        }(i)
    }
    
    wg.Wait()
}

// WaitGroup with timeout
func waitGroupWithTimeout(timeout time.Duration) error {
    var wg sync.WaitGroup
    done := make(chan struct{})
    
    // Start workers
    for i := 0; i < 5; i++ {
        wg.Add(1)
        go func(id int) {
            defer wg.Done()
            time.Sleep(time.Duration(id) * time.Second)
        }(i)
    }
    
    // Wait in goroutine
    go func() {
        wg.Wait()
        close(done)
    }()
    
    // Wait with timeout
    select {
    case <-done:
        return nil
    case <-time.After(timeout):
        return fmt.Errorf("timeout waiting for workers")
    }
}
```

**WaitGroup Rules:**

- **Add() before goroutine starts:** Prevent race conditions
- **Done() in defer:** Ensures it's called even if panic
- **Can't copy:** Pass pointer to WaitGroup
- **Can reuse:** After Wait() returns, can use again
- **Negative counter panics:** More Done() than Add() causes panic

### ``sync.Mutex`` & ``sync.RWMutex``

Mutexes provide exclusive access to shared resources, implementing mutual exclusion.

```go
// Basic Mutex usage
type Counter struct {
    mu    sync.Mutex
    value int
}

func (c *Counter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}

func (c *Counter) Value() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.value
}

// RWMutex for read-heavy workloads
type Cache struct {
    mu    sync.RWMutex
    items map[string]interface{}
}

func NewCache() *Cache {
    return &Cache{
        items: make(map[string]interface{}),
    }
}

func (c *Cache) Get(key string) (interface{}, bool) {
    c.mu.RLock()  // Multiple readers allowed
    defer c.mu.RUnlock()
    
    item, found := c.items[key]
    return item, found
}

func (c *Cache) Set(key string, value interface{}) {
    c.mu.Lock()  // Exclusive write lock
    defer c.mu.Unlock()
    
    c.items[key] = value
}

func (c *Cache) Delete(key string) {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    delete(c.items, key)
}

// Multiple reads, single write demonstration
func (c *Cache) Snapshot() map[string]interface{} {
    c.mu.RLock()
    defer c.mu.RUnlock()
    
    // Create copy while holding read lock
    snapshot := make(map[string]interface{}, len(c.items))
    for k, v := range c.items {
        snapshot[k] = v
    }
    return snapshot
}

// Mutex embedding pattern
type SafeMap struct {
    sync.Mutex  // Embedded mutex
    m map[string]int
}

func (sm *SafeMap) Inc(key string) {
    sm.Lock()
    defer sm.Unlock()
    sm.m[key]++
}

// Fine-grained locking
type ShardedMap struct {
    shards []MapShard
}

type MapShard struct {
    mu    sync.RWMutex
    items map[string]interface{}
}

func NewShardedMap(shardCount int) *ShardedMap {
    shards := make([]MapShard, shardCount)
    for i := range shards {
        shards[i].items = make(map[string]interface{})
    }
    return &ShardedMap{shards: shards}
}

func (m *ShardedMap) getShard(key string) *MapShard {
    hash := fnv32(key)
    return &m.shards[hash%uint32(len(m.shards))]
}

func (m *ShardedMap) Get(key string) (interface{}, bool) {
    shard := m.getShard(key)
    shard.mu.RLock()
    defer shard.mu.RUnlock()
    
    val, ok := shard.items[key]
    return val, ok
}

// Try-lock pattern (using channels)
type TryMutex struct {
    ch chan struct{}
}

func NewTryMutex() *TryMutex {
    ch := make(chan struct{}, 1)
    ch <- struct{}{}  // Initially unlocked
    return &TryMutex{ch: ch}
}

func (m *TryMutex) TryLock() bool {
    select {
    case <-m.ch:
        return true
    default:
        return false
    }
}

func (m *TryMutex) Unlock() {
    select {
    case m.ch <- struct{}{}:
    default:
        panic("unlock of unlocked mutex")
    }
}

// Deadlock prevention with lock ordering
type BankAccount struct {
    id      int
    balance int
    mu      sync.Mutex
}

func Transfer(from, to *BankAccount, amount int) {
    // Always lock in consistent order to prevent deadlock
    if from.id < to.id {
        from.mu.Lock()
        defer from.mu.Unlock()
        to.mu.Lock()
        defer to.mu.Unlock()
    } else {
        to.mu.Lock()
        defer to.mu.Unlock()
        from.mu.Lock()
        defer from.mu.Unlock()
    }
    
    if from.balance >= amount {
        from.balance -= amount
        to.balance += amount
    }
}
```

**Mutex vs RWMutex Performance:**

- **Mutex:** Equal cost for all operations
- **RWMutex:** Optimized for read-heavy workloads
- **RLock:** Multiple goroutines can hold simultaneously
- **Lock:** Exclusive access, waits for all RLocks

**Common Mutex Pitfalls:**

- Forgetting to unlock (use defer)
- Locking in different orders (deadlock)
- Holding locks too long (contention)
- Copying mutex (pass pointer)

### ``sync.Once``

Once ensures a function is executed exactly once, regardless of concurrent access.

```go
// Basic Once usage
var (
    instance *Singleton
    once     sync.Once
)

type Singleton struct {
    config Config
}

func GetInstance() *Singleton {
    once.Do(func() {
        fmt.Println("Creating singleton instance")
        instance = &Singleton{
            config: loadConfig(),
        }
    })
    return instance
}

// Once with initialization
type Database struct {
    conn *sql.DB
    once sync.Once
    err  error
}

func (db *Database) Connect() error {
    db.once.Do(func() {
        db.conn, db.err = sql.Open("postgres", "connection-string")
        if db.err == nil {
            db.err = db.conn.Ping()
        }
    })
    return db.err
}

// Lazy initialization pattern
type ExpensiveResource struct {
    once sync.Once
    data []byte
}

func (r *ExpensiveResource) Get() []byte {
    r.once.Do(func() {
        r.data = loadExpensiveData()
    })
    return r.data
}

// Once with error handling
type Service struct {
    client *Client
    once   sync.Once
    err    error
}

func (s *Service) getClient() (*Client, error) {
    s.once.Do(func() {
        s.client, s.err = initializeClient()
    })
    return s.client, s.err
}

// Reset pattern (not directly supported)
type ResettableOnce struct {
    mu   sync.Mutex
    done uint32
    m    sync.Mutex
}

func (o *ResettableOnce) Do(f func()) {
    if atomic.LoadUint32(&o.done) == 0 {
        o.doSlow(f)
    }
}

func (o *ResettableOnce) doSlow(f func()) {
    o.m.Lock()
    defer o.m.Unlock()
    if o.done == 0 {
        defer atomic.StoreUint32(&o.done, 1)
        f()
    }
}

func (o *ResettableOnce) Reset() {
    atomic.StoreUint32(&o.done, 0)
}

// Multiple once for phases
type Application struct {
    initOnce  sync.Once
    startOnce sync.Once
    stopOnce  sync.Once
}

func (app *Application) Init() {
    app.initOnce.Do(func() {
        fmt.Println("Initializing application")
        loadConfiguration()
        setupLogging()
    })
}

func (app *Application) Start() {
    app.Init()  // Ensure init is done
    
    app.startOnce.Do(func() {
        fmt.Println("Starting application")
        startHTTPServer()
        startBackgroundJobs()
    })
}

func (app *Application) Stop() {
    app.stopOnce.Do(func() {
        fmt.Println("Stopping application")
        stopBackgroundJobs()
        stopHTTPServer()
    })
}
```

**Once Characteristics:**

- **Exactly once:** Even with concurrent calls
- **Blocks other callers:** Until first execution completes
- **No reset:** Can't re-execute after completion
- **Panic propagation:** If function panics, Once considers it done

### ``sync.Map`` (Concurrent Map)

``sync.Map`` is a concurrent map optimized for specific use cases where regular map + mutex isn't optimal.

```go
// Basic sync.Map usage
func basicSyncMap() {
    var m sync.Map
    
    // Store values
    m.Store("key1", "value1")
    m.Store("key2", 100)
    m.Store("key3", struct{}{})
    
    // Load values
    if value, ok := m.Load("key1"); ok {
        fmt.Println("Found:", value)
    }
    
    // Load or store
    actual, loaded := m.LoadOrStore("key4", "new-value")
    if loaded {
        fmt.Println("Already existed:", actual)
    } else {
        fmt.Println("Stored new value:", actual)
    }
    
    // Delete
    m.Delete("key2")
    
    // Range over all entries
    m.Range(func(key, value interface{}) bool {
        fmt.Printf("%v: %v\n", key, value)
        return true  // Continue iteration
    })
}

// Cache implementation with sync.Map
type ConcurrentCache struct {
    items sync.Map
    stats struct {
        hits   uint64
        misses uint64
    }
}

func (c *ConcurrentCache) Get(key string) (interface{}, bool) {
    value, found := c.items.Load(key)
    if found {
        atomic.AddUint64(&c.stats.hits, 1)
    } else {
        atomic.AddUint64(&c.stats.misses, 1)
    }
    return value, found
}

func (c *ConcurrentCache) Set(key string, value interface{}) {
    c.items.Store(key, value)
}

func (c *ConcurrentCache) GetOrCompute(key string, compute func() interface{}) interface{} {
    // Try to load existing value
    if value, ok := c.items.Load(key); ok {
        return value
    }
    
    // Compute and store
    newValue := compute()
    actual, _ := c.items.LoadOrStore(key, newValue)
    return actual
}

// Session store with expiration
type SessionStore struct {
    sessions sync.Map
}

type Session struct {
    ID        string
    Data      interface{}
    ExpiresAt time.Time
}

func (s *SessionStore) Get(id string) (*Session, bool) {
    value, ok := s.sessions.Load(id)
    if !ok {
        return nil, false
    }
    
    session := value.(*Session)
    if time.Now().After(session.ExpiresAt) {
        s.sessions.Delete(id)
        return nil, false
    }
    
    return session, true
}

func (s *SessionStore) CleanExpired() {
    now := time.Now()
    s.sessions.Range(func(key, value interface{}) bool {
        session := value.(*Session)
        if now.After(session.ExpiresAt) {
            s.sessions.Delete(key)
        }
        return true
    })
}

// Type-safe wrapper around sync.Map
type SafeStringMap struct {
    m sync.Map
}

func (sm *SafeStringMap) Store(key string, value string) {
    sm.m.Store(key, value)
}

func (sm *SafeStringMap) Load(key string) (string, bool) {
    value, ok := sm.m.Load(key)
    if !ok {
        return "", false
    }
    return value.(string), true
}

func (sm *SafeStringMap) Range(f func(key, value string) bool) {
    sm.m.Range(func(k, v interface{}) bool {
        return f(k.(string), v.(string))
    })
}

// Comparison: sync.Map vs regular map with mutex
func benchmark() {
    const numGoroutines = 100
    const numOperations = 10000
    
    // Regular map with RWMutex
    regularMap := &struct {
        sync.RWMutex
        m map[string]int
    }{m: make(map[string]int)}
    
    // sync.Map
    var syncMap sync.Map
    
    // Benchmark will show sync.Map is faster for:
    // 1. Many goroutines, few keys (key contention)
    // 2. Mostly reads with rare writes
    // 3. Keys are written once but read many times
}
```

**When to use ``sync.Map``:**

- **(1) Write-once, read-many:** Keys are only written once but read frequently
- **(2) Disjoint key sets:** Different goroutines access different keys
- **NOT for:** General purpose concurrent map (use regular map + mutex)

**``sync.Map`` Performance Characteristics:**

- No need for entire map locking
- Copy-on-write for read-mostly scenarios
- Lock-free reads in common cases
- More memory overhead than regular map

### ``sync.Pool`` (Object Pooling)

Pool provides a cache of temporary objects that can be reused, reducing GC pressure.

```go
// Basic Pool usage
var bufferPool = sync.Pool{
    New: func() interface{} {
        // Create new buffer when pool is empty
        return new(bytes.Buffer)
    },
}

func processData(data []byte) string {
    // Get buffer from pool
    buf := bufferPool.Get().(*bytes.Buffer)
    defer func() {
        buf.Reset()  // Clean before returning
        bufferPool.Put(buf)
    }()
    
    // Use buffer
    buf.Write(data)
    buf.WriteString(" processed")
    return buf.String()
}

// Sized buffer pool
type BufferPool struct {
    pool sync.Pool
}

func NewBufferPool(size int) *BufferPool {
    return &BufferPool{
        pool: sync.Pool{
            New: func() interface{} {
                return make([]byte, size)
            },
        },
    }
}

func (p *BufferPool) Get() []byte {
    return p.pool.Get().([]byte)
}

func (p *BufferPool) Put(buf []byte) {
    // Clear sensitive data before returning
    for i := range buf {
        buf[i] = 0
    }
    p.pool.Put(buf)
}

// Connection pool pattern
type ConnPool struct {
    pool sync.Pool
    dial func() (net.Conn, error)
}

func NewConnPool(dial func() (net.Conn, error)) *ConnPool {
    return &ConnPool{
        dial: dial,
        pool: sync.Pool{
            New: func() interface{} {
                conn, err := dial()
                if err != nil {
                    return err
                }
                return conn
            },
        },
    }
}

func (p *ConnPool) Get() (net.Conn, error) {
    v := p.pool.Get()
    if err, ok := v.(error); ok {
        return nil, err
    }
    return v.(net.Conn), nil
}

func (p *ConnPool) Put(conn net.Conn) {
    if conn != nil {
        p.pool.Put(conn)
    }
}

// JSON encoder pool
var encoderPool = sync.Pool{
    New: func() interface{} {
        return json.NewEncoder(nil)
    },
}

func encodeJSON(w io.Writer, v interface{}) error {
    enc := encoderPool.Get().(*json.Encoder)
    defer encoderPool.Put(enc)
    
    enc.SetOutput(w)
    err := enc.Encode(v)
    enc.SetOutput(nil)  // Clear writer reference
    
    return err
}

// Benchmark showing Pool benefits
func benchmarkWithPool() {
    data := make([]byte, 1024)
    
    // Without pool - allocates every time
    for i := 0; i < 1000000; i++ {
        buf := make([]byte, 1024)
        copy(buf, data)
        _ = buf
    }
    
    // With pool - reuses allocations
    pool := sync.Pool{
        New: func() interface{} {
            return make([]byte, 1024)
        },
    }
    
    for i := 0; i < 1000000; i++ {
        buf := pool.Get().([]byte)
        copy(buf, data)
        pool.Put(buf)
    }
}

// Pool with statistics
type MonitoredPool struct {
    pool     sync.Pool
    created  uint64
    reused   uint64
    returned uint64
}

func (p *MonitoredPool) Get() interface{} {
    v := p.pool.Get()
    if v == nil {
        atomic.AddUint64(&p.created, 1)
        v = p.pool.New()
    } else {
        atomic.AddUint64(&p.reused, 1)
    }
    return v
}

func (p *MonitoredPool) Put(v interface{}) {
    atomic.AddUint64(&p.returned, 1)
    p.pool.Put(v)
}
```

**Pool Characteristics:**

- **GC interaction:** Objects may be removed during GC
- **Thread-safe:** Safe for concurrent use
- **No size limit:** Pool can grow unbounded
- **Temporary storage:** Not for permanent caching
- **Per-P storage:** Each P has local pool storage

**Pool Best Practices:**

- Clean objects before returning to pool
- Don't store pointers to pool objects
- Use for frequently allocated temporary objects
- Not suitable for connection pooling (use channels)

### ``sync.Cond``

Cond implements a condition variable for goroutine coordination when waiting for/announcing condition changes.

```go
// Basic Cond usage
type Queue struct {
    items []interface{}
    cond  *sync.Cond
}

func NewQueue() *Queue {
    return &Queue{
        cond: sync.NewCond(&sync.Mutex{}),
    }
}

func (q *Queue) Put(item interface{}) {
    q.cond.L.Lock()
    defer q.cond.L.Unlock()
    
    q.items = append(q.items, item)
    q.cond.Signal()  // Wake one waiting goroutine
}

func (q *Queue) Get() interface{} {
    q.cond.L.Lock()
    defer q.cond.L.Unlock()
    
    for len(q.items) == 0 {
        q.cond.Wait()  // Releases lock and waits
    }
    
    item := q.items[0]
    q.items = q.items[1:]
    return item
}

// Broadcast example
type Barrier struct {
    n       int
    count   int
    cond    *sync.Cond
}

func NewBarrier(n int) *Barrier {
    return &Barrier{
        n:    n,
        cond: sync.NewCond(&sync.Mutex{}),
    }
}

func (b *Barrier) Wait() {
    b.cond.L.Lock()
    defer b.cond.L.Unlock()
    
    b.count++
    if b.count == b.n {
        b.count = 0
        b.cond.Broadcast()  // Wake all waiting goroutines
        return
    }
    
    b.cond.Wait()
}

// Producer-consumer with condition
type BoundedBuffer struct {
    buffer   []interface{}
    capacity int
    mu       sync.Mutex
    notFull  *sync.Cond
    notEmpty *sync.Cond
}

func NewBoundedBuffer(capacity int) *BoundedBuffer {
    bb := &BoundedBuffer{
        buffer:   make([]interface{}, 0, capacity),
        capacity: capacity,
    }
    bb.notFull = sync.NewCond(&bb.mu)
    bb.notEmpty = sync.NewCond(&bb.mu)
    return bb
}

func (bb *BoundedBuffer) Put(item interface{}) {
    bb.mu.Lock()
    defer bb.mu.Unlock()
    
    for len(bb.buffer) == bb.capacity {
        bb.notFull.Wait()  // Wait until not full
    }
    
    bb.buffer = append(bb.buffer, item)
    bb.notEmpty.Signal()  // Signal that buffer is not empty
}

func (bb *BoundedBuffer) Get() interface{} {
    bb.mu.Lock()
    defer bb.mu.Unlock()
    
    for len(bb.buffer) == 0 {
        bb.notEmpty.Wait()  // Wait until not empty
    }
    
    item := bb.buffer[0]
    bb.buffer = bb.buffer[1:]
    bb.notFull.Signal()  // Signal that buffer is not full
    
    return item
}

// Read-write lock with condition
type RWCond struct {
    readers int
    writers int
    mu      sync.Mutex
    cond    *sync.Cond
}

func NewRWCond() *RWCond {
    rwc := &RWCond{}
    rwc.cond = sync.NewCond(&rwc.mu)
    return rwc
}

func (rwc *RWCond) RLock() {
    rwc.mu.Lock()
    defer rwc.mu.Unlock()
    
    for rwc.writers > 0 {
        rwc.cond.Wait()
    }
    rwc.readers++
}

func (rwc *RWCond) RUnlock() {
    rwc.mu.Lock()
    defer rwc.mu.Unlock()
    
    rwc.readers--
    if rwc.readers == 0 {
        rwc.cond.Broadcast()
    }
}
```

**Cond Methods:**

- **Wait():** Atomically unlocks mutex and waits
- **Signal():** Wakes one waiting goroutine
- **Broadcast():** Wakes all waiting goroutines

**Cond vs Channels:**

- Use Cond for: Multiple waiters, complex conditions
- Use channels for: Simple signaling, passing data

## 8.5 Atomic Operations

The atomic package provides low-level atomic memory operations for lock-free programming.

### Atomic Package

Atomic operations are indivisible - they complete entirely or not at all, without interference from other goroutines.

```go
import (
    "sync/atomic"
    "runtime"
)

// Basic atomic operations
func basicAtomic() {
    var counter int64
    
    // Add
    atomic.AddInt64(&counter, 1)
    atomic.AddInt64(&counter, -1)  // Subtraction
    
    // Load
    value := atomic.LoadInt64(&counter)
    
    // Store
    atomic.StoreInt64(&counter, 100)
    
    // Swap
    old := atomic.SwapInt64(&counter, 200)
    
    // Compare and Swap (CAS)
    swapped := atomic.CompareAndSwapInt64(&counter, 200, 300)
    // Returns true if value was 200 and changed to 300
}

// Atomic counter
type AtomicCounter struct {
    value int64
}

func (c *AtomicCounter) Increment() int64 {
    return atomic.AddInt64(&c.value, 1)
}

func (c *AtomicCounter) Decrement() int64 {
    return atomic.AddInt64(&c.value, -1)
}

func (c *AtomicCounter) Get() int64 {
    return atomic.LoadInt64(&c.value)
}

func (c *AtomicCounter) Set(v int64) {
    atomic.StoreInt64(&c.value, v)
}

func (c *AtomicCounter) CompareAndSwap(old, new int64) bool {
    return atomic.CompareAndSwapInt64(&c.value, old, new)
}

// Atomic boolean
type AtomicBool struct {
    value uint32
}

func (b *AtomicBool) Set(v bool) {
    var i uint32
    if v {
        i = 1
    }
    atomic.StoreUint32(&b.value, i)
}

func (b *AtomicBool) Get() bool {
    return atomic.LoadUint32(&b.value) != 0
}

func (b *AtomicBool) Toggle() bool {
    for {
        old := atomic.LoadUint32(&b.value)
        new := 1 - old  // Toggle between 0 and 1
        if atomic.CompareAndSwapUint32(&b.value, old, new) {
            return new != 0
        }
    }
}

// Atomic pointer operations
type Node struct {
    value int
    next  *Node
}

type AtomicStack struct {
    head unsafe.Pointer  // *Node
}

func (s *AtomicStack) Push(v int) {
    node := &Node{value: v}
    for {
        head := atomic.LoadPointer(&s.head)
        node.next = (*Node)(head)
        if atomic.CompareAndSwapPointer(&s.head, head, unsafe.Pointer(node)) {
            return
        }
    }
}

func (s *AtomicStack) Pop() (int, bool) {
    for {
        head := atomic.LoadPointer(&s.head)
        if head == nil {
            return 0, false
        }
        
        node := (*Node)(head)
        if atomic.CompareAndSwapPointer(&s.head, head, unsafe.Pointer(node.next)) {
            return node.value, true
        }
    }
}

// atomic.Value for complex types
type Config struct {
    Timeout  time.Duration
    MaxConns int
    Endpoint string
}

type AtomicConfig struct {
    v atomic.Value
}

func (c *AtomicConfig) Load() *Config {
    cfg := c.v.Load()
    if cfg == nil {
        return nil
    }
    return cfg.(*Config)
}

func (c *AtomicConfig) Store(cfg *Config) {
    c.v.Store(cfg)
}

func (c *AtomicConfig) Update(f func(*Config) *Config) {
    for {
        old := c.Load()
        new := f(old)
        
        // This is not truly atomic update
        // Use Mutex for complex atomic updates
        c.Store(new)
        break
    }
}

// Wait-free statistics
type Stats struct {
    requests uint64
    errors   uint64
    bytes    uint64
}

func (s *Stats) RecordRequest(size int, err error) {
    atomic.AddUint64(&s.requests, 1)
    atomic.AddUint64(&s.bytes, uint64(size))
    if err != nil {
        atomic.AddUint64(&s.errors, 1)
    }
}

func (s *Stats) Snapshot() Stats {
    return Stats{
        requests: atomic.LoadUint64(&s.requests),
        errors:   atomic.LoadUint64(&s.errors),
        bytes:    atomic.LoadUint64(&s.bytes),
    }
}

// Spin lock using atomic
type SpinLock struct {
    locked uint32
}

func (s *SpinLock) Lock() {
    for !atomic.CompareAndSwapUint32(&s.locked, 0, 1) {
        runtime.Gosched()  // Yield to other goroutines
    }
}

func (s *SpinLock) Unlock() {
    atomic.StoreUint32(&s.locked, 0)
}

func (s *SpinLock) TryLock() bool {
    return atomic.CompareAndSwapUint32(&s.locked, 0, 1)
}

// Atomic generation counter
type Generation struct {
    value uint64
}

func (g *Generation) Next() uint64 {
    return atomic.AddUint64(&g.value, 1)
}

func (g *Generation) Current() uint64 {
    return atomic.LoadUint64(&g.value)
}

// Reference counting
type RefCounted struct {
    refs int64
    data interface{}
}

func (r *RefCounted) Retain() {
    atomic.AddInt64(&r.refs, 1)
}

func (r *RefCounted) Release() {
    if atomic.AddInt64(&r.refs, -1) == 0 {
        // Last reference, cleanup
        r.cleanup()
    }
}

func (r *RefCounted) cleanup() {
    // Cleanup resources
    r.data = nil
}
```

**Atomic Types Supported:**

- **int32, int64:** AddInt32/64, LoadInt32/64, StoreInt32/64, SwapInt32/64, CompareAndSwapInt32/64
- **uint32, uint64:** Same operations with Uint prefix
- **uintptr:** For pointer arithmetic
- **unsafe.Pointer:** AtomicPointer operations
- **atomic.Value:** Store/Load for any type (interface{})

### When to Use Atomic vs Mutex

The choice between atomic operations and mutexes depends on the complexity of the operation and performance requirements.

```go
// Simple counter - Atomic is better
type CounterComparison struct {
    // Atomic version - faster for high contention
    atomicCount int64
    
    // Mutex version - slower but more flexible
    mu         sync.Mutex
    mutexCount int64
}

func (c *CounterComparison) IncrementAtomic() {
    atomic.AddInt64(&c.atomicCount, 1)
}

func (c *CounterComparison) IncrementMutex() {
    c.mu.Lock()
    c.mutexCount++
    c.mu.Unlock()
}

// Complex operation - Mutex is better
type BankAccount struct {
    mu      sync.Mutex
    balance int64
    history []Transaction
}

func (a *BankAccount) Withdraw(amount int64) error {
    a.mu.Lock()
    defer a.mu.Unlock()
    
    if a.balance < amount {
        return ErrInsufficientFunds
    }
    
    a.balance -= amount
    a.history = append(a.history, Transaction{
        Type:   "withdrawal",
        Amount: amount,
        Time:   time.Now(),
    })
    
    return nil
}

// Flag checking - Atomic is perfect
type Service struct {
    running uint32
    // other fields
}

func (s *Service) Start() {
    if !atomic.CompareAndSwapUint32(&s.running, 0, 1) {
        return  // Already running
    }
    // Start service
}

func (s *Service) Stop() {
    if !atomic.CompareAndSwapUint32(&s.running, 1, 0) {
        return  // Not running
    }
    // Stop service
}

func (s *Service) IsRunning() bool {
    return atomic.LoadUint32(&s.running) != 0
}

// Configuration updates - atomic.Value
type Server struct {
    config atomic.Value  // stores *Config
}

func (s *Server) UpdateConfig(cfg *Config) {
    s.config.Store(cfg)
}

func (s *Server) GetConfig() *Config {
    return s.config.Load().(*Config)
}

// When atomic becomes complex - use mutex
type ComplexCounter struct {
    mu    sync.Mutex
    value int64
    max   int64
}

func (c *ComplexCounter) IncrementWithMax(delta int64) (int64, error) {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    if c.value+delta > c.max {
        return c.value, ErrMaxExceeded
    }
    
    c.value += delta
    return c.value, nil
}

// Performance comparison
func benchmark() {
    const goroutines = 100
    const iterations = 1000000
    
    // Atomic counter
    var atomicCounter int64
    var wg sync.WaitGroup
    
    start := time.Now()
    for i := 0; i < goroutines; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            for j := 0; j < iterations; j++ {
                atomic.AddInt64(&atomicCounter, 1)
            }
        }()
    }
    wg.Wait()
    atomicTime := time.Since(start)
    
    // Mutex counter
    var mutexCounter int64
    var mu sync.Mutex
    
    start = time.Now()
    for i := 0; i < goroutines; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            for j := 0; j < iterations; j++ {
                mu.Lock()
                mutexCounter++
                mu.Unlock()
            }
        }()
    }
    wg.Wait()
    mutexTime := time.Since(start)
    
    fmt.Printf("Atomic: %v\n", atomicTime)  // Much faster
    fmt.Printf("Mutex: %v\n", mutexTime)
}

// Hybrid approach
type HybridStats struct {
    // Use atomic for simple counters
    requests uint64
    errors   uint64
    
    // Use mutex for complex state
    mu          sync.RWMutex
    percentiles []float64
    histogram   map[int]int
}

func (s *HybridStats) RecordRequest(latency time.Duration, err error) {
    atomic.AddUint64(&s.requests, 1)
    
    if err != nil {
        atomic.AddUint64(&s.errors, 1)
    }
    
    // Complex operation needs mutex
    s.mu.Lock()
    s.updatePercentiles(latency)
    s.histogram[int(latency.Milliseconds())]++
    s.mu.Unlock()
}
```

**When to Use Atomic:**

- **Simple operations:** Counter increment/decrement
- **Single variable:** Operating on one memory location
- **High contention:** Many goroutines accessing same data
- **Lock-free required:** Real-time systems, interrupts
- **Read-heavy:** atomic.Value for read-mostly data
- **Flags/State:** Simple boolean or enum states

**When to Use Mutex:**

- **Complex operations:** Multiple steps must be atomic
- **Multiple variables:** Coordinated access to several fields
- **Conditional logic:** If-then operations
- **Data structures:** Maps, slices, complex types
- **Read-modify-write:** When logic depends on read value
- **Error handling:** Operations that can fail

**Performance Characteristics:**

|Aspect|Atomic|Mutex|
|---|---|---|
|**Speed**|Very fast (hardware level)|Slower (OS involvement)|
|**Contention**|No blocking|Can cause blocking|
|**Complexity**|Simple operations only|Any complexity|
|**Memory**|Minimal overhead|Mutex structure overhead|
|**Fairness**|No guarantee|Fair scheduling|
|**Debugging**|Harder to debug|Easier with tools|

**Common Patterns:**

```go
// 1. Toggle pattern
type Toggle struct {
    state uint32
}

func (t *Toggle) Toggle() bool {
    return atomic.AddUint32(&t.state, 1)%2 == 0
}

// 2. Once pattern without sync.Once
type OnceFlag struct {
    done uint32
}

func (o *OnceFlag) Do(f func()) {
    if atomic.CompareAndSwapUint32(&o.done, 0, 1) {
        f()
    }
}

// 3. Sequence number
type Sequence struct {
    value uint64
}

func (s *Sequence) Next() uint64 {
    return atomic.AddUint64(&s.value, 1)
}

// 4. Rate limiter
type RateLimiter struct {
    tokens uint64
    max    uint64
}

func (r *RateLimiter) Allow() bool {
    for {
        current := atomic.LoadUint64(&r.tokens)
        if current == 0 {
            return false
        }
        if atomic.CompareAndSwapUint64(&r.tokens, current, current-1) {
            return true
        }
    }
}
```

**Best Practices:**

1. **Start with mutex:** Optimize to atomic only if needed
2. **Benchmark both:** Performance varies with workload
3. **Document memory model:** Atomic operations can be subtle
4. **Avoid clever tricks:** Maintainability over micro-optimization
5. **Use atomic.Value carefully:** Only for immutable data
6. **Memory alignment:** 64-bit atomics need 64-bit alignment
7. **Test with race detector:** `go test -race`

**Common Pitfalls:**

- Non-atomic read-modify-write with atomics
- Assuming atomic operations provide ordering guarantees
- Using atomic.Value with mutable data
- Forgetting memory alignment on 32-bit systems
- Over-optimizing with atomics when mutex is clearer

## 8.6 Context Package

The context package provides a way to carry deadlines, cancellation signals, and request-scoped values across API boundaries and between goroutines. It's essential for managing the lifecycle of operations in concurrent Go programs.

**Core Concept:** Context flows through your program like a river, carrying cancellation signals and deadlines downstream to all derived operations.

### What is Context?

Context is an interface that carries deadlines, cancellation signals, and request-scoped values across API boundaries. It's designed to be passed as the first parameter of functions, especially in concurrent operations.

```go
// The Context interface
type Context interface {
    // Deadline returns the time when work should be canceled
    Deadline() (deadline time.Time, ok bool)
    
    // Done returns a channel that's closed when work should be canceled
    Done() <-chan struct{}
    
    // Err returns nil if Done is not closed, or explains why it was canceled
    Err() error
    
    // Value returns the value associated with key, or nil
    Value(key interface{}) interface{}
}
```

**Why Context Exists:**

- **Cancellation propagation:** Cancel entire trees of goroutines
- **Deadline enforcement:** Ensure operations complete within time limits
- **Request-scoped data:** Carry request IDs, user info, etc.
- **Standardization:** Common pattern across all Go code

### Context Creation and Hierarchy

Contexts form a tree structure where cancellation flows from parent to children:

```go
import (
    "context"
    "time"
)

// Root contexts (never cancel these)
func rootContexts() {
    // Background context - top level, never canceled
    ctx := context.Background()
    
    // TODO context - placeholder when unsure which context to use
    ctx = context.TODO()
    
    // Both are essentially empty contexts
    // Background() for main, init, tests
    // TODO() as placeholder during refactoring
}

// Context derivation tree
func contextHierarchy() {
    // Root
    root := context.Background()
    
    // Level 1: Add cancellation
    ctx1, cancel1 := context.WithCancel(root)
    defer cancel1()
    
    // Level 2: Add timeout to ctx1
    ctx2, cancel2 := context.WithTimeout(ctx1, 5*time.Second)
    defer cancel2()
    
    // Level 3: Add value to ctx2
    ctx3 := context.WithValue(ctx2, "userID", "123")
    
    // When cancel1() is called, ctx1, ctx2, and ctx3 all get canceled
    // When ctx2 times out, ctx2 and ctx3 get canceled (ctx1 remains)
}

// Context is immutable - derivation creates new context
func immutability() {
    ctx1 := context.Background()
    ctx2 := context.WithValue(ctx1, "key", "value")
    
    // ctx1 is unchanged, ctx2 is new context with value
    fmt.Println(ctx1.Value("key"))  // nil
    fmt.Println(ctx2.Value("key"))  // "value"
}
```

### Context for Cancellation

Cancellation is the most common use of context, allowing coordinated shutdown of goroutines:

```go
// Basic cancellation
func basicCancellation() {
    ctx, cancel := context.WithCancel(context.Background())
    
    go func() {
        for {
            select {
            case <-ctx.Done():
                fmt.Println("Goroutine canceled:", ctx.Err())
                return
            default:
                // Do work
                doWork()
                time.Sleep(100 * time.Millisecond)
            }
        }
    }()
    
    time.Sleep(1 * time.Second)
    cancel()  // Signal cancellation
    
    // ctx.Err() returns context.Canceled
}

// Cancellation propagation
func cancellationPropagation() {
    parent, parentCancel := context.WithCancel(context.Background())
    child1, child1Cancel := context.WithCancel(parent)
    child2, _ := context.WithCancel(parent)
    
    // Start workers
    go worker(child1, "worker1")
    go worker(child2, "worker2")
    
    // Canceling parent cancels all children
    parentCancel()  // Both workers stop
    
    // But canceling child doesn't affect parent or siblings
    child1Cancel()  // Only worker1 stops
}

func worker(ctx context.Context, name string) {
    for {
        select {
        case <-ctx.Done():
            fmt.Printf("%s: stopped due to %v\n", name, ctx.Err())
            return
        case <-time.After(500 * time.Millisecond):
            fmt.Printf("%s: working\n", name)
        }
    }
}

// HTTP request cancellation
func httpWithCancellation() {
    ctx, cancel := context.WithCancel(context.Background())
    defer cancel()
    
    req, err := http.NewRequestWithContext(ctx, "GET", "https://api.example.com/data", nil)
    if err != nil {
        return err
    }
    
    // Start request in goroutine
    respCh := make(chan *http.Response, 1)
    errCh := make(chan error, 1)
    
    go func() {
        resp, err := http.DefaultClient.Do(req)
        if err != nil {
            errCh <- err
            return
        }
        respCh <- resp
    }()
    
    // Cancel after 2 seconds if needed
    select {
    case resp := <-respCh:
        defer resp.Body.Close()
        // Process response
    case err := <-errCh:
        fmt.Println("Request error:", err)
    case <-time.After(2 * time.Second):
        cancel()  // Cancel the request
        fmt.Println("Request canceled due to timeout")
    }
}

// Database query cancellation
func databaseQueryWithCancel(ctx context.Context, db *sql.DB) error {
    // Query is automatically canceled if context is canceled
    rows, err := db.QueryContext(ctx, "SELECT * FROM users WHERE active = true")
    if err != nil {
        if ctx.Err() != nil {
            return fmt.Errorf("query canceled: %w", ctx.Err())
        }
        return err
    }
    defer rows.Close()
    
    for rows.Next() {
        // Check for cancellation during iteration
        select {
        case <-ctx.Done():
            return ctx.Err()
        default:
        }
        
        // Process row
        var user User
        if err := rows.Scan(&user); err != nil {
            return err
        }
        processUser(user)
    }
    
    return rows.Err()
}

// Graceful shutdown pattern
type Server struct {
    ctx    context.Context
    cancel context.CancelFunc
}

func NewServer() *Server {
    ctx, cancel := context.WithCancel(context.Background())
    return &Server{ctx: ctx, cancel: cancel}
}

func (s *Server) Run() {
    // Start multiple components
    go s.handleHTTP()
    go s.processQueue()
    go s.monitorHealth()
    
    // Wait for shutdown signal
    sigCh := make(chan os.Signal, 1)
    signal.Notify(sigCh, os.Interrupt, syscall.SIGTERM)
    
    select {
    case <-sigCh:
        fmt.Println("Shutdown signal received")
    case <-s.ctx.Done():
        fmt.Println("Context canceled")
    }
    
    // Trigger graceful shutdown
    s.Shutdown()
}

func (s *Server) Shutdown() {
    fmt.Println("Starting graceful shutdown...")
    
    // Cancel context to signal all goroutines
    s.cancel()
    
    // Wait for cleanup with timeout
    shutdownCtx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
    defer cancel()
    
    // Wait for components to finish
    <-shutdownCtx.Done()
    
    if shutdownCtx.Err() == context.DeadlineExceeded {
        fmt.Println("Forced shutdown after timeout")
    } else {
        fmt.Println("Graceful shutdown complete")
    }
}
```

### Context for Deadlines

Deadlines ensure operations complete within specified time limits:

```go
// WithTimeout - duration from now
func withTimeout() {
    ctx, cancel := context.WithTimeout(context.Background(), 3*time.Second)
    defer cancel()  // Important: always call cancel to release resources
    
    select {
    case <-time.After(5 * time.Second):
        fmt.Println("Operation completed")
    case <-ctx.Done():
        fmt.Println("Timeout:", ctx.Err())  // context.DeadlineExceeded
    }
}

// WithDeadline - specific time
func withDeadline() {
    deadline := time.Now().Add(10 * time.Second)
    ctx, cancel := context.WithDeadline(context.Background(), deadline)
    defer cancel()
    
    // Check if context has deadline
    if deadline, ok := ctx.Deadline(); ok {
        fmt.Println("Operation must complete by:", deadline)
    }
    
    // Check remaining time
    remaining := time.Until(deadline)
    fmt.Printf("Time remaining: %v\n", remaining)
}

// Cascading timeouts
func cascadingTimeouts() {
    // Parent: 5 seconds total
    parentCtx, parentCancel := context.WithTimeout(context.Background(), 5*time.Second)
    defer parentCancel()
    
    // Child operations with their own timeouts
    results := make(chan Result, 3)
    
    // Operation 1: max 2 seconds
    go func() {
        ctx, cancel := context.WithTimeout(parentCtx, 2*time.Second)
        defer cancel()
        results <- fetchData(ctx, "source1")
    }()
    
    // Operation 2: max 3 seconds
    go func() {
        ctx, cancel := context.WithTimeout(parentCtx, 3*time.Second)
        defer cancel()
        results <- fetchData(ctx, "source2")
    }()
    
    // Operation 3: inherits parent timeout
    go func() {
        results <- fetchData(parentCtx, "source3")
    }()
    
    // Collect results
    for i := 0; i < 3; i++ {
        select {
        case result := <-results:
            fmt.Println("Got result:", result)
        case <-parentCtx.Done():
            fmt.Println("Parent timeout reached")
            return
        }
    }
}

// Deadline-aware operations
func deadlineAwareOperation(ctx context.Context) error {
    deadline, hasDeadline := ctx.Deadline()
    if !hasDeadline {
        // No deadline, proceed normally
        return longRunningOperation()
    }
    
    remaining := time.Until(deadline)
    if remaining < 100*time.Millisecond {
        // Not enough time
        return fmt.Errorf("insufficient time remaining: %v", remaining)
    }
    
    // Adjust operation based on deadline
    if remaining < 1*time.Second {
        return quickOperation()  // Use faster algorithm
    }
    
    return normalOperation()
}

// Timeout renewal pattern
func renewableTimeout(baseTimeout time.Duration) {
    ctx := context.Background()
    
    for {
        // Create new timeout for each iteration
        iterCtx, cancel := context.WithTimeout(ctx, baseTimeout)
        
        err := doWorkWithTimeout(iterCtx)
        cancel()  // Clean up immediately
        
        if err != nil {
            if err == context.DeadlineExceeded {
                fmt.Println("Operation timed out, retrying...")
                continue
            }
            fmt.Println("Operation failed:", err)
            break
        }
        
        fmt.Println("Operation succeeded")
        break
    }
}

// SLA enforcement
func enforceSLA(ctx context.Context, sla time.Duration) error {
    // Ensure we meet SLA regardless of parent context
    slaCtx, cancel := context.WithTimeout(ctx, sla)
    defer cancel()
    
    done := make(chan error, 1)
    
    go func() {
        done <- performOperation(slaCtx)
    }()
    
    select {
    case err := <-done:
        return err
    case <-slaCtx.Done():
        // Log SLA violation
        logSLAViolation(sla)
        return fmt.Errorf("SLA exceeded: %v", sla)
    }
}
```

### Context for Values

Context can carry request-scoped values, but should be used sparingly:

```go
// Context key best practice - use custom type
type contextKey string

const (
    userIDKey     contextKey = "userID"
    requestIDKey  contextKey = "requestID"
    sessionKey    contextKey = "session"
)

// Adding values to context
func addingValues() {
    ctx := context.Background()
    
    // Add user ID
    ctx = context.WithValue(ctx, userIDKey, "user-123")
    
    // Add request ID
    ctx = context.WithValue(ctx, requestIDKey, "req-abc-456")
    
    // Add session
    ctx = context.WithValue(ctx, sessionKey, &Session{
        ID:        "sess-789",
        UserID:    "user-123",
        ExpiresAt: time.Now().Add(24 * time.Hour),
    })
    
    processRequest(ctx)
}

// Retrieving values safely
func getUserID(ctx context.Context) (string, bool) {
    userID, ok := ctx.Value(userIDKey).(string)
    return userID, ok
}

func getRequestID(ctx context.Context) string {
    if reqID, ok := ctx.Value(requestIDKey).(string); ok {
        return reqID
    }
    return "unknown"
}

func getSession(ctx context.Context) *Session {
    if session, ok := ctx.Value(sessionKey).(*Session); ok {
        return session
    }
    return nil
}

// Middleware pattern for adding values
func authMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        // Extract auth token
        token := r.Header.Get("Authorization")
        
        // Validate and get user
        user, err := validateToken(token)
        if err != nil {
            http.Error(w, "Unauthorized", http.StatusUnauthorized)
            return
        }
        
        // Add user to context
        ctx := context.WithValue(r.Context(), userIDKey, user.ID)
        ctx = context.WithValue(ctx, "user", user)
        
        // Pass along with enriched context
        next.ServeHTTP(w, r.WithContext(ctx))
    })
}

func requestIDMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        requestID := r.Header.Get("X-Request-ID")
        if requestID == "" {
            requestID = generateRequestID()
        }
        
        ctx := context.WithValue(r.Context(), requestIDKey, requestID)
        
        // Add to response headers
        w.Header().Set("X-Request-ID", requestID)
        
        next.ServeHTTP(w, r.WithContext(ctx))
    })
}

// Logging with context values
type Logger struct{}

func (l *Logger) Log(ctx context.Context, level, message string) {
    fields := map[string]interface{}{
        "level":   level,
        "message": message,
        "time":    time.Now(),
    }
    
    // Add context values
    if userID, ok := getUserID(ctx); ok {
        fields["user_id"] = userID
    }
    
    if reqID := getRequestID(ctx); reqID != "" {
        fields["request_id"] = reqID
    }
    
    // Output structured log
    fmt.Printf("%+v\n", fields)
}

// Tracing across service boundaries
func makeServiceCall(ctx context.Context, url string) (*http.Response, error) {
    req, err := http.NewRequestWithContext(ctx, "GET", url, nil)
    if err != nil {
        return nil, err
    }
    
    // Propagate trace context
    if traceID := getTraceID(ctx); traceID != "" {
        req.Header.Set("X-Trace-ID", traceID)
    }
    
    if spanID := getSpanID(ctx); spanID != "" {
        req.Header.Set("X-Span-ID", spanID)
    }
    
    return http.DefaultClient.Do(req)
}
```

**What NOT to Store in Context:**

- Optional function parameters
- Database connections
- Configuration values
- Large objects
- Mutable state

**What to Store in Context:**

- Request IDs for tracing
- User authentication info
- Request deadlines
- Cancellation signals

### Context Best Practices

**1. Context as First Parameter**

```go
// GOOD - context is first parameter
func GetUser(ctx context.Context, userID string) (*User, error) {
    // Implementation
}

// BAD - context not first
func GetUser(userID string, ctx context.Context) (*User, error) {
    // Don't do this
}

// BAD - context in struct (usually)
type UserService struct {
    ctx context.Context  // Avoid storing context
}
```

**2. Never Store Context in Structs (with rare exceptions)**

```go
// BAD - storing context in struct
type BadWorker struct {
    ctx context.Context  // This context might be canceled unexpectedly
}

// GOOD - pass context to methods
type GoodWorker struct {
    // Worker fields
}

func (w *GoodWorker) DoWork(ctx context.Context) error {
    // Use passed context
}

// EXCEPTION - request-scoped structs
type Request struct {
    ctx context.Context  // OK for request lifetime
    // Other request fields
}
```

**3. Always Call Cancel**

```go
// GOOD - using defer
func goodExample() {
    ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
    defer cancel()  // Always call cancel
    
    doWork(ctx)
}

// BAD - forgetting cancel
func badExample() {
    ctx, _ := context.WithTimeout(context.Background(), 5*time.Second)
    // Cancel not called - resource leak!
    doWork(ctx)
}

// GOOD - cleanup pattern
func cleanupPattern() error {
    ctx, cancel := context.WithCancel(context.Background())
    
    // Ensure cleanup on all paths
    defer func() {
        cancel()
        cleanup()
    }()
    
    if err := operation1(ctx); err != nil {
        return err  // defer still runs
    }
    
    if err := operation2(ctx); err != nil {
        return err  // defer still runs
    }
    
    return nil
}
```

**4. Don't Pass nil Context**

```go
// BAD - passing nil
func badCall() {
    ProcessData(nil, data)  // Will likely panic
}

// GOOD - use TODO if context unclear
func goodCall() {
    ProcessData(context.TODO(), data)
}

// BETTER - use appropriate context
func betterCall(ctx context.Context) {
    ProcessData(ctx, data)
}
```

**5. Context Value Keys**

```go
// BAD - using string keys directly
ctx = context.WithValue(ctx, "user", user)  // Collision prone

// GOOD - custom type for keys
type contextKey int

const userKey contextKey = iota

ctx = context.WithValue(ctx, userKey, user)

// BETTER - package-private key types
type userKeyType struct{}

var userContextKey = userKeyType{}

func WithUser(ctx context.Context, user *User) context.Context {
    return context.WithValue(ctx, userContextKey, user)
}

func UserFromContext(ctx context.Context) (*User, bool) {
    user, ok := ctx.Value(userContextKey).(*User)
    return user, ok
}
```

### Real-World Context Patterns

```go
// Repository pattern with context
type UserRepository struct {
    db *sql.DB
}

func (r *UserRepository) GetByID(ctx context.Context, id string) (*User, error) {
    // Respect context cancellation
    var user User
    
    query := "SELECT id, name, email FROM users WHERE id = $1"
    err := r.db.QueryRowContext(ctx, query, id).Scan(&user.ID, &user.Name, &user.Email)
    
    if err == sql.ErrNoRows {
        return nil, ErrNotFound
    }
    if err != nil {
        return nil, fmt.Errorf("query user: %w", err)
    }
    
    return &user, nil
}

func (r *UserRepository) List(ctx context.Context, limit, offset int) ([]*User, error) {
    query := "SELECT id, name, email FROM users LIMIT $1 OFFSET $2"
    rows, err := r.db.QueryContext(ctx, query, limit, offset)
    if err != nil {
        return nil, err
    }
    defer rows.Close()
    
    var users []*User
    for rows.Next() {
        // Check context in long loops
        if ctx.Err() != nil {
            return nil, ctx.Err()
        }
        
        var user User
        if err := rows.Scan(&user.ID, &user.Name, &user.Email); err != nil {
            return nil, err
        }
        users = append(users, &user)
    }
    
    return users, rows.Err()
}

// Service layer with context
type UserService struct {
    repo  *UserRepository
    cache *Cache
    log   *Logger
}

func (s *UserService) GetUser(ctx context.Context, id string) (*User, error) {
    // Add tracing span
    ctx, span := trace.StartSpan(ctx, "UserService.GetUser")
    defer span.End()
    
    // Check cache first
    if user, ok := s.cache.Get(ctx, id); ok {
        s.log.Info(ctx, "User found in cache")
        return user, nil
    }
    
    // Set operation timeout
    ctx, cancel := context.WithTimeout(ctx, 3*time.Second)
    defer cancel()
    
    // Get from database
    user, err := s.repo.GetByID(ctx, id)
    if err != nil {
        s.log.Error(ctx, "Failed to get user", err)
        return nil, err
    }
    
    // Update cache
    s.cache.Set(ctx, id, user)
    
    return user, nil
}

// HTTP handler with full context usage
func (s *UserService) HTTPHandler(w http.ResponseWriter, r *http.Request) {
    // Extract request ID or generate new one
    requestID := r.Header.Get("X-Request-ID")
    if requestID == "" {
        requestID = uuid.New().String()
    }
    
    // Create context with request ID
    ctx := context.WithValue(r.Context(), requestIDKey, requestID)
    
    // Add timeout for entire request
    ctx, cancel := context.WithTimeout(ctx, 10*time.Second)
    defer cancel()
    
    // Log with context
    s.log.Info(ctx, "Handling user request")
    
    // Parse user ID from URL
    userID := chi.URLParam(r, "userID")
    
    // Get user with context
    user, err := s.GetUser(ctx, userID)
    if err != nil {
        if errors.Is(err, context.DeadlineExceeded) {
            http.Error(w, "Request timeout", http.StatusGatewayTimeout)
            return
        }
        if errors.Is(err, context.Canceled) {
            http.Error(w, "Request canceled", http.StatusServiceUnavailable)
            return
        }
        http.Error(w, err.Error(), http.StatusInternalServerError)
        return
    }
    
    // Return response
    w.Header().Set("X-Request-ID", requestID)
    json.NewEncoder(w).Encode(user)
}

// Background job with context
func (s *UserService) BackgroundSync(parentCtx context.Context) {
    // Create independent context for background job
    ctx, cancel := context.WithCancel(context.Background())
    defer cancel()
    
    // Listen for parent cancellation
    go func() {
        <-parentCtx.Done()
        cancel()
    }()
    
    ticker := time.NewTicker(5 * time.Minute)
    defer ticker.Stop()
    
    for {
        select {
        case <-ticker.C:
            // Create timeout for each sync
            syncCtx, syncCancel := context.WithTimeout(ctx, 1*time.Minute)
            
            if err := s.syncUsers(syncCtx); err != nil {
                s.log.Error(syncCtx, "Sync failed", err)
            }
            
            syncCancel()
            
        case <-ctx.Done():
            s.log.Info(ctx, "Background sync stopped")
            return
        }
    }
}
```

### Advanced Context Patterns

```go
// Merge multiple contexts
func mergeContexts(ctx1, ctx2 context.Context) (context.Context, context.CancelFunc) {
    ctx, cancel := context.WithCancel(ctx1)
    
    go func() {
        select {
        case <-ctx1.Done():
            cancel()
        case <-ctx2.Done():
            cancel()
        }
    }()
    
    return ctx, cancel
}

// Context with retry
func retryWithContext(ctx context.Context, fn func(context.Context) error) error {
    backoff := 100 * time.Millisecond
    maxBackoff := 10 * time.Second
    
    for attempt := 0; ; attempt++ {
        // Create timeout for this attempt
        attemptCtx, cancel := context.WithTimeout(ctx, 5*time.Second)
        err := fn(attemptCtx)
        cancel()
        
        if err == nil {
            return nil
        }
        
        // Check if parent context is done
        if ctx.Err() != nil {
            return ctx.Err()
        }
        
        // Log retry
        log.Printf("Attempt %d failed: %v, retrying in %v", attempt+1, err, backoff)
        
        // Wait with backoff
        select {
        case <-time.After(backoff):
            backoff *= 2
            if backoff > maxBackoff {
                backoff = maxBackoff
            }
        case <-ctx.Done():
            return ctx.Err()
        }
    }
}

// Context-aware worker pool
type WorkerPool struct {
    workers int
    tasks   chan Task
    results chan Result
}

func (p *WorkerPool) Start(ctx context.Context) {
    var wg sync.WaitGroup
    
    for i := 0; i < p.workers; i++ {
        wg.Add(1)
        go func(workerID int) {
            defer wg.Done()
            
            for {
                select {
                case task, ok := <-p.tasks:
                    if !ok {
                        return
                    }
                    
                    // Process with timeout
                    taskCtx, cancel := context.WithTimeout(ctx, 30*time.Second)
                    result := p.processTask(taskCtx, task)
                    cancel()
                    
                    select {
                    case p.results <- result:
                    case <-ctx.Done():
                        return
                    }
                    
                case <-ctx.Done():
                    return
                }
            }
        }(i)
    }
    
    // Cleanup
    go func() {
        wg.Wait()
        close(p.results)
    }()
}
```

**Context Anti-patterns to Avoid:**

1. **Using context.Value for required parameters**

```go
// BAD
func badFunction(ctx context.Context) {
    db := ctx.Value("db").(*sql.DB)  // Will panic if missing
}

// GOOD
func goodFunction(ctx context.Context, db *sql.DB) {
    // Explicit parameter
}
```

2. **Storing mutable state in context**

```go
// BAD
ctx = context.WithValue(ctx, "counter", &counter)
// Multiple goroutines modifying counter = race condition

// GOOD
// Use channels or mutexes for mutable state
```

3. **Creating context in library init**

```go
// BAD
var globalCtx = context.Background()  // Don't create global contexts

// GOOD
func DoWork(ctx context.Context) {
    // Accept context as parameter
}
```

**Context Guidelines Summary:**

**DO:**

- Pass context as first parameter
- Call cancel when done (use defer)
- Use context.TODO() when refactoring
- Create child contexts for child operations
- Check ctx.Err() in loops
- Use custom types for context keys
- Respect context cancellation promptly

**DON'T:**

- Store context in structs (usually)
- Pass nil context
- Use string keys directly
- Store optional parameters
- Ignore context cancellation
- Create global contexts
- Use context.Value for required data

**When to Use Each Context Type:**

- **WithCancel:** Manual cancellation control
- **WithTimeout:** Operation has maximum duration
- **WithDeadline:** Must complete by specific time
- **WithValue:** Request-scoped metadata only

**Performance Considerations:**

- Context creation is cheap (allocation + pointer setup)
- Value lookup is O(n) through parent chain
- Cancel propagation is O(n) for child contexts
- Always cancel to free resources (goroutine + memory)

## 8.7 Concurrency Patterns

Concurrency patterns are proven solutions to common concurrent programming problems. These patterns help structure concurrent code in maintainable, efficient, and correct ways.

### Worker Pools

Worker pools manage a fixed number of goroutines to process tasks, preventing unbounded goroutine creation and controlling resource usage.

```go
// Basic worker pool
type WorkerPool struct {
    workers   int
    taskQueue chan Task
    wg        sync.WaitGroup
}

type Task interface {
    Execute() error
}

func NewWorkerPool(workers int, queueSize int) *WorkerPool {
    return &WorkerPool{
        workers:   workers,
        taskQueue: make(chan Task, queueSize),
    }
}

func (p *WorkerPool) Start() {
    for i := 0; i < p.workers; i++ {
        p.wg.Add(1)
        go p.worker(i)
    }
}

func (p *WorkerPool) worker(id int) {
    defer p.wg.Done()
    
    for task := range p.taskQueue {
        fmt.Printf("Worker %d processing task\n", id)
        if err := task.Execute(); err != nil {
            fmt.Printf("Worker %d error: %v\n", id, err)
        }
    }
}

func (p *WorkerPool) Submit(task Task) {
    p.taskQueue <- task
}

func (p *WorkerPool) Shutdown() {
    close(p.taskQueue)
    p.wg.Wait()
}

// Advanced worker pool with results
type Job struct {
    ID   int
    Data interface{}
}

type Result struct {
    JobID int
    Value interface{}
    Err   error
}

type ResultPool struct {
    workers  int
    jobs     chan Job
    results  chan Result
    done     chan struct{}
}

func NewResultPool(workers int) *ResultPool {
    return &ResultPool{
        workers: workers,
        jobs:    make(chan Job, workers*2),
        results: make(chan Result, workers*2),
        done:    make(chan struct{}),
    }
}

func (p *ResultPool) Start(ctx context.Context) {
    var wg sync.WaitGroup
    
    for i := 0; i < p.workers; i++ {
        wg.Add(1)
        go func(workerID int) {
            defer wg.Done()
            
            for {
                select {
                case job, ok := <-p.jobs:
                    if !ok {
                        return
                    }
                    
                    result := p.process(workerID, job)
                    
                    select {
                    case p.results <- result:
                    case <-ctx.Done():
                        return
                    }
                    
                case <-ctx.Done():
                    return
                }
            }
        }(i)
    }
    
    go func() {
        wg.Wait()
        close(p.results)
        close(p.done)
    }()
}

func (p *ResultPool) process(workerID int, job Job) Result {
    // Simulate work
    time.Sleep(time.Millisecond * 100)
    
    return Result{
        JobID: job.ID,
        Value: fmt.Sprintf("Processed by worker %d", workerID),
        Err:   nil,
    }
}

// Dynamic worker pool
type DynamicPool struct {
    minWorkers  int
    maxWorkers  int
    queue       chan func()
    workerCount int32
    mu          sync.Mutex
    cond        *sync.Cond
}

func NewDynamicPool(min, max int) *DynamicPool {
    p := &DynamicPool{
        minWorkers: min,
        maxWorkers: max,
        queue:      make(chan func(), max*2),
    }
    p.cond = sync.NewCond(&p.mu)
    
    // Start minimum workers
    for i := 0; i < min; i++ {
        p.addWorker()
    }
    
    // Monitor and adjust workers
    go p.monitor()
    
    return p
}

func (p *DynamicPool) addWorker() {
    atomic.AddInt32(&p.workerCount, 1)
    
    go func() {
        defer atomic.AddInt32(&p.workerCount, -1)
        
        for fn := range p.queue {
            fn()
        }
    }()
}

func (p *DynamicPool) monitor() {
    ticker := time.NewTicker(1 * time.Second)
    defer ticker.Stop()
    
    for range ticker.C {
        queueLen := len(p.queue)
        workers := atomic.LoadInt32(&p.workerCount)
        
        // Scale up if queue is backing up
        if queueLen > int(workers)*2 && workers < int32(p.maxWorkers) {
            p.addWorker()
        }
        
        // Scale down if idle (implementation depends on tracking idle workers)
        // This is simplified
    }
}

func (p *DynamicPool) Execute(fn func()) {
    p.queue <- fn
}

// Worker pool with timeout
type TimeoutPool struct {
    workers int
    tasks   chan func(context.Context) error
    timeout time.Duration
}

func (p *TimeoutPool) Start(ctx context.Context) {
    for i := 0; i < p.workers; i++ {
        go func() {
            for task := range p.tasks {
                taskCtx, cancel := context.WithTimeout(ctx, p.timeout)
                
                done := make(chan error, 1)
                go func() {
                    done <- task(taskCtx)
                }()
                
                select {
                case err := <-done:
                    if err != nil {
                        log.Printf("Task error: %v", err)
                    }
                case <-taskCtx.Done():
                    log.Printf("Task timeout")
                }
                
                cancel()
            }
        }()
    }
}
```

**Worker Pool Benefits:**

- **Resource control:** Limits concurrent operations
- **Prevents exhaustion:** Bounds memory and CPU usage
- **Queueing:** Buffers work during spikes
- **Graceful shutdown:** Clean termination
- **Error isolation:** Worker crash doesn't affect others

### Pipeline Pattern

Pipeline pattern chains processing stages where each stage receives data from the previous stage, processes it, and sends to the next stage.

```go
// Basic pipeline stages
func generator(nums ...int) <-chan int {
    out := make(chan int)
    go func() {
        for _, n := range nums {
            out <- n
        }
        close(out)
    }()
    return out
}

func square(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        for n := range in {
            out <- n * n
        }
        close(out)
    }()
    return out
}

func filter(in <-chan int, predicate func(int) bool) <-chan int {
    out := make(chan int)
    go func() {
        for n := range in {
            if predicate(n) {
                out <- n
            }
        }
        close(out)
    }()
    return out
}

// Using the pipeline
func simplePipeline() {
    // Set up pipeline
    numbers := generator(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    squares := square(numbers)
    evens := filter(squares, func(n int) bool { return n%2 == 0 })
    
    // Consume results
    for n := range evens {
        fmt.Println(n)  // 4, 16, 36, 64, 100
    }
}

// Pipeline with error handling
type Data struct {
    Value interface{}
    Err   error
}

func readFiles(files []string) <-chan Data {
    out := make(chan Data)
    go func() {
        defer close(out)
        for _, file := range files {
            content, err := os.ReadFile(file)
            out <- Data{Value: content, Err: err}
        }
    }()
    return out
}

func processContent(in <-chan Data) <-chan Data {
    out := make(chan Data)
    go func() {
        defer close(out)
        for data := range in {
            if data.Err != nil {
                out <- data
                continue
            }
            
            content := data.Value.([]byte)
            processed := bytes.ToUpper(content)
            out <- Data{Value: processed, Err: nil}
        }
    }()
    return out
}

func saveResults(in <-chan Data) <-chan Data {
    out := make(chan Data)
    go func() {
        defer close(out)
        for data := range in {
            if data.Err != nil {
                out <- data
                continue
            }
            
            content := data.Value.([]byte)
            err := os.WriteFile("output.txt", content, 0644)
            out <- Data{Value: nil, Err: err}
        }
    }()
    return out
}

// Cancellable pipeline
func cancellablePipeline(ctx context.Context) {
    gen := func(ctx context.Context) <-chan int {
        out := make(chan int)
        go func() {
            defer close(out)
            for i := 0; ; i++ {
                select {
                case out <- i:
                case <-ctx.Done():
                    return
                }
            }
        }()
        return out
    }
    
    process := func(ctx context.Context, in <-chan int) <-chan int {
        out := make(chan int)
        go func() {
            defer close(out)
            for {
                select {
                case n, ok := <-in:
                    if !ok {
                        return
                    }
                    select {
                    case out <- n * n:
                    case <-ctx.Done():
                        return
                    }
                case <-ctx.Done():
                    return
                }
            }
        }()
        return out
    }
    
    ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
    defer cancel()
    
    numbers := gen(ctx)
    squares := process(ctx, numbers)
    
    for n := range squares {
        fmt.Println(n)
        if n > 100 {
            cancel()  // Stop pipeline
        }
    }
}

// Complex data pipeline
type Record struct {
    ID   string
    Data map[string]interface{}
}

type Pipeline struct {
    stages []Stage
}

type Stage interface {
    Process(context.Context, <-chan Record) <-chan Record
}

func (p *Pipeline) Run(ctx context.Context, input <-chan Record) <-chan Record {
    output := input
    
    for _, stage := range p.stages {
        output = stage.Process(ctx, output)
    }
    
    return output
}

// Transform stage
type TransformStage struct {
    transform func(Record) Record
}

func (s *TransformStage) Process(ctx context.Context, in <-chan Record) <-chan Record {
    out := make(chan Record)
    
    go func() {
        defer close(out)
        for {
            select {
            case record, ok := <-in:
                if !ok {
                    return
                }
                
                transformed := s.transform(record)
                
                select {
                case out <- transformed:
                case <-ctx.Done():
                    return
                }
                
            case <-ctx.Done():
                return
            }
        }
    }()
    
    return out
}

// Filter stage
type FilterStage struct {
    predicate func(Record) bool
}

func (s *FilterStage) Process(ctx context.Context, in <-chan Record) <-chan Record {
    out := make(chan Record)
    
    go func() {
        defer close(out)
        for {
            select {
            case record, ok := <-in:
                if !ok {
                    return
                }
                
                if s.predicate(record) {
                    select {
                    case out <- record:
                    case <-ctx.Done():
                        return
                    }
                }
                
            case <-ctx.Done():
                return
            }
        }
    }()
    
    return out
}

// Batch stage
type BatchStage struct {
    size int
}

func (s *BatchStage) Process(ctx context.Context, in <-chan Record) <-chan []Record {
    out := make(chan []Record)
    
    go func() {
        defer close(out)
        
        batch := make([]Record, 0, s.size)
        
        for {
            select {
            case record, ok := <-in:
                if !ok {
                    if len(batch) > 0 {
                        out <- batch
                    }
                    return
                }
                
                batch = append(batch, record)
                
                if len(batch) == s.size {
                    select {
                    case out <- batch:
                        batch = make([]Record, 0, s.size)
                    case <-ctx.Done():
                        return
                    }
                }
                
            case <-ctx.Done():
                return
            }
        }
    }()
    
    return out
}
```

**Pipeline Characteristics:**

- **Composability:** Stages can be mixed and matched
- **Separation of concerns:** Each stage has single responsibility
- **Concurrent execution:** Stages run in parallel
- **Back-pressure:** Natural flow control through channels
- **Easy testing:** Stages can be tested independently

### Fan-in/Fan-out

Fan-out distributes work to multiple goroutines, while fan-in merges results from multiple goroutines.

```go
// Fan-out: distribute work to multiple workers
func fanOut(in <-chan int, workers int) []<-chan int {
    outs := make([]<-chan int, workers)
    
    for i := 0; i < workers; i++ {
        out := make(chan int)
        outs[i] = out
        
        go func() {
            defer close(out)
            for n := range in {
                out <- process(n)  // Heavy processing
            }
        }()
    }
    
    return outs
}

// Fan-in: merge multiple channels into one
func fanIn(channels ...<-chan int) <-chan int {
    out := make(chan int)
    var wg sync.WaitGroup
    
    for _, ch := range channels {
        wg.Add(1)
        go func(c <-chan int) {
            defer wg.Done()
            for n := range c {
                out <- n
            }
        }(ch)
    }
    
    go func() {
        wg.Wait()
        close(out)
    }()
    
    return out
}

// Complete fan-out/fan-in example
func fanOutFanIn() {
    // Generate work
    work := make(chan int, 100)
    go func() {
        for i := 0; i < 100; i++ {
            work <- i
        }
        close(work)
    }()
    
    // Fan-out to workers
    workers := fanOut(work, 5)
    
    // Fan-in results
    results := fanIn(workers...)
    
    // Consume results
    for result := range results {
        fmt.Println(result)
    }
}

// Advanced fan-out with work distribution
type WorkDistributor struct {
    workers   int
    workFn    func(interface{}) (interface{}, error)
    input     chan interface{}
    output    chan Result
}

func NewWorkDistributor(workers int, workFn func(interface{}) (interface{}, error)) *WorkDistributor {
    return &WorkDistributor{
        workers: workers,
        workFn:  workFn,
        input:   make(chan interface{}, workers*2),
        output:  make(chan Result, workers*2),
    }
}

func (d *WorkDistributor) Start(ctx context.Context) {
    var wg sync.WaitGroup
    
    // Fan-out
    for i := 0; i < d.workers; i++ {
        wg.Add(1)
        go func(workerID int) {
            defer wg.Done()
            
            for {
                select {
                case work, ok := <-d.input:
                    if !ok {
                        return
                    }
                    
                    result, err := d.workFn(work)
                    
                    select {
                    case d.output <- Result{Value: result, Err: err}:
                    case <-ctx.Done():
                        return
                    }
                    
                case <-ctx.Done():
                    return
                }
            }
        }(i)
    }
    
    // Close output when all workers done
    go func() {
        wg.Wait()
        close(d.output)
    }()
}

// Ordered fan-in (maintains order)
type OrderedResult struct {
    Index int
    Value interface{}
    Err   error
}

func orderedFanIn(results []<-chan OrderedResult) <-chan OrderedResult {
    out := make(chan OrderedResult)
    
    go func() {
        defer close(out)
        
        // Track next expected index
        nextIndex := 0
        pending := make(map[int]OrderedResult)
        
        // Merge all channels
        merged := mergeOrdered(results...)
        
        for result := range merged {
            pending[result.Index] = result
            
            // Send all consecutive results
            for {
                if next, ok := pending[nextIndex]; ok {
                    out <- next
                    delete(pending, nextIndex)
                    nextIndex++
                } else {
                    break
                }
            }
        }
    }()
    
    return out
}

func mergeOrdered(channels ...<-chan OrderedResult) <-chan OrderedResult {
    out := make(chan OrderedResult)
    var wg sync.WaitGroup
    
    for _, ch := range channels {
        wg.Add(1)
        go func(c <-chan OrderedResult) {
            defer wg.Done()
            for result := range c {
                out <- result
            }
        }(ch)
    }
    
    go func() {
        wg.Wait()
        close(out)
    }()
    
    return out
}

// Bounded fan-out
type BoundedFanOut struct {
    maxWorkers int
    sem        chan struct{}
}

func NewBoundedFanOut(maxWorkers int) *BoundedFanOut {
    return &BoundedFanOut{
        maxWorkers: maxWorkers,
        sem:        make(chan struct{}, maxWorkers),
    }
}

func (f *BoundedFanOut) Process(items []interface{}, fn func(interface{}) error) error {
    var wg sync.WaitGroup
    errors := make(chan error, len(items))
    
    for _, item := range items {
        wg.Add(1)
        f.sem <- struct{}{}  // Acquire semaphore
        
        go func(i interface{}) {
            defer wg.Done()
            defer func() { <-f.sem }()  // Release semaphore
            
            if err := fn(i); err != nil {
                errors <- err
            }
        }(item)
    }
    
    wg.Wait()
    close(errors)
    
    // Collect errors
    for err := range errors {
        if err != nil {
            return err
        }
    }
    
    return nil
}
```

**Fan-out/Fan-in Use Cases:**

- **CPU-bound work:** Distribute to multiple cores
- **I/O parallelization:** Multiple concurrent requests
- **Batch processing:** Process chunks in parallel
- **Map-reduce:** Distribute map, merge reduce

### Rate Limiting

Rate limiting controls the frequency of operations to prevent overwhelming resources or violating API limits.

```go
// Token bucket rate limiter
type TokenBucket struct {
    tokens    chan struct{}
    rate      time.Duration
    capacity  int
    stop      chan struct{}
}

func NewTokenBucket(rate time.Duration, capacity int) *TokenBucket {
    tb := &TokenBucket{
        tokens:   make(chan struct{}, capacity),
        rate:     rate,
        capacity: capacity,
        stop:     make(chan struct{}),
    }
    
    // Fill initial tokens
    for i := 0; i < capacity; i++ {
        tb.tokens <- struct{}{}
    }
    
    // Refill tokens
    go tb.refill()
    
    return tb
}

func (tb *TokenBucket) refill() {
    ticker := time.NewTicker(tb.rate)
    defer ticker.Stop()
    
    for {
        select {
        case <-ticker.C:
            select {
            case tb.tokens <- struct{}{}:
                // Token added
            default:
                // Bucket full
            }
        case <-tb.stop:
            return
        }
    }
}

func (tb *TokenBucket) Allow() bool {
    select {
    case <-tb.tokens:
        return true
    default:
        return false
    }
}

func (tb *TokenBucket) Wait(ctx context.Context) error {
    select {
    case <-tb.tokens:
        return nil
    case <-ctx.Done():
        return ctx.Err()
    }
}

// Sliding window rate limiter
type SlidingWindow struct {
    mu        sync.Mutex
    window    time.Duration
    limit     int
    requests  []time.Time
}

func NewSlidingWindow(window time.Duration, limit int) *SlidingWindow {
    return &SlidingWindow{
        window:   window,
        limit:    limit,
        requests: make([]time.Time, 0, limit),
    }
}

func (sw *SlidingWindow) Allow() bool {
    sw.mu.Lock()
    defer sw.mu.Unlock()
    
    now := time.Now()
    windowStart := now.Add(-sw.window)
    
    // Remove old requests
    validRequests := sw.requests[:0]
    for _, t := range sw.requests {
        if t.After(windowStart) {
            validRequests = append(validRequests, t)
        }
    }
    sw.requests = validRequests
    
    // Check limit
    if len(sw.requests) >= sw.limit {
        return false
    }
    
    // Add new request
    sw.requests = append(sw.requests, now)
    return true
}

// Rate limiter with golang.org/x/time/rate
import "golang.org/x/time/rate"

type APIClient struct {
    limiter *rate.Limiter
    client  *http.Client
}

func NewAPIClient(rps int, burst int) *APIClient {
    return &APIClient{
        limiter: rate.NewLimiter(rate.Limit(rps), burst),
        client:  &http.Client{Timeout: 10 * time.Second},
    }
}

func (c *APIClient) Get(ctx context.Context, url string) (*http.Response, error) {
    // Wait for permission
    if err := c.limiter.Wait(ctx); err != nil {
        return nil, err
    }
    
    req, err := http.NewRequestWithContext(ctx, "GET", url, nil)
    if err != nil {
        return nil, err
    }
    
    return c.client.Do(req)
}

// Multi-tier rate limiting
type MultiTierLimiter struct {
    global    *rate.Limiter
    perUser   map[string]*rate.Limiter
    perIP     map[string]*rate.Limiter
    mu        sync.RWMutex
}

func NewMultiTierLimiter() *MultiTierLimiter {
    return &MultiTierLimiter{
        global:  rate.NewLimiter(1000, 100),  // 1000 req/s global
        perUser: make(map[string]*rate.Limiter),
        perIP:   make(map[string]*rate.Limiter),
    }
}

func (m *MultiTierLimiter) getUserLimiter(userID string) *rate.Limiter {
    m.mu.RLock()
    limiter, exists := m.perUser[userID]
    m.mu.RUnlock()
    
    if exists {
        return limiter
    }
    
    m.mu.Lock()
    defer m.mu.Unlock()
    
    // Double check
    if limiter, exists = m.perUser[userID]; exists {
        return limiter
    }
    
    // Create new limiter for user
    limiter = rate.NewLimiter(10, 5)  // 10 req/s per user
    m.perUser[userID] = limiter
    return limiter
}

func (m *MultiTierLimiter) Allow(userID, ip string) bool {
    // Check all tiers
    if !m.global.Allow() {
        return false
    }
    
    userLimiter := m.getUserLimiter(userID)
    if !userLimiter.Allow() {
        return false
    }
    
    // Similar for IP...
    return true
}

// Adaptive rate limiting
type AdaptiveLimiter struct {
    mu           sync.RWMutex
    current      *rate.Limiter
    minRate      rate.Limit
    maxRate      rate.Limit
    errorRate    float64
    adjustPeriod time.Duration
}

func (a *AdaptiveLimiter) adjust() {
    ticker := time.NewTicker(a.adjustPeriod)
    defer ticker.Stop()
    
    for range ticker.C {
        a.mu.Lock()
        
        if a.errorRate > 0.1 {  // >10% errors
            // Decrease rate
            newRate := a.current.Limit() * 0.9
            if newRate < a.minRate {
                newRate = a.minRate
            }
            a.current.SetLimit(newRate)
        } else if a.errorRate < 0.01 {  // <1% errors
            // Increase rate
            newRate := a.current.Limit() * 1.1
            if newRate > a.maxRate {
                newRate = a.maxRate
            }
            a.current.SetLimit(newRate)
        }
        
        a.mu.Unlock()
    }
}
```

**Rate Limiting Strategies:**

- **Token Bucket:** Allows bursts, refills at constant rate
- **Sliding Window:** Smooth rate over time window
- **Fixed Window:** Simple but can have edge cases
- **Leaky Bucket:** Constant output rate
- **Adaptive:** Adjusts based on system load

### Circuit Breaker

Circuit breaker prevents cascading failures by stopping requests to failing services.

```go
// Circuit breaker states
type State int

const (
    StateClosed State = iota  // Normal operation
    StateOpen                 // Failure threshold reached
    StateHalfOpen            // Testing if service recovered
)

// Basic circuit breaker
type CircuitBreaker struct {
    mu              sync.RWMutex
    state           State
    failures        int
    successes       int
    maxFailures     int
    maxSuccesses    int
    timeout         time.Duration
    lastFailureTime time.Time
}

func NewCircuitBreaker(maxFailures int, timeout time.Duration) *CircuitBreaker {
    return &CircuitBreaker{
        state:        StateClosed,
        maxFailures:  maxFailures,
        maxSuccesses: maxFailures / 2,
        timeout:      timeout,
    }
}

func (cb *CircuitBreaker) Call(fn func() error) error {
    cb.mu.Lock()
    defer cb.mu.Unlock()
    
    // Check state
    switch cb.state {
    case StateOpen:
        // Check if timeout has passed
        if time.Since(cb.lastFailureTime) > cb.timeout {
            cb.state = StateHalfOpen
            cb.successes = 0
        } else {
            return fmt.Errorf("circuit breaker is open")
        }
        
    case StateHalfOpen:
        // Allow limited requests to test
    
    case StateClosed:
        // Normal operation
    }
    
    // Execute function
    err := fn()
    
    // Update state based on result
    if err != nil {
        cb.onFailure()
    } else {
        cb.onSuccess()
    }
    
    return err
}

func (cb *CircuitBreaker) onFailure() {
    cb.failures++
    cb.lastFailureTime = time.Now()
    
    switch cb.state {
    case StateClosed:
        if cb.failures >= cb.maxFailures {
            cb.state = StateOpen
            cb.failures = 0
        }
        
    case StateHalfOpen:
        cb.state = StateOpen
        cb.failures = 0
    }
}

func (cb *CircuitBreaker) onSuccess() {
    cb.failures = 0
    
    switch cb.state {
    case StateHalfOpen:
        cb.successes++
        if cb.successes >= cb.maxSuccesses {
            cb.state = StateClosed
            cb.successes = 0
        }
    }
}

// Advanced circuit breaker with metrics
type AdvancedCircuitBreaker struct {
    mu            sync.RWMutex
    state         State
    
    // Configuration
    failureThreshold   float64
    successThreshold   int
    timeout           time.Duration
    
    // Metrics
    requests          *RingBuffer
    consecutiveFails  int
    consecutiveSuccess int
    
    // Callbacks
    onStateChange func(from, to State)
}

type RingBuffer struct {
    data  []bool  // true = success, false = failure
    index int
    size  int
}

func (rb *RingBuffer) Add(success bool) {
    rb.data[rb.index] = success
    rb.index = (rb.index + 1) % rb.size
}

func (rb *RingBuffer) FailureRate() float64 {
    failures := 0
    for _, success := range rb.data {
        if !success {
            failures++
        }
    }
    return float64(failures) / float64(rb.size)
}

func (cb *AdvancedCircuitBreaker) Execute(ctx context.Context, fn func() error) error {
    if !cb.canExecute() {
        return fmt.Errorf("circuit breaker is open")
    }
    
    // Execute with timeout
    done := make(chan error, 1)
    go func() {
        done <- fn()
    }()
    
    select {
    case err := <-done:
        cb.recordResult(err == nil)
        return err
    case <-ctx.Done():
        cb.recordResult(false)
        return ctx.Err()
    }
}

func (cb *AdvancedCircuitBreaker) canExecute() bool {
    cb.mu.RLock()
    defer cb.mu.RUnlock()
    
    switch cb.state {
    case StateClosed:
        return true
    case StateOpen:
        return time.Since(cb.lastStateChange()) > cb.timeout
    case StateHalfOpen:
        return true
    }
    
    return false
}

func (cb *AdvancedCircuitBreaker) recordResult(success bool) {
    cb.mu.Lock()
    defer cb.mu.Unlock()
    
    cb.requests.Add(success)
    
    if success {
        cb.consecutiveSuccess++
        cb.consecutiveFails = 0
        
        if cb.state == StateHalfOpen && cb.consecutiveSuccess >= cb.successThreshold {
            cb.changeState(StateClosed)
        }
    } else {
        cb.consecutiveFails++
        cb.consecutiveSuccess = 0
        
        if cb.state == StateHalfOpen {
            cb.changeState(StateOpen)
        } else if cb.state == StateClosed {
            if cb.requests.FailureRate() > cb.failureThreshold {
                cb.changeState(StateOpen)
            }
        }
    }
}

// HTTP client with circuit breaker
type ResilientHTTPClient struct {
    client   *http.Client
    breakers map[string]*CircuitBreaker
    mu       sync.RWMutex
}

func (c *ResilientHTTPClient) Get(url string) (*http.Response, error) {
    breaker := c.getBreakerForURL(url)
    
    var resp *http.Response
    err := breaker.Call(func() error {
        var err error
        resp, err = c.client.Get(url)
        if err != nil {
            return err
        }
        
        // Consider 5xx errors as failures
        if resp.StatusCode >= 500 {
            resp.Body.Close()
            return fmt.Errorf("server error: %d", resp.StatusCode)
        }
        
        return nil
    })
    
    return resp, err
}

func (c *ResilientHTTPClient) getBreakerForURL(url string) *CircuitBreaker {
    host := getHost(url)
    
    c.mu.RLock()
    breaker, exists := c.breakers[host]
    c.mu.RUnlock()
    
    if exists {
        return breaker
    }
    
    c.mu.Lock()
    defer c.mu.Unlock()
    
    // Double check
    if breaker, exists = c.breakers[host]; exists {
        return breaker
    }
    
    breaker = NewCircuitBreaker(5, 30*time.Second)
    c.breakers[host] = breaker
    return breaker
}
```

## 8.8 Concurrency Pitfalls

Understanding common concurrency pitfalls is crucial for writing correct concurrent programs. These issues can be subtle and may only manifest under specific conditions.

### Race Conditions

Race conditions occur when multiple goroutines access shared memory concurrently and at least one access is a write.

```go
// Classic race condition
func raceExample() {
    var counter int
    var wg sync.WaitGroup
    
    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            counter++  // RACE: Read-Modify-Write
        }()
    }
    
    wg.Wait()
    fmt.Println(counter)  // Result varies!
}

// Map race condition
func mapRace() {
    m := make(map[string]int)
    var wg sync.WaitGroup
    
    // Writer
    wg.Add(1)
    go func() {
        defer wg.Done()
        for i := 0; i < 1000; i++ {
            m[fmt.Sprintf("key%d", i)] = i  // RACE: Concurrent map write
        }
    }()
    
    // Reader
    wg.Add(1)
    go func() {
        defer wg.Done()
        for i := 0; i < 1000; i++ {
            _ = m[fmt.Sprintf("key%d", i)]  // RACE: Concurrent map read
        }
    }()
    
    wg.Wait()  // Likely to panic!
}

// Slice race condition
func sliceRace() {
    slice := make([]int, 0)
    var wg sync.WaitGroup
    
    for i := 0; i < 100; i++ {
        wg.Add(1)
        go func(n int) {
            defer wg.Done()
            slice = append(slice, n)  // RACE: Append is not thread-safe
        }(i)
    }
    
    wg.Wait()
    fmt.Println(len(slice))  // May be less than 100!
}

// Struct field race
type Counter struct {
    value int
}

func (c *Counter) Increment() {
    c.value++  // RACE if called concurrently
}

func (c *Counter) Get() int {
    return c.value  // RACE with Increment
}

// Interface race
type DataStore interface {
    Get(key string) string
    Set(key string, value string)
}

type MapStore struct {
    data map[string]string
}

func (m *MapStore) Get(key string) string {
    return m.data[key]  // RACE without synchronization
}

func (m *MapStore) Set(key string, value string) {
    m.data[key] = value  // RACE
}

// Closure variable race
func closureRace() {
    var wg sync.WaitGroup
    
    for i := 0; i < 10; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            fmt.Println(i)  // RACE: All goroutines share same i
        }()
    }
    
    wg.Wait()
}

// Fixed closure
func closureFixed() {
    var wg sync.WaitGroup
    
    for i := 0; i < 10; i++ {
        wg.Add(1)
        go func(n int) {  // Pass as parameter
            defer wg.Done()
            fmt.Println(n)
        }(i)
    }
    
    wg.Wait()
}

// Channel race - closing
func channelRace() {
    ch := make(chan int)
    
    // Multiple goroutines trying to close
    go func() {
        time.Sleep(time.Millisecond)
        close(ch)  // RACE: Multiple closes panic
    }()
    
    go func() {
        time.Sleep(time.Millisecond)
        close(ch)  // RACE
    }()
}

// Detecting races with testing
func TestRaceCondition(t *testing.T) {
    // Run with: go test -race
    
    var counter int
    var wg sync.WaitGroup
    
    for i := 0; i < 100; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            counter++  // Race detector will catch this
        }()
    }
    
    wg.Wait()
    
    if counter != 100 {
        t.Errorf("Expected 100, got %d", counter)
    }
}

// Race-free alternatives
type SafeCounter struct {
    mu    sync.Mutex
    value int
}

func (c *SafeCounter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}

func (c *SafeCounter) Get() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.value
}

// Or using atomic
type AtomicCounter struct {
    value int64
}

func (c *AtomicCounter) Increment() {
    atomic.AddInt64(&c.value, 1)
}

func (c *AtomicCounter) Get() int64 {
    return atomic.LoadInt64(&c.value)
}

// Or using channels
type ChannelCounter struct {
    ch chan int
    value int
}

func NewChannelCounter() *ChannelCounter {
    c := &ChannelCounter{
        ch: make(chan int),
    }
    go c.run()
    return c
}

func (c *ChannelCounter) run() {
    for delta := range c.ch {
        c.value += delta
    }
}

func (c *ChannelCounter) Increment() {
    c.ch <- 1
}
```

**Using the Race Detector:**

The `-race` flag enables Go's race detector, which instruments memory accesses to detect races at runtime.

```bash
# Run with race detector
go run -race main.go

# Test with race detector
go test -race ./...

# Build with race detector
go build -race

# Benchmark with race detector
go test -race -bench=.
```

**Race Detector Output Example:**

```
==================
WARNING: DATA RACE
Write at 0x00c0000b4010 by goroutine 7:
  main.raceExample.func1()
      /path/to/file.go:10 +0x3a

Previous write at 0x00c0000b4010 by goroutine 6:
  main.raceExample.func1()
      /path/to/file.go:10 +0x3a

Goroutine 7 (running) created at:
  main.raceExample()
      /path/to/file.go:8 +0x7c

Goroutine 6 (finished) created at:
  main.raceExample()
      /path/to/file.go:8 +0x7c
==================
```

**Race Detector Characteristics:**

- **Runtime overhead:** 5-10x CPU, 5-10x memory
- **Not for production:** Use in testing/development only
- **Probability based:** May not catch all races
- **Requires execution:** Only detects races in executed code
- **No false positives:** If it reports a race, there is one

### Deadlocks

Deadlocks occur when goroutines are waiting for each other in a circular dependency, preventing any progress.

```go
// Simple deadlock
func simpleDeadlock() {
    ch := make(chan int)
    
    ch <- 1  // Blocks forever - no receiver
    
    <-ch     // Never reached
}

// Mutual channel deadlock
func mutualDeadlock() {
    ch1 := make(chan int)
    ch2 := make(chan int)
    
    go func() {
        ch1 <- 1
        <-ch2  // Waits for ch2
    }()
    
    go func() {
        ch2 <- 2
        <-ch1  // Waits for ch1
    }()
    
    // Both goroutines deadlock if sends happen first
}

// Lock ordering deadlock
func lockOrderingDeadlock() {
    var mu1, mu2 sync.Mutex
    
    go func() {
        mu1.Lock()
        time.Sleep(time.Millisecond)
        mu2.Lock()  // Tries to lock mu2 while holding mu1
        
        mu2.Unlock()
        mu1.Unlock()
    }()
    
    go func() {
        mu2.Lock()
        time.Sleep(time.Millisecond)
        mu1.Lock()  // Tries to lock mu1 while holding mu2
        
        mu1.Unlock()
        mu2.Unlock()
    }()
}

// Channel direction deadlock
func channelDirectionDeadlock() {
    ch := make(chan int)
    
    go func() {
        <-ch  // Waiting to receive
    }()
    
    go func() {
        <-ch  // Also waiting to receive - no sender!
    }()
    
    time.Sleep(time.Second)
    // Program hangs
}

// WaitGroup deadlock
func waitGroupDeadlock() {
    var wg sync.WaitGroup
    
    wg.Add(1)
    
    go func() {
        wg.Wait()  // Waiting for itself!
        wg.Done()  // Never reached
    }()
    
    wg.Wait()  // Main also waits - deadlock
}

// Select deadlock
func selectDeadlock() {
    ch1 := make(chan int)
    ch2 := make(chan int)
    
    select {
    case <-ch1:
        // Never happens
    case <-ch2:
        // Never happens
    // No default case - blocks forever
    }
}

// Preventing deadlocks

// 1. Lock ordering
type SafeTransfer struct {
    accounts []*Account
}

type Account struct {
    ID      int
    balance int
    mu      sync.Mutex
}

func (st *SafeTransfer) Transfer(from, to *Account, amount int) {
    // Always lock in order of ID to prevent deadlock
    if from.ID < to.ID {
        from.mu.Lock()
        defer from.mu.Unlock()
        to.mu.Lock()
        defer to.mu.Unlock()
    } else {
        to.mu.Lock()
        defer to.mu.Unlock()
        from.mu.Lock()
        defer from.mu.Unlock()
    }
    
    if from.balance >= amount {
        from.balance -= amount
        to.balance += amount
    }
}

// 2. Timeout on operations
func timeoutPrevention() {
    ch := make(chan int)
    
    select {
    case val := <-ch:
        fmt.Println("Got value:", val)
    case <-time.After(1 * time.Second):
        fmt.Println("Timeout - preventing deadlock")
    }
}

// 3. Buffered channels
func bufferedPrevention() {
    ch := make(chan int, 1)  // Buffer prevents deadlock
    
    ch <- 1  // Doesn't block
    val := <-ch
    fmt.Println(val)
}

// 4. Proper goroutine lifecycle
func properLifecycle() {
    done := make(chan struct{})
    data := make(chan int)
    
    // Worker
    go func() {
        defer close(done)
        for val := range data {
            process(val)
        }
    }()
    
    // Send data
    for i := 0; i < 10; i++ {
        data <- i
    }
    close(data)  // Signal completion
    
    <-done  // Wait for worker
}

// Detecting deadlocks
func detectDeadlock() {
    // Go runtime detects some deadlocks
    // "fatal error: all goroutines are asleep - deadlock!"
    
    ch := make(chan int)
    <-ch  // Runtime detects this deadlock
}

// Complex deadlock detection
type DeadlockDetector struct {
    mu       sync.Mutex
    waiting  map[string][]string  // What each goroutine waits for
    holding  map[string][]string  // What each goroutine holds
}

func (dd *DeadlockDetector) WaitFor(goroutineID, resource string) {
    dd.mu.Lock()
    defer dd.mu.Unlock()
    
    dd.waiting[goroutineID] = append(dd.waiting[goroutineID], resource)
    
    // Check for cycles
    if dd.hasCycle(goroutineID) {
        panic("Potential deadlock detected!")
    }
}

func (dd *DeadlockDetector) Acquired(goroutineID, resource string) {
    dd.mu.Lock()
    defer dd.mu.Unlock()
    
    dd.holding[goroutineID] = append(dd.holding[goroutineID], resource)
    
    // Remove from waiting
    waiting := dd.waiting[goroutineID]
    for i, r := range waiting {
        if r == resource {
            dd.waiting[goroutineID] = append(waiting[:i], waiting[i+1:]...)
            break
        }
    }
}

func (dd *DeadlockDetector) hasCycle(start string) bool {
    // Implement cycle detection algorithm
    visited := make(map[string]bool)
    stack := []string{start}
    
    for len(stack) > 0 {
        current := stack[len(stack)-1]
        stack = stack[:len(stack)-1]
        
        if visited[current] {
            return true  // Cycle detected
        }
        visited[current] = true
        
        // Add dependencies to stack
        for _, resource := range dd.waiting[current] {
            for holder, holdings := range dd.holding {
                for _, held := range holdings {
                    if held == resource {
                        stack = append(stack, holder)
                    }
                }
            }
        }
    }
    
    return false
}
```

**Deadlock Prevention Strategies:**

1. **Lock ordering:** Always acquire locks in the same order
2. **Lock timeout:** Use try-lock or timeout mechanisms
3. **Avoid nested locks:** Minimize lock scope
4. **Banker's algorithm:** Pre-declare resource needs
5. **Lock-free algorithms:** Use atomic operations

### Channel vs Mutex Decision

Choosing between channels and mutexes is a fundamental design decision in Go concurrent programming.

```go
// When to use CHANNELS

// 1. Passing ownership
func passingOwnership() {
    type Result struct {
        data []byte
    }
    
    // Channel transfers ownership
    results := make(chan Result)
    
    go func() {
        data := computeData()
        results <- Result{data: data}  // Ownership transferred
        // Don't touch data after sending
    }()
    
    result := <-results
    // Now we own result.data
}

// 2. Distributing work
func distributeWork() {
    jobs := make(chan Job, 100)
    results := make(chan Result, 100)
    
    // Workers
    for w := 0; w < 5; w++ {
        go worker(jobs, results)
    }
    
    // Send work
    for _, job := range getAllJobs() {
        jobs <- job
    }
    close(jobs)
}

// 3. Coordinating state machines
func stateMachine() {
    type Event struct {
        Type string
        Data interface{}
    }
    
    events := make(chan Event)
    
    go func() {
        state := "idle"
        for event := range events {
            switch state {
            case "idle":
                if event.Type == "start" {
                    state = "running"
                }
            case "running":
                if event.Type == "stop" {
                    state = "idle"
                }
            }
        }
    }()
}

// 4. Composing concurrent operations
func composition() {
    input := generator()
    filtered := filter(input)
    transformed := transform(filtered)
    
    for result := range transformed {
        fmt.Println(result)
    }
}

// When to use MUTEXES

// 1. Protecting internal state
type Cache struct {
    mu    sync.RWMutex
    items map[string]Item
}

func (c *Cache) Get(key string) (Item, bool) {
    c.mu.RLock()
    defer c.mu.RUnlock()
    
    item, ok := c.items[key]
    return item, ok
}

// 2. Simple counters/flags
type Service struct {
    mu      sync.Mutex
    running bool
    counter int64
}

func (s *Service) Start() error {
    s.mu.Lock()
    defer s.mu.Unlock()
    
    if s.running {
        return errors.New("already running")
    }
    s.running = true
    return nil
}

// 3. Coordinating access to resources
type ResourcePool struct {
    mu        sync.Mutex
    resources []Resource
    inUse     map[int]bool
}

func (p *ResourcePool) Acquire() (Resource, error) {
    p.mu.Lock()
    defer p.mu.Unlock()
    
    for i, r := range p.resources {
        if !p.inUse[i] {
            p.inUse[i] = true
            return r, nil
        }
    }
    return nil, errors.New("no resources available")
}

// COMPARISON: Same problem, different approaches

// Counter with channels
type ChannelCounter struct {
    ch    chan int
    value int
}

func NewChannelCounter() *ChannelCounter {
    c := &ChannelCounter{
        ch: make(chan int),
    }
    go c.run()
    return c
}

func (c *ChannelCounter) run() {
    for delta := range c.ch {
        c.value += delta
    }
}

func (c *ChannelCounter) Increment() {
    c.ch <- 1
}

func (c *ChannelCounter) Get() int {
    result := make(chan int)
    c.ch <- 0  // Special signal
    return <-result
}

// Counter with mutex (simpler!)
type MutexCounter struct {
    mu    sync.Mutex
    value int
}

func (c *MutexCounter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}

func (c *MutexCounter) Get() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.value
}

// Decision matrix function
func decideChannelVsMutex(scenario string) string {
    decisions := map[string]string{
        "transfer_ownership":     "channel",
        "share_memory":          "mutex",
        "coordinate_goroutines": "channel",
        "protect_state":         "mutex",
        "send_signals":          "channel",
        "cache_access":          "mutex",
        "work_distribution":     "channel",
        "simple_counter":        "atomic/mutex",
        "pipeline":              "channel",
        "shared_map":            "mutex",
    }
    
    return decisions[scenario]
}

// Hybrid approach - using both
type HybridQueue struct {
    mu    sync.Mutex
    items []Item
    ready chan struct{}  // Signal when items available
}

func (q *HybridQueue) Push(item Item) {
    q.mu.Lock()
    q.items = append(q.items, item)
    q.mu.Unlock()
    
    // Non-blocking signal
    select {
    case q.ready <- struct{}{}:
    default:
    }
}

func (q *HybridQueue) Pop() (Item, bool) {
    q.mu.Lock()
    defer q.mu.Unlock()
    
    if len(q.items) == 0 {
        return Item{}, false
    }
    
    item := q.items[0]
    q.items = q.items[1:]
    return item, true
}

func (q *HybridQueue) WaitForItem() Item {
    for {
        if item, ok := q.Pop(); ok {
            return item
        }
        
        <-q.ready  // Wait for signal
    }
}

// Performance comparison
func benchmark() {
    const ops = 1000000
    
    // Channel-based
    start := time.Now()
    ch := make(chan int, 1)
    for i := 0; i < ops; i++ {
        ch <- i
        <-ch
    }
    channelTime := time.Since(start)
    
    // Mutex-based
    start = time.Now()
    var mu sync.Mutex
    var val int
    for i := 0; i < ops; i++ {
        mu.Lock()
        val = i
        mu.Unlock()
    }
    mutexTime := time.Since(start)
    
    // Atomic-based
    start = time.Now()
    var atomicVal int64
    for i := 0; i < ops; i++ {
        atomic.StoreInt64(&atomicVal, int64(i))
    }
    atomicTime := time.Since(start)
    
    fmt.Printf("Channel: %v\n", channelTime)
    fmt.Printf("Mutex: %v\n", mutexTime)
    fmt.Printf("Atomic: %v\n", atomicTime)
}
```

**Channel vs Mutex Decision Guide:**

**Use Channels When:**

- **Transferring ownership:** Data moves between goroutines
- **Distributing work:** Job queues, worker pools
- **Coordinating goroutines:** Synchronization, ordering
- **Composing pipelines:** Data transformation stages
- **Signaling events:** Notifications, cancellations
- **IO operations:** Network, disk operations

**Use Mutexes When:**

- **Protecting shared state:** Caches, registries
- **Simple counters:** Increment/decrement operations
- **Short critical sections:** Quick in-and-out
- **Performance critical:** Lower overhead than channels
- **Complex data structures:** Maps, trees, graphs
- **Read-heavy workloads:** RWMutex for optimization

**Use Atomic When:**

- **Single values:** Counters, flags
- **Lock-free required:** Avoid blocking
- **High contention:** Many goroutines accessing
- **Simple operations:** Load, store, add, CAS

**Decision Factors:**

|Factor|Channels|Mutexes|Atomic|
|---|---|---|---|
|**Complexity**|Higher|Medium|Lower|
|**Performance**|Slower|Medium|Fastest|
|**Ownership**|Transfer|Shared|Shared|
|**Blocking**|Yes|Yes|No|
|**Composability**|High|Low|None|
|**Debugging**|Easier|Harder|Hardest|

**Common Anti-patterns:**

```go
// ANTI-PATTERN: Channel for shared state
type BadCache struct {
    get chan getRequest
    set chan setRequest
}

type getRequest struct {
    key  string
    resp chan string
}

// Too complex for simple cache!

// ANTI-PATTERN: Mutex for message passing
type BadQueue struct {
    mu    sync.Mutex
    items []Item
}

func (q *BadQueue) BlockingGet() Item {
    for {
        q.mu.Lock()
        if len(q.items) > 0 {
            item := q.items[0]
            q.items = q.items[1:]
            q.mu.Unlock()
            return item
        }
        q.mu.Unlock()
        
        time.Sleep(10 * time.Millisecond)  // Busy waiting!
    }
}

// ANTI-PATTERN: Mixing paradigms incorrectly
func confused(ch chan int, mu *sync.Mutex, val *int) {
    mu.Lock()
    *val = <-ch  // Holding mutex while blocking on channel!
    mu.Unlock()
}
```

**Best Practices Summary:**

1. **Start simple:** Use the simplest solution that works
2. **"Share memory by communicating":** Prefer channels for coordination
3. **"Don't communicate by sharing memory":** Unless it's simpler
4. **Profile before optimizing:** Measure, don't guess
5. **Be consistent:** Don't mix patterns unnecessarily
6. **Document your choice:** Explain why you chose channels vs mutexes

**Testing Concurrent Code:**

```go
// Test for race conditions
go test -race ./...

// Test for deadlocks
go test -timeout 10s ./...

// Stress testing
func TestConcurrentAccess(t *testing.T) {
    const goroutines = 100
    const operations = 1000
    
    cache := NewCache()
    var wg sync.WaitGroup
    
    for i := 0; i < goroutines; i++ {
        wg.Add(1)
        go func(id int) {
            defer wg.Done()
            for j := 0; j < operations; j++ {
                key := fmt.Sprintf("key-%d-%d", id, j)
                cache.Set(key, j)
                cache.Get(key)
            }
        }(i)
    }
    
    wg.Wait()
}

// Benchmark concurrent operations
func BenchmarkConcurrent(b *testing.B) {
    cache := NewCache()
    
    b.RunParallel(func(pb *testing.PB) {
        for pb.Next() {
            cache.Set("key", "value")
            cache.Get("key")
        }
    })
}
```

**Key Takeaways:**

- **Race conditions:** Use -race flag, protect shared memory
- **Deadlocks:** Order locks, use timeouts, avoid circular dependencies
- **Channel vs Mutex:** Choose based on ownership and communication patterns
- **Test thoroughly:** Concurrent bugs are hard to reproduce
- **Keep it simple:** Complex synchronization is error-prone

## 9. Testing

Testing is a first-class citizen in Go, with built-in support in the standard library and toolchain. Go's testing philosophy emphasizes simplicity, clarity, and table-driven tests.

## 9.1 Unit Testing

Unit testing in Go uses the `testing` package and follows conventions that make tests discoverable and runnable with the `go test` command.

**Testing Fundamentals:**

- Test files end with `_test.go`
- Test functions start with `Test` and take `*testing.T`
- Tests live in the same package (white-box) or `_test` package (black-box)
- Run with `go test` or `go test ./...` for all packages

### Basic Testing Structure

```go
// math.go
package math

import "errors"

func Add(a, b int) int {
    return a + b
}

func Divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

// math_test.go
package math

import (
    "testing"
)

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    expected := 5
    
    if result != expected {
        t.Errorf("Add(2, 3) = %d; want %d", result, expected)
    }
}

func TestDivide(t *testing.T) {
    result, err := Divide(10, 2)
    if err != nil {
        t.Fatalf("unexpected error: %v", err)
    }
    
    expected := 5.0
    if result != expected {
        t.Errorf("Divide(10, 2) = %f; want %f", result, expected)
    }
}

func TestDivideByZero(t *testing.T) {
    _, err := Divide(10, 0)
    if err == nil {
        t.Error("expected error for division by zero")
    }
}

// Test helper functions
func TestWithHelper(t *testing.T) {
    assertEqual(t, 2+2, 4)
    assertError(t, Divide(1, 0))
    assertNoError(t, Divide(10, 2))
}

func assertEqual(t *testing.T, got, want interface{}) {
    t.Helper()  // Mark as helper function
    if got != want {
        t.Errorf("got %v, want %v", got, want)
    }
}

func assertError(t *testing.T, _, err interface{}) {
    t.Helper()
    if err == nil {
        t.Error("expected error but got nil")
    }
}

func assertNoError(t *testing.T, _, err interface{}) {
    t.Helper()
    if err != nil {
        t.Errorf("unexpected error: %v", err)
    }
}
```

**Testing Methods:**

- **t.Error/Errorf:** Mark test as failed but continue
- **t.Fatal/Fatalf:** Mark test as failed and stop
- **t.Skip/Skipf:** Skip test with reason
- **t.Helper:** Mark function as test helper
- **t.Parallel:** Run test in parallel
- **t.Cleanup:** Register cleanup function

### Table-driven Tests

Table-driven tests are Go's idiomatic way to test multiple scenarios with the same logic, making tests comprehensive and maintainable.

```go
// Basic table-driven test
func TestAddTableDriven(t *testing.T) {
    tests := []struct {
        name     string
        a, b     int
        expected int
    }{
        {"positive numbers", 2, 3, 5},
        {"negative numbers", -2, -3, -5},
        {"mixed numbers", -5, 10, 5},
        {"with zero", 0, 5, 5},
        {"both zero", 0, 0, 0},
        {"large numbers", 1000000, 2000000, 3000000},
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            result := Add(tt.a, tt.b)
            if result != tt.expected {
                t.Errorf("Add(%d, %d) = %d; want %d", 
                    tt.a, tt.b, result, tt.expected)
            }
        })
    }
}

// Table-driven test with error handling
func TestDivideTableDriven(t *testing.T) {
    tests := []struct {
        name      string
        dividend  float64
        divisor   float64
        want      float64
        wantErr   bool
        errString string
    }{
        {
            name:     "normal division",
            dividend: 10,
            divisor:  2,
            want:     5,
            wantErr:  false,
        },
        {
            name:     "decimal division",
            dividend: 7,
            divisor:  2,
            want:     3.5,
            wantErr:  false,
        },
        {
            name:      "division by zero",
            dividend:  10,
            divisor:   0,
            want:      0,
            wantErr:   true,
            errString: "division by zero",
        },
        {
            name:     "negative numbers",
            dividend: -10,
            divisor:  2,
            want:     -5,
            wantErr:  false,
        },
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got, err := Divide(tt.dividend, tt.divisor)
            
            if tt.wantErr {
                if err == nil {
                    t.Errorf("Divide() error = nil, wantErr %v", tt.wantErr)
                    return
                }
                if tt.errString != "" && err.Error() != tt.errString {
                    t.Errorf("Divide() error = %v, want %v", err.Error(), tt.errString)
                }
                return
            }
            
            if err != nil {
                t.Errorf("Divide() unexpected error = %v", err)
                return
            }
            
            if got != tt.want {
                t.Errorf("Divide() = %v, want %v", got, tt.want)
            }
        })
    }
}

// Complex table-driven test
type User struct {
    ID       int
    Name     string
    Email    string
    Age      int
    IsActive bool
}

func ValidateUser(u User) error {
    if u.Name == "" {
        return errors.New("name is required")
    }
    if u.Email == "" {
        return errors.New("email is required")
    }
    if !strings.Contains(u.Email, "@") {
        return errors.New("invalid email format")
    }
    if u.Age < 0 || u.Age > 150 {
        return errors.New("invalid age")
    }
    return nil
}

func TestValidateUser(t *testing.T) {
    tests := []struct {
        name    string
        user    User
        wantErr bool
        errMsg  string
    }{
        {
            name: "valid user",
            user: User{
                Name:  "John Doe",
                Email: "john@example.com",
                Age:   30,
            },
            wantErr: false,
        },
        {
            name: "missing name",
            user: User{
                Email: "john@example.com",
                Age:   30,
            },
            wantErr: true,
            errMsg:  "name is required",
        },
        {
            name: "missing email",
            user: User{
                Name: "John Doe",
                Age:  30,
            },
            wantErr: true,
            errMsg:  "email is required",
        },
        {
            name: "invalid email format",
            user: User{
                Name:  "John Doe",
                Email: "invalid-email",
                Age:   30,
            },
            wantErr: true,
            errMsg:  "invalid email format",
        },
        {
            name: "negative age",
            user: User{
                Name:  "John Doe",
                Email: "john@example.com",
                Age:   -1,
            },
            wantErr: true,
            errMsg:  "invalid age",
        },
        {
            name: "age too high",
            user: User{
                Name:  "Methuselah",
                Email: "old@example.com",
                Age:   200,
            },
            wantErr: true,
            errMsg:  "invalid age",
        },
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            err := ValidateUser(tt.user)
            
            if tt.wantErr {
                if err == nil {
                    t.Error("expected error but got nil")
                    return
                }
                if err.Error() != tt.errMsg {
                    t.Errorf("error = %q, want %q", err.Error(), tt.errMsg)
                }
            } else {
                if err != nil {
                    t.Errorf("unexpected error: %v", err)
                }
            }
        })
    }
}

// Table-driven test with setup and cleanup
func TestWithSetupAndCleanup(t *testing.T) {
    tests := []struct {
        name  string
        input string
        setup func() string
        cleanup func()
        want  string
    }{
        {
            name:  "test with file",
            input: "test.txt",
            setup: func() string {
                // Create temp file
                f, _ := os.CreateTemp("", "test")
                f.WriteString("test content")
                f.Close()
                return f.Name()
            },
            cleanup: func() {
                // Cleanup will be called with t.Cleanup
            },
            want: "test content",
        },
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            filename := tt.setup()
            t.Cleanup(func() {
                os.Remove(filename)
            })
            
            content, err := os.ReadFile(filename)
            if err != nil {
                t.Fatal(err)
            }
            
            if string(content) != tt.want {
                t.Errorf("got %q, want %q", content, tt.want)
            }
        })
    }
}

// Table-driven benchmark
func BenchmarkAdd(b *testing.B) {
    testCases := []struct {
        name string
        a, b int
    }{
        {"small", 1, 2},
        {"medium", 100, 200},
        {"large", 1000000, 2000000},
    }
    
    for _, tc := range testCases {
        b.Run(tc.name, func(b *testing.B) {
            for i := 0; i < b.N; i++ {
                Add(tc.a, tc.b)
            }
        })
    }
}
```

**Table-driven Test Best Practices:**

- **Descriptive names:** Each test case should have a clear name
- **Complete coverage:** Include edge cases, error cases, and happy paths
- **Keep it DRY:** Share test logic, vary only the data
- **Order matters:** Put most common cases first for readability
- **Use subtests:** Enable running specific test cases

### Subtests (t.Run)

Subtests allow you to create hierarchical tests with better organization, parallel execution control, and selective running.

```go
// Basic subtest usage
func TestMath(t *testing.T) {
    t.Run("Addition", func(t *testing.T) {
        t.Run("Positive", func(t *testing.T) {
            if Add(2, 3) != 5 {
                t.Error("2+3 should be 5")
            }
        })
        
        t.Run("Negative", func(t *testing.T) {
            if Add(-2, -3) != -5 {
                t.Error("-2+-3 should be -5")
            }
        })
        
        t.Run("Zero", func(t *testing.T) {
            if Add(0, 0) != 0 {
                t.Error("0+0 should be 0")
            }
        })
    })
    
    t.Run("Division", func(t *testing.T) {
        t.Run("Normal", func(t *testing.T) {
            result, err := Divide(10, 2)
            if err != nil || result != 5 {
                t.Error("10/2 should be 5")
            }
        })
        
        t.Run("ByZero", func(t *testing.T) {
            _, err := Divide(10, 0)
            if err == nil {
                t.Error("should error on divide by zero")
            }
        })
    })
}

// Parallel subtests
func TestParallel(t *testing.T) {
    // Mark parent test as parallel
    t.Parallel()
    
    testCases := []struct {
        name  string
        value int
    }{
        {"test1", 1},
        {"test2", 2},
        {"test3", 3},
        {"test4", 4},
        {"test5", 5},
    }
    
    for _, tc := range testCases {
        tc := tc  // Capture range variable
        
        t.Run(tc.name, func(t *testing.T) {
            t.Parallel()  // Mark subtest as parallel
            
            // Simulate time-consuming test
            time.Sleep(time.Second)
            
            if tc.value < 0 {
                t.Errorf("value should not be negative: %d", tc.value)
            }
        })
    }
}

// Subtest with shared setup
func TestWithSharedSetup(t *testing.T) {
    // Shared setup for all subtests
    db := setupTestDatabase(t)
    t.Cleanup(func() {
        db.Close()
    })
    
    t.Run("Create", func(t *testing.T) {
        user := User{Name: "Alice", Email: "alice@example.com"}
        err := db.CreateUser(user)
        if err != nil {
            t.Errorf("failed to create user: %v", err)
        }
    })
    
    t.Run("Read", func(t *testing.T) {
        // This runs after Create in sequence
        user, err := db.GetUser("alice@example.com")
        if err != nil {
            t.Errorf("failed to get user: %v", err)
        }
        if user.Name != "Alice" {
            t.Errorf("got name %q, want %q", user.Name, "Alice")
        }
    })
    
    t.Run("Update", func(t *testing.T) {
        err := db.UpdateUser("alice@example.com", User{Name: "Alice Smith"})
        if err != nil {
            t.Errorf("failed to update user: %v", err)
        }
    })
    
    t.Run("Delete", func(t *testing.T) {
        err := db.DeleteUser("alice@example.com")
        if err != nil {
            t.Errorf("failed to delete user: %v", err)
        }
    })
}

// Nested subtests with setup/teardown
func TestNestedWithSetup(t *testing.T) {
    t.Run("Group1", func(t *testing.T) {
        // Setup for Group1
        resource := acquireResource()
        t.Cleanup(func() {
            resource.Release()
        })
        
        t.Run("Test1", func(t *testing.T) {
            // Can run in parallel within group
            t.Parallel()
            resource.Use()
        })
        
        t.Run("Test2", func(t *testing.T) {
            t.Parallel()
            resource.Use()
        })
    })
    
    t.Run("Group2", func(t *testing.T) {
        // Different setup for Group2
        conn := openConnection()
        t.Cleanup(func() {
            conn.Close()
        })
        
        t.Run("Test3", func(t *testing.T) {
            conn.Send("data")
        })
    })
}

// Running specific subtests
// go test -run TestMath/Addition
// go test -run TestMath/Division/ByZero
// go test -run "TestMath/.*Zero"

// Skip subtests conditionally
func TestConditional(t *testing.T) {
    tests := []struct {
        name     string
        skip     bool
        skipMsg  string
        testFunc func(t *testing.T)
    }{
        {
            name: "requires_docker",
            skip: !isDockerAvailable(),
            skipMsg: "Docker not available",
            testFunc: func(t *testing.T) {
                // Docker-dependent test
            },
        },
        {
            name: "requires_network",
            skip: !isNetworkAvailable(),
            skipMsg: "Network not available",
            testFunc: func(t *testing.T) {
                // Network-dependent test
            },
        },
        {
            name: "always_runs",
            skip: false,
            testFunc: func(t *testing.T) {
                // Always runs
            },
        },
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            if tt.skip {
                t.Skip(tt.skipMsg)
            }
            tt.testFunc(t)
        })
    }
}

// Dynamic subtest generation
func TestDynamic(t *testing.T) {
    operations := map[string]func(int, int) int{
        "add":      func(a, b int) int { return a + b },
        "subtract": func(a, b int) int { return a - b },
        "multiply": func(a, b int) int { return a * b },
    }
    
    testData := []struct {
        a, b int
        expected map[string]int
    }{
        {
            a: 10, b: 5,
            expected: map[string]int{
                "add":      15,
                "subtract": 5,
                "multiply": 50,
            },
        },
        {
            a: 3, b: 7,
            expected: map[string]int{
                "add":      10,
                "subtract": -4,
                "multiply": 21,
            },
        },
    }
    
    for _, data := range testData {
        t.Run(fmt.Sprintf("%d_%d", data.a, data.b), func(t *testing.T) {
            for opName, opFunc := range operations {
                t.Run(opName, func(t *testing.T) {
                    result := opFunc(data.a, data.b)
                    expected := data.expected[opName]
                    if result != expected {
                        t.Errorf("%s(%d, %d) = %d, want %d",
                            opName, data.a, data.b, result, expected)
                    }
                })
            }
        })
    }
}
```

**Subtest Features:**

- **Hierarchical organization:** Group related tests
- **Selective execution:** Run specific subtests with `-run`
- **Parallel execution control:** Parallelize within groups
- **Shared setup/cleanup:** Setup once for multiple subtests
- **Better failure reporting:** Shows full test path

### Test Fixtures

Test fixtures provide consistent test data and environment setup for reliable, repeatable tests.

```go
// File-based fixtures
type FileFixture struct {
    t    *testing.T
    dir  string
    files map[string]string
}

func NewFileFixture(t *testing.T) *FileFixture {
    dir := t.TempDir()  // Automatically cleaned up
    
    return &FileFixture{
        t:     t,
        dir:   dir,
        files: make(map[string]string),
    }
}

func (f *FileFixture) CreateFile(name, content string) string {
    path := filepath.Join(f.dir, name)
    err := os.WriteFile(path, []byte(content), 0644)
    if err != nil {
        f.t.Fatal(err)
    }
    f.files[name] = path
    return path
}

func (f *FileFixture) Path(name string) string {
    return f.files[name]
}

func TestWithFileFixture(t *testing.T) {
    fixture := NewFileFixture(t)
    
    // Create test files
    configPath := fixture.CreateFile("config.json", `{"key": "value"}`)
    dataPath := fixture.CreateFile("data.txt", "test data")
    
    // Test with fixtures
    config, err := LoadConfig(configPath)
    if err != nil {
        t.Fatal(err)
    }
    
    if config.Key != "value" {
        t.Errorf("expected key=value, got key=%s", config.Key)
    }
}

// Database fixtures
type DBFixture struct {
    t  *testing.T
    db *sql.DB
}

func NewDBFixture(t *testing.T) *DBFixture {
    db, err := sql.Open("sqlite3", ":memory:")
    if err != nil {
        t.Fatal(err)
    }
    
    fixture := &DBFixture{t: t, db: db}
    fixture.setup()
    
    t.Cleanup(func() {
        db.Close()
    })
    
    return fixture
}

func (f *DBFixture) setup() {
    schema := `
    CREATE TABLE users (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL,
        email TEXT UNIQUE NOT NULL,
        created_at DATETIME DEFAULT CURRENT_TIMESTAMP
    );
    
    CREATE TABLE posts (
        id INTEGER PRIMARY KEY,
        user_id INTEGER,
        title TEXT,
        content TEXT,
        FOREIGN KEY (user_id) REFERENCES users(id)
    );`
    
    _, err := f.db.Exec(schema)
    if err != nil {
        f.t.Fatal(err)
    }
}

func (f *DBFixture) InsertUser(name, email string) int64 {
    result, err := f.db.Exec(
        "INSERT INTO users (name, email) VALUES (?, ?)",
        name, email,
    )
    if err != nil {
        f.t.Fatal(err)
    }
    
    id, err := result.LastInsertId()
    if err != nil {
        f.t.Fatal(err)
    }
    
    return id
}

func (f *DBFixture) InsertPost(userID int64, title, content string) int64 {
    result, err := f.db.Exec(
        "INSERT INTO posts (user_id, title, content) VALUES (?, ?, ?)",
        userID, title, content,
    )
    if err != nil {
        f.t.Fatal(err)
    }
    
    id, err := result.LastInsertId()
    if err != nil {
        f.t.Fatal(err)
    }
    
    return id
}

func TestWithDBFixture(t *testing.T) {
    fixture := NewDBFixture(t)
    
    // Insert test data
    userID := fixture.InsertUser("Alice", "alice@example.com")
    postID := fixture.InsertPost(userID, "First Post", "Hello World")
    
    // Test queries
    var count int
    err := fixture.db.QueryRow(
        "SELECT COUNT(*) FROM posts WHERE user_id = ?",
        userID,
    ).Scan(&count)
    
    if err != nil {
        t.Fatal(err)
    }
    
    if count != 1 {
        t.Errorf("expected 1 post, got %d", count)
    }
}

// Golden files fixtures
type GoldenFixture struct {
    t       *testing.T
    dir     string
    update  bool
}

func NewGoldenFixture(t *testing.T) *GoldenFixture {
    return &GoldenFixture{
        t:      t,
        dir:    "testdata",
        update: os.Getenv("UPDATE_GOLDEN") == "true",
    }
}

func (g *GoldenFixture) Check(name string, got []byte) {
    goldenPath := filepath.Join(g.dir, name+".golden")
    
    if g.update {
        err := os.MkdirAll(g.dir, 0755)
        if err != nil {
            g.t.Fatal(err)
        }
        
        err = os.WriteFile(goldenPath, got, 0644)
        if err != nil {
            g.t.Fatal(err)
        }
        
        g.t.Logf("Updated golden file: %s", goldenPath)
        return
    }
    
    want, err := os.ReadFile(goldenPath)
    if err != nil {
        g.t.Fatal(err)
    }
    
    if !bytes.Equal(got, want) {
        g.t.Errorf("output does not match golden file %s", goldenPath)
        g.t.Logf("got:\n%s", got)
        g.t.Logf("want:\n%s", want)
    }
}

func TestWithGoldenFiles(t *testing.T) {
    golden := NewGoldenFixture(t)
    
    // Generate output
    output := GenerateReport(testData)
    
    // Compare with golden file
    golden.Check("report", output)
}

// HTTP test server fixture
type ServerFixture struct {
    t      *testing.T
    server *httptest.Server
    client *http.Client
}

func NewServerFixture(t *testing.T, handler http.Handler) *ServerFixture {
    server := httptest.NewServer(handler)
    
    t.Cleanup(func() {
        server.Close()
    })
    
    return &ServerFixture{
        t:      t,
        server: server,
        client: server.Client(),
    }
}

func (f *ServerFixture) Get(path string) *http.Response {
    resp, err := f.client.Get(f.server.URL + path)
    if err != nil {
        f.t.Fatal(err)
    }
    return resp
}

func (f *ServerFixture) PostJSON(path string, body interface{}) *http.Response {
    data, err := json.Marshal(body)
    if err != nil {
        f.t.Fatal(err)
    }
    
    resp, err := f.client.Post(
        f.server.URL+path,
        "application/json",
        bytes.NewReader(data),
    )
    if err != nil {
        f.t.Fatal(err)
    }
    
    return resp
}

func TestWithServerFixture(t *testing.T) {
    handler := http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        switch r.URL.Path {
        case "/api/users":
            json.NewEncoder(w).Encode([]User{
                {Name: "Alice"},
                {Name: "Bob"},
            })
        default:
            w.WriteHeader(http.StatusNotFound)
        }
    })
    
    fixture := NewServerFixture(t, handler)
    
    resp := fixture.Get("/api/users")
    defer resp.Body.Close()
    
    if resp.StatusCode != http.StatusOK {
        t.Errorf("expected 200, got %d", resp.StatusCode)
    }
    
    var users []User
    json.NewDecoder(resp.Body).Decode(&users)
    
    if len(users) != 2 {
        t.Errorf("expected 2 users, got %d", len(users))
    }
}

// Fixture builder pattern
type TestDataBuilder struct {
    users  []User
    posts  []Post
    config Config
}

func NewTestDataBuilder() *TestDataBuilder {
    return &TestDataBuilder{
        config: DefaultConfig(),
    }
}

func (b *TestDataBuilder) WithUser(name, email string) *TestDataBuilder {
    b.users = append(b.users, User{
        ID:    len(b.users) + 1,
        Name:  name,
        Email: email,
    })
    return b
}

func (b *TestDataBuilder) WithPost(userID int, title string) *TestDataBuilder {
    b.posts = append(b.posts, Post{
        ID:     len(b.posts) + 1,
        UserID: userID,
        Title:  title,
    })
    return b
}

func (b *TestDataBuilder) WithConfig(cfg Config) *TestDataBuilder {
    b.config = cfg
    return b
}

func (b *TestDataBuilder) Build() *TestData {
    return &TestData{
        Users:  b.users,
        Posts:  b.posts,
        Config: b.config,
    }
}

func TestWithBuilder(t *testing.T) {
    data := NewTestDataBuilder().
        WithUser("Alice", "alice@example.com").
        WithUser("Bob", "bob@example.com").
        WithPost(1, "First Post").
        WithPost(1, "Second Post").
        WithPost(2, "Bob's Post").
        Build()
    
    if len(data.Users) != 2 {
        t.Errorf("expected 2 users, got %d", len(data.Users))
    }
    
    if len(data.Posts) != 3 {
        t.Errorf("expected 3 posts, got %d", len(data.Posts))
    }
}
```

**Fixture Best Practices:**

- **Use t.TempDir():** Automatic cleanup of temporary directories
- **Use t.Cleanup():** Register cleanup functions
- **Isolate tests:** Each test should have its own fixtures
- **Make fixtures reusable:** Create helper packages for common fixtures
- **Use golden files:** For complex expected outputs

### Mocking Interfaces

Mocking allows testing components in isolation by replacing dependencies with test doubles.

```go
// Interface to mock
type EmailSender interface {
    Send(to, subject, body string) error
}

type SMSSender interface {
    Send(to, message string) error
}

// Production implementation
type SMTPEmailSender struct {
    host string
    port int
}

func (s *SMTPEmailSender) Send(to, subject, body string) error {
    // Real SMTP implementation
    return nil
}

// Manual mock
type MockEmailSender struct {
    SendFunc   func(to, subject, body string) error
    SendCalls  []SendCall
}

type SendCall struct {
    To      string
    Subject string
    Body    string
}

func (m *MockEmailSender) Send(to, subject, body string) error {
    m.SendCalls = append(m.SendCalls, SendCall{
        To:      to,
        Subject: subject,
        Body:    body,
    })
    
    if m.SendFunc != nil {
        return m.SendFunc(to, subject, body)
    }
    
    return nil
}

// Service using the interface
type NotificationService struct {
    emailSender EmailSender
    smsSender   SMSSender
}

func NewNotificationService(email EmailSender, sms SMSSender) *NotificationService {
    return &NotificationService{
        emailSender: email,
        smsSender:   sms,
    }
}

func (s *NotificationService) NotifyUser(user User, message string) error {
    if user.Email != "" {
        err := s.emailSender.Send(user.Email, "Notification", message)
        if err != nil {
            return fmt.Errorf("failed to send email: %w", err)
        }
    }
    
    if user.Phone != "" {
        err := s.smsSender.Send(user.Phone, message)
        if err != nil {
            return fmt.Errorf("failed to send SMS: %w", err)
        }
    }
    
    return nil
}

// Testing with mocks
func TestNotificationService(t *testing.T) {
    t.Run("sends email when user has email", func(t *testing.T) {
        mockEmail := &MockEmailSender{}
        mockSMS := &MockSMSSender{}
        
        service := NewNotificationService(mockEmail, mockSMS)
        
        user := User{
            Name:  "Alice",
            Email: "alice@example.com",
        }
        
        err := service.NotifyUser(user, "Hello")
        if err != nil {
            t.Fatal(err)
        }
        
        // Verify email was sent
        if len(mockEmail.SendCalls) != 1 {
            t.Errorf("expected 1 email call, got %d", len(mockEmail.SendCalls))
        }
        
        call := mockEmail.SendCalls[0]
        if call.To != "alice@example.com" {
            t.Errorf("email sent to wrong address: %s", call.To)
        }
        
        // Verify SMS was not sent
        if len(mockSMS.SendCalls) != 0 {
            t.Errorf("expected no SMS calls, got %d", len(mockSMS.SendCalls))
        }
    })
    
    t.Run("handles email error", func(t *testing.T) {
        mockEmail := &MockEmailSender{
            SendFunc: func(to, subject, body string) error {
                return errors.New("SMTP error")
            },
        }
        mockSMS := &MockSMSSender{}
        
        service := NewNotificationService(mockEmail, mockSMS)
        
        user := User{Email: "alice@example.com"}
        err := service.NotifyUser(user, "Hello")
        
        if err == nil {
            t.Error("expected error but got nil")
        }
        
        if !strings.Contains(err.Error(), "failed to send email") {
            t.Errorf("unexpected error: %v", err)
        }
    })
}

// Advanced mock with expectations
type ExpectingMock struct {
    t           *testing.T
    expectations []Expectation
    callIndex    int
}

type Expectation struct {
    Method string
    Args   []interface{}
    Return []interface{}
}

func (m *ExpectingMock) Expect(method string, args ...interface{}) *Expectation {
    exp := Expectation{
        Method: method,
        Args:   args,
    }
    m.expectations = append(m.expectations, exp)
    return &m.expectations[len(m.expectations)-1]
}

func (m *ExpectingMock) Returns(values ...interface{}) {
    if len(m.expectations) > 0 {
        m.expectations[len(m.expectations)-1].Return = values
    }
}

func (m *ExpectingMock) AssertExpectations() {
    if m.callIndex != len(m.expectations) {
        m.t.Errorf("expected %d calls, got %d", len(m.expectations), m.callIndex)
    }
}

// Spy pattern - records but doesn't change behavior
type EmailSpy struct {
    EmailSender
    Calls []SendCall
}

func NewEmailSpy(sender EmailSender) *EmailSpy {
    return &EmailSpy{
        EmailSender: sender,
    }
}

func (s *EmailSpy) Send(to, subject, body string) error {
    s.Calls = append(s.Calls, SendCall{
        To:      to,
        Subject: subject,
        Body:    body,
    })
    
    return s.EmailSender.Send(to, subject, body)
}

// Stub pattern - returns predefined responses
type CacheStub struct {
    data map[string]interface{}
    err  error
}

func (c *CacheStub) Get(key string) (interface{}, error) {
    if c.err != nil {
        return nil, c.err
    }
    
    return c.data[key], nil
}

func (c *CacheStub) Set(key string, value interface{}) error {
    if c.err != nil {
        return c.err
    }
    
    c.data[key] = value
    return nil
}

// Interface with multiple methods
type Repository interface {
    Create(entity interface{}) error
    Get(id string) (interface{}, error)
    Update(id string, entity interface{}) error
    Delete(id string) error
    List(filter Filter) ([]interface{}, error)
}

// Configurable mock
type MockRepository struct {
    CreateFunc func(entity interface{}) error
    GetFunc    func(id string) (interface{}, error)
    UpdateFunc func(id string, entity interface{}) error
    DeleteFunc func(id string) error
    ListFunc   func(filter Filter) ([]interface{}, error)
    
    calls []MethodCall
    mu    sync.Mutex
}

type MethodCall struct {
    Method string
    Args   []interface{}
    Time   time.Time
}

func (m *MockRepository) Create(entity interface{}) error {
    m.recordCall("Create", entity)
    
    if m.CreateFunc != nil {
        return m.CreateFunc(entity)
    }
    return nil
}

func (m *MockRepository) Get(id string) (interface{}, error) {
    m.recordCall("Get", id)
    
    if m.GetFunc != nil {
        return m.GetFunc(id)
    }
    return nil, nil
}

func (m *MockRepository) recordCall(method string, args ...interface{}) {
    m.mu.Lock()
    defer m.mu.Unlock()
    
    m.calls = append(m.calls, MethodCall{
        Method: method,
        Args:   args,
        Time:   time.Now(),
    })
}

func (m *MockRepository) CallsTo(method string) []MethodCall {
    m.mu.Lock()
    defer m.mu.Unlock()
    
    var filtered []MethodCall
    for _, call := range m.calls {
        if call.Method == method {
            filtered = append(filtered, call)
        }
    }
    return filtered
}

// Testing with configurable mock
func TestServiceWithMock(t *testing.T) {
    mock := &MockRepository{
        GetFunc: func(id string) (interface{}, error) {
            if id == "123" {
                return User{ID: "123", Name: "Alice"}, nil
            }
            return nil, errors.New("not found")
        },
        CreateFunc: func(entity interface{}) error {
            user, ok := entity.(User)
            if !ok {
                return errors.New("invalid type")
            }
            if user.Name == "" {
                return errors.New("name required")
            }
            return nil
        },
    }
    
    service := NewService(mock)
    
    // Test Get
    user, err := service.GetUser("123")
    if err != nil {
        t.Fatal(err)
    }
    
    if user.Name != "Alice" {
        t.Errorf("expected Alice, got %s", user.Name)
    }
    
    // Verify mock was called
    getCalls := mock.CallsTo("Get")
    if len(getCalls) != 1 {
        t.Errorf("expected 1 Get call, got %d", len(getCalls))
    }
}

// Mock generator interface (for tools like mockgen)
//go:generate mockgen -source=interfaces.go -destination=mocks/mock_interfaces.go

// Test double factory
type TestDoubles struct {
    Email EmailSender
    SMS   SMSSender
    Cache Cache
    DB    Repository
}

func NewTestDoubles() *TestDoubles {
    return &TestDoubles{
        Email: &MockEmailSender{},
        SMS:   &MockSMSSender{},
        Cache: &CacheStub{data: make(map[string]interface{})},
        DB:    &MockRepository{},
    }
}

func (td *TestDoubles) WithEmail(sender EmailSender) *TestDoubles {
    td.Email = sender
    return td
}

func (td *TestDoubles) WithFailingEmail() *TestDoubles {
    td.Email = &MockEmailSender{
        SendFunc: func(to, subject, body string) error {
            return errors.New("email failed")
        },
    }
    return td
}
```

**Mocking Strategies:**

**Manual Mocks:**

- Full control over behavior
- Can add verification logic
- Good for simple interfaces
- No external dependencies

**Mock Generators (mockgen, moq):**

- Automatic mock generation
- Consistent API
- Good for large interfaces
- Requires tooling setup

**Test Doubles Types:**

- **Mock:** Verifies behavior (method calls, arguments)
- **Stub:** Returns predefined data
- **Spy:** Records calls but delegates to real implementation
- **Fake:** Simplified working implementation

**Mocking Best Practices:**

1. **Mock interfaces, not structs:** Design with interfaces
2. **Keep interfaces small:** Easier to mock and test
3. **Verify behavior, not implementation:** Focus on what, not how
4. **Use real implementations when possible:** Mock only external dependencies
5. **Generate mocks for stability:** Use tools for large interfaces
6. **Reset mocks between tests:** Avoid test pollution

**Testing Command Guidelines:**

```bash
# Run all tests
go test ./...

# Run specific test
go test -run TestName

# Run with coverage
go test -cover ./...
go test -coverprofile=coverage.out ./...
go tool cover -html=coverage.out

# Run with race detector
go test -race ./...

# Run benchmarks
go test -bench=.

# Run with verbose output
go test -v

# Run parallel tests with specific count
go test -parallel=4

# Update golden files
UPDATE_GOLDEN=true go test ./...

# Skip long tests
go test -short ./...

# Test with specific tags
go test -tags=integration ./...
```

**Key Testing Principles:**

- **Fast:** Unit tests should run quickly
- **Isolated:** Tests shouldn't depend on each other
- **Repeatable:** Same result every time
- **Self-validating:** Pass or fail, no manual inspection
- **Timely:** Write tests with the code