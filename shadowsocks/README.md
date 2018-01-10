# 构建一个shadowsocks镜像


```bash
docker run -d -p 9901:9901 -e SERVER_PORT=9901 -e PASSWORD=password --restart=always shadowsocks
```
