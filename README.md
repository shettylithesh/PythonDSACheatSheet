# Python Cheat Sheet

A Cheat Sheet 📜 to **revise** Python syntax in **less time**. Particularly useful for solving Data Structure and Algorithmic problems or a quick overview before an interview.

> [Click here for similar Java Resource (not made by me)](https://drive.google.com/file/d/1ao4ZA28zzBttDkuS6MLQI52gDs_CJZEm/view) <br>
> Get a PDF of this sheet at the end. <br>
> Leave a ⭐ if you like the cheat sheet (contributions welcome!) <br>

# Table of Contents
- [Basics](#basics)
- [Data Structures](#data-structures)
  - [Lists](#lists)
  - [Dictionary](#dictionary)
  - [Counter](#counter)
  - [Deque](#deque)
  - [Heapq](#heapq)
  - [Sets](#sets)
  - [Tuples](#tuples)
  - [Strings](#strings)
- [Built-in Functions](#built-in-functions)
- [Advanced Topics](#advanced-topics)
- [Best Practices](#best-practices)
- [Tips & Gotchas](#tips--gotchas)

# Basics

## Data Types
![Python Data Types](https://user-images.githubusercontent.com/59110866/173563442-1a6fa3d2-b569-4eb0-99cc-9b91cc8be1eb.png)

## Operator Precedence
![Python Operators](https://user-images.githubusercontent.com/47276307/172329850-61fc0809-a4b0-416c-848b-1c502ecb4772.jpg)

# Data Structures

## Lists
Time Complexities:
![List Operations](https://user-images.githubusercontent.com/47276307/172330098-1c5f0a6e-7f80-4f4f-9be6-1d734e2c70cd.jpg)

```python
nums = [1,2,3]

# Common Operations
nums.index(1)      # Find index
nums.append(1)     # Add to end
nums.insert(0,10)  # Add 10 from left (at index 0 which is start)
nums.remove(3)     # Remove value
nums.pop()         # Remove & return last element
nums.sort()        # In-place sort (TimSort: O(n log n))
nums.reverse()     # In-place reverse
nums.copy()        # Return shallow copy

# List Slicing
nums[start:stop:step]  # Generic slice syntax
nums[-1]    # Last item
nums[::-1]  # Reverse list
nums[1:]    # Everything after index 1
nums[:3]    # First three elements
```
```python
nums = [1, 2, 3, 4]

# Missing but useful:
nums.count(2)          # Count occurrences of 2 → 1
nums.clear()           # Empty the list → []
nums.extend([5,6])     # Extend with another iterable → [1,2,3,4,5,6]
nums *= 2              # Repeat list → [1,2,3,4,1,2,3,4]
a = list("abc")        # ['a', 'b', 'c'] - incase string manipulation needed with extra space of O(n)

# List Comprehensions (missing in original)
matrix = [[1,2], [3,4]]
flattened = [x for row in matrix for x in row]  # [1, 2, 3, 4]
conditional = [x for x in range(5) if x % 2 == 0]  # [0, 2, 4]
```
## Dictionary
Time Complexities:
![Dictionary Operations](https://user-images.githubusercontent.com/47276307/172330107-e68e3228-1c76-4bfb-bb38-04d18f94d5b9.jpg)

```python
d = {'a':1, 'b':2}

# Essential Operations
d.get('key', default)     # Safe access with default
d.setdefault('key', 0)    # Set if missing
d.items()                 # Key-value pairs
d.keys()                  # Just keys
d.values()               # Just values
d.pop(key)              # Remove and return value
d.update({key: value})  # Batch update

# Advanced Usage
from collections import defaultdict
d = defaultdict(list)     # Auto-initialize missing keys
d = defaultdict(int)      # Useful for counting
```
```python
d = {'a': 1, 'b': 2}

# Missing but critical:
d.popitem()            # Remove and return last (key,val) → ('b', 2)
dict.fromkeys(['a','b'], 0)  # Create dict with keys → {'a':0, 'b':0}
d | {'c':3}            # Merge (Python 3.9+) → {'a':1, 'b':2, 'c':3}

# Dictionary Comprehensions (missing)
square_dict = {x: x**2 for x in range(3)}  # {0: 0, 1: 1, 2: 4}
swapped = {v: k for k, v in {'a': 1}.items()}  # {1: 'a'}
```
```
📌 Remember
- You cannot use a list as dictionary because lists can't be hashed.
```
## Counter
```python
from collections import Counter

# Initialize
c = Counter(['a','a','b'])    # From iterable
c = Counter("hello")          # From string

# Operations
c.most_common(2)      # Top 2 frequent elements
c['a'] += 1           # Increment count
c.update("more")      # Add counts from iterable
c.total()             # Sum of all counts
```
```python
from collections import Counter
c = Counter('abracadabra')

# Missing but handy:
c.elements()           # Iterator: 'a'×5, 'b'×2, etc.
c.subtract({'a':1})    # In-place subtract → Counter({'a':4})
+c                     # Remove zero/negative counts → Counter({'a':5})
```

## Deque
Time Complexities:
![Deque Operations](https://user-images.githubusercontent.com/47276307/172330115-78500420-3276-4e45-8ce3-fd668b7eb14e.jpg)

```python
from collections import deque

# Perfect for BFS - O(1) operations on both ends
d = deque()
d.append(1)          # Add right
d.appendleft(2)      # Add left
d.pop()              # Remove right
d.popleft()          # Remove left
d.extend([1,2,3])    # Extend right
d.extendleft([1,2,3])# Extend left
d.rotate(n)          # Rotate n steps right (negative for left)
```
```python
from collections import deque
d = deque([1,2,3])

# Missing but useful:
d.clear()              # Empty deque → deque([])
d.maxlen               # None (or fixed max length if set)
d.reverse()            # In-place reverse → deque([3,2,1])
```
## Heapq

```python
import heapq

# MinHeap Operations - All O(log n) except heapify
nums = [3,1,4,1,5]
heapq.heapify(nums)          # Convert to heap in-place: O(n)
heapq.heappush(nums, 2)      # Add element: O(log n)
smallest = heapq.heappop(nums)  # Remove smallest: O(log n)

# MaxHeap Trick: Multiply by -1
nums = [-x for x in nums]    # Convert to maxheap: O(n)
heapq.heapify(nums)          # O(n)
largest = -heapq.heappop(nums)  # Get largest: O(log n)

# Advanced Operations
k_largest = heapq.nlargest(k, nums)    # O(n * log k)
k_smallest = heapq.nsmallest(k, nums)  # O(n * log k)

# Custom Priority Queue
heap = []
heapq.heappush(heap, (priority, item))  # Sort by priority
```
```python
import heapq

# Missing but practical:
heapq.merge([1,3], [2,4])  # Merge sorted iterables → [1,2,3,4]
heapq.heappushpop(heap, 0)  # Push 0 then pop smallest
heapq.heapreplace(heap, 0)  # Pop smallest then push 0
```

## Sets
Time Complexities:
![Untitled](https://user-images.githubusercontent.com/47276307/172330132-7a785f5f-bbc6-43b9-b82f-794190813787.jpg)

```python
s = {1,2,3}

# Common Operations
s.add(4)             # Add element
s.remove(4)          # Remove (raises error if missing)
s.discard(4)         # Remove (no error if missing)
s.pop()              # Remove and return arbitrary element

# Set Operations
a.union(b)           # Elements in a OR b
a.intersection(b)    # Elements in a AND b
a.difference(b)      # Elements in a but NOT in b
a.symmetric_difference(b)  # Elements in a OR b but NOT both
a.issubset(b)        # True if all elements of a are in b
a.issuperset(b)      # True if all elements of b are in a
```
```python
s1, s2 = {1,2}, {2,3}

# Missing but powerful:
s1.isdisjoint(s2)      # True if no common elements → False
s1.intersection_update(s2)  # In-place intersection → s1 = {2}
s1.difference_update(s2)    # In-place difference → s1 = {1}

# Set Comprehensions (missing)
unique_chars = {c for c in 'hello'}  # {'h', 'e', 'l', 'o'}
squares = {x**2 for x in [-2, 2]}  # {4} (duplicates removed)
```

## Tuples
```python
# Tuples are immutable lists
t = (1, 2, 3, 1)

# Essential Operations
t.count(1)      # Count occurrences of value
t.index(2)      # Find first index of value

# Useful Patterns
x, y = (1, 2)   # Tuple unpacking
coords = [(1,2), (3,4)]  # Tuple in collections
```
```python
t = (1, 2, [3, 4])

# Missing but important:
hash((1,2))           # Works if all elements immutable
t[2].append(5)        # Mutable elements can change! → (1,2,[3,4,5])
```

## Strings
```python
s = "hello world"

# Essential Methods
s.split()            # Split on whitespace
s.split(',')         # Split on comma
s.strip()            # Remove leading/trailing whitespace
s.lower()            # Convert to lowercase
s.upper()            # Convert to uppercase
s.isalnum()          # Check if alphanumeric
s.isalpha()          # Check if alphabetic
s.isdigit()          # Check if all digits
s.find('sub')        # Index of substring (-1 if not found)
s.count('sub')       # Count occurrences
s.replace('old', 'new')  # Replace all occurrences

# ASCII Conversion
ord('a')             # Char to ASCII (97)
chr(97)              # ASCII to char ('a')

# Join Lists
''.join(['a','b'])   # Concatenate list elements, can be used while doing string manipulation in O(1) instead of O(n)

#Traversal - just like lists using 'in' operator, indexes.

#String Slicing - just like list slicing

```
```python
s = "Python"

# Missing but useful:
s.startswith('Py')     # True
s.endswith('on')       # True
s.partition('th')      # ('Py', 'th', 'on')
s.rjust(10, '*')       # '****Python' (right-justify)
s.encode('utf-8')      # Convert to bytes → b'Python'

# String One-Liners (missing)
is_palindrome = s == s[::-1]  # True if palindrome
alternating = 'abc' * 2  # 'abcabc' (string repetition)
```

# Built-in Functions

```python
# Iteration Helpers
enumerate(lst)        # Index + value pairs
zip(lst1, lst2)      # Parallel iteration
map(fn, lst)         # Apply function to all elements
filter(fn, lst)      # Keep elements where fn returns True
any(lst)             # True if any element is True
all(lst)             # True if all elements are True
len(lst)             # returns length of list, tuple, set, dict, string, etc

# Binary Search (import bisect)
bisect.bisect(lst, x)     # Find insertion point
bisect.bisect_left(lst, x)# Find leftmost insertion point
bisect.insort(lst, x)     # Insert maintaining sort

# Type Conversion
int('42')            # String to int
str(42)              # Int to string
list('abc')          # String to list
''.join(['a','b'])   # List to string
set([1,2,2])         # List to set

# Math
abs(-5)              # Absolute value
pow(2, 3)            # Power
round(3.14159, 2)    # Round to decimals
```
```python
# Missing but essential:
sum([1,2,3])          # Sum elements → 6
min([1,2,3], key=lambda x: -x)  # Custom key → 3
eval('2+3')           # Evaluate string → 5 (use cautiously!)
locals()              # Dictionary of local variables
```

# Advanced Topics

## Custom Sorting with cmp_to_key
```python
from functools import cmp_to_key

def compare(item1, item2):
    # Return -1: item1 comes first
    # Return 1:  item2 comes first
    # Return 0:  items are equal
    if item1 < item2:
        return -1
    elif item1 > item2:
        return 1
    return 0

# Sort using custom comparison
sorted_list = sorted(items, key=cmp_to_key(compare))
```

## Taking Multiple Inputs
```python
# Basic multiple input
x, y = input("Enter two values: ").split()

# Multiple integers
x, y = map(int, input("Enter two numbers: ").split())

# List of integers
nums = list(map(int, input("Enter numbers: ").split()))

# Multiple inputs with custom separator
values = input("Enter comma-separated values: ").split(',')

# List comprehension method
x, y = [int(x) for x in input("Enter two numbers: ").split()]
```

## Math Module Essentials
```python
import math

# Constants
math.pi       # 3.141592653589793
math.e        # 2.718281828459045

# Common Functions
math.ceil(2.3)        # 3 - Smallest integer greater than x
math.floor(2.3)       # 2 - Largest integer less than x
math.gcd(a, b)        # Greatest common divisor
math.log(x, base)     # Logarithm with specified base
math.sqrt(x)          # Square root
math.pow(x, y)        # x^y (prefer x ** y for integers)

# Trigonometry
math.degrees(rad)     # Convert radians to degrees
math.radians(deg)     # Convert degrees to radians
```

## Important Python Integer Operations
```python
# Binary representation
bin(10)              # '0b1010'
format(10, 'b')      # '1010' (without prefix)

# Division and Modulo
divmod(10, 3)        # (3, 1) - returns (quotient, remainder)

# Negative number handling
x = -3
y = 2
print(x // y)        # -2 (floor division)
print(int(x/y))      # -1 (preferred for negative numbers)
print(x % y)         # 1 (Python's modulo with negative numbers)
```
## Structural Pattern Matching (Python 3.10+)
```python
match value:
    case 1: print("One")
    case x if x > 1: print(f"Greater than 1: {x}")
    case _: print("Other")

# Walrus Operator (Python 3.8+)
if (n := len([1,2,3])) > 2: 
    print(f"Length is {n}")  # → Length is 3
```
# Best Practices

## Documentation
```python
def binary_search(arr, target):
    """
    Find target in sorted array using binary search.
    Args:
        arr: Sorted list of numbers
        target: Number to find
    Returns:
        Index of target or -1 if not found
    """
    pass
```

## Testing
```python
# Use assertions for edge cases
assert binary_search([], 1) == -1, "Empty array should return -1"
assert binary_search([1], 1) == 0, "Single element array should work"
```

# Tips & Gotchas

1. Integer Division:
```python
# Use int() for consistent negative number handling
print(-3//2)        # Returns -2
print(int(-3/2))    # Returns -1 (usually desired)
```

2. Default Dictionaries:
```python
# Prefer defaultdict for frequency counting
from collections import defaultdict
freq = defaultdict(int)
for x in lst:
    freq[x] += 1    # No KeyError if x is new
```

3. Heap Priority:
```python
# For custom priority in heapq, use tuples
heap = []
heapq.heappush(heap, (priority, item))
```

4. List Comprehension:
```python
# Often clearer than map/filter
squares = [x*x for x in range(10) if x % 2 == 0]
```

5. String Building:
```python
# Use join() instead of += for strings
chars = ['a', 'b', 'c']
word = ''.join(chars)  # More efficient
```

6. Using Sets for Efficiency:
```python
# O(1) lookup for contains operations
seen = set()
if x in seen:  # Much faster than list lookup
    print("Found!")
```

7. Custom Sort Keys:
```python
# Sort by length then alphabetically
words.sort(key=lambda x: (len(x), x))
```

8. Default Arguments Warning:
```python
# Don't use mutable defaults
def bad(lst=[]):     # This can cause bugs
    lst.append(1)
    return lst

def good(lst=None):  # Do this instead
    if lst is None:
        lst = []
    lst.append(1)
    return lst
```

---
Made with ❤️ for fellow leetcoders.
