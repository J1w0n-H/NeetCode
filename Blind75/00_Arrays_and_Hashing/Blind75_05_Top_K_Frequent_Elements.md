# Blind 75 - 05. Top K Frequent Elements

## 문제 정보
- **제목**: Top K Frequent Elements
- **난이도**: Medium
- **언어**: Python
- **출처**: Blind 75

## 문제 설명
정수 배열 `nums`와 정수 `k`가 주어졌을 때, 배열 내에서 가장 빈번하게 나타나는 `k`개의 요소를 반환하는 문제입니다.

### 요구사항
- **입력**: `nums` (정수 배열), `k` (반환할 요소 개수)
- **출력**: 가장 빈번한 `k`개 요소의 배열
- **특징**: 
  - 테스트 케이스는 항상 고유한 답을 가짐
  - 출력 순서는 중요하지 않음

## 예시
```python
# 예시 1
nums = [1, 2, 2, 3, 3, 3]
k = 2
# 출력: [2, 3] (2는 2번, 3은 3번 나타남)

# 예시 2
nums = [7, 7]
k = 1
# 출력: [7] (7은 2번 나타남)

# 예시 3
nums = [1]
k = 1
# 출력: [1] (1은 1번 나타남)
```

## 제약 조건
- `1 <= nums.length <= 10^4`
- `-1000 <= nums[i] <= 1000`
- `1 <= k <= number of distinct elements in nums`

## 내 코드 (오답/비효율)
```python
def topKFrequent(nums: List[int], k: int) -> List[int]:
    count = {}
    res = []
    
    # 빈도수 계산
    for num in nums:
        count[num] = count.get(num, 0) + 1
    
    # k개 요소 찾기
    while len(res) != k:
        for key, value in count.items():
            if len(count) == 1:
                res.append(key)
                break
            elif value == max(sublist, key=count.get):
                res.append(key)
                sublist[key] = 0  # 이미 선택된 요소 제외
                break
    
    return res
```

## 정답 코드 + 피드백
```python
from collections import Counter
from typing import List

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 방법 1: Counter와 most_common 사용 (가장 효율적)
        count = Counter(nums)
        return [item[0] for item in count.most_common(k)]
        
        # 방법 2: 정렬 기반 접근
        # count = {}
        # for num in nums:
        #     count[num] = count.get(num, 0) + 1
        # 
        # sorted_items = sorted(count.items(), key=lambda x: x[1], reverse=True)
        # return [item[0] for item in sorted_items[:k]]
```

### 피드백

#### 1. **알고리즘 복잡성**
- **내 코드**: 복잡한 로직으로 구현 (while 루프 + max 함수 반복)
- **정답 코드**: 간단하고 효율적인 Counter 기반 접근
- **개선점**: 불필요한 복잡성을 제거하고 직관적인 방법 사용

#### 2. **구현 방식 비교**
```python
# ❌ 복잡한 로직 (내 코드)
while len(res) != k:
    for key, value in count.items():
        if value == max(sublist, key=count.get):  # O(n) 반복
            res.append(key)
            sublist[key] = 0

# ✅ 간단하고 명확한 로직 (정답 코드)
count = Counter(nums)  # O(n) 빈도수 계산
return [item[0] for item in count.most_common(k)]  # O(n log k)
```

#### 3. **성능 최적화**
- **내 코드**: 매번 `max()` 함수 호출로 O(n²) 시간복잡도
- **정답 코드**: Counter 사용으로 O(n log k) 시간복잡도
- **결과**: 더 효율적이고 확장 가능한 솔루션

## 기억할 요점 🔑

### 1. 빈도수 기반 문제 해결 전략
```python
# 1단계: Counter로 빈도수 계산
from collections import Counter
count = Counter(nums)  # 자동으로 빈도수 계산

# 2단계: most_common으로 상위 k개 추출
result = [item[0] for item in count.most_common(k)]
```

### 2. 시간복잡도 비교
```python
# 내 코드: O(n²) - 매번 max() 함수 호출
# 정렬 방식: O(n log n) - 정렬 후 앞에서 k개 추출
# Counter 사용: O(n log k) - 힙 기반 (가장 효율적)
```

### 3. Python 내장 함수 활용
```python
# Counter: 자동 빈도수 계산
count = Counter(nums)

# most_common: 상위 k개 반환
top_k = count.most_common(k)

# 리스트 컴프리헨션: 결과 추출
result = [item[0] for item in top_k]
```

### 4. 대안적 접근 방법
```python
# 정렬 기반 접근
def topKFrequent(nums: List[int], k: int) -> List[int]:
    count = {}
    for num in nums:
        count[num] = count.get(num, 0) + 1
    
    sorted_items = sorted(count.items(), key=lambda x: x[1], reverse=True)
    return [item[0] for item in sorted_items[:k]]
```

## 테스트 케이스 결과
```python
# Case 1
nums = [1, 2, 2, 3, 3, 3]
k = 2
# 출력: [2, 3] ✅

# Case 2
nums = [7, 7]
k = 1
# 출력: [7] ✅

# Case 3
nums = [1]
k = 1
# 출력: [1] ✅

# Case 4
nums = [1, 1, 1, 2, 2, 3]
k = 2
# 출력: [1, 2] ✅
```

## 다음에 주의할 점 ⚠️
1. **알고리즘 선택**: 복잡한 로직보다는 간단하고 효율적인 방법 우선 고려
2. **Counter 활용**: 빈도수 관련 문제에서는 Counter 클래스 우선 고려
3. **시간복잡도**: 반복적인 `max()` 함수 호출은 성능 저하의 원인
4. **코드 가독성**: 복잡한 조건문보다는 내장 함수 활용이 더 명확
5. **Python 최적화**: `most_common()` 메서드의 효율성 이해하기

---
*마지막 업데이트: 2024년*
