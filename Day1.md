# 代码随想录算法训练营第一天|704、二分查找、27、移除元素 

**时长：4道题2个小时左右，其中35题研究二分查找的边界搜索花了比较多时间理解**

## 704 二分查找 难度：简单
**题目分析:** 最原始的二分查找题目。
java code如下

~~~
class Solution {
    public int search(int[] nums, int target) {
        int left=0;
        int right=nums.length-1;
        
        while(left<=right){
            int mid=left+(right-left)/2;

            //target在右半边
            if(nums[mid]<target){
                left=mid+1;
            }
            //target在左半边
            else if (nums[mid]>target){
                right=mid-1;
            }
            //匹配
            else if (nums[mid]==target){
                return mid;
            }
        }
        //前面未匹配
        return -1;

    }
}
~~~

### 在这里分享一些自己学自labuladong的一些二分查找知识的灵感和启发：

其实在二分查找中，最关键的问题是一些细节问题。 主要有以下几个点：

1.左右指针的初始值
2.while循环的条件判断
3.左指针和右指针的更新规则

从第一个点开始说，我自己的理解是，其实right 可以设为长度-1，也可以设为长度，这主要其实取决于你想要每次搜索的情况是闭区间还是开区间。如果是想要闭区间，那么你要不遗漏数组所有元素，又不会index out，那么当然就是设置为[0.长度-1].同理如果想要开区间，那么就会变成[0,长度)

而选择闭区间还是开区间，同样也影响着第二点，while循环中的条件，当极限情况结束while循环时，如果是闭区间那么，应该是[left,left-1]这样时，搜索区间里才没有元素，就不会遗漏。那么就应该是left<=right. 反之如果是开区间.[left,left) 时就已经没有树在搜索区间里了。

同样的，这个也影响着第三点，left 和 right 的更新，大家可以自己思考一下，然后后面遇到更多复杂的二分查找时，可以试着这个思路思考一下。

**这个也是我自己的灵感，十分欢迎大家指正**



## 35 搜索插入位置 难度：简单
**题目分析:** 最原始的二分查找题目上，只是对未找到的情况，对返回值，不再是704题的-1。。

java code如下

~~~
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left=0;
        int right=nums.length-1;
        int ans=nums.length;
        while(left<=right){
            int mid=left+(right-left)/2;
            //target在左半边,此时找到了一个可能符合答案的数，也就是目前暂时搜到的最小的，但又大于等于target的
            if(nums[mid]>=target){
                ans=mid;
                right=mid-1;
            }
            //target 在右半边
            else{
                left=left+1;
            }
        }
        //未找到，返回插入位置
        return ans;

    }


}
~~~

**题解**

相比704题，这个题多的部分，我自己觉得还不是那么简单好想的。我参考了labuladong 和 官方题解的思路，我自己觉得还是官方的做法我更能够理解一点。
将题目要求转化为求到第一个大于等于target的坐标。那么在while循环中核心的部分就是如何体现这个求 大于等于target 的左侧边界这个事情。





## 34 在排序数组中查找元素的第一个和最后一个位置 难度：中等
**题目分析:** 寻找左侧边界和右侧边界的二分查找问题。

java code如下

~~~
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left=0;
        int right=nums.length-1;
        int ans_l= nums.length;
        int ans_r= nums.length;

        //寻找左边界
        while(left<=right){
            int mid=left+(right-left)/2;

            if(target<=nums[mid]){
                ans_l=mid;
                right=mid-1;
            }
            else{
                left=mid+1;
            }
            
        }
        if(ans_l==nums.length || nums[ans_l]!=target ) 
            return new int[]{-1,-1};

        //寻找右边界
        left=0;
        right=nums.length-1;
        while(left<=right){
            int mid=left+(right-left)/2;

            if(target>=nums[mid]){
                ans_r=mid;
                left=mid+1;
            }
            else{
                right=mid-1;
            }
        }
        return new int[]{ans_l,ans_r};
    }
}

~~~

**题解**
用了两个二分查找，分别找左边界和右边界。其中在寻找完左边界之后，就可以进行判断是否存在target。


## 27 移除元素 难度：简单
**题目分析:**  双指针法，左指针指向新数组的末尾，右指针指向当前遍历的元素。

java code如下
~~~

class Solution {
    public int removeElement(int[] nums, int val) {
        int left=0;
        int right=0;

        while (right<nums.length){
            if (nums[right]!=val){
                nums[left]=nums[right];
                left++;
            }
            right++;
        }
        return left;
    }
    
}

~~~

**题解**
主要是利用双指针这个思想，然后知道左右指针各代表什么含义，还有就是根据题意，返回的长度，是开区间。
