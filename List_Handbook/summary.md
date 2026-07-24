# Python List Handbook - Summary

This folder is a beginner-friendly handbook for Python lists. It starts from the basics and gradually moves toward interview-ready concepts like traversal, copying, nested lists, comprehensions, and important list functions.

## What You Should Know After Completing This Folder

- What a list is and why Python lists are dynamic arrays.
- How to create lists using `[]`, values, mixed data, nested lists, and `list()`.
- How indexing and negative indexing work.
- How slicing works and how it creates a new list.
- How to add, update, and delete elements.
- How to search inside a list.
- How to traverse a list using `for`, `while`, `range()`, `enumerate()`, `zip()`, and `reversed()`.
- How assignment, shallow copy, and deep copy differ.
- How nested lists represent 2D data like matrices.
- How list comprehensions make clean new lists.
- Which list functions and methods are most important for interviews.

## Section-Wise Map

| File | Topic | Main Idea |
|---|---|---|
| `1_.ipynb` | Introduction | Lists are ordered, mutable, indexed, dynamic collections. |
| `2_.ipynb` | Creating Lists | Different ways to create lists. |
| `3_.ipynb` | Accessing Elements | Indexing, negative indexing, and reading values. |
| `4_.ipynb` | Updating Lists | Changing values using index positions. |
| `5_.ipynb` | Adding Elements | Adding items using methods like `append()`, `insert()`, and `extend()`. |
| `6_.ipynb` | Removing Elements | Removing values using `pop()`, `remove()`, `del`, and related ideas. |
| `7_.ipynb` | Slicing Lists | Extracting parts of a list using start, stop, and step. |
| `8_.ipynb` | Searching Lists | Finding values and checking membership. |
| `9_.ipynb` | Traversing Lists | Visiting each element in different ways. |
| `10_.ipynb` | Copying Lists | Assignment vs copying, shallow copy, and deep copy. |
| `11_.ipynb` | Nested Lists | 2D lists, matrix-style data, and nested traversal. |
| `12_.ipynb` | List Comprehensions | Creating new lists with compact syntax. |
| `13_.ipynb` | List Functions and Methods | Most-used built-ins and list methods. |

## Most Important Interview Points

### 1. Lists Are Mutable

A list can be changed after creation.

```python
nums = [10, 20, 30]
nums[1] = 99
print(nums)
```

Output:

```python
[10, 99, 30]
```

### 2. Assignment Does Not Copy a List

```python
a = [1, 2, 3]
b = a
b.append(4)

print(a)
```

Output:

```python
[1, 2, 3, 4]
```

Both `a` and `b` point to the same list.

### 3. Use copy() or Slicing for a Shallow Copy

```python
a = [1, 2, 3]
b = a.copy()

b.append(4)

print(a)
print(b)
```

### 4. append() vs extend()

```python
a = [1, 2]
a.append([3, 4])
print(a)
```

Output:

```python
[1, 2, [3, 4]]
```

```python
a = [1, 2]
a.extend([3, 4])
print(a)
```

Output:

```python
[1, 2, 3, 4]
```

### 5. pop() vs remove()

```python
nums = [10, 20, 30]

nums.pop(1)      # removes by index
nums.remove(30)  # removes by value
```

### 6. sort() vs sorted()

```python
nums = [3, 1, 2]

new_nums = sorted(nums)
print(nums)
print(new_nums)

nums.sort()
print(nums)
```

`sorted()` creates a new list. `sort()` changes the original list.

### 7. List Comprehension Is for Creating New Lists

```python
nums = [1, 2, 3, 4]
squares = [num * num for num in nums]

print(squares)
```

Output:

```python
[1, 4, 9, 16]
```

## Common Time Complexities

| Operation | Complexity | Reason |
|---|---:|---|
| Access by index | `O(1)` | Direct index lookup |
| Update by index | `O(1)` | Direct index update |
| `append()` | Usually `O(1)` | Adds at end |
| `pop()` | `O(1)` | Removes from end |
| `insert()` | `O(n)` | Elements may shift |
| `pop(index)` | `O(n)` | Elements may shift |
| `remove(value)` | `O(n)` | Searches first |
| `value in list` | `O(n)` | Linear search |
| Slicing | `O(k)` | Copies `k` elements |
| Traversal | `O(n)` | Visits all elements |
| Sorting | `O(n log n)` | Python uses Timsort |

## Beginner Mistakes To Avoid

- Do not use `list` as a variable name.
- Do not confuse index and value.
- Remember that indexing starts from `0`.
- Remember that slicing excludes the stop index.
- Do not modify a list while looping over it unless you know exactly what you are doing.
- Remember that many list methods change the list and return `None`.
- Use `deepcopy()` when copying nested lists that must be fully independent.

## Quick Revision Checklist

- Can you create an empty list?
- Can you access the first and last element?
- Can you slice the first three elements?
- Can you add one element at the end?
- Can you remove an element by value?
- Can you remove an element by index?
- Can you loop with both index and value using `enumerate()`?
- Can you copy a list without aliasing?
- Can you flatten a 2D list?
- Can you write a simple list comprehension?

## Final Advice

For interviews, focus on clarity first. Python lists are simple to use, but interviewers often test whether you understand what happens internally: indexing, shifting, copying, mutability, and time complexity.

If your solution uses lists correctly and you can explain the complexity, you are already in a strong position.
