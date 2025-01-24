---
title: Coding Standards
parent: Engineering Standards
nav_oder: 1
last_modified_date: 2025-01-20 12:00
---
# Coding Standards
This document defines the Mediahub coding standards for Python development. Following these guidelines ensures readable, maintainable, and scalable code.

---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## General Thoughts

- Keep code simple, readable, and focused.
- Follow the principle of "One Function, One Purpose."
- Ensure functions perform a single responsibility effectively.
- Check for black reformatting (each repository should specify the black version used).

---

## Function Naming and Purpose

Each function should perform a single, well-defined task. Avoid combining unrelated operations within the same function.

### Guidelines

**DO:**

```python
def post_comment(self):
    if self.success:
        comment = 'Build succeeded'
    elif self.warning:
        comment = 'Build had issues'
    elif self.failed:
        comment = 'Build failed'

    if self.success:
        self.post(comment, type='success')
    else:
        self.post(comment, type='error')
```

**DON’T:**

```python
def get_comment(self):
    comments = {
        'success': 'Build succeeded',
        'warning': 'Build had issues',
        'failed': 'Build failed'
    }
    return comments[self.type]

def post_comment(self, comment):
    self.post(comment, type=self.type)
```

---

## Docstrings - Sphinx Style

Use the Sphinx style for docstrings to standardize documentation and make it easier to generate documentation.

- Begin each docstring with a one-line summary.
- Use `:param` and `:return` directives to describe parameters and return values.
- Include examples and explanations where applicable.
- With type hints, avoid duplicating type definitions with `:type:` or `:rtype:`.

### Guidelines

**DO:**

```python
def str_to_list(string: str) -> list[str]:
    """
    Converts a comma-separated string into a list.

    :param string: The input string containing comma-separated values.
    :return: A list of values extracted from the input string.
    """
    return [x.strip() for x in string.split(",")]
```

**DON’T:**

```python
def str_to_list(string):
    """
    Converts a comma-separated string into a list.

    :param string: The input string containing comma-separated values.
    :return: A list of values extracted from the input string.
    """
    return [x.strip() for x in string.split(",")]
```

---

## Type Hints

Type hints improve readability and provide hints for better error checking. Every function should include type hints for both parameters and return types.

### Dataclass

The `dataclasses` module allows you to define classes with minimal boilerplate, ideal for representing data objects with attributes.

#### General Guidelines

- **Simple Data Storage:** Use dataclasses for classes that primarily store data without complex behavior.
- **Readability and Consistency:** They make the code more readable, especially when the class has many attributes.
- **Immutability:** With the `frozen=True` argument, dataclasses can create immutable instances, ensuring data consistency.

#### Example

```python
from dataclasses import dataclass
from typing import Optional, List

@dataclass
class User:
    username: str
    email: str
    age: Optional[int] = None
    roles: List[str] = None
```

### TypedDict

TypedDict allows you to create dictionaries with a specific structure and type requirements for each key.

#### General Guidelines

- **Structured Dictionaries:** Use TypedDict for JSON-like data structures or configurations.
- **Type Safety:** Enforcing a structure on dictionaries helps catch errors during development and provides better autocompletion.

```python
from typing import TypedDict, Optional

class UserProfile(TypedDict):
    username: str
    email: str
    age: Optional[int]
```

---

## PEP 8 Formatting

Follow [PEP 8](https://www.python.org/dev/peps/pep-0008/) guidelines for code formatting. Some key points include:

- Use 4 spaces for indentation (never tabs).
- Keep lines to a maximum of 79 characters.
- Use blank lines to separate functions and classes.
- Use black reformatting to ensure consistency.

### Imports

Imports should be structured, minimal, and grouped logically.

#### General Guidelines

- Structure imports into three sections: standard library, third-party libraries, and local application-specific imports.
- Use explicit imports to clarify dependencies and avoid conflicts.
- Avoid wildcard imports (e.g., `from module import *`).

#### Import Order

1. **Standard Library Imports:** Built-in modules, such as `os`, `sys`, `datetime`.
2. **Third-Party Library Imports:** External libraries, such as `requests`, `numpy`.
3. **Local Application Imports:** Project-specific imports.

**DO:**

```python
# Standard library imports
import os
import sys

# Third-party library imports
import numpy as np

# Local application imports
from myproject.module import my_function
```

**DON’T:**

```python
import numpy as np
from myproject.module import my_function
import os
```


---

## Exceptions

Handling exceptions properly is crucial for building resilient and maintainable code.


### General Guidelines
- **Use specific exception types**: Catch specific exceptions rather than using a blanket `except Exception` wherever possible. This ensures only relevant errors are caught and prevents unintended side effects.
- **Avoid silent exceptions**: Always log or handle exceptions meaningfully instead of suppressing them, which can obscure bugs and make debugging difficult.
- **Use custom exception classes** for application-specific errors. This makes handling and debugging errors within your domain easier.
- **Clean up with `finally`**: Use `finally` for clean-up actions that should occur regardless of success or failure, such as closing files or network connections.
- **Maintain context when re-raising exceptions**: Use `raise ... from` to retain the original traceback for easier debugging.

---

### Using Specific Exceptions

Avoid catching generic `Exception` classes when more specific exceptions can be handled. This leads to more predictable error handling and debugging.

**DO:**

```python
key_name = "Key"
try:
    key_vals = my_dict[key_name]
except KeyError as e:
    raise KeyError(f"{key_name} not found.") from e
```

**DON'T:**

```python
key_name = "Key"
try:
    key_vals = my_dict[key_name]
except:
    pass
```

---

### Create Your Own Exceptions

Custom exceptions are helpful for representing domain-specific errors.

**DO:**

```python
class ModelNotExistsError(Exception):
    pass

if model is None:
    raise ModelNotExistsError("Model not found.")
```

**DON'T:**

```python
if model is None:
    raise ValueError("Model not found.")
```

---

### Avoiding Silent Failures

Never use `pass` in `except` blocks. Always log or handle exceptions to prevent critical issues from being ignored.

**DO:**

```python
for item, category in item_dict.items():
    try:
        update_item(item, category)
    except KeyError:
        logging.error(f"Category {category} not found for item {item}. Please add the category first.")
```

**DON'T:**

```python
for item, category in item_dict.items():
    try:
        update_item(item, category)
    except KeyError:
        pass
```

---

### Using `finally` for Clean-up

Use `finally` to ensure resource cleanup occurs regardless of whether exceptions are raised.

**DO:**

```python
try:
    connection = open_database_connection()
    process_data(connection)
except DatabaseError as e:
    logging.error("Database error occurred.")
    raise
finally:
    connection.close()
```

**DON'T:**

```python
try:
    connection = open_database_connection()
    process_data(connection)
except DatabaseError:
    pass
```

---

### Raising Exceptions with Context

When raising a new exception or re-raising an existing one, retain the original context using `raise ... from`.

**DO:**

```python
def parse_number(value: str) -> int:
    try:
        return int(value)
    except ValueError as e:
        raise ValueError("Invalid integer format") from e
```

**DON'T:**

```python
def parse_number(value: str) -> int:
    try:
        return int(value)
    except ValueError:
        raise ValueError("Invalid integer format")  # Context is lost
```

---

## Additional Topics

### Collaborate on the Same Branch

When collaborating on the same branch, it is recommended to rebase before pushing changes. This avoids overwriting others' work and simplifies conflict resolution.

#### Workflow Example

```bash
git commit -am "Make some changes"
git pull --rebase
git push origin enhancement/branch-name
```
