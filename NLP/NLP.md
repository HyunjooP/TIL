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



- 모듈 호출

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



