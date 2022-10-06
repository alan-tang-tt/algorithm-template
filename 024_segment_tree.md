# 线段树

模板题：[307. 区域和检索 - 数组可修改](https://leetcode.cn/problems/range-sum-query-mutable/)

```
class NumArray {

    int[] arr;
    int n;
    int[] trees;

    public NumArray(int[] nums) {
        this.arr = nums;
        this.n = nums.length;
        this.trees = new int[4 * n];
        build(arr, trees, 1, 0, n - 1);
    }
    
    public void update(int index, int val) {
        update(arr, trees, 1, 0, n - 1, index, val);
    }
    
    public int sumRange(int left, int right) {
        return query(arr, trees, 1, 0, n - 1, left, right);
    }

    private void build(int[] arr, int[] trees, int node, int start, int end) {
        if (start == end) {
            trees[node] = arr[start];
            return;
        }

        int mid = (start + end) / 2;
        int leftNode = 2 * node;
        int rightNode = 2 * node + 1;

        build(arr, trees, leftNode, start, mid);
        build(arr, trees, rightNode, mid + 1, end);

        trees[node] = trees[leftNode] + trees[rightNode];
    }

    private void update(int[] arr, int[] trees, int node, int start, int end, int idx, int val) {
        if (start == end) {
            arr[idx] = val;
            trees[node] = val;
            return;
        }

        int mid = (start + end) / 2;
        int leftNode = 2 * node;
        int rightNode = 2 * node + 1;

        if (idx <= mid) {
            update(arr, trees, leftNode, start, mid, idx, val);
        } else {
            update(arr, trees, rightNode, mid + 1, end, idx, val);
        }

        trees[node] = trees[leftNode] + trees[rightNode];
    }

    private int query(int[] arr, int[] trees, int node, int start, int end, int l, int r) {
        if (end < l || r < start) {
            return 0;
        }

        if (start == end) {
            return trees[node];
        }

        if (l <= start && end <= r) {
            return trees[node];
        }

        int mid = (start + end) / 2;
        int leftNode = 2 * node;
        int rightNode = 2 * node + 1;

        int leftSum = query(arr, trees, leftNode, start, mid, l, r);
        int rightSum = query(arr, trees, rightNode, mid + 1, end, l, r);

        return leftSum + rightSum;
    }
}
```
