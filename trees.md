# LeetCode 543 — Diameter of Binary Tree

## Difficulty

Medium

## Pattern

* Postorder DFS
* Return one thing, compute another

---

# Core Idea

At every node:

\text{diameterThroughNode} = \text{leftHeight} + \text{rightHeight}

Keep updating global maximum diameter.

---

# Recursive Meaning

```cpp id="d0pj0y"
height(node) = height of current subtree
```

---

# Why Postorder?

Because current node needs:

* left subtree height
* right subtree height

So children must be solved first.

---

# Important Insight

* Function RETURNS height
* But simultaneously UPDATES diameter

---

# Return Statement

```cpp id="gvnd6r"
return 1 + max(lh, rh);
```

---

# Common Mistake

Trying to directly return diameter from recursion.

---

# One-Line Revision

Return height upward, update diameter at every node.
