# Homework for lections 5-6
## Task 1
#### What is the most frequent browser?

``` 
[student1@localhost ~]$ cat scriptAwk
#! /bin/awk -f
BEGIN {
FS="\""
}
{
++requests[$6]
}
END{
maxReq=0;
for(brows in requests)
        if(requests[brows] > maxReq){
                maxReq=requests[brows]
                comBrows=brows}
print comBrows, " - ", maxReq, " req."
}
[student1@localhost ~]$ ~/scriptAwk access.logr
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0)  -  340874  req.
```

With that script one can figure out, that the most common browser is "Internet Explorer 7 on Windows Vista" (according to https://developers.whatismybrowser.com/useragents/).

---

## Task 2
#### Show number of requests per month for ip 216.244.66.230.

```
[student1@localhost ~]$ cat ~/hw3t2/scriptAwk
#! /bin/awk -f
BEGIN {FS="/"}

$1~/216.244.66.230/ {
 date = substr($3,1,4)" "$2
 ++requests[date]
}
END{
 for(date in requests)
  print date, "-", requests[date]," req."
}

[student1@localhost ~]$ ~/hw3t2/scriptAwk_v2 access.logr | sort -k1g -k2M
2020 Dec - 1  req.
2021 Jan - 43  req.
2021 Feb - 14  req.
2021 Mar - 2  req.
2021 Apr - 34  req.
2021 May - 27  req.
2021 Jun - 3  req.
2021 Jul - 23  req.
2021 Aug - 108  req.
2021 Sep - 7  req.
2021 Oct - 23  req.
2021 Nov - 106  req.
2021 Dec - 5  req.
```
---

## Task 3
#### Show total amount of data which server has provided for each unique ip.

```
[student1@localhost ~]$ cat ~/hw3t3/scriptAwk
#! /bin/awk -f
{
ARRAY[$1]+=$10}

END{
for(i in ARRAY)
        print ARRAY[i], "bytes for ", i
}   

[student1@localhost ~]$ ~/hw3t3/scriptAwk access.log.2
...
11863 bytes for  5.183.60.18
81982479 bytes for  157.33.1.197
24897504 bytes for  73.45.141.120
13020 bytes for  204.15.145.39
10184644 bytes for  157.55.39.148
34198293 bytes for  159.89.187.19
10466 bytes for  94.154.220.93
26209910 bytes for  145.253.118.26
...

```
I've printed only few of output lines just to show that the script works correctly.

---

## Task 4
#### Change all browsers to "lynx"

```
[student1@localhost ~]$ sed -r 's/(Mozilla|Safari|Opera|Firefox|Edge|OPR|Chrome|Puffin|UCBrowser|YaBrowser|SamsungBrowser|360Spider)/lynx/gi' ~/access.log
45.132.51.36 - - [22/Dec/2020:03:19:30 +0100] "POST /index.php?option=com_contact&view=contact&id=1 HTTP/1.1" 200 188 "-" "lynx/5.0(Linux;Android8.1.0;LenovoTB-X304F)AppleWebKit/537.36(KHTML,likeGecko)lynx/85.0.4183.81lynx/537.36" "-"
45.132.51.36 - - [22/Dec/2020:03:19:55 +0100] "GET /index.php?option=com_contact&view=contact&id=1 HTTP/1.1" 200 9873 "-" "lynx/5.0(Macintosh;IntelMacOSX10_15_6)AppleWebKit/537.36(KHTML,likeGecko)lynx/85.0.4183.83lynx/537.36" "-"
45.132.51.36 - - [22/Dec/2020:03:19:55 +0100] "POST /index.php?option=com_contact&view=contact&id=1 HTTP/1.1" 200 188 "-" "lynx/5.0(Macintosh;IntelMacOSX10_15_6)AppleWebKit/537.36(KHTML,likeGecko)lynx/85.0.4183.83lynx/537.36" "-"```
```
I've printed only few of output lines just to show that the script works correctly.

---

## Task 5
#### Masquerade all ip addresses. Rewrite file.

```
[student1@localhost ~]$ sed -i -r 's/([0-9]{1,3}\.){3}[0-9]{1,3}/lynx/' ~/access.log.2
...
lynx - - [23/Dec/2020:06:35:52 +0100] "GET /index.php?option=com_contact&view=contact&id=1 HTTP/1.1" 200 9873 "-" "Mozilla/5.0(Linux;Android10;SM-M205FN)AppleWebKit/537.36(KHTML,likeGecko)Chrome/85.0.4183.81MobileSafari/537.36" "-"
lynx - - [23/Dec/2020:06:35:58 +0100] "POST /index.php?option=com_contact&view=contact&id=1 HTTP/1.1" 200 188 "-" "Mozilla/5.0(Linux;Android10;SM-M205FN)AppleWebKit/537.36(KHTML,likeGecko)Chrome/85.0.4183.81MobileSafari/537.36" "-"
lynx - - [23/Dec/2020:06:36:26 +0100] "GET /index.php?option=com_contact&view=contact&id=1 HTTP/1.1" 200 9873 "-" "Mozilla/5.0(Linux;Android10;HRY-LX1)AppleWebKit/537.36(KHTML,likeGecko)Chrome/85.0.4183.81MobileSafari/537.36" "-"
lynx - - [23/Dec/2020:06:36:27 +0100] "POST /index.php?option=com_contact&view=contact&id=1 HTTP/1.1" 200 188 "-" "Mozilla/5.0(Linux;Android10;HRY-LX1)AppleWebKit/537.36(KHTML,likeGecko)Chrome/85.0.4183.81MobileSafari/537.36" "-"
...
```
