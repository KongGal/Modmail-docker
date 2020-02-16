# Modmail-docker


Modmail-docker is using Docker Compose which is a tool for defining and running multi-container Docker applications. With Compose, you use a Compose file to configure your application's services. Then, using a single command, you create and start all the services from your configuration

This repo contains a .env file and a docker-compose.yml file which will be used to setup Modmail, Logviewer, Traefik and MongoDB

All support for Modmail and Logviewer should done at their repos

Modmail https://github.com/kyb3r/modmail  
Logviewer https://github.com/kyb3r/logviewer  
or on their support discord server https://discord.gg/etJNHCQ  

### Prerequisites

  - Docker
  - Docker-compose
  - Git

all 3 must be installed prior to setting up Modmail-docker
Find a guide on how to setup docker, docker-compose and GIT for your distribution 

### Quality of life
Add a alias to your .bashrc

```
$ nano ~/.bashrc
```
Add in this in the bottom
```sh
alias dc='sudo docker-compose'
```
Now reload your bash to get the new alias or close your terminal and connect again
```sh
$ exec bash
```

### Installation

Go to the directory you want modmail and logviewer to be installed in.

And git clone the this repo

```sh
$ sudo git clone https://github.com/KongGal/Modmail-docker.git .
```

Now configure the .env file to your needs by opening the file with your favourite Terminal Text Editor for this i use nano

```sh
$ nano .env
```
And fill out
```code
MODMAIL_TOKEN=
MODMAIL_GUILD_ID=
MODMAIL_OWNERS=
LOG_URL=
``` 
Next step is to create your docker network which the 4 containers will run on with 

```sh
$ sudo docker network create internet
```
Now you should have a filled out .env file and a docker network created and all there is left to do is pull the docker images
```sh
$ dc pull
```
Which will pull the latest version of
  - Modmail https://github.com/kyb3r/modmail
  - Logviewer https://github.com/kyb3r/logviewer
  - Traefik https://github.com/containous/traefik
  - MongoDB https://github.com/mongodb/mongo

Now create the docker containers from the images together with infomation from the .env file and docker-compose.yml
```sh
$ dc create
```

Run a test run to check if everything runs

```sh
$ dc up
```
And you should now see it spin up each service and the logs of it
If everthing seems to run fine then stop the docker compose
```
ctrl + C
```
Now to start all the containers in the background
```sh
$ dc start
```
Now all your containers should run in the background


### Commands

```sh
$ dc pull
```
dc pull which fetch the latest images, **before you do this you must stop your containers!**

```sh
$ dc create
```
dc create which will create your containers with the images you pulled and your settings from docker-compose.yml and .env
This most also be done everytime you change something in .env or docker-compose.yml

```sh
$ dc start
```
dc start will start all containers or a targeted container by adding its name after, modmail is used here as a example
```sh
$ dc stop
```
This will stop all containers and must be done before you do a pull or create!

```sh
$ dc logs
```
dc logs will show you the log files, if no container is specified then a merged logs of all containers can add -f to follow the logs

```sh
$ dc ps
```
dc ps is process status which will show you the status on all the containers

You can with all commands use container name to only affect that container such as
```sh
$ dc stop modmail
$ dc pull modmail
$ dc create modmail
$ dc start modmail
$ dc logs modmail
```


### How to update

Stop your containers with
```sh
$ dc stop
```
Pull latest version of images
```sh
$ dc pull
```
Rebuild containers with the new images
```sh
$ dc create
```
Start your containers again with
```sh
$ dc start
```
and your Modmail, Logviewer, Traefik, MongoDB is up to date

### Extra

If you want to run a inbox server you have to remove comment from 
```
- MODMAIL_GUILD_ID=${MODMAIL_INBOX_GUILD_ID}
```
in the docker-composer.yml on line 30

for issues or need of help with the docker-compose setup feel free to create a issue or come poke me on the modmail support discord server  
for issues or in need of Modmail or Logivewer create a issue on their repo's or contact them on their discord https://discord.gg/etJNHCQ
