# App Deployment

- [App Deployment](#app-deployment)
  - [Deploying a Node.js App on Ubuntu Server](#deploying-a-nodejs-app-on-ubuntu-server)
  - [Prerequisites](#prerequisites)
  - [Step 1: Update and Upgrade Packages](#step-1-update-and-upgrade-packages)
  - [Step 2: Install Nginx](#step-2-install-nginx)
  - [Step 3: Install Node.js](#step-3-install-nodejs)
  - [Step 4: Clone Your Node.js Application](#step-4-clone-your-nodejs-application)
  - [Conclusion](#conclusion)
  - [Deployment Script](#deployment-script)
  - [Method 1:](#method-1)
  - [Method 2:](#method-2)
  - [Tier 2 Deployment](#tier-2-deployment)
  - [Step 1 (App)](#step-1-app)
    - [Code (App Deployment Script)](#code-app-deployment-script)
      - [Explanation](#explanation)
      - [Steps:](#steps)
      - [Usage](#usage)
  - [Step 2 (Database)](#step-2-database)
    - [Code (Database Script)](#code-database-script)
    - [Explanation](#explanation-1)
    - [Steps:](#steps-1)
    - [Usage](#usage-1)
- [Monolithic vs. Two-Tier Architecture Comparison](#monolithic-vs-two-tier-architecture-comparison)
  - [Monolithic Architecture](#monolithic-architecture)
    - [Characteristics:](#characteristics)
  - [Two-Tier Architecture](#two-tier-architecture)
    - [Characteristics:](#characteristics-1)
  - [Conclusion](#conclusion-1)

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
## Method 1:
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
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo DEBIAN_FRONTEND=noninteractive -E bash - && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs
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
## Method 2:
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
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo DEBIAN_FRONTEND=noninteractive -E bash - && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs
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

echo install pm2
sudo npm install -g pm2
echo done!

echo stop app
pm2 stop app
echo done!

echo start app
pm2 start app.js app
echo done!
```

## Tier 2 Deployment
## Step 1 (App)
### Code (App Deployment Script)

```
#!/bin/bash

echo updating...
sudo apt update -y
echo done!

echo upgrading packages...
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo done!

echo installing nginx...
sudo DEBIAN_FRONTEND=noninteractive apt install nginx -y < /dev/null
echo done!

# configure reverse proxy
sudo sed -i '51s/.*/\t        proxy_pass http:\/\/34.244.251.42:3000;/' /etc/nginx/sites-enabled/default
# changing a config file

echo restarting nginx...
sudo systemctl restart nginx
echo done!

echo enabling nginx...
sudo systemctl enable nginx
echo done!

echo install node js
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo DEBIAN_FRONTEND=noninteractive -E bash - && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs
echo done!

echocheck js version
note -v
echo done!

echo set DB_HOST env var
export DB_HOST=mongodb://172.31.40.65:27017/posts
echo done!

echo install app folder
git clone https://github.com/Luix-Sparta/tech258-sparta-test-app.git
echo done!

echo cd app folder
cd ~/tech258-sparta-test-app/app
echo done!

echo install npm
sudo -E npm install
echo done!

echo install pm2
sudo -E npm install -g pm2
echo done!

echo stop app
pm2 stop app
echo done!

echo start app
pm2 start app.js app
echo done!


```
#### Explanation 
This script automates the deployment process for a Tier 2 environment, including updating system packages, installing and configuring Nginx as a reverse proxy, setting up Node.js and MongoDB, and deploying an application from a GitHub repository.

#### Steps:

1. **Update and Upgrade:**
   - Updates the package list and upgrades installed packages to their latest versions.

2. **Install Nginx:**
   - Installs Nginx web server to act as a reverse proxy for the application.

3. **Configure Reverse Proxy:**
   - Modifies the Nginx configuration file to set up a reverse proxy to the application running on a specified IP address and port.

4. **Restart and Enable Nginx:**
   - Restarts Nginx service to apply the changes and enables it to start automatically on system boot.

5. **Install Node.js:**
   - Adds Node.js repository and installs Node.js and npm for running JavaScript applications.

6. **Check Node.js Version:**
   - Verifies the installed Node.js version.

7. **Set Environment Variable:**
   - Sets the DB_HOST environment variable to specify the MongoDB connection URL.

8. **Clone Application Repository:**
   - Clones the application code from the specified GitHub repository.

9. **Navigate to Application Directory:**
   - Changes the working directory to the cloned application folder.

10. **Install npm Dependencies:**
    - Installs the required npm dependencies for the application.

11. **Install pm2:**
    - Installs the pm2 process manager globally for managing Node.js applications.

12. **Stop Existing Application:**
    - Stops any existing instances of the application managed by pm2.

13. **Start Application with pm2:**
    - Starts the application using pm2 process manager, specifying the entry point (app.js) and application name (app).


#### Usage

- Ensure that the script has executable permissions (`chmod +x script_name.sh`) and is executed with appropriate privileges.
- Customize the script variables, such as IP addresses, port numbers, and GitHub repository URL, to match your deployment environment.
- Execute the script on the target server to deploy the application automatically.

This script streamlines the deployment process, making it easier to manage and replicate deployments across different environments.


## Step 2 (Database)
### Code (Database Script)

```
#!/bin/bash

echo updating...
sudo apt update -y
echo done!

echo upgrading packages...
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo done!

echo importing the public key used by the package management system
sudo apt-get install gnupg curl
echo done!

echo importing the MongoDB public GPG key
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo -E gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor --yes

echo done!

echo creating a list file for MongoDB
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
echo done!

echo reloading local package database
sudo apt-get update
echo done!

echo installing mongo db 7.0.6
#sudo DEBIAN_FRONTEND=noninteractive apt-get install -y mongodb-org=7.0.6 mongodb-org-database=7.0.6 mongodb-org-server=7.0.6 mongodb-mongosh-shared-openssl3=2.2.4 mongodb-org-mongos=7.0.6 mongodb-org-tools=7.0.6
sudo DEBIAN_FRONTEND=noninteractive apt-get install -y mongodb-org=7.0.6 mongodb-org-database=7.0.6 mongodb-org-server=7.0.6 mongodb-mongosh=2.2.4 mongodb-org-mongos=7.0.6 mongodb-org-tools=7.0.6
echo done!

echo set versions
echo "mongodb-org hold" | sudo dpkg --set-selections
echo "mongodb-org-database hold" | sudo dpkg --set-selections
echo "mongodb-org-server hold" | sudo dpkg --set-selections
echo "mongodb-mongosh hold" | sudo dpkg --set-selections
echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
echo "mongodb-org-tools hold" | sudo dpkg --set-selections
echo done!

echo configuring bind IP in mongo db config file - 0.0.0.0
sudo sed -i "s,\\(^[[:blank:]]*bindIp:\\) .*,\\1 0.0.0.0," /etc/mongod.conf
echo done!

echo restarting mongo db #f(or start)
sudo systemctl restart mongod
echo done!

echo enabling mongo db
sudo systemctl enable mongod
echo done!
```


### Explanation 
This script automates the installation and configuration of MongoDB version 7.0.6 on an Ubuntu system. It also configures MongoDB to listen on all network interfaces.

### Steps:

1. **Update and Upgrade:**
   - Updates the package list and upgrades installed packages to their latest versions.

2. **Install Required Packages:**
   - Installs necessary packages gnupg and curl for package management and key import.

3. **Import MongoDB Public Key:**
   - Imports the MongoDB public GPG key to verify package signatures.

4. **Add MongoDB Repository:**
   - Adds the MongoDB repository to the system's package sources.

5. **Reload Package Database:**
   - Reloads the local package database to reflect the changes made.

6. **Install MongoDB 7.0.6:**
   - Installs MongoDB version 7.0.6 along with related packages using the specified version.

7. **Set Package Versions:**
   - Sets the installed MongoDB packages to hold their current version to prevent unintended upgrades.

8. **Configure MongoDB Bind IP:**
   - Modifies the MongoDB configuration file to bind MongoDB to all available network interfaces (0.0.0.0).

9. **Restart MongoDB Service:**
   - Restarts the MongoDB service to apply the configuration changes.

10. **Enable MongoDB Service:**
    - Enables the MongoDB service to start automatically on system boot.


### Usage

- Ensure that the script has executable permissions (`chmod +x script_name.sh`) and is executed with appropriate privileges.
- Customize the script variables, such as MongoDB version and configuration settings, to match your requirements.
- Execute the script on the target server to install and configure MongoDB automatically.

This script simplifies the process of installing and configuring MongoDB, making it easier to set up MongoDB instances consistently across different environments.

# Monolithic vs. Two-Tier Architecture Comparison

## Monolithic Architecture

Monolithic architecture refers to a traditional architectural style where the entire application is developed, deployed, and managed as a single unit. Here are some characteristics:

### Characteristics:
- **Single Unit:** The entire application, including its components such as user interface, business logic, and data access layers, is packaged and deployed as a single unit.
- **Tightly Coupled:** Components within the monolith are tightly coupled, meaning changes in one part may require modifications in other parts.
- **Scalability Challenges:** Scaling individual components independently can be challenging. The entire application needs to be scaled, even if only a specific component requires additional resources.
- **Development Simplicity:** Initially, development is often simpler as developers work within a single codebase and environment.
- **Deployment Complexity:** Deploying changes to a monolithic application can be complex and risky, especially as the application grows larger.
- **Technology Stack:** Typically, a monolithic application uses a single technology stack for all its components.

## Two-Tier Architecture

Two-tier architecture, also known as client-server architecture, involves dividing an application into two parts: client and server. Here's an overview of its characteristics:

### Characteristics:
- **Client-Server Model:** The application is divided into two parts: client, which handles the presentation logic, and server, which manages the business logic and data storage.
- **Decoupled Components:** Components are decoupled, allowing for easier maintenance and scalability. Changes in one tier usually don't require modifications in the other.
- **Scalability:** Two-tier architecture allows for more granular scalability. The client and server tiers can be scaled independently based on demand.
- **Development Complexity:** Development may involve more coordination between client-side and server-side teams, but it also allows for specialization in each tier.
- **Deployment Simplicity:** Deploying changes is typically simpler compared to monolithic architectures, as changes can be targeted to specific tiers.
- **Technology Diversity:** Different technologies can be used for the client and server tiers, allowing for flexibility in choosing the most suitable tools for each component.

## Conclusion

Both monolithic and two-tier architectures have their own advantages and disadvantages. Monolithic architecture offers simplicity in development but can be challenging to scale and maintain as the application grows. On the other hand, two-tier architecture provides better scalability and flexibility but requires careful design and coordination between client and server components. The choice between these architectures depends on factors such as the size and complexity of the application, scalability requirements, and development team preferences.
