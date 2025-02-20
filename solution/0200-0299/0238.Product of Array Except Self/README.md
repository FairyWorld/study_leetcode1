# [238. 除自身以外数组的乘积](https://leetcode.cn/problems/product-of-array-except-self)

[English Version](/solution/0200-0299/0238.Product%20of%20Array%20Except%20Self/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给你一个整数数组&nbsp;<code>nums</code>，返回 <em>数组&nbsp;<code>answer</code>&nbsp;，其中&nbsp;<code>answer[i]</code>&nbsp;等于&nbsp;<code>nums</code>&nbsp;中除&nbsp;<code>nums[i]</code>&nbsp;之外其余各元素的乘积</em>&nbsp;。</p>

<p>题目数据 <strong>保证</strong> 数组&nbsp;<code>nums</code>之中任意元素的全部前缀元素和后缀的乘积都在&nbsp; <strong>32 位</strong> 整数范围内。</p>

<p>请<strong>不要使用除法，</strong>且在&nbsp;<code>O(<em>n</em>)</code> 时间复杂度内完成此题。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> nums = <code>[1,2,3,4]</code>
<strong>输出:</strong> <code>[24,12,8,6]</code>
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> nums = [-1,1,0,-3,3]
<strong>输出:</strong> [0,0,9,0,0]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-30 &lt;= nums[i] &lt;= 30</code></li>
	<li><strong>保证</strong> 数组&nbsp;<code>nums</code>之中任意元素的全部前缀元素和后缀的乘积都在&nbsp; <strong>32 位</strong> 整数范围内</li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你可以在 <code>O(1)</code>&nbsp;的额外空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组<strong>不被视为</strong>额外空间。）</p>

## 解法

<!-- 这里可写通用的实现逻辑 -->

**方法一：两次遍历**

我们定义两个变量 `left` 和 `right`，分别表示当前元素左边所有元素的乘积和右边所有元素的乘积。对于数组中的第一个元素，左边没有元素，所以 `left = 1`；对于数组中的最后一个元素，右边没有元素，所以 `right = 1`。用一个长度为 $n$ 的数组 `ans` 来存储最终的答案。

我们先从左到右遍历数组，对于遍历到的第 $i$ 个元素，我们用 `left` 更新 `ans[i]` 的值，然后 `left` 乘以 `nums[i]`。

接下来，我们从右到左遍历数组，对于遍历到的第 $i$ 个元素，我们将 `ans[i]` 乘以 `right`，然后 `right` 乘以 `nums[i]`。

时间复杂度 $O(n)$，忽略答案的空间消耗，空间复杂度 $O(1)$。其中 $n$ 是数组的长度。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        ans = [0] * n
        left = right = 1
        for i, v in enumerate(nums):
            ans[i] = left
            left *= v
        for i in range(n - 1, -1, -1):
            ans[i] *= right
            right *= nums[i]
        return ans
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];
        for (int i = 0, left = 1; i < n; ++i) {
            ans[i] = left;
            left *= nums[i];
        }
        for (int i = n - 1, right = 1; i >= 0; --i) {
            ans[i] *= right;
            right *= nums[i];
        }
        return ans;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n);
        for (int i = 0, left = 1; i < n; ++i) {
            ans[i] = left;
            left *= nums[i];
        }
        for (int i = n - 1, right = 1; i >= 0; --i) {
            ans[i] *= right;
            right *= nums[i];
        }
        return ans;
    }
};
```

### **Go**

```go
func productExceptSelf(nums []int) []int {
	n := len(nums)
	ans := make([]int, n)
	left, right := 1, 1
	for i, v := range nums {
		ans[i] = left
		left *= v
	}
	for i := n - 1; i >= 0; i-- {
		ans[i] *= right
		right *= nums[i]
	}
	return ans
}
```

### **JavaScript**

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function (nums) {
    const n = nums.length;
    let ans = new Array(n);
    for (let i = 0, left = 1; i < n; ++i) {
        ans[i] = left;
        left *= nums[i];
    }
    for (let i = n - 1, right = 1; i >= 0; --i) {
        ans[i] *= right;
        right *= nums[i];
    }
    return ans;
};
```

### **TypeScript**

```ts
function productExceptSelf(nums: number[]): number[] {
    const n = nums.length;
    let ans = new Array(n);
    for (let i = 0, left = 1; i < n; ++i) {
        ans[i] = left;
        left *= nums[i];
    }
    for (let i = n - 1, right = 1; i >= 0; --i) {
        ans[i] *= right;
        right *= nums[i];
    }
    return ans;
}
```

```ts
function productExceptSelf(nums: number[]): number[] {
    return nums.map((_, i) =>
        nums.reduce((pre, val, j) => pre * (i === j ? 1 : val), 1),
    );
}
```

### **Rust**

```rust
impl Solution {
    pub fn product_except_self(nums: Vec<i32>) -> Vec<i32> {
        let mut dp_left = vec![1_i32; nums.len()];
        let mut dp_right = vec![1_i32; nums.len()];
        for i in 1..nums.len() {
            dp_left[i] = dp_left[i - 1] * nums[i - 1];
        }
        for i in (0..(nums.len() - 1)).rev() {
            dp_right[i] = dp_right[i + 1] * nums[i + 1];
        }
        dp_left
            .into_iter()
            .enumerate()
            .map(|(i, x)| x * dp_right[i])
            .collect()
    }
}
```

```rust
impl Solution {
    pub fn product_except_self(nums: Vec<i32>) -> Vec<i32> {
        let n = nums.len();
        let mut l = 1;
        let mut r = 1;
        let mut res = vec![0; n];
        for i in 0..n {
            res[i] = l;
            l *= nums[i];
        }
        for i in (0..n).rev() {
            res[i] *= r;
            r *= nums[i];
        }
        res
    }
}
```

### **...**

```

```

<!-- tabs:end -->
