# Obsidian-Gitsync-Perlite

Docker container to continuously sync Obsidian markdown notes from a GitHub repository and publish it for the webs.

Official Perlite [demo here](https://perlite.secure77.de/).

![image](https://user-images.githubusercontent.com/21357789/221725827-d14001aa-0030-4b5e-b509-cf826227c5b0.png)

# Usage

````
# clone this repository
git clone https://github.com/l4rm4nd/Obsidian-Mkdocs-Gitsync
cd Obsidian-Mkdocs-Gitsync

# adjust `docker-compose.yml` to your needs:
# 1. add your to be synced GitHub repo at env variable `GIT_SYNC_REPO`
# 2. add your GitHub username at env variable `GIT_SYNC_USERNAME` - only if your repo is private
# 3. add GitHub access token at env variable `GIT_SYNC_PASSWORD` - only if your repo is private
# 4. add your GitHub repo name at env variable `HIDE_FOLDERS`

# fix permissions; may have to be run a second time after starting the container
sudo chmod -R 777 repository/
sudo chown -R 1000:1000 repository/

# start the container
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

# Links & Images

To correctly display images and links you have to adjust your Obsidian settings slightly. 

In detail, you have to enable relative path links. Please follow the instructions [here](https://github.com/secure-77/Perlite/wiki/03---Perlite-Settings#required-settings).

# Acknowledgement

Many thanks to the original devs:

- ❤️ [secure-77](https://github.com/secure-77) for [Perlite](https://github.com/secure-77/Perlite)
- ❤️ [kubernetes](https://github.com/kubernetes) for [git-sync](https://github.com/kubernetes/git-sync)

# Repo Statistics

![Alt](https://repobeats.axiom.co/api/embed/9f8de6ac8c10d682c08f9dafdf062711f182654c.svg "Repobeats analytics image")
