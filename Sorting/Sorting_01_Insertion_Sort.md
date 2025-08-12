# Sorting - 01. Insertion Sort

## 문제 정보
- **제목**: Insertion Sort
- **난이도**: 중급
- **언어**: Python
- **출처**: Core Skills - Sorting

## 문제 설명
Insertion Sort 알고리즘을 구현하는 문제입니다. 정렬 과정의 각 단계를 보여주는 리스트를 반환해야 합니다.

### 요구사항
- **입력**: `pairs` (Pair 객체들의 리스트)
- **출력**: 정렬 과정의 각 단계를 보여주는 리스트의 리스트
- **기능**: Insertion Sort를 수행하면서 각 단계마다 배열의 상태를 기록

### Pair 클래스
```python
class Pair:
    def __init__(self, key: int, value: str):
        self.key = key
        self.value = value
```
- `key`: 정수 값 (정렬 기준)
- `value`: 문자열 값

## 예시
```python
# 입력
pairs = [Pair(3, "cat"), Pair(3, "bird"), Pair(2, "dog")]

# 출력 (각 단계별 상태)
[
    [(3, "cat"), (3, "bird"), (2, "dog")],  # 초기 상태
    [(3, "cat"), (3, "bird"), (2, "dog")],  # 첫 번째 단계 (변화 없음)
    [(2, "dog"), (3, "cat"), (3, "bird")]   # 최종 정렬된 상태
]
```

## 제약 조건
- 각 단계마다 배열의 현재 상태를 정확히 기록해야 함
- `pairs` 리스트는 직접 수정하지 않고 복사본 사용
- 정렬은 `key` 값을 기준으로 오름차순

## 내 코드 (오답)
```python
class Pair:
    def __init__(self, key: int, value: str):
        self.key = key
        self.value = value

def insertionSort(pairs: List[Pair]) -> List[List[Pair]]:
    sorted_list = []
    sorted_list.append(pairs.copy())
    
    for i in range(0, len(pairs)-1):
        for j in range(len(pairs)-1):
            if pairs[j].key > pairs[j+1].key:
                pairs[j], pairs[j+1] = pairs[j+1], pairs[j]
                sorted_list.append(pairs.copy())
    
    return sorted_list
```

## 정답 코드 + 피드백
```python
class Pair:
    def __init__(self, key: int, value: str):
        self.key = key
        self.value = value

def insertionSort(pairs: List[Pair]) -> List[List[Pair]]:
    n = len(pairs)
    res = []
    
    for i in range(n):
        j = i - 1
        while j >= 0 and pairs[j].key > pairs[j + 1].key:
            pairs[j], pairs[j + 1] = pairs[j + 1], pairs[j]
            j -= 1
        res.append(pairs[:])
    
    return res
```

### 피드백

#### 1. **알고리즘 구현 오류**
- **내 코드**: Bubble Sort와 유사한 이중 루프 구조
- **정답 코드**: 올바른 Insertion Sort 구현
- **문제점**: Insertion Sort는 한 번에 하나씩 요소를 올바른 위치에 삽입하는 알고리즘

#### 2. **상태 기록 방식 오류**
- **내 코드**: `pairs.copy()`를 사용하여 원본 배열을 직접 수정
- **정답 코드**: `pairs[:]`를 사용하여 슬라이싱으로 복사
- **문제점**: 원본 배열이 변경되어 예상과 다른 결과 발생

#### 3. **루프 구조 문제**
```python
# ❌ 잘못된 방식 (Bubble Sort와 유사)
for i in range(0, len(pairs)-1):
    for j in range(len(pairs)-1):
        if pairs[j].key > pairs[j+1].key:
            # 교환

# ✅ 올바른 Insertion Sort
for i in range(n):
    j = i - 1
    while j >= 0 and pairs[j].key > pairs[j + 1].key:
        # 교환
        j -= 1
```

## 기억할 요점 🔑

### 1. Insertion Sort 알고리즘 구조
```python
def insertionSort(arr):
    n = len(arr)
    for i in range(n):
        j = i - 1
        # 현재 요소를 올바른 위치에 삽입
        while j >= 0 and arr[j] > arr[j + 1]:
            arr[j], arr[j + 1] = arr[j + 1], arr[j]
            j -= 1
```

### 2. 배열 복사 방식
```python
# ✅ 얕은 복사 (shallow copy)
arr_copy = arr[:]        # 슬라이싱
arr_copy = arr.copy()    # copy() 메서드

# ❌ 참조 복사
arr_copy = arr           # 같은 객체 참조
```

### 3. 상태 기록 시점
```python
# Insertion Sort에서 상태 기록
for i in range(n):
    # 현재 단계 시작 전 상태 기록
    res.append(arr[:])
    
    # 정렬 로직 수행
    j = i - 1
    while j >= 0 and arr[j] > arr[j + 1]:
        arr[j], arr[j + 1] = arr[j + 1], arr[j]
        j -= 1
```

### 4. Bubble Sort vs Insertion Sort
```python
# Bubble Sort: 인접한 요소들을 비교하여 교환
for i in range(n):
    for j in range(n-1):
        if arr[j] > arr[j+1]:
            arr[j], arr[j+1] = arr[j+1], arr[j]

# Insertion Sort: 현재 요소를 올바른 위치에 삽입
for i in range(n):
    j = i - 1
    while j >= 0 and arr[j] > arr[j + 1]:
        arr[j], arr[j + 1] = arr[j + 1], arr[j]
        j -= 1
```

## 테스트 케이스 결과
```python
# 입력
pairs = [Pair(3, "cat"), Pair(3, "bird"), Pair(2, "dog")]

# 올바른 출력
[
    [(3, "cat"), (3, "bird"), (2, "dog")],  # 초기 상태
    [(3, "cat"), (3, "bird"), (2, "dog")],  # 첫 번째 단계 (변화 없음)
    [(2, "dog"), (3, "cat"), (3, "bird")]   # 최종 정렬된 상태
]
```

## 다음에 주의할 점 ⚠️
1. **알고리즘 구분**: Insertion Sort와 Bubble Sort의 차이점 명확히 이해하기
2. **상태 기록**: 각 단계마다 정확한 시점에 배열 상태를 복사하여 기록하기
3. **배열 복사**: `pairs[:]` 또는 `pairs.copy()` 사용하여 원본 배열 보호하기
4. **루프 구조**: Insertion Sort의 올바른 루프 구조 기억하기

---
*마지막 업데이트: 2024년*
