# 🎾 网球比赛智能分析系统

一个基于深度学习和机器学习的网球比赛分析工具，能够自动检测网球轨迹、球场边界、球员位置和球的弹跳点。

![硬地球场分析](TennisProject-main/pics/hard.gif)
![草地球场分析](TennisProject-main/pics/grass.gif)
![红土球场分析](TennisProject-main/pics/clay.gif)

## 📋 项目概述

本项目集成了多个先进的计算机视觉和机器学习技术，为网球比赛提供全面的智能分析：

- **球轨迹检测**: 使用TrackNet深度学习模型实时跟踪网球轨迹
- **球场检测**: 神经网络检测网球场的14个关键点
- **弹跳点预测**: 基于CatBoost回归器预测球的弹跳位置
- **球员检测**: 识别和跟踪球场上的球员位置
- **场景分割**: 自动分割比赛中的不同场景

## 🚀 主要功能

### 1. 球轨迹检测 (Ball Detection)
- 使用TrackNet深度学习模型
- 实时跟踪网球在视频中的位置
- 生成连续的球轨迹数据

### 2. 球场检测 (Court Detection)
- 检测网球场的14个关键点
- 计算单应性矩阵进行视角转换
- 支持不同场地类型（硬地、草地、红土）

### 3. 弹跳点预测 (Bounce Detection)
- 基于CatBoost回归器
- 根据球轨迹预测弹跳位置
- 提供准确的弹跳时间点

### 4. 球员检测 (Person Detection)
- 识别球场上的球员
- 区分上下半场球员
- 跟踪球员移动轨迹

## 📦 环境要求

- Python 3.8+
- CUDA支持（推荐，用于GPU加速）
- 至少4GB内存

## 🔧 安装步骤

### 1. 克隆项目
```bash
git clone https://github.com/your-username/TennisProject.git
cd TennisProject
```

### 2. 创建虚拟环境
```bash
# 使用conda
conda create -n tennis-env python=3.8
conda activate tennis-env

# 或使用venv
python -m venv venv
source venv/bin/activate  # Linux/Mac
# 或
venv\Scripts\activate     # Windows
```

### 3. 安装依赖
```bash
pip install -r TennisProject-main/requirements.txt
```

### 4. 下载预训练模型
项目包含以下预训练模型文件：
- `model_best.pt` - TrackNet球检测模型
- `model_tennis_court_det.pt` - 球场检测模型
- `ctb_regr_bounce.cbm` - 弹跳预测模型

## 🎯 使用方法

### 基本用法
```bash
python TennisProject-main/main.py \
    --path_ball_track_model model_best.pt \
    --path_court_model model_tennis_court_det.pt \
    --path_bounce_model ctb_regr_bounce.cbm \
    --path_input_video your_video.mp4 \
    --path_output_video output_video.mp4
```

### 参数说明
- `--path_ball_track_model`: TrackNet球检测模型路径
- `--path_court_model`: 球场检测模型路径
- `--path_bounce_model`: 弹跳预测模型路径
- `--path_input_video`: 输入视频文件路径
- `--path_output_video`: 输出视频文件路径

### 视频要求
- 分辨率: 1280x720 (推荐)
- 格式: MP4, AVI等常见格式
- 内容: 网球比赛视频，包含完整的球场视野

## 📁 项目结构

```
TennisProject-main/
├── main.py                 # 主程序入口
├── ball_detector.py        # 球检测模块
├── court_detection_net.py  # 球场检测网络
├── bounce_detector.py      # 弹跳检测模块
├── person_detector.py      # 球员检测模块
├── court_reference.py      # 球场参考模型
├── homography.py          # 单应性变换
├── utils.py               # 工具函数
├── requirements.txt       # 依赖包列表
└── pics/                  # 示例图片
    ├── hard.gif          # 硬地球场示例
    ├── grass.gif         # 草地球场示例
    └── clay.gif          # 红土球场示例

TrackNet-main/             # TrackNet球检测模型
TennisCourtDetector-main/  # 球场检测模型
```

## 🔍 技术架构

### 核心算法
1. **TrackNet**: 基于深度学习的球轨迹检测
2. **Court Detection Net**: 卷积神经网络球场关键点检测
3. **CatBoost**: 梯度提升决策树用于弹跳预测
4. **YOLO**: 实时目标检测用于球员识别

### 处理流程
1. 视频输入 → 场景分割
2. 球轨迹检测 → 轨迹数据
3. 球场检测 → 单应性矩阵
4. 球员检测 → 位置信息
5. 弹跳预测 → 弹跳点
6. 结果可视化 → 输出视频

## 📊 输出结果

分析后的视频将包含：
- 球的实时轨迹线
- 球场边界标注
- 球员位置标记
- 弹跳点标识
- 小地图显示

## 🤝 贡献指南

欢迎提交Issue和Pull Request来改进项目！

### 开发环境设置
1. Fork项目
2. 创建功能分支
3. 提交更改
4. 创建Pull Request

## 📄 许可证

本项目采用MIT许可证 - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- [TrackNet](https://github.com/yastrebksv/TrackNet) - 球轨迹检测
- [TennisCourtDetector](https://github.com/yastrebksv/TennisCourtDetector) - 球场检测
- 感谢所有贡献者和开源社区

## 📞 联系方式

如有问题或建议，请通过以下方式联系：
- 提交GitHub Issue
- 发送邮件至: your-email@example.com

## 🔗 相关链接

- [项目博客文章](https://medium.com/@kosolapov.aetp/tennis-analysis-using-deep-learning-and-machine-learning-a5a74db7e2ee)
- [TrackNet预训练模型](https://github.com/yastrebksv/TrackNet)
- [球场检测预训练模型](https://github.com/yastrebksv/TennisCourtDetector)
- [弹跳预测模型](https://drive.google.com/file/d/1Eo5HDnAQE8y_FbOftKZ8pjiojwuy2BmJ/view?usp=drive_link)

---

⭐ 如果这个项目对您有帮助，请给我们一个星标！ 