开始于2022年12月26日



<hr>

# PAT乙级刷题记录：

| 编号 |           标题           |   分类   |
| :--: | :----------------------: | :------: |
| 1001 | 害死人不偿命的(3n+1)猜想 | 简单模拟 |
| 1002 |        写出这个数        | 简单模拟 |
| 1003 |        我要通过！        | 简单模拟 |
| 1004 |         成绩排名         |   排序   |
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



<br>



### 1003 我要通过！

题目链接：[1003 我要通过！](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805323154440192)

AC代码：

```c++
#include <iostream>
#include <map>
using namespace std;

int n;
string str;
map<char, int> mp;

bool func(string s){
    int n = s.size();
    int p, t = 0;
    
    // 注意每次开始前要先清空map
    mp.clear();
    for(int i = 0; i < n; i++ ){
        mp[s[i]]++;
        
        // p和t记录P和T出现的位置
        if(s[i] == 'P') p = i;
        if(s[i] == 'T') t = i;
    }
    
    // 正确的条件：只有PAT三个字母，P和T出现一次，P前面的A的数目乘以P和T中间A的数目等于T后面的A的数目
    if(mp.size() == 3 && mp['P'] == 1 && mp['A'] >= 1 && mp['T'] == 1 && p < t - 1 && p * (t-p-1) == n-t-1) return true;
    return false;
       
}

int main(){
    cin >> n;
    
    while(n--){
        cin >> str;
        if(func(str)) cout << "YES" << endl;
        else cout << "NO" << endl;
    }
    
    return 0;
}
```

注意：

- 看了别人的思路才知道要P前面的A的数目乘以P和T中间A的数目等于T后面的A的数目-=
- 注意每次开始要清空map



<br>



## 排序

### 1004 成绩排名

原题链接：[1004 成绩排名](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805321640296448)

思路：

- 重写小于号，用结构体排序来实现

AC代码：

```c++
// B1004
#include <iostream>
#include <algorithm>
using namespace std;

int n;
const int maxn = 1e5 + 10;
struct student{
	string name;
	string id;
	int score;
	
	bool  operator< (const student& t) const{
        return score > t.score;
    }

}st[maxn];

int main(){
	cin >> n;
	
	for(int i = 0; i < n; i ++ )
		cin >> st[i].name >> st[i].id >> st[i].score;
		
	sort(st, st + n);
	
	cout << st[0].name << " " << st[0].id  << endl;
	cout << st[n-1].name << " " << st[n-1].id  << endl;
	
	return 0;
} 
```

