```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAXSIZE 1000

int main(){
    // 建立一个char型数组叫data
    unsigned char data[MAXSIZE];
    // i用于循环 flag用于标志帧同步标记 index用于标记帧定界符下标
    int i , flag = 0, index;
    // 两个指针 指向input文件和output文件
    FILE *fpin = fopen("input.txt", "rb");
    FILE *fpout = fopen("output.txt", "w");
    // 判断两个文件是否能打开
    if(fpin == NULL && fpout == NULL){
        printf("文件打不开!");
        exit(0);
    }
    // 将读取的input文件存入到数组data中
    fread(data, 1, MAXSIZE, fpin);
    // 获取文件存入数组的长度
    int flen = ftell(fpin);
    
    for(i = 0; i < flen; i++){
        // 判断是否存在帧定界符 存在将flag置为1
        if(data[i] == 0xAB){
            index = i;
            flag = 1;
            // 判断帧定界符前7位是否是前同步码,有一个不是就将flag置为0
            for(i = index - 7; i < index; i++){
                if(data[i] != 0xAA){
                    flag = 0;
                }
            }
        }
    }

    if(flag){
        
        printf("第1帧开始解析:\n");
        printf("前导码: ");
        for(i = 0 ; i < index ; i++){
            printf("%2x ", data[i]);
        }
        printf("\n");

        printf("帧定界符: ");
        printf("%2x", data[index]);
        printf("\n");

        printf("目的地址: ");
        for(i = index + 1 ; i < index + 6 ; i++){
            printf("%2x", data[i]);
            printf("-");
        }
        printf("%2x", data[index + 6]);
        printf("\n");

        printf("源地址: ");
        for(i = index + 7 ; i < index + 12 ; i++){
            printf("%2x", data[i]);
            printf("-");
        }
        printf("%2x", data[index + 12]);
        printf("\n");

        printf("长度字段: ");
        for(i = index + 13 ; i < index + 15; i++){
            printf("%2x ", data[i]);
        }
        printf("\n");

        printf("数据格式: ");
        
        //int l = flen - 4 - index - 15;
        
        for(i = index + 15; i < flen - 4; i++){
            printf("%c", data[i]);
            // 将数据字段写入到output文件
            fprintf(fpout, "%c", data[i]);
        }
        printf("\n");

        printf("帧校验字段: ");
        for(i = flen - 1; i > flen - 5; i--){
            printf("%2x ", data[i]);
        }
        printf("\n");
    
        printf("帧全部解析完成!");

    }else{
        printf("没有帧同步信息!");
    }
    
    // 关闭文件指针
    fclose(fpin);
    fclose(fpout);
    return 0;
}
```
