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

##  难度：


### 第一想法:



### 题解:


##  难度：


### 第一想法:



### 题解:


