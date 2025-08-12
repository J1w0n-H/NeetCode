# Stack 📚

> 스택 자료구조를 활용한 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **14. Valid Parentheses** - 유효한 괄호
- [ ] **15. Min Stack** - 최소값 스택

## 🔧 주요 개념

### **스택 기본 패턴**
```python
# 기본 스택 구현
stack = []
stack.append(element)      # push
element = stack.pop()      # pop
top = stack[-1]           # peek

# 괄호 매칭
def isValid(s):
    stack = []
    brackets = {')': '(', '}': '{', ']': '['}
    
    for char in s:
        if char in '({[':
            stack.append(char)
        elif char in ')}]':
            if not stack or stack.pop() != brackets[char]:
                return False
    return len(stack) == 0
```

## 📝 문제 유형별 접근법

### **괄호 매칭**
- 여는 괄호는 스택에 push
- 닫는 괄호는 스택 top과 매칭 확인

### **최소값 스택**
- 두 개의 스택 활용 (값, 최소값)
- push/pop 시 최소값 동기화

## 🚀 최적화 팁

1. **스택 활용** - LIFO 특성 활용
2. **해시맵 활용** - 괄호 쌍 매핑
3. **경계 조건** - 빈 스택 체크
4. **메모리 최적화** - 필요한 경우에만 추가 공간

---

*"스택은 괄호 매칭과 역순 처리의 핵심 자료구조다!"* 🚀
