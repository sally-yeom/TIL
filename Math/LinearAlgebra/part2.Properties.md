## 벡터와 행렬의 연산
### 벡터/행렬의 덧셈과 뺄셈
+ 요소 별 연산(element-wise)
	* ![Math](https://latex.codecogs.com/gif.latex?x%20&plus;%20y%20%3D%20%5Cbegin%7Bbmatrix%7D%2010%20%5C%5C%2011%20%5C%5C%2012%20%5C%5C%20%5Cend%7Bbmatrix%7D%20&plus;%20%5Cbegin%7Bbmatrix%7D%200%20%5C%5C%201%20%5C%5C%202%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%2010%20&plus;%200%20%5C%5C%2011%20&plus;%201%20%5C%5C%2012%20&plus;%202%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%2010%20%5C%5C%2012%20%5C%5C%2014%20%5C%5C%20%5Cend%7Bbmatrix%7D)

### 스칼라와 벡터/행렬의 곱셈
+ 벡터, 행렬의 모든 원소에 스칼라c를 곱하는 것
	* ![Math](https://latex.codecogs.com/gif.latex?c%20%5Cbegin%7Bbmatrix%7D%20a_%7B11%7D%20%26%20a_%7B12%7D%20%5C%5C%20a_%7B21%7D%20%26%20a_%7B22%7D%20%5Cend%7Bbmatrix%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%20ca_%7B11%7D%20%26%20ca_%7B12%7D%20%5C%5C%20ca_%7B21%7D%20%26%20ca_%7B22%7D%20%5Cend%7Bbmatrix%7D)

### 브로드캐스팅
+ 벡터와 스칼라의 경우, 관례적으로 1-벡터 사용
	* ![Math](https://latex.codecogs.com/gif.latex?%5Cbegin%7Bbmatrix%7D%2010%20%5C%5C%2011%20%5C%5C%2012%20%5C%5C%20%5Cend%7Bbmatrix%7D%20-%2010%20%3D%20%5Cbegin%7Bbmatrix%7D%2010%20%5C%5C%2011%20%5C%5C%2012%20%5C%5C%20%5Cend%7Bbmatrix%7D%20-%2010%5Ccdot%20%5Cmathbf%7B1%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%2010%20%5C%5C%2011%20%5C%5C%2012%20%5C%5C%20%5Cend%7Bbmatrix%7D%20-%20%5Cbegin%7Bbmatrix%7D%2010%20%5C%5C%2010%20%5C%5C%2010%20%5C%5C%20%5Cend%7Bbmatrix%7D)

### 선형조합(linear combination)
+ 벡터/행렬에 아래의 스칼라 값을 곱한 후 더하거나 뺀 것
	* ![Math](https://latex.codecogs.com/gif.latex?c_1x_1%20&plus;%20c_2x_2%20&plus;%20c_3x_3%20&plus;%20%5Ccdots%20&plus;%20c_Lx_L%20%3D%20x)

### 벡터와 벡터의 곱셈
+ 내적(inner product/dot product): 벡터와 벡터의 곱
+ 조건
	* 두 벡터의 차원(길이)가 같아야 함
	* 앞 벡터가 행벡터이고 뒤 벡터가 열벡터여야 함
	* ![Math](https://latex.codecogs.com/gif.latex?x%5ETy)
	* ![Math](https://latex.codecogs.com/gif.latex?x%5ET%20y%20%3D%20%5Cbegin%7Bbmatrix%7D%20x_%7B1%7D%20%26%20x_%7B2%7D%20%26%20%5Ccdots%20%26%20x_%7BN%7D%20%5Cend%7Bbmatrix%7D%20%5Cbegin%7Bbmatrix%7D%20y_%7B1%7D%20%5C%5C%20y_%7B2%7D%20%5C%5C%20%5Cvdots%20%5C%5C%20y_%7BN%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%3D%20x_1%20y_1%20&plus;%20%5Ccdots%20&plus;%20x_N%20y_N%20%3D%20%5Csum_%7Bi%3D1%7D%5EN%20x_i%20y_i)

### 가중합/가중평균
+ 가중합: 복수의 데이터를, 가중치를 곱한 후 합하는 것
+ 가중평균: 가중합의 가중치값을 전체 가중치의 합으로 나누어 구한 값
	* ![Math](https://latex.codecogs.com/gif.latex?w_1%20x_1%20&plus;%20%5Ccdots%20&plus;%20w_N%20x_N%20%3D%20%5Csum_%7Bi%3D1%7D%5EN%20w_i%20x_i)

### 유사도
+ 두 벡터가 닮은 정도를 정량적으로 표현한 값
+ 내적을 이용하여 코사인 유사도 계산

### 행렬과 행렬의 곱셈
+ 교환 법칙과 분배 법칙: 교환법칙은 성립하지 않으며, 덧셈에 대한 분배 법칙은 성립
+ (행렬) 곱셈의 연결: 연속된 행렬의 곱셈은 계산 순서를 바꿔도 괜찮음

### 선형회귀 모형(linear regression model)
+ 독립변수 x에서 종속변수 y를 예측하는 방법의 하나
+ 독립변수 벡터 x와 가중치 벡터 w의 가중합으로 y에 관한 예측값 y-hat 계산
	* ![Math](https://latex.codecogs.com/gif.latex?%5Chat%7By%7D%20%3D%20w_1%20x_1%20&plus;%20%5Ccdots%20&plus;%20w_N%20x_N)
+ 비선형적 문제를 잘 예측하지 못할 수 있음

### 제곱합(sum of squares)
+ 각 데이터(벡터)를 제곱하여 모두 더한 값
	* ![Math](https://latex.codecogs.com/gif.latex?x%5ET%20x%20%3D%20%5Cbegin%7Bbmatrix%7D%20x_%7B1%7D%20%26%20x_%7B2%7D%20%26%20%5Ccdots%20%26%20x_%7BN%7D%20%5Cend%7Bbmatrix%7D%20%5Cbegin%7Bbmatrix%7D%20x_%7B1%7D%20%5C%5C%20x_%7B2%7D%20%5C%5C%20%5Cvdots%20%5C%5C%20x_%7BN%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20x_i%5E2)

### 잔차(residual, error)
+ 예측치와 실젯값 사이의 차이
	* ![Math](https://latex.codecogs.com/gif.latex?%5Cbegin%7Baligned%7D%20e%20%26%3D%20%5Cbegin%7Bbmatrix%7D%20e_%7B1%7D%20%5C%5C%20e_%7B2%7D%20%5C%5C%20%5Cvdots%20%5C%5C%20e_%7BM%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%5C%5C%20%26%3D%20%5Cbegin%7Bbmatrix%7D%20y_%7B1%7D%20%5C%5C%20y_%7B2%7D%20%5C%5C%20%5Cvdots%20%5C%5C%20y_%7BM%7D%20%5C%5C%20%5Cend%7Bbmatrix%7D%20-%20%5Cbegin%7Bbmatrix%7D%20x%5ET_%7B1%7Dw%20%5C%5C%20x%5ET_%7B2%7Dw%20%5C%5C%20%5Cvdots%20%5C%5C%20x%5ET_%7BM%7Dw%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%5C%5C%20%26%3D%20y%20-%20Xw%20%5Cend%7Baligned%7D)
+ 잔차 제곱합(Residual Sum of Squares): 잔차벡터의 각 원소를 제곱한 후 더한 값
	* ![Math](https://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20e_i%5E2%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%28y_i%20-%20w%5ETx_i%29%5E2%20%3D%20e%5ETe%20%3D%20%28y%20-%20Xw%29%5ET%20%28y%20-%20Xw%29)

### 이차형식(Quadratic Form)
+ 어떤 벡터와 정방행렬이 "행벡터*정방행렬*열벡터" 형태로 되어있는 것
+ +) 스칼라의 영역에서 제곱의 개념을 행렬로 사상한 개념이라고 생각하면 될 듯함 -> 일반화의 관점
	* ![Math](https://latex.codecogs.com/gif.latex?w%5ETX%5ETXw)

## 행렬의 성질
### 정부호와 준정부호 (행렬의 부호)
+ 양의 정부호(positive definite): 영벡터가 아닌 모든 벡터 x에 대해 아래 부등식이 성립하면, 행렬 A는 양의 정부호
	* ![Math](https://latex.codecogs.com/gif.latex?x%5ET%20A%20x%20%3E%200)
+ 양의 준정부호: 아래 부등식이 등호를 포함한다면, 행렬 A는 양의 준정부호
	* ![Math](https://latex.codecogs.com/gif.latex?x%5ET%20A%20x%20%5Cgeq%200)

### 놈(norm / 행렬의 크기)
+ 행렬(벡터)의 크기를 나타내는 값
	* ![Math](https://latex.codecogs.com/gif.latex?%5CVert%20A%20%5CVert_p%20%3D%20%5Cleft%28%20%5Csum_%7Bi%3D1%7D%5EN%20%5Csum_%7Bj%3D1%7D%5EM%20%7Ca_%7Bij%7D%7C%5Ep%20%5Cright%29%5E%7B1/p%7D)
+ p는 1, 2 혹은 무한대
+ 일반적으로 p=2인 경우가 가장 많이 쓰임
+ 놈의 공식적 정의 4가지가 있음

### 대각합(trace)
+ 대각원소의 합. 정방행렬에 대해서만 정의됨
+ 
