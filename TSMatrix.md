### 压缩矩阵

##### 结构体定义

```c++
#define MAXSIZE 12500
#define TRUE true
#define FALSE false

typedef int ElemType;
typedef bool Status;

typedef struct {
    int i, j;
    ElemType e;
}Triple;

typedef struct {
    Triple data[MAXSIZE + 1];
    int mu, nu, tu;
} TSMatrix;
```

##### 创建压缩矩阵(三元组表示法)

```c++
Status CreateTSM(TSMatrix &M) {
    int t;
    int x, y, z;
    cout << "请输入矩阵的行数: " ;
    cin >> M.mu;
    cout << "请输入矩阵的列数: " ;
    cin >> M.nu;
    cout << "请输入矩阵元素的个数: " ;
    cin >> M.tu;
    if (M.mu == 0 && M.nu == 0 && M.tu == 0) {
        cout << "输入不合法" << endl;
    }
    for (t = 1; t <= M.tu; t++) {
        cin >> x >> y >> z;

        if (x == 0 && y == 0 && z == 0) {
            cout << "输入不合法" << endl;
        }
        M.data[t].i = x;
        M.data[t].j = y;
        M.data[t].e = z;
    }
    //遍历
    for (t = 1; t <= M.tu; t++) {
        cout << M.data[t].i << " " << M.data[t].j << " " << M.data[t].e << " " << endl;
    }
    cout << endl;
    return TRUE;
}
```

##### 快速转置

```c++
Status FastTransposeSMatrix(TSMatrix M, TSMatrix &T) {
    // num 每一列中非0元素的个数
    // copt 每一列中第一个非0元素所在的位置
    int col, num[MAXSIZE + 1], copt[MAXSIZE + 1];
    // M 转置为 T
    // M 的行 = T 的列
    T.nu = M.mu;
    // M 的列 = T 的行
    T.mu = M.nu;
    // M 非0元素个数 = T 非0元素的个数
    T.tu = M.tu;
    // 如果有非0元素 开始转置
    if (T.tu) {
        // 初始化
        for (col = 1; col <= M.nu; ++col) {
            num[col] = 0;
        }
        // 计算每一列中非0元素的个数
        for (int t = 1; t <= M.tu; ++t) {
            ++num[M.data[t].j];
        }
        cout << "num : " ;
        for (int t = 1; t <= M.nu; ++t) {
            cout << num[t] << " ";
        }
        cout << endl;
        //
        copt[1] = 1;
        // 求col列中第一个非零元素在T.data[]中的正确位置
        for (col = 2; col <= M.nu; ++col) {
            copt[col] = copt[col - 1] + num[col - 1];
        }
        cout << "copt: " ;
        for (int s = 1; s <= M.nu; s++) {
            cout << copt[s] << " ";
        }
        cout << endl;
        // 遍历三元组M
        for (int p = 1; p <= M.tu; ++p) {
            // col 记录当前所在列
            col = M.data[p].j;
            // q表示每一列第一个非0元素
            int q = copt[col];
            T.data[q].i = M.data[p].j;
            T.data[q].j = M.data[p].i;
            T.data[q].e = M.data[p].e;
            ++copt[col];
        }
        cout << "转置之后: " <<endl;
        for (int i = 1; i <= T.tu; i++) {
            cout << T.data[i].i << " " << T.data[i].j << " " << T.data[i].e << endl;
        }

    }
    return TRUE;
}
```
