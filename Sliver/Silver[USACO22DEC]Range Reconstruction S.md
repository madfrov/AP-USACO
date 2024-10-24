# [USACO22DEC] Range Reconstruction S
原题link: https://usaco.org/index.php?page=viewproblem2&cpid=1256

洛谷链接:https://www.luogu.com.cn/problem/P8902

# [USACO22DEC] Range Reconstruction S

## 题目描述

Bessie 有一个数组 a1,⋯,aN*，其中 1≤N≤300 并对于所有 i有 0 ≤ ai ≤ 10**9 。她不会告诉你数组 a本身，但她会告诉你 a的每个子数组的全距。也就是说，对于每对索引 i≤j*，Bessie 告诉你 ri,j=max⁡ a[i⋯j]−min⁡ a[i⋯j]。给定这些 r 的值，构造一个可以作为 Bessie 的原始数组的数组。你的数组中的数值应在[−10^9,10^9]范围内。

## 输入格式

输入的第一行包含 N。

以下 N行，第 i*i* 行包含整数 ri,i,ri,i+1,⋯ ,ri,*N*。

输入保证存在某个数组 *a*，其中的数值在[0,10^9]范围内，满足对于所有的i*≤*j*，有 ri,j=max⁡ a[i⋯j]−min⁡a[i⋯j]*。

## 输出格式

输出一行，包含 N个整数 b1,b2,⋯,bN，在 [−10^9,10^9]范围内，表示你的数组。这些数需要满足对于所有的 i≤j有 ri,j=max⁡a[i⋯j]−min⁡a[i⋯j]。

## 样例 #1

### 样例输入 #1

```
3
0 2 2
0 1
0
```

### 样例输出 #1

```
1 3 2
```

## 样例 #2

### 样例输入 #2

```
3
0 1 1
0 0
0
```

### 样例输出 #2

```
0 1 1
```

## 样例 #3

### 样例输入 #3

```
4
0 1 2 2
0 1 1
0 1
0
```

### 样例输出 #3

```
1 2 3 2
```

## 样例 #4

### 样例输入 #4

```
4
0 1 1 2
0 0 2
0 2
0
```

### 样例输出 #4

```
1 2 2 0
```

## 说明/提示

### 样例 1 解释

例如，r1,3=max⁡a[1⋯3]−min⁡a[1⋯3]=3−1=2。

### 样例 2 解释

这个样例满足子任务 1 的限制。

### 样例 3 解释

这个样例满足子任务 2 的限制。

### 测试点性质

- 测试点 55 满足 r1,N<=1。
- 测试点 6−8 满足对于所有 1≤i*<*N* 均有 ri,i+1=1。
- 测试点 9−14没有额外限制。

```
maxN = 310
a = [[0] * maxN for _ in range(maxN)]  # 初始化一个二维数组a，用于存储输入的数
ans = [0] * maxN  # 初始化数组ans，存储计算结果

def main():
    n = int(input())  # 输入n，表示矩阵的大小
    for i in range(1, n + 1):
        values = list(map(int, input().split()))  # 输入第i行的数，并转换为整数列表
        for j, value in enumerate(values, start=i):  # 从第i列开始填入数据
            a[i][j] = value
    
    ans[1] = 0  # 初始化第一个结果为0
    ans[2] = ans[1] + a[1][2]  # 计算第二个结果
    last = 2  # 初始化last为2，表示上一个已计算的索引

    # 从第3个元素开始遍历到第n个元素
    for i in range(3, n + 1):
        if a[last-1][i] == a[last-1][last] + a[last][i]:  # 检查是否满足某个条件
            if ans[last] > ans[last-1]:
                ans[i] = ans[last] + a[last][i]  # 根据条件更新ans[i]
            else:
                ans[i] = ans[last] - a[last][i]
        elif a[last-1][i] < a[last-1][last] + a[last][i]:  # 检查另一个条件
            if ans[last] > ans[last-1]:
                ans[i] = ans[last] - a[last][i]
            else:
                ans[i] = ans[last] + a[last][i]
        if a[i-1][i] != 0:  # 如果a[i-1][i]不是0，更新last
            last = i

    for i in range(1, n + 1):  # 输出结果数组
        print(ans[i], end=" ")
    print()

if __name__ == "__main__":
    main()
```
By Apg2-1张皓然
```
#include<bits/stdc++.h>
using namespace std;
int n,m,weight;
int const N=3e2+10;
int a[N][N]; 
int dp[N];
bool check(int ind)
{
	
	int ma,mi;
	for(int i=1;i<=ind;i++)
	{
		ma=dp[i];
		mi=dp[i];
		for(int j=i;j<=ind;j++)
		{
			ma=max(dp[j],ma);
			mi=min(dp[j],mi);
		}
		if(a[i][ind]!=ma-mi)
		{
			return false;
		}
	}
	return true;
}
int main()                           
{
	cin>>n;
	dp[0]=0;//初始化为0，随便设定的 
	for(int i=1;i<=n;i++)
	{
		for(int j=i;j<=n;j++)
		{
			
			cin>>a[i][j];
		}
	}
	for(int i=2;i<=n;i++)
	{
		dp[i]=dp[i-1]+a[i-1][i];
	
		if(check(i))
		{
			continue;
		}
		else
		{
			dp[i]=dp[i-1]-a[i-1][i];
		}
		
	}
	for(int i=1;i<=n;i++)
	{
		cout<<dp[i]<<" ";
	}
	return 0;
}
```
