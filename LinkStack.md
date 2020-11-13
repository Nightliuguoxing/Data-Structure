### 链栈(未完成)

##### 结构体定义

```c++
typedef int ElemType;
typedef bool Status;
typedef true TRUE;
typedef false FALSE;

typedef struct SNode{
    ElemType data;
    struct SNode *next;
    int length;
}SNode, *LinkStack;
```

##### 初始化

```c++
Status InitLinkStack(LinkStack &S){
    S = NULL;
    S->length = 0;
    if(S->length == 0) return TRUE;
    return FALSE;
}
```
