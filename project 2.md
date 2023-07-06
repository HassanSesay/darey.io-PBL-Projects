## WEB STACK IMPLEMENTATION (LEMP STACK)


# Step 1: Install Nginx Web Server

Launch an EC2 instance:Go to the AWS Management Console and navigate to the EC2 service. Click on "Launch Instance" and select the Ubuntu Server 18.04 LTS (or the latest version) AMI. Choose an instance type, configure other settings as needed, and launch the instance. Connect to the EC2 instance: Once the instance runs, select it in the EC2 dashboard and click "Connect". You can follow the instructions to connect using SSH. For example, using the terminal on your local machine: ssh -i <path_to_key_file.pem> ubuntu@<public_dns_name>

Replace <path_to_key_file.pem> with the path to your private key file, and <public_dns_name> with the public DNS name of your EC2 instance.

Update the package lists: sudo apt update (for Ubuntu) or sudo yum update (for CentOS).

Install Nginx: sudo apt install nginx (for Ubuntu) or sudo yum install nginx (for CentOS).

Start Nginx: sudo service nginx start (for Ubuntu) or sudo service nginx start (for CentOS).

Configure Nginx to start on boot: sudo systemctl enable nginx (for Ubuntu) or sudo chkconfig nginx on (for CentOS).

# Step 2: Install MySQL

Install MySQL: sudo apt install mysql-server (for Ubuntu) or sudo yum install mysql-server (for CentOS).

Start MySQL: sudo service mysql start (for Ubuntu) or sudo service mysqld start (for CentOS).

Secure MySQL installation: sudo mysql_secure_installation (follow the prompts to set a root password and secure your installation).

# Step 3: Install PHP

Install PHP and its dependencies: sudo apt install php-fpm php-mysql (for Ubuntu) or sudo yum install php-fpm php-mysql (for CentOS).
Start PHP-FPM: sudo service php-fpm start (for Ubuntu) or sudo service php-fpm start (for CentOS).

# Step 4: Configure Nginx to Use PHP Processor

Open the Nginx default configuration file: sudo nano /etc/nginx/sites-available/default (for Ubuntu) or sudo nano /etc/nginx/conf.d/default.conf (for CentOS).
Find the location block that starts with location ~ \.php$ {.
Uncomment and modify the lines to look like this:
Save the file and exit the text editor.
Restart Nginx: sudo service nginx restart (for Ubuntu) or sudo service nginx restart (for CentOS).

# Step 5: Test PHP with Nginx

Create a PHP test file: sudo nano /var/www/html/info.php.

Save the file and exit the text editor.
Open a web browser and navigate to http://your_server_ip/info.php.
You should see the PHP information page if PHP is configured correctly.

# Step 6: Retrieve Data from MySQL Database with PHP

Write the PHP code to connect to the MySQL database, retrieve data, and display it on a webpage. The exact code will depend on your specific requirements.
For database operations, you can use the PHP MySQL extension or a more modern MySQL library like PDO or MySQLi.
Please ensure the PHP code has the credentials (host, database name, username, and password) to connect to the MySQL database.

By following these steps, you will have successfully implemented a LEMP stack and tested PHP with Nginx

![test 2](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/e189299e-5ebc-419c-82fb-29f7269c76fe)

