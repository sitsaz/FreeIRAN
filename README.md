# FreeIRAN 🕊️
🌟 A Simple Bash Script With TUI For Setting Up Ubuntu Server

🏹 Brave hearts unite for a Free Iran, lighting the path to a brighter future with unwavering determination.

What does this script do? you can select to:
1. Update & Cleanup Server 🧬
2. Install Essential Packages 🎉
3. Install Speedtest 🚀
4. Create SWAP File 💾
5. Enable BBR 🛸
6. Enable Hybla 🌐
7. Schedule Automatic Updates & Restarts at 01:00 GMT+3:30 ⏳
8. Install Multiprotocol VPN Panels (X-UI/S-UI/H-UI/Reality-EZPZ/Marzban/Hiddify/Vaxilu/FranzKafkaYu) 🦄
9. Obtain SSL Certificates 🗺️
10. Install Pi-Hole Network-Wide Adblocker 🛡️
11. Change SSH Port 🥅
12. Enable UFW 🔒
13. Install & Configure WARP Proxy ✨
14. Install Erlang MTProto Proxy 💫
15. Setup Hysteria II 🌈
16. Setup TUIC v5 🔥
17. Setup Juicity 🍹
18. Setup WireGuard ♟️
19. Setup OpenVPN 🎗️
20. Setup IKEv2/IPsec 🧭
21. Create non-root SSH User 👤

⚠️ Manually set the parameters yourself when prompted during the setup.

⚠️ در هنگام راه‌اندازی، وقتی درخواست برای تنظیم پارامترها نمایش داده می‌شود، پارامترها را به صورت دستی وارد کنید.
<p align="center">
  <img src="https://raw.githubusercontent.com/ErfanNamira/FreeIRAN/main/Images/FreeIRAN1.4.0.jpg" alt="FreeIRAN1.4.0">
</p>

## How to run 📦
It's highly recommended to run this script only on a fresh install of Ubuntu 22.04.
```
curl -O https://raw.githubusercontent.com/ErfanNamira/FreeIRAN/main/FreeIRAN.sh && chmod +x FreeIRAN.sh && sed -i -e 's/\r$//' FreeIRAN.sh && sudo apt update && sudo apt install -y dialog && ./FreeIRAN.sh
```
To run the script after the first time, just enter the following command in the terminal:
```
./FreeIRAN.sh
```
## Access Panels 🚪
1. If you have installed Reality-EZPZ, you can access its TUI by running the following command:
```
bash <(curl -sL https://bit.ly/realityez) -m
```
2. If you have installed X-UI Panels, you can access their command-line interface by using the following command:
```
x-ui
```
3. If you have installed S-UI, you can access it's web interface by
```
http://ip:port/webbasepath
    Panel Port: 2095
    Panel Path: /app/
    Subscription Port: 2096
    Subscription Path: /sub/
    User/Passowrd: admin
```
If you want to uninstall S-UI:
```
systemctl disable sing-box --now
systemctl disable s-ui  --now
rm -f /etc/systemd/system/s-ui.service
rm -f /etc/systemd/system/sing-box.service
systemctl daemon-reload
rm -fr /usr/local/s-ui
```
4. If you have installed H-UI, you can access it's web interface by
```
http://ip:8081
Username/Password: sysadmin
```
If you want to uninstall H-UI:
```
systemctl stop h-ui
rm -rf /etc/systemd/system/h-ui.service /usr/local/h-ui/
```
5. If you have installed Pi-hole, you can access its command-line interface by using the following command:
```
pihole
```
## 💠 After setup has completed, don't forget to:

1. Add your desired adlists via Pi-hole web interface
```
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
https://raw.githubusercontent.com/d3ward/toolz/master/src/d3host.txt
https://big.oisd.nl/
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/domains/pro.txt
https://blocklistproject.github.io/Lists/abuse.txt
https://blocklistproject.github.io/Lists/ads.txt
https://blocklistproject.github.io/Lists/crypto.txt
https://blocklistproject.github.io/Lists/drugs.txt
https://blocklistproject.github.io/Lists/fraud.txt
https://blocklistproject.github.io/Lists/gambling.txt
https://blocklistproject.github.io/Lists/malware.txt
https://blocklistproject.github.io/Lists/phishing.txt
https://blocklistproject.github.io/Lists/ransomware.txt
https://blocklistproject.github.io/Lists/redirect.txt
https://blocklistproject.github.io/Lists/scam.txt
https://raw.githubusercontent.com/MasterKia/PersianBlocker/main/PersianBlockerHosts.txt
```
2. Update Pi-hole Database
```
pihole -g
```
3. Modify Lighttpd

⭕ If you have installed Pi-hole/reality-ezpz, then Lighttpd/docker is listening on port 80 by default. If you haven't changed the Lighttpd port, it's necessary to stop it before obtaining SSL certificates. Below, you can find commands to start, stop, restart, and modify the configuration of Lighttpd.

