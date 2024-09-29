# [USACO23FEB] Cow-libi

原题链接: https://usaco.org/index.php?page=viewproblem2&cpid=1303

【题目描述】

有 g 处抓获，第 i 处抓获如 (xi,yi,ti)(−10^9≤xi,yi≤10^9,0≤ti≤10^9)，表示 ti 时刻 (xi,yi) 有一处抓获，FJ 抓到了 n 头嫌疑奶牛，每头奶牛都提供了如 (xj,yj,tj) 的证词，表示它 tj 时刻在 (xj,yj)，一头奶牛一个单位时间可以移动一个单位距离，奶牛可以洗脱自己的清白，当且仅当它没有足够的时间作出所有的抓获，即，只要它没有足够的时间从它提供的证词的时刻到达随便一个抓获处，它就是清白的。

问有多少奶牛是清白的？

【输入】

第一行输入 g,n。

接下来 g 行每行三个整数 xi,yi,ti 表示一处抓获。

接下来 n 行每行三个整数 xj,yj,tj 表示一个证词。

【输出】

一行一个整数表示清白的牛的个数。

【输入样例】

```
2 4
0 0 100
50 0 200
0 50 50
1000 1000 0
50 0 200
10 0 170
```

【输出样例】

```
2
```

有两个放牧点，第一个在（0,0），时间 100 第二个在（50,0，时间为 200

There were two grazings; the first at (0,0) at time 100 and the second at (50,0) at time 200

The first cow's alibi does not prove her innocence. She has just enough time to arrive at the first grazing.

The second cow's alibi does prove her innocence. She is nowhere near any of the grazings.

Unfortunately for the third cow, being at the scene of the crime does not prove innocence.

Finally, the fourth cow is innocent because it's impossible to make it from her alibi to the final grazing in time.

