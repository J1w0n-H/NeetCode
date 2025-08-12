# Greedy 🎯

> 그리디 알고리즘 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **33. Jump Game** - 점프 게임
- [ ] **34. Gas Station** - 주유소

## 🔧 주요 개념

### **그리디 기본 패턴**
```python
# Jump Game
def canJump(nums):
    max_reach = 0
    
    for i in range(len(nums)):
        if i > max_reach:
            return False
        
        max_reach = max(max_reach, i + nums[i])
        
        if max_reach >= len(nums) - 1:
            return True
    
    return True

# Gas Station
def canCompleteCircuit(gas, cost):
    total_gas = 0
    current_gas = 0
    start_station = 0
    
    for i in range(len(gas)):
        total_gas += gas[i] - cost[i]
        current_gas += gas[i] - cost[i]
        
        # 현재 가스가 부족하면 시작점 변경
        if current_gas < 0:
            current_gas = 0
            start_station = i + 1
    
    return start_station if total_gas >= 0 else -1

# 최소 동전 개수
def coinChange(coins, amount):
    coins.sort(reverse=True)
    count = 0
    
    for coin in coins:
        count += amount // coin
        amount %= coin
    
    return count if amount == 0 else -1
```

## 📝 문제 유형별 접근법

### **Jump Game**
- 각 위치에서 도달할 수 있는 최대 거리 추적
- 현재 위치가 도달 가능한지 확인

### **Gas Station**
- 전체 가스와 비용의 차이 계산
- 누적 가스가 음수가 되면 시작점 변경

## 🚀 최적화 팁

1. **로컬 최적** - 각 단계에서 최선의 선택
2. **정렬 활용** - 큰 값부터 처리
3. **누적 계산** - 전체 상태 추적
4. **경계 조건** - 불가능한 경우 처리

---

*"그리디는 각 단계에서 최선의 선택을 하는 알고리즘이다!"* 🚀
