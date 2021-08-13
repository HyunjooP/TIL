# 데이터 시각화(Data Visualization)

matplotlib 불러오기

```
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
```



## 1. 한글 폰트 설치



### Colab

나눔 폰트

```
!apt-get install -y fonts-nanum
!sudo fc-cache -fv
!rm ~/.cache/matplotlib -rf

# 자잘한 설명 안 뜨게 하고 싶으면 마지막에 > /dev/null 붙이기
```

코랩 런타임 다시 시작 후

```
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
```

```
# 마이너스 표시
mpl.rcParams['axes.unicode_minus'] = False
import matplotlib.pyplot as plt
plt.rc('font', family='NanumBarunGothic') 
```

### Jupyter Notebook 

```
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
```

```
# 마이너스 표시
mpl.rcParams['axes.unicode_minus'] = False
import matplotlib.pyplot as plt
plt.rc('font', family='Malgun Gothic') 
```



## 2. 라인 플롯

선을 그리는 라인 플롯(line plot)

```
plt.title("Plot")
plt.plot([1, 4, 9, 16])
plt.show()
```

```
plt.title("x ticks")
plt.plot([10, 20, 30, 40], [1, 4, 9, 16])
plt.show()
```



### 스타일 지정

색깔(color), 마커(marker), 선 종류(line style)

```
# 적용방법
plt.plot([10, 20, 30, 40], [1, 4, 9, 16], c="b",
         lw=5, ls="--", marker="o", ms=15, mec="g", mew=5, mfc="r")
plt.title("스타일 적용 예")
```



### 그림 범위 지정

xlim 명령과 ylim 명령을 사용

```

plt.title("x축, y축의 범위 설정")
plt.plot([10, 20, 30, 40], [1, 4, 9, 16],
         c="b", lw=5, ls="--", marker="o", ms=15, mec="g", mew=5, mfc="r")
plt.xlim(0, 50)
plt.ylim(-10, 30)
plt.show()
```



### 틱 설정

플롯이나 차트에서 축상의 위치 표시 지점을 틱(tick)

 `xticks` 명령이나 `yticks` 사용

```
X = np.linspace(-np.pi, np.pi, 256)
C = np.cos(X)
plt.title("x축과 y축의 tick label 설정")
plt.plot(X, C)
plt.xticks([-np.pi, -np.pi / 2, 0, np.pi / 2, np.pi])
plt.yticks([-1, 0, +1])
plt.show()
```



### 그리드 설정

틱 위치를 잘 보여주기 위한 그리드 설정

```
plt.grid(False)
plt.grid(True)
```





### 여러개의 선 그리기

x 데이터, y 데이터, 스타일 문자열을 반복하여 인수로 넘긴다.

```
t = np.arange(0., 5., 0.2)
plt.title("라인 플롯에서 여러개의 선 그리기")
plt.plot(t, t, 'r--', t, 0.5 * t**2, 'bs:', t, 0.2 * t**3, 'g^-')
plt.show()
```



### 범례(Legend)

legend 명령, loc 인수 사용

```
plt.plot(X, C, label="cosine") # label 사용
plt.plot(X, S, label="sine")
plt.legend(loc='lower center') # 위치
```





### x축, y축 라벨, 타이틀

xlabel, ylabel 사용

```
X = np.linspace(-np.pi, np.pi, 256)
C, S = np.cos(X), np.sin(X)
plt.plot(X, C, label="cosine")
plt.xlabel("time")
plt.ylabel("amplitude")
plt.title("Cosine Plot")
plt.show()
```



## 3. 여러 개의 그림 그리기

맷플롯리브가 그리는 그림은 Figure 객체, Axes 객체, Axis 객체 등으로 구성

- Figure 객체(그림이 그려지는 캔버스나 종이)는 한 개 이상의 Axes 객체를 포함하고

- Axes 객체는(하나의 플롯) 다시 두 개 이상의 Axis 객체(가로축이나 세로축)를 포함한다.

### Figure 객체

```
f1 = plt.figure(figsize=(10, 2))	# 사이즈가 10, 2
```



### Axes 객체와 subplot

여러 개의 플롯

```
subplot(2, 1, 1)
# 여기에서 윗부분에 그릴 플롯 명령 실행
subplot(2, 1, 2)
# 여기에서 아랫부분에 그릴 플롯 명령 실행
```







## 4. 다양한 플롯



### Bar chart

x 데이터가 카테고리 값인 경우

```
plt.bar(x, y)	
plt.barh(y_pos, performance, xerr=error, alpha=0.4) # 가로
```





### Pie chart

카테고리별 값의 상대적인 비교를 해야할 때

```
plt.axis('equal')
```

```
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct='%1.1f%%', shadow=True, startangle=90)
```



### Histogram

데이터의 분포를 확인하기 위함

```
arrays, bins, patches = plt.hist(x, bins=10)
```



### Scatter plot(산점도)

두 개의 실수 데이터 집합의 상관관계를 살펴볼 때 사용

```
plt.scatter(X, Y)
```



### Imshow

이미지 데이터

```
import matplotlib.image as img
```

```
image = img.imread('파일이름')
plt.imshow(image)
plt.show()
```

사이킷런

````
from sklearn.datasets import load_digits
digits = load_digits()
X = digits.images[0]
X
````



### Box plot

```
# setosa의 feature 박스 플롯

setosa = iris[iris.species == 'setosa']
plt.boxplot([setosa.sepal_length, setosa.sepal_width,
             setosa.petal_length, setosa.petal_width,],
            labels=['sepal_length','sepal_width','petal_length','setosa.petal_width' ])
plt.title('setosa의 feature 박스 플롯')
plt.show()
```





## 5. Seaborn



### 카운트 플롯

카테고리 값별로 데이터가 얼마나 있는지 확인



### 페어 플롯 (다차원 실수형 데이터)

3차원 이상의 데이터, 각 열의 조합을 스캐터 플롯으로 표현



### 2차원 카테고리 데이터

heatmap





### 다차원 복합데이터

예를 들어 barplot, violinplot, boxplot 등 에서는 두 가지 카테고리 값에 의한 실수 값의 변화를 보기 위한 hue 인수를 제공한다. hue 인수에 카테고리 값을 가지는 변수의 이름을 지정하면 카테고리 값에 따라 다르게 시각화된다. hue 값이 시각화되는 방법은 플롯의 종류에 따라 다르다.

```
sns.barplot(x="day", y="total_bill", hue="sex", data=tips)
```



