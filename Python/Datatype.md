# Python Data Types: String, List, Tuple, Set, and Dictionary

## Introduction
Python provides five main built-in data types used to store collections of data:
- **String (`str`)**: Immutable sequence of characters.
- **List (`list`)**: Ordered, mutable sequence of elements.
- **Tuple (`tuple`)**: Ordered, immutable sequence of elements.
- **Set (`set`)**: Unordered, mutable collection of unique elements.
- **Dictionary (`dict`)**: Collection of key-value pairs.

---

## 1. String (`str`)
### Definition
A **string** is an **immutable sequence** of characters enclosed in **single (`'`), double (`"`), or triple (`''' """`) quotes**.

### Example
```python
s = "Hello, World!"
```

### Accessing Elements in a String
#### Using Indexing
```python
s = "Python"
print(s[0])   # Output: P
print(s[-1])  # Output: n (Negative Indexing)
```

#### Using Slicing
```python
s = "Python"
print(s[0:4])   # Output: Pyth
print(s[:4])    # Output: Pyth (Same as above)
print(s[2:])    # Output: thon
print(s[::2])   # Output: Pto (Step of 2)
```

### String Methods
| Method | Description | Example |
|--------|------------|---------|
| `upper()` | Converts to uppercase | `"hello".upper()` → `"HELLO"` |
| `lower()` | Converts to lowercase | `"HELLO".lower()` → `"hello"` |
| `title()` | Title case | `"hello world".title()` → `"Hello World"` |
| `strip()` | Removes whitespace | `" hello ".strip()` → `"hello"` |
| `replace(old, new)` | Replaces substring | `"hello".replace("h", "H")` → `"Hello"` |
| `split(sep)` | Splits string into a list | `"a,b,c".split(",")` → `['a', 'b', 'c']` |
| `join(iterable)` | Joins list items into a string | `"-".join(['a', 'b', 'c'])` → `"a-b-c"` |

---

## 2. List (`list`)
### Definition
A **list** is an **ordered, mutable** sequence of elements that can hold different data types.

### Example
```python
my_list = [10, 20, 30, "hello", 5.5]
```

### Accessing Elements in a List
#### Using Indexing
```python
print(my_list[0])   # Output: 10
print(my_list[-1])  # Output: 5.5
```

#### Using Slicing
```python
print(my_list[1:4])   # Output: [20, 30, "hello"]
print(my_list[::-1])  # Output: [5.5, "hello", 30, 20, 10] (Reversing a List)
```

### List Methods
| Method | Description | Example |
|--------|------------|---------|
| `append(item)` | Adds item to end | `lst.append(100)` |
| `extend(iterable)` | Extends list | `lst.extend([200, 300])` |
| `insert(index, item)` | Inserts item | `lst.insert(1, 50)` |
| `remove(item)` | Removes first occurrence | `lst.remove(30)` |
| `pop(index)` | Removes & returns item | `lst.pop(2)` |
| `sort()` | Sorts list | `lst.sort()` |
| `reverse()` | Reverses list | `lst.reverse()` |
| `clear()` | Removes all items | `lst.clear()` |

---

## 3. Tuple (`tuple`)
### Definition
A **tuple** is an **ordered, immutable** sequence of elements.

### Example
```python
my_tuple = (1, 2, 3, "hello", 5.5)
```

### Accessing Elements in a Tuple
#### Using Indexing
```python
print(my_tuple[0])   # Output: 1
print(my_tuple[-1])  # Output: 5.5
```

### Tuple Methods
| Method | Description | Example |
|--------|------------|---------|
| `count(item)` | Counts occurrences | `t.count(2)` |
| `index(item)` | Returns index | `t.index(3)` |

---

## 4. Set (`set`)
### Definition
A **set** is an **unordered, mutable** collection of **unique** elements.

### Example
```python
my_set = {1, 2, 3, 4, 5}
```

### Set Methods
| Method | Description | Example |
|--------|------------|---------|
| `add(item)` | Adds item | `s.add(6)` |
| `remove(item)` | Removes item (Error if missing) | `s.remove(3)` |
| `discard(item)` | Removes item (No error) | `s.discard(3)` |
| `pop()` | Removes random item | `s.pop()` |
| `union(set2)` | Combines sets | `s1.union(s2)` |
| `intersection(set2)` | Common elements | `s1.intersection(s2)` |
| `difference(set2)` | Difference | `s1.difference(s2)` |

---

## 5. Dictionary (`dict`)
### Definition
A **dictionary** is a **mutable** collection of key-value pairs.

### Example
```python
my_dict = {"name": "Alice", "age": 25, "city": "New York"}
```

### Dictionary Methods
| Method | Description | Example |
|--------|------------|---------|
| `keys()` | Returns all keys | `d.keys()` |
| `values()` | Returns all values | `d.values()` |
| `items()` | Returns key-value pairs | `d.items()` |
| `get(key, default)` | Gets value, returns default if missing | `d.get("name")` |
| `update(dict2)` | Updates dictionary | `d.update({"age": 30})` |
| `pop(key)` | Removes & returns value | `d.pop("city")` |
| `clear()` | Removes all items | `d.clear()` |

---

## Conclusion
Each data type in Python has **unique properties**:
✔ **Strings** → Immutable, used for text  
✔ **Lists** → Mutable, ordered collection  
✔ **Tuples** → Immutable, ordered collection  
✔ **Sets** → Mutable, unordered, unique elements  
✔ **Dictionaries** → Mutable, key-value pairs  

Let me know if you need further details! 🚀

