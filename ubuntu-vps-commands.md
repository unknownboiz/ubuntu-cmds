# Linux Ubuntu VPS Commands Cheatsheet

This document contains essential commands for managing an Ubuntu VPS (Virtual Private Server). Organized by category for quick reference.

---

## 📦 Package Management

| Command | Description |
|---------|-------------|
| `sudo apt update` | Update package index |
| `sudo apt upgrade` | Upgrade all installed packages |
| `sudo apt install <package>` | Install a new package |
| `sudo apt remove <package>` | Remove a package (keep config files) |
| `sudo apt purge <package>` | Remove a package and its config files |
| `sudo apt search <term>` | Search for packages |
| `apt list --installed` | List installed packages |
| `sudo apt autoremove` | Remove unused dependencies |

---

## 🔄 System Update & Upgrade

```bash
# Full system upgrade (including dist upgrade)
sudo apt update && sudo apt full-upgrade -y

# Reboot after kernel update
sudo reboot
```

---

## 👥 User Management

| Command | Description |
|---------|-------------|
| `adduser <username>` | Create a new user with home directory |
| `adduser <username> sudo` | Add user to sudo group (Ubuntu) |
| `passwd <username>` | Change user password |
| `deluser <username>` | Delete a user (keep home directory) |
| `deluser --remove-home <username>` | Delete user and home directory |
| `whoami` | Show current user |
| `id <username>` | Show user UID/GID info |

---

## 📁 File & Directory Operations

| Command | Description |
|---------|-------------|
| `cd <path>` | Change directory |
| `ls` / `ls -l` | List files (detailed) |
| `ls -a` | Show hidden files |
| `mkdir -p <path>` | Create directory (and parents) |
| `rm -r <dir>` | Remove directory recursively |
| `rm -f <file>` | Force remove file |
| `cp <src> <dst>` | Copy file/folder |
| `mv <src> <dst>` | Move/rename file/folder |
| `cat <file>` | Display file content |
| `less <file>` | View file content (paged) |
| `head -n <file>` | Show first n lines |
| `tail -n <file>` | Show last n lines |
| `chmod <permissions> <file>` | Change file permissions |
| `chown <user>:<group> <file>` | Change file ownership |
| `touch <file>` | Create empty file or update timestamp |

---

## 🌐 Network Commands

| Command | Description |
|---------|-------------|
| `ip addr` / `ifconfig` | Show IP addresses |
| `ip route` | Show routing table |
| `ping <host>` | Test network connectivity |
| `curl -I <url>` | Check HTTP headers |
| `wget <url>` | Download file via HTTP/HTTPS |
| `speedtest-cli` | Test internet speed (install via apt) |
| `netstat -tulnp` | Show listening ports (install `net-tools` if needed) |
| `ss -tulnp` | Modern alternative to netstat |
| `hostname -I` | Show local IP address |
| `traceroute <host>` | Trace network path |

*Common network tools installation:*
```bash
sudo apt install net-tools curl wget
```

---

## 🛠️ Service Management (systemd)

| Command | Description |
|---------|-------------|
| `systemctl status <service>` | Check service status |
| `systemctl start <service>` | Start a service |
| `systemctl stop <service>` | Stop a service |
| `systemctl restart <service>` | Restart a service |
| `systemctl enable <service>` | Enable auto-start at boot |
| `systemctl disable <service>` | Disable auto-start at boot |
| `systemctl list-units --type=service` | List all services |
| `journalctl -u <service>` | View service logs |
| `journalctl -f` | Follow service logs (live) |

*Common examples:*
```bash
# Nginx
sudo systemctl restart nginx
sudo systemctl enable nginx

# Apache
sudo systemctl restart apache2
sudo systemctl enable apache2

# MySQL / MariaDB
sudo systemctl restart mysql
sudo systemctl enable mysql
```

---

## 📊 System Monitoring

