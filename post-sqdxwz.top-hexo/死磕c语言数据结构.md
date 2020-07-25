---
title: 死磕c语言数据结构
date: 2019-10-13 08:44:17
thumbnail: https://i.loli.net/2019/10/13/k2NlQ89ZM6rbaAB.png
tags: 数据结构
categories: 死磕系列
---

**持续更新...**

<!--more-->

# 一、排序

## 1.冒泡排序

```c
#include<stdio.h>
#include<stdlib.h>

int main(){
	int n,i,j,a[100],temp;
	scanf("%d",&n);//输入的数字个数
	for(i=0;i<n;i++){
		scanf("%d",&a[i]); //输入 
	} 
	//冒泡排序 
	for(i=0;i<n;i++){
		for(j=0;j<n-i;j++){
			if(a[j]<a[j+1]){
				temp = a[j];
				a[j] = a[j+1];
				a[j+1] = temp; 
			} 
		} 
	} 
	for(i=0;i<n;i++){
		printf("%d ",a[i]); //输出 
	} 
	return 0; 
} 
```

## 2.桶排序

```c
#include<stdio.h>
#include<stdlib.h>

int main(){
	int n,m,i,j,a[100];
	scanf("%d",&n);
	for(i=0;i<100;i++){
		a[i] = 0;
	}
	for(i=0;i<n;i++){
		scanf("%d",&m);
		a[m]++;
	}
	for(i=0;i<100;i++){
		for(j=0;j<a[i];j++){
			printf("%d ",i);
		}
	}
	return 0;
} 
```

## 3.快速排序

```html
为什么说  叫快速排序，顾名思义， 排序的速度很快。
它的核心思想就是将 最左的数字 记为 基准值
举个例子  假如
6    1   2   7   9   3   4   5   10  8
首先 定下 6为基准值接下来 想达到的目的是 6放在中间 左边都是小于6的右边都是大于6的
从左到右找到 比6大的有  第一个为7
同样从右到左 找到 比6小的 第一个数为 5
两个交换 得到
6    1   2   5   9   3   4   7   10  8
同理 得到
6    1   2   5   4   3   9   7   10  8
将6送到中间去
3    1   2   5   4   6   9   7   10  8
得到之前的目的了把
之后  6的左边 3 1 2 5 4 重复上述的方法 进行 排序（相当于把这五个数看做 一个新的排序将 3 设为基准）
右边 的9 7 10 8 同样
变化过程如下：
3    1   2   5   4
2    1   3   5   4

9    7   10  8
9    7   8   10
8    7   9   10

之后  基准值进入中间区域之后  依次进行以上操作 （其实就是个 递归操作）

最后得到1    2   3   4   5   6   7   8   9   10
上代码
```

```c
#include <stdio.h>
#include <stdlib.h>

int number[101];
int n;

void quickSort(int left, int right)
{
     int baseNumber;// 基准值初始化 
     int i;
     int j;
     int t;
     if (left > right) // 向右找数 和向左找数 碰到 则结束 找数 
     {
         return;
     }
     baseNumber = number[left];  // 记住基准值 
     i = left;
     j = right;
     while(i != j)
     {
          //  顺序很重要要先从右向左找 
          while((number[j] >= baseNumber)&&(i<j))
          {
               j--;
          }
          //   从左向右找 
          while((number[i] <= baseNumber)&&(i<j))
          {
               i++; 
          } 
          //  左右 找数没有碰到 
          if(i<j)
          {
              //  比基准值大的数和基准值小的数  交换 
              t = number[i];
              number[i] = number[j];
              number[j] = t;       
          }

    }
     // while结束 则  i = j  则 到 中间 所以此时的i为中间的索引  
     // 中间数字  和  基准值交换  
      number[left] = number[i];
      number[i] = baseNumber;

      //递归   左面的 继续 sort   右边的同理 
      quickSort(left, i-1);
      quickSort(i+1, right); 
      return ;
}

int main(int argc, char *argv[])
{
    int  i, j;
    scanf("%d",&n);
    for(i=1 ;i<=n; i++)
    {
        scanf("%d",&number[i]);
    }
    quickSort(1,n);
    for(i =1; i<=n; i++)
    {
        printf("%d   ",number[i]);         
    }
     system("PAUSE");    
}
```

python版的排序：https://zzdproject.netlify.com/#/sort

# 二、队列、栈、链表


## 1.队列

```c
队列顾名思义就像一群数字排成一个队列一样的性质
所以它的最标志性性质就是  FIFO(First In First Out) "先进先出"

这里规定 加入 队列数据为一个数组
head指向第一个数字 tail指向 最后一个数字的下一个，这样是为了 NULL的操作判定

只允许 在队列的头部（head）进行删除----出队
只允许在队列的尾部（tail）进行插入---- 入队
队列为 NULL时  head = tail
删除一个数据 则  head++;
插入一个数据则  q[tail] = data; tail++;
```

