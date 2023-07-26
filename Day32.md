
# 代码随想录算法训练营13期 第八章 贪心算法 part02

 
 **学习时长**
 
## 122. 买卖股票的最佳时机 II  难度：中等


### 第一想法:

其实贪心没想出来，但是一个很形似贪心的dp我倒是写出来了，但是其实画个图，贪心很好理解的，就是累加上坡，就能等于最大利润。
题解给的动态规划非常规，是一个2*n的数组。



### 题解:
~~~
class Solution {
    public int maxProfit(int[] prices) {
        int[] dp = new int[prices.length];
        for(int i = 1;i<dp.length;i++){
            if(prices[i]>prices[i-1])
                dp[i]=dp[i-1]+prices[i]-prices[i-1];
            else
                dp[i]=dp[i-1];
        }
        return dp[prices.length-1];
        
    }
}

~~~


## 55. 跳跃游戏 难度：中等


### 第一想法:

我看了例子之后，结合只有出现0才可能false，就想到了从末尾开始向前遍历，遍历到0开始判断前面的是否能够跨过这个0，所有0都能跨过就是true，有一个没法跨过就是false。
题解给的是从前往后，不断更新能到达的最远位置的。



### 题解:

~~~
class Solution {
    public boolean canJump(int[] nums) {
        if(nums.length==1)
            return true;
        for(int i = nums.length-2;i>=0;i--){
            if(nums[i]==0){
                int temp = i-1;
                while(temp>=0){
                    if(nums[temp]>i-temp)
                        break;
                    temp--;
                }
                if(temp<0)
                    return false;
            }
        }
        return true;
    }
}


~~~


## 45. 跳跃游戏 II 难度：中等


### 第一想法:

 每次跳跃都跳的尽量远，扩充上一次位置中能跳的最远的右边界，不断循环，直到右边界超过最后一个位置



### 题解:
~~~
class Solution {
    public int jump(int[] nums) {
        if(nums.length==1)
            return 0;
        int left = 0;
        int count = 1;
        int right = nums[0];
        while(right<nums.length-1){
            int temp_right=right;
            for(int i = left;i<=right;i++){
                temp_right=Math.max(i+nums[i],temp_right);
            }
            left = right;
            right=temp_right;
            count++;
        }
        return count;
    }
}

~~~
