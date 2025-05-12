[Problem - C - Codeforces](https://codeforces.com/gym/574954/problem/C)

也是一道典型的==差分标记数组==题目，只是当时做的时候还没学前缀和，现在做做吧~

```cpp
void solve(vector<int> &q) {  
    int p;  
    cin >> p;  
    while(p--){  
        int l, r;  
        cin >> l >> r;  
        q[l] += 1;  
        q[r + 1] -= 1;  
    }  
}  
  
signed main() {  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr), cout.tie(nullptr);  
    int t, m;  
    cin >> t >> m;  
    int n = t;  
    vector<int> q(m + 2,0); //将学生的空闲时间段通过差分数组表示出来，m+2防止越界 
    while(t--){  
        solve(q);  
    }  
    int minn = 0, num = INT_MAX;  
    vector<int> pre(m + 1,0);  //差分数组的前缀和，用于后续数组的遍历，题目要求到达的人尽可能多，则n-pre[i]尽可能小pre[i]表示为i时间有多少人为空闲
    pre[0] = 0;  
    for(int i = 1; i <= m; i++){  
        pre[i] = pre[i - 1] + q[i];  
        int absent = n - pre[i];  
        if(absent < num){  
            num = absent;  
            minn = i;  
        }  
    }  
    cout << minn << " " << num << endl;

```
把[前缀和，差分数组前知](前缀和，差分数组前知.md)搞懂了，这题就是水题！！
