# [USACO24FEB] Maximizing Productivity B

## 题目描述

Farmer John 有 N（1<=N<=2*10^5）个农场，编号为 1 到 N。已知 FJ 会在时刻 c_i 关闭农场 i。Bessie 在时刻 S 起床，她希望在农场关闭前访问尽可能多的农场，从而最大限度地提高她这一天的生产力。她计划在时刻 t_i+S 访问农场 i。Bessie 必须于严格早于 Farmer John 关闭农场的时刻抵达农场才能成功进行访问。

Bessie 有  Q（1<= Q<=2*10^5）个询问。对于每个询问，她会给你两个整数 S 和 V。对于每个询问，输出当 Bessie 在时刻 S 起床是否可以访问至少 V 个农场。

## 输入格式

输入的第一行包含 N 和 Q。

第二行包含 c_1,c_2,c_3....c_N（1<=c_i<=10^6）。

第三行包含 t_1,t_2,t_3....t_N（1<=t_i<=10^6）。

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

- 测试点 2-4：N,Q <= 10^3。
- 测试点 5-9：c_i,t_i <= 20。
- 测试点 10-17：没有额外限制。
- # [USACO24JAN] Majority Opinion B

  ## 题目描述

<<<<<<< HEAD
  Farmer John 有一项重要的任务——弄清楚要为他的奶牛们购买什么类型的干草。

  Farmer John 的 $N$ 头奶牛（$2\le N\le 10^5$）编号为 $1$ 到 $N$，每头奶牛喜欢恰好一种类型的干草 $h_i$（$1\le h_i\le N$）。他希望他的所有奶牛都喜欢同一种干草。

  为了实现这一目标，Farmer John 可以主持焦点小组访谈。一次焦点小组访谈为让编号从 $i$ 到 $j$ 的连续范围内的所有奶牛聚集在一起参加一次访谈。如果有一种干草是小组中超过一半的奶牛喜欢的，则此次焦点小组访谈结束后，所有奶牛最终都会喜欢这种干草。如果不存在这种类型的干草，那么奶牛们不会改变她们喜欢的干草类型。例如，在由 $16$ 头奶牛组成的焦点小组访谈中，需要有其中 $9$ 头或更多的奶牛具有相同的干草喜好，才能使其余奶牛改变其喜好以与之一致。

  Farmer John 想知道哪些类型的干草有可能变为同时受到所有奶牛的喜爱。他一次只能主持一个焦点小组访谈，但为了使所有奶牛都喜欢同一类型的干草，他可以根据需要任意多次地主持焦点小组访谈。

  ## 输入格式

  输入的第一行包含一个整数 $T$，为独立的测试用例的数量（$1\le T\le 10$）。

  每一个测试用例的第一行包含 $N$。

  第二行包含 $N$ 个整数，为奶牛们喜爱的干草类型 $h_i$。

  输入保证所有测试用例的 $N$ 之和不超过 $2\cdot 10^5$。

  ## 输出格式

  输出 $T$ 行，对于每个测试用例输出一行。

  如果可能使所有奶牛同时喜欢同一种干草，则以升序输出所有可能的此类干草的类型，否则输出 $-1$。在同一行内输出一列整数时，相邻的数用空格分隔，并确保行末没有多余空格。

  ## 样例 #1

  ### 样例输入 #1

  ```
  5
  5
  1 2 2 2 3
  6
  1 2 3 1 2 3
  6
  1 1 1 2 2 2
  3
  3 2 3
  2
  2 1
  ```

  ### 样例输出 #1

  ```
  2
  -1
  1 2
  3
  -1
  ```

  ## 提示

  ### 样例解释

  在输入样例中，有 5 个测试用例。

  在第一个测试用例中，仅可能使所有奶牛喜欢种类 $2$。FJ 可以通过主持一次所有奶牛的焦点小组访谈达到这一目的。

  在第二个测试用例中，可以证明没有奶牛会改变她们喜爱的干草种类。

  在第三个测试用例中，有可能使所有奶牛喜欢种类 $1$，可以通过主持三次焦点小组访谈达到这一目的——首先使奶牛 $1$ 到 $4$ 进行一次焦点小组访谈，随后使奶牛 $1$ 到 $5$ 进行一次焦点小组访谈，随后使奶牛 $1$ 到 $6$ 进行一次焦点小组访谈。以类似的逻辑，依次操作奶牛 $3$ 到 $6$，随后是奶牛 $2$ 到 $6$，随后是奶牛 $1$ 到 $6$，我们可以使所有奶牛喜欢种类 $2$。

  在第四个测试用例中，有可能使所有奶牛喜欢种类 $3$，可以通过主持一次所有奶牛的焦点小组访谈达到这一目的。

  在第五个测试用例中，可以证明没有奶牛会改变她们喜爱的干草种类。

  ### 测试点性质

  - 测试点 $2$：$N=2$。
  - 测试点 $3-4$：$N\le 50$。
  - 测试点 $5-6$：对于所有的 $1\le i\le N−1$，有 $h_i\le h_i+1$。
  - 测试点 $7-15$：没有额外限制。
