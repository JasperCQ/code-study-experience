# 代码随想录算法训练营13期 第九章 动态规划part03

 
 **学习时长**
 
## 343. 整数拆分 难度：中等


### 第一想法:

其实想状态转移的时候我是想出来了这个的，只是确实最开始我是觉得应该是dp[j],dp[i-j]这样拆分，但是其实，遍历只需要，只需要一边拆分就可以。不需要多边拆分的，


### 题解:
~~~
class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n+1];
        dp[2]=1;
        for(int i=3;i<n+1;i++){
            for(int j=1;j<i;j++){
                dp[i]=Math.max(dp[i],j*Math.max(dp[i-j],i-j));
            }

        }
        return dp[n];
    }
}

~~~

## 96. 不同的二叉搜索树 难度：中等


### 第一想法:

这个题我第一时间是真的没想到要怎么用dp解决的，因为不是常规的那种熟悉的能看出来的dp,而且也确实，如果把n放的很大的话是很难看得出来规律的。但是本质上其实它拆解出来就是一个能从上一个状态转移到下个状态的问题，就能够用dp解决。



### 题解:

~~~
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n+1];
        dp[0]=1;
        for(int i=1;i<n+1;i++){
            for(int j=1;j<=i;j++){
                dp[i]+=dp[j-1]*dp[i-j];
            }
        }
        return dp[n];
    }
}

~~~
