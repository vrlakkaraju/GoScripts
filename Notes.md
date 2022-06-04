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
  * `var (
       speed int = 10
       heat float64 = 31.5
       off bool = true
       brand string = "famous"
  )`
* Zero values and Short declaration 
  * ` booleans --> false`
     `numerics --> 0`
     `strings --> ""`
     `pointers --> nil`
  * `safe := true` [NOTE: can't be used at the package scope, works only at the block scope]  



# Packages

## path 
* utility routines for manipulating slash-separated paths
  * `func Ext(path string) string`
  * `func Join(elem ...string) string`
  * `func Match(pattern, name string) (matched bool, err error)`
  * `func Split(path string) (dir, file string)` 
