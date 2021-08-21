# galatency

用于对比客户端直接访问应用和通过GA访问应用之间的延迟差异<br>
该应用分为两部分：

- nodejs的web服务
1. 返回客户端index.html
2. 客户端和nodejs之间websocket连接
3. 分别记录直接访问应用和通过GA访问的延迟
4. 将延迟数据提交给python web服务

- python的web服务
1. 接收客户端提交的延迟数据
2. 写入ddb

## 安装依赖
```
cd node-ws
npm i
cd python-flask
pip install -r requirements.txt
```

## 开启web应用
```
cd node-ws
node index.js
cd python-flask
python ga.py
```

## Testing
在客户端打开浏览器输入 http://服务器ip/

## License
This library is licensed under the Apache 2.0 License.
