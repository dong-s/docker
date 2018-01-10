# 构建一个shadowsocks镜像



```bash

# 通过ENV可以自定以一下参数

# SERVER_ADDR 0.0.0.0
# SERVER_PORT 8888
# PASSWORD    password
# METHOD      aes-256-cfb


docker run -d -p 9901:9901 -e SERVER_PORT=9901 -e PASSWORD=password --restart=always shadowsocks
```
