重启于 2023年3月7日



<hr>

## 目录：

| 编号 |           标题           |         分类         |
| :--: | :----------------------: | :------------------: |
| 1001 | 害死人不偿命的(3n+1)猜想 |       简单模拟       |
| 1002 |        写出这个数        |       简单模拟       |
| 1003 |        我要通过！        |       简单模拟       |
| 1004 |         成绩排名         |         排序         |
| 1005 |      继续(3n+1)猜想      |    简单模拟+排序     |
| 1006 |     换个格式输出整数     |       简单模拟       |
| 1007 |        素数对猜想        | 筛选法求素数（好题） |
| 1008 |   数组元素循环右移问题   |       简单模拟       |
| 1009 |          说反话          |  简单模拟 二维数组   |
| 1010 |      一元多项式求导      |       简单模拟       |
| 1011 |          A+B和C          |       大数加法       |
| 1012 |         数字分类         |       简单模拟       |
| 1013 |          数素数          |     筛选法求素数     |
| 1014 |      福尔摩斯的约会      |     模拟 小坑多      |
| 1015 |          德才论          |      模拟 排序       |



<br>

<hr>

<br>



## 1001 害死人不偿命的(3n+1)猜想

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



<hr>



## 1002 写出这个数

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



<hr>



## 1003 我要通过！

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



<hr>



## 1004 成绩排名

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



<hr>



## 1005 继续(3n+1)猜想

题目链接：[1005 继续(3n+1)猜想](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805320306507776)

AC代码：

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int arr[10000];

// 自定义排序 为了从大到小逆序输出 
bool cmp(int a, int b) {return a > b;}

int main() {
    int k, n, flag = 0;
    cin >> k;
    vector<int> v(k);
    
    for (int i = 0; i < k; i++) {
        cin >> n;
        v[i] = n;
        while (n != 1) {
            if (n % 2 != 0) n = 3 * n + 1;
            n = n / 2;
            if (arr[n] == 1) break;
            arr[n] = 1;
        }
    }
    sort(v.begin(), v.end(), cmp);
    for (int i = 0; i < v.size(); i++) {
        if (arr[v[i]] == 0) {
            if (flag == 1) cout << " ";
            cout << v[i];
            flag = 1;
        }
    }
    return 0;
}
```



<hr>



## 1006 换个格式输出整数

题目链接：[1006 换个格式输出整数](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805318855278592?type=7&page=0)

AC代码：

```cpp
#include <iostream>
#include <cstring>
using namespace std;

int main(){
    string ans;
    int n, a, b;
    scanf("%d", &n);
    
    // 百位
    a = n / 100;
    while(a--) printf("B");
    n %= 100;
    
    // 十位
    b = n / 10;
    while(b--) printf("S");
    n %= 10;
    
    // 个位
    for(int i = 1; i <= n; i++) printf("%d", i);
    
    return 0;
}
```



<hr>


## 1007 素数对猜想

题目链接：[1007 素数对猜想](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805317546655744?type=7&page=0)

**思路：**

打表，以空间换时间，是很常用的一种提高算法效率的思想。

**筛法求素数：**

指从小到大筛去一个已知素数的所有倍数。

以筛选法求10000以内的素数为例，根据素数2可筛去4、6、8…等数，然后根据索数3可筛去9、6、12、15…等数，由于4已被筛去了，下一个用于筛选的素数是5…依此类推，最后剩余的就是10000以内的素数。


AC代码：

```cpp
#include <iostream>
#include <cmath>
using namespace std;

const int maxn = 100010;
int a[maxn];

// 筛选法求素数 ：找出所有的非素数, 剩下的就是素数
void fun(){    
    a[0] = a[1] = 1;    // 最小的素数是2, 素数标记为0
    for(int i = 2; i < sqrt(maxn); i++){
        if(a[i] == 0){    // 已经是素数的不进入循环
            for(int j = i * 2; j <= maxn; j += i)
                a[j] = 1;
        }
    }
}

