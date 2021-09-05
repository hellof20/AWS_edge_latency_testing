# AWS_edge_latency_testing

用于对比客户端直接访问应用和通过GA访问应用之间的延迟差异<br>
该应用分为两部分：

- nodejs的web服务
1. 返回客户端index.html
2. 客户端和nodejs之间websocket连接
3. 分别记录直接访问应用和通过GA访问的延迟
4. 将延迟数据提交给python web服务

## Installing
```
$ cd node-ws
$ npm i
```

## Usage
Server
```
$ cd node-ws
$ node index.js
```

client
Open the browser and input http://serverip/

## License
This library is licensed under the Apache 2.0 License.
