# Python Tuple Interview Notes

## Module 1 — Tuple Fundamentals

A tuple is an ordered sequence whose slots cannot be reassigned. It is useful for fixed records, coordinates, database rows, configuration pairs, and multiple return values.

```python
empty = ()
point = (10, 20)
single = (42,)       # comma matters
not_tuple = (42)     # int: parentheses only group
packed = "Ada", 36, "ML"
name, age, job = packed
```

Packing collects comma-separated values; unpacking assigns them to matching targets. A tuple is immutable and usually heterogeneous; a list is mutable and commonly homogeneous. Use a list when the collection changes and a tuple when its structure is fixed. Common mistakes are omitting the comma in a one-item tuple, trying `t[0] = x`, and unpacking the wrong number of values. Interview tip: immutability is about tuple slots, not necessarily nested objects.

## Module 2 — Tuple Operations

For `t = (10, 20, 30, 20)`:

```python
t[0]                 # 10, indexing O(1)
t[-1]                # 20, negative indexing O(1)
t[1:3]              # (20, 30), slicing O(k) and creates a tuple
for value in t: ...   # iteration O(n)
20 in t               # True, membership O(n)
99 not in t           # True
t + (40,)             # concatenation; new tuple, O(n + m)
("x",) * 3            # repetition; O(k)
len(t)                # 4, O(1)
min(t), max(t)        # (10, 30), O(n)
sum(t)                # 80, O(n)
t.count(20)           # 2, O(n)
t.index(30)           # 2, O(n), ValueError if absent
```

`min`, `max`, and `sum` need compatible/numeric values. `index(value, start, stop)` can limit a search. Repeated membership tests are often better served by a set when order is irrelevant. A slice never mutates the source.

## Module 3 — Immutability (Deep Understanding)

```python
t = (1, 2)
# t[0] = 9             # TypeError
t += (3,)             # rebinding t to a new tuple; not in-place mutation

t = ([1, 2], [3, 4])
t[0].append(5)        # works: the list object changed
print(t)              # ([1, 2, 5], [3, 4])
# t[0] = [9]           # TypeError: tuple slot assignment
```

A tuple stores references. Its identity (`t is other`, or `id(t)`) can remain unchanged while the contents of a referenced list change. Equality compares contents. A tuple is hashable only if every nested item is hashable:

```python
good = {(12.9, 77.6): "Bengaluru"}
# bad = {([1, 2], "x"): "value"}  # TypeError: list is unhashable
```

Thus, not every tuple can be a dictionary key or set element. Interview answers should distinguish shallow immutability from deep immutability. Avoid mutable objects whose hash-relevant state can change even if a custom class is technically hashable.

## Module 4 — Packing, Unpacking & Pythonic Tricks

```python
record = "Riya", 95, True
student, score, passed = record
a, b = 1, 2
a, b = b, a                    # swap
head, *middle, tail = (1, 2, 3, 4)  # 1, [2, 3], 4
first, _, third = ("keep", "ignore", "keep")

def min_max(values):
    return min(values), max(values)  # returned as one tuple

for index, name in enumerate(("Ana", "Bo"), start=1):
    print(index, name)

for name, score in zip(("Ana", "Bo"), (90, 85)):
    print(name, score)
```

`_` conventionally means “intentionally ignored” but is still a variable. Star unpacking captures a list. Unpacking must match unless `*` is used. `zip` stops at the shortest input; use `zip(a, b, strict=True)` in Python 3.10+ when unequal lengths are a bug.

## Module 5 — Interview Coding Questions

### Questions (attempt first)

1. Reverse a tuple. 2. Find the second-largest distinct value. 3. Count frequencies. 4. Flatten a tuple of tuples. 5. Zip two tuples. 6. Sort `(name, score)` by score descending. 7. Convert list↔tuple. 8. Remove duplicates preserving order. 9. Unpack `(name, (city, country))`. 10. Find common values preserving first-tuple order. 11. Rotate right by `k`. 12. Partition even/odd. 13. Sum an arbitrarily nested tuple of integers. 14. Find the first maximum index.

