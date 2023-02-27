# Obsidian-Gitsync-Perlite

Docker container to continously sync Obsidian markdown notes from a GitHub repository and publish it for the webs.

# Usage

````
# clone this repository
git clone https://github.com/l4rm4nd/Obsidian-Mkdocs-Gitsync
cd Obsidian-Mkdocs-Gitsync

# change variables in compose file
# add GitHub username
# add GitHub access token
# add your GitHub repo to sync
nano docker-compose.yml

# fix permissions
sudo chmod -R 777 repository/
sudo chown -R 1000:1000 repository/

# start the container
docker compose up -d

# Web service available at http://127.0.0.1:8888
# May combine with a reverse proxy such as Traefik
````

# Acknowledgement

Many thanks to the following people:

- ❤️ [secure-77](https://github.com/secure-77) for [Perlite](https://github.com/secure-77/Perlite)
- ❤️ [kubernetes](https://github.com/kubernetes) for [git-sync](https://github.com/kubernetes/git-sync)
