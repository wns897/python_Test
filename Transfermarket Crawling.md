```python
# 필요한 라이브러리 불러오기
import requests
from bs4 import BeautifulSoup
import pandas as pd
import time
```





```python
# requests.get()으로 url정보 요청하기
headers = {'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36 Edg/89.0.774.75'}

url = "https://www.transfermarkt.com/spieler-statistik/wertvollstespieler/marktwertetop"

r = requests.get(url, headers=headers)
r.status_code
```


   


```python
#BeautifulSoup()으로 웹페이지 분석 준비하기
soup = BeautifulSoup(r.text,'html.parser') #r.content대신 r.text도 가능
print(soup)

```



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
