# pandas教程

## 数据结构

### pandas 数据结构 Series

Series是由一组数据与一组索引(行索引)组成的数据结构。

```py
# 创建一个Series，Series默认使用0开始的数做数据标签
s1 = pd.Series(["a","b","c"])
# 指定索引的创建Series
s2 = pd.Series([1,2,3,4], index=["a","b","c","d"])
# 使用字典创建Series
s3 = pd.Series({"a":1, "b":2, "c":3})
# 使用index获取Series的索引
s3.index
# 使用values获取Series的值
s3.values
```

### pandas数据结构 DataFrame

DataFrame是由一组数据与一对索引（行索引和列索引）组成的表格型数据结构。


```py
# 创建一个DataFrame，只传入一个单一列表时，该列表的值会显示成一列，且行和列都是从0开始的默认索引。
df1 = pd.DataFrame(["a", "b", "c", "d"])
```


```py
# 当传入一个嵌套列表时，会根据嵌套列表数显示成多列数据，行、列索引同样是从0开始的默认索引。
df2 = pd.DataFrame([["a","A"],["b","B"],["c","C"],["d","D"]])
```



```py
# 通过columns参数自定义列索引
df3 = pd.DataFrame([["a","A"],["b","B"],["c","C"],["d","D"]], columns=["小写","大写"])

# 通过字典传入
df4 = pd.DataFrame({"小写":["a","b","c","d"],"大写":["A","B","C","D"]})

# 指定索引
df5 = pd.DataFrame({"小写":["a","b","c","d"],"大写":["A","B","C","D"]}, index=["一","二","三","四"])

```


```py
# 利用index方法获取DataFrame的行索引
df2.index
```

## 导入外部数据

### 导入excel
```py
# 通过read_excel可以将excel读入成为DataFrame
df = pd.read_excel("file_path")
# 指定sheet导入
df1 = pd.read_excel("file_path", sheet_name="Sheet1")
# 通过sheet的顺序传入
df1 = pd.read_excel("file_path", sheet_name=0)
# 指定行索引，index_col默认为0，指定第几列作为行索引。
df1 = pd.read_excel("file_path", sheet_name=0, index_col=0)
# 指定列索引，指定第几列作为列索引，默认第0列
df1 = pd.read_excel("file_path", sheet_name=0, header=0)
# 通过usecols来指定要导入的列,指定多个值可以导入多个列
df1 = pd.read_excel("file_path", usecols=0)
df1 = pd.read_excel("file_path", usecols=[0,2,3])
```

### 导入csv


```py
df = pd.read_csv("file_path")
# 指定分隔符，默认是逗号
df = pd.read_csv("file_path", sep=",")
# 指定读取行数
df = pd.read_csv("file_path", sep=",", nrows=0)
# 指定编码格式，默认使用utf-8
df = pd.read_csv("file_path", sep=",", encoding="utf-8")
```

### 导入TXT


```py
df = pd.read_table("file_path")
# 具体参数和csv类似
```

### 导入sql

#### mysql

```py
import pymysql

sql = "select * from table_name"
eng = pymsql.connect("127.0.0.1","username","password","dbname",charset="utf-8")
df = pd.read_sql(sql,eng)
```

#### postgresql

读取postgres

```py
import psycopg2
import pandas as pd

# postgres config
postgres_host = "47.102.137.93"               # 数据库地址
postgres_port = "5432"       # 数据库端口
postgres_user = "collapsar"              # 数据库用户名
postgres_password = "Collapsar2020"      # 数据库密码
postgres_datebase = "collapsar"      # 数据库名字
postgres_table1 = "qs_ranking_topuniversities"           #数据库中的表的名字

conn_string = "host=" + postgres_host + " port=" + postgres_port + " dbname=" + postgres_datebase + \
              " user=" + postgres_user + " password=" + postgres_password
conn = psycopg2.connect(conn_string)

sql_command1 = "select * from {}" .format(postgres_table1)

try:
    data = pd.read_sql(sql_command1, conn)
except:
    print("load data from postgres failure !")
    exit()
print(data)
```

## 整理数据

```py
# 默认显示5行
df.head()
# 显示前2行
df.head(2)
# shape方法以元组的形式返回行、列数
df.shape
(4,4)
# info()方法会输出整个表中所有列的数据类型
df.info()
# 获取数值字段类型的分布值。 只会获取数值字段
df.describe()

# 删除含有NaN值的行，返回删除后的数据
df.dropna()
# 删除空白行，只会删除那些全为空值的行
df.dropna(how="all")

```

### 数据填充

