# python爬虫

反爬手段

```python
1.user-Agent:
	user-Aent用户代理
2.代理IP
	
3.验证码访问
	打码平台
		云打码平台
		超级码
4.动态加载网页 网页返回的是js数据 并不是网页的真实数据
	selenium驱动真实的浏览器发送请求
5.数据加密
	分析js代码
```

urllib库使用

```python
# 使用urllib来获取百度首页的源码
import urllib.request

# 定义一个url
url = 'http://www.baidu.com'
# 模拟浏览器向服务器发送请求   response响应的意思
response = urllib.request.urlopen(url)
#获取响应中的页面源码  content 内容的意思
#read方法 返回的是字节形式的二进制数据
#将二进制的数据转换为字符串
#二进制到字符串  解码  decode
content=response.read().decode("UTF-8")
print(content)
```

一个类型六个方法

read readline  readlines  getcode geturl getheaders

```
#返回状态码 如果是200证明逻辑没有错
getcode()
#返回的是url地址
geturl()
#返回的是状态信息和响应头
getheaders()
```

### urllib下载

下载网页

urllib.request.urlretrieve(url,文件名)

1.请求对象的定制urllib.request.Request

```
import  urllib.request
url_page="https://www.baidu.com"
#url的组成
#http/https  www.baidu.com      80/443              s           wd=周杰伦          #
#协议             主机              端口号          路径            参数               描点
#http 80
headers={
"user-agent":
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36"
}
#请求对象的定制
request=urllib.request.Request(url=url_page,headers=headers)

response=urllib.request.urlopen(request)
connect=response.read().decode("utf-8")
print(connect)
```

2.get请求 urllib.parse.quote

将文字转为unicode的编码

 3.urllib_get请求方式的urlencode

多个参数的时候使用urlencode

4.post请求

post请求参数必须编码

参数是放在请求对象定制当中

编码之后必须调用encode方法

```python
import urllib.request
import urllib.parse
import json
url = "https://fanyi.baidu.com/sug"
headers = {
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36"

}

data={
    "kw":"word"
}
#post请求的参数,必须要进行编码
data=urllib.parse.urlencode(data).encode("utf-8")
#post请求的参数  需要放在请求对象定制的参数中
#post请求的参数 必须进行编码
request=urllib.request.Request(url=url,data=data,headers=headers,method="POST")
#向服务器发送请求
response=urllib.request.urlopen(request)
#获取响应的数据
content=response.read().decode("UTF-8")
#字符串改为json对象

obj=json.loads(content)
print(obj)
```

## ajax的get请求豆瓣

```python
#get请求
#获取豆瓣电影的第一页
import urllib.request


url="https://movie.douban.com/j/chart/top_list?type=24&interval_id=100%3A90&action=&start=0&limit=20"

headers={
"user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36"
}
#请求对象的定制
request=urllib.request.Request(url=url,headers=headers)

#获取响应的数据
response=urllib.request.urlopen(request)
content=response.read().decode("utf-8")
#下载数据到本地
#open方法默认使用gbk编码,我们要是想要保存汉子 那么需要在open方法中制定编码格式
# fp=open("douban.json","w",encoding="utf-8")
# fp.write(content)
with open("douban.json","w",encoding="utf-8") as fp:
    fp.write(content)
```

获取多个页面

