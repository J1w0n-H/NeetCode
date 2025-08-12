# Math & Geometry 📐

> 수학 및 기하학 문제들의 오답노트

## 📋 문제 목록

### 🔄 **예정 문제들**
- [ ] **37. Rotate Image** - 이미지 회전
- [ ] **38. Spiral Matrix** - 나선형 행렬

## 🔧 주요 개념

### **행렬 조작 기본 패턴**
```python
# Rotate Image (90도 시계방향)
def rotate(matrix):
    n = len(matrix)
    
    # 전치 (transpose)
    for i in range(n):
        for j in range(i, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    
    # 각 행 뒤집기
    for i in range(n):
        matrix[i].reverse()

# Spiral Matrix
def spiralOrder(matrix):
    if not matrix:
        return []
    
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    
    while top <= bottom and left <= right:
        # 위쪽 행
        for j in range(left, right + 1):
            result.append(matrix[top][j])
        top += 1
        
        # 오른쪽 열
        for i in range(top, bottom + 1):
            result.append(matrix[i][right])
        right -= 1
        
        # 아래쪽 행
        if top <= bottom:
            for j in range(right, left - 1, -1):
                result.append(matrix[bottom][j])
            bottom -= 1
        
        # 왼쪽 열
        if left <= right:
            for i in range(bottom, top - 1, -1):
                result.append(matrix[i][left])
            left += 1
    
    return result

# Pascal's Triangle
def generate(numRows):
    if numRows == 0:
        return []
    
    triangle = [[1]]
    
    for i in range(1, numRows):
        row = [1]
        for j in range(1, i):
            row.append(triangle[i-1][j-1] + triangle[i-1][j])
        row.append(1)
        triangle.append(row)
    
    return triangle
```

## 📝 문제 유형별 접근법

### **이미지 회전**
- 전치 후 각 행 뒤집기
- 90도 회전 = 전치 + 행 뒤집기

### **나선형 순회**
- 4방향 순서대로 경계 줄이기
- 경계 조건 체크로 중복 방지

## 🚀 최적화 팁

1. **제자리 조작** - 추가 공간 없이 행렬 수정
2. **경계 관리** - top, bottom, left, right 변수 활용
3. **수학적 패턴** - 파스칼 삼각형 등의 수학적 규칙
4. **인덱스 계산** - 행렬 인덱스 조작 주의

---

*"수학과 기하학은 패턴과 규칙을 찾는 문제다!"* 🚀
