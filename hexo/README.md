# 在jenkins上增加hexo

配合jenkins，使hexo在docker中构建，并自动发布到nginx。

```bash
docker run -p 8080:8080 dong/hexo
```