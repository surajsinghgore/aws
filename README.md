
# AWS

Amazon Web Services (AWS) is a comprehensive, scalable cloud computing platform offering a wide range of services including computing power, storage, and networking capabilities.

## INSTALL UPDATES ON VPS
first update vps with latest update
Download Latest Update
```bash
sudo apt-get update
```
Download and Install latest update
```bash
sudo apt-get upgrade
```

## NGINX ON VPS
install NGINX
```bash
sudo apt install nginx
```

configure NGINX file
```bash
sudo nano /etc/nginx/sites-available/default
```
check NGINX verision
```
sudo nginx -v

```
check NGINX config
```
sudo nginx -t

```
reload NGINX config changes
```
sudo nginx -s reload

```
start NGINX
```
nginx
```


NGINX Config file
```
vim etc/nginx/nginx.conf
```

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
## INSTALL NODEJS AND NPM ON VPS
with latest version of nodejs

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```
OR with specific version

```bash
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

install nodejs on vps

```bash
sudo apt install nodejs
```
verify installation of Nodejs

```bash
node --version
```
verify installation of NPM
```bash
npm --version
```
## INSTALL NODEJS AND NPM WITh NVM ON VP
1.Step First


```bash
 curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
 ```

2.Step Second

```bash
source ~/.bashrc
 ```
3.Step Third
 ```
 nvm install --lts
 ```

## GIT ON VPS

1.Install
```bash
sudo apt install git
```
2.Clone Project 

```
sudo git clone <project-url>
```

## PM2 (Process Manager) 2

Install
```
sudo npm i pm2 -g
```
Start Command
```
pm2 start index
```

Other Commands
```
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show log stream)
pm2 flush (Clear logs)

# To make sure app starts when reboot
pm2 startup ubuntu
```


## Adding SSL CERTIFICATE WITH DOMAIN NAME with LetsEncrypt
1.Step First
```bash
sudo add-apt-repository ppa:certbot/certbot
```
2.Step Second
```bash
sudo apt-get update
```
3.Step Third
```bash
sudo apt-get install python3-certbot-nginx
```
4.Step Fourth
```bash
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```
5.Step Fifth

Only valid for 90 days, test the renewal process with
```bash
certbot renew --dry-run
```


## Setup FireWall
```bash
sudo ufw enable
sudo ufw status
sudo ufw allow ssh (Port 22)
sudo ufw allow http (Port 80)
sudo ufw allow https (Port 443)

```

##

## Deploy static website on VPS

1.Step 1 Install Latest Update of Sytem
```
sudo apt-get update
```
2.Step 2: Install NGINX
```
sudo apt install nginx
```
3.Clone your project from github to /var/www/html folder
```bash
cd /var/www/html
```
4.Paste your <project-files> into html folder with home file name index.html
```
git clone 
```
5.NOW COPY and paste the IPV4 Public address of VPS IN BROWSER

```bash
34.52.124.76
```

**Add Domains With Static Hositing**

1.Open DNS MANAGEMENT OF DOMAIN PROVIDER
| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| CNAME | @ | 34.52.124.76 |

| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| A | @ | 34.52.124.76 |

or 

__Add Sub Domains With Static Hositing__

| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| CNAME | @ | 34.52.124.76 |


##
## Deploy NODEJS APP ON VPS



1.Step 1 Install Latest Update of Sytem
```
sudo apt-get update
```


2.Step 2 Install NODEJS and NPM
```
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```
Install nodejs and npm
```
sudo apt install nodejs
```

3.Step 3 Clone Nodejs Project from github

```
git clone 
```
4.Go To Project folder

```
cd <project-folder>

```
5.Install NPM packages

```
npm install

```
6.Install PM2

```
npm install pm2 -g

```
7.Start Pm2, so that node app run even if server is closed

```
sudo pm2 start index.js

```

8.Allow the port used by the Node.js app to be publicly accessible.

for aws users
```
8.1 Go to Instance, click on create instance.

8.2 Go to Security.

8.3 Go to Security Groups.

8.4 Click on edit inbound rule,click add rule.

8.5 Allow the PORT which wanted to publicly accessible.

8.6 Save rules.

```

9.Now Cleck Node app

```
54.23.980.12:3000
```

**Add Domains With NODEJS Hositing**


| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| A | @ | 34.52.124.76 |

or 

__Add Sub Domains With NODEJS Hositing__

| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| CNAME | @ | 34.52.124.76 |


**Run NODEJS APP with NGINX**

All above steps with same with additional steps:-

10.Install nginx

```
sudo apt install nginx
```
11.Go to /etc/nginx/sites/available folder

```
cd /etc/nginx/sites-available/
```
12.Edit default nginx file
```
sudo vim default
```
13.configure the below changes

Press "i" key for inster mode 

