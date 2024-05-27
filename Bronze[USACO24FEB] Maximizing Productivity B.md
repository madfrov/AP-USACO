# [USACO24FEB] Maximizing Productivity B

## 题目描述

Farmer John 有 N（1<=N<=2*10^5）个农场，编号为 1 到 N。已知 FJ 会在时刻 c_i 关闭农场 i。Bessie 在时刻 S 起床，她希望在农场关闭前访问尽可能多的农场，从而最大限度地提高她这一天的生产力。她计划在时刻 t_i+S 访问农场 i。Bessie 必须于严格早于 Farmer John 关闭农场的时刻抵达农场才能成功进行访问。

Bessie 有  Q（1<= Q<=2*10^5）个询问。对于每个询问，她会给你两个整数 S 和 V。对于每个询问，输出当 Bessie 在时刻 S 起床是否可以访问至少 V 个农场。

## 输入格式

输入的第一行包含 N 和 Q。

第二行包含 c_1,c_2,c_3\ldots c_N（1<=c_i<=10^6）。

第三行包含 t_1,t_2,t_3\ldots t_N（1<=t_i<=10^6）。

以下 $Q$ 行，每行包含两个整数 V（1<=V<=N）和 S（1<=S<=10^6）。

## 输出格式

对 Q 个询问的每一个输出一行，输出 `YES`（是）或 `NO`（否）。

## 样例 #1

### 样例输入 #1

```
5 5
3 5 7 9 12
4 2 3 3 8
1 5
1 6
3 3
4 2
5 1
```

### 样例输出 #1

```
YES
NO
YES
YES
NO
```

## 提示

### 样例解释

对于第一个询问，Bessie 将在时间 t=[9,7,8,8,13]访问农场， 因此她在 FJ 关闭农场之前能准时访问到的只有农场 4。

对于第二个询问，Bessie 将无法准时访问到任何农场。

对于第三个询问，Bessie 将可以准时访问到农场 3,4,5。

对于第四个和第五个询问，Bessie 将能够准时访问除第一个农场之外的所有农场。

### 测试点性质

- 测试点 2-4：N,Q\le 10^3。
- 测试点 5-9：c_i,t_i\le 20。
- 测试点 10-17：没有额外限制。

```
n, q = map(int, input().split())
c = list(map(int, input().split()))
t = list(map(int, input().split()))
late = [c[i] - t[i] for i in range(n)]
late.sort(reverse=True)

for i in range(q):
    v, s = map(int, input().split())
    if s < late[v-1]:
        print("YES")
    else:
        print("NO")
```
