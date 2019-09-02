• Apply patches and updates via yum, apt, and other package managers.
```ansible multi -b -m yum -a "name=ntp state=present"```
```ansible multi -b -m service -a "name=ntpd state=started enabled=yes"```
```ansible multi -b -a "service ntpd stop"```
```ansible multi -b -a "ntpdate -q 0.rhel.pool.ntp.org"```
```ansible multi -b -a "service ntpd start"```
```ansible app -b -m package -a "name=git state=present"```
• Check resource usage (disk space, memory, CPU, swap space, network). 
```ansible multi -a "df -h"```
```ansible multi -a "free -m"```
```ansible multi -a "date"```
• Manage system users and groups.
```ansible app -b -m group -a "name=admin state=present"```
```ansible app -b -m user -a "name=ansible-hyd group=admin createhome=yes"```
```ansible app -b -m user -a "name=johndoe state=absent remove=yes"```
• Check log files.
```ansible multi -b -a "tail /var/log/messages"```
```ansible multi -b -m shell -a "tail /var/log/messages | grep ansible-command | wc -l"```
• Copy files to and from servers.
```ansible multi -m stat -a "path=/etc/environment"```
```ansible multi -m copy -a "src=/etc/hosts dest=/tmp/hosts"```
```ansible multi -b -m fetch -a "src=/etc/hosts dest=/tmp"```
```ansible multi -m file -a "dest=/tmp/test mode=644 state=directory"```
```ansible multi -m file -a "src=/src/symlink dest=/dest/symlink owner=root group=root state=link"```
```ansible multi -m file -a "dest=/tmp/test state=absent"```
• Deploy applications or run application maintenance.
```ansible app -b -m yum -a "name=MySQL-python state=present"```
```ansible app -b -m yum -a "name=python-setuptools state=present"```
```ansible app -b -m easy_install -a "name=django<2 state=present"```
```ansible app -a "python -c 'import django; print django.get_version()'"```
```ansible db -b -m yum -a "name=mariadb-server state=present"```
```ansible db -b -m service -a "name=mariadb state=started enabled=yes"```
```ansible db -b -a "iptables -F"```
```ansible db -b -a "iptables -A INPUT -s 192.168.60.0/24 -p tcp -m tcp --dport 3306 -j ACCEPT"```
• Manage cron jobs.
```ansible multi -b -m cron -a "name='daily-cron-all-servers' hour=4 job='/path/to/daily-script.sh'"```
```ansible multi -b -m cron -a "name='daily-cron-all-servers' state=absent"```
• Async or Fire and forget or Background jobs
```ansible multi -b -B 3600 -a "yum -y update"```
```ansible multi -b -m async_status -a "jid=763350539037"```
```ansible multi -B 3600 -P 0 -a "yum install tree -y"```
