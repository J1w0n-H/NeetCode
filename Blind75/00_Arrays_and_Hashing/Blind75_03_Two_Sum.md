# Blind 75 - 03. Two Sum

## 문제 정보
- **제목**: Two Sum
- **난이도**: Easy
- **언어**: Python
- **출처**: Blind 75

## 문제 설명
정수 배열 `nums`와 정수 `target`이 주어졌을 때, 배열 내에서 두 숫자의 합이 `target`이 되는 두 숫자의 인덱스를 반환합니다.

### 요구사항
- **입력**: `nums` (정수 배열), `target` (목표 합)
- **출력**: 두 숫자의 인덱스를 담은 배열 `[i, j]`
- **조건**: 
  - 정확히 하나의 답이 존재
  - 같은 요소를 두 번 사용할 수 없음

## 예시
```python
# 예시 1
nums = [2, 7, 11, 15], target = 9
# 출력: [0, 1] (nums[0] + nums[1] = 2 + 7 = 9)

# 예시 2
nums = [3, 2, 4], target = 6
# 출력: [1, 2] (nums[1] + nums[2] = 2 + 4 = 6)

# 예시 3
nums = [3, 3], target = 6
# 출력: [0, 1] (nums[0] + nums[1] = 3 + 3 = 6)
```

## 제약 조건
- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- 정확히 하나의 유효한 답이 존재

## 내 코드 (오답)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # 브루트 포스 방식 (비효율적)
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return []
```

## 정답 코드 + 피드백
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # 해시맵을 사용한 효율적인 방식
        seen = {}  # {숫자: 인덱스}
        
        for i, num in enumerate(nums):
            complement = target - num
            
            # 보수가 이미 해시맵에 있는지 확인
            if complement in seen:
                return [seen[complement], i]
            
            # 현재 숫자와 인덱스를 해시맵에 저장
            seen[num] = i
        
        return []  # 답이 없는 경우 (문제 조건상 발생하지 않음)
```

### 피드백

#### 1. **알고리즘 효율성**
- **내 코드**: 이중 루프로 O(n²) 시간복잡도
- **정답 코드**: 해시맵 사용으로 O(n) 시간복잡도
- **개선점**: 100배 이상의 성능 향상

#### 2. **구현 방식 비교**
```python
# ❌ 비효율적: 브루트 포스 (내 코드)
for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        if nums[i] + nums[j] == target:
            return [i, j]

# ✅ 효율적: 해시맵 사용 (정답 코드)
seen = {}
for i, num in enumerate(nums):
    complement = target - num
    if complement in seen:
        return [seen[complement], i]
    seen[num] = i
```

#### 3. **핵심 아이디어**
- **보수(Complement) 개념**: `target - 현재숫자`가 이미 본 숫자인지 확인
- **한 번의 순회**: 각 숫자를 한 번씩만 확인
- **해시맵 활용**: O(1) 시간에 숫자 존재 여부 확인

## 기억할 요점 🔑

### 1. Two Sum 문제 해결 전략
```python
# 1단계: 해시맵 초기화
seen = {}  # {숫자: 인덱스}

# 2단계: 각 숫자에 대해 보수 확인
for i, num in enumerate(nums):
    complement = target - num
    
    # 3단계: 보수가 이미 있으면 답 반환
    if complement in seen:
        return [seen[complement], i]
    
    # 4단계: 현재 숫자 저장
    seen[num] = i
```

### 2. 시간복잡도 비교
```python
# 브루트 포스: O(n²) - 모든 쌍을 확인
# 해시맵 방식: O(n) - 한 번의 순회
# 정렬 + 투 포인터: O(n log n) - 정렬 후 양 끝에서 접근
```

### 3. Python 최적화 기법
```python
# enumerate 사용
for i, num in enumerate(nums):  # 인덱스와 값 동시 접근

# 해시맵 검색
if complement in seen:  # O(1) 시간복잡도

# 딕셔너리 get 메서드
seen.get(complement, -1)  # 기본값 처리
```

## 테스트 케이스 결과
```python
# Case 1
nums = [2, 7, 11, 15], target = 9
# 출력: [0, 1] ✅

# Case 2
nums = [3, 2, 4], target = 6
# 출력: [1, 2] ✅

# Case 3
nums = [3, 3], target = 6
# 출력: [0, 1] ✅

# Case 4
nums = [1, 5, 8, 1, 9], target = 10
# 출력: [0, 4] ✅
```

## 다음에 주의할 점 ⚠️
1. **알고리즘 선택**: 브루트 포스보다는 해시맵 방식 우선 고려
2. **보수 개념**: `target - 현재값`을 활용한 효율적인 검색
3. **한 번의 순회**: 각 요소를 한 번씩만 확인하는 방식 설계
4. **해시맵 활용**: O(1) 검색을 위한 딕셔너리 자료구조 활용

---
*마지막 업데이트: 2024년*
