<a name="Lg5V9"></a>
## 3. 线性表-顺序表
线性表的定义
零个或者多个数据源函数的有限序列.
一个元素节点中,它前面的叫**前驱**,后面的叫**后继**.
我们的顺序表需要实现以下几个函数功能

```
// 初始化一个线性表
ElemType initializeList(SqList *L);
// 清空一个线性表
ElemType ClearList(SqList *L);
// 判断一个线性表是否为空
ElemType IsEmpty(SqList *L);
// 查找一个元素,有则返回下标,没有则返回 0
ElemType LocateElem(SqList *L, ElemType e);
// 获取线性表一个元素并返回给 e
ElemType GetElem(SqList *L, int i, ElemType *e);
// 插入元素
ElemType InsertElem(SqList *L, int i, ElemType e);
// 删除元素
ElemType DeleteElem(SqList *L, int i, ElemType *e);
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625710065-d4c31c13-d92d-43dc-af74-336fc0d8c23c.gif#averageHue=%23ffffff&clientId=u016f4683-b8a9-4&from=paste&id=ua201b81d&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=ud2df2c37-d482-434d-a85a-bd35c2b5ed7&title=)
<a name="OGopj"></a>
### 3.1 创建一个顺序表
概念巨几把好懂,话不多说实现代码(don't BB show me code)
首先我们在结构体中定义一个数组来实现线性表的连续存储

```
#include <stdio.h>
#include <stdlib.h>
#define initialize_size 20

#define OK 1
#define ERROR 0
#define TRUE 1
#define FALSE 0

typedef int ElemType;

typedef struct
{
   ElemType *data;
   int max_size;
   int lenght;
} SqList;
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625710027-59ceb162-b3f7-4c3f-92d1-2825d3a232fd.gif#averageHue=%23ffffff&clientId=u016f4683-b8a9-4&from=paste&id=uc6d2f57d&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=ubf4963ae-470f-4128-9403-8e5badcc608&title=)
这里我们得区分一个数组长度和线性表长度,lenght在我们后续每一步添加和删除元素得时候都会随之改变,而这个数组长度是最大长度.
当然我们也可以使动态数组来创建数组,但是先从简单做起.
<a name="Y1Nf1"></a>
### 3.2 顺序表的初始化

```
ElemType initializeList(SqList *L)
{
   L->data = (ElemType *)malloc(initialize_size * sizeof(ElemType));
   if ((*L).data == NULL)
   {
      printf("初始化失败");
      exit(ERROR);
   }
   L->lenght = 0;
   L->max_size = initialize_size;
   printf("线性表----初始化成功-----\n");
   return OK;
}
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625710024-0fb57d5e-fb6d-4809-a4f4-79f926fafd73.gif#averageHue=%23ffffff&clientId=u016f4683-b8a9-4&from=paste&id=uac9e52b7&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=u1abe549d-4cb0-4d3e-bcd6-e7c60baea48&title=)
<a name="PSqVK"></a>
### 3.3 顺序表的判断和清空
这里我们判断线性表是否为空,和但线性表不为空时的清空操作.

```
ElemType ClearList(SqList *L)
{
   if (!L->data)
      return FALSE;
   L->lenght = 0;
}

ElemType IsEmpty(SqList *L)
{
   if (L->lenght == 0)
   {
      printf("\n线性表是空");
      return TRUE;
   }
   printf("\n线性表不为空");
   return FALSE;
}
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625710022-d9518a38-289b-482b-93c9-b2fddc078778.gif#averageHue=%23ffffff&clientId=u016f4683-b8a9-4&from=paste&id=u99747a32&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=u8c99d611-9649-4346-a2d5-6a35fa0ef10&title=)
<a name="b0fdb"></a>
### 3.4 顺序表元素的查找

```
// 查找一个元素,有则返回下标,没有则返回 0
ElemType LocateElem(SqList *L, ElemType e);

ElemType LocateElem(SqList *L, ElemType e)
{
   if (!L->data)
      return 0;
   for (int h = 0; h < L->lenght; h++)
   {
      if (L->data[h] == e)
         return h;
   }
   return 0;
}
```
<a name="ItOxy"></a>
### 3.5 顺序表元素获取
这里我提一嘴基础知识
下面这种静态初始化数组,可行.

