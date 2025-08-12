# Backtracking 🔙

> 백트래킹 기법을 활용한 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **24. Subsets** - 부분집합
- [ ] **25. Permutations** - 순열

## 🔧 주요 개념

### **백트래킹 기본 패턴**
```python
# 부분집합 생성
def subsets(nums):
    def backtrack(start, path):
        result.append(path[:])
        
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    
    result = []
    backtrack(0, [])
    return result

# 순열 생성
def permutations(nums):
    def backtrack(path, used):
        if len(path) == len(nums):
            result.append(path[:])
            return
        
        for i in range(len(nums)):
            if not used[i]:
                used[i] = True
                path.append(nums[i])
                backtrack(path, used)
                path.pop()
                used[i] = False
    
    result = []
    used = [False] * len(nums)
    backtrack([], used)
    return result
```

## 📝 문제 유형별 접근법

### **부분집합**
- 각 요소를 선택하거나 선택하지 않는 두 가지 경우
- 재귀적으로 모든 조합 탐색

### **순열**
- 각 위치에 모든 요소를 한 번씩 배치
- 사용된 요소 추적을 위한 used 배열

## 🚀 최적화 팁

1. **경로 복사** - `path[:]`로 현재 상태 저장
2. **상태 추적** - used 배열로 중복 선택 방지
3. **조건 최적화** - 불필요한 재귀 호출 줄이기
4. **메모리 효율** - 경로 재사용으로 공간 절약

---

*"백트래킹은 모든 가능한 해를 체계적으로 탐색하는 기법이다!"* 🚀
