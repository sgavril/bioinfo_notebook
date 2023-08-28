# Setting up SSH on Ubuntu machine

### Check service
```
sudo systemctl status sshd

# If not running
sudo systemctl start sshd
```

### Check logs
```
cat /var/log/auth.log

cat /etc/ssh/sshd_config

ls -l ~/.ssh # Should be 700
ls -l ~/.ssh/authorized_keys # Should be 600
```

### After making changes
```
sudo systemctl restart sshd
```

### Other commands to troubleshoot
```
ss -tuln # see if ssh is running and which port
ifconfig # Check network interfaces
iptables -L # firewall rules
```