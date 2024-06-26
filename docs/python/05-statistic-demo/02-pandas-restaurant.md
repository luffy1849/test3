---
slug: /02-pandas-restaurant
---

# 2. 数据分析实际案例之：pandas在餐厅评分数据中的使用



# 简介

为了更好的熟练掌握pandas在实际数据分析中的应用，今天我们再介绍一下怎么使用pandas做美国餐厅评分数据的分析。

# 餐厅评分数据简介

数据的来源是UCI ML Repository，包含了一千多条数据，有5个属性，分别是：

userID： 用户ID

placeID：餐厅ID

rating：总体评分

food_rating：食物评分

service_rating：服务评分

我们使用pandas来读取数据：

```
import numpy as np

path = '../data/restaurant_rating_final.csv'
df = pd.read_csv(path)
df
```

|      | userID | placeID | rating | food_rating | service_rating |
| ---: | -----: | ------: | -----: | ----------: | -------------- |
|    0 |  U1077 |  135085 |      2 |           2 | 2              |
|    1 |  U1077 |  135038 |      2 |           2 | 1              |
|    2 |  U1077 |  132825 |      2 |           2 | 2              |
|    3 |  U1077 |  135060 |      1 |           2 | 2              |
|    4 |  U1068 |  135104 |      1 |           1 | 2              |
|  ... |    ... |     ... |    ... |         ... | ...            |
| 1156 |  U1043 |  132630 |      1 |           1 | 1              |
| 1157 |  U1011 |  132715 |      1 |           1 | 0              |
| 1158 |  U1068 |  132733 |      1 |           1 | 0              |
| 1159 |  U1068 |  132594 |      1 |           1 | 1              |
| 1160 |  U1068 |  132660 |      0 |           0 | 0              |

1161 rows × 5 columns

# 分析评分数据

如果我们关注的是不同餐厅的总评分和食物评分，我们可以先看下这些餐厅评分的平均数，这里我们使用pivot_table方法：

```
mean_ratings = df.pivot_table(values=['rating','food_rating'], index='placeID',
                                 aggfunc='mean')
mean_ratings[:5]
```

|         | food_rating | rating |
| ------: | ----------: | -----: |
| placeID |             |        |
|  132560 |        1.00 |   0.50 |
|  132561 |        1.00 |   0.75 |
|  132564 |        1.25 |   1.25 |
|  132572 |        1.00 |   1.00 |
|  132583 |        1.00 |   1.00 |

然后再看一下各个placeID，投票人数的统计：

```
ratings_by_place = df.groupby('placeID').size()
ratings_by_place[:10]
```

```
placeID
132560     4
132561     4
132564     4
132572    15
132583     4
132584     6
132594     5
132608     6
132609     5
132613     6
dtype: int64
```

如果投票人数太少，那么这些数据其实是不客观的，我们来挑选一下投票人数超过4个的餐厅：

```
active_place = ratings_by_place.index[ratings_by_place >= 4]
active_place
```

```
Int64Index([132560, 132561, 132564, 132572, 132583, 132584, 132594, 132608,
            132609, 132613,
            ...
            135080, 135081, 135082, 135085, 135086, 135088, 135104, 135106,
            135108, 135109],
           dtype='int64', name='placeID', length=124)
```

选择这些餐厅的平均评分数据：

```
mean_ratings = mean_ratings.loc[active_place]
mean_ratings
```

|         | food_rating |   rating |
| ------: | ----------: | -------: |
| placeID |             |          |
|  132560 |    1.000000 | 0.500000 |
|  132561 |    1.000000 | 0.750000 |
|  132564 |    1.250000 | 1.250000 |
|  132572 |    1.000000 | 1.000000 |
|  132583 |    1.000000 | 1.000000 |
|     ... |         ... |      ... |
|  135088 |    1.166667 | 1.000000 |
|  135104 |    1.428571 | 0.857143 |
|  135106 |    1.200000 | 1.200000 |
|  135108 |    1.181818 | 1.181818 |
|  135109 |    1.250000 | 1.000000 |

124 rows × 2 columns

对rating进行排序，选择评分最高的10个：

```
top_ratings = mean_ratings.sort_values(by='rating', ascending=False)
top_ratings[:10]
```

|         | food_rating |   rating |
| ------: | ----------: | -------: |
| placeID |             |          |
|  132955 |    1.800000 | 2.000000 |
|  135034 |    2.000000 | 2.000000 |
|  134986 |    2.000000 | 2.000000 |
|  132922 |    1.500000 | 1.833333 |
|  132755 |    2.000000 | 1.800000 |
|  135074 |    1.750000 | 1.750000 |
|  135013 |    2.000000 | 1.750000 |
|  134976 |    1.750000 | 1.750000 |
|  135055 |    1.714286 | 1.714286 |
|  135075 |    1.692308 | 1.692308 |

我们还可以计算平均总评分和平均食物评分的差值，并以一栏diff进行保存：

```
mean_ratings['diff'] = mean_ratings['rating'] - mean_ratings['food_rating']

sorted_by_diff = mean_ratings.sort_values(by='diff')
sorted_by_diff[:10]
```

|         | food_rating |   rating |      diff |
| ------: | ----------: | -------: | --------: |
| placeID |             |          |           |
|  132667 |    2.000000 | 1.250000 | -0.750000 |
|  132594 |    1.200000 | 0.600000 | -0.600000 |
|  132858 |    1.400000 | 0.800000 | -0.600000 |
|  135104 |    1.428571 | 0.857143 | -0.571429 |
|  132560 |    1.000000 | 0.500000 | -0.500000 |
|  135027 |    1.375000 | 0.875000 | -0.500000 |
|  132740 |    1.250000 | 0.750000 | -0.500000 |
|  134992 |    1.500000 | 1.000000 | -0.500000 |
|  132706 |    1.250000 | 0.750000 | -0.500000 |
|  132870 |    1.000000 | 0.600000 | -0.400000 |

将数据进行反转，选择差距最大的前10：

```
sorted_by_diff[::-1][:10]
```

|         | food_rating |   rating |     diff |
| ------: | ----------: | -------: | -------: |
| placeID |             |          |          |
|  134987 |    0.500000 | 1.000000 | 0.500000 |
|  132937 |    1.000000 | 1.500000 | 0.500000 |
|  135066 |    1.000000 | 1.500000 | 0.500000 |
|  132851 |    1.000000 | 1.428571 | 0.428571 |
|  135049 |    0.600000 | 1.000000 | 0.400000 |
|  132922 |    1.500000 | 1.833333 | 0.333333 |
|  135030 |    1.333333 | 1.583333 | 0.250000 |
|  135063 |    1.000000 | 1.250000 | 0.250000 |
|  132626 |    1.000000 | 1.250000 | 0.250000 |
|  135000 |    1.000000 | 1.250000 | 0.250000 |

计算rating的标准差，并选择最大的前10个：

```
# Standard deviation of rating grouped by placeID
rating_std_by_place = df.groupby('placeID')['rating'].std()
# Filter down to active_titles
rating_std_by_place = rating_std_by_place.loc[active_place]
# Order Series by value in descending order
rating_std_by_place.sort_values(ascending=False)[:10]
```

```
placeID
134987    1.154701
135049    1.000000
134983    1.000000
135053    0.991031
135027    0.991031
132847    0.983192
132767    0.983192
132884    0.983192
135082    0.971825
132706    0.957427
Name: rating, dtype: float64
```

