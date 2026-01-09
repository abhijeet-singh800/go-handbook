> [!NOTE]
> This is not meant to be a crash course for a person who is starting fresh with the language , its a handbook for someone who is already familiar with the language and need a quick , concise and comprehensive reference document.

> [!NOTE]
> Don't forget to add a star to this repo to visit it later.

# Table of Content
- [Table of Content](#table-of-content)
	- [Introduction](#introduction)
- [Project Architecture](#project-architecture)
	- [Modules and Packages](#modules-and-packages)
	- [Initialisation](#initialisation)
	- [Module Structure](#module-structure)
- [Public / Private Objects](#public--private-objects)
- [Hello World](#hello-world)
	- [Print Functions](#print-functions)
- [Constants and Variables](#constants-and-variables)
- [Data Types](#data-types)
	- [Boolean Types](#boolean-types)
	- [Float Types](#float-types)
	- [Integer Types](#integer-types)
	- [Byte Type](#byte-type)
	- [Complex Types](#complex-types)
	- [String and Rune Data Types](#string-and-rune-data-types)
- [Operators](#operators)
		- [Arithmetic](#arithmetic)
		- [Comparison](#comparison)
		- [Logical](#logical)
		- [Other](#other)
- [Type Conversions](#type-conversions)
- [Strings and Runes](#strings-and-runes)
	- [Length Problem](#length-problem)
- [String / Integer Conversion](#string--integer-conversion)
		- [String to Integer (`strconv.Atoi`)](#string-to-integer-strconvatoi)
		- [Integer to String (`strconv.Itoa`)](#integer-to-string-strconvitoa)
		- [Common Mistake](#common-mistake)
- [Iota](#iota)
		- [Basic Example (0, 1, 2...)](#basic-example-0-1-2)
		- [Starting from 1 (Math)](#starting-from-1-math)
		- [Skipping Values](#skipping-values)
		- [Advanced: Bitmasking (Powers of 2)](#advanced-bitmasking-powers-of-2)
		- [The Reset Rule](#the-reset-rule)
- [New Keyword](#new-keyword)
		- [`new(T)` vs `&T{}`](#newt-vs-t)
- [Functions](#functions)
	- [Functions As Values And Closures](#functions-as-values-and-closures)
	- [Variadic Functions](#variadic-functions)
- [Error](#error)
- [Blank Identifier](#blank-identifier)
		- [Why use it?](#why-use-it)
- [Defer Keyword](#defer-keyword)
		- [Key Rules](#key-rules)
	- [Benchmark a Function](#benchmark-a-function)
	- [Recovering from Panics](#recovering-from-panics)
		- [3 Rules of Recovery](#3-rules-of-recovery)
- [Conditionals](#conditionals)
	- [If Else](#if-else)
	- [Switch](#switch)
- [Loops](#loops)
	- [Loop Labels](#loop-labels)
		- [Real World Example](#real-world-example)
		- [Analysis](#analysis)
- [GoTo Labels](#goto-labels)
- [`init()` Functions](#init-functions)
		- [Key Rules](#key-rules-1)
- [Arrays and Slices](#arrays-and-slices)
		- [Slices](#slices)
		- [Operations on Arrays and Slices](#operations-on-arrays-and-slices)
- [Maps](#maps)
- [Structs](#structs)
	- [Anonymous structs](#anonymous-structs)
- [Interfaces](#interfaces)
- [Embedding](#embedding)
		- [Struct Embedding](#struct-embedding)
		- [Interface Embedding](#interface-embedding)
- [Empty Interface](#empty-interface)
			- [Example 1: The Chameleon Variable](#example-1-the-chameleon-variable)
			- [Example 2: Accepting Any Argument](#example-2-accepting-any-argument)
			- [The "Catch" (Important)](#the-catch-important)
- [Any Type](#any-type)
		- [Example 1: The "Any" Variable](#example-1-the-any-variable)
		- [Example 2: Mixed Lists (Slices)](#example-2-mixed-lists-slices)
		- [Example 3: Generics (Constraint)](#example-3-generics-constraint)
- [Type Assertion](#type-assertion)
- [Type Switch](#type-switch)
	- [Basic Check](#basic-check)
	- [Value Extraction](#value-extraction)
- [Type Alias](#type-alias)
	- [Basic](#basic)
	- [Interface Types](#interface-types)
	- [Ordered Constrains Package](#ordered-constrains-package)
- [JSON](#json)
	- [Marshalling](#marshalling)
	- [Unmarshaling](#unmarshaling)
		- [Strict Unmarshaling](#strict-unmarshaling)
	- [Unknown Types](#unknown-types)
		- [Critical Pitfall: The `float64` Rule](#critical-pitfall-the-float64-rule)
- [Pointers](#pointers)
	- [Pass be Reference in Go](#pass-be-reference-in-go)
		- [Structs](#structs-1)
		- [Arrays (Fixed Size)](#arrays-fixed-size)
		- [Basic Types (Int, String, Bool)](#basic-types-int-string-bool)
		- [The Exception: Maps and Slices ("Reference Types")](#the-exception-maps-and-slices-reference-types)
		- [Shallow Copy](#shallow-copy)
	- [Summary Table](#summary-table)
- [Concurrency](#concurrency)
	- [WaitGroups](#waitgroups)
		- [How it works (The 3 Rules)](#how-it-works-the-3-rules)
		- [Code Example](#code-example)
		- [Common Pitfall](#common-pitfall)
	- [Channels](#channels)
		- [Unbuffered Channel](#unbuffered-channel)
		- [Buffered Channel](#buffered-channel)
		- [Read Only Channels Functions](#read-only-channels-functions)
		- [Write Only Channels Functions](#write-only-channels-functions)
		- [Select Channels](#select-channels)
		- [Default - Select Statement](#default---select-statement)
	- [Mutex](#mutex)
			- [Best Practice: `defer`](#best-practice-defer)
		- [Read Mutex](#read-mutex)
- [Generics](#generics)
	- [Interface Type Alias Generics](#interface-type-alias-generics)


## Introduction

* Imperative language
* Designed to be simple in architecture
* Statically typed
* Syntax tokens similar to C (but less parentheses and no semicolons) and the structure to Oberon-2
* Compiles to native code (no JVM)
* No classes, but structs with methods
* Interfaces
* No implementation inheritance. There's [type embedding](http://golang.org/doc/effective%5Fgo.html#embedding), though.
* Functions are first class citizens
* Functions can return multiple values
* Has closures
* Pointers, but not pointer arithmetic
* Built-in concurrency primitives: Goroutines and Channels

# Project Architecture

[[GO Programming#Packages|Go Programming - Packages - Cerebrum]]
## Modules and Packages

| **Feature**    | **Go Packages**                                                  | **Go Modules**                                                               |
| -------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Definition** | Single directory containing one or more Go source files (`.go`). | Collection of Go packages that are versioned together as a Project.          |
| **Purpose**    | Organize and structure code. Acts as a "library" or namespace.   | Manage dependencies and versions for your entire project.                    |
| **Scope**      | A single directory.                                              | An entire project or repository, which can contain many packages.            |
| **Key File**   | No specific file; defined by its directory path.                 | `go.mod` (defines the module and its dependencies) and `go.sum` (checksums). |

## Initialisation 
In a new empty folder run the following command to start a new module (project)

```bash
go mod init github.com/your-username/my-project
```

this will create a `go.mod` file (manifest file for your project), here is the format of the file.

```go
// Defines the path for this module
module github.com/your-username/my-project

// Specifies the Go version it was written for
go 1.21

// Lists all direct dependencies and their versions
require (
    github.com/gin-gonic/gin v1.9.1
    github.com/google/uuid v1.6.0
)
```

## Module Structure
Lets see how you can structure your code so you can use it inside your module
Project Structure
```
myproject/ 
├── go.mod 
├── main.go 
├── mathutil/ 
│ └── mathutil.go 
└── greeting/ 
  └── greeting.go
```

`go.mod`
```go
module github.com/your-username/myproject

go 1.21
```

`mathutil/mathutil.go` (Sub-package 1)
```go
package mathutil

// Add returns the sum of two integers.
func Add(a, b int) int {
    return a + b
}
```

`greeting/greeting.go` (Sub-package 2)
```go
package greeting

import (
    "fmt"
    // Import path is based on the module name from go.mod
    "github.com/your-username/myproject/mathutil"
)

// Hello returns a greeting with a calculated number.
func Hello(name string) string {
    // Using a function from the mathutil package
    num := mathutil.Add(5, 2)
    return fmt.Sprintf("Hello, %s! Your lucky number is %d.", name, num)
}
```

`main.go` (The Main Package)
```go
package main

import (
    "fmt"
    // Import path for the greeting package
    "github.com/your-username/myproject/greeting"
)

func main() {
    // Using a function from the greeting package
    message := greeting.Hello("Go Developer")
    fmt.Println(message)
}
```


# Public / Private Objects
- Public - Can be used outside the Package (Start with Capital Letters)
- Private - Cant be used outside the Package (Starts with Small Letters)
```go 
type Car struct{     // Public Struct
	Modlel string    // Public Field
	engine engine	 // Private Field
}

type engine struct{                  // Private Struct
	caparity int                     // Private Field
	Engine_manifacturer string       // Public Field
}

func PrintHello() {           // Public Function
	fmt.printf("Hello")
}

func hello() {                // Private Function
	fmt.printf("Not Public")
}

type Vehicle interface {       // Public Interface
	Drive()                    // Public Method
}

type engineFunctions interface{// Private Interface
	start()                    // Private Method
} 

name := "Abhijeet Singh"    // Private Variable
Pi := 3.14                  // Public Variable
```


# Hello World
`hello.go`
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello Go")
}
```

Command to run it : `go run hello.go`

## Print Functions
`fmt.Print()` - No new line at the end
```go
fmt.Print(" Next part.")
```

`fmt.Println()` - Adds a new line at the end
```go
fmt.Println("This is a new line.")
```

`fmt.Printf()` - Formatted Print statements , no new line at the end 
- `%s` - For Strings 
- `%d` - For Integers 
- `%v` - General Variable

```go
name := "Alex"
age := 30

fmt.Printf("My name is %s and I am %d years old.\n", name, age)
    
fmt.Printf("User: %v, Age: %v\n", name, age)
```

# Constants and Variables 

Declaration without Initialisation
```go
var foo int
```

Declaration with Initialisation
```go
var foo int = 42 
```

Declaration of Multiple Variables at once
```go
var foo, bar int = 42, 1302
```

Type Omitted thus will be inferred
```go
var foo = 42 
```

Short Declaration with inferred type
```go
foo := 42 // shorthand, only in func bodies, omit var keyword, type is always implicit
```

Try to avoid inferred type while creating variables returning form functions , as its isn't obvious what the type of returned variables it
```go
foo := hello() // avoit it , as the type isn't obvious
var foo int = hello() // you know the returning type just by reading
```

Constant Declaration
```go
const constant = "This is a constant" //Type Inferred 
```

# Data Types 

## Boolean Types 

| Data Type | Range             |     |
| --------- | ----------------- | --- |
| `bool`    | `true` or `false` |     |

## Float Types 
| `float32`                                                   | `float64`                                                          |
| ----------------------------------------------------------- | ------------------------------------------------------------------ |
| 32 bits (4 bytes)                                           | 64 bits (8 bytes)                                                  |
| $\pm 1.18 \times 10^{-38}$ to $\pm 3.4 \times 10^{38}$      | $\pm 2.23 \times 10^{-308}$ to $\pm 1.80 \times 10^{308}$          |
| ~6-9 decimal digits                                         | ~15-17 decimal digits                                              |
| Graphics, machine learning (when speed/memory are critical) | General-purpose math, scientific computing (default for most uses) |

## Integer Types
|**Type**|**Size**|**Range (Exact)**|
|---|---|---|
|**`int8`**|8 bits (1 byte)|-128 to 127|
|**`int16`**|16 bits (2 bytes)|-32,768 to 32,767|
|**`int32`**|32 bits (4 bytes)|-2,147,483,648 to 2,147,483,647|
|**`int64`**|64 bits (8 bytes)|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|
|**`int`**|**Platform-dependent**|Same as `int32` (on 32-bit systems) or `int64` (on 64-bit systems)|

|**Type**|**Size**|**Range (Exact)**|
|---|---|---|
|**`uint8`**|8 bits (1 byte)|0 to 255|
|**`uint16`**|16 bits (2 bytes)|0 to 65,535|
|**`uint32`**|32 bits (4 bytes)|0 to 4,294,967,295|
|**`uint64`**|64 bits (8 bytes)|0 to 18,446,744,073,709,551,615|
|**`uint`**|**Platform-dependent**|Same as `uint32` (on 32-bit systems) or `uint64` (on 64-bit systems)|

Choosing a data type depends on the type of the data you are working with, For Example lets say you are trying to store RGB values inside a variable , in this case `uint8` is sufficient because you are not going to exceed that range.

## Byte Type 

| **Feature**         | **Description**                                                                |
| ------------------- | ------------------------------------------------------------------------------ |
| **Declaration**     | `byte`                                                                         |
| **Underlying Type** | `uint8` (unsigned 8-bit integer).                                              |
| **Size**            | 8 bits (1 byte).                                                               |
| **Range**           | 0 to 255.                                                                      |
| **Common Use**      | Represents raw data, binary files, image data, or individual ASCII characters. |

## Complex Types
| **Type**         | **Total Size**      | **Component Type**                 | **Component Range (approx.)**                             |
| ---------------- | ------------------- | ---------------------------------- | --------------------------------------------------------- |
| **`complex64`**  | 64 bits (8 bytes)   | `float32` (for real and imaginary) | $\pm 1.18 \times 10^{-38}$ to $\pm 3.4 \times 10^{38}$    |
| **`complex128`** | 128 bits (16 bytes) | `float64` (for real and imaginary) | $\pm 2.23 \times 10^{-308}$ to $\pm 1.80 \times 10^{308}$ |


## String and Rune Data Types
| **Feature**    | `string`                           | `rune`                                     |
| -------------- | ---------------------------------- | ------------------------------------------ |
| **Definition** | A read-only slice of bytes.        | An alias for the `int32` type.             |
| **Represents** | Text, encoded in UTF-8.            | A single character or Unicode code point.  |
| **Literal**    | `"Hello"` (double quotes)          | `'a'` (single quotes)                      |
| **Zero Value** | `""` (empty string)                | `0` (the null character)                   |
| **Mutability** | **Immutable** (cannot be changed). | Just an integer; its value can be changed. |
For more information on Strings [[#Strings|click here]].
For more information on Runes [[#Rune|click here]].

# Operators 
### Arithmetic
|Operator|Description|
|--------|-----------|
|`+`|addition|
|`-`|subtraction|
|`*`|multiplication|
|`/`|quotient|
|`%`|remainder|
|`&`|bitwise and|
|`\|`|bitwise or|
|`^`|bitwise xor|
|`&^`|bit clear (and not)|
|`<<`|left shift|
|`>>`|right shift|

### Comparison
|Operator|Description|
|--------|-----------|
|`==`|equal|
|`!=`|not equal|
|`<`|less than|
|`<=`|less than or equal|
|`>`|greater than|
|`>=`|greater than or equal|

### Logical
| Operator | Description |
| -------- | ----------- |
| `&&`     | logical and |
| `\|\|`   | logical or  |
| `!`      | logical not |
 
### Other
|Operator|Description|
|--------|-----------|
|`&`|address of / create pointer|
|`*`|dereference pointer|
|`<-`|send / receive operator (see 'Channels' below)|



# Type Conversions
Languages like Java have a concept of implicit type conversion, where Java does automatically convert the type of a variable such that no data is lost.
Go does not have implicit type conversion (as Go is a strongly typed language) and you cant operate on two different types so you need to convert them into same types.

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

// alternative syntax
i := 42
f := float64(i)
u := uint(f)
```

If you are working with important data , make sure that you don't type convert into a data type with lower storage then the original data type .


# Strings and Runes
```go
var name 
string = "jack" //declaration and init
anotherName := "john" //implied type

// doublequotes for single line strings 
singleLineString := "this is a single line string"

// backquotes for multi line string
multiLineString :=`This is a line 1 and
this is line 2 of a multi line string.
`
```

```go
var rune char = 'a'  // Runes are created using single quotes
char1 := 'a'  // Inferred types
```

```go
var myString = "résumé"  // Strings are stores as UTF8 bytes
// UTF8 contains variable length characters
var indexed = myString[1]
fmt.Printf("%v, %T\n", indexed, indexed)

for i, v := range myString{
fmt.Println(i, v)
/*
Will Return -
114, uint8   // Returned 1st part of the UTF8 encoding rather then 233
		     // Strings are arrays of unit8 underneath

0 114        // Skips 2 index as é contains 2 bytes
1 233        // Returns 233 (full UTF8 encoding for é) because of     3 115           range keyword in the loop
4 117
5 109
6 233

String Stoed in Memory
   r          é                   s          u        m   
[01110010, 11000011, 10101001, 01110011, 01110161, 01101101, 
   é
11000011, 16101601]
*/
```

While dealing with strings its easier to cast them into arrays of strings rather than dealing with the underlying byte arrays you can do that by 
```go
myString := []rune("résumé")
var indexed = myString[1]
fmt.Printf("%v, %T\n", indexed, indexed)

for i, v := range myString{
fmt.Println(i, v)

/*
Will Return -
114, int32  // Returns the full UTF8 encoding this time 
			// Runes are underneath
0 114        // Does not skip an index this time
1 233        
2 115           
3 117
4 109
5 233
*/
```

## Length Problem 
Go uses the `UTF-8` encoding , thus the length of string returned by the `len` function is not the actual length of the string , as `len` returns the bits of memory occupied by the string and if you are using some funky characters in your string like `ø` which contains more then one bit in the memory then the length returned might not what you expect. Thus in this case you can use the following method to count the characters in your sting 

```go
import "unicode/utf8"

length := utf8.RuneCountInString("øÂæÆ") //will return 4
```

# String / Integer Conversion
### String to Integer (`strconv.Atoi`)
```go
func main() {
	strVal := "100"

	// 1. Convert
	// Returns: int, error
	num, err := strconv.Atoi(strVal)
	
	if err != nil {
		fmt.Println("Conversion failed:", err)
	} else {
		fmt.Printf("Type: %T, Value: %d\n", num, num) // Type: int, Value: 100
	}
}
```

### Integer to String (`strconv.Itoa`)
```go
func main() {
	numVal := 42

	// 1. Convert
	strVal := strconv.Itoa(numVal)

	fmt.Printf("Type: %T, Value: %q\n", strVal, strVal) // Type: string, Value: "42"
}
```

### Common Mistake
```go
val := 65
wrong := string(val) // This returns "A", NOT "65" 
// Returns the UTF-8 character for value 65

right := strconv.Itoa(val) // This returns "65"
```

# Iota
It is used to Enumerate (Define) multiple variable using int values (0,1,2.....)
### Basic Example (0, 1, 2...)
```go
const (
	// iota starts at 0
	Red = iota 
	
	// Implicitly repeats "iota", so this is 1
	Blue 
	
	// This is 2
	Green 
)

func main() {
	fmt.Println(Red, Blue, Green) // Output: 0 1 2
}
```

### Starting from 1 (Math)
If you don't want to start at 0, you can do math on the first line.
```go
const (
	// iota is 0, so: 0 + 1 = 1
	Monday = iota + 1 
	
	// Implicitly: iota + 1 -> 1 + 1 = 2
	Tuesday 
	
	// Implicitly: iota + 1 -> 2 + 1 = 3
	Wednesday 
)
```
### Skipping Values
Use the **Blank Identifier (`_`)** to throw away an index.
```go
const (
	Small = iota // 0
	_            // 1 (Skipped/Wasted)
	Large        // 2
)
```
### Advanced: Bitmasking (Powers of 2)
This is the most powerful use of `iota`. It is used to create flags (permissions, settings) using the bit-shift operator (`<<`).
```go
const (
	// 1 shifted left 0 times (binary 001) = 1
	Read = 1 << iota 
	
	// 1 shifted left 1 time  (binary 010) = 2
	Write 
	
	// 1 shifted left 2 times (binary 100) = 4
	Execute 
)

// Why? So you can combine them:
// 1 + 2 = 3 (Read AND Write permissions)
```

### The Reset Rule
`iota` is scoped to the `const` block. As soon as you start a **new** `const (...)` block, `iota` resets back to **0**.

```go
const (
	A = iota // 0
	B = iota // 1
)

const (
	C = iota // Resets to 0!
)
```


# New Keyword
In Go, **`new(Type)`** does three things:
1. Allocates memory for that Type.
2. Sets the value to "Zero" (0, "", false, nil).
3. Returns a **Pointer** (`*Type`) to that memory.

```go
type User struct {
	Name string
	Age  int
}

func main() {
	// 1. Use new()
	// This allocates memory and returns a pointer (*User)
	u := new(User) 

	// 2. Check the Type
	fmt.Printf("Type: %T \n", u) // Output: *main.User

	// 3. Check the Value (It is zeroed out)
	fmt.Printf("Value: %+v \n", u) // Output: &{Name: Age:0}

	// 4. Set fields (Go automatically handles the pointer)
	u.Name = "Alice"
	fmt.Println("Name:", u.Name)
}
```

### `new(T)` vs `&T{}`

You will rarely see `new` in actual Go code. Most developers prefer using the **Address Of (`&`)** operator because it lets you initialize values immediately.

```go
// Option A: Using new (Verbose)
u := new(User)
u.Name = "Bob"

// Option B: Using literal (Preferred)
// This does the exact same thing: creates a pointer to a User.
u := &User{Name: "Bob"}
```

**Key Takeaway:** `new` returns a **Pointer**, not the value itself.

# Functions 
Go uses pass-by-value for all function arguments. This means that when you pass a variable to a function, a copy of that variable's value is made and passed to the function. Any modifications made to the parameter within the function will only affect this local copy and not the original variable in the caller's scope.

If you need to change the original values you can use Pointers with the functions.

```go
// a simple function
func functionName() {}

// function with parameters (again, types go after identifiers)
func functionName(param1 string, param2 int) {}

// multiple parameters of the same type
func functionName(param1, param2 int) {}

// return type declaration
func functionName() int {
    return 42
}

// Can return multiple values at once
func returnMulti() (int, string) {
    return 42, "foobar"
}
var x, str = returnMulti()

// Return multiple named results simply by return
func returnMulti2() (n int, s string) {
    n = 42
    s = "foobar"
    // n and s will be returned
    return
}
var x, str = returnMulti2()

```

## Functions As Values And Closures
```go
func main() {
    // assign a function to a name
    add := func(a, b int) int {
        return a + b
    }
    // use the name to call the function
    fmt.Println(add(3, 4))
}

// Closures, lexically scoped: Functions can access values that were
// in scope when defining the function
func scope() func() int{
    outer_var := 2
    foo := func() int { return outer_var}
    return foo
}

func another_scope() func() int{
    // won't compile because outer_var and foo not defined in this scope
    outer_var = 444
    return foo
}


// Closures
func outer() (func() int, int) {
    outer_var := 2
    inner := func() int {
        outer_var += 99 // outer_var from outer scope is mutated.
        return outer_var
    }
    inner()
    return inner, outer_var // return inner func and mutated outer_var 101
}
```

## Variadic Functions
```go
func main() {
	fmt.Println(adder(1, 2, 3)) 	// 6
	fmt.Println(adder(9, 9))	// 18

	nums := []int{10, 20, 30}
	fmt.Println(adder(nums...))	// 60
}

// By using ... before the type name of the last parameter you can indicate that it takes zero or more of those parameters.
// The function is invoked like any other function except we can pass as many arguments as we want.
func adder(args ...int) int {
	total := 0
	for _, v := range args { // Iterates over the arguments whatever the number.
		total += v
	}
	return total
}
```


# Error
There is no exception handling. Instead, functions that might produce an error just declare an additional return value of type [`error`](https://golang.org/pkg/builtin/#error). This is the `error` interface:

```go
// creating errors
import "errors"

err = errors.New("Error Message") // Returns a New error with message "Error Message"
```


```go
// The error built-in interface type is the conventional interface for representing an error condition,
// with the nil value representing no error.
type error interface {
    Error() string
}
```

Here's an example:
```go
func sqrt(x float64) (float64, error) {
	if x < 0 {
		return 0, errors.New("negative value")
	}
	return math.Sqrt(x), nil
}

func main() {
	val, err := sqrt(-1)
	if err != nil {
		// handle error
		fmt.Println(err) // negative value
		return
	}
	// All is good, use `val`.
	fmt.Println(val)
}
```

# Blank Identifier
The underscore (_) is known as the Blank Identifier.
It acts as a "black hole" for values. You use it when a function returns a value you do not need, because Go forbids unused variables.

```go
package main

import (
	"fmt"
	"strconv"
)

// A function that returns TWO values
func getCoordinates() (int, int) {
	return 100, 200
}

func main() {
	// 1. Ignoring a return value
	// We only want 'x'. We don't care about 'y', so we use '_'
	x, _ := getCoordinates()
	fmt.Println("X:", x)

	// 2. Ignoring an error (Risky but common in quick scripts)
	// strconv.Atoi returns (int, error). We throw away the error.
	num, _ := strconv.Atoi("50")
	fmt.Println("Number:", num)
	
	// 3. Ignoring the Index in a Loop
	// range returns (index, value). We only want the value.
	items := []string{"A", "B"}
	for _, item := range items {
		fmt.Println("Item:", item)
	}
}
```

### Why use it?

If you tried to write `x, y := getCoordinates()` but never used `y`, the Go compiler would throw an error: **"y declared but not used."** The underscore tells the compiler: _"I know this value exists, but I am intentionally ignoring it."

# Defer Keyword
The `defer` keyword schedules a function call to be run **automatically** when the surrounding function finishes (returns).

```go
func readFile(filename string) {
	fmt.Println("1. Opening file...")
	file, err := os.Open(filename)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}

	// SCHEDULE THE CLOSE IMMEDIATELY
	// This line will not run now. It will run at the very end.
	defer file.Close()

	fmt.Println("2. Reading file contents...")
	// ... Imagine complex logic here ...
	
	fmt.Println("3. Function is finishing.")
	
	// 'defer file.Close()' runs right here, automatically.
}
```

### Key Rules

1. **LIFO (Last-In, First-Out):** If you use multiple `defer` statements, they run in reverse order (like a stack of plates).
    - `defer A()`
    - `defer B()`
    - **Result at end:** Runs `B()` then `A()`.
2. **Evaluation:** The arguments to the deferred function are evaluated **when `defer` is executed**, not when the call actually runs.

## Benchmark a Function 
```go
// 1. The Helper Function
// This calculates how long passed since 'start'
func timeTrack(start time.Time, name string) {
	elapsed := time.Since(start)
	fmt.Printf("%s took %s\n", name, elapsed)
}

// 2. The Function we want to benchmark
func bigTask() {
	// A. 'time.Now()' runs NOW (at the start).
	// B. 'timeTrack' is scheduled to run at the END.
	defer timeTrack(time.Now(), "Big Task")

	fmt.Println("Working...")
	time.Sleep(2 * time.Second) // Simulate 2 seconds of work
}

func main() {
	bigTask()
}
```

Defer with Anonymous Functions 
```go
func fastTask() {
	start := time.Now()
	defer func() {
		fmt.Println("Fast Task took:", time.Since(start))
	}()
	time.Sleep(100 * time.Millisecond)
}
```

## Recovering from Panics
Think of it like an **Airbag**:
1. **`defer`**: You install the airbag before you start driving (at the top of the function).
2. **`panic`**: The crash happens.
3. **`recover`**: The airbag deploys, saving the program from "death" (exiting).1

```go
func riskyFunction() {
    // 1. Install the Safety Net (MUST be a deferred function)
    defer func() {
        // 2. Check if a panic occurred
        if r := recover(); r != nil {
            fmt.Println("Recovered from crash:", r)
        }
    }()

    fmt.Println("Start risky business...")

    // 3. Trigger a Crash
    // This stops execution HERE and jumps to the deferred function.
    panic("Something went wrong!")

    fmt.Println("This line is never reached.")
}

func main() {
    fmt.Println("App Started")
    
    riskyFunction()
    
    fmt.Println("App Continued Running! (Saved from crash)")
}
```
Output
```
App Started
Start risky business...
Recovered from crash: Something went wrong!
App Continued Running! (Saved from crash)
```

### 3 Rules of Recovery
1. **Defer First:** You must define the `defer` **before** the panic happens (usually at the very top of the function).
2. **Anonymous Function:** `recover()` only works when called **inside** the deferred function directly.
3. **Scope:** `recover` only catches panics happening in the **same goroutine**. It cannot catch a panic happening in a different goroutine spawned by `go func()`.


# Conditionals 
## If Else 
```go
func main() {
	// Basic one
	if x > 10 {
		return x
	} else if x == 10 {
		return 10
	} else {
		return -x
	}

	// You can put one statement before the condition
	if a := b + c; a < 42 {
		return a
	} else {
		return a - 42
	}

	// Type assertion inside if
	var val interface{} = "foo"
	if str, ok := val.(string); ok {
		fmt.Println(str)
	}
}
```

## Switch 
```go
    // switch statement
    switch operatingSystem {
    case "darwin":
        fmt.Println("Mac OS Hipster")
        // cases break automatically, no fallthrough by default
    case "linux":
        fmt.Println("Linux Geek")
    default:
        // Windows, BSD, ...
        fmt.Println("Other")
    }

    // as with for and if, you can have an assignment statement before the switch value
    switch os := runtime.GOOS; os {
    case "darwin": ...
    }

    // you can also make comparisons in switch cases
    number := 63
    name := "jack"
    age := 13
    switch {
        case number < 42:
            fmt.Println("Smaller than 42")
        case name == "jack":
            fmt.Println("Name is Jack")
        case age != 0 :
            fmt.Println("He is not a new born")
    }
    // The above switch will just execute the first stament as the 
    // break is impretive in go lang

    // cases can be presented in comma-separated lists
    var char byte = '?'
    switch char {
        case ' ', '?', '&', '=', '#', '+', '%':
            fmt.Println("Should escape")
    }
```

Switch Fallthrough
```go
func main() {
	num := 100

	switch num {
	case 100:
		fmt.Println("1. Found 100")
		// Without this, the code would stop here.
		fallthrough 

	case 200:
		// This runs AUTOMATICALLY, even though num is not 200.
		fmt.Println("2. Also ran this case!")
		
	case 300:
		// No fallthrough above, so this stops.
		fmt.Println("3. This will NOT run")
	}
}
```


# Loops
```go
    // There's only `for`, no `while`, no `until`
    for i := 1; i < 10; i++ {
    }
    for ; i < 10;  { // while - loop
    }
    for i < 10  { // you can omit semicolons if there is only a condition
    }
    for { // you can omit the condition ~ while (true)
    }
    
```

## Loop Labels
```go
// use break/continue on current loop
// use break/continue with label on outer loop
// Lables can be name anything - in this case its here and there
here:
    for i := 0; i < 2; i++ {
        for j := i + 1; j < 3; j++ {
            if i == 0 {
                continue here
            }
            fmt.Println(j)
            if j == 2 {
                break
            }
        }
    }

there:
    for i := 0; i < 2; i++ {
        for j := i + 1; j < 3; j++ {
            if j == 1 {
                continue
            }
            fmt.Println(j)
            if j == 2 {
                break there
            }
        }
    }
```

### Real World Example
```go
func main() {
	// 1. Define the Label
OuterLoop:
	for i := 1; i <= 3; i++ {
		fmt.Printf("Row %d: ", i)

		for j := 1; j <= 3; j++ {
			
			// CASE A: Labeled Continue
			// Skip the rest of Row 2 entirely, jump to Row 3
			if i == 2 {
				fmt.Println(" (Skipping rest of row)")
				continue OuterLoop
			}

			// CASE B: Labeled Break
			// Stop EVERYTHING when we hit i=3, j=2
			if i == 3 && j == 2 {
				fmt.Println(" (Found target! Stopping everything)")
				break OuterLoop
			}

			fmt.Printf("%d ", j)
		}
		fmt.Println()
	}
	
	fmt.Println("Done.")
}
```

```
Row 1: 1 2 3 
Row 2:  (Skipping rest of row)
Row 3: 1  (Found target! Stopping everything)
Done.
```

### Analysis
1. **`continue OuterLoop`**: When `i==2`, it didn't just skip `j=1`; it abandoned the inner loop entirely and forced the **Outer Loop** to increment to 3.
2. **`break OuterLoop`**: When `i==3, j==2`, it didn't just stop the inner loop (which would normally let the outer loop finish); it killed the **Outer Loop** immediately.


# GoTo Labels
Stop the execution and jumps to specified labels
```go
func main() {
	age := 15

	if age < 18 {
		// Jump straight to the "Error" label
		goto Error
	}

	fmt.Println("Welcome to the club!")
	return // Stop here so we don't accidentally run the error code below

Error: // The Label definition
	fmt.Println("Access Denied: You are too young.")
}
```

# `init()` Functions
This function run automatically before `main()`
```go
var databaseStatus string

// This runs FIRST (Automatically)
func init() {
	fmt.Println("1. Init function is running...")
	databaseStatus = "Connected"
}

// This runs SECOND
func main() {
	fmt.Println("2. Main function is running...")
	
	// The variable is already set!
	fmt.Println("Database Status:", databaseStatus)
}
```

```
1. Init function is running...
2. Main function is running...
Database Status: Connected
```

### Key Rules
1. **No Arguments/Returns:** `init` takes no parameters and returns nothing.
2. **Multiple Inits:** You can have multiple `init` functions in one package (or even one file). They execute in the order they appear.
3. **Order of Execution:**
    1. Global Variables are initialized.
    2. `init()` functions run.
    3. `main()` runs.

# Arrays and Slices
```go
// Arrays are stroed in continious memory locations
var a [10]int // declare an int array with length 10. Array length is part of the type!
a[3] = 42     // set elements
i := a[3]     // read elements

// declare and initialize
var a = [2]int{1, 2}
a := [2]int{1, 2} //shorthand
a := [...]int{1, 2} // elipsis -> Compiler figures out array length
```

### Slices

```go
var a []int                              // declare a slice - similar to an array, but length is unspecified
var a = []int {1, 2, 3, 4}               // declare and initialize a slice (backed by the array given implicitly)
a := []int{1, 2, 3, 4}                   // shorthand
chars := []string{0:"a", 2:"c", 1: "b"}  // ["a", "b", "c"]

var b = a[lo:hi]	// creates a slice (view of the array) from index lo to hi-1
var b = a[1:4]		// slice from index 1 to 3
var b = a[:3]		// missing low index implies 0
var b = a[3:]		// missing high index implies len(a)
a =  append(a,17,3)	// append items to slice a
c := append(a,b...)	// concatenate slices a and b

// create a slice with make
a = make([]byte, 5, 5)	// type of the elements, second length of the slice , last is the capacity of the array in the memory
a = make([]byte, 5)	// capacity is optional, if not provided then defaults to same as length

// create a slice from an array
x := [3]string{"Лайка", "Белка", "Стрелка"}
s := x[:] // a slice referencing the storage of x
// x[:] - creates a slice containing all the elements of the array x
// s does not contain a copy of the data. It creates a "Slice Header" (a tiny data structure) that points to the memory of x
// creating s is very fast because no data is copied—only pointers
// if you change a value in slice s (e.g., s[1] = "Rex"), the original array x will also change
```

### Operations on Arrays and Slices
`len(a)` gives you the length of an array/a slice. It's a built-in function, not a attribute/method on the array.

```go
// loop over an array/a slice
for i, e := range a {
    // i is the index, e the element
}

// if you only need e:
for _, e := range a {
    // e is the element
}

// ...and if you only need the index
for i := range a {
}

// In Go pre-1.4, you'll get a compiler error if you're not using i and e.
// Go 1.4 introduced a variable-free form, so that you can do this
for range time.Tick(time.Second) {
    // do it once a sec
}
// Memory Leak Risk Warning : this loop cant be stopped
```

# Maps

```go
m := make(map[string]int)
m["key"] = 42
fmt.Println(m["key"])

delete(m, "key")

elem, ok := m["key"] // test if key "key" is present and retrieve it, if so

// map literal
var m = map[string]Vertex{
    "Bell Labs": {40.68433, -74.39967},
    "Google":    {37.42202, -122.08408},
}

// iterate over map content
for key, value := range m {
}

```

# Structs 
For more watch [This is your last video about Golang Structs!](https://www.youtube.com/watch?v=c8H0w4yBL10)

There are no classes, only structs. Structs can have methods.

```go
// A struct is a type. It's also a collection of fields

// Declaration
type Vertex struct {
    X, Y float64
}

// Creating
var v = Vertex{1, 2}
var v = Vertex{X: 1, Y: 2} // Creates a struct by defining values with keys
var v = []Vertex{{1,2},{5,2},{5,5}} // Initialize a slice of structs

// Accessing members
v.X = 4

type car struct {
	model string
	year int
	ownerInfo owner   // Fields can also be other structs
}

type owner struct {
	name string
}

// Initilization 
switft := car{"Maruti", 2020, owner{"Abhi"}}
ownerName := car.name  // We can access the fields or methods (see Embedding Section of the handbook) of the inner struct directly

type truck struct {
	model string
	owner    // This struct will inherit the fields of the owner
}

trala := truck{"tata", "Abhi"}   // Inherited the name field


// You can declare methods on structs. The struct you want to declare the
// method on (the receiving type) comes between the the func keyword and
// the method name. The struct is copied on each method call(!)
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

// Call method
v.Abs()

// For mutating methods, you need to use a pointer (see below) to the Struct as the type. With this, the struct value is not copied for the method call.
func (v *Vertex) add(n float64) {
    v.X += n
    v.Y += n
}

v := Vertex{1, 1}  // v is a Value, not a pointer
v.add(5.0)         // Go implicitly compiles this as (&v).add(5.0)
fmt.Println(v)     // Output: {6 6} - The original was modified
```
## Anonymous structs
Cheaper and safer than using `map[string]interface{}`.
```go
point := struct {
	X, Y int
}{1, 2}
```

# Interfaces
For more information watch [Golang: The Last Interface Explanation You'll Ever Need](https://www.youtube.com/watch?v=SX1gT5A9H-U)

- Keep Interfaces small 
- Interfaces should have no Knowledge of the satisfying types 
- Interfaces are not classes

> [!NOTE]
> For more information on this topic read [[GO Programming#Interfaces| Go Programming - cerebrum]] 

```go
// 1. The Interface (The Contract)
// Any type that has a "Say()" method counts as a "Speaker".
type Speaker interface {
    Say()
}

// 2. The Concrete Types
type Dog struct{}
type Person struct{}

// 3. The Implementation
// Dog implements Speaker implicitly because it has Say()
func (d Dog) Say() { fmt.Println("Woof!") }

// Person implements Speaker implicitly because it has Say()
func (p Person) Say() { fmt.Println("Hello!") }

// 4. Polymorphism in action
// This function accepts ANYTHING that satisfies the Speaker interface
func makeItTalk(s Speaker) {
    s.Say()
}

func main() {
    d := Dog{}
    p := Person{}

    // Both work because they both fulfill the contract
    makeItTalk(d)
    makeItTalk(p)
}
```

```go
type shape interface {
  area() float64
  perimeter() float64
}

type rect struct {
    width, height float64
}
func (r rect) area() float64 {
    return r.width * r.height
}
func (r rect) perimeter() float64 {
    return 2*r.width + 2*r.height
}

type circle struct {
    radius float64
}
func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perimeter() float64 {
    return 2 * math.Pi * c.radius
}

// Function Implementing Interfaces
func printShapeData(s shape) {
	fmt.Printf("Index: %v - Area: %v - Perimeter: %v\n", i, s.area(), s.perimeter())
}
```
# Embedding 
In Go (Golang), **Embedding** is a way to combine different types to reuse code.

Since Go does not have "Classes" or "Inheritance" (like Java or Python), it uses **Composition**. Embedding allows you to put one struct (or interface) inside another.

The "magic" of embedding is **Promoted Methods**. When you embed a type, all of its methods become available on the outer type automatically. It looks like the outer type "inherited" the methods, but it actually just holds the inner type and forwards the calls to it.

It has two types:
- **Struct Embedding** is about reusing code (implementation).
- **Interface Embedding** is about reusing rules (contracts).

### Struct Embedding 
```go
package main

import "fmt"

// 1. The Inner Type (The Engine)
type Engine struct {
    Horsepower int
}

func (e Engine) Start() {
    fmt.Println("Vroom! Engine started with", e.Horsepower, "horsepower.")
}

// 2. The Outer Type (The Car)
type Car struct {
    Make  string
    Model string
    Engine // <--- EMBEDDING: The Car "has an" Engine
}

func main() {
    // Initialize
    myCar := Car{
        Make:  "Tesla",
        Model: "Model S",
        Engine: Engine{
            Horsepower: 400,
        },
    }

    // 3. USE IT
    // We can call Start() directly on myCar!
    // The method is "promoted" from the Engine to the Car.
    myCar.Start() 
    
    // We can also access the inner data if we want
    fmt.Printf("This %s has %d HP\n", myCar.Model, myCar.Horsepower)
}
```

- **Less Boilerplate:** You don't have to write a wrapper method like `func (c Car) Start() { c.engine.Start() }`. Go does it for you.
- **Organisation:** It allows you to build complex objects out of small, reusable blocks.

### Interface Embedding 
```go 
package main

import "fmt"

// 1. Small, specific interface (Job 1)
type Printer interface {
    Print(doc string)
}

// 2. Another small, specific interface (Job 2)
type Scanner interface {
    Scan()
}

// 3. INTERFACE EMBEDDING (The Merger)
// A "Copier" isn't a new thing; it's just something that can 
// do BOTH printing and scanning.
type Copier interface {
    Printer
    Scanner
}

// --- The Implementation ---

// 4. A concrete struct (The Machine)
type OfficeJet struct {
    Model string
}

// Implement the Printer interface
func (o OfficeJet) Print(doc string) {
    fmt.Println(o.Model, "is printing:", doc)
}

// Implement the Scanner interface
func (o OfficeJet) Scan() {
    fmt.Println(o.Model, "is scanning a document.")
}

func main() {
    // Create the real object
    myMachine := OfficeJet{Model: "HP 5000"}

    // 5. Use the combined interface
    // This function demands a "Copier". 
    // myMachine works because it has both Print() and Scan() methods.
    runCopyJob(myMachine) 
}

// This function accepts the EMBEDDED interface
func runCopyJob(c Copier) {
    fmt.Println("--- Starting Copy Job ---")
    c.Scan()
    c.Print("The Scanned Image")
}
```

- **Small is Beautiful:** You can keep your interfaces tiny (like `Reader` and `Writer`). This follows the **Interface Segregation Principle** (the "I" in SOLID).
- **Mix and Match:** You don't need to create a massive "MegaInterface" from scratch. You just glue together the small pieces you need for a specific function.

# Empty Interface 
- Go's most powerful / dangerous feature 

- The Empty Interface has zero methods.
- Since every type in Go has at least zero methods, every type satisfies the empty interface.
- Think of it as a **"Mystery Box"** that can hold anything.
- Used to handle data when you don't know the type.
- Useful when un-marshalling JSON of unknown type
- Avoid it when you know the types

#### Example 1: The Chameleon Variable
A single variable that can change its type at runtime.

```go
func main() {
	// 1. Declare an empty interface
	var anything interface{}

	// 2. Put a string in it
	anything = "Hello"
	fmt.Printf("Value: %v \n", anything)

	// 3. Put an int in THE SAME variable
	anything = 42
	fmt.Printf("Value: %v \n", anything)

	// 4. Put a struct in it
	anything = true
	fmt.Printf("Value: %v \n", anything)
}
```

---

#### Example 2: Accepting Any Argument
This is how functions like `fmt.Println` allow you to print strings, numbers, and objects without separate functions for each.

```go
// This function accepts ANY type of data
func Describe(i interface{}) {
	fmt.Printf("Type: %T, Value: %v\n", i, i)
}

func main() {
	Describe(100)           // Pass an int
	Describe("Golang")      // Pass a string
	Describe([]int{1, 2})   // Pass a slice
}
```

---

#### The "Catch" (Important)
Once you put a value into an empty interface, the compiler **forgets** what it is. You lose all behavior (methods and operators) until you take it out.
```go
package main

func main() {
	var val interface{} = 10

	// ERROR! 
	// The compiler treats 'val' as a generic object, not an integer.
	// You cannot do math on it directly.
	// fmt.Println(val + 5) 

	// FIX: You must Type Assert it back to an int first
	realInt := val.(int)
	println(realInt + 5) // Now it works (prints 15)
}
```

# Any Type
In Go 1.18 and later, **`any`** is simply an **alias** for `interface{}`.
They are identical. The Go team added `any` because writing `interface{}` over and over again is tedious and hard to read.
```go
// These two lines mean EXACTLY the same thing
var a interface{}
var b any 
```

### Example 1: The "Any" Variable
Just like the empty interface, `any` can hold a value of any type.
```go
func main() {
    var data any

    data = 100        // Int
    fmt.Println(data)

    data = "Hello"    // String
    fmt.Println(data)

    data = 3.14       // Float
    fmt.Println(data)
}
```

### Example 2: Mixed Lists (Slices)
You can use `any` to create arrays that hold different types of data at the same time.
```go
func main() {
    // A slice that holds "any" type of data
    mixedList := []any{ "Start", 42, true, 99.9 }

    for _, v := range mixedList {
        fmt.Printf("Value: %v \t(Type: %T)\n", v, v)
    }
}
```

### Example 3: Generics (Constraint)
While `any` acts like `interface{}`, it is most commonly seen in **Generics** to say "This function accepts a type `T`, and I don't care what `T` is."
```go
// [T any] means T can be any type
func PrintValue[T any](val T) {
    fmt.Println("Generic print:", val)
}

func main() {
    PrintValue(10)
    PrintValue("Text")
}
```


# Type Assertion
It is a way to check which type we are handling while working with interfaces
```go
func main() {
	// An empty interface can hold anything (The Box)
	var myBox interface{} = "I am a string"

	// 1. THE UNSAFE WAY (Panic potential)
	// We assert: "The value inside myBox is definitely a string."
	val := myBox.(string) 
	fmt.Println("Unsafe value:", val)

	// 2. THE SAFE WAY (Comma-ok idiom)
	// We assert: "Check if this is an int, but don't crash if I'm wrong."
	// ok will be true if successful, false if not.
	num, ok := myBox.(int) 

	if ok {
		fmt.Println("It is an int:", num)
	} else {
		fmt.Println("It is NOT an int. Conversion failed safely.")
	}
}
```

```go
func main() {
    // 1. The Interface Variable
    // 'val' is generic. The compiler ONLY knows it is an interface{}.
    // It does NOT know it has a field called "Name".
    var val interface{} = Person{Name: "Alice"}

    // fmt.Println(val.Name) // <--- ERROR! interfaces don't have fields.

    // 2. Type Assertion
    // We tell the compiler: "Trust me, underneath this interface is a Person struct."
    p, ok := val.(Person) 

    if ok {
        // Now 'p' is a real Person struct, so we can access .Name
        fmt.Println("Found person:", p.Name)
    } else {
        fmt.Println("Value is not a Person")
    }
}

type Person struct {
    Name string
}
```


```go
type shape interface {
	area() float64
}

type circle struct {
	radius float64
}

func (c circle) area() float64{
	return 3.14*c.radius*c.radius
}

c, ok := s.(circle)
if !ok {
	// log an error if s isn't a circle
	log.Fatal("s is not a circle")
}

radius := c.radius
```

# Type Switch
## Basic Check 
```go
func doSomething(i any) {
    // syntax: variable.(type)
    switch i.(type) {
    case int:
        fmt.Println("I got an Integer!")
    case string:
        fmt.Println("I got a String!")
    case bool:
        fmt.Println("I got a Boolean!")
    default:
        fmt.Println("I don't know what this type is.")
    }
}

func main() {
    doSomething(100)
    doSomething("Hello")
}
```

## Value Extraction
```go
func process(i any) {
    // 'v' becomes the specific type inside each case block
    switch v := i.(type) {
    
    case int:
        // Here, v is an int. We can add 10.
        fmt.Printf("Math: %d + 10 = %d\n", v, v+10)
        
    case string:
        // Here, v is a string. We can use len().
        fmt.Printf("String length: %d\n", len(v))
        
    case []string:
        // Here, v is a slice of strings. We can loop over it.
        fmt.Printf("List has %d items\n", len(v))
        
    default:
        fmt.Printf("Unknown type: %T\n", v)
    }
}

func main() {
    process(50)             // Hits 'case int'
    process("Golang")       // Hits 'case string'
    process([]string{"A"})  // Hits 'case []string'
}
```


# Type Alias
## Basic 
```go
// 1. Create the Alias (Note the equals sign)
type Seconds = int

func main() {
	var s Seconds = 10
	var i int = 20

	// 2. MIX THEM
	// No type conversion needed! 
	// Go sees them as the exact same type.
	total := s + i 
}
```

## Interface Types 
```go
// 1. Create the Alias , Single type alias handling multiple native types
type Seconds interface{
	int | int8 | int16 | float32 | float64
}

func main() {
	var s Seconds = 10
	var i Seconds = 10.111
}
```

## Ordered Constrains Package
`golang.org/x/exp/constraints` provides 

| Interface Type | Description                            | Included Types (All include `~`)                         |
| -------------- | -------------------------------------- | -------------------------------------------------------- |
| **`Signed`**   | All signed integer types.              | `int`, `int8`, `int16`, `int32`, `int64`                 |
| **`Unsigned`** | All unsigned integer types.            | `uint`, `uint8`, `uint16`, `uint32`, `uint64`, `uintptr` |
| **`Integer`**  | **Union** of all integers.             | `Signed`                                                 |
| **`Float`**    | Floating-point numbers.                | `float32`, `float64`                                     |
| **`Complex`**  | Complex numbers.                       | `complex64`, `complex128`                                |
| **`Ordered`**  | Types that support `<` `>` comparison. | `Integer`                                                |

```go
import (
	"fmt"
	"golang.org/x/exp/constraints"
)

// using Ordered Interface Type
func Min[T constraints.Ordered](a, b T) T {
	if a < b {
		return a
	}
	return b
}
// using Integer Interface Type
func IsEven[T constraints.Integer](n T) bool { 
return n%2 == 0 
}
```

# JSON
## Marshalling
```go
package main

import (
	"encoding/json"
	"fmt"
)

// Define the struct with JSON tags
type User struct {
	// 1. RENAME: Maps the Go field "FullName" to the JSON key "username"
	FullName string `json:"username"`

	// 2. OMIT EMPTY: If Age is 0 (the zero value), do not include it in the JSON
	Age int `json:"age,omitempty"`

	// 3. IGNORE: This field will never be shown in the JSON (good for passwords)
	Password string `json:"-"`

	// 4. NO TAG: Will use the exact Go field name ("Email")
	Email string
}

func main() {
	// Create a struct instance
	user := User{
		FullName: "John Doe",
		Age:      0,            // Zero value, so it will be omitted
		Password: "secret_pass", // Will be ignored
		Email:    "john@example.com",
	}

	// Convert struct to JSON
	// Returns a byte slice ([]byte) and an error
	jsonData, err := json.Marshal(user)
	if err != nil {
		fmt.Println(err)
		return
	}

	// Convert bytes to string to print
	fmt.Println(string(jsonData))
}
```

Output
```json
{"username":"John Doe","Email":"john@example.com"}
```

## Unmarshaling
- Extra JSON Fields will be ignored
- Missing JSON Fields will result in struct field having an Zero Value
- If you don't provide a struct tag, Go tries to match `Username` to `"Username"`, and if that fails, it tries `"username"` (case-insensitive match).

```go
package main

import (
	"encoding/json"
	"fmt"
)

// The Target Struct
type UserProfile struct {
	// 1. EXPLICIT TAG:
	// This looks specifically for JSON key "full_name".
	Name string `json:"full_name"`

	// 2. NO TAG (CASE-INSENSITIVE FALLBACK):
	// Go first looks for "Country". If not found, it looks for "country".
	Country string

	// 3. MISSING IN JSON:
	// This field exists in Go, but the JSON won't have data for it.
	// It will remain at its "Zero Value" (0).
	Age int
}

func main() {
	// The Raw JSON
	// Contains:
	// - "full_name": Matches struct with tag.
	// - "country": Lowercase in JSON, Uppercase in struct (Fallback works).
	// - "twitter_handle": Exists in JSON, but NOT in struct (Extra field).
	// - (Missing): "Age" is not here.
	jsonString := `
	{
		"full_name": "Alice Wonderland", 
		"country": "UK", 
		"twitter_handle": "@alice_in_code" 
	}`

	// Variable to hold the result
	var user UserProfile

	// Unmarshal
	// Note: Go ignores the extra "twitter_handle" without error.
	// Pointer to the user variable so that Unmarshall function can change the fields in the user variable
	err := json.Unmarshal([]byte(jsonString), &user)
	if err != nil {
		panic(err)
	}

	// Print Result
	fmt.Printf("Name:    %s\n", user.Name)
	fmt.Printf("Country: %s (Matched via Case-Insensitivity)\n", user.Country)
	fmt.Printf("Age:     %d (Kept Zero Value)\n", user.Age)
}
```

Output
```
Name:    Alice Wonderland
Country: UK (Matched via Case-Insensitivity)
Age:     0 (Kept Zero Value)
```

### Strict Unmarshaling
Demands a completely matching of the struct and the `json` string

```go
package main

import (
	"encoding/json"
	"fmt"
	"strings"
)

// The Target Struct
type User struct {
	Name string `json:"name"`
}

func main() {
	// The Raw JSON
	// Contains "email", which is NOT in the User struct.
	jsonString := `{"name": "Alice", "email": "alice@ex.com"}`

	// 1. Setup the Decoder
	// We wrap the string in a Reader because Decoders work with streams/readers.
	reader := strings.NewReader(jsonString)
	decoder := json.NewDecoder(reader)

	// 2. ENFORCE STRICTNESS
	// This tells the decoder: "If you see a field I don't know, fail immediately."
	decoder.DisallowUnknownFields()

	var user User

	// 3. Decode
	err := decoder.Decode(&user)

	if err != nil {
		// This block WILL run because of the extra "email" field
		fmt.Println("Validation Failed:", err)
	} else {
		fmt.Printf("Success: %+v\n", user)
	}
}
```

Output
```
Validation Failed: json: unknown field "email"
```

This is extremely useful for **API validation**. If a client sends you data with a typo (e.g., sending `"usernaame"` instead of `"username"`), the default behavior would silently ignore it and leave your struct empty. Using 
`DisallowUnknownFields` forces the client to fix their typo.

## Unknown Types
```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	// 1. The "Mystery" JSON
	// Imagine this comes from an external API and changes often.
	jsonString := `
	{
		"event": "login_attempt",
		"timestamp": 1678900000,
		"success": true,
		"metadata": {
			"ip": "192.168.1.1"
		}
	}`

	// 2. Create a Generic Map
	// This map can hold any JSON object.
	var result map[string]interface{}

	// 3. Unmarshal
	err := json.Unmarshal([]byte(jsonString), &result)
	if err != nil {
		panic(err)
	}

	// 4. Iterate over keys (Discovery)
	fmt.Println("--- Discovering Fields ---")
	for key, value := range result {
		fmt.Printf("Key: %s, Value: %v, Type: %T\n", key, value, value)
	}

	// 5. Accessing Specific Data (Type Assertion)
	// To USE the data (e.g., do math), you MUST assert the type.
	
	fmt.Println("\n--- Accessing Data ---")

	// WARNING: JSON numbers are always float64 in generic maps!
	// We cannot assert to 'int' directly.
	if ts, ok := result["timestamp"].(float64); ok {
		fmt.Printf("Timestamp: %.0f\n", ts)
	}

	if success, ok := result["success"].(bool); ok {
		if success {
			fmt.Println("Login Successful!")
		}
	}
}
```

```
--- Discovering Fields ---
Key: event, Value: login_attempt, Type: string
Key: timestamp, Value: 1.6789e+09, Type: float64
Key: success, Value: true, Type: bool
Key: metadata, Value: map[ip:192.168.1.1], Type: map[string]interface {}

--- Accessing Data ---
Timestamp: 1678900000
Login Successful!
```

### Critical Pitfall: The `float64` Rule

When you unmarshal into `interface{}`, Go converts **all** JSON numbers to **`float64`**.
- Even if the JSON says `100` (looks like an int), Go stores it as `100.0` (`float64`).
- **Do not** do `val.(int)`. It will fail (panic or return false). You must assert `val.(float64)` first, then convert to int if needed (`int(val.(float64))`).


# Pointers 
Mainly used to modify variables outside the scope of function 
- `&` - address of operator - Gets the address of the operator 
- `* - with a type` - it tells the compiler that variable is the pointer to that type
- `* - with a variable` - de-reference operator , gets the value stored at that memory address of the pointer

```go
var p *int // p is the pointer to int
var p *int = &x // pointer p store the address of variable x
p := &x  // pointer p (infered) stores the address of x
p := &Person{"Abhijeet"} //Pointer p stoed address of struct

person := Person{"Abhijeet"}

p := &person // Pointer p (infered) stores address of person
var p *Person = &person // *Person is the type of pointer to struct

var num int = *p  // Values stored at address of p is assigned to num (derefferencing of p)
var person Person = *p  // Struct stored at address of p is assigned to person variable (derefferencing of p)
```

## Pass be Reference in Go
By default Go passes by values , thus the changes you make in a functions are not reflect outside it also you cant change a variable outside your scope

You can change this by using pointers 
### Structs
To modify the original, pass a pointer (`*Struct`).
```go
type User struct {
	Name string
}

// Accepts a POINTER to User
func rename(u *User) {
	u.Name = "Bob" // Go automatically dereferences (*u).Name
}

func main() {
	u := User{Name: "Alice"}
	
	// Pass the ADDRESS of u
	rename(&u)
	
	fmt.Println(u.Name) // Prints: Bob (Original was changed)
}
```
### Arrays (Fixed Size)
If you pass an array to a function, Go copies **every single item**. To avoid this and modify the original, pass a pointer to the array.
```go
// Accepts a POINTER to an array of 3 ints
func updateArray(arr *[3]int) {
	// We update index 0
	arr[0] = 999
}

func main() {
	nums := [3]int{1, 2, 3}

	// Pass the ADDRESS of the array
	updateArray(&nums)

	fmt.Println(nums) // Prints: [999 2 3]
}
```
### Basic Types (Int, String, Bool)
You cannot change an integer inside a function unless you pass its address.
```go
func zeroOut(n *int) {
	*n = 0 // Update the value at this address
}

func main() {
	count := 100
	zeroOut(&count)
	fmt.Println(count) // Prints: 0
}
```
### The Exception: Maps and Slices ("Reference Types")
Maps and Slices are special. They contain internal pointers effectively.
- **You do NOT need to use `*`** to modify their _contents_.
- They act like pass-by-reference by default.
```go
// No pointer needed!
func modifyMap(m map[string]string) {
	m["key"] = "modified"
}

// No pointer needed!
func modifySlice(s []int) {
	s[0] = 999
}

func main() {
	// 1. Map
	myMap := map[string]string{"key": "original"}
	modifyMap(myMap)
	fmt.Println(myMap["key"]) // Prints: modified

	// 2. Slice
	mySlice := []int{1, 2, 3}
	modifySlice(mySlice)
	fmt.Println(mySlice[0])   // Prints: 999
}
```

### Shallow Copy
When you assign a Slice or a Map to a new variable (e.g., `var2 := var1`), Go copies the **header** (which contains a pointer), but it does **not** copy the underlying data.
```go
func main() {
	// --- EXAMPLE 1: SLICES ---
	// 1. Create Original
	originalSlice := []int{10, 20, 30}

	// 2. Assign to a new variable
	// This creates a new "Slice Header", but it points to the SAME array.
	refSlice := originalSlice

	// 3. Modify the NEW variable
	refSlice[0] = 999

	// 4. Check the ORIGINAL
	// It changed!
	fmt.Println(originalSlice) // Prints [999 20 30]
	fmt.Println(refSlice)      // Prints [999 20 30]


	// --- EXAMPLE 2: MAPS ---
	// 1. Create Original
	originalMap := map[string]string{"role": "Admin"}

	// 2. Assign to a new variable
	// Maps are purely pointers to data structures.
	refMap := originalMap

	// 3. Modify the NEW variable
	refMap["role"] = "Guest"

	// 4. Check the ORIGINAL
	// It changed!
	fmt.Println(originalMap["role"]) // Prints "Guest"
	fmt.Println(refMap["role"])      // Prints "Guest"
}
```
## Summary Table

| **Type**              | **Default Behavior**         | **To Modify Original** |
| --------------------- | ---------------------------- | ---------------------- |
| **Int, String, Bool** | Copy                         | Pass `*int`            |
| **Struct**            | Copy                         | Pass `*Struct`         |
| **Array** `[N]T`      | Copy (Slow for large arrays) | Pass `*[N]T`           |
| **Slice** `[]T`       | **Reference-like**           | Pass `[]T`             |
| **Map**               | **Reference-like**           | Pass `map`             |

# Concurrency
![concurrency](https://storage.googleapis.com/qvault-webapp-dynamic-assets/course_assets/1pQKFgw.png)

```go
go hello() // Runs the function on a concurrently 

go func (x int){
	// run the anonymus function concurrently
}
```


## WaitGroups
A **WaitGroup** is like a **Counter**. It allows your main program to wait for a specific number of goroutines to finish before quitting.

Without a WaitGroup, the `main()` function often exits immediately, killing your background workers before they finish.

### How it works (The 3 Rules)
1. **`Add(1)`**: "I am starting a new worker." (Increments counter).
2. **`Done()`**: "I am finished." (Decrements counter).
3. **`Wait()`**: "Stop here until the counter is 0."

### Code Example

**Crucial Note:** When passing a WaitGroup to a function, you **must** pass a pointer (`*sync.WaitGroup`), otherwise Go copies the lock and it won't work.
```go
package main

import (
	"fmt"
	"sync"
	"time"
)

// Worker function accepts a POINTER to the WaitGroup
func worker(id int, wg *sync.WaitGroup) {
	// 3. On exit, decrement the counter
	// 'defer' ensures this runs even if the function crashes.
	defer wg.Done()

	fmt.Printf("Worker %d: Starting\n", id)
	time.Sleep(1 * time.Second) // Simulate work
	fmt.Printf("Worker %d: Done\n", id)
}

func main() {
	// 1. Create the WaitGroup
	var wg sync.WaitGroup

	for i := 1; i <= 3; i++ {
		// 2. Increment counter BEFORE starting the goroutine
		wg.Add(1)
		
		// Pass the address (&wg)
		go worker(i, &wg)
	}

	fmt.Println("Main: Waiting for workers...")

	// 4. Block here until counter reaches 0
	wg.Wait()

	fmt.Println("Main: All done. Exiting.")
}
```
Output
```
Main: Waiting for workers...
Worker 1: Starting
Worker 2: Starting
Worker 3: Starting
( ... 1 second wait ... )
Worker 1: Done
Worker 3: Done
Worker 2: Done
Main: All done. Exiting.
```
### Common Pitfall

- Never put wg.Add(1) inside the goroutine.

The goroutine might not start immediately. The code could hit wg.Wait() while the counter is still 0, causing main to exit before the workers even wake up. Always Add() in the main thread.

## Channels 
- Enable inter thread communication
- Non Buffered Channel - Channels that can hold only one value
- Buffered Channel - Channels that can hold more than one value
```go
ch := make(chan int) // Unbuffred Channel
ch := make(chan int, 100)  // Buffered channel , can hold 100 values

ch := make(chan int) // create a channel of type int
ch <- 42             // Send a value to the channel ch.
v := <-ch            // Receive a value from ch
close(ch) // closes the channel (only sender should close)

// read from channel and test if it has been closed
v, ok := <-ch
// if ok is false, channel has been closed

// Read from channel until it is closed
for i := range ch {
    fmt.Println(i)
}

//Send on a close channel panics
c <- "Hello, World!"
close(c)
c <- "Hello, Panic!"  // Panics

// A receave from a close channel returns 0 immidiately
var c = make(chan int, 100)
close(c)
fmt.Println(<-c) // 0
```

### Unbuffered Channel
- **Send (`ch <- v`)** stops execution until **Receive (`<-ch`)** happens.
- **Receive (`<-ch`)** stops execution until **Send (`ch <- v`)** happens.
- **If both occur in the same goroutine**, you get a **Deadlock** (crash).

Deadlock - Waiting for Receiver
```go
var c chan string
c <- "Hello, World!"
// fatal error: all goroutines are asleep - deadlock!
```

Deadlock - Waiting for Sender
```go
var c chan string
fmt.Println(<-c)
// fatal error: all goroutines are asleep - deadlock!
```

Working program - Proper Handshake
```go
func main() {
    ch := make(chan int)

    // 1. Launch a partner in the background
    go func() {
        fmt.Println("Sender: I am working...")
        time.Sleep(2 * time.Second) // Simulate work
        fmt.Println("Sender: Sending value now!")
        
        // This blocks strictly until main is ready to receive
        ch <- 100 
    }()

    fmt.Println("Receiver: I am waiting...")
    
    // 2. Main blocks here for 2 seconds
    // It resumes ONLY when the goroutine sends the data.
    val := <-ch 
    
    fmt.Println("Receiver: Got", val)
}
```


### Buffered Channel

| Action             | State of Buffer                | Result                                 |
| ------------------ | ------------------------------ | -------------------------------------- |
| **Send** `ch <- v` | **Space Available** (0/2, 1/2) | **Instantly continues** (Non-blocking) |
| **Send** `ch <- v` | **Full** (2/2)                 | **Stops/Blocks** (Waits for space)     |
| **Receive** `<-ch` | **Has Data** (1/2, 2/2)        | **Instantly continues** (Non-blocking) |
| **Receive** `<-ch` | **Empty** (0/2)                | **Stops/Blocks** (Waits for data)      |

Deadlock - Send when buffer is full
```go
func main() {
    // Capacity is 2
    ch := make(chan string, 2)

    // 1. First send: OK (Buffer: 1/2)
    ch <- "A" 

    // 2. Second send: OK (Buffer: 2/2)
    ch <- "B" 
    
    fmt.Println("Buffer is full now.")

    // 3. EXECUTION STOPS HERE!
    // The buffer is full. We cannot add "C".
    // We are forced to wait until someone reads from the channel.
    ch <- "C" 

    fmt.Println("This line runs only if space clears up.")
}
```

Deadlock - Read when buffer is empty
```go
func main() {
    // Capacity is 2
    ch := make(chan int, 2)

    // 1. Send one item
    ch <- 100 
    
    // 2. First receive: OK (We take 100 out)
    fmt.Println(<-ch) 

    // 3. EXECUTION STOPS HERE!
    // The buffer is now empty (0 items).
    // We wait here forever for new data.
    fmt.Println(<-ch) 
}
```

No deadlock - Perfect Handshake
```go
func main() {
    // 1. Create a Buffered Channel (Capacity 2)
    // We have 2 empty slots.
    ch := make(chan string, 2)
    
    // 2. Send First Item
    // NON-BLOCKING: There is space (1/2), so we drop the letter and keep running.
    ch <- "Hello" 
    
    // 3. Send Second Item
    // NON-BLOCKING: There is space (2/2), so we drop the letter and keep running.
    ch <- "World" 

    // NOTE: If we tried to send a 3rd item here, it WOULD block.

    // 4. Read First Item
    // NON-BLOCKING: The box has mail, so we grab it instantly.
    msg1 := <-ch 
    fmt.Println("Received:", msg1)

    // 5. Read Second Item
    // NON-BLOCKING: The box has mail, so we grab it instantly.
    msg2 := <-ch
    fmt.Println("Received:", msg2)
}
```


A closed channel will return zero values for the type immediately
```go
// Receave form close channel returns zero value immidiately
var c = make(chan int, 2)
c <- 1
c <- 2
close(c)   
for i := 0; i < 3; i++ {
    fmt.Printf("%d ", <-c)  // 1 2 0
}
```

### Read Only Channels Functions
```go
// This channels will not accept any new data inside this funcion
// You can only read it, inside this function 

func consumes(ch <-chan int) { // Arrow out in function defination
	val := <-ch fmt.Println("Read:", val) 

// ch <- 100 // COMPILER ERROR: "send to receive-only type <-chan int" 
}
```

### Write Only Channels Functions
```go
// This channel will not return any data inside this function 
// You can only write to it , inside this function

func produce(ch chan<- string) { // Arrow in , in the function definition
    ch <- "Hello"
    
// fmt.Println(<-ch) // COMPILER ERROR: "receive from send-only type chan<- string"
}
```

### Select Channels
The `select` statement is like a **`switch` for channels**.
It lets a single goroutine wait on **multiple** channels at the same time.
- It blocks (waits) until **one** of the cases is ready.
- If multiple are ready at the same time, it picks one **at random**.
```go
func main() {
    fast := make(chan string)
    slow := make(chan string)

    // 1. Start two senders
    go func() { fast <- "Fast Car" }()
    go func() { slow <- "Slow Car" }()

    fmt.Println("Waiting for a winner...")

    // 2. Select waits for ONE of these to happen
    select {
    case msg1 := <-fast:
        fmt.Println("Winner:", msg1)
    case msg2 := <-slow:
        fmt.Println("Winner:", msg2)
    }
}
```

### Default - Select Statement 
The `default` case makes a `select` statement **Non-Blocking**.
Normally, `select` waits forever until a channel is ready. With `default`, it checks: **"Is any channel ready right now? No? Then run the default code and move on."**

```go
func main() {
    ch := make(chan string) // Empty channel

    select {
    case msg := <-ch:
        fmt.Println("Received:", msg)
    default:
        // Runs IMMEDIATELY because 'ch' is empty.
        // The program does NOT stop or freeze here.
        fmt.Println("No data ready. I am not waiting.")
    }
}
```

Output
```
No data ready. I am not waiting.
```

## Mutex
We use this to prevent **Race Conditions**, where two goroutines try to write to the same variable at the exact same time, causing errors.

- `Lock()` -> Lock the variable inside so that no other goroutine can access it
- `Unlock()` -> Unlock the variable inside so that other goroutine can access it


```go
// 1. The Shared Data
var count int

// 2. The Lock
// We usually put the Mutex right next to the data it protects.
var mu sync.Mutex

func increment(wg *sync.WaitGroup) {
	defer wg.Done()

	// --- CRITICAL SECTION START ---
	// "I am using the counter now. Everyone else wait."
	mu.Lock()

	count++ // Safe because only one goroutine is here at a time.

	// "I am done. Next person can come in."
	mu.Unlock()
	// --- CRITICAL SECTION END ---
}

func main() {
	var wg sync.WaitGroup

	// Start 1000 goroutines
	for i := 0; i < 1000; i++ {
		wg.Add(1)
		go increment(&wg)
	}

	// Wait for all to finish
	wg.Wait()

	fmt.Println("Final Count:", count) // Always prints 1000
}
```
Without a Mutex, if 1000 goroutines try to do `count++` at the same time, some numbers will get lost (e.g., the result might be 950 instead of 1000). The Mutex fixes this.

#### Best Practice: `defer`

If your function crashes or returns early before hitting `Unlock()`, your program will freeze forever (Deadlock). To prevent this, use `defer` immediately after locking:
```go
mu.Lock()
defer mu.Unlock() // Will unlock automatically when function ends

// ... do complex work ...
```

### Read Mutex
- **`RLock()` / `RUnlock()`**: "I just want to **read**. Others can read with me, but no one can write.    
- **`Lock()` / `Unlock()`**: "I need to **write**. Everyone else get out (readers and writers)."

```go
var (
	// The Shared Data
	data = "Empty"
	// The Reader-Writer Mutex
	rwMu sync.RWMutex
)

// READER: Uses RLock (Allows multiple readers)
func read(id int, wg *sync.WaitGroup) {
	defer wg.Done()

	rwMu.RLock() // <--- REQUEST READ PERMISSION
	fmt.Printf("Reader %d: Reading data: %s\n", id, data)
	time.Sleep(1 * time.Second) // Simulate reading time
	rwMu.RUnlock() // <--- DONE READING
}

// WRITER: Uses Lock (Blocks everyone)
func write(newValue string, wg *sync.WaitGroup) {
	defer wg.Done()

	rwMu.Lock() // <--- REQUEST EXCLUSIVE PERMISSION
	fmt.Println("--- Writer: Writing new data... ---")
	data = newValue
	time.Sleep(1 * time.Second) // Simulate writing time
	rwMu.Unlock() // <--- DONE WRITING
}

func main() {
	var wg sync.WaitGroup

	// 1. Start 3 Readers
	// They will all read at the SAME TIME (because of RLock)
	for i := 1; i <= 3; i++ {
		wg.Add(1)
		go read(i, &wg)
	}

	time.Sleep(100 * time.Millisecond) // Ensure readers start first

	// 2. Start a Writer
	// It has to WAIT until the readers are done.
	wg.Add(1)
	go write("Updated Data", &wg)

	wg.Wait()
}
```

If you used a standard `Mutex`, Reader 2 would have to wait for Reader 1 to finish. With `RWMutex`, Reader 1, 2, and 3 access the data **simultaneously**, making the program much faster when you have **many reads and few writes**.
# Generics 
Have a look at [[#Type Alias]] before reading this

```go
// [T int | float64] is the Generic Type Parameter.
// It tells Go: "T can be an int OR a float64."
func Add[T int | float64](a, b T) T {
    return a + b
}
 // Not this function can accept both int and float64 types to add them , otherwise we would have to make two seperate function 

func main() {
    // 1. Use with Integers
    // Go figures out T is 'int' automatically
    sumInt := Add(10, 20)
    fmt.Println("Int Sum:", sumInt)

    // 2. Use with Floats
    // Go figures out T is 'float64' automatically
    sumFloat := Add(5.5, 4.4)
    fmt.Println("Float Sum:", sumFloat)
}
```

## Interface Type Alias Generics 
```go
type Seconds interface{
	int | float32 | float64
}

func SecondsAfter(t Seconds){
	// This also uses Generics , just its in a interface
}
```

