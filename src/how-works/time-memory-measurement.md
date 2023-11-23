# Time and Memory Measurement

<!-- toc -->

This code measures the execution time and memory consumption using the `time` and `resource` modules. Let's break down how the time and memory measurements are implemented:

# Time Measurement
The `perf_counter` function from the `time` module is used to measure the execution time.

```python
start_time = perf_counter()
# ... (code to be measured)
print(perf_counter() - start_time)
```
- `start_time` is recorded using `perf_counter()` before the code to be measured.
- The execution time is calculated by subtracting `start_time` from the current time after the code has executed.
- The result is printed, representing the time taken for the code to run.

# Memory Consumption Measurement (RAM)

> `getrusage` only works in linux/unix and FreeBSD operative systems based, therefore, **this functionality is disabled in windows**. For more compatibility information check the [resource library docs](https://docs.python.org/3/library/resource.html).

The `getrusage` function from the `resource` module is used to measure the maximum resident set size, which is an indicator of memory consumption.

```python
print(getrusage(RUSAGE_SELF).ru_maxrss) if isLinux else print(0)
```
- `getrusage(RUSAGE_SELF).ru_maxrss` retrieves the maximum consumption of RAM used by the process.
- This value is printed only if the operating system is Linux (`isLinux` is `True`); otherwise, it prints 0.