⭕ اگر شما Pi-hole یا reality-ezpz را نصب کرده‌اید، در این صورت Lighttpd/docker به صورت پیش‌فرض از پورت 80 استفاده می‌کند. اگر پورت Lighttpd را تغییر نداده‌اید، قبل از دریافت گواهی SSL، لازم است آن را متوقف کنید. در زیر، شما می‌توانید دستوراتی برای شروع، توقف، بازآغاز و تغییر پیکربندی Lighttpd پیدا کنید.
```
sudo nano /etc/lighttpd/lighttpd.conf
```
```
sudo systemctl start lighttpd.service
sudo systemctl stop lighttpd.service
sudo systemctl restart lighttpd.service
```
4. Obtain SSL Certificates 
```
sudo certbot certonly --standalone --preferred-challenges http --agree-tos --email yourmail@gmail.com -d sub.domain.com
```
5. Change SSH Port
```
sudo nano /etc/ssh/sshd_config
sudo systemctl reload sshd
```
6. Setup UFW
```
sudo nano /etc/default/ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow SSHPORT/tcp
sudo ufw limit SSHPORT/tcp
sudo ufw allow PORT
sudo ufw enable
sudo ufw status verbose
sudo systemctl enable ufw
```
7. Change WARP License Key
```
warp-cli set-license <your-warp-plus-license-key>
```
8. WARP Status
```
bash <(curl -fsSL git.io/warp.sh) status
```
9. Change Server DNS to use Pi-hole
```
sudo nano /etc/resolv.conf
nameserver 127.0.0.53
```
If /resolv.conf managed by systemd-resolved, then you have to follow these steps:
```
cd /etc/netplan/
ls
nano ab-cloud-init.yaml
sudo netplan apply
```
You need to add the following lines to the 'ab-cloud-init.yaml' file:
```
nameservers:
  addresses: [127.0.0.53]
```
10. Restart your server with
```
sudo shutdown -r now
```
## Optional: Install qbittorrent-nox 🔮
```
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
sudo apt update
sudo apt install qbittorrent-nox
sudo nano /etc/systemd/system/qbittorrent-nox.service
qbittorrent-nox
sudo adduser --system --group qbittorrent-nox
sudo adduser root qbittorrent-nox
sudo systemctl daemon-reload
sudo systemctl enable qbittorrent-nox
sudo systemctl start qbittorrent-nox
sudo systemctl status qbittorrent-nox
```
### qbittorrent-nox.service configuration
```
[Unit]
Description=qBittorrent-nox
After=network.target

[Service]
Type=forking
ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8000
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
## Optional: Install miniserve 🪄
```
wget https://github.com/svenstaro/miniserve/releases/download/v0.27.1/miniserve-0.27.1-x86_64-unknown-linux-gnu
ls -l /root/miniserve
chmod +x /root/miniserve
sudo mv /etc/letsencrypt/live/abc.domain.xyz/fullchain.pem /etc/letsencrypt/live/abc.domain.xyz/certificate.cert
sudo mv /etc/letsencrypt/live/abc.domain.xyz/privkey.pem /etc/letsencrypt/live/abc.domain.xyz/private.key
```
### miniserve.service configuration
```
sudo nano /etc/systemd/system/miniserve.service
-------------------
[Unit]
Description=Miniserve File Server
After=network.target

[Service]
ExecStart=/root/miniserve -p 2087 --tls-cert /etc/letsencrypt/live/abc.domain.xyz/certificate.cert --tls-key /etc/letsencrypt/live/abc.domain.xyz/private.key --auth USER:PASS /Downloads
WorkingDirectory=/root
Restart=always
User=root

[Install]
WantedBy=multi-user.target
-------------------
mkdir /Downloads
sudo systemctl daemon-reload
sudo systemctl enable miniserve.service
sudo systemctl start miniserve.service
sudo systemctl status miniserve.service
```
## Optional: WARP XrayConfig ✨
```
{
  "protocol": "socks",
  "settings": {
    "servers": [
      { 
        "address": "127.0.0.1",
        "port":40000
      }
    ]
  },
  "tag":"warp"
},
```

## Used Projects 💞
```
https://github.com/pi-hole
https://github.com/vaxilu/x-ui
https://github.com/alireza0/x-ui
https://github.com/alireza0/s-ui
https://github.com/MHSanaei/3x-ui
https://github.com/jonssonyan/h-ui
https://github.com/Gozargah/Marzban
https://github.com/FranzKafkaYu/x-ui
https://github.com/aleskxyz/reality-ezpz
https://github.com/hiddify/Hiddify-Server
https://github.com/radkesvat/ReverseTlsTunnel
https://github.com/deathline94/Juicity-Installer
https://github.com/deathline94/tuic-v5-installer
https://github.com/deathline94/Hysteria-Installer
https://github.com/HirbodBehnam/MTProtoProxyInstaller
https://github.com/angristan/wireguard-install
https://github.com/angristan/openvpn-install
https://github.com/blocklistproject/Lists
https://github.com/hwdsl2/setup-ipsec-vpn
https://github.com/rahgozar94725/freedom
https://github.com/seriyps/mtproto_proxy
https://github.com/svenstaro/miniserve
https://github.com/P3TERX/warp.sh
```
## Buy Me a Coffee ☕❤️
```
LiteCoin (LTC): ltc1qwhd8jpwumg5uywgv028h3lnsck8mjxhxnp4rja
```