```python
import urllib.request
import urllib.parse


#下载豆瓣电影的前十页
#请求对象的定制
#获取响应的数据
#下载数据

def create_request(page):
    #start=0&limit=20
    base_url="https://movie.douban.com/j/chart/top_list?type=24&interval_id=100%3A90&action=&"

    headers={
        "user-agent":
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36"
    }
    data={
        "start":(page-1)*20,
        "limit":20
    }
    data =urllib.parse.urlencode(data)
    #定制请求头
    url=base_url+data
    request=urllib.request.Request(url=url,headers=headers)
    # print(url)
    return request
#获取响应头
def get_conten(request):
    response=urllib.request.urlopen(request)
    content=response.read().decode("utf-8")
    return content
#下载数据
def down_load(page,content):
    with open("douban_"+str(page)+".json","w",encoding="utf-8") as fp:
        fp.write(content)
#程序的入口
if __name__ == '__main__':
    start_page=int(input("请输入其实的页码"))
    end_page=int(input("请输入结束的页码"))

    for page in range(start_page,end_page+1):
        #每一页都有自己请求对象的定制
        request=create_request(page)
        #获取响应数据
        content=get_conten(request)
        #下载数据
        down_load(page,content)
```

## ajax的post请求 肯德基

```python
# https://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname
# cname: 北京
# pid:
# pageIndex: 2
# pageSize: 10
import urllib.request, urllib.parse


# 先定义请求头
# 获取响应
# 下载数据
# 先定义请求头
def create_request(caame_data, page):
    url = "https://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname"
    headers = {
        "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36"
    }
    data = {
        "cname": caame_data,
        "pid":"",
        "pageIndex": page,
        "pageSize": 10
    }
    data = urllib.parse.urlencode(data).encode("utf-8")

    request = urllib.request.Request(url=url, headers=headers, data=data)
    return request

    # 获取请求头


def get_content(request):
    response = urllib.request.urlopen(request)
    content = response.read().decode("utf-8")
    return content
    # 下载


def donw_load(caame_data,page, content):
    with open(caame_data + "肯德基门店列表第" + str(page) + ".json", "w", encoding="utf-8") as fp:
        fp.write(content)


if __name__ == '__main__':
    caame_data = input("请输入要查询的城市")
    sta_page = int(input("请输入开始页面"))
    end_page = int(input("请输入结束页面"))
    for page in range(sta_page, end_page + 1):
        # 先定义请求头
        request = create_request(caame_data, page)
        # 获取响应
        content = get_content(request)
        # 下载
        donw_load(caame_data, page, content)
```

## URLError\HTTPError

```
简介:
1.HTTPError类是URLError类的子类
2.导入包urllib.error.HTTPError     urllib.error.URLError
3.HTTP错误: http错误是针对浏览器无法链接到服务器而增加出来的错误提示,引导并告诉浏览者该页面哪里出现了问题
4.通过urllib发送请求的时候,有可能会发送失败,这个时候回如果想让你的代码更加健壮,可以通过try-execpt进行捕获异常,异常有两类URLError\HTTPError
```

# cookie登录

cookie是保存登录信息的

referer判断当前路径是不是由上一个路径进来的

### Handler处理器

```
handler    build_opener			opener		ProxyHandler
```

```
为什么要学习handler?
	urllib.request.urlopen(url)
	不能定制请求头
	urllib.request.Request(url,headers,data)
	可以定制请求头
	Handler
		定制更高级的请求头(动态cookie和代理,不能使用请求对象的定制)
```

