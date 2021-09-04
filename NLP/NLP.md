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





####  TF-IDF(Term Frequency-Inverse Document Frequency)









## 5. 벡터의 유사도(Vector Similarity)



### 1) 코사인 유사도(Cosine Similarity)



