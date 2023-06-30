# 代码随想录算法训练营13期 第六章 二叉树 part06


 
 **学习时长**
 
## 654.最大二叉树 难度：中等


### 第一想法:

第一想法这个不是挺简单的吗，就是只要做过中序和前序遍历，甚至比那个还简单，因为思路都给出来了


### 题解

~~~

class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        if(nums.length==0)
            return null;
        int rootIndex = 0;
        int maxVal = 0;
        for(int i = 0; i<nums.length;i++){
            if(nums[i]>maxVal){
                rootIndex = i;
                maxVal=nums[i];
            }
        }

        TreeNode root = new TreeNode(maxVal);
        root.left = constructMaximumBinaryTree(Arrays.copyOfRange(nums,0,rootIndex));
        root.right = constructMaximumBinaryTree(Arrays.copyOfRange(nums,rootIndex+1,nums.length));
        return root;

    }
}


~~~

### 困难

发现最大的问题不在于这个解法，而是，有更简化的解法，单调栈解法能够达到O(n)的时间复杂度，就很恐怖了。但是我看了下，大概能看懂，但是我感觉实际中肯定是用不出来的，针对这道题想的时候。


## 617. 合并二叉树 难度：简单


### 第一想法:

这题感觉没什么难度就是按照要求遍历两颗树就行，写熟了之后感觉写这种还挺熟悉的

### 题解
~~~
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1 == null & root2 == null)
            return null;
        else if(root1 == null & root2 != null)
            return root2;
        else if(root1 != null & root2 == null)
            return root1;
        else{
            TreeNode nodeNew = new TreeNode(root1.val + root2.val);
            nodeNew.left = mergeTrees(root1.left,root2.left);
            nodeNew.right = mergeTrees(root1.right,root2.right);
            return nodeNew;
        }
    }
}

~~~


### 困难



## **700. 二叉搜索树中的搜索** 难度：简单

### 第一想法

这个题就是BST 性质就简单应用

### 题解

```java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if(root==null)
            return null;
        if(root.val == val)
            return root;
        if(root.val > val)
            return searchBST(root.left,val);
        else{
            return searchBST(root.right,val);
        }
    }
}
```

### 困难

## **98. 验证二叉搜索树** 难度：中等

### 第一想法

就是中序遍历出来应该是一个递增列表，

### 题解

```java
class Solution {
    List<Integer> nodes = new ArrayList<>();
    public boolean isValidBST(TreeNode root) {
        inorder(root);
        for(int i = 1; i<nodes.size();i++){
            if(nodes.get(i-1)>=nodes.get(i))
                return false;
        }
        return true;
    }

    public void inorder(TreeNode root){
        if(root == null)
            return;
        inorder(root.left);
        this.nodes.add(root.val);
        inorder(root.right);
    }
}
```

### 困难
