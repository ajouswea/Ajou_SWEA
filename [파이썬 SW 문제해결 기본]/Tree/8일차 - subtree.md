# subtree 8일차

```python
def dfs(n):
    global answer
    answer+=1
    if l_child[n] != None:
        dfs(l_child[n])
    if r_child[n] != None:
        dfs(r_child[n])

for tc in range(int(input())):
    E, N = map(int,input().split())
    l_child = [None for _ in range(E + 1)]
    r_child = [None for _ in range(E + 1)]
    raw_data = [v-1 for v in list(map(int,input().split()))]
    for i in range(0,len(raw_data),2):
        if l_child[raw_data[i]]==None:
            l_child[raw_data[i]] = raw_data[i + 1]
        else:
            r_child[raw_data[i]] = raw_data[i + 1]
    answer = 0
    dfs(N-1)
    print(f'#{tc+1} {answer}')
```