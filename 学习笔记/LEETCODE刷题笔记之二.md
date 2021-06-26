# LEETCODE刷题笔记之二

#### 前情提要

我们继续我们的刷题节奏，今天给大家带来想要分享的是关于三数相加的一些问题

### 第一道题目

#### 问题描述

#### LEETCODE 15

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/3sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 输入输出

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

```
输入：nums = []
输出：[]
```

```
输入：nums = [0]
输出：[]
```

#### 思路

其实我们可以看到我们可以用一个三次遍历，用三个i，j，k来去进行加法计算把最后的结果和0，进行比对，但是我们可以发现这样的算法时间复杂度是$O(n^3)$并且可能会有重复的结果产生，这样我们消除重复的值又会有新的困难。

#### 进一步的思路

那么我们可以这么做，对于数组进行排序，排序算法比较快速的算法是归并排序和快速排序，时间复杂度只需要$O(nlogn)$。之后我们遍历一下数组，用i来表示遍历过程中的下标，之后我们用一个指向最远的指针c来进行我们的最后一个数的位置移动操作，因为我们的目标是三数之和为0，所以我们的最后一个指针其实它的移动是有规律的，因为，随着j的向右移动，它只可能会朝向左进行移动。这样的好处是什么，我们减少了j和c的移动次数，这样能够把时间复杂度从$O(n^3)$变成$O(n^2)$。

#### 代码

```java
List<List<Integer>> ans=new ArrayList<>();//存放答案数组
Arrays.sort(nums);//引用java的包进行排序操作
for(int i=0;i<nums.length;i++){//对于i进行遍历
    if (i>0&&nums[i]==nums[i-1])//细节，通过这样的两行代码来防止相同的第一个数进行多次操作
        continue;
    int c=nums.length-1;//每个i都有一个最初指向数组末尾的指针
    for(int j=i+1;j<nums.length;j++){//遍历j从i+1开始到结束，不从最初开始是为了避免重复和避免i和j的位置一样
        if(j>i+1&&nums[j]==nums[j-1])//跟i相似的操作，通过这个操作避免对于相同的第二个数进行操作
            continue;
        int target=-nums[i] - nums[j];//我们计算出c应该具有的值，因为nums[j]的大小在之后的过程中只会增加，所以我们可以在上述移动后的基础上继续进行向左的移动
        while(j<c&&nums[c]>=target){//移动的过程
            if (nums[c]==target){//如果找到正确的结果就把它放入答案数组
                ArrayList<Integer> mid=new ArrayList<>();
                mid.add(nums[i]);
                mid.add(nums[j]);
                mid.add(nums[c]);
                ans.add(mid);
                break;
            }
            c--;
        }
    }
}
return ans;
```

#### 细节

细节就是我们的避免重复的操作，如果不进行这样的操作的话，我们的答案当中会有重复的解。

### 第二道题目

#### LEETCODE 16

#### 问题描述

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

 

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/3sum-closest
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 输入输出

```
输入：nums = [-1,2,1,-4], target = 1
输出：2
```

#### 思路

这道题目的思路和上面基本上是一样的，我们进行排序操作，然后我们遍历一遍数组，之后我们采用双指针来进行答案的缩进，区别在于我们这边不需要对于重复性有太多的要求，大题的思路如下

- 我们遍历一遍数组，用下标i来表示
- 然后创建两个指针，一个是start，一个是end，一个指向的是i+1，另外一个指向的是数组末尾
- 如果我们的结果比target大，就让end--，如果比target小，就让start++，最后能够逼近正确答案。

#### 代码

```java
Arrays.sort(nums);//还是要对数组进行排序，时间复杂度是nlogn
int ansCon=Integer.MAX_VALUE;//这个是存放最小差距的值，其实没啥必要233，可以继续进行简化
int ans=0;//这个是存放答案的值
for(int i=0;i<nums.length-1;i++){//遍历，注意一个细节，因为我们的start=i+1，所以不能到末尾只能是末尾-1
    int start=i+1;
    int end=nums.length-1;
    while(start<end){
        int nowSum=nums[i]+nums[start]+nums[end];//计算目前的值
        if(Math.abs(nowSum-target)<ansCon) {//更新答案
            ansCon = Math.abs(nowSum - target);
            ans =nowSum;
        }
        if (nowSum>target)//看如何移动指针
            end--;
        else{//看如何移动指针
            start++;
        }
    }
}
return ans;
```

#### 总结

三数问题是很经典的一类问题，我们要灵活的使用双指针的思想，来简化我们问题的时间复杂度。