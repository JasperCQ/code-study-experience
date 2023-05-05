# 代码随想录算法训练营13期 栈与队列2—— 20. 有效的括号 、1047. 删除字符串中的所有相邻重复项、 150. 逆波兰表达式求值


 
 **学习时长**
 
## 20. 有效的括号 难度：简单


### 第一想法: 

第一想法就是利用栈，因为明显最后出现的左括号要与最先出现的右括号进行匹配

~~~
class Solution {
    public boolean isValid(String s) {
        ArrayDeque<Character> stack = new ArrayDeque<>();

        ArrayList<Character> left_ls= new ArrayList<>();
        ArrayList<Character> right_ls= new ArrayList<>();
        left_ls.add('(');
        left_ls.add('[');
        left_ls.add('{');
        right_ls.add(')');
        right_ls.add(']');
        right_ls.add('}');

        for(int i=0;i<s.length();i++){
            //left brackets
            if(left_ls.contains(s.charAt(i))){
                stack.addFirst(s.charAt(i));
            }
            else{
                if(stack.size()==0||left_ls.indexOf(stack.removeFirst())!=right_ls.indexOf(s.charAt(i)))
                    return false;
            }
        }
        if (stack.size()>0)
            return false;
        return true;


    }
}

~~~


### 题解

### 困难:

采用了一个stack 两个大小为3的list，方便写，过程中还是deque 这个接口对应stack 的方法不熟



 
##  1047. 删除字符串中的所有相邻重复项 难度：1286分


### 第一想法

第一想法就是用栈来解决

~~~

class Solution {
    public String removeDuplicates(String s) {
        ArrayDeque<Character> stack = new ArrayDeque<>();

        for(int i = 0; i<s.length();i++){
            if (stack.size()==0)
                stack.addLast(s.charAt(i));
            else{
                if (stack.peekLast()==s.charAt(i))
                    stack.removeLast();
                else
                    stack.addLast(s.charAt(i));
            }
        }
        char[] res_char=new char[stack.size()];
        int cur=0;
        while(stack.size()>0){
            res_char[cur]=stack.pollFirst();
            cur++;
        }

        return new String(res_char);
    }
}

~~~


### 题解

### 困难
主要就是在于写栈和队列混合用的时候要注意别弄混







 
## 题目名字 难度：


### 第一想法

### 题解

### 困难
