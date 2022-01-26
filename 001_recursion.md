# 递归模板

```java
private int dfs(int n) {
    // 递归的退出条件
    if (n <= 1) {
        // return ...
    }
    
    // 递归的逻辑处理
    // ...
}
```

# 示例1

求斐波那契数：https://leetcode-cn.com/problems/fibonacci-number/

```java
class Solution {

    public int fib(int n) {
        return f(n);
    }

    private int f(int n) {
        // 递归的退出条件
        if (n <= 1) {
            return n;
        }

        // 递归的逻辑处理
        return f(n - 1) + f(n - 2);
    }
}
```

# 示例2

二叉树的中序遍历：https://leetcode-cn.com/problems/binary-tree-inorder-traversal/

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        dfs(list, root);
        return list;
    }

    private void dfs(List<Integer> list, TreeNode node) {
        // 递归的退出条件
        if (node == null) {
            return;
        }

        // 递归的逻辑处理
        dfs(list, node.left);
        list.add(node.val);
        dfs(list, node.right);
    }
}
```

# 最后

欢迎关注公众号【彤哥来刷题啦】，每日分享高质量题解，专栏【算法140讲】连载中……

![](https://img.oicoding.cn/img/20211226095624.png)
