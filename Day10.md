# 代码随想录算法训练营13期  232.用栈实现队列、 225. 用队列实现栈 


 
 **学习时长**
 
 
 
## 232. 用栈实现队列 难度：简单

~~~

class MyQueue {

    private Deque<Integer> instack;
    private Deque<Integer> outstack;

    public MyQueue() {
        this.instack= new ArrayDeque<>();
        this.outstack = new ArrayDeque<>();

    }

    public void push(int x) {
    this.instack.push(x);
    }

    public int pop() {
        if (outstack.isEmpty()){
            in2out();
        }
        return outstack.pop();
    }

    public int peek() {
        if (outstack.isEmpty()) {
            in2out();
        }
        return outstack.peek();
    }

    public boolean empty() {
        return instack.isEmpty() && outstack.isEmpty();
    }

    private void in2out(){
        while (!instack.isEmpty()) {
            outstack.push(instack.pop());
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */

~~~

### 第一想法:

之前遇到过这种题，知道是两个栈，一个入栈，一个出栈来完成队列的功能。

### 题解

### 困难：

之前不了解java的deque可以的功能和相关的方法





 

 
## 225. 用队列实现栈 难度：简单


### 第一想法

### 题解

### 困难



 

