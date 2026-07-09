# Linux

> The OS that runs the internet. Shell, processes, networking, systemd.

---

## Purpose

Master Linux fundamentals for backend/DevOps work.

## Prerequisites

- Command line basics.

## Learning Outcome

You can navigate, configure, and troubleshoot Linux servers.

## Dependencies

- A Linux system (or WSL/macOS).

## Related Files

- [Docker/](../Docker/) · [Kubernetes/](../Kubernetes/) · [Cloud/](../Cloud/) · [CHEATSHEET.md#shell](../CHEATSHEET.md#shell)

## AI Instructions

When working with Linux:
1. Use `man <cmd>` for help.
2. Don't run as root.
3. Use `sudo` for privileged ops.
4. Use SSH keys, not passwords.
5. Use `ufw` / `iptables` for firewall.
6. Use systemd for services.
7. Monitor with `htop`, `iotop`, `dstat`.

## Human Notes

### Essential commands
```bash
# Navigation
pwd, ls, cd, tree

# Files
cat, less, head, tail, touch, mkdir, rm, cp, mv, ln
find, fd, rg (ripgrep)
chmod, chown

# Process
ps, top, htop, kill, killall, jobs, bg, fg, nohup, disown
systemctl, journalctl

# Networking
ping, traceroute, dig, nslookup
netstat, ss, lsof -i
curl, wget
ip, ifconfig

# Disk
df, du, lsblk, mount, umount
dd, rsync

# Users
whoami, id, su, sudo, useradd, usermod, passwd

# Text
grep, sed, awk, sort, uniq, cut, tr, tee
jq, yq (JSON/YAML)

# Archives
tar, gzip, gunzip, zip, unzip

# SSH
ssh, scp, sftp, ssh-keygen, ssh-copy-id
~/.ssh/config
```

### SSH
```bash
ssh-keygen -t ed25519
ssh-copy-id user@host
```

`~/.ssh/config`:
```
Host myserver
  HostName example.com
  User alice
  Port 22
  IdentityFile ~/.ssh/id_ed25519
```

### systemd
```bash
systemctl status nginx
systemctl start nginx
systemctl enable nginx
systemctl restart nginx
journalctl -u nginx -f
```

### Service file
`/etc/systemd/system/myapp.service`:
```ini
[Unit]
Description=My App
After=network.target

[Service]
Type=simple
User=appuser
WorkingDirectory=/opt/myapp
ExecStart=/usr/bin/node /opt/myapp/server.js
Restart=on-failure
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```

### Permissions
```
-rwxr-xr--  user  group  size  date  name
```
- `rwx` (user) `r-x` (group) `r--` (other).
- `chmod 755 file` = rwxr-xr-x.
- `chmod +x file` = add execute.

### Cron
```cron
# m h dom mon dow command
0 8 * * * /opt/backup.sh
*/5 * * * * /opt/check.sh
```
`crontab -e` to edit.

### Processes & signals
- `kill <pid>` — SIGTERM.
- `kill -9 <pid>` — SIGKILL (no cleanup).
- `kill -HUP <pid>` — reload config.
- `nohup ./app &` — run in background, survives logout.

### Logs
- `/var/log/` for system logs.
- `journalctl` for systemd.
- `tail -f /var/log/syslog`.

### Firewall
```bash
ufw allow 22/tcp
ufw allow 80/tcp
ufw allow 443/tcp
ufw enable
ufw status
```

### Performance
- `htop` — processes.
- `iotop` — disk I/O.
- `iftop` — network.
- `dstat` — all-in-one.
- `vmstat` — VM stats.
- `free -h` — memory.
- `df -h` — disk.
- `du -sh *` — directory sizes.

### Network troubleshooting
```bash
ping example.com
traceroute example.com
dig example.com
ss -tlnp  # listening ports
lsof -i :3000  # what's on port 3000
tcpdump -i eth0 port 80
```

### Files to know
- `/etc/passwd` — users.
- `/etc/group` — groups.
- `/etc/sudoers` — sudo config.
- `/etc/hosts` — local DNS.
- `/etc/resolv.conf` — DNS resolvers.
- `/etc/environment` — system env vars.
- `~/.bashrc` / `~/.zshrc` — shell config.
- `~/.ssh/` — SSH keys + config.

### Package managers
- Debian/Ubuntu: `apt`.
- RHEL/CentOS: `dnf` / `yum`.
- Arch: `pacman`.
- Alpine: `apk`.

### Useful tools
- `tmux` — terminal multiplexer.
- `zsh` + `oh-my-zsh` — better shell.
- `starship` — cross-shell prompt.
- `fzf` — fuzzy finder.
- `ripgrep`, `fd`, `bat`, `eza` — modern coreutils.

## Common Mistakes

- ❌ Running as root.
- ❌ Password SSH login.
- ❌ No firewall.
- ❌ No fail2ban (brute-force protection).
- ❌ Manual edits without backup.
- ❌ Not using `man`.

## Tools

- Linux man pages: https://man7.org/linux/man-pages/
- Explain Shell: https://explainshell.com/
- tldr pages: https://tldr.sh/

## References

- The Linux Documentation Project: https://tldp.org/
- Linux Command: https://linuxcommand.org/

## Further Reading

- *The Linux Command Line* — William Shotts (free)
- *UNIX and Linux System Administration Handbook* — Evi Nemeth et al.

## Exercises

1. Set up a Linux VPS from scratch (user, SSH, firewall, nginx).
2. Run a Node app with systemd.
3. Diagnose a slow server.

## Projects

- Build a Linux home server (file share, media, backup).

---

**Previous:** [GitHub/](../GitHub/) · **Next:** [Cloud/](../Cloud/) · **Related:** [Docker/](../Docker/)
