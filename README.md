# AWS_edge_latency_testing

AWS_edge_latency_testing用于对比从客户端浏览器直接访问应用、通过GlobalAccelerator访问应用、通过Cloudfront动态加速访问应用这三者之间所花费时间的差异。

大部分基于浏览器的网络测试工具都是通过发送http请求来计算所花费时间，但是由于一个完整HTTP的请求包含dns解析、TCP握手等多个环节，因此所测得的延迟数据不太准确。AWS_edge_latency_testing采用websocket方式在建立好连接的基础上，再发送数据包进行测试，更接近实际的延迟数据。

## Architecture
![edge-architecture.png](https://pwmbjs.s3.cn-north-1.amazonaws.com.cn/AWS_edge_latency_testing/edge-architecture.png)

## Feature
- 显示当前客户端的IP地址与所在区域
- 支持延迟测试
- 支持上传文件测试
- 自定义测试次数与时间间隔
- 测试数据自动写入Dynamodb，可用于后续分析
- 支持对AWS所有区域进行测试

## Deployment
**通过cloudformation模板进行部署**

在需要测试区域通过cloudformation模板（代码中的cloudformation.yaml）进行部署测试服务端，参数说明如下

![cloudformation.png](https://pwmbjs.s3.cn-north-1.amazonaws.com.cn/AWS_edge_latency_testing/cloudformation.png)

**修改测试地址**
- 等待cloudformation模板部署完成，找到cloudforamtion的Outputs中的AcceleratorDNS、CloudfrontDNS和InstanceIp
- 修改代码 node-ws/public/testing.js中的地址为cloudformation模板生成的地址, 如
```
var frankfurt_directurl = 'ws://35.158.115.62'
var frankfurt_gaurl = 'ws://aa204fb2285eaba0f.awsglobalaccelerator.com'
var frankfurt_cdnurl = 'ws://d12v8yek5riemm.cloudfront.net'
```
- 等待10分钟后，测试服务端会自动更新测试地址

## Usage
**获取测试地址**
- 打开任何一个cloudformation模板部署完成的区域，找到cloudforamtion的Outputs
- 找到InstanceIp, 如3.89.224.235


**访问测试页面**
- 打开浏览器，输入找到的InstanceIp

## DEMO
访问链接 http://3.89.224.235

## Test Result Sample
**阿里云雅加达访问AWS弗吉尼亚区域，ping的延迟比较**
![ali-yjd-ping.png](https://pwmbjs.s3.cn-north-1.amazonaws.com.cn/AWS_edge_latency_testing/ali-yjd-ping.png)

**阿里云雅加达访问AWS弗吉尼亚区域，上传200K文件的延迟比较**
![ali-yjd-200K.png](https://pwmbjs.s3.cn-north-1.amazonaws.com.cn/AWS_edge_latency_testing/ali-yjd-200K.png)

## License
This library is licensed under the Apache 2.0 License.
