
 
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



## 134. 加油站 难度：中等


### 第一想法:

其实没有想出来这个题，这个题关键在画图其实可以解决，而且也要想清楚什么情况是无解的


### 题解:
~~~
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;
        // 相当于图像中的坐标点和最低点
        int sum = 0, minSum = 0;
        int start = 0;
        for (int i = 0; i < n; i++) {
            sum += gas[i] - cost[i];
            if (sum < minSum) {
                // 经过第 i 个站点后，使 sum 到达新低
                // 所以站点 i + 1 就是最低点（起点）
                start = i + 1;
                minSum = sum;
            }
        }
        if (sum < 0) {
            // 总油量小于总的消耗，无解
            return -1;
        }
        // 环形数组特性
        return start == n ? 0 : start;
    }
}

~~~


## 135. 分发糖果 难度：困难


### 第一想法:

我最开始想的是找到最小的那个孩子然后处理，但是发现不对，
题解的先满足部分条件，再在满足另外一部分条件的基础上，又满足另一部分这种想法，确实不容易想到。之前也没遇到过



### 题解:
~~~
class Solution {
    /**
         分两个阶段
         1、起点下标1 从左往右，只要 右边 比 左边 大，右边的糖果=左边 + 1
         2、起点下标 ratings.length - 2 从右往左， 只要左边 比 右边 大，此时 左边的糖果应该 取本身的糖果数（符合比它左边大） 和 右边糖果数 + 1 二者的最大值，这样才符合 它比它左边的大，也比它右边大
    */
    public int candy(int[] ratings) {
        int len = ratings.length;
        int[] candyVec = new int[len];
        candyVec[0] = 1;
        for (int i = 1; i < len; i++) {
            candyVec[i] = (ratings[i] > ratings[i - 1]) ? candyVec[i - 1] + 1 : 1;
        }

        for (int i = len - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                candyVec[i] = Math.max(candyVec[i], candyVec[i + 1] + 1);
            }
        }

        int ans = 0;
        for (int num : candyVec) {
            ans += num;
        }
        return ans;
    }
}

~~~

