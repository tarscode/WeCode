# 二叉树最近公共祖先

> 刘洋
> 2017.6.1

题目链接：https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/#/description

## 内容

### 正文

给定一棵二叉树，找到两个节点的最近公共祖先(LCA)


```
输入样例：
        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4
```


### 输入


```
5  1 
```

### 输出


```
3
```

## 分析

递归分别遍历左右子树

## 解法

### 递归遍历

#### 思路

后序遍历二叉树，令当前遍历节点为cur。因为后序遍历需要先处理左右节点。

1. 如果当前节点cur等于null或者p或者q,直接返回cur。
2. 如果left和right都为空，说明整棵子树没有发现p和q，返回null。
3. 如果left和right都不为空，说明左右子树存在p和q,且最近公共祖先为cur。
4. 如果left和right中有一个不为空，则不为空的为最近公共祖先，将其返回。

复杂分析

- 时间复杂度O(n)
- 空间复杂度O(n)

#### 备注

- 无

#### 代码


```
public class LowestCommonAncestor {

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) { //找到p、q或者为空
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q); //查询左子树
        TreeNode right = lowestCommonAncestor(root.right, p, q); //查询右子树

        //当前子树均没有p和q
        if (left != null && right != null) {
            return root;
        }

        //left和right中不为空的为最近公共祖先
        return left != null ? left : right;
    }
}

class TreeNode {

    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int x) {
        val = x;
    }
}
```

