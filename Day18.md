# 代码随想录算法训练营13期 第六章 二叉树 part05 
 
 **学习时长**
 
## 513. 找树左下角的值 难度：中等


### 第一想法：

用层序遍历就可以，用一个数存每一层的最左边节点就行。

### 题解：

用递归其实应该也ok的，思路应该就是判断下深度，取最深的，最先遍历到的就行。
~~~

class Solution {
    public int findBottomLeftValue(TreeNode root) {
        int res = 0;
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.addLast(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0 ; i<size;i++) {
                
                TreeNode cur = queue.pollFirst();
                if(i==0){
                    res=cur.val;
                }
                if (cur.left != null)
                    queue.addLast(cur.left);
                if (cur.right != null)
                    queue.addLast(cur.right);
            }
        }
        
        return res;
    }
}

~~~

### 困难


## 112. 路径总和 难度：简单


### 第一想法：

就是说是回溯，其实在具体写的过程中我感觉因为这题太简单，所以也没有明显的撤销选择这个过程，而是传不同的值就可以。



### 题解

~~~
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root == null)
            return false;
        return traverse(root,targetSum);
    }
    public boolean traverse(TreeNode root, int target){
        if(root.left == null && root.right == null){
            if(root.val == target)
                return true;
            else
                return false;
        }
        boolean leftRes = false;
        boolean rightRes = false;
        if(root.left!=null)
            leftRes = traverse(root.left,target-root.val);
        if(root.right!=null)
            rightRes =traverse(root.right,target-root.val);
        return  leftRes || rightRes;
    }
}

~~~


### 困难：

其实我个人不太理解把这种称之为回溯的原因。



## 113. 路径总和 II 难度： 中等


### 第一想法：

跟上一题很像，需要改一些返回值，遍历方式之类的

### 题解：

~~~
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        if(root==null)
            return this.res;
        List<Integer> start = new ArrayList<>();
        start.add(root.val);
        traverse(root,targetSum,start);
        return this.res;
    }


    public void traverse(TreeNode root, int target, List<Integer> path){
        if(root.left == null && root.right == null){
            if(root.val == target)
                this.res.add(new ArrayList<>(path));
            else
                return;

        }
        if(root.left!=null) {
            path.add(root.left.val);
            traverse(root.left, target - root.val, path);
            path.remove(path.size()-1);
        }
        if(root.right!=null) {
            path.add(root.right.val);
            traverse(root.right, target - root.val, path);
            path.remove(path.size()-1);
        }
    }
}



~~~

### 困难：

关键可能在于一个是add要注意add一个深拷贝的列表，一个是回溯需要撤销选择。




## 105. 从前序与中序遍历序列构造二叉树 难度：中等


### 第一想法：

这题之前做过，其实大概有想法知道怎么做。


### 题解：

~~~

class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder.length<=0)
            return null;
        int rootVal = preorder[0];
        TreeNode root = new TreeNode(rootVal);
        int rootIndex = 0;
        for ( int i = 0; i< inorder.length;i++){
            if (inorder[i]== rootVal){
                rootIndex = i;
                break;
            }
        }
        root.left = buildTree(Arrays.copyOfRange(preorder,1,rootIndex+1),Arrays.copyOfRange(inorder,0,rootIndex));
        root.right = buildTree(Arrays.copyOfRange(preorder,rootIndex+1,inorder.length),Arrays.copyOfRange(inorder,rootIndex+1,preorder.length));
        return root;
    }
}
~~~

### 困难：

做的不熟练，二是，居然最开始中序和前序记反了



