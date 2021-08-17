# Web + Crawling





## 1. Web



- Web server <--> Web Client / get, post

- HTML5, CSS3, JavaScript -> 대략적인 내용만 볼 예정

- HTML 구조 - 반복적인 내용을 어떻게 가져올 것인가

- CSS Selector - id, class

  

Java - JSP, Apache Tomcat

Python - Django, Flask

NodeJS









## 2. Crawling



- 구글과 같은 검색엔진에서는 웹 사이트의 정적인 데이터를 긁어다가 필요한
  정보를 추출해서 검색 인덱스를 생성
- 라이브러리
  - Beautiful Soup: 가장 일반적, 요즘 성공률이 낮음
  - Jsoup: 자바 버전
  - Selenium: 구글/네이버 가능
  - 

HTML 파일 열기

```
from bs4 import BeautifulSoup
with open("00_Example.html") as fp:
	soup = BeautifulSoup fp , html.parser
```



find/findall 태그

```
first_div = soup.find ("div) 	# 하나만 찾음
print(first_div)
```

```
all_divs = soup.find_all ("div")	# 다 찾음
print(all_divs)
```



CSS Selector로 찾기

```
ex_id_div = soup.select_one ('#ex_id')
ex_id_div
```









## 3. GenieChart



https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent



### 1) 인터넷에서 데이터 가져오기

```
import requests
import pandas as pd
```

```
url = 'https://www.genie.co.kr/chart/top200'
req = requests.get(url)
html = req.text
html
```

```
header = {'User-Agent': 
            'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36'}
req = requests.get(url, headers = header)
html = req.text
```





### 2) 찾으려고 하는 데이터의 태그 찾기

```
# <table class="list-wrap">
table = soup.select_one('table.list-wrap')
trs = table.select('tr.list')
len(trs)
```





### 3) 여러개의 데이터 중 원하는 정보 추출

```
# Rank, Title, Artist, Album
tr = trs[0]
tr.select_one('.number').get_text()
```

```
# title
tr.select_one('.info').find('a').get_text()
```



### 4) 모든 데이터를 반복문으로 가져오기

```
rank_list, title_list, artist_list, album_list = [],[], [],[]
for tr in trs:
    rank = int(tr.select_one('.number').get_text().split('\n')[0])
    title = tr.select_one('.info').find('a').get_text().strip()
    artist = tr.select_one('.info').select_one('.artist').get_text().strip()
    album = tr.select_one('.info').select_one('.albumtitle').get_text().strip()
    rank_list.append(rank)
    title_list.append(title)
    artist_list.append(artist)
    album_list.append(album)
```

```
df = pd.DataFrame(lines, columns=['순위','곡명','가수','앨범'])
df.head()
```





### 5) 모든 페이지 데이터 가져오기

```
sub = 'https://www.genie.co.kr/chart/top200?ditc=D&ymd=20210817&hh=14&rtm=Y&pg='
rank_list, title_list, artist_list, album_list = [],[], [],[]

for page in range(1,5):
    url = f'{sub}{page}'
    req = requests.get(url, headers = header)
    html = req.text
    soup = BeautifulSoup(html, 'html.parser')
    trs = soup.select('tr.list')
    for tr in trs:
        rank = int(tr.select_one('.number').get_text().split('\n')[0])
        title = tr.select_one('.info').find('a').get_text().strip()
        artist = tr.select_one('.info').select_one('.artist').get_text().strip()
        album = tr.select_one('.info').select_one('.albumtitle').get_text().strip()
        rank_list.append(rank)
        title_list.append(title)
        artist_list.append(artist)
        album_list.append(album)
```

```
df = pd.DataFrame({
      '순위':rank_list, '곡명':title_list,
      '가수':artist_list, '앨범':album_list
})
df.tail()
```







## 4. 식신



```
import requests
import pandas as pd
from urllib.parse import quote
```



