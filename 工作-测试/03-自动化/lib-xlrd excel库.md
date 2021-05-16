#### 安装

```
pip install xlrd
```



#### 使用

```python
import xlrd

xls = xlrd.open_workbook(filename)
```



#### 常用参数

```python
xls.sheet_names() # excel所有的sheet名称
sheet = xls.sheets()[index] # 指定一个sheet
sheet.name # 获取sheet名称
sheet.ncols # 获取sheet列数
sheet.nrows # 获取sheet行数
sheet.row_values(idnex) # 获取指定索引行数据
sheet.clo_values(index) # 获取指定索引列数据
sheet.row(3)[4].value # 第4行，第5列的数据
# 遍历的方式可以获取数据
```

