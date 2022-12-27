开始于2022年12月26日



<hr>

# PAT乙级刷题记录：

| 编号 |           标题           |   分类   |
| :--: | :----------------------: | :------: |
| 1001 | 害死人不偿命的(3n+1)猜想 | 简单模拟 |
| 1002 |        写出这个数        | 简单模拟 |
|      |                          |          |



<br>

<hr>
<br>



## 简单模拟

### 1001 害死人不偿命的(3n+1)猜想

题目链接： [1001 害死人不偿命的(3n+1)猜想](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805325918486528)

AC代码：

```c++
#include<iostream>
using namespace std;

int main(){
    int n, count = 0;
    scanf("%d", &n);
    
    while(n != 1){
        if(n % 2) n = (3 * n + 1) / 2;
        else n /= 2;
        
        count++;
    }
    printf("%d\n", count);
    
    return 0;
}
```



<br>



### 1002 写出这个数

题目链接：[1002 写出这个数](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805324509200384)

AC代码：

```c++
#include <iostream>
using namespace std;

int sum = 0;
string s[] = {"ling", "yi", "er", "san", "si", "wu", "liu", "qi", "ba", "jiu"};
string str, tmp;

int main(){
    cin >> str;
    for(int i = 0; i < str.size(); i++ ){
        sum += (str[i] - '0');
    }
    
    tmp = to_string(sum);
    for(int i = 0; i < tmp.size(); i++ ){
        if(!i) cout << s[tmp[i] - '0'];
        else cout << " " << s[tmp[i] - '0'];
    }
    
    return 0;
}
```

注意：

- 相加为0的时候是“零”不是“十”
