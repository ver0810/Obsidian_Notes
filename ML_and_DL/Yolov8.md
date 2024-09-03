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
 
| Argument  | Default | Descrpition                                                      |
| --------- | ------- | ---------------------------------------------------------------- |
| model     | None    | 指定训练的文件，接受`.pt` 预训练的文件 或者一个`.yaml`的配置文件                          |
| data      | None    | 数据集的配置文件                                                         |
| epochs    | 100     | 总训练时期。每个时期代表都会对数据集进行完整遍历                                         |
| time      | None    | 最大训练时间（小时为单位）。会覆盖epochs的设置。允许自动停止一段时间内的持续训练。                     |
| patience  | 100     | 在提前停止训练之前等待验证指标没有改变的时间数。有利于防止过拟合。                                |
| batch     | 16      | 批大小。有三种模式：1.整数模式 2.batch=-1 60%gpu利用率自动模式 3.batch=0.7利用率分数。      |
| imgsz     | 640     | 图像大小，图像载入模型前都会设置为该值                                              |
| save      | True    | 保存模型点和最终权重                                                       |
| cache     | False   | 启用内存，代价会使内存占用率提高                                                 |
| device    | None    | 指定训练的设备，单一gpu`device=0`,多gpu`device=0, 1`, cpu`device=cpu`, 苹果芯片 |
| workers   | 8       | 指定数据加载前的工作线程数                                                    |
| project   | None    | 保存数据输出的目录名称                                                      |
| name      | None    | 运行的目录名称，用于保存输出和项目日志                                              |
| optimizor | 'auto'  | 选择训练优化器。影响模型的收敛速度                                                |
| verbose   | 0       | 在模型训练期间输出详细的日志输出                                                 |
| dropout   | 0.0     | 分类任务中正则化的dropout率，                                               |

#### Logging

utralytics 提供三种日志记录器，`Comet`, `ClearML`, `tensorboad`
#### 常见的参数设置

| Argument | Default | Description                                                            |
| -------- | ------- | ---------------------------------------------------------------------- |
| `model`  | `None`  | 训练模型的路径.                                                               |
| `data`   | `None`  | 训练集配置路径 (e.g., `coco8.yaml`).                                          |
| `epochs` | `100`   | 总的训练时期                                                                 |
| `batch`  | `16`    | 批大小                                                                    |
| `imgsz`  | `640`   | 训练目标图像的大小                                                              |
| `device` | `None`  | Computational device(s) for training like `cpu`, `0`, `0,1`, or `mps`. |
| `save`   | `True`  | 能够保存训练的检查和最后的权重                                                        |

---
### Val
**Example**
```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolov8n.pt")  # load an official model
#model = YOLO("path/to/best.pt")  # or load a custom model

# Validate the model
metrics = model.val()  # no arguments needed, dataset and settings remembered
metrics.box.map  # map50-95
metrics.box.map50  # map50
metrics.box.map75  # map75
metrics.box.maps  # a list contains map50-95 of each category
```

Argument of validation

| Argument      | Type    | Default | Description                                                 |
| ------------- | ------- | ------- | ----------------------------------------------------------- |
| `data`        | `str`   | `None`  | 指定数据集配置文件的路径（例如，coco8.yaml）。该文件包括验证数据的路径、类名和类的数量。           |
| `imgsz`       | `int`   | `640`   | 定义输入图像的大小。所有图像在处理前都会调整至此尺寸。                                 |
| `batch`       | `int`   | `16`    | 设置每批的图像数量。对 AutoBatch 使用 -1，它会根据 GPU 内存可用性自动调整。             |
| `save_json`   | `bool`  | `False` | If `True`, 保存为`json`文件                                      |
| `save_hybrid` | `bool`  | `False` | 如果为 True，则保存将原始注释与其他模型预测相结合的标签的混合版本。                        |
| `conf`        | `float` | `0.001` | 设置检测的最小置信度阈值。置信度低于此阈值的检测将被丢弃                                |
| `iou`         | `float` | `0.6`   | 设置非极大值抑制 (NMS) 的交并集 (IoU) 阈值。有助于减少重复检测。                     |
| `max_det`     | `int`   | `300`   | 限制每个图像的最大检测数量。在密集场景中很有用，可以防止过度检测。                           |
| `half`        | `bool`  | `True`  | 启用半精度 (FP16) 计算，减少内存使用量并可能提高速度，同时对精度的影响最小。                  |
| `device`      | `str`   | `None`  | 指定用于验证的设备（cpu、cuda:0 等）。允许灵活地利用 CPU 或 GPU 资源。               |
| `dnn`         | `bool`  | `False` | 如果为 True，则使用 OpenCV DNN 模块进行 ONNX 模型推理，提供 PyTorch 推理方法的替代方案 |
| `plots`       | `bool`  | `False` | 设置为 True 时，生成并保存预测与真实情况的图，以便对模型性能进行视觉评估。                    |
| `rect`        | `bool`  | `False` | 如果为 True，则使用矩形推理进行批处理，减少填充并可能提高速度和效率                        |
| `split`       | `str`   | `val`   | 确定用于验证的数据集分割（val、test 或 train）。允许灵活选择用于性能评估的数据段。            |
|               |         |         |                                                             |
|               |         |         |                                                             |
yolov8 提供一些关键的指标
- mAP50 (mean Average Precision at IoU threshold 0.5)
- mAP75 (mean Average Precision at IoU threshold 0.75)
- mAP50-95 (mean Average Precision across multiple IoU thresholds from 0.5 to 0.95)

