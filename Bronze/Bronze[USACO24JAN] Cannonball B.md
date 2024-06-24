# [USACO24JAN] Cannonball B

## 题目描述

Bessie 已经精通了变成炮弹并沿着长度为 $N$ $1\le N\le 10^5$的数轴弹跳的艺术，数轴上的位置从左到右编号为 $1,2,\cdots,N$。她从某个整数位置 $S$ $1\le S\le N$ 开始，以 $1$ 的起始能量向右弹跳。 如果 Bessie 的能量为 $k$，则她将弹跳至距当前位置向前距离 $k$ 处进行下一次弹跳。

从 $1$ 到 $N$ 的每个整数位置上均有炮击目标或跳板。每个炮击目标和跳板都有一个在 $0$ 到 $N$ 范围内的整数值。一个数值为 $v$ 的跳板会使 Bessie 的能量增加 $v$ 并反转她的方向。一个数值为 $v$ 的炮击目标会当着陆时能量不小于 $v$ 时被击破。着陆在炮击目标上不会改变 Bessie 的能量和方向。被击破的炮击目标将保持击破状态，Bessie 依然可以该炮击目标上弹跳，同样不会改变能量和方向。

如果 Bessie 弹跳无限长的时间或直到她离开数轴，她会击破多少个炮击目标？

如果 Bessie 开始时位于一个她可以击破的炮击目标，她会立刻这样做。类似地，如果 Bessie 开始时位于一个跳板，跳板的效果将在她第一次跳跃之前生效。

## 输入格式

输入的第一行包含 $N$ 和 $S$，其中 $N$ 为数轴的长度，S 为 Bessie 的起始位置。

以下 $N$ 行描述了每一个位置。其中第 $i$ 行包含整数 $q_i$ 和 $v_i$，如果位置 $i$ 上有一个跳板则 $q_i=0$，位置 $i$ 上有一个炮击目标则 $q_i=1$ $v_i$ 是位置 $i$ 上的跳板或炮击目标的数值。

## 输出格式

输出一个整数，为将被击破的炮击目标数量。

## 样例 #1

### 样例输入 #1

```
5 2
0 1
1 1
1 2
0 1
1 1
```

### 样例输出 #1

```
1
```

## 样例 #2

### 样例输入 #2

```
6 4
0 3
1 1
1 2
1 1
0 1
1 1
```

### 样例输出 #2

```
3
```

## 提示

### 样例解释 1

Bessie 从坐标 $2$ 开始，这是一个数值为 $1$ 的炮击目标，所以她立刻击破了它。然后她弹跳至坐标 $3$，这是一个数值为 $2$ 的炮击目标，所以她无法击破它。她继续弹跳至坐标 $4$，这改变了她的方向并将她的能量增加了 $1$，达到 $2$。她跳回至坐标 $2$，这是一个已经被击破的炮击目标，所以她继续弹跳。此时，她弹跳至了坐标 $0$，因此她停了下来。她击破了恰好一个炮击目标，位于坐标 $2$。

### 样例解释 2

Bessie 经过的路径为 $4\to 5\to 3\to 1\to 6$，下一次弹跳将会使她离开数轴 $11$ 。她依次击破了炮击目标 $4,3,6$。

### 测试点性质

 - 测试点 $3-5$：N <= 100。
 - 测试点 $6-10$：N <= 1000。
 - 测试点 $11-20$：没有额外限制。

