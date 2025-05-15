## 문제 1: 두 수의 차 구하기

**문제 설명**: 두 정수 'num1', 'num2'가 주어질 때, 'num1'에서 'num2'를 뺀 값을 return하도록 solution 함수를 완성하기

**제한 사항**: -50000 ≤ num1 ≤ 50000, -50000 ≤ num2 ≤ 50000

### 풀이 접근
- 두 수를 입력받고, 그 차이를 계산하여 반환합니다.
- 입력 값이 제한 범위를 벗어나면 에러 메시지를 출력하도록 합니다. (None 반환)

### 코드:
```python
def solution(num1, num2):
    if not (-50000 <= num1 <= 50000 and -50000 <= num2 <= 50000):
        print("입력 값이 제한 범위를 벗어났습니다.")
        return None
    return num1-num2
```

## 문제 2: 합 구하기

'num1'과 'num2'의 합 (제한 사항, 풀이 접근은 문제1과 동일)

### 코드:
```python
def solution(num1, num2):
    if not (-50000 <= num1 <= 50000 and -50000 <= num2 <= 50000):
        print("입력 값이 제한 범위를 벗어났습니다.")
        return None
    return num1+num2
```

## 문제 3: 두 수의 곱 구하기

**문제 설명**: 두 정수 'num1', 'num2'가 주어질 때, 'num1'와 'num2'를 곱 값을 return하도록 solution 함수를 완성하기

**제한 사항**: 0 ≤ num1 ≤ 100, 0 ≤ num2 ≤ 100

### 풀이 접근
- 두 수를 입력받고, 그 곱을 계산하여 반환합니다.
- 입력 값이 제한 범위를 벗어나면 에러 메시지를 출력하도록 합니다. (None 반환)

### 코드:
```python
def solution(num1, num2):
    if not (0<=num1<=100 and 0<=num2<=100):
        print("입력 값이 제한 범위를 벗어났습니다.")
        return None
    return num1*num2
```

## 문제4: 몫 구하기

'num1'을 'num2'로 나눈 몫 (제한 사항은 문제3과 동일)

### 풀이 접근
- 0으로 나눌 때 예외 처리
- 정수 나누셈 연산자(//) 사용 : 나머지를 버리고 몫만 반환 (예. 7//3 결과는 2)

#### 참고
- 일반 나눗셈 연산자(/) : 실수형 몫을 반환 (예. 7/3 결과는 2.333``)

### 코드:
```python
def solution(num1, num2):
    if not (0 <= num1 <= 100 and 0 <= num2 <= 100):
        print("입력 값이 제한 범위를 벗어났습니다.")
        return None
    if num2 == 0:
        print("0으로 나눌 수 없습니다.")
        return None
    return num1 // num2
```

## 문제 5: 응용

**문제 설명**: 두 정수 'num1', 'num2'가 주어질 때, 'num1'을 'num2'로 나눈 값에 1,000을 곱한 후 정수 부분을 return하도록 solution 함수를 완성하기

**제한 사항**: 0 ≤ num1 ≤ 100, 0 ≤ num2 ≤ 100

### 풀이 접근
- 예) num1=1, num2=16일 경우, 1/16=0.0625이고 여기에 *1,000하면 62.5가 되며, 정수 부분은 62
- 일반 나눗셈 연산자(/) 사용 후 곱셈 계산, 이후 결과값의 정수 부분만 반환 (int() 사용)

#### 참고
- round(값, 소수점 자리수) : 결과값을 반올림하여 정수 반환
- round(62.499) 결과는 62 : 자리수를 0 또는 생략하면 정수 부분으로 반올림
- round(62.499, 1) 결과는 62.5 : 소수점 이하 자리 (오른쪽)
- round(62.499, -1) 결과는 60 : 정수 자리 (왼쪽)

### 코드:
```python
def solution(num1, num2):
    if not (0 <= num1 <= 100 and 0 <= num2 <= 100):
        print("입력 값이 제한 범위를 벗어났습니다.")
        return None
    if num2 == 0:
        print("0으로 나눌 수 없습니다.")
        return None
    return int((num1/num2)*1000)
```
