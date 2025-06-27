# Conda常用命令

1. **创建新环境：**

   ```
   conda create --name myenv
   ```

   创建一个名为`myenv`的新环境。

2. **激活环境**：

   ```
   conda activate myenv
   ```

   激活名为`myenv`的环境。

3. **退出环境**：

   ```
   conda deactivate
   ```

   退出当前激活的环境。

4. **列出所有环境**：

   ```
   conda env list
   ```

   列出所有已创建的环境。

5. **删除环境**：

   ```
   conda env remove --name myenv
   ```

   删除名为`myenv`的环境。

6. **安装包**：

   ```
   conda install numpy
   ```

   在当前激活的环境中安装`numpy`包。

7. **更新包**：

   ```
   conda update numpy
   ```

   更新当前环境中的`numpy`包。

8. **卸载包**：

   ```
   conda remove --name myenv numpy
   ```

   从名为`myenv`的环境中卸载`numpy`包。

9. **搜索包**：

   ```
   conda search scipy
   ```

   搜索可用的`scipy`包。

10. **查看包详细信息**：

    ```
    conda info scipy
    ```

    查看`scipy`包的详细信息。

11. **查看环境信息**：

    ```
    conda info --envs
    ```

    查看所有环境的信息。

12. **更新Conda**：

    ```
    conda update conda
    ```

    更新Conda本身。

13. **查看Conda版本**：

    ```
    conda --version
    ```

    查看当前Conda的版本。

14. **查看已安装的包**：

    ```
    conda list
    ```

    列出当前环境中安装的所有包。

15. **清理不必要的包和缓存**：

    ```
    conda clean --all
    ```

    清理所有不必要的包和缓存文件。