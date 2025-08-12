# 1D Dynamic Programming 🧮

> 1차원 동적 프로그래밍 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **29. Climbing Stairs** - 계단 오르기
- [ ] **30. House Robber** - 도둑질

## 🔧 주요 개념

### **1D DP 기본 패턴**
```python
# 계단 오르기
def climbStairs(n):
    if n <= 2:
        return n
    
    dp = [0] * (n + 1)
    dp[1] = 1
    dp[2] = 2
    
    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]

# 공간 최적화 버전
def climbStairsOptimized(n):
    if n <= 2:
        return n
    
    prev, curr = 1, 2
    for i in range(3, n + 1):
        prev, curr = curr, prev + curr
    
    return curr

# House Robber
def rob(nums):
    if not nums:
        return 0
    if len(nums) == 1:
        return nums[0]
    
    dp = [0] * len(nums)
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])
    
    for i in range(2, len(nums)):
        dp[i] = max(dp[i-1], dp[i-2] + nums[i])
    
    return dp[-1]

# 공간 최적화 버전
def robOptimized(nums):
    if not nums:
        return 0
    if len(nums) == 1:
        return nums[0]
    
    prev, curr = nums[0], max(nums[0], nums[1])
    
    for i in range(2, len(nums)):
        prev, curr = curr, max(curr, prev + nums[i])
    
    return curr
```

## 📝 문제 유형별 접근법

### **계단 오르기**
- 각 단계에서 1계단 또는 2계단 오르기
- 이전 두 단계의 방법 수 합

### **House Robber**
- 인접한 집을 털 수 없음
- 현재 집을 털거나 털지 않는 두 가지 선택

## 🚀 최적화 팁

1. **공간 최적화** - 이전 두 값만 저장
2. **경계 조건** - 작은 입력값 처리
3. **점화식 파악** - 문제의 재귀적 구조 이해
4. **메모이제이션** - 중복 계산 방지

---

*"1D DP는 선형 구조의 최적화 문제를 해결한다!"* 🚀
