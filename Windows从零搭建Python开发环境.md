# Windows从零搭建Python开发环境

> 一份手把手教程，带你从零开始配置 VSCode + Python + Conda + Git + Jupyter Notebook 开发环境，避开所有新手常见的坑。

---

## 📌 目录

1. [前言：为什么需要这样的配置环境？](#前言)
2. [准备工作：软件下载清单](#准备工作)
3. [【重要】终端类型澄清：别再搞混了！](#终端类型澄清)
4. [第一步：解决“环境变量”与“中文路径”隐患](#第一步解决环境变量与中文路径隐患)
5. [第二步：安装 Miniconda (Conda)](#第二步安装-miniconda-conda)
6. [第三步：创建独立的Python环境](#第三步创建独立的python环境)
7. [第四步：安装 VS Code 及核心插件](#第四步安装-vs-code-及核心插件)
8. [第五步：安装 Git 版本控制](#第五步安装-git-版本控制)
9. [第六步：在 VS Code 中关联 Python 环境](#第六步在-vs-code-中关联-python-环境)
10. [第七步：VS Code中使用Jupyter Notebook并选择Kernel](#第七步vs-code中使用jupyter-notebook并选择kernel)
11. [第八步：解决“中文路径”问题的最佳实践](#第八步解决中文路径问题的最佳实践)
12. [第九步：写一段测试代码验证环境](#第九步写一段测试代码验证环境)
13. [附录一：常用命令速查表](#附录一常用命令速查表)
14. [附录二：常见问题排查表](#附录二常见问题排查表)

---

## 前言：为什么需要这样的配置环境？

很多编程初学者会遇到这些问题：

- 安装完Python后，在终端输入`python`显示“不是内部或外部命令”
- 好不容易装好了，却发现代码里的中文路径导致程序崩溃
- 写的代码因为没有版本管理，改错了就找不回来了
- 电脑用户名是中文，导致各种莫名其妙的报错
- 打开Jupyter Notebook，不知道选哪个kernel，明明装了包却无法导入
- 在cmd里装完包，到VS Code里又找不到，因为在不同的环境里

本教程将逐一解决这些痛点，手把手带你完成配置。

---

## 准备工作：软件下载清单

请提前下载以下安装包（全部选择Windows 64位版本）：

| 软件 | 下载地址 | 说明 |
| :--- | :--- | :--- |
| **Miniconda** (推荐) | [清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/) | 环境管理工具，比Anaconda更轻量 |
| **VS Code** | [官网](https://code.visualstudio.com/) | 代码编辑器 |
| **Git** | [官网](https://git-scm.com/downloads/win) | 版本控制工具 |

> 💡 **为什么不用Anaconda？** Anaconda预装了太多用不到的包，Miniconda只有核心功能，需要什么包自己装，更清爽，也节省硬盘空间。

---

## 【重要】终端类型澄清：别再搞混了！

这是很多同学最困惑的地方：电脑里有一堆“黑框框”，到底用哪个？

### Windows常见终端类型对比

| 终端名称 | 怎么打开 | 特点 | 本教程用不用？ |
| :--- | :--- | :--- | :--- |
| **CMD (命令提示符)** | `Win+R` → 输入 `cmd` | Windows经典黑框，功能较少 | ✅ **可以用**（但必须安装时勾选了添加PATH） |
| **PowerShell** | 右键开始菜单 → “Windows PowerShell” | 功能更强大，语法略有不同 | ✅ **可以用** |
| **Anaconda Prompt** | 开始菜单搜索 “Anaconda Prompt” | 自动激活conda环境，但只限conda | ⚠️ **不推荐**（只能管理conda，和VS Code终端不一致） |
| **VS Code终端** | VS Code中 `Ctrl + `` ` | 集成在编辑器内，最方便 | ✅ **强烈推荐**（本教程主要使用这个） |

### 🎯 核心建议：统一使用 VS Code 终端

**本教程所有命令，都请在VS Code终端中执行。**

原因：
1. VS Code终端会自动识别你当前打开的文件夹
2. 它本质上就是cmd或PowerShell，但多了和编辑器的联动
3. 不需要来回切换窗口，写代码和敲命令在一个界面完成
4. 你在VS Code终端里装包、激活环境，VS Code的Jupyter Notebook能立刻识别

### 如何打开VS Code终端？

1. 打开VS Code
2. 点击菜单栏 `终端` → `新建终端`
3. 或者直接按快捷键：`Ctrl + `` ` （注意：\` 是键盘左上角Esc下面的那个键）

### 如何确认你现在用的是正确的终端？

打开终端后，观察左侧提示符：
- 如果你已经激活了conda环境，会显示 `(环境名) PS 路径>` 或 `(环境名) 路径>`
- 输入 `conda --version`，能正常显示版本号 → ✅ 终端可用

### ❌ 常见错误

| 错误操作 | 后果 |
| :--- | :--- |
| 在Anaconda Prompt里装包，然后去VS Code终端里运行 | 因为终端环境不同，VS Code里找不到刚装的包 |
| 打开多个不同终端，在A里装包，在B里运行代码 | 环境不互通，白白浪费时间 |
| 用记事本打开cmd，但安装时没勾选添加到PATH | 输入`conda`报错“不是内部或外部命令” |

### ✅ 正确做法

**就认准一个：VS Code内置终端。** 所有安装、激活、装包、运行，都在这里面完成。

---

## 第一步：解决“环境变量”与“中文路径”隐患

**在做任何事情之前，请先检查你的Windows用户名：**

1. 打开 `C:\Users\` 文件夹
2. 查看你的用户名文件夹名称

⚠️ **如果你的用户名是中文（例如：C:\Users\张三）**：
- 建议你**新建一个英文名的本地账户**再继续
- 原因：很多科学计算库（如TensorFlow、PyTorch）和编译器根本无法识别中文路径，会导致各种玄学报错

---

## 第二步：安装 Miniconda (Conda)

Conda是一个包管理和环境管理工具，它能让你在一台电脑上创建多个隔离的Python环境，避免不同项目之间的包版本冲突。

### 1. 运行安装程序
- 右键点击下载好的 `Miniconda3-latest-Windows-x86_64.exe`
- 选择 **“以管理员身份运行”**

### 2. 关键安装选项

| 安装步骤 | 操作 | 原因 |
| :--- | :--- | :--- |
| **安装路径** | 修改为 `D:\Miniconda3` | **务必不要安装在中文路径！** 建议装在D盘根目录 |
| **高级选项** | ✅ 勾选 **“Add Miniconda3 to my PATH environment variable”** <br> ✅ 勾选 **“Register Miniconda3 as my default Python”** | 这两个选项必须勾选，否则终端无法识别conda命令 |

### 3. 验证安装
- 打开 **VS Code终端**（`Ctrl + `` `）
- 输入：`conda --version`
- 如果显示版本号（如 `conda 24.x.x`），说明安装成功

### 4. 配置国内镜像源（加速下载）

在VS Code终端中依次输入以下命令，切换清华镜像源：

```bash
conda config --set show_channel_urls yes
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2/
```

---

## 第三步：创建独立的Python环境

不要直接在 `base` 环境中写代码！我们需要为这个教程单独创建一个干净的环境。

### 在VS Code终端中执行以下命令：

```bash
# 1. 创建一个名为 myenv 的环境，指定Python版本为3.11
conda create -n myenv python=3.11 -y

# 2. 激活这个环境
conda activate myenv

# 3. 验证Python是否可用
python --version
```

> 💡 **环境隔离的好处**：如果项目A需要Python 3.7 + 旧版TensorFlow，项目B需要Python 3.11 + 新版PyTorch，你可以创建两个独立环境，互不干扰。

---

## 第四步：安装 VS Code 及核心插件

### 1. 安装 VS Code
双击安装程序，一路“下一步”，建议勾选以下选项：
- ✅ 创建桌面快捷方式
- ✅ 添加到PATH（重新启动后生效）
- ✅ 将Code注册为受支持的文件类型的编辑器

### 2. 安装必装插件

打开 VS Code，点击左侧**扩展图标**（或按 `Ctrl+Shift+X`），搜索并安装以下插件：

| 插件名称 | 作用 |
| :--- | :--- |
| **Python** (Microsoft官方) | Python核心支持（调试、语法高亮、智能提示） |
| **Pylance** | 超快的代码补全和类型检查 |
| **GitLens** | 可视化Git提交历史 |
| **Chinese (Simplified) Language Pack** | 中文界面（可选） |
| **Jupyter** (Microsoft官方) | 在VS Code中运行Jupyter Notebook |

### 3. 将VS Code配置为Git默认编辑器

打开VS Code终端，执行：

```bash
git config --global core.editor "code --wait"
```

---

## 第五步：安装 Git 版本控制

### 1. 安装 Git
- 右键 `Git-xxx-64-bit.exe`，选择 **“以管理员身份运行”**
- **关键选项**（其他保持默认）：
  - **选择编辑器**：选择 **“Use Visual Studio Code as Git's default editor”**（用我们刚装好的VS Code）
  - **调整PATH环境**：选择 **“Git from the command line and also from 3rd-party software”**（这样在cmd中也能用git命令）
  - **换行符转换**：选择 **“Checkout Windows-style, commit Unix-style line endings”**

### 2. 验证安装并配置身份

打开VS Code终端，执行：

```bash
# 验证安装
git --version

# 配置你的身份（提交代码时会记录这些信息）
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱@example.com"

# 设置默认分支名为 main
git config --global init.defaultBranch main
```

---

## 第六步：在 VS Code 中关联 Python 环境

这是最关键的一步！让VS Code知道我们刚才用conda创建的环境在哪里。

### 1. 打开项目文件夹
- 在电脑上新建一个文件夹，例如 `D:\MyPythonProject`
- **路径中不要包含中文或空格！**
- 将整个文件夹拖入VS Code窗口中，或点击 `文件` → `打开文件夹`

### 2. 选择Python解释器
- 按 `Ctrl + Shift + P`，打开命令面板
- 输入 `Python: Select Interpreter` 并选择
- 在弹出的列表中，选择我们创建的环境：
  - 应该显示类似 `Python 3.11.0 ('myenv': conda)` 的选项
  - 路径类似 `D:\Miniconda3\envs\myenv\python.exe`

### 3. 新建终端验证
- 在VS Code中打开新终端：`终端` → `新建终端`（或按 `Ctrl + `` `）
- 终端左侧应该显示 `(myenv)`，表示conda环境已自动激活
- 输入 `python`，应该能看到Python 3.11的版本信息

---

## 第七步：VS Code中使用Jupyter Notebook并选择Kernel

很多同学在VS Code里打开`.ipynb`文件后，发现右上角显示“选择内核”，点开后一头雾水——这么多Python环境，到底选哪个？这一节帮你彻底搞明白。

### 1. 前提：确保你的conda环境中已安装Jupyter

在 **VS Code终端** 中执行以下命令（确保终端已激活 `myenv` 环境）：

```bash
# 1. 确认当前激活的环境
conda activate myenv  # 如果还没激活的话

# 2. 在该环境中安装 Jupyter 和 ipykernel
conda install jupyter ipykernel -y
```

> 💡 **为什么需要这一步？** Jupyter内核是运行notebook的“引擎”，你必须在你想要使用的conda环境里安装它，VS Code才能识别并列出这个环境。

### 2. 将conda环境注册为Jupyter Kernel

安装完jupyter后，需要手动将conda环境注册为一个可选的kernel：

```bash
# 确保当前已激活目标环境（如 myenv）
conda activate myenv

# 将该环境注册为kernel，名称为 "myenv"
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

参数说明：

| 参数 | 含义 |
| :--- | :--- |
| `--name` | kernel的内部名称（建议和conda环境名一致） |
| `--display-name` | 在VS Code内核选择菜单中显示的名称（可以自定义） |

执行完毕后，可以用以下命令查看已注册的所有kernel：

```bash
jupyter kernelspec list
```

### 3. 在VS Code中选择正确的Kernel

1. 在VS Code中打开或新建一个`.ipynb`文件：
   - 点击 `文件` → `新建文件` → `Jupyter Notebook`
   - 或者直接按 `Ctrl+Shift+P` → 输入 `Create: New Jupyter Notebook`

2. 点击右上角的 **“选择内核”** 按钮（如果没有显示，点击右上角状态栏的内核名称）

3. 在弹出的菜单中：
   - 选择 **“Jupyter Kernel”** → **“现有Jupyter内核”**
   - 你会看到刚才注册的 `Python (myenv)`
   - 点击选中它

4. 验证成功：notebook右上角应显示 `Python (myenv)`，运行一个单元格（`Shift+Enter`），能看到正确的Python版本和环境路径。

### 4. 如何在终端中管理包并同步到Jupyter

这是一个典型的工作流：你想在 `myenv` 环境中安装 `numpy`、`pandas`、`matplotlib` 等包，然后在Jupyter中使用它们。

```bash
# Step 1: 确保在VS Code终端中，且已激活目标环境
conda activate myenv

# Step 2: 安装需要的包（现在都装到了正确的环境里）
conda install numpy pandas matplotlib -y
# 或者用pip（如果conda源里没有某个包）
pip install scikit-learn

# Step 3: 验证包是否安装成功
conda list | findstr numpy   # 查看numpy是否在列表中
python -c "import numpy; print(numpy.__version__)"  # 直接测试导入

# Step 4: 回到VS Code的Jupyter Notebook
# 点击工具栏的“...” → “重新加载”内核
# 然后再次确认kernel为 "Python (myenv)"
# 新安装的包现在就可以在notebook中import了
```

### 5. 完整示例：从创建环境到运行Jupyter Notebook

> 💡 这是一个“一键复制”式的完整流程，直接按顺序在 **VS Code终端** 中执行即可。

```bash
# 1. 创建新环境（假设用于AI学习）
conda create -n python-for-ai python=3.11 -y

# 2. 激活环境
conda activate python-for-ai

# 3. 安装jupyter和ipykernel
conda install jupyter ipykernel -y

# 4. 注册kernel
python -m ipykernel install --user --name python-for-ai --display-name "Python (python-for-ai)"

# 5. 安装常用数据科学包
conda install numpy pandas matplotlib seaborn -y
pip install scikit-learn

# 6. 验证环境
python -c "import numpy, pandas, sklearn; print('All packages imported successfully!')"
```

然后打开VS Code，新建Jupyter Notebook，选择kernel为 `Python (python-for-ai)`，就可以愉快地写代码了。

### 六、常见问题：为什么我的环境没有出现在Kernel列表中？

| 现象 | 原因 | 解决方法 |
| :--- | :--- | :--- |
| 列表里只有一个`Python 3.x.x 64-bit` | 没有安装`ipykernel`或未注册 | 执行上面的注册命令 |
| 列表里有很多重复的环境 | 之前多次注册 | 用`jupyter kernelspec remove 环境名`删除多余的 |
| 选中环境后运行单元格报错 | 该环境的Python解释器损坏 | 重新创建conda环境 |
| 刚装的包在notebook里`import`报错 | kernel没重启 | 点击“...” → “重新加载”内核 |

### 7. 在VS Code终端中一键激活conda环境的小技巧

每次打开VS Code终端，默认可能是`base`环境。如果你想让终端**自动激活**某个指定环境：

**方法一：手动激活（最推荐，最可靠）**
每次打开新终端后，输入：`conda activate python-for-ai`

**方法二：设置VS Code默认激活环境**
在项目文件夹的`.vscode/settings.json`中添加：

```json
{
    "python.defaultInterpreterPath": "D:/Miniconda3/envs/python-for-ai/python.exe",
    "terminal.integrated.profiles.windows": {
        "Conda": {
            "path": "cmd.exe",
            "args": ["/K", "D:/Miniconda3/Scripts/activate.bat", "D:/Miniconda3", "&&", "conda activate python-for-ai"]
        }
    },
    "terminal.integrated.defaultProfile.windows": "Conda"
}
```

**方法三：查看当前终端是否在正确的环境中**
终端左侧应显示 `(python-for-ai)`，如果没有，说明没激活。执行 `conda info --envs` 可以查看所有环境，带 `*` 的是当前激活的。

---

## 第八步：解决“中文路径”问题的最佳实践

虽然我们避开了中文用户名，但有时仍需处理中文文件名。以下是代码层面的解决方案。

### 方法一：使用 `pathlib` 处理路径（推荐）

```python
from pathlib import Path

# 无论路径是否有中文，都安全
file_path = Path("C:/用户/张三/数据.csv")
with open(file_path, encoding='utf-8') as f:
    content = f.read()
```

### 方法二：读取文件时明确指定编码

```python
# 错误示例（会报错）
with open('中文文件.txt', 'r') as f:
    data = f.read()

# 正确示例
with open('中文文件.txt', 'r', encoding='utf-8') as f:
    data = f.read()
```

---

## 第九步：写一段测试代码验证环境

在VS Code中新建一个文件 `test.py`，输入以下代码：

```python
# 测试Python环境
import sys
print(f"Python版本: {sys.version}")

# 测试Conda环境
import os
conda_prefix = os.environ.get('CONDA_PREFIX', '未激活conda环境')
print(f"Conda环境路径: {conda_prefix}")

# 测试Git版本控制
print("环境配置完成！🎉")
```

### 运行代码：
- 点击右上角的 **三角形运行按钮** ▶
- 或在终端中输入：`python test.py`

如果能看到正确的版本信息和路径，恭喜你，环境配置成功！

### 测试Jupyter Notebook

1. 在VS Code中按 `Ctrl+Shift+P`，输入 `Create: New Jupyter Notebook`
2. 在第一个单元格中输入：
```python
import sys
import numpy as np
print(sys.version)
print(np.__version__)
```
3. 确保右上角kernel显示 `Python (myenv)` 或 `Python (python-for-ai)`
4. 按 `Shift+Enter` 运行

如果能正常输出版本号，说明Jupyter环境也配置成功了！

---

## 附录一：常用命令速查表

### Conda命令

| 操作 | 命令 |
| :--- | :--- |
| 创建环境 | `conda create -n 环境名 python=3.x` |
| 激活环境 | `conda activate 环境名` |
| 退出环境 | `conda deactivate` |
| 安装包 | `conda install 包名` 或 `pip install 包名` |
| 查看环境列表 | `conda env list` |
| 删除环境 | `conda env remove -n 环境名` |
| 查看当前环境的包 | `conda list` |

### Jupyter Kernel命令

| 操作 | 命令 |
| :--- | :--- |
| 注册kernel | `python -m ipykernel install --user --name 环境名 --display-name "显示名称"` |
| 查看已注册kernel | `jupyter kernelspec list` |
| 删除kernel | `jupyter kernelspec remove kernel名称` |

### Git命令

| 操作 | 命令 |
| :--- | :--- |
| 初始化仓库 | `git init` |
| 查看状态 | `git status` |
| 添加文件到暂存区 | `git add .` |
| 提交代码 | `git commit -m "说明"` |
| 查看版本 | `git --version` |

### 验证命令

| 操作 | 命令 |
| :--- | :--- |
| 检查conda版本 | `conda --version` |
| 检查python版本 | `python --version` |
| 检查git版本 | `git --version` |
| 查看当前激活的环境 | `conda info --envs`（带*的是当前环境） |

---

## 附录二：常见问题排查表

| 问题现象 | 可能原因 | 解决方法 |
| :--- | :--- | :--- |
| `'conda' 不是内部或外部命令` | 安装时没勾选添加到PATH | 重装Miniconda，勾选“Add to PATH” |
| `'python' 不是内部或外部命令` | Python未加入环境变量 | 重装时勾选“Add Python to PATH” |
| 终端不显示 `(myenv)` | 未激活conda环境 | 执行 `conda activate myenv` |
| 代码读取文件报 `UnicodeDecodeError` | 编码问题 | 在 `open()` 中添加 `encoding='utf-8'` |
| `FileNotFoundError`：路径含中文 | Windows默认编码问题 | 改用 `pathlib` 模块处理路径 |
| Jupyter kernel列表为空 | 未安装ipykernel或未注册 | `conda install ipykernel -y` 然后重新注册 |
| 刚装的包在Jupyter里找不到 | kernel没重启或选错了环境 | 重启kernel，检查右上角环境名是否正确 |
| 在Anaconda Prompt装包，VS Code里找不到 | 两个终端用的不是同一个Python环境 | 统一使用VS Code终端进行操作 |
| 打开多个终端搞混了环境 | 不同终端激活了不同的conda环境 | 关掉多余的终端，只保留VS Code终端 |
| `pip install` 装到了全局而不是conda环境 | 安装时没激活conda环境 | 先 `conda activate 环境名` 再装包 |

---

## 🎯 总结

完成以上配置后，你的Windows电脑已经拥有了一个**干净、隔离、可复现**的Python开发环境：

- ✅ Conda管理Python版本和包依赖
- ✅ VS Code提供代码编辑和调试
- ✅ Jupyter Notebook支持交互式编程，可以自由切换kernel
- ✅ Git提供版本控制
- ✅ 避开了中文路径和终端混乱的所有坑

**记住最重要的一条铁律：所有操作都在VS Code终端里完成，不要打开CMD、PowerShell或Anaconda Prompt。**

现在，你可以安心地开始写第一行Python代码了！🚀

---

*教程结束。如有问题，请对照附录二中的排查表逐步检查。*