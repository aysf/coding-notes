
# Installing Go

tested in Debian 10.
Execute these following lines on the terminal

```bash

# preparation
sudo apt update
sudo apt install curl

# choose version
version=1.17.4

# download go
curl -O https://dl.google.com/go/go$version.linux-amd64.tar.gz

# extract tarball
tar xfv go$version.linux-amd64.tar.gz
# note: x for extract, f for filename and v for verbose

# Recursively change the owner and group of this directory into root and move to /usr/local
sudo chown -R root:root ./go
sudo mv go /usr/local

# setting path
nano ~/.bashrc

# add the folling lines to .bashrc and save it
GOPATH=$HOME/work
PATH=$PATH:/usr/local/go/bin:$GOPATH/bin

# refresh by running
source ~/.bashrc

# testing
go version

```

alternatively, put the lines to file, say `installer.sh`, set the execute permission using `chmod +x` and run the script using `./installer.sh` or `bash installer.sh` or `sh installer.sh`

reference : https://www.digitalocean.com/community/tutorials/how-to-install-go-on-debian-10


# Learning Indicator

## Mastering Beginer to Advance of Go should be able to answer following these problems
1. What is Go Type Alias and give the example 
2. What is Go Channel and give the example
3. What is Go Routinne and give the example

## Answer

### 1 Go Type Alias

source:
 - https://www.youtube.com/watch?v=Vg603e9C-Vg
 - https://yourbasic.org/golang/type-alias/
 - https://medium.com/a-journey-with-go/go-aliases-simple-and-efficient-8506d93b079e

### 2 Go Channel

### 3 Go Routine




# Hello World from http

to create simple web apps to print "hello world" in the browser, you need to put this into `main.go` and run

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {

	http.HandleFunc("/hello", func(rw http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(rw, "Hello World")
	})

	fmt.Printf("server run on localhost:8000\n")
	if err := http.ListenAndServe(":8000", nil); err != nil {
		log.Fatal(err)
	}
}
```

golang concurency: goroutine in press keyboard

```
package main

import (
	"fmt"

	"github.com/eiannone/keyboard"
)

var char rune

func main() {
	fmt.Println("Press any key, or q to quit")

	_ = keyboard.Open()
	defer func() {
		keyboard.Close()
	}()

	for {
		char, _, _ = keyboard.GetSingleKey()
		if char == 'q' || char == 'Q' {
			break
		}
		listenForKeyPress()
	}

}

func listenForKeyPress() {
	fmt.Println("you pressed", string(char))
}
```


https://tecadmin.net/install-go-on-linuxmint/

# Bookmark
- https://stackoverflow.com/questions/34190170/go-interface-method-returning-interface-doesnt-match-method-returning-concrete