| Command | Description |
|---------|-------------|
| `top` | Interactive process viewer |
| `htop` | Modern interactive process viewer (install via apt) |
| `free -h` | Show memory usage in human-readable format |
| `df -h` | Show disk space usage |
| `du -sh <dir>` | Show directory size |
| `uptime` | Show system uptime and load |
| `cat /proc/cpuinfo` | Show CPU information |
| `cat /proc/meminfo` | Show memory information |
| `vmstat 1` | Report virtual memory statistics |

---

## 🔒 Security Basics

| Command | Description |
|---------|-------------|
| `ufw status` | Check UFW firewall status |
| `sudo ufw enable` | Enable firewall |
| `sudo ufw allow <port>` | Allow port through firewall |
| `sudo ufw allow ssh` | Allow SSH connections |
| `sudo ufw deny <port>` | Block port through firewall |
| `sudo ufw default deny incoming` | Deny all incoming by default |
| `sudo ufw default allow outgoing` | Allow all outgoing by default |
| `sudo apt install fail2ban` | Install fail2ban (brute-force protection) |
| `sudo systemctl start fail2ban` | Start fail2ban |
| `sudo grep -r "password" /etc/ssh/sshd_config` | Check SSH config for password auth |

*Basic UFW examples:*
```bash
# Allow common services
sudo ufw allow 22/tcp    # SSH
sudo ufw allow 80/tcp    # HTTP
sudo ufw allow 443/tcp   # HTTPS

# Delete a rule
sudo ufw delete allow 22/tcp
```

---

## 🔑 SSH & Remote Access

| Command | Description |
|---------|-------------|
| `ssh user@hostname` | Connect to remote server via SSH |
| `ssh -p <port> user@host` | Connect via custom SSH port |
| `ssh-keygen -t rsa -b 4096` | Generate SSH key pair |
| `ssh-copy-id user@host` | Copy public key to remote server |
| `sshd -T` | Test SSH server configuration |

*To disable password authentication after setting up keys:*
```bash
sudo nano /etc/ssh/sshd_config
# Set: PasswordAuthentication no
sudo systemctl restart sshd
```

---

## 💿 Disk & Storage

| Command | Description |
|---------|-------------|
| `lsblk` | List block devices |
| `fdisk -l` | List disk partitions |
| `mount | grep /dev` | Show mounted file systems |
| `swapon -s` | Show swap spaces |
| `crontab -e` | Edit cron jobs for scheduled tasks |
| `crontab -l` | List current cron jobs |

*Common cron example (run backup daily at 2 AM):*
```bash
0 2 * * * /path/to/backup/script.sh
```

---

## 📝 Useful One-Liners

```bash
# Update & upgrade everything
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y

# Show system information (install neofetch or fetch via apt)
neofetch

# Check disk usage of top 5 largest directories
du -sh /* | sort -hr | head -n 5

# Find large files (>100MB) in /var
find /var -type f -size +100M -exec ls -lh {} \;

# Empty a large log file without deleting it
> /var/log/syslog

# Show free and used memory
free -m

# Show disk space
df -h
```

---

## 🛡️ Quick Reference Cheat Sheet

```
# System basics
sudo apt update && sudo apt upgrade -y         # Update system
neofetch                                      # Show system info

# User management
adduser deploy                                # Create user
usermod -aG sudo deploy                       # Add user to sudo

# Network
ip addr                                       # Show IPs
ping -c 4 google.com                          # Test connectivity
sudo ufw enable                               # Enable firewall
sudo ufw allow ssh                            # Allow SSH
sudo ufw allow 80/tcp                         # Allow HTTP
sudo ufw allow 443/tcp                        # Allow HTTPS

# Services
sudo systemctl restart nginx                  # Restart Nginx
sudo systemctl status mysql                     # Check MySQL status

# Monitoring
top                                           # Process monitor
df -h                                         # Disk space
free -h                                       # Memory usage

# SSH
ssh user@your-vps-ip                          # Connect via SSH
ssh-keygen -t rsa                               # Generate SSH key
ssh-copy-id user@host                         # Copy key to server
```

