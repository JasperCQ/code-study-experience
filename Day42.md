# 代码随想录算法训练营13期 第九章 动态规划part04


## 背包问题

### 01背包问题： 二维dp，和把二维压缩成一维

一维dp倒序遍历本质：
倒序遍历的原因是，本质上还是一个对二维数组的遍历，并且右下角的值依赖上一层左上角的值，因此需要保证左边的值仍然是上一层的，从右向左覆盖。
 
 **学习时长**
 
## 416. 分割等和子集 难度：中等


### 第一想法:

其实难点主要在一：怎么能够把这样一个看似分割问题，转化为一个刚好装满背包的dp形式问题。
然后难点二：就是想清楚状态转移方程


###  题解:

~~~

class Solution {
    public boolean canPartition(int[] nums) {
        int sum=0;
        for(int i=0;i<nums.length;i++){
            sum+=nums[i];
        }
        if (sum%2!=0)
            return false;
        boolean [][]dp= new boolean[nums.length+1][sum/2+1];
        
        for(int i=0;i<nums.length+1;i++){
            dp[i][0]=true;
        }
        for(int j=0;j<sum/2+1;j++){
            dp[0][j]=false;
        }

        for(int i =1;i<nums.length+1;i++){
            for(int j=1;j<sum/2+1;j++){
                if(j-nums[i-1]<0)
                    dp[i][j]=dp[i-1][j];
                else{
                dp[i][j]=dp[i-1][j] || dp[i-1][j-nums[i-1]];
                }
            }
        }
        return dp[nums.length][sum/2];
    }
}

~~~



