# Shortcuts - Writeup
### Description
```
A web app for those who are too lazy to SSH in.

http://web1.cybercastors.com:14437
```

## Cracking
- #### Us going to website, we just see a webpage with some ASCII art.
![castorsCTF](https://i.imgur.com/9I9xuTO.png)
- #### Looking at the source reveals that there is one endpoint in the website called `/list`
![castorsCTF](https://i.imgur.com/e7WHUEv.png)
- #### Going to the endpoint we see that we can upload some files so this should be RCE (Remote Code Execution)
![castorsCTF](https://i.imgur.com/YqB8UZo.png)
- #### My friends and I got to know by going to some files on this endpoint that this is related to Golang and we *probably* have Remote Code Execution. So I just wrote a little code in go which would let us execute system commands.

#### grep.go
```go
package main

import (
    "fmt"
    "os/exec"
)

func main() {
    out, _ := exec.Command("ls",  "/home").Output()
    fmt.Println(string(out))
}
```

[This checks the users on this system]

- #### Running this gives us

![castorsCTF](https://i.imgur.com/lPKGowP.png)
 - #### Now `lsing` into the home gives us some saucy stuff.
 ![castorsCTF](https://i.imgur.com/HkDUhxf.png)
 - #### Now we just use the `cat` command to get the flag.
 ![castorsCTF](https://i.imgur.com/Gigdrpn.png)
