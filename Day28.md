

 
 **学习时长**
 
## 93.复原IP地址 难度：


### 第一想法:

第一想法还是采用回溯法解决。



### 题解:
在实际处理过程中，一个是参数的选择，我最开始选择的Stringbuilder，因为最后是要求字符串嘛，但是实际过程中发现，Stringbuilder作为参数，因为要加点。挺容易出错的。改成list，最后再join会更清晰

~~~
class Solution {
    private List<List<String>> result = new ArrayList<>();

    public List<String> restoreIpAddresses(String s) {
        backtrack(0,new StringBuilder(s),new ArrayList<>());
        List<String> res = new ArrayList<>();
        for(List<String> ips: this.result){
            System.out.println(ips);
            res.add(String.join(".",ips));
        }
        return res;
    }


    public void backtrack(int count,StringBuilder sb,List<String> path){
        if(count==4) {
            if (sb.length() == 0) {
                
                this.result.add(new ArrayList<>(path));
            }
            else
                return;
        }

        if(sb.length()<=3) {
            for (int i = 0; i < sb.length(); i++) {
                if(sb.charAt(0)=='0' && i>0)
                    break;
                String temp = sb.substring(0, i + 1);
                int ip = Integer.parseInt(temp);
                if(ip<=255){
                    path.add(temp);
                    backtrack(count+1,new StringBuilder(sb.substring(i+1,sb.length())),path);
                    path.remove(path.size()-1);
                }

            }
        }
        else{
            for (int i = 0; i < 3; i++) {
                if(sb.charAt(0)=='0' && i>0)
                    break;
                String temp = sb.substring(0, i + 1);
                int ip = Integer.parseInt(temp);
                if(ip<=255){
                    path.add(temp);
                    backtrack(count+1,new StringBuilder(sb.substring(i+1,sb.length())),path);
                    path.remove(path.size()-1);
                }

            }
        }

    }
}

~~~


## 78. 子集 难度：中等


### 第一想法:

这个题其实就是最基础的回溯算法的解法，只是说在添加到结果那里，不是直到叶节点才添加，而是每个节点都添加。


### 题解:
~~~
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> subsets(int[] nums) {
        backtrack(0,nums,new ArrayList<>());
        return this.result;
    }

    public void backtrack(int start,int[] nums,ArrayList<Integer> path){
        this.result.add(new ArrayList<>(path));
        if(start==nums.length)
            return;
        for(int i = start;i<nums.length;i++){
            path.add(nums[i]);
            backtrack(i+1,nums,path);
            path.remove(path.size()-1);
        }

    }
}

~~~


## 90. 子集 II 难度：中等


### 第一想法:

这个就是有重，的子集题目嘛，结合前面组合的解法排序后剪枝就可以。


### 题解:
~~~
class Solution {
    private List<List<Integer>> result = new ArrayList<>();
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        backtrack(0,nums,new ArrayList<>());
        return this.result;
    }
    
    public void backtrack(int start,int[] nums,ArrayList<Integer> path){
        this.result.add(new ArrayList<>(path));
        if(start==nums.length)
            return;
        for(int i = start;i<nums.length;i++){
            if(i>start && nums[i]==nums[i-1])
                continue;
            path.add(nums[i]);
            backtrack(i+1,nums,path);
            path.remove(path.size()-1);
        }

    }
}

~~~

