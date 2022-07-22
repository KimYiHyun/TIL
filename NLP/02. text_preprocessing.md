# 자연어처리
</br>

### 텍스트 전처리


❓ **텍스트 전처리란?**
- 용도에 맞게 텍스트를 사전에 처리하는 작업
- 코퍼스(corpus)데이터를 용도에 맞게 토큰화(Tokenization), 정제(cleaning), 정규화(cormalization), 인코딩(encoding)함
    - 코퍼스 : 말뭉치 또는 말모둠. 언어 데이터를 모아둔 집합.
</br>

👉🏻 **토큰화**
- 주어진 코퍼스(corpus)에서 토큰(token) 단위로 나누는 작업 ⇒ 텍스트에 대한 정보를 의미있는 단위별로 구분
- 토큰의 단위가 상황에 따라 다르지만, 보통 의미있는 단위로 토큰을 정의
- NLTK, KoNLPY 라이브러리 이용
</br>

👉🏻 **단어 토큰화(Word Tokenization)**
- 토큰의 기준을 단어(word)로 하는 경우
- 이 때, 단어는 단어 단위 외에도 단어구, 의미를 갖는 문자열로도 간주됨
- 토큰화 작업은 단순히 구두점이나 특수문자를 전부 제거하는 정제(cleaning) 작업을 수행하는 것만으로 해결되지 않음
- 구두점이나 특수문자를 전부 제거하면 토큰이 의미를 잃어버리는 경우도 발생
- 영어는 띄어쓰기 단위로 자르면 단어 토큰이 구분되나, 한국어는 띄어쓰기만으로는 단어 토큰을 구분하기 어려움
</br>

 **word_tokenize 사용**

```python
import nltk
from nltk.tokenize import word_tokenize

print(word_tokenize("Don't be fooled by the dark sounding name, Mr.Jone's Orphanage is as cheery as cheery goes for a pastry shop."))
```

