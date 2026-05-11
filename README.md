# Install Debian

# sudo apt install systemd-sysv pour aoir shudown et reboot

# sudo apt install sudo
addgroup
su -
chmod usergroup -aG wheel user
visudo et %wheel ALL(ALL:ALL)
exit et reconnect

# Changer ifupdown to networkmanager
sudo rm -rf /etc/network/interface /etc/network/interface.old
sudp apt install network-manager
sudo systemctl enable --now NetworkManager
reboot

# Fixer IPV4 et bloquer IPV6
nmcli connection show
https://www.fosslinux.com/62880/how-to-set-up-a-static-ip-address-on-debian-11.htm
sudo nmcli con mod "<Nom connection>" ipv4.addresses 192.168.1.52/24 ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8 8.8.4.4" ipv4.method manual
sudo nmcli con up "<Nom connection>"
sudo nmcli con mod "ens33-static" ipv6.method disabled

# Installer tailscale
sudo apt install curl
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up -> Connecter à tailscale via url fourni
tailscale ip
tailscale status

# Installer docker
Set up Docker's apt repository.

## Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

## Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl status docker

sudo systemctl start docker
