# linux-migration
Demo of migration between Linux operating systems, which migrates a simple php based web site between four different Linux distributions.
* A demonstration of the differences that you find betweeen different Linux distributions.
* A demonstration of how Ansible can ease the migration between different Linux distributions.

## Setup Linux distros
* Red Hat Enterprise Linux (Login required, Red Hat Enterprise Linux 9.2 KVM Guest Image): https://access.redhat.com/downloads/content/479/ver=/rhel---9/9.2/x86_64/product-software
* OpenSUSE: https://download.opensuse.org/repositories/Cloud:/Images:/Leap_15.5/images/openSUSE-Leap-15.5.x86_64-NoCloud.qcow2
* Ubuntu: https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64-disk-kvm.img
* Oracle Linux: https://yum.oracle.com/templates/OracleLinux/OL9/u2/x86_64/OL9U2_x86_64-kvm-b197.qcow

## Running the demo
1. Clone this repository:
```
git clone https://github.com/mglantz/linux-migration
```

2. Setup Ansible inventory(ies) for your systems
3. Run the first playbook, against Ubuntu:
```
cd linux-migration
cp playbooks/apache-ubuntu.yml .
ansible-playbook -i ubuntu-inventory apache-ubuntu.yml
```
4. Access website on your Ubuntu Linux server
5. Run the second playbook, against OpenSUSE
```
cp apache-ubuntu.yml apache-suse.yml
ansible-playbook -i suse-inventory apache-suse.yml
```
6. Correct and explain the issues in the playbook
* Package manager change from apt to zypper
* Apache PHP dependency change from libapache2-mod-php to apache2-mod_php8
* unarchieve settings change from /var/www/html/ to /srv/www/htdocs/
* unarchieve settings change from owner/group www-data to root
* Adding tasks to start the apache2 service
7. Run the third playbook, against Red Hat Enterprise Linux
```
cp apache-suse.yml apache-rhel.yml
ansible-playbook -i rhel-inventory apache-rhel.yml
```
8. Correct and explain the issues in the playbook
* Package manager change from zypper to dnf
* Apache package and service name change from apache2 to httpd
* Remove the Apache PHP dependency apache2-mod_php8
9. Run the fourth playbook, against Oracle Linux
```
cp apache-rhel.yml apache-ol.yml
ansible-playbook -i ol-inventory apache-ol.yml
```
10. Correct and explain the issues in the playbook
* Add task to install package: tar
* Add task to open up a firewall opening for firewalld

