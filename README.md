# Go Programming: Zero to Hero
## Complete Guide to Mastering Go (Golang)

---

# Table of Contents

1. [Introduction to Go](#1-introduction-to-go)
2. [Setting Up Your Environment](#2-setting-up-your-environment)
3. [Your First Go Program](#3-your-first-go-program)
4. [Variables and Data Types](#4-variables-and-data-types)
5. [Constants](#5-constants)
6. [Control Flow](#6-control-flow)
7. [Functions](#7-functions)
8. [Packages and Modules](#8-packages-and-modules)
9. [Arrays and Slices](#9-arrays-and-slices)
10. [Maps](#10-maps)
11. [Structs](#11-structs)
12. [Pointers](#12-pointers)
13. [Methods and Interfaces](#13-methods-and-interfaces)
14. [Error Handling](#14-error-handling)
15. [Concurrency: Goroutines](#15-concurrency-goroutines)
16. [Concurrency: Channels](#16-concurrency-channels)
17. [Select Statement](#17-select-statement)
18. [Defer, Panic, and Recover](#18-defer-panic-and-recover)
19. [Testing in Go](#19-testing-in-go)
20. [Working with Files](#20-working-with-files)
21. [Strings and Runes](#21-strings-and-runes)
22. [Standard Library Overview](#22-standard-library-overview)
23. [Best Practices](#23-best-practices)
24. [Next Steps](#24-next-steps)

---

# 1. Introduction to Go

## What is Go?

Go (also known as Golang) is a statically typed, compiled programming language designed at Google by Robert Griesemer, Rob Pike, and Ken Thompson. It was first released in 2009 and officially launched in 2012.

## Why Learn Go?

- **Fast Compilation**: Go compiles extremely fast compared to other compiled languages
- **Simple Syntax**: Clean and easy-to-read syntax
- **Built-in Concurrency**: First-class support for concurrency with goroutines and channels
- **Strong Standard Library**: Comprehensive standard library
- **Cross-platform**: Compile for multiple platforms from a single codebase
- **Static Typing**: Catch errors at compile time
- **Garbage Collection**: Automatic memory management
- **Powerful Tooling**: Excellent tooling included with the language (go fmt, go test, etc.)

## Key Features of Go

| Feature | Description |
|---------|-------------|
| Goroutines | Lightweight threads managed by Go runtime |
| Channels | Type-safe communication between goroutines |
| Interfaces | Implicit implementation (duck typing) |
| Packages | Code organization and reuse |
| Static Linking | Single binary deployment |
| Fast Build | Incremental compilation |

---

# 2. Setting Up Your Environment

## Installing Go

### macOS / Linux

```bash
# Download Go
curl -O https://go.dev/dl/go1.22.0.linux-amd64.tar.gz

# Extract to /usr/local
sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz

# Add to PATH (add to ~/.bashrc or ~/.zshrc)
export PATH=$PATH:/usr/local/go/bin

# Verify installation
go version
```

### Windows

1. Download the MSI installer from https://go.dev/dl/
2. Run the installer and follow the prompts
3. Open Command Prompt or PowerShell and verify:

```powershell
go version
```

## Setting Up Your IDE/Editor

### VS Code (Recommended)

1. Install VS Code from https://code.visualstudio.com/
2. Install the Go extension by Google
3. Open a Go file and VS Code will prompt you to install Go tools

### Goland (IntelliJ)

1. Download from https://www.jetbrains.com/go/
2. Install and configure your Go SDK path

## Verifying Your Setup

Create and run a simple test:

```bash
# Create a test file
mkdir ~/go-projects
cd ~/go-projects
go mod init hello
```

```go
// hello.go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go!")
}
```

```bash
go run hello.go
```

Expected output: `Hello, Go!`

---

# 3. Your First Go Program

## Understanding the Structure

```go
// This is a comment
package main        // Every Go program starts with a package declaration

import "fmt"       // Import packages using double quotes

// Main function - entry point of the program
func main() {
    fmt.Println("Hello, World!")
}
```

## Key Observations

1. **No semicolons**: Go automatically inserts semicolons at line endings
2. **Indentation**: Uses tabs for indentation (go fmt handles this automatically)
3. **Curly braces**: Opening brace must be on the same line as the function declaration
4. **Package main**: Executable programs must use `package main`
5. **fmt.Println**: Println prints a line with a newline character

## Running Your Program

```bash
# Run directly (compile and run in memory)
go run hello.go

# Build to create executable
go build hello.go

# Build with custom name
go build -o myprogram hello.go

# Run the built executable
./myprogram
```

## Multiple Imports

```go
package main

import (
    "fmt"
    "math"
)

func main() {
    fmt.Println("Square root of 16 is", math.Sqrt(16))
}
```

---

# 4. Variables and Data Types

## Declaring Variables

### Explicit Declaration

```go
var name string = "Alice"
var age int = 30
var height float64 = 5.7
var isStudent bool = true
```

### Type Inference

```go
var name = "Alice"        // Inferred as string
var age = 30              // Inferred as int
var height = 5.7         // Inferred as float64
var isStudent = true      // Inferred as bool
```

### Short Variable Declaration

```go
// Only inside functions
name := "Alice"
age := 30
height := 5.7
isStudent := true
```

### Multiple Variable Declaration

```go
var (
    firstName = "John"
    lastName  = "Doe"
    age       = 25
)

// Multiple in one line
var a, b, c = 1, 2, 3
x, y, z := 4, 5, 6
```

## Basic Data Types

### Integers

| Type | Description | Range |
|------|-------------|-------|
| int8 | 8-bit signed | -128 to 127 |
| int16 | 16-bit signed | -32,768 to 32,767 |
| int32 | 32-bit signed | -2,147,483,648 to 2,147,483,647 |
| int64 | 64-bit signed | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| uint8 | 8-bit unsigned | 0 to 255 |
| uint16 | 16-bit unsigned | 0 to 65,535 |
| uint32 | 32-bit unsigned | 0 to 4,294,967,295 |
| uint64 | 64-bit unsigned | 0 to 18,446,744,073,709,551,615 |
| int | Platform dependent (32 or 64 bit) | Platform dependent |
| uint | Platform dependent unsigned | Platform dependent |
| rune | Alias for int32 (represents Unicode code point) | Same as int32 |

### Floating Point

```go
var pi float32 = 3.14159
var e float64 = 2.71828

// Short declaration
ratio := 3.14
```

### Complex Numbers

```go
var c complex64 = 1 + 2i
var d complex128 = 1 + 2i

// Using complex function
c = complex(1, 2)
```

### Strings

```go
var name string = "Hello, Go!"
var emptyString string = ""

// Multiline strings (raw strings)
message := `This is a multiline
string that spans
multiple lines`
```

### Booleans

```go
var isActive bool = true
var isEmpty bool = false

// Short declaration
isReady := true
```

## Zero Values (Default Values)

When a variable is declared but not initialized, Go assigns a zero value:

| Type | Zero Value |
|------|------------|
| Numeric (int, float) | 0 |
| Boolean | false |
| String | "" (empty string) |
| Pointer, Interface, Slice, Channel, Map | nil |

```go
var i int      // 0
var f float64  // 0
var b bool     // false
var s string   // ""
var arr []int  // [] (empty slice)
```

## Type Conversion

Go does not support automatic type conversion. You must convert explicitly:

```go
var i int = 42
var f float64 = float64(i)  // Convert int to float64
var u uint = uint(i)        // Convert int to uint

// Integer to string (requires strconv package)
import "strconv"
s := strconv.Itoa(i)        // "42"
s := fmt.Sprintf("%d", i)  // "42"

// String to integer
i, err := strconv.Atoi("42")

// Float to string
s := strconv.FormatFloat(f, 'f', 2, 64)  // "3.14"
```

---

# 5. Constants

## Declaring Constants

Constants are immutable values determined at compile time:

```go
const pi = 3.14159
const appName = "MyApp"
const version string = "1.0.0"

// Multiple constants
const (
    statusActive = 1
    statusInactive = 2
    statusPending = 3
)
```

## Typed vs Untyped Constants

```go
const typedInt int = 42        // Typed constant
const untypedInt = 42         // Untyped constant (can be used where int is expected)
const untypedFloat = 3.14     // Untyped floating-point constant
```

## Iota Enumerator

`iota` is a predeclared identifier that represents successive untyped integer constants:

```go
const (
    Sunday = iota  // 0
    Monday         // 1
    Tuesday        // 2
    Wednesday      // 3
    Thursday       // 4
    Friday         // 5
    Saturday       // 6
)

// Advanced iota usage
const (
    Flag1 = 1 << iota  // 1 (1 << 0)
    Flag2              // 2 (1 << 1)
    Flag3              // 4 (1 << 2)
)

const (
    _ = iota           // Ignore first value (0)
    KB = 1 << (10 * iota)  // 1024
    MB                       // 1048576
    GB                       // 1073741824
    TB                       // 1099511627776
)
```

---

# 6. Control Flow

## If Statement

```go
age := 18

if age >= 18 {
    fmt.Println("You are an adult")
}

// With else
if age < 18 {
    fmt.Println("You are a minor")
} else {
    fmt.Println("You are an adult")
}

// With else if
score := 85

if score >= 90 {
    fmt.Println("Grade: A")
} else if score >= 80 {
    fmt.Println("Grade: B")
} else if score >= 70 {
    fmt.Println("Grade: C")
} else {
    fmt.Println("Grade: F")
}

// With initialization (variable scope limited to if block)
if n := 10; n > 5 {
    fmt.Println("n is greater than 5")
}
```

## Switch Statement

```go
day := "Monday"

switch day {
case "Monday":
    fmt.Println("Start of work week")
case "Friday":
    fmt.Println("End of work week")
case "Saturday", "Sunday":
    fmt.Println("Weekend!")
default:
    fmt.Println("Regular weekday")
}
```

### Switch Without Expression

```go
num := 42

switch {
case num < 0:
    fmt.Println("Negative")
case num == 0:
    fmt.Println("Zero")
case num > 0 && num < 100:
    fmt.Println("Positive and less than 100")
default:
    fmt.Println("100 or more")
}
```

### Fallthrough

```go
switch num := 2; num {
case 1:
    fmt.Println("One")
    fallthrough
case 2:
    fmt.Println("Two (also executes)")
    fallthrough
case 3:
    fmt.Println("Three (also executes)")
default:
    fmt.Println("Other")
}
```

## For Loop

### Standard For Loop

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

### While-style For Loop

```go
i := 0
for i < 5 {
    fmt.Println(i)
    i++
}
```

### Infinite Loop

```go
for {
    fmt.Println("This runs forever")
    // Use break to exit
    // Use return to exit function
    break
}
```

### For Range Loop

```go
// Arrays/Slices
fruits := []string{"apple", "banana", "orange"}

for index, fruit := range fruits {
    fmt.Printf("%d: %s\n", index, fruit)
}

// Maps
ages := map[string]int{
    "Alice": 30,
    "Bob":   25,
}

for name, age := range ages {
    fmt.Printf("%s is %d years old\n", name, age)
}

// Strings
text := "Hello"

for index, char := range text {
    fmt.Printf("%d: %c\n", index, char)
}

// With index only
for index := range fruits {
    fmt.Println(index)
}

// With value only
for _, fruit := range fruits {
    fmt.Println(fruit)
}
```

### Break and Continue

```go
// Break - exit loop
for i := 0; i < 10; i++ {
    if i == 5 {
        break
    }
    fmt.Println(i)  // Prints 0, 1, 2, 3, 4
}

// Continue - skip iteration
for i := 0; i < 5; i++ {
    if i == 2 {
        continue
    }
    fmt.Println(i)  // Prints 0, 1, 3, 4
}

// Nested loops with labeled break
outer:
for i := 0; i < 3; i++ {
    for j := 0; j < 3; j++ {
        if i == 1 && j == 1 {
            break outer  // Breaks out of both loops
        }
        fmt.Printf("%d,%d ", i, j)
    }
}
```

---

# 7. Functions

## Basic Functions

```go
// Simple function
func greet() {
    fmt.Println("Hello!")
}

greet()  // Call the function
```

### Parameters and Return Values

```go
// Single parameter
func greet(name string) {
    fmt.Println("Hello,", name)
}

greet("Alice")  // Hello, Alice

// Multiple parameters
func add(a int, b int) int {
    return a + b
}

result := add(3, 4)  // 7

// Return multiple values
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

result, err := divide(10, 2)
```

### Named Return Values

```go
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return  // Naked return - returns x and y
}
```

### Variable Number of Arguments

```go
// Variadic function
func sum(numbers ...int) int {
    total := 0
    for _, n := range numbers {
        total += n
    }
    return total
}

sum(1, 2, 3)        // 6
sum(1, 2, 3, 4, 5)  // 15
sum()               // 0

// With regular parameters
func greetMany(prefix string, names ...string) {
    for _, name := range names {
        fmt.Println(prefix, name)
    }
}

greetMany("Mr.", "Smith", "Jones", "Brown")
```

## Functions as Values

```go
// Assign function to variable
add := func(a, b int) int {
    return a + b
}

result := add(3, 4)  // 7

// Function as parameter
func apply(op func(int, int) int, a, b int) int {
    return op(a, b)
}

result := apply(add, 3, 4)  // 7
```

## Closures

```go
// Closure function
func counter() func() int {
    count := 0
    return func() int {
        count++
        return count
    }
}

next := counter()
fmt.Println(next())  // 1
fmt.Println(next())  // 2
fmt.Println(next())  // 3

// Factory function
func multiplier(factor int) func(int) int {
    return func(x int) int {
        return x * factor
    }
}

double := multiplier(2)
triple := multiplier(3)

fmt.Println(double(5))   // 10
fmt.Println(triple(5))  // 15
```

## Defer

Functions can be scheduled to run after the surrounding function completes (even if it panics):

```go
func readFile(filename string) {
    file, err := os.Open(filename)
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    defer file.Close()  // Will run when readFile exits

    // Read and process file
    // ...
}
```

Multiple defers execute in LIFO (Last In, First Out) order:

```go
func example() {
    defer fmt.Println("First")
    defer fmt.Println("Second")
    defer fmt.Println("Third")

    fmt.Println("Main logic")
}
// Output:
// Main logic
// Third
// Second
// First
```

---

# 8. Packages and Modules

## Package System

### Package Declaration

Every Go file starts with a package declaration:

```go
package main  // Executable programs
package math  // Library packages
```

### Package Names

- The package name should match the directory name (usually lowercase, short)
- Files in the same package can access each other's functions without importing
- `package main` is special - it tells Go this is an executable, not a library

## Creating Modules

### Initialize a Module

```bash
go mod init module-name
# Example:
go mod init github.com/username/myapp
```

This creates a `go.mod` file:

```
module github.com/username/myapp

go 1.22
```

### Directory Structure

```
myapp/
├── go.mod
├── main.go
└── greet/
    └── greet.go
```

### Package with Functions

```go
// greet/greet.go
package greet

import "fmt"

func Hello(name string) {
    fmt.Printf("Hello, %s!\n", name)
}

func Goodbye(name string) {
    fmt.Printf("Goodbye, %s!\n", name)
}
```

### Using the Package

```go
// main.go
package main

import (
    "fmt"
    "myapp/greet"
)

func main() {
    fmt.Println("Welcome to my app!")
    greet.Hello("Alice")
    greet.Goodbye("Alice")
}
```

## Importing Packages

### Standard Import

```go
import "fmt"
import "strings"
import "math"
```

### Grouped Import

```go
import (
    "fmt"
    "strings"
    "math"
)
```

### Named Import (Alias)

```go
import (
    f "fmt"           // Alias as 'f'
    str "strings"     // Alias as 'str'
)

func main() {
    f.Println("Hello")      // Using 'f'
    f.Println(str.ToUpper("hello"))  // Using 'str'
}
```

### External Packages

```bash
# Install a package
go get github.com/gin-gonic/gin

# Install specific version
go get github.com/gin-gonic/gin@v1.9.1
```

```go
import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{"message": "pong"})
    })
    r.Run()
}
```

## Module Management

### go.mod File

```
module github.com/myapp

go 1.22

require (
    github.com/gin-gonic/gin v1.9.1
    github.com/go-sql-driver/mysql v1.7.1
)
```

### Useful Commands

```bash
go mod init module-name      # Initialize new module
go mod tidy                 # Update dependencies
go mod download             # Download dependencies
go mod verify               # Verify dependencies
go list -m all             # List all modules
go get package@version     # Add/update package
go mod why package         # Explain why package is needed
```

---

# 9. Arrays and Slices

## Arrays

### Declaration

```go
// Fixed size, explicit type
var numbers [5]int

// With initialization
var fruits [3]string = [3]string{"apple", "banana", "orange"}

// Short declaration
colors := [3]string{"red", "green", "blue"}

// Let Go infer length
names := [...]string{"Alice", "Bob", "Charlie"}  // Length is 3
```

### Accessing Elements

```go
fruits := [3]string{"apple", "banana", "orange"}

fmt.Println(fruits[0])  // apple
fmt.Println(fruits[2]) // orange

// Modify element
fruits[1] = "mango"
```

### Array Length

```go
fruits := [3]string{"apple", "banana", "orange"}

fmt.Println(len(fruits))  // 3
```

### Iterating Over Arrays

```go
fruits := [3]string{"apple", "banana", "orange"}

for i := 0; i < len(fruits); i++ {
    fmt.Println(fruits[i])
}

for index, fruit := range fruits {
    fmt.Printf("%d: %s\n", index, fruit)
}
```

## Slices

Slices are dynamic, flexible views into arrays.

### Declaration

```go
// Create a slice
var nums []int

// With make function
nums := make([]int, 5)         // Length 5, capacity 5
nums := make([]int, 3, 10)    // Length 3, capacity 10

// Literal initialization
fruits := []string{"apple", "banana", "orange"}

// From array
arr := [5]int{1, 2, 3, 4, 5}
slice := arr[1:4]  // Elements at index 1, 2, 3
```

### Slice Operations

```go
fruits := []string{"apple", "banana"}

// Append elements
fruits = append(fruits, "orange")
fruits = append(fruits, "mango", "grape")

// Length and Capacity
fmt.Println(len(fruits))  // 4
fmt.Println(cap(fruits))  // Depends on implementation

// Copy slice
source := []int{1, 2, 3}
dest := make([]int, len(source))
copy(dest, source)

// Sub-slices
nums := []int{1, 2, 3, 4, 5}
slice1 := nums[1:3]   // [2, 3]
slice2 := nums[:3]    // [1, 2, 3]
slice3 := nums[3:]    // [4, 5]
slice4 := nums[:]     // [1, 2, 3, 4, 5]
```

### Slices are Reference Types

```go
original := []int{1, 2, 3}
copy := original

copy[0] = 100

fmt.Println(original)  // [100, 2, 3] - changed!
fmt.Println(copy)     // [100, 2, 3]
```

### Useful Functions

```go
import "sort"

nums := []int{3, 1, 4, 1, 5, 9, 2, 6}

// Sort
sort.Ints(nums)
fmt.Println(nums)  // [1, 1, 2, 3, 4, 5, 6, 9]

// Search (sorted slice)
index := sort.SearchInts(nums, 5)  // Returns index of 5

// Check if sorted
sorted := sort.IntsAreSorted(nums)

// Strings
words := []string{"banana", "apple", "cherry"}
sort.Strings(words)
fmt.Println(words)  // [apple banana cherry]

// Reverse
sort.Sort(sort.Reverse(sort.IntSlice(nums)))
```

---

# 10. Maps

## Declaration and Initialization

```go
// Declaration
var ages map[string]int

// Initialization
ages = make(map[string]int)

// Literal initialization
ages := map[string]int{
    "Alice": 30,
    "Bob":   25,
}
```

## Operations

### Adding/Updating Elements

```go
ages := map[string]int{}

// Add element
ages["Charlie"] = 35

// Update element
ages["Alice"] = 31
```

### Accessing Elements

```go
ages := map[string]int{"Alice": 30, "Bob": 25}

// Direct access
age := ages["Alice"]  // 30

// Two-value access (check if key exists)
age, exists := ages["Charlie"]
if !exists {
    fmt.Println("Charlie not found")
}
```

### Deleting Elements

```go
ages := map[string]int{"Alice": 30, "Bob": 25}

delete(ages, "Bob")  // Delete Bob

// Check if deleted
_, exists := ages["Bob"]
fmt.Println("Bob exists:", exists)  // false
```

### Length

```go
ages := map[string]int{"Alice": 30, "Bob": 25}

fmt.Println(len(ages))  // 2
```

### Iterating Over Maps

```go
ages := map[string]int{
    "Alice":   30,
    "Bob":     25,
    "Charlie": 35,
}

// Iterate key-value pairs
for name, age := range ages {
    fmt.Printf("%s is %d years old\n", name, age)
}

// Iterate keys only
for name := range ages {
    fmt.Println(name)
}

// Iterate values only
for _, age := range ages {
    fmt.Println(age)
}
```

### Maps are Reference Types

```go
original := map[string]int{"a": 1}
copy := original
copy["a"] = 100

fmt.Println(original["a"])  // 100
fmt.Println(copy["a"])       // 100
```

## Thread Safety

Maps are NOT safe for concurrent use. For concurrent access, use sync.Map or mutex:

```go
import "sync"

var counter = struct {
    sync.RWMutex
    m map[string]int
}{m: make(map[string]int)}

// Increment
counter.Lock()
counter.m["page"]++
counter.Unlock()

// Read
counter.RLock()
count := counter.m["page"]
counter.RUnlock()
```

---

# 11. Structs

## Defining Structs

```go
// Define a struct type
type Person struct {
    Name  string
    Age   int
    Email string
}

// Nested structs
type Address struct {
    Street string
    City   string
    State  string
    Zip    string
}

type Employee struct {
    Person
    Address
    ID     int
    Salary float64
}
```

## Creating Struct Instances

```go
// Using field names
person := Person{
    Name:  "Alice",
    Age:   30,
    Email: "alice@example.com",
}

// Without field names (order matters)
person := Person{"Alice", 30, "alice@example.com"}

// Using new keyword (returns pointer)
person := new(Person)
person.Name = "Alice"
person.Age = 30

// Zero value struct
var person Person  // All fields are zero values

// Using make (only for structs with pointers, slices, maps)
person := &Person{
    Name:  "Alice",
    Age:   30,
}
```

## Accessing Fields

```go
person := Person{Name: "Alice", Age: 30}

fmt.Println(person.Name)   // Alice
fmt.Println(person.Age)    // 30

// Modify fields
person.Age = 31
```

## Nested Structs

```go
type Address struct {
    Street string
    City   string
}

type Person struct {
    Name    string
    Address Address
}

person := Person{
    Name: "Alice",
    Address: Address{
        Street: "123 Main St",
        City:   "New York",
    },
}

fmt.Println(person.Address.City)  // New York
```

## Anonymous Structs

```go
person := struct {
    Name string
    Age  int
}{
    Name: "Alice",
    Age:  30,
}
```

## Struct Tags

```go
import "encoding/json"

type Person struct {
    Name  string `json:"name"`
    Age   int    `json:"age"`
    Email string `json:"email,omitempty"`
}

p := Person{Name: "Alice", Age: 30}

// Marshal to JSON
jsonData, _ := json.Marshal(p)
fmt.Println(string(jsonData))
// {"name":"Alice","age":30}
```

---

# 12. Pointers

## Understanding Pointers

Go uses pointers to reference memory locations.

### Memory Addresses

```go
x := 42
fmt.Println(&x)  // Print memory address, e.g., 0xc000014088
```

### Pointer Declaration

```go
var p *int        // p is a pointer to an int

x := 42
p = &x           // p now points to x

fmt.Println(p)   // Memory address
fmt.Println(*p)  // Value at that address: 42
```

### Zero Value of Pointers

```go
var p *int  // nil (zero value for pointers)

if p != nil {
    fmt.Println(*p)
} else {
    fmt.Println("p is nil")
}
```

### Creating Pointers with new

```go
p := new(int)     // Allocate memory for int, returns *int
*p = 42
fmt.Println(*p)   // 42
fmt.Println(p)    // Memory address
```

## Pointer Operations

### Dereferencing

```go
x := 42
p := &x

fmt.Println(*p)   // 42

*p = 100          // Modify value through pointer
fmt.Println(x)    // 100
```

### Passing Pointers to Functions

```go
func double(n *int) {
    *n = *n * 2
}

x := 5
double(&x)
fmt.Println(x)  // 10
```

### Pointers and Slices/Maps

Slices and maps already behave like references, but pointers can be used:

```go
func modifySlice(s []int) {
    s[0] = 100  // Modifies original slice
}

nums := []int{1, 2, 3}
modifySlice(nums)
fmt.Println(nums)  // [100, 2, 3]
```

## When to Use Pointers

### Use Pointers When:

- Modifying the original value (function needs to modify caller data)
- Large structs (avoid copying)
- nil value is meaningful
- Defining methods on types

### Use Values When:

- Immutable data
- Simple types (int, float, bool)
- Small structs (copying is cheap)

## Pointer to Struct

```go
type Person struct {
    Name string
    Age  int
}

person := Person{Name: "Alice", Age: 30}

// Pointer to struct
p := &person

fmt.Println(p.Name)   // Alice (Go auto-dereferences)
fmt.Println((*p).Name)  // Alice (explicit dereference)

// Modify through pointer
p.Age = 31
fmt.Println(person.Age)  // 31
```

---

# 13. Methods and Interfaces

## Methods

Methods are functions attached to types.

### Method Syntax

```go
type Person struct {
    Name string
    Age  int
}

// Value receiver (copy)
func (p Person) Greet() {
    fmt.Printf("Hello, I'm %s\n", p.Name)
}

// Pointer receiver (reference)
func (p *Person) SetAge(age int) {
    p.Age = age
}

person := Person{Name: "Alice", Age: 30}
person.Greet()      // Hello, I'm Alice
person.SetAge(31)
fmt.Println(person.Age)  // 31
```

### Value vs Pointer Receivers

**Use pointer receivers when:**
- Method needs to modify the receiver
- Method involves a large struct (avoid copying)
- Method involves sync.Mutex or similar

**Use value receivers when:**
- Method doesn't need to modify receiver
- Value is small (int, bool, etc.)

## Interfaces

Interfaces define behavior without implementation.

### Basic Interface

```go
type Shape interface {
    Area() float64
    Perimeter() float64
}

type Rectangle struct {
    Width  float64
    Height float64
}

func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

func (r Rectangle) Perimeter() float64 {
    return 2 * (r.Width + r.Height)
}

type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return math.Pi * c.Radius * c.Radius
}

func (c Circle) Perimeter() float64 {
    return 2 * math.Pi * c.Radius
}
```

### Using Interfaces

```go
func printArea(s Shape) {
    fmt.Printf("Area: %.2f\n", s.Area())
}

rect := Rectangle{Width: 10, Height: 5}
circle := Circle{Radius: 7}

printArea(rect)    // Area: 50.00
printArea(circle)  // Area: 153.94
```

## Empty Interface

```go
var i interface{} = "hello"
fmt.Println(i)  // hello

// Accept any type
func printAny(v interface{}) {
    fmt.Println(v)
}

printAny(42)
printAny("hello")
printAny(3.14)
```

## Type Assertions

```go
var i interface{} = "hello"

// Type assertion (may panic if wrong)
s := i.(string)
fmt.Println(s)  // hello

// Type assertion with ok check
s, ok := i.(string)
if ok {
    fmt.Println(s)
} else {
    fmt.Println("not a string")
}

// Switch on type
switch v := i.(type) {
case string:
    fmt.Println("string:", v)
case int:
    fmt.Println("int:", v)
default:
    fmt.Println("unknown type")
}
```

## Common Standard Library Interfaces

### Stringer

```go
type Stringer interface {
    String() string
}

type Person struct {
    Name string
}

func (p Person) String() string {
    return "Person: " + p.Name
}

p := Person{Name: "Alice"}
fmt.Println(p)  // Person: Alice
```

### Error

```go
type Error interface {
    Error() string
}

// Implementing error
type MyError struct {
    Message string
}

func (e MyError) Error() string {
    return e.Message
}
```

### Reader and Writer

```go
import "io"

type Reader interface {
    Read(p []byte) (n int, err error)
}

type Writer interface {
    Write(p []byte) (n int, err error)
}
```

---

# 14. Error Handling

## The Error Interface

```go
type error interface {
    Error() string
}
```

## Creating Errors

### Using errors.New

```go
import "errors"

func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}
```

### Using fmt.Errorf

```go
import "fmt"

func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("cannot divide %f by zero", a)
    }
    return a / b, nil
}
```

### Custom Error Types

```go
import "errors"

type ValidationError struct {
    Field   string
    Message string
}

func (e ValidationError) Error() string {
    return fmt.Sprintf("%s: %s", e.Field, e.Message)
}

err := ValidationError{
    Field:   "email",
    Message: "invalid email format",
}
```

## Handling Errors

### Basic Error Handling

```go
result, err := divide(10, 0)
if err != nil {
    fmt.Println("Error:", err)
    return
}
fmt.Println("Result:", result)
```

### Custom Error Types with Type Assertion

```go
result, err := divide(10, 0)
if err != nil {
    if valErr, ok := err.(ValidationError); ok {
        fmt.Println("Validation error:", valErr.Field)
    } else {
        fmt.Println("Other error:", err)
    }
    return
}
```

### Ignoring Errors (when intentionally ignored)

```go
result, _ = divide(10, 0)  // Underscore ignores the error
```

## Error Wrapping (Go 1.13+)

```go
import "fmt"

func readConfig(path string) error {
    return fmt.Errorf("config not found: %w", err)
}

func loadApp() error {
    if err := readConfig("/path/to/config"); err != nil {
        return fmt.Errorf("failed to load app: %w", err)
    }
    return nil
}

// Check for specific error using errors.Is
import "errors"

err := loadApp()
if errors.Is(err, ErrNotFound) {
    // Handle not found
}
```

## Best Practices

1. **Don't ignore errors**
2. **Return errors, don't panic** (in most cases)
3. **Wrap errors with context**
4. **Use specific error types when needed**
5. **Error messages should be lowercase** (conventional)

---

# 15. Concurrency: Goroutines

## What are Goroutines?

Goroutines are lightweight threads managed by the Go runtime. They run concurrently with other goroutines in the same address space.

## Starting a Goroutine

```go
func sayHello() {
    fmt.Println("Hello!")
}

func main() {
    go sayHello()  // Start a new goroutine
    fmt.Println("World!")

    // Wait for goroutine to complete
    time.Sleep(time.Second)
}
```

## Anonymous Goroutines

```go
func main() {
    go func(msg string) {
        fmt.Println(msg)
    }("Hello from goroutine")

    fmt.Println("Hello from main")
    time.Sleep(time.Second)
}
```

## Goroutines are Non-blocking

```go
func main() {
    go fmt.Println("This won't print immediately")
    fmt.Println("This will print first")

    // Without sleep, program exits before goroutine runs
    time.Sleep(time.Millisecond)
}
```

## Waiting for Goroutines with sync.WaitGroup

```go
import "sync"

func worker(id int, wg *sync.WaitGroup) {
    defer wg.Done()  // Signal completion
    fmt.Printf("Worker %d starting\n", id)
    time.Sleep(time.Second)
    fmt.Printf("Worker %d done\n", id)
}

func main() {
    var wg sync.WaitGroup

    for i := 1; i <= 5; i++ {
        wg.Add(1)  // Add a goroutine to wait group
        go worker(i, &wg)
    }

    wg.Wait()  // Block until all goroutines complete
    fmt.Println("All workers done")
}
```

## sync.Mutex for Shared Resources

```go
import (
    "sync"
    "fmt"
)

type Counter struct {
    count int
    mu    sync.Mutex
}

func (c *Counter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.count++
}

func (c *Counter) Get() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.count
}

func main() {
    counter := Counter{}

    var wg sync.WaitGroup

    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            counter.Increment()
            wg.Done()
        }()
    }

    wg.Wait()
    fmt.Println("Counter:", counter.Get())  // Should be 1000
}
```

---

# 16. Concurrency: Channels

## Channel Basics

Channels provide communication between goroutines.

### Creating Channels

```go
ch := make(chan int)        // Unbuffered channel
ch := make(chan int, 10)    // Buffered channel with capacity 10
```

### Sending and Receiving

```go
// Unbuffered channel
ch := make(chan int)

// Send (blocking)
go func() {
    ch <- 42  // Send 42 to channel
}()

// Receive (blocking)
value := <-ch
fmt.Println(value)  // 42

// Receive with ok
value, ok := <-ch
if ok {
    fmt.Println(value)
}
```

### Channel Directions

When using channels as function parameters, you can specify direction:

```go
// Sender only - can only send
func send(ch chan<- int) {
    ch <- 42
}

// Receiver only - can only receive
func receive(ch <-chan int) {
    value := <-ch
    fmt.Println(value)
}
```

## Buffered vs Unbuffered Channels

### Unbuffered Channel

```go
ch := make(chan int)

// Sending blocks until receiver is ready
// Receiving blocks until sender is ready
// Synchronization happens automatically
```

### Buffered Channel

```go
ch := make(chan int, 3)

// Sending blocks only when buffer is full
// Receiving blocks only when buffer is empty
// Asynchronous until buffer is full
```

```go
ch := make(chan string, 2)

ch <- "Hello"
ch <- "World"
// ch <- "Blocked"  // Would block because buffer is full

fmt.Println(<-ch)  // Hello
fmt.Println(<-ch)  // World
```

## Channel Range and Close

### Ranging Over Channel Values

```go
ch := make(chan int, 5)

go func() {
    for i := 1; i <= 5; i++ {
        ch <- i
    }
    close(ch)  // Close channel when done
}()

for value := range ch {
    fmt.Println(value)
}
// 1, 2, 3, 4, 5
```

### Closing Channels

```go
ch := make(chan int)

// Only sender should close channel
close(ch)

// Receive from closed channel
value, ok := <-ch
// ok is false, value is zero value
```

## Select Statement

The `select` statement lets a goroutine wait on multiple channel operations:

```go
ch1 := make(chan string)
ch2 := make(chan string)

go func() {
    time.Sleep(time.Second)
    ch1 <- "from channel 1"
}()

go func() {
    time.Sleep(time.Millisecond * 500)
    ch2 <- "from channel 2"
}()

select {
case msg1 := <-ch1:
    fmt.Println("Received:", msg1)
case msg2 := <-ch2:
    fmt.Println("Received:", msg2)
case <-time.After(time.Millisecond * 100):
    fmt.Println("Timeout")
}
```

### Select with Default

```go
select {
case msg := <-ch:
    fmt.Println(msg)
default:
    fmt.Println("No message available")
}
```

## Channel Patterns

### Fan-Out (Multiple Workers)

```go
func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Printf("worker %d started job %d\n", id, j)
        time.Sleep(time.Second)
        fmt.Printf("worker %d finished job %d\n", id, j)
        results <- j * 2
    }
}

func main() {
    jobs := make(chan int, 100)
    results := make(chan int, 100)

    // Start 3 workers
    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }

    // Send 5 jobs
    for j := 1; j <= 5; j++ {
        jobs <- j
    }
    close(jobs)

    // Collect results
    for a := 1; a <= 5; a++ {
        <-results
    }
}
```

### Pipeline Pattern

```go
func generate(nums ...int) <-chan int {
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

func main() {
    // Pipeline: generate -> square -> print
    for n := range square(square(generate(2, 3))) {
        fmt.Println(n)  // 16, 81
    }
}
```

---

# 17. Select Statement

## Basic Select

```go
select {
case <-ch1:
    fmt.Println("Received from ch1")
case ch2 <- 42:
    fmt.Println("Sent 42 to ch2")
case <-time.After(time.Second):
    fmt.Println("Timeout")
}
```

## Select with Multiple Cases

```go
ch1 := make(chan string)
ch2 := make(chan string)

go func() {
    ch1 <- "message from ch1"
}()

go func() {
    ch2 <- "message from ch2"
}()

for i := 0; i < 2; i++ {
    select {
    case msg1 := <-ch1:
        fmt.Println(msg1)
    case msg2 := <-ch2:
        fmt.Println(msg2)
    }
}
```

## Select with Default

```go
select {
case msg := <-ch:
    fmt.Println(msg)
default:
    fmt.Println("No message ready")
}
```

## Empty Select

```go
select {}
// Blocks forever (deadlock)
```

## Select with Nil Channel

```go
var ch1 chan int  // nil channel

select {
case <-ch1:  // Never ready (blocked)
    fmt.Println("This won't print")
case <-ch2:
    fmt.Println("ch2 ready")
default:
    fmt.Println("default case")
}
// Output: default case
```

---

# 18. Defer, Panic, and Recover

## Defer

Defer postpones the execution of a function until the surrounding function returns.

### Basic Usage

```go
func readFile(filename string) {
    file, err := os.Open(filename)
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    defer file.Close()

    // Use file
}
```

### Multiple Defers (LIFO Order)

```go
func example() {
    defer fmt.Println("First")
    defer fmt.Println("Second")
    defer fmt.Println("Third")

    fmt.Println("Main")
}
// Output:
// Main
// Third
// Second
// First
```

### Defer with Named Return Values

```go
func double(a []int) (n int) {
    defer func() {
        n *= 2
    }()

    n = len(a)
    return
}

result := double([]int{1, 2, 3})
fmt.Println(result)  // 6 (2 * 3)
```

## Panic

Panic is like an unhandled exception that stops execution.

### Triggering Panic

```go
func main() {
    panic("Something went wrong!")
    fmt.Println("This won't print")
}
```

### When to Use Panic

- Irrecoverable errors (programming bugs)
- Program invariants are violated
- Initialization failures when nothing else makes sense

### Panic Behavior

1. Stops normal execution
2. Starts unwinding the stack
3. Runs deferred functions
4. Prints stack trace and exits

```go
func main() {
    defer fmt.Println("This runs")

    panic("Panic!")
    fmt.Println("This won't run")
}
```

## Recover

Recover regains control of a panicking goroutine.

### Basic Recover

```go
func safeCall() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered from", r)
        }
    }()

    panic("Something went wrong")
}

func main() {
    safeCall()
    fmt.Println("Program continues")
}
```

### Recover in Defer Function

```go
func mayPanic() {
    panic("Oops!")
}

func doRecover() {
    if r := recover(); r != nil {
        fmt.Println("Recovered:", r)
    }
}

func main() {
    defer doRecover()
    mayPanic()
    fmt.Println("After mayPanic")
}
// Output:
// Recovered: Oops!
// After mayPanic
```

### Best Practices

1. **Use panic sparingly** - most errors should be handled with error returns
2. **Defer recover** - catch panics at package boundaries
3. **Log and exit** - after recover, either fix the issue or exit gracefully

---

# 19. Testing in Go

## Test Files

Test files must:
1. End with `_test.go`
2. Be in the same package or a `xxx_test` package
3. Import `testing` package

## Writing Tests

### Basic Test

```go
// math.go
package math

func Add(a, b int) int {
    return a + b
}

func Multiply(a, b int) int {
    return a * b
}
```

```go
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

func TestMultiply(t *testing.T) {
    result := Multiply(3, 4)
    expected := 12

    if result != expected {
        t.Errorf("Multiply(3, 4) = %d; want %d", result, expected)
    }
}
```

### Table-Driven Tests

```go
func TestAddTableDriven(t *testing.T) {
    tests := []struct {
        name     string
        a, b     int
        expected int
    }{
        {"simple", 2, 3, 5},
        {"negative", -1, -1, -2},
        {"zero", 0, 5, 5},
        {"large", 1000, 2000, 3000},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            result := Add(tt.a, tt.b)
            if result != tt.expected {
                t.Errorf("Add(%d, %d) = %d; want %d", tt.a, tt.b, result, tt.expected)
            }
        })
    }
}
```

## Running Tests

```bash
go test                          # Run all tests
go test -v                       # Verbose output
go test -run TestAdd            # Run specific test
go test -run "TestAdd|TestMul"  # Run tests matching pattern
go test -cover                   # Show coverage
go test -coverprofile=cover.out # Save coverage report
go test -bench .                # Run benchmarks
go test -race                   # Check for race conditions
```

## Test Functions

| Function | Description |
|----------|-------------|
| testing.T.Error | Log error and mark test as failed |
| testing.T.Errorf | Log formatted error |
| testing.T.Fatal | Log error and stop test immediately |
| testing.T.Fatalf | Log formatted error and stop test |
| testing.T.Skip | Skip this test |
| testing.T.Skipf | Skip with formatted message |

## Benchmark Tests

```go
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(1, 2)
    }
}
```

```bash
go test -bench=BenchmarkAdd -benchmem
```

## Example Tests

```go
func ExampleAdd() {
    result := Add(2, 3)
    fmt.Println(result)
    // Output: 5
}
```

---

# 20. Working with Files

## Reading Files

### Read Entire File

```go
import (
    "os"
    "fmt"
    "io/ioutil"
)

func main() {
    data, err := ioutil.ReadFile("file.txt")
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    fmt.Println(string(data))
}
```

### Read File with os.Open

```go
import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("file.txt")
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    defer file.Close()

    scanner := bufio.NewScanner(file)
    for scanner.Scan() {
        fmt.Println(scanner.Text())
    }

    if err := scanner.Err(); err != nil {
        fmt.Println("Error:", err)
    }
}
```

### Read File Line by Line

```go
import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("file.txt")
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    defer file.Close()

    reader := bufio.NewReader(file)
    for {
        line, _, err := reader.ReadLine()
        if err != nil {
            break
        }
        fmt.Println(string(line))
    }
}
```

## Writing Files

### Write Entire File

```go
import (
    "os"
    "fmt"
)

func main() {
    content := "Hello, World!"

    err := os.WriteFile("output.txt", []byte(content), 0644)
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
}
```

### Write with os.Create

```go
import (
    "bufio"
    "os"
    "fmt"
)

func main() {
    file, err := os.Create("output.txt")
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    defer file.Close()

    writer := bufio.NewWriter(file)

    for i := 1; i <= 10; i++ {
        fmt.Fprintf(writer, "Line %d\n", i)
    }

    writer.Flush()
}
```

## File Operations

```go
import "os"

func main() {
    // Rename file
    os.Rename("old.txt", "new.txt")

    // Delete file
    os.Remove("file.txt")

    // Check if file exists
    _, err := os.Stat("file.txt")
    if os.IsNotExist(err) {
        fmt.Println("File does not exist")
    }

    // Create directory
    os.Mkdir("newdir", 0755)

    // Create directory recursively
    os.MkdirAll("path/to/dir", 0755)

    // Remove directory
    os.Remove("dir")
}
```

---

# 21. Strings and Runes

## Strings

### Creating Strings

```go
str := "Hello, World!"
str := `Multiline
string`

empty := ""
```

### String Length

```go
import "unicode/utf8"

str := "Hello"
len(str)           // 5 bytes
utf8.RuneCountInString(str)  // 5 characters
```

### Accessing Characters

```go
str := "Hello"

for i := 0; i < len(str); i++ {
    fmt.Printf("%c ", str[i])
}
// H e l l o
```

### Iterating with Runes

```go
str := "Hello 世界"

for i, r := range str {
    fmt.Printf("%d: %c\n", i, r)
}
// 0: H
// 1: e
// 2: l
// ...
```

## String Package (strings)

```go
import "strings"

s := "Hello, World!"

// Case conversion
strings.ToLower(s)   // "hello, world!"
strings.ToUpper(s)   // "HELLO, WORLD!"
strings.ToTitle(s)   // "HELLO, WORLD!"

// Search functions
strings.Contains(s, "World")        // true
strings.Contains(s, "world")        // false
strings.HasPrefix(s, "Hello")       // true
strings.HasSuffix(s, "!")            // true
strings.Index(s, "World")           // 7
strings.LastIndex(s, "o")           // 8

// Modification
strings.Replace(s, "World", "Go", 1)    // "Hello, Go!"
strings.ReplaceAll(s, "o", "0")         // "Hell0, W0rld!"
strings.TrimSpace("  hello  ")          // "hello"
strings.Split("a-b-c", "-")               // ["a", "b", "c"]
strings.Join([]string{"a", "b"}, "-")    // "a-b"

// Repetition
strings.Repeat("ab", 3)  // "ababab"

// Fields and Trim
strings.Fields("  a b c  ")  // ["a", "b", "c"]
strings.Trim("!!!hello!!!", "!")  // "hello"
```

## strconv Package

```go
import "strconv"

// String to int
n, _ := strconv.Atoi("42")

// Int to string
s := strconv.Itoa(42)

// String to float
f, _ := strconv.ParseFloat("3.14", 64)

// Float to string
s := strconv.FormatFloat(3.14, 'f', 2, 64)  // "3.14"

// String to bool
b, _ := strconv.ParseBool("true")

// Bool to string
s := strconv.FormatBool(true)

// Int to base conversion
s := strconv.FormatInt(255, 16)  // "ff" (hex)
s := strconv.FormatInt(255, 2)   // "11111111" (binary)
```

## String Formatting

### fmt.Sprintf

```go
name := "Alice"
age := 30

s := fmt.Sprintf("Name: %s, Age: %d", name, age)
// "Name: Alice, Age: 30"
```

### Format Verbs

| Verb | Description | Example |
|------|-------------|---------|
| %v | Default format | `fmt.Sprintf("%v", x)` |
| %T | Type | `fmt.Sprintf("%T", x)` |
| %d | Integer decimal | `fmt.Sprintf("%d", 42)` |
| %f | Float | `fmt.Sprintf("%f", 3.14)` |
| %.2f | Float with precision | `fmt.Sprintf("%.2f", 3.14159)` |
| %s | String | `fmt.Sprintf("%s", "hello")` |
| %c | Character | `fmt.Sprintf("%c", 'A')` |
| %x | Hex | `fmt.Sprintf("%x", 255)` |
| %p | Pointer | `fmt.Sprintf("%p", &x)` |
| %t | Boolean | `fmt.Sprintf("%t", true)` |

---

# 22. Standard Library Overview

## fmt Package

```go
import "fmt"

// Print
fmt.Print("Hello")           // Print without newline
fmt.Println("Hello")         // Print with newline
fmt.Printf("Hello %s\n", "World")  // Print formatted

// Print types
fmt.Printf("%v\n", 42)       // 42
fmt.Printf("%v\n", 3.14)      // 3.14
fmt.Printf("%v\n", true)     // true
```

## os Package

```go
import "os"

// Environment variables
os.Getenv("PATH")
os.Setenv("KEY", "value")

// Command line arguments
os.Args  // []string

// Exit
os.Exit(1)

// Working directory
os.Getwd()
os.Chdir("/path")
```

## time Package

```go
import "time"

// Current time
now := time.Now()

// Specific time
t := time.Date(2024, 1, 15, 10, 30, 0, 0, time.UTC)

// Formatting
t.Format("2006-01-02 15:04:05")

// Parsing
t, _ := time.Parse("2006-01-02", "2024-01-15")

// Duration
time.Sleep(time.Second * 2)
time.Sleep(time.Millisecond * 500)

// Time operations
t.Add(time.Hour)
t.Sub(otherTime)
t.Before(otherTime)
t.After(otherTime)
```

## json Package

```go
import "encoding/json"

// Marshal (struct to JSON)
type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

p := Person{Name: "Alice", Age: 30}
data, _ := json.Marshal(p)      // {"name":"Alice","age":30}
data, _ := json.MarshalIndent(p, "", "  ")

// Unmarshal (JSON to struct)
var p2 Person
json.Unmarshal(data, &p2)

// Streaming
encoder := json.NewEncoder(w)
decoder := json.NewDecoder(r)
```

## io Package

```go
import "io"

// Common interfaces
type Reader interface {
    Read(p []byte) (n int, err error)
}

type Writer interface {
    Write(p []byte) (n int, err error)
}

type Closer interface {
    Close() error
}

// Utilities
io.Copy(writer, reader)
io.ReadAll(reader)
io.WriteString(writer, "text")
```

## filepath Package

```go
import "path/filepath"

filepath.Join("a", "b", "c")       // "a/b/c"
filepath.Dir("/path/to/file")      // "/path/to"
filepath.Base("/path/to/file")     // "file"
filepath.Ext("file.txt")           // ".txt"
filepath.Abs("relative/path")      // absolute path
filepath.IsAbs("/path/to/file")   // true
```

## log Package

```go
import "log"

// Simple logging
log.Println("Info log")
log.Printf("Value: %d", 42)

// Fatal (exits after logging)
log.Fatal("Fatal error")

// Panic (panics after logging)
log.Panic("Panic error")

// Custom logger
logger := log.New(os.Stderr, "PREFIX: ", log.LstdFlags)
logger.Println("Custom log")
```

## regexp Package

```go
import "regexp"

// Compile pattern
re := regexp.MustCompile(`\d+`)

// Match
re.MatchString("abc123def")  // true

// Find
re.FindString("abc123def")   // "123"
re.FindAllString("a1b2c3", -1)  // ["1", "2", "3"]

// Replace
re.ReplaceAllString("abc123def", "X")  // "abcXdef"

// Split
re.Split("a1b2c3", -1)  // ["a", "b", "c"]
```

---

# 23. Best Practices

## Code Organization

### Project Structure

```
myproject/
├── cmd/
│   └── app/
│       └── main.go
├── internal/
│   ├── handlers/
│   ├── models/
│   └── services/
├── pkg/
│   └── utils/
├── go.mod
└── go.sum
```

### Package Naming

- Use lowercase, short names
- Match directory name
- Use singular forms (`strings`, `errors`)
- No underscores or mixed case

## Error Handling

```go
// Good
if err != nil {
    return fmt.Errorf("operation failed: %w", err)
}

// Good - handle specific errors
if os.IsNotExist(err) {
    return ErrNotFound
}

// Bad
if err != nil {
    // ignore error
}
```

## Concurrency

```go
// Good - use mutex for shared state
varmu sync.Mutex
varm map[string]int

func update(key string, val int) {
    mu.Lock()
    defer mu.Unlock()
    m[key] = val
}

// Good - use channels for communication
ch := make(chan int)
go worker(ch)
```

## Performance Tips

1. **Use sync.Pool** for frequently allocated objects
2. **Prefer strconv over fmt** for string conversion
3. **Use bytes.Buffer** for string concatenation in loops
4. **Reuse slices and maps** when possible
5. **Avoid allocations in hot paths**

## Formatting

```bash
# Always format before committing
go fmt ./...

# Run vet for common issues
go vet ./...

# Format and vet
go fmt ./... && go vet ./...
```

## Documentation

```go
// Package math provides mathematical functions.
package math

// Add returns the sum of two integers.
//
// Example:
//
//	result := Add(2, 3)
//	// result is 5
func Add(a, b int) int {
    return a + b
}
```

---

# 24. Next Steps

## Practice Projects

1. **CLI Tool** - Command-line todo list
2. **Web Server** - REST API with net/http
3. **File Processor** - Batch file operations
4. **Concurrent Crawler** - Web crawler with goroutines
5. **Chat Server** - Real-time messaging with websockets

## Learning Path

```
1. Fundamentals ✓
2. Data Types and Control Flow ✓
3. Functions and Methods ✓
4. Collections (Arrays, Slices, Maps) ✓
5. Structs and Interfaces ✓
6. Error Handling ✓
7. Concurrency ✓
8. Testing ✓
9. Standard Library ✓

Next:
10. Building Web Applications
11. Database Operations
12. Working with APIs
13. Building CLI Tools
14. Microservices
15. Testing & Benchmarking
```

## Recommended Resources

- **Official Go Tour**: tour.golang.org
- **Effective Go**: golang.org/doc/effective_go
- **Go by Example**: gobyexample.com
- **Golang Wiki**: github.com/golang/go/wiki
- **Standard Library Docs**: pkg.go.dev

## Community

- **Golang Weekly**: golangweekly.com
- **r/golang**: reddit.com/r/golang
- **Gopher Slack**: gophers.slack.com
- **Go Forum**: forum.golang.org

---

# Quick Reference Card

## Basic Syntax

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

## Variables

```go
var x int = 10
y := 20  // Short declaration
const PI = 3.14
```

## Control Flow

```go
if x > 0 {
    // code
} else {
    // code
}

for i := 0; i < 10; i++ {
    // code
}
```

## Functions

```go
func add(a, b int) int {
    return a + b
}
```

## Collections

```go
// Array
arr := [3]int{1, 2, 3}

// Slice
slice := []int{1, 2, 3}
slice = append(slice, 4)

// Map
m := map[string]int{"a": 1, "b": 2}
```

## Goroutines and Channels

```go
go func() {
    ch <- 42
}()

value := <-ch

select {
case msg := <-ch1:
    fmt.Println(msg)
case <-time.After(time.Second):
    fmt.Println("Timeout")
}
```

## Error Handling

```go
result, err := doSomething()
if err != nil {
    return fmt.Errorf("failed: %w", err)
}
```

---

*Congratulations! You have completed the complete Go programming tutorial from Zero to Hero!*

*Remember: The best way to learn Go is by writing code. Start with small projects and gradually tackle more complex applications.*

**Happy Coding!** 🚀
