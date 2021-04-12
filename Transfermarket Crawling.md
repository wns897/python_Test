```python
# 필요한 라이브러리 불러오기
import requests
from bs4 import BeautifulSoup
import pandas as pd
import time
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    <ipython-input-1-f080a2e88f8d> in <module>
          1 #필요한 라이브러리 불러오기
          2 import requests
    ----> 3 from bs4 import BeautifulSoup
    

    ModuleNotFoundError: No module named 'bs4'



```python
# requests.get()으로 url정보 요청하기
headers = {'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36 Edg/89.0.774.75'}

url = "https://www.transfermarkt.com/spieler-statistik/wertvollstespieler/marktwertetop"

r = requests.get(url, headers=headers)
r.status_code
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-3-9dbcfafaae24> in <module>
          4 url = "https://www.transfermarkt.com/spieler-statistik/wertvollstespieler/marktwertetop"
          5 
    ----> 6 r = requests.get(url, headers=headers)
          7 r.status_code


    /usr/local/lib/python3.7/site-packages/requests/api.py in get(url, params, **kwargs)
         74 
         75     kwargs.setdefault('allow_redirects', True)
    ---> 76     return request('get', url, params=params, **kwargs)
         77 
         78 


    /usr/local/lib/python3.7/site-packages/requests/api.py in request(method, url, **kwargs)
         59     # cases, and look like a memory leak in others.
         60     with sessions.Session() as session:
    ---> 61         return session.request(method=method, url=url, **kwargs)
         62 
         63 


    /usr/local/lib/python3.7/site-packages/requests/sessions.py in request(self, method, url, params, data, headers, cookies, files, auth, timeout, allow_redirects, proxies, hooks, stream, verify, cert, json)
        514             hooks=hooks,
        515         )
    --> 516         prep = self.prepare_request(req)
        517 
        518         proxies = proxies or {}


    /usr/local/lib/python3.7/site-packages/requests/sessions.py in prepare_request(self, request)
        457             auth=merge_setting(auth, self.auth),
        458             cookies=merged_cookies,
    --> 459             hooks=merge_hooks(request.hooks, self.hooks),
        460         )
        461         return p


    /usr/local/lib/python3.7/site-packages/requests/models.py in prepare(self, method, url, headers, files, data, params, auth, cookies, hooks, json)
        313         self.prepare_method(method)
        314         self.prepare_url(url, params)
    --> 315         self.prepare_headers(headers)
        316         self.prepare_cookies(cookies)
        317         self.prepare_body(data, files, json)


    /usr/local/lib/python3.7/site-packages/requests/models.py in prepare_headers(self, headers)
        445         self.headers = CaseInsensitiveDict()
        446         if headers:
    --> 447             for header in headers.items():
        448                 # Raise exception on invalid header value.
        449                 check_header_validity(header)


    AttributeError: 'set' object has no attribute 'items'



```python
#BeautifulSoup()으로 웹페이지 분석 준비하기
soup = BeautifulSoup(r.text,'html.parser') #r.content대신 r.text도 가능
print(soup)

```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-4-7b23d776d361> in <module>
          1 #BeautifulSoup()으로 웹페이지 분석 준비하기
    ----> 2 soup = BeautifulSoup(r.text,'html.parser') #r.content대신 r.text도 가능
          3 print(soup)


    NameError: name 'BeautifulSoup' is not defined



```python
#선수들의 정보가 담긴 태그와 클래스 찾기
player_info=soup.find_all('tr', class_=[]'odd', 'even'])
```


      File "<ipython-input-5-de60d8d17f78>", line 2
        player_info=soup.find_all('tr', class_=[]'odd', 'even'])
                                                     ^
    SyntaxError: invalid syntax




```python
#첫번째 요소 확인하기
print(player_info[0])
#전체 개수 확인하기
print(len(player_info)
```


      File "<ipython-input-6-689fdf9efb6b>", line 4
        print(len(player_info)
                              ^
    SyntaxError: unexpected EOF while parsing




```python
#7개 정보를 담을 빈 리스트 만들기 number, name, position, age, nation, team, value

number=[]
name=[]
position=[]
age=[]
nation=[]
team=[]
value=[]
```


```python
#player_info에서 'td'태그만 모두 찾기
for info in player_info:
    player = info.find_all("td")
    #print(player)
    #print(player[0])
#해당 정보를 찾아서 각 리스트에 .append로 추가하기
    number.append(player[0].text)
    name.append(print[3].text)
    position.append(player[4].text)
    age.append(player[5].text)
    nation.append(player[6].img['alt'])
    team.append(player[7].img['alt'])
    value.append(player[8].text.strip())
    
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-8-e2dbd2855f90> in <module>
          1 #player_info에서 'td'태그만 모두 찾기
    ----> 2 for info in player_info:
          3     player = info.find_all("td")
          4     #print(player)
          5     #print(player[0])


    NameError: name 'player_info' is not defined



```python
#pd.DataFrame()으로 저장하기

df = pd.DataFrame(
    {"number":number,
     "name":name,
     "position":position,
     "age":age,
     "nation":nation,
     "team":team,
     "value":value}
)
df
```


```python
#df.to_csv()로 csv파일 만들기
df,to_csv('transfermakt25.csv', index=False)
```
