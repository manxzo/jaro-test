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


(base) ➜  ~ >....

echo "=== SERVER LAN IPs ==="

hostname -I

About
No description, website, or topics provided.
Resources
 Readme
 Activity
Stars
 0 stars
Watchers
 0 watching
Forks
 0 forks
Releases
No releases published
Create a new release
Packages
No packages published
Publish your first package
Contributors
1
@manxzo
manxzo Manojkumar
Footer

=== BASIC SERVER CHECK ===
pop-os
Thu May  7 07:09:40 PM +08 2026
 19:09:40 up 16 min,  1 user,  load average: 0.05, 0.10, 0.08
makyd
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
3: wlp12s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    inet 192.168.88.5/24 brd 192.168.88.255 scope global dynamic noprefixroute wlp12s0
       valid_lft 6552sec preferred_lft 6552sec
4: tailscale0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1280 qdisc fq_codel state UNKNOWN group default qlen 500
    inet 100.85.19.11/32 scope global tailscale0
       valid_lft forever preferred_lft forever
5: br-31af7304b305: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    inet 172.20.0.1/16 brd 172.20.255.255 scope global br-31af7304b305
       valid_lft forever preferred_lft forever
6: br-3285a839ea1c: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    inet 172.18.0.1/16 brd 172.18.255.255 scope global br-3285a839ea1c
       valid_lft forever preferred_lft forever
7: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
8: br-8f4ee7e1b4be: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    inet 172.21.0.1/16 brd 172.21.255.255 scope global br-8f4ee7e1b4be
       valid_lft forever preferred_lft forever
9: br-b95037d754b0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    inet 172.19.0.1/16 brd 172.19.255.255 scope global br-b95037d754b0
       valid_lft forever preferred_lft forever
