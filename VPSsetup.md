1. Create User and disable root login:\
  Commands:\
    ssh in -$ ssh root@123.45.67.890\
    change password -$ passwd\
    add user -$ useradd -m exampleuser\
    create new user password -$ passwd exampleuser\
    update system with updated mirrors -$ sudo pacman -Syyuu\
    install vim -$ sudo pacman -S vim\
    link vi to vim -$ ln -s /usr/bin/vim /usr/bin/vi\
    edit sudo file -$ visudo\
      under root ALL=(ALL) ALL add\
      exampleuser ALL=(ALL) ALL\
    edit the ssh config -$ sudo vim /etc/ssh/ssh_config\
      PermitRootLogin no\
    restart sshd -$ sudo systemctl restart sshd\
 
2. Log in as new user and generate ssh keys and setup the connection to local machine:\
  Commands:\
    Client -$ ssh-keygen -t rsa\
    Client -$ ssh-copy-id -i $HOME/.ssh/id_rsa.pub user@server\
    Server -$ sudo vim /etc/ssh/ssh_config\
      edit the line: PermitRootLogin no\
    Server -$ sudo systemctl restart sshd\

3. ssh using keys:\
  Commands:\
    ssh user@server\

4. Install firewall:\
  Commands:\
    sudo pacman -S ufw\
    sudo enable ufw\

5. Setup server with Nginx:\
  Commands:\
    sudo pacman -S nginx\
    sudo pacman -S certbot certbot-nginx\
    sudo mkdir /usr/shared/nginx/$DOMAINNAME\
    sudo vim /usr/shared/nginx/$DOMAINNAME/index.html\
      add basic html code (example can be found in examples/helloworld.html)\
    sudo mkdir /etc/nginx/sites-available\
    sudo mkdir /etc/nginx/sites-enabled\
    sudo vim /etc/nginx/sites-available/$DOMAINNAME\
      paste example code found in examples/domain.conf\
    sudo ln -s /etc/nginx/sites-available/$DOMAINNAME /etc/nginx/sites-enabled/\
    sudo vim /etc/nginx/nginx.conf\
      replace all with code found in examples/nginx.conf\
    sudo ufw allow 80\
    sudo certbot --nginx\
    sudo ufw allow 443\
    sudo systemctl restart nginx\
