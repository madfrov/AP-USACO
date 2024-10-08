# [USACO23Jan] Following Directions

原题链接: https://usaco.org/index.php?page=viewproblem2&cpid=1279

【题目描述】

Farmer John 有一个正方形的草地，草地被划分为了 (N+1)×(N+1)(1≤N≤1500) 的格子。设 (i,j) 为从上到下、从左到右第 i 行，第 j 列的格子。每个满足 1≤i,j≤n 的格子 (i,j) 之中都住着一头牛，而且每个这样的格子上都有一个路标指向右或下。除此之外，所有满足 i=N+1 或 j=N+1 的格子，除了 (N+1,N+1) 都会有一个饲料桶。牛在每个饲料桶进食需要的价格不同；位置 (i,j) 上的桶喂饱一只牛需要价格 ci,j(1≤ci,j≤500)。

每天晚饭时间，Farmer John 摇响晚餐铃时，所有牛都沿着路标的指向前进，直到它们遇到了饲料桶，之后它们会在它们自己遇到的饲料桶那里进食。第二天，所有牛又会回到自己原来的位置。

为了维持预算，Farmer John 想要知道每天喂食需要的价钱。然而，每天晚饭之前，总会有一头牛 (i,j) 翻转它那里的路标（原来向下则变成向右，反之亦然）。被翻转的路标指向将在后面的日子里保持不变，除非它又被进行了翻转。

给出每天被翻转的路标的坐标，请输出每天喂食需要的价格（总共有 Q 天，1≤Q≤1500）。

【输入】

第一行为 N(1≤N≤1500)

接下来的 N+1 行从上到下输入初始的路标朝向和每个饲料桶的价格 ci,j。前 N 行每行包含一个长度为 N 的字符串，其中每个字符只能是 R 或 D（R 表示向右，D 表示向下），之后是一个数，表示价格 ci,N+1，第 (N+1) 行包含 N 个数，依次表示价格 cN+1,j。

接下来的一行为 Q(1≤Q≤1500)。

之后的 Q 行，每行有两个整数 i 和 j(1≤i,j≤N)，表示每天被翻转的路标的坐标。


【输出】

共 *Q*+1 行：第一行是初始的总价格，之后 *Q* 行依次是每次被翻转后的总价格。

【输入样例】

```
2
RR 1
DD 10
100 500
4
1 1
1 1
1 1
2 1
```

【输出样例】

```
602
701
602
701
1501
```

在第一次翻转之前，(1,1)和(1,2)处的奶牛的饲养成本为 1，(2,1)处的奶牛的饲养成本为 100，(2,2)处的奶牛的饲养成本为 500。602 第一次翻转后，(1,1)处路标的方向由 R 变为 D，(1,1)处的奶牛现在需要花费 100 美元饲喂（其他路标保持不变），因此现在的总费用为 701 第二次和第三次翻转后，同一路标来回切换。第四次翻转后，(1,1)和(2,1)处的奶牛现在需要花费 500喂养，总成本为 1501.

Ans in c++ :
```
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

const int N = 1505;
long long n, ans, a[N][N], q, x, y;
char c[N][N];
bool cnt[N][N];

void dfs(long long x, long long y, long long sum)
{
	if(x == 0 || y == 0)
		return ;
	a[x][y] = sum;
	ans += sum;
	if(c[x-1][y] == 'D')
		dfs(x-1, y, sum);
	if(c[x][y-1] == 'R')
		dfs(x, y-1, sum);
	return ;
}

void dfs1(long long x, long long y, long long sum)
{
	if(x == 0 || y == 0)
		return ;
	ans -= a[x][y];
	a[x][y] = sum;
	ans += a[x][y];
	if(c[x-1][y] == 'D')
		dfs1(x-1, y, sum);
	if(c[x][y-1] == 'R')
		dfs1(x, y-1, sum);
	return ;
}

int main(int argc, char** argv)
{
	scanf("%d", &n);
	for(int i = 1;i <= n;i++)
	{
		for(int j = 1;j <= n;j++)
			cin >> c[i][j];
		scanf("%d", &a[i][n+1]);
	}
	for(int i = 1;i <= n;i++)
		scanf("%d", &a[n+1][i]);
	for(int i = 1;i <= n;i++)
	{
		if(c[i][n] == 'R')
			dfs(i, n, a[i][n + 1]);
		if(c[n][i] == 'D')
			dfs(n, i, a[n + 1][i]);
	}
	printf("%d\n", ans);
	cin >> q;
	while(q--)
	{
		cin >> x >> y;
		if(c[x][y] == 'R')
		{
			c[x][y] = 'D';
			ans -= a[x][y];
			a[x][y] = a[x+1][y];
			ans += a[x][y];
			dfs1(x, y, a[x][y]);
		}
		else
		{
			c[x][y] = 'R';
			ans -= a[x][y];
			a[x][y] = a[x][y+1];
			ans += a[x][y];
			dfs1(x, y, a[x][y]);
		}
		cout << ans << endl;
	}
	return 0;
}
```
