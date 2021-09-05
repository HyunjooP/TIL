# 딥러닝을 이용한 자연어 처리

참고 https://wikidocs.net/



**Natural Language Prosessing**



- 응용 사례

  - 텍스트 요약 (Summly)
  - 자동 질의 응답 (Wolfram Alpha)
  - 대화 시스템 (Siri)
  - 기계 번역 (Google Translate)
  - 검색엔진 등

- 파이썬 패키지

  - 말뭉치: 샘플 문서 집합

  - 토큰 생성: 문장 분석을 위해 나뉘어진 작은 문자열

  - 형태소 분석

  - 품사 부착

    

## 1. 텍스트 전처리

### 1) 토큰화(Tokenization)



- corpus를 토큰(token)이라 불리는 단위로 나누는 작업을 의미



#### 단어 토큰화

- NLTK 모듈 호출 방법

```
import nltk
nltk.download('punkt')
nltk.download('stopwords')		# 불용어 다운로드	
```



#### 문장 토큰화

- KSS(Korean Sentence Splitter) 다운로드

```
# Korean Sentence Splitter
!pip install kss
```



#### 이진 분류기

- 마침표가 단어의 일부분일 경우(ex. ph.D)
- 마침표가 문장의 구분자일 경우



#### 한국어 토큰화

 

- KoNLPy 패키지를 주로 이용
  - Okt(Open Korea Text)
  - 메캅(Mecab)
  - 코모란(Komoran)
  - 한나눔(Hannanum)
  - 꼬꼬마(Kkma)





**형태소(morpheme), 뜻을 작은 말의 단위**

- **자립 형태소** : 접사, 어미, 조사와 상관없이 자립하여 사용할 수 있는 형태소. 그 자체로 단어가 된다. 체언(명사, 대명사, 수사), 수식언(관형사, 부사), 감탄사 등이 있다.
- **의존 형태소** : 다른 형태소와 결합하여 사용되는 형태소. 접사, 어미, 조사, 어간를 말한다.



- morphs : 형태소 추출

