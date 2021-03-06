# RH124:
# 1.User & Groups:
 - useradd username or edit /etc/passwd
 - passwd username or passwd --stdin username (to see password while typing) or echo 'password' | passwd --stdin username
 - usermod -s /bin/bash username or chsh username 
 - usermod -c "Description of User" username
 - userdel username (Will del user but home directory will exists) --> rm -r username (run this after that to delete cleanly)
  - userdel -r username - Delete's everything
 - useradd -u 50 -s /sbin/nologin -d /home/user -c "definition for user" username
 - groupadd -g 200 groupname
 - groupmod -g 2001 groupname
 - usermod -aG group username
 
# 2.Password Management:
 - date -d "+95 days"
 - chage -m 0 -M 90 -W 7 -I 14 -E 2022-12-25 user
 - change -l username
 - chage -d 0 username or chage -m 0 username - ask user to change password when he logs in next time
 - usermod -L username - lock user Acc
 - usermod -U username - Unlock User Acc
 
# 3.Files & permission:
 - (u,g,o,a) (r,w,x) (4=r, 2=w, 1=x)
 - chmod g+rw file_name
 - chmod o-wx file_name
 - chmod a=x file_name
 - chmod 777 file_name
 - chmod 400 file_name
 
# 4.SELinux
 - ls -Z or ls -Zd is used to see this user, role, type & securitu levels
 - getenforce 
 - setenforce
 - semanage fcontext -a -t httpd_sys_content_t "/sample(/.*)?" - run it in / 
 - restorecon -RFv /sample/ - to make changes
 - getsebool -a - to list all boolean type
 - getsebool httpd_enable_homedirs - of particular one
 - setsebool httpd_enable_homedirs on - set boolean of particular one
 
# 5.Linux Process
 - ps -ef | ps -aux
 - jobs
 - fg %1 and bg %1 [1 is the lisy No from "jobs" command]
 - sleep 10min & - [& for running in BG]
 - ps j
 - kill -l
 - kill -9 pid or pkill -U username
 - pstree
 
# 6.Service & daemons
 - systemctl start/restart/stop/list-units/mask/unmask service-name
 
# 7.Analysing and storing log
 - vi /etc/rsyslog.conf
 - vi /etc/rsyslog.d/custom.conf
  - 1.Insert "*.debug  /var/log/custom.log"
 - logger -p local7.notice "log entry by mohan" - here, local7 is facility & notice is priority
 - journalctl -n 5
 - journalctl -p err(/debug)
 - journalctl -u username(/apache2)
 - journalctl --since yesterday(/today)
 - journalctl --until yesterday
 - journalctl --since ???YYYY-MM-DD HH:MM:SS??? --until ???2021-02-30 20:30:00???
 - journalctl --since "-10 min"
 
# 8.Maitaining Accurate time
 - timedatectl 
 - timedatectl set-timezone Asia/Kolkata
 - tzselect
 - timedatectl set-ntp true
  - then restart chronyd service
 - chronyc sources -v
 
# 9.Compressing & Archiving
 - tar -czvf source_file dest_file 
 - tar -xzvf source_file dest_file
 
# 10.Copying Files
 - scp -i ???*.pem??? user@source_server1:/home/ user@dest_server:/home/
 - scp -r directory_name user@dest_server:/home/
 - sftp username@server
 - ? - to get what are commands available in sftp
 - put /etc/hosts
 - get /home/user/sample.txt
 - rsync - used to copy files same as push and pull works in git
 - rsync -av /etc/hosts user@dest_server:/home/user

# 11.Installing and Updating software packages
 - RPM - redhat package manager
 - YUM - yellowtalk updating manager
 - DNF is new version of YUM
# ll /etc/yum.repos.d/
 - yum repolist
 - you should have *.repo files /etc/yum.repos.d to run yum command
 - cat sam.repo
   - [BASEOS]
   - name=Base OS packages
   - baseurl=http://content.example.com/rhel8.2/x86_64/dvd/BaseOS
   - enabled=true #enabling url to use fine
   - gpgcheck=false 
   - gpgkey= 
 - yum list - to check software in repo
 - yum info software_name - to get software info
 - yum grouplist
 - yum groupinstall ???group_name???
 - yum history
 - yum history undo 13 - (13 is list no from ???yum history???)
 
# 12.Accessing File system
 - df -hT
 - lsblk or lsblk -fp
 - du -sch *
 
# 13.Locate & Find
 - locate -i name_to_fine ( "updatedb" command needs to be run before locate is run)
 - find / -name filename
 - find /etc -name *.conf
 - find / (-user / -group) * - to get files specific user
 - find / -perm 777
 - find / -size 10M - files of 10M
 - find / -size +10M - files greater than 10M
 - find / -size -10M - files less than 10M
 - find / -size +10M -size -15M - files between 10M
 - find / -mmin 120 - files modified on 120min
 - find / -mmin +120 - files modified before 2 hrs
