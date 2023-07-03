# 代码随想录算法训练营13期 第六章 二叉树part07

 
 **学习时长**
 
##  530.二叉搜索树的最小绝对差  难度:简单


### 第一想法：

第一想法就是中序遍历出来，然后遍历一下节点值选出差值最小的就行了。

### 题解
~~~
class Solution {
    List<Integer> nodes = new ArrayList<>();
    public int getMinimumDifference(TreeNode root) {
        inorder(root);
        int res = Integer.MAX_VALUE;
        for(int i = 1 ;i<nodes.size();i++){
            if(nodes.get(i)-nodes.get(i-1)<res)
                res=nodes.get(i)-nodes.get(i-1);
        }
        return res;
    }
    public void inorder(TreeNode root){
        if(root == null)
            return;

        inorder(root.left);
        this.nodes.add(root.val);
        inorder(root.right);
    }
}


~~~

### 困难


##  501.二叉搜索树中的众数  难度：简单


### 第一想法：
中序遍历出来，然后遍历两遍就可以

### 题解：

我看了给的题解，用的双指针的这种方式，但是其实时间复杂度还是在O(N)级别的，而且其实在这种不两遍遍历的解法中，会导致反复添加和清理result数组。所以我就有点懒得写这道题了。

### 困难




## 236. 二叉树的最近公共祖先 难度：中等


### 第一想法：

我本来是隐约记得可以用父节点，但是想了哈直接巧妙的递归哈就行


### 题解
~~~

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null)
            return null;
        if(root.equals(p) || root.equals(q))
            return root;

        TreeNode left = lowestCommonAncestor(root.left, p , q);
        TreeNode right = lowestCommonAncestor(root.right,p,q);
        if(left == null  && right ==null)
            return null;
        if(left == null && right != null)
            return right;
        if(left!=null && right == null)
            return left;
        //left != null && right != null
        return root;
    }
}

~~~

### 困难


