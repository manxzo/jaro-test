# jaro-test

echo "=== BASIC SERVER CHECK ==="

hostname

date

uptime

whoami

ip -4 addr

ip route

echo "=== CHECK SSH SERVER ==="

sudo apt update

sudo apt install -y openssh-server

sudo systemctl enable --now ssh

sudo systemctl status ssh --no-pager

echo "=== ALLOW SSH FROM LOCAL 192.168.1.0/24 ONLY ==="

sudo ufw allow from 192.168.1.0/24 to any port 22 proto tcp

sudo ufw status verbose

echo "=== CONFIRM PORT 22 IS LISTENING ==="

sudo ss -tulpn | grep ':22' || echo "SSH is not listening on port 22"

echo "=== TAILSCALE STATUS ==="

systemctl status tailscaled --no-pager || true

tailscale status || true

tailscale netcheck || true

echo "=== RECENT TAILSCALE LOGS ==="
journalctl -u tailscaled -n 100 --no-pager || true

echo "=== SERVER LAN IPs ==="

hostname -I
