学习笔记  
运行 target_encoding_v1_exercise.py 输出的统计结果。
```text
/Users/justdoit/.pyenv/versions/3.8.6/bin/python "/Volumes/SanDisk1T/Google 云端硬盘/Colab Notebooks/ml-training-camp/chap02/target_encoding/target_encoding_v1_exercise.py"
Timer unit: 1e-06 s

Total time: 3.75616 s
File: /Volumes/SanDisk1T/Google 云端硬盘/Colab Notebooks/ml-training-camp/chap02/target_encoding/target_encoding_v1_exercise.py
Function: target_mean_v1 at line 7

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
     7                                           def target_mean_v1(data, y_name, x_name):
     8         1         58.0     58.0      0.0      result = np.zeros(data.shape[0])
     9       501        732.0      1.5      0.0      for i in range(data.shape[0]):
    10       500    3155764.0   6311.5     84.0          groupby_result = data[data.index != i].groupby([x_name], as_index=False).agg(['mean', 'count'])
    11       500     599606.0   1199.2     16.0          result[i] = groupby_result.loc[groupby_result.index == data.loc[i, x_name], (y_name, 'mean')]
    12         1          1.0      1.0      0.0      return result

Timer unit: 1e-06 s

Total time: 0.066865 s
File: /Volumes/SanDisk1T/Google 云端硬盘/Colab Notebooks/ml-training-camp/chap02/target_encoding/target_encoding_v1_exercise.py
Function: target_mean_v2 at line 15

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
    15                                           def target_mean_v2(data, y_name, x_name):
    16         1         20.0     20.0      0.0      result = np.zeros(data.shape[0])
    17         1          1.0      1.0      0.0      value_dict = dict()
    18         1          1.0      1.0      0.0      count_dict = dict()
    19       501        279.0      0.6      0.4      for i in range(data.shape[0]):
    20       500       9789.0     19.6     14.6          if data.loc[i, x_name] not in value_dict.keys():
    21        10        619.0     61.9      0.9              value_dict[data.loc[i, x_name]] = data.loc[i, y_name]
    22        10        211.0     21.1      0.3              count_dict[data.loc[i, x_name]] = 1
    23                                                   else:
    24       490      18237.0     37.2     27.3              value_dict[data.loc[i, x_name]] += data.loc[i, y_name]
    25       490       9514.0     19.4     14.2              count_dict[data.loc[i, x_name]] += 1
    26       501        295.0      0.6      0.4      for i in range(data.shape[0]):
    27       500      27898.0     55.8     41.7          result[i] = (value_dict[data.loc[i, x_name]] - data.loc[i, y_name]) / (count_dict[data.loc[i, x_name]] - 1)
    28         1          1.0      1.0      0.0      return result

Timer unit: 1e-06 s

Total time: 0.001862 s
File: /Volumes/SanDisk1T/Google 云端硬盘/Colab Notebooks/ml-training-camp/chap02/target_encoding/target_encoding_v1_exercise.py
Function: target_mean_v3 at line 31

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
    31                                           def target_mean_v3(y_np, x_np):
    32         1          3.0      3.0      0.2      length = y_np.shape[0]
    33         1         29.0     29.0      1.6      result = np.zeros(length)
    34         1          3.0      3.0      0.2      value_dict = defaultdict(int)
    35         1          1.0      1.0      0.1      count_dict = defaultdict(int)
    36       501        170.0      0.3      9.1      for i in range(length):
    37       500        436.0      0.9     23.4          value_dict[x_np[i]] += y_np[i]
    38       500        333.0      0.7     17.9          count_dict[x_np[i]] += 1
    39       501        175.0      0.3      9.4      for i in range(length):
    40       500        712.0      1.4     38.2          result[i] = (value_dict[x_np[i]] - y_np[i]) / (count_dict[x_np[i]] - 1)
    41         1          0.0      0.0      0.0      return result

0.0
```