```
import urllib.request


url="https://www.baidu.com"
headers={
   "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36",
  "Cookie": "BIDUPSID=12B162722AE2BE5FAE8A5140ECA98DBD; PSTM=1728027177; BAIDUID=12B162722AE2BE5F8DE4C1CA2949294E:FG=1; BD_UPN=12314753; newlogin=1; H_WISE_SIDS=60451_60783_60844; H_WISE_SIDS_BFESS=60451_60783_60844; H_PS_PSSID=60451_60853_60885_60875; BDUSS=283dE5NVDhNaWw2Vms3Y05LRld3T0tMTUNxY2EwRHhTSGlINElnTFdaSWM5RFZuSVFBQUFBJCQAAAAAAAAAAAEAAADCA~H4x-~C5Nau6eRfAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABxnDmccZw5nQ; BDUSS_BFESS=283dE5NVDhNaWw2Vms3Y05LRld3T0tMTUNxY2EwRHhTSGlINElnTFdaSWM5RFZuSVFBQUFBJCQAAAAAAAAAAAEAAADCA~H4x-~C5Nau6eRfAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABxnDmccZw5nQ; BDORZ=FFFB88E999055A3F8A630C64834BD6D0; BAIDUID_BFESS=12B162722AE2BE5F8DE4C1CA2949294E:FG=1; ZFY=hKPjeVAvuuclodwQlohikTpOvShL2ewWAFgR3TNCfeA:C; B64_BOT=1; BA_HECTOR=008h010121a42g8k0k8kah2592kdet1jh1o151v; COOKIE_SESSION=94814_0_8_3_11_11_1_0_8_7_0_2_94620_0_0_0_1729159206_0_1729159206%7C9%230_1_1728027182%7C1; sugstore=0; H_PS_645EC=d70b7vJUTmyiuTrcNdlqwKZ9ZQ7ugBsNczl6iEDbcU9z6o23nXXcSD8ubs8c0TTv1ESY1A"
}
request=urllib.request.Request(url=url,headers=headers)
#获取handler对象
proxies={"http":"http://127.0.0.1:8888"}
handler=urllib.request.ProxyHandler(proxies=proxies)
#获取build_opener()
opener=urllib.request.build_opener(handler)
#调用opener
reponse=opener.open(request)
content=reponse.read().decode("utf-8")
print(content)
```

### ProxyHandler

```
import urllib.request


url="https://2024.ip138.com"
headers={
   "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36",
    }
request=urllib.request.Request(url=url,headers=headers)
#获取handler对象
proxies={"http":"47.104.27.165:80"}
handler=urllib.request.ProxyHandler(proxies=proxies)
#获取build_opener()
opener=urllib.request.build_opener(handler)
#调用opener
reponse=opener.open(request)
content=reponse.read().decode("utf-8")
print(content)
```

## 解析

1. xpath

   etree.parse()解析本地文件

   ```
   html_tree=etree.parse("本地文件地址")
   ```

   etree.HTML()	解析服务器响应文件

   ```
   html_tree=etree.HTML(response.read().decode("utf-8"))
   ```

   ### xpath基本语法

   ```
   /text()获取标签中的内容
   
   tree.xpath("//ul/li[@id]/text()")
   1.路径查询
   //:查询所有子孙节点,不考虑层级关系
   /:找直接子节点
   2.谓词查询
   //div[@id]
   //div[@id="maincontent"]
   3.属性查询
   //@class
   
   li_list=tree.xpath('//body//ul/li[@id="l1"]/@class')
   4.模糊查询
   //div[contains(@id,"he")]
   
   li_list=tree.xpath('//ul/li[contains(@id,"l")]/text()')
   #一谁开始
   //div[starts-with(@id,"he")]
   5.内容查询
   //div/h1/text()
   6.逻辑运算
   //div[@id="head"and@class="s_down"]
   //title|//price
   ```

   

