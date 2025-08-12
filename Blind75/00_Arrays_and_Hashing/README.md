# Arrays & Hashing 📊

> 배열과 해싱 관련 문제들의 오답노트

## 📋 문제 목록

### ✅ **완료된 문제들** (8개)
- [x] **01. Contains Duplicate** - 중복 요소 확인
- [x] **02. Valid Anagram** - 애너그램 확인
- [x] **03. Two Sum** - 두 수의 합
- [x] **04. Group Anagrams** - 애너그램 그룹화
- [x] **05. Top K Frequent Elements** - 상위 K개 빈도 요소
- [x] **06. Encoding & Decoding** - 문자열 인코딩/디코딩
- [x] **07. Products of Array Except Self** - 자기 자신을 제외한 곱
- [x] **08. Longest Consecutive Sequence** - 최장 연속 수열

## 🔧 주요 개념

### **해시맵 (HashMap)**
```python
# 기본 사용법
count = {}
count[key] = count.get(key, 0) + 1

# defaultdict 사용
from collections import defaultdict
count = defaultdict(int)
count[key] += 1
```

### **해시셋 (HashSet)**
```python
# 중복 제거
unique_nums = set(nums)

# 존재 확인
if target in unique_nums:  # O(1)
    # 처리 로직
```

### **빈도수 계산**
```python
# Counter 사용
from collections import Counter
freq = Counter(nums)
most_common = freq.most_common(k)
```

## 📝 문제 유형별 접근법

### **중복 확인**
- 해시셋을 사용하여 O(n) 시간에 중복 확인
- 정렬 후 인접 요소 비교 (O(n log n))

### **애너그램**
- 문자 빈도수 계산 후 비교
- 정렬 후 문자열 비교

### **두 수의 합**
- 해시맵에 `target - num` 존재 여부 확인
- 투 포인터 (정렬된 배열의 경우)

### **빈도수 기반**
- Counter를 사용한 빈도수 계산
- 힙을 사용한 상위 K개 요소 찾기

## 🚀 최적화 팁

1. **해시맵 조회** - O(1) 시간 복잡도 활용
2. **중복 제거** - set을 사용한 자동 중복 제거
3. **공간 최적화** - 필요한 경우에만 추가 공간 사용
4. **경계 조건** - 빈 배열, 단일 요소 등 고려

---

*"해시맵과 해시셋은 알고리즘의 핵심 도구다. O(1) 조회를 활용하여 효율적인 솔루션을 만들자!"* 🚀
