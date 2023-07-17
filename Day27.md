
 
 **学习时长**
 
## 39. 组合总和 难度：中等


### 第一想法: 

就还是回溯算法的能做的，因为是组合问题，所以还是使用一个start变量就行，只是说，在循环那里要注意，可以包括递归自身这个节点。



### 题解:

比较难想到的是，我没想到的剪枝部分，可以通过先排序，从小到大排，其实就可以当前面的数已经大于target的时候，就没必要考虑后面的了，
~~~
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        backtrack(0,target,candidates,new ArrayList<>());
        return this.result;
    }

    public void backtrack(int start,int target,int[] candidates,ArrayList<Integer> path){
        if(target<0)
            return;
        if(target==0){
            this.result.add(new ArrayList<>(path));
        }
        for(int i = start;i<candidates.length;i++){
            path.add(candidates[i]);
            backtrack(i,target-candidates[i],candidates,path);
            path.remove(path.size()-1);
        }
        
    }
}


~~~



##  难度：


### 第一想法:



### 题解:


##  难度：


### 第一想法:



### 题解:


