# easy-TVframework-go
#### 可用itv服务器IP在 liveITV/config.go 中配置，当前配置为示例不可直接使用。

## Golang 多平台构建支持
go install mvdan.cc/garble@latest

## Docker 多平台构建支持
docker buildx create --name mybuilder --use --driver docker-container  
docker buildx inspect --bootstrap

## 编译二进制可执行文件&执行
### 全平台
make  

### 指定平台
make linux_amd64

### 运行二进制文件
itv_linux_amd64 -token=itv

## Docker部署运行
docker run -d --restart always -p 8123:8123 --name easy-itv mzbgf/easy-itv:latest -token=mytoken

## GitHub Actions
本项目使用 GitHub Actions 进行自动化构建和发布：

1. 自动同步上游代码（每天运行一次）
2. 自动构建并发布 Docker 镜像到：
   - Docker Hub: mzbgf/easy-itv:latest
   - GitHub Container Registry: ghcr.io/mzbgf/easy-itv:latest

### 需要的 Secrets
- `DOCKERHUB_USERNAME`: Docker Hub 用户名
- `DOCKERHUB_TOKEN`: Docker Hub 访问令牌

## 构建多平台镜像并推送至HUB仓库
docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t mzbgf/easy-itv:latest --push .

## 编辑 Sync_Update.sh 39行 指定升级服务器SSH
#### 检查升级路径在config中配置
#### version与线上不一致会触发升级
