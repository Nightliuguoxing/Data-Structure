### 顺序队列

##### 结构体定义

```c++
#define MAXQSIZE 100
#define ERROR 0
#define OK 1
#define TRUE true
#define FALSE false
typedef int Status;
typedef int QElemType;

typedef struct {
    QElemType *base;
    int front;
    int rear;
} SqQueue;
```

##### 判空

```c++
bool IsEmpty(SqQueue Q) {
    if (Q.rear == Q.front) return TRUE;
    return FALSE;
}
```

##### 判满

```c++
bool IsFull(SqQueue Q) {
    if ((Q.rear + 1) % MAXQSIZE == Q.front) return TRUE;
    return FALSE;
}
```

##### 初始化

```c++
Status InitQueue(SqQueue &Q) {
    Q.base = (QElemType *) malloc(MAXQSIZE * sizeof(QElemType));
    if (!Q.base) return ERROR;
    Q.front = Q.rear = 0;
    return OK;
}
```

##### 获取长度

```c++
Status GetLength(SqQueue Q) {
    if (Q.rear == Q.front) return OK;
    int length = (Q.rear - Q.front + MAXQSIZE) % MAXQSIZE;
    return OK;
}
```

##### 获取队头元素

```c++
Status GetHead(SqQueue Q){
    if (IsEmpty(Q)) return ERROR;
    QElemType e = Q.base[Q.front];
    return OK;
}
```

##### 入队

```c++
Status EnQueue(SqQueue &Q, QElemType e) {
    if (IsFull(Q)) return ERROR;
    Q.base[Q.rear] = e;
    Q.rear = (Q.rear + 1) % MAXQSIZE;
    return OK;
}
```

##### 出队

```c++
Status DeQueue(SqQueue &Q) {
    if (IsEmpty(Q)) return ERROR;
    QElemType e = Q.base[Q.front];
    Q.front = (Q.front + 1) % MAXQSIZE;
    return OK;
}
```

##### 置空

```c++
Status SetEmpty(SqQueue &Q) {
    Q.rear = Q.front = 0;
    return OK;
}
```

##### 销毁

```c++
Status DestoryQueue(SqQueue &Q) {
    if (Q.base) {
        free(Q.base);
    }
    Q.base = 0;
    Q.rear = Q.front = 0;
    return OK;
}
```

##### 遍历

```c++
Status Traverse(SqQueue Q) {
    if(IsEmpty(Q)) return ERROR;
    while (Q.front != Q.rear) {
        cout << Q.base[Q.front] << " ";
        Q.front = (Q.front + 1) % MAXQSIZE;
    }
    cout << endl;
    return OK;
}
```
