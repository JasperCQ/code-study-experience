# 代码随想录算法训练营13期 二叉树part01

 
 **学习时长**

## 递归遍历


## 144. 二叉树的前序遍历 难度：简单


### 第一想法

### 题解:
emmm，没什么可说的。
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
    private List<Integer> res = new ArrayList<>();

    public List<Integer> preorderTraversal(TreeNode root) {
        if(root == null)
            return new ArrayList<Integer>();
        
        this.res.add(root.val);
        preorderTraversal(root.left);
        preorderTraversal(root.right);
        return res;

    }
}

~~~

### 困难



## 145. 二叉树的后序遍历 难度：简单


### 第一想法

### 题解
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
    private List<Integer> res = new ArrayList<>();

    public List<Integer> postorderTraversal(TreeNode root) {

        if(root==null)
            return new ArrayList<>();
        postorderTraversal(root.left);
        postorderTraversal(root.right);
        res.add(root.val);
        return res;

    }
}

~~~


### 困难




## 94. 二叉树的中序遍历 难度：简单


### 第一想法

### 题解

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
    private List<Integer> res = new ArrayList<>();

    public List<Integer> inorderTraversal(TreeNode root) {
        if(root == null)
            return new ArrayList<>();
        inorderTraversal(root.left);
        res.add(root.val);
        inorderTraversal(root.right);
        return res;
        
    }
}

~~~


### 困难





