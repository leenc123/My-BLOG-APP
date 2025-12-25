---
title: docker命令整理
tags: [docker,docker-compose]
cover: https://fs.buttercms.com/resize=width:885/F9JOAPMdRmWTAr7Ddned
categories: [运维]
---

# Docker & Docker Compose 常用指令速查手册

## 📦 Docker 基础指令

### 容器生命周期管理

| 指令 | 说明 | 示例 |
|------|------|------|
| `docker run` | 创建并启动容器 | `docker run -d --name myapp nginx:latest` |
| `docker start` | 启动已停止的容器 | `docker start myapp` |
| `docker stop` | 停止运行中的容器 | `docker stop myapp` |
| `docker restart` | 重启容器 | `docker restart myapp` |
| `docker pause` | 暂停容器 | `docker pause myapp` |
| `docker unpause` | 恢复暂停的容器 | `docker unpause myapp` |
| `docker rm` | 删除容器 | `docker rm myapp` |
| `docker rm -f` | 强制删除运行中的容器 | `docker rm -f myapp` |

### 容器操作

| 指令 | 说明 | 示例 |
|------|------|------|
| `docker ps` | 列出运行中的容器 | `docker ps` |
| `docker ps -a` | 列出所有容器（包括停止的） | `docker ps -a` |
| `docker exec` | 在运行中的容器中执行命令 | `docker exec -it myapp bash` |
| `docker logs` | 查看容器日志 | `docker logs myapp` |
| `docker logs -f` | 实时查看容器日志 | `docker logs -f myapp` |
| `docker inspect` | 查看容器详细信息 | `docker inspect myapp` |
| `docker stats` | 查看容器资源使用情况 | `docker stats` |

### 镜像管理

| 指令 | 说明 | 示例 |
|------|------|------|
| `docker images` | 列出本地镜像 | `docker images` |
| `docker pull` | 拉取镜像 | `docker pull nginx:latest` |
| `docker build` | 构建镜像 | `docker build -t myapp:1.0 .` |
| `docker rmi` | 删除镜像 | `docker rmi nginx:latest` |
| `docker tag` | 给镜像打标签 | `docker tag myapp:1.0 myapp:latest` |
| `docker push` | 推送镜像到仓库 | `docker push myapp:1.0` |

## 🚀 Docker Compose 常用指令

### 基本操作

| 指令 | 说明 | 示例 |
|------|------|------|
| `docker-compose up` | 创建并启动所有服务 | `docker-compose up` |
| `docker-compose up -d` | 后台启动所有服务 | `docker-compose up -d` |
| `docker-compose down` | 停止并删除所有容器 | `docker-compose down` |
| `docker-compose stop` | 停止所有服务 | `docker-compose stop` |
| `docker-compose start` | 启动已停止的服务 | `docker-compose start` |
| `docker-compose restart` | 重启所有服务 | `docker-compose restart` |
| `docker-compose restart [service]` | 重启指定服务 | `docker-compose restart nginx` |

### 构建与重建

| 指令 | 说明 | 示例 |
|------|------|------|
| `docker-compose build` | 构建或重新构建服务镜像 | `docker-compose build` |
| `docker-compose up --build` | 构建镜像并启动服务 | `docker-compose up --build` |
| `docker-compose up -d --build` | 后台构建并启动 | `docker-compose up -d --build` |
| `docker-compose up -d --build [service]` | 重建指定服务 | `docker-compose up -d --build nginx` |

### 日志与监控

| 指令 | 说明 | 示例 |
|------|------|------|
| `docker-compose logs` | 查看所有服务日志 | `docker-compose logs` |
| `docker-compose logs -f` | 实时查看所有服务日志 | `docker-compose logs -f` |
| `docker-compose logs [service]` | 查看指定服务日志 | `docker-compose logs nginx` |
| `docker-compose logs -f [service]` | 实时查看指定服务日志 | `docker-compose logs -f nginx` |
| `docker-compose ps` | 列出所有服务状态 | `docker-compose ps` |

### 其他实用指令

| 指令 | 说明 | 示例 |
|------|------|------|
| `docker-compose exec` | 在服务容器中执行命令 | `docker-compose exec nginx bash` |
| `docker-compose pull` | 拉取服务镜像 | `docker-compose pull` |
| `docker-compose config` | 验证并查看配置 | `docker-compose config` |
| `docker-compose scale` | 设置服务实例数量 | `docker-compose scale web=3` |

## 🔧 实用组合指令

### 重启流程
```bash
# 完整重启流程
sudo docker-compose down
sudo docker-compose up -d

# 仅重启特定服务
sudo docker-compose restart nginx

# 重建并重启特定服务
docker-compose up -d --build nginx

# 重建并重启所有服务
docker-compose up -d --build
```

### 日志监控组合
```bash
# 查看所有服务实时日志
docker-compose logs -f

# 查看特定服务实时日志
docker-compose logs -f nginx

# 使用docker命令查看特定容器日志
docker logs -f [容器名或容器ID]
```

### 调试与维护
```bash
# 进入容器内部
docker-compose exec nginx bash
# 或
docker exec -it [容器名] bash

# 查看容器资源使用
docker stats

# 清理未使用的资源
docker system prune -a
```

## 📝 最佳实践提示

1. **使用 `-d` 参数**：在生产环境中始终使用 `-d` 参数让容器在后台运行
2. **日志管理**：使用 `-f` 参数实时监控日志，便于调试
3. **资源清理**：定期使用 `docker system prune` 清理未使用的镜像、容器和网络
4. **版本控制**：在 `docker-compose.yml` 中明确指定镜像版本，避免意外更新
5. **数据持久化**：使用 volumes 或 bind mounts 持久化重要数据

---
