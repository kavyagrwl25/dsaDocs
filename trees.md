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

# LeetCode 100 — Same Tree

## Pattern

- DFS on two trees together
- Return true/false directly
- Compare structure and values

## Core Idea

Two trees are same if:

```text
current nodes are same
left subtrees are same
right subtrees are same
```

## Important Insight

Here the function **does not return height**.

It directly returns:

```text
Are these two subtrees same?
```

## Code

```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == NULL && q == NULL) return true;
        if (p == NULL || q == NULL) return false;
        if (p->val != q->val) return false;

        return isSameTree(p->left, q->left) &&
               isSameTree(p->right, q->right);
    }
};
```

## Important Concept

A recursive return goes only **one level up**, not directly to main.

So if one small subtree returns true, parent still checks the remaining subtree.

## `&&` Short-Circuit

```cpp
A && B
```

If `A` is false, `B` is not checked.

```text
true && false = false
false && true = false
```

So one mismatch anywhere makes the final answer false.

## One-Line Revision

Return whether current subtree pair is same using value check + left check + right check.

---

# Pattern Comparison

| Problem | Function Returns | Function Computes / Checks |
|---|---|---|
| Diameter of Binary Tree | Height | Maximum diameter |
| Balanced Binary Tree | Height | Balance condition |
| Same Tree | True/False | Same structure and values |

---

# Final Revision Line

In tree DFS, first understand what each recursive call should return.  
Sometimes it returns height and updates an answer, and sometimes it directly returns true/false.

---


# 572. Subtree of Another Tree

## Approach

At every node of `root`:

- Check if both trees are exactly same using `isSame()`
- If yes → return `true`
- Else search in:
  - left subtree
  - right subtree

---

## isSame()

Checks whether two trees are identical:

- Both NULL → true
- One NULL → false
- Values different → false
- Recursively compare left and right children

---

## Pattern

```text
DFS Traversal + Same Tree Check

Traverse every node in main tree → check if subtree rooted at that node is same as given subtree
```

---