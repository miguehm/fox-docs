# Charts Generator

<!-- toc -->

We have used the `matplotlib` and `manim` library to represent the comparison of the execution times and memory usage of the Fox algorithm with matrices of either integers or floats.

# Matplotlib

## Calculate Mean Times and Memory Usage

```python
times_MPI, times_SEC, memory_MPI, memory_SEC = data(min_e, max_e, isInt=isInt)
```
Calls the `data` function to obtain execution times and memory usage for sequential and parallel executions.

## Prepare Data for Plotting

```python
y_Time_MPI   = [np.mean(times_MPI [exponent]) for exponent in times_MPI ]
y_Time_SEC   = [np.mean(times_SEC [exponent]) for exponent in times_SEC ]
y_Memory_MPI = [np.mean(memory_MPI[exponent]) for exponent in memory_MPI]
y_Memory_SEC = [np.mean(memory_SEC[exponent]) for exponent in memory_SEC]
```
Calculates the mean times and memory usage for both MPI and sequential executions.

## Configure Bar Chart Parameters

```python
bar_w = 0.35
x_Time_MPI   = np.array([exponent - bar_w/2 for exponent in times_MPI])
x_Time_SEC   = np.array([exponent + bar_w/2 for exponent in times_SEC])
x_Memory_MPI = np.array([exponent - bar_w/2 for exponent in memory_MPI])
x_Memory_SEC = np.array([exponent + bar_w/2 for exponent in memory_SEC])
```
Sets parameters for the bar chart, including bar width and positions for both time and memory plots.

## Create Matplotlib Figure

```python
fig, (Time_ax, Memory_ax) = plt.subplots(1, 2, figsize=(20, 5)) if isLinux else plt.subplots(1, 1, figsize=(10, 5))
```
Creates a Matplotlib figure with one or two subplots, depending on whether the operating system is Linux.

## Configure Plot Titles and Labels

```python
fig.suptitle(f'Comparison of Fox Algorithm Executions with {num_type} numbers.\n{PROCESSOR} - {nthreads} Threads - {RAM}GB')
Time_ax.set_title('Sequential and Parallel Execution Time Comparison')
Time_ax.set_xlabel('Matrix Order')
Time_ax.set_ylabel('Execution Time (s)')
```
Sets titles and labels for the plots.

## Plot Execution Time Bars

```python
bars_Time_MPI = Time_ax.bar(x_Time_MPI, y_Time_MPI, bar_w, label='MPI', color='#EA75FA')
bars_Time_SEC = Time_ax.bar(x_Time_SEC, y_Time_SEC, bar_w, label='Sequential', color='#4590FA')
```
Plots bars for execution times for both MPI and sequential executions.

## Plot Memory Usage Bars

> In the background we use `getrusage`. This function only works in linux/unix and FreeBSD operative systems based, therefore, **this functionality is disabled in windows**. For more compatibility information check the [resource library docs](https://docs.python.org/3/library/resource.html).

```python
if isLinux:
   Memory_ax.set_title('Memory Usage (RAM) Comparison')
   Memory_ax.set_xlabel('Matrix Order')
   Memory_ax.set_ylabel('Memory Used (MB)')
   bars_Memory_MPI = Memory_ax.bar(x_Memory_MPI, y_Memory_MPI, bar_w, label='MPI', color='#EA75FA')
   bars_Memory_SEC = Memory_ax.bar(x_Memory_SEC, y_Memory_SEC, bar_w, label='Sequential', color='#4590FA')
```
Plots bars for memory usage for both MPI and sequential executions.

## Display Labels and Legends

```python
for bar in bars_Time_SEC + bars_Time_MPI:
   x_pos   = bar.get_x() + bar.get_width()/2.0
   y_value = bar.get_height()
   Time_ax.text(x_pos, y_value, f'{y_value:5.5}s', va='bottom', ha='center')
Time_ax.legend()

if isLinux:
   for bar in bars_Memory_SEC + bars_Memory_MPI:
       x_pos   = bar.get_x() + bar.get_width()/2.0
       y_value = bar.get_height()
       Memory_ax.text(x_pos, y_value, f'{(y_value/1024):5.5}MB', va='bottom', ha='center')
   Memory_ax.legend()
```

Displays labels and legends on the plots.

## Save Plots

```python
plt.tight_layout()
fig.savefig(create_dir('charts', f'{2**(min_e)}-{2**(max_e-1)}', 'int' if isInt else 'float'))
```
Saves the plots to a file.

# Manim

This Manim script defines a scene that creates an animated bar chart using data from different matrix multiplication scenarios. The script loops over various parameters, generates animations, and saves the results in an organized directory structure.

## Manim Scene Class

```python
class chart(Scene):
   def construct(self):
```
Defines a Manim scene class named `chart`.

## Configure Frame Dimensions

```python
config["frame_width"] = 12
config["frame_height"] = 8
```
Sets the width and height of the animation frame.

## Create Bar Chart

```python
chart = BarChart(
   values = np.zeros(len(data)),
   y_range=[0, round(max_v + max_v/8,2), round(max_v/4,2)],
   x_length=16,
   y_length=6,
   bar_width=0.8,
   bar_names=[2**exp for exp in EXP],
   y_axis_config={"font_size": 24},
   x_axis_config={"font_size": 24},
).scale(0.7)
```
Creates a bar chart using Manim's `BarChart` class with specified configurations.

## Create Axes Labels

```python
x_label = chart.get_x_axis_label('Matrix Size', edge=DOWN, direction=DOWN, buff=0.05).scale(0.6)
y_l = 'Time (s)' if MEASURE == 'time_mean' else 'Memory (MB)'
y_label = chart.get_y_axis_label(y_l, edge=UP, direction=UP, buff=-1).scale(0.6).rotate(PI/2).next_to(chart, LEFT)
```
Adds labels for the x-axis and y-axis.

## Create Group for Chart and Labels

```python
gv = VGroup(chart, x_label, y_label).to_edge(DOWN)
```
Groups the chart and labels together.

## Create Title and Architecture Information

```python
Title = f'Comparison of RAM used by the Fox algorithm with {dt} numbers using the {meth} method' if MEASURE == 'memory_mean' else f'Comparison of execution time of the Fox algorithm with {dt} numbers using the {meth} method'
t_top = Tex(Title).scale(0.75).to_edge(UP)
architecture = Tex(f'{PROCESSOR} {THREADS} {RAM} DDR4 3200MHz', color='purple_a').scale(0.6).next_to(t_top, DOWN)
```
Creates a title and information about the system architecture.

## Display Elements

```python
self.play(Create(gv), Create(t_top), Create(architecture))
```
Displays the grouped chart, labels, title, and architecture information.

## Animate Chart Bars
```python
self.play(chart.animate.change_bar_values(data), run_time=1.5)
```
Animates the bars in the chart based on the data.

## Display Bar Labels

```python
self.play(Create(chart.get_bar_labels(font_size=30, color=WHITE)))
```
Displays labels for the bars in the chart.

## Save and Display Animation

```python
self.wait(3)
```
Waits for 3 seconds before completing the animation.

## Main Execution Loop

```python
if __name__ == '__main__':
    # Loop over different parameters (DTYPE, METHOD, EXP) and generate animations for each case.
```

Uses nested loops to iterate over different data parameters and create animations for each case.

## Move Generated Files

```python
shutil.move('manim/media/images/chart.png', f'{path}/{file}.png')
shutil.move('manim/media/videos/720p30/chart.mp4', f'{path}/{file}.mp4')
```
Moves the generated image and video files to a specified directory.
