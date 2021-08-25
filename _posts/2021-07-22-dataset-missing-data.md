---
title: Dataset - fix missing values
author: Hahunavth
date: 2121-07-22 11:00:00 +0700
categories: [Machine Learning, Preprocessor]
tags: [code, Python]
---


```python
# Handle missing data
import pandas as pd
import numpy as np
from sklearn.impute import SimpleImputer
import matplotlib.pyplot as plt

# print all result (defalut is last result)
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```


```python
# Read csv
imputer = SimpleImputer(missing_values=np.nan, strategy="mean")

dataframe = pd.read_csv('libreMissingData.csv', header=None)
print(dataframe)

data = dataframe.values
imputer.fit(data)
result = imputer.transform(data)
print(data)
print(result)
```

          0   1
    0   1.0   3
    1   NaN   5
    2   8.0   9
    3  10.0  15





    SimpleImputer()



    [[ 1.  3.]
     [nan  5.]
     [ 8.  9.]
     [10. 15.]]
    [[ 1.          3.        ]
     [ 6.33333333  5.        ]
     [ 8.          9.        ]
     [10.         15.        ]]



```python
# Graph
X = result[:, 0]
y = result[:, 1]
plt.scatter(X, y)
plt.show()
```




    <matplotlib.collections.PathCollection at 0x7f43b68284c0>





![png](/assets/post/missingData_files/missingData_2_1.png)
