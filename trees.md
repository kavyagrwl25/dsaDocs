# Tree Pattern — Return One Thing, Compute Another

## Core Pattern

In many tree DFS problems, recursion does two jobs:

1. **Returns useful information to the parent**
2. **Computes / updates answer at the current node**

This is usually done using **postorder DFS**.

---

## Why Postorder DFS?

Because the current node needs results from both children first:

```text
left subtree -> right subtree -> current node
```

So whenever a problem says:

```text
Use left and right subtree information at every node
```

Think:

```text
Postorder DFS
```

---

## Common Template

```cpp
int dfs(TreeNode* root) {
    if (root == NULL) return 0;

    int lh = dfs(root->left);
    int rh = dfs(root->right);

    // compute/update answer using lh and rh

    return 1 + max(lh, rh);
}
```

---

# LeetCode 543 — Diameter of Binary Tree

## Pattern

- Postorder DFS
- Return height
- Update diameter separately

## Core Idea

At every node:

```cpp
diameterThroughNode = leftHeight + rightHeight;
```

Keep updating the maximum diameter.

## Important Insight

The function **returns height**, not diameter.

```cpp
return 1 + max(lh, rh);
```

But at every node, we update:

```cpp
diameter = max(diameter, lh + rh);
```

## Code

```cpp
class Solution {
public:
    int diameter = 0;

    int height(TreeNode* root) {
        if (root == NULL) return 0;

        int lh = height(root->left);
        int rh = height(root->right);

        diameter = max(diameter, lh + rh);

        return 1 + max(lh, rh);
    }

    int diameterOfBinaryTree(TreeNode* root) {
        height(root);
        return diameter;
    }
};
```

## One-Line Revision

Return height upward, update diameter at every node.

---

# LeetCode 110 — Balanced Binary Tree

## Pattern

- Postorder DFS
- Return height
- Check balance separately

## Core Idea

At every node:

```cpp
abs(leftHeight - rightHeight) <= 1
```

If this condition fails at any node, the tree is not balanced.

## Important Insight

The function **returns height**, not true/false.

```cpp
return 1 + max(lh, rh);
```

But at every node, we check:

```cpp
if (abs(lh - rh) > 1) ans = false;
```

## Code

```cpp
class Solution {
public:
    int checkHeight(TreeNode* root, bool &ans) {
        if (root == NULL) return 0;

        int lh = checkHeight(root->left, ans);
        int rh = checkHeight(root->right, ans);

        if (abs(lh - rh) > 1) {
            ans = false;
        }

        return 1 + max(lh, rh);
    }

    bool isBalanced(TreeNode* root) {
        bool ans = true;
        checkHeight(root, ans);
        return ans;
    }
};
```

## Common Mistake

Do not reset answer back to true:

```cpp
else {
    ans = true;
}
```

Once any subtree is unbalanced, final answer should stay false.

## One-Line Revision

Return height upward, check balance at every node.

---

# Pattern Comparison

| Problem | Function Returns | Function Computes / Checks |
|---|---|---|
| Diameter of Binary Tree | Height | Maximum diameter |
| Balanced Binary Tree | Height | Balance condition |

---

# Final Revision Line

In tree DFS, first get answers from left and right child, then use them at the current node, and return useful information back to the parent.