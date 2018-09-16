# Financial-Data

import pandas as pd
from pandas_datareader import data as pdr # 直接使用yahoo的資料所以再加上這行
import fix_yahoo_finance as yf # pip install fix_yahoo_finance
import datetime

yf.pdr_override()
DAX = pdr.get_data_yahoo('2330.TW', start = datetime.datetime(2017, 7, 26))
DAX.info()

## 收盤價
DAX['Close'].plot(figsize=(8,5))

## 移動平均線
DAX['5d'] = pd.rolling_mean(DAX['Close'], window=5)
DAX['60d'] = pd.rolling_mean(DAX['Close'], window=60)
DAX['144d'] = pd.rolling_mean(DAX['Close'], window=144)

DAX[['Close','5d','60d','144d']].tail()

DAX[['Close','5d','60d','144d']].plot(figsize=(8,5))
