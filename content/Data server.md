### Creating user

Log in as root
```
ssh root@10.36.17.152
```

Create user directory for new user
```
useradd -m -d /mnt/pve/Homes/<username directory name> <username>
```

Add the newly created user into the sudo group
```
usermod -aG sudo <username>
```

Make user's default shell as bash
```
chsh -s /bin/bash <username>
```

Set username's password. It will prompt for typing your new password.

```
passwd <username>
```

Deleting a user. This command recursively deletes everything related to user including its home directory.

```
sudo userdel -r <username>
```


### Speedtest

Run this command to know about internet download speed. Note that these speeds are dependent on which server is selected for communications.

```
speedtest-cli
```
