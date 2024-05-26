# [USACO18DEC] Mixing Milk B

## 题目描述

农业，尤其是生产牛奶，是一个竞争激烈的行业。Farmer John 发现如果他不在牛奶生产工艺上有所创新，他的乳制品生意可能就会受到重创！

幸运的是，Farmer John 想出了一个好主意。他的三头获奖的乳牛，Bessie、Elsie 和 Mildred，各自产奶的口味有些许不同，他打算混合这三种牛奶调制出完美的口味。

为了混合这三种不同的牛奶，他拿来三个桶，其中分别装有三头奶牛所产的奶。这些桶可能有不同的容积，也可能并没有完全装满。然后他将桶 $1$ 的牛奶倒入桶 $2$，然后将桶 $2$ 中的牛奶倒入桶 $3$，然后将桶 $3$ 中的牛奶倒入桶 $1$，然后再将桶 $1$ 的牛奶倒入桶 $2$，如此周期性地操作，共计进行 $100$ 次（所以第 $100$ 次操作会是桶 $1$ 倒入桶 $2$）。当 Farmer John 将桶 $a$ 中的牛奶倒入桶 $b$ 时，他会倒出尽可能多的牛奶，直到桶 $a$ 被倒空或是桶 $b$ 被倒满。

请告诉 Farmer John 当他倒了 $100$ 次之后每个桶里将会有多少牛奶。

## 输入格式

输入文件的第一行包含两个空格分隔的整数：第一个桶的容积 $c_1$，以及第一个桶里的牛奶量 $m_1$。$c_1$ 和 $m_1$ 均为正，并且不超过 $10^9$。第二和第三行类似地包含第二和第三个桶地容积和牛奶量。

## 输出格式

输出三行，给出倒了 $100$ 次之后每个桶里的牛奶量。

## 样例 #1

### 样例输入 #1

```
10 3
11 4
12 5
```

### 样例输出 #1

```
0
10
2
```

## 提示

在这个例子中，每倒一次之后每个桶里的牛奶量如下：

0. 初始状态：3  4  5
1. 桶1->2：0  7  5
2. 桶2->3：0  0  12
3. 桶3->1：10 0  2
4. 桶1->2：0  10 2
5. 桶2->3：0  0  12

（之后最后三个状态循环出现……）

```
c = [0] * 4
m = [0] * 4

for x in range(1, 4):
    c[x], m[x] = map(int, input().split())

for x in range(1, 101):
    f = (x - 1) % 3 + 1
    if f == 3:
        s = 1
    else:
        s = f + 1
    mi = min(c[s] - m[s], m[f])
    m[f] -= mi
    m[s] += mi

print(m[1])
print(m[2])
print(m[3])
```



# [USACO16FEB] Circular Barn S

## 题目背景

*本题与 [金组同名题目](/problem/P6170) 在题意上一致，唯一的差别是数据范围。*

## 题目描述

作为当代建筑的爱好者，Farmer John 建造了一个圆形新谷仓，谷仓内部 n 个房间排成环形（3 <= n \<= 1000），按顺时针顺序编号为 1.....n，每个房间都有通往与其相邻的左右房间的门，还有一扇门通往外面。

现在 FJ 有 n 头奶牛，他的目标是让每个房间恰好有一头奶牛。然而不幸的是，现在奶牛们随意呆在某个房间里，第 i 个房间里有 c_i 头奶牛。保证 Sum c_i =n。

FJ 决定采用这样的方法来解决这个问题：让某些奶牛**顺时针**穿过某些房间到达指定的位置。如果一头奶牛穿过了 d扇门，他消耗的能量为 d^2。你需要帮 FJ 算出所有奶牛消耗的能量和最小值是多少。

## 输入格式

第一行一个整数 n，接下来 n 行，第 i 行一个整数 c_i。

## 输出格式

输出所有奶牛最小消耗能量和。

## 样例 #1

### 样例输入 #1

```
10
1
0
0
2
0
0
1
2
2
2
```

### 样例输出 #1

```
33
```

```
n = int(input())
a = []
cnt = 0
maxx = -float('inf')
p = 0
ans = 0

for _ in range(n):
    x = int(input())
    while x:
        a.append(cnt)
        x -= 1
    cnt += 1

b = [a[i] - i for i in range(n)]

for i in range(n):
    if b[i] > maxx:
        maxx = b[i]
        p = i

c = [0] * n
c[p] = a[p]

for i in range(p-1, -1, -1):
    c[i] = (c[i+1] - 1) % n

for i in range(p+1, n):
    c[i] = (c[i-1] + 1) % n

for i in range(n):
    if c[i] < a[i]:
        c[i] += n
    ans += (c[i] - a[i]) ** 2

print(ans)

```

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

```
n, m = map(int, input().split())
s = input()
s = s[n-1] + s

a = []
sum = 0

for i in range(n):
    a.append(int(input()))
    sum += a[i]

ans = 0

for i in range(n+1):
    if s[i] == 'R' and s[i+1] == 'L':
        l = 0
        r = 0
        lpos = i - 1 if i - 1 >= 0 else i - 1 + n
        rpos = i + 2 if i + 2 <= n else i + 2 - n
        while s[lpos] == 'R':
            l += a[lpos]
            lpos -= 1
            if lpos < 0:
                lpos += n
        while s[rpos] == 'L':
            r += a[rpos]
            rpos += 1
            if rpos > n:
                rpos -= n
        ans += min(m, l) + min(m, r)

print(sum - ans)
```

