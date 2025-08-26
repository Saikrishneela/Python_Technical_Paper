# 🐍 Python Data Structures: List, Set, Dictionary

---

## 🔹 1. List in Python
### 📌 Definition
- A **list** is an **ordered collection** of elements.  
- It is **mutable** → elements can be added, removed, or changed.  
- Allows **duplicate values**.  
- Elements are accessed using **indexing** (`0` for first element, `-1` for last).  

**Syntax:**
```python
    my_list = [10, 20, 30, "Hello", 5.5]


✅ Properties of List
 - Ordered → Preserves the order of insertion.
 - Mutable → Can change after creation.
 - Duplicates allowed → [1, 1, 2] is valid.
 - Heterogeneous → Can store different data types.
 - Indexing supported → Access via positive & negative indices.

✅ List Methods with Examples

| Method             | Description                                    | Example                       | Output       |
| ------------------ | ---------------------------------------------- | ----------------------------- | ------------ |
| `append(x)`        | Adds element at end                            | `lst=[1,2]; lst.append(3)`    | `[1, 2, 3]`  |
| `insert(i, x)`     | Inserts at index `i`                           | `lst=[1,2]; lst.insert(1,10)` | `[1, 10, 2]` |
| `extend(iterable)` | Adds multiple elements                         | `lst=[1]; lst.extend([2,3])`  | `[1, 2, 3]`  |
| `remove(x)`        | Removes first occurrence of `x`                | `lst=[1,2,2]; lst.remove(2)`  | `[1, 2]`     |
| `pop([i])`         | Removes element at index `i` (last by default) | `lst=[1,2,3]; lst.pop()`      | `[1, 2]`     |
| `clear()`          | Removes all elements                           | `lst=[1,2]; lst.clear()`      | `[]`         |
| `index(x)`         | Returns first index of `x`                     | `lst=[10,20]; lst.index(20)`  | `1`          |
| `count(x)`         | Counts occurrences of `x`                      | `lst=[1,1,2]; lst.count(1)`   | `2`          |
| `sort()`           | Sorts ascending                                | `lst=[3,1,2]; lst.sort()`     | `[1, 2, 3]`  |
| `reverse()`        | Reverses list order                            | `lst=[1,2,3]; lst.reverse()`  | `[3, 2, 1]`  |
| `copy()`           | Returns shallow copy                           | `lst=[1,2]; new=lst.copy()`   | `[1, 2]`     |





🔹 2. Set in Python
📌 Definition

A set is an unordered collection of unique elements.

No duplicates allowed.

It is mutable, but only immutable items (numbers, strings, tuples) can be stored.

Syntax:
my_set = {10, 20, 30}



✅ Properties of Set

Unordered → No fixed order.

Unique elements only → Automatically removes duplicates.

Unindexed → Cannot access elements by position.

Mutable → Elements can be added or removed.

✅ Set Methods with Examples

| Method                        | Description                           | Example                             | Output                 |
| ----------------------------- | ------------------------------------- | ----------------------------------- | ---------------------- |
| `add(x)`                      | Adds single element                   | `s={1,2}; s.add(3)`                 | `{1,2,3}`              |
| `update(iterable)`            | Adds multiple elements                | `s={1}; s.update([2,3])`            | `{1,2,3}`              |
| `remove(x)`                   | Removes element (error if not found)  | `s={1,2}; s.remove(2)`              | `{1}`                  |
| `discard(x)`                  | Removes element safely                | `s={1}; s.discard(5)`               | `{1}`                  |
| `pop()`                       | Removes & returns random element      | `s={1,2,3}; s.pop()`                | Random element removed |
| `clear()`                     | Removes all elements                  | `s={1,2}; s.clear()`                | `set()`                |
| `union(other)`                | Returns union of sets                 | `{1,2}.union({2,3})`                | `{1,2,3}`              |
| `intersection(other)`         | Returns common elements               | `{1,2,3}.intersection({2,3,4})`     | `{2,3}`                |
| `difference(other)`           | Elements in one set but not the other | `{1,2,3}.difference({2})`           | `{1,3}`                |
| `symmetric_difference(other)` | Elements in either but not both       | `{1,2}.symmetric_difference({2,3})` | `{1,3}`                |
| `issubset(other)`             | Checks if subset                      | `{1,2}.issubset({1,2,3})`           | `True`                 |
| `issuperset(other)`           | Checks if superset                    | `{1,2,3}.issuperset({2})`           | `True`                 |
| `copy()`                      | Returns shallow copy                  | `s={1,2}; new=s.copy()`             | `{1,2}`                |



🔹 3. Dictionary in Python
📌 Definition
 - A dictionary is a collection of key-value pairs.
 - Keys must be unique and immutable (string, number, tuple).
 - Values can be duplicated and mutable.
 - Preserves insertion order (Python 3.7+).

Syntax:
   my_dict = {"name": "Alice", "age": 25}


✅ Properties of Dictionary
 - Key-value storage → fast lookup.
 - Keys are unique; values may repeat.
 - Mutable → Can add, update, remove pairs.
 - Ordered → Keeps insertion order.


✅ Dictionary Methods with Examples

| Method                     | Description                          | Example                          | Output                 |
| -------------------------- | ------------------------------------ | -------------------------------- | ---------------------- |
| `get(key, default)`        | Returns value or default             | `d={"a":1}; d.get("a")`          | `1`                    |
| `keys()`                   | Returns all keys                     | `d={"a":1,"b":2}; d.keys()`      | `dict_keys(['a','b'])` |
| `values()`                 | Returns all values                   | `d={"a":1,"b":2}; d.values()`    | `dict_values([1,2])`   |
| `items()`                  | Returns key-value pairs              | `d={"a":1,"b":2}; d.items()`     | `[('a',1), ('b',2)]`   |
| `update(other)`            | Updates dictionary                   | `d={"a":1}; d.update({"b":2})`   | `{'a':1,'b':2}`        |
| `pop(key)`                 | Removes key and returns value        | `d={"a":1}; d.pop("a")`          | `1`                    |
| `popitem()`                | Removes last inserted item           | `d={"a":1,"b":2}; d.popitem()`   | Removes `("b":2)`      |
| `setdefault(key, default)` | Adds key with default if not present | `d={"a":1}; d.setdefault("b",2)` | `{'a':1,'b':2}`        |
| `clear()`                  | Removes all items                    | `d={"a":1}; d.clear()`           | `{}`                   |
| `copy()`                   | Returns shallow copy                 | `d={"a":1}; new=d.copy()`        | `{'a':1}`              |



🔎 Final Comparison Table

| Feature        | List                        | Set                             | Dictionary                       |
| -------------- | --------------------------- | ------------------------------- | -------------------------------- |
| **Definition** | Ordered, mutable collection | Unordered, unique collection    | Key-value pairs                  |
| **Duplicates** | Allowed                     | Not allowed                     | Keys not allowed, values allowed |
| **Access**     | By index                    | By membership (`in`)            | By key                           |
| **Mutable?**   | Yes                         | Yes                             | Yes                              |
| **Order**      | Preserves insertion order   | No order                        | Ordered (3.7+)                   |
| **Syntax**     | `[1,2,3]`                   | `{1,2,3}`                       | `{"a":1, "b":2}`                 |
| **Use Case**   | Sequential/Indexed data     | Unique elements, set operations | Mapping data (key → value)       |


📝 Real-Life Example

# LIST → Store marks (duplicates allowed)
marks = [90, 85, 90, 70]
print("Marks:", marks)   # [90, 85, 90, 70]

# SET → Store unique courses (duplicates removed)
courses = {"Math", "Science", "English", "Math"}
print("Courses:", courses)  # {'English', 'Math', 'Science'}

# DICTIONARY → Store student record
student = {"name": "John", "age": 20, "marks": [90,85,70], "course": "Math"}
print("Student Info:", student)
# {'name': 'John', 'age': 20, 'marks': [90, 85, 70], 'course': 'Math'}
