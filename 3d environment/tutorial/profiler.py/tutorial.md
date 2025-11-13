# Tutorial: `profiler.py` - Measuring Our Code's Performance

This script provides a simple tool to measure how long each part of our pipeline takes to run. This is called **profiling**. Profiling is essential for understanding the performance of our code and identifying "bottlenecks" – the parts of the code that are the slowest and might need optimization.

For our thesis, analyzing the trade-offs between reconstruction quality and performance is a key goal, so having a profiler is very important.

This script introduces a new concept: a **Class**.

---

### What is a Class?

Think of a class as a blueprint for creating objects. In our `utils.py` file, we wrote functions. A class can contain both data (variables) and functions (which are called "methods" when they are inside a class).

Our `Profiler` class is a blueprint for creating "profiler objects". Each profiler object will have its own internal stopwatch and a logbook to keep track of timings.

---

### The `import` Statement

```python
import time
```

-   **`import time`**: This imports Python's built-in `time` library. We'll use it to get the current system time, which is the basis for our stopwatch.

---

### The `Profiler` Class

```python
class Profiler:
    # ... methods go here ...
```

-   **`class Profiler:`**: This line declares a new class named `Profiler`.

---

### The `__init__` Method (The Constructor)

```python
    def __init__(self):
        self.start_time = None
        self.step_times = {}
```

-   **`def __init__(self):`**: This is a special method called the **constructor**. It's automatically called whenever you create a new object from this class (e.g., `my_profiler = Profiler()`). Its job is to set up the initial state of the object.
-   **`self`**: The `self` parameter refers to the specific object instance that is being created. It's how the object can store and access its own data.
-   **`self.start_time = None`**: We create a variable `start_time` that belongs to this object (`self`). This will store the timestamp of when we start timing a step. We initialize it to `None`, meaning it has no value yet.
-   **`self.step_times = {}`**: We create a dictionary called `step_times`. This will be our logbook, where we store the name of each step and how long it took to run (e.g., `{"Frame Extraction": 0.5, "Depth Estimation": 3.2}`).

---

### The `start` Method

```python
    def start(self):
        self.start_time = time.time()
```

-   **`def start(self):`**: This defines a method named `start`.
-   **`self.start_time = time.time()`**: This is like clicking the "start" button on a stopwatch. `time.time()` returns the current time as a floating-point number (the number of seconds since a specific point in history called the "epoch"). We save this start time in our object's `start_time` variable.

---

### The `record` Method

```python
    def record(self, step_name):
        if self.start_time is None:
            print("Profiler has not been started.")
            return
        
        end_time = time.time()
        self.step_times[step_name] = end_time - self.start_time
        self.start_time = end_time
```

-   **`def record(self, step_name):`**: This method is like hitting the "lap" button on a stopwatch. It records the time for a specific step and immediately starts timing the next one. It takes `step_name` as input, which is a string describing the step we just finished (e.g., "Depth Estimation").
-   **`if self.start_time is None:`**: A quick check to make sure someone called `start()` before calling `record()`.
-   **`end_time = time.time()`**: We get the current time, which marks the end of the step we were timing.
-   **`self.step_times[step_name] = end_time - self.start_time`**: We calculate the duration of the step by subtracting the `start_time` from the `end_time`. We then add this to our `step_times` dictionary, with the `step_name` as the key.
-   **`self.start_time = end_time`**: This is a clever trick. To immediately start timing the *next* step, we reset the `start_time` to be the `end_time` of the step we just finished.

---

### The `report` Method

```python
    def report(self):
        print("\n--- Profiler Report ---")
        for step, duration in self.step_times.items():
            print(f"{step}: {duration:.4f} seconds")
        print("-----------------------")
```

-   **`def report(self):`**: This method prints out a nicely formatted summary of all the recorded times.
-   **`print(...)`**: We print a header for our report.
-   **`for step, duration in self.step_times.items():`**: We loop through our `step_times` dictionary. The `.items()` method gives us both the key (the `step` name) and the value (the `duration`) for each entry in the dictionary.
-   **`print(f"{step}: {duration:.4f} seconds")`**: We print the name of the step and its duration.
    -   `{duration:.4f}`: This is a formatting instruction. It tells Python to format the `duration` as a floating-point number with exactly 4 digits after the decimal point. This keeps the report clean and readable.
-   **`print(...)`**: We print a footer to finish the report.

```