---

*Last updated: 2026*

---
## 🐳 Docker & Container Management

| Command | Description |
|---------|-------------|
| `docker --version` | Check Docker version |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers |
| `docker images` | List Docker images |
| `docker pull <image>` | Pull image from registry |
| `docker run -d -p 80:80 <image>` | Run container in detached mode |
| `docker stop <container>` | Stop a running container |
| `docker start <container>` | Start a stopped container |
| `docker rm <container>` | Remove a container |
| `docker rmi <image>` | Remove an image |
| `docker logs <container>` | View container logs |
| `docker exec -it <container> /bin/bash` | Execute command in running container |
| `docker compose up -d` | Start containers defined in docker-compose |
| `docker compose down` | Stop and remove containers |

*Docker installation:*
```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl start docker
sudo systemctl enable docker
```

---

## 🟢 Node.js & npm

| Command | Description |
|---------|-------------|
| `node --version` | Check Node.js version |
| `npm --version` | Check npm version |
| `npm install -g <package>` | Install global package |
| `npm init -y` | Initialize new Node.js project |
| `npm install` | Install project dependencies |
| `npm run` | List available npm scripts |
| `npm build` | Build the project |
| `pm2 list` | List running processes managed by PM2 |
| `pm2 start <app>` | Start application with PM2 |
| `pm2 restart all` | Restart all managed apps |
| `pm2 logs` | View PM2 logs |

*Node.js setup:*
```bash
# Install Node.js via NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
nvm install 20

# Or install via apt
sudo apt install nodejs npm -y
```

---

## 🐍 Python & Pip

| Command | Description |
|---------|-------------|
| `python3 --version` | Check Python version |
| `pip3 --version` | Check pip version |
| `pip3 install <package>` | Install Python package |
| `pip3 install --upgrade pip` | Upgrade pip |
| `python3 -m venv venv` | Create virtual environment |
| `source venv/bin/activate` | Activate virtual environment |
| `pip3 install -r requirements.txt` | Install from requirements file |
| `python3 manage.py runserver` | Start Django development server |
| `python3 app.py` | Run Python application |

*Python setup:*
```bash
# Install Python tools
sudo apt install python3-pip python3-venv -y

# Create and use virtual environment
python3 -m venv myenv
source myenv/bin/activate
pip install django flask
```

---

## 📜 Text Processing & Editing

| Command | Description |
|---------|-------------|
| `nano <file>` | Simple text editor |
| `vim <file>` | Advanced text editor |
| `sed -i 's/find/replace/g' <file>` | In-place text replacement |
| `awk '{print $1}' <file>` | Extract first column |
| `grep -r "pattern" .` | Recursive search in directory |
| `sort <file>` | Sort file contents |
| `uniq <file>` | Remove duplicate lines |
| `cut -d',' -f1 <file>` | Extract specific field |
| `wc -l <file>` | Count lines in file |
| `file <file>` | Determine file type |

---

## 🌿 Git Essentials

| Command | Description |
|---------|-------------|
| `git --version` | Check Git version |
| `git config --global user.name "Name"` | Set global username |
| `git config --global user.email "email"` | Set global email |
| `git init` | Initialize new Git repo |
| `git clone <url>` | Clone remote repository |
| `git status` | Check repository status |
| `git add <file>` | Stage changes |
| `git commit -m "message"` | Commit changes |
| `git push origin main` | Push to remote |
| `git pull origin main` | Pull from remote |
| `git branch` | List branches |
| `git branch -a` | List all branches |
| `git checkout -b <branch>` | Create and switch to new branch |
| `git merge <branch>` | Merge branch |

