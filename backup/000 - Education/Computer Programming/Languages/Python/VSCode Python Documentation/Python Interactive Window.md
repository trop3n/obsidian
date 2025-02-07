---
up: "[[VSCode Python Docs]]"
tags:
  - education/computerprogramming/languages/python/vscode/interactivewindows
prev: "[[Python Environments]]"
---

# Python Interactive Window

[Jupyter](https://jupyter-notebook.readthedocs.io/en/latest/) (formerly IPython Notebook) is an open-source project that lets you easily combine Markdown text and executable Python source code on one canvas called a **notebook**. Visual Studio Code supports working with [Jupyter Notebooks natively](https://code.visualstudio.com/docs/datascience/jupyter-notebooks), as well as through Python code files. This topic covers the support offered through Python code files and demonstrates how to:

- Work with Jupyter-like code cells
- Run code in the Python Interactive Window
- View, inspect and filter variables using the *Variables Explorer* and *Data Viewer*
- Connect to a remote Jupyter server
- Debug a Jupyter notebook
- Export a Jupyter notebook

To work with Jupyter notebooks, you must activate an Anaconda environment in VSCode, or another Python environment in which you've installed the Jupyter package. To select an environment, use the **Python: Select Interpreter** command from the Command Palette (`Ctrl+Shift+P`)

Once the appropriate environment is activated, you can create and run Jupyter-like code cells, connect to a remote Jupyter server for running code cells, and export Python files as Jupyter notebooks.
## Jupyter Code Cells

You define Jupyter-like code cells within Python code using a `# %` comment:

```python
# %
msg = "Hello World"
print(msg)

# %
msg = "Hello again"
print(msg)
```

> [!NOTE]
> **Note**: Make sure to have the code shown above in a file with a `.py` extension.

When the Python extension detects a code cell, it adds **Run Cell** and **Debug Cell** CodeLens adornments. The first cell also includes **Run Below** and all subsequent cells include **Run Above**:

![](https://i.imgur.com/wQLkfPX.png)