````
from konlpy.tag import Okt  
okt=Okt()  
print(okt.morphs("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))
````

```
['열심히', '코딩', '한', '당신', ',', '연휴', '에는', '여행', '을', '가봐요']  
```



- pos : 품사 태깅(Part-of-speech tagging)

````
print(okt.pos("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))  
````

```
[('열심히','Adverb'), ('코딩', 'Noun'), ('한', 'Josa'), ('당신', 'Noun'), (',', 'Punctuation'), ('연휴', 'Noun'), ('에는', 'Josa'), ('여행', 'Noun'), ('을', 'Josa'), ('가봐요', 'Verb')] 
```



- nouns : 명사 추출

````
print(okt.nouns("열심히 코딩한 당신, 연휴에는 여행을 가봐요")) 
````

```
['코딩', '당신', '연휴', '여행']  
```



### 2) 정제(Cleaning) 및 정규화(Normalization)

- 정제(cleaning) : 갖고 있는 코퍼스로부터 노이즈 데이터를 제거한다.
- 정규화(normalization) : 표현 방법이 다른 단어들을 통합시켜서 같은 단어로 만들어준다.



정제 및 정규화 기법

1. 표기가 다른 단어들의 통합

2. 대, 소문자 통합

3. 불필요한 단어 제거
4. 정규 표현식



### 3) 어간추출(Stemming)과 표제어추출(Lemmatization)

- corpus의 복잡도를 줄이기 위해 하나의 단어로 일반화 시키는 것





#### **표제어 추출(Lemmatization)**

- 품사의 정보와 함께 Lemma 추출

```
n.lemmatize('dies', 'v')
```

```
'die'
```



```
n.lemmatize('watched', 'v')
```

```
'watch'
```



#### 어간 추출(Stemming)

- 단어의 의미(줄기?)를 추출

```
words=['formalize', 'allowance', 'electricical']
print([s.stem(w) for w in words])
```

```
['formal', 'allow', 'electric']
```





- 어간 추출과 표제어 추출의 차이

|           | **Stemming** | **Lemmatization** |
| --------- | ------------ | ----------------- |
| am        | am           | be                |
| the going | the go       | the going         |
| having    | hav          | have              |





### 4) 불용어(Stopwords)

- 큰 의미가 없는 단어 토큰화

- NLTK에서 불용어 활용

```
from nltk.corpus import stopwords
```



### 5) 정규 표현식(Regular Expression)

- re 모듈을 이용한 텍스트 정제



#### 정규표현식 문법

| 특수 문자      | 설명                                                         |
| :------------- | :----------------------------------------------------------- |
| .              | 한 개의 임의의 문자를 나타냅니다. (줄바꿈 문자인 \n는 제외)  |
| ?              | 앞의 문자가 존재할 수도 있고, 존재하지 않을 수도 있습니다. (문자가 0개 또는 1개) |
| *              | 앞의 문자가 무한개로 존재할 수도 있고, 존재하지 않을 수도 있습니다. (문자가 0개 이상) |
| +              | 앞의 문자가 최소 한 개 이상 존재합니다. (문자가 1개 이상)    |
| ^              | 뒤의 문자로 문자열이 시작됩니다.                             |
| $              | 앞의 문자로 문자열이 끝납니다.                               |
| {숫자}         | 숫자만큼 반복합니다.                                         |
| {숫자1, 숫자2} | 숫자1 이상 숫자2 이하만큼 반복합니다. <br />?, *, +를 이것으로 대체할 수 있습니다. |
| {숫자,}        | 숫자 이상만큼 반복합니다.                                    |
| [ ]            | 대괄호 안의 문자들 중 한 개의 문자와 매치합니다. [amk]라고 한다면 a 또는 m 또는 k 중 하나라도 존재하면 매치를 의미합니다. [a-z]와 같이 범위를 지정할 수도 있습니다. [a-zA-Z]는 알파벳 전체를 의미하는 범위이며, 문자열에 알파벳이 존재하면 매치를 의미합니다. |
| [^문자]        | 해당 문자를 제외한 문자를 매치합니다.                        |
| l              | AlB와 같이 쓰이며 A 또는 B의 의미를 가집니다.                |





| 문자 규칙 | 설명                                                         |
| :-------- | :----------------------------------------------------------- |
| \         | 역 슬래쉬 문자 자체를 의미합니다                             |
| \d        | 모든 숫자를 의미합니다. [0-9]와 의미가 동일합니다.           |
| \D        | 숫자를 제외한 모든 문자를 의미합니다. [^0-9]와 의미가 동일합니다. |
| \s        | 공백을 의미합니다. [ \t\n\r\f\v]와 의미가 동일합니다.        |
| \S        | 공백을 제외한 문자를 의미합니다. [^ \t\n\r\f\v]와 의미가 동일합니다. |
| \w        | 문자 또는 숫자를 의미합니다. [a-zA-Z0-9]와 의미가 동일합니다. |
| \W        | 문자 또는 숫자가 아닌 문자를 의미합니다. [^a-zA-Z0-9]와 의미가 동일합니다. |





#### 정규표현식 모듈 함수



| 모듈 함수     | 설명                                                         |
| :------------ | :----------------------------------------------------------- |
| re.compile()  | 정규표현식을 컴파일하는 함수입니다. 다시 말해, 파이썬에게 전해주는 역할을 합니다. 찾고자 하는 패턴이 빈번한 경우에는 미리 컴파일해놓고 사용하면 속도와 편의성면에서 유리합니다. |
| re.search()   | 문자열 전체에 대해서 정규표현식과 매치되는지를 검색합니다.   |
| re.match()    | 문자열의 처음이 정규표현식과 매치되는지를 검색합니다.        |
| re.split()    | 정규 표현식을 기준으로 문자열을 분리하여 리스트로 리턴합니다. |
| re.findall()  | 문자열에서 정규 표현식과 매치되는 모든 경우의 문자열을 찾아서 리스트로 리턴합니다. 만약, 매치되는 문자열이 없다면 빈 리스트가 리턴됩니다. |
| re.finditer() | 문자열에서 정규 표현식과 매치되는 모든 경우의 문자열에 대한 이터레이터 객체를 리턴합니다. |
| re.sub()      | 문자열에서 정규 표현식과 일치하는 부분에 대해서 다른 문자열로 대체합니다. |



### 6) 정수 인코딩(Integer Encoding)

- 각 단어를 고유한 정수에 맵핑 시키는 작업
- 빈도수로 정렬한 뒤에 인덱스 부여



#### Counter 사용하기

```
from collections import Counter
```

#### NLTK의 FreqDist 사용하기

```
from nltk import FreqDist
```

#### Enumerate 

```
test=['a', 'b', 'c', 'd', 'e']
for index, value in enumerate(test): 
# 입력의 순서대로 0부터 인덱스를 부여함.
  print("value : {}, index: {}".format(value, index))
```





#### Keras의 텍스트 전처리

- 기본적인 전처리를 위한 도구 제공

```
from tensorflow.keras.preprocessing.text import Tokenizer
```

```
tokenizer = Tokenizer()
tokenizer.fit_on_texts(sentences) # fit_on_texts()안에 코퍼스를 입력으로 하면 빈도수를 기준으로 단어 집합을 생성한다.
```







### 7) 패딩(Padding)

- 여러 문장의 길이를 임의로 동일하게 맞춰주는 작업



#### Numpy

```
import numpy as np
from tensorflow.keras.preprocessing.text import Tokenizer
```

데이터 -> 정수 인코딩 -> 정수 맵핑 후 출력 -> 긴문장 길이 계산 -> 가장 긴 문장 길이에 맞춰 숫자 0이 같은 길이로 패딩됨



#### Keras

```
from tensorflow.keras.preprocessing.sequence import pad_sequences
```







### 8) 원-핫  인코딩 (One-Hot Encoding)

단어 집합(Vocabulary)에 정수 인덱스를 부여하여 벡터로 다루는 것.



(1) 각 단어에 고유한 인덱스를 부여하고 (정수 인코딩)
(2) 표현하고 싶은 단어의 인덱스의 위치에 1을 부여하고, 다른 단어의 인덱스의 위치에는 0을 부여

```
from konlpy.tag import Okt  
okt=Okt()  
token=okt.morphs("나는 자연어 처리를 배운다")  
print(token)
```

```
['나', '는', '자연어', '처리', '를', '배운다']  
```



```
word2index={}
for voca in token:
     if voca not in word2index.keys():
       word2index[voca]=len(word2index)
print(word2index)
```

```
{'나': 0, '는': 1, '자연어': 2, '처리': 3, '를': 4, '배운다': 5} 
```



```
def one_hot_encoding(word, word2index):
       one_hot_vector = [0]*(len(word2index))
       index=word2index[word]
       one_hot_vector[index]=1
       return one_hot_vector
```

```
one_hot_encoding("자연어",word2index)
```

```
[0, 0, 1, 0, 0, 0]  
```





### 9) 데이터의 분리(Spltting Data)



#### 지도 학습(Supervised Learning)

- 훈련/테스트 파일 분리



#### X와 y 분리하기

- Scikit-learn으로 분리하기

```
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size= 0.2, random_state=1234)
```







### 10) 한국어 전처리 패키지



1) PyKoSpacing: 띄어쓰기 패키지
2) Py-Hanspell: 네이버 맞춤법 검사기 기반
3) SOYNLP: 품사 태깅, 다어 토큰화 지원

```
!pip install soynlp
```

- 신조어 문제
- 학습하기
- 응집확률: 내부 문자열이 얼마나 응집하여 자주 등장하는지 판단
- 브랜칭 엔트로피: 다음 문자가 등장할 수치 계산
- L tokenizer: 가장 높은 분리 기준을 찾아냄
- 최대 점수 토크나이저: 띄어쓰기
- 반복되는 문자 정제

```
from soynlp.normalizer import *
```



- Customized KoNLPy

```
pip install customized_konlpy
```

```
from ckonlpy.tag import Twitter
```









## 2. 언어 모델



### 1) 언어 모델(Language Model)

- 가장 자연스러운 단어 시퀀스를 찾아내는 모델

- 확률 할당
  - 기계 번역
  - 오타 번역
  - 음성 인식
- 주어진 이전 단어들로부터 다음 단어 예측



### 2) 통계적 언어 모델(Statistical Language Model, SLM)

- 조건부 확률
- 문장에 대한 확률
- 카운트 기반의 접근



### 3) N-gram 언어 모델

- 모든 단어를 고려하는 것이 아닌, 일부 단어만 고려하는 접근방법
- n개의 연속적인 단어 나열
- n개의 단어 뭉치 단위로 끊어서 하나의 토큰으로 간주



### 4) 한국어에서의 언어 모델

- 한국어는 어순이 중요하지 않다





### 5) 펄플렉서티(Perplexity)

- 언어 모델을 비교하여 내부평가 하는 것







## 4. 카운트 기반의 단어 표현

- 국소표현(Local Representation): 단어 자체만 표현
- 분산표현(Distributed Reoresentation): 주변을 참고하여 표현



![image-20210901102157725](C:\Users\fromh\AppData\Roaming\Typora\typora-user-images\image-20210901102157725.png)



### 1) Bag of Words(BoW)

- 순서 고려하지 않고 출현 빈도에만 집중
- 국소 표현, 단어의 빈도수를 카운트하여 단어를 수치화하는 표현 방법



#### Count Vectorizer

```
from sklearn.feature_extraction.text import CountVectorizer
```



### 2) DTM(Document-Term Matrix, 문서 단어 행렬)

- 서로 다른 문서들의 BoW들을 결합한 표현 방법
- 다수의 문서에서 등장하는 각 단어들의 빈도를 행렬로 표현함





####  TF-IDF(Term Frequency-Inverse Document Frequency)

- 단어 빈도-역 문서 빈도







## 5. 벡터의 유사도(Vector Similarity)

문서들 간에 동일한 단어 또는 비슷한 단어가 얼마나 공통적으로

많이 사용되었는지 수치화



### 1) 코사인 유사도(Cosine Similarity)

- 두 벡터 간의 코사인 각도를 이용해 유사도를 구함



#### 유사도를 이용한 추천 시스템 구현

- IMDB







## 6. 토픽 모델링(Topic Modeling)







## 10. 워드 임베딩(Word Embedding)



### 1) 워드 임베딩



### 2) 워드투벡터



