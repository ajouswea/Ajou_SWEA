# min max

> [알고리즘 분류],[문제 URI](https://swexpertacademy.com/main/learn/course/lectureProblemViewer.do)

## `Problem`
> max-min

## `1st try`
- **`Before try`(`접근법`)**
`o(n)`으로 min과 max를 탐색하도록 하자

- `Algorithm`
```python
T = int(input())
for tc in range(1,T+1):
    input() # garbage
    min_v = 1000001;max_v = 0
    for i in input().split():
        i = int(i)
        if i<min_v:
            min_v = i
        if i>max_v:
            max_v = i
    result = max_v - min_v
    print("#%d %d"%(tc,result))
```
- **After try(회고)**
그냥 input받고 sort 하고 [-1]-[0]하면 되긴 하다.