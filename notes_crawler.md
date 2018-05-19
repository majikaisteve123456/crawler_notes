<h1>python爬虫入门简介</h1>

1. 掌握定向网络数据爬取和网页解析的基本能力
the website is the API
2. Requests Python第三方网络爬虫库   
   自动爬取HTML页面，自动网络请求提交
3. robots.txt 网络爬虫排除标准 “盗亦有道”

#Requests库的安装#
---
Requests   
简单、简洁 一行代码就能爬取  
安装Requests库  


>import requests  
>r=requests.get("http://www.baidud.com")  
>print(r.status_code)  
>r.enconding='utf-8'  
>print(r.text)  

![picture](picture\picture1.png)

r.status_code为200即表示为访问成功

#Requests库的get方法
---
r=requests.get(url)  
构造一个向服务器请求资源的Request对象  
返回一个包含服务器返回的相关资源的Response

requests.get(url,params=None，**kwargs)
url：拟获取页面的url链接
params:url中的额外参数，字典或字节流格式，可选  
**kwargs:12个控制访问的参数 

type(r):class 'requests.models.Response'

r.headers:返回get请求的页面的头部信息 

![picture2](picture\picture2.png)

1. if r.status_code =200
   可以使用r.text r.encoding r.apparent_encoding r.content 去解析
2. if r.status_code=404 or else
   某些原因出错导致异常

网络上的资源都有编码方式 r.enconding是从http头部的charset 字段获得的，如果含有该字段说明存储资源的服务器对资源编码是有要求的  
如果 header中不存在charset,则认为编码为ISO-8859-1

r.apparent_enconding:根据网页内容分析出的编码格式

#爬取网页的通用代码框架
---
通用代码框架：一组代码，可以准确可靠地爬取网页内容  
requests.get(url)不一定经常能够使用，网络连接有风险
![picture3](picture\picture3.png)

requests.ConnectionError 拒绝连接是指服务器的防火墙拒绝连接  

requests.TooManyRedirects 指访问的URL重定向的次数超过了Requests库的所要求的最大重定向次数

requests.ConnectTimeout 是指与远程服务器连接过程所发生的超时异常

requests.Timeout 是指发出URL请求到获得内容整个过程的异常。

![picture4](picture/picture4.png)   


##爬取网页的通用代码框架
>import requests  
>def getHTMLText(url)    
>>try:  
>>>r=
>
 



