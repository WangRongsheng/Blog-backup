---
layout: post
cid: 81
title: 数据结构期末52道OnlineJudge机试题目考核-大二上
slug: 81
date: 2019/12/28 18:14:00
updated: 2020/02/22 13:59:48
status: publish
author: 王荣胜
categories: 
  - 基础算法
tags: 
  - 52OJ
thumb2: https://s2.ax1x.com/2019/12/28/lmEb9K.png
---


<!--more-->

<center>
<img src="https://s2.ax1x.com/2019/12/28/lmEb9K.png" alt="lmEb9K.png" border="0" /></center>

**所有题目全部在杭电OJ完成：**[http://acm.hdu.edu.cn/](http://acm.hdu.edu.cn/)

```c
//1000 A + B Problem
#include<iostream> 
using namespace std;

int main(){
    int a,b,sum;
    while(cin>>a>>b){
        sum = 0;
        sum = a + b;
        cout<<sum<<endl; 
    } 
} 
```

```c
//1005 Number Sequence
#include <iostream>
int A,B;
int f(int n){
    if( n == 1 || n == 2){
        return 1;
    }
    return (A*f(n-1)+B*f(n-2))%7;
}
int main(){
 
    int n;
    while(scanf("%d%d%d",&A,&B,&n)!=EOF,A||B||n){
        int a = f(n%49);
        printf("%d\n",a);
    }
}
```

```c
//1008 Elevator
#include<iostream>
using namespace std;

int main(){
    int n,a[100],i,sum;
    while(cin>>n&&n!=0){
        sum = 0;
        for(i=0;i<n;i++){
            cin>>a[i];
        }
        if(n==1){
            sum = a[0]*6+5;
        }
        else{
        sum = n*5+a[0]*6;
        for(i=0;i<n-1;i++){
            if(a[i+1]>a[i]){
                sum += (a[i+1]-a[i])*6;
            }
            else{
                sum += (a[i]-a[i+1])*4;
            }
        }
    }
        cout<<sum<<endl;
    }
}
```

```c
//1012 u Calculate e
#include<stdio.h>

int main() {
    double e;
    int i, tmp;
    e = 1;
    tmp = 1;
    printf("n e\n");
    printf("- -----------\n");
    printf("0 1\n");
    for(i = 1; i < 10; i++) {
        tmp *= i;
        e += 1.0/tmp;
        if(i>=3) printf("%d %.9lf\n", i, e);
        else if(2 == i) printf("%d %.1lf\n", i, e);
        else printf("%d %.0lf\n",i, e);
    }
}
```

```c
//1032 The 3n + 1 problem
#include <iostream>
using namespace std;
 
int main()
{
    int a,b,t,i,max;
    while(cin >> a >> b)
    {
        cout << a << " " << b << " ";
        if(a>b)//大小不确定
        {
            t = a;
            a = b;
            b = t;
        }
        max = 0;
        for(i = a; i<=b; i++)
        {
            int n = i, sum = 1;
            while(n-1)//等于1时就结束
            {
                if(n%2)
                    n = 3*n+1;
                else
                    n = n/2;
                sum++;
            }
            if(sum>max)
            max = sum;
        }
        cout << max << endl;
    }
}
```

```c
//1037 Keep on Truckin'
#include<iostream>
using namespace std;

int main(){
    int a,b,c,count;
    while(cin>>a>>b>>c){
        count =0; 
        if(a<=168){
            count+=1; 
            cout<<"CRASH "<<a<<endl; 
        } 
        if(b<=168){
            count+=1;
            cout<<"CRASH "<<b<<endl;
        } 
        if(c<=168){
            count+=1;
            cout<<"CRASH "<<c<<endl;
        }
        if(count!=1){
            cout<<"NO CRASH"<<endl; 
        } 
    } 
}
```

```c
//1040 As Easy As A+B
#include<iostream>
using namespace std;

int main(){
    int n,m,q,i,j,a[1000],t;
    cin>>n;
    for(q=0;q<n;q++){
        cin>>m;
        for(j=0;j<m;j++){
            cin>>a[j];
        }
        for (i = 0; i < m - 1; i++)     
            for (j = 0; j < m - 1 - i; j++)
            if (a[j] > a[j + 1]){
                t = a[j+1];
                a[j+1] = a[j];
                a[j] = t;
            }
        for(j=0;j<m;j++){
            if(j!=m-1)
                cout<<a[j]<<" ";
            else{
                cout<<a[j]<<endl;
            }
        }    
        a[0] = 0;
    }
}
```

```c
//1042 N!
#include<stdio.h>
int main()
{
    int a[10000];
    int i,j,c,m,n;
    while(scanf("%d",&n)!=EOF){
    a[0]=1;
    m=0; 
    for(i=1;i<=n;i++)
    { 
        c=0; 
        for(j=0;j<=m;j++)
        { 
        a[j]=a[j]*i+c; 
        c=a[j]/10000; 
        a[j]=a[j]%10000; 
        } 
    if(c>0) {m++;a[m]=c;} 
    } 
    printf("%d",a[m]); 
    for(i=m-1;i>=0;i--) printf("%4.4d",a[i]);
    printf("\n");
    }
    return 0;
}
```

```c
//1048 The Hardest Problem Ever
#include <stdio.h>
#include <string.h>
#include <ctype.h>
 
char str[220];
 
int main()
{
    while(gets(str)){
        if(!strcmp(str, "ENDOFINPUT")) break;
        else if(!strcmp(str, "START") || !strcmp(str, "END")) continue;
        for(int i = 0; str[i]; ++i){
            if(isalpha(str[i])) str[i] = ((str[i] - 'A') + 26 - 5) % 26 + 'A';
        }
        puts(str);
    }
    return 0;
}
```

```c
//1056 HangOver
#include<iostream>
using namespace std;

int main(){
    float a,sum,i,count;
    while(cin>>a&&a){
        sum = 0;
        count = 0;
        for(i=2;sum<a;i++){
            sum += 1/i;
            count ++;
        }
        cout<<count<<" card(s)"<<endl;
        
    }
}
```

```c
//1089 A+B for Input-Output Practice (I)
#include<iostream> 
using namespace std;

int main(){
    int a,b,sum;
    while(cin>>a>>b){
        sum = 0;
        sum = a + b;
        cout<<sum<<endl; 
    } 
} 
```

```c
//1094 A+B for Input-Output Practice (VI)
#include<iostream> 
using namespace std;

int main(){
    int a[1000],sum,n,i;
    while(cin>>n){ 
        for(i=0;i<n;i++){
            cin>>a[i]; 
        } 
        sum = 0;
        for(i=0;i<n;i++){
            sum += a[i];  
        } 
        cout<<sum<<endl; 
    } 
}
```

```c
/*
最大公约数求法：
有两整数a和b：

① a%b得余数c

② 若c=0，则b即为两数的最大公约数

③ 若c≠0，则a=b，b=c，再回去执行①
*/
//1108 最小公倍数
#include<iostream>
using namespace std;

int main(){
    int a,b,i;
    while(scanf("%d %d",&a,&b)!=EOF){
        for(i=1;i!=0;i++){
            if(i%a==0&&i%b==0){
                cout<<i<<endl;
                break;
            }
    }
}
}
```

```c
//1157 Who's in the Middle
#include<iostream>
#include<algorithm>
using namespace std;

int main(){
    int n,a[100000],i,t;
    while(cin>>n){
        for(i=0;i<n;i++){
            cin>>a[i];
        }
        sort(a,a+n);
        t = n/2;
        cout<<a[t]<<endl;
    }
}
```

```c
//1222 Wolf and Rabbit
#include<stdio.h>

int gcd(int a,int b)
{
    return b?gcd(b,a%b):a;
}

int main()
{
    int p,n,m,i;
    while(scanf("%d",&p)!=EOF)
    {
        for(i=0;i<p;i++)
        {
            scanf("%d%d",&m,&n);
            if(gcd(m,n)==1)
                printf("NO\n");
            else
                printf("YES\n");
        }
    }
}
```

```c
// 1280 前m大的数

#include<stdio.h>
#include <algorithm>
using namespace std;
#include <string.h>
    int a[5005];
    int b[5000005];
int main()
{
    int i,j,n,m,l,count;
    while(scanf("%d%d",&n,&m)!=EOF)
    {
        l=count=0;
        memset(a,0,sizeof(a));
        memset(b,0,sizeof(b));
        for(i=1;i<=n;i++)
            scanf("%d",&a[i]);
        sort(a+1,a+1+n);
        for(i=n;i>=1;i--)
            for(j=i-1;j>=0;j--)
            {
                count++;
                b[l++]=a[i]+a[j];
                if(count==n*(n-1)/2)
                    break;
            }
            sort(b,b+l);
            for(i=l-1;m>0;m--,i--)
            {
                if(m!=1)
                    printf("%d ",b[i]);
                else
                    printf("%d\n",b[i]);
            }
    }
    return 0;
}
```



```c
//1395 2^x mod n = 1
#include<stdio.h>

int main()
{
    int n, x, round;
    while (scanf("%d", &n) != EOF)
    {
        if (n % 2 == 0 || n == 1)
        {
            printf("2^? mod %d = 1\n", n);
        }
        else
        {
            x = 1, round = 2;
            while (round != 1)
            {
                round = round * 2 % n;
                ++x;
            }
            printf("2^%d mod %d = 1\n", x, n);
        }
    }
}
```


```c
//1465 不容易系列之一
#include <stdio.h>
int main()
{
    __int64 a[21];
    int i,n;
    a[1]=0;
    a[2]=1;
    while(scanf("%d",&n)!=EOF)
    {
        for(i=3;i<n+1;i++){
            a[i]=(i-1)*(a[i-1]+a[i-2]);
            }
        printf("%I64d\n",a[n]);
    }
    return 0;
}
```

```c
//1495 非常可乐
#include<iostream>
using namespace std;

int gcd(int a,int b){
    return b?gcd(b,a%b):a; 
} 

int main(){
    int a,b,c;
    while(cin>>a>>b>>c&&a+b+c){
        a/=gcd(b,c);
        if(a&1) cout<<"NO"<<endl;
        else cout<<a-1<<endl; 
    } 
} 
```

```c
//1555  How many days?
#include<iostream>
using namespace std;

int main(){
    int m,k,times;
    while(cin>>m>>k&&m!=0&&k!=0){
        times = 0;
        while(m--){
            times+=1;
            if(times%k==0){
                m++;
            }
        }
        cout<<times<<endl;    
    }
}
```



```c
//1412 {A} + {B}
#include<iostream>
#include<algorithm>
using namespace std;
const int N=10000+10;
int a[N*2];

int main()
{
    int n,m,i;
    while(~scanf("%d%d",&n,&m))
    {
        for(i=0; i<n+m; i++)
            scanf("%d",&a[i]);
        sort(a,a+n+m);
        int y=unique(a,a+n+m)-a;
        for(i=0; i<y; i++)
        {
            printf("%d",a[i]);
            if(i!=y-1)
                printf(" ");
        }
        printf("\n");
    }
    return 0;
}
```

```c
//1466 计算直线的交点数
#include<stdio.h>
int dp[21][191];

int main()
{
    int i,j,k,n;
    memset(dp,0,sizeof(dp));
    for(i=0;i<21;i++){
        dp[i][0]=1;
    }                                //初始化，一定有0个交点，所以dp[i][0]==1
    for(i=1;i<21;i++){
        for(j=0;j<i;j++){        //j条平行线，剩下i-j条自由线
            for(k=0;k<191;k++){          //i-j条自由线是否有k个交点的交法，有则i条直线就可以多一种交法
                if(dp[i-j][k]==1){
                    dp[i][(i-j)*j+k]=1;
                }
            }
        }
    }
    while(scanf("%d",&n)!=EOF){
        printf("0");
        for(i=1;i<191;i++){
            if(dp[n][i]==1){
                printf(" %d",i);
            }
        }
        printf("\n");
    }
    return 0;
}
```

```c
//1521 排列组合
#include <iostream>
using namespace std;

int a[15],n,m,ans;

int fun(int num)
{
    if(num == 0)return 1;
    int sum=1,i;
    for(i=2;i<=num;i++)sum*=i;
    return sum;
}

void dfs(int num,int sum,int ma)
{
    if(sum>m)return ;
    if(num == n)
    {
        if(sum == m)
        {
            ans+=fun(m)/ma;
        }
        return ;
    }

    int i;
    for(i=0;i<=a[num];i++)
    {
        dfs(num+1,sum+i,ma*fun(i));
    }
}

int main()
{
    int i,j;
    while(~scanf("%d %d",&n,&m))
    {
        for(i=0;i<n;i++)
        {
            scanf("%d",&a[i]);
        }
        ans=0;
        dfs(0,0,1);
        printf("%d\n",ans);
    }
    return 0;
}
```


```c
//1562 Guess the number
#include<iostream>
using namespace std;

int main(){
    int a,b,c,n,i,count;
    cin>> n; 
    while(n--){
        cin>>a>>b>>c;
        count=0; 
        for(i=1000;i<=9999;i++){
            count+=1;
            if(i%a==0&&(i+1)%b==0&&(i+2)%c==0){
                cout<<i<<endl;  
                break;
            } 
        } 
        if(count==9000){
            cout<<"Impossible"<<endl; 
        } 
    } 
}
```

```c
//1708 Fibonacci String
#include <stdio.h>
#include <string.h>
 
int main(){
    int n,k,i,j;
    int a[26],b[26],f[52];
    char s1[52],s2[52];
    scanf("%d",&n);
    while(n--){
        scanf("%s%s%d",s1,s2,&k);
        memset(a,0,sizeof(a));
        memset(b,0,sizeof(b));
        j=strlen(s1);
        for(i=0;i<j;i++)
            a[s1[i]-'a']++;
        j=strlen(s2);
        for(i=0;i<j;i++)
            b[s2[i]-'a']++;
        for(i=0;i<26;i++){
            f[0]=a[i];
            f[1]=b[i];
            for(j=2;j<=k;j++)
                f[j]=f[j-2]+f[j-1];
            printf("%c:%d\n",'a'+i,f[k]);
        }
        printf("\n");
    }
    return 0;
}
```

```c
//1716  排列2
#include<iostream>
#include<algorithm>
using namespace std;
int main()
{
    int a[5],tem;
    cin>>a[1]>>a[2]>>a[3]>>a[4];
    while(a[1]||a[2]||a[3]||a[4])
    {
        sort(a+1,a+5);
        tem=a[1];
        if(tem)
            cout<<a[1]<<a[2]<<a[3]<<a[4];
        while(next_permutation(a+1,a+5))
        {

            int i=1;
            if(a[1])
            {
                if(tem && a[i]==tem)
                    cout<<" ";
                for(i=1; i<=4; i++)
                {
                    if(a[i]!=tem && i==1 && tem)
                        cout<<endl;
                    cout<<a[i];
                }
            }
            tem=a[1];
        }
        cout<<endl;
        cin>>a[1]>>a[2]>>a[3]>>a[4];
        if(a[1]||a[2]||a[3]||a[4])
            cout<<endl;
    }
}
```

```c
//1720 A+B Coming
#include<iostream>
using namespace std;

int main()
{
    int a,b;
    while(cin >> hex >> a >> b)
    {
        cout << dec << a + b << endl;
    }
}
```

```c
//1994 利息计算
#include<stdio.h>
int main()
{
    int t,q;
    double y,e,f,g;
    scanf("%d",&t);
    while(t--)
    {
        scanf("%lf%d%lf%lf%lf",&y,&q,&e,&f,&g);
        double sum1=y*(1+(f*(q+365))/36500);
        double sum2;
        sum2=y*(1+(e*q)/36500);
        sum2=sum2*(1+g/100);
        printf("%.1lf\n%.1lf\n",sum2,sum1);
    }
}
```


```c
//2000 ASCII码排序
#include<iostream>
#include<algorithm>
using namespace std;

int main(){
    char a,b,c,n[3];
    while(cin>>a>>b>>c){
        n[0]=(int)a;
        n[1]=(int)b;
        n[2]=(int)c;
        sort(n,n+3);
        cout<<(char)n[0]<<" "<<(char)n[1]<<" "<<(char)n[2]<<endl;
    }
} 
```

```c
//2001 计算两点间的距离
#include<stdio.h>
#include<stdlib.h>
#include<math.h>

int main(){
    double x1,y1,x2,y2,sum,x,y;
    while(scanf("%lf%lf%lf%lf",&x1,&y1,&x2,&y2)!=EOF){
        sum = 0;
        x = x1-x2;
        y = y1-y2; 
        sum = sqrt(pow(x,2)+pow(y,2));
        printf("%.2lf\n",sum); 
    }
    return 0; 
}
```

```c
//2002 计算球体积
#include<stdio.h>
#include<stdlib.h>
#define PI 3.1415927

int main(){
    double r,v;
    while(scanf("%lf",&r)!=EOF){
        v = 0; 
        v = (4*PI*r*r*r)/3; 
        printf("%.3lf\n",v);
    } 
    return 0; 
} 
```

```c
//2003 求绝对值
#include<stdio.h>
#include<stdlib.h>

int main(){
    double num;
    while(scanf("%lf",&num)!=EOF){
        if(num<0){
            printf("%0.2lf\n",-num); 
        } 
        else{
            printf("%0.2lf\n",num); 
        } 
    } 
    return 0; 
} 
```

```c
//2004 成绩转换
#include<stdio.h>
#include<stdlib.h>

int main(){
    int score;
    while(scanf("%d",&score)!=EOF){
        if(score>100 || score<0){
            printf("Score is error!\n"); 
        } 
        else if(score>=90 && score<=100){
            printf("A\n"); 
        } 
        else if(score>=80 && score<=89){
            printf("B\n"); 
        }
        else if(score>=70 && score<=79){
            printf("C\n"); 
        }
        else if(score>=60 && score<=69){
            printf("D\n"); 
        }
        else if(score>=0 && score<=59){
            printf("E\n"); 
        }
    } 
    return 0; 
}
```

```c
//2005 第几天？
#include<iostream>
using namespace std;

int main(){
    int mdays[]={0,31,28,31,30,31,30,31,31,30,31,30,31};
    int y,m,d,days,i;
    while(scanf("%d/%d/%d",&y,&m,&d)!=EOF){
        days=0; 
        if((y%4==0&&y%100!=0)||y%400==0){
            mdays[2]=29; 
        } 
        else{
            mdays[2]=28; 
        } 
        for(i=1;i<m;i++){
            days+=mdays[i]; 
        } 
        days += d; 
        cout<<days<<endl; 
    } 
}
```

```c
//2006 求奇数的乘积
#include<stdio.h>
#include<stdlib.h>

int main(){
    int n,a[100],sum,i;
    while(scanf("%d",&n)!=EOF){
        sum = 1; 
        for(i=0;i<n;i++){
            scanf("%d",&a[i]); 
        } 
        for(i=0;i<n;i++){
            if(a[i]%2!=0){
                sum *= a[i]; 
            } 
        }
        printf("%d\n",sum); 
    }
    return 0; 
}
```

```c
//2007 平方和与立方和
#include<stdio.h>
#include<stdlib.h>

int main(){
    int m,n,t,i,sum1,sum2;
    while(scanf("%d%d",&m,&n)!=EOF){
        sum1 = 0;
        sum2 = 0; 
        if(n<m){
            t = m;
            m = n;
            n = t; 
        } 
        for(i=m;i<=n;i++){
            if(i%2==0){
                sum1 += i*i; 
            } 
            else{
                sum2 += i*i*i; 
            } 
        } 
        printf("%d %d\n",sum1,sum2); 
    } 
    return 0; 
}
```

```c
//2009 求数列的和
#include<stdio.h>
#include<stdlib.h>
#include<math.h> 

int main(){
    double n,sum;
    int i,m; 
    while(scanf("%lf%d",&n,&m)!=EOF){
        sum = n;
        for(i=1;i<m;i++){
            n = sqrt(n);
            sum += n;
        } 
        printf("%.2lf\n",sum);
    } 
    return 0;
} 
```

```c
//2010 水仙花数
#include<iostream>
using namespace std;

int main(){
    int a,b,i,ge,shi,bai,t; 
    while(cin>>a>>b){
        bool bfind = false;
        bool bfirst = true;
        if(a>b){
            t =a;
            a = b;
            b =t; 
        }
        for(i=a;i<=b;i++){
            ge = i%10;
            shi = i/10%10;
            bai = i/100%10;
            if(ge*ge*ge+shi*shi*shi+bai*bai*bai==i){
                bfind = true; 
                if(!bfirst){
                    cout<<" "<<i; 
                } 
                else{
                    cout<<i;
                    bfirst = false; 
                } 
            } 
        } 
        if(!bfind){
            cout<<"no"; 
        } 
        cout<<endl; 
    } 
}
```

```c
//2011 多项式求和
#include<stdio.h>
#include<stdlib.h>
#include<math.h>

int main(){
    int i,j,m,n[1000];
    float sum;
    scanf("%d",&m);
    for(i=0;i<m;i++){
        scanf("%d",&n[i]);
    }
    for(i=0;i<m;i++){
        sum = 0;
        for(j=1;j<=n[i];j++){
            sum += pow(-1,j+1)*1/j;
        }
        printf("%.2f\n",sum);
    }
    return 0;
}
```

```c
//2016 数据的交换输出
#include<iostream>
#include<algorithm>
using namespace std;

int main(){
    int n,a[1000],i,b[1000],t;
    while(cin>>n && n!=0){
        for(i=0;i<n;i++){
            cin>>a[i];
            b[i]=a[i];
        }
        sort(a,a+n);
        for(i=0;i<n;i++){
            if(a[0]==b[i]){
                t = b[0];
                b[0] = a[0];
                b[i] = t; 
                break;
            }
        }
    for(i=0;i<n;i++){
        if(i!=n-1){
            cout<<b[i]<<" ";
        } 
        else{
            cout<<b[i]; 
        } 
    }
    cout<<endl; 
    a[0]=0;
    b[0]=0;
    }
 return 0;
} 
```

```c
//2017 字符串统计
#include<iostream>
using namespace std;

int main(){
    int n,i,count,l;
    char s[1000];
    cin>>n;
    while(n--){
        count = 0; 
        scanf("%s",&s);
        l = strlen(s); 
        for(i=0;i<l;i++){
            if(s[i]>='0' && s[i]<='9'){
                count+=1; 
            } 
        } 
        cout<<count<<endl;
        s[0] = 0; 
    } 
} 
```

```c
//2018 母牛的故事
#include<iostream>
using namespace std;

int f(int n){
    if(n<=4){
        return n; 
    } 
    return f(n-1)+f(n-3); 
} 

int main(){
    int n;
    while(cin>>n&&n!=0){
        cout<<f(n)<<endl; 
    } 
}
```

```c
//2019 数列有序!
#include<iostream>
#include<algorithm>
using namespace std;

int main(){
    int n,m,i,a[10000];
    while(cin>>n>>m&&n!=0&&m!=0){
        for(i=0;i<n;i++){
            cin>>a[i];
        }
        a[n]=m;
        sort(a,a+n+1);
        for(i=0;i<n+1;i++){
            cout<<a[i];
            if(i!=n){
                cout<<" ";
            }
        }
        cout<<endl;
    }
}
```



```c
//2020 绝对值排序
#include<iostream>
#include<algorithm>
using namespace std;

int com(int a,int b){
    return abs(a)>abs(b);
}

int main(){
    int n,i,a[10000];
    while(cin>>n&&n!=0){
        for(i=0;i<n;i++){
            cin>>a[i];
        } 
        sort(a,a+n,com);
        for(i=0;i<n;i++){
            cout<<a[i];
            if(i!=n-1){
                cout<<" ";
            }
        }
        cout<<endl;
        
    } 
} 
```

```c
//2023 求平均成绩
#include <stdio.h>
#include <string.h>

int main(void)
{
    int n, m;
    int i, j;
    int t, d;
    int s[50];
    int c[5];
    int sc[50][5];

    while (scanf("%d%d", &n, &m) != EOF)
    {
        memset(s, 0, sizeof(s));
        memset(c, 0, sizeof(c));
        memset(sc, 0, sizeof(sc));
        for (i = 0 ; i < n ; i++)
        {
            for (j = 0 ; j < m ; j++)
            {
                scanf("%d", &sc[i][j]);
                c[j] += sc[i][j];
                s[i] += sc[i][j];
            }
        }
        for (i = 0 ; i < n ; i++)
            printf("%.2lf%c", s[i] * 1.0 / m, i < n - 1 ? ' ' : ' \n');
        for (i = 0 ; i < m ; i++)
            printf("%.2lf%c", c[i] * 1.0 / n, i < m - 1 ? ' ' : ' \n');
        for (t = i = 0 ; i < n ; i++)
        {
            for (d = 1, j = 0 ; j < m ; j++)
            {
                if (sc[i][j] < 1.0 * c[j] / n)
                {
                    d = 0;
                    break;
                }
            }
            if (d) t++;
        }
        printf("%d\n\n", t);
    }

    return 0;
}
```

```c
//2029 Palindromes _easy version
#include<iostream>
#include<cstring>
using namespace std;

int main(){
    int n,i,count;
    char a[1000]; 
    cin>>n;
    while(n--){
        count=0; 
        scanf("%s",a);
        for(i=0;i<strlen(a)/2;i++){
            if(a[i]==a[strlen(a)-i-1]){
                count++; 
            } 
        } 
        if(count==strlen(a)/2){
            cout<<"yes"<<endl; 
        } 
        else
        {
            cout<<"no"<<endl; 
         } 
         a[0]=0;
          
         
    } 
}
```

```c
//2032 杨辉三角
#include<iostream>
using namespace std;

int main(){
    int n,a[100][100],i,j;
    while(cin>>n){ 
        for(i=0;i<n;i++){
            a[i][0]=1; 
        } 
        /*------*/
        for(i=1;i<n;i++){
            for(j=1;j<n;j++){
                a[i][j]=a[i-1][j]+a[i-1][j-1]; 
            } 
        }
        /*------*/ 
        for(i=0;i<n;i++){
            for(j=0;j<=i;j++){
                cout<<a[i][j];
                if(j!=i){
                    cout<<" "; 
                } 
            } 
            cout<<endl; 
        }
        cout<<endl; 
    } 
} 
```

```c
//2033 人见人爱A+B
#include<iostream>
using namespace std;

int main(){
    int c,i,a[1000],m,n,p;
    cin>>c;
    while(c--){
        for(i=0;i<6;i++){
            cin>>a[i]; 
        } 
        m = (a[2]+a[5])%60; //秒 
        n = ((a[1]+a[4])+(a[2]+a[5])/60)%60; //分 
        p = ((a[0]+a[3])+(a[1]+a[4]+(a[2]+a[5])/60)/60); //时 
        cout<<p<<" "<<n<<" "<<m<<endl;  
    } 
}
```

```c
//2084 数塔
#include<iostream>
using namespace std;

int main(){
    int a[200][200],i,j,t,n;
    cin>>t;
    while(t--){
        cin>>n;
        for(i=1;i<=n;i++){
            for(j=1;j<=i;j++){
                cin>>a[i][j]; 
            } 
        } 
        for(i=n;i>=1;i--){
            for(j=1;j<=i;j++){
                if(a[i+1][j]>=a[i+1][j+1]){
                    a[i][j] += a[i+1][j];  
                } 
                else{
                    a[i][j]+=a[i+1][j+1]; 
                } 
            } 
        } 
        cout<<a[1][1]<<endl; 
    } 
}
```

```c
//2096 小明A+B
#include<iostream>
using namespace std;

int main(){
    int a,b,c,m,n,p,q,r,s,sum,u,v,sumi;
    cin>>c;
    while(c--){
        cin>>a>>b;
        m = a%10;
        n = a/10%10;
        p = b%10;
        q = b/10%10;
        r = m*1+n*10;
        s = p*1+q*10;
        sum = r +s;
        u = sum%10;
        v = sum/10%10;
        sumi = u*1+v*10;
        cout<<sumi<<endl; 
    } 
     
} 
```

```c
//3782 xxx定律
#include<iostream>
using namespace std;

int main(){
    int n,count;
    while(cin>>n&&n!=0){
        count = 0;
        while(1){
            if(n==1){
                break;
            }
            if(n%2==0){
                n = n/2;
                count++;
            }
            else{
                n = (3*n+1)/2;
                count++;
            }
    }
    cout<<count<<endl;
        
        
    }
}
```

```c
//1282 回文数猜想
#include<iostream>
using namespace std;

int fun(int num)
{
    int sum = 0;
    while(num)
    {
        sum+=num%10;
        num/=10;
        if(num)
            sum*=10;
    }
    return sum;
}
int main()
{
    int num;
    int a[65535];
    while(scanf("%d",&num)!=EOF)
    {
        int j = 0;
        a[j] = num;
        while(num!=fun(num))
        {
            j++;
            a[j] = num+fun(num);
            num = a[j];
        }
       cout<<j<<endl;
        for(int i=0;i<j;i++)
        {
            cout<<a[i]<<"--->";
 
        }
        cout<<a[j]<<endl;
    }
    return 0;
}
```