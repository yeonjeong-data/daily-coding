## 문제 1: 짝수와 홀수

**문제 설명**: 정수 num이 짝수일 경우 "Even"을 반환, 홀수인 경우 "Odd"를 반환하는 함수

**제한 사항**: num은 int 범위의 정수이고, 0은 짝수로 표현

## 풀이 접근
- 파이썬에서 짝수/홀수 판별 시,  나누기(/)가 아니라 나머지 연산자(%) 사용
> 짝수는 2로 나눴을 때, 나머지가 0
> 홀수는 2로 나눴을 때, 나머지가 1

## 코드:

```python
def solution(num):
    return "Even" if num % 2 == 0 else "Odd"
```

* 차이점 정리
- 나누기(/)               > 5 / 2의 결과는 2.5
- 몫(//)                     > 5 // 2의 결과는 2
- 나머지 연산자(%) > 5 % 2의 결과는 1


## 문제 2: 평균 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/12944

**문제 설명**: 정수를 담고 있는 배열 arr의 평균값을 return하는 함수

**제한 사항**: arr은 길이 1 이상, 100 이하인 배열이고, arr의 원소는 -10,000 이상 10,000 이하인 정수

## 코드:

```python
def solution(arr):
    if not (1 <= len(arr) <= 100):
        return "Error: 배열 길이는 1 이상 100 이하입니다."
    if any(not (-10000 <= x <= 10000) for x in arr):
        return "Error: 배열 원소는 -10,000 이상 10,000 이하의 정수입니다."
    return sum(arr) / len(arr)
```

## 문제 3: 자릿수 더하기

https://school.programmers.co.kr/learn/courses/30/lessons/12931

**문제 설명**: 자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수 (예. N = 123이면 1 + 2 + 3 = 6을 return)

**제한 사항**: N의 범위 : 100,000,000 이하의 자연수

## 풀이 접근
- 자연수 N을 문자열로 변환 ( str(n) )
- 각 자릿수를 하나씩 가져와 정수로 변환하여 합산

## 코드:

```python
def solution(n):
    return sum(int(digit) for digit in str(n))
```

* 구문 분석
-  for digit in str(n)
 > n을 문자열로 변환하여 각 자릿수를 하나씩 순회 (예. n = 123이면 str(n)은 '123'이 되어, 각각 '1', '2', '3'를 순회)
- int(digit)
 > 순회 중에 얻은 각 자릿수를 int로 변환 (예. '1' → 1, '2' → 2, '3' → 3)

## 문제 4: 약수의 합

https://school.programmers.co.kr/learn/courses/30/lessons/12928

**문제 설명**: 정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성

**제한 사항**: n은 0 이상 3000이하인 정수

## 코드 1:

```python
def solution(n):
    answer = 0
    for i in range(1, n+1):
        if n % i == 0:
            answer+=i
    return answer
```
```sql
* range(시작값, 끝값, 증가값) : 이때, 끝값으로 적은 값은 포함되지 않는다.
- 예1) range(5)는 0부터 4까지의 숫자 생성
- 예2)  range(2, 6)은 2부터 5까지의 숫자를 생성
- 예3) range(0, 10, 2)는 0부터 9까지의 숫자 중에서 2씩 증가하는 숫자를 생성 (0, 2, 4, 6, 8)
```

## 코드 2:

```python
def solution(n):
    answer = 0
    for i in range(1, int(n**0.5) + 1): # 약수의 대칭성을 이용하여 반만 탐색
        if n % i == 0:                          #  i가 약수인지 확인
            answer += i                       # 작은 약수 더하기
            if i != n // i:                        # 서로 다른 쌍인 경우, 큰 약수도 더하기
                answer += n // i
    return answer
```

## 문제 5: 나머지가 1이 되는 수 찾기

https://school.programmers.co.kr/learn/courses/30/lessons/87389

**문제 설명**: 자연수 n이 매개변수로 주어졌을 때, n을 x로 나눈 나머지가 1이 되도록 하는 가장 작은 자연수 x를 return 하도록 solution 함수를 완성 (답이 항상 존재함은 증명될 수 있음)

**제한 사항**: 3 ≤ n ≤ 1,000,000

## 코드:

```python
def solution(n):
    for x in range (1,n):
        if n%x==1:
            return x
```
