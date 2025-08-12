# Graphs 🕸️

> 그래프 탐색 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **26. Number of Islands** - 섬의 개수
- [ ] **27. Clone Graph** - 그래프 복사

## 🔧 주요 개념

### **그래프 탐색 기본 패턴**
```python
# DFS - 재귀
def dfs(node, visited):
    if not node or node in visited:
        return
    
    visited.add(node)
    # 노드 처리
    
    for neighbor in node.neighbors:
        dfs(neighbor, visited)

# BFS - 큐
def bfs(start):
    if not start:
        return
    
    queue = [start]
    visited = {start}
    
    while queue:
        node = queue.pop(0)
        # 노드 처리
        
        for neighbor in node.neighbors:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

# 섬의 개수 세기
def numIslands(grid):
    def dfs(i, j):
        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]) or grid[i][j] == '0':
            return
        
        grid[i][j] = '0'  # 방문 표시
        
        # 4방향 탐색
        dfs(i + 1, j)
        dfs(i - 1, j)
        dfs(i, j + 1)
        dfs(i, j - 1)
    
    count = 0
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == '1':
                dfs(i, j)
                count += 1
    
    return count
```

## 📝 문제 유형별 접근법

### **섬의 개수**
- 2D 그리드에서 연결된 '1'들을 하나의 섬으로 간주
- DFS로 연결된 모든 '1'을 '0'으로 변경

### **그래프 복사**
- BFS로 모든 노드를 순회하며 복사
- 해시맵으로 원본-복사본 매핑

## 🚀 최적화 팁

1. **방문 표시** - 중복 방문 방지
2. **경계 체크** - 배열 범위 벗어남 방지
3. **재귀 vs 반복** - 스택 오버플로우 고려
4. **메모리 효율** - 방문 배열 대신 값 변경

---

*"그래프는 연결 관계를 표현하는 기본 자료구조다!"* 🚀
