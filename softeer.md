### 소프티어 level 2

GPT식 숫자 비교

- https://softeer.ai/practice/11001

#### 조건 정리:
- n 조건 확인
- 숫자는 오름차순으로 정렬해야 합니다.
- 정수부가 같으면 소수부를 비교해야 합니다.
- 소수부를 비교할 때는 입력받은 그대로 비교해야 하며, 자리수와 상관없이 숫자 그대로 비교합니다.
  - 예를 들어 2.100은 2.9보다 크고, 1.3은 1.11보다 작습니다.
- 정수와 실수 모두 입력받은 그대로 출력해야 합니다.


#### 해결 전략:
1. 입력받은 숫자를 문자열로 처리합니다.
2. 소수점이 있는 경우 정수부와 소수부를 분리합니다.
  - 소수부는 숫자 그대로 비교하기 위해 int()를 사용해 소수부를 정수로 변환합니다.
  - 소수부가 없는 경우는 소수부를 0으로 간주하여 처리합니다.
  - 소수부를 숫자값으로 직접 비교해야 합니다.
3. sorted() 함수로 오름차순으로 정렬하여, 작은 값이 먼저 나오게 합니다.
4. 입력받은 숫자들을 그대로 출력합니다.

``` python

import sys

# 1. 입력받고 리스트로 변환
data = sys.stdin.read().split()
n = int(data[0])  # 첫 번째 값은 숫자의 개수 (1 ≤ N ≤ 1000)

# N의 범위를 체크
if n < 1 or n > 1000:
    print("Error: N must be between 1 and 1000.")
    sys.exit(1)  # 범위를 벗어나면 프로그램 종료

numbers = data[1:n+1]  # 나머지 숫자만 리스트로 저장 (문자열 상태 유지)

# 2. 숫자 조건 체크 (0 이상 100 이하, 소수점 아래 최대 3자리)
def check_valid_number(num):
    # 숫자가 0 이상 100 이하인지 체크
    if not (0 <= float(num) <= 100):
        return False
    # 소수점 아래 3자리까지 허용되는지 체크
    if '.' in num:
        decimal_part = num.split('.')[1]
        if len(decimal_part) > 3:
            return False
    return True

# 숫자 조건 체크
for num in numbers:
    if not check_valid_number(num):
        print(f"Error: {num} is not valid. It should be between 0 and 100, and have at most 3 decimal places.")
        sys.exit(1)  # 조건을 벗어나면 프로그램 종료

# 3. 정수부 + 소수부 기준으로 정렬
def custom_sort(num):
    if '.' in num:
        int_part, decimal_part = num.split('.')
        # 소수부를 숫자처럼 취급하여 비교
        decimal_part = int(decimal_part)  # 소수부를 숫자로 변환
    else:
        int_part = num
        decimal_part = 0  # 소수부가 없으면 0을 소수부로 간주
    
    return (int(int_part), decimal_part)  # 정수부 + 소수부 비교

# 4. 리스트를 정렬 (오름차순)
finallist = sorted(numbers, key=custom_sort)  # 정렬된 리스트를 finallist에 저장

# 5. 결과 출력 (입력받은 그대로 출력)
for num in finallist:
    print(num)  # 입력받은 그대로 출력



```


틀렸습니다!
