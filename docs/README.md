# Docker 和 系统管理 命令

## Docker 命令

### 拉取 Redis 镜像
```bash
docker pull redis
```

### 运行 Redis 容器
```bash
docker run -p 6379:6379 --name redis -v /data/redis/redis.conf:/etc/redis/redis.conf -d redis redis-server /etc/redis/redis.conf
```

### 检查 Redis 是否运行
```bash
netstat -tulnp | grep 6379
```

### 清理 Docker 资源

- **清理所有未使用的卷**
  ```bash
  docker volume prune
  ```

- **清理所有未使用的网络和自定义网络**
  ```bash
  docker network prune
  ```

- **清理所有未使用的镜像、容器、卷和网络（谨慎使用）**
  ```bash
  docker system prune
  ```

### 查看所有容器（包括已停止的）
```bash
docker ps -a
```

## 文件管理

### 压缩和解压缩文件

- **压缩文件夹**
  ```bash
  zip -r fileName.zip 文件夹名
  ```

- **强制解压文件**
  ```bash
  unzip -o dist.zip
  ```

- **压缩当前目录下所有文件**
  ```bash
  zip archive.zip *
  ```

- **解压文件**
  ```bash
  unzip archive.zip
  ```

### 删除文件或文件夹

- **删除文件**
  ```bash
  rm -f dist*
  ```

- **递归删除文件夹**
  ```bash
  rm -rf directory
  ```

## 网络和进程管理

### 检查端口占用

- **在 Linux 上检查端口 8080**
  ```bash
  netstat -ano | grep "8080"
  ```

- **在 Windows 上杀死进程**
  ```bash
  taskkill /pid 8080 -f
  ```

### 进入 Docker 容器
```bash
docker exec -it jenkins /bin/bash
```

### Docker 镜像加速
- 阿里云镜像加速配置：[阿里云镜像加速控制台](https://cr.console.aliyun.com/cn-beijing/instances/mirrors)

### 清空日志
```bash
cd /var/lib/docker/containers/
du -sh */ | sort -h
truncate -s 0 a.log
```

## 系统信息

### 查看 Linux 版本
```bash
cat /etc/os-release
```

## Java 后台进程管理

### 在后台运行 JAR 文件
```bash
nohup java -jar /usr/local/src/bfj/msg-0.jar > /usr/local/src/bfj/info.log 2>&1 &
```

### 检查后台运行的进程
```bash
kill pid
```

### 停止后台进程
```bash
kill $(ps aux | grep 'msg.jar' | awk '{print $2}')
```

## URL 访问提示
- 不能直接复制 URL 时，可以在前面加上 `https://r.jina.ai/`

## Nginx 命令

### 启动 Nginx
```bash
start nginx
```

### 停止 Nginx
```bash
nginx -s stop
```

### 重新加载 Nginx 配置
```bash
nginx -s reload
```

希望这个整理后的 Markdown 格式命令集能帮助你更方便地管理和使用你的系统资源！