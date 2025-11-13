# Tutorial: `utils.py` - Your Programming Toolkit

Welcome to your first step in building the 3D reconstruction pipeline! The `utils.py` file is like a toolbox for our project. Just as a carpenter has a toolbox with hammers and screwdrivers, we have a file with reusable helper functions. We put simple, common tasks in here so we don't have to write the same code over and over again in different parts of our project.

Let's go through it line by line.

---

### The `import` Statements

```python
import json
import os
```

-   **`import json`**: This line brings in Python's built-in `json` library. JSON is a standard format for storing and exchanging data. It's human-readable and easy for computers to understand. We'll use it to save our object detection results. Think of it as importing the knowledge of how to read and write in the JSON language.

-   **`import os`**: This line imports the `os` library, which provides a way of using operating system dependent functionality. We use it to interact with the computer's file system, for things like creating directories or checking if a file exists. It's our tool for managing files and folders.

---

### The `read_json` Function

```python
def read_json(file_path):
    """Reads a JSON file and returns the data."""
    with open(file_path, 'r') as f:
        data = json.load(f)
    return data
```

-   **`def read_json(file_path):`**: This defines a function named `read_json`. A function is a reusable block of code that performs a specific task. This one takes one argument (or input), `file_path`, which is the location of the JSON file we want to read.

-   **`"""Reads a JSON file and returns the data."""`**: This is a "docstring". It's a comment that explains what the function does. It's a good practice to include these to make your code easier to understand for yourself and others.

-   **`with open(file_path, 'r') as f:`**: This is the standard and safest way to open a file in Python.
    -   `open(file_path, 'r')`: The `open()` function opens a file. The first argument is the path to the file, and the second argument, `'r'`, means we are opening it in "read mode".
    -   `with ... as f:`: The `with` statement ensures that the file is automatically closed after we are done with it, even if errors occur. We give the opened file a temporary name, `f`.

-   **`data = json.load(f)`**: This is where the magic happens. The `json.load()` function reads the content of the file `f` and converts the JSON data into a Python data structure (like a list or a dictionary). We store this data in a variable called `data`.

-   **`return data`**: The `return` statement sends the `data` we just read back as the output of the function.

---

### The `ensure_dir` Function

```python
def ensure_dir(dir_path):
    """Creates a directory if it does not exist."""
    if not os.path.exists(dir_path):
        os.makedirs(dir_path)
```

-   **`def ensure_dir(dir_path):`**: This defines a function named `ensure_dir` that takes one argument, `dir_path`, which is the path of the directory we want to make sure exists.

-   **`"""Creates a directory if it does not exist."""`**: The docstring explaining the function's purpose.

-   **`if not os.path.exists(dir_path):`**: This line checks if the directory already exists.
    -   `os.path.exists(dir_path)`: This function from the `os` library returns `True` if a file or directory exists at the given path, and `False` otherwise.
    -   `if not ...`: The `not` keyword inverts the result. So, the code inside the `if` block will only run if the directory *does not* exist.

-   **`os.makedirs(dir_path)`**: If the directory doesn't exist, this line creates it. The `os.makedirs()` function can create all the intermediate directories in a path if they don't exist. For example, if you ask it to create `results/depth` and the `results` directory doesn't exist, it will create `results` first and then `depth` inside it.

That's it! You've just understood your first file. These simple functions will be very useful throughout our project.
