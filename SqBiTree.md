### 二叉树

##### 结构体定义
```c++
#define OK 1
#define ERROR 0
#define OVERFLOW -2

typedef char TElemType;
typedef int Status;

typedef struct BiTNode{
    TElemType data;
    struct BiTNode *lchild, *rchild;
}BiTNode, *BiTree;
```

##### 先序创建二叉树
```c++
Status CreateBiTree(BiTree &T){
    char ch;
    ch = getchar();
    if (ch == ' '){
        T = NULL;
    }else{
        T = (BiTNode *) malloc (sizeof(BiTNode));
        if(!T) exit(OVERFLOW);
        T->data = ch;
        CreateBiTree(T->lchild);
        CreateBiTree(T->rchild);
    }
    return OK;
}
```
##### 获取叶子结点
```c++
Status GetLeaf(BiTree T){
    int count;
    if(T == NULL){
        count = 0;
    }else if(T->lchild == NULL && T->rchild == NULL){
        count = 1;
    }else{
        count = GetLeaf(T->lchild) + GetLeaf(T->rchild);
    }
    return count;
}
```

##### 获取二叉树深度
```c++
Status GetDeep(BiTree T){
    if(T == NULL){
        return 0;
    }
    int l = GetDeep(T->lchild);
    int r = GetDeep(T->rchild);
    return l >= r ? l + 1 : r + 1;
}
```

##### 前序遍历
```c++
Status PreOrderTraverse(BiTree T, int deep){
    static int prel = GetDeep(T);
    if(T == NULL){
        return ERROR;
    }
    cout << " " << T->data << endl;
    PreOrderTraverse(T->lchild , deep + 1);
    PreOrderTraverse(T->rchild , deep + 1);
    return OK;
}
```

##### 中序遍历
```c++
Status InOrderTraverse(BiTree T, int deep){
    static int inl = GetDeep(T);
    if(T == NULL){
        return ERROR;
    }
    InOrderTraverse(T->lchild , deep + 1);
    cout << " " << T->data << endl;
    InOrderTraverse(T->rchild , deep + 1);
    return OK;
}
```

##### 后续遍历
```c++
Status PostOrderTraverse(BiTree T, int deep){
    static int pol = GetDeep(T);
    if(T == NULL){
        return ERROR;
    }
    PostOrderTraverse(T->lchild , deep + 1);
    PostOrderTraverse(T->rchild , deep + 1);
    cout << " " << T->data << endl;
    return OK;
}
```

##### 交换子树
```c++
Status ExChangeTree(BiTree &T){
    BiTNode *p;
    if(T != NULL){
        p = T->lchild;
        T->lchild = T->rchild;
        T->rchild = p;
        ExChangeTree(T->lchild);
        ExChangeTree(T->rchild);
    }
}
```