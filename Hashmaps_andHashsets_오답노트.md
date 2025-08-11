# Hashmaps and Hashsets 오답노트 📚

## 문제 정보
- **주제**: Hashmaps and Hashsets (1/8)
- **난이도**: 기초
- **언어**: Python

## 문제 설명
두 개의 함수를 구현하는 문제입니다:
1. `build_hash_map(keys: List[str], values: List[int]) -> Dict[str, int]`: 키와 값 리스트를 받아 해시맵을 생성
2. `get_values(hash_map: Dict[str, int], keys: List[str]) -> List[int]`: 해시맵에서 특정 키들의 값들을 반환

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
1. **코드 스타일**: 
   - `my_dict={}` → `my_dict = {}` (공백 추가)
   - 변수명을 더 명확하게 (`my_dict` → `output_dict`, `scores` → `output`)

2. **구현 방식**:
   - `range(len(values))` 대신 `zip(keys, values)` 사용이 더 파이썬스럽고 안전함
   - `pass` 문은 불필요함

3. **안전성**:
   - `zip()` 사용 시 키와 값의 길이가 다를 경우 자동으로 짧은 쪽에 맞춰짐
   - `range(len())` 사용 시 인덱스 오류 가능성 있음

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
1. `zip()` 함수 활용하기
2. 변수명을 명확하고 일관성 있게 작성하기
3. 불필요한 코드 제거하기
4. 파이썬의 관용적인 코딩 스타일 적용하기

---
*마지막 업데이트: 2024년*
