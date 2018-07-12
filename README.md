# A basic 5 Docker container Wordpress setup based off Alpine

This is totally experimental, but I've been running this setup on a 1GB DigitalOcean Docker Droplet with no problem, and fast.

## Setup contains:
* Nginx web server
* MariaDB server
* PHP, Wordpress, Memcached
* Nginx reverse proxy to handle all requests, inlcuding SSL
* Let's Encrypt SSL companion container

## Project contains
* Docker-Compose / Stack file
* Dockerfile
* Initial file structure with Nginx, PHP, Wordpress config files

## Deployment:
* Standup any cloud server, create user with sufficient rights
* Install Docker, initialize Swarm
* Create Wordpress destination directory
* Copy docker-compose.yml to destination directory
* Copy all files in 'initial files structure' to '<destination directory>/data'
* Go through all files (including docker-compose.yaml) and replace skillstack.io with desired domain
* Run 'docker stack deploy' (test it first with '- LETSENCRYPT_TEST=true' in the nginx web server container)
* Test in Chrome — it will complain about the invalid SSL certificate. That's ok.
* Remove '- LETSENCRYPT_TEST=true' option and deploy again -> 'docker stack deploy'
* Have fun with Wordpress

## Known issues
* Memcached not working properly yet. Couldn't find out why. Remove 'object-cache.php' from 'wp-content' directory and do not install Memcached plugin in Wordpress, it will slow down the entire system.