```c
#include <stdio.h>
#include <stdlib.h>

struct queue
{
int data[100];
int head;
int tail;       
}; // ;别忘了

int main()
{
    struct queue q;//  有struct
    int i;
    // 此时为NULL 
    q.head = 1;
    q.tail = 1;
    for(i=1; i<=9; i++)
    {
         //   插入 
        scanf("%d",&q.data[q.tail]);
        q.tail++;         
    }
    while(q.head < q.tail)
    {
        printf("%d ",q.data[q.head]);
        q.head++;
        //  插入 
        q.data[q.tail] = q.data[q.head];
        q.tail++;
        //删除 
        q.head++;
    }
    return 0;
}
```

## 2.栈

```html
它的最标志性性质就是  LIFO(Last In First Out) "后进先出"
1.一个数组+一个指向栈顶的变量top即可。
2.top=0  为NULL
3.进栈为 top++; s[top] = data
4.出栈为 top--；
以回文数 为例子
```


```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    char a[101]; // 回文数 
    char stack[101]; //栈 
    int i;
    int len, mid, top, next; 
    gets(a); //得到字符串 
    len = strlen(a); //得到长度 
    mid = len/2 - 1; //中点 
    top = 0; // 栈顶指向 
    for(i=0; i<=mid; i++)
    {
        stack[++top] = a[i]; //入栈 
    }
    //判断数字长度为奇数还是偶数 
    if(len%2==0)
    {
        next = mid + 1;
    }else{
        next = mid + 2;      
    }
    // 判断是否为回文数 
    for(i=next; i<=len-1; i++)
    {
        if(a[i] != stack[top])
          break;
        top--;
    }
    //  top = 0 相当于 全部出栈 即 为回文数 
    if(top == 0)
    {
        printf("我觉得ok"); 
    }else{
        printf("我觉得不行");
    } 

    return 0;  
}
```

## 3.链表

```c
//输入输出操作
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
//节点结构体 
struct node
{
   int data;
   struct node *next;
};

int main()
{    
     struct node *head, *p, *q, *t;
     int i,n,data_input;
     scanf("%d",&n);// 输入 数据的个数 
     head = NULL; //头结点 
     for(i=1; i<=n; i++)
     {
         scanf("%d",&data_input);
         //动态申请一个空间，用来存放一个结点，并用临时指针p指向这个结点 
         p = (struct node *)malloc(sizeof(struct node));
         p->data = data_input;// 将数据存储到当前 结点的 data中 
         p->next = NULL;//设置当前的结点 的后继指针为NULL，也就是当前结点的下一个结点为NULL 
         if(head==NULL)
         {
             head = p; // 如果这个是第一个 创建的结点  则将 这个头指针指向这个结点 
         }else{
             q->next = p;//如果不是第一个创建的结点，则将上一个结点的后继指针指向当前结点 
         }
         q = p;//q也指向当前结点 
     }  

     t = head;
     while(t!=NULL)
	{
         printf("%d ",t->data); //输出所有的数 
         t = t->next; 
     }
     return 0;  
}
```

```c
//插入操作
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
//节点结构体 
struct node
{
   int data;
   struct node *next;
};

int main()
{    
     struct node *head, *p, *q, *t;
     int i,n,data_input;
     int data_insert;
     scanf("%d",&n);// 输入 数据的个数 
     head = NULL; //头结点 
     for(i=1; i<=n; i++)
     {
         scanf("%d",&data_input);
         //动态申请一个空间，用来存放一个结点，并用临时指针p指向这个结点 
         p = (struct node *)malloc(sizeof(struct node));
         p->data = data_input;// 将数据存储到当前 结点的 data中 
         p->next = NULL;//设置当前的结点 的后继指针为NULL，也就是当前结点的下一个结点为NULL 
         if(head==NULL)
         {
             head = p; // 如果这个是第一个 创建的结点  则将 这个头指针指向这个结点 
         }else{
             q->next = p;//如果不是第一个创建的结点，则将上一个结点的后继指针指向当前结点 
         }
         q = p;//q也指向当前结点 
     }  

     //************** 插入操作**********************//
     scanf("%d",&data_insert); //  输入插入的值 
     t = head;  //  链表头 
     while(t!=NULL) 
     {
          // 如果 当前结点 是最后一个结点或者下一个结点 的值大于 插入数的时候插入 
         if((t->next==NULL)||(t->next->data >data_insert))
         {
              // 创建 缓存 
              p = (struct node *)malloc(sizeof(struct node));
              p->data = data_insert;
              p->next = t->next;// 新增结点的后继指针  等于 此时结点的后继结点的指向  即 新增结点 指向 此时结点的下一个指向 
              // 此时结点的后继指针指向  这个新增结点 
              t->next = p;
              break;
         }
         //继续下一个结点（相当于遍历） 
         t = t->next;
     }

     t = head;
     while(t!=NULL)
     {
         printf("%d ",t->data);
         t = t->next;
     }
     return 0;  
}
```