*Git setup for new repo:*
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:username/repo.git
git push -u origin main
```

---

## 🗄️ Database Management

| Command | Description |
|---------|-------------|
| `mysql -u root -p` | Login to MySQL |
| `show databases;` | List databases |
| `use <database>;` | Select database |
| `show tables;` | List tables |
| `create database <name>;` | Create new database |
| `create user '<user>'@'%' identified by '<pass>';` | Create MySQL user |
| `grant all privileges on <database>.* to '<user>'@'%';` | Grant user permissions |
| `flush privileges;` | Reload permissions |
| `mysqldump -u root -p <database> > backup.sql` | Backup database |
| `mysql < database < backup.sql` | Restore database |

*PostgreSQL commands:*
```bash
psql -U postgres          # Login
\l                      # List databases
\dt                     # List tables
CREATE DATABASE mydb;   # Create database
\c mydb                 # Connect to database
\dt                     # List tables in current DB
```

---

## 📁 Advanced File Management

| Command | Description |
|---------|-------------|
| `find /path -type f -name "pattern"` | Find files by name |
| `find /path -type f -size +100M` | Find files larger than 100MB |
| `xargs command` | Build and execute command from input |
| `alias ll='ls -la'` | Create command alias |
| `alias update='sudo apt update && sudo apt upgrade -y'` | Create shortcut |
| `history` | Show command history |
| `!!` | Re-run last command |
| `!n` | Re-run command number n |
| `ctrl+r` | Reverse search history |

*File permissions octal notation:*
```bash
# 755 = rwxr-xr-x (owner full, group/others read+execute)
chmod 755 script.sh

# 644 = rw-r--r-- (owner read+write, group/others read)
chmod 644 index.html

# 777 = rwxrwxrwx (everyone full access - avoid in production!)
chmod 777 file
```

---

## 🔐 Advanced Security

| Command | Description |
|---------|-------------|
| `sudo passwd -l root` | Lock root account |
| `sudo passwd -u root` | Unlock root account |
| `sudo chage -E -1 <username>` | Disable account expiration |
| `sudo chage -d 0 <username>` | Force password change on next login |
| `grep root /etc/passwd` | Check root user status |
| `last | head -n 20` | Show last 20 login attempts |
| `lastb | head -n 10` | Show failed login attempts |
| `chroot <directory> /bin/bash` | Change root directory (chroot) |
| `apt-get build-dep <package>` | Install build dependencies |

*Firewall rules with UFW (detailed):*
```bash
# Check current status
sudo ufw status verbose

# Reset firewall to defaults
sudo ufw reset

# Deny specific IP
sudo ufw deny from 203.0.113.50

# Allow specific IP
sudo ufw allow from 203.0.113.50 to any port 22

# Enable with specific policy
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable

# Show numbered list for easy deletion
sudo ufw status numbered

# Delete rule by number
sudo ufw delete 3
```

---

## 📊 Process Management

| Command | Description |
|---------|-------------|
| `ps aux | grep <process>` | Find running processes |
| `pkill <process>` | Kill process by name |
| `kill <PID>` | Kill process by ID |
| `kill -9 <PID>` | Force kill process (SIGKILL) |
| `renice <priority> -p <PID>` | Change process priority |
| `bg` | Move stopped job to background |
| `fg` | Bring background job to foreground |
| `jobs` | List background jobs |
| `disown -h <job>` | Remove job from shell tracking |

*Common process signals:*
```bash
# Graceful shutdown
kill <PID>

# Force terminate
kill -9 <PID>

# Reload configuration
kill -HUP <PID>

