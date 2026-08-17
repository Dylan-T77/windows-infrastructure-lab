# Linux Command Reference

A practical quick-reference for Linux administration, networking and troubleshooting.

> Commands are written primarily for Ubuntu/Debian-based systems. Some commands may differ on other distributions.

## System Information

```bash
uname -a
cat /etc/os-release
hostnamectl
uptime
whoami
id
```

## CPU, Memory and Disk

```bash
lscpu
free -h
df -h
du -sh /path/to/directory
lsblk
```

## Processes

```bash
ps aux
ps aux | grep <process>
top
htop
pgrep <process>
kill <PID>
```

## Files and Directories

```bash
pwd
ls -lah
cd /path/to/directory
mkdir <directory>
touch <file>
cp <source> <destination>
mv <source> <destination>
rm <file>
rm -r <directory>
find /path -name "<pattern>"
```

## Permissions and Ownership

```bash
ls -l
chmod 644 <file>
chmod 755 <directory>
chown <user>:<group> <file>
```

## Networking

```bash
ip addr
ip route
ip link
ping <host>
ss -tulpn
ip neigh
hostname -I
```

## DNS

```bash
resolvectl status
resolvectl query <hostname>
host <hostname>
dig <hostname>
```

## Services / systemd

```bash
systemctl status <service>
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl enable <service>
systemctl disable <service>
systemctl list-units --type=service
```

## Logs

```bash
journalctl
journalctl -b
journalctl -u <service>
journalctl -p err -b
```

## Package Management — Debian/Ubuntu

```bash
sudo apt update
sudo apt upgrade
sudo apt install <package>
sudo apt remove <package>
sudo apt purge <package>
sudo apt autoremove
apt search <package>
```

## Users and Groups

```bash
whoami
id <user>
getent passwd <user>
getent group <group>
sudo adduser <user>
sudo usermod -aG <group> <user>
sudo passwd <user>
```

## SSH

```bash
ssh <user>@<host>
ssh -p <port> <user>@<host>
scp <file> <user>@<host>:/path/
```

## Firewall — UFW

```bash
sudo ufw status verbose
sudo ufw allow 22/tcp
sudo ufw deny <port>
sudo ufw delete allow 22/tcp
sudo ufw enable
sudo ufw disable
```

## Archives

```bash
tar -czf archive.tar.gz <directory>
tar -xzf archive.tar.gz
unzip archive.zip
```

## Troubleshooting Sequence

```bash
ip addr
ip route
resolvectl status
ping <gateway>
ping <IP>
ping <hostname>
ss -tulpn
systemctl status <service>
journalctl -u <service>
```
