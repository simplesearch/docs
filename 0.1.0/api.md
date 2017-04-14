

### 1. 搜索接口
- POST /rest/search
- test: http://localhost/rest/search?alias=lagou&query=ElasticSearch

Name | Required | Description | Schema | Default
---|---|---|---|---
alias | 是 | 搜索配置别名 | string | 
query | 是 | 搜索关键词 | string | 
from |  | 分页，从第几条开始读 | integer | 0
size |  | 分页，每页数量 | integer | 40
sort |  | 排序规则，字段:排序，多个字段用逗号分隔 | string | 

- SearchResponse

Name | Description | Schema | Default
---|---|---|---
time | 搜索耗时 | integer | 
total | 搜索总数 | integer | 
result | 搜索结果 | < Map«string,object» > array | 


### 2. 智能提示接口
- POST /rest/suggest
- test: http://localhost/rest/suggest?index=lagou&suggest=s

Name | Required | Description | Schema | Default
---|---|---|---|---
alias | 是 | 索引别名 | string | 
query | 是 | 搜索关键词 | string | 

- SuggestResponse

Name | Description | Schema | Default
---|---|---|---
time | 搜索耗时 | integer | 
total | 搜索总数 | integer | 
result | 搜索结果 | < Map«string,Integer» > array | 

### 3. 索引接口
- POST /rest/index
- test: http://localhost/rest/index

Name | Required |Description | Schema | Default
---|---|---|---|---
index | 是 | 索引名称 | string | 
_id | 是 | 唯一id | string | 
row | 是 | 索引内容,不能包含_id的key，如果包含会被此接口执行的时候删除，并且打出WARN日志 | Map<String,Object> | 


### 4. 批量索引接口
- POST /rest/bulk
- test: http://localhost/rest/bulk

Name | Required | Description | Schema | Default
---|---|---|---|---
index | 是 | 索引名称 | string | 
array | 是 | 索引内容,必须包含_id的key，如果任意一条数据不包含，此接口不会执行并且返回错误信息 | List<Map<String,Object>> | 


### 5. 删除索引接口
- POST /rest/delete
- test: http://localhost/delete?index=lagou&_id=xxxxxxxxxxxxxxxx

Name | Required | Description | Schema | Default
---|---|---|---|---
index | 是 | 索引名称 | string | 
_id | 是 | 根据_id删除索引记录 | string | 




> index ， bulk ， delete 接口统一返回

Name | Description | Schema | Default
---|---|---|---
error | true: 接口执行错误, false: 接口执行成功 | boolean | 
errorMsg | 错误消息 | String |


