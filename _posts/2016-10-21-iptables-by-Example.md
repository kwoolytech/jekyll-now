---
layout: post
title: iptables by Example
---

I got brand new Raspberry Pi3 and have decided to make it as a WiFi Access Point.
While I configuring it, I got a decent use case example for iptables.

Suppose we have a WiFi interface, ```wlan0``` and an interface for Internet, ```eth0```. 
Obviously we need a routing. Packets that were received on ```wlan0``` needs to be forwarded to ```eth0```, vice and versa.

Here is configuration that does the job.

> sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
  sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
  sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT  
  
Before we translate those foreign languages to natural word, we need to get familiar with some terms.
  
## Table
 - ```filter```
 - ```nat```
 - ```mangle```
 - ```raw```
 
## Chain
 - ```INPUT``` : All the packets that a host receives.
 - ```OUTPUT``` : All the packets that a host transmits.
 - ```FORWARD``` : All the packets that does not destine to a host. 
 - ```POSTROUTING``` 

## Match
 - ```--source```(-s)
 - ```--destination```(-d) 
 - ```--protocol```(-p)
 - ```--in-interface```(-i)
 - ```--out-interface```(-o)
 - ```--table```(-t)
 - ```--match```(-m)
 - ```--jump```(-j)
 - ```--syn```(-y)
 - ```--fragment```(-f)
 - ```--state```
 - ```--string```
 - ```--comment```

## Target
 - ```ACCEPT```
 - ```DROP```
 - ```REJECT```
 - ```LOG```
 - ```RETURN```
 - ```MASQUERADE```
 
## Command
 - ```--append```(-A)
 - ```--delete```(-D) 
 - ```--check```(-C)
 - ```--replace```(-R)
 - ```--insert```(-I)
 - ```--list```(-L)
 - ```--flush```(-F)
 - ```--zero```(-Z)
 - ```--new```(-N)
 - ```--delete-chain```(-X)
 - ```--policy```(-P)
 
 
## sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
> In the NAT table, for the POSTROUTING chain, set MASQUERADE for the packets go outward the eth0.

## sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
> Append a ACCEPT rule for FORWARD packets that from eth0 to wlan0 if its state is either RELATED or ESTABLISHED.

## sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT  
> Append a ACCEPT rule for FORWARD packets that from wlan0 to eth0.