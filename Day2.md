# 代码随想录算法训练营第二天 | 977 有序数组的平方、209 长度最小的子数组、59 螺旋矩阵II
 
 **学习时长1h 10 min左右**
 
## 209 长度最小的子数组 难度：中等

### 第一想法：

第一想法其实就是看到题目求连续子数组的形式，然后判断条件又比较简单，所以直接考虑用滑动窗口法。

### code
~~~

class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int left=0;
        int right=0;
        int sum=0;
        int res=Integer.MAX_VALUE;
        while(right<nums.length){
            //扩大窗口
            sum+=nums[right];
            right++;

            //缩小窗口
            while(sum>=target){
                res=Math.min(res,right-left);
                sum-=nums[left];
                left++;
            }
        }

        if(res==Integer.MAX_VALUE)
            return 0;
        return res;
    }
}

~~~


### 题解:
其实滑动窗口法的核心就是什么时候缩小窗口，什么时候扩大窗口，写好这两个部分的逻辑，就能写出代码，这道题的话就是用一个 sum 变量来记录窗口中的和，用来判断应该缩小还是扩大。
需要把返回值初始设为最大值，其实根据题意的话大于10^5 就可以了。


### 困难：
之前做过滑动窗口法，虽然第一时间没有记住框架，但是有印象，再加上知道核心思想，所以没有什么困难。


## 977. 有序数组的平方 难度：1130分


### 第一想法:

首先，看到这是一个排了序的数组，然后有负数的可能存在，那么，绝对值最大的数只可能出现在数组两端，所以左边一个指针，右边一个指针，共同遍历，把答案数组从后往前填充就行。

### code

~~~

class Solution {
    public int[] sortedSquares(int[] nums) {
        int left=0;
        int right=nums.length-1;
        int[] res=new int[nums.length];
        int cur=nums.length-1;
        while (cur>=0){
            //左边小
            if (nums[left]>0 || Math.abs(nums[left])<Math.abs(nums[right])){
                res[cur]=nums[right]*nums[right];
                right--;
                cur--;
            }
            else{
                res[cur]=nums[left]*nums[left];
                left++;
                cur--;
            }

        }
        return res;
    }
}

~~~

### 题解:
这道题我java语言中用了Math 库，然后我觉得这道题没什么需要讲的。

### 困难




## 59. 螺旋矩阵 II 难度：中等


### 第一想法

因为这种螺旋矩阵，再加上看了下题，感觉应该就是模拟的思路，然后又隐约有点印象，就采取了设置4个边界，当遍历超过边界时，就转向，就是模拟生成矩阵。


~~~

class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res= new int[n][n];
        int upperbound=0;
        int lowerbound=n-1;
        int leftbound=0;
        int rightbound=n-1;
        int cur_x=0;
        int cur_y=0;
        int count=1;
        
        while(true){
            //向右走
            while(cur_y<=rightbound){
                res[cur_x][cur_y]=count;
                cur_y++;
                count++;
            }
            
            upperbound++;
            //调回来一格，可以继续走
            cur_y--;
            count--;
            if(count>=n*n)
                break;

            //向下走
            while(cur_x<=lowerbound){
                res[cur_x][cur_y]=count;
                cur_x++;
                count++;
            }
            rightbound--;
            //调回来一格，可以继续走
            cur_x--;
            count--;
            if(count>=n*n)
                break;

            //向左走
            while(cur_y>=leftbound){
                res[cur_x][cur_y]=count;
                cur_y--;
                count++;
            }
            lowerbound--;
            //调回来一格，可以继续走
            cur_y++;
            count--;
            if(count>=n*n)
                break;

            //向上走
            while(cur_x>=upperbound){
                res[cur_x][cur_y]=count;
                cur_x--;
                count++;
            }
            leftbound++;
            //调回来一格，可以继续走
            cur_x++;
            count--;
            if(count>=n*n)
                break;
                
        }
        
        return res;
    }
}

~~~

### 题解

我觉得这道题从思路上没什么特别好说的

### 困难

有一个点是，我自己最开始是设置while 条件是 count <= n*n ，然后发现会超时，我大概思考了一下觉得很有可能是，在里面完成模拟后，但是count并不会大于N*N ，所以一直不出来，所以我就改成了在每个方向走完后，加一个if 来break。