default file
```
server{

server_name surajsingh.online www.surajsingh.online;
location /{

    proxy_pass http://localhost:3000;
       proxy_http_version 1.1;
       proxy_set_header Upgrade $http_upgrade;
       proxy_set_header Connection 'upgrade';
       proxy_set_header Host $host;
       proxy_cache_bypass $http_upgrade;
} 
}

```
Press ESC KEY + ":" +wq

reload nginx 

```
sudo nginx -s reload
```

13.Add SSL CERTIFICATE


## HOW TO HOST MULTIPLE WEBSITES ON SINGLE VPS HOSITING

1.Install Latest Update

```bash
sudo apt-get update
```

2.Install nginx
```bash
sudo apt install nginx
```

**IF YOU DON'T HAVE DOMAINS**

3.Allow Port for publicly access in case of without domain names.

| PORT |  
| :-------- | 
| 80       | 
| 90      | 
| 1000      | 

you can select any port according to you


4.Import projects in /var/www folder

```
cd /var/www
```
| PORT |  PROJECT NAME | PROJECT DOMAIN NAME |PROJECT LOCATION |
| :-------- | :-------- | :-------- |:-------- | 
| 80       | default | www.surajsingh.com | /var/www/html|
| 90      | elearning | www.shubham.com |/var/www/elearning|
| 1000      | imagesSlider | www.piyush.com|/var/www/imagesSlider|

5.Clone your projects in www directory

```
git clone 

```

**HOST 1 WEBSITE**

place your file in /var/www/html folder (default method)

```
cd /var/www/html
```

__add domain to WEBSITE 1__

go to /etc/nginx/sites-available

**If You Have DOMAIN NAME**
```
cd /etc/nginx/sites-available

```
```
sudo vim default

```

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

                root /var/www/html;

                server_name surajsingh.com www.surajsingh.com;

 location / {
        try_files $uri $uri/ =404;
        }
}
```

**If You DON'T HAVE DOMAIN NAME**

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

                root /var/www/html;

                server_name 53.45.234.56:80;

 location / {
        try_files $uri $uri/ =404;
        }
}
```

reload nginx server

```
sudo nginx -s reload
```

ADD DOMAIN NAME


| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| A | @ | 53.45.234.56 |

or 

Add Sub Domains With NODEJS Hositing

| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| CNAME | @ | 53.45.234.56 |

Add SSL CERTIFICATE

##

**HOST 2 WEBSITE** elearning

place your project in /var/www/ folder 

```
cd /var/www/
```

__add domain to WEBSITE 2__

go to /etc/nginx/sites-available


**If You Have DOMAIN NAME**
```
cd /etc/nginx/sites-available

```
create file elearning.com
```
sudo touch elearning.com
```
```
sudo vim elearning.com

```
If You Have domain name
```
server {
        listen 80 ;
        listen [::]:80;

                root /var/www/elearning;

                server_name shubham.com www.shubham.com;

 location / {
        try_files $uri $uri/ =404;
        }
}
```

**If You DON'T HAVE DOMAIN NAME**

```
server {
        listen 90;
        listen [::]:90;

                root /var/www/elearning;

                server_name 53.45.234.56:90;

 location / {
        try_files $uri $uri/ =404;
        }
}

```
copy the file elearning.com to /etc/nginx/sites-enabled folder

```
sudo ln -s elearning.com /etc/nginx/sites-enabled/
```

or 

```
sudo cp -f elearning.com /etc/nginx/sites-enabled/
```

reload nginx server

```
sudo nginx -s reload
```

ADD DOMAIN NAME


| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| A | @ | 53.45.234.56 |

or 

Add Sub Domains With NODEJS Hositing

| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| CNAME | @ | 53.45.234.56 |

Add SSL CERTIFICATE


##

**HOST 3 WEBSITE** imagesSlider

place your project in /var/www/ folder 

```
cd /var/www/
```

__add domain to WEBSITE 3__

go to /etc/nginx/sites-available


**If You Have DOMAIN NAME**
```
cd /etc/nginx/sites-available

```
create file imagesSlider.com
```
sudo touch imagesSlider.com
```
```
sudo vim imagesSlider.com

```
If You Have domain name
```
server {
        listen 80 ;
        listen [::]:80;

                root /var/www/imagesSlider;

                server_name piyush.com www.piyush.com;

 location / {
        try_files $uri $uri/ =404;
        }
}
```

**If You DON'T HAVE DOMAIN NAME**

```
server {
        listen 1000;
        listen [::]:1000;

                root /var/www/imagesSlider;

                server_name 53.45.234.56:1000;

 location / {
        try_files $uri $uri/ =404;
        }
}
```
copy the file imagesSlider.com to /etc/nginx/sites-enabled folder

```
sudo ln -s imagesSlider.com /etc/nginx/sites-enabled/
```