![img1](https://github.com/madfrov/AP-USACO/blob/main/Sliver/Scoreing1.jpg)

Ans in Python
```
def main():
    G, n = map(int, input().split())
    
    # 存储吃草点的信息
    grass_points = []
    for _ in range(G):
        x, y, t = map(int, input().split())
        grass_points.append((x, y, t))
    
    # 按时间排序吃草点
    grass_points.sort(key=lambda p: p[2])
    
    ans = 0
    for _ in range(n):
        cowx, cowy, cowt = map(int, input().split())
        
        # 处理特殊情况
        if cowt < grass_points[0][2]:
            if (grass_points[0][0] - cowx)**2 + (grass_points[0][1] - cowy)**2 > (grass_points[0][2] - cowt)**2:
                ans += 1
            continue
        
        if cowt > grass_points[-1][2]:
            if (grass_points[-1][0] - cowx)**2 + (grass_points[-1][1] - cowy)**2 > (grass_points[-1][2] - cowt)**2:
                ans += 1
            continue
        
        # 二分查找
        left, right = 0, G - 1
        while left <= right:
            mid = (left + right) // 2
            if grass_points[mid][2] < cowt:
                res = mid
                left = mid + 1
            else:
                right = mid - 1
        
        # 检查是否可以到达相邻的两个点
        innocent = False
        for i in [res, res + 1]:
            if i < G and (grass_points[i][0] - cowx)**2 + (grass_points[i][1] - cowy)**2 > (grass_points[i][2] - cowt)**2:
                innocent = True
                break
        
        if innocent:
            ans += 1
    
    print(ans)

if __name__ == "__main__":
    main()
```
Ans in C++
```
#include <bits/stdc++.h>
using namespace std;
#define int long long  // 因为题目中计算后会超int，所以全部修改为long long
int G, n, ans;
struct node {
    int x, y, t;
    bool operator < (node other) {  // 后面用到sor排序，重载"<"
        return t < other.t;
    }
}g[100005];
signed main()  // 前面有define，所以这里改为signed
{
    cin >> G >> n;  // 输入G和n
    for (int i=1; i<=G; i++) {  // 输入G个吃草的点
        cin >> g[i].x >> g[i].y >> g[i].t;
    }
    sort(g+1, g+G+1);  // 所有的点按照从小到大排序
    int cowx, cowy, cowt;
    for (int i=1; i<=n; i++) {  // 输入每只奶牛的证词
        cin >> cowx >> cowy >> cowt;
        int res=0;  // 定义二分答案
        if (cowt<g[1].t) {  // 如果cowt时刻小于g[1].t
            if ((g[1].x-cowx)*(g[1].x-cowx)+(g[1].y-cowy)*(g[1].y-cowy) > (g[1].t-cowt)*(g[1].t-cowt)) {  // 如果它没有足够的时间到达g[1]
                ans++;  // 就是无辜的
            }
        } else if (cowt>g[G].t) {  // 如果cowt的时刻大于g[G].t
            if ((g[G].x-cowx)*(g[G].x-cowx)+(g[G].y-cowy)*(g[G].y-cowy) > (g[G].t-cowt)*(g[G].t-cowt)) {  // 如果它没有足够的时间到达g[G]
                ans++;  // 也是无辜的
            }
        } else {
            int l = 1, r = G;
            while (l<=r) {  // 二分答案模板
                int mid = (l+r)/2;
                if (g[mid].t<cowt) {  // g[mid].t小于cowt时（其他模板代码固定，可以开调试观察这里的结果）
                    res = mid;  // 就更新res
                    l = mid+1;  // 然后增加l，找到最大的l
                } else {  // 否则
                    r = mid-1;  // 减少r
                }
            }
            bool innocent = false;  // 定义标记位
            if ((g[res].x-cowx)*(g[res].x-cowx) + (g[res].y-cowy)*(g[res].y-cowy) > (g[res].t-cowt)*(g[res].t-cowt)) {  // 如果无法到res这个点
                    innocent = true;  // 修改标记位
            }
            if ((g[res+1].x-cowx)*(g[res+1].x-cowx) + (g[res+1].y-cowy)*(g[res+1].y-cowy) > (g[res+1].t-cowt)*(g[res+1].t-cowt)) {  // 如果无法到res+1这个点
                innocent = true;  // 修改标记位
            }
            ans += innocent;  // 只要有一个吃草点无法到达，就是无辜的
        }
    }
    cout << ans << endl;  // 输出无辜的奶牛数量
    return 0;
}
```
Ans 2 in c++
```
#include <bits/stdc++.h>
#define int long long
using namespace std;

int n,m,cnt;

struct nod{
	int x,y,t;
}nn[100010],mm[100010];

//两分查找，返回右端点 
int two_search(int t){
	int head=0,tail=n+1;
	while(head + 1 < tail){
		int mid=(head+tail)/2;
		if(nn[mid].t>t)tail=mid;
		else head = mid;
	}
	return tail;
}

//返回true表示不能作案 
bool ispos(int pos,int i){
	if((nn[pos].t-mm[i].t)*(nn[pos].t-mm[i].t)<(nn[pos].x-mm[i].x)*(nn[pos].x-mm[i].x)+(nn[pos].y-mm[i].y)*(nn[pos].y-mm[i].y))return true;
	else return false;
}
//返回值为true是能作案 
bool check(int pos,int i){
	//检测pos, pos - 1
	int pos1=pos-1,pos2=pos;
	if (pos2 != n + 1 && ispos(pos2, i)) return false;
	if (pos1 != 0 && ispos(pos1, i)) return false;
	return true;
}

bool cmp(nod q,nod p){
	return q.t<p.t;
}

signed main(){
	scanf("%lld%lld",&n,&m);
	for(int i=1;i<=n;++i)
		scanf("%lld%lld%lld",&nn[i].x,&nn[i].y,&nn[i].t);
	for(int i=1;i<=m;++i)
		scanf("%lld%lld%lld",&mm[i].x,&mm[i].y,&mm[i].t);
	sort(nn+1,nn+1+n,cmp);
	for(int i=1;i<=m;++i){
		int pos=two_search(mm[i].t);
		if(!check(pos,i))++cnt;
	}
	cout<<cnt<<endl;
	return 0;
}
```
