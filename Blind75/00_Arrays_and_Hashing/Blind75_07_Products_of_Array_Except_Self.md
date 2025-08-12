# Blind 75 - 07. Products of Array Except Self

## 문제 정보
- **난이도**: Medium
- **카테고리**: Array, Prefix Sum
- **출처**: LeetCode

## 문제 설명
Given an integer array `nums`, return an array `output` where `output[i]` is the product of all the elements of `nums` except `nums[i]`.

Each product is guaranteed to fit in a 32-bit integer.

**Follow-up**: Could you solve it in O(n) time without using the division operation?

**Example 1:**
```
Input: nums = [1,2,4,6]
Output: [48,24,12,8]
```

**Example 2:**
```
Input: nums = [-1,0,1,2,3]
Output: [0,-6,0,0,0]
```

**Constraints:**
- 2 <= nums.length <= 1000
- -20 <= nums[i] <= 20

## 내 코드 (오답)
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        res = [0] * n

        for j in range(n):
            result = 1
            for i, num in enumerate(nums):
                if i != j:
                    result = result * nums[i]
            res[j] = result
        return res
```

## 정답 코드 + 피드백

### 1. **Division 방식 (간단하지만 제약사항 위반)**
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        prod, zero_cnt = 1, 0
        for num in nums:
            if num:
                prod *= num
            else:
                zero_cnt += 1
        if zero_cnt > 1: 
            return [0] * len(nums)

        res = [0] * len(nums)
        for i, c in enumerate(nums):
            if zero_cnt: 
                res[i] = 0 if c else prod
            else: 
                res[i] = prod // c
        return res
```

### 2. **Prefix & Suffix 방식 (최적화)**
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1] * (len(nums))

        prefix = 1
        for i in range(len(nums)):
            res[i] = prefix
            prefix *= nums[i]
        postfix = 1
        for i in range(len(nums) - 1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]
        return res
```

### 피드백

**내 코드의 문제점:**
1. **시간 복잡도**: O(n²)로 비효율적 - 중첩 루프 사용
2. **중복 계산**: 모든 요소를 매번 다시 계산하여 불필요한 연산
3. **제약사항 위반**: Follow-up에서 요구하는 O(n) 시간 복잡도 미달성
4. **변수명 혼동**: `result`와 `res` 변수명이 비슷하여 가독성 저하
5. **비효율적인 조건문**: `if i != j` 조건을 매번 확인
6. **코드 흐름 복잡성**: 각 위치마다 전체 배열을 순회하는 직관적이지 않은 로직

**정답 코드의 장점:**
1. **Division 방식**: O(n) 시간 복잡도, 0 처리 로직 포함
2. **Prefix & Suffix 방식**: O(n) 시간, O(1) 추가 공간 (출력 배열 제외)
3. **영리한 접근**: prefix와 postfix를 활용한 효율적인 계산

## 기억할 요점

### 1. **Prefix Sum 개념**
```python
# 기본 prefix sum
prefix = [0] * n
prefix[0] = nums[0]
for i in range(1, n):
    prefix[i] = prefix[i-1] + nums[i]

# Product prefix sum
prefix = [1] * n
prefix[0] = nums[0]
for i in range(1, n):
    prefix[i] = prefix[i-1] * nums[i]
```

### 2. **Prefix & Suffix 조합 패턴**
```python
# 1단계: 왼쪽에서 오른쪽으로 prefix 계산
prefix = 1
for i in range(n):
    res[i] = prefix  # 현재 위치까지의 prefix
    prefix *= nums[i]  # 다음 위치를 위한 prefix 업데이트

# 2단계: 오른쪽에서 왼쪽으로 postfix 계산
postfix = 1
for i in range(n-1, -1, -1):
    res[i] *= postfix  # 기존 prefix에 postfix 곱하기
    postfix *= nums[i]  # 다음 위치를 위한 postfix 업데이트
```

### 3. **코드 흐름 핵심 설명**

#### **예시: nums = [1, 2, 4, 6]**

**1단계: Prefix 계산 (왼쪽 → 오른쪽)**
```
초기: res = [1, 1, 1, 1], prefix = 1

i=0: res[0] = prefix = 1, prefix = prefix * nums[0] = 1 * 1 = 1
     → res = [1, 1, 1, 1]

i=1: res[1] = prefix = 1, prefix = prefix * nums[1] = 1 * 2 = 2  
     → res = [1, 1, 1, 1]

i=2: res[2] = prefix = 2, prefix = prefix * nums[2] = 2 * 4 = 8
     → res = [1, 1, 2, 1]

i=3: res[3] = prefix = 8, prefix = prefix * nums[3] = 8 * 6 = 48
     → res = [1, 1, 2, 8]

