# [USACO19Jan]  Grass Planting
原题link: https://usaco.org/index.php?page=viewproblem2&cpid=894&lang=zh

洛谷链接:https://www.luogu.com.cn/problem/P5197

到了一年中Farmer John在他的草地里种草的时间了。整个农场由N块草地组成（1≤N≤10^5），方便起见编号为1…N，由N−1条双向的小路连接，每块草地都可以经过一些小路到达其他所有的草地。 Farmer John当然可以在每块草地里种不同种类的草，但是他想要使得使用的草的种类数最小，因为他用的草的种类数越多，他就需要负担更高的花费。

不幸的是，他的奶牛们对选择农场上的草表现得十分苛刻。如果两块相邻（由一条小路直接相连）的草地种了同一种草，或者即使是两块接近相邻（均可由一条小路直接连向同一块草地）的草地，那么奶牛们就会抱怨她们进餐的选择不够多样。Farmer John能做的只能是抱怨这些奶牛，因为他知道她们不能被满足的时候会制造多大的麻烦。

请帮助Farmer John求出他的整个农场所需要的最少的草的种类数。

## 输入格式

输入的第一行包含N。以下N−1行每行描述了一条小路连接的两块草地。

## 输出格式

输出Farmer John需要使用的最少的草的种类数

## 输入输出样例

**输入 #1**复制

```
4
1 2
4 3
2 3
```

**输出 #1**复制

```
3
```

## 说明/提示

在这个简单的例子中，4块草地以一条直线的形式相连。最少需要三种草。例如，Farmer John可以用草A，B和C将草地按A - B - C - A的方式播种。

```
def add(u, v, lst, nxt, to, d):
    global tot
    tot += 1
    to[tot] = v
    d[v] += 1  # Increment the in-degree
    nxt[tot] = lst[u]
    lst[u] = tot

def main():
    import sys
    input = sys.stdin.readline

    n = int(input().strip())
    global tot
    tot = 0

    mxn = 100005
    lst = [0] * mxn
    nxt = [0] * (mxn * 2)
    to = [0] * (mxn * 2)
    d = [0] * mxn

    for _ in range(n - 1):
        a, b = map(int, input().strip().split())
        add(a, b, lst, nxt, to, d)
        add(b, a, lst, nxt, to, d)

    ans = 0
    for i in range(1, n + 1):
        ans = max(ans, d[i] + 1)

    print(ans)

if __name__ == "__main__":
    main()
```
