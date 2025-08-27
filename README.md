 cài Docker CE và Docker Compose v2 (plugin) trên Red Hat Enterprise Linux 9 (RHEL 9). Làm theo thứ tự dưới đây là được.

1) Gỡ bản cũ/đụng độ (nếu có)

sudo dnf remove -y podman-docker docker docker-client docker-client-latest \
  docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
2) Thêm Docker CE repo chính thức

sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
sudo dnf makecache
3) Cài Docker + Compose plugin

sudo dnf install -y docker-ce docker-ce-cli containerd.io \
  docker-buildx-plugin docker-compose-plugin
4) Bật và khởi động dịch vụ

sudo systemctl enable --now docker
sudo systemctl status docker --no-pager
5) Cho phép chạy Docker không cần sudo (tuỳ chọn)

sudo usermod -aG docker $USER
# đăng xuất & đăng nhập lại, rồi kiểm tra:
docker info
6) Kiểm tra nhanh

docker compose version
