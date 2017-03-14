---
layout: post
title: "02-线性结构1 两个有序链表序列的合并"
date: 2017-03-14 20:36:21 +0800
comments: true
categories: begin again
---

本题要求实现一个函数，将两个链表表示的递增整数序列合并为一个非递减的整数序列。

```C
#include <stdio.h>
#include <stdlib.h>

typedef int ElementType;
typedef struct Node *PtrToNode;
struct Node {
    ElementType Data;
    PtrToNode   Next;
};
typedef PtrToNode List;

List Read(); /* 细节在此不表 */
void Print( List L ); /* 细节在此不表；空链表将输出NULL */

List Merge( List L1, List L2 );

int main()
{
    List L1, L2, L;
    L1 = Read();
    L2 = Read();
    L = Merge(L1, L2);
    Print(L);
    Print(L1);
    Print(L2);
    return 0;
}

/* 你的代码将被嵌在这里 */
```

输入样例：

```
3
1 3 5
5
2 4 6 8 10
```

输出样例：

```
1 2 3 4 5 6 8 10 
NULL
NULL
```



样例代码：

```C
#include<stdio.h>
#include<stdlib.h>
typedef int ElementType;
typedef struct Node *PtrToNode; //定义新类型，名字为PtrToNode，类型为指向Node结构体的指针
struct Node{
    ElementType Data;
    PtrToNode Next;
};
typedef PtrToNode List; //❤️定义一个链表，存储的数据格式是Node结构体，名字为List

List Read();
void Print(List L);	//注意括号里带参数的数据类型
List Merge(List L1, List L2);

int main(){
    List L1, L2, L;
    L1 = Read();
    L2 = Read();
    L = Merge(L1, L2);
    Print(L);
    Print(L1);
    Print(L2);
    
    return 0;
}
List Merge(List L1, List L2){
    List r;
    PtrToNode L = (PtrToNode)malloc(sizeof(struct Node));	//malloc出struct Node大小的空间，类型转换为PtrToNode，❤️这是头指针
    List p = L1->Next;
    List q = L2->Next;
    r = L;
    L->Next = NULL;
    while (p != NULL && q != NULL) {
        if (p->Data < q->Data) {
            r->Next = p;
            p = p->Next;
            r = r->Next;
        }
        else{
            r->Next = q;
            q = q->Next;
            r = r->Next;
        }
    }
    r->Next = NULL;
    if (p != NULL) {
        r->Next = p;
    }
    if (q != NULL) {
        r->Next = q;
    }
    L1->Next = NULL;
    L2->Next = NULL;
    return L;
}
List Read(){
    int len = 0;
    int num = 0;
    PtrToNode h = NULL;
    PtrToNode last = NULL;
    
    scanf("%d", &len);
    if(len == 0){
        return NULL;
    }
    h = (PtrToNode)malloc(sizeof(struct Node));
    h->Next = NULL;
    last = h;
    while(len){
        scanf("%d", &num);
        PtrToNode node = (PtrToNode)malloc(sizeof(struct Node));
        node->Data = num;
        node->Next = NULL;
        last->Next = node;
        last = node;
        len--;
    }
    return h;
}
void Print(List L){
    if (L->Next == NULL) {
        printf("NULL\n");
        return ;
    }
    L = L->Next;
    while (L != NULL) {
        printf("%d ", L->Data);
        L = L->Next;
    }
    putchar('\n');
}

```