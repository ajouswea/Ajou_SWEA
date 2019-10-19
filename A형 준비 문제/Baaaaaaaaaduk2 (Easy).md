# Baaaaaaaaaduk2 (Easy)

> https://www.acmicpc.net/problem/16988

## 1st try
```
- z_pos를 구하고 2개의 조합을 구한다.


```

```python
def permute(arr,c):
    r = [[]]
    for i in range(c):
        r = [[a]+b for a in arr for b in r if a not in b]
    return r

def dbfs(_y,_x):
    visited[_y][_x] = 1
    stack = [(_y,_x)]
    segment = [(_y,_x)]
    while stack:
        y,x = stack.pop()
        for nxy in (y,x+1),(y,x-1),(y+1,x),(y-1,x):
            ny,nx =nxy
            if (0<=ny<N and 0<=nx<M) and not visited[ny][nx] and board[ny][nx]==2:
                visited[ny][nx]=1
                stack.append((ny,nx))
                segment.append((ny, nx))
    w_pos.append(segment)



# 1이나 outof bound이거나 perm속에 있어야한다. 없다면 false
def check(perm):
    global result
    count = 0
    for seg in w_pos:
        flag = False
        for w in seg:
            for nxy in (w[0],w[1]+1),(w[0],w[1]-1),(w[0]+1,w[1]),(w[0]-1,w[1]):
                ny,nx = nxy
                if (0<=ny<N and 0<=nx<M) and board[ny][nx]==0 and (ny,nx) not in perm:
                    flag = True
                    break
            if flag:break
        else:count+=len(seg)

    if count>result:
        result = count


# 시작 할 때 segment를 줄여야 한다.
N,M = map(int,input().split())
board = [list(map(int,input().split(' '))) for _ in range(N)]
visited = [[0]*M for _ in range(N)]
w_pos = []
z_pos = []
for y in range(N):
    for x in range(M):
        if board[y][x]==0:
            z_pos.append((y,x))
        elif board[y][x]==2:
            if not visited[y][x]:
                dbfs(y,x)    # segment


result = 0
for perm in permute(z_pos,2):
    check(perm)
print(result)
```


- 수정본
```python
def permute(arr,c):
    r = [[]]
    for i in range(c):
        r = [[a]+b for a in arr for b in r if a not in b]
    return r







def dbfs(_y,_x):
    visited[_y][_x] = 1
    stack = [(_y,_x)]
    segment = [(_y,_x)]
    while stack:
        y,x = stack.pop()
        for nxy in (y,x+1),(y,x-1),(y+1,x),(y-1,x):
            ny,nx =nxy
            if (0<=ny<N and 0<=nx<M) and not visited[ny][nx] and board[ny][nx]==2:
                visited[ny][nx]=1
                stack.append((ny,nx))
                segment.append((ny, nx))
    w_pos.append(segment)



# 1이나 outof bound이거나 perm속에 있어야한다. 없다면 false
def check(perm):
    global result
    count = 0
    for seg in w_pos:
        flag = False
        for w in seg:
            for nxy in (w[0],w[1]+1),(w[0],w[1]-1),(w[0]+1,w[1]),(w[0]-1,w[1]):
                ny,nx = nxy
                if (0<=ny<N and 0<=nx<M) and board[ny][nx]==0 and (ny,nx) not in perm:
                    flag = True
                    break
            if flag:break
        else:count+=len(seg)

    if count>result:
        result = count


# 시작 할 때 segment를 줄여야 한다.
N,M = map(int,input().split())
board = [list(map(int,input().split(' '))) for _ in range(N)]
visited = [[0]*M for _ in range(N)]
w_pos = []
z_pos = []
for y in range(N):
    for x in range(M):
        if board[y][x]==0:
            z_pos.append((y,x))
        elif board[y][x]==2:
            if not visited[y][x]:
                dbfs(y,x)    # segment

result = 0
_combs = []
combination(10,2)
# print(len(z_pos))
# combination(len(z_pos),2)
print(_combs)
# for comb in combs(len(z_pos),2):
#     check([z_pos[c] for c in comb])
print(result)
```