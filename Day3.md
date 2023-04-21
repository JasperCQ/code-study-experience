# 代码随想录算法训练营13期Day3： 203.移除链表元素 、 707.设计链表、206.反转链表 


 **学习时长 45min大概**
 
## 203 移除链表元素 难度：简单


### 第一想法:

移除链表元素，就首先定义虚拟dummy节点，方便之后return 新的头节点，然后循环里面，就执行判读，然后删除逻辑就行。

~~~
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(-1,head);
        ListNode pre = dummy;

        while(head!=null){
            if (head.val==val){
                pre.next=head.next;
            }
            else{
                pre=pre.next;
            }
            head=head.next;
        }
        return dummy.next;
    }
}


~~~

### 题解

### 困难




## 707. 设计链表 难度：中等


### 第一想法: 

设计链表，看了下题目的要求，用单链表节点设计就可以，类那里给两个属性，dummy和size，后续那些方法的实现就按要求就应该可以

~~~

class MyLinkedList {
    private ListNode dummy;
    private int size;

    public MyLinkedList() {
        this.dummy= new ListNode(-1);
        this.size=0;
    }
    
    public int get(int index) {
        if(index>=size)
            return -1;
        ListNode cur=this.dummy;
        for(int i=0;i<index;i++){
            cur=cur.next;
        }
        return cur.next.val;

    }
    
    public void addAtHead(int val) {
        ListNode temp=this.dummy.next;
        ListNode cur = new ListNode(val,temp);
        this.dummy.next= cur;
        this.size++;
    }
    
    public void addAtTail(int val) {
        ListNode temp=this.dummy;
        while(temp.next!=null){
            temp=temp.next;
        }
        ListNode cur = new ListNode(val);
        temp.next=cur;
        this.size++;
    }
    
    public void addAtIndex(int index, int val) {
        ListNode cur=this.dummy;
        if(index<=this.size){
            for(int i=0;i<index;i++){
                cur=cur.next;
            }
            ListNode temp= cur.next;
            cur.next= new ListNode(val,temp);
            this.size++;
        }
        
    }
    
    public void deleteAtIndex(int index) {
        if(index>=this.size)
            return;
        ListNode cur=this.dummy;
        for(int i=0;i<index;i++){
            cur=cur.next;
        }
        
        ListNode temp=cur.next;
        cur.next=temp.next;
        size--;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */

~~~


### 题解



### 困难
其实没有太大的困难，就是写每个方法的时候，注意控制该控制的变量，然后有些边界情况要有所考虑就行了。


## 206. 反转链表 难度： 简单


### 第一想法：

我是想用递归来写，顺便锻炼一下自己写递归的能力。

~~~

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    private ListNode dummy;
    public ListNode reverseList(ListNode head) {
        this.dummy=new ListNode(-1);
        traverse(null,head);
        return this.dummy.next;
    }

    public void traverse(ListNode pre, ListNode head){
        if(head==null){
            this.dummy.next=pre;
            return;
        }
        
        traverse(head,head.next);
        head.next=pre;
    }


}

~~~

### 题解：
其实我的想法就是通过一个递归函数，去反转这个链表，然后外面定义一个类属性dummy，用来连接应该返回的头节点
显然反转这个操作应该放在后序遍历的位置，因为这样才不影响前面的递归。

### 困难
