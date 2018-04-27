# LEMP-DOCKER
Linux - NGINX - Mysql - PHP7 for development environment

# This is for what?
I saw many docker newbies asking me about how to build a stack for development using docker. 
Today i will answer that question with a demo project. Check it out

# Software specs:
   - Docker 18.03.0-ce, build 0520e24
   - Docker-compose 1.8.0
   - Slim 3.6.1
   - Composer 1.6.4
# Instructions:
1. Install Docker:
   - Ubuntu 16.04 (64 bits): https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#os-requirements
   
   Install Docker Compose:
   - Ubuntu 16.04 (64 bits): https://docs.docker.com/compose/install/
   
2. Clone this public repository:
   `https://github.com/crazyfree/LEMP-docker`

3. Clone into www/html folder
   `git clone <repo url> ./www/html/app`

4. Execute the following commands
   -To execute the docker-compose file: `docker-compose up -d`

5. At this point, the containers should be running, check them with: `docker ps -a` 

6. Open browser and type `localhost` you should see the running project on screen
   NOTE: If you got an error go below to FILE PERMISSIONS (over Ubuntu)

7. Phpmyadmin available at `localhost:8080`

## Error Handle: 
1. If port 80 is occupied by another process when running docker-compose up it will return error port is already used. Because the nginx is config using port 80. Then you can decide either free the port 80 or change the docker config so nginx will use another port.
    - To change nginx config by editing docker-compose.yml file, on nginx section change ports from 80:80 to port_you_want_to_use:80 (example 8888:80)

## File Permissions:
1. If you are using docker over Windows -> You'll not have any error (from step 1 through 8)
2. If you are using docker over linux -> It's probably that on STEP 7 you got an error (PERMISSION ERROR)
   - DEVELOPMENT: For "testing" purposes go at the level of **myappname** and execute: `sudo chmod -R 777` (***Warning*** :exclamation: : Security issues)
   - PRODUCTION: To fix the permission's issues, follow instructions of: [Docker & File Permissions](https://serversforhackers.com/c/dckr-file-permissions)   
        - NOTE 1: For the "PHP container", if you get an error trying to go inside the container using "bash", then, try with "/bin/bash" or "sh"
        - :key: NOTE 2: If don't want to review the Video, you can try the following: Go at the level of **app** and execute: `sudo chown -R 82:docker myappname/` (If this do not work, then try the video)

## Composer Installation:
`sudo at-get install composer`

   - Error: "mbstring not found". To Fix try: `sudo apt-get install php7.0-mbstring`
   
   ![mbstring](https://user-images.githubusercontent.com/17578664/34341464-dc0f2668-e976-11e7-9516-40057a267569.jpg)
   
   - Error: "dom not found". to fix try: `sudo apt-get install php7.0-xml` and then `sudo apt-get install zip unzip php7.0-zip`
   
   ![dom](https://user-images.githubusercontent.com/17578664/34341576-e40af570-e978-11e7-8799-9b60a7dc9eac.jpg)

## Docker usefull commands:
If you are using Ubuntu 16.04, you need to add `sudo` at the begining of all the **docker** commands:

- To list all containers: `docker ps -a`
- To stop all containers: `docker stop $(docker ps -a -q)`
  - Ubuntu example: `sudo docker stop $(sudo docker ps -a -q)`
- To remove all containers: `docker rm $(docker ps -a -q)`
- To remove all images of the disk (force to remove). ***Warning*** :exclamation: : `docker rmi -f $(docker images -q)`
- To go inside the container: `docker exec -it <name-of-the-container> bash`

