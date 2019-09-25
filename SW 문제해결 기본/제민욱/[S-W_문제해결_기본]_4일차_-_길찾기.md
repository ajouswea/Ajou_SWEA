#  [S/W 문제해결 기본] 4일차 - 길찾기
> [링크](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14geLqABQCFAYD)

- 접근법
```
도시에 대하여 child 배열 2개를 만들고, 연결 되어있다면 해당 값 idx에 child idx를 넣어준다.

-> 입력값으로 node의 갯수가 나오지 않았기 때문에, list로 하지 않고 defaultdict로 만들어주었다. 또한 visited를 set으로 두어 체크해주었다.(cycle이 생긴다는 건 생각하지 않아도 될것이, 만약 cycle해서 다른 path로 가는 경우와 애초부터 다른 path로 가는 방법이 같기 때문이다.)
```

```python
from collections import defaultdict

def dfs(node,visited):
    global answer
    if answer:
        return
    elif node == 99:
        answer = 1
        return
    for nxt in graph[node]:
        if nxt not in visited:
            new_visited = visited.copy()
            new_visited.add(nxt)
            dfs(nxt,new_visited)

for _ in range(10):
    tc, edges = map(int,input().split())
    nodes = list(map(int,input().split()))
    graph = defaultdict(list)
    for i in range(0,len(nodes),2):
        graph[nodes[i]].append(nodes[i+1])

    answer = 0
    dfs(0,set([0]))
    print(f'#{tc} {answer}')

```

