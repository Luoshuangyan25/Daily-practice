# Daily-
#include <stdio.h>
#include <stdlib.h>

int array(int arr1[],int arr2[]){
   int tag = 1;
   for(int i = 0;i < 6;i++){
      if(arr1[i] != arr2[i]){
        tag = 0;
      }
   }
   return tag;
}
int main()
{
    int mashu[5] = {0};//记录码数数组
    int i = 0, sum = 0, j = 0;
    for(i = 0; i < 5;i++){
        printf("请输入%d码数鞋的数量：\n",36+i);
        scanf("%d",&mashu[i]);
        sum = sum + mashu[i];
    }
//    for(i = 0; i < 5;i++){
//        printf("%d ",mashu[i]);
//    }
//    printf("\n");
    int xiangshu = 0,hoxiang = 0;
    if(sum % 15 == 0){
        xiangshu = sum / 15;
    }else{
        xiangshu = (sum / 15)+1;
        hoxiang = sum%15;
    }
    int shan[5] = {0},yu[5] = {0},vum = 0;//基本鞋数
    for(i = 0; i < 5;i++){
        shan[i] = mashu[i]/xiangshu;
        yu[i] = mashu[i]%xiangshu;
        vum = vum + shan[i];
    }
//    printf("%d %d %d\n",xiangshu,hoxiang,vum);
    int result[xiangshu][6];
    if(hoxiang != 0){ //若最后一箱不满
          result[xiangshu-1][0] = hoxiang - vum;
          for(i = 0; i < xiangshu-1; i++){//其他第一列存各箱剩余数
             result[i][0] = 15 - vum;
          }
    }else{
          for(i = 0; i < xiangshu; i++){//第一列存各箱剩余数
            result[i][0] = 15 - vum;
          }
    }
    for(i = 0; i < xiangshu; i++){  //其他储存各码鞋数
        for(j = 1; j < 6;j++){
        result[i][j] = shan[j-1];
        }
    }
//    for(i = 0;i < xiangshu;i++){
//        for(j = 1;j < 6;j++){
//            printf("%d ",result[i][j]);
//        }
//        printf("\n");
//    }
    //循环执行
    int p = 0;
    for(int t = 0;t < 5;t++){
            //p指针指向余数数组最大值下标
            for(i = 0;i < 5;i++){
               if(yu[i]>yu[p])
                  p = i;
            }
            int operate = yu[p],op = 0; //操作数（最大值）op指向result数组
            while(operate != 0){
                if(result[op][0] != 0 ){ //还有剩余
                    result[op][p+1]++;
                    result[op][0]--;
                    op++; //op指向下一个
                    operate--;
                }else{
                    op++;
                }
            }
            yu[p] = 0;
    }
//    int count = 0;
//    while(count != xiangshu - 1) {
//        int num = 0;
//
//    }
//    printf("每箱装36-40码鞋数为：\n");
//    printf("36 37 38 39 40\n");
//    for(i = 0;i < xiangshu;i++){
//        for(j = 1;j < 6;j++){
//            printf("%d ",result[i][j]);
//        }
//        printf("\n");
//    }
    i = 0, j = 0;
    int count = 1, k = 36;
    while(i < xiangshu){
        int num2 = array(result[i], result[i + 1]);
        if(num2 == 1){
            i++;
            count++;
        }
        else{
            for(j = 1; j < 6; j++){
                printf("%d码的鞋:%d双 ", k + j - 1, result[i][j]);
            }
            printf(" 共需要%d箱\n", count);
            count = 1;
            i++;
        }
    }
    return 0;
}
