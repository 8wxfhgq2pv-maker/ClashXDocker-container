# ClashX Docker Container

兼容 ClashX 的 Docker 代理服务器

## 📋 功能

- ✅ Shadowsocks 代理服务器
- ✅ V2Ray VLESS 支持
- ✅ Trojan 支持
- ✅ Docker 容器化部署
- ✅ docker-compose 快速启动
- ✅ 本地和网络两用

## 🚀 快速开始

### 方式1: docker-compose（推荐）

```bash
# 1. 启动所有服务
docker-compose up -d

# 2. 查看日志
docker-compose logs -f

# 3. 停止服务
docker-compose down
```

### 方式2: Docker 直接构建

```bash
# Shadowsocks
docker build -f Dockerfile.shadowsocks -t clash-proxy:ss .
docker run -d -p 8388:8388 --name proxy-ss clash-proxy:ss

# V2Ray
docker build -f Dockerfile.v2ray -t clash-proxy:v2ray .
docker run -d -p 10086:10086 --name proxy-v2ray clash-proxy:v2ray

# Trojan
docker build -f Dockerfile.trojan -t clash-proxy:trojan .
docker run -d -p 443:443 --name proxy-trojan clash-proxy:trojan
```

## 📝 配置文件

- `ss-config.json` - Shadowsocks 配置
- `v2ray-config.json` - V2Ray 配置
- `trojan-config.json` - Trojan 配置
- `clash-config.yaml` - ClashX 配置示例

## 🔗 ClashX 配置

在 ClashX 中导入对应的配置文件：

```yaml
proxies:
  - name: "Docker SS"
    type: ss
    server: 127.0.0.1
    port: 8388
    cipher: aes-256-gcm
    password: "your_password"

rules:
  - MATCH,Docker SS
```

## 📊 端口映射

| 服务 | 端口 | 协议 |
|------|------|------|
| Shadowsocks | 8388 | SS |
| V2Ray | 10086 | VLESS |
| Trojan | 443 | TLS |

## 🛠️ 常用命令

```bash
# 查看运行中的容器
docker ps

# 查看容器日志
docker logs -f <container-name>

# 进入容器
docker exec -it <container-name> bash

# 停止容器
docker stop <container-name>

# 删除容器
docker rm <container-name>

# 查看容器网络
docker network ls
```

## ⚙️ 环境变量

可通过环境变量自定义配置：

```bash
docker run -e SS_PASSWORD="custom_password" -e SS_PORT="9999" clash-proxy:ss
```

## 🔒 安全建议

1. 修改默认密码
2. 使用强加密方式（aes-256-gcm）
3. 限制容器的网络访问
4. 定期更新镜像
5. 使用防火墙规则

## 📚 相关链接

- [Shadowsocks GitHub](https://github.com/shadowsocks/shadowsocks)
- [V2Ray 官方文档](https://www.v2fly.org/)
- [Trojan GitHub](https://github.com/trojan-gfw/trojan)
- [ClashX GitHub](https://github.com/yichengchen/clashX)
- [Docker 官方文档](https://docs.docker.com/)

## 📄 许可

MIT License
