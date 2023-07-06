## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
A technology stack is a set of frameworks and tools used to develop a software product. This set of frameworks and tools are very specifically chosen to work together in creating a well-functioning software. They are acronymns for individual technologies used together for a specific technology product. some examples are…

LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)
LEMP (Linux, Nginx, MySQL, PHP or Python, or Perl)
MERN (MongoDB, ExpressJS, ReactJS, NodeJS)
MEAN (MongoDB, ExpressJS, AngularJS, NodeJS)....

![test1](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/9f204ad4-ea3a-42f2-bd3c-af5e4306dd76)

# Step 1: Launch an AWS EC2 Instance

Sign in to the AWS Management Console.
Navigate to the EC2 service.
Launch a new EC2 instance with an appropriate Linux-based operating system (e.g. Ubuntu).

# Step 2: Connect to the EC2 Instance

Obtain the public IP or DNS of the EC2 instance.
Use an SSH client (e.g., PuTTY) to connect to the EC2 instance using the appropriate key pair. The key pair we have already create it when deploy the ec2 instance.

## Step 3: Install Apache and Update the Firewall

Update the package lists: sudo apt update (for Ubuntu) or sudo yum update (for CentOS).
Install Apache web server: sudo apt install apache2 (for Ubuntu) or sudo yum install httpd (for CentOS).
Start Apache: sudo service apache2 start (for Ubuntu) or sudo service httpd start (for CentOS).
Allow HTTP traffic in the firewall: sudo ufw allow 'Apache' (for Ubuntu) or sudo firewall-cmd --permanent --add-service=http (for CentOS). we can do this in the security group of the aws console.

# Step 4: Install MySQL

Install MySQL: sudo apt install mysql-server (for Ubuntu) or sudo yum install mysql-server (for CentOS).
Start MySQL: sudo service mysql start (for Ubuntu) or sudo service mysqld start (for CentOS).
Secure MySQL installation: sudo mysql_secure_installation (follow the prompts to set a root password and secure your installation).

# Step 5: Install PHP

Install PHP and its dependencies: sudo apt install php libapache2-mod-php php-mysql (for Ubuntu) or sudo yum install php php-mysql (for CentOS).
Restart Apache: sudo service apache2 restart (for Ubuntu) or sudo service httpd restart (for CentOS).

# Step 6: Create a Virtual Host for Your Website

Create a directory for your website: sudo mkdir /var/www/mywebsite (replace "mywebsite" with your desired directory name).
Assign ownership to the Apache user: sudo chown -R $USER:$USER /var/www/mywebsite.
Create a sample index file: echo "<?php phpinfo(); ?>" | sudo tee /var/www/mywebsite/index.php.
Create a virtual host configuration file: sudo nano /etc/apache2/sites-available/mywebsite.conf (for Ubuntu) or sudo nano /etc/httpd/conf.d/mywebsite.conf (for CentOS).
Enable the virtual host: sudo a2ensite mywebsite.conf (for Ubuntu) or sudo ln -s /etc/httpd/conf.d/mywebsite.conf /etc/httpd/conf-enabled/ (for CentOS).
Restart Apache: sudo service apache2 restart (for Ubuntu) or sudo service httpd restart (for CentOS).

# Step 7: Enable PHP on the Website (continued)

Find the line ;extension=mysqli and remove the semicolon at the beginning to uncomment the line.
Save the file and exit the text editor.
Restart Apache: sudo service apache2 restart (for Ubuntu) or sudo service httpd restart (for CentOS).

At this point, you have successfully implemented a LAMP stack on your AWS EC2 instance. Your website should be accessible through the domain or IP address associated with your EC2 instance.
