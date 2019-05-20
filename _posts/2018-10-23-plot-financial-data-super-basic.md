---
layout: post
title:  "Plot Financial Data Using Matplotlib (super basic)"
date:   2018-10-23 21:30:09 +0900
comments: true
tags:
- programming
---

## import libraries
In order to plot the data, we need to import libraries for dataframe and plot, also set plot inline if you're  using a notebook.
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
```

## plot stock price
Code is super simple, you just need to set the index of the dataframe to timestamp. If you find the figure to small, use pylab to set the figure size.
```python
from pylab import rcParams
rcParams['figure.figsize'] = 50,13
apple_data = market_train_df[market_train_df['assetCode'] == 'AAPL.O']
apple_data.set_index('time')['close'].plot(grid = True)
```
<img src="/img/python-plot-financial-data-1.png" style="height:50%">

## compare multiple plots
Then I'm trying to sanitize the data by looking at the figure it self, I want to plot all suspicious assets.
```python
for code in suspicious_asset_code:
    apple_data = market_train_df[market_train_df['assetCode'] == code]
    apple_data.set_index('time')['close'].plot(grid = True)
```
<img src="/img/python-financial-plot-2.png" style="height:50%">

This only gives me one figure with all assets, it's ugly. I want to plot them one by one.

Subplot will give you figures put up together, use 
```python
# treat the whole figure as a grid, specify how many rows and columns you wanna plot and the index of the current sub plot
fig.add_subplot(row, columns, index)
```
Then you'll get graphs all together to detect abnormal data.
<img src="/img/python-plot-subplot.png" style="height:50%">
