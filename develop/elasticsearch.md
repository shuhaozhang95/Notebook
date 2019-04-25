### Elastic Search

Elasticsearch是一个全文搜索引擎，用 JAVA编写的，内部使用Lucene做索引与搜索，并且提供一套简单一直的RESTful API。

一个分布式的实时文档存储，每个字段可以被索引与搜索

一个分布式实时分析搜索引擎

能够胜任上百个服务节点的扩展，并支持PB级别的结构化或者非结构化数据。



Elasticsearch使用JavaScript Object Notation或者JSON作为文档的序列化格式。JSON序列化被大多数编程语言所支持，并且已经成为NoSQL领域的标准格式。



##### 基本操作

*索引*

```js
PUT /megacorp（索引名称）/employee（类型名称）/1（ID）
{
    "first_name" : "John",
    "last_name" :  "Smith",
    "age" :        25,
    "about" :      "I love to go rock climbing",
    "interests": [ "sports", "music" ]
}
```

*检索*

```js
GET /megacorp（索引库）/employee（类型）/1（ID）
```

*轻量搜索*

涉及到查询字符串（_query-string_）搜索，我们通过一个URL参数来传递查询信息给搜索接口

```jsx
GET /megacorp/employee/_search?q=last_name:Smith
```

*查询表达式搜索*

支持更加复杂的查询。领域特定语言（DSL），指定了使用以一个JSON请求。请求体由JSON构造，并使用了一个match查询。

```js
GET /megacorp/employee/_search
{
    "query" : {
        "match" : {
            "last_name" : "Smith"
        }
    }
}
```

*更复杂搜索*

可以在表达式搜索的基础上 增加filter过滤器

```js
GET /megacorp/employee/_search
{
    "query" : {
        "bool": {
            "must": {
                "match" : {
                    "last_name" : "smith" 
                }
            },
            "filter": {
                "range" : {
                    "age" : { "gt" : 30 } 
                }
            }
        }
    }
}
```

*全文搜索*（使用about）

```js
GET /megacorp/employee/_search
{
    "query" : {
        "match" : {
            "about" : "rock climbing"
        }
    }
}
```

短语搜索（用match_phrase）

```js
GET /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    }
}
```

高亮搜索（使用highlight使得搜索内容中高亮显示被选中的原因）

```js
GET /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    },
    "highlight": {
        "fields" : {
            "about" : {}
        }
    }
}
```

分析（groupby的功能）

```js
GET /megacorp/employee/_search
{
  "aggs": {
    "all_interests": {
      "terms": { "field": "interests" }
    }
  }
}
```