1단계 완료: res = [1, 1, 2, 8]
```

**2단계: Postfix 계산 (오른쪽 → 왼쪽)**
```
초기: postfix = 1

i=3: res[3] *= postfix = 8 * 1 = 8, postfix = postfix * nums[3] = 1 * 6 = 6
     → res = [1, 1, 2, 8]

i=2: res[2] *= postfix = 2 * 6 = 12, postfix = postfix * nums[2] = 6 * 4 = 24
     → res = [1, 1, 12, 8]

i=1: res[1] *= postfix = 1 * 24 = 24, postfix = postfix * nums[1] = 24 * 2 = 48
     → res = [1, 24, 12, 8]

i=0: res[0] *= postfix = 1 * 48 = 48, postfix = postfix * nums[0] = 48 * 1 = 48
     → res = [48, 24, 12, 8]

최종 결과: [48, 24, 12, 8]
```

#### **핵심 아이디어:**
- **res[i] = prefix**: i 위치의 왼쪽에 있는 모든 요소들의 곱
- **res[i] *= postfix**: i 위치의 오른쪽에 있는 모든 요소들의 곱을 곱함
- **결과**: res[i] = (왼쪽 요소들의 곱) × (오른쪽 요소들의 곱) = 자기 자신을 제외한 모든 요소의 곱

### 4. **0 처리 로직**
```python
# 0이 2개 이상이면 모든 결과가 0
if zero_cnt > 1:
    return [0] * len(nums)

# 0이 1개인 경우
if zero_cnt:
    res[i] = 0 if nums[i] else prod  # 0이 아닌 위치는 0, 0인 위치는 전체 곱
```

### 5. **공간 복잡도 최적화**
```python
# ❌ 추가 배열 사용
pref = [0] * n
suff = [0] * n

# ✅ 출력 배열에 직접 계산
res = [1] * n  # 출력 배열을 prefix 저장소로 활용
```

### 6. **중첩 루프 최적화**
```python
# ❌ O(n²) 중첩 루프
for j in range(n):
    result = 1
    for i, num in enumerate(nums):
        if i != j:
            result = result * nums[i]
    res[j] = result

# ✅ O(n) 두 번의 순회
# 1단계: prefix 계산
# 2단계: postfix 계산
```

### 7. **변수명 명확성**
```python
# ❌ 혼동되는 변수명
result = 1  # 곱셈 결과
res = [0] * n  # 결과 배열

# ✅ 명확한 변수명
product = 1  # 곱셈 결과
output = [1] * n  # 결과 배열
```

## 시간 및 공간 복잡도

### **내 코드**
- **시간 복잡도**: O(n²) - 중첩 루프
- **공간 복잡도**: O(1) 추가 공간 (출력 배열 제외)

### **Division 방식**
- **시간 복잡도**: O(n) - 한 번의 순회
- **공간 복잡도**: O(1) 추가 공간 (출력 배열 제외)

### **Prefix & Suffix 방식**
- **시간 복잡도**: O(n) - 두 번의 순회
- **공간 복잡도**: O(1) 추가 공간 (출력 배열 제외)

## 테스트 케이스

```python
# 테스트 1: 일반적인 경우
nums = [1, 2, 4, 6]
# prefix: [1, 1, 2, 8]
# postfix: [48, 24, 6, 1]
# 결과: [48, 24, 12, 8]

# 테스트 2: 0 포함
nums = [-1, 0, 1, 2, 3]
# 0이 1개이므로 0이 아닌 위치는 모두 0
# 결과: [0, -6, 0, 0, 0]

# 테스트 3: 음수 포함
nums = [-1, -2, -3]
# 결과: [6, 3, 2]
```

## 다음에 주의할 점

1. **시간 복잡도 고려**: O(n²)보다는 O(n) 솔루션 찾기
2. **Prefix Sum 활용**: 누적 계산이 필요한 문제에서 유용
3. **공간 최적화**: 추가 배열 없이 출력 배열 활용하기
4. **0 처리**: 곱셈에서 0은 특별한 경우로 처리
5. **방향성**: 왼쪽→오른쪽, 오른쪽→왼쪽 순회 조합 고려
6. **제약사항 준수**: Follow-up 요구사항 확인하기
7. **변수명 명확성**: `result`와 `res` 같은 혼동되는 변수명 피하기
8. **중첩 루프 최적화**: 가능하면 단일 루프나 두 번의 순회로 대체하기
9. **코드 가독성**: 변수명과 로직을 명확하게 작성하기
10. **코드 흐름 이해**: 알고리즘의 동작 원리를 단계별로 파악하기
11. **패턴 인식**: 비슷한 문제에서 재사용할 수 있는 패턴 찾기
