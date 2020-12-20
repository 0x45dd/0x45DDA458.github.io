---
title: DNS Amplification DDoS Attack
published: true
---
# [](#header-2)DNS

The Domain Name System (DNS) is a hierarchical decentralized naming system for computers, services, or other resources connected to the Internet or a private network. It associates various information with domain namesassigned to each of the participating entities

# [](#header-2)How to Work?


When I want to go to berk.red with my browser, the browser first asks me if i can translate berk.red address to me The system looks in the /etc/hosts directory. If there is an ip address on the berk.red domain it will use it. Otherwise it goes to the DNS resolver provided by DHCP. If not, it goes to the root server.



# [](#header-2)DNS INQUIRIES

By leaving the DNS recursion query on, you allow an attacker to use your DNS on your behalf. DNS Amplification attacks, a professional attack technique, attack by sending packets to you via a DNS server that is in your domain (If 1 DNS packet is 50 bytes, this packet will be returned in response to 10x ie 500 bytes).

Thus, the attacker will not only use your bandwidth, but at the same time will also provide his / her own privacy, creating the perception that the attacker is like you. How do we know if our DNS server is open for the recursion query?


You can learn in two shapes

1. If you want to check the settings of your DNS server

2. From the outside DNS server will do DNS Recursion query.


## [](#header-3)NMAP RECURSIVE INQUIRY

Using a script located in Nmap it helps to detect the weakness of the dns server 1 to get 10 Let's first scan the DNS server list that we found using this script of NMAP.


```js
// nmap scan command
nmap -sU -p 53 --script=dns-recursion -iL /file/path/for/dns-server-list
```
## [](#header-3)Saddam DNS Amplification Tool

Saddam is DDoS tool about,


  1. DNS Amplification (Domain Name System)
  2. NTP Amplification (Network Time Protocol)
  3. SNMP Amplification (Simple Network Management Protocol)
  4. SSDP Amplification (Simple Service Discovery Protocol)

  ```js
  // how to install
  git clone https://github.com/OffensivePython/Saddam.git
  ```

you need install pinject module

```js
// pinject install
git clone https://github.com/OffensivePython/Pinject.git
```
```js
// pinject install
cd Pinject && cp pinject.py ../Saddam
```

and we can use right now 

```js
//usage
python Saddam.py -h
```

With Saddam, you can set up dns recursive attacks and control your dns servers against amplification attacks.

We will just scan some DNS Server for learning. They are public servers

```js
//usage
Saddam git:(master) ✗ python Saddam.py benchmark -d dnsfile.txt:blablablabla.com
	   _____           __    __
	  / ___/____ _____/ /___/ /___ _____ ___
	  \__ \/ __ `/ __  / __  / __ `/ __ `__ \
	 ___/ / /_/ / /_/ / /_/ / /_/ / / / / / /
	/____/\__,_/\__,_/\__,_/\__,_/_/ /_/ /_/
	https://github.com/OffensivePython/Saddam
	   https://twitter.com/OffensivePython

Protocol|  IP  Address  |     Amplification     |     Domain
---------------------------------------------------------------------------
  dns   | 195.29.106.21 |   5x (45B -> 229B)    |blablablabla.com
  dns   |211.193.163.251|   4x (45B -> 223B)    |blablablabla.com
  dns   |208.67.220.220 |   4x (45B -> 191B)    |blablablabla.com
  dns   | 150.7.186.254 |   5x (45B -> 267B)    |blablablabla.com
  dns   |213.61.185.238 |   4x (45B -> 180B)    |blablablabla.com
  dns   | 112.171.51.19 |   5x (45B -> 255B)    |blablablabla.com
  dns   | 95.174.99.75  |   4x (45B -> 191B)    |blablablabla.com
  dns   | 115.21.26.101 |   5x (45B -> 255B)    |blablablabla.com
  dns   | 54.39.198.39  |    1x (45B -> 45B)    |blablablabla.com
  dns   | 104.194.9.10  |    1x (45B -> 45B)    |blablablabla.com
  dns   |192.185.235.10 |   3x (45B -> 143B)    |blablablabla.com
  dns   |162.241.243.198|    1x (45B -> 45B)    |blablablabla.com
Total tested: 19
```
Follow me with twitter @berkdusunur
