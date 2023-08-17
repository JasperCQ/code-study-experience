# 代码随想录算法训练营13期 第九章 动态规划 part05



 **学习时长**
 
## 1049. 最后一块石头的重量 II  难度：中等


### 第一想法:
就还是01背包问题的变种，刚好装满，和416题一样，需要先对题目进行变换，变换之后的本质就还是dp解决。


### 题解:

~~~
class Solution {
    public int lastStoneWeightII(int[] stones) {
        int sum = Arrays.stream(stones).sum();
        int target = sum/2;
        int length = stones.length;
        boolean[][] dp = new boolean[length+1][target+1];
        for(int i=0;i<length+1;i++){
            dp[i][0]=true;
        }
        
        for(int i = 1;i<length+1;i++){
            for(int j =1;j<target+1;j++){
                if(j>=stones[i-1]){
                    dp[i][j]=dp[i-1][j-stones[i-1]] || dp[i-1][j];


                }
                else
                    dp[i][j]=dp[i-1][j];

            }
        }
        if(dp[length][target]==true){
            if(sum%2==0)
                return 0;
            else
                return 1;
        }
        for(int j = target;j>=0;j--){
            if(dp[length][j]==true){
                if(sum%2==0)
                    return 2*(target-j);
                else
                    return 2*(target-j)+1;
            }
        }
        return -1;
    }
}


~~~

## 494. 目标和 难度：中等


### 第一想法:

第一时间想直接DP，发现存在负数问题，所以其实是需要变换的，变换之后就变成经典的416号的问题了。



### 题解:
~~~
public int findTargetSumWays(int[] nums, int target) {
        int length = nums.length;

        int sum = Arrays.stream(nums).sum();
        if((sum-target)%2!=0 || sum<target)
            return 0;

        int new_target = (sum-target)/2;
        int[][] dp = new int[length+1][new_target+1];
            
        dp[0][0]=1;

        for(int i=1;i<length+1;i++){
            for(int j=0;j<new_target+1;j++){
                if(j>=nums[i-1])
                    dp[i][j]=dp[i-1][j]+dp[i-1][j-nums[i-1]];
                else
                    dp[i][j]=dp[i-1][j];
            }
        }
        return dp[length][new_target];
    }

~~~





## 474. 一和零 难度：中等


### 第一想法:
就是一个三维dp问题


### 题解:
~~~
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int length =  strs.length;
        int[][][] dp = new int[m+1][n+1][length+1];

        for(int i=0;i<m+1;i++){
            for(int j=0;j<n+1;j++){
                for(int k=1;k<length+1;k++){
                    int count_0=0;
                    int count_1=0;
                    for(int index=0;index<strs[k-1].length();index++){
                        if(strs[k-1].charAt(index)=='1')
                            count_1++;
                        else
                            count_0++;
                    }
                    
                    if(i>=count_0 && j>=count_1)
                        dp[i][j][k] = Math.max(dp[i-count_0][j-count_1][k-1]+1,dp[i][j][k-1]);
                    else
                        dp[i][j][k] = dp[i][j][k-1];


                }
            }
        }
        
        return dp[m][n][length];
    }
}

~~~

