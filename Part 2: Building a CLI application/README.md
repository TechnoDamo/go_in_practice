This part covers:
- CMD flags, options, and arguments
- Passing configuration into application
- Starting and gracefully stoping a web server
- Path routing for web and I servers
# Bulding CLI app
The Go standard library has built-in functionality forworking with command-line arguments and flags.
## Command-line flags
*Argument and flag handling in the Go standard lbrary is based on [Plan 9](https://en.wikipedia.org/wiki/Plan_9_from_Bell_Labs), which has a different style from the GNU/Linus based systems.* <br/>
<br/>

```go
// Go style
program -verbose -output file.txt -count 5 arg1 arg2

// vs GNU style  
program --verbose --output=file.txt --count=5 arg1 arg2
```

### Key differences
1. **Long options**
Go treats short flags (-la) the same as long ones (--la).
2. **Value assignment**
(-file name) instead of (--file=name) or (--file name)
3. **Combined shortoptions**
The Go flag system does not let to combine multiple flags (-la wouldbe one single flag). <br/>

There are two ways of defining a flag.
```go
// Method 1: Define flags and get pointers to their values
// flag.Type(name, default, description) returns *Type
portPtr := flag.Int("port", 8080, "port number for the server")
hostPtr := flag.String("host", "localhost", "host address for the server")
debugPtr := flag.Bool("debug", false, "enable debug mode")
    
// Method 2: Bind flags to existing variables (more common in real applications)
// flag.TypeVar(&variable, name, default, description)
var cfg Config
    
flag.IntVar(&cfg.Port, "port", 8080, "port number for the server")
flag.StringVar(&cfg.Host, "host", "localhost", "host address for the server") 
flag.BoolVar(&cfg.Debug, "debug", false, "enable debug mode")
flag.StringVar(&cfg.DataDir, "data-dir", "./data", "directory for data files")

flag.Parse() // parse cmd args
```
flag.Parse() runs through flags in the order of declaration and latest values of the same flag overwrite previous ones. <br/><br/>
Common useful flag package methods:
- **VisitAll()** - inspect all defined flags.
- **PrintDefaults()** - Show flag for help.
- **Args()** - Get positional arguments (all after flags)
## Defining valid values via enums
## Slices, arrays and maps
## Command-line frameworks
# Handling configuration
# Working with the real-world web servers