
# 代码随想录算法训练营13期 第七章 回溯算法part01 


 
 **学习时长**
 
## 77. 组合  难度：中等


### 第一想法:
经典的回溯算法，组合问题的话，就是首先就是选择列表的问题，从前往后选就可以，然后剪支的部分要注意。


### 题解:

~~~
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> combine(int n, int k) {
        backtrack(k,1,n,new ArrayList<>());
        return this.result;
    }

    public void backtrack(int k, int left, int right,List<Integer> path){

        if(k==0) {
            this.result.add(new ArrayList<>(path));
            return;
        }

        for(int i = left; i<=right+1-k;i++){
            path.add(i);
            backtrack(k-1,i+1,right,path);
            path.remove(path.size()-1);
        }

    }
}

~~~



