# al-folio 本地部署指南 (Windows)

## Windows 本地快速部署 (WSL + Docker)

对于 Windows 用户，建议在 **WSL (Ubuntu)** 环境下通过 **Docker** 运行项目，以避免 Windows 原生环境下的路径性能和文件权限问题。

### 1. 在 WSL 中安装 Docker
在该模式下，容器内已预装 Ruby/Jekyll 环境，无需在本地折腾依赖。请在 WSL 终端执行：

```bash
# 更新并安装 Docker & Docker Compose
sudo apt update
sudo apt install docker.io docker-compose

# 启动 Docker 服务
sudo service docker start

# (建议) 将当前用户加入 docker 组，避免每次都要输入 sudo
# 执行后需要重启 WSL 或重新登录生效
sudo usermod -aG docker $USER
```

### 2. 运行项目
进入项目目录并启动镜像：
需要打开TUN模式的VPN,德国线路可以，香港不行。全程需要开VPN TUN模式或换源）

```bash
# 进入项目目录
cd /mnt/d/GitHub/xuhui-hu.github.io

# 拉取最新镜像并启动
docker compose down
docker compose up
```

如果出现jekyll-1  | fatal: cannot chdir to 'D:/GitHub/xuhui-hu.github.io': No such file or directory
Run the following commands in your WSL terminal:

Clean up the problematic files:

Bash

rm Gemfile.lock
rm -rf .bundle
(Note: It is safe to delete Gemfile.lock; the container will generate a fresh one compatible with Linux.)

### 3. 预览与访问
运行成功后，在 Windows 浏览器中输入以下地址即可预览：
- **访问地址**: [http://localhost:8080](http://localhost:8080)

> **提示**: Docker 模式下默认使用 **8080** 端口，而非官方默认的 4000 端口。



