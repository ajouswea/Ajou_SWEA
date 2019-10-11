# Brainf**k
> [시뮬레이션], [문제링크](https://www.acmicpc.net/problem/3954)

```
- 목표: Terminates or Loops

- 조건
    -  프로그램이 명령어를 50,000,000번 이상 수행한 경우,프로그램은 항상 종료되었거나 무한 루프에 빠져있다.
    - 데이터 배열 값이 underflow나 overflow를 일으킬 수 있다.
        - 오버플로우: max를 넘어가면 min으로 변환
        - 언더플로우: min을 넘어가면 max로 변환
    - 프로그램을 수행하기 전에, 데이터 배열의 값은 0으로 초기화되어 있고, 포인터가 가리키는 칸은 0번 칸이다.
    - 출력은 무시한다.

- Loop가 생성될 조건
    - 괄호가 시작되는 곳으로 만약 같은 값이 들어온다면 loop의 시작이므로 LOOP Opened CLosed를 return
```

## 1st try (x)
- `,`이 나왔을 때 어떻게 처리를 해주어야 하는건가?
- loop검사는 한번 왔던 곳을 같은 값(메모리 값, 메모리 idx)으로 다시 돌아온다면 무한 루프가 발생하지 않을까?
```python
END = 5000000
def interpret(mp,pp,op,flag):
    bracket_flag = False
    if program[pp]=='+':
        memory[mp] += 1
    elif program[pp]=='-':
        memory[mp] -= 1
    elif program[pp]=='<':
        mp -= 1
        if mp==-1:
            mp=len(memory)
    elif program[pp]=='>':
        mp += 1
        if mp==len(memory):
            mp=0
    elif program[pp] == '[':
        op = pp
        if memory[mp]==0:
            pp = bracket_dict[pp]
            bracket_flag = True

        if loop_trace.get(op,None)==None:
            loop_trace[op] = [(mp,memory[mp])]
        else:
            if (mp,memory[mp]) not in loop_trace[op]:
                loop_trace[op].append((mp,memory[mp]))
            else:
                flag = True

    elif program[pp]==']':
        if memory[mp] != 0:
            pp = bracket_dict[pp]
            bracket_flag = True
    elif program[pp] == '.':
        pass
    else:
        memory[mp] = 255 if input_data == [] else ord(input_data.pop())

    return mp,pp+1,op,flag if not bracket_flag else mp,pp,op,flag

# main()
for tc in range(int(input())):
    sm,sc,si = map(int,input().split())
    program = list(input())

    # 괄호 idx위치 저장
    stack = [];bracket_dict = dict()
    for i,p in enumerate(program):
        if p == '[':
            stack.append(i)
        elif p == ']':
            opened = stack.pop()
            closed = i
            bracket_dict[opened]=closed
            bracket_dict[closed]=opened


    loop_trace = dict()
    mem_pnt = prg_pnt = break_cnt = opened =  0

    memory = [0]*sm
    input_data = list(input())[::-1]
    flag = False
    while break_cnt<END:
        mem_pnt, prg_pnt, opened, flag = interpret(mem_pnt,prg_pnt,opened,flag)
        break_cnt+=1
        if flag: break
        if prg_pnt == sc:
            print('Terminates')
            break

    # 종료 조건
    if flag or break_cnt==END:
        print(f'Loops {opened} {bracket_dict[opened]}')
```