# 二分要点

1. 找到二分的条件；
2. 移动左右指针；

# 二分模板一

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] == target) {
                return mid;
            }

            if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return -1;
    }
}
```

满足条件时直接返回，注意 while 条件带等号。

# 二分模板二

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int mid = (left + right) / 2;
            
            if (nums[mid] >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return nums[left] == target ? left : -1;
    }
}
```

最后返回语句中的 left 换成 right 也是可以的，注意 while 条件不带等号。

# 二分模板三

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int mid = (left + right + 1) / 2;
            
            if (nums[mid] <= target) {
                left = mid;
            } else {
                right = mid - 1;
            }
        }

        return nums[left] == target ? left : -1;
    }
}
```

最后返回语句中的 left 换成 right 也是可以的，注意 while 条件不带等号。

# 示例

704. 二分查找：https://leetcode-cn.com/problems/binary-search/

三种写法见上述模板。

# 其他

1. `(left + right) / 2` 可以写成 `(left + right) >> 1`，右移一位就是除以2；
2. 数据范围较大时可以写成 `left + (right - left) / 2`，可以防止溢出；

# 推荐

推荐记住模板一和模板二，是最常用的。

# 最后

欢迎关注公众号【彤哥来刷题啦】，每日分享高质量题解，专栏【算法140讲】连载中……

![](https://img.oicoding.cn/img/20211226095624.png)
