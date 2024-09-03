## 全排列

> [!Info]
> 按照字典序输出自然数 1 到 n 所有不重复的排列，即 n 的全排列，要求所产生的任一数字序列中不允许出现重复的数字。


```cpp
#include <bits/stdc++.h>
using namespace std;
int a[100], n;
int book[100] = {0};
void dfs(int k){
    if (k > n){
        for (int i=1; i<=n; i++){
            cout << setw(5) << a[i];
        }
        cout << endl;
        return;
    }
    for (int i=1; i<=n ;i++){
        if (book[i] == 0){
            a[k] = i;
            book[i] = 1;
            dfs(k+1);//下一步选择
            book[i] = 0;//回退
        }
    }
}
int main()
{
    cin >> n;
    dfs(1);
    return 0;
}
```