## Trying to enable SSH into Linux computers again

#### Status checks and logs
sudo systemctl status sshd
sudo ufw status
netstat -tuln | grep 22
sudo journalctl -u ssh
sudo cat /var/log/auth.log
ip a


#### Things to try
sudo systemctl restart sshd
chmod 700 ~/.ssh 
chmod 600 ~/.ssh/id_* # Private keys
