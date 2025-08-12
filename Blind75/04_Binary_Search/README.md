# Binary Search 🔍

> 이진 탐색 기법을 활용한 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **16. Search in Rotated Sorted Array** - 회전된 정렬 배열에서 검색
- [ ] **17. Find Minimum in Rotated Sorted Array** - 회전된 정렬 배열의 최소값

## 🔧 주요 개념

### **이진 탐색 기본 패턴**
```python
# 기본 이진 탐색
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

# 회전된 배열에서 이진 탐색
def search_rotated(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        
        # 왼쪽 절반이 정렬되어 있는 경우
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # 오른쪽 절반이 정렬되어 있는 경우
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    
    return -1
```

## 📝 문제 유형별 접근법

### **정렬된 배열 검색**
- 기본 이진 탐색으로 O(log n) 시간에 검색
- 중간값과 타겟 비교하여 범위 축소

### **회전된 정렬 배열**
- 어느 절반이 정렬되어 있는지 확인
- 정렬된 절반에서 타겟 존재 여부 판단

## 🚀 최적화 팁

1. **오버플로우 방지** - `mid = left + (right - left) // 2`
2. **경계 조건** - `left <= right` vs `left < right`
3. **중복 처리** - 중복 요소가 있는 경우 고려
4. **회전 배열** - 정렬된 절반 식별이 핵심

---

*"이진 탐색은 정렬된 데이터에서 O(log n) 검색을 가능하게 한다!"* 🚀
