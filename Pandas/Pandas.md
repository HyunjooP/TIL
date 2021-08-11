# Pandas



- Cheat sheet이 두 장, 양이 상당히 많음
- 넘파이와는 인덱싱 방법이 조금 다름
  - 열을 Series 라고 표현, 여러개가 모여 - Data Frame이라 부름
- csv(comma separated values) 파일을 이용
  - 공공데이터는 대부분 csv 형식

- numpy와 padas 불러오기

```
import numpy as np
import pandas as pd
```



## 1. Series



시리즈 = 값 + 인덱스

시리즈 생성, 인덱스 값 부여

```python
s = pd.Series([9904312, 3448737, 2890451, 2466052],
              index=["서울", "부산", "인천", "대구"])
```

시리즈의 값 - 넘파이의 배열

```
s.values
```

시리즈의 인덱스

```
s.index
```

인덱스 이름

```
s.name = "인구"
s.index.name = "도시"
```

시리즈 인덱싱

```
s[1], s["부산"], s.부산
s[3], s["대구"], s.대구
```

```
# 인덱스로 슬라이싱하면 마지막까지 포함됨
s['부산':'대구']
```

```
s[[0,3,1]]
# 리스트 형태로 주면 2차원으로 나옴
```

```
# 필터링
s[(2500000 < s ) & ( s < 3000000)]
```



### 딕셔너리

```
s2 = pd.Series({"서울": 9631482, "부산": 3393191, "인천": 2632035, "대전": 1490158},
               index=["부산", "서울", "인천", "대전"])
               
'서울' in s2
# 키 값으로 맵핑 가능
```



### 인덱스 기반 연산

```
s.values - s2.values
```

```
# 데이터 갱신 및 추가 가능
rs['부산'] = 1.63
```



## 2. Data Frame

colums = 열방향 인덱스(컬럼)의 순서

index = 인덱스의 순서

```
df = pd.DataFrame(data, index=index, columns=columns)
```



행 데이터

```
행 데이터는 슬라이싱으로 표현
```





열 데이터의 갱신, 추가, 삭제

```
# 열 데이터 추가
df['2020'] = [1,2,3,4]
```

```
# 하나의 열만 인덱싱하면 시리즈가 반환
df["지역"]
```

데이터 프레임으로 표현하는 방법 [[ ]]

```
df[['지역','2015']]   # Dataframe
```





### 개별 데이터 인덱싱

무조건 열 먼저

```
df[열][행]
```







### 데이터 입출력

csv 파일 읽는 방법

```
pd.read_csv('sample1.csv')
```

열 인덱스 정보가 없는 경우

```
pd.read_csv('sample2.csv', names=['c1', 'c2', 'c3'])
# name으로 지정해줌
```

```
pd.read_csv('sample1.csv', index_col='c1')
# 특정한 열 인덱싱 처리
```



csv가 아니거나 데이터에 조작이 필요한 경우

```
# sep 사용
pd.read_table('sample3.txt', sep='\s+')
```

건너 뛰어야 하는 행

```
pd.read_csv('sample4.txt', skiprows=[0, 1])
```

누락된 데이터는 NaN으로 표시

```
pd.read_csv('s5.csv', na_values=['누락', ' '])
```





csv 파일 출력

```
df.to_csv('sample6.csv')
```

```
df.to_csv('sample7.txt', sep='|')
# sep으로 구분
```

```
df.index = ["a", "b", "c"]
df.to_csv('sample9.csv', index=False, header=False)
# 헤더 출력
```





인터넷상의 csv 파일

```
df = pd.read_csv(경로)
```

```
df.head(5)
# 상단 5행만 갖고오자
```





## 3. 고급 인덱싱



loc 인덱서

```
# 행 하나만
df.loc['x']
```

```
# 행은 슬라이싱으로 
df.loc['x':'y']
```

```
# 데이터 리스트
df.loc[["b", "c"]]
```



인덱서 2개를 받는 경우

```
df.loc['x','A']
# 행과 열
```

```
# 슬라이싱 가능
df.loc['y':, 'B']
```



iloc 인덱서

```
# 정수 인덱싱만 가능
df.iloc[0,0]
```







## 4. 데이터 오퍼레이션



데이터 갯수 세기

```
s = pd.Series(range(10))
s[3] = np.nan

s.count()
```

```
titanic.describe()
titanic.info()
# 등등으로 데이터 보기
```



anscombe?

- 산포도를 통해 눈으로 먼저 확인

```
anscombe = sns.load_dataset('anscombe')
anscombe
```



카테고리 값 세기

```
# value.counts
titanic.sex.value_counts()
```



정렬

```
s2.value_counts().sort_index()

# 내림차순
s.sort_values(ascending=False)
```



행/열 합계

```
# sum(axis)
np.random.seed(1)
df2 = pd.DataFrame(np.random.randint(10, size=(4, 8)))
```







### apply 변환



```
# 최대값 최소값 차이
df3.apply(lambda x: x.max() - x.min()
df3.apply(lambda x: x.max() - x.min(), axis=1)
```

예시) 타이타닉호 승객 중 20살을 기준으로 성인/미성년 구분 데이터 만들기



### fillna method

```
# NaN 값을 원하는 값으로 변경하는 메서드
df3.apply(pd.value_counts).fillna(0.0)
```





### astype

```
# 전체 데이터 자료형을 변경할 때
df3.apply(pd.value_counts).fillna(0.0).astype(int)
```



실수 값을 카테고리 값으로 변환

- `cut`: 실수 값의 경계선을 지정하는 경우
- `qcut`: 갯수가 똑같은 구간으로 나누는 경우





## 5. 인덱스 조작

- `set_index` : 기존의 행 인덱스를 제거하고 데이터 열 중 하나를 인덱스로 설정
- `reset_index` : 기존의 행 인덱스를 제거하고 인덱스를 데이터 열로 추가

```
# 특정한 열을 인덱스로 설정하기
df2 = df1.set_index("C1")
```

