# 鱼课堂字典项目v1.0版本执行帮助文档 


## 程序一：Dictionary Import

```
--username youyu --password ****** --filepath D:\share\dic.xlsx
```

步骤：
1. 创建一个文件目录，创建一个xlsx文件，作为导入的字典表文件，字典表文件必须包含单词列表项
2. 修改文件中的参数 `df = pd.read_excel(filename, sheet_name=3, index_col=1, usecols=[0, 2], nrows=5)` 其中sheetname需要按照自己的excel格式修改，nrows需要按照自己的要求修改查询
3. 在run参数中添加如下参数。然后运行即可

## 程序二：Frequency Analysis

```
--username root --password ****** --table_name cet4freq --directory "D:\ydic"
```

步骤：
1. 创建ydic文件夹，在文件夹中添加TXT文档，将所有需要记录词频的工具加入到TXT文档中，所有文档使用txt保存
2. 修改参数中的table_name 和 directory 为自己的配置
3. 在run参数中添加如下参数，然后运行即可


## 程序三：ANKI TOOLS

```
--username root --password ****** --table_name dictest --filepath d:\share\anki.txt
```

步骤：
1. 创建文件目录 d:\share\ ， 也可以自己创建
2. 在数据库中找到需要导出的字典库内容，选择相应的表名
3. 在run参数中添加上面参数，然后运行即可。