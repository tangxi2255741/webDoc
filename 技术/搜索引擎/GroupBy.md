Post请求：172.28.159.62:30000/ivc-order/order/_search（索引/type/）

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "saler": "shzq"
          }
        }
      ],
      "must_not": [],
      "should": []
    }
  },
  "from": 0,
  "size": 0,
  "sort": [],
  "aggs": {
    "pin": {
      "terms": {
        "size": 50,
        "field": "pin"
      }
    }
  }
}
```

