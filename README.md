# Flask application
This repository aims at creating a Flask application with multiple containers, a bridge network, volumes and bind mounts.
Firstly, without using docker-compose.
And then, by using docker-compose.

## Prerequisites
Have Docker and docker compose installed on your host machine.
Install Docker depending on your OS:
- [Install Docker on Linux](https://devinci-online.brightspace.com/content/enforced/90043-MESIIN482022/Installing%20Docker%20on%20Linux.pdf?_&d2lSessionVal=G3ZDsw8zwnkzDA6EVga1ydyJu)
- [Install Docker on Windows 10/11]( https://devinci-online.brightspace.com/content/enforced/90043-MESIIN482022/Installing%20Docker%20with%20WSL2%20on%20Windows%2010%20&%2011.pdf?_&d2lSessionVal=G3ZDsw8zwnkzDA6EVga1ydyJu)
- [Install Docker on MacOS]( https://devinci-online.brightspace.com/content/enforced/90043-MESIIN482022/Installing%20Docker%20on%20macOS.pdf?_&d2lSessionVal=G3ZDsw8zwnkzDA6EVga1ydyJu)

Install docker compose:
- [Install the Compose pluging]( https://docs.docker.com/compose/install/linux/)

Then, clone this repository.
## Without docker-compose
In your local repository, run the following commands:
```bash
docker network create --driver bridge mynetwork
```
```bash
docker build -t my_flask_app .
```
```bash
docker volume create mongodb_data
```
```bash
docker run -d --network mynetwork --name mongodb -v mongodb_data:/data/db -p 27017:27017 mongo:latest
```
```bash
docker run -it --name flaskapp --network mynetwork -p 5000:5000 –-mount type=bind,source=$(pwd)/text_file.txt,target=/app/text_file.txt my_flask_app
```
Then on your web browser, visit http://localhost:5000

You should see the content of the text_file.txt file. Also, if you make any changes on the text_file.txt, you should see them by refreshing the page.
## By using docker-compose
Run:
```bash
docker-compose up
```
