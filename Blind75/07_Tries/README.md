# Tries 🔤

> 트라이 자료구조를 활용한 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **22. Implement Trie** - 트라이 구현

## 🔧 주요 개념

### **트라이 기본 구현**
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
    
    def startsWith(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

## 📝 문제 유형별 접근법

### **트라이 구현**
- 노드별로 자식 노드들을 딕셔너리로 관리
- 단어 끝 표시를 위한 is_end 플래그

### **문자열 검색**
- 접두사 검색: 트라이를 따라가며 존재 여부 확인
- 완전한 단어 검색: 끝 노드의 is_end 플래그 확인

## 🚀 최적화 팁

1. **딕셔너리 활용** - O(1) 자식 노드 접근
2. **메모리 효율** - 공통 접두사 공유
3. **경계 조건** - 빈 문자열 처리
4. **구조 설계** - 노드와 트라이 클래스 분리

---

*"트라이는 문자열 검색의 효율적인 자료구조다!"* 🚀
