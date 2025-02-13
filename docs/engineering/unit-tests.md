---
title: Unit Testing
parent: Engineering Standards
nav_order: 7
last_modified_date: 2025-01-20 12:00
---

# Unit Testing

Unit testing ensures that individual units of code (functions, methods, or classes) perform as expected. By writing effective unit tests, we can maintain code quality, catch bugs early, and improve overall confidence in the codebase.

---

## Organise Tests

Maintain a clear and consistent structure for your test files. Mirror the source code structure in the `tests/` folder to make it easy to locate corresponding test files:

```plaintext
project_name
├── src
│   ├── __init__.py
│   ├── main.py
│   └── utils.py
└── tests
    ├── __init__.py
    ├── test_main.py
    └── test_utils.py
```

- Each test file should begin with `test_` to ensure they are discoverable by test runners like `pytest`.
- Group tests logically based on functionality or modules.

---

## Use Fixtures

Fixtures provide a way to set up and tear down reusable test data or environments. This reduces code duplication and improves test maintainability. Use `pytest` fixtures for clean, reusable setups:

### Example Fixture:
```python
import pytest

@pytest.fixture
def sample_data():
    return {"key": "value"}

def test_sample_data(sample_data):
    assert sample_data["key"] == "value"
```

### Tips for Fixtures:
- Use `autouse=True` for fixtures that should run automatically for every test.
- Scope fixtures appropriately using `@pytest.fixture(scope="function")` or `scope="module"` for broader use.
- Combine fixtures to manage complex setups.

---

## Types of Tests

1. **Unit Tests**
   - Focus on testing individual functions or methods in isolation.
   - Mock dependencies to ensure tests are independent.

2. **Integration Tests**
   - Verify interactions between multiple components.
   - Ensure that combined functionality works as expected.

3. **End-to-End (E2E)**
   - Test the complete workflow of an application.
   - Typically used for user-facing functionality and requires careful handling of external dependencies.

---

## Best Practices for Unit Testing

### 1. Write Descriptive Test Names
   - Test names should clearly describe what the test is validating.
   - Use the format `test_[functionality]_when_[scenario]_then_[expected_result]`.
     
   **Example:**
   ```python
   def test_add_numbers_when_given_valid_inputs_then_returns_correct_sum():
       result = add_numbers(2, 3)
       assert result == 5
   ```

### 2. Keep Tests Small and Focused
   - Test a single behavior or condition per test.
   - Avoid testing multiple scenarios in one test case.

### 3. Mock External Dependencies
   - Replace external systems or services with mocks to:
     - Isolate the unit being tested.
     - Avoid network calls or database dependencies.
   
   **Example:**
   ```python
   from unittest.mock import Mock

   def test_external_service_call():
       mock_service = Mock(return_value="mocked response")
       result = my_function(mock_service)
       assert result == "mocked response"
   ```

### 4. Use Assertions Effectively
   - Write clear and specific assertions to verify expected behavior.
   - Test edge cases and boundary conditions.

   **Example:**
   ```python
   def test_divide_by_zero():
       with pytest.raises(ZeroDivisionError):
           divide_numbers(1, 0)
   ```

### 5. Automate and Run Tests Frequently
   - Integrate unit tests into Continuous Integration (CI) pipelines.
   - Run tests locally before committing changes.

### 6. Aim for High Test Coverage (But Not at the Expense of Quality)
   - Strive to cover critical paths and edge cases.
   - Avoid writing tests just to increase coverage metrics without meaningful validation.

### 7. Keep Tests Independent
   - Ensure tests do not rely on the state set up by other tests.
   - Use fixtures or setup methods to ensure isolation.

### 8. Maintain and Refactor Tests
   - Update tests whenever the code changes.
   - Remove obsolete or redundant tests to avoid clutter.

### 9. Use Parameterized Tests
   - Test multiple inputs and expected outputs in a single test function.
   
   **Example:**
   ```python
   @pytest.mark.parametrize("input,expected", [
       (2, 4),
       (3, 9),
       (4, 16),
   ])
   def test_square(input, expected):
       assert square(input) == expected
   ```

### 10. Document Tests
   - Add comments or docstrings to explain complex tests.
   - Use consistent naming conventions for test files, classes, and methods.

---

## Tools and Libraries

1. **pytest**
   - A versatile testing framework with support for fixtures, parameterization, and plugins.
   
2. **unittest**
   - A built-in Python library for unit testing with support for test discovery and assertions.

3. **mock**
   - Part of `unittest` for creating mock objects and patching dependencies.

4. **coverage**
   - A tool for measuring code coverage to identify untested code paths.



