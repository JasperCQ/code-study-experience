 **学习时长**


 
 
##  216. 组合总和 III 难度：中等


### 第一想法:

就是回溯算法，只是说返回值和参数的修改而已。还有就是剪枝部分需要注意



### 题解:
~~~
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        backtrack(k,n,1,new ArrayList<>());
        return this.result;
    }

    public void backtrack(int k, int target, int left,List<Integer> path){
        
        if(k==0) {
            if(target==0)
                this.result.add(new ArrayList<>(path));
            return;
        }
        if(target<left)
            return;
        
        for(int i = left; i<=10-k;i++){
            path.add(i);
            backtrack(k-1,target-i,i+1,path);
            path.remove(path.size()-1);
        }

    }
}

~~~


## 17. 电话号码的字母组合 难度：中等


### 第一想法:

就还是使用回溯法，只是有一些对字符串的处理要注意。



### 题解:

采用StringBuilder作为参数，方便后续的处理。

~~~

class Solution {
    private List<String> result = new ArrayList<>();
    String[] mapping = new String[] {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

    public List<String> letterCombinations(String digits) {
        if(digits.length()==0)
            return new ArrayList<String>();
        backtrack(0,digits,new StringBuilder());
        return this.result;
    }


    public void backtrack(int index,String digits, StringBuilder sb){

        if(index>=digits.length()) {
            this.result.add(sb.toString());
            return;
        }

        int digit = digits.charAt(index)-'0';
        for(int i = 0; i<this.mapping[digit].length();i++){
            sb.append(this.mapping[digit].charAt(i));
            backtrack(index+1,digits,sb);
            sb.deleteCharAt(sb.length()-1);
        }

    }
}

~~~



