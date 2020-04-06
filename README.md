# ipname

hostnames for all

* **DNS** Server: `ipname.me`
* site: https://www.ipname.me/

## description

This is a free public service that resolves any domain name to it's IP address.
If no IP Address in the hostname, then this dns service will reply with your IP Address
usage

```
    192.168.1.1.ipname.me ---> 192.168.1.1
foo.192.168.1.1.ipname.me ---> 192.168.1.1
www.192-168-1-1-ipname.me ---> 192.168.1.1
```

but

```
thisisnotarealdomain.tld ---> 116.202.176.26
```

## dig examples

```sh
$ dig +short @ipname.me 10.20.30.40
10.20.30.40

$ dig +short @ipname.me www.192.168.1.1
192.168.1.1

$ dig +short @ipname.me www.192-168-1-1-ipname.me
192.168.1.1

$ dig +short @ipname.me example-93.184.216.34-org
93.184.216.34
```

but

```sh
$ dig +short @ipname.me googleyahoo.com
116.202.176.26
```

## who it works

dnsdist supports Lua via **LuaJIT**, so we can use string.match for our pattern matching.

```lua
string.match(reply, "%d+%.%d+%.%d+%.%d+")
```

then we access the FFI library, which allows calling external C functions and using C data structures from pure Lua code. And with the help of [INET_PTON](http://man7.org/linux/man-pages/man3/inet_pton.3.html), we can validate the IPv4 from the hostname!

<br>
The entire configuration is about 42lines!!! You can check it here: [dnsdist.conf](dnsdist.conf)

*update*: 

## mentions

inspired by [xip.io](http://xip.io) & [ifconfig.co](https://ifconfig.co)

Powered by [dnsdist](https://dnsdist.org/) & [lua](https://www.lua.org)

## footnote

This is only for **testing** purposes, do not use it for production service.
