



### **杨辉三角**

老师讲的方法

```c
#include<stdio.h>

double f(int n)			//范围会超出用double
{
	int i;
	double product = 1;
	for (i = 1; i <= n; i++)
	{
		product *= i;
	}
	return product;
}		//阶乘函数

double C(int n, int k)
{
	return f(n) / (f(k) * f (n - k));
}			// 阶乘公式函数
void printfYH(int n)	// 不用返回，直接打印，void
{
	int i, j, m;
	for (i = 0; i <= n; i++)
	{
		for (m = 0; m <= (n - i); m++)
		printf("  ");	//空格2， 4 perfect
		for (j = 0; j <= i; j++)	//从零行开始
		{
			printf("%4g", C(i, j));	//g 去掉不必要的零 
		 } 
		 printf("\n");
	}
}		// 布局，输出函数

int main()	//主函数，unique
{
	int n;
	
	printf("n = ");
	scanf("%d", &n);
	printfYH(n);	//函数调用
	return 0;
	
 } 
```

网上版本

```c
#include <stdio.h>
/* 
 * 定义阶乘，在这里可能会想。为什么要用float，当我试第一次的时候，
 * 如果用int的话，那么在打印行数多了以后就会出错。
 * 这是因为阶乘的数比较大，如果用int就不够用了。下同
 */
float J(int i){
    int j;
    float k=1;
    for(j=1;j<=i;j++)
        k=k*j;
    return(k);
}
float C(int i,int j){  /*定义组合数*/
    float k;
    k=J(j)/(J(i)*J(j-i));
    return(k);
}
void main(){
    int i=0,j,k,n;  /*打印杨辉三角*/ 
    while(i<=0||i>16){
        printf("请输入要打印的行数：");
        scanf("%d",&i);
    }
    printf("%d行杨辉三角如下：\n",i);
    for(j=0;j<i;j++){
        for(k=1;k<=(i-j);k++)
            printf("  ");
        for(n=0;n<=j;n++)
            printf("%4.0f",C(n,j));
        printf("\n");
    }
    printf("\n\n");
}
```

**==知识点==**

+ return 1, 2, 3;  -->逗号表达式，有效的只是最后一个

+ return  2.8；--> 如果返回值类型是double  ，结果return 2.0

  ​		返回值类型 函数名（类型 形式参数1， 类型 形式参数2, ....）-->头部

  ```c
  long fac(int n, int k)	//无分号
  ```

  

  + 函数原型声明  形式参量名可以省略
  
  + expected primary-expression before int （调用函数时，参数前面多加了int）
  
  + 全局变量，==非必要不用==，违背了最小权限原则，破坏了函数的封装性
  
  + ```c
    extern 类型名 变量名 //扩大作用域
    ```
  
  + ```c
    static 类型名  变量名 //系统保留这个值
    ```
  
  + 

**静态局部变量**

```c
#include<stdio.h>

double fac(int n)
{
    static double result = 1;	//静态局部变量 存在 静 里面 
    
    result *= n;
    
    return result;
}	//服务函数，执行后便被回收
int main()
{
    double result;
    int i, n;
    scanf("%d", &n);
    for (i = 1; i <= n; i++)
    {
        result = fac(i);
    }
    printf("result = %g\n", result);
    return 0;
}
```

斐多拉契数列

```c
#include<stdio.h>
double fib(int n)
{
    static double f = 1, s = 1, t;
    t = f + s;
    f = s;
    s = t;
    return t;
}

int main()
{
    double result;
    int i, n;
    scanf("%d", &n);
    
    for (i = 3; i <= n; i++)
    {
        result = fib(i);
    }
    printf("result = %g\n", result);
    return 0;
}
```

**==递归==**：调用了自身函数

```c
#include<stdio.h>

double fib(int n)
{
    if(1 == n || 2 ==  n)
        return 1;
    else
        return f(n - 1) + f(n - 2);	//从哪里调过来，就返回到哪里
}

int main()
{
    int n;
    scanf("%d", &n);
    
    printf("result = %g\n", fib (n));
    return 0;
}
```

|      |      | **程序**                                    |
| ---- | ---- | ------------------------------------------- |
|      |      | 栈            ----->形参     局部变量       |
|      |      | 静            ---- > 全局变量、静态局部变量 |
|      |      | 堆                                          |

