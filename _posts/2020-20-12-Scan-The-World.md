---
title: Scan The World!
published: true
---

# [](#header-2)What is .git Folder?

Git is a distributed version-control system for tracking changes in any set of files, originally designed for coordinating work among programmers cooperating on source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows. (Wikipedia)
In recent years, security researchers have seen that source code can be accessed with forgotten /.git repositories on applications.



## [](#header-2)Online Exam System

This system was recently used by my university. Do not be afraid! I only got 50 from the exam. We need be to ethical

**Vendor Homepage:** https://github.com/sunnygkp10/

**Software Link:** https://github.com/sunnygkp10/Online-Exam-System-.git

I cloned application in my local and we can start !

![](https://1.bp.blogspot.com/-C-dB-vFfFSI/XtuK14moucI/AAAAAAAAA9E/ctSHvjOdmh4ZmHX0WckU0LIQLUu-xuN9ACK4BGAYYCw/s1600/Screenshot%2B2020-06-06%2Bat%2B14.27.42.png)

In the picture above we have seen that the webapp has the registration form for students. We can start by analysis here.

![](https://4.bp.blogspot.com/-EmzEdQGsFgk/XtuLVVZhhJI/AAAAAAAAA9U/0E5Cj3akcrodV3gxC2MHRhBBf_6LtJdfACK4BGAYYCw/s1600/Screenshot%2B2020-06-06%2Bat%2B14.32.18.png)

WebApp get the user information in index.php file and send via POST method the signin.php file. I open the signin.php file.

![](https://1.bp.blogspot.com/-iJqW8fyhuEA/XtuLXJ0nKBI/AAAAAAAAA9c/Cl_-4K_81ewDFPdtFNBLO48WKxSU6DW9gCK4BGAYYCw/s1600/Screenshot%2B2020-06-06%2Bat%2B14.36.04.png)

In sing.php the content is as in the picture above. Before we look for vulnerability, let's look at what some of the functions that the developer uses.

**ucwords** =  capitalizes the first letter of each word.

**strtolower** = used to lower case all content in a variable.

**stripslashes** = function is used to clear the backslash (\) sign at a value

**addslashes** = A backslash is applied in front of special characters in a string, such as db queries.



These filters will be no solution for **Stored XSS** vulnerability. This is the first vuln we found. Then we will see how we can hijack the cookie of the admin.

After all these filters, the variables are queried below with insert into

```js
$q3=mysqli_query($con,"INSERT INTO user VALUES  ('$name' , '$gender' , '$college','$email' ,'$mob', '$password')");

```

Some mysql database versions reverse slash is not important. Also we can say this code affected **sql injection** vulnerability. BUT!

I am not recommended exploit sqli here. Database can be very stress because in the query here **"insert into"**

We registered web app, and  will be review the user panel

![](https://2.bp.blogspot.com/-xWqo3_BL8XM/XtuLY0XtygI/AAAAAAAAA9k/IMoA7a5zwE0lUpU98H3lzTZFloFlsHHhQCK4BGAYYCw/s1600/Screenshot%2B2020-06-06%2Bat%2B15.04.23.png)

Lets start analysis account.php file. Here have a **Reflected XSS**

```js
 <!--alert message-->
<?php if(@$_GET['w'])
{echo'<script>alert("'.@$_GET['w'].'");</script>';}
?>
<!--alert message end-->
```
sometimes it's so hard to understand the developer :(

![](https://2.bp.blogspot.com/-5k_7cjXT4Uw/XtuL2L5M66I/AAAAAAAAA98/Pw4vyeEhrIU2vbqxcLdm6ru5-9usu3jUwCK4BGAYYCw/s1600/Screenshot%2B2020-06-06%2Bat%2B15.09.24.png)

Start during exam **eid** value affected **union based sql inj**

I want to analysis at the dash.php file

![](https://4.bp.blogspot.com/-w7w-u39SwJg/XtuL36QXrWI/AAAAAAAAA-E/YB-XXzEtBak416sQHx7rskbty74w_RX1QCK4BGAYYCw/s1600/Screenshot%2B2020-06-06%2Bat%2B15.14.10.png)

Developer not check user. All user can be review dash.php file. Can we say this vulnerability **IDOR (insecure direct object references)**

![](https://2.bp.blogspot.com/-wmfiQv48bhA/XtuL5qkCa5I/AAAAAAAAA-M/oY-9DycV2sMeMGYdyNXKPese3oQcaUAeACK4BGAYYCw/s1600/Screenshot%2B2020-06-06%2Bat%2B15.16.31.png)

We started with basic web application. This first post for series. Thank you for reading

Follow me with twitter @berkdusunur
