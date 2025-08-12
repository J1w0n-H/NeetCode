# Sliding Window 🪟

> 슬라이딩 윈도우 기법을 활용한 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **12. Best Time to Buy and Sell Stock** - 주식 매수/매도 타이밍
- [ ] **13. Longest Substring Without Repeating Characters** - 중복 없는 최장 부분문자열

## 🔧 주요 개념

### **슬라이딩 윈도우 기본 패턴**
```python
# 고정 크기 윈도우
window_size = k
for i in range(len(nums) - window_size + 1):
    window = nums[i:i + window_size]
    # 윈도우 내 요소들 처리

# 가변 크기 윈도우
left, right = 0, 0
while right < len(nums):
    # 윈도우 확장
    right += 1
    
    # 조건 만족 시 윈도우 축소
    while condition:
        left += 1
```

## 📝 문제 유형별 접근법

### **최대/최소 부분배열**
- 윈도우 크기를 고정하고 이동하며 계산
- 누적합 활용하여 효율성 향상

### **조건 만족하는 최장/최단 부분배열**
- 윈도우를 확장하며 조건 확인
- 조건 만족 시 윈도우 축소

## 🚀 최적화 팁

1. **누적합 활용** - O(1)로 윈도우 합 계산
2. **해시맵 활용** - 윈도우 내 요소 빈도수 추적
3. **조건 최적화** - 불필요한 계산 줄이기
4. **경계 조건** - 윈도우 크기 체크

---

*"슬라이딩 윈도우는 연속된 부분배열 문제의 핵심 기법이다!"* 🚀
