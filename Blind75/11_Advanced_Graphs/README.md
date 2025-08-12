# Advanced Graphs 🕸️⚡

> 고급 그래프 알고리즘 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **28. Course Schedule** - 강의 스케줄

## 🔧 주요 개념

### **위상 정렬 (Topological Sort)**
```python
# Course Schedule - 위상 정렬
def canFinish(numCourses, prerequisites):
    # 인접 리스트 및 진입 차수 계산
    graph = [[] for _ in range(numCourses)]
    in_degree = [0] * numCourses
    
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        in_degree[course] += 1
    
    # 진입 차수가 0인 노드들을 큐에 추가
    queue = []
    for i in range(numCourses):
        if in_degree[i] == 0:
            queue.append(i)
    
    # 위상 정렬 수행
    count = 0
    while queue:
        course = queue.pop(0)
        count += 1
        
        # 이웃 노드들의 진입 차수 감소
        for neighbor in graph[course]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    return count == numCourses

# DFS를 이용한 위상 정렬
def canFinishDFS(numCourses, prerequisites):
    graph = [[] for _ in range(numCourses)]
    visited = [0] * numCourses  # 0: 미방문, 1: 방문중, 2: 완료
    
    for course, prereq in prerequisites:
        graph[prereq].append(course)
    
    def hasCycle(course):
        if visited[course] == 1:  # 사이클 발견
            return True
        if visited[course] == 2:  # 이미 완료
            return False
        
        visited[course] = 1  # 방문중
        
        for neighbor in graph[course]:
            if hasCycle(neighbor):
                return True
        
        visited[course] = 2  # 완료
        return False
    
    for course in range(numCourses):
        if hasCycle(course):
            return False
    
    return True
```

## 📝 문제 유형별 접근법

### **위상 정렬**
- 의존 관계가 있는 작업들의 순서 결정
- 진입 차수가 0인 노드부터 처리

### **사이클 감지**
- DFS로 방문 상태 추적
- 방문중인 노드를 다시 방문하면 사이클

## 🚀 최적화 팁

1. **진입 차수 활용** - BFS 기반 위상 정렬
2. **방문 상태 추적** - DFS 기반 사이클 감지
3. **인접 리스트** - 메모리 효율적인 그래프 표현
4. **경계 조건** - 빈 그래프, 단일 노드 처리

---

*"고급 그래프 알고리즘은 복잡한 의존 관계를 해결한다!"* 🚀
