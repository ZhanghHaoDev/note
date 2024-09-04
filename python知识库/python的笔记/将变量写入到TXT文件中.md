# 将变量写入到TXT文件中

```python
fileft = open("ft.txt", "w") # fileft:变量名称，ft.txt:文件名称，r（读）、w（写）、a（追加）
for i in range(ft.shape[0]): # 该变量是二维数组
    for j in range(ft.shape[1]):
        fileft.write(str(ft[i][j]) + "\n")
fileft.close() # 关闭文件
```

这里需要注意的是不要将创建文件的代码写道循环中，否则会使得文件重复创建，造成数据丢失