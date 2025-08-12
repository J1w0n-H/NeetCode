# Trees 🌳

> 트리 순회 및 비교 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **20. Maximum Depth of Binary Tree** - 이진 트리의 최대 깊이
- [ ] **21. Same Tree** - 같은 트리인지 확인

## 🔧 주요 개념

### **트리 순회 기본 패턴**
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# DFS - 재귀
def maxDepth(root):
    if not root:
        return 0
    return 1 + max(maxDepth(root.left), maxDepth(root.right))

# BFS - 큐
def maxDepthBFS(root):
    if not root:
        return 0
    
    queue = [(root, 1)]
    max_depth = 0
    
    while queue:
        node, depth = queue.pop(0)
        max_depth = max(max_depth, depth)
        
        if node.left:
            queue.append((node.left, depth + 1))
        if node.right:
            queue.append((node.right, depth + 1))
    
    return max_depth

# 같은 트리 확인
def isSameTree(p, q):
    if not p and not q:
        return True
    if not p or not q:
        return False
    if p.val != q.val:
        return False
    
    return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```

## 📝 문제 유형별 접근법

### **트리 깊이**
- DFS: 재귀적으로 좌우 서브트리 깊이 계산
- BFS: 레벨별로 순회하며 깊이 추적

### **트리 비교**
- 구조와 값이 모두 동일한지 확인
- 재귀적으로 좌우 서브트리 비교

## 🚀 최적화 팁

1. **재귀 활용** - 트리 구조에 자연스러운 접근
2. **BFS vs DFS** - 문제에 맞는 순회 방식 선택
3. **경계 조건** - 빈 노드 처리
4. **메모리 효율** - 스택/큐 크기 고려

---

*"트리는 재귀와 순회의 기본 자료구조다!"* 🚀
