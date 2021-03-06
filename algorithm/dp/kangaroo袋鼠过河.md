### 袋鼠过河

一只袋鼠要从河这边跳到河对岸，河很宽，但是河中间打了很多桩子，每隔一米就有一个，每个桩子上都有一个弹簧，袋鼠跳到弹簧上就可以跳的更远。每个弹簧力量不同，用一个数字代表它的力量，如果弹簧力量为5，就代表袋鼠下一跳最多能够跳5米，如果为0，就会陷进去无法继续跳跃。河流一共N米宽，袋鼠初始位置就在第一个弹簧上面，要跳到最后一个弹簧之后就算过河了，给定每个弹簧的力量，求袋鼠最少需要多少跳能够到达对岸。如果无法到达输出-1

**输入描述:**

```
输入分两行，第一行是数组长度N (1 ≤ N ≤ 10000)，第二行是每一项的值，用空格分隔。
```



##### **输出描述:**

```
输出最少的跳数，无法到达输出-1
```

示例1

## 输入

```
5
2 0 1 1 1
5
1 2 3 4 5
```

## 输出

```
4
3
```

***解题思路：***

数组长度n为河的宽度，每隔1米1个桩，如果把跳到每个木桩看做1个状态，用数组status表示，状态总数为n+1**（0~n）**，用status[i]表示当跳到第i个桩时所用的最少跳数，其中status[0]=0，我们可以定义status[i]很大表示为不可跳到这个桩；输入序列数组input每个元素表示在其对应的桩上可以往前跳的长度，input[0]=2表示从第0个桩可以向前跳1m,2m；从第i个桩出发，可以往前跳的范围为{1, 2…j…input[i] }, 状态转换方程为：

> **status[ i + j ] = min{ status[ i + j ],  status[ i ] + 1}**
>
> **注意：**
>
> 当跳到第n-1个桩时并没有结束，需要在跳1次才算结束！

```c++
#include<iostream>
using namespace std;

int min(int a,int b)
{
	return a<b?a:b;
}

int main()
{
	int n;
	cin>>n;
	int *p = new int[n];
	int *status = new int[n+1];
	for(int i=0;i<n;i++)
	{
		cin>>p[i];
		status[i+1]=1000000;
	}
	status[0]=0;
	for(int i=0;i<n;i++)
	{
		for(int j=1;j<=p[i];j++)
		{
			if(i+j>=n)
			{
				status[n] = min(status[n],status[i]+1);	
			}
			else
			{
				status[i+j]=min(status[i+j],status[i]+1);
			}	
		}
		for(int z=0;z<=n;z++)
		{
			cout<<status[z]<<"\t";
		} 
		cout<<endl;
	}
	int total = status[n]>=1000000?-1:status[n];
	cout<<total<<endl;
	delete[]p;
	delete[]status;
	return 0;
}

```

**测试样例**

```
5
1 2 3 4 5
0       1       1000000 1000000 1000000 1000000
0       1       2       2       1000000 1000000
0       1       2       2       3       3
0       1       2       2       3       3
0       1       2       2       3       3
3
```





