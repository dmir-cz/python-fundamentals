
## 1. Numeric Types

### **Boolean (`bool`)**
* **Values:** `True` or `False`.
* **Subtype of Integer:** In Python, `bool` is actually a subclass of `int`. `True` behaves like `1` and `False` behaves like `0` in arithmetic operations.
* **Truthiness:** Almost any object can be evaluated in a boolean context. Generally, empty sequences (strings, lists) and the number `0` are `False`; everything else is `True`.

### **Integers (`int`)**
* **Arbitrary Precision:** Unlike many other languages, Python integers have no "overflow." They can be as large as your computer’s memory allows.
* **Readability:** As you noted, underscores (e.g., `1_000_000`) are ignored by the interpreter but help humans read large numbers.
* **Bases:** You can represent integers in other bases:
    * Binary: `0b10` (2)
    * Hexadecimal: `0x10` (16)

### **Floating Point (`float`)**
* **Representation:** Implemented using `double` in C (64-bit). 
* **The Precision Issue:** Computers represent floats in binary, which cannot exactly represent certain decimal fractions (like $0.1$). This is why `0.1 + 0.1 + 0.1 != 0.3`.
* **Comparison:** Never compare floats using `==`. Use an "epsilon" (a tiny margin of error) as you did in your notes, or use `math.isclose()`:
    ```python
    import math
    math.isclose(0.1 + 0.1 + 0.1, 0.3)  # Returns True
    ```

### **Decimal (`decimal.Decimal`)**
* **Purpose:** Used when absolute precision is required (e.g., financial applications).
* **Usage:** Must be imported from the `decimal` module. It is slower than `float` but avoids the binary approximation errors.

### **Complex (`complex`)**
* **Format:** Written as `real + imag j` (e.g., `3 + 5j`).
* **Use Case:** Scientific computing and engineering.

---

## 2. Sequence Types

| Type | Name | Mutable? | Description |
| :--- | :--- | :--- | :--- |
| **String** | `str` | No | Unicode text. Defined by `' '`, `" "`, or `""" """`. |
| **List** | `list` | **Yes** | Ordered collection of items (can be mixed types). |
| **Tuple** | `tuple` | No | Like a list, but cannot be changed after creation. Often used for fixed data. |

---

## 3. Mapping and Set Types

### **Dictionary (`dict`)**
* Stores data in **key-value pairs**.
* Keys must be "hashable" (immutable types like strings, ints, or tuples).
* As of Python 3.7+, dictionaries maintain insertion order.

### **Sets (`set`)**
* Unordered collections of **unique** elements.
* Great for removing duplicates from a list or performing mathematical operations like unions and intersections.

---

## 4. The None Type

### **NoneType (`None`)**
* Represents the absence of a value. 
* Commonly used as a default return value for functions that don't explicitly return anything.
* **Pro-tip:** Always check for None using `is None` rather than `== None`.

---
