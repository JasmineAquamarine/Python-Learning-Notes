## 第3集 Pandas入门（Series与DataFrame）

- **对应章节**：第5章
- **核心内容**：
  - Series和DataFrame的创建与属性。
  - 数据索引和切片（loc、iloc）。
  - 常用数据查看方法（head、describe）。
- **实战内容**：
  - Titanic数据集初步探索。

### 3.1 Pandas数据结构介绍

- **Series：**一维数组型对象，包含一个值序列和一个索引列。
- **DataFrame：**表示矩阵的数据表，column是行，index是指标。

### 3.2 切片和索引

- **索引：**

  - **行索引：**df.loc['idex']（指标索引）/df.iloc[:0]（整数索引）
  - **列索引：**df['']（通用，可新建column）/df.column（仅可用于存在的）

- 一些索引对象的方法和属性

  - | 方法         | 描述                                             |
    | ------------ | ------------------------------------------------ |
    | append       | 将额外的索引对象粘贴到原索引后，产生一个新的索引 |
    | difference   | 计算两个索引的差集                               |
    | intersection | 计算两个索引的交集                               |
    | union        | 计算两个索引的并集                               |
    | isin         | 计算表示每一个值是否在传值容器中的布尔数组       |
    | delete       | 将位置i的元素删除，并产生新的索引                |
    | drop         | 根据传参删除指定索引值，并产生新的索引           |
    | insert       | 在位置i插入元素，并产生新的索引                  |
    | is_monotonic | 如果索引序列递增则返回True                       |
    | is_unique    | 如果索引序列唯一则返回True                       |
    | unique       | 计算索引的唯一值序列                             |

- Reindex方法

- axis = 1或axis = ‘columns’索引列

### 3.3 数据查看方法

```python
df.head()#可以看前5行的数据
df.describe()#计算Framework的一些统计数据，比如均值、标准差等
```

### 3.4 常用函数

P104、110-115

### 3.5 实战训练2：**Titanic数据集分析**

- **目标**：用Pandas加载和分析Titanic数据集，探索乘客生存率。
- **步骤**：
  1. 加载Titanic数据集（Kaggle提供）。
  2. 查看数据基本信息（如head、describe）。
  3. 计算乘客生存率，并按性别、舱位分组分析。
- **数据集**：
  - Kaggle Titanic数据集：[下载链接](https://www.kaggle.com/c/titanic/data)
- **代码展示：**

```python
import pandas as pd

# 加载数据
df = pd.read_csv("titanic.csv")

# 查看基本信息
print(df.head())
print(df.describe())

# 计算生存率
survival_rate = df['Survived'].mean()
print(f"Overall survival rate: {survival_rate:.2%}")

# 按性别和舱位分组分析
survival_by_gender = df.groupby('Sex')['Survived'].mean()
survival_by_class = df.groupby('Pclass')['Survived'].mean()
print(survival_by_gender, survival_by_class)
```

