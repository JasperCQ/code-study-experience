
 
 **学习时长**
 
## 1005. K 次取反后最大化的数组和 难度：简单


### 第一想法:

其实做的时候，因为有几天没刷题了，感觉思路有点乱。我是采用sort两次这种方法比较直接，但是肯定时间复杂度会高一点



### 题解:
一个分情况讨论的简单贪心问题。
~~~
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        Arrays.sort(nums);
        int cur = 0;
        for(int i=0;i<k;i++){
            if(cur<nums.length && nums[cur]<0){
                nums[cur]=-1*nums[cur];
                cur++;
            }
            else {
                if((k-i)%2==0)
                    return Arrays.stream(nums).sum();
                Arrays.sort(nums);
                nums[0]=-1*nums[0];
                return Arrays.stream(nums).sum();                
            }
        }
        return Arrays.stream(nums).sum();
    }
}
~~~



##  难度：


### 第一想法:



### 题解:



##  难度：


### 第一想法:



### 题解:


