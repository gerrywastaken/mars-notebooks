# mars-notebooks

``` python
import sys
import math as mt
import numpy as np
import matplotlib.pyplot as plt
import uuid
import os

def plot_style():
    dark_gray  = '#282C34'   # Color for border lines and background (dark gray)
    white      = '#ffffff'  # Color for text (e.g. labels, legend, etc.) (white)
    light_gray = '#e6e1dc'   # Color for axis labels (light gray)
    slate_gray = '#928374'   # Color for grid lines (slate gray)

    style = {
        'figure.facecolor': dark_gray,
        'axes.facecolor':   dark_gray,
        'axes.edgecolor':   dark_gray,
        'legend.facecolor': dark_gray,
        'legend.edgecolor': dark_gray,
        'grid.color':       dark_gray,
        'axes.labelcolor':  light_gray,
        'xtick.color':      light_gray,
        'ytick.color':      light_gray,
        'text.color':       white,
        'figure.dpi':       200,
        'grid.linestyle':   '-',
        'grid.linewidth':   0.2,
        'legend.frameon':   True,
        'legend.fontsize':  10,
        'legend.framealpha': 1,
    }

    plt.style.use('dark_background')
    plt.rcParams.update(style)

def plot_label(title="", xlabel="", ylabel=""):
    plt.xlabel(xlabel)
    plt.ylabel(ylabel)
    plt.title(title)

def plot(*args, title="", xlabel="", ylabel="", **kwargs):
    fig, ax = plt.subplots()
    plot_style()

    x = []
    # Display the plot in an interactive mode
    background_color = "#282C34"

    # fig.patch.set_facecolor(background_color)
    ax.set_facecolor(background_color)

    # find the minimum and maximum values of x and y
    xmin = np.min(args[:, 0])
    xmax = np.max(args[:, 0])
    ymin = np.min(args[:, 1])
    ymax = np.max(args[:, 1])


    for arg in args:
        ax.plot(arg[0], arg[1], label=arg[2])

    ax.legend()
    plot_label(title=title, xlabel=xlabel, ylabel=ylabel)
    ax.set_xlim(xmin, xmax)
    ax.set_ylim(ymin, ymax)
    plt.show()

plot_style()

def table(**kwargs):
    # Get list of column headers and data arrays
    headers = list(kwargs.keys())
    data_arrays = list(kwargs.values())

    # Print header row
    header = "|"
    for h in headers:
        header += " {} |".format(h)
    print(header)

    # Print separator row
    separator = "|"
    for h in headers:
        separator += "-|"
    print(separator)

    # Print data rows
    num_rows = len(data_arrays[0])
    for i in range(num_rows):
        row = "|"
        for data_array in data_arrays:
            row += " {:.4f} |".format(data_array[i])
        print(row)


x = np.linspace(-10.0, 10.0, num=100)
y = x**(2/3)

plot(
  [x, y, "x ^ 2/3"],
)
```

