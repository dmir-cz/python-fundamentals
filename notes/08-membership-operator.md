In Python, `in` and `not in` are known as **membership operators**. They are used to check whether a specific value exists within a sequence (like a string, list, tuple, or dictionary).

They are incredibly readable—almost like writing a sentence in English—and they always return a **Boolean** value: either `True` or `False`.

---

## 1. The `in` Operator
The `in` operator returns `True` if the value is found inside the sequence.

### Examples:
* **With Lists:**
    ```python
    fruits = ["apple", "banana", "cherry"]
    print("banana" in fruits)  # Output: True
    print("orange" in fruits)  # Output: False
    ```
* **With Strings:**
    ```python
    message = "Hello, world!"
    print("Hello" in message) # Output: True
    print("z" in message)     # Output: False
    ```

---

## 2. The `not in` Operator
The `not in` operator is the exact opposite. It returns `True` if the value is **not** found in the sequence.

### Examples:
* **With Lists:**
    ```python
    users = ["Alice", "Bob", "Charlie"]
    print("Eve" not in users) # Output: True (Because Eve isn't there)
    ```
* **With Numbers:**
    ```python
    numbers = [1, 2, 3, 4, 5]
    print(10 not in numbers)  # Output: True
    ```

---

## 3. How they work with Dictionaries
When you use membership operators with a dictionary, Python checks the **keys**, not the values.

```python
person = {"name": "Leo", "age": 25}

print("name" in person)   # True (It's a key)
print("Leo" in person)    # False (It's a value, not a key)
```

---

## Summary Table

| Operator | Returns `True` if... | Returns `False` if... |
| :--- | :--- | :--- |
| **`in`** | The value exists in the sequence | The value is missing |
| **`not in`** | The value is missing from the sequence | The value exists |

> **Pro-Tip:** Using `in` is much faster and cleaner than writing a manual `for` loop to check if an item exists in a list. It’s one of the things that makes Python "Pythonic."

---
 