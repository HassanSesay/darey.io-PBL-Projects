## WEB STACK IMPLEMENTATION (LEMP STACK)
Here's a step-by-step guide to implementing a LEMP (Linux, Nginx, MySQL, PHP) stack on an AWS EC2 instance using the Ubuntu AMI:

Launch an EC2 instance:

Go to the AWS Management Console and navigate to the EC2 service. Click on "Launch Instance" and select the Ubuntu Server 18.04 LTS (or the latest version) AMI. Choose an instance type, configure other settings as needed, and launch the instance. Connect to the EC2 instance:

Once the instance runs, select it in the EC2 dashboard and click "Connect". You can follow the instructions to connect using SSH. For example, using the terminal on your local machine: ssh -i <path_to_key_file.pem> ubuntu@<public_dns_name>

Replace <path_to_key_file.pem> with the path to your private key file, and <public_dns_name> with the public DNS name of your EC2 instance.

Update the system packages:

sudo apt update

sudo apt upgrade

Install Nginx:

sudo apt install nginx

Start Nginx and enable it to start on boot: sudo systemctl start nginx

sudo systemctl enable nginx

Verify Nginx is running:

You can just open a web browser and enter your EC2 instance's public IP or public DNS in the address bar. You should see the default Nginx welcome page indicating a successful installation.

Install MySQL:

sudo apt install mysql-server

Secure the MySQL installation: sudo mysql_secure_installation

Follow the prompts to set a root password and answer the security-related questions.

Install PHP and required extensions:

sudo apt install php-fpm php-mysql

Configure Nginx to use PHP: sudo nano /etc/nginx/sites-available/default

Inside the server block, replace index index.html with index index.php index.html, and add the following lines:

location ~ .php$ { include snippets/fastcgi-php.conf; fastcgi_pass unix:/var/run/php/php7.2-fpm.sock; }

Restart Nginx and PHP-FPM for the changes to take effect:

sudo systemctl restart nginx sudo systemctl restart php7.2-fpm

Test PHP:

Create a PHP info file in the web root directory:

echo "" | sudo tee /var/www/html/phpinfo.php

![test 2](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/e189299e-5ebc-419c-82fb-29f7269c76fe)


