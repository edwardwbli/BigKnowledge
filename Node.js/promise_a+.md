#[Promise A Plus](https://cnodejs.org/topic/560dbc826a1ed28204a1e7de)
Key: 
>回调，callback,promise/a+规范,then

Abstract: 
>Promise表示一个异步操作的最终结果。与Promise最主要的交互方法是通过将函数传入它的then方法从而获取得Promise最终的值或Promise最终最拒绝（reject）的原因。

Sample:
```javascript
var elasticsearch = require('elasticsearch');
var client = new elasticsearch.Client({
    host: 'localhost:9200',
    log: 'trace'
});
client.ping({
    requestTimeout: 30000,
    // undocumented params are appended to the query string                                                                                                                           
    hello: "elasticsearch"
}, function (error) {
    if (error) {
        console.error('elasticsearch cluster is down!');
    } else {
        console.log('All is well');
    }
});
client.search({
    q: 'pants'
}).then(function (body) {
    var hits = body.hits.hits;
}, function (error) {
    console.trace(error.message);
});
client.indices.delete({
    index: 'test_index',
    ignore: [404]
}).then(function (body) {
    // since we told the client to ignore 404 errors, the                                                                                                                             
    // promise is resolved even if the index does not exist                                                                                                                           
    console.log('index was deleted or never existed');
}, function (error) {
    // oh no!                                                                                                                                                                         
});

```