2. jsonpath

   ```
   jsonpath
   	使用
   	obj=json.load(open('json文件','r',encoding='utf-8'))
   	ret=jsonpath.jsonpath(obj,'jsonpath语法')
   ```

   | XPATH | JSON             |                                                              |
   | ----- | ---------------- | ------------------------------------------------------------ |
   | /     | $                | 表示根元素                                                   |
   | .     | @                | 当前元素                                                     |
   | /     | .or[]            | 子元素                                                       |
   | ..    | n/a              | 父元素                                                       |
   | //    | ..               | 递归下降，JSONPATH从EX4借鉴                                  |
   | *     | *                | 通配符表示所有元素                                           |
   | @     | n/a              | 属性访问字符                                                 |
   | []    | []               | 子元素访问字符                                               |
   | \|    | [,]              | 连接操作符在Xpath结果结合并与其他节点集合，JSON允许name或者数组索引 |
   | n/a   | [start:end:step] | 数组分隔符从ES4借鉴                                          |
   | []    | ?()              | 应用过滤表达式                                               |
   | n/a   | ()               | 脚本表达式，使用在脚本下面                                   |
   | ()    | n/a              | Xpath分组                                                    |

   淘票票删掉json前后圆括号

   ```
   content=content.split('(')[1].split(')')[0]
   ```

   ```python
   import urllib.request
   import json
   import time
   import jsonpath
   url = 'https://dianying.taobao.com/cityAction.json?activityId&_ksTS=1729246151992_104&jsoncallback=jsonp105&action=cityAction&n_s=new&event_submit_doGetAllRegion=true'
   headers = {
       "sec-ch-ua-platform": "\"Windows\"",
       "x-requested-with": "XMLHttpRequest",
       "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36",
       "accept": "text/javascript, application/javascript, application/ecmascript, application/x-ecmascript, */*; q=0.01",
       "sec-ch-ua": "\"Google Chrome\";v=\"129\", \"Not=A?Brand\";v=\"8\", \"Chromium\";v=\"129\"",
       "sec-ch-ua-mobile": "?0",
       "bx-v": "2.5.22",
       "sec-fetch-site": "same-origin",
       "sec-fetch-mode": "cors",
       "sec-fetch-dest": "empty",
       "referer": "https://dianying.taobao.com/",
       # "accept-encoding": "gzip, deflate, br, zstd",
       "accept-language": "zh-CN,zh;q=0.9,en;q=0.8",
       "cookie": "isg=BLW1YVTfPmaQUVrYVkl-uT3fxDFvMmlEd7jkVTfa4SwrDtQA_4BLFISIXNI4c4H8",
       "priority": "u=1, i"
   }
   request = urllib.request.Request(url=url, headers=headers)
   
   response = urllib.request.urlopen(request)
   content = response.read().decode("utf-8")
   content = content.split('(')[1].split(')')[0]
   with open("地区.json", "w", encoding="utf-8") as fp:
       fp.write(content)
   # time.sleep(10)
   obj=json.load(open('地区.json', 'r', encoding='utf-8'))
   citv=jsonpath.jsonpath(obj, '$..regionName')
   print(citv)
   ```

3. BeautifulSoup

   1.BeautifulSoup简称

   bs4

   2.什么是BeautifulSoup

   BeautifulSoup和xml一样,是一个html 的解析器,主要功能也是解析和提取数据

   3.效率没lxml的效率高

   ```
   导入 
   	from bs4 import BeautifulSoup
   创建对象
   	服务器响应的文件生成对象
   	soup=BeautifulSoup(response.read().decode(),'lxml')
   	本地文件生对象
   	soup=BeautifulSoup(open('1.html'),'lxml')
   	注意:默认打开文件的编码格式gbk所以需要指定的打开编码格式
   ```

   节点定位

   ```
   1.根据标签名查找节点
   	soup.a		[注]只能找到第一个a
   	soup.a.name			#返回的是<a class="a1" href="" id="">尚硅谷</a>
   	soup.a.attrs		#返回的是属性{'href': '', 'id': '', 'class': ['a1']}
   
   2.bs4的函数
   	1.find				#返回第一个符合条件的数据
   	#根据标题
       print(soup.find('a',title="a1"))		#返回title =a1符合条件的数据
       #根据class需要加下划线
   	print(soup.find('a',class_="a1"))
   	2.find_all		#返回全部符合条件的列表
   	#找到所有的a和span标签
   	print(soup.find_all(['a','span']))	
   	#获取所有的li标签,但是只需要两个
   	print(soup.find_all('li',limit=2))
   	
   ```

   ```
   select
   1.element
   2..class  	#.代表class
   3.#id		##代表id
   4.属性选择器
   #查找li标签中有id的标签
   print(soup.select('li[id]'))
   #查找li表中中id为l2的标签
   print(soup.select('li[id="l2"]'))
   5.#层级选择器
   # #   后代选择器
   # print(soup.select('div li'))
   
   #子代选择器
       #某标签的第一子标签
   print(soup.select('div > ul > li'))
   ```

