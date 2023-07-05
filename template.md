
 
 **学习时长**
 
## 669. 修剪二叉搜索树  难度：中等


### 第一想法:

其实感觉也不是很难，就是分情况讨论各个情况的不同的处理策略呗。

### 题解:
~~~
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if(root == null)
            return null;

        if(root.val < low){
            return trimBST(root.right,low,high);
        }
        else if (root.val == low){
            root.left = null;
            root.right = trimBST(root.right,low,high);
            return root;
        }
        else if(root.val > low && root.val < high){
            root.left = trimBST(root.left,low,high);
            root.right = trimBST(root.right,low,high);
            return root;
        }
        else if (root.val == high){
            root.right=null;
            root.left = trimBST(root.left,low,high);
            return root;
        }
        else if (root.val > high)
            return trimBST(root.left,low,high);
        return root;
    }
}

~~~


