# 🧩 Dynamic Programming Challenges

---

## 🟢 01 — Fibonacci Number

### Problem
Given `n`, return the `nth` Fibonacci number.
`F(0) = 0, F(1) = 1, F(n) = F(n-1) + F(n-2)`

### Solutions

#### 🐍 Python
```python
def fib(n):
    if n <= 1: return n
    dp = [0, 1]
    for i in range(2, n + 1):
        dp.append(dp[-1] + dp[-2])
    return dp[n]
```

#### 🟨 JavaScript
```javascript
function fib(n) {
    if (n <= 1) return n;
    let a = 0, b = 1;
    for (let i = 2; i <= n; i++) [a, b] = [b, a + b];
    return b;
}
```

---

## 🟢 02 — Climbing Stairs

### Problem
You are climbing a staircase with `n` steps. Each time you can climb 1 or 2 steps. How many distinct ways can you climb to the top?

### Solutions

#### 🐍 Python
```python
def climbStairs(n):
    if n <= 2: return n
    a, b = 1, 2
    for _ in range(3, n + 1):
        a, b = b, a + b
    return b
```

#### 🟨 JavaScript
```javascript
function climbStairs(n) {
    if (n <= 2) return n;
    let a = 1, b = 2;
    for (let i = 3; i <= n; i++) [a, b] = [b, a + b];
    return b;
}
```

#### ☕ Java
```java
public int climbStairs(int n) {
    if (n <= 2) return n;
    int a = 1, b = 2;
    for (int i = 3; i <= n; i++) { int c = a + b; a = b; b = c; }
    return b;
}
```

---

## 🟡 03 — Longest Common Subsequence

### Problem
Given two strings `text1` and `text2`, return the length of their longest common subsequence.

**Example:**
```
Input:  text1 = "abcde", text2 = "ace"
Output: 3  ("ace")
```

### Solutions

#### 🐍 Python
```python
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    return dp[m][n]
```

#### ☕ Java
```java
public int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length(), n = text2.length();
    int[][] dp = new int[m + 1][n + 1];
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++)
            dp[i][j] = text1.charAt(i-1) == text2.charAt(j-1)
                ? dp[i-1][j-1] + 1
                : Math.max(dp[i-1][j], dp[i][j-1]);
    return dp[m][n];
}
```

---

## 🟡 04 — 0/1 Knapsack

### Problem
Given weights and values of `n` items, and a knapsack of capacity `W`, find the maximum value you can carry.

### Solutions

#### 🐍 Python
```python
def knapsack(W, weights, values, n):
    dp = [[0] * (W + 1) for _ in range(n + 1)]
    for i in range(1, n + 1):
        for w in range(W + 1):
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w], values[i-1] + dp[i-1][w - weights[i-1]])
            else:
                dp[i][w] = dp[i-1][w]
    return dp[n][W]
```

#### ➕ C++
```cpp
int knapsack(int W, vector<int>& weights, vector<int>& values, int n) {
    vector<vector<int>> dp(n + 1, vector<int>(W + 1, 0));
    for (int i = 1; i <= n; i++)
        for (int w = 0; w <= W; w++)
            dp[i][w] = weights[i-1] <= w
                ? max(dp[i-1][w], values[i-1] + dp[i-1][w - weights[i-1]])
                : dp[i-1][w];
    return dp[n][W];
}
```

---

## 🔴 05 — Edit Distance

### Problem
Given two strings `word1` and `word2`, return the minimum number of operations (insert, delete, replace) to convert `word1` to `word2`.

### Solutions

#### 🐍 Python
```python
def minDistance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(m + 1): dp[i][0] = i
    for j in range(n + 1): dp[0][j] = j
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
    return dp[m][n]
```

#### 🟨 JavaScript
```javascript
function minDistance(word1, word2) {
    const m = word1.length, n = word2.length;
    const dp = Array.from({length: m + 1}, (_, i) => Array.from({length: n + 1}, (_, j) => i || j));
    for (let i = 1; i <= m; i++)
        for (let j = 1; j <= n; j++)
            dp[i][j] = word1[i-1] === word2[j-1]
                ? dp[i-1][j-1]
                : 1 + Math.min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]);
    return dp[m][n];
}
```

---

## 🔗 Practice Links
- [LeetCode DP Problems](https://leetcode.com/tag/dynamic-programming/)
- [Striver DP Series](https://takeuforward.org/dynamic-programming/striver-dp-series-dynamic-programming-problems/)

---

*Part of [NutanGarage Coding Challenges](../README.md)*
