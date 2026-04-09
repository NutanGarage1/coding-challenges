# 🟢 01 — Two Sum

## Problem

Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers that add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**
```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9
```

---

## 💡 Approach

Use a **HashMap** to store each number and its index as you iterate. For each number, check if `target - number` already exists in the map.

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## Solutions

### 🐍 Python
```python
def twoSum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        diff = target - num
        if diff in seen:
            return [seen[diff], i]
        seen[num] = i
```

---

### 🟨 JavaScript
```javascript
function twoSum(nums, target) {
    const seen = new Map();
    for (let i = 0; i < nums.length; i++) {
        const diff = target - nums[i];
        if (seen.has(diff)) return [seen.get(diff), i];
        seen.set(nums[i], i);
    }
}
```

---

### ☕ Java
```java
import java.util.HashMap;

public int[] twoSum(int[] nums, int target) {
    HashMap<Integer, Integer> seen = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int diff = target - nums[i];
        if (seen.containsKey(diff)) return new int[]{seen.get(diff), i};
        seen.put(nums[i], i);
    }
    return new int[]{};
}
```

---

### ➕ C++
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> seen;
    for (int i = 0; i < nums.size(); i++) {
        int diff = target - nums[i];
        if (seen.count(diff)) return {seen[diff], i};
        seen[nums[i]] = i;
    }
    return {};
}
```

---

## 🔗 Practice Link
- [LeetCode #1 — Two Sum](https://leetcode.com/problems/two-sum/)

---

*Part of [NutanGarage Coding Challenges](../README.md)*
