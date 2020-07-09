
Install docker with pacman

mkdir jenkins in home

enable and start docker with systemctl

https://www.jenkins.io/doc/book/installing/#installing-docker

create docker-compose.yml inside jenkins dir: 
version: '2'
services:
        jenkins:
                image: 'jenkins/jenkins:lts'
                ports:
                        - '50000:50000'
                restart: always
                tty: true
                user: root
                volumes:
                        - ./jenkins-data:/var/jenkins_home
                        - /usr/share/nginx/games:/var/jenkins_home/games
                networks:
                        apps_network:
                                aliases:
                                - jenkins
                                ipv4_address: 172.16.223.10
networks:
        apps_network:
                driver: bridge
                ipam:
                        driver: default
                        config:
                        - subnet: 172.16.223.0/24

install docker-compose

run sudo docker-compose up -d

create a new file in sites-available jenkins.com:
Add an entry to the DNS zone
Step 2 of 3
* Fields followed by an asterisk are mandatory.

Sub-domain
jenkins
.miskify.com.
TTL

Personalised
60
s.
Target 
miskify.com.
The CNAME record currently generated is as follows:
jenkins 60 IN CNAME miskify.com.

then symlink
sudo ln -s /etc/nginx/sites-available/jenkins.com /etc/nginx/sites-enabled/

now jenkins should work but not sure if there were any more steps

at the end remember to allow only vpn ip to access jenkins. sudo vim /etc/nginx/sites-available/jenkins.com 
its not going to work though. 2 options to fix. Have the jenkins and vpn on 2 different vps or redirect jenkins to local ip address inside the one vps

