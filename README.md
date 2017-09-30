# Ansible_Daily

ansible localhost -m debug -a 'var=groups.keys()' | grep -i fal
ansible all -m ping
ansible 10.1.1.1 -m raw-a 'ifconfig|eth0'

ansible-doc -l
ansible-doc -s  module_name

ansible all -m shell -a echo "123456789" |passwd –stdin user1'
ansible all -m user -a "name=test password=<abc>"
ansible 10.1.1.11 -m user -a 'name=test state=absent remove=yes'
ansible all -m group -a 'gid=2014 name=nolinux'

ansible all -m yum -a "state=present name=httpd"
ansible all -m service -a "name=httpd state=started"
ansible 10.1.1.11 -m service -a 'name=httpd state=restarted enabled=yes'
ansibel all -m service -a "name=httpd state=restarted"
ansible all -m service -a "name=httpd state=stoped"

ansible all -m script -a '/tmp/a.sh'
ansible webservers -m copy -a "src=/etc/hosts dest=/tmp/hosts"
ansible all -m file -a "dest=/tmp/t.sh mode=755 owner=root group=root"
ansible 10.1.1.1 -m synchronize -a 'src=/root/a dest=/tmp/ compress=yes'
ansible all -m cron -a 'name="custom job" minute=\*/3 hour=\* day=\* month=\* weekday=\* job="/usr/sbin/ntpdate 172.16.25.1"'

https://github.com/fboender/ansible-cmdb
First, generate Ansible output for your hosts:

mkdir out
ansible -m setup --tree out/ all
Next, call ansible-cmdb on the resulting out/ directory to generate the CMDB overview page:

ansible-cmdb out/ > overview.html
ansible-cmdb -t txt_table --columns name,os,ip,mem,cpus out/

