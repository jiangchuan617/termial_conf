# pandas 格式说明

## s索引格式

### Series索引



```python
# 列索引
s[0:20]
# 时间索引
detect_time_start = pd.to_datetime("2019-01-01 08")
detect_time_end = pd.to_datetime("2019-01-01 20")
s[detect_time_start:detect_time_end]
```

### DataFrame索引

```python
# 行索引
df.loc[pd.to_datetime("2019-01-01 00:00:00")]
# 行间隔索引
df[::60]
# 列索引
df.loc[:,["溢流浓度"]]
df["溢流浓度"] == df.loc[:,"溢流浓度"]

```



## 时间格式

```python
# pd时间格式
detect_time_start = pd.to_datetime("2019-01-01 08")
detect_time_end = pd.to_datetime("2019-01-01 20")

# 生成等间隔的时间index
s_date_str = "2019-01-01"  # 统计的开始时间
e_date_str = "2019-01-31"  # 统计的结束时间
s_time_str = s_date_str + " 08:00:00"
e_time_str = e_date_str + " 23:59:59"
date_time_b = pd.date_range(s_time_str, e_time_str, freq='12H')  # DatetimeIndex

```



## 保存与读取

```python
# csv
df.to_csv("df.csv",columns=None, header=True, index=False)
pd.read_csv("df.csv")
# hdf5
df.to_hdf('df19.h5', key='df', mode='w')
df= pd.read_hdf('df19.h5', 'df')
```



## 画图格式

```python
s = df.loc[:,["溢流浓度"]]
s.plot()
s['溢流浓度'].hist(bins=50)
```



## 修正时间

```python
index_amend = old_index + pd.Timedelta(hours=8)
df = df.reindex(index_amend)
```

