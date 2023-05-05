# 代码随想录算法训练营13期  232.用栈实现队列、 225. 用队列实现栈 


 
 **学习时长：1h**
 
 
 
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


### 第一想法：

第一想法也是想用类似栈模拟队列的方式，但是发现不行。看了题解后，写了。
~~~
class MyStack {
    private Deque<Integer> queue1;
    private Deque<Integer> queue2;

    public MyStack() {
        this.queue1= new ArrayDeque<>();
        this.queue2= new ArrayDeque<>();
    }

    public void push(int x) {
        this.queue1.addLast(x);
    }

    public int pop() {
        while(this.queue1.size()>1){
            this.queue2.addLast(this.queue1.pollFirst());
        }
        int res = this.queue1.pollFirst();
        this.queue1=this.queue2;
        this.queue2=new ArrayDeque<Integer>();
        return res;
    }

    public int top() {
        while(this.queue1.size()>1){
            this.queue2.addLast(this.queue1.pollFirst());
        }
        int res = this.queue1.pollFirst();
        this.queue2.addLast(res);
        this.queue1=this.queue2;
        this.queue2=new ArrayDeque<Integer>();
        return res;
    }

    public boolean empty() {
        if (this.queue1.size()==0){
            return true;
        }
        else
            return false;
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */

~~~

### 题解

### 困难

主要也是在于对于Deque 这个接口的方法不熟




 

