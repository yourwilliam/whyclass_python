# Pip

使用pip安装模块：

```bash
# 安装包
pip install PackageName

# 更新模块 (比较少使用，最好减少随意的升级包)
pip install -U PackageName

# 使用pip卸载模块：
pip unstall PackageName

# 查看已经过期的模块：
pip list --outdated

#  升级pip版本 （可以升级）
python -m pip install -U pip

# 将第三方库的版本降级，以selenium 选择制定版本安装
pip install selenium==3.8.1

# 查询库中的包版本，使用较多，用于需要一个包来查询库中的版本名字
pip serach PackageName

# 将当前环境已安装的软件包导出为 requirements.txt 方便后续安装
pip freeze ****

# 使用pip安装导出的依赖文件
pip install -r requirements.txt

# 使用第三方镜像安装

pip install PackageName -i https://mirrors.aliyun.com/pypi/simple
```

常用命令集：

install 安装软件包 download 下载软件包 uninstall 卸载软件包 freeze 导出已安装的包 list 列出已安装的软件包列表 show 查看已安装的包的信息 search 搜索软件包 wheel 按照要求导入建立wheels hash 计算软件压缩包的哈希 completion 用于补全pip命令的选项或参数 help 显示命令的帮助文档

