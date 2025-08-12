# 2D Dynamic Programming 🧮📊

> 2차원 동적 프로그래밍 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **31. Unique Paths** - 고유한 경로
- [ ] **32. Longest Common Subsequence** - 최장 공통 부분수열

## 🔧 주요 개념

### **2D DP 기본 패턴**
```python
# Unique Paths
def uniquePaths(m, n):
    dp = [[0] * n for _ in range(m)]
    
    # 첫 번째 행과 열은 모두 1
    for i in range(m):
        dp[i][0] = 1
    for j in range(n):
        dp[0][j] = 1
    
    # 각 셀은 위와 왼쪽에서 오는 경로의 합
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    
    return dp[m-1][n-1]

# 공간 최적화 버전
def uniquePathsOptimized(m, n):
    dp = [1] * n
    
    for i in range(1, m):
        for j in range(1, n):
            dp[j] += dp[j-1]
    
    return dp[n-1]

# Longest Common Subsequence
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]
```

## 📝 문제 유형별 접근법

### **Unique Paths**
- 각 셀은 위와 왼쪽에서 오는 경로의 합
- 첫 번째 행과 열은 모두 1로 초기화

### **Longest Common Subsequence**
- 두 문자열의 공통 부분수열 중 최장 길이
- 문자가 같으면 대각선 + 1, 다르면 위/왼쪽 중 최대값

## 🚀 최적화 팁

1. **공간 최적화** - 1차원 배열로 2차원 표현
2. **초기화** - 첫 번째 행/열 값 설정
3. **점화식** - 현재 상태와 이전 상태의 관계 파악
4. **경계 조건** - 빈 문자열, 단일 문자 처리

---

*"2D DP는 격자 구조의 최적화 문제를 해결한다!"* 🚀
