# disk 돌리기

- 2차원 배열을 두고 disk를 돌리고, 인접한 녀석이 존재하면 삭제
- 삭제를 해당 분기에서 못한다면 mean값에 따라서 값 +1/-1
- 모든 명령어를 실행해주고 남아있는 val들의 총합 return 해주면 된다.

```python
def clock(arr,ty,n):
    global N,M
    n %= M
    for y in range(N):
        if (y+1)%ty == 0:
            arr[y] = arr[y][M-n:]+arr[y][:M-n]
            # 시험때는 [:]를 해주어서 copy를 해주었다.
def counter_clock(arr,ty,n):
    global N, M
    n %= M
    for y in range(N):
        if (y+1)%ty == 0:
            arr[y] = arr[y][n:]+arr[y][:n]

# visited_set을 두고 중복 control 해줬으면 더욱 깔끔했을 것
# visit없이 board[y][x]=0으로 해버린다면 each time

import pprint
from collections import deque
def bfs(_y,_x):
    global N,M
    v = board[_y][_x]
    queue = deque([(_y,_x)])
    init_flag = False
    killed = 0
    while queue:
        y,x = queue.popleft()
        for ny,nx in (y,x+1),(y,x-1),(y+1,x),(y-1,x):
            if (0<=ny<N and 0<=nx<M) and board[ny][nx]==v:
                queue.append((ny,nx))
                board[ny][nx]=0
                killed+=1
                if not init_flag:
                    init_flag = True
                    board[_y][_x]=0
                    killed+=1
    return killed



# main()
board = None
cmd = None
N = M = 0
with open('tmp.txt','r') as f:
    N,M = map(int,f.readline().split())
    board = [list(map(int,f.readline().split())) for _ in range(N)]
    cmd = []


alive = N*M
for c in cmd:

    # bfs_all()
    flag = False
    for y in range(N):
        for x in range(M):
            if board[y][x]:
                killed=bfs(y,x)
                alive-=killed
                if not flag and killed:
                    flag = True
    # 평균값
    if alive==0:break
    if not flag:
        mean = sum([sum(row) for row in board])//alive
        for y in range(N):
            for x in range(M):
                if board[y][x]:
                    if board[y][x]==mean:continue
                    elif board[y][x]>mean:
                        board[y][x] -= 1
                    else:
                        board[y][x] += 1
print(sum([sum(row) for row in board]))
```

- 앞으로 pycharm문제에서 with open으로 테스트를 계속 돌릴 수 있도록 with open으로 read 해주자. window터미널에서 cat을 사용하지 못하니까, 