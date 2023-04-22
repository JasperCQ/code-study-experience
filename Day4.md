# 代码随想录算法训练营13期  24. 两两交换链表中的节点、19.删除链表的倒数第N个节点 、142.环形链表II



 **学习时长 1h左右**
 
## 24. 两两交换链表中的节点 难度：中等


### 第一想法：

就觉得就是一个简单的操作链表的题，控制两个指针遍历就行。

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
    public ListNode swapPairs(ListNode head) {
        if(head==null)
            return null;
        if(head.next==null)
            return head;
        ListNode dummy= new ListNode(-1,head);
        ListNode pre = dummy;
        ListNode cur = head;

        while(cur!=null){
            if (cur.next==null)
                break;
            ListNode temp=cur.next.next;
            pre.next=cur.next;
            cur.next.next=cur;
            cur.next=temp;
            pre=pre.next.next;
            cur=cur.next;

        }
        return dummy.next;

    }
}

~~~

### 题解：


### 困难：

其实在具体解题的时候，这两个指针的设置还挺考究的，设置的不好容易非常麻烦。


## 19. 删除链表的倒数第 N 个结点 难度：中等


### 第一想法:

之前做过，所以知道大概是两个指针，让两个指针保持n的距离就能完成这个任务

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        
        ListNode dummy  = new ListNode(-1,head);
        ListNode pre=dummy;
        ListNode left = head;
        ListNode right= head;
        int count=0;
        while(right!=null){
            
            if(count>=n){
                left=left.next;
                pre=pre.next;
            }
            right=right.next;
            count++;
        }
        pre.next=left.next;
        return dummy.next;
    }
}
~~~


### 题解

### 困难：

还是要设置dummy，最开始不想设置，但发现还是会存在只有一个节点时会出现问题。




## 142. 环形链表 II 难度：中等


### 第一想法:

也是以前做过的题，去复习了一下环形的那个方法，就行了
~~~

/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode dummy= new ListNode(-1,head);
        ListNode slow= dummy;
        ListNode fast= dummy;

        while(fast!=null){
            if (fast.next==null)
                break;
            fast=fast.next.next;
            slow=slow.next;
            //第一次相遇
            if (fast==slow){
                slow=dummy;
                while(slow!=fast){
                    slow=slow.next;
                    fast=fast.next;
                }
            //第二次相遇
                return slow;
            }
        }

        return null;

    }
}

~~~

### 题解:

在这里直接借用labuladong 的图：

![image](https://user-images.githubusercontent.com/131168940/233798282-d78c9a2a-a44f-47fa-899f-ac51049f8fcd.png)


### 困难 ：
知道了方法的话，其实没什么难的，注意如果使用dummy的话，第二次相遇重置指针也要从dummy起步，不然会永远碰不到。
