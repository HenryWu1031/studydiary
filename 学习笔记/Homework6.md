# Homework6

#### 1827406023 吴航宇

### 1、问题解答

按照ppt中和课上老师所讲的动态规划思想，我们先定义一个函数

$OPT(i)$是有多少种方式能把i写成1，3，4的和

我们的目标是$OPT(n)$

下面我们列出Bellman等式

$OPT(n)=\left\{\begin{aligned}1&   &n=1,2\\2& &n=3\\4&&n=4\\OPT(n-1)+OPT(n-3)+OPT(n-4)&&n>4\end{aligned}\right.$

经过等式我们可以列出伪代码

$CountWayToSumNFromOneThreeFour(n)$

- $M[0]=1$
- $M[1]=1$
- $M[2]=2$
- $M[3]=4$

- $for\ i=4\ to\ n-1$
  - $M[i]=M[i-1]+M[i-3]+M[i-4]$

- $return\  M[n-1]$

通过我们的伪代码我们可以看到这个函数的时间和空间复杂度都是$O(n)$

### 2、问题解答

分析问题：这道题要求我们计算求最终结果为n的最少计算步骤以及具体计算过程，但是我们的计算步骤只能是题目所给三个步骤中的一个

我们继续定义一个函数

$OPT(i)$这个函数表示最终结果为i时所需要的最少计算步骤

那么我们的目标就是去计算$OPT(n)$

我们经过分析得到如下的Bellman公式

$OPT(n)=\left\{\begin{aligned}1&&n=2,3\\min(OPT(n-1)+1,OPT(n/2)+1)&&if \quad n是2的倍数,但不是3的倍数\\min(OPT(n-1)+1,OPT(n/3)+1)&&if \quad n是3的倍数,但不是2的倍数\\min(OPT(n-1)+1,OPT(n/3)+1,OPT(n/2)+1)&& if \quad n是6的倍数\\OPT(n-1)+1&& else\end{aligned}\right.$

把它转换为伪代码变成如下：

$CountTheFewestStepTon(n)$

- $M[2]=1$
- $M[3]=1$
- $for\ i=1\ to\ n$
  - $if\ i\%2==0\ and\ i\%3!=0:$
    - $M[i]=min(M[i-1]+1,M[i/2]+1)$

- - $else\ if \ i\%2!=0\ and\ i\%3==0:$
    - $M[i]=min(M[i-1]+1,M[i/3]+1)$
  - $else\ if \ i\%2==0\ and\ i\%3==0:$
    - $M[i]=min(M[i-1]+1,M[i/3]+1,M[i/2]+1)$
  - $else:$
    - $M[i]=M[i-1]+1$

- $return\ M[n]$

我们可以看到这个算法的时间复杂度和空间复杂度都是$O(n)$

### 3、问题解答

这个问题一开始我拿到是毫无头绪的，后来当我在梳理ppt是我偶然发现了新大陆

下面我就把算法的思想写出来

算法主要使用了06Dynamicprogramming part2这个ppt的中的longest common subsequence的变形

我们把序列倒过来，这样就变成了一个新的序列

对于这原本的序列和倒过来的新序列，我们进行longest common subsequence算法

我们也是定义一个函数$OPT(i,j)$

这个函数表示两个序列中的子序列，切割是从第一个的0-i和第二个的0-j，最长的相同子序列的长度大小

我们的目标是得到$OPT(n,n)$的大小

我们可以得到Bellman公式为

$OPT(i,j)=\left\{\begin{aligned}0&&if\ i==0或j==0\\1+OPT(i-1,j-1)&&if \ x_i==y_j\\max(OPT(i-1,j),OPT(i,j-1))&&if\ x_i!=y_i\end{aligned}\right.$

我们把它转化为伪代码：

$CountLongesetCommanSubsequence(Str1,Str2,n)$

$for\ i=0\ to \ n$

- $M[i][0]=0$

$for\ j=0\ to \ n$

- $M[0][j]=0$

$for\ i=1\ to \ n$

- $for\ j=1\ to \ n$
  - $if\ str1[i-1]==str2[j-1]$
    - $M[i][j]=1+M[i-1][j-1]$

- - $else$
    - $M[i][j]=max(M[i-1][j],M[i][j-1])$

$return\ M[n][n]$

然后我们根据状态表回溯traceback，寻找出这最长的相同子序列的值，就完成了我们的算法

因为把序列反转的时间复杂度是$O(n)$

建立动态规划状态表的时间复杂度和空间复杂度为$O(n^2)$

所以我们可以知道总的时间复杂度和空间复杂度都为$O(n^2)$

### 4、问题解答

算法的基本思想还是跟前面的差不太多，主要是使用了动态规划的思想。

但是这道题目比较复杂的地方在于，我们怎么样去判断一个找零金额无法被找零

我们会定义一个函数$OPT(i,v)$表示使用$x_1,x_2,\cdots,x_i$的零钱找v元能否可行，以及可行的钞票数

我们发现我们的目标就是$OPT(n,v)$

下面我们给出bellman等式

$OPT(i,v)=\left\{\begin{aligned}0&&if \ i==0\ and\ v==0\\-1&&if \ i==0\ and\ v!=0\quad or\ OPT(i-1,v-x_i)<0\ \\1+OPT(i-1,v-x_i)&&if\ v>=x_i\ and\ OPT(i-1,v-x_i)>=0\\OPT(i-1,v)&& if\ v<x_i\end{aligned}\right.$

伪代码如下：

这次的状态表是这样的，n+1行，有v+1列

- 对第一行,除了（0，0）为0，其余都遍历为-1
- 然后我们遍历第1到第n+1行，即$for\ i=1\ to\ n$
- 在基础上                                              $for\ j=0\ to\ v$

- 核心代码
- $if\ v<x_i: $
  - $M[i][v]=M[i-1][v]$
- $elseif\ v>=x_i\ and\ M[i-1][v-x_i]>=0:$
  - $M[i][v]=1+M[i-1][v-x_i]$
- $elseif\ M[i-1][v-x_i]<0:$
  - $M[i][v]=-1$

- $Return\ M[n][v]$

如果结果是-1，说明不存在解

如果结果是大于0的数，我们可以用回溯算法在状态表中回溯获得找零结果

我们可以看到这个算法的时间复杂度和空间复杂度都是$O(nv)$