[Problem - A - Codeforces](https://codeforces.com/contest/1882/problem/A)

==800分的贪心题目==

You are given a sequence $a_{1}, a_{2}, \ldots, a_{n}$. A sequence $b_{1}, b_{2}, \ldots, b_{n}$ is called good, if it satisfies all of the following conditions:

-   $b_{i}$ is a positive integer for $i = 1, 2, \ldots, n$;
-   $b_{i} \neq a_{i}$ for $i = 1, 2, \ldots, n$;
-   $b_{1} < b_{2} < \ldots < b_{n}$

Find the minimum value of $b_{n}$ among all good sequences $b_{1}, b_{2}, \ldots, b_{n}$.

题目的大概意思就是给一个序列$a_n$,要求最小的满足与$a_n$对应的$b_n$，并且在连续的$b_n$中，$b_{1} < b_{2} < \ldots < b_{n}$
因此题目的思路就很明显了:
1. 当$i==1$时，如果a[1]是1的话，则将b[1]初始化为2，如果a[1]!=1，则b[1]=1，因为题目并没有对b数组与a数组直接的大小关系进行限制
2. 当$i>=2$时，检查当前位置的a[i]与b[i-1]的大小关系，如果$a[i]==b[i-1]+1$-> ==为什么有这个条件？因为题目中要求$b_i$!=$a_i$==,则$b[i]=b[i-1]+2$,否则，$b[i]=b[i-1]+1$;

代码部分:
```cpp
void solve() {  
    int n;  
    cin >> n;  
    vector<int> a(n + 1,0), b(n + 1,0);  
    for(int i = 1; i <= n; i++){  
        cin >> a[i];  
        if(i == 1) b[1] = (a[1] == 1) ? 2 : 1;  
        if(a[i] == b[i - 1] + 1){  
            b[i] = b[i - 1] + 2;  
        } else{  
            b[i] = b[i - 1] + 1;  
        }  
        // cout << b[i] << " ";  
    }  
    cout << b[n] << endl;  
}
```