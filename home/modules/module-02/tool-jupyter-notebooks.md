# Tool Guide: Jupyter Notebooks

{% hint style="info" %}
**In one sentence:** A Jupyter notebook (a `.ipynb` file) lets you run code in small boxes called cells and see each result right under the code that made it.
{% endhint %}

## Why analysts use it

Exploring data means asking one small question, looking at the answer, and then asking the next one. A notebook fits that: you run one cell, check the output, and keep going. Charts show up right inside the notebook. When you share an analysis, the notebook is often what you hand over, so it needs to read cleanly from top to bottom.

## Notebooks vs. scripts

You already know `.py` scripts from Module 1. Here's how notebooks are different:

| | `.py` script | `.ipynb` notebook |
| --- | --- | --- |
| How it runs | Every line, top to bottom, all at once | One cell at a time (Shift+Enter) |
| Memory | Forgets everything when it ends | The **kernel** keeps your variables between cells |
| Showing a result | You need `print()` | A cell shows its last line's value on its own |
| Best for | Finished programs and reusable code | Exploring data and showing your work |

{% hint style="warning" %}
**The kernel remembers what you ran, in the order you ran it, not the order on the page.** Before you share a notebook, use **Restart & Run All**. It starts fresh and runs every cell from the top, which proves the notebook really works.
{% endhint %}

## What you'll learn about it in Module 2

| Where | What you'll do |
| --- | --- |
| Quest 2.2 (Day 2) | Run cells, see how the kernel remembers variables, and use Restart & Run All |
| Quest 2.11 (Day 12) | Save charts from a notebook as image files for a README |
| Project (Days 15–19) | Turn your notebook into something an employer can read: no leftover instructions, every cell runs |

## How to start in VS Code

1. Open your `.ipynb` file in VS Code.
2. Click **Select Kernel** (top right) and choose your project's Python environment.
3. Click into a cell and press **Shift+Enter** to run it.

## Common first-day problems

| Problem | Fix |
| --- | --- |
| `NameError: name 'df' is not defined` | The cell that makes `df` hasn't run yet. Run the cells above it first. |
| The notebook works for you but breaks for someone else | It depends on a cell you deleted or ran out of order. Use Restart & Run All, then fix the first error. |
| VS Code asks you to install `ipykernel` | Click **Install**. It's the piece that connects VS Code to Python. |

## Getting started resources

* [Jupyter Notebooks in VS Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) (official guide for the editor you'll use)
* [Jupyter: Get started](https://docs.jupyter.org/en/latest/start/index.html) (what notebooks and kernels are)

---

**Next:** [Tool Guide: pandas](tool-pandas.md)
