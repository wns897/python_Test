```python
#requests 불러오기 pip install requests
import requests
```


```python
#headers에 'User-Agent' 값 넣기
headers = { 'User-Agent' : "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36 Edg/89.0.774.75"}
#url에 주소 넣기
url = "https://www.transfermarkt.com/"

#requests.get()으로 요청하기
r = requests.get(url, headers = headers)

#status_code 응답확인하기
r.status_code
```




    200



# BeautifulSoup Quick Start 실습


```python
html_doc = """<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>

<p class= "story">Once upon a time there were three little sisters: and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>
and they lived at the bottom of a well.</p>

<p class="story">...</p>"""
```


```python
from bs4 import BeautifulSoup
soup = BeautifulSoup(html_doc, 'html.parser')

```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    <ipython-input-14-11f369478349> in <module>
    ----> 1 from bs4 import BeautifulSoup
          2 soup = BeautifulSoup(html_doc, 'html.parser')


    ModuleNotFoundError: No module named 'bs4'



```python
# p 태그 정보 가져오기(처음 나오는 것 한 개)
soup.p
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-16-33d903c81094> in <module>
          1 # p 태그 정보 가져오기(처음 나오는 것 한 개)
    ----> 2 soup.p
    

    NameError: name 'soup' is not defined



```python
soup.find('p')
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-19-83b1b2773536> in <module>
    ----> 1 soup.find('p')
    

    NameError: name 'soup' is not defined



```python
#a 태그에 있는 ''href' 속성값 가져오기(처음 나오는 것 한개)
soup.find('a')['href']
soup.a['href']
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-20-8d4acee334a8> in <module>
          1 #a 태그에 있는 ''href' 속성값 가져오기(처음 나오는 것 한개)
    ----> 2 soup.find('a')
    

    NameError: name 'soup' is not defined



```python
#a 태그에 있는 텍스트 가져오기(처음 나오는 것 한 개)
soup.find('a').text
soup.find('a').get_text()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-22-bf1498d19510> in <module>
          1 #a 태그에 있는 텍스트 가져오기(처음 나오는 것 한 개)
    ----> 2 soup.find('a').text
    

    NameError: name 'soup' is not defined



```python
#a 태그에 있는 요소들 모두 가져오기
soup.find_all('a')
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-23-0401d64d556c> in <module>
          1 #a 태그에 있는 요소들 모두 가져오기
    ----> 2 soup.find_all('a')
    

    NameError: name 'soup' is not defined



```python
#두번째 a태그에 있는 정보 가져오기
soup.find_all('a')[1]
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-24-8c9c61a8b011> in <module>
          1 #두번째 a태그에 있는 정보 가져오기
    ----> 2 soup.find_all('a')[1]
    

    NameError: name 'soup' is not defined



```python
# a 태그에 있는 'href'속성값 모두 가져오기
a_list = soup.find_all('a')
for i in a_list:
    print(i['href'])
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-25-e97bb366007f> in <module>
          1 # a 태그에 있는 'href'속성값 모두 가져오기
    ----> 2 a_list = soup.find_all('a')
          3 for i in a_list:
          4     print(i['href'])


    NameError: name 'soup' is not defined



```python
#a 태그에 있는 텍스트 모두 가져오기
a_list = soup.find_all('a')
for i in a_list:
    print(i.text)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-26-dd73d7150458> in <module>
          1 #a 태그에 있는 텍스트 모두 가져오기
    ----> 2 a_list = soup.find_all('a')
          3 for i in a_list:
          4     print(i.text)


    NameError: name 'soup' is not defined



```python
#태그와 속성갑을 같이 넣어 찾아오기
#a 태그 이면서 class가 sister인 값 모두 찾아오기
soup.find_all("a", class_="sister")
soup.find_all("a",{"class":"sister"})
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-28-2596b4fd6c83> in <module>
          1 #태그와 속성갑을 같이 넣어 찾아오기
          2 #a 태그 이면서 class가 sister인 값 모두 찾아오기
    ----> 3 soup.find_all("a", class_="sister")
    

    NameError: name 'soup' is not defined



```python
#a태그이면서 id가 link3인 요소들 모두 찾기
soup.find_all("a", id="link3")
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-29-33fbe784015a> in <module>
          1 #a태그이면서 id가 link3인 요소들 모두 찾기
    ----> 2 soup.find_all("a", id="link3")
    

    NameError: name 'soup' is not defined



```python
soup.find_all("a",{"id":"link3"})
```