### 节点信息

```
1.获取节点内容
	obj.string
	obj.get_tecxt
2.  节点属性
	obj.name
	attrs是将属性值作为一个字典返回
	obj=soup.select('#p1')[0]
	print(obj.attrs.get('class'))
	print(obj.get('class'))
	print(obj['class'])	
	
```

## selenium

1. selenium

   ```
   1.什么是selenium？
   （1）Selenium是一个用于web应用程序测试的工具。
   （2）Selenium测试直接运行在浏览器中，就像真正的用户在操作一样。
   （3）支持通过各种driver（FirfoxDriver，IternetExplorerDriver，OperaDriver，ChromeDriver）驱动
   真实浏览器完成测试。
   （4）selenium也是支持无界面浏览器操作的。
   ```

   ```
   2.为什么使用selenium？
   模拟浏览器功能，自动执行网页中的js代码，实现动态加载
   ```

   ```
   3.如何安装selenium？
   （1）操作谷歌浏览器驱动下载地址
   http://chromedriver.storage.googleapis.com/index.html
   （2）谷歌驱动和谷歌浏览器版本之间的映射表
   http://blog.csdn.net/huilan_same/article/details/51896672
   （3）查看谷歌浏览器版本
   谷歌浏览器右上角-->帮助-->关于
   (4) pip install selenium
   ```

   ```
   #导入selenium
   from selenium import webdriver
   from selenium.webdriver.chrome.service import Service
   
   # 创建浏览器操作对象
   path = 'D:\\chrome-win64\\chromedriver.exe'
   service = Service(path)
   browser = webdriver.Chrome(service=service)
   
   # 访问网站
   url = 'https://www.baidu.com'
   import time
   
   
   browser.get(url)
   
   content=browser.page_source
   print(content)
   ```

   

2. seleuim的元素定位

   ```
   元素定位:自动化做的就是模拟鼠标和键盘来操作这些元素,点击输入等等.操作这些元素前首先要找到他们,webdriver提供了很多定位元素的方法
   
   #元素id定位
   
   
   # button=browser.find_element('id','su')
   # print(button)
   
   #根据标签属性的属性值来获取对象
   
   # button=browser.find_element('name','wd')
   # print(button)
   
   #根据xpath语句来获取对象
   
   # button=browser.find_element('xpath','//*[@id="su"]')
   # print(button)
   
   #根据标签的名字来获取对象
   
   # button=browser.find_element('tag name','input')
   # print(button)
   
   # 使用 CSS 选择器根据 class 名称获取对象  bs4
   # button = browser.find_element('css selector', '.bg.s_btn_wr')
   # print(button)
   
   #
   button=browser.find_element('link text','新闻')
   print(button)
   ```

   ```
   获取元素属性
   	.get_attribute('class')
   获取元素文本
   	
   获取标签名
   	.tag_name
   ```

 ### phantomjs

```
1.什么是phantomjs？
(1）是一个无界面的浏览器
（2）支持页面元素查找，js的执行等
（3）由于不进行css和gui谊染，运行效率要比真实的浏览器要快很多
```

### Chromehandless

无头模式

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
# 设置 Chrome 浏览器选项
chrome_options = Options()
chrome_options.add_argument('--headless')  # 无头模式
chrome_options.add_argument('--disable-gpu')  # 适配一些系统中的无头模式问题
chrome_options.add_argument('--window-size=1920,1080')  # 设置窗口大小

