### 顺序表

##### 结构体定义
```c
#define MAXSIZE 100
#define OK 1
#define ERROR 0

typedef Elemtype int;
typedef Status int;

typedef struct {
    ElemType *elem;
    int Length;
    int ListSize;
}SqList;
```

##### 初始化
```c++
Status Init_SqList(SqList &L){
    L.elem = (Elemtype *) malloc (MAXSIZE * sizeof (ElemType));
    if(!L.elem) return ERROR;
    L.Length = 0;
    L.ListSize = MAXSIZE;
    return OK;
}
```

##### 插入
```c++
Status Insert_SqList(SqList &L, int i, ElemType e){
    if(i < 1 || i > L.Length + 1) return ERROR;
    if(L.Length >= MAXSIZE) return ERROR;
    for(int n = L.Length - 1; n >= i - 1; n--){
        L.elem[n + 1] = L.elem[n];
    }
    L.elem[i - 1] = e;
    ++L.Length;
    return OK;
}
```

##### 删除
```c++
Status Delete_SqList(SqList &L, int i, ElemType &e){
    if(i < 1 || i > L.Length) return ERROR;
    if(L.Length <= 0) return ERROR;
    e = L.elem[i - 1];
    for(int n = i; n <= L.Length - 1 ; n++){
        L.elem[n - 1] = L.elem[n];
    }
    --L.Length;
    return OK;
}
```

##### 遍历
```c++
Status Traverse_SqList(SqList L){
    if(L.Length <= 0) return ERROR;
    for(int i = 0 ; i < L.Length ; i++){
        cout << L.elem[i] << " ";
    }
    return OK;
}
```

##### 逆置
```c++
Status Inversion_SqList(SqList &L){
    if(L.Length <= 0) return ERROR;
    ElemType t;
    for (int i = 1 ; i <= L.Length/2 ; i++){
        t = L.elem[L.Length - i];
        L.elem[L.Length - i] = L.elem[i -1];
        L.elem[i - 1] = t;
    }
    return OK;
}
```

##### 合并(1)
```c++
Status Merge_SqList(SqList LA, SqList LB, SqList &LC){
    Init_SqList(LC);
    int i = j = 1, k = 0;
    
}
```

##### 合并(2)
```c++
Status Merge_SqList(SqList LA, SqList LB){
    
}
```