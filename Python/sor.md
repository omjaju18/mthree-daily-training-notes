Here is a **detailed explanation** of all major **sorting and searching algorithms** in Python, including their **definitions, complexities, and commented Python implementations**.

---

# 🔹 **Sorting Algorithms**
Sorting algorithms arrange elements in a specific order (ascending/descending). The main sorting algorithms include:

---

## **1. Bubble Sort**
📌 **Definition**: Bubble Sort repeatedly swaps adjacent elements if they are in the wrong order.  
📌 **Time Complexity**:  
   - **Best Case**: O(n) (Already sorted)  
   - **Worst/Average Case**: O(n²)  
📌 **Space Complexity**: O(1)  

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):  # Outer loop for passes
        swapped = False
        for j in range(0, n-i-1):  # Inner loop for comparisons
            if arr[j] > arr[j+1]:  # Swap if elements are in the wrong order
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True
        if not swapped:  # If no swaps, array is sorted
            break
    return arr

# Example usage
arr = [64, 25, 12, 22, 11]
print(bubble_sort(arr))  # Output: [11, 12, 22, 25, 64]
```

---

## **2. Selection Sort**
📌 **Definition**: Finds the minimum element and places it in its correct position.  
📌 **Time Complexity**: O(n²)  
📌 **Space Complexity**: O(1)  

```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i  # Assume current index has the smallest value
        for j in range(i+1, n):
            if arr[j] < arr[min_idx]:  # Find minimum in the remaining array
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]  # Swap with the correct position
    return arr

# Example usage
arr = [64, 25, 12, 22, 11]
print(selection_sort(arr))  # Output: [11, 12, 22, 25, 64]
```

---

## **3. Insertion Sort**
📌 **Definition**: Builds the sorted array one element at a time by placing it in its correct position.  
📌 **Time Complexity**:  
   - **Best Case**: O(n)  
   - **Worst/Average Case**: O(n²)  
📌 **Space Complexity**: O(1)  

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):  # Start from the second element
        key = arr[i]  # Element to be inserted
        j = i - 1
        while j >= 0 and arr[j] > key:  # Shift elements to the right
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key  # Insert the key at the right position
    return arr

# Example usage
arr = [64, 25, 12, 22, 11]
print(insertion_sort(arr))  # Output: [11, 12, 22, 25, 64]
```

---

## **4. Merge Sort (Divide & Conquer)**
📌 **Definition**: Recursively divides the array into two halves, sorts them, and merges the sorted halves.  
📌 **Time Complexity**: O(n log n)  
📌 **Space Complexity**: O(n)  

```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2  # Find the middle of the array
        left_half = arr[:mid]
        right_half = arr[mid:]

        merge_sort(left_half)  # Recursively sort the left half
        merge_sort(right_half)  # Recursively sort the right half

        i = j = k = 0
        while i < len(left_half) and j < len(right_half):  # Merge sorted halves
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        while i < len(left_half):  # Add remaining elements from left
            arr[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):  # Add remaining elements from right
            arr[k] = right_half[j]
            j += 1
            k += 1
    return arr

# Example usage
arr = [64, 25, 12, 22, 11]
print(merge_sort(arr))  # Output: [11, 12, 22, 25, 64]
```

---

## **5. Quick Sort (Divide & Conquer)**
📌 **Definition**: Picks a pivot, partitions the array, and sorts recursively.  
📌 **Time Complexity**:  
   - **Best/Average Case**: O(n log n)  
   - **Worst Case (when pivot is smallest/largest)**: O(n²)  
📌 **Space Complexity**: O(log n)  

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]  # Choose the middle element as pivot
    left = [x for x in arr if x < pivot]  # Elements less than pivot
    middle = [x for x in arr if x == pivot]  # Pivot element(s)
    right = [x for x in arr if x > pivot]  # Elements greater than pivot
    return quick_sort(left) + middle + quick_sort(right)

# Example usage
arr = [64, 25, 12, 22, 11]
print(quick_sort(arr))  # Output: [11, 12, 22, 25, 64]
```

---

# 🔹 **Searching Algorithms**
Searching algorithms are used to find an element in an array.

---

## **1. Linear Search**
📌 **Definition**: Checks each element one by one.  
📌 **Time Complexity**: O(n)  
📌 **Space Complexity**: O(1)  

```python
def linear_search(arr, target):
    for i in range(len(arr)):  # Loop through each element
        if arr[i] == target:  # Check if the element matches the target
            return i  # Return index if found
    return -1  # Return -1 if not found

# Example usage
arr = [10, 20, 30, 40]
print(linear_search(arr, 30))  # Output: 2
```

---

## **2. Binary Search (Only for Sorted Arrays)**
📌 **Definition**: Divides the array into two halves and searches in the appropriate half.  
📌 **Time Complexity**: O(log n)  
📌 **Space Complexity**: O(1)  

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid  # Element found
        elif arr[mid] < target:
            left = mid + 1  # Search in the right half
        else:
            right = mid - 1  # Search in the left half
    return -1  # Element not found

# Example usage
arr = [10, 20, 30, 40, 50]
print(binary_search(arr, 30))  # Output: 2
```

---

These are the most **commonly asked sorting and searching algorithms** in interviews. Let me know if you need **more practice questions or variations**! 🚀
