# 💡 소수 찾기

&nbsp; 소수란 1과 자기 자신을 제외한 자연수로는 나누어 떨어지지 않는 자연수이다. 단, 1이상이여야 한다.   
예를 들어 1, 2, 3, 6으로 나누어 떨어지는 6은 소수가 아니다.   
하지만 1과 7을 제외하고는 나누어 떨어지지 않는 7은 소수이다.   

소수를 찾을 때 약수의 성질을 이용하면 효율적으로 구현할 수 있다.  
- 약수의 성질  
  : 모든 약수에 대하여 가운데 약수를 기준으로 하여 대칭을 이룬다.

    <img src="https://user-images.githubusercontent.com/70243735/121998916-9243fa00-cde7-11eb-8cde-73edcc8a535f.png" width ="300px">

<br>

## 💡 소수 판별 함수 코드

```python
import math

def is_prime_number(x):
    # 2부터 x의 제곱근까지의 모든 수를 확인하여
    for i in range(2, int(math.sqrt(x))+1):
        # x가 해당 수로 나누어 떨어지다면 소수가 아님
        if x % i == 0:
            return False
    return True
print(is_prime_number(7))
print(is_prime_number(12))
```

<br>

## 💡 에라토스테네스의 체

&nbsp; 하나의 수가 아닌, 여러개의 수가 소수인지 아닌지를 판별할때 사용하는 대표적인 알고리즘이다.
에라토스테네스의 체는 N보다 작거나 같은 모든 소수를 찾을 때 사용할 수 있다.

**[ 동작 방식 ]**
1. 2부터 N까지의 모든 자연수를 나열한다.
2. 남은 수 중에서 아직 처리하지 않은 가장 작은 수 i를 찾는다.
3. 남은 수 중에서 **i의 배수를 모두 제거**한다.  
    : i는 제거하지 않는다. i는 소수이다.
4. 더이상 반복할 수 없을때까지 2~3번 과정을 반복한다.

<br>

<img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif">


<br>
<br>

## 💡 에라토스테네스의 체 구현 코드

에라토스테네스의 체를 이용하여 2부터 100까지 모든 수에 대하여 소수를 찾는 코드이다.

```python
import math

n = 100
numbers = [True for i in range(n+1)]

# 2부터 n의 제곱근까지 모든 수를 확인
for i in range(2, int(math.sqrt(n))+1):
    # 남은 수 중에서(= 소수 중에서)
    if numbers[i]:
        # i를 제외한 i의 모든 배수 삭제
        j = 2
        while i * j <= n:
            numbers[i * j] = False
            j += 1

# 모든 소수 출력
for i in range(2, n+1):
    if numbers[i]:
        print(i, end=' ')
```