```bash

#---------------------------- Folder Structure

#create chroot jail directory
sudo su
mkdir /home/jail
mkdir /home/jail/{bin,lib,lib64}

#prepare jail, give jailed user an access to ls and bash
cp /bin/ls /home/jail/bin/
cp /bin/bash /home/jail/bin/

#identify library dependecies
ldd ls
ldd bash

#copy dependencies (from ldd output)
# lib64 <- ld-linux-x86-64.so.2
# lib <- libc.so.6 libpthread.so.0 libdl.so.2 libselinux.so.1 libpcre.so.3 libtinfo.so.6


#---------------------------- Test
#test  (most of commands should not work)
chroot /home/jail/ bin/bash
#> bash-5.0# cat
#> bash: cat: command not found
#> bash-5.0# pwd
#> /
#> bash-5.0# ls
#> bin  lib  lib64



#---------------------------- Users

#create rest users
groupadd jailed_users
useradd -g jailed_users inmate_1
useradd -g jailed_users inmate_2

#verify
groups inmate_1
>inmate_1 : jailed_users


#what to do next?
force user to use chrooted home dir

standard login:
https://unix.stackexchange.com/questions/199960/login-to-users-session-with-chroot

ssh:
https://www.tecmint.com/restrict-ssh-user-to-directory-using-chrooted-jail/
```