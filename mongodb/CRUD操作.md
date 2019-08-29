1.插入文档：insert 如果插入数据的时候，collection还不存在，会自动创建集合

2.查询文档：
    db.collection.find(query,projection)
    query--document类型：可选，使用查询操作符指定查询条件
    projection--document类型：指定使用投影运算符返回的字段省略此参数返回匹配文档中的所有字段
    projection语法：
        {field1:<boolean>, field2:<boolean> ...}
    说明：
        1或者true表示返回字段
        0或者false表示不返回字段
        _id：默认就是1，没指定返回该字段时，默认会返回，除非设置为0时，就不会返回该字段。
        参考：https://blog.csdn.net/congcong68/article/details/46841075# </br>
             https://blog.csdn.net/congcong68/article/details/46919227</br>

3.更新文档：

4.删除文档：

5.批处理：
