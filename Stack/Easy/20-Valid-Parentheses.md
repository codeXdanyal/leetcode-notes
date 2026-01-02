# LeetCode Problem 20: Valid Parentheses

### Table of Contents
- [Problem Description](#problem-description)
- [Problem Understanding](#problem-understanding)
- [Key Observations](#key-observations)
- [Constraints Analysis](#constraints-analysis)
- [Edge Cases](#edge-cases)
- [My Approach (Step-by-Step)](#my-approach-step-by-step)
- [Why This Approach Works](#why-this-approach-works)
- [Time and Space Complexity](#time-and-space-complexity)
- [Complete Code Implementation](#complete-code-implementation)

## Problem Description
Given a string s containing just the characters `'(', ')', '{', '}', '['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### Example 1:

```text 
Input: s = "()"

Output: true
```

### Example 2:

```text 
Input: s = "()[]{}"

Output: true
```

### Example 3:

```text 
Input: s = "(]"

Output: false
```

### Example 4:

```text 
Input: s = "([])"

Output: true
```

### Example 5:
```text
Input: s = "([)]"

Output: false
```

## Problem Understanding
You are given a string containing only parentheses characters: `()`, `{}`, and `[]`. The task is to determine whether the string is valid. A valid string must meet two conditions: every opening bracket must have a corresponding closing bracket of the same type, and brackets must be closed in the correct order. If any bracket is unmatched or misordered, the string is invalid. The goal is to return `true` if the string is valid, otherwise `false`.

## Key Observations
A stack data structure is ideal for this problem because it follows Last-In-First-Out (LIFO) order. The last opening bracket encountered should match the next closing bracket. Using a stack allows checking the most recently opened bracket against the current closing bracket efficiently. Each bracket is processed only once, and no additional memory beyond the stack is required.

## Constraints Analysis
The string length can range from 1 to 10,000 characters. An empty string is considered valid. Strings with only one bracket are invalid. Brackets can be nested in any combination, so a solution must correctly handle sequences like `"([{}])"` and `"([)]"`. Performance is not a major concern due to reasonable string length, but the algorithm must correctly handle edge cases and nested brackets.

## Edge Cases
- If the string is empty, return `true`.
- If the string contains only one bracket, return `false`.
- If a closing bracket appears before its corresponding opening bracket, return `false`.
- These checks prevent errors such as trying to access elements from an empty stack.

## My Approach (Step-by-Step)
Start by checking if the string is empty; if so, return `true`. Initialize an empty stack. Iterate through each character of the string. If the character is an opening bracket (`(, {, [`), push it onto the stack. If the character is a closing bracket (`), }, ]`), check if the stack is not empty and whether the top element matches this closing bracket. If it matches, pop the top element. If it does not match, return `false`. After processing all characters, check if the stack is empty. If it is, return `true`; otherwise, return `false`.

## Why This Approach Works
The stack ensures that brackets are matched in the correct order. The last opened bracket is always at the top of the stack, which guarantees correct pairing with the next closing bracket. Because each opening bracket is pushed once and popped once, all brackets are checked exactly once, ensuring correctness for nested and sequential brackets.

## Time and Space Complexity
Time complexity is `O(n)`, where n is the length of the string, since each character is processed once. Space complexity is `O(n)` in the worst case if all characters are opening brackets, as they will all be stored in the stack.

## Complete Code Implementation
```cpp

class Solution
{


public:
    bool isValid(string str)
    {
        stack<char> s;
        
        if (str.empty())
        {
            return true;
        }

        for (char c : str)
        {
            if (c == '(' || c == '{' || c == '[')
            {
                s.push(c);
            }
            else if (!s.empty() &&
                     ((s.top() == '(' && c == ')') ||
                      (s.top() == '{' && c == '}') ||
                      (s.top() == '[' && c == ']')))
            {
                s.pop();
            }
            else
            {
                return false;
            }
        }

        if (!s.empty())
            return false;
        return true;
    }
};
```


