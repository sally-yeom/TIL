## 선형대수
----
+ 데이터분석에 필요한 각종 계산을 돕는 학문
+ 선형대수를 사용하면 복잡한 계산과정을 간단한 수식으로 서술 가능
![Math](https://latex.codecogs.com/gif.latex?y%20%3D%20Xw)
+ 선형대수를 이해하는 관점 2가지
	* Numeric operation
	* Geometric intuition



## 데이터와 행렬
----
### 데이터 유형
+ 스칼라: 숫자 하나만으로 이루어진 데이터
![Math](https://latex.codecogs.com/gif.latex?x%20%5Cin%20R)
	
+ 벡터
	* 여러 숫자가 특정한 순서대로 모여있는 것
	* 기본적으로 열벡터로 상정
	* 특징벡터: 예측/추론 등의 문제에서 입력 데이터로 사용되는 데이터 벡터
![Math](https://latex.codecogs.com/gif.latex?x%20%3D%20%5Cbegin%7Bbmatrix%7D%20x_%7B1%7D%20%5C%5C%20x_%7B2%7D%20%5C%5C%20x_%7B3%7D%20%5C%5C%20x_%7B4%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D)

+ 행렬(matrix)
	* 복수 차원의 데이터 레코드(벡터)를 합쳐서 표기
	* 행렬로 표시할 때는, 벡터를 열벡터가 아닌 행벡터로 표시
	* 스칼라, 벡터도 수학적으로 행렬
![Math](https://latex.codecogs.com/gif.latex?X%20%3D%20%5Cbegin%7Bbmatrix%7D%20%5Cboxed%7B%5Cbegin%7Bmatrix%7D%20x_%7B1%2C%201%7D%20%26%20x_%7B1%2C%202%7D%20%26%20x_%7B1%2C%203%7D%20%26%20x_%7B1%2C%204%7D%5Cend%7Bmatrix%7D%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B2%2C%201%7D%20%26%20x_%7B2%2C%202%7D%20%26%20x_%7B2%2C%203%7D%20%26%20x_%7B2%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B3%2C%201%7D%20%26%20x_%7B3%2C%202%7D%20%26%20x_%7B3%2C%203%7D%20%26%20x_%7B3%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B4%2C%201%7D%20%26%20x_%7B4%2C%202%7D%20%26%20x_%7B4%2C%203%7D%20%26%20x_%7B4%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B5%2C%201%7D%20%26%20x_%7B5%2C%202%7D%20%26%20x_%7B5%2C%203%7D%20%26%20x_%7B5%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B6%2C%201%7D%20%26%20x_%7B6%2C%202%7D%20%26%20x_%7B6%2C%203%7D%20%26%20x_%7B6%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D)
	![Math](https://latex.codecogs.com/gif.latex?X%20%5Cin%20%5Cmathbf%7BR%7D%5E%7B6%5Ctimes%204%7D)

+ 텐서(tensor)
	* 위 표현들을 N 차원으로 일반화한 개념

