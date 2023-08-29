# CONFIGURE APACHE AS A LOAD BALANCER
Prior to moving forward with the project, it's essential to confirm the existence of the stipulated requirements.

Requirements:

Ensure that the subsequent servers are both installed and properly set up under Project-7:

Two Web Servers operating on RHEL 8.
One MySQL DB Server running on Ubuntu 20.04.
One NFS server running on RHEL 8.
![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/ea77e030-6e29-4345-97b7-804238cc0e8e)
![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/101029a0-24c8-446c-b26e-56abc2cc1705)

2. Establish an open TCP connection on port 80 for Project-8-apache-lb by generating an Inbound Rule within the Security Group.

3. Deploy Apache Load Balancer on the Project-8-apache-lb server and set up its configuration to direct incoming traffic to both Web Servers:

# Begin by installing the Apache2 package:
sudo apt update

sudo apt install apache2 -y

 sudo apt-get install libxml2-dev
 ![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/95f51bf7-891a-4e18-900a-4faa2f1e6e35)

 Activate the specified modules using the provided commands:
 
sudo a2enmod rewrite

sudo a2enmod proxy

sudo a2enmod proxy_balancer

sudo a2enmod proxy_http

sudo a2enmod headers

sudo a2enmod lbmethod_bytraffic
# Restart apache2 service
sudo systemctl restart apache2

sudo systemctl status apache2

![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/9536a6c2-a6de-46cd-bc77-09eeb2e5c245)

# Configuring Load Balancer

Modify the default.conf file to incorporate the backend web servers into the load balancer's proxy for routing. You can accomplish this by following these steps:

Open the default.conf file for editing:
sudo vi /etc/apache2/sites-available/000-default.conf

Inside the <VirtualHost *:80> section of the configuration, add the provided configuration as follows:
<VirtualHost *:80>
    # Existing configuration ...

    <Proxy "balancer://mycluster">
        BalancerMember http://<WebServer1-Private-IP-Address>:80 loadfactor=5 timeout=1
        BalancerMember http://<WebServer2-Private-IP-Address>:80 loadfactor=5 timeout=1
        ProxySet lbmethod=bytraffic
        # ProxySet lbmethod=byrequests
    </Proxy>

    ProxyPreserveHost On
    ProxyPass / balancer://mycluster/
    ProxyPassReverse / balancer://mycluster/

    # Additional configuration ...
</VirtualHost>
Replace <WebServer1-Private-IP-Address> and <WebServer2-Private-IP-Address> with the actual private IP addresses of your backend web servers. You can also choose the desired load balancing method by uncommenting either ProxySet lbmethod=bytraffic or ProxySet lbmethod=byrequests, as required.

The "bytraffic" load balancing method will allocate incoming traffic among your Web Servers based on their current load. The "loadfactor" parameter allows you to manage the proportion in which traffic is distributed.

To validate the configuration, follow these steps:

Attempt to access your load balancer's public IP address or Public DNS name from your web browser: http://<LB-Public-IP-or-DNS>/index.php.

To ensure that the configuration is functioning correctly:

If you have mounted /var/log/httpd/ from your Web Servers to the NFS server in Project-7, ensure that these mounts are unmounted.
Confirm that each Web Server maintains its own log directory.
Open two SSH/Putty consoles, each connected to a separate Web Server. Run the following command in both consoles to monitor access logs:
sudo tail -f /var/log/httpd/access_log
![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/9481b981-ab55-4b8b-9c09-13cde4f1cc74)

Restart the apache2 server sudo systemctl restart apache2

# To test the load balancing connection using the public IP address of your load balancer server, follow these steps:

Open a web browser on your computer.

Enter the public IP address of your load balancer server in the browser's address bar. It should look something like: http://<Load-Balancer-Public-IP>/.

Press Enter to access the URL.

The load balancer should distribute the incoming requests to your backend Web Servers based on the "bytraffic" load balancing method you configured earlier. You should see responses from both Web Servers in the browser.

Refresh the page multiple times and observe how the responses alternate between the Web Servers, showcasing the load balancing in action.

By testing the connection in this manner, you can verify that the load balancer is functioning correctly and distributing traffic among your backend Web Servers as intended.
![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/a0cb3c5e-4b68-4fd2-b724-ac4775f7af90)

# To ensure that traffic is being evenly distributed to both web servers and to monitor the logs of both servers as the load balancer receives traffic (achieved by refreshing the webpage), you can follow these steps:

Keep your SSH/Putty consoles open for both Web Servers.

In each console, run the following command to monitor the access logs in real-time:
![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/3c699e3d-0100-4420-945f-6454b4d7e755)


# Configuring DNS Names (Locally)
To simplify the process of adding new web servers to the load balancer proxy list without needing to provide their private IP addresses each time, you can define them in the hosts file and assign domain names to each server. Here's how you can achieve this:

Open the hosts file for editing using the provided command:
sudo vi /etc/hosts

127.0.0.1 localhost

172.31.91.129 web 1

172.31.88.76 web2


server 1

![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/3bfa5ac2-e314-47f2-aaaf-29edb3e12592)


server 2

![image](https://github.com/HassanSesay/darey.io-PBL-Projects/assets/114838820/098d5f07-e486-431f-8980-a830437782cd)



