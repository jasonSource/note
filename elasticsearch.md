### ES

- Es 索引默认5个分片

- 每个索引

- 节点：运行了单个实例的es主机节点,他是集群的一个成员，可以存储数据，参数集群索引及搜索操作

- 集群：es可以作为一个独立的单个搜索服务器，处理大型数据集，实现容错和高可用，被称为集群

- 分片：es的分片机制可将一个所以内的数据分布的存储于多个节点

- 副本：副本是一个分片的精确复制，每个分片可以有零个或多个副本

- 映射：映射是定义文档及其包含的字段如何存储和索引的过程

- - 哪些字符串字段应该被视为全文字段
  - 哪些字段包含数字、日期或地理位置
  - 文档中所有字段的值是否应该被索引到catch-all_all字段中
  - 日期值的格式
  - 用于控制动态添加字段的映射的自定义规则

- 数据类型

- - String和keyword都是存储字符串类型
  - - String存储后会分词，keyword不会进行分词

- _search 查询的结果

- - took：查询花费的时间，使用毫秒为单位
  - Time_out；查询是否超时boolean单位
  - _shards：多少个shard被查询，多少个被命中，多少个被跳过，多少个失败
  - Max_score：发现最相关文档的分数
  - Hits.total.value：查询出文档的个数
  - Hits.sort：文档的排序位置
  - Hits._score：文档的相关性分数

- From 对应mysql查询的offset，

- size 需要查询文档的个数

- 查询整个文档

~~~json
    GET /bank/_search
    {
      "query":{"match_all":{}},
      "sort":[
        {"account_number":"asc"}
      ],
      "from":10,
      "size":10
    }
~~~

- 查询文档添加条件

~~~json
GET /bank/_search
{
  "query":{"match":{"address":"mill lane"}}
}
~~~

- 使用短语查询（不进行分词）

~~~json
GET /bank/_search
{
  "query":{"match_phrase":{"address":"mill lane"}}
}
~~~

- 使用多个条件进行查询

~~~json
GET /bank/_search
{
  "query":{
    "bool":{
      "must":[
        {"match":{"age":"40"}}
      ],
      "must_not":[
        {"match":{"state":"ID"}}
      ]
    }
  }
}
~~~

- 限制多个条件范围查询

~~~json
GET /bank/_search
{
  "query":{
    "bool":{
      "must":{"match_all":{}},
      "filter":{
        "range":{
          "balance":{
            "gte":20000,
            "lte":30000
          }
        }
      }
    }
  }
}
~~~





