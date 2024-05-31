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
