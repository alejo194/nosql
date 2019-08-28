#### 索引（Index）
1、索引的基础知识： Index </br>
   (1) 默认索引：_id(唯一性的索引) </br>
       db.emp.getIndexes()
   (2)查询：部门号等于10，工资小于3000的文档
   
       db.emp.find({deptno:{$eq:10},sal:{$lt:3000}}) --->全表扫描
       db.emp.find({deptno:{$eq:10},sal:{$lt:3000}}).explain()
       "winningPlan":{
             "stage": "COLLSCAN",
             ......
       }
       
   (3)创建索引
   
       db.emp.createIndex({"deptno":1, "sal":1})
       "winningPlan":{
             "stage": "FETCH",
             "inputStage":{
                  "stage": "IXSCAN",
                  ......
       }
       
2、索引的类型一： 单键索引 </br>
3、索引的类型二： 多键索引 </br>
4、索引的类型三： 复合索引 </br>
5、索引的类型四： 过期索引 </br>
6、索引的类型五： 全文索引 </br>
7、索引的类型六： 地理位置索引 </br>
