## 문제 1: x만큼 간격이 있는 n개의 숫자

https://school.programmers.co.kr/learn/courses/30/lessons/12954

**문제 설명**: 함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴

**제한 사항**: x는 -10000000 이상, 10000000 이하인 정수이고, n은 1000 이하인 자연수

## 코드:

```python
def solution(x, n):
    if not (-10000000 <= x <= 10000000):
        return "오류: x는 -10000000 이상, 10000000 이하의 정수여야 합니다."
    if not (1 <= n <= 1000):
        return "오류: n은 1000 이하의 자연수여야 합니다."

    return [x*i for i in range(1, n+1)]
```

## 문제 2: 자연수 뒤집어 배열로 만들기

https://school.programmers.co.kr/learn/courses/30/lessons/12932

**문제 설명**: 자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴 (예. n이 12345이면 [5,4,3,2,1]을 리턴)

**제한 사항**: n은 10,000,000,000이하인 자연수

## 풀이 접근
* 슬라이싱: 문자열이나 리스트에서 특정 범위를 추출할 때 사용
- 기본 형태: 문자열[시작:끝:증가폭]
> 생략 시, 증가폭 기본값 = 1 (오른쪽으로 이동)
* 역순 슬라이싱: [::-1]
- 시작과 끝을 비워두어 전체 문자열을 대상으로 함
- 증가폭을 -1로 설정하여 오른쪽에서 왼쪽으로 한 칸씩 이동

## 코드:

```python
def solution(n):
    if not (1 <= n <= 10000000000):
        return "오류: n은 10,000,000,000 이하의 자연수"
    
    return [int(digit) for digit in str(n)[::-1]]   # 문자열로 변환하여 뒤집기
```

## 문제 3: 문자열을 정수로 바꾸기

https://school.programmers.co.kr/learn/courses/30/lessons/12925

**문제 설명**: 문자열 s를 숫자로 변환한 결과를 반환하는 함수

**제한 사항**: s의 길이는 1 이상 5이하, s의 맨앞에는 부호(+, -)가 올 수 있다. s는 부호와 숫자로만 이루어져있으며, s는 "0"으로 시작하지 않는다.

예) str이 "1234"이면 1234를 반환하고, "-1234"이면 -1234를 반환

## 코드:

```python
def solution(s):
    return int(s)
```

## 문제 4: 정수 제곱근 판별

https://school.programmers.co.kr/learn/courses/30/lessons/12934

**문제 설명**: 임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하고자 한다. n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하기

**제한 사항**: n은 1이상, 50000000000000 이하인 양의 정수

## 풀이 접근
- 정수의 제곱근을 구한 후, 그 숫자를 제곱하여 n 값이 나오는지 확인

## 코드:

```python
import math

def solution(n):
    if not (1 <= n <= 50000000000000):
        return "오류: n은 1 이상, 50조 이하의 양의 정수"
    x = math.isqrt(n) 
    if x ** 2 == n:
        return (x + 1) ** 2
    return -1
```

## 문제 5: 정수 내림차순으로 배치하기

https://school.programmers.co.kr/learn/courses/30/lessons/12933

**문제 설명**: 함수 solution은 정수 n을 매개변수로 입력받는다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴하기 (예, n이 118372면 873211을 리턴)

**제한 사항**: n은 1이상 8000000000 이하인 자연수

## 풀이 접근
- 자연수 n을 문자열로 변환하여 각 자릿수 추출 : str(n)
- 각 자릿수를 내림차순으로 정렬 : sorted(str(n), reverse=True)
- 정렬된 문자열을 하나로 이어 붙이기 : ''.join(...)
- 이어 붙인 문자열을 다시 정수로 변환하여 반환 : int(...)

## 코드:

```python
def solution(n):
    return int(''.join(sorted(str(n), reverse=True)))
```
