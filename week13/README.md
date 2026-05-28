# README

## 📦 安装步骤

在 python-for-ai 环境中安装 CPU 版本的 PyTorch，用于神经网络教学。

### 1. 激活环境并安装

```bash
# 激活 python-for-ai 环境
conda activate python-for-ai

# 安装 CPU 版 PyTorch（推荐使用 conda，依赖管理更稳定）
conda install pytorch torchvision torchaudio cpuonly -c pytorch -y
```

### 2. 验证安装

```bash
# 进入 Python 环境测试
python -c "
import torch
import torchvision
print('✅ PyTorch 版本:', torch.__version__)
print('✅ torchvision 版本:', torchvision.__version__)
print('✅ CUDA 是否可用:', torch.cuda.is_available())
print('✅ CPU 模式正常工作')
"
```

预期输出：
```
✅ PyTorch 版本: 2.x.x
✅ torchvision 版本: 0.x.x
✅ CUDA 是否可用: False
✅ CPU 模式正常工作
```

---

## 🧠 简单神经网络示例（测试用）

安装完成后，可以运行这个简单的神经网络代码验证：

```python
import torch
import torch.nn as nn
import torch.optim as optim

# 创建一个简单的线性回归神经网络
class SimpleNet(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc = nn.Linear(1, 1)  # 输入1维，输出1维
    
    def forward(self, x):
        return self.fc(x)

# 生成简单数据：y = 2x + 1
x = torch.tensor([[1.0], [2.0], [3.0], [4.0]])
y = torch.tensor([[3.0], [5.0], [7.0], [9.0]])

# 训练模型
model = SimpleNet()
criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)

for epoch in range(100):
    optimizer.zero_grad()
    output = model(x)
    loss = criterion(output, y)
    loss.backward()
    optimizer.step()

# 测试：输入 x=5，期望输出 11
test_x = torch.tensor([[5.0]])
print(f"预测结果: {model(test_x).item():.2f} (期望: 11.00)")
```

---

## 💡 如果 conda 安装慢或失败

### 备选方案：使用 pip 安装

```bash
conda activate python-for-ai

# 使用官方 CPU 专用源（速度快）
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

### 使用国内镜像源加速

```bash
# 清华源
pip install torch torchvision torchaudio -i https://pypi.tuna.tsinghua.edu.cn/simple

# 或者配置 pip 镜像后安装
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip install torch torchvision torchaudio
```

---

## 📋 更新后的环境完整信息

安装完成后，你的 `python-for-ai` 环境将包含：

| 类别 | 库 | 用途 |
|------|-----|------|
| 数据分析 | numpy, pandas, scipy | 数据处理 |
| 可视化 | matplotlib, seaborn | 图表绘制 |
| 机器学习 | scikit-learn | 传统ML算法 |
| 深度学习 | **pytorch, torchvision** | 神经网络、CNN |
| 开发工具 | jupyter | 交互式编程 |

---

## 🚀 快速验证环境完整性

```python
# 一次性测试所有核心库
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import sklearn
import torch
import torchvision

print("=" * 40)
print("python-for-ai 环境检查")
print("=" * 40)
print(f"✅ NumPy: {np.__version__}")
print(f"✅ Pandas: {pd.__version__}")
print(f"✅ Matplotlib: {plt.matplotlib.__version__}")
print(f"✅ Seaborn: {sns.__version__}")
print(f"✅ scikit-learn: {sklearn.__version__}")
print(f"✅ PyTorch: {torch.__version__}")
print(f"✅ torchvision: {torchvision.__version__}")
print(f"✅ CUDA 可用: {torch.cuda.is_available()} (CPU模式)")
print("=" * 40)
print("🎉 环境配置完成，可以开始深度学习课程！")
```