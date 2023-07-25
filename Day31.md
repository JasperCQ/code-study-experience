# 代码随想录算法训练营13期  第八章 贪心算法 part01


 
 **学习时长**
 
## 455. 分发饼干 难度：简单


### 第一想法:

就是最小的s分配给最小的g，所以对两个数组排个序就行。



### 题解:
~~~
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int p_s = 0;
        int p_g = 0;
        int res = 0;
        while(p_s<s.length && p_g<g.length){
            if(s[p_s]>=g[p_g]){
                res++;
                p_g++;
            }
            p_s++;
        }
        return res;
    }
}

~~~



## 376. 摆动序列 难度：中等


### 第一想法:

这题贪心真的不好想，然后有dp的解法，但我暂时不去看
贪心要考虑三个特殊情况



### 题解:
~~~
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if (nums.length <= 1) {
            return nums.length;
        }
        //当前差值
        int curDiff = 0;
        //上一个差值
        int preDiff = 0;
        int count = 1;
        for (int i = 1; i < nums.length; i++) {
            //得到当前差值
            curDiff = nums[i] - nums[i - 1];
            //如果当前差值和上一个差值为一正一负
            //等于0的情况表示初始时的preDiff
            if ((curDiff > 0 && preDiff <= 0) || (curDiff < 0 && preDiff >= 0)) {
                count++;
                preDiff = curDiff;
            }
        }
        return count;
    }
}


~~~




## 53. 最大子数组和 难度：中等


### 第一想法:

其实最开始想的和题解的贪心差不多，但是没注意是只要和，如果是要返回整个数组的话，其实过程还是比较麻烦的，
然后这个题其实用dp做我感觉才是比较经典的做法。


### 题解:

~~~
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums.length == 1){
            return nums[0];
        }
        int sum = Integer.MIN_VALUE;
        int count = 0;
        for (int i = 0; i < nums.length; i++){
            count += nums[i];
            sum = Math.max(sum, count); // 取区间累计的最大值（相当于不断确定最大子序终止位置）
            if (count <= 0){
                count = 0; // 相当于重置最大子序起始位置，因为遇到负数一定是拉低总和
            }
        }
       return sum;
    }
}


~~~
