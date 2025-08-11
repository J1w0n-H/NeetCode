# Blind 75 - 01. Contains Duplicate

## 문제 정보
- **제목**: Contains Duplicate
- **난이도**: Easy
- **언어**: Python
- **출처**: Blind 75

## 문제 설명
정수 배열 `nums`가 주어졌을 때, 배열 내에 어떤 값이 한 번 이상 나타나면 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다.

### 요구사항
- **입력**: `nums` (정수 배열)
- **출력**: `true` (중복이 있으면) 또는 `false` (중복이 없으면)

## 예시
```python
# 예시 1
nums = [1, 2, 3, 3]
# 출력: true (3이 두 번 나타남)

# 예시 2
nums = [1, 2, 3, 4]
# 출력: false (모든 값이 한 번씩만 나타남)

# 예시 3
nums = [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]
# 출력: true (여러 값이 중복됨)
```

## 제약 조건
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

## 내 코드 (정답)
```python
class Solution:
    def hasDuplicate(self, nums: List[int]) -> bool:
        for i in range(len(nums)-1):
            if nums[i] in nums[i+1:]:
                return True
        return False
```

## 정답 코드 + 피드백
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        # 방법 1: Set 사용 (권장)
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False
        
        # 방법 2: 정렬 후 비교
        # nums.sort()
        # for i in range(len(nums) - 1):
        #     if nums[i] == nums[i + 1]:
        #         return True
        # return False
```

### 피드백

#### 1. **알고리즘 효율성**
- **내 코드**: `nums[i] in nums[i+1:]` 사용으로 O(n²) 시간복잡도
- **정답 코드**: Set 사용으로 O(n) 시간복잡도
- **개선점**: 중복 검사를 위한 Set 자료구조 활용

#### 2. **함수명 일치**
- **내 코드**: `hasDuplicate` (문제 요구사항과 다름)
- **정답 코드**: `containsDuplicate` (문제 요구사항과 일치)
- **주의점**: 함수명을 정확히 맞춰야 함

#### 3. **성능 비교**
```python
# ❌ 비효율적인 방식 (내 코드)
for i in range(len(nums)-1):
    if nums[i] in nums[i+1:]:  # O(n) 검색을 n번 반복
        return True

# ✅ 효율적인 방식 (정답 코드)
seen = set()  # O(1) 검색
for num in nums:
    if num in seen:  # O(1) 검색
        return True
    seen.add(num)
```

## 기억할 요점 🔑

### 1. 중복 검사 최적화 전략
```python
# Set 사용 (가장 효율적)
seen = set()
for num in nums:
    if num in seen:  # O(1) 시간복잡도
        return True
    seen.add(num)
return False
```

### 2. 시간복잡도 비교
```python
# 내 코드: O(n²) - 슬라이싱과 in 연산자 반복
# 정답 코드: O(n) - Set을 사용한 한 번의 순회
# 정렬 방식: O(n log n) - 정렬 후 인접 요소 비교
```

### 3. Python 자료구조 활용
```python
# Set: 중복 제거, O(1) 검색
# List: 순서 유지, O(n) 검색
# Dict: 키-값 쌍, O(1) 검색
```

## 테스트 케이스 결과
```python
# Case 1
nums = [1, 2, 3, 3]
# 출력: true ✅

# Case 2
nums = [1, 2, 3, 4]
# 출력: false ✅

# Case 3
nums = [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]
# 출력: true ✅
```

## 다음에 주의할 점 ⚠️
1. **함수명 정확성**: 문제에서 요구하는 함수명을 정확히 사용하기
2. **자료구조 선택**: 중복 검사에는 Set이 가장 효율적
3. **시간복잡도**: 슬라이싱과 in 연산자의 조합은 O(n²) 주의
4. **코드 간결성**: Set을 사용하면 더 간결하고 효율적인 코드 작성 가능

---
*마지막 업데이트: 2024년*
