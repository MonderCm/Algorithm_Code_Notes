# 二分查找
```
	signed main() {  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr), cout.tie(nullptr);  
    cin >> n;  
    for (int i = 1; i <= n; i++) cin >> a[i] >> b[i];  
  
    int l = 1, r = 1e9 + 10, minn = INT_MAX, maxx = INT_MIN;  
    while (l <= r){  
        int mid = l + ((r - l) >> 1);  //寻找左边界
        int t = check(mid);  
        if (t == 0 || t == 1){  
            r = mid - 1;  
            if (t == 0) minn = mid;  更新可能的最小值
        } else{  
            l = mid + 1;  
        }  
    }
```