```py
# 将所有NAN数据填充0
df.fillna(0)

df.fillna({"性别":"男","年龄":"30"})

```

### 删除重复值

```py
# 默认对所有值进行重复判断，且默认保留第一行
df.drop_duplicates()
# 针对一列的重复值进行判断
df.drop_duplicates(subset="列名")
# 针对多列的重复值进行判断
df.drop_duplicates(subset=["列名1", "列名2"])
# keep的默认值是first，默认保留第一行，可以改为last，保留最后一行
df.drop_duplicates(subset=["列名1", "列名2"], keep="last")
# 如果设置为false则删除所有的
df.drop_duplicates(subset=["列名1", "列名2"], keep=False)
```

### pandas数据类型

* int：整数型
* float
* object: python对象类型，用O表示
* string_ : 字符串类型，用S表示，S10表示长度为10的字段
* unicode_ : 固定长度的Unicode类型，跟字符串定义方式一样
* datetime64[ns]: 时间格式

```py
# 获取某一列的数据类型
df['列名1'].dtype
# 将唯一识别码从int类型转化为float类型
df['列名1'].astype('float64')
```

数据类型

```py
Data type   Description
bool_   Boolean (True or False) stored as a byte
int_    Default integer type (same as C long; normally either int64 or int32)
intc    Identical to C int (normally int32 or int64)
intp    Integer used for indexing (same as C ssize_t; normally either int32 or int64)
int8    Byte (-128 to 127)
int16   Integer (-32768 to 32767)
int32   Integer (-2147483648 to 2147483647)
int64   Integer (-9223372036854775808 to 9223372036854775807)
uint8   Unsigned integer (0 to 255)
uint16  Unsigned integer (0 to 65535)
uint32  Unsigned integer (0 to 4294967295)
uint64  Unsigned integer (0 to 18446744073709551615)
float_  Shorthand for float64.
float16 Half precision float: sign bit, 5 bits exponent, 10 bits mantissa
float32 Single precision float: sign bit, 8 bits exponent, 23 bits mantissa
float64 Double precision float: sign bit, 11 bits exponent, 52 bits mantissa
complex_    Shorthand for complex128.
complex64   Complex number, represented by two 32-bit floats (real and imaginary components)
complex128  Complex number, represented by two 64-bit floats (real and imaginary components)
```

### 添加索引

```py
# 给表传入列索引
df.columns = ["列名1", "列名2", "列名3"]
# 给表添加行索引，这里也可以添加其它值字段
df.index = [1,2,3,4,5,6]
# 重新设置索引列，在set_index()里指定要用做行索引的列名
df.set_index("列名1")
# 使用rename，使用一个dictionary来新
df.rename(columns = {"列名1":"新列1", "列名2":"新列名2"})
# 使用rename来设置行名
df.rename(index = {1:"一",2:"二",3:"三"})
```

## 数据选择(重要部分)

几种数据选择方法：

loc:通过选取行（列）标签索引数据
iloc:通过选取行（列）位置编号索引数据
ix:既可以通过行（列）标签索引数据，也可以通过行（列）位置编号索引数据

```py
# 获取一列
df["列名1"]
# 获取多列
df[["列名1","列名2","列名3"]]
# 通过iloc来查找具体列，获取第一列和第三列的数值。
# iloc的两个元素分别代表行，列。
df.iloc[:, [0,2]]
# 可以使用切片的方式来选择第一列和第四列的值
df.iloc[:, 0:3]
# 选择一行
df.loc["一"]
# 选择多行
df.loc[["一","二","三"]]
# 可以支持列表和切片方式来选择多个行和列
df.iloc[0]
df.iloc[[0,1]]
df.iloc[0:2]
# 选择年龄小于200的
df[df["年龄"]<200]
# 可以使用&来结合多个条件
df[ (df["年龄"]<200) & (df["唯一识别码"]<100) ]
# 交叉行列选择
df.loc[["一","二"],["列名1","列名2"]]
df.iloc[[1,2],[0,2]]
# 布尔索引+普通索引
df[df["rank"]<20][["title","country"]]
df.iloc[0:2,1:2]
df.ix[0:2, ["列名1","列名2"]]

```

###数值替换

```py
# 将一列的值由240替换为33
df["列名"].replace(240,33)
df.replace(np.NAN, 0)
# 多列替换
df.replace([240,280,260], 33)
df.replace({240:33, 260:33, 280:36})
```

### 排序

```py
#
df.sort_values(by=["列名"])
# ascending 默认值为True，表示升序排列。False表示降序排列
df.sort_values(by=["列名"], ascending=False)

df.sort_values(by=["列名"], ascending=False, na_position="first")
```
