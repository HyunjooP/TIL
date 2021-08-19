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









## 5. Selenium

Selenium 설치

```
conda activate base
conda install selenium
```



크롬드라이버 다운로드 https://sites.google.com/a/chromium.org/chromedriver/downloads





## 6. 유튜브 랭킹(selenium)





url 가져오기

```
url ='https://youtube-rank.com/board/bbs/board.php?bo_table=youtube&page=1'
driver.get(url)
```

```
html = driver.page_source
soup = BeautifulSoup(html, 'html.parser')
```



css selector로 정보 가져오기

```
channel = channel_list[0]
category = channel.select_one('p.category').get_text().strip()
category
```

```
name = channel.select_one('.subject a').text.strip()
name
```

```
subscriber = channel.select_one('.subscriber_cnt').text
view = channel.select_one('.view_cnt').text
video = channel.select_one('.video_cnt').text[:-1]
subscriber,view, video
```



리스트로 만들기

```
channels = []
for channel in channel_list:
    category = channel.select_one('p.category').get_text().strip(' \n[]')
    name = channel.select_one('.subject a').text.strip()
    subscriber = channel.select_one('.subscriber_cnt').text
    view = channel.select_one('.view_cnt').text
    video = channel.select_one('.video_cnt').text[:-1]
    channels.append([category, name, subscriber, view, video])
```



데이터프레임으로 시각화

```
df = pd.DataFrame(channels, columns=['카테고리','채널','구독자수','조회수','콘텐츠수'])
df.head()
```





만과 억을 숫자로 바꿔보자

```
def convert_unit(s):
    #s = ''.join(s.split('억'))
    s = s.replace('억', '').replace('개','').replace(',','')
    s = s.replace('만', '0000')
    return f'{int(s):,d}'
```

```
convert_unit('123억6,557만개')
```





페이지 1~10까지

```
results = []
for page in range(1,11):
    url = 'https://youtube-rank.com/board/bbs/board.php?bo_table=youtube&page='+str(page)
    driver.get(url)
    time.sleep(3)
    html = driver.page_source
    soup = BeautifulSoup(html, 'html.parser')
    channel_list = soup.select('.aos-init')

    for channel in channel_list:
        category = channel.select_one('p.category').get_text().strip(' \n[]')
        name = channel.select_one('.subject a').text.strip()
        subscriber = convert_unit(channel.select_one('.subscriber_cnt').text)
        view = convert_unit(channel.select_one('.view_cnt').text)
        video = convert_unit(channel.select_one('.video_cnt').text)
        results.append([category,name,subscriber,view,video])
```











## 7. 유튜브 랭킹 시각화



파일 먼저 불러오고

```
df = pd.read_csv(filename)
df.head()
```



정수를 숫자로 변환

```
def str2int(x):
  return int(x.replace(',',''))
```



변환한 숫자 기준으로 정렬

```
df['비디오수2'] = df.비디오수.apply(str2int)
df.head()
```



top20 막대 그래프

```
df.sort_values(by='비디오수2', ascending=False).head(10)
```

```
df2 = df.sort_values(by='비디오수2', ascending=False).head(20)
plt.barh(df2['채널명'], df2['비디오수'])
plt.show()
```



sns로 시각화

```
import seaborn as sns
df2 = df[['채널명', '비디오수2']].sort_values(by='비디오수2', ascending=False)
sns.barplot(y='채널명', x='비디오수2', data=df2.head(20))
plt.title('비디오수 Top20 채널')
plt.show()
```



카테고리 숫자로 파이 그래프 만들기

```
df3 = df.카테고리.value_counts()
```

```
df3 = df.카테고리.value_counts().to_frame()
```

```
df3.plot.pie(autopct='%.2f%%')
plt.title("카테고리 수 채널별 분포")
plt.axis('equal')
plt.show()
```





## 8. 인스타그램 크롤링(제주명소)





사전 준비

```
from selenium import webdriver
from bs4 import BeautifulSoup
import time
import pandas as pd
```

```
# password.txt 파일 생성하여 gitignore에 추가
```

```
chromedriver = '/Users/fromh/Downloads/chromedriver'
driver = webdriver.Chrome(chromedriver)
```

```
insta_url = 'https://instagram.com'
driver.get(insta_url)
time.sleep(1)
```





인스타그램 로그인

```
with open('password.txt') as fp:
    password = fp.read()
```