int main(){
    fun();    // 先打表
    int n, tmp = 3, ans = 0;    // tmp上一个素数, 从3开始
    cin >> n;

    for(int i = 0; i <= n; i++){
        if(a[i] == 0){    // 是素数的话
            if(i - tmp == 2) ans++;
            tmp = i;
        }
    }
    
    cout << ans << endl;

    return 0;
}
```



<hr>


## 1008 数组元素循环右移问题

题目链接：[1008 数组元素循环右移问题](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805316250615808?type=7&page=0)

AC代码：

```cpp
#include <iostream>
using namespace std;

int n, m, a[110];

int main(){
    cin >> n >> m;
    for(int i = 0; i < n; i++) cin >> a[i];

    if(m >= n) m %= n;    // m大于n的情况需要进行取余

    // 向右移动m次
    for(int i = 0; i < m; i++){    
        int tmp =a[n - m + i];
        for(int j = n - m + i; j > i; --j)
            a[j] = a[j - 1]; // 向右移动一位
        a[i] = tmp;
    }

    // 输出
    cout << a[0];
    for(int i = 1; i < n; i++)
        cout << " " << a[i];

    return 0;
}
```



<hr>



## 1009 说反话

题目链接：[1009 说反话](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805314941992960?type=7&page=0)

AC代码：

```cpp
#include <iostream>
#include <cstring>
using namespace std;

char word[90][90];

int main(){
	char str[90];
	cin.getline(str, 90);
	
	int len = strlen(str), r = 0, c = 0;	//r行 c列
	for(int i = 0; i < len; i ++ ){
		if(str[i] != ' '){
			word[r][c++] = str[i];
		}
		else{
			word[r][c] = '\0';
			r++;
			c = 0;
		}
	} 
	
	for(int i = r; i >= 0; i -- ){
		if(i == r) cout << word[i];
		else cout << ' ' << word[i];
	}
	return 0;
} 
```



<hr>


## 1010 一元多项式求导

题目链接：[1010 一元多项式求导](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805313708867584?type=7&page=0)

AC代码：

```cpp
#include <iostream>
using namespace std;

int a, b, flag = 0;    // a、b为一次读两个数 flag为0表示是输出的第1个数

int main(){
    while(~scanf("%d %d", &a, &b)){
        if(a*b){
            printf("%s%d %d", (flag?" ": ""), a*b, b-1);    // 用于输出第一个数时特殊处理
            flag++;
        }
        if(!flag) printf("0 0");	// 当结果为0时 按题目要求输出
    }

    return 0;
}
```



<hr>



## 1011 A+B和C

题目链接：[1011 A+B和C](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805312417021952?type=7&page=0)

直接使用long long实现的AC代码：

```cpp
#include <iostream>
using namespace std;

typedef long long ll;
int t;

int main(){
    scanf("%d", &t);
    for(int cases = 1; cases <= t; cases++){
        long long a, b, c;
        scanf("%lld %lld %lld", &a, &b, &c);

        printf("Case #%d: %s\n", cases, (a+b>c)?"true":"false");
    }

    return 0;
}
```



<hr>



## 1012 数字分类

题目链接：[1012 数字分类](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805311146147840?type=7&page=0)

按题目说的模拟即可，但注意第8个测试点，a2不能直接用是否等于0来判断N

AC代码：

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int n, a[1010], a1 = 0, a2 = 0, c = 1, a3 = 0, sum4 = 0, count4 = 0, a5 = 0;
bool flag2 = false;    // a2是否有效的标记

int main(){
    scanf("%d", &n);
    for(int i = 0; i < n; i++) scanf("%d", &a[i]);

    for(int i = 0; i < n; i++){
        if(a[i] % 5 == 0 && a[i] % 2 == 0) a1 += a[i];
        
        if(a[i] % 5 == 1){
            flag2 = true;
            a2 += c * a[i];
            c *= -1;
        }
        
        if(a[i] % 5 == 2) a3++;

        if(a[i] % 5 == 3){
            sum4 += a[i];
            count4++;
        }

        if(a[i] % 5 == 4){
            a5 = max(a5, a[i]);
        }
    }

    if(a1 == 0) printf("N"); else printf("%d", a1);
    if(!flag2) printf(" N"); else printf(" %d", a2);
    if(a3 == 0) printf(" N"); else printf(" %d", a3);
    if(sum4 == 0) printf(" N"); else printf(" %.1f", float(sum4) / count4);
    if(a5 == 0) printf(" N"); else printf(" %d", a5);

    
    return 0;
}
```