# Graceful restart
kill -TERM <PID>
```

---

## 📦 Snap Package Management

| Command | Description |
|---------|-------------|
| `snap --version` | Check Snap version |
| `snap list` | List installed Snap packages |
| `snap install <package>` | Install Snap package |
| `snap remove <package>` | Remove Snap package |
| `snap refresh <package>` | Refresh Snap to latest version |
| `snap changes` | Show recent Snap changes |

*Common Snap installations:*
```bash
sudo snap install core        # Install core snap
sudo snap install firefox     # Install Firefox
sudo snap install docker      # Install Docker via Snap
sudo snap install --classic certbot  # Install Certbot with full access
```

---

## 🌐 Web Server Configuration (Nginx/Apache)

| Command | Description |
|---------|-------------|
| `nginx -t` | Test Nginx configuration |
| `nginx -s reload` | Reload Nginx config gracefully |
| `a2enmod <module>` | Enable Apache module (e.g., rewrite, ssl) |
| `a2endis <module>` | Disable Apache module |
| `a2ensite <site>` | Enable Apache site |
| `a2dissite <site>` | Disable Apache site |
| `certbot --nginx` | Install Let's Encrypt certificate for Nginx |
| `certbot --apache` | Install Let's Encrypt certificate for Apache |
| `crontab -e` | Edit cron for auto-renewal |

*Nginx configuration common paths:*
```bash
# Main config file
/etc/nginx/nginx.conf

# Site configurations
/etc/nginx/sites-available/
/etc/nginx/sites-enabled/

# Enable site symlink
sudo ln -s /etc/nginx/sites-available/mysite /etc/nginx/sites-enabled/

# Test and reload
sudo nginx -t
sudo systemctl reload nginx
```

---

## 📈 System Resource Monitoring (Advanced)

| Command | Description |
|---------|-------------|
| `pidstat 1` | Report processor activities |
| `iostat -xz 1` | I/O statistics |
| `netstat -i` | Network interface statistics |
| `sar -u 1 3` | CPU utilization summary |
| `sar -d 1 3` | Disk activity summary |
| `mpstat 1` | Report processors' statistics |
| `free -s 1` | Refresh memory usage every second |
| `vmstat 5` | Report virtual memory statistics every 5s |

*System load average explanation:*
- **Load 1.0** = average over last 1 minute
- **Load 5.0** = average over last 5 minutes  
- **Load 15.0** = average over last 15 minutes
- On a single-core system: load > 1.0 means system is overloaded
- On a 4-core system: load > 4.0 means system is overloaded

---

## 🔄 Service Lifecycle Commands (Complete Reference)

| Action | Command |
|--------|---------|
| List all services | `systemctl list-units --type=service --all` |
| List running services | `systemctl list-units --type=service --state=running` |
| List failed services | `systemctl list-units --type=service --state=failed` |
| Enable at boot | `systemctl enable <service>` |
| Disable at boot | `systemctl disable <service>` |
| Mask service (prevent start) | `systemctl mask <service>` |
| Unmask service | `systemctl unmask <service>` |
| Show service type | `systemctl show <service> --property=Type` |
| Show service description | `systemctl show <service> --property=Description` |
| Show service dependencies | `systemctl show <service> --property=Into` |

*Common service management workflow:*
```bash
# Complete restart with status check
sudo systemctl restart nginx
sudo system status nginx
# Or: sudo systemctl reload-or-restart nginx

# Check if service is active/running
systemctl is-active nginx    # Returns: active/inactive/failed
systemctl is-enabled nginx   # Returns: enabled/disabled/static

# Log viewing
journalctl -u nginx --since "1 hour ago"
journalctl -u nginx -f      # Follow logs live
```

---

## 💾 Backup & Recovery Scripts

*Simple backup script (save as /usr/local/bin/backup.sh):*
```bash
#!/bin/bash
# VPS Backup Script
# Edit these variables
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/backups"
SOURCE_DIR="/var/www"
DB_USER="root"
DB_PASS="your_password"

# Create backup directory
mkdir -p ${BACKUP_DIR}

# Backup website files
tar -czf ${BACKUP_DIR}/www_${DATE}.tar.gz ${SOURCE_DIR}

# Backup database
mysqldump -u ${DB_USER} -p${DB_PASS} --all-databases | gzip > ${BACKUP_DIR}/db_${DATE}.sql.gz