or 

```
sudo cp -f imagesSlider.com /etc/nginx/sites-enabled/
```
reload nginx server

```
sudo nginx -s reload
```

ADD DOMAIN NAME


| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| A | @ | 53.45.234.56 |

or 

Add Sub Domains With NODEJS Hositing

| TYPE | NAME     | POINT TO                |
| :-------- | :------- | :------------------------- |
| CNAME | @ | 53.45.234.56 |

Add SSL CERTIFICATE

now website will live on

without domain

```
default
53.45.234.56

elearning
53.45.234.56:90

imagesSlider
53.45.234.56:1000
```


with domain

```
default
https://www.surajsingh.com

elearning
https://www.shubham.com

imagesSlider
https://www.piyush.com
```

subdomain will live on 

```
default
http://surajsingh.com

elearning
http://shubham.com

imagesSlider
http://piyush.com
```




## SET ENVIRONMENT VARIABLES ON VPS
 temporary way

```bash
export key=value

```
or

permanent way

step 1 (go to root folder)
```
cd /
```
step 2 (create .bash_profile file)
```
sudo vim .bash_profile
```
step 3 : (insert environment variables inside .bash_profile file)
```
export key1="value"
export key2="value"
```
step 4 (reload file)

```
source .bash_profile
```




##
## Deploy REACT APP ON VPS

Way 1 (using static build)


1.Install latest version in vps
```
sudo apt-get update
```
2.Install NGINX
```
sudo apt install nginx
```

3.Clone react project in /var/www/html folder
```
cd /var/www/html
```
```
git clone <react-project>
```

4.Install NodeJs and NPM

```
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```
```
sudo apt install nodejs
```



5.Go inside react project folder and install npm packages

```
cd <project-folder>
```
```
sudo npm install
```

6.After packages install , build react app
```
sudo npm run build
```

7.After successful build extract all files from build folder to /var/www/html folder

```
cd build

```
```
sudo mv allfiles /var/www/html
```

NOW YOU CAN ADD DOMAIN NAME BY configure **/etc/nginx/sites-available/default** filer
```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

                root /var/www/html;

                server_name surajsingh.com www.surajsingh.com;

 location / {
        try_files $uri $uri/ =404;
        }
}

```
reload nginx 

```
sudo nginx -s reload
```

##
2 SECOND WAY 


1.Install latest version in vps
```
sudo apt-get update
```
2.Install NGINX
```
sudo apt install nginx
```

3.Clone react project in any folder

```
git clone <react-project>
```

4.Install NodeJs and NPM

```
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```
```
sudo apt install nodejs
```



5.Go inside react project folder and install npm packages

```
cd <project-folder>
```
```
sudo npm install
```

6.Run REACT APP
```
npm start
```

7.Allow PORT 3000 publicly

8.You can see react website on IPV4
```
54.23.567.35:3000
```

9.Install Pm2
```
npm i pm2 -g
```
10.Start pm2 to start react app

```
sudo pm2 start npm --name "reactApp" -- start
```

or step 10 replace with

serving react with serve

```
npm run build
```
```
sudo pm2 serve build/ 3000 --name "reactApp" -- spa
```

NOW YOU CAN ADD DOMAIN NAME BY configure **/etc/nginx/sites-available/default** filer
```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

                root /var/www/html;

                server_name surajsingh.com www.surajsingh.com;

 location / {
         proxy_pass http://localhost:3000;
        try_files $uri $uri/ =404;
        }
}

```
reload nginx 

```
sudo nginx -s reload
```



##
## Deploy NEXTJS APP ON VPS


1.Install latest version in vps
```
sudo apt-get update
```
2.Install NGINX
```
sudo apt install nginx
```

3.Clone nextjs project in any folder

```
git clone <nextjs-project>
```

4.Install NodeJs and NPM

```
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```
```
sudo apt install nodejs
```



5.Go inside nextjs project folder and install npm packages

```
cd <project-folder>
```

```
npm install

```

6.Build NEXTJS app

```
npm run build
```

7.We need to pass 3000 request to 80

8.Go to /etc/nginx/sites-available/ folder and create file nextjsapp
```
cd /etc/nginx/sites-available/
```
```
sudo touch nextjsapp 
```
```
sudo vim nextjsapp
```
```
server{
    listen 80;
    listen [::]:80;
    server_name surajsingh.online www.surajsingh.online;
    #or if you not have domain name
    server_name 56.23.945.34:3000;

    location / {
       proxy_pass http://localhost:3000;
       proxy_http_version 1.1;
       proxy_set_header Upgrade $http_upgrade;
       proxy_set_header Connection 'upgrade';
       proxy_set_header Host $host;
       proxy_cache_bypass $http_upgrade;
    }
}
```

