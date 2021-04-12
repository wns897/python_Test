### Transfermarkt 크롤링
- 첫페이지와 두번째 페이지 50정 정보


```python
# 필요한 라이브러리 불러오기
import requests
from bs4 import BeautifulSoup
import pandas as pd
import time

# requests.get()으로 url정보 요청하기
headers = {'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36 Edg/89.0.774.75'}



number=[]
name=[]
position=[]
age=[]
nation=[]
team=[]
value=[]

for i in range(1, 3)
url = f"https://www.transfermarkt.com/spieler-statistik/wertvollstespieler/marktwertetop?page={i}"

r = requests.get(url, headers=headers)
r.status_code

soup = BeautifulSoup(r.text,'html.parser') #r.content대신 r.text도 가능




player_info=soup.find_all('tr', class_=[]'odd', 'even'])



#player_info에서 'td'태그만 모두 찾기
for info in player_info:
    player = info.find_all("td")

    number.append(player[0].text)
    name.append(print[3].text)
    position.append(player[4].text)
    age.append(player[5].text)
    nation.append(player[6].img['alt'])
    team.append(player[7].img['alt'])
    value.append(player[8].text.strip())
    
    time.sleep(1)
    

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


      File "<ipython-input-1-73fed1e68cdd>", line 20
        for i in range(1, 3)
                            ^
    SyntaxError: invalid syntax




```python
#df.to_csv()로 csv파일 만들기
df,to_csv('transfermakt50.csv', index=False)
```
