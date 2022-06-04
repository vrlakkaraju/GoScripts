# My Golang notes 

* To intialize a module 
  * `go mod mymodule`

* To download all required packages (to add module requirements and sums) 
  * `go mod tidy`

* To run a script witout building it
  * `go run myscript.go`

* To build a package with a specific name (-o option)
  * `go build -o myscript`


# Variables

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



# Raw string literal
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

## unicode/utf8

* **RuneCountInString:** `len` function returns number of **bytes** in a string, instead of number of **characters**. For example, `len("hello")` returns 5 as the characters are english characters and each char occupy only 1byte. But it becomes obvious for non-english characters as some of those characters occupy more than one byte. So to find out the length of a string, use `utf8.RuneCountInString("hello")` instead of `len("hello")`
  
  
