# ipname

hostnames for all

**DNS**: `ipname.me`

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
thisisnotarealdomain.tld ---> 116.203.115.192
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
116.203.115.192
```

## who it works

dnsdist supports Lua, so we can use string.match for our pattern matching.

```lua
string.match(reply, "%d+%.%d+%.%d+%.%d+")
```

The entire configuration is about 12lines !!! You can check it here: [dnsdist.conf](dnsdist.conf)

*Disclaimer*: This is not an IPv4 pattern matching, but works as proof of concept

## mentions

inspired by [xip.io](http://xip.io) & [ifconfig.co](https://ifconfig.co)

Powered by [dnsdist](https://dnsdist.org/) & [lua](https://www.lua.org)

## footnote

This is only for **testing** purposes, do not use it for production service.