### Solutions

```python
def reverse_tuple(values):
    return values[::-1]                 # O(n)

def second_largest(values):
    distinct = sorted(set(values))
    if len(distinct) < 2:
        raise ValueError("need two distinct values")
    return distinct[-2]                 # O(n log n)

def frequencies(values):
    counts = {}
    for value in values:
        counts[value] = counts.get(value, 0) + 1
    return tuple(counts.items())        # average O(n)

def flatten_once(values):
    return tuple(item for group in values for item in group)

def zip_tuples(left, right):
    return tuple(zip(left, right, strict=True))

def sort_by_score(rows):
    return tuple(sorted(rows, key=lambda row: row[1], reverse=True))

def convert(values):
    result = tuple(values)
    return result, list(result)

def unique_in_order(values):
    return tuple(dict.fromkeys(values))

def unpack_record(record):
    name, (city, country) = record
    return name, city, country

def common_in_order(left, right):
    right_values = set(right)
    return tuple(value for value in left if value in right_values)

def rotate_right(values, k):
    if not values:
        return values
    k %= len(values)
    return values[-k:] + values[:-k] if k else values

def partition_even_odd(values):
    return (tuple(v for v in values if v % 2 == 0),
            tuple(v for v in values if v % 2 != 0))

def nested_sum(value):
    if isinstance(value, int):
        return value
    return sum(nested_sum(item) for item in value)

def first_max_index(values):
    if not values:
        raise ValueError("empty tuple")
    best = 0
    for index, value in enumerate(values[1:], start=1):
        if value > values[best]:
            best = index
    return best
```

Key explanations: `set` removes duplicates but requires hashable values; `dict.fromkeys` preserves insertion order in modern Python; rotation uses modulo for large `k`; sorting is `O(n log n)`; the nested sum is recursive; the first-maximum solution uses one pass and updates only on `>`.

## Module 6 — Interview Theory

Tuples usually use less memory and can iterate slightly faster than lists because their size/structure is fixed, but this is implementation-dependent: measure real workloads with `timeit`. Both have O(1) indexing and O(n) search. Tuple concatenation in a loop can become O(n²); build a list and convert once.

Use tuples for immutable records, coordinates, fixed return groups, and hashable composite keys. Do not use them where items must be appended, removed, reordered, or updated. A tuple can be a dictionary key or set element only when all nested values are hashable. `sys.getsizeof` does not include recursively referenced objects.

### Top 20 tuple interview questions

1. **What is a tuple?** An ordered immutable sequence.
2. **Empty tuple?** `()` or `tuple()`.
3. **One-item tuple?** `(x,)`; the comma matters.
4. **Are parentheses required?** No; commas pack values.
5. **Can slots change?** No.
6. **Can it contain a list?** Yes, and that list can mutate.
7. **Are all tuples hashable?** No; nested items must be hashable.
8. **Why use tuples as keys?** Their hash can remain stable.
9. **Reverse syntax?** `t[::-1]`.
10. **What does `+` do?** Creates a new tuple.
11. **What does `*` do?** Repeats references into a new tuple.
12. **How unpack?** `a, b = t`.
13. **What does `*rest` capture?** Zero or more values in a list.
14. **Multiple function results?** Packed into a tuple.
15. **Membership complexity?** O(n).
16. **Index complexity?** O(1).
17. **Slice complexity?** O(k) to create the result.
18. **Why often faster than lists?** Fixed structure and lower overhead.
19. **When use a list?** When the collection changes.
20. **Core immutability distinction?** Immutable container does not mean immutable contents.

Final checklist: explain the comma, shallow immutability, identity versus contents, hashability, star unpacking, `enumerate`/`zip`, and time complexity. Prefer clear data contracts over micro-optimizing tuple-versus-list speed.
