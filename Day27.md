
 
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



## 40. 组合总和 II 难度：中等


### 第一想法:

最开始看的时候，还没意识到这个元素重，但不能复选的组合题目的特殊处，但是看了示例，感觉是需要排序的。
果然是需要排序后，进行剪枝，这个剪枝的if其实还不是特别直接。



### 题解:

~~~

class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
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
            if(i>start && candidates[i]==candidates[i-1])
                continue;
            path.add(candidates[i]);
            backtrack(i+1,target-candidates[i],candidates,path);
            path.remove(path.size()-1);
        }

    }
}
~~~


##   131.分割回文串  难度：中等


### 第一想法:

第一下看这个题没有跟前面的组合问题联系起来，但是其实只要画出回溯树，就能看出来本质没变。



### 题解:
提交完发现，时间比较慢，看了官方题解，发现在判断回文子串这部分存在很多重复计算，可以通过dp算法或者是记忆化搜索来提前规范哪些是回文子串，不然的话直接使用双指针在循环中会存在重复计算。

~~~
class Solution {
    private List<List<String>> result = new ArrayList<>();
    public List<List<String>> partition(String s) {
        backtrack(new StringBuilder(s),new ArrayList<>());
        return this.result;
    }

    public void backtrack(StringBuilder sb, List<String> path){
        if(sb.length()==0)
            this.result.add(new ArrayList<>(path));


        for(int i = 0; i<sb.length();i++){
            String temp = sb.substring(0,i+1);
            if(isPalindrome(temp)) {
                path.add(temp);
                backtrack(new StringBuilder(sb.substring(i+1,sb.length())),path);
                path.remove(path.size()-1);
            }
            
            
        }


    }

    public boolean isPalindrome(String s){

        int left = 0;
        int right = s.length()-1;
        while(left<right){
            if(s.charAt(left)!=s.charAt(right))
                return false;
            left++;
            right--;
        }
        return true;

    }
}

~~~


