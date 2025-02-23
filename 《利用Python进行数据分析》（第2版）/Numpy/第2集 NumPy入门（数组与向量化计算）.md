## 第2集 NumPy入门（数组与向量化计算）

- **对应章节**：第4章
- **核心知识点**：
  - NumPy数组的创建和基本操作。
  - 向量化计算的优势（对比Python原生循环）。
  - 广播（Broadcasting）机制。
- **实战项目**：
  - 实战训练1：矩阵运算与图像处理。

### 2.1 NumPy简介

- **为什么学习NumPy**

  - 存储大量数据方便
  - 运行快
  - 操作简单——使用了向量化的计算

- **NumPy的类型与维度**

  - ndarray

  - int和float型

  - ```python
    np.astype()#用于转化类型，如果是小数转化为整数，小数部分会被直接抹去
    ```

  | 名称       | 描述                                                         |
  | :--------- | :----------------------------------------------------------- |
  | bool_      | 布尔型数据类型（True 或者 False）                            |
  | int_       | 默认的整数类型（类似于 C 语言中的 long，int32 或 int64）     |
  | intc       | 与 C 的 int 类型一样，一般是 int32 或 int 64                 |
  | intp       | 用于索引的整数类型（类似于 C 的 ssize_t，一般情况下仍然是 int32 或 int64） |
  | int8       | 字节（-128 to 127）                                          |
  | int16      | 整数（-32768 to 32767）                                      |
  | int32      | 整数（-2147483648 to 2147483647）                            |
  | int64      | 整数（-9223372036854775808 to 9223372036854775807）          |
  | uint8      | 无符号整数（0 to 255）                                       |
  | uint16     | 无符号整数（0 to 65535）                                     |
  | uint32     | 无符号整数（0 to 4294967295）                                |
  | uint64     | 无符号整数（0 to 18446744073709551615）                      |
  | float_     | float64 类型的简写                                           |
  | float16    | 半精度浮点数，包括：1 个符号位，5 个指数位，10 个尾数位      |
  | float32    | 单精度浮点数，包括：1 个符号位，8 个指数位，23 个尾数位      |
  | float64    | 双精度浮点数，包括：1 个符号位，11 个指数位，52 个尾数位     |
  | complex_   | complex128 类型的简写，即 128 位复数                         |
  | complex64  | 复数，表示双 32 位浮点数（实数部分和虚数部分）               |
  | complex128 | 复数，表示双 64 位浮点数（实数部分和虚数部分）               |

### 2.2 生成ndarray

| 函数名         | 描述                                                 |
| -------------- | ---------------------------------------------------- |
| array          | 将输入数据转换为nparray，默认复制所有输入数据        |
| asarray        | 将输入转换为ndarray                                  |
| arange         | Python内建函数range的数组版                          |
| ones           | 根据给定形状和数据类型生成全1的数组                  |
| ones_like      | 根据所给的数组生成一个形成一样的全1的数组            |
| zeros          | 根据给定形状和数据类型生成全0的数组                  |
| zeros_like     | 根据所给数组生成一个形状一样的全0数组                |
| empty          | 根据给定形状生成一个没有初始化熟知的空数组           |
| empty_like     | 根据给定数组生成一个形状一样但没有初始化数值的空数组 |
| full           | 根据给定的形状和数据类型生成指定数值的数组           |
| full_alike     | 根据给定数组生成一个形状一样但内容为制定数值的数组   |
| eye,identity   | 生成一个N×N特征矩阵（对角线位置全是1，其余位置是0）  |
| random.randn() | 生成一些随机    正态分布的数据                       |

### 2.3 NumPy基本操作

- **索引&切片**
  - [] 选中数据的子集或某单元素，如果修改，会覆盖原数据（因为numpy用于处理大型数据，如果一味的复制会导致内存不足），除非使用.copy()提前复制数据
  - 布尔索引，可用于筛选符合一定条件的数据p100-102
  - 可以筛选符合特定顺序的自己，需要传递一个指明所需顺序的列表或数组p103
  - 使用.reshape()可以改变其维度形状
- **转置&换轴**
  - .T:转置；.transpose():换轴
- **通用函数**
- **文件输入&输出**
- **线性代数**
- **伪随机数**

### 2.4 广播机制

数学运算一般要求参与运算的数组形状相同，但由于NumPy的广播机制，它允许不同形状的数据之间进行算术运算。它会自动将较小的数组扩展为较大数组兼容的形状，然后进行元素级运算。

- **标量与数组相加**

  ```python
  import numpy as np
  
  # 创建一个数组
  arr = np.array([1, 2, 3])
  # 标量
  scalar = 5
  
  # 进行加法运算
  result = arr + scalar
  print(result)
  ```

- **不同形状数组相加**

  ```python
  import numpy as np
  
  # 创建两个数组
  arr1 = np.array([[1, 2, 3], [4, 5, 6]])  # 形状为 (2, 3)
  arr2 = np.array([1, 2, 3])  # 形状为 (3,)
  
  # 进行加法运算
  result = arr1 + arr2
  print(result)
  ```

- **无法广播的例子**

  ```python
  import numpy as np
  
  arr1 = np.array([[1, 2], [3, 4]])  # 形状为 (2, 2)
  arr2 = np.array([1, 2, 3])  # 形状为 (3,)
  
  try:
      result = arr1 + arr2
      print(result)
  except ValueError as e:
      print(f"发生错误: {e}")
  ```


### 2.5 实战训练1：矩阵运算与图像处理

- **目标**：用NumPy实现矩阵运算，并将其应用到图像处理中。

- **步骤**：

  1. 使用NumPy生成随机矩阵，并计算矩阵乘法。
  2. 加载一张图片（使用PIL或OpenCV库），将其转换为NumPy数组。
  3. 对图片进行简单处理（如灰度化、裁剪、旋转）。

- **数据集**：

  - 任意图片文件（如JPG、PNG）。

- **代码示例**：

  ```python
  import numpy as np
  from PIL import Image
  
  # 生成随机矩阵
  matrix_a = np.random.rand(3, 3)
  matrix_b = np.random.rand(3, 3)
  result = np.dot(matrix_a, matrix_b)
  
  # 加载图片并转换为NumPy数组
  image = Image.open("example.jpg")
  image_array = np.array(image)
  
  # 灰度化处理
  gray_image = np.dot(image_array[..., :3], matrix_a[0])
  Image.fromarray(gray_image).show()
  ```

## 