
# AWS

Amazon Web Services (AWS) is a comprehensive, scalable cloud computing platform offering a wide range of services including computing power, storage, and networking capabilities.

## TOPICS LEARNT

1.Traditional Vs Cloud Computing

2.Cloud Computing Service Model 

3.Deployment Model Of Clouds

4.EC2 (Elastic Compute Cloud)

5.Route 53 ---domain management

6.AWS S3 -- storage management

7.AWS Amplify --host latest tech stack website with directly through github

8.Elastic Beanstalk 



# Node.js Deployment

> Steps to deploy a Node.js app to DigitalOcean using PM2, NGINX as a reverse proxy and an SSL from LetsEncrypt

## 1. Create Free AWS Account
Create free AWS Account at https://aws.amazon.com/

## 2. Create and Lauch an EC2 instance and SSH into machine
I would be creating a t2.medium ubuntu machine for this demo.

## 3. Install Node and NPM
```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -

latest current version lts
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

sudo apt install nodejs

node --version
```

## 4. Clone your project from Github
```
git clone https://github.com/piyushgargdev-01/short-url-nodejs
```

## 5. Install dependencies and test app
```
sudo npm i pm2 -g
pm2 start index

# Other pm2 commands
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show log stream)
pm2 flush (Clear logs)

# To make sure app starts when reboot
pm2 startup ubuntu
```

## 6. Setup Firewall
```
sudo ufw enable
sudo ufw status
sudo ufw allow ssh (Port 22)
sudo ufw allow http (Port 80)
sudo ufw allow https (Port 443)
```

## 7. Install NGINX and configure
```
sudo apt install nginx

sudo nano /etc/nginx/sites-available/default
```
Add the following to the location part of the server block
```
    server_name yourdomain.com www.yourdomain.com;

    location / {
        proxy_pass http://localhost:8001; #whatever port your app runs on
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
```
```
# Check NGINX config
sudo nginx -t

# Restart NGINX
sudo nginx -s reload
```

## 8. Add SSL with LetsEncrypt
```
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

# Only valid for 90 days, test the renewal process with
certbot renew --dry-run
```
Video Tutorial: https://youtu.be/Qmld1te08Ns

## Nginx Ubuntu Installation

Update Packages
```sh
sudo apt-get update
```

Install Nginx
```sh
sudo apt-get install nginx
```

Verify Installation
```sh
sudo nginx -v
```
Start Nginx Server
```sh
nginx
```

Now visit `http://localhost:80` and you would be able to see default nginx welcome page.

## Nginx Docker Installation

Run Docker Ubuntu Image
```sh
docker run -it -p 8080:80 ubuntu
```

Update Packages
```sh
sudo apt-get update
```

Install Nginx
```sh
sudo apt-get install nginx
```

Verify Installation
```sh
sudo nginx -v
```
Start Nginx Server
```sh
nginx
```
Now visit `http://localhost:8080` and you would be able to see default nginx welcome page.

## Nginx Conf File

Install VIM
```sh
sudo apt-get install vim
```

Open `nginx.conf` file
```sh
vim etc/nginx/nginx.conf
```

Type Sample Nginx Conf
```
events {
}

http {
  server {
    listen 80;
    server_name _;
    
    location / {
      return 200 "Hello from Nginx Sever";
    }
  }
}
```




### Deploy NextJS Project using Github on Nginx Remote Server or VPS
- Get Access to Remote Server via SSH
```sh
Syntax:- ssh -p PORT USERNAME@HOSTIP
Example:- ssh -p 1034 raj@216.32.44.12
```
- Verify that all required softwares are installed
```sh
nginx -v
node -v
npm -v
git --version
pm2 --version
```
- Install Software (If required)
```sh
sudo apt install nginx
sudo apt install git
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```
- Install PM2 (If required)
```sh
sudo npm install -g pm2@latest
```
- Add PM2 Process on Startup
```sh
sudo pm2 startup
```
- Verify Nginx is Active and Running
```sh
sudo service nginx status
```
- Verify Web Server Ports are Open and Allowed through Firewall
```sh
sudo ufw status verbose
```
- Exit from Remote Server
```sh
exit
```
- Login to Your Domain Provider Website
- Navigate to Manage DNS
- Add Following Records:

