# EFKK

`Elasticsearch` + `Fluentd` + `Kibana`+ `Kafka` 搭建日志监控系统，建议部署在内网

1. `Filebeat` 采集日志，相比Logstash更加轻量级和易部署，对系统资源开销更小
2. `Elasticsearch` 日志搜索
3. `Kibana` 日志展示
4. `Kafka` 日志缓冲


## 部署

准备工作：
1. 开放端口9092可内网访问、5601可公网访问
2. 修改`.env`文件中的`KAFKA_EXTERNAL_HOST`为宿主机IP

3.执行脚本
```shell
# 当前目录下所有文件赋予权限(读、写、执行)  -- 解决es启动报错问题...
#chown -R 3000:3000 ./app/elasticsearch

# 运行
sudo docker-compose -f docker-compose.yml -p efkk up -d
```

## 访问
1. Kafka地址：IP:9092

2. kibana访问地址：http://IP:5601
   默认账号密码：`elastic/t1izUrGP6uiC7aZBG1m5`
