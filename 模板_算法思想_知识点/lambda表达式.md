在 C++ 中，**lambda 表达式**（Lambda Expression）是一种**匿名函数**，可以在定义处直接写出一段可调用的代码，它的基本语法结构如下：

```cpp
[capture](parameters) -> return_type {    
         // 函数体
}
```

各部分含义：
1. **`[capture]`**：**捕获列表**，用于从外部作用域“捕获”变量到 lambda 内部。
    
    - `[]`：不捕获任何外部变量
        
    - `[x, &y]`：按值捕获 `x`，按引用捕获 `y`
        
    - `[=]`：按值捕获所有外部变量
        
    - `[&]`：按引用捕获所有外部变量
        
    - `[this]`：捕获当前对象的指针
        
2. **`(parameters)`**：参数列表，和普通函数一样，可以写形参。也可以为空 `()`。
    
3. **`-> return_type`**（可选）：显式指定返回类型。如果函数体里只有一个 `return` 并且编译器能推断类型，这部分可以省略。
    
4. **函数体 `{ … }`**：具体要执行的代码。


**示例**
1. **最简单的无参无捕获**
```cpp
auto f = []() {      
	std::cout << "Hello, Lambda!" << std::endl;  
}; 
f();  // 调用 lambda，输出 Hello, Lambda!
```
    
2. **带参数和隐式返回类型**
```cpp
    auto add = [](int x, int y) {  
        return x + y;  
    }; 
    
    int s = add(2, 3);  // s == 5
```
    
3. **按值和按引用捕获**
 
```cpp
    int a = 10, b = 20; 
	auto by_value = [a]() mutable {  // mutable 允许在 lambda 内修改捕获的 a 副本    
		 a += 5;      
		 return a;  // 15，但外部的 a 依然是 10
	}; 
	auto by_ref   = [&b]() {      
		  b += 5;      
		  return b;  // 外部的 b 变成了 25 
	};
```
    
4. **在 `sort` 中用 lambda**
```cpp

vector<pair<ll,int>> weights; // …… 填充 weights ……   
sort(weights.begin(), weights.end(), 
[](const pair<ll,int>& p1, const pair<ll,int>& p2) {           return p1.first < p2.first;    
});
```
这里的 lambda 就是一个临时的比较函数，用来告诉 `sort` 按 `pair.first` 升序排序。

---

**总结**：

- Lambda 表达式让你可以在需要“可调用对象”（如函数指针、函数对象、比较器、回调函数）的地方，**定义内联的匿名小函数**，并能灵活捕获外部变量，写法简洁、阅读方便。