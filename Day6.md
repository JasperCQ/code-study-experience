# 代码随想录算法训练营13期  242.有效的字母异位词 、349. 两个数组的交集、202. 快乐数、1. 两数之和


 
 **学习时长 接近 2h**
 
## 242. 有效的字母异位词 难度：简单


### 第一想法：
理解了一下字母异位词，很明显用一个hashmap 就可以解决。


~~~

class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length())
            return false;
        //遍历s
        HashMap<Character, Integer> dictionary = new HashMap<Character, Integer>();
        for (int i = 0; i < s.length(); i++) {
            if (dictionary.containsKey(s.charAt(i)))
                dictionary.replace(s.charAt(i), dictionary.get(s.charAt(i)) + 1);
            else
                dictionary.put(s.charAt(i), 1);


        }
        //遍历t
        for (int i = 0; i < t.length(); i++) {
            if (dictionary.containsKey(t.charAt(i)))
                dictionary.replace(t.charAt(i), dictionary.get(t.charAt(i))-1);
            else
                return false;

        }
            
        for(Character key:dictionary.keySet()){
            if(dictionary.get(key)!=0)
                return false;
        }
        return true;
    }
}

~~~
### 题解:
第一次遍历存储s的字符频次，第二次遍历t，最后看是否能对上


### 困难：

写的时候还没有我想象的那么简单，一个是，我习惯了python中的字典，相比来说，java中的hashmap并不熟。



## 349. 两个数组的交集 难度：简单



### 第一想法：

第一想法是，用一个set 存储nums1中的数字，然后遍历nums2，如果set1有的话，就把答案放到res set 中。

~~~

class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set1= new HashSet<>();
        HashSet<Integer> res = new HashSet<>();
        for(int num: nums1){
            set1.add(num);
        }
        for(int num: nums2){
            if(set1.contains(num)){
                res.add(num);
            }
        }

        int[] res_ls=new int[res.size()];
        int count=0;
        for(int num:res){
            res_ls[count]=num;
            count++;
        }
        return res_ls;
    }
}

~~~

### 题解:


### 困难

md，写了半天，就是不熟悉set 和 hashset 的一些容器的规矩，想把set转换成int[] 返回，查了好久。
最后还是只能遍历




## 202. 快乐数 难度：简单



### 第一想法:

这道题第一想法，还真没有联系到哈希表和这道题，但是确实无限循环这个加粗字应该关注

~~~

class Solution {
    public boolean isHappy(int n) {
        Set<Integer> sum_set= new HashSet<>();
        sum_set.add(n);
        while (n!=1){
            int cur=n;
            int next=0;
            while(cur>0){
                int temp=cur%10;
                next+=temp*temp;
                cur=cur/=10;
            }
            if(sum_set.contains(next))
                return false;
            else
                sum_set.add(next);
            n=next;
        }
        return true;
    }
}

~~~

### 题解：

官方题解还给了链表判断是否有环的解法，这个其实很好理解，也很巧妙，就是，把走过的路径变成链表，就联系上前面做过的题了，
不过还是用set 来判断是否重复会更简单理解。

### 困难:
想出这个解法感觉并不容易。




## 1. 两数之和 难度：简单


### 第一想法：

使用哈希表的话，就是比对现在target减去现在遍历的数，能否等于哈希表中的数

~~~

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> sites= new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            if( sites.containsKey(target-nums[i]))
                return new int[]{i,sites.get(target-nums[i])};
            sites.put(nums[i],i);
        }
        return new int[]{-1,-1};
    }
}

~~~

### 题解

### 困难