```
int arr[10]= {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625710026-0be7038b-d1f8-48ef-9b59-4fbdca71b3d9.gif#averageHue=%23ffffff&clientId=u016f4683-b8a9-4&from=paste&id=ufe65f970&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=uf8fa85ad-22da-489e-b128-bc23bab3f6f&title=)
但是下面这种就不可行

```
int arr[10];
   arr[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
```
![image.png](https://cdn.nlark.com/yuque/0/2023/gif/33584294/1697625710670-8789fedc-a883-4ad0-83fd-1c8c799fac90.gif#averageHue=%23ffffff&clientId=u016f4683-b8a9-4&from=paste&id=u27278919&originHeight=1&originWidth=1&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=43&status=done&style=none&taskId=u3ac1c884-9014-4a34-8506-95e349df025&title=)
因为定义好数组之后,arr[]就表示这个数组的地址 你怎么将这么大坨赋值给一个指针.
**所以在结构体中定义了数组后期需要循环来赋值**
回归正题,我们获取线性表中的元素代码如下:
 	

-  	首先判断是否为空 	
-  	下标 i 是否符合条件 	

```
// 将线性表中的第i位置的元素值返回给e
ElemType GetElem(SqList *L, int i, ElemType *e)
{
   if (i < 1 || i > L->lenght || L->lenght == 0)
      return ERROR;
   *e = L->data[i - 1];
   return OK;
}
```
<a name="CtiNu"></a>
### 3.6 顺序表元素插入
我们需要在意的三个点
 	

-  	下标如果输入错误抛出异常 	
-  	将所有元素后移一位插入元素 	
-  	表长 +1 	

```
// 线性表中插入元素
ElemType ListInsert(SqList *L, int i, ElemType e);

ElemType InsertElem(SqList *L, int i, ElemType e)
{
   if (i < 1 || i > L->lenght + 1)
      return ERROR;
   if (i <= L->lenght)
   {
      for (int h = L->lenght; h >= i; h--)
         L->data[h] = L->data[h - 1];
   }
   L->data[i - 1] = e;
   L->lenght++;
   return OK;
}
```
<a name="XeTsB"></a>
### 3.7 顺序表元素的删除
 	

-  	注意下标问题 	
-  	表长减一 	
-  	在删除前赋值给第三变量,然后返回 	

```
// 删除第i位置的值,并返回其值.
ElemType ListDelete(SqList *L, int i, ElemType *e);

ElemType DeleteElem(SqList *L, int i, ElemType *e)
{
   if (i < 1 || i > L->lenght)
      return ERROR;
   *e = L->data[i - 1];
   for (int h = i; h <= L->lenght; h++)
      L->data[h - 1] = L->data[h];
   L->lenght--;
   return OK;
}
```
<a name="b4ZEo"></a>
### 3.9 顺序表全部代码

```
#include <stdio.h>
#include <stdlib.h>
#define initialize_size 20

#define OK 1
#define ERROR 0
#define TRUE 1
#define FALSE 0

typedef int ElemType;

typedef struct
{
   ElemType *data;
   int max_size;
   int lenght;
} SqList;

// 初始化一个线性表
ElemType initializeList(SqList *L);
// 清空一个线性表
ElemType ClearList(SqList *L);
// 判断一个线性表是否为空
ElemType IsEmpty(SqList *L);
// 查找一个元素,有则返回下标,没有则返回 0
ElemType LocateElem(SqList *L, ElemType e);
// 获取线性表一个元素并返回给 e
ElemType GetElem(SqList *L, int i, ElemType *e);
// 插入元素
ElemType InsertElem(SqList *L, int i, ElemType e);
// 删除元素
ElemType DeleteElem(SqList *L, int i, ElemType *e);

void print(SqList *L)
{
   for (int h = 0; h < L->lenght; h++)
      printf("%d  ", L->data[h]);
}

int main(void)
{
   SqList L;
   // 初始化线性表
   initializeList(&L);

   // 往顺序表中放数据
   for (int h = 0; h < 10; h++)
   {
      L.data[h] = h;
      L.lenght++;
   }
   print(&L);

   // 判断是否为空
   IsEmpty(&L);

   // 查找元素
   int Found_e = 5;
   int result;
   result = LocateElem(&L, Found_e);
   printf("\n%d\n", result);

   // 插入元素
   int insert_e = 100;
   InsertElem(&L, Found_e, insert_e);
   print(&L);

   // 删除元素
   int delete_e = 0;
   ElemType *back_e = &delete_e;
   DeleteElem(&L, Found_e, back_e);
   printf("\n%d\n", delete_e);
   print(&L);

   //清空线性表再判断
   ClearList(&L);
   IsEmpty(&L);

   return 0;
}

ElemType initializeList(SqList *L)
{
   L->data = (ElemType *)malloc(initialize_size * sizeof(ElemType));
   if ((*L).data == NULL)
   {
      printf("初始化失败");
      exit(ERROR);
   }
   L->lenght = 0;
   L->max_size = initialize_size;
   printf("线性表----初始化成功-----\n");
   return OK;
}

ElemType ClearList(SqList *L)
{
   if (!L->data)
      return FALSE;
   L->lenght = 0;
}

ElemType IsEmpty(SqList *L)
{
   if (L->lenght == 0)
   {
      printf("\n线性表是空");
      return TRUE;
   }
   printf("\n线性表不为空");
   return FALSE;
}

ElemType LocateElem(SqList *L, ElemType e)
{
   if (!L->data)
      return 0;
   for (int h = 0; h < L->lenght; h++)
   {
      if (L->data[h] == e)
         return h;
   }
   return 0;
}

ElemType GetElem(SqList *L, int i, ElemType *e)
{
   if (i < 1 || i > L->lenght || L->lenght == 0)
      return ERROR;
   *e = L->data[i - 1];
   return OK;
}

ElemType InsertElem(SqList *L, int i, ElemType e)
{
   if (i < 1 || i > L->lenght + 1)
      return ERROR;
   if (i <= L->lenght)
   {
      for (int h = L->lenght; h >= i; h--)
         L->data[h] = L->data[h - 1];
   }
   L->data[i - 1] = e;
   L->lenght++;
   return OK;
}

ElemType DeleteElem(SqList *L, int i, ElemType *e)
{
   if (i < 1 || i > L->lenght)
      return ERROR;
   *e = L->data[i - 1];
   for (int h = i; h <= L->lenght; h++)
      L->data[h - 1] = L->data[h];
   L->lenght--;
   return OK;
}
```
最后执行的结果如下：
```
线性表----初始化成功-----
0  1  2  3  4  5  6  7  8  9       
线性表不为空
5
0  1  2  3  100  4  5  6  7  8  9  
100
0  1  2  3  4  5  6  7  8  9       
线性表是空
```
OK! 至此线性表中的顺序表就先告一段落.
