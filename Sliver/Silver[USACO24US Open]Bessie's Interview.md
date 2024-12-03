# [USACO24US Open] Bessie's Interview
原题link: https://usaco.org/index.php?page=viewproblem2&cpid=1422

洛谷链接:https://www.luogu.com.cn/problem/P10277

## 题目描述

Bessie 正在寻找新工作！幸运的是，K* 名农夫目前正在招聘并举行面试。由于工作竞争激烈，农夫们决定按申请的顺序对奶牛进行编号和面试。有 N* 头奶牛在 Bessie 之前申请，因此她的编号为N*+1（1≤K≤N≤3⋅105）。

面试过程如下。在时刻 0，对于每一个 1≤i≤K，农夫 *i* 将开始面试奶牛 i*。一旦一名农夫完成面试，他将立刻开始面试队列中的下一头奶牛。如果多名农夫同时完成，下一头奶牛可以根据自己的偏好选择接受任一此时空闲的农夫的面试。

对于每一个 1≤i≤N，Bessie 已经知道奶牛 *i* 的面试将恰好花费 t**i 分钟（1≤ti≤109）。然而，她不知道每头奶牛对农夫的偏好。

由于这份工作对 Bessie 来说非常重要，所以她想要认真准备面试。为此，她需要知道她会在何时接受面试，以及哪些农夫可能会面试她。帮助她求出这些信息！

## 输入格式

输入的第一行包含两个整数 N 和 K。

第二行包含 N* 个整数 t1…tN。

## 输出格式

输出的第一行包含 Bessie 的面试将开始的时刻。

第二行包含一个长为 *K* 的 `01` 字符串，其中如果农夫 i 可能面试 Bessie 则第 i 个字符为 `1`，否则为 `0`。

## 输入输出样例

**输入 #1**复制

```
6 3
3 1 4159 2 6 5
```

**输出 #1**复制

```
8
110
```

## 说明/提示

### 样例解释 1

除了 Bessie 之外有 6 头奶牛，以及 3 名农夫。面试过程将如下进行：

1. 于时刻 t=0，农夫 1 面试奶牛 1，农夫 2 面试奶牛 2，农夫 3 面试奶牛 3。

2. 于时刻 t=1，农夫 2 结束了对奶牛 2 的面试并开始面试奶牛 4。

3. 于时刻 t=3, 农夫 1 和农夫 2 都完成了面试，从而有两种可能：

    

   - 农夫 1 面试奶牛 5，农夫 2面试奶牛 6。在这种情况下，农夫 2 将于时刻 t=8完成面试并开始面试 Bessie。
   - 农夫 1 面试奶牛 6，农夫 2 面试奶牛 5。在这种情况下，农夫 1 将于时刻 t=8完成面试并开始面试 Bessie。

从而，Bessie 的面试将于时刻 *t*=8 开始，并且她可能会被农夫 1 或农夫 2 面试。

### 测试点性质

- 测试点 2−3：没有两名农夫同时完成面试。
- 测试点 4−9：N≤3⋅103。
- 测试点 10−21：没有额外限制。


python solution
```
import heapq

N, K = map(int, input().split())

T = list(map(int, input().split()))
times = [0] * K

edges_into = dict()

for t in T:
    start = heapq.heappop(times)
    end = start + t
    edges_into.setdefault(end, []).append(start)
    heapq.heappush(times, end)

q = [heapq.heappop(times)]
vis = set()
for x in q:
    if x in vis:
        continue
    vis.add(x)
    if x not in edges_into:
        continue
    for prv in edges_into[x]:
        q.append(prv)

print(q[0])
print("".join(["1" if t in vis else "0" for t in T[:K]]))
```
