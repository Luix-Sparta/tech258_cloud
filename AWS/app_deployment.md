# App Deployment

## Deploying a Node.js App on Ubuntu Server

In this document, I'll walk through the steps to deploy a Node.js application on an Ubuntu server. I'll automate the process with a Bash script for easier deployment.

## Prerequisites
Before you begin, make sure you have the following:

- An Ubuntu server with sudo privileges
- Basic knowledge of using the terminal and SSH
- The Node.js application you want to deploy hosted on GitHub or any other Git repository
  
## Step 1: Update and Upgrade Packages
First, SSH into your Ubuntu server and run the following commands to update and upgrade your system packages:

```
sudo apt update -y
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
```

## Step 2: Install Nginx
Next, install Nginx using the following command:

```
sudo DEBIAN_FRONTEND=noninteractive apt install nginx 
```
## Step 3: Install Node.js
Now, install Node.js and npm on your server. We'll use NodeSource to install the latest Node.js LTS version:


```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs
```

## Step 4: Clone Your Node.js Application
Clone your Node.js application repository to your server. Replace <repository-url> with the URL of your Git repository:

```
git clone <repository-url>
```

Step 5: Install npm Dependencies
Navigate to your application directory and install npm dependencies:

```
cd <your-application-directory>
sudo npm install
```

Step 6: Start Your Node.js Application
Finally, start your Node.js application:

```
npm start app.js &
```

## Conclusion
You've successfully deployed your Node.js application on an Ubuntu server. Visitors can now access your application through the server's IP address or domain name.

## Deployment Script
```
#!/bin/bash

echo updating...
sudo apt update -y
echo done!

echo upgrading packages...
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo done!

echo installing nginx...
sudo DEBIAN_FRONTEND=noninteractive apt install nginx 
echo done!

echo restarting nginx...
sudo systemctl restart nginx
echo done!

echo enabling nginx...
sudo systemctl enable nginx
echo done!

echo install node js
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - &&sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs
echo done!

echocheck js version
note -v
echo done!

echo install app folder
git clone https://github.com/Luix-Sparta/tech258-sparta-test-app.git
echo done

echo cd app folder
cd ~/tech258-sparta-test-app/app
echo done!

echo install npm
sudo npm install
echo done!

echo npm start app.js
npm start app.js &
echo done!

# npm start app.js
node app.js
```
