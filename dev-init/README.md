# 本机开发环境docker环境搭建

## 使用说明

### 重命名环境变量文件

使用前请将 .env_0 改成 .env，并将里面的 IP 改成自己电脑 IP

### emqx 配置

- 修改 emqx 桥接配置
修改 emqx/emqx_bridge_mqtt.conf 中的 clientid，避免和他人冲突

- 添加资源
类型为 MQTT Bridge , “桥接挂载点” 设置为空，

- 添加规则
规则内容: SELECT * FROM "hdec/#"
响应动作：桥接数据到 MQTT Broker
消息内容模板: ${payload}

### 启动服务

```sh
docker-compose up -d mysql
docker-compose up -d redis
docker-compose up -d tdengine
docker-compose up -d kafka
docker-compose up -d easegress
docker-compose up -d emqx

```

### 重启服务

有时修改完一些配置后，需要重新运行某个服务，运行命令：

```sh
docker-compose up -d --force-recreate xxxx
```

举例：

```sh
docker-compose up -d --force-recreate redis
docker-compose up -d --force-recreate tdengine
docker-compose up -d --force-recreate easegress
docker-compose up -d --force-recreate emqx
```

### 查看日志

```sh
docker logs -f --tail 100 redis
docker logs -f --tail 100 tdengine
docker logs -f --tail 100 easegress
docker logs -f --tail 100 emqx
```