service = Service('D:\\chrome-win64\\chromedriver.exe')
browser = webdriver.Chrome(service=service, options=chrome_options)
```



先导入属性

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
import time

# 设置 Chrome 浏览器选项
chrome_options = Options()
chrome_options.add_argument('--headless')  # 无头模式
chrome_options.add_argument('--disable-gpu')  # 适配一些系统中的无头模式问题
chrome_options.add_argument('--window-size=1920,1080')  # 设置窗口大小

service = Service('D:\\chrome-win64\\chromedriver.exe')
driver = webdriver.Chrome(service=service, options=chrome_options)

try:
    # 打开百度页面
    driver.get('https://www.baidu.com')

    # 给页面加载一些时间
    time.sleep(2)

    # 截图保存到本地
    driver.save_screenshot('baidu_screenshot.png')
    print("截图已保存为 'baidu_screenshot.png'")
finally:
    # 关闭浏览器
    driver.quit()

```

# request

1.基本使用

```
1.文档：
	官方文档
		https://requests.readthedocs.io/projects/cn/zh-cn/latest/
	快速上手
		http://cn.python-requests.org/zh_CN/latest/user/quickstart.html
```

2.

```
response的属性以及类型
类型		  :models.Response
r.text		：获取网站源码
r.encoding	：访问或定制编码方式
r.url		：获取请求的ur1
r.content	：响应的字节类型
r.status_code：响应的状态码
r.headers	：响应的头信息
```

```
#url 请求资源路径
#params 参数
#kwargs 字典
```

get请求

```python
import requests

url = 'https://www.baidu.com/s'
headers = {
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36",
}
data = {
    'wd': '北京'
}
# url 请求资源路径
# params 参数
# kwargs 字典
response = requests.get(url=url, params=data, headers=headers)
content= response.text
print(content)

#参数使用params传递
#参数无需urlencode编码
#不需要请求对象的定制
#请求资源路径的?可以加也可以不加

```

post

```
# 初始化会话对象
session = requests.session()
作用是创建一个 Session 对象，它用于保持和管理多个请求之间的会话。与 requests.get() 或 requests.post() 不同，session 对象可以在多个请求之间保持 cookie 和 HTTP 连接，从而模拟更真实的浏览器行为
```

## scrapy

```
(1） scrapy是什么?
Scrapy是一个为了爬取网站数据，提取结构性数据而编写的应用框架可以应用在包括数据挖
掘，信息处理或存储历史数据等一系列的程序中
```

### 1.创建项目 在终端输入 scrapy startpoject 项目名称

```
1.创建爬虫的项目 scrapy startproject 项目的名字
            项目名字不能使用中文
2.创建爬虫文件
    要在spiders文件夹中创建爬虫文件
    cd 项目的名字\项目的名字\spiders
    创建爬虫文件
    scrapy genspider 爬虫文件的名字    要爬取的网页

3.运行爬虫代码
    scrapy crawl 爬虫的名字
注释掉settings.py里面的
#注释掉以后 就不遵守 robots协议了
# ROBOTSTXT_OBEY = True
```

```
2.项目组成：
		spiders
			init_.Py
			自定义的爬虫文件.py--》由我们自己创建，是实现爬虫核心功能的文件
		_init__..Py
		items.py---》定义数据结构的地方，是一个继承自scrapy.Item的类
		middlewares.py---》中间件代理
		pipelines.py--》管道文件，里面只有一个类，用于处理下载数据的后续处理
		默认是300优先级，值越小优先级越高（1-1000）
		settings.py---》配置文件比如：是否遵守robots协议，User-Agent定义等
		scrapy的项目结构
		
		
    项目名字
        项目名字
            spiders文件夹(存储的是爬虫文件)
                init
                自定义的爬虫文件        核心功能    ******
            init
            items       定义数据结构的地方
            middleware  中间件     代理
            pipelines   管道  用来处理下载的数据
            settings    配置文件    robots协议  和ua定义


2.response的属性和方法
    response.text   获取的是响应的字符串
    response.body   获取的是二进制数据
    response.xpath  可以直接使用xpath方法解析xpath语法
    response.extract()  提取seletor对象data属性值
    response.extract_first()    提取seletor列表的第一个数据
```

