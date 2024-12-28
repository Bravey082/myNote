# 常用命令速查

## 容器管理

### Docker 基础操作

- **镜像管理**
  ```bash
  docker pull redis              # 拉取镜像
  docker images                  # 查看所有镜像
  docker rmi image_id           # 删除镜像
  docker ps -a                   # 查看所有容器
  docker exec -it jenkins /bin/bash  # 进入容器
  docker stop container_id       # 停止容器
  docker start container_id      # 启动容器
  docker restart container_id    # 重启容器
  ```

- **容器运行**
  ```bash
  docker run -p 6379:6379 --name redis \
    -v /data/redis/redis.conf:/etc/redis/redis.conf \
    -d redis redis-server /etc/redis/redis.conf
  
  docker run -d --name mysql \    # 运行MySQL容器
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=123456 \
    mysql:5.7
  ```

### Docker 维护

- **资源清理**
  ```bash
  docker volume prune           # 清理未使用的卷
  docker network prune         # 清理未使用的网络
  docker system prune         # 清理所有未使用资源
  docker logs container_id    # 查看容器日志
  ```

- **配置与日志**
  - 镜像加速：通过[阿里云镜像加速控制台](https://cr.console.aliyun.com/cn-beijing/instances/mirrors)配置
  ```bash
  cd /var/lib/docker/containers/
  du -sh */ | sort -h          # 查看日志大小
  truncate -s 0 a.log         # 清理日志
  ```

## 系统运维

### 文件管理

- **压缩与解压**
  ```bash
  zip -r fileName.zip 文件夹名   # 压缩文件夹
  zip archive.zip *             # 压缩当前目录
  unzip -o dist.zip            # 强制解压
  unzip archive.zip            # 普通解压
  tar -czvf file.tar.gz dir/   # 压缩目录
  tar -xzvf file.tar.gz       # 解压tar包
  ```

- **文件操作**
  ```bash
  rm -f dist*                  # 删除文件
  rm -rf directory            # 删除目录
  cp -r source dest           # 复制目录
  mv source dest              # 移动/重命名
  chmod +x file              # 添加执行权限
  chown user:group file      # 更改所有者
  ```

### 系统监控

- **网络检查**
  ```bash
  netstat -tulnp | grep 6379   # 检查端口
  netstat -ano | grep "8080"   # 查看端口占用
  ping host                    # 测试连通性
  curl -I url                  # 检查网站状态
  ifconfig                     # 查看网络接口
  ```

- **系统信息**
  ```bash
  cat /etc/os-release         # 查看系统版本
  free -h                     # 查看内存使用
  df -h                       # 查看磁盘使用
  top                        # 查看系统进程
  ps aux | grep process      # 查找特定进程
  ```

## 应用服务管理

### Java 应用

- **运行与管理**
  ```bash
  nohup java -jar /usr/local/src/bfj/msg-0.jar > /usr/local/src/bfj/info.log 2>&1 &  # 后台运行
  kill pid                     # 停止进程
  kill $(ps aux | grep 'msg.jar' | awk '{print $2}')  # 停止特定 JAR
  jps                         # 列出Java进程
  jstat -gc pid              # 查看GC状态
  ```

### Nginx 服务

- **服务控制**
  ```bash
  start nginx                  # 启动
  nginx -s stop               # 停止
  nginx -s reload             # 重载配置
  nginx -t                    # 测试配置
  ```

- **日志管理**
  ```bash
  tail -f /var/log/nginx/access.log  # 实时查看访问日志
  tail -f /var/log/nginx/error.log   # 实时查看错误日志
  ```

## 实用技巧

- 访问加速：URL 访问困难时，可在前面添加 `https://r.jina.ai/`
- 查找文件：`find / -name filename`
- 文本搜索：`grep -r "text" directory/`
- 磁盘清理：`du -sh * | sort -hr | head -n 10`
- 文件权限：`chmod 777 filename`
- 文件夹权限：`chmod -R 777 directory/`
- 文件夹创建：`mkdir -p directory/subdir`
- 文件夹删除：`rm -rf directory/`
- 文件夹复制：`cp -r source/ dest/`
- 文件夹移动：`mv source/ dest/`
- 文件夹重命名：`mv oldname newname`

### 文本处理

- **文本编辑**
  ```bash
  sed -i 's/old/new/g' file    # 替换文本内容
  awk '{print $1}' file        # 打印第一列
  head -n 10 file              # 查看前10行
  tail -n 20 file              # 查看后20行
  wc -l file                   # 统计行数
  ```

- **文本搜索**
  ```bash
  grep -n "pattern" file       # 显示匹配行号
  grep -v "pattern" file       # 显示不匹配的行
  grep -r "text" .             # 递归搜索当前目录
  ```

### 系统管理

- **进程管理**
  ```bash
  ps -ef | grep process        # 查看特定进程
  pgrep process_name          # 获取进程ID
  nohup command &             # 后台运行命令
  jobs                        # 查看后台任务
  fg %n                       # 将后台任务调至前台
  ```

- **用户管理**
  ```bash
  useradd username            # 创建用户
  passwd username             # 设置密码
  usermod -aG group user      # 添加用户到组
  who                         # 查看当前登录用户
  last                        # 查看登录历史
  ```

### 网络工具

- **网络诊断**
  ```bash
  traceroute host             # 路由追踪
  nslookup domain             # DNS查询
  dig domain                  # DNS详细查询
  ss -tunlp                   # 查看网络连接
  iptables -L                 # 查看防火墙规则
  ```

### 实用小技巧

- 历史命令搜索：`Ctrl + R`
- 清空终端：`clear` 或 `Ctrl + L`
- 终止当前命令：`Ctrl + C`
- 命令行移动：
  - 行首：`Ctrl + A`
  - 行尾：`Ctrl + E`
  - 向前一个词：`Alt + B`
  - 向后一个词：`Alt + F`
- 快速目录切换：
  - 上一个目录：`cd -`
  - 主目录：`cd ~`
  - 根目录：`cd /`

### 性能优化

- **内存管理**
  ```bash
  sync && echo 3 > /proc/sys/vm/drop_caches    # 清理内存缓存
  vmstat 1 10                                  # 监控系统性能
  sar -r 1 10                                  # 监控内存使用
  ```

- **磁盘管理**
  ```bash
  iotop                       # 监控磁盘I/O
  fstrim -v /                 # 优化SSD性能
  hdparm -tT /dev/sda        # 测试磁盘速度
  ```
