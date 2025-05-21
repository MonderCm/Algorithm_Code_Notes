题目:
$\hspace{15pt}$Tk 有两个长度为 $n$ 的数组 $\{a_1,a_2,\dots,a_n\}$ 与 $\{b_1,b_2,\dots,b_n\}$. $\hspace{15pt}$记数组 $c$ 的每个元素为 $c_i=a_i \times b_i \times i$. $\hspace{15pt}$Tk 希望你重新排列数组 $b$ 使得数组 $c$ 的和最大.


这个题我自己做的时候已经猜到个大概，就是说大的b[i]与大的a[i]相对应，小的b[i]与小的a[i]对应-> ==重排不等式==,简单来说就是：==**对于两个同样长度的实数序列，将它们同号同向（即同样的升序或降序）配对后，点积达到最大；反向配对（一个升序一个降序）时，点积达到最小。**==

题目的目的是:$$\sum_{i=1}^n a_i \cdot b_i \cdot i$$
由于 $a​_i$ 和位置 i 都是固定的，我们可以把它们合并成一个“权重”:
$$w_i = a_i \cdot i$$
根据重排不等式，要让两个数列的乘积和最大---也就是把更大的b值分配给更大的w值。

**解题思路:**
- **计算权重**：对每个下标 iii（从 1 开始计数），计算 $w_i=a_i×i$
	
- **排序权重**：把所有 $(w_i,i)$ 按 $w_i$​ 从小到大排序，记录每个权重对应的原始下标。
    
- **排序 b：将数组 b 本身从小到大排序。
    
- **匹配赋值**：对于排序后第 k 小的权重，其对应位置就分配排序后第 k 小的 b 值。
    
- **输出结果**：按照原始下标顺序输出新排列的 b 数组。

```cpp
int a[N], b[N];  
  
signed main() {  
    ios::sync_with_stdio(false);  
    cin.tie(nullptr), cout.tie(nullptr);  
    int n;  
    cin >> n;  
    vector<int> a(n), b(n);  
    for(int i = 0; i < n; i++) cin >> a[i];  
    for(int i = 0; i < n; i++) cin >> b[i];  
    sort(b.begin(),b.end()); //从小到大排序b_i 
    vector<pair<int ,int>> w;//用于处理a_i*i的值，并且保存原始下标i，目的是为了让b能够分配到正确的原始数组a[i]对应的位置  
    w.reserve(n);//预分配内存，实际w.size()==0  
    for(int i = 0; i < n; i++){  
        w.emplace_back(a[i] * (i + 1),i);//在vector末尾构建信的pair并插入  
    }  
    sort(w.begin(),w.end(),  
         [](const pair<int ,int> &p1,  
            const pair<int ,int> &p2) {  
             return p1.first < p2.first;  
         });//从小到大排序w_i 
  
    vector<int> re(n);  
    for(int i = 0; i < n; i++){  
        int index = w[i].second;//当前最小w_i对应的下标  
        re[index] = b[i];//将最小的b_i分配给当前位置的a_i  
    }  
    for(int i = 0; i < n; i++) cout << re[i] << " ";  
  
    return 0;  
}

```
**时间复杂度:**
1. ​**输入处理**​：读取两个数组，时间复杂度为O(n)。
2. ​**排序数组b**​：时间复杂度为O(n log n)。
3. ​**构建并排序向量w**​：
    - 构建w的循环是O(n)。
    - 对w排序的时间复杂度为O(n log n)。
4. ​**生成结果数组re**​：循环处理，时间复杂度O(n)。
5. ​**输出结果**​：时间复杂度O(n)。

​**总时间复杂度**​ = O(n log n) + O(n log n) + O(n) + O(n) = ​**O(n log n)​**。

**本题学到的一些新内容:**

1. ==weights.reserve(n)== 
	**预先给 `weights` 分配能够容纳 `n` 个元素的内存空间。这样做可以避免在后面不断 `push_back` 或 `emplace_back` 时，多次重新分配内存，提高效率。**
2. ==emplace_back(...)==
	**直接在 `vector` 的末尾原地构造一个新的元素，如果先前分配了如`vector<int>a(n)`->`a[0~n-1]`,则使用**`emplace_back(x)`**时，`a[n]==x`，比 `push_back(make_pair(...))` 少一次拷贝，更高效。**
3. ==pair==->模板
	**定义:是 C++ 标准库里提供的一个模板，用来把两个不同类型（或者相同类型）的值“打包”在一起**
```cpp
	template<typename T1, typename T2>
struct pair {
    T1 first;
    T2 second;
    // …还有一些构造、比较运算符等…
};
```
`vector<pair<ll,int>> weights;`相当于定义了一个元素类型是pair<ll,int>的动态数组,每个元素有两个成员:
- `first`：类型是 `ll`（即 `long long`），这里用来存储“权重”值。
    
- `second`：类型是 `int`，用来存储对应的原始下标。

