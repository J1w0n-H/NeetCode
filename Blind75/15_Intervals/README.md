# Intervals ⏰

> 구간 관련 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **35. Merge Intervals** - 구간 병합
- [ ] **36. Insert Interval** - 구간 삽입

## 🔧 주요 개념

### **구간 처리 기본 패턴**
```python
# Merge Intervals
def merge(intervals):
    if not intervals:
        return []
    
    # 시작점 기준으로 정렬
    intervals.sort(key=lambda x: x[0])
    
    merged = []
    current = intervals[0]
    
    for interval in intervals[1:]:
        # 겹치는 구간 병합
        if current[1] >= interval[0]:
            current[1] = max(current[1], interval[1])
        else:
            merged.append(current)
            current = interval
    
    merged.append(current)
    return merged

# Insert Interval
def insert(intervals, newInterval):
    result = []
    i = 0
    
    # 새 구간보다 작은 구간들 추가
    while i < len(intervals) and intervals[i][1] < newInterval[0]:
        result.append(intervals[i])
        i += 1
    
    # 겹치는 구간들 병합
    while i < len(intervals) and intervals[i][0] <= newInterval[1]:
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i += 1
    
    result.append(newInterval)
    
    # 나머지 구간들 추가
    while i < len(intervals):
        result.append(intervals[i])
        i += 1
    
    return result

# Meeting Rooms
def canAttendMeetings(intervals):
    if not intervals:
        return True
    
    intervals.sort(key=lambda x: x[0])
    
    for i in range(1, len(intervals)):
        if intervals[i][0] < intervals[i-1][1]:
            return False
    
    return True
```

## 📝 문제 유형별 접근법

### **구간 병합**
- 시작점 기준으로 정렬
- 겹치는 구간들을 하나로 병합

### **구간 삽입**
- 새 구간과 겹치는 기존 구간들 찾기
- 겹치는 구간들을 병합하여 삽입

## 🚀 최적화 팁

1. **정렬 우선** - 시작점 기준 정렬이 핵심
2. **겹침 판단** - `end >= start` 조건 활용
3. **병합 로직** - 시작점은 최소, 끝점은 최대
4. **경계 조건** - 빈 배열, 단일 구간 처리

---

*"구간 문제는 정렬과 겹침 판단이 핵심이다!"* 🚀
