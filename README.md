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
```
i        # insert mode
Esc      # normal mode
:wq      # save and quit
:q!      # quit without saving
/word    # search forward
n        # next match
N        # previous match
```


## Archiving and Compression

### Create compressed archive of a directory
sudo tar -czf javed.tar.gz /data/javed

### Create archive directly in target directory
sudo tar -czf /home/javed.tar.gz /data/javed

### List contents of a tar.gz without extracting
tar -tzf /home/javed.tar.gz

## Directory Navigation Basics (Linux)
```
### Home directory shortcut
~            # current user's home directory
cd ~         # go to home directory
cd           # go to home directory

### Root of filesystem
/            # root directory (top of filesystem)
cd /         # move to filesystem root

### Common navigation commands
cd ..        # move up one directory
cd -         # switch to previous directory
pwd          # print current directory

### Useful checks
echo ~       # show expanded home directory path
ls /         # list top-level system directories
```
## Grant executable permission to a script (all users)

### SSH to App Server 3
ssh banner@172.16.238.12

### Grant execute permission to all users
sudo chmod a+x /tmp/xfusioncorp.sh

### Verify permissions
ls -l /tmp/xfusioncorp.sh

### Set user owner and group owner to root
sudo chown root:root /etc/hosts

### Set file permissions so others have read-only access
sudo chmod 644 /etc/hosts

### Remove all permissions for user jim
sudo setfacl -m u:jim:--- /etc/hosts

### Grant read-only permission to user jerome
sudo setfacl -m u:jerome:r-- /etc/hosts

### Verify ACLs and permissions
getfacl /etc/hosts
ls -l /etc/hosts


### What 644 means (octal notation)
- 6 = owner → read (4) + write (2) = rw-
- 4 = group → read only = r--
- 4 = others → read only = r--

### Resulting permission string
-rw-r--r--

### Effect
- Owner (root) can read and modify the file
- Group can read the file
- Others can read the file
- No one except the owner can modify it

### Why 644 is commonly used
- Standard permission for system config files
- Prevents unauthorized modification
- Allows system services and users to read the file

### Relation with ACLs
- `chmod` sets baseline permissions
- `setfacl` adds user-specific exceptions
- ACLs refine permissions, they do not replace `chmod`

### One-line rule
`chmod 644` → only the owner can edit; everyone else can read

## replace string inside a file (in-place edit)

### replace all occurrences of a string in a file
sudo sed -i 's/About/Software/g' /root/nautilus.xml

### verify replacement
grep About /root/nautilus.xml
grep Software /root/nautilus.xml

### replace string without modifying file (preview)
sed 's/About/Software/g' /root/nautilus.xml

### replace string and create backup
sudo sed -i.bak 's/About/Software/g' /root/nautilus.xml

### one-line rule
sed -i 's/old/new/g' file

# become root
sudo -i

# check if cron.allow is incorrectly created as a directory
ls -ld /etc/cron.allow

# remove cron.allow directory if it exists (cron expects a file)
rm -rf /etc/cron.allow

# create cron.allow file and allow mariyam
vi /etc/cron.allow
# add inside:
mariyam

# create or edit cron.deny file and deny rod
vi /etc/cron.deny
# add inside:
rod

# set correct ownership and permissions
chown root:root /etc/cron.allow /etc/cron.deny
chmod 600 /etc/cron.allow /etc/cron.deny

# verify access
su - mariyam
crontab -e

su - rod
crontab -e