```
from datetime import datetime

# 生成当前时间戳
timestamp = datetime.now().strftime('%Y%m%d%H%M%S')
```

#### scrapy架构组成

![image-20241020120317866](./Pictures/image-20241020120317866.png)

###  scrapy shell

```
1.什么是scrapy shell?
Scrapy终端，是一个交互终端，供您在未启动spider的情况下尝试及调试您的爬取代码。其本意是用来测试提取
数据的代码，不过您可以将其作为正常的python终端，在上面测试任何的Python代码。
该终端是用来测试xPath或cSS表达式，查看他们的工作方式及从爬取的网页中提取的数据。在编写您的spider时，该
终端提供了交互性测试您的表达式代码的功能，免去了每次修改后运行spider的麻烦。
一旦熟悉了scrapy终端后，您会发现其在开发和调试spider时发挥的巨大作用。
```

在window终端中输入 scrapy shell 域名

如果想看到一些高亮 或者自动补全基于安装ipython

懒加载反爬

### Crawlspider

```
1.创建项目：scrapy startproject dushuproject
2.跳转到spiders路径cd \dushuproject\dushuproject\spiders
3.创建爬虫类：scrapy genspider -t crawl read www.dushu.com
4.items
5.spiders
6.settings
7.pipelines
数据保存到本地
数据保存到mysql数据库
```

```
1. scrapy startproject 项目名字
2 cd ////
3.scrapt genspider -t crawl 名字 域名
```



```
链接提取
	scrapy.linkextractors.linkExtractor
	allow=(),			#正则表达式
	deny=()				#(不用正则表达式) 不提取符和规则的链接
	allow_domains=()	#(不用)允许的域名
	deny_domains=()		#(不用)不允许的域名
	restrict_xpaths=()	#xpath 提取符合xpath规则的链接
	restrict_css=()		#提取符合选择器规则的链接
	
提取链接
	link.extract_links(response)

```

```
6.注意事项
【注1】callback只能写函数名字符串，callback='parse_item
【注2】在基本的spider中，如果重新发送请求，那里的callback写的是callback=self.parse_item 【注-
-稍后看】follow=true是否跟进就是按照提取连接规则进行提取
```

```
（1）日志级别：
		在settings
		LOG_LEVEL='级别'
		###
		LOG_FILE='logdemo.log'
		CRITICAL：严重错误
		ERROR:般错误
		WARNING:警告
		INFO:-般信息
		DEBUG调试信息
		默认的日志等级是DEBUG
		只要出现了DEBUG或者DEBUG以上等级的日志
		那么这些日志将会打印
(2）settings.py文件设置：
	默认的级别为DEBUG，会显示上面所有的信息
	在配置文件中settings·Py
	LOG_FILE：将屏幕显示的信息全部记录到文件中，屏幕不再显示，注意文件后缀一定是.1og
	LOG_LEVEL：设置日志显示的等级，就是显示哪些，不显示哪些
```

scrapy中post请求

# 代理池

![image-20241022181143923](./Pictures/image-20241022181143923.png)

1.定义ip数据模型类

- 定义prox类,继承object
- 实现_ _ init _  _ 方法,负责初始化,
- ip:代理ip的地址
- port:代理ip的端口号
- protocol:代理ip支持的协议类型 ,http是0.https是1 https和http都支持是2
- nick_type:代理ip的匿名程度 高匿名是0 匿名是1 透明是2
- speed:代理ip的响应速度,单位是s
- area:代理ip所在的地区
- score:代理ip的评分
- disable_name:不可用域名列表

2. 实现代理池工具模块
   - 实现日志模块
     - 拷贝笔记日志代码到项目中
     - 把日志相关配置信息 放到配置文件中
     - 修改日志代码, 使用配置文件中的配置信息
3. 

