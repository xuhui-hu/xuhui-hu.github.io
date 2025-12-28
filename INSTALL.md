# al-folio 个人博客：本地开发与云端部署完全指南

本指南专门针对在 Windows 环境下，使用 **WSL (Ubuntu)** 和 **Docker** 进行高效开发的流程进行总结。

---

## 🛠 一、 环境准备 (仅需执行一次)

### 安装 Docker 服务
在 WSL 终端（Ubuntu）中运行，确保本地拥有运行容器的能力：

```bash
# 更新并安装
sudo apt update
sudo apt install docker.io docker-compose -y

# 启动服务
sudo service docker start

# 免 sudo 配置 (执行后需重启终端)
sudo usermod -aG docker $USER
```

---

## 🚀 二、 本地开发流程 (日常使用)

### 1. 项目访问路径

**不要**直接在 Windows 的 D 盘或 C 盘目录下运行 Docker，请确保项目文件夹位于 WSL 内部路径中：

* **物理路径**: `\\wsl.localhost\Ubuntu\home\michael\GitHub\xuhui-hu.github.io`
* **快速打开**: 在 WSL 终端进入目录后输入 `code .` 直接唤起 VS Code。


### 2. 启动预览 (必须开启 VPN TUN 模式)

为了能顺利拉取 `amirpourmand/al-folio` 镜像及其 Ruby 依赖，请确保 VPN 已连接至 **德国或美国** 线路。

```bash
# 进入项目根目录
cd ~/GitHub/xuhui-hu.github.io

# 如之前启动过，还要先清理一下
docker compose down

# 启动服务
docker compose up
```
如果拉不下来，大概率换条速度快的线路。

### 3. 预览地址

在 Windows 浏览器输入：

* **访问网址**: [http://localhost:8080](http://localhost:8080)


---

## 📤 三、 云端发布流程 (推送到 GitHub)

当你在本地修改完文章，准备发布到线上时，请遵循以下步骤以保证网络稳定和 Actions 编译通过。

### 1. 停止本地预览

在终端按 `Ctrl + C` 停止 Docker 容器。

### 2. 断开 VPN 并提交

为了保证 Git 推送速度和避免 IP 异常，建议**关闭 VPN** 后再推送：

```bash
# 1. 暂存修改
git add .

# 2. 提交日志
git commit -m "Update blog content: removed jekyll-terser for stability"

# 3. 推送 (如果提示需要 pull，请参考 git pull origin main)
git push origin main

```

---

## 📈 四、 维护建议

暂无