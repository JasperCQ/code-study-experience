# 代码随想录算法训练营13期 第九章 动态规划part01

 
 **学习时长**
 
## 509. 斐波那契数  难度：简单



### 第一想法:

入门DP题



### 题解:
~~~

class Solution {
    public int fib(int n) {
        int[] dp = new int[n+1];
        if(n==0)
            return 0;
        dp[1]=1;
        for(int i = 2; i<n+1;i++){
            dp[i]=dp[i-1]+dp[i-2];
        }
        
        return dp[n];
    }
}

~~~




 
## 70. 爬楼梯  难度：简单


### 第一想法:

和上一题一样的



### 题解:
~~~
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n+1];
        if(n==1)
            return 1;
        dp[1]=1;
        dp[2]=2;
        for(int i=3;i<n+1;i++){
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
}


~~~


 
## 746. 使用最小花费爬楼梯 难度：简单


### 第一想法:

也是入门的DP


### 题解:

~~~
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int size = cost.length;
        int[] dp = new int[size+1];
        for(int i = 2;i<size+1;i++){
            dp[i] = Math.min(dp[i-2]+cost[i-2],dp[i-1]+cost[i-1]);
        }
        return dp[size];
    }
}

~~~


