# Heap & Priority Queue 🗃️

> 힙과 우선순위 큐를 활용한 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **23. Merge K Sorted Lists** - K개 정렬된 리스트 병합

## 🔧 주요 개념

### **힙 기본 사용법**
```python
import heapq

# 최소 힙 (기본)
min_heap = []
heapq.heappush(min_heap, 5)
heapq.heappush(min_heap, 3)
heapq.heappush(min_heap, 7)

smallest = heapq.heappop(min_heap)  # 3

# 최대 힙 (음수 활용)
max_heap = []
heapq.heappush(max_heap, -5)
heapq.heappush(max_heap, -3)
heapq.heappush(max_heap, -7)

largest = -heapq.heappop(max_heap)  # 7

# K개 정렬된 리스트 병합
def mergeKLists(lists):
    min_heap = []
    
    # 각 리스트의 첫 번째 요소를 힙에 추가
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(min_heap, (lst.val, i, lst))
    
    dummy = ListNode(0)
    current = dummy
    
    while min_heap:
        val, list_idx, node = heapq.heappop(min_heap)
        current.next = node
        current = current.next
        
        # 다음 노드가 있으면 힙에 추가
        if node.next:
            heapq.heappush(min_heap, (node.next.val, list_idx, node.next))
    
    return dummy.next
```

## 📝 문제 유형별 접근법

### **K개 리스트 병합**
- 각 리스트의 첫 번째 요소를 힙에 저장
- 최소값을 꺼내서 결과 리스트에 추가
- 다음 노드가 있으면 힙에 다시 추가

### **상위 K개 요소**
- 최소 힙으로 K개 요소 유지
- 새로운 요소가 힙의 최소값보다 크면 교체

## 🚀 최적화 팁

1. **힙 크기 제한** - K개만 유지하여 메모리 절약
2. **인덱스 활용** - 리스트 구분을 위한 인덱스 저장
3. **경계 조건** - 빈 리스트 처리
4. **최대/최소 힙** - 음수 활용으로 최대 힙 구현

---

*"힙은 우선순위 기반 정렬의 핵심 자료구조다!"* 🚀
