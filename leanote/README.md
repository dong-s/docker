# 构建一个leanote镜像

构建一个内置mongo的leanote镜像，主要是用来同步的。

```bash
docker run -d -p 9000:9000 -v xx/app.conf:/home/leanote/conf/app.conf --restart=always d0ng/leanote
```
