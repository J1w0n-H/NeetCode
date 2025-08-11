# Sorting - 02. Hashmaps and Hashsets

## 문제 정보
- **제목**: Hashmaps and Hashsets
- **난이도**: 기초
- **언어**: Python
- **출처**: Core Skills - Sorting

## 문제 설명
두 개의 함수를 구현하는 문제입니다:

### 1. build_hash_map 함수
```python
def build_hash_map(keys: List[str], values: List[int]) -> Dict[str, int]:
```
- **입력**: `keys` (문자열 리스트), `values` (정수 리스트)
- **출력**: 키-값 쌍으로 구성된 딕셔너리
- **기능**: 두 리스트를 받아서 해시맵을 생성

### 2. get_values 함수
```python
def get_values(hash_map: Dict[str, int], keys: List[str]) -> List[int]:
```
- **입력**: `hash_map` (딕셔너리), `keys` (문자열 리스트)
- **출력**: 요청된 키들에 해당하는 값들의 리스트
- **기능**: 해시맵에서 특정 키들의 값들을 반환

## 예시
```python
# build_hash_map 예시
keys = ["Alice", "Bob", "Charlie"]
values = [90, 80, 70]
result = build_hash_map(keys, values)
# 출력: {"Alice": 90, "Bob": 80, "Charlie": 70}

# get_values 예시
hash_map = {"Alice": 90, "Bob": 80, "Charlie": 70}
keys = ["Alice", "Bob"]
result = get_values(hash_map, keys)
# 출력: [90, 80]
```

## 제약 조건
- `keys`와 `values` 리스트의 길이는 같음
- 모든 키는 문자열, 모든 값은 정수
- 중복 키가 있을 경우 마지막 값으로 덮어쓰기

## 내 코드 (오답)
```python
from typing import List, Dict

def build_hash_map(keys: List[str], values: List[int]) -> Dict[str, int]:
    pass
    my_dict={}
    for i in range(len(values)):
        my_dict[keys[i]] = values[i]
    return my_dict

def get_values(hash_map: Dict[str, int], keys: List[str]) -> List[int]:
    pass
    scores = []
    for key in keys:
        scores.append(hash_map[key])
    return scores
```

## 정답 코드 + 피드백
```python
from typing import List, Dict

def build_hash_map(keys: List[str], values: List[int]) -> Dict[str, int]:
    output_dict = {}
    for key, value in zip(keys, values):
        output_dict[key] = value
    return output_dict

def get_values(hash_map: Dict[str, int], keys: List[str]) -> List[int]:
    output = []
    for key in keys:
        output.append(hash_map[key])
    return output
```

### 피드백

#### 1. **코드 스타일**
- **내 코드**: `my_dict={}` → `my_dict = {}` (공백 추가)
- **정답 코드**: 변수명을 더 명확하게 (`my_dict` → `output_dict`, `scores` → `output`)
- **개선점**: 일관성 있는 네이밍과 코드 스타일

#### 2. **구현 방식**
- **내 코드**: `range(len(values))` 사용
- **정답 코드**: `zip(keys, values)` 사용이 더 파이썬스럽고 안전함
- **개선점**: `pass` 문 제거, 더 직관적인 반복문

#### 3. **안전성**
```python
# ❌ 좋지 않은 방식 (내 코드)
for i in range(len(values)):
    my_dict[keys[i]] = values[i]

# ✅ 파이썬스러운 방식 (정답 코드)
for key, value in zip(keys, values):
    output_dict[key] = value
```

## 기억할 요점 🔑

### 1. Pythonic한 반복문 작성
```python
# ❌ 좋지 않은 방식
for i in range(len(values)):
    my_dict[keys[i]] = values[i]

# ✅ 파이썬스러운 방식
for key, value in zip(keys, values):
    output_dict[key] = value
```

### 2. 변수명 규칙
- 의미있는 이름 사용 (`output_dict`, `output`)
- 일관성 있는 네이밍 컨벤션

### 3. 코드 스타일
- 연산자 주변 공백 추가 (`=` → ` = `)
- 불필요한 `pass` 문 제거

### 4. 해시맵 기본 개념
- 키-값 쌍으로 데이터 저장
- O(1) 시간복잡도로 검색 가능
- 중복 키는 마지막 값으로 덮어쓰기

## 테스트 케이스 결과
```python
# build_hash_map 테스트
print(build_hash_map(["Alice", "Bob", "Charlie"], [90, 80, 70]))
# 출력: {'Alice': 90, 'Bob': 80, 'Charlie': 70}

# get_values 테스트
print(get_values({"Alice": 90, "Bob": 80, "Charlie": 70}, ["Alice", "Bob", "Charlie"]))
# 출력: [90, 80, 70]
```

## 다음에 주의할 점 ⚠️
1. **`zip()` 함수 활용**: 두 리스트를 동시에 순회할 때 사용
2. **변수명 명확성**: 의미있는 이름 사용하고 일관성 유지
3. **코드 스타일**: 연산자 주변 공백, 불필요한 코드 제거
4. **파이썬 관용구**: `zip()`, `enumerate()` 등 활용하기

---
*마지막 업데이트: 2024년*
