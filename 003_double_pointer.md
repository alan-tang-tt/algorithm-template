# 双指针

## 快慢双指针

示例：[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode fast = head, slow = head;
        while (k-- > 0) {
            fast = fast.next;
        }

        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
        }

        return slow;
    }
}
```

## 左右双指针

示例：[917. 仅仅反转字母](https://leetcode-cn.com/problems/reverse-only-letters/)

```java
class Solution {
    public String reverseOnlyLetters(String s) {
        char[] arr = s.toCharArray();
        int left = 0, right = s.length() - 1;

        while (left < right) {
            // ---ab-c-d--
            while (left < right && !Character.isLetter(arr[left])) {
                left++;
            }

            while (left < right && !Character.isLetter(arr[right])) {
                right--;
            }

            swap(arr, left++, right--);
        }

        return new String(arr);
    }

    private void swap(char[] arr, int left, int right) {
        char tmp = arr[left];
        arr[left] = arr[right];
        arr[right] = tmp;
    }
}
```

## 读写双指针

示例：[443. 压缩字符串](https://leetcode-cn.com/problems/string-compression/)

```java
class Solution {
    public int compress(char[] chars) {
        int read = 0, write = 0;

        while (read < chars.length) {
            int count = 1;
            read++;
            while (read < chars.length && chars[read] == chars[read - 1]) {
                read++;
                count++;
            }

            chars[write++] = chars[read - 1];

            if (count > 1) {
                char[] arr = String.valueOf(count).toCharArray();
                for (char c : arr) {
                    chars[write++] = c;
                }
            }
        }

        return write;
    }
}
```

源码中的运用：`ArrayList.removeAll()` 方法。

## 同向双指针

示例：[21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode();
        ListNode tmp = dummy;

        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                tmp.next = list1;
                list1 = list1.next;
            } else {
                tmp.next = list2;
                list2 = list2.next;
            }
            tmp = tmp.next;
        }

        tmp.next = list1 == null ? list2 : list1;

        return dummy.next;
    }
}
```

## 滑动窗口双指针

示例：[1984. 学生分数的最小差值](https://leetcode-cn.com/problems/minimum-difference-between-highest-and-lowest-of-k-scores/)

```java
class Solution {
    public int minimumDifference(int[] nums, int k) {
        // 1 4 7 9
        Arrays.sort(nums);

        int ans = Integer.MAX_VALUE;
        for (int i = 0; i < nums.length - k + 1; i++) {
            ans = Math.min(ans, nums[i + k - 1] - nums[i]);
        }
        return ans;
    }
}
```
