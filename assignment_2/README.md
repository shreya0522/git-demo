
# ANSIBLE ASSIGNMENT-2

Install nginx in your servers(more then 2) and 
 make sure the log files of nginx should not be granted more than 1 GB space on the nodes
Create equal number of websites as per your team  members and every members website should be hosted for only 2 hours and after every 2 hours another website should start displaying.
    - First 2 hours <team>.opstree.com should display content of tanya website
    - Next 2 hours <team>.opstree.com should display content of Heena website

Install Apache 
Also Configure nginx to run as reverse proxy to apache after completing first point individually.

Run the ansible commands in such a way that workers nodes are updated one by one and not altogether and also make sure using all type of strategies.


# Solutions

## 1: Install nginx in your servers(more then 2)
 
```bash
 ansible all -m apt -a "name=nginx state=present" --become 
```
![](/pictures/1.png)

## 2: make sure the log files of nginx should not be granted more than 1 GB space on the nodes

#### first created nginx_logrotate.conf file
![](/pictures/2a.png)

#### through "copy module" the "logrotate.conf" file is transferred to destination ie from control server to nodes
```bash
ansible all -m copy -a "src=nginx_logrotate.conf dest=/etc/logrotate.d/nginx" --become 
```
![](/pictures/1-0.png)


## 3: Create equal number of websites as per your team  members and every members website should be hosted for only 2 hours and after every 2 hours another website should start displaying.
## First 2 hours <team>.opstree.com should display content of tanya website
## Next 2 hours <team>.opstree.com should display content of Heena website

#### creating 2 directory in /var/www/shreya.opstree.com 
```bash
ansible all -m file -a "dest=/var/www/shreya.opstree.com state=directory" -become
```

```bash
ansible all -m file -a "dest=/var/www/afzal.opstree.com state=directory" -become
```
#### creating the files index.html in both folders with content 'hello'
```bash 
ansible all -m copy -a "content='hello from shreya' dest=/var/www/shreya.opstree.com/index.html" -become
```
```bash 
ansible all -m copy -a "content='hello from afzal' dest=/var/www/afzal.opstree.com/index.html" -become
```
![](/pictures/3c-1.png)

#### line added
![](/pictures/3C2.png)

#### creating a file & adding server block in /etc/nginx/sites-available/shreya.conf and etc/nginx/sites-available/afzal.conf thereafter restarting nginx
![](/pictures/3c-3.png)
![](/pictures/3c-4.png)
![](/pictures/3c-5.png)

#### host name resolution in /etc/hosts
![](/pictures/3c-7.png)

#### verify
![](/pictures/3c-8.png)

#### script for cron job named "website.sh" copy the cron job script file in remote host remote directory and runn the same cron job using appropriate cron job expression
![](/pictures/4-0.png)
![](/pictures/4-1.png)
![](/pictures/4-3.png)











 