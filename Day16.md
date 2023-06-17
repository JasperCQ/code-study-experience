# 代码随想录算法训练营13期 第六章  二叉树part03


 **学习时长**
 
## 104.二叉树的最大深度 难度：简单


### 第一想法:

使用遍历和子树解法都能解决。我写的是遍历解法。

### 题解：
就是在外部设置一个变量，然后在一个无返回值的遍历函数中遍历树，操作就行了。

~~~

class Solution {
    private int res = 0;
    public int maxDepth(TreeNode root) {
        this.traverse(root,1);
        return this.res;
    }
    public void traverse(TreeNode root,int depth){
        if(root==null)
            return;
        if(depth>this.res)
            this.res=depth;
        traverse(root.left,depth+1);
        traverse(root.right,depth+1);
    }
}
~~~


### 困难


## 111. 二叉树的最小深度 难度：简单


### 第一想法:

修改一下上一题其实就可以了。

### 题解：

~~~

class Solution {
private int res = Integer.MAX_VALUE;
    public int minDepth(TreeNode root) {
        if(root==null)
            return 0;
        this.traverse(root,1);
        return this.res;
    }
    public void traverse(TreeNode root,int depth){
        if(root==null)
            return;
        if(root.left==null && root.right==null){
            if(this.res>depth)
                this.res=depth;
        }
        traverse(root.left,depth+1);
        traverse(root.right,depth+1);
    }
}

~~~


### 困难



## 222. 完全二叉树的节点个数 难度：中等


### 第一想法

### 题解:
想出O(n)的解法很简单，但是确实想了会没想出来O（logn）的，还是利用递归求深度这个部分。

~~~

class Solution {
    /**
     * 针对完全二叉树的解法
     *
     * 满二叉树的结点数为：2^depth - 1
     */
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        TreeNode left = root.left;
        TreeNode right = root.right;
        int leftDepth = 0, rightDepth = 0; // 这里初始为0是有目的的，为了下面求指数方便
        while (left != null) {  // 求左子树深度
            left = left.left;
            leftDepth++;
        }
        while (right != null) { // 求右子树深度
            right = right.right;
            rightDepth++;
        }
        if (leftDepth == rightDepth) {
            return (2 << leftDepth) - 1; // 注意(2<<1) 相当于2^2，所以leftDepth初始为0
        }
        return countNodes(root.left) + countNodes(root.right) + 1;
    }
}

~~~

### 困难

想出满二叉树不用遍历就能计算出结点数，且这个结构在完全二叉树中是嵌套的



