<!--theme: -->
## Introduction
**Ultralytics YOLOv8**，这是广受好评的**实时对象检测**和**图像分割**模型的最新版本。 YOLOv8 基于深度学习和计算机视觉领域的前沿进步而构建，在速度和准确性方面提供无与伦比的性能。其流线型设计使其适用于各种应用程序，并可轻松适应从边缘设备到云 API 的不同硬件平台。

---
## Install
windows 需要配置c环境，环境变量。python3.8有问题不建议。
```shell
# Install the ultralytics package from PyPI
pip install ultralytics
```
---

## Task
1. Detect
2. Segment
3. Classify
4. Pose
5. OBB(Oriented Bounding Boxes Object Detection)
---

---
## 检测
### Train
**Example**
```python
from ultralytics import YOLO

# Load a model
#model = YOLO("yolov8n.yaml")  # build a new model from YAML
#model = YOLO("yolov8n.pt")  # load a pretrained model (recommended for training)
model = YOLO("yolov8n.yaml").load("yolov8n.pt")  # build from YAML and transfer weights

# Train the model
results = model.train(data="coco8.yaml", epochs=100, imgsz=640)
```

### Train Settings

#### **hyperparameters**（超参数）
模型训练前必须手动设置的参数，与模型的参数（权重和偏置）超参数不是通过训练数据来得到的。
1. **批大小（batch size）** 每次迭代时用于训练的样本数量。批大小较大会使计算更加稳定，但需要更多的内存；较小的批大小可能导致计算波动较大。
2. **学习率（learning rate）** 决定了模型在每次迭代中更新权重的步伐大小。学习率太高可能导致模型不收敛，太低则可能导致收敛速度过慢或陷入局部最优。
3. **动量（momentum）** 一种优化技术
4. **权重衰减（weight decay）** 也叫L2正则化，防止模型过拟合
5. **正则化系数（Regularizstion Parameters）** 如L1， L2正则化系数
6. **激活函数(activation function)** 决定输出， ReLU、Sigmoid、Tanh
7. **优化器[[optimizer]]** 决定如何调整模型的权重，以减小损失函数，SGD（随机梯度下降）、Adam、RMSprop
8. **[[loss function]]** 用于衡量模型预测值与真实值之间差距的函数。损失函数的值越小，表示模型的预测结果与真实结果越接近。
 
| Argument | Default | Descrpition                                                      |
| -------- | ------- | ---------------------------------------------------------------- |
| model    | None    | 指定训练的文件，接受`.pt` 预训练的文件 或者一个`.yaml`的配置文件                          |
| data     | None    | 数据集的配置文件                                                         |
| epochs   | 100     | 总训练时期。每个时期代表都会对数据集进行完整遍历                                         |
| time     | None    | 最大训练时间（小时为单位）。会覆盖epochs的设置。允许自动停止一段时间内的持续训练。                     |
| patience | 100     | 在提前停止训练之前等待验证指标没有改变的时间数。有利于防止过拟合。                                |
| batch    | 16      | 批大小。有三种模式：1.整数模式 2.batch=-1 60%gpu利用率自动模式 3.batch=0.7利用率分数。      |
| imgsz    | 640     | 图像大小，图像载入模型前都会设置为该值                                              |
| save     | True    | 保存模型点和最终权重                                                       |
| cache    | False   | 启用内存，代价会使内存占用率提高                                                 |
| device   | None    | 指定训练的设备，单一gpu`device=0`,多gpu`device=0, 1`, cpu`device=cpu`, 苹果芯片 |


---
### Val
**Example**
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
### Predict
```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolov8n.pt")  # load an official model
model = YOLO("path/to/best.pt")  # load a custom model

# Predict with the model
results = model("https://ultralytics.com/images/bus.jpg")  # predict on an image
```

---
## 使用自己的训练集训练
### 1. 收集数据
### 2. 注释图像
### 3. 生成yolo的txt注释
#### 使用Roboflow
---
### 4. 组织数据集
#### datasets 的结构

```
dataset/
├── train/
│   ├── images/
│   └── labels/
└── val/
    ├── images/
    └── labels/
```
---
在根目录下创建一个data.yaml的文件来描述数据集的相关信息。
```yaml
train: C:/Users/ver/Desktop/yolo_fruit/datasets/train
val: C:/Users/ver/Desktop/yolo_fruit/datasets/valid
test: C:/Users/ver/Desktop/yolo_fruit/datasets/test
device: 0

nc: 9
names: ['Apple', 'Banana', 'Grapes', 'Kiwi', 'Mango', 'Orange', 'Pineapple', 'Sugerapple', 'Watermelon']

```
![](C:\Users\ver\Pictures\Screenshots\data_yaml.png)

---