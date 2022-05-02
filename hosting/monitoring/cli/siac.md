---
description: Using the siac binary to perform host actions
---

# siac

## Using siac

```
siac [options]
```

```
siac [flags]
```



### Options

#### Available Commands:

```
  alerts      view daemon alerts
  consensus   Print the current state of consensus
  gateway     Perform gateway actions
  help        Help about any command
  host        Perform host actions
  hostdb      Interact with the renter's host database.
  json        provide a json dump of siad's current status
  miner       Perform miner actions
  profile     Start and stop profiles for the daemon
  ratelimit   set the global maxdownloadspeed and maxuploadspeed
  renter      Perform renter actions
  stack       Get current stack trace for the daemon
  stop        Stop the Sia daemon
  update      Update Sia
  utils       various utilities for working with Sia's types
  version     Print version information
  wallet      Perform wallet actions
```



#### Flags:

```
  -a, --addr string            Which host/port to communicate with 
                               (i.e. the host/port siad is listening on)
                               (default "localhost:9980")    
                                                   
  -s, --alert-suppress         Suppress siac alerts
  
      --apipassword string     The password for the API's http authentication 
      
  -h, --help                   Help for siac
  
  -d, --sia-directory string   Location of the sia directory
  
      --useragent string       The useragent used by siac to connect to the daemon's API (default "Sia-Agent")
 
  -v, --verbose                Display additional information
```



### Examples

Display host status:

```
siac host
```



Display a detailed itemization of earned coins and expected revenues:

```
siac host -v
```



Display current state of consensus:

```
siac consensus
```



Display help for a specific action:

```
siac host --help
```





Use `siac [command] --help` for more information about a command.
