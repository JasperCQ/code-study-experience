# 代码随想录算法训练营13期 第六章   二叉树part04

 
 **学习时长**
 
## 110. 平衡二叉树 难度：简单


### 第一想法:

就是写一个计算高度的递归函数，然后从根节点开始不断往下判断左右子树的高度差是否满足条件，再递归的判断左右子树就可以。


### 题解：
我看了题解后，其实自己做的时候也有思考就是，这种自顶向下的递归写法，显然存在着很多冗余操作，所以自底向上的解法时间复杂度更好，自底向上的解法是把关键的判断这个步骤挪到了求高度里面，并且采用后序遍历，这样在求高度的过程中就能够判断子树的是否平衡。

~~~
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
public boolean isBalanced(TreeNode root) {
        if(root==null){
            return true;
        }
        if(Math.abs(getHeight(root.left)-getHeight(root.right))<=1){
            return isBalanced(root.left) && isBalanced(root.right);
        }
        return false;
    }

    public int getHeight(TreeNode root){
        if(root==null){
            return 0;
        }
        int leftHeight=getHeight(root.left);
        int rightHeight=getHeight(root.right);
        return Math.max(leftHeight+1,rightHeight+1);

    }
}

~~~

### 困难
