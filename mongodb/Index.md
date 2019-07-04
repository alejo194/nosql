#### MongoDB 索引
在MongoDB中索引支持高效执行查询。如果没有索引，MongoDB必须执行集合扫描，即扫描集合中的每个文档，以选择哪些匹配查询语句的文档。如果查询存在适当的索引，MongoDB可以使用该索引来限制它必须检查的文档数量。</br>
索引是一种特殊的数据结构[1]，它以一种易于遍历的形式存储集合数据集的一小部分。索引存储特定字段或一组字段的值，按字段的值排序。索引条目的排序支持高效的相等匹配和基于范围的查询操作。此外，MongoDB可以使用索引中的顺序返回排序后的结果。</br>

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
     支持item字段查询或item和stock字段查询
     > db.products.find( { item: "Banana" } )
     > db.products.find( { item: "Banana", stock: { $gt: 5 } } )
     
     排序顺序
     索引以升序(1)或降序(-1)排序顺序存储对字段的引用。对于单字段索引，键的排序顺序并不重要，因为MongoDB可以在任意方向遍历索引。
     但是，对于复合索引，排序顺序对于决定索引是否支持排序操作很重要。
     > db.events.find().sort({username: 1,date: -1})
     或
     > db.events.find().sort({username: -1,date: 1})
     下面的索引都支持上面操作
     > db.events.createIndex({"username": 1, "date": -1})
     但是上面的索引不支持username升序排序和data升序排序，如下
     > db.events.find().sort({username: 1, date: 1})
     
     前缀
     索引前缀是索引字段的开始子集。例如，考虑以下复合索引:
     { "item": 1, "location": 1, "stock": 1 }
     索引有以下前缀索引：
     { item: 1 }
     { item: 1, location: 1 }
     但是，MongoDB不能使用索引来支持包含以下字段的查询，因为没有item字段，列出的字段中没有一个对应于前缀索引:
     location字段
     stock字段
     location和stock字段
     
##### 3. Multikey Indexes
    要索引包含数组值的字段，MongoDB为数组中的每个元素创建索引键。这些多键索引支持对数组字段的高效查询。多键索引可以在数组上构造，
    数组既包含标量值[1](例如字符串、数字)，也包含嵌套文档。
    
    3.1 创建多值索引
    > db.coll.createIndex({<field>: <1 or -1>})
    如果任何索引字段是数组，MongoDB会自动创建一个多键索引;您不需要显式地指定多键类型。
    
    3.2 索引范围
    
    3.3 唯一多键索引
    对于惟一索引，惟一约束适用于集合中不同的文档，而不是单个文档中。
    
    3.4 限制
    
    3.5 复合多键索引
    对于复合多键索引，每个索引文档最多只能有一个索引字段，其值为数组。
    如果文档中有多个要索引的字段是数组，则不能创建复合多键索引，例如：
    { _id: 1, a: [ 1, 2 ], b: [ 1, 2 ], category: "AB - both arrays" }
    
    但是，在创建复合多键索引之后，如果您试图插入一个a和b字段都是数组的文档，MongoDB将无法插入。
    
    如果字段是文档数组，则可以为嵌入的字段建立索引，以创建复合索引。例如，考虑一个包含以下文档的集合:
    { _id: 1, a: [ { x: 5, z: [ 1, 2 ] }, { z: [ 1, 2 ] } ] }
    { _id: 2, a: [ { x: 5 }, { z: 4 } ] }
    可以在{ "a.x": 1, "a.z": 1 }创建复合索引
    
    3.6 排序
    
    3.7 分片键
    你不能指定一个多键索引作为分片键索引
    
    3.8 Hashed 索引
    Hashed 索引不能是多键的
    
    3.9 覆盖查询
    多键索引不能覆盖数组字段上的查询。
    
    3.10 查询整个数组字段
    
    3.11 $expr
    $expr 不支持多键索引。
    
    3.11 嵌入文档的索引数组
    可以在包含嵌套对象的数组字段上创建多键索引。
    {
    _id: 1,
    item: "abc",
    stock: [
    { size: "S", color: "red", quantity: 25 },
    { size: "S", color: "blue", quantity: 10 },
    { size: "M", color: "blue", quantity: 50 }
    ]
    }
    {
    _id: 2,
    item: "def",
    stock: [
    { size: "S", color: "blue", quantity: 20 },
    { size: "M", color: "blue", quantity: 5 },
    { size: "M", color: "black", quantity: 10 },
    { size: "L", color: "red", quantity: 2 }
    ]
    }
    {
    _id: 3,
    item: "ijk",
    stock: [
    { size: "M", color: "blue", quantity: 15 },
    { size: "L", color: "blue", quantity: 100 },
    { size: "L", color: "red", quantity: 25 }
    ]
    }
    ...
    
    创建多键索引
    > db.inventory.createIndex({"stock.size":1, "stock.quantity":1})
    
    > db.inventory.find( { "stock.size": "M" } )
    > db.inventory.find( { "stock.size": "S", "stock.quantity": { $gt: 20 } } )
    复合多键索引还可以支持排序操作
    > db.inventory.find( ).sort( { "stock.size": 1, "stock.quantity": 1 } )
    > db.inventory.find( { "stock.size": "M" } ).sort( { "stock.quantity": 1 } )
    
##### 4. Text Indexes
##### 5. 2dsphere Indexes
##### 6. 2d Indexes
##### 7. geoHaystack Indexes
##### 8. Hashed Indexes
