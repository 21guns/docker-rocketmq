# tag
- server , broker , latest ( 最新版 , new)
- server-4.5.1 , broker-4.5.1
- server-4.4.0 , broker-4.4.0
- server-4.3.2 , broker-4.3.2
- server-4.3.0 , broker-4.3.0

# docker-rocketmq
rocketmq

rocketmq Version 4.3.0 , 4.3.2, 4.4.0, 4.5.1

# server
```SHELL
docker run -d -p 9876:9876 --name rmqserver  foxiswho/rocketmq:server
```

# broker
```SHELL
docker run -d -p 10911:10911 -p 10909:10909 --name rmqbroker --link rmqserver:namesrv -e "NAMESRV_ADDR=namesrv:9876" -e "JAVA_OPTS=-Duser.home=/opt"  -e "JAVA_OPT_EXT=-server -Xms128m -Xmx128m -Xmn128m" foxiswho/rocketmq:broker
```

## broker 配置文件位置 (容器内)

```SHELL
/etc/rocketmq/broker.conf
```

## 使用自己的配置文件
请全部复制到shell 中执行
```SHELL
docker run -d -p 10911:10911 -p 10909:10909 --name rmqbroker --link rmqserver:namesrv \
-e "NAMESRV_ADDR=namesrv:9876" \
-e "JAVA_OPTS=-Duser.home=/opt"  \
-e "JAVA_OPT_EXT=-server -Xms128m -Xmx128m -Xmn128m" \
-v /User/fox/rmq/conf/broker.conf:/etc/rocketmq/broker.conf \
foxiswho/rocketmq:broker
```
>/User/fox/rmq/conf/broker.conf 为我的本地配置文件目录

# console
来自
https://hub.docker.com/r/styletang/rocketmq-console-ng/

```SEHLL
docker run --name rmqconsole --link rmqserver:namesrv -e "JAVA_OPTS=-Drocketmq.namesrv.addr=IP地址:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false" -p 8180:8080 -t styletang/rocketmq-console-ng
```

浏览器访问
```SEHLL
localhost:8180
```

Example:
```SEHLL
docker run --name rmqconsole --link rmqserver:namesrv -e "JAVA_OPTS=-Drocketmq.namesrv.addr=namesrv:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false" -p 8180:8080 -t styletang/rocketmq-console-ng
```

# docker-compose

```SHELL
cd rmq

docker-compose up

```
访问浏览器
```SHELL
localhost:8180
```


# 其他案例

https://github.com/foxiswho/docker-consul-fabio-apollo-rocketmq-rabbitmq