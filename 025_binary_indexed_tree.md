# 树状数组

模板题：[307. 区域和检索 - 数组可修改](https://leetcode.cn/problems/range-sum-query-mutable/)

```java
class NumArray {

    int[] arr;
    int n;
    int[] trees;

    public NumArray(int[] nums) {
        this.arr = nums;
        this.n = nums.length;
        this.trees = new int[n + 1];
        for (int i = 0; i < n; i++) {
            add(trees, i + 1, nums[i]);
        }
    }
    
    public void update(int index, int val) {
        add(trees, index + 1, val - arr[index]);
        arr[index] = val;
    }
    
    public int sumRange(int left, int right) {
        return presum(trees, right + 1) - presum(trees, left);
    }

    private int lowbit(int i) {
        return i & -i;
    }

    private void add(int[] trees, int i, int val) {
        while (i <= n) {
            trees[i] += val;
            i += lowbit(i);
        }
    }

    private int presum(int[] trees, int i) {
        int sum = 0;
        while (i > 0) {
            sum += trees[i];
            i -= lowbit(i);
        }
        return sum;
    }
}
```
