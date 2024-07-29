<!--theme: rose-pine-moon -->
## Introduction
**Ultralytics YOLOv8**，这是广受好评的**实时对象检测**和**图像分割**模型的最新版本。 YOLOv8 基于深度学习和计算机视觉领域的前沿进步而构建，在速度和准确性方面提供无与伦比的性能。其流线型设计使其适用于各种应用程序，并可轻松适应从边缘设备到云 API 的不同硬件平台。

---
## Install
```shell
# Install the ultralytics package from PyPI
pip install ultralytics
```
---

## 主要的功能
1. Detect
2. Segment
3. Classify
4. Pose
5. OBB(Oriented Bounding Boxes Object Detection)
---
# 检测
## Train
```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolov8n.yaml")  # build a new model from YAML
model = YOLO("yolov8n.pt")  # load a pretrained model (recommended for training)
model = YOLO("yolov8n.yaml").load("yolov8n.pt")  # build from YAML and transfer weights

# Train the model
results = model.train(data="coco8.yaml", epochs=100, imgsz=640)
```
---
## Val
```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolov8n.pt")  # load an official model
model = YOLO("path/to/best.pt")  # load a custom model

# Validate the model
metrics = model.val()  # no arguments needed, dataset and settings remembered
metrics.box.map  # map50-95
metrics.box.map50  # map50
metrics.box.map75  # map75
metrics.box.maps  # a list contains map50-95 of each category
```
---
## Predict
```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolov8n.pt")  # load an official model
model = YOLO("path/to/best.pt")  # load a custom model

# Predict with the model
results = model("https://ultralytics.com/images/bus.jpg")  # predict on an image
```
---
![](C:\Users\ver\Pictures\Screenshots\results.png)
17 / 49 错误率
正确率 32 / 49 = 0.6306

---
## Pose

![bg](C:\Users\ver\Desktop\yolo_test\image.jpg)
![](C:\Users\ver\Desktop\yolo_test\runs\pose\predict\image.jpg)

---
### 使用自己的训练集训练
## datasets 的结构

```
dataset/
├── train/
│   ├── images/
│   └── labels/
└── val/
    ├── images/
    └── labels/
```

在根目录下创建一个data.yaml的文件来描述数据集的相关信息。
**roboflow** 收集数据，打标签，导出yolov8类型的数据集

---
