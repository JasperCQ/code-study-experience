

 
 **学习时长**
 
## 491. 递增子序列 难度：中等


### 第一想法:

确实是炸一看和子集II很像，但是实际上递增子序列，会导致之前用的先排序的方法不起作用，可以换成构造used集合来规避选择重复的元素



### 题解:
~~~
class Solution {
   private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> findSubsequences(int[] nums) {
        backtrack(0,nums,new ArrayList<>());
        return this.result;
    }

    public void backtrack(int start,int[] nums,ArrayList<Integer> path){
        if(path.size()>=2)
            this.result.add(new ArrayList<>(path));

        if(start==nums.length)
            return;
        HashSet<Integer> used = new HashSet<>();
        for(int i = start;i<nums.length;i++){
            if(used.contains(nums[i]))
                continue;
            if(path.size()>0 && nums[i]<path.get(path.size()-1))
                continue;
            used.add(nums[i]);
            path.add(nums[i]);
            backtrack(i+1,nums,path);
            path.remove(path.size()-1);
        }

    }
}

~~~


## 46. 全排列 难度：中等


### 第一想法:

排列的话，其实思路挺简单的，就是不能用start，但是又要排除之前用过的，我本来考虑是采取传入不同的list，但是比较复杂，还不如直接的思路就是参数多个boolean数组。



###  题解:
~~~
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> permute(int[] nums) {
        backtrack(nums,new ArrayList<>(),new boolean[nums.length]);
        return this.result;
    }

    public void backtrack(int[] nums, List<Integer> path, boolean[] used){
        if(path.size()==nums.length)
            this.result.add(new ArrayList<>(path));

        for(int i = 0; i<nums.length;i++){
            if(used[i])
                continue;
            path.add(nums[i]);
            used[i]=true;
            backtrack(nums,path,used);
            path.remove(path.size()-1);
            used[i]=false;
        }


    }
}

~~~


## 47. 全排列 II 难度：中等


### 第一想法:

就是在上一个题的基础上加入了重复的元素，要保证答案不重复。
其实就是结合了前面的内容，最开始我没想好排序后那个操作能否用到这个题，于是我用了多加一个set来去重的方法，是一定可以的。
不过发现其实本质是一样的，


### 题解:
~~~
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> permuteUnique(int[] nums) {
        backtrack(nums,new ArrayList<>(),new boolean[nums.length]);
        return this.result;
    }
    public void backtrack(int[] nums, List<Integer> path, boolean[] used){
        if(path.size()==nums.length)
            this.result.add(new ArrayList<>(path));

        HashSet<Integer> used_set = new HashSet<>();
        for(int i = 0; i<nums.length;i++){
            if(used[i])
                continue;
            if(used_set.contains(nums[i]))
                continue;
            path.add(nums[i]);
            used[i]=true;
            used_set.add(nums[i]);
            backtrack(nums,path,used);
            path.remove(path.size()-1);
            used[i]=false;
        }


    }
}

~~~

