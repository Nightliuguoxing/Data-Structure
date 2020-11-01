### 链表

##### 结构体定义
```c++
#define MAXSIZE 100
#define OK 1
#define ERROR 0

typedef ElemType int;
typedef Status int;

typedef struct LNode{
    ElemType data;
    struct LNode *next;
}LNode, *LinkList;
```

##### 初始化
```c++
Status Init_LinkList(LinkList &L){
    L = (LinkList) malloc (sizeof(LNode));
    L->next = NULL;
    return OK;
}
```

##### 头插法
```c++
Status HeadInsert_LinkList(LinkList &L, int n){
    LNode p;
    for(int i = 0 ; i < n ; i++){
        p = (LNode *) malloc (sizeof(LNode));
        if(!p) return ERROR;
        cin >> p->date;
        p->next = L->next;
        L->next = p;
    }
    return OK;
}
```

##### 尾插法
```c++
Status TailInsert_LinkList(LinkList &L, int n){
    LNode p;
    LinkList q = L;
    for(int i = 0 ; i < n ; i++){
        p = (LNode *) malloc (sizeof(LNode));
        if(!p) return ERROR;
        cin >> p->data;
        p->next = q->next;
        q->next = p;
        q = q->next;
    }
    return OK;
}
```

##### 遍历
```c++
Status Traverse_LinkList(LinkList L){
    LNode *p;
    p = L->next;
    if(p == NULL) return ERROR;
    while(p!=NULL){
        cout << p->data << endl;
        p = p->next;
    }
    return OK;
}
```

##### 按序号查找结点值
```c++
Status GetElem_LinkList(LinkList L, int i){
    int j = 0;
    LNode *p = L;
    if(i == 0) {
        cout << "NULL";
        return OK;
    }
    while(p && j < i ){
        p = p->next;
        j++;
    } 
    cout << p->data;
    return OK; 
}
```

###### 按值查找结点
```c++
Status LocateElem_LinkList(LinkList L, ElemType e){
    int i = 0;
    LNode *p = L;
    while(p != NULL && p->data != e){
        p = p->next;
        // FIXME
        i++;
    }
    cout << i ;
    return OK;
}
```

##### 前插
```c++
Status Insert_LinkList(LinkList &L, int i, ElemType e){
    LNode *p = L, *s;
    int k = 0;
    while(p && k < i - 1){
        p = p->next;
        k++;
    }
    if(!p || k < i - 1) return ERROR;
    s = (LNode *) malloc (sizeof(LNode));
    s->data = e;
    s->next = p->next;
    p->next = s;
    return OK;
}
```

##### 删除(位置)
```c++
Status Delete_LinkList(LinkList &L, int i){
    LNode *p = L, *q;
    int k = 0;
    while(p->next && k < i - 1){
        p = p->next;
        k++;
    }
    if(!(p->next) || k < i - 1) return ERROR;
    q = p->next;
    p->next = q->next;
    cout << q->data << " ";
    free(q);
    return OK;
}
```

##### 逆序
```c++
Status Inversion_LinkList(LinkList &L){
    LNode *p , *q;
    p = L->next;
    L->next = NULL;
    while(p != NULL){
       q = p;
       p = p->next;
       q->next = L->next;
       L->next = q;
    } 
    return OK;
}

Status Inversion_T_LinkList(LinkList &L){
    LNode *p , *r, *pre;
    p = L->next;
    r = p->next;
    p->next = NULL;
    while(r != NULL){
       pre = p;
       p = r;
       r = r->next;
       p->next = pre;
    } 
    L->next = p;
    return OK;
}
```

##### 删除相同元素的值
```c++
Status Delete_E_LinkList(LinkList &L, ElemType e){
   LNode *p = L->next , *pre = L, *q;
   while(p != NULL){
       if(p->data == e){
           q = p;
           p = p->next;
           pre->next = p;
           free(q);
       }else{
           pre = p;
           p = p->next;
       }
   }
   return OK;
}

Status Delete_E_LinkList(LinkList &L, ElemType e){
    LNode *p = L->next, *r = L, *q;
    while(p != NULL){
        if(p->data != e){
            r->next = p;
            r = p;
            p = p->next;
        }else{
            q = p;
            p = p->next;
            free(q);
        }
        r->next = NULL;
    }
    return OK;
}
```

##### 合并有序顺序表(递增)
```c++
Status Merge_LinkList(LinkList &LA, LinkList &LB, LinkList &LC){
    LNode *pa = LA->next, *pb = LB->next, *pc, *q;
    LC = pc = LA;
    while(pa && pb){
        if(pa->data < pb->data){
            pc->next = pa;
            pc = pa;
            pa = pa->next;
        }else if (pa->data > pb->data){
            pc->next = pb;
            pc = pb;
            pb = pb->next;
        }else{
            pc->next = pa;
            pc = pa;
            pa = pa->next;
            q = pb;
            pb = pb->next;
            free(q);
        }
    }
    pc->next=pa?pa:pb;
    free(LB);
    return OK;
}
```
