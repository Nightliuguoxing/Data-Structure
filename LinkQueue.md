### 链队列

##### 结构体定义

```c++
#define ERROR 0
#define OK 1

typedef int QElemType;
typedef int Status;

typedef struct QNode {
    QElemType data;
    struct QNode *next;
} QNode, *QueuePtr;

typedef struct {
    QueuePtr front;
    QueuePtr rear;
} LinkQueue;
```

##### 初始化

```c++
Status InitQueue(LinkQueue &Q) {
    Q.front = Q.rear = (QueuePtr) malloc(sizeof(QNode));
    if (!Q.front) return ERROR;
    Q.front->next = NULL;
    return OK;
}
```

##### 销毁

```c++
Status DestoryQueue(LinkQueue &Q) {
    while (Q.front) {
        Q.rear = Q.front->next;
        free(Q.front);
        Q.front = Q.rear;
    }
    return OK;
}
```

##### 入队

```c++
Status EnQueue(LinkQueue &Q, QElemType e) {
    QueuePtr p = (QueuePtr) malloc(sizeof(QNode));
    if (!p) return ERROR;
    p->data = e;
    p->next = NULL;
    Q.rear->next = p;
    Q.rear = p;
    return OK;
}
```

##### 出队

```c++
Status DeQueue(LinkQueue &Q) {
    if (Q.rear == Q.front) return ERROR;
    QueuePtr p = Q.front->next;
    QElemType e = p->data;
    Q.front->next = p->next;
    if (Q.rear == Q.front) Q.rear = Q.front;
    free(p);
    return OK;
}
```

##### 获取头队列元素

```c++
Status GetHead(LinkQueue Q) {
    if (Q.rear == Q.front) return ERROR;
    QElemType e = Q.front->next->data;
    return OK;
}
```

##### 清空

```c++
Status SetEmpty(LinkQueue &Q) {
    if (Q.rear == Q.front) return OK;
    Q.front = Q.rear;
    Q.rear->next = NULL;
    return OK;
}
```

##### 判空

```c++
Status IsEmpty(LinkQueue Q) {
    if (Q.rear == Q.front) return OK;
    return ERROR;
}
```

##### 获取队列长度

```c++
Status GetLength(LinkQueue Q) {
    int length = 0, count = 0;
    if(Q.rear == Q.front) return count;
    QNode *s;
    s = Q.front->next;
    while (s!=NULL){
        count++;
        s = s->next;
    }
    return length;
}
```

##### 遍历

```c++
Status Traverse(LinkQueue Q) {
    if (Q.rear == Q.front) return ERROR;
    QNode *s;
    QElemType e;
    s = Q.front->next;
    while (s) {
        e = s->data;
        s = s->next;
    }
    return OK;
}
```