=======
for i in range(q):
    v, s = map(int, input().split())
    if s < late[v-1]:
        print("YES")
    else:
        print("NO")
```
Answer by Matthew Xie in C++
```
#include <stdio.h>
int n, q, c[200001], t[200001], sum;
int s, v;
int main () {
    scanf("%d %d", &n, &q);
    for (int i = 1;i <= n; ++ i) {
        scanf("%d", &c[i]);
    }
    for (int i = 1;i <= n; ++ i) {
        scanf("%d", &t[i]);
    }
    while (q --) {
        scanf("%d %d", &s, &v);
        sum = 0;
        for (int i = 1; i <= n; ++ i) {
            if (t[i] + s < c[i]) {
                sum ++;
            }
        }
        if (sum >= v) {
            printf("YES\n");
        } else {
            printf("NO\n");
        }
    }
    
}
```
Answer made by Justin.Lee
```
N,Q=[int(i) for i in input().split()]
close_time=[int(i) for i in input().split()]
open_time=[int(i) for i in input().split()]
difference=sorted([int(close_time[i]-open_time[i])for i in range(len(close_time))],reverse=True)
y_n=''
for i in range(Q):
    S,V=[int(i)for i in input().split()]
    if difference[S-1]>V:
        y_n+=('YES\n')
    else:
        y_n+=('NO\n')
print(y_n)

```
Answer by IKun Chen
```
N, Q = map(int, input().split())  
c = list(map(int, input().split()))  
t = list(map(int, input().split()))  
  
windows = [(c[i] - t[i], i) for i in range(N)]   
  
windows.sort(reverse=True)  
  
for _ in range(Q):  
    V, S = map(int, input().split())  
    count = 0   
    total_time = 0  
    for window, _ in windows:  
        if total_time + window <= S:  
            total_time += window  
            count += 1  
            if count >= V:  
                print("YES")  
                break  
    else:  
        print("NO")
```
Answers by James Liu
```
N=int(input())
Q=int(input())
c=list(map(int,input().split()))
g=list(map(int,input().split()))
V=list(map(int,input().split()))
S=list(map(int,input().split()))
a=[]
for b in range(N):
    a.append(c[b]-g[b])
for b1 in range(Q):
    sum=0
    for b2 in range(Q):
        if a[b2]-S[b1]>0:
            sum+=1
    if sum>=V[b1]:
        print('yes')
    else:
        print('no')
```
Answer by Vicky Zhang in Java
```

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class P5_30 {

	public static void tongji() {
		
		Scanner im=new Scanner(System.in);
		int numoffarm=im.nextInt();  //ln1
		int numofivi=im.nextInt();
		
		List<Integer> closetime=new ArrayList<>();
		for(int i=0;i<numoffarm;i++) {  //ln2
			closetime.add(im.nextInt());
			
		}
		
		List<Integer> taketime=new ArrayList<>();
		for(int i=0;i<numoffarm;i++) {   //ln3
			taketime.add(im.nextInt());
			
		}
		
		List<Integer> timebed=new ArrayList<>();  //隐藏
		for(int i=0;i<numoffarm;i++) {
			timebed.add(closetime.get(i)-taketime.get(i));
			
		}
		
		
		List<String> ans=new ArrayList<>();
		for(int i=0;i<numofivi;i++) {
			int count=0;
			int timere=im.nextInt();
			int timegetup=im.nextInt();
			
			for(int x:timebed) {
				if(x>timegetup) {
					count++;
				}	
			}
			
			if(count>=timere) {
				ans.add("YES");
			}else {
				ans.add("NO");
			}
		}
		
		for(String x:ans) {
			System.out.println(x);
		}
		
	}
	
	
	
	
	
	
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		tongji();
		
		
		
	}

}

```
Answer by Sally Fu
```
num_farm,num_q = map(int, input().split())
c=list(map(int, input().split()))
t=list(map(int, input().split()))
c_n=[]
for i in range(num_farm):
    c_n.append(c[i]-t[i])
c_n.sort(reverse=True)
for i in range(num_q):
    V,S=map(int, input().split())
    if S<=c_n[V-1]:
        print("YES")
    else:
        print("NO")
```
Answer by David Ao
```
n,q=map(int,input('pls input').split())
c=list(map(int,input().split()))
t=list(map(int,input().split()))
late_time=[c[i]-t[i] for i in range(n)]
late_time.sort(reverse=True)
print(late_time)
#上面都没问题 
for i in range(len(late_time)):
    ge,up=map(int,input('pls input').split())#放下来
    if up<late_time[ge-1]:#改为ge-1
        print('yes') 
    else:
        print('no')
```
Answer by Kelly Chen
```
n,q=list(map(int,input().split()))
fj=list(map(int,input().split()))
Bessie=list(map(int,input().split()))
late=[fj[i]-Bessie[i]for i in range(n)]

late.sort(reverse=True)


all=[]#创个列表储存v,s的结果
for i in range(q):
    Q=list(map(int,input().split()))
    all.append(Q)

for i in range(q):

    if all[i][1]<late[all[i][0]-1]:

            print(("YES"))
    else:
        print("NO")
```

Answer by today
>>>>>>> 98baffefb78371d3306b70ab944dc9b29ddd3011
