## 선형대수
+ 데이터분석에 필요한 각종 계산을 돕는 학문
+ 선형대수를 사용하면 복잡한 계산과정을 간단한 수식으로 서술 가능
![Math](https://latex.codecogs.com/gif.latex?y%20%3D%20Xw)
+ 선형대수를 이해하는 관점 2가지
	* Numeric operation
	* Geometric intuition



## 데이터와 행렬
### 데이터 유형
+ 스칼라: 숫자 하나만으로 이루어진 데이터
![Math](https://latex.codecogs.com/gif.latex?x%20%5Cin%20R)
	
+ 벡터
	* 여러 숫자가 특정한 순서대로 모여있는 것
	* 기본적으로 열벡터로 상정
	* 특징벡터: 예측/추론 등의 문제에서 입력 데이터로 사용되는 데이터 벡터
	* ![Math](https://latex.codecogs.com/gif.latex?x%20%3D%20%5Cbegin%7Bbmatrix%7D%20x_%7B1%7D%20%5C%5C%20x_%7B2%7D%20%5C%5C%20x_%7B3%7D%20%5C%5C%20x_%7B4%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D)

+ 행렬(matrix)
	* 복수 차원의 데이터 레코드(벡터)를 합쳐서 표기
	* 행렬로 표시할 때는, 벡터를 열벡터가 아닌 행벡터로 표시
	* 스칼라, 벡터도 수학적으로 행렬
	* ![Math](https://latex.codecogs.com/gif.latex?X%20%3D%20%5Cbegin%7Bbmatrix%7D%20%5Cboxed%7B%5Cbegin%7Bmatrix%7D%20x_%7B1%2C%201%7D%20%26%20x_%7B1%2C%202%7D%20%26%20x_%7B1%2C%203%7D%20%26%20x_%7B1%2C%204%7D%5Cend%7Bmatrix%7D%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B2%2C%201%7D%20%26%20x_%7B2%2C%202%7D%20%26%20x_%7B2%2C%203%7D%20%26%20x_%7B2%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B3%2C%201%7D%20%26%20x_%7B3%2C%202%7D%20%26%20x_%7B3%2C%203%7D%20%26%20x_%7B3%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B4%2C%201%7D%20%26%20x_%7B4%2C%202%7D%20%26%20x_%7B4%2C%203%7D%20%26%20x_%7B4%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B5%2C%201%7D%20%26%20x_%7B5%2C%202%7D%20%26%20x_%7B5%2C%203%7D%20%26%20x_%7B5%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B6%2C%201%7D%20%26%20x_%7B6%2C%202%7D%20%26%20x_%7B6%2C%203%7D%20%26%20x_%7B6%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D)
	* ![Math](https://latex.codecogs.com/gif.latex?X%20%5Cin%20%5Cmathbf%7BR%7D%5E%7B6%5Ctimes%204%7D)

+ 텐서(tensor)
	* 위 표현들을 N 차원으로 일반화한 개념


### 전치 연산
+ 행렬의 행과 열을 바꾸는 연산
	* ![Math](https://latex.codecogs.com/gif.latex?X%20%3D%20%5Cbegin%7Bbmatrix%7D%20%5Cboxed%7B%5Cbegin%7Bmatrix%7D%20x_%7B1%2C%201%7D%20%26%20x_%7B1%2C%202%7D%20%26%20x_%7B1%2C%203%7D%20%26%20x_%7B1%2C%204%7D%5Cend%7Bmatrix%7D%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B2%2C%201%7D%20%26%20x_%7B2%2C%202%7D%20%26%20x_%7B2%2C%203%7D%20%26%20x_%7B2%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B3%2C%201%7D%20%26%20x_%7B3%2C%202%7D%20%26%20x_%7B3%2C%203%7D%20%26%20x_%7B3%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B4%2C%201%7D%20%26%20x_%7B4%2C%202%7D%20%26%20x_%7B4%2C%203%7D%20%26%20x_%7B4%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B5%2C%201%7D%20%26%20x_%7B5%2C%202%7D%20%26%20x_%7B5%2C%203%7D%20%26%20x_%7B5%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B6%2C%201%7D%20%26%20x_%7B6%2C%202%7D%20%26%20x_%7B6%2C%203%7D%20%26%20x_%7B6%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%5C%3B%5C%3B%20%5Crightarrow%20%5C%3B%5C%3B%20X%5ET%20%3D%20%5Cbegin%7Bbmatrix%7D%20%5Cboxed%7B%5Cbegin%7Bmatrix%7D%20x_%7B1%2C%201%7D%20%5C%5C%20x_%7B1%2C%202%7D%20%5C%5C%20x_%7B1%2C%203%7D%20%5C%5C%20x_%7B1%2C%204%7D%5Cend%7Bmatrix%7D%7D%20%26%20%5Cbegin%7Bmatrix%7D%20x_%7B2%2C%201%7D%20%5C%5C%20x_%7B2%2C%202%7D%20%5C%5C%20x_%7B2%2C%203%7D%20%5C%5C%20x_%7B2%2C%204%7D%5Cend%7Bmatrix%7D%20%26%20%5Cbegin%7Bmatrix%7D%20x_%7B3%2C%201%7D%20%5C%5C%20x_%7B3%2C%202%7D%20%5C%5C%20x_%7B3%2C%203%7D%20%5C%5C%20x_%7B3%2C%204%7D%5Cend%7Bmatrix%7D%20%26%20%5Cbegin%7Bmatrix%7D%20x_%7B4%2C%201%7D%20%5C%5C%20x_%7B4%2C%202%7D%20%5C%5C%20x_%7B4%2C%203%7D%20%5C%5C%20x_%7B4%2C%204%7D%5Cend%7Bmatrix%7D%20%26%20%5Cbegin%7Bmatrix%7D%20x_%7B5%2C%201%7D%20%5C%5C%20x_%7B5%2C%202%7D%20%5C%5C%20x_%7B5%2C%203%7D%20%5C%5C%20x_%7B5%2C%204%7D%5Cend%7Bmatrix%7D%20%26%20%5Cbegin%7Bmatrix%7D%20x_%7B6%2C%201%7D%20%5C%5C%20x_%7B6%2C%202%7D%20%5C%5C%20x_%7B6%2C%203%7D%20%5C%5C%20x_%7B6%2C%204%7D%5Cend%7Bmatrix%7D%20%26%20%5Cend%7Bbmatrix%7D)


### 행렬의 행 표기법과 열 표기법
+ 행렬의 복수의 열벡터 혹은 복수의 행벡터를 합친 형태로 표기 가능
	*  ![Math](https://latex.codecogs.com/gif.latex?X%20%3D%20%5Cbegin%7Bbmatrix%7D%20c_1%20%26%20c_2%20%26%20%5Ccdots%20%26%20c_M%20%5Cend%7Bbmatrix%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%20r_1%5ET%20%5C%5C%20r_2%5ET%20%5C%5C%20%5Cvdots%20%5C%5C%20r_N%5ET%20%5C%5C%20%5Cend%7Bbmatrix%7D)

### 특수한 벡터와 행렬
+ 영벡터: 모든 원소가 0인 N차원 벡터
	* ![Math](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B0%7D_N%20%3D%20%5Cmathbf%7B0%7D%20%3D%200%20%3D%20%5Cbegin%7Bbmatrix%7D%200%20%5C%5C%200%20%5C%5C%20%5Cvdots%20%5C%5C%200%20%5C%5C%20%5Cend%7Bbmatrix%7D)
+ 일벡터: 모든 원소가 1인 N차원 벡터
	* ![Math](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B1%7D_N%20%3D%20%5Cmathbf%7B1%7D%20%3D%201%20%3D%20%5Cbegin%7Bbmatrix%7D%201%20%5C%5C%201%20%5C%5C%20%5Cvdots%20%5C%5C%201%20%5C%5C%20%5Cend%7Bbmatrix%7D)
+ 정방행렬(square matrix): 행 개수와 열 개수가 같은 행렬
	* ![Math](https://latex.codecogs.com/gif.latex?X%20%5Cin%20%5Cmathbf%7BR%7D%5E%7BN%5Ctimes%20N%7D)
	* ![Math](https://latex.codecogs.com/gif.latex?X%20%3D%20%5Cbegin%7Bbmatrix%7D%20%5Cboxed%7B%5Cbegin%7Bmatrix%7D%20x_%7B1%2C%201%7D%20%26%20x_%7B1%2C%202%7D%20%26%20x_%7B1%2C%203%7D%20%26%20x_%7B1%2C%204%7D%5Cend%7Bmatrix%7D%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B2%2C%201%7D%20%26%20x_%7B2%2C%202%7D%20%26%20x_%7B2%2C%203%7D%20%26%20x_%7B2%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B3%2C%201%7D%20%26%20x_%7B3%2C%202%7D%20%26%20x_%7B3%2C%203%7D%20%26%20x_%7B3%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20x_%7B4%2C%201%7D%20%26%20x_%7B4%2C%202%7D%20%26%20x_%7B4%2C%203%7D%20%26%20x_%7B4%2C%204%7D%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cbegin%7Bmatrix%7D%20%5Cend%7Bmatrix%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%5C%3B%5C%3B)
+ 대각행렬(diagonal matrix): 모든 비대각 요소가 0인 행렬, 반드시 정방행렬일 필요 없음
	* ![Math](https://latex.codecogs.com/gif.latex?D%20%3D%20%5Cbegin%7Bbmatrix%7D%20d_%7B1%7D%20%26%200%20%26%20%5Ccdots%20%26%200%20%5C%5C%200%20%26%20d_%7B2%7D%20%26%20%5Ccdots%20%26%200%20%5C%5C%20%5Cvdots%20%26%20%5Cvdots%20%26%20%5Cddots%20%26%20%5Cvdots%20%5C%5C%200%20%26%200%20%26%20%5Ccdots%20%26%20d_%7BM%7D%20%5C%5C%200%20%26%200%20%26%20%5Ccdots%20%26%200%20%5C%5C%200%20%26%200%20%26%20%5Ccdots%20%26%200%20%5C%5C%200%20%26%200%20%26%20%5Ccdots%20%26%200%20%5C%5C%20%5Cend%7Bbmatrix%7D)
+ 항등행렬(identity matrix): 모든 대각요소가 1인 행렬
	* ![Math](https://latex.codecogs.com/gif.latex?I%20%3D%20%5Cbegin%7Bbmatrix%7D%201%20%26%200%20%26%20%5Ccdots%20%26%200%20%5C%5C%200%20%26%201%20%26%20%5Ccdots%20%26%200%20%5C%5C%20%5Cvdots%20%26%20%5Cvdots%20%26%20%5Cddots%20%26%20%5Cvdots%20%5C%5C%200%20%26%200%20%26%20%5Ccdots%20%26%201%20%5C%5C%20%5Cend%7Bbmatrix%7D)
+ 대칭행렬(symmetric matrix): 전치연산으로 얻은 전치행렬과 원래 행렬이 같은 행렬
	* ![Math](https://latex.codecogs.com/gif.latex?S%20%3D%20%5Cbegin%7Bbmatrix%7D%201%20%26%202%20%26%20%5Ccdots%20%26%205%20%5C%5C%202%20%26%201%20%26%20%5Ccdots%20%26%204%20%5C%5C%20%5Cvdots%20%26%20%5Cvdots%20%26%20%5Cddots%20%26%20%5Cvdots%20%5C%5C%205%20%26%204%20%26%20%5Ccdots%20%26%201%20%5C%5C%20%5Cend%7Bbmatrix%7D)
