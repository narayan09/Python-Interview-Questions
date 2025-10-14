# Python List Interview Questions & Answers

A comprehensive collection of Python list interview questions organized by difficulty level - from basic to advanced programming challenges. Perfect for preparing for Python developer interviews with 5+ years of experience.

## 📋 Table of Contents
- [Common Questions (20)](#common-questions)
- [Technical Questions on Lists (10)](#technical-questions-on-lists)  
- [Programming Questions with Lists (10)](#programming-questions-with-lists)
- [How to Use This Repository](#how-to-use-this-repository)

---

## Common Questions

### Basic Level (1-7)

**1. What is a list in Python?**  
A list is a mutable, ordered collection of elements that can store different data types. Elements are enclosed in square brackets `[]`.

**2. How do you create an empty list in Python?**  
```python
empty_list = []
# or
empty_list = list()
```

**3. What is the difference between a list and tuple?**  
- Lists are mutable (can be changed), tuples are immutable
- Lists use `[]`, tuples use `()`
- Lists have more built-in methods than tuples

**4. How do you access elements in a list?**  
Using indexing: `my_list[0]` (first element), `my_list[-1]` (last element)

**5. What are list comprehensions?**  
A concise way to create lists using a single line of code:
```python
squares = [x**2 for x in range(10)]
```

**6. How do you add elements to a list?**  
- `append()`: Add single element at end
- `insert()`: Add element at specific position  
- `extend()`: Add multiple elements

**7. How do you remove elements from a list?**  
- `remove()`: Remove by value
- `pop()`: Remove by index (returns element)
- `del`: Delete by index or slice

### Medium Level (8-14)

**8. What is the difference between `append()` and `extend()`?**  
- `append()` adds entire object as single element
- `extend()` adds each element individually

**9. How do you reverse a list in Python?**  
```python
# Method 1: In-place
my_list.reverse()

# Method 2: Create new list
new_list = my_list[::-1]

# Method 3: Using reversed()
new_list = list(reversed(my_list))
```

**10. How can you iterate over two lists simultaneously?**  
Using `zip()` function:
```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
for num, letter in zip(list1, list2):
    print(num, letter)
```

**11. What is list slicing? Give examples.**  
Extracting portions of a list using `[start:stop:step]`:
```python
my_list = [0, 1, 2, 3, 4, 5]
print(my_list[1:4])    # [1, 2, 3]
print(my_list[::2])    # [0, 2, 4]
print(my_list[::-1])   # [5, 4, 3, 2, 1, 0]
```

**12. How do you convert a list of characters to a string?**  
```python
char_list = ['h', 'e', 'l', 'l', 'o']
result = ''.join(char_list)  # 'hello'
```

**13. How do you find the maximum and minimum elements in a list?**  
```python
my_list = [3, 1, 4, 1, 5, 9, 2, 6]
max_val = max(my_list)  # 9
min_val = min(my_list)  # 1
```

**14. What happens when you modify a list while iterating over it?**  
It can cause unexpected behavior. Better to iterate over a copy or use list comprehension.

### Advanced Level (15-20)

**15. How do you flatten a nested list?**  
```python
# Using list comprehension
nested = [[1, 2], [3, 4], [5, 6]]
flattened = [item for sublist in nested for item in sublist]

# Using itertools
import itertools
flattened = list(itertools.chain.from_iterable(nested))
```

**16. What is the difference between deep copy and shallow copy of lists?**  
- Shallow copy: Creates new list but references same objects
- Deep copy: Creates new list with new copies of all objects

**17. How do you sort a list of dictionaries by a specific key?**  
```python
students = [{'name': 'John', 'age': 25}, {'name': 'Jane', 'age': 22}]
sorted_students = sorted(students, key=lambda x: x['age'])
```

**18. What are the time complexities of common list operations?**  
- Access by index: O(1)
- Append: O(1) amortized
- Insert at beginning: O(n)
- Delete by index: O(n)
- Search: O(n)

**19. How do you remove duplicates from a list while preserving order?**  
```python
def remove_duplicates(lst):
    seen = set()
    result = []
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result
```

**20. Explain list multiplication vs list repetition.**  
```python
# List repetition
[0] * 3  # [0, 0, 0] - creates 3 separate integers

# List multiplication with mutable objects
[[0] * 3] * 2  # [[0, 0, 0], [0, 0, 0]] - same inner list referenced twice
```

---

## Technical Questions on Lists

**1. What is the internal implementation of Python lists?**  
Python lists are implemented as dynamic arrays (C arrays) with extra space allocated for efficient appends.

**2. How does Python handle memory allocation for lists?**  
Lists over-allocate memory to make append operations efficient. When capacity is exceeded, a new larger array is allocated.

**3. What is the difference between `is` and `==` when comparing lists?**  
- `==` compares values/content
- `is` compares object identity (memory location)

**4. How do you create a list of lists without reference issues?**  
```python
# Wrong way (all sublists are same object)
matrix = [[0] * 3] * 3

# Correct way
matrix = [[0] * 3 for _ in range(3)]
```

**5. What is list mutability and how does it affect function parameters?**  
Lists are mutable objects passed by reference. Modifications inside functions affect the original list.

**6. How do `sort()` and `sorted()` differ?**  
- `sort()`: Sorts list in-place, returns None
- `sorted()`: Returns new sorted list, original unchanged

**7. What is the purpose of `__len__()` and `__getitem__()` in lists?**  
These are magic methods that enable `len(list)` and `list[index]` functionality.

**8. How do you implement a custom comparison for list sorting?**  
```python
# Using key function
sorted(words, key=len)  # Sort by length

# Using functools.cmp_to_key for complex comparisons
from functools import cmp_to_key
sorted(items, key=cmp_to_key(custom_compare))
```

**9. What are list iterators and how do they work?**  
Lists are iterable objects. `iter(list)` returns an iterator that tracks position and raises `StopIteration` when exhausted.

**10. How does Python's garbage collection work with lists containing circular references?**  
Python uses reference counting + cycle detection to handle circular references in data structures like lists.

---

## Programming Questions with Lists

**1. Write a function to find the second largest number in a list.**
```python
def find_second_largest(numbers):
    if len(numbers) < 2:
        return None
    
    largest = second_largest = float('-inf')
    
    for num in numbers:
        if num > largest:
            second_largest = largest
            largest = num
        elif num > second_largest and num != largest:
            second_largest = num
            
    return second_largest if second_largest != float('-inf') else None

# Test
print(find_second_largest([3, 1, 4, 1, 5, 9, 2, 6]))  # Output: 6
```

**2. Implement a function to rotate a list by k positions.**
```python
def rotate_list(lst, k):
    if not lst:
        return lst
    
    k = k % len(lst)  # Handle k > len(lst)
    return lst[-k:] + lst[:-k]

# Test
print(rotate_list([1, 2, 3, 4, 5], 2))  # Output: [4, 5, 1, 2, 3]
```

**3. Write a function to merge two sorted lists.**
```python
def merge_sorted_lists(list1, list2):
    result = []
    i = j = 0
    
    while i < len(list1) and j < len(list2):
        if list1[i] <= list2[j]:
            result.append(list1[i])
            i += 1
        else:
            result.append(list2[j])
            j += 1
    
    # Add remaining elements
    result.extend(list1[i:])
    result.extend(list2[j:])
    return result

# Test
print(merge_sorted_lists([1, 3, 5], [2, 4, 6]))  # Output: [1, 2, 3, 4, 5, 6]
```

**4. Find all pairs in a list that sum to a target value.**
```python
def find_pairs_with_sum(lst, target):
    seen = set()
    pairs = []
    
    for num in lst:
        complement = target - num
        if complement in seen:
            pairs.append((complement, num))
        seen.add(num)
    
    return pairs

# Test
print(find_pairs_with_sum([2, 7, 11, 15, 3, 6], 9))  # Output: [(2, 7), (3, 6)]
```

**5. Implement a function to find the longest increasing subsequence.**
```python
def longest_increasing_subsequence(arr):
    if not arr:
        return []
    
    n = len(arr)
    lis = [1] * n
    parent = [-1] * n
    
    for i in range(1, n):
        for j in range(i):
            if arr[j] < arr[i] and lis[j] + 1 > lis[i]:
                lis[i] = lis[j] + 1
                parent[i] = j
    
    # Find the ending position of LIS
    max_length = max(lis)
    max_idx = lis.index(max_length)
    
    # Reconstruct the LIS
    result = []
    current = max_idx
    while current != -1:
        result.append(arr[current])
        current = parent[current]
    
    return result[::-1]

# Test
print(longest_increasing_subsequence([10, 9, 2, 5, 3, 7, 101, 18]))
```

**6. Write a function to remove duplicates from a list while maintaining order.**
```python
def remove_duplicates_ordered(lst):
    seen = set()
    result = []
    
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    
    return result

# Test
print(remove_duplicates_ordered([1, 2, 2, 3, 4, 4, 5]))  # Output: [1, 2, 3, 4, 5]
```

**7. Implement a function to find the intersection of multiple lists.**
```python
def find_intersection(*lists):
    if not lists:
        return []
    
    result = set(lists[0])
    for lst in lists[1:]:
        result &= set(lst)
    
    return list(result)

# Test
print(find_intersection([1, 2, 3, 4], [2, 3, 4, 5], [3, 4, 5, 6]))  # Output: [3, 4]
```

**8. Write a function to find the maximum sum of any contiguous subarray (Kadane's Algorithm).**
```python
def max_subarray_sum(arr):
    if not arr:
        return 0
    
    max_current = max_global = arr[0]
    
    for i in range(1, len(arr)):
        max_current = max(arr[i], max_current + arr[i])
        max_global = max(max_global, max_current)
    
    return max_global

# Test
print(max_subarray_sum([-2, 1, -3, 4, -1, 2, 1, -5, 4]))  # Output: 6
```

**9. Implement a function to rearrange array elements by sign (positive and negative alternately).**
```python
def rearrange_by_sign(arr):
    positive = [x for x in arr if x > 0]
    negative = [x for x in arr if x < 0]
    
    result = []
    min_len = min(len(positive), len(negative))
    
    for i in range(min_len):
        result.append(positive[i])
        result.append(negative[i])
    
    # Add remaining elements
    result.extend(positive[min_len:])
    result.extend(negative[min_len:])
    
    return result

# Test
print(rearrange_by_sign([1, 2, 3, -4, -1, 4]))  # Output: [1, -4, 2, -1, 3, 4]
```

**10. Write a function to find all unique triplets that sum to zero.**
```python
def three_sum(nums):
    nums.sort()
    result = []
    
    for i in range(len(nums) - 2):
        # Skip duplicates
        if i > 0 and nums[i] == nums[i-1]:
            continue
            
        left, right = i + 1, len(nums) - 1
        
        while left < right:
            current_sum = nums[i] + nums[left] + nums[right]
            
            if current_sum < 0:
                left += 1
            elif current_sum > 0:
                right -= 1
            else:
                result.append([nums[i], nums[left], nums[right]])
                
                # Skip duplicates
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                
                left += 1
                right -= 1
    
    return result

# Test
print(three_sum([-1, 0, 1, 2, -1, -4]))  # Output: [[-1, -1, 2], [-1, 0, 1]]
```

---

## How to Use This Repository

### For Interview Preparation:
1. **Start with Common Questions**: Master the basics before moving to advanced topics
2. **Practice Programming Questions**: Code each solution and test with different inputs
3. **Understand Time/Space Complexity**: Analyze the efficiency of each solution
4. **Review Technical Concepts**: Understand internal implementations and memory management

### For Interviewers:
- Use questions progressively based on candidate experience
- Focus on problem-solving approach, not just correct answers
- Ask follow-up questions about optimization and edge cases

### Study Tips:
- Practice coding without IDE initially
- Explain your thought process aloud
- Consider edge cases (empty lists, single elements, duplicates)
- Know multiple approaches for each problem

---

## Contributing

Feel free to contribute additional questions, optimize existing solutions, or suggest improvements. Please ensure:
- Questions are relevant for 5+ years experience level
- Code solutions are tested and efficient
- Explanations are clear and comprehensive

## License

This repository is open source and available under the [MIT License](LICENSE).

---

**Happy Coding! 🐍**