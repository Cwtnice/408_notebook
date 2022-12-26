开始于2022年12月26日



<hr>

# PAT乙级刷题记录：

| 编号 | 标题                     | 分类     |
| :--- | ------------------------ | -------- |
| 1001 | 害死人不偿命的(3n+1)猜想 | 简单模拟 |
| 1002 | 写出这个数               | 简单模拟 |
|      |                          |          |



<br>

<hr>

<br>



## 简单模拟

### 1001 害死人不偿命的(3n+1)猜想

题目连接： [1001 害死人不偿命的(3n+1)猜想](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805325918486528)

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



