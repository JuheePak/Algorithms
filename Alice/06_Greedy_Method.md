### `Greedy Method(탐욕적 기법)`

- **순간의 최적의 선택**이 궁극적으로 최적의 선택이다.
- **단순한 방법**도 문제 풀이에는 충분하다.



### 거스름돈 문제

> 거스름돈 n원을 돌려주어야 할 때, 돌려주어야 하는 동전 개수의 최솟값을 출력하는 프로그램을 작성하세요.

``` python
import sys

def coinChange(n) :
    '''
    n원을 돌려주기 위해 필요한 동전 개수의 최솟값을 반환하는 함수를 작성하세요.
    '''
    result = 0 # 동전의 개수
    coins = [100, 50, 10, 5, 1] # 동전 각각의 리스트
    
    for coin in coins:
        result += n // coin
        
        n = n % coin # 지불하고 남은 액수   
    return result

def main():
    n = int(input())
    print(coinChange(n))

if __name__ == "__main__":
    main()
```



### 기울기가 가장 큰 두 점 찾기 (Big)

> 2차원 평면에 n개의 점이 있다. 이 점들 중에서 두 점을 선택했을 때, 그 기울기의 절댓값의 최댓값을 출력하는 프로그램을 작성하시오. 단, 모든 점의 x좌표는 다르다고 가정한다. 또한, 두 점 (x1, y1), (x2, y2)의 기울기는 (y2 - y1) / (x2 - x1) 으로 정의된다.
>
> 예를 들어, 4개의 점이 각각 (0, 3), (1, 1), (2, 2), (4, 1) 에 위치해 있다고 하면, 기울기의 절댓값의 최댓값은 2가 된다.
>
> 이 경우 기울기 절댓값의 최댓값인 2를 출력합니다.
>
> 입력으로는 첫줄에 점의 개수가, 그 다음줄부터는 점의 x좌표와 y좌표가 입력됩니다.

``` python
import sys

def getSlope(a, b):
    return abs((b[1] - a[1]) / (b[0] - a[0]))
def maxSlope(points) :
    '''
    n개의 점들 중에서 2개의 점을 선택했을 때, 얻을 수 있는 기울기의 절댓값 중에서 가장 큰 값을 반환하는 함수를 작성하세요.

    **주의** : 소숫점 넷째자리에서 반올림하는 것은 고려할 필요가 없습니다. 이는 main()에서 출력을 할 때에 처리가 되므로, 기울기의 최댓값을 구하는 것에 집중해 주시길 바랍니다.
    '''    
    points.sort()
    result = 0
    for i in range(len(points) -1):
        result = max(result, getSlope(points[i], points[i+1]))

    return result

def main():
    n = int(input())
    points = []

    for i in range(n) :
        line = [int(x) for x in input().split()]
        points.append( (line[0], line[1]) )

    print("%.3lf" % maxSlope(points))

if __name__ == "__main__":
    main()
```



### Fractional knapsack

> *n*개의 물건이 있고, 각 물건은 무게 w_i와 가치 c_i를 갖는다. 이제 이 물건들을 배낭에 넣으려 한다. 이 배낭은 무게 m까지를 버틸 수 있다.
>
> 한 가지 재미있는 사실은, 물건을 쪼갤 수 있다는 것이다. 물론, 물건을 쪼개게 되면 무게가 줄지만, 가치도 줄게 된다. 예를 들어, 무게를 절반으로 줄이면 가치 역시도 절반으로 줄어들게 된다.
>
> 배낭이 버틸 수 있는 무게 m과 n개의 물건의 정보가 주어질 때, 배낭이 담을 수 있는 가치의 최댓값을 소숫점 넷째자리에서 반올림하여 출력하는 프로그램을 작성하세요.
>
> 입력에 첫줄에는 물건의 개수n과 베낭의 버틸수 있는 무게 m이 입력됩니다.
>
> 이후 n*n*개의 줄에 대하여 각 물건의 무게 w_i, 그리고 가치 c_i가 주어진다.

``` python
import sys

def fKnapsack(materials, m) :
    '''
    크기 m까지 버틸 수 있는 베낭이 담을 수 있는 최대 가치를 반환하는 함수를 작성하세요.
    주의: 셋째 자리에서 반올림하는 것을 고려하지 않고 작성하셔도 됩니다.    
    물건을 가성비 순서대로 넣기
    x[0]: 무게
    x[1]: 가치
    '''
    materials = sorted(materials, key = lambda x: x[1]/x[0], reverse=True)
    
    weight = 0
    value = 0
    
    for i in range(len(materials)):
        """
        1. 물건을 넣어도 아직 버틸만한 무게일 때
        2. 물건을 넣으면 딱 m만큼 무게가 될 때
        3. 물건을 다 넣으면 m을 넘어갈 때
        """
        if weight + materials[i][0] < m:
            weight += materials[i][0]
            value += materials[i][1]
            
        elif weight + materials[i][0] == m:
            weight += materials[i][0]
            value += materials[i][1]
            
            return value
        else:
            temp = m - weight
            value += temp*(materials[i][1]/materials[i][0])
            return value
            
    return value
def main():
    line = [int(x) for x in input().split()]

    n = line[0]
    m = line[1]

    materials = []

    for i in range(n) :
        data = [int(x) for x in input().split()]
        materials.append( (data[0], data[1]) )

    print("%.3lf" % fKnapsack(materials, m))

if __name__ == "__main__":
    main()
```

