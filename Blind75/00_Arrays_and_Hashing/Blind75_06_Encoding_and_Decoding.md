# Blind 75 - 06. Encoding & Decoding

## 문제 정보
- **난이도**: Medium
- **카테고리**: String, Design
- **출처**: LeetCode

## 문제 설명
Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

**Example 1:**
```
Input: ["Hello","World"]
Output: "5#Hello5#World"
```

**Example 2:**
```
Input: [""]
Output: "0#"
```

**Constraints:**
- 1 <= strs.length <= 200
- 0 <= strs[i].length <= 200
- strs[i] contains any possible characters out of 256 valid ASCII characters.

## 내 코드 (오답)
```python
class Solution:
    size = []

    def encode(self, strs: List[str]) -> str:
        res = ""
        
        for word in strs:
            res += word
            print(word, self.size)
            self.size.append(len(word))
        print(res, self.size)
        return res    

    def decode(self, s: str) -> List[str]:
        res = []
        sum = 0
        print(s)
        j=0
        while j < len(self.size)-1:
            for i, ch in enumerate(s):
                print(sum, j, self.size[j])    
                if sum == self.size[j]:
                    res.append(s[i-sum:i])
                    print("OK")
                    sum -= self.size[j]
                    
                    j+=1
                print(ch, i, self.size, sum)
                sum += 1
        res.append(s[len(s)-j:])
        return res
```

## 정답 코드 + 피드백
```python
class Solution:
    def encode(self, strs: List[str]) -> str:
        res = ""
        for s in strs:
            res += str(len(s)) + "#" + s
        return res

    def decode(self, s: str) -> List[str]:
        res = []
        i = 0
        while i < len(s):
            j = i
            while s[j] != '#':
                j += 1
            length = int(s[i:j])
            i = j + 1
            j = i + length
            res.append(s[i:j])
            i = j
        return res
```

### 피드백

**내 코드의 문제점:**
1. **클래스 변수 오용**: `self.size`를 클래스 변수로 사용하여 여러 인스턴스 간 데이터 공유 문제 발생
2. **길이 정보 누락**: `encode()`에서 문자열 길이 정보를 저장하지 않아 `decode()`에서 원본 문자열 복원 불가능
3. **복잡한 디코딩 로직**: `sum` 변수를 사용한 복잡한 인덱스 계산으로 버그 발생 가능성 높음
4. **비효율적인 중첩 루프**: `while`과 `for` 루프의 중첩으로 O(n²) 시간 복잡도
5. **디버깅 코드 포함**: `print` 문들이 프로덕션 코드에 남아있음
6. **논리적 오류**: `sum` 변수의 증가/감소 로직이 복잡하고 오류 발생 가능성 높음

**정답 코드의 장점:**
1. **단순한 구분자**: `길이#문자열` 형태로 하나의 구분자만 사용
2. **직접적인 파싱**: 길이를 읽자마자 바로 문자열을 추출
3. **메모리 효율성**: 추가 배열 없이 직접 처리
4. **명확한 로직**: 각 단계가 명확하고 이해하기 쉬움
5. **코드 간결성**: 더 적은 코드로 동일한 기능 구현
6. **안정성**: 복잡한 인덱스 계산 없이 안정적인 파싱

## 기억할 요점

### 1. **구분자 설계의 중요성**
- 복잡한 구분자는 파싱을 어렵게 만들고 버그 발생 가능성 증가
- 단순한 구분자(`길이#문자열`)가 가장 효율적

### 2. **클래스 변수 vs 인스턴스 변수**
```python
# ❌ 잘못된 방법 - 클래스 변수 사용
class Solution:
    size = []  # 모든 인스턴스가 공유

# ✅ 올바른 방법 - 인스턴스 변수 사용
class Solution:
    def __init__(self):
        self.size = []  # 각 인스턴스마다 독립적
```

### 3. **구분자 설계의 중요성**
```python
# ❌ 복잡한 구분자 사용
res += str(sz) + ','  # 길이 + 쉼표
res += '#'            # 별도 구분자
# 결과: "4,5,3,#HelloWorldCode"

# ✅ 단순한 구분자 사용
res += str(len(s)) + "#" + s  # 길이 + # + 문자열
# 결과: "5#Hello4#Code3#Yes"
```

### 4. **문자열 파싱 패턴**
```python
# 길이를 먼저 읽고, 그 다음에 문자열 추출
j = i
while s[j] != '#':
    j += 1
length = int(s[i:j])
i = j + 1
j = i + length
res.append(s[i:j])
i = j
```

### 5. **인덱스 관리**
- `i`는 현재 위치를 추적
- `j`는 임시로 사용하여 구분자 위치 찾기
- 각 단계 후 `i`를 적절히 업데이트

### 6. **경계 조건 처리**
- 빈 문자열 리스트: `if not strs: return ""`
- 빈 문자열: `if not s: return []`

### 7. **알고리즘 설계 원칙**
- **단순성**: 복잡한 로직보다는 직관적인 접근 방식 선택
- **효율성**: 불필요한 중첩 루프 피하기
- **명확성**: 각 단계의 목적이 명확해야 함

### 8. **디버깅 코드 관리**
- 개발 중에는 `print` 문으로 디버깅
- 프로덕션 코드에서는 반드시 제거
- 로깅 시스템 사용 고려

## 시간 및 공간 복잡도

**시간 복잡도**: O(m)
- `encode()`: 모든 문자열을 순회하며 O(m)
- `decode()`: 인코딩된 문자열을 한 번 순회하며 O(m)
- 여기서 m은 모든 문자열의 길이 합

**공간 복잡도**: O(m + n)
- `encode()`: 결과 문자열을 위한 O(m)
- `decode()`: 원본 문자열 리스트를 위한 O(n)
- 여기서 n은 문자열의 개수

## 테스트 케이스

```python
# 테스트 1: 일반적인 경우
strs = ["Hello", "World"]
encoded = solution.encode(strs)  # "5#Hello5#World"
decoded = solution.decode(encoded)  # ["Hello", "World"]

# 테스트 2: 빈 문자열 포함
strs = ["", "abc", ""]
encoded = solution.encode(strs)  # "0#3#abc0#"
decoded = solution.decode(encoded)  # ["", "abc", ""]

# 테스트 3: 특수 문자 포함
strs = ["Hello#World", "Test,Comma"]
encoded = solution.encode(strs)  # "11#Hello#World11#Test,Comma"
decoded = solution.decode(encoded)  # ["Hello#World", "Test,Comma"]
```

## 다음에 주의할 점

1. **클래스 변수 사용 금지**: `self.size = []` 같은 클래스 변수는 여러 인스턴스 간 데이터 공유 문제 발생
2. **구분자 설계**: 가능한 한 단순한 구분자 사용 (하나의 구분자로 충분)
3. **중간 배열 최소화**: 불필요한 `sizes` 배열 생성 피하기
4. **인덱스 관리**: 문자열 파싱 시 인덱스 업데이트 순서 주의
5. **경계 조건**: 빈 문자열, 특수 문자 등 예외 상황 고려
6. **메모리 효율성**: 추가 메모리 사용을 최소화
7. **가독성**: 복잡한 로직보다는 직관적인 접근 방식 선택
8. **디버깅 코드 제거**: `print` 문은 개발 완료 후 반드시 제거
9. **알고리즘 복잡도**: 중첩 루프 사용 시 시간 복잡도 고려
10. **논리적 오류 방지**: 복잡한 변수 증가/감소 로직은 버그 발생 가능성 높음
