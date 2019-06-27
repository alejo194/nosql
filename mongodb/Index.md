#### MongoDB 索引
     索引的类型：Single Field Indexes, Compound Indexs, Multikey Indexes, Text Indexes, 2dsphere Indexes, 2d Indexes, geoHaystack Indexes, Hashed Indexes
     
##### Single Field Indexes
    MongoDB提供了对文档集合中任何字段上的索引的完整支持。默认情况下，所有集合在_id字段上都有一个索引，应用程序和用户可以添加额外的索引来支持重要的查询和操作。
    本文档描述单个字段上的升序/降序索引。
    
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
    
    
##### Compound Indexs
##### Multikey Indexes
##### Text Indexes
##### 2dsphere Indexes
##### 2d Indexes
##### geoHaystack Indexes
##### Hashed Indexes
