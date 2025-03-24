Here is a list of **most commonly asked Python programs** in coding interviews, covering different topics such as **strings, lists, recursion, searching, sorting, data structures, and algorithms**. 🚀  

---

## **1️⃣ Basic Python Programs**  
1️⃣ **Check if a number is even or odd**  
```python
num = int(input("Enter a number: "))
if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

2️⃣ **Check if a number is prime**  
```python
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

num = int(input("Enter a number: "))
print("Prime" if is_prime(num) else "Not Prime")
```

3️⃣ **Find the factorial of a number (Recursion & Iterative)**  
```python
# Recursive approach
def factorial(n):
    return 1 if n == 0 else n * factorial(n - 1)

# Iterative approach
def factorial_iter(n):
    fact = 1
    for i in range(1, n+1):
        fact *= i
    return fact

num = int(input("Enter a number: "))
print("Factorial:", factorial(num))
```

---

## **2️⃣ String Manipulation**
4️⃣ **Reverse a string**  
```python
s = input("Enter a string: ")
print(s[::-1])  # Using slicing
```

5️⃣ **Check if a string is a palindrome**  
```python
def is_palindrome(s):
    return s == s[::-1]

s = input("Enter a string: ")
print("Palindrome" if is_palindrome(s) else "Not Palindrome")
```

6️⃣ **Count occurrences of each character in a string**  
```python
from collections import Counter

s = input("Enter a string: ")
print(Counter(s))
```

7️⃣ **Remove duplicate characters from a string**  
```python
def remove_duplicates(s):
    return "".join(set(s))

s = input("Enter a string: ")
print(remove_duplicates(s))
```

---

## **3️⃣ List & Array Problems**
8️⃣ **Find the largest and smallest element in a list**  
```python
arr = [3, 1, 4, 1, 5, 9]
print("Max:", max(arr))
print("Min:", min(arr))
```

9️⃣ **Reverse a list**  
```python
arr = [1, 2, 3, 4, 5]
print(arr[::-1])  # Using slicing
```

🔟 **Find the second largest element in a list**  
```python
arr = list(set([1, 2, 2, 3, 4, 5]))
arr.sort()
print("Second largest:", arr[-2])
```

---

## **4️⃣ Searching & Sorting**
1️⃣1️⃣ **Binary Search** (Array must be sorted)  
```python
def binary_search(arr, x):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == x:
            return mid
        elif arr[mid] < x:
            left = mid + 1
        else:
            right = mid - 1
    return -1

arr = [1, 3, 5, 7, 9, 11]
x = 7
print("Element found at index:", binary_search(arr, x))
```

1️⃣2️⃣ **Bubble Sort**  
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

arr = [64, 34, 25, 12, 22, 11, 90]
bubble_sort(arr)
print("Sorted list:", arr)
```

1️⃣3️⃣ **Quick Sort**  
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + middle + quick_sort(right)

arr = [3, 6, 8, 10, 1, 2, 1]
print("Sorted list:", quick_sort(arr))
```

---

## **5️⃣ Recursion Problems**
1️⃣4️⃣ **Find Fibonacci numbers (Recursive & Iterative)**  
```python
# Recursive
def fib(n):
    return n if n <= 1 else fib(n-1) + fib(n-2)

# Iterative
def fib_iter(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

print(fib(10))  # Recursive
print(fib_iter(10))  # Iterative
```

---

## **6️⃣ Advanced Problems**
1️⃣5️⃣ **Check if two strings are anagrams**  
```python
from collections import Counter

def is_anagram(s1, s2):
    return Counter(s1) == Counter(s2)

print(is_anagram("listen", "silent"))  # True
```

1️⃣6️⃣ **Find the missing number in an array of size `n-1` (1 to n)**  
```python
def missing_number(arr, n):
    return n * (n + 1) // 2 - sum(arr)

arr = [1, 2, 4, 5, 6]
print("Missing number:", missing_number(arr, 6))
```

1️⃣7️⃣ **Find duplicate elements in a list**  
```python
def find_duplicates(arr):
    return list(set([x for x in arr if arr.count(x) > 1]))

arr = [1, 2, 3, 4, 2, 3, 5]
print(find_duplicates(arr))
```

1️⃣8️⃣ **Find the first non-repeating character in a string**  
```python
def first_non_repeating(s):
    for char in s:
        if s.count(char) == 1:
            return char
    return None

print(first_non_repeating("aabbccdee"))  # d
```

1️⃣9️⃣ **Find the longest word in a sentence**  
```python
sentence = "The quick brown fox jumps over the lazy dog"
longest_word = max(sentence.split(), key=len)
print("Longest word:", longest_word)
```

---

## **7️⃣ Data Structures**
2️⃣0️⃣ **Implement a stack using Python list**  
```python
class Stack:
    def __init__(self):
        self.stack = []
    
    def push(self, item):
        self.stack.append(item)
    
    def pop(self):
        return self.stack.pop() if self.stack else None

s = Stack()
s.push(5)
s.push(10)
print(s.pop())  # 10
```

2️⃣1️⃣ **Implement a queue using collections.deque**  
```python
from collections import deque

q = deque()
q.append(1)
q.append(2)
print(q.popleft())  # 1
```

---

These **21 Python programs** cover a wide range of interview topics. Let me know if you need more! 🚀🔥
