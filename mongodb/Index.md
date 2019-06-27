#### MongoDB 索引
    索引的类型：Single Field Indexes, Compound Indexs, Multikey Indexes, Text Indexes, 2dsphere Indexes, 2d Indexes,
                geoHaystack Indexes, Hashed Indexes
     
##### 1. Single Field Indexes
    MongoDB提供了对文档集合中任何字段上的索引的完整支持。默认情况下，所有集合在_id字段上都有一个索引，应用程序和用户可以添加
    额外的索引来支持重要的查询和操作。本文档描述单个字段上的升序/降序索引。
    
    {
    "_id": ObjectId("570c04a4ad233577f97dc459"),
    "score": 1034,
    "location": { state: "NY", city: "New York" }
    }
    
    在records集合中的score字段上创建一个升序的索引
    > db.records.createIndex( { score: 1 } )
    索引规范中字段的值描述了该字段的索引类型。1代表升序，-1代表降序 
    在score字段上创建的索引将支持查询
    > db.records.find({score:2})
    > db.records.find({score:{$gt:10}})
    
    在一个嵌入式字段创建索引
    > db.records.createIndex({"lacation.state":1})
    在location.state字段上创建的索引支持查询
    > db.records.find({"location.state":"CA"})
    > db.records.find({"location.city":"Albany",  "location.state": "NY"})
    
    在一个嵌入式文档上创建索引
    > db.records.createIndex({location:1})
    下面的查询可以使用location字段上的索引
    > db.records.find({location:{city:"New York", state:"NY"}})
    注：当对嵌入的文档执行相等匹配时，字段顺序很重要，并且嵌入的文档必须完全匹配。   
    
##### 2. Compound Indexs
    MongoDB支持复合索引，其中一个索引结构包含对集合文档中的多个字段[1]的引用。
    MongoDB对任何复合索引施加32个字段的限制。
    复合索引支持多个字段的查询
    
    创建一个复合索引
    db.collection.createIndex({<field1>:<type>, <field2>:<type2>, ...})
    ****注：不能创建具有散列索引类型的复合索引****
    
    products集合
    {
     "_id": ObjectId(...),
     "item": "Banana",
     "category": ["food", "produce", "grocery"],
     "location": "4th Street Store",
     "stock": 4,
     "type": "cases"
     }
     
     在item和stock字段上创建升序索引
     > db.products.createIndex({"item":1, "stock":1})
     
##### 3. Multikey Indexes
##### 4. Text Indexes
##### 5. 2dsphere Indexes
##### 6. 2d Indexes
##### 7. geoHaystack Indexes
##### 8. Hashed Indexes
