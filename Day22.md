# 代码随想录算法训练营13期 第六章 二叉树part08

 
 **学习时长**
 
## 235. 二叉搜索树的最近公共祖先 难度：中等


### 第一想法：

就是简化版的二叉树的最近公共祖先呗，利用下BST的特性，能够把时间复杂度降低到O（logn）

### 题解：

~~~
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(p.val>q.val)
            return getLowestCommonAncestor(root,q.val,p.val);
        else
            return getLowestCommonAncestor(root,p.val,q.val);
        
    }
    public TreeNode getLowestCommonAncestor(TreeNode root, int valSmall, int valLarge){
        if(root==null)
            return null;
        if(valSmall>root.val)
            return getLowestCommonAncestor(root.right,valSmall,valLarge);
        else if(valLarge<root.val)
            return getLowestCommonAncestor(root.left,valSmall,valLarge);
        return root;
    }
}

~~~

### 困难



## 701. 二叉搜索树中的插入操作 难度：中等


### 第一想法:

第一时间其实没想出简单的做法

### 题解

实际上就是利用BST，先搜索到合适的位置，然后插入就行，只是这个返回值的选择还比较巧妙。
~~~

class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if(root==null)
            return new TreeNode(val);
        if(root.val>val)
            root.left=insertIntoBST(root.left, val);
        else
            root.right = insertIntoBST(root.right,val);
        return root;
    }
}
~~~

### 困难



## 450.删除二叉搜索树中的节点  难度：中等


### 第一想法:

第一想法其实感觉还挺复杂的，还想到了之前学数据结构和算法的课一路上移的算法，但是感觉那种太复杂了，所以直接看了思路提示

### 题解

其实有些地方还挺复杂，容易弄错的，比如说两个子节点的情况时，先再次调用deletenode就是一个很巧妙的做法。同时还必须注意下面这段代码一定要有root.right=的部分    root.right=deleteNode(root.right,newNode.val);
~~~

class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root==null)
            return null;
        if(root.val>key)
            root.left=deleteNode(root.left,key);
        else if(root.val<key)
            root.right=deleteNode(root.right,key);
        else{
            //叶节点
            if(root.left==null && root.right == null)
                return null;
            //只有一个子节点
            if(root.left != null && root.right == null)
                return root.left;
            if(root.left == null && root.right != null)
                return root.right;
            //两个子节点
            else{

                TreeNode newNode = getMinNode(root.right);
                root.right=deleteNode(root.right,newNode.val);
                newNode.left= root.left;
                newNode.right = root.right;
                return newNode;
            }

        }

        return root;
    }
    public TreeNode getMinNode(TreeNode root){
        while(root.left!=null)
            root=root.left;
        return root;
    }
}
~~~


### 困难
