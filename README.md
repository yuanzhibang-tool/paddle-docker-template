# paddle-env
paddle ai env for vscode

# 1.windows 使用 `wsl2` 安裝 docker，不建议安装docker-desktop,请参考下方`如何在wsl2安装docker?`
# 2.安装nvidia最新驱动,并配置`nvidia docker`环境
# 3.由于`paddle`镜像比较大,建议使用docker先pull再使用容器打开,例如`tag:2.5.0-gpu-cuda11.2-cudnn8.2-trt8.0`大于10GB.
# 4.拉取镜像过慢建议使用国内加速,详情请百度.

---

## 配置nvidia环境
```bash
# 切换管理员
sudo -i;
# !搜索英伟达驱动
apt search nvidia-driver
# !查找如 `nvidia-driver-535`数字选择最新的
apt install  nvidia-driver-535 -y
# !检查是否能识别到nvidia设备
nvidia-smi

# 安装`nvidia-container-toolkit`,具体参照[英伟达官方引导](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
#! 以下以ubuntu为例,代码来自上方连接

# !添加英伟达源
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
      && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
      && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
            sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
            sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
apt update -y
apt install -y nvidia-container-toolkit
nvidia-ctk runtime configure --runtime=docker
systemctl restart docker
# !即可在docker中使用nvidia gpu
```
---

## 如何在wsl2安装docker?
下方代码来自[https://nickjanetakis.com/blog/install-docker-in-wsl-2-without-docker-desktop](https://nickjanetakis.com/blog/install-docker-in-wsl-2-without-docker-desktop)

```bash
# Install Docker, you can ignore the warning from Docker about using WSL
    curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Add your user to the Docker group
sudo usermod -aG docker $USER

# Install Docker Compose v2
sudo apt-get update && sudo apt-get install docker-compose-plugin

# Sanity check that both tools were installed successfully
docker --version
docker compose version

# Using Ubuntu 22.04 or Debian 10 / 11? You need to do 1 extra step for iptables
# compatibility, you'll want to choose option (1) from the prompt to use iptables-legacy.
sudo update-alternatives --config iptables
```
