# LEETCODE刷题笔记之四

作者：why

#### 前情提要

最近一直在刷leetcode，今天想对于回溯法做一个小结。是我自己个人的一个总结也是跟大家进行一些我的想法的分享。

### 第一道题目

#### LEETCODE 46

#### 题目描述

给定一个 **没有重复** 数字的序列，返回其所有可能的全排列。

#### 输入输出

输入: [1,2,3]
输出: [ [1,2,3], [1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

#### 我的思路

基本上这个问题就是一个经典的回溯法可以解决的问题，回溯的思想就是我先去把某一个元素放入某个容器，或者我把某种状态变化到另一种状态，如果可以那么我就打印出这种状态，如果这个元素或者说这个状态是不正确的那么我就把这种状态否定，并回到之前的状态，即有一种时间回溯的感觉。其实回溯法其实就是深度优先搜索的一种思想，当我们在深度优先算法中找不到前进的方向或者最终的终点时，我们可以回到某一时刻的状态，继续进行搜索。

```java
public class Solution46 {
    //存放最终答案的java容器
    List<List<Integer>> ans=new ArrayList<>();
    //全排列的方法
    public List<List<Integer>> permute(int[] nums) {
        //我们用来存放是否访问过的数组（避免重复使用某一元素）
        boolean[] isVisted=new boolean[nums.length];
        //回溯法的核心，这是一个递归的调用
        dfs(nums,isVisted,new ArrayList<Integer>());
        //返回答案
        return ans;
    }
    //核心算法
    public void dfs(int[] nums,boolean[] isVisited,ArrayList<Integer> path){
        //如果我们的路径，也就是我们用来存放我们一步步加入元素的容器的尺寸和num数组的长度是一样的，这说明我们找到了一个全排列，所以我们把它放入最终的答案数组
        if(path.size()==nums.length)
            ans.add(new ArrayList<>(path));
        //我们对于从下标0到数组num长度减1的数进行遍历
        for (int i=0;i<nums.length;i++){
            //如果没有被访问，即被加入到路径容器中，就进行下面的操作
            if (!isVisited[i]){
                //变成访问过的元素
                isVisited[i]=true;
                //加入到路径容器中
                path.add(nums[i]);
                //递归进行深度优先搜索
                dfs(nums,isVisited,path);
                //回溯的两步，去掉路径容器的最后的值，因为最后被添加的最先被回溯到
                path.remove(path.size()-1);
                //第二步，因为回溯，所以这个元素要被设置回未访问的
                isVisited[i]=false;
            }
        }
    }
}
```

#### 回溯算法的搜索树

假设我们的nums是【1，2，3】

![image-20210201235450049](C:\Users\why19991031\Pictures\image-20210201235450049.png)

#### 总结

今天跟大家分享的是我关于leetcode上面一道题的一些感悟，这道题之外还有很多的变化，如果有机会我会在日后跟大家进行分享。希望大家能够一起变得更强！