# Sorting - 03. Hashmaps and Hashsets (고급)

## 문제 정보
- **제목**: Hashmaps and Hashsets (고급)
- **난이도**: 중급
- **언어**: Python
- **출처**: Core Skills - Sorting

## 문제 설명
두 개의 고급 함수를 구현하는 문제입니다:

### 1. count_chars 함수
```python
def count_chars(s: str) -> Dict[str, int]:
```
- **입력**: 문자열 `s`
- **출력**: 각 문자가 등장하는 횟수를 담은 딕셔너리
- **기능**: 문자열에서 각 문자의 빈도수를 계산

### 2. nested_list_to_dict 함수
```python
def nested_list_to_dict(nums: List[List[int]]) -> Dict[int, List[int]]:
```
- **입력**: 정수들의 리스트의 리스트 `nums`
- **출력**: 첫 번째 요소를 키로, 나머지 요소들을 값으로 하는 딕셔너리
- **기능**: 각 서브리스트의 첫 번째 요소를 키로 하고, 나머지 요소들을 값으로 하는 해시맵 생성

## 예시
```python
# count_chars 예시
s = "hello"
result = count_chars(s)
# 출력: {'h': 1, 'e': 1, 'l': 2, 'o': 1}

# nested_list_to_dict 예시
nums = [[1, 2, 3], [4, 5], [1, 6, 7]]
result = nested_list_to_dict(nums)
# 출력: {1: [2, 3, 6, 7], 4: [5]}
```

## 제약 조건
- `count_chars`: 빈 문자열도 처리 가능
- `nested_list_to_dict`: 각 서브리스트는 최소 1개 이상의 요소를 가짐
- 중복 키가 있을 경우 값들을 합쳐서 저장

## 내 코드 (오답)
```python
from collections import defaultdict
from typing import List, Dict

def count_chars(s: str) -> Dict[str, int]:
    pass
    freq = defaultdict(int)
    for i in range(len(s)):
        freq[s[i]] += 1
    return freq

def nested_list_to_dict(nums: List[List[int]]) -> Dict[int, List[int]]:
    pass
    first = defaultdict(list)
    #Check if it's the first element of this list
    for num in nums:
        first[num[0]] += num
        first[num[0]].remove(num[0])
        #print("first:", first, "num:", num)
    return first
```

## 정답 코드 + 피드백
```python
from collections import defaultdict
from typing import List, Dict

def count_chars(s: str) -> Dict[str, int]:
    count = defaultdict(int)
    for char in s:
        count[char] += 1
    return count

def nested_list_to_dict(nums: List[List[int]]) -> Dict[int, List[int]]:
    output = defaultdict(list)
    for sublist in nums:
        first = sublist[0]
        for i in range(1, len(sublist)):
            output[first].append(sublist[i])
    return output
```

### 피드백

#### count_chars 함수
1. **구현 방식**: 
   - 내 코드: `for i in range(len(s))` 사용 (인덱스 기반)
   - 정답 코드: `for char in s` 사용 (직접 순회)
   - **결론**: 둘 다 정상 작동하지만, 직접 순회가 더 파이썬스러움

2. **코드 스타일**:
   - `freq[s[i]] += 1` → `freq[s[i]] += 1` (공백 추가)
   - 변수명: `freq`는 적절함

#### nested_list_to_dict 함수
1. **심각한 논리 오류**:
   - 내 코드: `first[num[0]] += num` (전체 리스트를 더함)
   - 정답 코드: `output[first].append(sublist[i])` (개별 요소만 추가)
   - **문제점**: `+=`로 리스트를 더하면 `[1, 2, 3] + [4, 5] = [1, 2, 3, 4, 5]`가 됨

2. **잘못된 접근**:
   - `first[num[0]].remove(num[0])`는 의도한 결과를 만들지 못함
   - 첫 번째 요소만 제거하려 했지만, 이미 잘못된 데이터가 들어감

3. **올바른 접근**:
   - 첫 번째 요소를 키로 사용
   - 나머지 요소들만 (`sublist[1:]`) 값으로 추가

## 기억할 요점 🔑

### 1. defaultdict 활용
```python
# defaultdict(int): 기본값 0
# defaultdict(list): 기본값 빈 리스트
# defaultdict(set): 기본값 빈 집합
```

### 2. 문자열 순회 방식
```python
# ✅ 권장: 직접 순회
for char in s:
    count[char] += 1

# ⚠️ 가능하지만 덜 파이썬스러움
for i in range(len(s)):
    count[s[i]] += 1
```

### 3. 리스트 조작 시 주의사항
```python
# ❌ 잘못된 방식
first[num[0]] += num  # 전체 리스트를 더함

# ✅ 올바른 방식
for i in range(1, len(sublist)):
    output[first].append(sublist[i])
```

### 4. 중첩 리스트 처리 패턴
```python
# 첫 번째 요소를 키로, 나머지를 값으로
for sublist in nums:
    key = sublist[0]           # 첫 번째 요소
    values = sublist[1:]       # 나머지 요소들
    output[key].extend(values) # 또는 append 반복
```

## 테스트 케이스 결과
```python
# count_chars 테스트
print(count_chars("hello"))
# 출력: {'h': 1, 'e': 1, 'l': 2, 'o': 1}

# nested_list_to_dict 테스트
print(nested_list_to_dict([[1, 2, 3], [4, 5], [1, 6, 7]]))
# 출력: {1: [2, 3, 6, 7], 4: [5]}
```

## 다음에 주의할 점 ⚠️
1. **`+=` 연산자 사용 시 리스트의 전체가 더해지는 것 주의**
2. **`defaultdict`의 기본값 타입을 정확히 이해하기**
3. **중첩 리스트 처리 시 인덱싱과 슬라이싱 활용하기**
4. **문자열 순회는 가능하면 직접 순회 방식 사용하기**

---
*마지막 업데이트: 2024년*
