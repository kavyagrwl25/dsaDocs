# Stack Revision — DSA Short Notes

## 1. What is Stack?

A stack is a linear data structure that follows:

LIFO = Last In, First Out

The element inserted last is removed first.

Example:

Stack of plates

---

## 2. Basic Stack Operations

```cpp
stack<int> st;

st.push(x);    // insert element
st.pop();      // remove top element
st.top();      // access top element
st.empty();    // check empty or not
st.size();     // size of stack
```

Important:

```cpp
st.pop(); // does not return the popped value
```

Correct way:

```cpp
int x = st.top();
st.pop();
```

---

## 3. When to Think of Stack?

Think of stack when the problem involves:

- Previous useful elements
- Reversal
- Undo operation
- Matching brackets
- Nested structure
- Next greater / smaller
- Previous greater / smaller

Common keywords:

- nearest
- previous
- next
- valid parentheses
- balanced
- remove
- span
- histogram
- monotonic

---

## 4. Core Stack Pattern

```cpp
stack<int> st;

for(int i = 0; i < n; i++) {
    while(!st.empty() && condition) {
        st.pop();
    }

    // use st.top() if needed

    st.push(arr[i]);
}
```

Main idea:

Pop useless elements.  
Keep useful elements.

---

## 5. Parentheses / Matching Pattern

Used in:

- Valid Parentheses
- Balanced Brackets
- Min Remove to Make Valid Parentheses

```cpp
bool isValid(string s) {
    stack<char> st;

    for(char ch : s) {
        if(ch == '(' || ch == '{' || ch == '[') {
            st.push(ch);
        }
        else {
            if(st.empty()) return false;

            if(ch == ')' && st.top() != '(') return false;
            if(ch == '}' && st.top() != '{') return false;
            if(ch == ']' && st.top() != '[') return false;

            st.pop();
        }
    }

    return st.empty();
}
```

Core thought:

Opening bracket waits for its correct closing bracket.

---

## 6. Monotonic Stack

A monotonic stack keeps elements in a useful sorted order.

It is mostly used for:

- Next Greater Element
- Next Smaller Element
- Previous Greater Element
- Previous Smaller Element
- Stock Span
- Daily Temperatures
- Largest Rectangle in Histogram

---

## 7. Increasing Stack

An increasing stack keeps smaller elements below bigger elements.

Used when finding smaller elements.

```cpp
while(!st.empty() && st.top() >= curr) {
    st.pop();
}
```

Meaning:

Remove elements greater than or equal to current.

---

## 8. Decreasing Stack

A decreasing stack keeps bigger elements below smaller elements.

Used when finding greater elements.

```cpp
while(!st.empty() && st.top() <= curr) {
    st.pop();
}
```

Meaning:

Remove elements smaller than or equal to current.

---

## 9. Next Greater Element on Right

Traverse from right to left.

```cpp
vector<int> ans(n, -1);
stack<int> st; // stores indices

for(int i = n - 1; i >= 0; i--) {
    while(!st.empty() && arr[st.top()] <= arr[i]) {
        st.pop();
    }

    if(!st.empty()) {
        ans[i] = arr[st.top()];
    }

    st.push(i);
}
```

Why store index?

Because index gives both value and position.

---

## 10. Previous Greater / Smaller

Traverse from left to right.

```cpp
for(int i = 0; i < n; i++) {
    while(!st.empty() && condition) {
        st.pop();
    }

    if(!st.empty()) {
        ans[i] = st.top();
    }

    st.push(arr[i]);
}
```

Direction rule:

Next element -> usually right to left  
Previous element -> usually left to right

---

## 11. Most Important Stack Thought

Before solving, ask:

Do I need to remember previous useful elements?

If yes, stack may work.

Then ask:

Which elements are useless now?

Those elements should be popped.

---

## 12. Must-Solve Stack Problems

1. Valid Parentheses
2. Next Greater Element
3. Previous Smaller Element
4. Daily Temperatures
5. Stock Span
6. Min Stack
7. Largest Rectangle in Histogram
8. Asteroid Collision
9. Remove K Digits

---

## 13. Final Cheat Sheet

Stack = LIFO

Use stack for:

- Brackets
- Reversal
- Undo
- Nested logic
- Nearest greater/smaller
- Previous useful elements

Monotonic stack:

- Pop useless elements
- Keep useful elements

Direction:

- Next greater/smaller -> right to left
- Previous greater/smaller -> left to right

Store index when:

- Position matters
- Distance matters
- Answer needs original index