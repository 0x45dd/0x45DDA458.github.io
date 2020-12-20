---
title: Development Metasploit Module After 0DAY
published: true
---

In this article I will tell you how to develop a 0day's metasploit module. Before writing Thank you to **Numan Türle (@numanturle)** for help on about ruby ​on rails

[Metasploit Module](https://www.exploit-db.com/exploits/46340).

## [](#header-2)Vulnerability
Vulnerability in a web application running on hardware, an input from a user caused a vulnerability in execution of a remote command execution.

This vulnerability affected 106 server

![](https://1.bp.blogspot.com/-ir01TF8xhQI/W99hBYdI3dI/AAAAAAAAA0g/vVuXG-aEiigo8hAVBHjNr0Si_sZf5ytoQCLcBGAs/s1600/Ekran%2BResmi%2B2018-11-05%2B00.12.01.png)


#### [](#header-3)Examples Request
![](https://4.bp.blogspot.com/-VWHDOqG0XXo/W99dnUp9POI/AAAAAAAAA0M/GaDHpIkObkI8Z3Pom14mFmBajLcKf4v5ACLcBGAs/s1600/Ekran%2BResmi%2B2018-11-04%2B23.58.56.png)

Usually this application is running on the server "8081" port. But when I do some research with shodan "50000" can work on ports such as "8080". **uploaddir** value causes remote command execution vulnerability.in 


##### [](#header-3)Example Response

![](https://1.bp.blogspot.com/-snJlS3EWS_4/W99du8koqAI/AAAAAAAAA0Q/RfXIEyIESmEftTwHRxJb_WYdlqqkRkK-ACLcBGAs/s1600/Ekran%2BResmi%2B2018-11-04%2B23.59.28.png)

The application works on **root** privileges. 

###### [](#header-2)Metasploit-Framework Modules Development

Before you start writing, you can benefit greatly from here.If we need to summarize the first picture, we mentioned that the msf module is remote and we will use http client. 

Then enter the author, platforms, date and arch values.if this vulnerability was remote code execution, we should have chosen ARCH_PHP. But I used ARCH_CMD for remote command execution

There is a point we need to pay attention to here.people often compare "remote code execution" and "remote command execution" vulnerabilities

[Exploit Development](https://www.offensive-security.com/metasploit-unleashed/exploit-development/).


![](https://4.bp.blogspot.com/-eFTL88WsI3w/W99hVxoPaeI/AAAAAAAAA0o/GpXEy87T9ZIwxosHfGkjDVJTeKGcGF-ggCLcBGAs/s1600/Ekran%2BResmi%2B2018-11-05%2B00.14.49.png)

If we need to summarize the first picture, we mentioned that the msf module is remote and we will use http client.



Then enter the author, platforms, date and arch values. There is a point we need to pay attention to here.People often compare "remote code execution" and "remote command execution" vulnerabilities.If this vulnerability was remote code execution, we should have chosen ARCH_PHP. 

![](https://1.bp.blogspot.com/-mV82zyO5tSY/W99j4FyP1nI/AAAAAAAAA00/XCWhpmSLqNwVoMAdvbTUImDY4kWgWiCMgCLcBGAs/s1600/Ekran%2BResmi%2B2018-11-05%2B00.25.40.png)

"if else" loop generated in response to  code in first lines. If response 200 and body / upload_tmp_dir / return vulnerable.

In the last lines we have specified the type of web request to be made "GET". Then the payload is entered with the "cmd" to the value that is the vulnerability. This payload gets backconnect with telnet.


![](https://1.bp.blogspot.com/-tucUey7Vxlo/W99oyAoyblI/AAAAAAAAA1A/05wcPM87ErMPXLBLg1ZQXoKygsQrUwDDACLcBGAs/s1600/DrLibrpWsAEHe4k.jpg-large.jpeg)


