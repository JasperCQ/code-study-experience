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



## 题目名字 难度：


### 第一想法

### 题解

### 困难



## 题目名字 难度：


### 第一想法

### 题解

### 困难

