# Linux-commands


## creating and adding a user to a usergroup
```
sudo groupadd nautilus_admin_users
sudo useradd rajesh
sudo usermod -aG nautilus_admin_users sonya
sudo id sonya
```
## useradd without shell permission usedfor service users etc
```
sudo useradd -m -s /usr/sbin/nologin ravi
```
## useradd without home directory
```
sudo useradd -M ravi
```
## useradd with expiry
```
sudo useradd -m username -e YYYY-MM-DD
```

## userdata transfer by maintaing file structure
```
sudo find /home/usersdata -type f -user yousuf -exec cp --parents {} /media \;

```
