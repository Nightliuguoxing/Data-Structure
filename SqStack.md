### 顺序栈

##### 结构体定义
```c++
#define MAXSIZE 10
#define OK 1
#define ERROR 0
#define TRUE 1
#define FALSE 0
typedef int SElemType;
typedef int Status;

typedef struct {
    SElemType *base;
    SElemType *top;
    int stackSize;
    int length = -1;
} SqStack;
```

##### 初始化
```c++
Status InitStack(SqStack &s) {
    s.base = (SElemType *) malloc(MAXSIZE * sizeof(SElemType));
    if (!s.base) return ERROR;
    s.top = s.base;
    s.stackSize = MAXSIZE;
    s.length = 0;
    return OK;
}
```
##### 判空
```c++
Status IsEmpty(SqStack s) {
    if (s.top == s.base)
        return TRUE;
    else
        return FALSE;
}
```
##### 判满
```c++
Status IsFull(SqStack s) {
    if (s.top - s.base >= s.stackSize)
        return TRUE;
    else
        return FALSE;
}
```
##### 入栈
```c++
Status Push(SqStack &s, SElemType e) {
    if (IsFull(s)) {
        if(!s.base) return ERROR;
        return ERROR;
    } else {
        *s.top = e;
        s.top++;
        s.length++;
        return OK;
    }
}
```
##### 出栈
```c++
Status Pop(SqStack &s, SElemType &e) {
    if (IsEmpty(s)) {
        if(!s.base) return ERROR;
        return ERROR;
    } else {
        e = *(--s.top);
        s.length--;
        return OK;
    }
}
```
##### 获取栈顶元素
```c++
Status GetTop(SqStack s, SElemType &e) {
    if (IsEmpty(s)) {
        return ERROR;
    } else {
        e = *(s.top - 1);
        return OK;
    }
}
```
##### 置空
```c++
Status SetEmpty(SqStack &s) {
    if (s.base) {
        s.top = s.base;
        s.length = 0;
        return OK;
    } else {
        return ERROR;
    }
}
```
##### 销毁
```c++
Status DestoryStack(SqStack &s) {
    if (s.base) {
        free(s.base);
        s.base = NULL;
        s.top = NULL;
        s.stackSize = 0;
        s.length = -1;
        return OK;
    } else {
        return ERROR;
    }
}
```
##### 遍历
```c++
Status visit(SElemType e) {
    cout << e << "  ";
    return true;
}

Status Traverse(SqStack s) {
    if (IsEmpty(s)) {
        if(!s.base) return ERROR;
    }
    while (!IsEmpty(s)){
        visit(*(--s.top));
    }
    cout << endl;
    return OK;
}
```