| Type | Host/Name | Value |
| :---: | :---: | :--- |
| A     | @     | Your Remote Server IP |
| A     | www   | Your Remote Server IP |
| AAAA  | @     | Your Remote Server IPv6 |
| AAAA  | www   | Your Remote Server IPv6 |

- Copy Project from Local Machine to Remote Server or VPS. There are two ways to do it:-
  1. Using Command Prompt
      - On Local Windows Machine Make Your Project Folder a Zip File using any of the software e.g. winzip
      - Open Command Prompt
      - Copy Zip File from Local Windows Machine to Linux Remote Server
      ```sh
      Syntax:- scp -P Remote_Server_Port Source_File_Path Destination_Path
      Example:- scp -P 1034 miniblog.zip raj@216.32.44.12:
      ```
      - Copied Successfully
      - Get Access to Remote Server via SSH
      ```sh
      Syntax:- ssh -p PORT USERNAME@HOSTIP
      Example:- ssh -p 1034 raj@216.32.44.12
      ```
      - Unzip the Copied Project Zip File
      ```sh
      Syntax:- unzip zip_file_name
      Example:- unzip miniblog.zip
      ```
      
  2. Using Github
      - Open Project on VS Code then add .gitignore file (If needed)
      - Push your Poject to Your Github Account as Private Repo
      - Make Connection between Remote Server and Github Repo via SSH Key
      - Generate SSH Keys
      ```sh
      Syntax:- ssh-keygen -t ed25519 -C "your_email@example.com"
      ```
      - If Permission Denied then Own .ssh then try again to Generate SSH Keys
      ```sh
      Syntax:- sudo chown -R user_name .ssh
      Example:- sudo chown -R raj .ssh
      ```
      - Open Public SSH Keys then copy the key
      ```sh
      cat ~/.ssh/id_ed25519.pub
      ```
      - Go to Your Github Repo
      - Click on Settings Tab
      - Click on Deploy Keys option from sidebar
      - Click on Add Deploy Key Button and Paste Remote Server's Copied SSH Public Key then Click on Add Key
      - Clone Project from your github Repo using SSH Path It requires to setup SSH Key on Github
      ```sh
      Syntax:- git clone ssh_repo_path
      Example:- git clone git@github.com:geekyshow1/miniblog.git
      ```
