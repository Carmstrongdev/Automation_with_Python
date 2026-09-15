#  Update a File Through a Python Algorithm

##  Project Overview

In this project, I used **Python to automate the process of removing unauthorized IP addresses from an allow list**.

My organization uses an allow list to control which IP addresses are allowed to access restricted content. The approved IP addresses are stored in an `allow_list.txt` file, while a separate `remove_list` contains IP addresses that should no longer have access.

I created a Python algorithm that:

1. Opens the `allow_list.txt` file
2. Reads the IP addresses
3. Converts the data into a list
4. Iterates through the `remove_list`
5. Removes matching IP addresses
6. Converts the updated list back into a string
7. Writes the updated list back to `allow_list.txt`

This allowed me to automate a task that would otherwise require manually editing the allow list.

---

#  Python Algorithm

The overall process looks like this:

```text
allow_list.txt
      │
      ▼
Read File Contents
      │
      ▼
Convert String → List
      │
      ▼
Compare Against remove_list
      │
      ▼
Remove Matching IP Addresses
      │
      ▼
Convert List → String
      │
      ▼
Write Updated List
      │
      ▼
allow_list.txt
```

---

# 1️ Open the Allow List File

The first step was to open the `allow_list.txt` file so I could access the IP addresses stored inside it.

I assigned the filename to the `import_file` variable:

```python
import_file = "allow_list.txt"
```

I then used a `with` statement to open the file in **read mode**:

```python
with open(import_file, "r") as file:
```

The `open()` function takes two main arguments:

* `import_file` — Specifies the file I want to open.
* `"r"` — Opens the file in **read mode**.

I used the `as` keyword to assign the opened file to the `file` variable.

The `with` statement also manages the file resource automatically and closes the file when the code block is finished.

---


# 2️ Read the File Contents

After opening the file, I needed to read its contents.

I used the `.read()` method:

```python
ip_addresses = file.read()
```

The `.read()` method reads the contents of the file and returns them as a **string**.

I stored the resulting string in the `ip_addresses` variable.

At this point, all of the IP addresses were stored together as a single string.

For example:

```text
192.168.1.10
192.168.1.15
192.168.1.20
```

The `.read()` method allowed me to access the information so I could manipulate it later in the algorithm.

---

# 3️ Convert the String Into a List

To remove individual IP addresses, I needed to convert the string into a list.

I used the `.split()` method:

```python
ip_addresses = ip_addresses.split()
```

The `.split()` method separates a string into individual elements and stores them in a list.

Because the IP addresses in the file are separated by whitespace, `.split()` separates each IP address into its own list element.

For example:

```python
ip_addresses = [
    "192.168.1.10",
    "192.168.1.15",
    "192.168.1.20"
]
```

Converting the data into a list makes it easier to work with and remove individual IP addresses.

---

# 4️ Iterate Through the Remove List

Next, I needed to check the IP addresses contained in `remove_list`.

I used a **`for` loop**:

```python
for element in remove_list:
```

The `for` loop allows Python to process each IP address in `remove_list` one at a time.

During each iteration, the current IP address is stored in the `element` variable.

For example:

```python
remove_list = [
    "192.168.1.15",
    "192.168.1.30"
]
```

Python processes each IP address individually and checks whether it needs to be removed from the allow list.

---

# 5️ Remove IP Addresses From the Allow List

I then needed to remove any IP address from `ip_addresses` that was also found in `remove_list`.

I used a conditional statement to check whether the IP address existed in the allow list:

```python
if element in ip_addresses:
    ip_addresses.remove(element)
```

The conditional check is important because calling `.remove()` on an item that does not exist in the list would result in an error.

The algorithm works by:

1. Checking whether the IP address exists in `ip_addresses`.
2. If it exists, `.remove()` removes it.
3. If it does not exist, Python moves on to the next IP address.

This allows the algorithm to automatically remove IP addresses that should no longer have access.

---

# 6️ Convert the Updated List Back Into a String

After removing the unauthorized IP addresses, I needed to convert the list back into a string before writing it back to the file.

I used the `.join()` method:

```python
ip_addresses = "\n".join(ip_addresses)
```

The `.join()` method combines the elements of an iterable into a single string.

I used:

```python
"\n"
```

as the separator.

The `\n` represents a **new line**, which keeps each IP address on its own line in the updated file.

For example, this list:

```python
[
    "192.168.1.10",
    "192.168.1.20",
    "192.168.1.25"
]
```

becomes:

```text
192.168.1.10
192.168.1.20
192.168.1.25
```

This puts the data back into the format used by `allow_list.txt`.

---

# 7️ Write the Updated List Back to the File

The final step was to update `allow_list.txt` with the revised list of IP addresses.

I opened the file again, this time using **write mode**:

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```
he `"w"` argument tells Python to open the file in **write mode**.

I then used the `.write()` method to replace the existing contents of the file with the updated `ip_addresses` string.

The final result is an updated allow list that no longer contains the IP addresses identified in `remove_list`.

---

# Complete Algorithm

The complete Python logic looks like this:

```python
import_file = "allow_list.txt"

with open(import_file, "r") as file:
    ip_addresses = file.read()

ip_addresses = ip_addresses.split()

for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)

ip_addresses = "\n".join(ip_addresses)

with open(import_file, "w") as file:
    file.write(ip_addresses)
```

---

# Python Concepts Used

| Python Concept | Purpose |
|---|---|
| `open()` | Opens a file for reading or writing |
| `with` | Manages the file resource and automatically closes it |
| `.read()` | Reads file contents into a string |
| `.split()` | Converts a string into a list |
| `for` loop | Iterates through each IP address in `remove_list` |
| `if` statement | Checks whether an IP address exists in the allow list |
| `in` | Checks whether an element exists in a list |
| `.remove()` | Removes an IP address from the list |
| `.join()` | Converts the list back into a string |
| `.write()` | Writes the updated data back to the file |

---

# Security Application

This project demonstrates how Python can be used to **automate security-related tasks**.

Instead of manually searching through an allow list and removing unauthorized IP addresses, the algorithm processes the list automatically.

This type of automation can help:

- Reduce manual work
- Make access-list updates more consistent
- Remove unauthorized IP addresses efficiently
- Reduce the possibility of human error
- Support routine security maintenance

---

# Summary

In this project, I created a Python algorithm that automatically updates an IP allow list.

I started by opening `allow_list.txt` and reading its contents into a string. I then converted that string into a list so individual IP addresses could be accessed and removed.

Next, I used a `for` loop to go through the IP addresses in `remove_list`. For each address, I checked whether it existed in the allow list. If it did, I removed it using the `.remove()` method.

Finally, I converted the updated list back into a string using `.join()` and used `.write()` to replace the contents of `allow_list.txt`.

This project gave me practical experience using **Python file handling, lists, loops, conditionals, string manipulation, and automation to solve a security-related problem**.

---

## Skills Demonstrated

**Python · File Handling · Automation · List Manipulation · Loops · Conditional Statements · String Manipulation · Access Control · Security Automation**