```
email = 'nowdrink'
input_id = driver.find_elements_by_css_selector('input._2hvTZ.pexuQ.zyHYP')[0]
input_id.clear()
input_id.send_keys(email)

input_pw = driver.find_elements_by_css_selector('input._2hvTZ.pexuQ.zyHYP')[1]
input_pw.clear()
input_pw.send_keys(password)
input_pw.submit()
time.sleep(3)
```

오류 코드는 예외 적용

```
try:
    driver.find_element_by_css_selector('.sqdOP.yWX7d.y3zKF').click()
    time.sleep(1)
    driver.find_element_by_css_selector('.aOOlW.HoLwm').click()
    #time.sleep(1)
    #driver.find_element_by_css_selector('.aOOlW.HoLwm').click()
except:
    pass
```

```
try:
    driver.find_element_by_css_selector('.aOOlW.HoLwm').click()
    time.sleep(1)
except:
    pass
```





특정 해시태그로 검색

```
from urllib.parse import quote
keyword = '제주도맛집'
search_url = 'https://www.instagram.com/explore/tags/'
url = f'{search_url}{quote(keyword)}'
```

```
driver.get(url)
time.sleep(5)
```







게시글 열어보기

```
driver.find_element_by_css_selector('div._9AhH0').click()
time.sleep(1)
```



정보 가져오기

```
html = driver.page_source
soup = BeautifulSoup(html, 'html.parser')
```

```
import unicodedata
try:
    content = soup.select_one('div.C4VMK > span').text
    content = unicodedata.normalize('NFC', content)
except:
    content = ' '
```



해시태그만 가져오기(re 모듈)

```
import re
tags = re.findall(r'#[^\s#,\\]+', content)
```



작성일자 가져오기

```
# 작성일자
date = soup.select_one('time.FH9sR.Nzb55')['datetime'][:10]
```



좋아요 가져오기

```
try:
    like = soup.select_one('div.Nm9Fw').text[4:-1]
except:
    like = 0
```



위치정보 가져오기

```
try:
    place = soup.select('div.M30cS')[0].text
    place = unicodedata.normalize('NFC', place)
except:
    place = ' '
```



데이터 정리

```
row = [content, date, like, place, tags]
```





다음 게시글로 이동하기

```
driver.find_element_by_css_selector('a.coreSpriteRightPaginationArrow').click()
time.sleep(2)
```



게시글 여러개 수집

```
from tqdm.notebook import tqdm
```

```
for keyword in ['제주도맛집', '제주맛집', '제주도관광', '제주여행']:
```



```
df = pd.DataFrame(results, columns=['content','date','like','place','tags'])
    df.to_csv(f'data/{keyword}.csv', index=False)

    driver.find_element_by_xpath('/html/body/div[6]/div[3]/button').click()
    time.sleep(2)
```





```
# 4가지 csv 파일의 중복을 제거한 후 통합 저장

jeju_df = pd.DataFrame([])
for keyword in ['제주도맛집','제주맛집','제주도관광','제주여행']:
    df = pd.read_csv(f'data/{keyword}.csv')
    jeju_df = jeju_df.append(df)


jeju_df.head()
```







## 9.  워드 클라우드



파일에서 태그만 불러오기

```
import pandas as pd
raw_df = pd.read_csv(filename)
raw_df.tags[:3]
```



필요한 부분만 슬라이싱

```
tags[2:-2].split("', '")[:5]
```

```
tags_total = []
for tags in raw_df.tags:
    tags_total.extend(tags[2:-2].split("', '"))
```



해시태그 수 카운트

```
from collections import Counter, OrderedDict
```



데이터 정제

```
stopwords = ['#삭제하고 싶은 해시태그]



tags_total = [tag for tag in tags_total if tag not in stopwords]

tags_counts = Counter(tags_total)
tags_counts.most_common(50)tag_counts.most_common(50)
```

```
'''tag_total_refined = []
for tag in tags_total:
    if tag not in stopwords:
        tags_total_refined.append(tag)'''
```





워드클라우드 만들기

```
from wordcloud import WordCloud
import matplotlib.pyplot as plt
```



폰트 설치

```
! ls -l /usr/share/fonts/truetype/nanum
```



```
path = '/usr/share/fonts/truetype/nanum/NanumGothic.ttf'
wordcloud = WordCloud(font_path=path,
                      background_color='white',
                      max_words=100,
                      relative_scaling=0.3,
                      width=800, height=400
                      ).generate_from_frequencies(tag_counts)
plt.figure(figsize=(15,10))
plt.imshow(wordcloud)
plt.axis('off')
plt.show()
```

