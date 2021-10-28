# 벡터가 뭔가요?

- 벡터는 숫자를 원소로 가지는 리스트(list) 또는 배열(array)입니다.

- ```python
  x = [1, 7, 2]
  x = np.array([1, 7, 2])
  ```

- 행벡터: 가로로 배열, 열벡터: 세로로 배열

- 벡터의 차원: 벡터 안 숫자의 갯수

- 벡터는 공간에서 한 점을 나타냅니다.

- 벡터는 원점으로부터 상대적 위치를 표현합니다.

- 벡터에 숫자를 곱해주면 길이만 변합니다. (스칼라 곱)

- 벡터끼리 같은 모양을 가지면 덧셈, 뺄셈을 계산할 수 있습니다.

- 벡터가 같은 모양을 가지면 성분곱(hadamard product)을 계산할 수 있다.

$$
\vec{x} = \begin{bmatrix}x_1\\x_2\\\vdots\\x_d \end{bmatrix}
\quad
\vec{y} =
\begin{bmatrix}y_1\\y_2\\\vdots\\y_d \end{bmatrix}
\quad
\vec{x}\odot\vec{y} = 
\begin{bmatrix}x_1y_1\\x_2y_2\\\vdots\\x_dy_d\\ \end{bmatrix}
$$

```python
import numpy as np
x = np.array([1, 7, 2])
y = np.array([5, 2, 1])

x + y
x - y
x * y
```



__벡터의 덧셈을 알아보자__

- 두 벡터의 덧셈은 다른 벡터로부터 상대적 위치이동을 표현합니다.



__벡터의 노름 구해보기__

- 벡터의 노름(norm)은 원점에서부터의 거리를 말합니다.
- 임의의 차원 d에 대해 성립
- L1 노름은 각 성분의 변화량의 절대값을 모두 더합니다.
- L2 노름은 피타고라스 정리를 이용해 유클리드 거리를 계산합니다.

$$
\vec{x} =
\begin{bmatrix} x_1\\x_2\\\vdots\\x_d \end{bmatrix}
\quad
\Vert\vec{x}\Vert_1 = 
\sum_{i=1}^{d} \vert x_i\vert
\quad
\Vert\vec{x}\Vert_2 = \sqrt{
\sum_{i=1}^{d} \vert x_i\vert^2}
$$

```python
def l1_norm(x):
    x_norm = np.abs(x)
    x_norm = np.sum(x_norm)
    return x_norm

def l2_norm(x):
    x_norm = x * x
    x_norm = np.sum(x_norm)
    x_norm = np.sqrt(x_norm)
    return x_norm

#l2-norm은 np.linalg.norm을 이용해도 구현 가능하다.
```



__왜 다른 노름을 소개하나요?__

- 노름의 종류에 따라 기하학적 성질이 달라집니다.
- 머신러닝에선 각 성질이 필요할 때가 있으므로 둘 다 사용합니다.



__두 벡터 사이의 거리를 구해보자!__

- l1, l2 노름을 이용해 두 벡터 사이의 거리를 계산할 수 있습니다.
- 두 벡터 사이의 거리를 계산할 때는 벡터의 뺄셈을 이용합니다.
- 뺄셈을 거꾸로 해도 거리는 같습니다.

$$
\Vert\vec{x} - \vec{y}\Vert = \Vert\vec{y} - \vec{x}\Vert
$$

__두 벡터 사이의 각도 구해보기__

- 두 벡터 사이의 거리를 이용하여 각도도 계산해 볼 수 있을까?
- 제2 코사인 법칙에 의해 두 벡터 사이의 각도를 계산할 수 있다.
- 분자를 쉽게 계산하는 방법이 내적이다.
- 내적은 np.inner를 이용해서 계산한다.

$$
cos\theta = \frac{<\vec{x}, \vec{y}>}{\Vert\vec{x}\Vert\Vert\vec{y}\Vert}
\quad
<\vec{x}, \vec{y}> = \sum_{i=1}^{d}x_iy_i
$$



__내적은 어떻게 해석할까?__

- 내적은 정사영(orthogonal projection vector)된 벡터의 길이와 관련이 있다.
- 내적은 정사영 길이를 벡터 y의 길이만큼 조정한 값이다.