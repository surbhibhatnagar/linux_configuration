# linux_configuration
## Ubuntu Linux server instance on Amazon Lightsail
i. The IP address and SSH port
    IP address: http://54.148.67.137/
    Port #: 2200    
ii. Public key : id_rsa.pub
    Download the public key and store it in .ssh folder of your local machine.
iii. Summary of linux configuration 
1. Update all currently installed packages.
          sudo apt-get update
          sudo apt-get upgrade
2. Change the SSH port from 22 to 2200 and configure firewall.
          change PORT field in sshd_config file located in /etc/ssh directory of server
3. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
          sudo ufw allow 2200/tcp
          sudo ufw allow http
          sudo ufw allow ntp
          sudo ufw enable 
          sudo ufw status
4. Create a new user account named grader.
          sudo adduser grader
5. Give grader the permission to sudo.
          sudo usermod -G sudo grader
6. Create an SSH key pair for grader using the ssh-keygen tool.
          ssh-keygen 
   Deploy key on VM:
          Login as a grader on VM and save public key in .ssh folder as id_rsa.pub
          chmod 700 .ssh
          chmod 644 .ssh/id_rsa.pub
   Login as grader: 
          ssh -i id_rsa.pub grader@54.148.67.137
7. Configure the local timezone to UTC.
          sudo dpkg-reconfigure tzdata
8. Install and configure Apache to serve a Python mod_wsgi application.
          sudo apt-get install apache2
          sudo apt-get install python-setuptools libapache2-mod-wsgi
          sudo service apache2 restart
9. Install and configure PostgreSQL:
          sudo apt-get install postgresql
          sudo su - postgres
          psql
          CREATE DATABASE catalog;
          CREATE USER catalog;
          ALTER ROLE catalog WITH PASSWORD 'password';
          GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;
10. Install git.
          sudo apt-get install git
11. Clone and setup Item Catalog project.

### A list of any third-party resources you made use of to complete this project.
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
