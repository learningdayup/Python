---
Requests库入门
---

## 目录
1.简单例子——访问百度
2.reques库的主要方法
3.requests库的异常
4.爬取网页的通用代码框架
5.HTTP协议


## 1.简单例子——访问百度

```
import requests

r = requests.get('http://www.baidu.com') # 访问百度
print(r.status_code)  #访问状态码 ，200 表示成功

r.encoding = 'utf-8'  #更改编码为utf-8
print(r.text)   #打印网络内容
print(r.headers)   #返回get请求获得页面的头部信息
# 如果header中不存在charset，则认为编码为ISO-8859-1

```


2.requests库学习
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019102114062918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1hCX3BsZWFzZQ==,size_16,color_FFFFFF,t_70)


**2.1 requests.request()**

requests.request(method, url, **kwargs)

method：请求方式，对应get/put/post等7种
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021150720170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1hCX3BsZWFzZQ==,size_16,color_FFFFFF,t_70)
url：拟获取页面的url链接

**kwargs：控制访问的参数，共13个
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021150958757.png)
```
kv = {'k1':'v1', 'k2':'v2'}
r = requests.request('GET', 'http://httpbin.org/post', params = kv)
print(r.url)  #http://httpbin.org/post?k1=v1&k2=v2
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021151300797.png)
```
kv = {'k1':'v1', 'k2':'v2'}
r = requests.request('POST', 'http://httpbin.org/post', data = kv)
body = '主体内容'
r = requests.request('POST', 'http://httpbin.org/post', data = body)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021151524927.png)
```
kv = {'k1':'v1'}
r = requests.request('POST', 'http://httpbin.org/post', json = kv)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021151700915.png)
```
hd = {'user-agent':'Chrome/10'}
r = requests.request('POST', 'http://httpbin.org/post', headers = hd)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021152220858.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021152258552.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021152312196.png)
```
fs = {'file':'open('data.xls', 'rb')}
r = requests.request('POST', 'http://httpbin.org/post', files = fs)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019102115250141.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021152513541.png)
```
pxs = {'http':'http://user:pass@10.10.10.1:1234'
		'https':'https://10.10.10.1:4321'}
r = requests.request('GET','http://www.baidu.com'. proxies = pxs)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021153443543.png)

**2.2 requests.get()**

```r = requests.get(url, params = None, **kwargs)```

构造一个向服务器请求资源的Request对象；
返回一个包含服务器资源的Response对象，包含爬虫返回的内容。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021141917544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1hCX3BsZWFzZQ==,size_16,color_FFFFFF,t_70)

url：拟获取页面的url链接；
params：url中的额外参数，字典或字节流格式，可选；
**kwargs：12个控制访问的参数


**2.3 requests.head()**


requests.head(url, **kwargs)
url：拟获取页面的url链接；
**kwargs：13个控制访问的参数

```
r = requests.head('http://httpbin.org/get')
print(r.headers)
print(r.text)  #空
```

**2.4 requests.post()**

requests.post(url, data = None, json = None, **kwargs)

url：拟获取页面的url链接；
data：字典、字节序列或文件，Request的内容
json：JSON格式的数据，Request的内容
**kwargs：11个控制访问的参数
```
payload = {'k1':'v1', 'k2':'v2'}
r = requests.post('http://httpbin.org/post', data = payload)
print(r.text)  #自动编码为form（表单）


r = requests.post('http://httpbin.org/post', data = 'ABC')
print(r.text)  #自动编码为data
```


**2.5 requests.put()**

requests.put(url, data = None, **kwargs)
url：拟获取页面的url链接；
data：字典、字节序列或文件，Request的内容
**kwargs：12个控制访问的参数

```
payload = {'k1':'v1', 'k2':'v2'}
r = requests.post('http://httpbin.org/post', data = payload)
print(r.text)  #自动编码为form（表单）
```

**2.6 requests.patch()**

requests.patch(url, data = None, **kwargs)
url：拟获取页面的url链接；
data：字典、字节序列或文件，Request的内容
**kwargs：12个控制访问的参数


**2.7 requests.delete()**

requests.delete(url, **kwargs)
url：拟获取页面的url链接；
**kwargs：13个控制访问的参数


## 3.requests库的异常

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021142729601.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1hCX3BsZWFzZQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021142950108.png)

## 4.爬取网页的通用代码框架
```
import requests

def getHTMLText(url):
	try:
		r = requests.get(url, timeout = 30)
		r.raise_for_status()  #如果状态不是200，引发HTTPError异常
		r.encoding = r.apparent_encoding
		return r.text
	except:
		return "产生异常"

if __name__ == "__main__":
	url = "http://www.baidu.com"
	print(getHTMLText(url))
```


## 5.HTTP协议
HTTP，超文本传输协议。
它是一个基于“请求与响应”模式的、无状态的应用层协议。
HTTP协议采用URL作为定位网络资源的标识。

URL

URL是通过HTTP协议存取资源的Internet路径，一个URL对应一个数据资源。

格式 http://host[:port][path]
host：合法的Internet主机域名或IP地址
port：端口号，缺省端口为80
path：请求资源的路径


![在这里插入图片描述](https://img-blog.csdnimg.cn/2019102114464718.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1hCX3BsZWFzZQ==,size_16,color_FFFFFF,t_70)
理解PATCH和PUT的区别

假设URL位置有一组数据UserInfo，包括UserID、UserName等20个字段。
需求：用户修改了UserName，其他不变。

采用PATCH，仅向URL提交UserName的局部更新请求。
采用PUT，必须将所有20个字段一并提交到URL，未提交字段被删除。

PATCH的最主要好处：节省网络带宽


![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021145549926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1hCX3BsZWFzZQ==,size_16,color_FFFFFF,t_70)


