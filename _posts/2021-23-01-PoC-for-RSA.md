---
title: Mathematical Proof of RSA CryptoSystem!
published: true
## [](#header-3)Before Start

I present my sincere love to N.I.H.O. for giving me the motivation to write this article. Another thanks will be to Academician Umut Kuran. He is the best computer scientist I know. He is also a very good mathematician. I'm grateful for everything he did for me

## [](#header-3)What is RSA Encryption? (Wikipedia)

RSA (Rivest–Shamir–Adleman) is a public-key cryptosystem that is widely used for secure data transmission. It is also one of the oldest. The acronym RSA comes from the surnames of Ron Rivest, Adi Shamir, and Leonard Adleman, who publicly described the algorithm in 1977. An equivalent system was developed secretly, in 1973 at GCHQ (the British signals intelligence agency), by the English mathematician Clifford Cocks. That system was declassified in 1997

In a public-key cryptosystem, the encryption key is public and distinct from the decryption key, which is kept secret (private). An RSA user creates and publishes a public key based on two large prime numbers, along with an auxiliary value. The prime numbers are kept secret. Messages can be encrypted by anyone, via the public key, but can only be decoded by someone who knows the prime numbers

![](https://hackernoon.com/hn-images/1*yNPjtfBw0UIXXiSBo6CfDw.png)

* Used in many digital certificates on the Internet.
* The most popular are asymmetric crypto structures.
* Used for small data transfer such as key transfer

As mentioned in the article, two prime numbers are needed for encryption.

## [](#header-3)RSA Encryption Proof

Actually so basic:

Decoding should be the opposite of encoding.

* dk  = decoding key
* ek  = encoding key
* pr  = private
* pub = public


suppose that dkpr(ekpub(x)) = x 

Let's create the rule between public and private keys.

```js
d.e = 1 mod(∮(n))
```
mod∮(n) in that case
```js
d.e = 1 + t ∮(n) 
```
```js
dkpr(y) = x^de = x^1+t∮(n) == (x^∮(n))^t.x(modn)
```
on more solid foundations

```js
gcd(x,n) = >>> because of the houses theorem x^∮(n) == 1(modn)
```
```js
dkpr^(y) = (x^∮(n))^t.x = 1^t.x == x(modn)
```

```js
$ sudo yum install mod_security
$ sudo /etc/init.d/httpd restart
```
After installing the packages, we will need to configure several configurations for the firewall to function properly. I'll use Apache as a web service that will explain the Debian operating system today.

After the installation is complete we will start apache2

```js
$ service apache2 restart
```
Then let's check our required module with apachectl (a checking tool for HTTP Service).

```js
$ apachectl -M |grep security 
```
![](https://2.bp.blogspot.com/-01JmGsc3Pvw/XAUMkRj_YqI/AAAAAAAAA2c/ZBvgUnAK2_cJ2OYK8e3IBxAf7wf_vHcXACLcBGAs/s1600/Ekran%2BResmi%2B2018-12-03%2B13.59.13.png)

**security2_module(shared)** Next we'll make a few changes to our pre-defined configuration file

```js
$ mv /etc/modsecurity/modsecurity.conf{-recommended,}
```
We make the name of our configuration file **modsecurity.conf** then open it with our nano editor.

We will make arrangements in 2 rule engines

#### [](#header-3)SecRuleEngine

It is one of the rule engines of the firewall and takes 3 different parameters.

* On  -- ( work)
* Off -- (not work)
* DetectionOnly -- (work but no block)

##### [](#header-3)SecResponseEngine

A quality resource written in 2007 is written off by default. I don't know how long it's been, but now it's open by default and it's used to buffer the answers, analyze them or not. It takes 2 different parameters.


* On  -- ( work)
* Off -- (not work)

We find the line that is **SecRuleEngine** and switch from **DetectionOnly** to **On**
Download now **SecResponseBodyAccess** opening **On** mode **Off** taking.

Adjusting the size of the data to be retrieved by POST method.

We are restarting our Apache service.


```js
$ service apache2 restart
```

Immediately thereafter, the log file called **modsec_audit.log** should be created under **/var/log/apache2/** where modsecurity records the traffic that is listening.

![](https://1.bp.blogspot.com/-8JHg7YdIQl8/XAUSG02pwAI/AAAAAAAAA2o/IjzoMENkixgbLTKK8dQJA4karzO_HvA2ACLcBGAs/s1600/Ekran%2BResmi%2B2018-12-03%2B14.22.48.png)

Now I'm going to create a php file with security vulnerabilities and then send a payload to the web service to see if it works.

###### [](#header-4)Vulnerability PHP File

```php
<?php 
$xss = $_GET['a'] 
echo $xss; 
?>
```
We understand from the code is a very simple Cross Site Scripting (XSS) vulnerability. HTTP GET will retrieve the data from the "a" input that comes with the request and print it to the screen.

![](https://4.bp.blogspot.com/-gBaFiQ3GE90/XAUUZ3c5j5I/AAAAAAAAA20/4Nx6qPrPiSwEKnX0X2igtkisxAre_pBogCLcBGAs/s1600/Ekran%2BResmi%2B2018-12-03%2B14.32.44.png)

Now let's send a simple XSS payload 

```php
<script>alert(1)</script>.
```


![](https://3.bp.blogspot.com/-lf_Ry_yI_TI/XAUVAmzKmhI/AAAAAAAAA28/vVgk2szOv3Q6Tq65azKZ4E-dHXeh0qklQCLcBGAs/s1600/Ekran%2BResmi%2B2018-12-03%2B14.35.19.png)

The log file on the back, where modsecurity records the traffic, understands that the incoming request has the code under **/usr/share/modsecurity/** rules, which detects harmful javascript code to exploit XSS vulnerability, and prevents it by returning 403 responses to the request.

Before moving on to the rule writing phase, I go around the directory where there are some rules and try to understand the event.

![](https://1.bp.blogspot.com/-5ZGrONY-KDY/XAUXBlXmjXI/AAAAAAAAA3I/LA74_Pv6XpgS2SyEvj7ajaWjpBEs6wBOgCLcBGAs/s1600/Ekran%2BResmi%2B2018-12-03%2B14.43.45.png)

I see that there are two different file types: .conf and .data under **/usr/share/modsecurity-crs/rules**.

There are payload lists in the .data files so that the rule files do not take up much space due to their vulnerability. For example, in the configuration file related to Response and SQL Injection, the anomaly of sqli weakness should be corrupted if the error is based on the screen, while the payload file, ie, sql-response.data file, if something catches the response is blocking.

Example: **You have an error in sql syntax - mysql error vs**

In a way, it does the job of including payloads in the conf file in another file.

###### [](#header-2)Rules

Detailed coming soon

Follow me with twitter @berkdusunur
