# python课程ipynb文件

为什么要学这门课
- AI时代的基本技能：看懂别人的, 评估（Evaluate）和修正（Debug） AI 生成的内容
- 解决问题的逻辑：能写自己的, 系统化思维与拆解能力, 把一个模糊的人工智能需求（如“识别这张图里的垃圾分类”）拆解为：数据采集、预处理、模型调用、结果呈现。
- Coding工具爆火的背景下，正视工具和技能的关系，算术与计算器

怎么学：
- 课上：课件的总览、示例代码
- 课下：
  - 博客、gpt
  - 项目中学习


For lecturer:
- install VMware
  - 准备纯净的“实验环境”
在正式上课前，你需要先在 VMware 中搭建好这个“新电脑”。
下载系统镜像 (ISO)：前往 Microsoft 官网 下载 Windows 10/11 的 ISO 镜像文件。
创建虚拟机 (VM)：
打开 VMware，点击 “创建新虚拟机” -> 选择 “典型”。
选择安装程序光盘映像文件 (ISO)，浏览并选中你下载的系统镜像。
配置参数：建议分配 至少 4GB 内存 和 2 个处理器核心，以保证演示时流畅不卡顿。
安装 VMware Tools (关键)：
系统装好进入桌面后，点击 VMware 菜单栏的 “虚拟机” -> “安装 VMware Tools”。
作用：安装后可以实现宿主机与虚拟机之间的文件拖拽、剪贴板共享以及全屏分辨率自适应。 

  - 建立“还原点”（快照功能）
这是虚拟机方案的核心优势。通过“快照”，你可以在演示失败或下一次上课前，一键将电脑恢复到“刚装好、最干净”的状态。
拍摄快照：
在虚拟机处于关机或开机状态（推荐关机，快照文件更小）时，点击菜单栏的 “虚拟机” -> “快照” -> “拍摄快照”。
命名为 “纯净系统-未装任何环境”。
如何恢复：
演示结束后，点击 “快照管理器”，选择该快照并点击 “转到”，虚拟机会立刻恢复到最初的状态。

- create shared folder in host pc
  link: https://www.nakivo.com/blog/3-simple-ways-to-transfer-files-from-a-vm-to-a-host/

For students:
- download course files and unzip (learn git by yourself later)
 link: https://github.com/ntu-caokun/python_course 

- download vscode
 link: https://code.visualstudio.com/

- download anaconda
 link: https://repo.anaconda.com/miniconda/

- install vscode， 能check的框都check
- install anaconda，能check的框都check
    - 以 管理员身份 运行 PowerShell（在 Windows 开始菜单搜索 PowerShell，右键以管理员身份运行）。
    - 输入以下命令并回车：'Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser'
    - 输入 Y 确认


## Use this repo
- vscode 打开课程资料文件夹
- 打开终端（Terminal）新建一个 PowerShell 终端
- 新建环境 conda env create -f environment.yaml
  - 如果下载有问题，可考虑使用清华镜像源 [教程](https://zhuanlan.zhihu.com/p/595179507)
- 激活环境 conda activate python_course
- 打开文件 jupyter notebook 
- 选定章节文件
- Alt+R slideshow; Shift+Enter实时修改运行block
 

Refs:
- [安装vscode](https://zhuanlan.zhihu.com/p/698865320)：常用的开发工具
- [安装anaconda](https://blog.csdn.net/weixin_43828245/article/details/124768518)：常用的环境管理工具
