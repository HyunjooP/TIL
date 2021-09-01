# 딥러닝을 이용한 자연어 처리

참고 https://wikidocs.net/



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



- 토큰(token)이라 불리는 단위로 나누는 작업을 의미



- NLTK 모듈 호출

```
import nltk
nltk.download('punkt')
nltk.download('stopwords')
```



- KSS

```
# Korean Sentence Splitter
!pip install kss
```



**형태소(morpheme)**

- **자립 형태소** : 접사, 어미, 조사와 상관없이 자립하여 사용할 수 있는 형태소. 그 자체로 단어가 된다. 체언(명사, 대명사, 수사), 수식언(관형사, 부사), 감탄사 등이 있다.
- **의존 형태소** : 다른 형태소와 결합하여 사용되는 형태소. 접사, 어미, 조사, 어간를 말한다.





- morphs : 형태소 추출
- pos : 품사 태깅(Part-of-speech tagging)
- nouns : 명사 추출





### 불용어(Stopwords)

```
from nltk.corpus import stopwords
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

