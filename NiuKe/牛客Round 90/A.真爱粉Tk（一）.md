
这题是签到题吧属于，题目要求判断n是否为为2.5的倍数，能被2.5整除肯定也能被5整除，因此就可以有以下代码~

```cpp
#include <bits/stdc++.h>  
using namespace std;  
#define endl "\n"  
#define lcm(x,y) ((x)/__gcd(x,y)*(y))  
#define int long long  
#define pb push_back()  
#define f first  
#define s second  
using ll = long long;  
constexpr int mod = 1e9 + 7, MOD = 998244353;  
constexpr int N = 1e9 + 10;  
  
signed main() {  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr), cout.tie(nullptr);  
    int n;  
    cin >> n;  
    int flag = 0;  
    if (n % 5 == 0){  
        flag = 1;  
    }  
    if (flag) cout << "Yes" << endl;  
    else cout << "No" << endl;  
    return 0;  
}

```
