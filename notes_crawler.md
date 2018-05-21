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


![picture](https://github.com/majikaisteve123456/crawler_notes/blob/master/picture1.png?raw=true)

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



![picture2](https://github.com/majikaisteve123456/crawler_notes/blob/master/picture2.png?raw=true)

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



![picture3](https://github.com/majikaisteve123456/crawler_notes/blob/master/picture3.png?raw=true)

requests.ConnectionError 拒绝连接是指服务器的防火墙拒绝连接  

requests.TooManyRedirects 指访问的URL重定向的次数超过了Requests库的所要求的最大重定向次数

requests.ConnectTimeout 是指与远程服务器连接过程所发生的超时异常

requests.Timeout 是指发出URL请求到获得内容整个过程的异常。

![picture4](https://github.com/majikaisteve123456/crawler_notes/blob/master/picture4.png?raw=true)   


##爬取网页的通用代码框架  
	import requests
    def getHtmlText(url):
        try:  
			r=requests.get(url,timeout=30)  
            r.raise_for_status()#如果状态不是200，引发HTTPError异常  
            r.encoding=r.apparent_encongding
            return r.text
         except:  
            return "产生异常"    

 上述代码中r.encoding=r.apparent_enconding使代码解码正确  
使用上述代码框架是用户爬取更加稳定  

#HTTP协议及Requests库的方法  
---
HTTP 超文本传输协议  
HTTP是一个基于“请求与响应”模式的、无状态的应用层协议  
无状态是指第一次请求和第二次请求之间没有关联  
采用URL作为定位网络资源的标识  
URL格式
http://host[:port][path]  
host:合法的Internet主机域名或IP地址  
port：端口号，缺省为80  
path：资源在服务器上路径   
URL:是通过HTTP协议存取资源的Internet路径，一个URL对应一个数据资源  

###http对资源的操作
！[picture5]()
Requests对资源的操作对应http协议对资源的操作
  
当发现资源过于大时，可以通过HEAD操作获取该资源的头部信息，对头部信息进行分析，得到概要信息。
！[picture6]()  

使用PATCH 对资源进行局部的更新。好处：节省网络带宽   

如果向URL POST一个字符串自动编码为data  
但是如果向URL POST一个字典，存储到表单字段下

#Requests库的主要方法解析
---
requests.request(method,url,**kwargs)  
method:请求方式
url:拟获取页面的url链接 

OPTIONS:获取服务端和客户端交互的参数  





  

 






