# Recursion — Short Revision

## 1. What is Recursion?

Recursion means a function calls itself to solve a smaller version of the same problem.

```cpp
solve(n) -> solve(n - 1)
```

---

## 2. Two Main Parts

Every recursive function has:

```text
1. Base Case
2. Recursive Case
```

Example:

```cpp
int factorial(int n) {
    if (n == 0) return 1;      // base case
    return n * factorial(n-1); // recursive case
}
```

---

## 3. Base Case

Base case stops recursion.

Without it, recursion keeps going and causes stack overflow.

```cpp
if (root == NULL) return 0;
```

---

## 4. Recursive Call Returns One Level Up

Very important:

```text
return true;
```

does not directly return to `main`.

It returns to the function call that called it.

Example:

```cpp
bool left = solve(root->left);
```

If `solve(root->left)` returns `true`, then:

```cpp
left = true;
```

Parent function still continues.

---

## 5. Call Stack

Recursion first goes down, then answers come back up.

```text
factorial(3)
= 3 * factorial(2)
= 3 * 2 * factorial(1)
= 3 * 2 * 1 * factorial(0)
= 6
```

---

## 6. Tree Recursion Template

```cpp
int dfs(TreeNode* root) {
    if (root == NULL) return 0;

    int left = dfs(root->left);
    int right = dfs(root->right);

    // use left and right answer

    return 1 + max(left, right);
}
```

---

## 7. Postorder DFS

Postorder means:

```text
Left -> Right -> Current
```

Use it when current node needs answers from children first.

Examples:

```text
Height of Tree
Diameter of Tree
Balanced Binary Tree
Maximum Path Sum
```

---

## 8. Return One Thing, Compute Another

Example: Diameter of Tree

```cpp
int height(TreeNode* root) {
    if (root == NULL) return 0;

    int lh = height(root->left);
    int rh = height(root->right);

    diameter = max(diameter, lh + rh);

    return 1 + max(lh, rh);
}
```

Here:

```text
Function returns height
But updates diameter
```

---

## 9. Direct Boolean Recursion

Example: Same Tree

```cpp
bool isSameTree(TreeNode* p, TreeNode* q) {
    if (p == NULL && q == NULL) return true;
    if (p == NULL || q == NULL) return false;
    if (p->val != q->val) return false;

    return isSameTree(p->left, q->left) &&
           isSameTree(p->right, q->right);
}
```

Here each call returns:

```text
Are these two subtrees same?
```

---

## 10. `&&` Short-Circuit

```cpp
A && B
```

If `A` is false, `B` is not checked.

```text
&& stops on false
&& does not stop on true
```

---

## 11. Early Stop in Recursion

No direct `break`.

Use `return`.

```cpp
bool find(TreeNode* root, int target) {
    if (root == NULL) return false;
    if (root->val == target) return true;

    return find(root->left, target) ||
           find(root->right, target);
}
```

---

## 12. Common Mistake

Avoid:

```cpp
if (wrong) ans = false;
else ans = true;
```

Because later true can overwrite previous false.

Better:

```cpp
if (wrong) ans = false;
```

---

## 13. How to Think

Ask:

```text
1. What is the base case?
2. What should each call return?
3. What should I do before recursion?
4. What should I do after recursion?
5. How will parent use the answer?
```

---

## Final Line

Recursion means solving smaller problems first, then using their answers to solve the current problem.