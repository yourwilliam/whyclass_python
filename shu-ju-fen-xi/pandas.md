# pandas

## 安装

Terminal中运行，注意请确保前面的虚拟环境

```bash
# 安装numpy
(venv)$ pip install numpy -i https://mirrors.aliyun.com/pypi/simple
# 安装pandas
(venv)$ pip install pandas -i https://mirrors.aliyun.com/pypi/simple

(venv)$ pip install matplotlib -i https://mirrors.aliyun.com/pypi/simple
```

## 数据导入

```python
df = pd.read_excel('../uva_course_spider/session_all.excel')
#指定导入sheet
df = pd.read_excel('../uva_course_spider/session_all.excel', sheet_name='Sheet1')
#按照个数指定sheet和索引列，使用None为默认第一行
df = pd.read_excel('../uva_course_spider/session_all.excel', sheet_name=0, header=0)
#指定导入列
df = pd.read_excel('../uva_course_spider/session_all.excel', usecols=[0,2])

#导入csv文件
df = pd.read_csv('../uva_course_spider/session_all.csv', header=None, sep=',')
#指定导入行数
df = pd.read_csv('../uva_course_spider/session_all.csv', header=None, sep=',', nrows=2,encoding='utf-8')
```

## Viewing data

```python
# 显示数据的头几行
df.head()
# 显示数据的尾行
df.tail(3)
# 显示行索引
df.index
# 显示列索引
df.columns
# 转化为矩阵
df.to_numpy()
```

## DataFrame

```python
#选择某些列
>>> df.iloc[:,[5,8]]
#选择连续列
>>> df.iloc[:,5:8]

#选择行
>>> df.iloc[0]
#选择某些行
>>> df.iloc[[1,4]]
#选择某几个连续行
>>> df.iloc[[1:4]]
```

```python
# 过滤行
>>> df[df[5] != 'Staff']
# 过滤行后选择列
>>> df[df[5] != 'Staff'][5]
# 等同于
>>> df[df[5] != 'Staff'].iloc[:,5]
```

### Missing Data

```python
# 删除NA
df1.dropna(how='any')
# 填充NA
df1.fillna(value=5)
# 判断是否是NA
pd.isna(df1)
```

### 数据可视化

安装matplotlib

```bash
$ pip install matplotlib -i https://mirrors.aliyun.com/pypi/simple
```

### 数据导出

## 相关教材

[numpy官方文档](https://www.numpy.org.cn/)

[pandas官网](https://pandas.pydata.org)

[pandas官方教材](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html)

[pandas cheat sheet](https://myslide.cn/slides/12068)

[Matplotlib 中文文档](https://www.matplotlib.org.cn/index.html)