copy this file to /etc/nginx/sites-enabled folder
```
sudo ln -s nextjs /etc/nginx/sites-enabled/
```
or 
```
sudo cp -f nextjs /etc/nginx/sites-enabled/

```
reload nginx server
```
sudo nginx -s reload
```

9.Now Install PM2 
```
sudo npm i pm2 -g
```
10.Now Serve Build File of Nextjs App 
```
sudo pm2 start npm --name "NextjsApp" --start
```
 or step 10 is replace with following steps:-

 1.create ecosystem.config.js file in project root folder

 ```
 cd <project-folder>
 ```
 ```
 sudo touch ecosystem.config.js
 ```
2.add below content inside ecosystem.config.js file
```
module.exports = {
  apps : [{
    name   : "Nextjs App",
    script : "sudo npm start",
     #port: 3001
  }]
}
```
3.Now Run ecosystem.config.js file with pm2

```
sudo pm2 start ecosystem.config.js
```
other pm2 commands
```
sudo pm2 stop ecosystem.config.js
sudo pm2 restart ecosystem.config.js
sudo pm2 reload ecosystem.config.js
sudo pm2 delete ecosystem.config.js
sudo pm2 start ecosystem.config.js
```


## default NGINX file content
```
##
# You should look at the following URL's in order to grasp a solid understanding
# of Nginx configuration files in order to fully unleash the power of Nginx.
# https://www.nginx.com/resources/wiki/start/
# https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/
# https://wiki.debian.org/Nginx/DirectoryStructure
#
# In most cases, administrators will remove this file from sites-enabled/ and
# leave it as reference inside of sites-available where it will continue to be
# updated by the nginx packaging team.
#
# This file will automatically load configuration files provided by other
# applications, such as Drupal or Wordpress. These applications will be made
# available underneath a path with that package name, such as /drupal8.
#
# Please see /usr/share/doc/nginx-doc/examples/ for more detailed examples.
##

# Default server configuration
#
server {
        listen 3000;
        listen [::]:3000;

        # SSL configuration
        #
        # listen 443 ssl default_server;
        # listen [::]:443 ssl default_server;
        #
        # Note: You should disable gzip for SSL traffic.
        # See: https://bugs.debian.org/773332
        #
        # Read up on ssl_ciphers to ensure a secure configuration.
        # See: https://bugs.debian.org/765782
        #
        # Self signed certs generated by the ssl-cert package
        # Don't use them in a production server!
        #
        # include snippets/snakeoil.conf;

        root /var/www/test2;

        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html;

        server_name 54.242.75.61:3000;

 location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }

        # pass PHP scripts to FastCGI server
        #
        #location ~ \.php$ {
   #       include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
        #       fastcgi_pass unix:/run/php/php7.4-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #       deny all;
        #}
}


# Virtual Host configuration for example.com
#
# You can move that to a different file under sites-available/ and symlink that
# to sites-enabled/ to enable it.
#
#server {
#       listen 80;
#       listen [::]:80;
#
#       server_name example.com;
#
#       root /var/www/example.com;
#       index index.html;
#
#       location / {
#               try_files $uri $uri/ =404;
#       }
#}

```

## HOST NODEJS AND REACT ON SAME SERVER
1.Go Inside React Client and build the project
```
cd <reac-project>
```
```
npm run build
```

2.Go Back to backend and start the server
```
cd ..
```
nodejs/index.js
```
npm i cors;
```

```
const cors = require("cors");
const path=require('path');
```
```
const buildpath=path.join(__dirname,"../client/build");
app.use(express.static(buildpath));

app.use(cors({"origin":"*"}));
```
```
node index.js
```
## Connect Domain or Sub Domain With VPS HOSITING
**CONNECT DOMAINS**

1.ADD **A** RECORD
![App Screenshot](https://res.cloudinary.com/dnxv21hr0/image/upload/v1712720046/aws/udbfaa8bjroor0lcnkwo.png)
![App Screenshot](https://res.cloudinary.com/dnxv21hr0/image/upload/v1712720031/aws/cpfe76ixo6vxe2alxudf.png)


2.ADD **CNAME** RECORD
![App Screenshot](https://res.cloudinary.com/dnxv21hr0/image/upload/v1712720047/aws/uuoionmjexhdvd4aihzt.png)
![App Screenshot](https://res.cloudinary.com/dnxv21hr0/image/upload/v1712720047/aws/ptddpphfcp1oljlxvoiq.png)

**CREATE AND CONNECT SUB DOMAINS FROM SINGLE DOMAIN**
![App Screenshot](https://res.cloudinary.com/dnxv21hr0/image/upload/v1712718795/aws/ypytlmscoquilekx14wb.png)

OR 

![App Screenshot](https://res.cloudinary.com/dnxv21hr0/image/upload/v1712718794/aws/zdxcyleu2vfgxkomh3zo.png)

