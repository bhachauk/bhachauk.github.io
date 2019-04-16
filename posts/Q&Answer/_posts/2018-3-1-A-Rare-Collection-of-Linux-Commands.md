---
layout: qanda
---

##### How to do simple chat in Linux with TCP-IP ?
{: .qandaq}

 - netcat
 - telnet
 
##### Steps :

1. Initiate <mark>netcat</mark> in a logical Port of Machine A

```
    nc -l 10000
``` 
 
 Here 10000 is a logical Port. You can assign <mark>2 ^ 16</mark> Ports. But some are default ports already.
 This means the service started over network on the port. A normal <mark>man nc</mark> briefs about it.
 
2. Now Connect using <mark>Telnet</mark> from the Machine B (or) local machine (Machine A):

- From another Machine like said (Machine B)

``` 
#telnet ip 10000
telnet localhost 10000
```

A simple TCP/IP Session has been implemented in a logical port and can read/write (Means Normal chat :)).
