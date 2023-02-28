# Obsidian-Gitsync-Perlite

Docker container to continuously sync Obsidian markdown notes from a GitHub repository and publish it for the webs.

![image](https://user-images.githubusercontent.com/21357789/221725827-d14001aa-0030-4b5e-b509-cf826227c5b0.png)

# Usage

````
# clone this repository
git clone https://github.com/l4rm4nd/Obsidian-Mkdocs-Gitsync
cd Obsidian-Mkdocs-Gitsync

# change variables in compose file
# add GitHub username
# add GitHub access token
# add your GitHub repo to sync
# add your repo name to HIDE_FOLDERS
nano docker-compose.yml

# fix permissions
sudo chmod -R 777 repository/
sudo chown -R 1000:1000 repository/

# start the container
docker network create proxy
docker compose up -d
````

Then browse http://127.0.0.1:8888 to inspect your markdown notes. May combine with a reverse proxy such as Traefik and publish securely to the interwebs. Enjoy!

# Customization

If you want to change the default notes path/name `Demo`, you also have to adjust the volume mappings for the perlite service too. So if your to be synced GitHub repo is called `Obsidian_Notes`, adjust the compose file's service Perlite as follows:

````
services:
  perlite:
    image: sec77/perlite:latest
    container_name: perlite
    restart: unless-stopped
    environment:
      - NOTES_PATH=Obsidian_Notes # <-- adjusted with custom repo name
      - HIDE_FOLDERS=docs,private,trash
      - LINE_BREAKS=true
    volumes:
      - ./repository/root:/var/www/perlite/Obsidian_Notes:ro # <-- adjusted with custom repo name
````

If you want to adjust the website's title, please adjust the `index.php` file that is bind mounted into the Perlite container. The following line is relevant:

````
12   $title = 'Obsidian-Gitsync-Perlite';
````

# Acknowledgement

Many thanks to the following people:

- ❤️ [secure-77](https://github.com/secure-77) for [Perlite](https://github.com/secure-77/Perlite)
- ❤️ [kubernetes](https://github.com/kubernetes) for [git-sync](https://github.com/kubernetes/git-sync)
