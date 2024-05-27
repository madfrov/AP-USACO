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


Answers 1:
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
Answers 2 by G2-5 Kelly Chen
```
t1=input().split()
t2=input().split()
t3=input().split()
for i in range(100):

    if i%3==0:
        cb=int(t2[0])
        cbi=int(t2[1])
        cai=int(t1[1])
        mi=min(cb-cbi,cai)
        mb=cbi+mi
        ma=cai-mi
        t2[1]=mb
        t1[1]=ma

    elif i%3==1:#2-3
        cb = int(t3[0])
        cbi = int(t3[1])
        cai = int(t2[1])
        mi = min(cb - cbi, cai)
        mb = cbi + mi
        ma = cai - mi
        t2[1] = ma
        t3[1] = mb

    elif i%3==2:
        cb = int(t1[0])
        cbi = int(t1[1])
        cai = int(t3[1])
        mi = min(cb - cbi, cai)
        mb = cbi + mi
        ma = cai - mi
        t3[1] = ma
        t1[1] = mb


print(t1[1],t2[1],t3[1])

```
Answers 3 by G1-2 Sally Fu
```
capA,A = input().split()
capB,B = input().split()
capC,C = input().split()
capA=int(capA)
capB=int(capB)
capC=int(capC)
A =int(A)
B =int(B)
C =int(C)
for i in range(100):
    if i%3==0:
        if (A+B) <=capB:
            B+=A
            A=0
        elif (A+B) >capB:
            A = (A+B)-capB
            B = capB
    if i%3==1:
        if (B+C) <=capC:
            C+=B
            B=0
        elif (B+C) >capC:
            B = (B+C)-capC
            C = capC
    if i%3==2:
        if (A+C) <=capA:
            A+=C
            C=0
        elif (C+A) >capA:
            C = (C+A)-capA
            A = capA
print(A,B,C)
```
```
#include <stdio.h>
int c[4], m[4];
void move(int x, int y) {
    if (m[y] - c[y] >= c[x]) {
            c[y] += c[x];
            c[x] = 0;
          } else {
            c[x] -= m[y] - c[y];
            c[y] = m[y];
        }
}
int main() {
    scanf("%d%d%d%d%d%d", &m[1], &c[1], &m[2], &c[2], &m[3], &c[3]);
    for (int i = 1; i <= 33; ++ i) {
        move(1, 2);
        move(2, 3);
        move(3, 1);
    }
    move(1, 2);
    printf("%d\n%d\n%d", c[1], c[2], c[3]);
}

```
