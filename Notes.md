# My Golang notes 
**NOTE:** These notes are a reference from https://github.com/inancgumus/learngo and full credits to Udemy course `Master and Deeply Understand Google's Go from Scratch with Illustrated In-Depth Tutorials & 1000+ Hands-On Exercises` by Inanc Gumus and Jose Portilla

* To intialize a module 
  * `go mod mymodule`

* To download all required packages (to add module requirements and sums) 
  * `go mod tidy`

* To run a script witout building it
  * `go run myscript.go`

* To build a package with a specific name (-o option)
  * `go build -o myscript`


## Variables

* Declaration and Initialization
  * `var speed int`
  * ```
    var (
       speed int = 10
       heat float64 = 31.5
       off bool = true
       brand string = "famous"
    )
* Zero values and Short declaration 
  * ```
     booleans --> false
     numerics --> 0
     strings --> ""
     pointers --> nil
  * ```
    safe := true
    safe, speed := true, 50
    
    [NOTE: can't be used at the package scope, works only at the block scope]  

  * Discording using blank-identifier
    variable,_ := value1, value2 
    
<img src="https://user-images.githubusercontent.com/67871237/172010394-f951ac42-bad7-40b2-bc95-0b9f3f09d42f.png" width="300" height="200">



## Raw string literal
<img src="https://user-images.githubusercontent.com/67871237/172013672-aff584a8-38a5-412a-9086-aa9979e82363.png" width="300" height="200">

  * **String literal:** Interpreted(means if there is any escape secquences ex:`\` or `\n`, GO will interpret them)
    ```	
    s = "<html>\n\t<body>\"Hello\"</body>\n</html>"
  * **Raw stringl iteral:** Not interpreted
    ```
      s = `
    <html>
     <body>"Hello"</body>
    </html>`

## enum and iota
* **enum** groups related constants in one type. Below `Weekday` is a custom type of int
* **iota** is a numeric universal counter starting at 0. Used ONLY with constant declarations
<img src="https://user-images.githubusercontent.com/67871237/172019199-47831784-fad7-43c2-b74c-d2a621f69f86.png" width="400" height="300">

## Printf
* `fmt.Printf` prints formatted output, some examples below
  * `%q` prints string with quotes ex: `"Ramana"`
  * `%s` prints string without quotes ex: `Ramana`
  * `%T` prints type of the var ex: 'int'
  * `%d` prints int values ex: `10`
  * `%.2f` prints float64 values with 2 precision points ex: `54.50`
  * `%t` prints bool values ex: `true`
  * `%v` prints value in default format 
  * `%+v` prints field names if the value is a struct
    
## if, else if and else
```
  if score > 3 {
    fmt.Printf("good")
  } else if score == 3 {
    fmt.Printf("may be")
  } else if score == 2 {
    fmt.Printf("meh...")
  } else {
    fmt.Printf("no")
  }
```

## Short IF; Simple statement; Short statement
* IF statement
  ```
    num,err := strconv.Atoi("33")
    if err != nil {
      fmt.Println(err)
    }
  ```  
* Short IF statement
    ```
    if num,err := strconv.Atoi("33"); err != nil {
      fmt.Println(err)
    }
    ```
    
## Shadowing
* if you declare a variable with same name (ex: `n` below) inside a inner scope (ex: `if` statement) as of variable in outer scope(`n` after `main`), variable inside inner scope will be shadowing outer scope variable. For example, below program should print: 10, but instead it prints: 0
```
func main() {
  var n int

  if n, err := strconv.Atoi("10"); err != nil {
    fmt.Printf("error: %s (n: %d)", err, n)
    return
  }

  fmt.Println(n)
}
```
* above shadowing problem can be solved by 
```
func main() {
  var n int
  var err error

  if n, err = strconv.Atoi("10"); err != nil {
    fmt.Printf("error: %s (n: %d)", err, n)
    return
  }

  fmt.Println(n)
}
```

## Switch statement
* Similar to IF statement with a different syntax
* case condition's type should match with switch condition's type
* switch statements are executed from top to bottom
```
city := "paris"
switch city {
case "paris", "Lyon":
  fmt.Println("France")
case "London":
  fmt.Println("UK")
default:
  fmt.Println("Unknown")
}
```
* `fallthrough` statement executes next clause without checking for it's condition
```
i := 194

