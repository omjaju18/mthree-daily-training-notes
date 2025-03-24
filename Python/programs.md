Here is a **simplified** version of all the Python programs along with **explanations in comments** to help you understand easily. 🚀  

---

## **1️⃣ Basic Python Programs**  

### **1️⃣ Check if a number is even or odd**
```python
num = int(input("Enter a number: "))  # Take user input
if num % 2 == 0:  # Check if divisible by 2
    print("Even")
else:
    print("Odd")
```

---

### **2️⃣ Check if a number is prime**
```python
num = int(input("Enter a number: "))  

if num < 2:
    print("Not Prime")  # Numbers less than 2 are not prime
else:
    is_prime = True  
    for i in range(2, int(num ** 0.5) + 1):  # Check divisibility
        if num % i == 0:
            is_prime = False
            break
    print("Prime" if is_prime else "Not Prime")  # Print result
```

---

### **3️⃣ Find factorial (Recursion & Iterative)**
```python
# Iterative approach
num = int(input("Enter a number: "))  
fact = 1

for i in range(1, num + 1):  # Multiply numbers from 1 to num
    fact *= i

print("Factorial:", fact)
```

---

### **4️⃣ Reverse a string**
```python
s = input("Enter a string: ")  # Take input string
print(s[::-1])  # Reverse using slicing
```

---

### **5️⃣ Check if a string is a palindrome**
```python
s = input("Enter a string: ")  
print("Palindrome" if s == s[::-1] else "Not Palindrome")  # Compare reverse
```

---

## **2️⃣ List & Array Problems**  

### **6️⃣ Find the largest and smallest element in a list**
```python
arr = [3, 1, 4, 1, 5, 9]  
print("Max:", max(arr))  # Get max element
print("Min:", min(arr))  # Get min element
```

---

### **7️⃣ Reverse a list**
```python
arr = [1, 2, 3, 4, 5]  
print(arr[::-1])  # Reverse using slicing
```

---

### **8️⃣ Find the second largest number**
```python
arr = list(set([1, 2, 2, 3, 4, 5]))  # Remove duplicates
arr.sort()  # Sort list
print("Second largest:", arr[-2])  # Get second last element
```

---

## **3️⃣ Searching & Sorting**  

### **9️⃣ Binary Search**
```python
def binary_search(arr, x):
    left, right = 0, len(arr) - 1  
    while left <= right:
        mid = (left + right) // 2  
        if arr[mid] == x:
            return mid  # Element found
        elif arr[mid] < x:
            left = mid + 1  
        else:
            right = mid - 1  
    return -1  # Element not found

arr = [1, 3, 5, 7, 9, 11]  
print("Element found at index:", binary_search(arr, 7))
```

---

### **🔟 Bubble Sort**
```python
arr = [64, 34, 25, 12, 22, 11, 90]  

for i in range(len(arr)):  
    for j in range(0, len(arr) - i - 1):  
        if arr[j] > arr[j+1]:  
            arr[j], arr[j+1] = arr[j+1], arr[j]  # Swap elements

print("Sorted list:", arr)
```

---

### **1️⃣1️⃣ Quick Sort**
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr  # Base case
    pivot = arr[len(arr) // 2]  
    left = [x for x in arr if x < pivot]  
    middle = [x for x in arr if x == pivot]  
    right = [x for x in arr if x > pivot]  
    return quick_sort(left) + middle + quick_sort(right)  

arr = [3, 6, 8, 10, 1, 2, 1]  
print("Sorted list:", quick_sort(arr))
```

---

## **4️⃣ Recursion Problems**  

### **1️⃣2️⃣ Find Fibonacci numbers**
```python
def fib(n):
    if n <= 1:
        return n  
    return fib(n-1) + fib(n-2)  # Recursive call

print(fib(10))  # Find 10th Fibonacci number
```

---

## **5️⃣ Advanced Problems**  

### **1️⃣3️⃣ Check if two strings are anagrams**
```python
from collections import Counter  

def is_anagram(s1, s2):
    return Counter(s1) == Counter(s2)  # Compare character counts

print(is_anagram("listen", "silent"))  # True
```

---

### **1️⃣4️⃣ Find the missing number in an array (1 to n)**
```python
def missing_number(arr, n):
    return n * (n + 1) // 2 - sum(arr)  # Sum formula approach

arr = [1, 2, 4, 5, 6]  
print("Missing number:", missing_number(arr, 6))
```

---

### **1️⃣5️⃣ Find duplicate elements in a list**
```python
def find_duplicates(arr):
    return list(set([x for x in arr if arr.count(x) > 1]))  # Find duplicates

arr = [1, 2, 3, 4, 2, 3, 5]  
print(find_duplicates(arr))
```

---

### **1️⃣6️⃣ Find the first non-repeating character in a string**
```python
def first_non_repeating(s):
    for char in s:
        if s.count(char) == 1:
            return char  
    return None  

print(first_non_repeating("aabbccdee"))  # d
```

---

### **1️⃣7️⃣ Find the longest word in a sentence**
```python
sentence = "The quick brown fox jumps over the lazy dog"  
longest_word = max(sentence.split(), key=len)  # Find longest word
print("Longest word:", longest_word)
```

---

## **6️⃣ Data Structures**  

### **1️⃣8️⃣ Implement a stack using list**
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

---

### **1️⃣9️⃣ Implement a queue using collections.deque**
```python
from collections import deque  

q = deque()  
q.append(1)  
q.append(2)  
print(q.popleft())  # 1
```

---

### **2️⃣0️⃣ Implement Linked List**
```python
class Node:
    def __init__(self, data):
        self.data = data  
        self.next = None  

class LinkedList:
    def __init__(self):
        self.head = None  

    def insert(self, data):
        new_node = Node(data)  
        new_node.next = self.head  
        self.head = new_node  

    def display(self):
        temp = self.head  
        while temp:
            print(temp.data, end=" -> ")  
            temp = temp.next  
        print("None")

ll = LinkedList()  
ll.insert(10)  
ll.insert(20)  
ll.insert(30)  
ll.display()  # 30 -> 20 -> 10 -> None
```

---

These are **simple & beginner-friendly solutions** with **comments** to help you understand. Let me know if you need more! 🚀🔥