<hr>



## 1013 数素数

题目链接：[1013 数素数](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805309963354112?type=7&page=0)

数组要开的大一点

AC代码：

```cpp
#include <iostream>
#include <cmath>
using namespace std;

const int maxn = 1000010;
int m, n, a[maxn];

// 将所有的非素数标记为1
void func(){
    a[0] = a[1] = 1;
    for(int i = 2; i < sqrt(maxn); i++){
        if(a[i] == 0){
            for(int j = 2 * i; j < maxn; j += i)
                a[j] = 1;
        }
    }
}

int main(){
    func();
    
    scanf("%d%d", &m, &n);
    int count = 0, count1 = 0;    // 记录范围和记录个数
    for(int i = 0; i < maxn; i++){
        if(a[i] == 0){
            count++;
            if(count >= m && count <= n){
                count1++;
                if(count1 != 1) putchar(' ');
                printf("%d", i);
                if(count1 == 10){
                    putchar('\n');
                    count1 = 0;
                }
            }
        }
    }

    return 0;
}
```



<hr>


## 1014 福尔摩斯的约会

题目链接：[1014 福尔摩斯的约会](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805308755394560?type=7&page=0)

这题目小坑特别多

AC代码：

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;

string s[7] = {"MON", "TUE", "WED", "THU",
               "FRI", "SAT", "SUN"};

int main(){
    string s1, s2;
    cin >> s1 >> s2;
    int len = min(s1.length(), s2.length());    // 取小值

    // 1、2行
    bool flag = true;    // 1星期 0小时
    for(int i = 0; i < len; i++){
        // 星期
        if(flag == true && s1[i] == s2[i] && s1[i] >= 'A' && s1[i] <= 'G'){
            cout << s[s1[i] - 'A'] << ' ';
            flag = false;
        }
        // 小时
        else if(flag == false && s1[i] == s2[i] && (isdigit(s1[i]) | (s1[i] >= 'A' && s1[i] <= 'N'))){
            if(s1[i] >= '0' && s1[i] <= '9'){
                printf("%02d:", s1[i] - '0');
                break;
            }
            if(s1[i] >='A' && s1[i] <= 'N'){
                printf("%d:", s1[i] - 'A' + 10);
                break;
            }
        }
    }

    // 3、4行
    cin >> s1 >> s2;
    len = min(s1.length(), s2.length());
    for(int i = 0; i < len; i++){
        if(s1[i] == s2[i] && isalpha(s1[i])){
            if(i == 60) printf("00");
            else printf("%02d", i);
            break;
        }
            
    }
    
    return 0;
}
```



<hr>



## 1015 德才论

题目链接：[1015 德才论](https://pintia.cn/problem-sets/994805260223102976/exam/problems/994805307551629312?type=7&page=0)

AC代码：

```cpp
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;

struct student{
    ll id, de, cai, total, level;  // d德 c才
    student(ll i, ll d, ll c, ll le):id(i), de(d), cai(c), level(le) {total=de + cai;}
};


int n, l, h;

int main(){
    ios::sync_with_stdio(false); // 取消stdin的同步, 加快速度

    vector<student>sts; // 结构体动态数组
    ll id, de, cai, level;

    cin >> n >> l >> h; // n总数 l录取最低线 h优先录取线
    while(n--){
        cin >> id >> de >> cai;

        // 划分等级
        if(de < l || cai < l) continue;
        if(de >= h && cai >= h) level = 1;
        else if(de >= h && cai < h) level = 2;
        else if(de < h && cai < h && de >= cai) level = 3;
        else level = 4;

        // 压入结构体数组
        sts.push_back(student(id, de, cai, level));
    }

    // 排序
    sort(sts.begin(), sts.end(), [](const student& s1, const student& s2){
        return tie(s1.level, s2.total, s2.de, s1.id) < tie(s2.level, s1.total, s1.de, s2.id);
    });

    cout << sts.size() << endl;
    for(auto& s : sts){
        cout << setw(8) << s.id << " " << s.de << " " << s.cai << endl;
    }

    return 0;
}
```

