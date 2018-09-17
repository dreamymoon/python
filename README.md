爬虫：
import urllib2 #直接请求
response=urllib2.urlopen('http://www.baidu.com') #获取状态码，200表示获取成功
print response.getcode()
cont=response.read()   #读取内容


import urllib2
url='http://www.baidu.com'

print '第一种方法'
response1=urllib2.urlopen(url)
print response1.getcode()
print len(response1.read())

print '第二种方法'
request=urllib2.Request(url)
request.add_header('user-agent','Mozilla/5.0')
response2=urllib2.urlopen(request)
print response2.getcode()
print len(response2.read())

print '第三种方法'
import cookielib
cj=cookielib.CookieJar()
opener=urllib2.build_opener(urllib2.HTTPCookieProcessor(cj))
urllib2.install_opener(opener)
response3=urllib2.urlopen(url)
print response3.getcode()
print cj
print response3.read()





Beautifulsoup：

#encoding: utf-8
from bs4 import BeautifulSoup

html_doc = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""

soup= BeautifulSoup(html_doc, 'html.parser',from_encoding='utf-8')
print "获取所有的链接"
links = soup.find_all('a')
for link in links:
    print link.name, link['href'], link.get_text()

print '获取Lacie的链接'
link_node= soup.find('a',href='http://example.com/lacie')
print link_node.name, link_node['href'], link_node.get_text()

print '正则匹配'
import re
link_node= soup.find('a',href=re.compile(r"ill"))
print link_node.name, link_node['href'], link_node.get_text()

print '获取P段落文字'
import re
p_node= soup.find('p',class_='title')
print p_node.name,  p_node.get_text()

