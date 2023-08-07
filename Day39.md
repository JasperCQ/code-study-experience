# 代码随想录算法训练营13期 第九章 动态规划part02


 **学习时长**
 
##  62.不同路径  难度：中等


### 第一想法:

最开始我感觉这个题型其实不像是dp类型，因为我之前一直觉得dp算法是处理最值问题的。但是发现状态转移方程是很好写出来的。

### 题解:
~~~
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m+1][n+1];
        dp[1][1]=1;
        for(int i=1;i<m+1;i++){
            for(int j=1;j<n+1;j++){
                if(i==1 && j==1)
                    continue;
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        

        return dp[m][n];
    }
}

~~~


##  63. 不同路径 II 难度：中等


### 第一想法:
在上题的基础上加入了障碍物，带来的效果其实就是在状态转移方程那里需要加上一些条件，而对边界情况的影响是，如果存在起点就阻碍的情况，就应该return 0


### 题解:
~~~
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m+1][n+1];
        if(obstacleGrid[0][0]==0)
            dp[1][1]=1;
        for(int i=1;i<m+1;i++){
            for(int j=1;j<n+1;j++){
                if(i==1 && j==1)
                    continue;
                if(obstacleGrid[i-1][j-1]!=1)
                    dp[i][j]=dp[i-1][j]+dp[i][j-1];
                
            }
        }
        return dp[m][n];

    }
}
~~~



