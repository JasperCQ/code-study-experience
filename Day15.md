# 代码随想录算法训练营13期 二叉树 part02
 
 **学习时长**
 
## 102. 二叉树的层序遍历 难度：中等


### 第一想法：

就是层序遍历呗，但是返回结果是一个二维数组，那么中间肯定是需要两层循环的

### 题解：

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        
        List<List<Integer>> res = new ArrayList<>();
        Deque<TreeNode> que = new ArrayDeque<>();
        if(root==null)
            return res;
        que.addLast(root);
        while (que.size()>0){
            int len = que.size();
            List<Integer> temp_res = new ArrayList<>();
            while (len > 0) {
                TreeNode temp = que.pollFirst();
                if(temp.left!=null)
                    que.addLast(temp.left);
                if(temp.right!=null)
                    que.addLast(temp.right);
                temp_res.add(temp.val);
                len--;
            }
            res.add(temp_res);
        }
        return res;
            
    }
}
~~~

### 困难



## 107. 二叉树的层序遍历 II 难度：中等


### 第一想法:

这个不是把上一题的改一改，只要添加每一层的时候添加到头部不就行了吗

### 题解：

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
   public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        Deque<TreeNode> que = new ArrayDeque<>();
        if(root==null)
            return res;
        que.addLast(root);
        while (que.size()>0){
            int len = que.size();
            List<Integer> temp_res = new ArrayList<>();
            while (len > 0) {
                TreeNode temp = que.pollFirst();
                if(temp.left!=null)
                    que.addLast(temp.left);
                if(temp.right!=null)
                    que.addLast(temp.right);
                temp_res.add(temp.val);
                len--;
            }
            res.add(0,temp_res);
        }
        return res;
    }
}

~~~

### 困难




## 199. 二叉树的右视图 难度：中等


### 第一想法：

把层序遍历的代码改一改想要的返回值，判断一下就可以了。

### 题解：

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
    public List<Integer> rightSideView(TreeNode root) {
        
        List<Integer> res = new ArrayList<>();
        Deque<TreeNode> que = new ArrayDeque<>();
        if(root==null)
            return res;
        que.addLast(root);
        while (que.size()>0){
            int len = que.size();
            while (len > 0) {
                TreeNode temp = que.pollFirst();
                if(temp.left!=null)
                    que.addLast(temp.left);
                if(temp.right!=null)
                    que.addLast(temp.right);
                if(len==1)
                    res.add(temp.val);
                len--;
            }
        }
        return res;
    }
}

~~~


### 困难




## 226. 翻转二叉树 难度：简单


### 第一想法：

翻转当前根节点的左右子节点，并且对左右子节点递归就行


### 题解：

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
    public TreeNode invertTree(TreeNode root) {
        if(root==null)
            return null;
        TreeNode temp = root.left;
        root.left= root.right;
        root.right=temp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}

~~~

### 困难




## 101. 对称二叉树 难度：简单


### 第一想法：

其实感觉也没有那么简单，主要是第一时间其实没有get到要怎么同时遍历两棵树，后来发现其实只要重新定义个递归函数，传两个参就行。

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
    public boolean compare(TreeNode leftRoot, TreeNode rightRoot){
        if(leftRoot==null && rightRoot!=null)
            return false;
        else if (rightRoot==null && leftRoot!=null)
            return false;
        else if (leftRoot==null && rightRoot==null)
            return true;
        else if (leftRoot.val!=rightRoot.val)
            return false;

        boolean outRes=compare(leftRoot.left,rightRoot.right);
        boolean inRes=compare(leftRoot.right,rightRoot.left);

        return outRes && inRes;

    }

    public boolean isSymmetric(TreeNode root) {
        return compare(root.left,root.right);
    }
}

~~~

### 困难






