# My Golang notes 

* To intialize a module 
  * `go mod mymodule`

* To download all required packages (to add module requirements and sums) 
  * `go mod tidy`

* To run a script witout building it
  * `go run myscript.go`

* To build a package with a specific name (-o option)
  * `go build -o myscript`







# Packages

## path 
* utility routines for manipulating slash-separated paths
  * `func Ext(path string) string`
  * `func Join(elem ...string) string`
  * `func Match(pattern, name string) (matched bool, err error)`
  * `func Split(path string) (dir, file string)` 
