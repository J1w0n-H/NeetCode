# Blind 75 - 08. Longest Consecutive Sequence

## 문제 정보
- **난이도**: Medium
- **카테고리**: Array, Hash Set
- **출처**: LeetCode

## 문제 설명
Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

**Example 1:**
```
Input: nums = [2,20,4,10,3,4,5]
Output: 4
Explanation: The longest consecutive sequence is [2, 3, 4, 5].
```

**Example 2:**
```
Input: nums = [0,3,2,5,4,6,1,1]
Output: 7
```

**Constraints:**
- 0 <= nums.length <= 1000
- -10^9 <= nums[i] <= 10^9

## 내 코드 (오답)
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums.sort()
        print(nums)
        if len(nums) == 0:
            return 0
        count = [0]
        sequence = 0
        for i in range(1, len(nums)):
            gap = nums[i] - nums[i-1]
            if gap == 1:
                sequence += 1
            elif gap > 1:
                count.append(sequence)
                sequence = 0
        count.append(sequence)
        return max(count) + 1
```

## 정답 코드 + 피드백

### 1. **Brute Force 방식 (비효율적)**
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        res = 0
        store = set(nums)

        for num in nums:
            streak, curr = 0, num
            while curr in store:
                streak += 1
                curr += 1
            res = max(res, streak)
        return res
```

### 2. **Sorting 방식 (중간 효율성)**
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if not nums:
            return 0
        res = 0
        nums.sort()

        curr, streak = nums[0], 0
        i = 0
        while i < len(nums):
            if curr != nums[i]:
                curr = nums[i]
                streak = 0
            while i < len(nums) and nums[i] == curr:
                i += 1
            streak += 1
            curr += 1
            res = max(res, streak)
        return res
```

### 3. **Hash Set 방식 (최적화)**
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        numSet = set(nums)
        longest = 0

        for num in numSet:
            if (num - 1) not in numSet:
                length = 1
                while (num + length) in numSet:
                    length += 1
                longest = max(length, longest)
        return longest
```

### 4. **Hash Map 방식 (고급)**
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        mp = defaultdict(int)
        res = 0

        for num in nums:
            if not mp[num]:
                mp[num] = mp[num - 1] + mp[num + 1] + 1
                mp[num - mp[num - 1]] = mp[num]
                mp[num + mp[num + 1]] = mp[num]
                res = max(res, mp[num])
        return res
```

### 피드백

**내 코드의 문제점:**
1. **시간 복잡도**: O(n log n)로 제약사항 위반 (O(n) 요구)
2. **로직 오류**: 연속된 수열의 시작점을 제대로 찾지 못함
3. **중복 처리 부족**: 같은 숫자가 여러 번 나올 때 처리 로직 부족
4. **경계 조건**: 빈 배열 처리 후에도 로직이 복잡함
5. **변수 초기화**: `count = [0]`로 시작하여 불필요한 0 포함

**정답 코드의 장점:**
1. **Hash Set 방식**: O(n) 시간 복잡도, 간단하고 효율적
2. **시작점 찾기**: `(num - 1) not in numSet`으로 연속 수열의 시작점만 확인
3. **중복 제거**: set을 사용하여 중복 자동 처리
4. **명확한 로직**: 각 연속 수열을 한 번씩만 계산

## 기억할 요점

### 1. **Hash Set 활용 패턴**
```python
# 연속 수열의 시작점 찾기
numSet = set(nums)
for num in numSet:
    if (num - 1) not in numSet:  # 시작점인지 확인
        # 연속 수열 계산 시작
        length = 1
        while (num + length) in numSet:
            length += 1
```

### 2. **연속 수열 계산 로직**
```python
# ❌ 잘못된 방법 - 모든 숫자에서 시작
for num in nums:
    streak = 0
    curr = num
    while curr in store:  # 중복 계산 발생
        streak += 1
        curr += 1

# ✅ 올바른 방법 - 시작점에서만 계산
for num in numSet:
    if (num - 1) not in numSet:  # 시작점 확인
        length = 1
        while (num + length) in numSet:  # 한 번만 계산
            length += 1
```

### 3. **정렬 vs Hash Set 비교**
```python
# ❌ 정렬 방식 (O(n log n))
nums.sort()
# 연속된 요소 찾기...

# ✅ Hash Set 방식 (O(n))
numSet = set(nums)
# O(1) 조회로 연속 수열 찾기
```

### 4. **중복 처리**
```python
# ❌ 배열에서 중복 처리
for i in range(1, len(nums)):
    if nums[i] == nums[i-1]:  # 중복 처리 로직 필요
        continue

# ✅ Set 사용으로 자동 중복 제거
numSet = set(nums)  # 중복 자동 제거
for num in numSet:  # 중복 없이 순회
```

### 5. **경계 조건 처리**
```python
# 빈 배열 처리
if not nums:
    return 0

# 단일 요소 처리
if len(nums) == 1:
    return 1
```

## 시간 및 공간 복잡도

### **내 코드**
- **시간 복잡도**: O(n log n) - 정렬
- **공간 복잡도**: O(1) 또는 O(n) (정렬 알고리즘에 따라)

### **Brute Force 방식**
- **시간 복잡도**: O(n²) - 최악의 경우
- **공간 복잡도**: O(n) - set 사용

### **Sorting 방식**
- **시간 복잡도**: O(n log n) - 정렬
- **공간 복잡도**: O(1) 또는 O(n)

### **Hash Set 방식**
- **시간 복잡도**: O(n) - 각 요소를 최대 2번 방문
- **공간 복잡도**: O(n) - set 사용

### **Hash Map 방식**
- **시간 복잡도**: O(n) - 각 요소를 한 번씩만 처리
- **공간 복잡도**: O(n) - hash map 사용

## 테스트 케이스

```python
# 테스트 1: 일반적인 경우
nums = [2, 20, 4, 10, 3, 4, 5]
# 정렬 후: [2, 3, 4, 4, 5, 10, 20]
# 연속 수열: [2, 3, 4, 5] → 길이 4

# 테스트 2: 중복 포함
nums = [0, 3, 2, 5, 4, 6, 1, 1]
# 정렬 후: [0, 1, 1, 2, 3, 4, 5, 6]
# 연속 수열: [0, 1, 2, 3, 4, 5, 6] → 길이 7

# 테스트 3: 빈 배열
nums = []
# 결과: 0

# 테스트 4: 단일 요소
nums = [1]
# 결과: 1
```

## 다음에 주의할 점

1. **시간 복잡도 준수**: O(n) 요구사항 확인하기
2. **Hash Set 활용**: 빠른 조회를 위해 set 사용하기
3. **시작점 찾기**: 연속 수열의 시작점만 확인하여 중복 계산 피하기
4. **중복 처리**: set을 사용하여 자동으로 중복 제거하기
5. **경계 조건**: 빈 배열, 단일 요소 등 예외 상황 고려하기
6. **정렬 피하기**: O(n log n)보다는 O(n) 솔루션 찾기
7. **로직 단순화**: 복잡한 조건문보다는 명확한 패턴 사용하기
8. **변수 초기화**: 불필요한 초기값 피하기
