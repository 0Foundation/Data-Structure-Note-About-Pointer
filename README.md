# Data-Structure-Note-About-Pointer
Jackaroo
指针
1.指针变量存储某个变量a的地址,地址就是该变量a在内存的编号
#include <iostream>
#include <stdio.h>

using namespace std;

int main()
{
    int * p;//p是一个变量的名字,int * 表示该p变量只能存储int类型变量的的地址
    int i=10;
    int j;


    p=&i;//p=i的地址,也就是说*p就是等价于i的,而i=10,所以*p等于10
    j=i;

    printf("i=%d,j=%d,*p=%d\n",i,j,*p);


    return 0;
}
2.通过被调函数修改主函数中普通变量的值
#include <iostream>
#include <stdio.h>

using namespace std;
void f(int  i)
{
   i=100;
}
int main()
{

    int i=9;
    f(i);
    printf("i=%d\n",i);//输出的i的值为9,调用的f(i)函数并没有改变i的值
    return 0;
}

#include <iostream>
#include <stdio.h>

using namespace std;
void f(int  * i)//定义了一个int * 类型的参数,名字叫做i
{
   *i=100;
}
int main()
{

    int i=9;
    f(&i);//将i的地址传给f()函数,从而修改主函数中i的值
    printf("i=%d\n",i);
    return 0;
}
3.指针和数组
数组在内存中是连续的
一维数组a[5]={1,2,3,4,5}
	一位数组名a是个指针常量,他存放的是一维数组第一个元素的地址,它的值不能被改变,一位数组名a这个指针指向的是数组的第一个元素,即a[0].
	
	a[i]<-->*(a+i)推出->a[3]==*(a+3)
#include <iostream>
#include <stdio.h>

using namespace std;

int main(void)
{
    int a[5]={1,2,3,4,5};//数组的名字a代表数组第一个元素的地址.即a这个指针变量指向的是a[0]这个元素
    //a[3]==*(a+3)
    printf("%p\n",a);
    printf("%p\n",a+1);
    printf("%p\n",a+2);
    printf("%d\n",*a+3);//*a等价于a[0],*a+3就等于4
    printf("%p\n",a+4);
}
4.数组中如何通过被调函数来改变主函数中数组中的值
	将主函数中变量的地址传给被调函数
	在被调函数中对传过来的地址所指的内容重新赋值,即如下面的p[0]=-1或者p[2]=-6,就可以修改数组中的内容

#include <iostream>
#include <stdio.h>

using namespace std;
void Show_Array(int * p,int len)
{
    p[0]=-1;//p现在就是数组a的第一个元素的地址,p[0]=*p=a[0]=*a
    p[2]=-6;//p[2]==*(p+2)==*(a+2)==a[2]
}

int main(void)
{
    int a[5]={1,2,3,4,5};
    Show_Array(a,5);//a等价于&a[0],&a[0]本身就是int * 类型.第二个参数是数组的长度
    printf("%d\n",a[2]);//结果是:a[2]=-6
}

5.调用函数来输出主函数中的数组
#include <iostream>
#include <stdio.h>

using namespace std;
void Show_Array(int * p,int len)
{
    int i=0;
    for(i=0;i<len;++i)
    {
       printf("%d\n",p[i]);
    }
}

int main(void)
{
    int a[5]={1,2,3,4,5};
    Show_Array(a,5);//a等价于&a[0],&a[0]本身就是int * 类型.第二个参数是数组的长度
}
6.指针变量的运算
	不能加,不能乘,不能相除
	如果两指针同于一个数组,则可以想减
	指针变量可以加减一个整数,前提是最终结果不超过指针所在数组的最大范围
	p+i的值是:p+i*(p所指向的变量所占的字节数)
	p-i的值是:p-i*(p所指向的变量所占的字节数)

7.每个指针变量所指向的变量无论多少字节,指针变量都只指向该变量的第一个字节所在的地址,该地址就可以代表这个变量的整体
	所有的指针变量都只占四个字节
#include <iostream>
#include <stdio.h>

using namespace std;

int main(void)
{
    double x=66.6;
    double * p;

    p=&x;//x占用8个字节,1个字节是8位,一个字节才有一个地址.p所指的地址是x第一个字节的地址,这个地址就可以代表x这个变量
    printf("%f\n",*p);
    double arr[3]={1.1,2.2,3.3};
    double * q;
    q=&arr[0];
    printf("%p\n",q);//%p的意思就是以十六进制输出
    q=&arr[1];
    printf("%p\n",q);

}
8.通过调用函数f()来修改指针变量p的值

#include <iostream>
#include <stdio.h>

using namespace std;
void f(int * *  q);//参数理解为指针变量的地址
int main(void)
{
    int i=10;
    int * p=&i;//等价于int * p,p=&i;
    printf("%p\n",p);
    f(&p);//要想改变p的值只能把地址传给f()
    printf("%p\n",p);
    printf("**********************\n");
    printf("%d\n",i);
    return 0;
}
void f(int * * q)//p本来就是int *类型,&p就是int * *类型
{
    *q=(int *)0xffffffff;//这个时候*q代表的是p本身,是一个int * 类型变量,他指向int 型变量i的地址.另外要注意类型转换
	

}



	



