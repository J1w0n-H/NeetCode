# Linked List 🔗

> 연결 리스트 조작 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **18. Reverse Linked List** - 연결 리스트 뒤집기
- [ ] **19. Merge Two Sorted Lists** - 두 정렬된 리스트 병합

## 🔧 주요 개념

### **연결 리스트 기본 패턴**
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 연결 리스트 뒤집기
def reverseList(head):
    prev = None
    curr = head
    
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp
    
    return prev

# 두 정렬된 리스트 병합
def mergeTwoLists(l1, l2):
    dummy = ListNode(0)
    current = dummy
    
    while l1 and l2:
        if l1.val <= l2.val:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    
    current.next = l1 if l1 else l2
    return dummy.next
```

## 📝 문제 유형별 접근법

### **리스트 뒤집기**
- 세 개의 포인터 활용 (prev, curr, next)
- 각 노드의 next 포인터 방향 변경

### **리스트 병합**
- 더미 노드로 시작점 생성
- 두 리스트를 순회하며 작은 값부터 연결

## 🚀 최적화 팁

1. **더미 노드** - 시작점 처리 단순화
2. **포인터 관리** - 노드 연결 순서 주의
3. **경계 조건** - 빈 리스트 처리
4. **메모리 효율** - 불필요한 노드 생성 방지

---

*"연결 리스트는 포인터 조작의 기본이다!"* 🚀
