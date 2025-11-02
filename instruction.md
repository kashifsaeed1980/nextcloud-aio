## Step 1
### Install Docker and Docker Compose
Run this command in terminal with `root` user.

    apt update && 
    apt upgrade -y &&
    curl -fsSL https://get.docker.com -o get-docker.sh &&
    sudo sh get-docker.sh &&
    curl -SL https://github.com/docker/compose/releases/download/v2.13.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose &&
    chmod +x /usr/local/bin/docker-compose &&
    apt-get install docker-compose-plugin

------------


## Step 2
## Install Nginx Proxy Manager and SSL Certificate Issue
- `mkdir npm`
- `cd npm`  

   

    # create docker-compose.yml file
    nano docker-compose.yml
    
    # paste this code
    
    services:
      app:
        image: 'jc21/nginx-proxy-manager:latest'
        restart: unless-stopped
        ports:
          - '80:80'
          - '81:81'
          - '443:443'
        volumes:
          - ./data:/data
          - ./letsencrypt:/etc/letsencrypt

 - Save this file with Press `Ctrl + X` and Press `Y` and Press `Enter`
Run Command `docker-compose up -d` and wait
   button
  - Open URL: `http://server-ip:81`
  - Default Login Detial
  Email:`admin@example.com`
  Password: `changeme`
- Follow the video instruction

------------


## Step 3
## Install Nextcloud and OnlyOffice
1. make a Nextcloud directory name `nc`
- `cd`
- `mkdir nc`
- `cd nc`

2. create `docker-compose.yml` file
`nano docker-compose.yml`

3. paste docker-compose.yml file code with press `Ctrl + A` and `Ctrl + C` and paste it in terminal with **right click** of mouse


Save this file with Press `Ctrl + X` , press `Y` and press `Enter` to save file
- Run this command `docker-compose up -d` and master container run in few minutes.
- Open URL `https://server-ip:8080`
- Follow video instructions

## Step 4
## Troubleshoot

**Error: 1** `occ maintenance:repair --include-expensive`
**Solution:**
Run Command:
`docker exec -it nextcloud-aio-nextcloud su -s /bin/bash -c 'php occ maintenance:repair --include-expensive' www-data`

**Error: 2** `Region Error`
**Solution:**
Run Command:
`sudo docker exec --user www-data -it nextcloud-aio-nextcloud php occ config:system:set default_phone_region --value=“FR”`

**Error: 3** `No SIP backend configured`
“No SIP backend configured” means that the optional telephone dial-in and dial-out feature is not set up. The SIP bridge is a separate component and is not included by default in the All-in-One installation.
Please note that this does not affect in-app communication. Users can still make voice and video calls within Nextcloud without any issues.