default via 192.168.88.1 dev wlp12s0 proto dhcp src 192.168.88.5 metric 600
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
172.18.0.0/16 dev br-3285a839ea1c proto kernel scope link src 172.18.0.1 linkdown
172.19.0.0/16 dev br-b95037d754b0 proto kernel scope link src 172.19.0.1
172.20.0.0/16 dev br-31af7304b305 proto kernel scope link src 172.20.0.1 linkdown
172.21.0.0/16 dev br-8f4ee7e1b4be proto kernel scope link src 172.21.0.1
192.168.88.0/24 dev wlp12s0 proto kernel scope link src 192.168.88.5 metric 600
=== CHECK SSH SERVER ===
Get:1 file:/var/cuda-repo-ubuntu2404-13-0-local  InRelease [1,572 B]
Get:1 file:/var/cuda-repo-ubuntu2404-13-0-local  InRelease [1,572 B]
Get:2 https://download.docker.com/linux/ubuntu noble InRelease [48.5 kB]
Hit:3 https://repo.steampowered.com/steam stable InRelease
Hit:4 https://brave-browser-apt-release.s3.brave.com stable InRelease
Get:5 https://download.docker.com/linux/ubuntu noble/stable amd64 Packages [53.4 kB]
Get:6 https://pkgs.tailscale.com/stable/ubuntu noble InRelease
Hit:7 http://apt.pop-os.org/proprietary noble InRelease
Get:8 http://apt.pop-os.org/release noble InRelease [18.0 kB]
Hit:9 http://apt.pop-os.org/ubuntu noble InRelease
Get:10 http://apt.pop-os.org/ubuntu noble-security InRelease [126 kB]
Get:11 http://apt.pop-os.org/ubuntu noble-updates InRelease [126 kB]
Get:12 http://apt.pop-os.org/ubuntu noble-backports InRelease [126 kB]
Get:13 http://apt.pop-os.org/release noble/main Sources [76.2 kB]
Get:14 http://apt.pop-os.org/release noble/main i386 Packages [92.5 kB]
Get:15 http://apt.pop-os.org/release noble/main amd64 Packages [230 kB]
Get:16 http://apt.pop-os.org/release noble/main amd64 Components [11.8 kB]
Get:17 http://apt.pop-os.org/release noble/main Icons (48x48) [11.2 kB]
Get:18 http://apt.pop-os.org/release noble/main Icons (64x64) [14.6 kB]
Get:19 http://apt.pop-os.org/release noble/main Icons (128x128) [28.6 kB]
Fetched 970 kB in 6s (161 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
513 packages can be upgraded. Run 'apt list --upgradable' to see them.
N: Skipping acquire of configured file 'stable/binary-i386/Packages' as repository 'https://download.docker.com/linux/ubuntu noble InRelease' doesn't support architecture 'i386'
N: Missing Signed-By in the sources.list(5) entry for 'http://apt.pop-os.org/ubuntu'
N: Missing Signed-By in the sources.list(5) entry for 'http://apt.pop-os.org/ubuntu'
N: Missing Signed-By in the sources.list(5) entry for 'http://apt.pop-os.org/ubuntu'
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  ncurses-term openssh-client openssh-sftp-server ssh-import-id
Suggested packages:
  keychain libpam-ssh monkeysphere ssh-askpass molly-guard
The following NEW packages will be installed:
  ncurses-term openssh-server openssh-sftp-server ssh-import-id
The following packages will be upgraded:
  openssh-client
1 upgraded, 4 newly installed, 0 to remove and 512 not upgraded.
Need to get 1,739 kB of archives.
After this operation, 6,747 kB of additional disk space will be used.
Get:1 http://apt.pop-os.org/ubuntu noble-security/main amd64 openssh-client amd64 1:9.6p1-3ubuntu13.16 [907 kB]
Get:2 http://apt.pop-os.org/ubuntu noble-security/main amd64 openssh-sftp-server amd64 1:9.6p1-3ubuntu13.16 [37.3 kB]
Get:3 http://apt.pop-os.org/ubuntu noble-security/main amd64 openssh-server amd64 1:9.6p1-3ubuntu13.16 [510 kB]
Get:4 http://apt.pop-os.org/ubuntu noble/main amd64 ncurses-term all 6.4+20240113-1ubuntu2 [275 kB]
Get:5 http://apt.pop-os.org/ubuntu noble-updates/main amd64 ssh-import-id all 5.11-0ubuntu2.24.04.1 [10.1 kB]
Fetched 1,739 kB in 3s (602 kB/s)
Preconfiguring packages ...
(Reading database ... 279807 files and directories currently installed.)
Preparing to unpack .../openssh-client_1%3a9.6p1-3ubuntu13.16_amd64.deb ...
Unpacking openssh-client (1:9.6p1-3ubuntu13.16) over (1:9.6p1-3ubuntu13.14) ...
Selecting previously unselected package openssh-sftp-server.
Preparing to unpack .../openssh-sftp-server_1%3a9.6p1-3ubuntu13.16_amd64.deb ...
Unpacking openssh-sftp-server (1:9.6p1-3ubuntu13.16) ...
Selecting previously unselected package openssh-server.
Preparing to unpack .../openssh-server_1%3a9.6p1-3ubuntu13.16_amd64.deb ...
Unpacking openssh-server (1:9.6p1-3ubuntu13.16) ...
Selecting previously unselected package ncurses-term.
Preparing to unpack .../ncurses-term_6.4+20240113-1ubuntu2_all.deb ...
Unpacking ncurses-term (6.4+20240113-1ubuntu2) ...
Selecting previously unselected package ssh-import-id.
Preparing to unpack .../ssh-import-id_5.11-0ubuntu2.24.04.1_all.deb ...
Unpacking ssh-import-id (5.11-0ubuntu2.24.04.1) ...
Setting up openssh-client (1:9.6p1-3ubuntu13.16) ...
Setting up ssh-import-id (5.11-0ubuntu2.24.04.1) ...
Setting up ncurses-term (6.4+20240113-1ubuntu2) ...
Setting up openssh-sftp-server (1:9.6p1-3ubuntu13.16) ...
Setting up openssh-server (1:9.6p1-3ubuntu13.16) ...

Creating config file /etc/ssh/sshd_config with new version
Creating SSH2 RSA key; this may take some time ...
3072 SHA256:ZD+BpTpI4ZtYhLkaI0RGKA2KdGuUtGEAn/I6YKyHpK0 root@pop-os (RSA)
Creating SSH2 ECDSA key; this may take some time ...
256 SHA256:t21FObQcaCuiEPFYllFNmANUlv1+PlEAeDsyeMPB6j4 root@pop-os (ECDSA)
Creating SSH2 ED25519 key; this may take some time ...
256 SHA256:y6EkoDwqnx17RToCmTIBEM8t9B2lzHeyung5iS1YMz8 root@pop-os (ED25519)
Created symlink /etc/systemd/system/sockets.target.wants/ssh.socket → /usr/lib/systemd/system/ssh.socket.
Created symlink /etc/systemd/system/ssh.service.requires/ssh.socket → /usr/lib/systemd/system/ssh.socket.
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for ufw (0.36.2-6) ...
Synchronizing state of ssh.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable ssh
Created symlink /etc/systemd/system/sshd.service → /usr/lib/systemd/system/ssh.service.
Created symlink /etc/systemd/system/multi-user.target.wants/ssh.service → /usr/lib/systemd/system/ssh.service.
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-05-07 19:09:56 +08; 10ms ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 11122 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 11124 (sshd)
      Tasks: 1 (limit: 37034)
     Memory: 1.9M (peak: 2.1M)
        CPU: 11ms
     CGroup: /system.slice/ssh.service
             └─11124 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

May 07 19:09:56 pop-os systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 07 19:09:56 pop-os sshd[11124]: Server listening on 0.0.0.0 port 22.
May 07 19:09:56 pop-os sshd[11124]: Server listening on :: port 22.
May 07 19:09:56 pop-os systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
=== ALLOW SSH FROM LOCAL 192.168.1.0/24 ONLY ===
Rule added
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), deny (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
80                         ALLOW IN    Anywhere
443                        ALLOW IN    Anywhere
25                         LIMIT IN    Anywhere
587                        LIMIT IN    Anywhere
465                        LIMIT IN    Anywhere
993                        LIMIT IN    Anywhere
22/tcp                     ALLOW IN    192.168.1.0/24
80 (v6)                    ALLOW IN    Anywhere (v6)
443 (v6)                   ALLOW IN    Anywhere (v6)
25 (v6)                    LIMIT IN    Anywhere (v6)
587 (v6)                   LIMIT IN    Anywhere (v6)
465 (v6)                   LIMIT IN    Anywhere (v6)
993 (v6)                   LIMIT IN    Anywhere (v6)

=== CONFIRM PORT 22 IS LISTENING ===
tcp   LISTEN 0      4096                              0.0.0.0:22         0.0.0.0:*    users:(("sshd",pid=11124,fd=3),("systemd",pid=1,fd=151))
tcp   LISTEN 0      4096                              0.0.0.0:2222       0.0.0.0:*    users:(("docker-proxy",pid=2499,fd=7))
tcp   LISTEN 0      4096                                 [::]:22            [::]:*    users:(("sshd",pid=11124,fd=4),("systemd",pid=1,fd=153))
tcp   LISTEN 0      4096                                 [::]:2222          [::]:*    users:(("docker-proxy",pid=2506,fd=7))
=== TAILSCALE STATUS ===
● tailscaled.service - Tailscale node agent
     Loaded: loaded (/usr/lib/systemd/system/tailscaled.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-05-07 18:52:52 +08; 17min ago
       Docs: https://tailscale.com/docs/
   Main PID: 1368 (tailscaled)
     Status: "Connected; manxzo@github; 100.85.19.11 fd7a:115c:a1e0::2901:132d"
      Tasks: 21 (limit: 37034)
     Memory: 70.9M (peak: 81.5M)
        CPU: 4.334s
     CGroup: /system.slice/tailscaled.service
             └─1368 /usr/sbin/tailscaled --state=/var/lib/tailscale/tailscaled.state --socket=/run/tailscale/tailscal…

May 07 19:08:48 pop-os tailscaled[1368]: logtail: upload succeeded after 1 failures and 42s
May 07 19:08:48 pop-os tailscaled[1368]: open-conn-track: timeout opening (TCP 100.85.19.11:36230 => 13.33.45…eer node
May 07 19:08:48 pop-os tailscaled[1368]: logtail: upload: log upload of 23713 bytes compressed failed 429: ra…d per ID
May 07 19:08:53 pop-os tailscaled[1368]: open-conn-track: timeout opening (TCP 100.85.19.11:36230 => 13.33.45…eer node
May 07 19:08:59 pop-os tailscaled[1368]: open-conn-track: timeout opening (TCP 100.85.19.11:36230 => 13.33.45…eer node
May 07 19:09:07 pop-os tailscaled[1368]: open-conn-track: timeout opening (TCP 100.85.19.11:36230 => 13.33.45…eer node
May 07 19:09:08 pop-os tailscaled[1368]: logtail: upload succeeded after 1 failures and 20s
May 07 19:09:09 pop-os tailscaled[1368]: logtail: upload: log upload of 23463 bytes compressed failed 429: ra…d per ID
May 07 19:09:28 pop-os tailscaled[1368]: logtail: upload succeeded after 1 failures and 20s
May 07 19:09:29 pop-os tailscaled[1368]: logtail: upload: log upload of 24002 bytes compressed failed 429: ra…d per ID
Hint: Some lines were ellipsized, use -l to show in full.
100.85.19.11    pop-os-1               manxzo@    linux    -
100.96.21.4     fablab-tantanly        manxzo@    linux    offline, last seen 102d ago
100.115.222.44  jetson-desktop         manxzo@    linux    offline, last seen 28m ago
100.122.132.99  manzo-legion-7-16irx9  manxzo@    linux    -
100.74.24.67    nx809j                 manxzo@    android  -
100.121.46.89   openwrt                manxzo@    linux    -
100.100.68.125  pop-os                 manxzo@    linux    -
100.119.190.44  samsung-sm-s711b       manxzo@    android  offline, last seen 147d ago
100.117.43.123  sm-p619                manxzo@    android  offline, last seen 21d ago
100.81.29.37    tantanly-pi            manxzo@    linux    offline, last seen 77d ago
100.71.14.82    ubuntu                 vpadmasm@  linux    offline, last seen 179d ago
100.96.13.10    vps-2dbce29f           manxzo@    linux    offline, last seen 37d ago
100.113.148.21  vps-d8e1403f-1         manxzo@    linux    -
100.127.203.88  vps-d8e1403f           manxzo@    linux    offline, last seen 31d ago

# Health check:
#     - Some peers are advertising routes but --accept-routes is false
2026/05/07 19:09:56 portmap: monitor: gateway and self IP changed: gw=192.168.88.1 self=192.168.88.5

Report:
	* Time: 2026-05-07T11:10:02.112629649Z
	* UDP: true
	* IPv4: yes, 183.90.83.108:50837
	* IPv6: no, but OS has support
	* MappingVariesByDestIP: false
	* PortMapping:
	* CaptivePortal: false
	* Nearest DERP: Singapore
	* DERP latency:
		- sin: 9.5ms   (Singapore)
		- blr: 47.6ms  (Bengaluru)
		- hkg: 47.6ms  (Hong Kong)
		- tok: 74.8ms  (Tokyo)
		- syd: 103.7ms (Sydney)
		- dbi: 159.6ms (Dubai)
		- par: 164.8ms (Paris)
		- fra: 165.3ms (Frankfurt)
		- sfo: 171.2ms (San Francisco)
		- mad: 172.7ms (Madrid)
		- lhr: 173.6ms (London)
		- nue: 176.9ms (Nuremberg)
		- sea: 178.4ms (Seattle)
		- ams: 179.9ms (Amsterdam)
		- lax: 182.5ms (Los Angeles)
		- waw: 188.2ms (Warsaw)
		- hel: 196.4ms (Helsinki)
		- den: 208.1ms (Denver)
		- ord: 214.2ms (Chicago)
		- dfw: 217.3ms (Dallas)
		- hnl: 224.2ms (Honolulu)
		- nyc: 229.2ms (New York City)
		- iad: 236.6ms (Ashburn)
		- mia: 243.5ms (Miami)
		- tor: 243.5ms (Toronto)
		- jnb: 343.9ms (Johannesburg)
		- nai: 344ms   (Nairobi)
		- sao: 350.3ms (São Paulo)
=== RECENT TAILSCALE LOGS === journalctl -u tailscaled -n 100 --no-pager
=== SERVER LAN IPs ===
192.168.88.5 100.85.19.11 172.20.0.1 172.18.0.1 172.17.0.1 172.21.0.1 172.19.0.1 fd00::a390:66c6:708c:b40d fd00::46dd:5280:c15:d455 fd7a:115c:a1e0::2901:132d
zsh: command not found: About
zsh: command not found: No
zsh: command not found: Resources
zsh: command not found: Readme
zsh: command not found: Activity
zsh: command not found: Stars
zsh: command not found: 0
zsh: command not found: Watchers
zsh: command not found: 0
zsh: command not found: Forks
zsh: command not found: 0
zsh: command not found: Releases
zsh: command not found: No
zsh: command not found: Create
zsh: command not found: Packages
zsh: command not found: No
zsh: command not found: Publish
zsh: command not found: Contributors
cd: no such entry in dir stack
zsh: command not found: @manxzo
zsh: command not found: manxzo
zsh: command not found: Footer
(base) ➜  ~

