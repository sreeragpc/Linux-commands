# Linux-commands

## creating and adding a user to a usergroup
sudo groupadd nautilus_admin_users
sudo useradd rajesh
sudo usermod -aG nautilus_admin_users sonya
sudo id sonya

## useradd without shell permission (used for service users)
sudo useradd -m -s /sbin/nologin ravi

## useradd without home directory
sudo useradd -M ravi

## useradd with expiry
sudo useradd -m username -e YYYY-MM-DD
sudo chage -l username

## change expiry for existing user
sudo chage -E YYYY-MM-DD username

## remove expiry (never expires)
sudo chage -E -1 username

## userdata transfer while maintaining directory structure
sudo find /home/usersdata -type f -user yousuf -exec cp --parents {} /media \;

## copy files from one server to another server
scp /tmp/index.html natasha@ststor01:/tmp/

## move files
sudo mv /tmp/index.html /usr/src/kodekloudrepos/official/

## copy directory (recursive)
sudo cp -r ecommerce.git /backup/

## delete all files inside a directory (keep directory)
sudo rm -rf /path/to/dir/*

## install git on centos/rhel
sudo yum install -y git

## uninstall git on centos/rhel
sudo yum remove -y git

## create a bare git repository
sudo git init --bare /opt/media.git

## clone a bare repository
cd /usr/src/kodekloudrepos
sudo git clone /opt/beta.git

## check git remotes (inside a cloned repo)
git remote -v

## disable root ssh login (security hardening)
sudo vi /etc/ssh/sshd_config
# set:
PermitRootLogin no

## alternative (recommended) drop-in ssh config
sudo vi /etc/ssh/sshd_config.d/99-disable-root.conf
PermitRootLogin no

## restart ssh service
sudo systemctl restart sshd

## verify effective ssh configuration
sudo sshd -T | grep permitrootlogin

## test root ssh (should fail)
ssh root@server_ip

## vi editor basics
i        # insert mode
Esc      # normal mode
:wq      # save and quit
:q!      # quit without saving
/word    # search forward
n        # next match
N        # previous match
