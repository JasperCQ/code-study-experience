# 代码随想录算法训练营13期 栈与队列2—— 20. 有效的括号 、1047. 删除字符串中的所有相邻重复项、 150. 逆波兰表达式求值


 
 **学习时长：可能2h？因为分开做的记不清了**
 
## 20. 有效的括号 难度：简单


### 第一想法: 

第一想法就是利用栈，因为明显最后出现的左括号要与最先出现的右括号进行匹配



### 题解

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







 
## 150、逆波兰表达式求值 难度：中等


### 第一想法:

因为好久没写了，现在回来补，不过看了一些逆波兰的解释，大概就知道是用栈来做，然后找了下规律，应该是遇到运算符前两个数出栈运算，结果再入栈。

### 题解：

~~~

class Solution {
    public int evalRPN(String[] tokens) {
        HashMap<String,BinaryOperator<Integer>> ops = new HashMap<>();
        ops.put("+",(x,y)->x+y);
        ops.put("-",(x,y)->x-y);
        ops.put("*",(x,y)->x*y);
        ops.put("/",(x,y)->x/y);
        ArrayDeque<String> stack= new ArrayDeque<>();
        if(tokens.length==1)
            return Integer.valueOf(tokens[0]).intValue();
        for(int i =0 ;i<tokens.length;i++){
            if(ops.containsKey(tokens[i])){
                 int num1=Integer.valueOf(stack.pop()).intValue();
                 int num2=Integer.valueOf(stack.pop()).intValue();
                 Integer temp = ops.get(tokens[i]).apply(num2,num1);
                 stack.push(temp.toString());
            }
            else{
                stack.push(tokens[i]);
                }
        }

        return Integer.valueOf(stack.pop()).intValue();

    }
}

~~~

### 困难：

我做的时候，因为我觉得用一个value为lambda表达式的hashmap来做是最方便的。但是因为之前也没写过类似的，所以再写的时候用到了一些自己之前也没用过的方法，都是在google 和 gpt 的帮助下。

