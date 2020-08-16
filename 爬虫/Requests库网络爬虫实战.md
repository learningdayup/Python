---
Requests库网络爬虫实战
---

## 目录
1.京东商品页面的爬取
2.亚马逊商品页面的爬取
3.百度/360搜索关键词提交
4.网络图片的爬取和存储
5.IP地址归属地的自动查询

## 1.京东商品页面的爬取

```
import requests

url = 'https://item.jd.com/2967929.html'
try:
    r = requests.get(url)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[:1000])
except:
    print('爬取失败')
```


## 2.亚马逊商品页面的爬取

```
import requests

url = 'https://www.amazon.cn/gp/product/B01M8L5Z3Y'
try:
    kv = {'user-agent': 'Mozilla/5.0'}
    r = requests.get(url, headers = kv)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[1000:2000])
except:
    print('爬取失败')
```

## 3.百度/360搜索关键词提交

百度
```
import requests

keyword = 'Python'
url = 'https://www.baidu.com/s'
try:
    kv = {'wd': keyword}
    r = requests.get(url, params = kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text))
except:
    print('爬取失败')
```

360
```
import requests

keyword = 'Python'
url = 'https://www.so.com/s'
try:
    kv = {'q': keyword}
    r = requests.get(url, params = kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text))
except:
    print('爬取失败')
```


## 4.网络图片的爬取和存储


```

import requests
import os

url = 'https://image.nationalgeograpgic.com.cn/2017/0211/20170211061910157.jpg'
root = "D://pics//"
path = root + url.split('/')[-1]
try:
    if not os.path.exists(root):
        os.mkdir(root)
    if not os.path.exists(path):
        r = requests.get(url)
        with open(path, 'wb') as f:
            f.write(r.content)
            f.close()
            print("文件保存成功")
    else:
        print("文件已存在")
except:
    print('爬取失败')
```


## 5.IP地址归属地的自动查询

```
import requests

url = 'https://m.ip138.com/ip.asp?ip='
try:
    r = requests.get(url + '202.204.80.112')
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[-500:])
except:
    print('爬取失败')
```