```
def cannonball_jump(num_positions, start_position, targets):
    energy = 1
    direction = 1
    broken_targets = 0
    has_broken = [False] * (num_positions + 1)
    last_energy = [0] * (num_positions + 1)
    last_direction = [0] * (num_positions + 1)

    current_position = start_position

    while 1 <= current_position <= num_positions:
        target_type, value = targets[current_position - 1]

        if target_type == 1:  # 炮击目标
            if not has_broken[current_position] and energy >= value:
                has_broken[current_position] = True
                last_energy[current_position] = energy
                last_direction[current_position] = direction
                broken_targets += 1
            elif last_energy[current_position] == energy and last_direction[current_position] == direction:
                break
        else:  # 跳板
            energy += value
            direction *= -1

        current_position += energy * direction

    return broken_targets

# 读取输入
num_positions, start_position = map(int, input().split())
targets = [tuple(map(int, input().split())) for _ in range(num_positions)]

# 调用函数并输出结果
print(cannonball_jump(num_positions, start_position, targets))
```
```
# 读取输入
n, s = map(int, input().split())

# 初始化变量
energy = 1
direction = 1
broken_targets = 0
visited = [False] * (n + 1)
targets = [tuple(map(int, input().split())) for _ in range(n)]

steps = 0
max_steps = 1145141

# 主要逻辑
while steps < max_steps:
    steps += 1
    target_type, value = targets[s - 1]

    if target_type == 1:  # 炮击目标
        if energy >= value and not visited[s]:
            broken_targets += 1
            visited[s] = True
    else:  # 跳板
        direction = -direction  # 反转方向
        energy += value

    s += direction * energy
    
    if s > n or s < 1:
        break  # 跳出数轴时退出

# 输出结果
print(broken_targets)
```
Answer by Ryan Wu
```
# 规则
# 0 = 跳板
# 1 = 目标

def listIntAAndB(a, b):
    c, d = input().split()
    a.append(int(c))
    b.append(int(d))
    return a, b

# input
N, S = input().split()
N = int(N)
S = int(S)
q = []
v = []
for i in range(N):
    q, v = listIntAAndB(q, v)
# print("N", N, "S", S, "q", q, "v", v)

num = 0
k = 1
pos = S
while 1 <= pos <= N:
    if q[pos - 1] == 0: # 跳板
        if k >= 0:
            k = -(k + v[pos - 1])
            pos += k
            # print(0.1, pos, k, num)
        elif k < 0:
            k = -(k - v[pos - 1])
            pos += k
            # print(0.2, pos, k, num)
    elif q[pos - 1] == 1: # 目标
        if (abs(k) >= v[pos - 1]) and (v[pos - 1] != 0): # 能击破
            v[pos - 1] = 0
            pos += k
            num += 1
            # print(1, pos, k, num)
        elif (abs(k) < v[pos - 1]) and (v[pos - 1] != 0): # 不能击破
            pos += k
            print(2, pos, k, num)
        elif v[pos - 1] == 0: # 跳板已击破
            pos += k
            # print(3, pos, k, num)

print(num)
```
Answer by Sally
```
N,S=input().split()
N=int(N)
S=int(S)
position=1 #1
energy=1
t=0#弹
p=1#炮击目标
c=1#顺时针
a=-1#逆时针
num_list=[]
for i in range(N):
    num_list.append(list(map(int,input().split())))
num_broken=0
now=S
visited=[False]*N
while 1 <= now <= N:#2
    op,energy_list=num_list[now-1]
    now_index= now-1
    if op==t: # 跳跳版
        energy += energy_list
        position*=-1 #
        now+=energy*position
    elif op==p:#炮击目标
        if energy_list <= energy and not visited[now_index]:#如果小于能量就被击破
            num_broken+=1 #击破是不是也要继续走
            visited[now_index] =True
        now+=position*energy
print(num_broken)
```
Answer by Ikun
```
def count_destroyed_targets(N,S,position):
    visited=set()
    energy=1
    destroyed_tragets=0
    direction=1
    current_pos=S
    
    while 1<= current_pos <=N :
        if (current_pos, energy, direction) in visited:  
            break  
        visited.add((current_pos, energy, direction))  
        q, v = position[current_pos - 1]
       
        if q==1 and energy>=v:
            destroyed_tragets+=1
        
        if q==0:
            energy+=v
            direction*=-1
        next_pos=current_pos+direction*energy 
        
        if next_pos<1 or next_pos>N:
            break
        current_pos=next_pos
    
    return destroyed_tragets

N,S=(map(int,input().split()))
position=[]
for _ in range(N):  
    q, v =map(int,input().split()) 
    position.append((q, v))  
print(count_destroyed_targets(N, S, position))
```