switch {
case i > 100:
  fmt.Printf("big ")
  fallthrough
case i > 0:
  fmt.Printf("positive ")
  fallthrough
default:
  fmt.Println("number")
} // prints `big positive number`
```

## FOR loop
* executes a block of code as long as it's condition is true

```
for i := 1; i <= 5; i++ { // i := --> init statement, i <= 5 --> condition, i++ --> post statement
  sum += i
}
```
OR
```
for i < 5 {
  sum += i
  i++
}
```
* Below is an **infinite** loop
```
for {
  sum += i
  i++
}
```

**break** statement: once i > 5 condition is true, execution breaks out of for loop
```
for {
  if i > 5 {
    break
  }
  sum += i
  i++
}
```

**continue** statememt: if i % 2 is non-zero, loop skips rest of the current step
```
for {
  if i > 5 {
    break
  }
  
  if i % 2 != 0 {
    i++
    continue
  }
  
  sum += i
  i++
}
```

**Nested loop** to print multiplication table:
```
func main() {
	fmt.Printf("%5s", "X") // Prints X after 4 spaces (right alinged)
	for i := 0; i <= 5; i++ {  // To print 0 to 5 in the same line as X so it completes row header with X 0 1 2 3 4 5
		fmt.Printf("%5d", i) 
	}
	fmt.Println()  // Print new line
	for i := 0; i <= 5; i++ {   // To print column header 
		fmt.Printf("%5d", i)
		for j := 0; j <= 5; j++ { // To print multiplication value for each position in the same line as of current i value
			fmt.Printf("%5d", i*j)
		}
		fmt.Println() // Go to next line after printing table for each i value
	}
}
```

OUTPUT for above code:
```
    X    0    1    2    3    4    5
    0    0    0    0    0    0    0
    1    0    1    2    3    4    5
    2    0    2    4    6    8   10
    3    0    3    6    9   12   15
    4    0    4    8   12   16   20
    5    0    5   10   15   20   25
```

**range clause** to loop over slice of values
```
s := "lazy cat jumps over the fence again and again" 
words := strings.Fields(s) // strings.Fields function returns []slice
for i,v := range words {
  fmt.Printf("#%-2d: %q", i+1, v)
}

```
OUTPUT for above code:
```
#1 : "lazy"
#2 : "cat"
#3 : "jumps"
#4 : "over"
#5 : "the"
#6 : "fence"
#7 : "again"
#8 : "and"
#9 : "again"
```

## Arrays
Collection of elements: **Indexable** and **Fixed** length.
Array stores elements in contiguous memory cells.
Array's type belongs to **compile-time**
Length of an array is **part of it's type** ex: [2]string, [5]byte,[3]int etc

Examples:

* var age [2]byte // [2] is the length of the array; byte is element type of the array
* create and initialize
```
var books = [4]string{
  "one",
  "two",
  "three",
  "four",
}
```
* use ELLIPSIS operator to find the length of the array automatically. For below,length of the array is **[3]string**
```
[...]string{"hi", "hello", "howdy"}
``` 

**Multi-dimensional arrays**

<img src="https://user-images.githubusercontent.com/67871237/173247734-06bbeeef-e504-4aea-a152-9e71c7340b6e.png" width="400" height="300">

* declaring and initializing multi-dimensional array. Here **[2]** is the length of the array and **[3]int** is the element type of the array
```
[2][3] int {
  {5,6,1},
  {9,8,4},
}
```

# Packages

## path 
* `dir, file := path.Split("/home/myfile")` result: `dir = home/` and `file=myfile`
* utility routines for manipulating slash-separated paths
  * `func Ext(path string) string`
  * `func Join(elem ...string) string`
  * `func Match(pattern, name string) (matched bool, err error)`
  * `func Split(path string) (dir, file string)` 

## os 
* `os.Args` is []string (slice of strings) which stores command-line arguments
* `go run main.go hello` will result in `os.Args[0] = /home/myscripts/main.go` (os.Args[0] is a path to the main.go)  and `os.Args[1] = "hello"`
* command-line arguments stored in `os.Args` are always `string` type so convert them appropriately if you want to use it as another type. For example, running `myscript.go 100` will result in os.Args[1] value as "100", which is a string so if you want to use it as an interger, convert it into int from string via `strconv.Atoi(os.Args[1])`

## unicode/utf8

* **RuneCountInString:** `len` function returns number of **bytes** in a string, instead of number of **characters**. For example, `len("hello")` returns 5 as the characters are english characters and each char occupy only 1byte. But it becomes obvious for non-english characters as some of those characters occupy more than one byte. So to find out the length of a string, use `utf8.RuneCountInString("hello")` instead of `len("hello")`
  
  

