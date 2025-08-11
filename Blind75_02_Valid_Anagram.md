# Blind 75 - 02. Valid Anagram

## 문제 정보
- **제목**: Valid Anagram
- **난이도**: Easy
- **언어**: Python
- **출처**: Blind 75

## 문제 설명
두 문자열 `s`와 `t`가 주어졌을 때, `t`가 `s`의 아나그램이면 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다.

**아나그램(Anagram)이란?**
아나그램은 다른 문자열과 정확히 동일한 문자를 포함하지만, 문자의 순서가 다를 수 있는 문자열입니다.

### 요구사항
- **입력**: `s` (문자열), `t` (문자열)
- **출력**: `true` (아나그램이면) 또는 `false` (아나그램이 아니면)

## 예시
```python
# 예시 1
s = "anagram", t = "nagaram"
# 출력: true

# 예시 2
s = "rat", t = "car"
# 출력: false

# 예시 3
s = "", t = ""
# 출력: true
```

## 제약 조건
- `1 <= s.length, t.length <= 5 * 10^4`
- `s`와 `t`는 영문 소문자로만 구성됩니다.

## 내 코드 (정답)
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        count = [0] * 26
        
        for i in range(len(s)):
            count[ord(s[i]) - ord('a')] += 1
            count[ord(t[i]) - ord('a')] -= 1
            
        return all(x == 0 for x in count)
```

## 정답 코드 + 피드백
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # 방법 1: 정렬 후 비교 (간단하지만 비효율적)
        # return sorted(s) == sorted(t)
        
        # 방법 2: 문자 빈도수 카운트 (효율적)
        if len(s) != len(t):
            return False
        
        count = [0] * 26
        
        for i in range(len(s)):
            count[ord(s[i]) - ord('a')] += 1
            count[ord(t[i]) - ord('a')] -= 1
            
        return all(x == 0 for x in count)
        
        # 방법 3: Counter 사용 (파이썬스러운 방식)
        # from collections import Counter
        # return Counter(s) == Counter(t)
```

### 피드백

#### 1. **알고리즘 선택**
- **내 코드**: 문자 빈도수 카운트 방식으로 효율적
- **정답 코드**: 여러 방법 제시 (정렬, 카운트, Counter)
- **결론**: 내 코드가 가장 효율적인 O(n) 시간복잡도

#### 2. **구현 방식 비교**
```python
# ❌ 비효율적: 정렬 방식
return sorted(s) == sorted(t)  # O(n log n)

# ✅ 효율적: 빈도수 카운트 (내 코드)
count = [0] * 26
for i in range(len(s)):
    count[ord(s[i]) - ord('a')] += 1
    count[ord(t[i]) - ord('a')] -= 1
return all(x == 0 for x in count)  # O(n)

# ✅ 효율적: Counter 사용
from collections import Counter
return Counter(s) == Counter(t)  # O(n)
```

#### 3. **코드 최적화**
- **내 코드**: 이미 최적화되어 있음
- **개선 가능**: Counter 사용으로 더 파이썬스러운 코드

## 기억할 요점 🔑

### 1. 아나그램 검사 전략
```python
# 1단계: 길이 비교 (빠른 조기 종료)
if len(s) != len(t):
    return False

# 2단계: 문자 빈도수 비교
count = [0] * 26
for i in range(len(s)):
    count[ord(s[i]) - ord('a')] += 1
    count[ord(t[i]) - ord('a')] -= 1

# 3단계: 모든 빈도수가 0인지 확인
return all(x == 0 for x in count)
```

### 2. 시간복잡도 비교
```python
# 정렬 방식: O(n log n) - 문자열 정렬
# 빈도수 카운트: O(n) - 한 번의 순회
# Counter 사용: O(n) - 내부적으로 최적화
```

### 3. Python 내장 함수 활용
```python
# Counter: 자동으로 빈도수 계산
from collections import Counter
return Counter(s) == Counter(t)

# all(): 모든 요소가 조건을 만족하는지 확인
return all(x == 0 for x in count)
```

## 테스트 케이스 결과
```python
# Case 1
s = "anagram", t = "nagaram"
# 출력: true ✅

# Case 2
s = "rat", t = "car"
# 출력: false ✅

# Case 3
s = "", t = ""
# 출력: true ✅

# Case 4
s = "hello", t = "world"
# 출력: false ✅
```

## 다음에 주의할 점 ⚠️
1. **길이 비교**: 아나그램은 길이가 같아야 하므로 먼저 확인
2. **문자 범위**: 소문자만 다룬다면 26개 배열로 충분
3. **빈도수 계산**: 한 번의 순회로 두 문자열 동시 처리
4. **Python 내장 함수**: Counter 사용 시 더 간결한 코드 작성 가능

---
*마지막 업데이트: 2024년*