- Create Virtual Host File
```sh
Syntax:- sudo nano /etc/nginx/sites-available/your_domain
Example:- sudo nano /etc/nginx/sites-available/sonamkumari.com
```
- Write following Code in Virtual Host File
```sh
server{
    listen 80;
    listen [::]:80;
    server_name your_domain www.your_domain;
    location / {
       proxy_pass http://localhost:3001;
       proxy_http_version 1.1;
       proxy_set_header Upgrade $http_upgrade;
       proxy_set_header Connection 'upgrade';
       proxy_set_header Host $host;
       proxy_cache_bypass $http_upgrade;
    }
}
```
- Enable Virtual Host or Create Symbolic Link of Virtual Host File
```sh
Syntax:- sudo ln -s /etc/nginx/sites-available/virtual_host_file /etc/nginx/sites-enabled/virtual_host_file
Example:- sudo ln -s /etc/nginx/sites-available/sonamkumari.com /etc/nginx/sites-enabled/sonamkumari.com
```
- Check Configuration is Correct or Not
```sh
sudo nginx -t
```
- Install Dependencies
```sh
cd ~/project_folder_name
npm install
```
- Create Production Build
```sh
npm run build
```
- Create pm2 config File inside project folder
```sh
nano ecosystem.config.js
```
- Write below code in ecosystem.config.js file
```sh
module.exports = {
  apps : [
      {
        name: "myapp",
        script: "npm start",
        port: 3001
      }
  ]
}
```
- Restart Nginx
```sh
sudo service nginx restart
```
- Start NextJS Application using pm2
```sh
pm2 start ecosystem.config.js
```
- Save PM2 Process
```sh
pm2 save
```
- Check PM2 Status
```sh
pm2 status
```
- Now you can make some changes in your project local development VS Code and Pull it on Remote Server (Only if you have used Github)
- Pull the changes from github repo
```sh
git pull
```
- Create Production Build
```sh
npm run build
```
- Reload using PM2
```sh
pm2 reload app_name/id
```
##
### How to Automate NextJS Project Deployment using Github Action
- On Your Local Machine, Open Your Project using VS Code or any Editor
- Create A Folder named .scripts inside your root project folder e.g. miniblog/.scripts
- Inside .scripts folder Create A file with .sh extension e.g. miniblog/.scripts/deploy.sh
- Write below script inside the created .sh file
```sh
#!/bin/bash
set -e

echo "Deployment started..."

# Pull the latest version of the app
git pull origin master
echo "New changes copied to server !"

echo "Installing Dependencies..."
npm install --yes

echo "Creating Production Build..."
npm run build

echo "PM2 Reload"
pm2 reload app_name/id

echo "Deployment Finished!"
```
- Go inside .scripts Folder then Set File Permission for .sh File
```sh
git update-index --add --chmod=+x deploy.sh
```
- Create Directory Path named .github/workflows inside your root project folder e.g. miniblog/.github/workflows
- Inside workflows folder Create A file with .yml extension e.g. miniblog/.github/workflows/deploy.yml
- Write below script inside the created .yml file
```sh
name: Deploy

# Trigger the workflow on push and
# pull request events on the master branch
on:
  push:
    branches: ["master"]
  pull_request:
    branches: ["master"]

# Authenticate to the the server via ssh
# and run our deployment script
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Server
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          port: ${{ secrets.PORT }}
          key: ${{ secrets.SSHKEY }}
          script: "cd ~/project_folder_name && ./.scripts/deploy.sh"
```
- Go to Your Github Repo Click on Settings
- Click on Secrets and Variables from the Sidebar then choose Actions
- On Secret Tab, Click on New Repository Secret
- Add Four Secrets HOST, PORT, USERNAME and SSHKEY as below
```sh
Name: HOST
Secret: Your_Server_IP
```
```sh
Name: PORT
Secret: Your_Server_PORT
```
```sh
Name: USERNAME
Secret: Your_Server_User_Name
```
- You can get Server User Name by loging into your server via ssh then run below command
```sh
whoami
```
- Generate SSH Key for Github Action by Login into Remote Server then run below Command
```sh
Syntax:- ssh-keygen -f key_path -t ed25519 -C "your_email@example.com"
Example:- ssh-keygen -f /home/raj/.ssh/gitaction_ed25519 -t ed25519 -C "gitactionautodep"
```
- Open Newly Created Public SSH Keys then copy the key
```sh
cat ~/.ssh/gitaction_ed25519.pub
```
- Open authorized_keys File which is inside .ssh/authroized_keys then paste the copied key in a new line
```sh
cd .ssh
nano authorized_keys
```
- Open Newly Created Private SSH Keys then copy the key, we will use this key to add New Repository Secret On Github Repo
```sh
cat ~/.ssh/gitaction_ed25519
```
```sh
Name: SSHKEY
Secret: Private_SSH_KEY_Generated_On_Server
```
- Commit and Push the change to Your Github Repo
- Get Access to Remote Server via SSH
```sh
Syntax:- ssh -p PORT USERNAME@HOSTIP
Example:- ssh -p 22 raj@216.32.44.12
```
- Pull the changes from github just once this time.
```sh
cd ~/project_folder_name
git pull
```
- Your Deployment should become automate.
- On Local Machine make some changes in Your Project then Commit and Push to Github Repo It will automatically deployed on Live Server
- You can track your action from Github Actions Tab
- If you get any File Permission error in the action then you have to change file permission accordingly.
- All Done


Reload Nginx
```
nginx -s reload
```

Visit `localhost:8080` or `localhost:80` and you should see Hello from Nginx Sever on browser.