![image](https://user-images.githubusercontent.com/56059126/180484793-696ce891-eaac-4e47-968b-e95ada6a352d.png)

(Don’t를 Do와 n’t로 분히, Jone’s는 Jone과 ‘s로 분리)
</br></br>

**wordPunctTokenizer 사용**

```python
import nltk
from nltk.tokenize import WordPunctTokenizer

WordPunctTokenizer().tokenize("Don't be fooled by the dark sounding name, Mr.Jone's Orphanage is as cheery as cheery goes for a pastry shop.")
```

(구두점을 별도로 분류 ⇒ Don’t를 Don과 ‘와 t로 분리, Jone’s를 Jone과 ‘와 s로 분리)
</br></br>

**토큰화에서 고려해야할 사항**

- 구두점이나 특수문자를 단순 제외해서는 안됨
- 줄임말과 단어 내에 띄어쓰기가 있는 경우
</br>

### **한국어 토큰화의 어려움**

- 영어는 New York과 같은 합성어나 he’s와 같이 줄임말에 대한 예외처리만 한다면, 띄어쓰기를 기준으로 하는 띄어쓰기 토큰화를 수행해도 단어 토큰화가 잘 작동함
- 한국어는 영어와는 달리 띄어쓰기만으로는 토큰화를 하기에 부족
- 한국어의 경우 띄어쓰기 단위를 ‘어절’이라 하는데, 어절 토큰화는 한국어 NLP에서 지양되고 있음. ⇒ 어절 토큰화와 단어 토크화가 같지 않기 때문
- 한국어는 띄어쓰기가 영어보다 잘 지켜지지 않음.
</br>

### 형태소

- 의미를 가지는 최소의 단위 (어휘적 의미 + 문법적 의미)
- 한국어는 명사와 조사가 한 어절을 이루거나 용언(동사, 형용사)이 활용을 하여 어절의 구조가 복잡
- 한국어 토큰화에서는 형태소란 개념을 반드시 이해해야 함
    - 자립형태소
        - 접사, 어미, 조사와 상관없이 자립하여 사용할 수 있는 형태소
        - 그 자체로 단어가 됨
        - 체언(명사, 대명사, 수사), 수식언(관형사, 부사), 감탄사 등이 있음
    - 의존 형태소
        - 다른 형태소와 결합하여 사용되는 형태소
        - 접사, 어미, 조사, 어간
- 형태소 분석
    - 형태소보다 단위가 큰 언어 단위인 어절, 혹은 문장을 최소 의미 단위인 형태소로 분절하는 과정
    - ‘어절 분석’ 혹은 ‘형태론적 분석’이 더 적합한 용어라고 볼 수도 있음.
</br>    

### 품사

- 공통된 성질을 지닌 낱말의 범주(명사, 동사)
- 오픈 소스의 형태소 분석가들은 각각 다른 방법으로 품사를 지정해 형태소를 추출(품사 태깅)
- 대표적으로 KoNLPy 사용

![image](https://user-images.githubusercontent.com/56059126/180484981-abf8dbd6-f2d2-4c06-be2e-a16ef556b736.png)

</br>

1. Okt(Twitter) 분석기

```python
#형태소 단위로 분해
from konlpy.tag import Okt
okt=Okt()

print(okt.morphs("이 여름 다시 한번 설레고 싶다, 그 여름을 틀어줘. 싹쓰리"))
```
![image](https://user-images.githubusercontent.com/56059126/180485694-95cd00d6-93e9-4f57-97a6-f929407d4231.png)

```python
#품사(POS) 태깅
print(okt.pos("이 여름 다시 한번 설레고 싶다, 그 여름을 틀어줘. 싹쓰리")) 
```

![image](https://user-images.githubusercontent.com/56059126/180485131-1e4b61bd-c27b-4e0a-95b6-88d9cc9d5d59.png)

```python
#명사 추출
print(okt.nouns("이 여름 다시 한번 설레고 싶다, 그 여름을 틀어줘. 싹쓰리")) #명사 추출
```

![image](https://user-images.githubusercontent.com/56059126/180485167-56213e22-f3ec-42dc-8806-7b57bc7aa01f.png)

</br>

1. 한나눔 분석기

```python
#형태소 단위로 분해
from konlpy.tag import Hannanum
han = Hannanum()

print(han.morphs("이 여름 다시 한번 설레고 싶다, 그 여름을 틀어줘. 싹쓰리"))  
```

![image](https://user-images.githubusercontent.com/56059126/180485231-031a6236-5680-4be5-9955-d633e67504bc.png)

```python
#품사(POS) 태깅
print(han.pos("이 여름 다시 한번 설레고 싶다, 그 여름을 틀어줘. 싹쓰리")) 
```

![image](https://user-images.githubusercontent.com/56059126/180485266-c31f841c-38bc-4ba1-93fd-59dc339232ad.png)

```python
#명사 추출
print(han.nouns("이 여름 다시 한번 설레고 싶다, 그 여름을 틀어줘. 싹쓰리"))  #명사분석
```

![image](https://user-images.githubusercontent.com/56059126/180485295-9879580f-469d-4102-a52a-5876459596e5.png)

</br>

### Corpus 이용

- 텍스트의 모음
    - Konlpy에는 한국 법률 말뭉치와 대한민국 국회의안 말뭉치가 존재

```python
import konlpy
from konlpy.corpus import kolaw   
from konlpy.tag import Okt

kot = Okt()

law_corpus = kolaw.open('constitution.txt').read()
law_corpus[:50]
```

![image](https://user-images.githubusercontent.com/56059126/180485350-045f3e2a-24d1-4e55-9d8f-52d934910b40.png)

```python
#품사 태깅
okt.pos(law_corpus[:50])
```

![image](https://user-images.githubusercontent.com/56059126/180485392-9a96f2ff-c41f-4b77-a9d2-7540d4f1888a.png)
</br></br>

### 정제(Cleaning)

- 코퍼스에서 노이즈 데이터 제거
    - 정제 작업은 토큰화 작업에 방해가 되는 부분들을 배제시키고, 토큰화 작업을 수행하기 위해서 토큰화 작업보다 앞서 이루어지기도 하지만
    - 토큰화 작업 이후에도 여전히 남아있는 노이즈들을 제거하기 위해 지속적으로 이루어지기도 함
    - 완벽한 정제 작업은 어려운 편이라서, 대부분의 경우 ‘이 정도면 됐다’ 라는 일종의 합의점을 찾기도 함
- 동일한 표현의 표기가 다른 단어들 통합
    - 같은 의미를 갖고 있음에도 표기가 다른 단어들을 하나의 단어로 정규화하는 방법을 사용
- 대, 소문자 통합
    - 영어권 언어에서 대, 소문자를 통합하는 것은 단어의 개수를 줄일 수 있는 또 다른 정규화 방법
    - 그러나, 대문자와 소문자를 무작정 통합해서는 안됨
    

```python
import re

#숫자만 제외
text1 = "서울 부동산 가격이 올해 들어 평균 30% 상승했습니다"

p = re.compile("[0-9]+")
p.sub("", text1)

#'서울 부동산 가격이 올해 들어 평균 % 상승했습니다'
```

```python
#문장부호, 특수문자 제외
text2 = "서울 부동산 가격이 올해 들어 평균 30% 상승했습니다!"

p = re.compile("\W+")
p.sub(" ", text2)

#'서울 부동산 가격이 올해 들어 평균 30 상승했습니다 '
```

```python
#*만 제외
text3 = "*서울 부동산 가격이 올해 들어 평균 30% 상승했습니다!"

p = re.compile("\*")
p.sub("", text3)

#'서울 부동산 가격이 올해 들어 평균 30% 상승했습니다!'
```
</br>

- 불필요한 단어의 제거
    - 불용어(Stopword) 제거
        - 문장 내에 자주 등장하지만 문장을 분석하는 데 있어서는 큰 도움이 되지 않는 단어들
    - 등장 빈도가 적은 단어
        - 텍스트 데이터에서 너무 적게 등장해서 자연어 처리에 도움이 되지 않는 단어들 제거
    - 길이가 짧은 단어
        - 영어권 언어에서 길이가 짧은 단어들은 대부분 불용어에 해당
        - 한국어에서는 길이가 짧은 단어라고 삭제하는 방법이 유효하지 않을 수 있음
        - 한국어 단어는 한자어가 많고, 한 글자만으로도 의미를 가진 경우가 많기 때문에
</br>

```python
import nltk 
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

example ="Family is not an important thing. It 's everything."
stop_words = set(stopwords.words('english'))

word_tokens = word_tokenize(example)
result = []

for w in word_tokens:
    if w not in stop_words:
        result.append(w)
        
print(word_tokens)
print(result)
```

![image](https://user-images.githubusercontent.com/56059126/180485481-4381846c-24ac-4c70-a1dd-b1ad9cbd06ed.png)
</br>

```python
import nltk 
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

example = """이 여름 다시 한번 설레고 싶다 그때 그 여름을 틀어줘 그 여름을 들려줘
이 여름도 언젠가는 그해 여름 오늘이 가장 젊은 내 여름"""
stop_words = "이 그 또 가장"

stop_words = stop_words.split(' ')

word_tokens = word_tokenize(example)
result =[]

for w in word_tokens:
    if w not in stop_words:
        result.append(w)
        
print(word_tokens)
print(result)
```

![image](https://user-images.githubusercontent.com/56059126/180485509-05bd251d-0691-453e-938b-16645e3aa4ed.png)
