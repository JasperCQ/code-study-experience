# 代码随想录算法训练营13期 哈希表part02  454.四数相加II 、 383. 赎金信、 15. 三数之和、18. 四数之和


 
 **学习时长**
 
## 454. 四数相加 II 难度：中等



### 第一想法：

第一想法其实想用dp，不过是个四维的有点麻烦，然后就想到了其实是之前两数之和的一个叠加版就可以，不知道时间复杂度合格不

~~~
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        HashMap<Integer,Integer> num_sum_1= new HashMap<>();
        //遍历nums1
        for(int key : nums1){
            if(num_sum_1.containsKey(key))
                num_sum_1.replace(key,num_sum_1.get(key)+1);
            else
                num_sum_1.put(key,1);
        }
        //遍历nums2
        HashMap<Integer,Integer> num_sum_2= new HashMap<>();
        for(int key : nums2){
            if(num_sum_2.containsKey(key))
                num_sum_2.replace(key,num_sum_2.get(key)+1);
            else
                num_sum_2.put(key,1);
        }
        //遍历nums3
        HashMap<Integer,Integer> num_sum_3= new HashMap<>();
        for(int key : nums3){
            if(num_sum_3.containsKey(key))
                num_sum_3.replace(key,num_sum_3.get(key)+1);
            else
                num_sum_3.put(key,1);
        }
        //遍历nums4
        HashMap<Integer,Integer> num_sum_4= new HashMap<>();
        for(int key : nums4){
            if(num_sum_4.containsKey(key))
                num_sum_4.replace(key,num_sum_4.get(key)+1);
            else
                num_sum_4.put(key,1);
        }
        //组合它们
        HashMap<Integer,Integer> num_sum_target_0= new HashMap<>();
        for(Map.Entry<Integer,Integer> entry: num_sum_1.entrySet()){
            num_sum_target_0.put(0-entry.getKey(), entry.getValue());
        }
        HashMap<Integer,Integer> num_sum_target_1= new HashMap<>();
        for(Map.Entry<Integer,Integer> entry: num_sum_target_0.entrySet()){
            for(Map.Entry<Integer,Integer> entry_2: num_sum_2.entrySet()){
                int target_new=entry.getKey()-entry_2.getKey();
               if(num_sum_target_1.containsKey(target_new))
                   num_sum_target_1.replace(target_new,num_sum_target_1.get(target_new)+entry.getValue()*entry_2.getValue());
               else
                   num_sum_target_1.put(target_new,entry.getValue()*entry_2.getValue());
            }
        }
        
        HashMap<Integer,Integer> num_sum_target_2= new HashMap<>();
        for(Map.Entry<Integer,Integer> entry: num_sum_target_1.entrySet()){
            for(Map.Entry<Integer,Integer> entry_2: num_sum_3.entrySet()){
                int target_new=entry.getKey()-entry_2.getKey();
                if(num_sum_target_2.containsKey(target_new))
                    num_sum_target_2.replace(target_new,num_sum_target_2.get(target_new)+entry.getValue()*entry_2.getValue());
                else
                    num_sum_target_2.put(target_new,entry.getValue()*entry_2.getValue());
            }
        }
        
        int count=0;
        for(Map.Entry<Integer,Integer> entry: num_sum_4.entrySet()){
            if(num_sum_target_2.containsKey(entry.getKey()))
                count+=num_sum_target_2.get(entry.getKey())*entry.getValue();
        }
        return count;
        
        
    }
}
~~~

### 题解:
我看了官方题解hhh，和我的核心思想是一样的，时间复杂度，从维度上来说也是一样的，但是显然两两分组，第二次分组时比较的做法，会比我现在这种做法好理解的多，平方项的常数也更小

### 困难：

太难写了，极容易弄混，我自己写完一遍过，我自己也很惊讶。


## 383. 赎金信 难度：简单



### 第一想法：

这个很简单，用一个hashmap存magazine的字符就行

~~~

