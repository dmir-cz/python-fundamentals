Python operators are the building blocks of any script, allowing you to perform everything from simple math to complex logic. Think of them as the verbs of the language.

Here is a breakdown of the most common operators you'll encounter.

---

## 1. Arithmetic Operators
These are your standard math tools used with numeric values to perform common mathematical operations.

| Operator | Name | Example | Result |
| :--- | :--- | :--- | :--- |
| `+` | Addition | `5 + 2` | `7` |
| `-` | Subtraction | `5 - 2` | `3` |
| `*` | Multiplication | `5 * 2` | `10` |
| `/` | Division | `5 / 2` | `2.5` |
| `%` | Modulus (Remainder) | `5 % 2` | `1` |
| `**` | Exponentiation | `5 ** 2` | `25` |
| `//` | Floor Division | `5 // 2` | `2` |

> **Note:** Floor division (`//`) rounds the result down to the nearest whole number, while the modulus (`%`) gives you only what is "left over."

---

## 2. Comparison Operators
Comparison operators return a **Boolean** value: either `True` or `False`. They are the "logic gates" for your `if` statements.

* **Equal to:** `==` (e.g., `5 == 5` is `True`)
* **Not equal:** `!=` (e.g., `5 != 3` is `True`)
* **Greater than:** `>`
* **Less than:** `<`
* **Greater than or equal to:** `>=`
* **Less than or equal to:** `<=`

---

## 3. Logical Operators
These are used to combine conditional statements.

* **`and`**: Returns `True` if **both** statements are true.
    * *Example:* `(5 > 3 and 10 > 5)` $\rightarrow$ `True`
* **`or`**: Returns `True` if **at least one** statement is true.
    * *Example:* `(5 > 3 or 5 > 10)` $\rightarrow$ `True`
* **`not`**: Reverses the result (True becomes False).
    * *Example:* `not(5 > 3)` $\rightarrow$ `False`

---

## 4. Assignment Operators
You already know `=`, which assigns a value to a variable. Python also has "augmented" assignment operators that perform a math operation and assignment in one step.

* **`+=`**: Add and assign (`x += 3` is the same as `x = x + 3`)
* **`-=`**: Subtract and assign
* **`*=`**: Multiply and assign
* **`/=`**: Divide and assign

---

In Python, `is` and `==` (the companion to `in` logic) are often confused, but they serve very different purposes. Think of it as the difference between **identity** and **membership**.

Here is a breakdown of how these operators function under the hood.

---

## 5. The `is` Operator (Identity)
The `is` operator checks if two variables point to the **exact same object** in memory. It doesn't care if the values look the same; it only cares about the memory address (the `id`).

* **Comparison:** `a is b` is roughly equivalent to `id(a) == id(b)`.
* **Best Use Case:** Checking if a variable is `None`, `True`, or `False`.

### Example:
```python
list_a = [1, 2, 3]
list_b = [1, 2, 3]
list_c = list_a

print(list_a == list_b) # True (They have the same contents)
print(list_a is list_b) # False (They are different objects in memory)
print(list_a is list_c) # True (They point to the same memory address)
```

> **Note:** Python performs "interning" for small integers (usually -5 to 256) and certain strings to save memory. In those specific cases, `is` might return `True` for two different variables because Python reused the memory slot, but you should never rely on this for logic!

---

## 6. The `in` Operator (Membership)
The `in` operator checks for **membership**. It validates whether a specific value exists within a collection (like a list, string, set, or dictionary).

* **Behind the scenes:** For lists, Python iterates through each item until it finds a match. For sets and dictionaries, it uses a hash table for near-instant lookups.

### Common Uses:
| Type | Behavior |
| :--- | :--- |
| **Strings** | Checks for substrings: `"apple" in "pineapple"` → `True` |
| **Lists/Tuples** | Checks for element equality: `1 in [1, 2, 3]` → `True` |
| **Dictionaries** | Checks **keys** only (by default): `"name" in {"name": "Alice"}` → `True` |
| **Sets** | Extremely fast lookup for unique items. |

---

## Key Differences at a Glance

| Feature | `is` | `in` |
| :--- | :--- | :--- |
| **Purpose** | Identity (Memory address) | Membership (Containment) |
| **Check** | Are these the *same* object? | Is this value *inside* that object? |
| **Common Partner** | `is not` | `not in` |
| **Typical Usage** | `if x is None:` | `if "user" in database:` |

---

### A Quick Warning on Logic
Be careful not to confuse `is` with `==`. 
* `==` checks **Equality** (Do they have the same value?)
* `is` checks **Identity** (Are they the same thing?)

If you are building a house, two houses might be identical in design (`==`), but they are not the same physical house (`is`). The `in` operator simply checks if there is a specific person currently standing inside one of those houses.

**Would you like to see how the performance of `in` differs between a List and a Set?**
 