---
### Predict
#### Example
```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolov8n.pt")  # load an official model
#model = YOLO("path/to/best.pt")  # or load a custom model

# Predict with the model
results = model("https://ultralytics.com/images/bus.jpg")  # predict on an image
```

> [!Tip] 使用stream=True处理长视频或大数据集以有效管理内存。当stream=False时，所有帧或数据点的结果都存储在内存中，这可能会快速累加并导致大型输入出现内存不足错误。相比之下，stream=True 使用生成器，仅将当前帧或数据点的结果保留在内存中，从而显着减少内存消耗并防止内存不足问题。

#### `Results` objects have the following methods:

| Method      | Return Type     | Description                          |
| ----------- | --------------- | ------------------------------------ |
| `update()`  | `None`          | 更新 Results 对象的框、掩码和概率属性。             |
| `cpu()`     | `Results`       | 返回 Results 对象的副本，其中包含 CPU 内存上的所有张量。  |
| `numpy()`   | `Results`       | 返回 Results 对象的副本，其中所有张量均作为 numpy 数组。 |
| `cuda()`    | `Results`       | 返回 Results 对象的副本，其中包含 GPU 内存上的所有张量。  |
| `to()`      | `Results`       | 返回具有指定设备和数据类型上的张量的 Results 对象的副本。    |
| `new()`     | `Results`       | 返回具有相同图像、路径和名称的新 Results 对象。         |
| `plot()`    | `numpy.ndarray` | 绘制检测结果。返回带注释的图像的 numpy 数组。           |
| `show()`    | `None`          | 展示所有的结果在屏幕上                          |
| `save()`    | `None`          | 保存带有注释的结果到文件                         |
| `verbose()` | `str`           | 返回每一次任务的log                          |
| `tojson()`  | `str`           | Convert the object to JSON format.   |
#### **`Results`** objects have the following attributes:

| Attribute    | Type                  | Description                   |
| ------------ | --------------------- | ----------------------------- |
| `orig_img`   | `numpy.ndarray`       | 原始对象是一个numpy数组                |
| `orig_shape` | `tuple`               | 原始图像的（height， width）尺寸大小的元组   |
| `boxes`      | `Boxes, optional`     | 包含检测框的box对象                   |
| `masks`      | `Masks, optional`     | 包含检测框的mask对象                  |
| `probs`      | `Probs, optional`     | 包含分类任务的每个类别的概率的 Probs 对象。     |
| `keypoints`  | `Keypoints, optional` | 包含每个对象检测到的关键点的 Keypoints 对象。  |
| `obb`        | `OBB, optional`       | 包含定向边界框的 OBB 对象               |
| `speed`      | `dict`                | 每个图像的预处理、推理和后处理速度的字典（以毫秒为单位）。 |
| `names`      | `dict`                | 类名字典                          |
| `path`       | `str`                 | 图像的的路径                        |

---

### Export
## Arguments

| Argument    | Type             | Default         | Description                                            |
| ----------- | ---------------- | --------------- | ------------------------------------------------------ |
| `format`    | `str`            | `'torchscript'` | 导出的模型格式                                                |
| `imgsz`     | `int` or `tuple` | `640`           | 导出的图片大小，可以使方形图的整数或者是(width, height)的元祖                 |
| `keras`     | `bool`           | `False`         | 可以导出Keras的格式，提供Tensorflow服务和apis                       |
| `optimize`  | `bool`           | `False`         | 导出到Torchscript时应用的优化器，可能会减小模型大小并提高性能。                  |
| `half`      | `bool`           | `False`         | 使用半精度量化                                                |
| `int8`      | `bool`           | `False`         | 使用int8量化                                               |
| `dynamic`   | `bool`           | `False`         | 允许 ONNX 和 TensorRT 导出的动态输入大小，增强处理不同图像尺寸的灵活性。           |
| `simplify`  | `bool`           | `False`         | 使用 onnxslim 简化 ONNX 导出的模型图，从而可能提高性能和兼容性。               |
| `opset`     | `int`            | `None`          | 指定 ONNX opset 版本以与不同的 ONNX 解析器和运行时兼容。如果未设置，则使用最新支持的版本。 |
| `workspace` | `float`          | `4.0`           | 设置 TensorRT 优化的最大工作空间大小（以 GiB 为单位），平衡内存使用和性能。          |
| `nms`       | `bool`           | `False`         | 在 CoreML 导出中添加非极大值抑制 (NMS)，这对于准确高效的检测后处理至关重要           |
| `batch`     | `int`            | `1`             | 指定导出模型批量推理大小或导出模型在预测模式下将同时处理的最大图像数                     |

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

