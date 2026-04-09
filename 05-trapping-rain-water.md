# 🔴 05 — Trapping Rain Water

## Problem

Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

**Example:**
```
Input:  height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

---

## 💡 Approach

Use the **Two Pointer** technique. Maintain `left` and `right` pointers and track `maxLeft` and `maxRight`. Water trapped at any position = `min(maxLeft, maxRight) - height[i]`.

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## Solutions

### 🐍 Python
```python
def trap(height):
    left, right = 0, len(height) - 1
    max_left = max_right = water = 0
    while left < right:
        if height[left] <= height[right]:
            if height[left] >= max_left:
                max_left = height[left]
            else:
                water += max_left - height[left]
            left += 1
        else:
            if height[right] >= max_right:
                max_right = height[right]
            else:
                water += max_right - height[right]
            right -= 1
    return water
```

---

### 🟨 JavaScript
```javascript
function trap(height) {
    let left = 0, right = height.length - 1;
    let maxLeft = 0, maxRight = 0, water = 0;
    while (left < right) {
        if (height[left] <= height[right]) {
            height[left] >= maxLeft ? maxLeft = height[left] : water += maxLeft - height[left];
            left++;
        } else {
            height[right] >= maxRight ? maxRight = height[right] : water += maxRight - height[right];
            right--;
        }
    }
    return water;
}
```

---

### ☕ Java
```java
public int trap(int[] height) {
    int left = 0, right = height.length - 1;
    int maxLeft = 0, maxRight = 0, water = 0;
    while (left < right) {
        if (height[left] <= height[right]) {
            if (height[left] >= maxLeft) maxLeft = height[left];
            else water += maxLeft - height[left];
            left++;
        } else {
            if (height[right] >= maxRight) maxRight = height[right];
            else water += maxRight - height[right];
            right--;
        }
    }
    return water;
}
```

---

### ➕ C++
```cpp
int trap(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int maxLeft = 0, maxRight = 0, water = 0;
    while (left < right) {
        if (height[left] <= height[right]) {
            height[left] >= maxLeft ? maxLeft = height[left] : water += maxLeft - height[left];
            left++;
        } else {
            height[right] >= maxRight ? maxRight = height[right] : water += maxRight - height[right];
            right--;
        }
    }
    return water;
}
```

---

## 🔗 Practice Link
- [LeetCode #42 — Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

---

*Part of [NutanGarage Coding Challenges](../README.md)*