# Keep only last 7 days of backups
find ${BACKUP_DIR} -name "*.tar.gz" -o -name "*.sql.gz" | sort -r | tail -n +8 | xargs rm -f

echo "Backup completed: ${DATE}"
```

*Make script executable and add to cron:*
```bash
chmod +x /usr/local/bin/backup.sh
# Add to crontab (run daily at 3 AM)
0 3 * * * /usr/local/bin/backup.sh >> /var/log/backup.log 2>&1
```

---

## ⚡ Quick Kill All Commands

| Situation | Command |
|-----------|---------|
| Kill all Node processes | `pkill -f node` |
| Kill all Python processes | `pkill -f python` |
| Kill all processes by user | `pkill -u username` |
| Kill process using port 3000 | `fuser -k 3000/tcp` or `kill $(lsof -t -i:3000)` |
| Reset Apache/MySQL | `sudo systemctl restart apache2` / `sudo systemctl restart mysql` |
| Clear memory cache | `sync; echo 3 | sudo tee /proc/sys/vm/drop_caches` |

*Memory caching explanation:*
- `drop_caches` frees pagecache, dentries, and inodes
- Useful after running memory-intensive operations
- **Warning**: Only use on production if you know what you're doing
- Better to use `swap` management instead

---

## 🌍 Internationalization & Localization

| Command | Description |
|---------|-------------|
| `locale -a` | List available locales |
| `dpkg-reconfigure locales` | Configure available locales |
| `export LANG=en_US.UTF-8` | Set system language |
| `update-locale LANG=en_US.UTF-8` | Permanently set language |

*Common locale installations:*
```bash
sudo apt install locales
sudo locale-gen en_US.UTF-8
sudo dpkg-reconfigure locales
```

---

## 📦 Flatpak Management

| Command | Description |
|---------|-------------|
| `flatpak --version` | Check Flatpak version |
| `flatpak list` | List installed Flatpaks |
| `flatpak install <ref>` | Install Flatpak application |
| `flatpak remove <app>` | Remove Flatpak application |
| `flatpak update` | Update all Flatpaks |
| `flatpak search <term>` | Search for Flatpaks |

*Common Flatpak installations:*
```bash
sudo apt install flatpak flatpak-builder
flatpak install flathub org.mozilla.firefox
flatpak install flathub org.gimp.GIMP
```

---

## 🎯 Complete VPS Initialization Checklist

```bash
# 1. Initial login and system update
ssh root@your-vps-ip
sudo apt update && sudo apt upgrade -y

# 2. Create non-root user with sudo
adduser deploy
usermod -aG sudo deploy

# 3. Set up SSH key authentication
su - deploy
ssh-keygen -t rsa -b 4096
# Copy public key to server: ssh-copy-id deploy@your-vps-ip
# Disable password auth: sudo nano /etc/ssh/sshd_config, set PasswordAuthentication no

# 4. Configure firewall
sudo ufw default allow outgoing
sudo ufw default deny incoming
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable

# 5. Install essential tools
sudo apt install net-tools htop vim curl wget git -y

# 6. Set up time synchronization
sudo apt install chrony -y
sudo systemctl enable chronyd
sudo systemctl start chronyd

# 7. Install web server (choose one)
# Nginx: sudo apt install nginx -y / sudo systemctl enable nginx
# Apache: sudo apt install apache2 -y / sudo systemctl enable apache

# 8. Install database (choose one)
# MySQL: sudo apt install mysql-server -y / sudo mysql_secure_installation
# PostgreSQL: sudo apt install postgresql postgresql-contrib -y

# 9. Install SSL certificate
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

# 10. Set up automatic updates
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

---

*Last updated: 2026*

*Comprehensive Linux Ubuntu VPS Commands Documentation*
*Contains over 300 commands across 15+ categories for VPS administration, development, security, and monitoring.*

*Tip: Bookmark this document or copy to /root/ for quick reference during VPS management tasks.*