# Tomcat JSP Server Template

This repository is for migrating old jsp-based sites on cafe24.

Tomcat 9 is used for javax compatibility (from 10, jakarta is used by default)


For SPARCS Academic Relations Team (by UrWrstNightmare/jihopark7777@gmail.com/night)


## How to setup

### 1. Preparation

1.1 GET the corresponding webapp directory of the server

1.2 GET the corresponding dump of the database

### 2. Setup

2.1 Clone this repository

2.2 Copy the webapp directory into the www directory

2.3 Copy the database dump into the .initdb directory (The file extension should be `.sql`)

2.4.1 Edit `docker-compose.yml`

- 2.4.1.1 Rename the db and tomcat services' names (Remember these values!)
- 2.4.1.2 In `services/db/environment` configure the database credentials. (Remember these values!)
- 2.4.1.3 Change the exposed ports of db and tomcat (Remember these values!)
- 2.4.1.4 Change the named volume's name

2.4.2 Go to `www/WEB-INF/classes/config` (JSP's compiled classes)

- 2.4.2.1 Change the database connector properties to the values configured above
  - The URL should be mapped to the db's NAME property
  - The username & password of the database should be the same as the environment variables

2.4.3 Edit `server.xml`

- 2.4.3.1 In the `<Service name="kepsi">` directive, change the secret value & name
- 2.4.3.2 Change the defaultHost, host and alias values
- 2.4.3.3 Change the Logger Valve's access log names

2.4.4 Run `sudo docker compose up -d`

2.4.5 (If you run nginx as your reverse proxy) Go to `/etc/nginx/sites-available`

- 2.4.5.1 Create the configuration file
- 2.4.5.2 Edit the server name and port number of the reverse proxy
- 2.4.5.3 Enable the service by running `sudo ln -s <origin absolute path> <destination>`
- 2.4.5.4. RUN `sudo systemctl restart nginx`

2.4.6 Configure DNS to point to your server's ip
