# 第一期分组

课题一:字典生成工具 dicgen
1. 新建数据库表
    1. 数据库表结构设计
    2. 通过不同的参数写入到不同的库中
2. 对接第三方翻译系统——第三方接口
    1. 获取词形词性
    2. 翻译
    3. 语音(MP3读音)
3. excel --> 数据库
    1. 数据库新建张表
    2. excel和数据库对应
    3. 写入数据库
4. 字典的相关功能操作
    1. 查询单词，各种查询方式
    2. 排序导出功能
5. 数据库导出Excel（学习如何使用excel）
    1. 查询部分功能
    2. 按照要求导出Excel


课题二：词频统计工具 freany
1. 文件夹中存储文章(word模式)
2. 读取文章存入数据库
    1. 设计数据库
        1. 考试类型(雅思、托福)
        2. 材料类型(真题、官方教辅、第三方资料书籍)
        3. 大家一起补充
3. 选择范围统计词频
    1. 可以为不同的材料类型设置权重
    2. 通过SQL选择不同的考试来分析词频
4. 不同的源的词频统计


课题三：ANKI导出工具 ankigen
1. 数据库内容按照参数需要读取
    1. 设计读取参数，按照不同类型读取
2. 读取字典内容写入队列
3. 导出成为ANKI使用的XML格式
4. 导入ANKI形成可背诵部分
5. 通过背诵的单词反馈数据库：
    1. 让各个学生背诵单词
    2. 获取单词难易程度和背诵情况
    3. 导出包含学习进度信息
    4. 反写回数据库
    5. 记录词频分析情况