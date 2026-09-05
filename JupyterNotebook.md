- **Jupyter**：提供交互式编程环境。你可以在 Notebook 里一格一格地写代码、运行代码，同时混合 Markdown、公式、图片和运行结果。常见的有 **Jupyter Notebook** 和 **JupyterLab**。
- **ipykernel**：是 Jupyter 中专门负责执行 **Python 代码** 的内核。你在某个单元格里点击运行后，代码实际上是交给 `ipykernel` 执行，再把结果返回给 Jupyter 界面显示。

Jupyter Notebook / JupyterLab
        ↓ 发送代码
     ipykernel
        ↓
   Python 解释器
        ↓
    执行代码
        ↓
 返回结果给 Jupyter