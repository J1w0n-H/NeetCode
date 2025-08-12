# Bit Manipulation 🔢

> 비트 조작 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **39. Number of 1 Bits** - 1의 개수
- [ ] **40. Counting Bits** - 비트 개수

## 🔧 주요 개념

### **비트 조작 기본 패턴**
```python
# Number of 1 Bits
def hammingWeight(n):
    count = 0
    while n:
        count += n & 1  # 마지막 비트 확인
        n >>= 1         # 오른쪽으로 시프트
    return count

# 최적화된 버전 (Brian Kernighan's Algorithm)
def hammingWeightOptimized(n):
    count = 0
    while n:
        n &= (n - 1)    # 가장 오른쪽 1 제거
        count += 1
    return count

# Counting Bits (0부터 n까지 각 숫자의 1의 개수)
def countBits(n):
    result = [0] * (n + 1)
    
    for i in range(1, n + 1):
        # i & (i-1)은 가장 오른쪽 1을 제거
        result[i] = result[i & (i-1)] + 1
    
    return result

# Single Number (XOR 활용)
def singleNumber(nums):
    result = 0
    for num in nums:
        result ^= num
    return result

# Power of Two
def isPowerOfTwo(n):
    return n > 0 and (n & (n - 1)) == 0
```

## 📝 문제 유형별 접근법

### **1의 개수 세기**
- 각 비트를 순회하며 1인지 확인
- Brian Kernighan 알고리즘으로 최적화

### **비트 개수 계산**
- 동적 프로그래밍으로 이전 결과 활용
- `i & (i-1)` 패턴 활용

## 🚀 최적화 팁

1. **비트 연산자** - `&`, `|`, `^`, `~`, `<<`, `>>` 활용
2. **Brian Kernighan** - 가장 오른쪽 1 제거로 최적화
3. **XOR 특성** - 같은 수를 두 번 XOR하면 0
4. **Power of 2** - `n & (n-1) == 0` 조건

---

*"비트 조작은 메모리 효율적인 알고리즘의 핵심이다!"* 🚀
