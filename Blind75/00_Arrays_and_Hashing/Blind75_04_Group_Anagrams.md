# Blind 75 - 04. Group Anagrams

## 문제 정보
- **제목**: Group Anagrams
- **난이도**: Medium
- **언어**: Python
- **출처**: Blind 75

## 문제 설명
문자열 배열 `strs`가 주어졌을 때, 모든 아나그램(anagram)을 함께 서브리스트로 묶는 문제입니다. 출력 순서는 중요하지 않습니다.

**아나그램(Anagram)이란?**
아나그램은 다른 문자열과 정확히 동일한 문자를 포함하지만, 문자의 순서가 다를 수 있는 문자열입니다.

### 요구사항
- **입력**: `strs` (문자열 배열)
- **출력**: 아나그램 그룹들의 리스트

## 예시
```python
# 예시 1
strs = ["act", "pots", "tops", "cat", "stop", "hat"]
# 출력: [["hat"], ["act", "cat"], ["stop", "pots", "tops"]]

# 예시 2
strs = ["x"]
# 출력: [["x"]]

# 예시 3
strs = [""]
# 출력: [[""]]
```

## 제약 조건
- `1 <= strs.length <= 1000`
- `0 <= strs[i].length <= 100`
- `strs[i]`는 소문자 영어 알파벳으로만 구성됩니다.

## 내 코드 (오답/비효율)
```python
from typing import List

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = []
        visited = [False] * len(strs)

        for i in range(len(strs)):
            if not visited[i]:
                sublist = [strs[i]]
                visited[i] = True
                for j in range(i+1, len(strs)):
                    if not visited[j] and self.isAnagram(strs[i], strs[j]) == True:
                        sublist.append(strs[j])
                        visited[j] = True
                res.append(sublist.copy())
        return res

    def isAnagram(self, s, t):
        if (len(s)!=len(t)):
            return False
        
        count = [0] * 26
        
        for i in range(len(s)):
            count [ord(s[i])-ord('a')]+=1
            count [ord(t[i])-ord('a')]-=1
            
        return all(x==0 for x in count)
```

## 정답 코드 + 피드백
```python
from collections import defaultdict
from typing import List

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # 아나그램을 그룹화할 딕셔너리
        # 키는 정렬된 문자열(아나그램의 '정규 형태'), 값은 해당 아나그램들의 리스트
        anagram_map = defaultdict(list)

        for s in strs:
            # 문자열을 정렬하여 아나그램의 '정규 형태' 키를 생성
            # 예: "eat", "tea", "ate" 모두 "aet"가 됨
            sorted_s = "".join(sorted(s))
            # 해당 키에 현재 문자열을 추가
            anagram_map[sorted_s].append(s)
        
        # 딕셔너리의 모든 값(아나그램 리스트들)을 반환
        return list(anagram_map.values())
```

### 피드백

#### 1. **알고리즘 효율성**
- **내 코드**: 중첩 루프와 `visited` 배열을 사용하는 브루트 포스 방식
- **정답 코드**: 해시맵을 사용한 최적화된 방식
- **시간복잡도**: O(n² * L) → O(n * L log L) 개선

#### 2. **구현 방식 비교**
```python
# ❌ 비효율적: 브루트 포스 (내 코드)
for i in range(len(strs)):
    for j in range(i+1, len(strs)):
        if self.isAnagram(strs[i], strs[j]):  # O(L) 시간
            # 그룹화 로직

# ✅ 효율적: 해시맵 사용 (정답 코드)
anagram_map = defaultdict(list)
for s in strs:
    sorted_s = "".join(sorted(s))  # O(L log L) 시간
    anagram_map[sorted_s].append(s)  # O(1) 시간
```

#### 3. **핵심 아이디어**
- **정규 형태 키**: 정렬된 문자열을 키로 사용하여 아나그램 그룹화
- **defaultdict 활용**: 새로운 키 접근 시 자동으로 빈 리스트 생성
- **한 번의 순회**: 각 문자열을 한 번씩만 처리

## 기억할 요점 🔑

### 1. 아나그램 그룹화 전략
```python
# 1단계: defaultdict 초기화
anagram_map = defaultdict(list)

# 2단계: 각 문자열을 정규 형태로 변환
for s in strs:
    sorted_s = "".join(sorted(s))  # 정규 형태 생성
    
# 3단계: 정규 형태를 키로 사용하여 그룹화
    anagram_map[sorted_s].append(s)

# 4단계: 모든 그룹 반환
return list(anagram_map.values())
```

### 2. 시간복잡도 분석
```python
# 내 코드: O(n² * L) - 모든 쌍을 비교하며 isAnagram 호출
# 정답 코드: O(n * L log L) - 각 문자열을 정렬하여 그룹화
# 개선 효과: n이 클 때 상당한 성능 향상
```

### 3. Python 최적화 기법
```python
# defaultdict 사용
from collections import defaultdict
anagram_map = defaultdict(list)  # 자동으로 빈 리스트 생성

# 문자열 정렬
sorted_s = "".join(sorted(s))  # 정렬된 문자열을 하나로 결합

# 딕셔너리 값 추출
return list(anagram_map.values())  # 모든 그룹을 리스트로 변환
```

## 테스트 케이스 결과
```python
# Case 1
strs = ["act", "pots", "tops", "cat", "stop", "hat"]
# 출력: [["hat"], ["act", "cat"], ["stop", "pots", "tops"]] ✅

# Case 2
strs = ["x"]
# 출력: [["x"]] ✅

# Case 3
strs = [""]
# 출력: [[""]] ✅

# Case 4
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
# 출력: [["bat"], ["nat", "tan"], ["ate", "eat", "tea"]] ✅
```

## 다음에 주의할 점 ⚠️
1. **알고리즘 선택**: 브루트 포스보다는 해시맵 기반 그룹화 우선 고려
2. **정규 형태 키**: 정렬된 문자열을 키로 사용하는 아이디어 기억
3. **defaultdict 활용**: 새로운 키 접근 시 자동 초기화로 코드 간소화
4. **시간복잡도**: n² 방식은 입력 크기가 클 때 시간 초과 위험

---
*마지막 업데이트: 2024년*
