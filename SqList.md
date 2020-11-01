### 顺序表

##### 结构体定义
```c++
#define MAXSIZE 100
#define OK 1
#define ERROR 0

typedef ElemType int;
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
    L.elem = (ElemType *) malloc (MAXSIZE * sizeof (ElemType));
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
    for (int i = 1 ; i < L.Length/2 ; i++){
        t = L.elem[L.Length - i];
        L.elem[L.Length - i] = L.elem[i -1];
        L.elem[i - 1] = t;
    }
    return OK;
}
```

##### 合并(三表)
```c++
Status Merge_SqList(SqList LA, SqList LB, SqList &LC){
    Init_SqList(LC);
    int i = j = 1, k = 0;
    if(LA.Length == 0 && LB.Length == 0) return ERROR;
    while(i <= LA.Length && j <= LB.Length){
        GetElem(LA, i, ea);
        GetElem(LB, j, eb);
        if(ea <= eb) {
            Insert_SqList(LC, k++, ea);
            i++;
        }else{
            Insert_SqList(LC, k++, eb);
            j++;
        }
    }
    while(i <= LA.Length){
        GetElem(LA, i++, ea);
        Insert_SqList(LC, k++, ea);
    }
    while(j <= LB.Length){
        GetElem(LB, i++, eb);
        Insert_SqList(LC, k++, eb);
    }
    return OK;
}
```

##### 删除相同元素的值
```c++
Status Delete_E_SqList(SqList &L, ElemType e){
    if(L.Length == 0) return ERROR;
    int count = 0;
    for(int i = 0; i < L.Length; i++){
        if(L.elem[i] != x){
            L.elem[count] = L.elem[i];
            count++;
        }
        L.length = count;
    }
}

Status Delete_E_SqList(SqList &L, ElemType e){
    if(L.Length == 0) return ERROR;
    int count = 0;
    for(int i = 0; i < L.Length; i++){
        if(L.elem[i] == e){
            count++;
        } else {
            L.elem[i - count - 1] = L.elem[i - 1];
        }
        L.Length = L.Length - count;

    }
}
```

##### 删除给定区间的元素
```c++
Status Delete_mn_SqList(SqList &L, ElemType m, ElemType n){
    int i, k = 0;
    if(L.Length == 0 || m >= n) return ERROR;
    for(i = 0 ; i < L.Length ; i++){
        if(L.elem[i] >= m && L.elem[i] <= n){
            k++;
        } else {
            L.elem[i - k] = L.elem[i];
        }
    }
    L.Length -= k;
    return OK;
}
```
##### 有序顺序表去重
```c++
Status Delete_Same_SqList(SqList &L, ElemType e){
    if(L.Length == 0) return ERROR;
    int i, j;
    for(i = 0 , j = 1; j < L.Length; j++){
        if(L.elem[i] != L.elem[j]){
            L.elem[++i] = L.elem[j];
        }
    }
    L.Length = i + 1;
    return OK;
}
```