class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        HashMap<Character,Integer> ChDict= new HashMap<>();
        for(int i=0;i<magazine.length();i++){
            if(ChDict.containsKey(magazine.charAt(i)))
                ChDict.replace(magazine.charAt(i),ChDict.get(magazine.charAt(i))+1);
            else
                ChDict.put(magazine.charAt(i),1);
        }
        
        for(int i=0;i<ransomNote.length();i++){
            if(!ChDict.containsKey(ransomNote.charAt(i)) || ChDict.get(ransomNote.charAt(i))==0)
                return false;
            else
                ChDict.replace(ransomNote.charAt(i),ChDict.get(ransomNote.charAt(i))-1);
        }
        return true;
    }
}
~~~

### 题解:

官方题解思想和我的差不多。

### 困难



## 15. 三数之和 难度：中等


### 第一想法：
理解题目还不是那么容易，首先是用一个哈希set，先遍历一遍，去除所有重复的，即遍历过程，后面重复的都直接不要了，然后把这个set变为数组，对这个数组进行双重循环遍历，且只扫后面的。
判断set中是否有正好负的

~~~
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n=nums.length;
        Arrays.sort(nums);
        
        List<List<Integer>> res= new ArrayList<>();
        for(int i=0;i<n;i++){
            if (i>0 && nums[i]==nums[i-1])
                continue;

            int target=-1*nums[i];
            int left=i+1;
            int right=n-1;
            while(left<right){
                if(left>i+1 && nums[left]==nums[left-1]){
                    left++;
                    continue;
                }
                if (right<n-1 && nums[right]==nums[right+1]){
                    right--;
                    continue;
                }

                if(nums[left]+nums[right]>target){
                    right--;
                }
                else if (nums[left]+nums[right]<target){
                    left++;
                }
                else{
                    List<Integer> temp = new ArrayList<>();
                    temp.add(nums[i]);
                    temp.add(nums[left]);
                    temp.add(nums[right]);
                    res.add(temp);
                    right--;
                }
            }
        }
        return res;
    }
}

~~~

### 题解:

这题是真挺难的，首先是如果用哈希表会很麻烦，直接三重循环，考虑到去重，以及时间复杂度，也不够效率，但是可以将问题转化为如果固定a的话，就转为一个一个有序数组中两个数之和为某个值。
然后细节就是要注意相邻元素如果重复的话，是不重复添加的。
**以后遇到时间复杂度在O（NlogN）以上的数组题，可以考虑先排个序先**


### 困难：
不容易想到这个思路，其中的一些细节也是容易写错的


## 18. 四数之和 难度：中等


### 第一想法：

是和上一个题一个思路，

~~~
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        int n=nums.length;
        Arrays.sort(nums);
        List<List<Integer>> res= new ArrayList<>();
        for(int i=0;i<n;i++){
            //重复跳过
            if (i>0 && nums[i]==nums[i-1])
                continue;
            
            for(int j =i+1;j<n;j++){
                //重复跳过
                if (j>i+1 && nums[j]==nums[j-1])
                    continue;
                //进入双指针部分
                long cur_target=(long) target-nums[i]-nums[j];
                int left=j+1;
                int right=n-1;
                while(left<right){
                    if(left>j+1 && nums[left]==nums[left-1]){
                        left++;
                        continue;
                    }
                    if (right<n-1 && nums[right]==nums[right+1]){
                        right--;
                        continue;
                    }

                    if(nums[left]+nums[right]>cur_target){
                        right--;
                    }
                    else if (nums[left]+nums[right]<cur_target){
                        left++;
                    }
                    else{
                        List<Integer> temp = new ArrayList<>();
                        temp.add(nums[i]);
                        temp.add(nums[j]);
                        temp.add(nums[left]);
                        temp.add(nums[right]);
                        res.add(temp);
                        right--;
                    }
                }
                
            }
        }
        return res;
    }
}

~~~

### 题解：

在实际解题中确实是和上一个是一个思路，但是有一些细节需要注意

### 困难：

注意到用例无法全对，在leetcode中是给出了报错的例子，所以能够检查出是由于超出了int取值范围，所以给可能超界的地方 转换类型为long 。

